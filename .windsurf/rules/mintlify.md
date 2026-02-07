# Mintlify technical writing rule

## Project context

- This is the BeatPass documentation project on the Mintlify platform
- We use MDX files with YAML frontmatter  
- Navigation is configured in `docs.json`
- We follow technical writing best practices
- Theme: mint | Default appearance: dark
- Fonts: Roboto (heading 600, body 400)
- Icons library: fontawesome

## Repository structure

- `help/` — Help Center content (platform guides, account settings, billing, etc.)
- `developers/` — API & Developer documentation (auth, rate limits, error catalog, webhooks, API reference)
- `release-notes/` — Changelog and version history (v2.x legacy, v3.0.x current)
- `snippets/` — Reusable content snippets (auto-hidden by Mintlify)
- `assets/` — Images, logos, and static resources
- `docs.json` — Site configuration and navigation

## Writing standards

- Use second person ("you") for instructions
- Write in active voice and present tense
- Start procedures with prerequisites
- Include expected outcomes for major steps
- Use descriptive, keyword-rich headings
- Keep sentences concise but informative

## Required page structure

Every page must start with frontmatter:

```yaml
---
title: "Clear, specific title"
description: "Concise description for SEO and navigation"
---
```

## Mintlify components

### docs.json

- Refer to the [docs.json schema](https://mintlify.com/docs.json) when building the docs.json file and site navigation

### Callouts

- `<Note>` for helpful supplementary information
- `<Warning>` for important cautions and breaking changes
- `<Tip>` for best practices and expert advice  
- `<Info>` for neutral contextual information
- `<Check>` for success confirmations

### Code examples

- When appropriate, include complete, runnable examples
- Use `<CodeGroup>` for multiple language examples
- Specify language tags on all code blocks
- Include realistic data, not placeholders
- Use `<RequestExample>` and `<ResponseExample>` for API docs

### Procedures

- Use `<Steps>` component for sequential instructions
- Include verification steps with `<Check>` components when relevant
- Break complex procedures into smaller steps

### Content organization

- Use `<Tabs>` for platform-specific content
- Use `<Accordion>` for progressive disclosure
- Use `<Card>` and `<CardGroup>` for highlighting content
- Wrap images in `<Frame>` components with descriptive alt text

## API documentation requirements

- Document all parameters with `<ParamField>` 
- Show response structure with `<ResponseField>`
- Include both success and error examples
- Use `<Expandable>` for nested object properties
- Always include authentication examples

## Reusable snippets

Use the `/snippets/` directory for content that appears on multiple pages. Mintlify auto-hides this folder from rendered navigation.

### Directory structure

- `snippets/warnings/` — Warning callouts (api-invite-only, no-public-sandbox, producer-only)
- `snippets/callouts/` — Info/Note callouts (platform-fee, subscription-required, stripe-connect-required)
- `snippets/sections/` — Reusable page sections (need-help, still-need-help, support-contact, api-getting-help, release-feedback, security-trust)
- `snippets/developer/` — Developer-specific blocks (bearer-auth-example, http-status-codes, rate-limit-headers)
- `snippets/data/` — Exported constants and data tables (platform-constants, plan-comparison-table)

### Usage

```mdx
import PlatformFee from "/snippets/callouts/platform-fee.mdx";

<PlatformFee />
```

### When to create a snippet

- Content appears on 3+ pages
- Content contains values that may change (prices, fees, emails)
- Content is a standardized section (Need Help?, API invite-only warning)

### When NOT to use a snippet

- Content is page-specific with unique context
- Content is deeply embedded in a larger sentence or table row
- Replacing would lose important page-specific nuance

## Quality standards

- Test all code examples before publishing
- Use relative paths for internal links
- Include alt text for all images
- Ensure proper heading hierarchy (start with h2)
- Check existing patterns for consistency
