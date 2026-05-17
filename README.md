# Platforms Code — Claude Code Skill

> A Claude Code skill that lets any AI generate UI fully compliant with the **Platforms Code** design system — the official design system of Saudi Digital Government Authority (DGA) government portals.

**Framework-independent.** Works with plain HTML, React, Angular, Vue, Svelte, or any other stack.  

**Design-system-accurate.** All rules extracted directly from the Figma source files and component CSS.  

**Community-maintained.** Not an official Digital Government Authority (DGA) product.

---

## What You Get

Once installed, any Claude-powered tool understands:

- Every design token (Saudi green palette, spacing, radius, shadows, typography)
- All components (buttons, forms, cards, modals, data tables, accordions, tags, avatars…)
- Full page templates (Home, 404, FAQ, Form, Search, Chatbot, e-Participation, and more)
- Required sections (Government Verification Stamp, Cookies Banner)
- RTL/Arabic layout rules
- Accessibility and interaction patterns

---

## Install

### One-line (Mac / Linux)

```bash
git clone https://github.com/hussainaljabri/platformscode-skill ~/.claude/skills/platformscode
```

### One-line (Windows PowerShell)

```powershell
git clone https://github.com/hussainaljabri/platformscode-skill "$env:USERPROFILE\.claude\skills\platformscode"
```

That's it. Restart Claude Code — the skill is live.

---

## Usage

After installing, simply describe what you want to build in natural language. Claude reads the skill automatically because it lives inside `.claude/skills/`.

**Examples:**

```
Build a login page for our government portal — Platforms Code compliant, RTL Arabic support, split layout

Create an approval tracking dashboard with a data table, KPI cards, and a create-request modal

Generate a FAQ page following the Platforms Code FAQ template
```

Claude will:
- Apply the Government Verification Stamp at the top of every page
- Place the Cookies Banner fixed at the bottom
- Use IBM Plex Sans Arabic throughout
- Use Saudi green (`#1f7a4f`) as the sole brand color
- Apply CSS custom property tokens — never hardcoded values
- Support RTL/Arabic with `dir="rtl"` 

You can also reference rule files directly in your prompt for precision:

```
Using the Platforms Code button spec in rules/button.md, build a button group with all variants
```

---

## Skill Structure

```
platformscode/
├── SKILL.md                       ← Entry point — AI reads this first
└── rules/
    ├── foundations.md             ← Design tokens (colors, spacing, radius, shadows, typography)
    │
    ├── button.md                  ← Button variants, sizes, states, CSS
    ├── card.md                    ← Card anatomy, shadow, hover, disabled
    ├── form-fields.md             ← Input, dropdown, checkbox, switch, radio
    ├── navigation.md              ← Header (72px), breadcrumbs, tabs
    ├── feedback.md                ← Alert, modal, notification
    ├── data-display.md            ← Tag, avatar, featured icon
    ├── layout.md                  ← 12-col grid, divider, flex utilities
    ├── accordion.md               ← Border-top separator, expand/collapse animation
    ├── icons.md                   ← Stroke/solid/duotone variants, sizes, usage
    ├── rtl.md                     ← RTL/Arabic layout rules
    │
    ├── section-gov-stamp.md       ← ⚑ Government Verification Stamp (required, z:300)
    ├── section-cookies-banner.md  ← 🍪 Cookies Banner (required, fixed bottom, z:200)
    ├── section-feedback.md        ← Feedback section
    ├── section-rating.md          ← Rating section
    │
    ├── page-home.md               ← Home page template
    ├── page-contact.md            ← Contact Us
    ├── page-help.md               ← Help & Support
    ├── page-faq.md                ← FAQ
    ├── page-form.md               ← Form / Application
    ├── page-search.md             ← Search Results
    ├── page-content.md            ← Content / Article
    ├── page-sitemap.md            ← Site Map
    ├── page-404.md                ← Page Not Found
    ├── page-about.md              ← About The Entity
    ├── page-chatbot.md            ← Chatbot
    ├── page-eparticipation.md     ← e-Participation
    ├── page-national-day.md       ← Saudi National Day 95
    ├── page-founding-day.md       ← Saudi Founding Day
    └── page-hajj.md               ← Hajj & Umrah
```

---

## AI Tool Compatibility

| Tool | Support |
|------|---------|
| Claude Code (CLI) | ✅ Full — place in `~/.claude/skills/platformscode/` |
| Claude.ai (Projects) | ✅ Upload rule files as project knowledge |
| Cursor | ✅ Place in `.cursor/rules/` and reference from `.cursorrules` |
| GitHub Copilot | ⚠️ Partial — copy rule files into repo as `.github/copilot-instructions.md` |
| Any AI with file context | ✅ Attach relevant `.md` files to your prompt |

---

## What "Platforms Code compliant" means

Every page this skill generates enforces:

| Rule | Value |
|------|-------|
| Font | IBM Plex Sans Arabic |
| Primary brand color | `#1f7a4f` (`--colors-primary-sa-flag-600`) |
| Colors | CSS custom properties only — never hardcoded |
| Interactive radius | `4px` (`--radius-sm`) |
| Container radius | `8px` (`--radius-md`) |
| Card radius | `16px` (`--radius-lg`) |
| Gov Stamp | First element in `<body>`, `position: sticky; top: 0; z-index: 300` |
| Cookies Banner | `position: fixed; bottom: 0; z-index: 200` — slides up |
| Header | `position: sticky; top` set dynamically via `recalcLayout()` |
| RTL | `dir="rtl"` on root triggers automatic mirroring |

---

## How It Works (for AI developers)

This skill follows the [Claude Code skills pattern](https://docs.anthropic.com/en/docs/claude-code/skills). When placed in `~/.claude/skills/platformscode/`:

1. Claude Code detects `SKILL.md` as the skill entry point
2. `SKILL.md` describes what the skill knows and references the `rules/` files
3. When building UI, Claude loads the relevant rule files on demand
4. Every generated page is compliant without the user needing to specify tokens manually

The rules are **pure Markdown** — no runtime, no dependencies, no build step. Just design knowledge extracted from source Figma files and component CSS.

---

## Updating

```bash
cd ~/.claude/skills/platformscode
git pull
```

---

## Source

Design specifications extracted from:
- [Platforms Code Figma community files](https://www.figma.com/@sdga) — Saudi Digital Government Authority
- `@platformscode/core` npm package component CSS

This skill is **not** affiliated with or endorsed by DGA/SDGA. It is a community tool to help developers build compliant UIs faster.

---

## Contributing

Pull requests welcome. Each rule file is self-contained Markdown — edit the relevant file, open a PR.

If you find a token, component, or page template missing from the Figma source files, open an issue with the Figma link and we'll add a rule file.

---

## License

MIT
