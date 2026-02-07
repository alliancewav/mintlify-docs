---
audience: help
title: "Mintlify Components for Release Notes"
sidebarTitle: "Component Reference"
description: "Approved Mintlify components for release note formatting."
---

# Mintlify Components for Release Notes

Quick reference for Mintlify components approved for use in release notes.

---

## Callouts (Alerts)

### Info

```mdx
<Info>
  Helpful information users should know.
</Info>
```

### Warning

```mdx
<Warning>
  Important notice that requires attention.
</Warning>
```

### Tip

```mdx
<Tip>
  Helpful advice or shortcut.
</Tip>
```

### Note

```mdx
<Note>
  Additional context or explanation.
</Note>
```

---

## Cards

### Single Card

```mdx
<Card title="Card Title" icon="star" href="/path">
  Card content description.
</Card>
```

### Card Group

```mdx
<CardGroup cols={2}>
  <Card title="Feature 1" icon="star">
    Description of feature 1.
  </Card>
  <Card title="Feature 2" icon="bolt">
    Description of feature 2.
  </Card>
</CardGroup>
```

**Approved icons**: See [Icon Guide](/help/release-notes/_meta/icon-guide)

---

## Accordions

### Single Accordion

```mdx
<Accordion title="Section Title" icon="icon-name">
  Content that can be expanded/collapsed.
</Accordion>
```

### Accordion Group

```mdx
<AccordionGroup>
  <Accordion title="First Section" icon="star">
    Content for first section.
  </Accordion>
  <Accordion title="Second Section" icon="bolt">
    Content for second section.
  </Accordion>
</AccordionGroup>
```

---

## Updates (Changelog Entries)

The `Update` component is used in `release-notes/changelog.mdx` to create the unified changelog with tag filters and RSS feed.

### Basic Update

```mdx
<Update label="February 7, 2026" description="v3.0.8-25" tags={["Security", "API"]}>
  ## API Security Hardening

  Comprehensive API security audit and hardening across the platform.

  - **Authentication enforced** on sensitive endpoints
  - **Developer token support** with Bearer auth and 90-day expiration
  - **New rate limits** for abuse protection

  [Read full release notes →](/release-notes/v3.0/3.0.8-25)
</Update>
```

### Update with RSS Override

Use the `rss` prop when the entry contains Mintlify components or HTML (these are excluded from RSS):

```mdx
<Update
  label="December 1, 2025"
  description="v3.0.8-12"
  tags={["Platform", "Feature"]}
  rss={{
    title: "December 2025 Production Launch",
    description: "BeatPass v3.0.8 is now live with Stripe Connect, Producer Dashboard, and more."
  }}
>
  ## Production Launch

  <Frame>
    <img src="/images/launch.png" alt="Production launch" />
  </Frame>

  [Read full release notes →](/release-notes/v3.0/3.0.8-12)
</Update>
```

### Update Props

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `label` | string | Yes | Date label (`"Month Day, Year"` format). Creates anchor link. |
| `description` | string | No | Version string (e.g., `"v3.0.8-25"`). Appears below label. |
| `tags` | string[] | No | Title Case tags for sidebar filters. Replaces table of contents. |
| `rss` | object | No | Custom `{title, description}` for RSS feed entry. |

### Tag Values (Title Case)

`Feature`, `Bug Fix`, `Security`, `Performance`, `UI/UX`, `Billing`, `Producer`, `Mobile`, `Platform`, `API`, `Notifications`

### RSS Feed

The changelog page (`release-notes/changelog.mdx`) has `rss: true` in frontmatter, which:
- Enables an RSS icon button at the top of the page
- Auto-generates an RSS feed at `/release-notes/changelog/rss.xml`
- Each `Update` with Markdown headings creates RSS entries automatically
- RSS entries contain pure Markdown only (components/HTML excluded)

### Placement Rules

- `Update` entries go in `release-notes/changelog.mdx` **only** (not individual release pages)
- **Newest entries at the top** (after frontmatter)
- Each entry must link to its full individual release note page

---

## Steps

```mdx
<Steps>
  <Step title="Step One">
    Instructions for first step.
  </Step>
  <Step title="Step Two">
    Instructions for second step.
  </Step>
  <Step title="Step Three">
    Instructions for third step.
  </Step>
</Steps>
```

Use for "How to Use" sections with 3-5 steps.

---

## Tabs

```mdx
<Tabs>
  <Tab title="Tab One">
    Content for the first tab.
  </Tab>
  <Tab title="Tab Two">
    Content for the second tab.
  </Tab>
</Tabs>
```

Use for organizing related content into switchable views (e.g., metrics, platform-specific instructions).

---

## Badges

```mdx
<Badge color="green">New</Badge>
<Badge color="blue">Updated</Badge>
<Badge color="red">Fixed</Badge>
<Badge color="purple">Beta</Badge>
```

**Colors**: green, blue, red, purple, yellow, gray

---

## Tooltips

Tooltips provide inline contextual definitions when a user hovers over a term. Use them to clarify domain jargon, technical terms, or BeatPass-specific concepts without disrupting reading flow.

### Basic Tooltip

```mdx
<Tooltip tip="Credits that control how many beat requests you can create each month.">tokens</Tooltip>
```

### Tooltip with Call-to-Action

```mdx
<Tooltip tip="A score based on recency, play count, and collaborators that determines your share of subscription revenue." cta="See the formula" href="/help/earnings/contribution-system/formula">contribution value</Tooltip>
```

### Tooltip Props

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `tip` | string | Yes | The text displayed in the tooltip on hover. |
| `headline` | string | No | Bold text displayed above the `tip` text. |
| `cta` | string | No | Call-to-action link text inside the tooltip. |
| `href` | string | No | URL for the CTA link. Required when using `cta`. |

### Tooltip Usage Rules

1. **First occurrence only** — Tooltip the first meaningful mention of a term per page. Never repeat the same tooltip on the same page.
2. **Keep `tip` text short** — One to two sentences max. If you need more, link to a dedicated page with `cta` + `href`.
3. **Use `cta` + `href` sparingly** — Only when a dedicated deeper page exists for the term.
4. **Don't nest inside headings** — Tooltips go in body text, not in `##` / `###` headings (unless the heading IS the defined term, e.g., a glossary entry).
5. **Don't duplicate callouts** — If a `<Note>`, `<Info>`, or `<Warning>` already explains the term in the same section, a tooltip is redundant.
6. **Works alongside bold/code** — `**<Tooltip tip="...">Stripe</Tooltip>**` and `<Tooltip tip="...">\`Retry-After\`</Tooltip>` are both valid.

### When to Use Tooltips

| Situation | Use Tooltip? | Example |
|-----------|-------------|---------|
| Domain jargon (BeatPass-specific) | ✅ Yes | contribution value, tokens, platform fee |
| Technical acronym or term | ✅ Yes | API, Bearer token, 2FA, XP |
| Industry term with BeatPass-specific meaning | ✅ Yes | exclusive license, Stripe Express |
| Common English word | ❌ No | subscription, upload, download |
| Term already explained in an adjacent callout | ❌ No | — |
| Same term later on the same page | ❌ No | — |

### Tooltip vs. Other Components

| Need | Use |
|------|-----|
| Quick inline definition (1-2 sentences) | `<Tooltip>` |
| Important notice or caveat | `<Warning>` / `<Note>` / `<Info>` |
| Multi-paragraph explanation | Dedicated section or linked page |
| Step-by-step instructions | `<Steps>` |

---

## Reusable Snippets

Mintlify supports **reusable snippets** — `.mdx` files that can be imported into any documentation page. BeatPass uses snippets to centralize content that appears on multiple pages, ensuring consistency and making updates easier as the documentation grows.

### How Snippets Work

Snippets are stored in `/snippets/` at the root of the documentation. Mintlify **automatically hides** the `snippets/` directory from rendered navigation, so these files never appear as standalone pages.

**Import and use:**
```mdx
import PlatformFee from "/snippets/callouts/platform-fee.mdx";

<PlatformFee />
```

**Rules:**
- Import statements go **after frontmatter**, before any content
- Use **absolute paths** starting with `/snippets/`
- Component names use **PascalCase** (e.g., `PlatformFee`, `ApiInviteOnly`)
- Each snippet renders as if its content were inline at the `<ComponentName />` location

### Directory Structure

```text
Documentation/snippets/
├── callouts/                     # Info/Note/Warning callout blocks
│   ├── platform-fee.mdx          # Platform fee explanation (Info)
│   ├── platform-fee-note.mdx     # Platform fee note for producers (Note)
│   ├── subscription-required.mdx # Paid plan required notice (Info)
│   └── stripe-connect-required.mdx # Stripe Connect setup required (Warning)
├── warnings/                     # Warning-only blocks
│   ├── api-invite-only.mdx       # API access invite-only warning
│   ├── no-public-sandbox.mdx     # No sandbox environment warning + table
│   └── producer-only.mdx         # Producer privileges required note
├── sections/                     # Reusable page sections (headings + content)
│   ├── need-help.mdx             # Generic "Need Help?" with contact info
│   ├── still-need-help.mdx       # Troubleshooting "Still Need Help?" with Steps
│   ├── support-contact.mdx       # One-line support contact sentence
│   ├── api-getting-help.mdx      # Developer-specific help table
│   ├── release-feedback.mdx      # Release notes feedback footer (Card + email)
│   └── security-trust.mdx        # Security trust closing Info block
├── developer/                    # Developer documentation blocks
│   ├── bearer-auth-example.mdx   # Bearer token auth code example
│   ├── http-status-codes.mdx     # HTTP status codes reference table
│   └── rate-limit-headers.mdx    # Rate limit header example
└── data/                         # Exported constants and data tables
    ├── platform-constants.mdx    # Exported JS variables (prices, fees, emails)
    └── plan-comparison-table.mdx # Full plan comparison table with Info callout
```

### Available Snippets Reference

#### Callouts

| Snippet | Import Name | What It Renders |
|---------|-------------|------------------|
| `callouts/platform-fee.mdx` | `PlatformFee` | `<Info>` explaining the 12% + $3 fee, that producers keep 100%, with link to platform-fee page |
| `callouts/platform-fee-note.mdx` | `PlatformFeeNote` | `<Note>` about producers receiving 100% of listed price |
| `callouts/subscription-required.mdx` | `SubscriptionRequired` | `<Info>` that a paid plan is required, with link to plan comparison |
| `callouts/stripe-connect-required.mdx` | `StripeConnectRequired` | `<Warning>` that Stripe Connect must be fully verified for payouts |

#### Warnings

| Snippet | Import Name | What It Renders |
|---------|-------------|------------------|
| `warnings/api-invite-only.mdx` | `ApiInviteOnly` | `<Warning>` that API access is invite-only with contact email |
| `warnings/no-public-sandbox.mdx` | `NoPublicSandbox` | `<Warning>` + impact table showing all API calls hit production |
| `warnings/producer-only.mdx` | `ProducerOnly` | `<Note>` that feature requires producer privileges |

#### Sections

| Snippet | Import Name | What It Renders |
|---------|-------------|------------------|
| `sections/need-help.mdx` | `NeedHelp` | `## Need Help?` heading with contact email and support page link |
| `sections/still-need-help.mdx` | `StillNeedHelp` | `## Still Need Help?` heading with `<Steps>` for search + contact |
| `sections/support-contact.mdx` | `SupportContact` | Single-line "contact the support team at contact@beatpass.ca" |
| `sections/api-getting-help.mdx` | `ApiGettingHelp` | `## Getting Help` heading with contact topic table |
| `sections/release-feedback.mdx` | `ReleaseFeedback` | `## Feedback` heading with Contact Support Card + email — **use on every release note** |
| `sections/security-trust.mdx` | `SecurityTrust` | `<Info>` block: "We take security seriously. Thank you for your trust in BeatPass." |

#### Developer

| Snippet | Import Name | What It Renders |
|---------|-------------|------------------|
| `developer/bearer-auth-example.mdx` | `BearerAuthExample` | HTTP code block showing Bearer auth header |
| `developer/http-status-codes.mdx` | `HttpStatusCodes` | Table of status codes with meaning and action |
| `developer/rate-limit-headers.mdx` | `RateLimitHeaders` | HTTP code block showing X-RateLimit headers |

#### Data

| Snippet | Import Name | What It Provides |
|---------|-------------|------------------|
| `data/platform-constants.mdx` | (exported variables) | JS constants: `supportEmail`, `platformFee`, `plans`, `apiTokenExpiry`, `baseUrl`, `publishingSplit`, `performanceLimit` |
| `data/plan-comparison-table.mdx` | `PlanComparisonTable` | Full feature comparison table across all four plans |

### Using Data Constants

The `platform-constants.mdx` file exports JavaScript variables for programmatic use:

```mdx
import { platformFee, plans, supportEmail } from "/snippets/data/platform-constants.mdx";

The platform fee is **{platformFee.formatted}** ({platformFee.currency}).

The Plus plan costs **{plans.plus.price}**.

Contact us at **{supportEmail}**.
```

### When to Use Snippets

| Situation | Use Snippet? | Why |
|-----------|-------------|-----|
| Platform fee explanation appears on a new page | ✅ Yes | `<PlatformFee />` ensures consistent wording |
| Page needs a "Need Help?" footer | ✅ Yes | `<NeedHelp />` centralizes contact info |
| API page needs invite-only warning | ✅ Yes | `<ApiInviteOnly />` keeps warning consistent |
| Page mentions subscription requirement | ✅ Yes | `<SubscriptionRequired />` links to plan comparison |
| Developer page needs auth example | ✅ Yes | `<BearerAuthExample />` keeps code block consistent |
| Content is unique to one page | ❌ No | No reuse benefit |
| Fee mention is inline in a sentence | ❌ No | Snippet renders a full block, not inline text |
| Content is inside a table cell or accordion | ❌ No | Snippet blocks don't nest well in these contexts |
| Page-specific troubleshooting steps | ❌ No | Context-specific content shouldn't be genericized |

### Creating New Snippets

Create a new snippet when:
- The same content block appears on **3+ pages**
- Content contains **values that may change** (prices, fees, contact emails)
- Content is a **standardized section** with identical structure across pages

**Steps:**
1. Create the `.mdx` file in the appropriate `/snippets/` subdirectory
2. Use the correct Mintlify components (`<Warning>`, `<Info>`, `<Note>`, `<Steps>`, etc.)
3. Import and use the snippet in all relevant pages
4. Remove the old inline content from those pages
5. Update this reference document with the new snippet

**Naming convention:**
- Filenames: `lowercase-with-hyphens.mdx`
- Import names: `PascalCase` matching the filename (e.g., `platform-fee.mdx` → `PlatformFee`)

---

## Tables

```mdx
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Data 1   | Data 2   | Data 3   |
| Data 4   | Data 5   | Data 6   |
```

Use for:
- Breaking changes tables
- Configuration options
- Before/after comparisons

---

## Code Blocks

### Basic Code Block

```mdx
```typescript
const example = "code";
```
```

### With Title

```mdx
```typescript Example Code
const example = "code";
```
```

### With Highlighting

```mdx
```typescript {2,4-5}
const line1 = "normal";
const line2 = "highlighted";
const line3 = "normal";
const line4 = "highlighted";
const line5 = "highlighted";
```
```

### Diff View

```mdx
```typescript
const old = "value"; // [!code --]
const new = "value"; // [!code ++]
```
```

**Note**: Use code blocks sparingly in release notes. Users are non-technical.

---

## Frames (Images)

```mdx
<Frame caption="Screenshot description">
  <img src="/path/to/image.png" alt="Descriptive alt text" />
</Frame>
```

**Note**: Screenshots in release notes should be redacted if they contain sensitive data.

---

## Component Usage Guidelines

### Do Use

- **Cards** — For related documentation links, feature highlights
- **Accordions** — For organizing multiple related items (Recent Highlights)
- **Steps** — For "How to Use" instructions
- **Badges** — For version numbers, status indicators
- **Tables** — For breaking changes, configuration options
- **Callouts** — For important notices, warnings, tips
- **Tooltips** — For inline definitions of jargon, technical terms, or BeatPass-specific concepts (first occurrence per page only)

### Don't Use

- **Code blocks** — Unless showing user-facing configuration
- **Complex iframes** — Not needed for release notes
- **Videos** — Too heavy for release notes
- **Interactive components** — Keep it simple

---

## Release Notes: Two-Part System

BeatPass uses a **two-part release notes system**. Every release requires:

1. **Individual page** in `release-notes/v3.0/{version}.mdx` — Full content using templates
2. **Changelog entry** in `release-notes/changelog.mdx` — `Update` component with summary

### Individual Page Structure

```mdx
---
title: "Update Title"
date: "YYYY-MM-DD"
severity: "minor"
audience: "All"
tags: ["feature"]
components: ["dashboard"]
---

# Update Title

## Summary

Brief overview in 2-3 sentences.

## What's New

- **Feature name** — What it does
- **Another feature** — What it does

## Why It Matters

<CardGroup cols={2}>
  <Card title="Benefit 1" icon="star">
    Explanation of benefit.
  </Card>
  <Card title="Benefit 2" icon="bolt">
    Explanation of benefit.
  </Card>
</CardGroup>

## How to Use

<Steps>
  <Step title="Navigate to Page">
    Click **profile avatar** → **Billing**.
  </Step>
  <Step title="Click Button">
    Click **Change plan**.
  </Step>
</Steps>

## Related

- [Documentation Link](/help/path)
```

### Changelog Entry Structure

Add at the **top** of `release-notes/changelog.mdx`:

```mdx
<Update label="{Month Day, Year}" description="v{version}" tags={["{Tag1}", "{Tag2}"]}>
  ## {Title}

  {1-2 sentence summary.}

  - **{Key change 1}** — Brief description
  - **{Key change 2}** — Brief description

  [Read full release notes →](/release-notes/v3.0/{version})
</Update>
```

See `template.mdx` for the complete workflow and tag reference.

---

## docs.json Configuration Requirements

The `docs.json` file controls site-wide settings. These configurations are **critical** and must be maintained:

### Icon Library

```json
"icons": {
  "library": "fontawesome"
}
```

**This MUST be set to `fontawesome`.** Without it, Mintlify defaults to fontawesome but the explicit setting prevents ambiguity. All icon names throughout the docs and navigation MUST be valid [Font Awesome 6](https://fontawesome.com/icons) names.

### Color Palette (WCAG AA Compliant)

```json
"colors": {
  "primary": "#187AB4",
  "light": "#5BC0F0",
  "dark": "#1F8AC8"
}
```

**Never change these without verifying WCAG AA contrast ratios:**
- Primary vs white: must be ≥ 4.5:1
- Light vs dark background (#050505): must be ≥ 4.5:1
- Use [webaim.org/resources/contrastchecker](https://webaim.org/resources/contrastchecker/) to verify
- Run `mint a11y` after any color change (exit code 0 = pass)

### Navigation Icon Names

All `"icon"` values in docs.json navigation groups/tabs must be valid FA6 names:

```json
✅ "icon": "scale-balanced"     // FA6 name
❌ "icon": "scale"              // Not valid in FA6 — renders blank
❌ "icon": "bar-chart"          // FA4 alias removed in FA6
❌ "icon": "message-square"     // Lucide name — not FA6
```

---

## Full Component Reference

For complete Mintlify documentation, see:
- [Mintlify Components Guide](https://mintlify.com/docs/components)
- [Mintlify Content Formatting](https://mintlify.com/docs/content)
- [docs.json Schema](https://mintlify.com/docs.json)

---

<Info>
  Keep release notes simple. Use components to enhance readability, not to add complexity.
</Info>
