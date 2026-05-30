# Platforms Code — Claude Code Skill

> A Claude Code skill that lets any AI generate UI fully compliant with the **Platforms Code** design system — the official design system of Saudi Digital Government Authority (DGA) government portals.

**Author:** [Hussain Al-Jabri](https://www.linkedin.com/in/engr-hussain-aljabri-a7305718b/) — Software Engineer · Saudi Arabia · [GitHub](https://github.com/hussainaljabri)  
**Based on:** [Platforms Code](https://www.figma.com/@sdga) by Saudi Digital Government Authority (SDGA / هيئة الحكومة الرقمية) — the mandated design standard for Saudi government portals under Vision 2030.  
**Status:** Community-maintained. Not an official SDGA/DGA product. — مجتمعي المصدر، غير رسمي وليس تابع لهيئة الحكومة الرقمية.

---

**Framework-independent.** Works with plain HTML, React, Angular, Vue, Svelte, or any other stack.  

**Design-system-accurate.** All rules extracted directly from the Figma source files and component CSS.  

**Open source.** MIT licensed — free to use, adapt, and contribute.

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

### Option 1 — Git clone (recommended, easy to update)

**Mac / Linux**
```bash
git clone https://github.com/hussainaljabri/platformscode-skill ~/.claude/skills/platformscode
```

**Windows PowerShell**
```powershell
git clone https://github.com/hussainaljabri/platformscode-skill "$env:USERPROFILE\.claude\skills\platformscode"
```

### Option 2 — Manual download (no git required)

1. Click **Code → Download ZIP** on this page
2. Extract the ZIP
3. Rename the extracted folder to `platformscode`
4. Move it to your Claude skills directory:

| OS | Path |
|----|------|
| Mac / Linux | `~/.claude/skills/platformscode/` |
| Windows | `%USERPROFILE%\.claude\skills\platformscode\` |

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
| OpenAI Codex CLI | ✅ Reference rule files from `AGENTS.md` in your project root |
| GitHub Copilot | ⚠️ Partial — copy rule files into repo as `.github/copilot-instructions.md` |
| Any AI with file context | ✅ Attach relevant `.md` files to your prompt |

---

## What "Platforms Code compliant" means

Compliance is not just visual — it covers typography, color discipline, layout stacking, and accessibility. Here is what the skill enforces and why each rule exists.

### Typography — IBM Plex Sans Arabic only

Every element uses `font-family: "IBM Plex Sans Arabic", sans-serif`. This is the only approved typeface — it covers both Latin and Arabic scripts in one face, ensuring consistent weight and spacing across bilingual content. Using system fonts, Tajawal, or Cairo breaks brand consistency.

### Color — Saudi green via CSS tokens, never hardcoded

```css
/* ✅ correct */
color: var(--colors-primary-sa-flag-600);   /* #1f7a4f */
background: var(--background-primary);

/* ❌ wrong */
color: #1f7a4f;
background: #ffffff;
color: green;
```

Token names are the contract. Hardcoded values break theming, dark mode, and future design updates. The only approved primary brand color is `#1f7a4f` — never a different green, blue, or teal.

### Border radius — by element type

The radius is not one-size-fits-all. Each level signals a different type of element:

| Element type | Radius | Token |
|---|---|---|
| Buttons, inputs, badges | `4px` | `--radius-sm` |
| Panels, sections, dropdowns | `8px` | `--radius-md` |
| Cards, modals, sheets | `16px` | `--radius-lg` |

Using `8px` on a button or `4px` on a card is visually off and breaks the design language hierarchy.

### Page stacking — gov stamp, cookies banner, header

Every full-page template has a strict three-layer stack. Getting this wrong causes elements to overlap or hide behind each other:

```
z-index: 300 │ Government Verification Stamp  ← position: sticky; top: 0
             │   (first element in <body>, always)
z-index: 200 │ Cookies Banner                 ← position: fixed; bottom: 0
             │   (slides up from bottom, never top)
z-index:  99 │ Site Header (72px)             ← position: sticky; top: {stamp height}px
             │   (top set dynamically by recalcLayout(), not hardcoded)
             │ Page content
```

`recalcLayout()` measures the stamp's rendered height on load and on resize and sets the header's `top` accordingly. This matters because the stamp can expand (showing verification tips) or be dismissed — both change its height.

### RTL and Arabic

Adding `dir="rtl"` to the root `<html>` element is sufficient. Flex and grid layouts mirror automatically. Logical CSS properties (`margin-inline-start`, `padding-inline-end`) are used throughout so no manual `left`/`right` flipping is needed.

```html
<!-- LTR (default) -->
<html lang="en">

<!-- RTL / Arabic -->
<html lang="ar" dir="rtl">
```

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

## Contributing

Pull requests welcome. Each rule file is self-contained Markdown — edit the relevant file, open a PR.

If you find a token, component, or page template missing from the Figma source files, open an issue with the Figma link and we'll add a rule file.

---

## License

MIT
