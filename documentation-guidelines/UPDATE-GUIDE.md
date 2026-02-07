---
audience: help
title: "AI Agent Guide: Updating Documentation"
sidebarTitle: "Update Guide"
description: "How to update existing BeatPass documentation accurately and efficiently."
---

# AI Agent Guide: Updating Documentation

**When to update:** Feature changes, UI redesigns, pricing changes, error corrections, or outdated information.

---

## Update Decision Tree

### When to Update vs. Rewrite

| Situation | Action | Reason |
|-----------|--------|--------|
| Minor UI text change | Update | Single element changed |
| New feature in existing area | Update | Add new section |
| Navigation path change | Update | Fix paths, keep content |
| Feature removed | Update | Remove section, add notice |
| Major redesign | Rewrite | Structure no longer fits |
| Multiple errors found | Rewrite | Foundation is wrong |
| Documentation for non-existent feature | Delete | Never should have existed |

### Pre-Update Checklist

Before modifying any existing documentation:

1. [ ] Read the current documentation file completely
2. [ ] Identify all claims and instructions in the doc
3. [ ] List what needs verification
4. [ ] Run verification commands
5. [ ] Mark outdated vs. still-accurate content
6. [ ] Plan minimal necessary changes

---

## The Update Process

### Step 1: Read and Analyze Current Doc

**What to identify:**
- Navigation instructions (likely to need updates)
- UI element references (check if labels changed)
- Database-dependent claims (verify still accurate)
- Screenshots (may need refresh)
- Related links (verify still valid)

**Example Analysis:**
```markdown
Current doc says:
- "Go to Settings → Subscription" [CHECK: verify actual path]
- "Click **Cancel Subscription**" [CHECK: verify button text]
- "Plans start at $19/month" [CHECK: query database]
- "MP3 uploads accepted" [CHECK: verify blocked_extensions]
```

### Step 2: Verify Current State

Run the same verification as for new documentation:

```bash
# If doc mentions menu items
php artisan tinker --execute="$menus = json_decode(\DB::table('settings')->where('name', 'menus')->first()->value, true); foreach($menus as $menu) { if (in_array('auth-dropdown', $menu['positions'] ?? [])) { foreach($menu['items'] as $item) { echo $item['label'] . ' → ' . $item['action'] . PHP_EOL; } } }"

# If doc mentions pricing
php artisan tinker --execute="echo json_encode(\DB::table('products')->get(['name', 'free'])->toArray());"
php artisan tinker --execute="echo json_encode(\DB::table('prices')->get(['product_id', 'amount', 'interval'])->toArray());"

# If doc mentions specific features
grep -r "featureName" resources/client/ --include="*.tsx"
```

### Step 3: Identify Changes Needed

Compare current doc vs. verified reality:

| Current Doc Says | Verified Reality | Action |
|------------------|------------------|--------|
| "Settings → Subscription" | "Profile avatar → Billing" | Update navigation |
| "Cancel Subscription" | "Cancel plan" | Update button text |
| "$19/month Classic" | "$29/month Classic" | Update pricing |
| "MP3 uploads" | MP3 blocked | Remove/correct |
| Feature X exists | Feature X removed | Remove section |
| Inline "Need Help?" section | Snippet exists | Replace with `<NeedHelp />` |
| Inline platform fee callout | Snippet exists | Replace with `<PlatformFee />` |
| Hardcoded `contact@beatpass.ca` | Snippet exists | Replace with `<SupportContact />` |

### Step 4: Make Minimal Targeted Changes

**Principles:**
- Change only what's wrong
- Preserve correct content
- Maintain existing tone and style
- Keep structure if possible

**Example Update:**

```diff
- Go to **Settings** → **Subscription**.
+ Click your **profile avatar**, then select **Billing**.

- Click **Cancel Subscription**.
+ Click **Cancel plan**.

- The Classic plan costs $19/month.
+ The Classic plan costs $29/month (CAD).
```

### Step 5: Add Update Context (Optional)

For significant changes, consider adding a note:

```mdx
<Info>
  Updated February 2026: Navigation changed from "Settings → Subscription" to "Profile avatar → Billing".
</Info>
```

**When to add context notes:**
- Navigation paths changed significantly
- Feature location moved
- Process steps reordered
- NOT needed for: typo fixes, minor wording improvements

---

## Special Update Scenarios

### Scenario 1: Feature Removed/Deprecated

**Approach:**
1. Add deprecation notice at top
2. Explain what replaced it (if anything)
3. Keep doc for reference but mark obsolete
4. Update related docs that linked to it

**Example:**
```mdx
---
audience: help
title: "Old Feature Name"
description: "This feature has been removed as of March 2026."
---

<Warning>
  **Removed in March 2026**: This feature is no longer available. 
  Use [New Feature](/help/path) instead.
</Warning>

# Old Feature Name

[Keep content for reference, but note it's obsolete]
```

### Scenario 2: Major UI Redesign

**Approach:**
1. Verify new UI completely
2. Rewrite navigation instructions
3. Update all UI references
4. Check if screenshots need refresh (flag for human)
5. Test mental walkthrough of instructions

**Common pitfalls:**
- Keeping old navigation paths that no longer exist
- Missing new buttons/sections that need documentation
- Not verifying that old features still work the same way

### Scenario 3: Pricing/Plan Changes

**Approach:**
1. Query database for current pricing
2. Update all price mentions
3. Update plan names if changed
4. Check for "starting at" claims
5. Verify billing intervals
6. Update ALL docs mentioning pricing (search first)

**Critical:** Pricing appears in many docs. Use search:
```bash
grep -r "\$29\|Classic\|monthly" Documentation/help/ --include="*.mdx"
```

### Scenario 4: Snippet Migration

**When updating a page that has inline content matching an existing snippet:**

**Approach:**
1. Identify inline content that duplicates a snippet ("Need Help?" sections, platform fee callouts, API warnings, support contact info)
2. Add the snippet import after frontmatter
3. Replace the inline content with the snippet component
4. Verify the page still reads naturally with the snippet in place

**Example:**
```diff
  ---
  title: "Page Title"
  ---
+ 
+ import NeedHelp from "/snippets/sections/need-help.mdx";
  
  [page content...]
  
- ## Need Help?
- 
- If you have questions, contact the support team at **contact@beatpass.ca**.
+ <NeedHelp />
```

**When to migrate:**
- During any update to a page that has inline snippet-eligible content
- When fixing contact email or fee amounts across multiple pages
- When standardizing support sections across a documentation area

**Available snippets to check for:**
- `NeedHelp` / `StillNeedHelp` — support footer sections
- `SupportContact` — inline support contact line
- `PlatformFee` / `PlatformFeeNote` — platform fee callouts
- `SubscriptionRequired` — paid plan notices
- `StripeConnectRequired` — Stripe setup warnings
- `ApiInviteOnly` — API access warnings
- `ProducerOnly` — producer privilege notices

### Scenario 5: Error Correction

**When user reports error:**
1. Verify the reported error is real
2. Find all instances of the error (may be in multiple docs)
3. Correct all occurrences
4. Check if error originated from missing verification

**Common errors to watch for:**
- Wrong navigation paths
- Incorrect button names
- Wrong pricing
- Features that don't exist
- Wrong upload formats
- Incorrect permission names

---

## Maintaining Consistency During Updates

### Maintaining Non-Technical Tone

When updating documentation, preserve (or improve) the non-technical, user-friendly tone:

**Keep it user-focused:**
- ❌ "We've implemented a new webhook handler"
- ✅ "You'll now receive instant notifications"

**Avoid technical explanations:**
- ❌ "The database query was optimized"
- ✅ "Pages load faster now"

**Don't add technical debt:**
- If a technical explanation sneaks in during an update, remove it
- If updating a doc that has technical content, simplify it
- Reference `/developers/` docs for technical details

**Release Note Updates Must Stay Non-Technical:**
Even when updating release notes for technical fixes:
- ❌ "Fixed the `payment_intent` webhook handler"
- ✅ "Fixed an issue where some payments weren't processing correctly"

**Check for Technical Creep:**
After updating, verify no new technical jargon was added.

### Cross-References

When updating:
1. Check if other docs link to this one (may need updates)
2. Verify linked docs are still relevant
3. Update link text if page title changed
4. Add links to new related docs

**Find what links to a page:**
```bash
grep -r "/help/current-page-path" Documentation/help/ --include="*.mdx"
```

### Frontmatter Preservation

Keep existing frontmatter unless:
- Title is wrong (update it)
- Audience changed (update it)
- Description is misleading (update it)

Never remove frontmatter fields unless instructed.

---

## Post-Update Verification

### Self-Review Checklist

- [ ] Updated content verified against current codebase
- [ ] Navigation paths tested mentally
- [ ] UI labels match actual interface
- [ ] No new technical jargon introduced
- [ ] Links still work (root-relative paths)
- [ ] Tone matches existing documentation
- [ ] Related docs checked for needed updates
- [ ] No accidental content deletion
- [ ] **Snippet opportunities identified** — inline content replaced with snippet imports where applicable
- [ ] **Existing snippet imports still valid** — paths and component names correct
- [ ] **No new inline duplication** — updated content doesn't duplicate existing snippets

### Diff Review

Before finalizing, review what changed:

```diff
- Go to **Settings**.
+ Click your **profile avatar**.
```

Ask:
- Is this change necessary? Yes
- Is the new text accurate? Verified
- Did I change anything else by accident? Review full diff

---

## Common Update Mistakes

### ❌ Don't Do This

1. **Update without verifying**
   - Wrong: Changing "Cancel Subscription" to "Cancel Plan" without checking
   - Fix: Always verify the current button text first

2. **Partial updates**
   - Wrong: Updating navigation in one place but missing other references
   - Fix: Search for all instances of old path/text

3. **Assuming old structure still works**
   - Wrong: Keeping old section organization after major redesign
   - Fix: Verify the entire user flow, not just one step

4. **Breaking consistency**
   - Wrong: Adding highly technical language to a simple user guide
   - Fix: Match existing tone and complexity

5. **Forgetting related docs**
   - Wrong: Updating billing page but not updating billing FAQ
   - Fix: Search for all docs mentioning the changed feature

6. **Removing too much**
   - Wrong: Deleting entire sections when only one sentence is wrong
   - Fix: Make surgical changes, preserve good content

7. **Not migrating to snippets**
   - Wrong: Updating inline "Need Help?" text without converting to snippet
   - Fix: Replace with `<NeedHelp />` import during the update
   - Opportunistically migrate inline content to snippets during any update

8. **Breaking snippet imports**
   - Wrong: Removing or renaming snippet imports during an update
   - Fix: Verify all import statements still reference correct paths

---

## Update Workflow Summary

```text
1. READ current documentation
2. LIST all claims/instructions
3. VERIFY each against codebase
4. IDENTIFY what needs changing
5. CHECK for snippet migration opportunities (inline content → snippet imports)
6. MAKE minimal targeted changes (including snippet imports)
7. CHECK related docs
8. SELF-REVIEW changes (including snippet usage)
9. SUBMIT update
```

---

## Emergency Updates

For urgent fixes (wrong pricing, broken instructions):

1. **Verify the error** — Confirm it's actually wrong
2. **Fix immediately** — Don't wait for full review
3. **Keep change minimal** — Fix only what's broken
4. **Document what changed** — Note in commit/message
5. **Follow up** — Check if other docs have same error

---

<Info>
  **Remember**: Updates are just as important as new documentation. 
  Outdated documentation is often worse than no documentation because it damages user trust.
</Info>

---

## Related Resources

- [Documentation Standards](/help/release-notes/_meta/DOCUMENTATION-STANDARDS) — Universal standards
- [New Doc Guide](/help/release-notes/_meta/NEW-DOC-GUIDE) — Creating new docs
- [AI Agent Guide](/help/release-notes/_meta/AI-AGENT-GUIDE) — Main entry point
- [Verification Standards](/help/release-notes/_meta/VERIFICATION) — Detailed verification
- [Mintlify Reference](/help/release-notes/_meta/MINTLIFY-REFERENCE) — Component usage
