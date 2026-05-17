---
name: dga-foundations
description: DGA design tokens — colors, typography, spacing, border radius, elevation, grid
metadata:
  tags: dga, tokens, colors, typography, spacing, grid, elevation, foundations
---

Figma source: https://www.figma.com/design/ejgmxM1qWJQFZ7kBMdfZP8/

## Colors

### Brand — Saudi Green

```
--colors-primary-sa-flag-25:  #f2faf5
--colors-primary-sa-flag-50:  #e4f4ec
--colors-primary-sa-flag-100: #c3e8d3
--colors-primary-sa-flag-200: #8dd6b4
--colors-primary-sa-flag-300: #6ec598
--colors-primary-sa-flag-400: #3dab78
--colors-primary-sa-flag-500: #25935f   ← main brand
--colors-primary-sa-flag-600: #1f7a4f   ← button primary default
--colors-primary-sa-flag-700: #196040
--colors-primary-sa-flag-800: #114530
--colors-primary-sa-flag-900: #0b3323
--colors-primary-sa-flag-950: #061f15
```

### Neutral / Gray

```
--colors-neutral-25:  #fcfcfd    --colors-neutral-50:  #f9fafb
--colors-neutral-100: #f2f4f7    --colors-neutral-200: #e4e7ec
--colors-neutral-300: #d0d5dd    --colors-neutral-400: #98a2b3
--colors-neutral-500: #667085    --colors-neutral-600: #475467
--colors-neutral-700: #344054    --colors-neutral-800: #1d2939
--colors-neutral-900: #101828    --colors-neutral-950: #0c111b
```

### Semantic colors

```
Success: --colors-green-600:  #16a34a   light bg: --colors-green-25:  #f0fdf4
Error:   --colors-red-600:    #dc2626   light bg: --colors-red-25:    #fff5f5
Warning: --colors-yellow-600: #d97706   light bg: --colors-yellow-25: #fffbeb
Info:    --colors-blue-600:   #2563eb   light bg: --colors-blue-25:   #eff6ff
```

### Semantic usage tokens

```
Background:  --background-primary | --background-secondary | --background-tertiary
             --background-success | --background-error | --background-warning | --background-info
             --background-success-light | --background-error-light | --background-warning-light
Text:        --text-primary | --text-secondary | --text-tertiary | --text-placeholder
             --text-success | --text-error | --text-warning | --text-info
Border:      --border-primary | --border-secondary
             --border-success | --border-error | --border-warning | --border-info
Button:      --button-background-primary-default | --button-background-primary-hover
             --button-background-secondary-default | --button-background-danger-default
```

---

## Typography

Font family: **IBM Plex Sans Arabic** (all weights 100–700)
Monospace: **Roboto Mono**

| Scale      | Size | Line Height |
|------------|------|-------------|
| Display XL | 72px | 90px        |
| Display    | 60px | 72px        |
| H1         | 48px | 60px        |
| H2         | 36px | 44px        |
| H3         | 30px | 38px        |
| H4         | 24px | 32px        |
| H5         | 20px | 30px        |
| H6         | 18px | 28px        |
| Body       | 16px | 24px        |
| Small      | 14px | 20px        |

---

## Spacing

```
--spacing-1: 4px    --spacing-2: 8px    --spacing-3: 12px   --spacing-4: 16px
--spacing-5: 20px   --spacing-6: 24px   --spacing-8: 32px   --spacing-10: 40px
--spacing-12: 48px  --spacing-16: 64px  --spacing-20: 80px  --spacing-24: 96px
```

---

## Border Radius

```
--radius-none: 0      --radius-xs: 2px    --radius-sm: 4px    --radius-md: 8px
--radius-lg: 16px     --radius-xl: 24px   --radius-full: 9999px
```

---

## Elevation / Shadows

```
--shadow-xs:  0px 1px 2px 0px rgba(16,24,40,0.05)
--shadow-sm:  0px 1px 3px 0px rgba(16,24,40,0.10), 0px 1px 2px rgba(16,24,40,0.06)
--shadow-md:  0px 4px 8px -2px rgba(16,24,40,0.10), 0px 2px 4px rgba(16,24,40,0.06)
--shadow-lg:  0px 12px 16px -4px rgba(16,24,40,0.08), 0px 4px 6px rgba(16,24,40,0.03)
--shadow-xl:  0px 20px 24px -4px rgba(16,24,40,0.08), 0px 8px 8px rgba(16,24,40,0.03)
--shadow-2xl: 0px 24px 48px -12px rgba(16,24,40,0.18)
--shadow-3xl: 0px 32px 64px -12px rgba(16,24,40,0.14)
```

---

## Grid & Breakpoints

12-column grid. Use `DgaGridContainer cols={12}` + `DgaGridItem colSpan={n}`.

```
xs: 0px    sm: 600px    md: 900px    lg: 1200px    xl: 1536px
```

Responsive `colSpan` via the `sx` prop:

```tsx
<DgaGridItem sx={{ gridColumn: { xs: 'span 12', md: 'span 6' } }}>
```

---

## sx prop

React components support an MUI-inspired `sx` prop for inline styles:

```tsx
// CSS object — camelCase keys
<DgaCard sx={{ padding: 'var(--spacing-6)', borderRadius: 'var(--radius-md)' }} />

// Nested selectors
<DgaButton sx={{ ':hover': { opacity: 0.9 }, '& .label': { fontWeight: 600 } }} />

// Responsive values
<DgaGridItem sx={{ width: { xs: '100%', md: '50%' } }} />
```
