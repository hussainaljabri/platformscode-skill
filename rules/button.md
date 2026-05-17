---
name: platformscode-button
description: Button visual spec — CSS, sizes, all variants and states extracted from source
metadata:
  tags: platformscode, button, css, design-spec, variants, states
---

Source CSS: `@platformscode/core/dist/collection/components/dga-button/dga-button.css`
Figma: https://www.figma.com/design/YGYwsEgALgfns9Maj8UbHX/

## Base structure

```html
<button class="btn btn--md btn--primary-brand">
  <!-- optional icon -->
  <span class="btn-label">Label</span>
  <!-- optional icon -->
</button>
```

## Base CSS

```css
.btn {
  appearance: none;
  border-radius: var(--radius-sm); /* 4px */
  cursor: pointer;
  border: 0;
  outline: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  box-sizing: border-box;
  overflow: hidden;
  font-family: "IBMPlexSansArabic", sans-serif;
}

.btn:focus-visible {
  outline: 2px solid var(--border-black);
}
```

## Sizes

| Size | Height | Font | Icon size |
|------|--------|------|-----------|
| `lg` | 40px | 500 16px/24px | 24×24 |
| `md` | 32px | 500 14px/20px | 20×20 |
| `sm` | 24px | 500 12px/18px | 16×16 |

```css
.btn--lg { height: 40px; padding-inline: var(--buttons-lg-padding); font: 500 16px/24px "IBMPlexSansArabic"; }
.btn--md { height: 32px; padding-inline: var(--buttons-md-padding); font: 500 14px/20px "IBMPlexSansArabic"; }
.btn--sm { height: 24px; padding-inline: var(--buttons-sm-padding); font: 500 12px/18px "IBMPlexSansArabic"; }
```

Icon-only (square):
```css
.btn--icon.btn--lg { width: 40px; height: 40px; padding: 0; }
.btn--icon.btn--md { width: 32px; height: 32px; padding: 0; }
.btn--icon.btn--sm { width: 24px; height: 24px; padding: 0; }
```

## Variants

### primary-brand (Saudi green — primary CTA)
```css
.btn--primary-brand { background-color: var(--button-background-primary-default); color: #fff; }
.btn--primary-brand:hover  { background: var(--button-background-primary-hovered); }
.btn--primary-brand:active { background: var(--button-background-primary-selected); }
.btn--primary-brand:disabled { background: var(--background-disabled); color: var(--text-default-disabled); }
```
> `--button-background-primary-default` resolves to `#1f7a4f` (Saudi green 600)

### primary-neutral (black — dark CTA)
```css
.btn--primary-neutral { background-color: var(--button-background-black-default); color: #fff; }
.btn--primary-neutral:hover  { background-color: var(--button-background-black-hovered); }
.btn--primary-neutral:active { background-color: var(--button-background-black-selected); }
.btn--primary-neutral:disabled { background: var(--background-disabled); color: var(--text-default-disabled); }
```

### secondary (filled gray)
```css
.btn--secondary { background-color: var(--button-background-neutral-default); color: var(--colors-text-primary); }
.btn--secondary:hover  { background: var(--button-background-neutral-default-hoverd); }
.btn--secondary:active { background: var(--button-background-neutral-default-selected); }
```

### secondary-outline (bordered, transparent bg)
```css
.btn--secondary-outline {
  outline: 1px solid var(--border-neutral-secondary);
  background-color: transparent;
  color: var(--text-default);
  mix-blend-mode: multiply;
}
.btn--secondary-outline:hover  { background: var(--button-background-neutral-default); }
.btn--secondary-outline:active { background: var(--button-background-neutral-selected); outline-color: var(--border-neutral-primary); }
.btn--secondary-outline:disabled { background: transparent; color: var(--text-default-disabled); border: 1px solid var(--border-neutral-secondary); }
```

### subtle (ghost — transparent with hover fill)
```css
.btn--subtle { background-color: transparent; color: var(--colors-text-primary); mix-blend-mode: multiply; }
.btn--subtle:hover  { background: var(--button-background-neutral-default); }
.btn--subtle:active { background: var(--button-background-neutral-selected); }
.btn--subtle:disabled { background: transparent; color: var(--text-default-disabled); }
```

### transparent (text-only, no bg on hover)
```css
.btn--transparent { background-color: transparent; color: var(--text-default); }
.btn--transparent:hover  { color: var(--button-background-primary-hovered); }
.btn--transparent:active { color: var(--button-background-primary-selected); }
```

### des-primary (destructive — red CTA)
```css
.btn--des-primary { background-color: var(--button-background-danger-primary-default); color: #fff; }
.btn--des-primary:hover  { background: var(--button-background-danger-primary-hovered); }
.btn--des-primary:disabled { background: var(--background-disabled); color: var(--text-default-disabled); }
```

### des-secondary, des-secondary-outline, des-subtle, des-transparent
Same pattern as non-destructive equivalents but using `--button-background-danger-*` tokens and `color: var(--text-error)`.

## States summary

| State | Visual change |
|-------|--------------|
| Default | Variant base background/color |
| Hover | Slightly darker or filled background |
| Active/pressed | Even darker, no outline |
| Focus-visible | `2px solid var(--border-black)` outline |
| Disabled | `var(--background-disabled)` bg, `var(--text-default-disabled)` text, `cursor: not-allowed` |

## On-color variant

When a button sits on a dark/colored background, add `--on-color` modifier. This inverts to white background with dark text:
```css
.btn--primary-brand--on-color { background-color: var(--button-background-oncolor-default); color: var(--text-default); }
```
