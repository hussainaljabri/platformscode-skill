---
name: platformscode-card
description: Card visual spec — CSS, anatomy, variants, hover and disabled states
metadata:
  tags: platformscode, card, css, design-spec
---

Source CSS: `@platformscode/core/dist/collection/components/dga-card/dga-card.css`
Figma: https://www.figma.com/design/YGYwsEgALgfns9Maj8UbHX/

## Anatomy

```
┌─────────────────────────────────┐
│ [optional image — full width]   │
│ [optional badge/icon — 48×48]   │
│                                 │
│  Title / heading text           │
│  Supporting text / description  │
│                                 │
│  [action buttons — row]         │
└─────────────────────────────────┘
```

## Base CSS

```css
.card {
  width: 100%;
  padding: var(--spacing-xl);       /* 24px */
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: var(--card-lg-gap);          /* 24px */
  border-radius: var(--radius-lg);  /* 16px */
  background: var(--background-card);
  border: 2px solid var(--background-card); /* same color = invisible border by default */
  cursor: pointer;
  position: relative;
  box-sizing: border-box;
  overflow: hidden;
}
```

## Variants

### Default (flat, no shadow)
No extra class — base `.card` only.

### With shadow
```css
.card--with-shadow {
  box-shadow: 0px 4px 8px -2px rgba(16, 24, 40, 0.1),
              0px 2px 4px -2px rgba(16, 24, 40, 0.06);
}
```

### With stroke border
```css
.card--stroke {
  border: 1px solid var(--border-neutral-primary);
}
```

## States

### Hover
```css
.card:hover {
  background: var(--background-neutral-50, #F9FAFB);
}
```

### Focus-visible
```css
.card:focus-visible {
  border: 2px solid var(--border-black);
}
```

### Disabled
```css
.card.disabled {
  color: var(--text-default-disabled);
  background-color: transparent;
  border-color: transparent;
  pointer-events: none;
}
.card.disabled::after {
  content: "";
  position: absolute;
  inset: 0;
  background-color: var(--background-disabled);
  opacity: 0.3;
}
```

## Image slot

When a card has an image at the top:
```css
.card__image-container {
  width: 100%;
  height: 200px;
  overflow: hidden;
  border-radius: var(--radius-lg, 16px);
}
.card__image-container img {
  width: 100%;
  height: auto;
  border-radius: inherit;
}
```

## Action slot

Buttons at the bottom of a card:
```css
.card__action {
  width: 100%;
  display: flex;
  gap: 12px;
}
.card__action--expanded {
  justify-content: flex-end;
}
```

## Expandable content

Hidden content revealed on expand:
```css
.collapse-content { display: none; }
.collapse-content.expanded { display: block; }

.expand-button {
  margin-left: auto;
  transition: transform 0.3s;
}
.expand-button[aria-expanded="true"] .expand-icon {
  transform: rotate(180deg);
}
```

## Implementation example (plain HTML)

```html
<div class="card card--with-shadow" tabindex="0">
  <!-- Optional image -->
  <div class="card__image-container">
    <img src="photo.jpg" alt="Card image" />
  </div>

  <!-- Icon badge (48×48) -->
  <div style="width:48px;height:48px;border-radius:var(--radius-md);background:var(--background-brand-light);display:flex;align-items:center;justify-content:center;color:var(--text-success)">
    <!-- icon here -->
  </div>

  <!-- Content -->
  <div style="display:flex;flex-direction:column;gap:8px">
    <h3 style="color:var(--text-display);font:600 16px/24px 'IBMPlexSansArabic'">Card Title</h3>
    <p style="color:var(--text-primary-paragraph);font:400 14px/20px 'IBMPlexSansArabic'">Supporting text goes here.</p>
  </div>

  <!-- Actions -->
  <div class="card__action">
    <button class="btn btn--md btn--primary-brand">Primary</button>
    <button class="btn btn--md btn--secondary-outline">Secondary</button>
  </div>
</div>
```
