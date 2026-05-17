---
name: platformscode-data-display
description: Data display specs — tag, avatar, featured icon, accordion — CSS and anatomy
metadata:
  tags: platformscode, tag, avatar, featured-icon, accordion, css, design-spec
---

Source CSS: `@platformscode/core/dist/collection/components/`
Figma: https://www.figma.com/design/YGYwsEgALgfns9Maj8UbHX/

---

## Tag / Badge

### CSS
```css
.tag {
  display: inline-flex;
  height: 24px;                           /* md default */
  padding: 0 var(--spacing-lg);           /* 0 18px */
  justify-content: center;
  align-items: center;
  gap: var(--spacing-xs);                 /* 4px */
  border-radius: var(--radius-sm);        /* 4px */
  font: 500 12px/18px "IBMPlexSansArabic";
}

/* Pill shape variant */
.tag--rounded { border-radius: var(--radius-full); }
```

### Sizes
| Size | Height |
|------|--------|
| `lg` | 32px |
| `md` | 24px |
| `sm` | 20px |

### Color variants
```css
.tag--neutral  { color: var(--tag-text-neutral);  background: var(--tag-background-neutral-light);  border: 1px solid var(--border-neutral-secondary); }
.tag--success  { color: var(--tag-text-success);  background: var(--tag-background-success-light);  border: 1px solid var(--tag-border-success-light); }
.tag--error    { color: var(--tag-text-error);    background: var(--tag-background-error-light);    border: 1px solid var(--tag-border-error-light); }
.tag--warning  { color: var(--tag-text-warning);  background: var(--tag-background-warning-light);  border: 1px solid var(--tag-border-warning-light); }
.tag--info     { color: var(--tag-text-info);     background: var(--tag-background-info-light);     border: 1px solid var(--tag-border-info-light); }
.tag--purple   { color: var(--colors-purple-700); background: var(--colors-purple-50);              border: 1px solid var(--colors-purple-200); }

/* Outlined (transparent bg) */
.tag--neutral-outlined { border: 1px solid var(--tag-border-neutral); background: transparent; color: var(--tag-text-neutral); }
```

---

## Avatar

### CSS
```css
.dga-avatar {
  position: relative;
  border-radius: var(--radius-full);    /* circular */
  border: 2px solid var(--border-white, #FFF);
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--button-background-neutral-default);
  overflow: hidden;
}

/* Image type */
.dga-avatar img { width: 100%; height: 100%; object-fit: cover; }

/* Initials — uppercase text centered */
.dga-avatar__text { text-transform: uppercase; font-weight: 600; }
```

### Sizes
| Size token | Dimensions | Initials font |
|-----------|-----------|--------------|
| `120` | 120×120 | `display-xs-semibold` (24px) |
| `80` | 80×80 | `text-xl-semibold` (20px) |
| `68` | 68×68 | `text-lg-semibold` (18px) |
| `48` | 48×48 | `text-md-semibold` (16px) |
| `40` | 40×40 | `text-sm-semibold` (14px) |
| `32` | 32×32 | `text-xs-semibold` (12px) |
| `24` | 24×24 | `text-2xs-semibold` (10px) |

```css
.dga-avatar--120 { width: 120px; height: 120px; border-width: 4px; }
.dga-avatar--80  { width: 80px;  height: 80px; }
.dga-avatar--48  { width: 48px;  height: 48px; }
.dga-avatar--40  { width: 40px;  height: 40px; }
.dga-avatar--32  { width: 32px;  height: 32px; }
```

---

## Featured Icon

A container with a colored icon — used in cards, banners, empty states.

### Sizes
| Size | Container | Icon |
|------|-----------|------|
| `xl` | 56×56 | 28×28 |
| `lg` | 48×48 | 24×24 |
| `md` | 40×40 | 20×20 |
| `sm` | 32×32 | 16×16 |

### CSS
```css
.featured-icon {
  display: flex;
  width: 40px; height: 40px;  /* md default */
  justify-content: center;
  align-items: center;
  border-radius: var(--radius-sm); /* 4px */
}

/* Circle variant */
.featured-icon--circle { border-radius: var(--radius-full); }

/* Size classes */
.featured-icon--xl { width: 56px; height: 56px; }
.featured-icon--lg { width: 48px; height: 48px; }
.featured-icon--md { width: 40px; height: 40px; }
.featured-icon--sm { width: 32px; height: 32px; }
```

### Color/style variants
```css
/* Light (colored bg, colored icon — most common) */
.featured-icon--light-brand   { color: var(--text-success);  background-color: var(--background-brand-light); }
.featured-icon--light-gray    { color: var(--text-display);  background-color: var(--background-neutral-50); }
.featured-icon--light-error   { color: var(--text-error);    background-color: var(--background-error-light); }
.featured-icon--light-warning { color: var(--text-warning);  background-color: var(--background-warning-light); }
.featured-icon--light-success { color: var(--text-success);  background-color: var(--background-success-light); }
.featured-icon--light-info    { color: var(--icon-info);     background-color: var(--background-info-light); }

/* Dark (white icon on colored bg) */
.featured-icon--dark-brand    { color: #fff; background-color: var(--text-success); }
.featured-icon--dark-error    { color: #fff; background-color: var(--background-error); }
.featured-icon--dark-success  { color: #fff; background-color: var(--background-success); }

/* Outlined (border only, transparent bg) */
.featured-icon--outlined-brand   { border: 1px solid var(--border-success); color: var(--text-success); background: transparent; }
.featured-icon--outlined-error   { border: 1px solid var(--border-error);   color: var(--text-error);   background: transparent; }
```

### Implementation example
```html
<!-- Light brand, medium, circle -->
<div class="featured-icon featured-icon--md featured-icon--circle featured-icon--light-brand">
  <svg width="20" height="20"><!-- icon SVG --></svg>
</div>
```

---

## Accordion

```css
.accordion-item {
  border-top: 1px solid var(--border-neutral-primary);
  width: 100%;
  position: relative;
}
/* Last item gets a bottom border too */
.accordion-item:last-child { border-bottom: 1px solid var(--border-neutral-primary); }

.accordion-item__header {
  display: flex;
  padding: var(--spacing-xl);   /* 24px — lg size */
  align-items: center;
  justify-content: space-between;
  gap: var(--spacing-xl);
  cursor: pointer;
  border: 2px solid transparent;
  user-select: none;
}

.accordion-item__header:hover {
  background: var(--button-background-neutral-hovered);
}
.accordion-item__header:focus-visible {
  border: 2px solid var(--border-black);
  outline: none;
}
.accordion-item__header:active {
  background-color: var(--button-background-neutral-pressed);
}

.accordion-item__title {
  color: var(--text-default);
  font: 500 16px/24px "IBMPlexSansArabic";
  flex: 1;
}

/* Arrow — rotates 180° when open */
.accordion-item__arrow {
  width: 16px; height: 16px;
  transition: transform 0.3s ease-in-out;
}
.accordion-item.active .accordion-item__arrow { transform: rotate(180deg); }

/* Body — animated open/close */
.accordion-item__body {
  max-height: 0;
  overflow: hidden;
  opacity: 0;
  transition: max-height 0.3s ease-in-out, opacity 0.3s ease-in-out, padding 0.3s;
  padding: 0 var(--spacing-xl);
  color: var(--text-primary-paragraph);
  font: 400 14px/20px "IBMPlexSansArabic";
}
.accordion-item.active .accordion-item__body {
  max-height: 2000px;
  opacity: 1;
  padding: var(--spacing-md) var(--spacing-xl) var(--spacing-3xl);
}

/* Sizes */
.accordion-item--lg .accordion-item__header { padding: var(--spacing-xl); }
.accordion-item--md .accordion-item__header { padding: var(--spacing-lg) var(--spacing-xl); }
.accordion-item--sm .accordion-item__header { padding: var(--spacing-md) var(--spacing-xl); }

/* Disabled */
.accordion-item.disabled .accordion-item__title,
.accordion-item.disabled .accordion-item__arrow { color: var(--text-default-disabled) !important; }
.accordion-item.disabled .accordion-item__header:hover { background: transparent; }
```
