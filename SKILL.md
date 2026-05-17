---
name: platformscode
description: Platforms Code design system — visual design specifications extracted from source CSS and Figma, framework-independent
metadata:
  tags: platformscode, dga, saudi, government, design-system, css, html, design-spec, rtl, arabic
---

## When to use

Use this skill whenever you are building UI that must be visually compliant with the **Platforms Code** design system — the design system used by Saudi Digital Government Authority (DGA) government portals.

This skill contains **design knowledge extracted directly from the source CSS and Figma files**. It is framework-independent: use it to generate plain HTML/CSS, React, Angular, Vue, Svelte, or any other technology. The skill tells you *what things look like and how they are structured* — not which library to import.

## Creativity is required, not optional

This skill enforces design consistency — but consistency is not the same as sameness. Every Platforms Code page must be **visually compelling and purposeful**. Within the constraints below, you have full creative freedom:

- **Layout**: Go beyond a simple grid of cards. Use asymmetric layouts, hero sections, split panels, full-bleed banners with Saudi green gradients, sticky sidebars, floating elements.
- **Typography**: Be bold with heading sizes. Use `display-sm` (30px/600) and `display-xs` (24px/600) for impact. Vary text weights intentionally. Create clear visual hierarchy.
- **Micro-interactions**: Add CSS transitions, hover elevations, animated counters, smooth collapsibles, skeleton loaders, progress animations. A government portal should still feel alive.
- **Visual accents**: Use the Saudi green (`#1f7a4f`) strategically — gradient hero banners, colored icon containers, accent borders, progress fills. The brand color is a design asset, not just a button color.
- **Illustration / empty states**: Design thoughtful empty states, success states, and error states. A blank table is not acceptable — use featured icons, descriptive copy, and a clear call to action.
- **Data visualization**: When showing metrics, go beyond a number in a box. Use SVG-based mini charts, donut rings, sparklines, progress rings, timeline steps.
- **Whitespace**: Use generous whitespace — it communicates quality and authority, which is right for a government system.

**The rules below are the floor — your creativity determines the ceiling.**

## What "Platforms Code compliant" means

A compliant UI must:
- Use **IBM Plex Sans Arabic** as the font family (supports LTR and RTL)
- Use only **Saudi green** (`#1f7a4f` / `--colors-primary-sa-flag-600`) as the primary brand color — never arbitrary greens or blues
- Apply **CSS custom property tokens** for all colors, spacing, radius, and shadows — never hardcode values
- Follow component **anatomy and sizing** as specified in the rules below
- Support **RTL (Arabic)** layout by adding `dir="rtl"` to the root element
- Use `border-radius: 4px` (`--radius-sm`) on interactive elements, `8px` (`--radius-md`) on containers, `16px` (`--radius-lg`) on cards
- **Always include the Government Verification Stamp** as the very first element in `<body>` on every full-page template — see [./rules/section-gov-stamp.md](./rules/section-gov-stamp.md). It is a slim dark-green sticky bar (`z-index: 300`) that identifies the site as an official Saudi government portal, collapsible with verification tips.
- **Always include the Cookies Banner** on every full-page template — see [./rules/section-cookies-banner.md](./rules/section-cookies-banner.md). It is `position: fixed; bottom: 0` — it slides up from the bottom of the viewport after a short delay. Verified pattern from moj.gov.sa, mewa.gov.sa, and ksau-hs.edu.sa. It does **not** affect header positioning.
- The **site header** (72px) must be `position: sticky` with its `top` value set dynamically via `recalcLayout()` to sit flush below the gov stamp only (cookie banner is at the bottom, not the top).

## Design tokens

All values come from CSS custom properties. Never hardcode colors or spacing.

See [./rules/foundations.md](./rules/foundations.md) for the complete token reference — colors, spacing, typography, shadows, radius.

## Components

Load the relevant rule file when building a specific component:

- **Button** — [./rules/button.md](./rules/button.md) — sizes, variants, states, CSS
- **Card** — [./rules/card.md](./rules/card.md) — anatomy, shadow, hover, disabled
- **Form fields** — [./rules/form-fields.md](./rules/form-fields.md) — input, dropdown, checkbox, switch, radio
- **Navigation** — [./rules/navigation.md](./rules/navigation.md) — header (72px height), breadcrumbs, tabs
- **Feedback** — [./rules/feedback.md](./rules/feedback.md) — alert (left accent bar), modal (600px, blurred backdrop), notification
- **Data display** — [./rules/data-display.md](./rules/data-display.md) — tag, avatar, featured icon
- **Layout** — [./rules/layout.md](./rules/layout.md) — 12-col grid, divider (1px neutral), flex utilities
- **Accordion** — [./rules/accordion.md](./rules/accordion.md) — border-top separator, expand/collapse animation
- **Icons** — [./rules/icons.md](./rules/icons.md) — variants (stroke/solid/duotone), sizes, usage

## RTL and Arabic

See [./rules/rtl.md](./rules/rtl.md) for RTL-specific rules. Key: `dir="rtl"` on root element triggers automatic mirroring — no manual CSS flip needed.

## Page templates

Load when building a full page — each file contains the page's section composition, component choices, and layout from Figma:

- **Home Page** — [./rules/page-home.md](./rules/page-home.md)
- **Contact Us** — [./rules/page-contact.md](./rules/page-contact.md)
- **Help & Support** — [./rules/page-help.md](./rules/page-help.md)
- **FAQ** — [./rules/page-faq.md](./rules/page-faq.md)
- **Form / Application** — [./rules/page-form.md](./rules/page-form.md)
- **Search Results** — [./rules/page-search.md](./rules/page-search.md)
- **Content / Article** — [./rules/page-content.md](./rules/page-content.md)
- **Site Map** — [./rules/page-sitemap.md](./rules/page-sitemap.md)
- **Page Not Found (404)** — [./rules/page-404.md](./rules/page-404.md)
- **About The Entity** — [./rules/page-about.md](./rules/page-about.md)
- **Chatbot** — [./rules/page-chatbot.md](./rules/page-chatbot.md)
- **e-Participation** — [./rules/page-eparticipation.md](./rules/page-eparticipation.md)
- **Saudi National Day 95** — [./rules/page-national-day.md](./rules/page-national-day.md)
- **Saudi Founding Day** — [./rules/page-founding-day.md](./rules/page-founding-day.md)
- **Hajj & Umrah** — [./rules/page-hajj.md](./rules/page-hajj.md)

## Section templates

- **Government Verification Stamp** — [./rules/section-gov-stamp.md](./rules/section-gov-stamp.md) ← required on every page, first in `<body>`
- **Cookies Banner** — [./rules/section-cookies-banner.md](./rules/section-cookies-banner.md) ← required on every page, `position: fixed; bottom: 0`, slides up from bottom
- **Feedback Section** — [./rules/section-feedback.md](./rules/section-feedback.md)
- **Rating Section** — [./rules/section-rating.md](./rules/section-rating.md)
