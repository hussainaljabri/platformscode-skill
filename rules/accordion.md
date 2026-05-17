---
name: platformscode-accordion
description: Accordion component — border-top separator, expand/collapse animation, single or multi-panel
metadata:
  tags: platformscode, accordion, collapse, expand, animation
---

Figma source: https://www.figma.com/design/ejgmxM1qWJQFZ7kBMdfZP8/

## Anatomy

```
┌─────────────────────────────────────────────────────────┐
│  Section title                                    [∨]   │  ← trigger (full-width button)
├─────────────────────────────────────────────────────────┤  ← border-top separator (open state)
│  Panel content — text, nested components, forms...      │  ← collapsible panel
└─────────────────────────────────────────────────────────┘
```

- Separator is `border-top: 1px solid var(--border-primary)` — only visible when panel is **open**
- The chevron rotates 180° when expanded
- Panels stack vertically with a `border-bottom: 1px solid var(--border-primary)` between items

---

## Design spec

### Container

```css
.accordion {
  border: 1px solid var(--border-primary);
  border-radius: var(--radius-md);    /* 8px */
  overflow: hidden;
}
```

### Accordion item

```css
.accordion-item {
  border-bottom: 1px solid var(--border-primary);
}
.accordion-item:last-child {
  border-bottom: none;
}
```

### Trigger button

```css
.accordion-trigger {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 16px 20px;
  background: none;
  border: none;
  cursor: pointer;
  font: 500 14px/20px "IBM Plex Sans Arabic", sans-serif;
  color: var(--text-primary);
  text-align: start;
  transition: background 0.15s;
}
.accordion-trigger:hover {
  background: var(--background-secondary);  /* --colors-neutral-50 */
}
.accordion-trigger:focus-visible {
  outline: 3px solid var(--colors-primary-sa-flag-300);
  outline-offset: -3px;
}
```

### Chevron icon

```css
.accordion-chevron {
  flex-shrink: 0;
  color: var(--text-secondary);
  transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}
.accordion-trigger[aria-expanded="true"] .accordion-chevron {
  transform: rotate(180deg);
}
```

### Collapsible panel

```css
.accordion-panel {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border-top: 0px solid var(--border-primary);
}
.accordion-panel.open {
  max-height: 800px;           /* large enough for any realistic content */
  border-top-width: 1px;
}
```

### Panel inner content

```css
.accordion-panel-inner {
  padding: 16px 20px 20px;
  font: 400 14px/20px "IBM Plex Sans Arabic", sans-serif;
  color: var(--text-secondary);
}
```

---

## Sizes

| Size | Trigger padding | Font size |
|------|----------------|-----------|
| sm   | 12px 16px       | 13px/18px |
| md   | 16px 20px       | 14px/20px ← default |
| lg   | 20px 24px       | 16px/24px |

---

## HTML pattern

```html
<div class="accordion" role="list">

  <div class="accordion-item" role="listitem">
    <button
      class="accordion-trigger"
      aria-expanded="false"
      aria-controls="panel-1"
      onclick="toggleAccordion(this)"
    >
      <span>Section title</span>
      <svg class="accordion-chevron" width="16" height="16" viewBox="0 0 24 24"
           fill="none" stroke="currentColor" stroke-width="2.5">
        <polyline points="6 9 12 15 18 9"/>
      </svg>
    </button>
    <div class="accordion-panel" id="panel-1">
      <div class="accordion-panel-inner">
        Panel content goes here.
      </div>
    </div>
  </div>

  <div class="accordion-item" role="listitem">
    <button
      class="accordion-trigger"
      aria-expanded="true"
      aria-controls="panel-2"
      onclick="toggleAccordion(this)"
    >
      <span>Another section (open by default)</span>
      <svg class="accordion-chevron" width="16" height="16" viewBox="0 0 24 24"
           fill="none" stroke="currentColor" stroke-width="2.5">
        <polyline points="6 9 12 15 18 9"/>
      </svg>
    </button>
    <div class="accordion-panel open" id="panel-2">
      <div class="accordion-panel-inner">
        This panel starts open.
      </div>
    </div>
  </div>

</div>
```

---

## JavaScript

```js
function toggleAccordion(trigger) {
  const panel   = document.getElementById(trigger.getAttribute('aria-controls'));
  const isOpen  = trigger.getAttribute('aria-expanded') === 'true';

  // For single-expand (accordion behaviour), close all others first:
  // document.querySelectorAll('.accordion-trigger[aria-expanded="true"]').forEach(t => {
  //   if (t !== trigger) collapseAccordion(t);
  // });

  if (isOpen) {
    trigger.setAttribute('aria-expanded', 'false');
    panel.classList.remove('open');
  } else {
    trigger.setAttribute('aria-expanded', 'true');
    panel.classList.add('open');
  }
}
```

### prefers-reduced-motion

```css
@media (prefers-reduced-motion: reduce) {
  .accordion-panel     { transition: none; }
  .accordion-chevron   { transition: none; }
  .accordion-trigger   { transition: none; }
}
```

---

## RTL

Trigger uses `text-align: start` so it respects `dir`. The chevron stays at `inline-end` automatically via `justify-content: space-between`. No extra CSS needed.
