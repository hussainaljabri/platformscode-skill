---
name: platformscode-layout
description: Layout specs — 12-col grid, divider, flex utilities, page container
metadata:
  tags: platformscode, layout, grid, divider, flex, css, design-spec
---

Source CSS: `@platformscode/core/dist/collection/components/dga-button/dga-button.css` (utilities section)
Figma: https://www.figma.com/design/YGYwsEgALgfns9Maj8UbHX/

---

## Page container

```css
.page-container {
  max-width: 1280px;
  margin-inline: auto;
  padding-inline: 24px; /* --spacing-6 */
  width: 100%;
  box-sizing: border-box;
}
```

---

## 12-Column Grid

```css
.grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 24px; /* default gap */
  width: 100%;
}

/* Column spans */
.col-1  { grid-column: span 1; }
.col-2  { grid-column: span 2; }
.col-3  { grid-column: span 3; }
.col-4  { grid-column: span 4; }
.col-6  { grid-column: span 6; }
.col-8  { grid-column: span 8; }
.col-9  { grid-column: span 9; }
.col-12 { grid-column: span 12; }
```

### Responsive example
```css
@media (max-width: 900px) {
  .col-6, .col-4, .col-3 { grid-column: span 12; }
}
@media (max-width: 600px) {
  .grid { gap: 16px; }
}
```

---

## Breakpoints

| Name | Min width |
|------|-----------|
| `xs` | 0 |
| `sm` | 600px |
| `md` | 900px |
| `lg` | 1200px |
| `xl` | 1536px |

---

## Flex utilities

```css
.flex        { display: flex; }
.flex-col    { display: flex; flex-direction: column; }
.flex-center { display: flex; align-items: center; justify-content: center; }
.flex-between{ display: flex; justify-content: space-between; }
.flex-wrap   { flex-wrap: wrap; }
.items-start { align-items: flex-start; }
.items-center{ align-items: center; }
.items-end   { align-items: flex-end; }
```

---

## Divider

### CSS
```css
.divider {
  display: block;
  background-color: var(--border-neutral-primary);
}

.divider--horizontal {
  width: 100%;
  height: 1px;
}

.divider--vertical {
  width: 1px;
  height: 100%;
}

/* Color variants */
.divider--white   { background-color: var(--border-white); }
.divider--primary { background-color: var(--border-primary); }
```

### Usage
```html
<!-- Horizontal (between sections) -->
<div class="divider divider--horizontal" role="separator"></div>

<!-- Vertical (between inline items) -->
<div style="display:flex;align-items:center;gap:16px">
  <span>Item 1</span>
  <div class="divider divider--vertical" style="height:20px"></div>
  <span>Item 2</span>
</div>
```

---

## Spacing utilities (from source CSS)

The design system generates spacing classes. Use CSS custom properties instead of these classes where possible:

```
--spacing-1: 4px    --spacing-2: 8px    --spacing-3: 12px
--spacing-4: 16px   --spacing-5: 20px   --spacing-6: 24px
--spacing-8: 32px   --spacing-10: 40px  --spacing-12: 48px
--spacing-16: 64px  --spacing-20: 80px  --spacing-24: 96px
```

---

## Section patterns

### Page with sidebar
```html
<div class="grid" style="gap:32px">
  <aside class="col-3">
    <!-- sidebar nav -->
  </aside>
  <main class="col-9">
    <!-- content -->
  </main>
</div>
```

### Card grid (3-up)
```html
<div class="grid" style="gap:24px">
  <div class="col-4"><!-- card --></div>
  <div class="col-4"><!-- card --></div>
  <div class="col-4"><!-- card --></div>
</div>
```

### Hero (centered, max 800px)
```html
<div style="max-width:800px;margin-inline:auto;text-align:center;padding:80px 24px">
  <!-- hero content -->
</div>
```
