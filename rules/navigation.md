---
name: platformscode-navigation
description: Navigation visual specs — header (72px), breadcrumbs, tabs — CSS and anatomy
metadata:
  tags: platformscode, navigation, header, breadcrumbs, tabs, css, design-spec
---

Source CSS: `@platformscode/core/dist/collection/components/dga-header/`
Figma: https://www.figma.com/design/YGYwsEgALgfns9Maj8UbHX/

---

## Header

### Anatomy
```
┌─────────────────────────────────────────────────────────┐  72px height
│ [Logo]    [Nav item] [Nav item] [Nav item]    [Actions] │
└─────────────────────────────────────────────────────────┘
             ↑ active item has green 8px pill at bottom
```

### CSS
```css
.header {
  position: relative;
  width: 100%;
  height: 72px;
  min-height: 72px;
  display: flex;
  z-index: 99;
  background-color: var(--background-menu);
}

.header--sticky {
  position: sticky;
  top: 0;
}

/* Bottom separator */
.header--divider::after {
  content: "";
  position: absolute;
  bottom: 0; left: 0;
  height: 1px; width: 100%;
  background-color: var(--background-neutral-300);
}

/* Inner nav container */
.header-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 72px;
  width: 100%;
  max-width: 1280px;
  margin-inline: auto;
  padding-inline: var(--spacing-4xl);
  box-sizing: border-box;
}
```

### Nav item
```css
.header-menu__item {
  display: inline-flex;
  height: 72px;
  padding: var(--spacing-md) var(--spacing-3xl);
  justify-content: center;
  align-items: center;
  gap: var(--spacing-xs);
  background-color: transparent;
  cursor: pointer;
  position: relative;
}

.header-menu__item:hover {
  background: var(--button-background-neutral-hovered);
}

/* Active indicator — green pill at bottom */
.header-menu__item--active::after,
.header-menu__item:hover::after {
  content: "";
  display: block;
  width: calc(100% - 24px);
  height: 8px;
  border-radius: var(--radius-full);
  position: absolute;
  bottom: 0; left: 50%;
  transform: translateX(-50%);
  background-color: var(--colors-primary-sa-flag-600); /* #1f7a4f */
}

.header-menu__item--active::after { background-color: var(--colors-primary-sa-flag-600); }
.header-menu__item:hover::after { background-color: var(--background-neutral-400); }

/* Label text */
.header-menu__item-label {
  font: 500 14px/20px "IBMPlexSansArabic";
  color: var(--text-default);
}
```

### Mobile (below 900px)
```css
@media (max-width: 56.25em) {
  .header-nav__menu,
  .header-nav__actions { display: none; }
  .header-nav__mobile-actions { display: flex; } /* hamburger */
}
```

---

## Breadcrumbs

### Anatomy
```
Home  /  Section  /  Current Page
  ↑ links    ↑ separator   ↑ plain text (active)
```

### CSS
```css
.breadcrumbs {
  display: flex;
  align-items: center;
  gap: var(--spacing-xs); /* 4px */
  flex-wrap: wrap;
}

.breadcrumbs__item {
  display: flex;
  align-items: center;
  gap: var(--spacing-xs);
}

.breadcrumbs__link {
  font: 400 14px/20px "IBMPlexSansArabic";
  color: var(--text-secondary);
  text-decoration: none;
  cursor: pointer;
}
.breadcrumbs__link:hover {
  color: var(--text-default);
  text-decoration: underline;
}

.breadcrumbs__current {
  font: 500 14px/20px "IBMPlexSansArabic";
  color: var(--text-default);
}

.breadcrumbs__separator {
  color: var(--text-secondary);
  font-size: 14px;
  user-select: none;
}

/* RTL — separator flips automatically with dir="rtl" */
```

---

## Tabs

### Anatomy
```
[Tab A]  [Tab B]  [Tab C]
─────────────────────────  1px bottom border
         ↑ active tab has brand-colored 2px bottom border
```

### CSS
```css
.tabs {
  display: flex;
  border-bottom: 1px solid var(--border-neutral-primary);
  gap: 0;
}

.tab-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-xs);
  padding: var(--spacing-md) var(--spacing-xl); /* 12px 24px */
  cursor: pointer;
  font: 500 14px/20px "IBMPlexSansArabic";
  color: var(--text-secondary);
  border-bottom: 2px solid transparent;
  margin-bottom: -1px; /* overlap the container border */
  white-space: nowrap;
  transition: color 0.15s, border-color 0.15s;
}

.tab-item:hover {
  color: var(--text-default);
  background: var(--button-background-neutral-hovered);
}

.tab-item--active {
  color: var(--text-success);                     /* brand green */
  border-bottom-color: var(--colors-primary-sa-flag-600);
}

.tab-item:disabled,
.tab-item--disabled {
  color: var(--text-default-disabled);
  pointer-events: none;
}
```

### Vertical tabs
```css
.tabs--vertical {
  flex-direction: column;
  border-bottom: none;
  border-inline-end: 1px solid var(--border-neutral-primary);
}
.tabs--vertical .tab-item {
  border-bottom: none;
  border-inline-end: 2px solid transparent;
  margin-bottom: 0;
  margin-inline-end: -1px;
}
.tabs--vertical .tab-item--active {
  border-inline-end-color: var(--colors-primary-sa-flag-600);
}
```
