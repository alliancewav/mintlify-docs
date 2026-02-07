---
audience: help
title: "Quick Reference"
sidebarTitle: "Quick Reference"
description: "One-page reference for writing release notes."
---

# Release Notes Quick Reference

Everything you need at a glance.

---

## File Naming

Individual release note pages use **version-based naming**:

```
release-notes/v3.0/{version}.mdx

Examples:
✅ release-notes/v3.0/3.0.8-26.mdx
✅ release-notes/v3.0/3.0.9.mdx
❌ release-notes/v3.0/update.mdx (too vague)
❌ release-notes/2026-02-10-playlist.mdx (wrong format)
```

---

## Release Notes Structure

BeatPass uses a **two-part system**: individual pages + unified changelog.

```
release-notes/
├── index.mdx                      # Landing page
├── changelog.mdx                  # Unified changelog (Update components + RSS)
├── v3.0/                          # Current version
│   ├── index.mdx                  # v3.0 overview
│   ├── 3.0.8-25.mdx              # Individual release pages
│   ├── 3.0.8-24.mdx
│   └── ...
└── v2.x/                          # Legacy version
    ├── index.mdx
    └── ...
```

**For every release, you must:**
1. Create individual page in `release-notes/v3.0/`
2. Add `Update` entry at **top** of `release-notes/changelog.mdx`
3. Update `docs.json` navigation (correct month group)

---

## Frontmatter Template (Individual Page)

```yaml
---
title: "Brief Title"
date: "YYYY-MM-DD"
severity: "minor"                   # major|minor|patch|hotfix
audience: "All"                     # All|Producers|Developers
tags: ["feature"]                   # See taxonomy
components: ["dashboard"]           # See taxonomy
---
```

## Changelog Entry Template

```mdx
<Update label="{Month Day, Year}" description="v{version}" tags={["{Tag1}", "{Tag2}"]}>
  ## {Title}

  {1-2 sentence summary.}

  - **{Key change 1}** — Brief description
  - **{Key change 2}** — Brief description

  [Read full release notes →](/release-notes/v3.0/{version})
</Update>
```

---

## Tag Quick Pick

### Individual Page Tags (lowercase)

| If you... | Use Tag |
|-----------|--------|
| Added something new | `feature` + component |
| Made something better | `improvement` |
| Fixed something broken | `bugfix` |
| Fixed a security issue | `security` |
| Made it faster | `performance` |
| Removed something | `deprecation` |

### Changelog Update Tags (Title Case)

| If you... | Use Tag |
|-----------|--------|
| Added something new | `Feature` |
| Fixed something broken | `Bug Fix` |
| Fixed a security issue | `Security` |
| Made it faster | `Performance` |
| Changed UI/visuals | `UI/UX` |
| Changed billing/pricing | `Billing` |
| Producer-specific change | `Producer` |
| Mobile improvement | `Mobile` |
| Major platform change | `Platform` |
| API change | `API` |

---

## Audience Quick Pick

| Who's affected? | Audience |
|-----------------|----------|
| Everyone | `All` |
| Only producers | `Producers` |
| Only listeners | `Listeners` |
| Admin tools | `Admins` |
| API/dev changes | `Developers` |

---

## Icon Quick Pick (Font Awesome 6 ONLY)

> **All icons must be valid FA6 names.** Verify at [fontawesome.com/icons](https://fontawesome.com/icons). Never use Lucide names.

| For | Use Icon (FA6) |
|-----|----------|
| Major release | `rocket` + green |
| Feature | `star` + amber |
| Improvement | `bolt` + blue |
| Bug fix | `wrench` + gray |
| Security | `shield` + red |
| Hotfix | `circle-exclamation` + red |
| Producer feature | `music` |
| Analytics | `chart-bar` |
| Billing | `credit-card` |
| Mobile | `mobile-screen-button` |
| Legal | `scale-balanced` |
| Upload | `cloud-arrow-up` |

---

## Common Phrases

### For New Features
- "New [feature name] for [audience]"
- "You can now [capability]"
- "Introducing [feature]: [one-line description]"

### For Improvements
- "[X]% faster [area]"
- "Improved [feature] with [benefit]"
- "Better [experience] through [change]"

### For Bug Fixes
- "Fixed [issue] that caused [problem]"
- "Resolved [error] in [area]"
- "Corrected [behavior] to [expected behavior]"

### For Security
- "Addressed [vulnerability type] in [area]"
- "Security update for [component]"
- "Fixed [issue] (no user action required)"

---

## UI Reference Patterns

```markdown
Click your **profile avatar** → **Billing**
Navigate to **Producer Dashboard** → **Analytics**
Select **Change plan** from the **Current Plan** section
Toggle the **Enable notifications** switch
```

---

## Snippet Quick Reference

Reusable snippets live in `/snippets/`. Import after frontmatter, use as JSX components.

### Common Snippet Imports

| Need | Import | Use |
|------|--------|-----|
| Platform fee callout | `import PlatformFee from "/snippets/callouts/platform-fee.mdx";` | `<PlatformFee />` |
| "Need Help?" footer | `import NeedHelp from "/snippets/sections/need-help.mdx";` | `<NeedHelp />` |
| "Still Need Help?" | `import StillNeedHelp from "/snippets/sections/still-need-help.mdx";` | `<StillNeedHelp />` |
| Support contact line | `import SupportContact from "/snippets/sections/support-contact.mdx";` | `<SupportContact />` |
| Subscription required | `import SubscriptionRequired from "/snippets/callouts/subscription-required.mdx";` | `<SubscriptionRequired />` |
| API invite-only | `import ApiInviteOnly from "/snippets/warnings/api-invite-only.mdx";` | `<ApiInviteOnly />` |
| Producer-only feature | `import ProducerOnly from "/snippets/warnings/producer-only.mdx";` | `<ProducerOnly />` |
| Plan comparison table | `import PlanComparisonTable from "/snippets/data/plan-comparison-table.mdx";` | `<PlanComparisonTable />` |

### Snippet Rules

- **Always use snippets** for repeated content — never duplicate inline
- **Absolute paths** — `/snippets/...` not `../snippets/...`
- **PascalCase names** — `PlatformFee` not `platformFee` or `platform-fee`
- **After frontmatter** — imports go between `---` and first content line
- **Full reference** — See [Mintlify Reference — Reusable Snippets](/documentation-guidelines/MINTLIFY-REFERENCE#reusable-snippets)

---

## Section Checklist

### Individual Release Note Page
- [ ] **Title**: 3-7 words, descriptive
- [ ] **Summary**: 2-3 sentences, benefit-focused
- [ ] **What's New**: 3-7 bullets, outcome-first
- [ ] **Why It Matters**: 2-4 bullets, user value
- [ ] **How to Use**: 3-5 steps (if applicable)
- [ ] **Migration**: Breaking changes (if any)
- [ ] **Related**: Links to docs (if applicable)

### Changelog Update Entry
- [ ] **Label**: `"Month Day, Year"` format
- [ ] **Description**: `"v{version}"` format
- [ ] **Tags**: 1-3 Title Case tags from approved set
- [ ] **Heading**: `## Title` inside the Update
- [ ] **Summary**: 1-2 sentences
- [ ] **Bullets**: 3-5 with `**Bold** — description` format
- [ ] **Link**: `[Read full release notes →](/release-notes/v3.0/{version})`

---

## Quick Validation

Before finishing, check:

1. **User-facing?** No internal code names
2. **Actionable?** Users know what to do
3. **Benefit clear?** Why they should care
4. **Accurate?** No broken links, correct dates
5. **Consistent?** Follows style guide
6. **Complete?** Both individual page AND changelog entry
7. **Sized right?** Individual: 200-600 words, Changelog entry: 50-100 words
8. **Icons valid?** All FA6 names (not Lucide)
9. **Links correct?** Doc paths for docs, full URLs for app pages
10. **Colors WCAG?** Run `mint a11y` if colors changed
11. **docs.json updated?** New page added to correct month group
12. **RSS clean?** Add `rss` prop if entry has components/HTML
13. **Tooltips used?** Domain jargon and technical terms have `<Tooltip>` on first occurrence
14. **Snippets used?** Repeated content uses imports from `/snippets/`

---

## Word Count Targets

| Section | Target |
|---------|--------|
| Summary | 25-50 words |
| What's New | 50-100 words |
| Why It Matters | 30-75 words |
| How to Use | 50-100 words (if applicable) |
| **Total** | **200-400 words** |

---

## Common Mistakes to Avoid

❌ "We updated..." → ✅ "New..." / "Updated..."
❌ "Bug fixed" → ✅ "Fixed [specific issue]"
❌ "Feature added" → ✅ "New [feature name]"
❌ "Improved performance" → ✅ "50% faster [area]"
❌ "Settings → Billing" → ✅ "**profile avatar** → **Billing**"

---

## Emergency Contacts

Questions about release notes?
- Documentation team: docs@beatpass.ca
- Slack: #docs-releases

---

## External Resources

- [Full Taxonomy](/help/release-notes/_meta/taxonomy)
- [Style Guide](/help/release-notes/_meta/style)
- [Audience Guide](/help/release-notes/_meta/audience-guide)
- [Icon Guide](/help/release-notes/_meta/icon-guide)
- [AI Agent Guide](/help/release-notes/_meta/AI-AGENT-GUIDE)
