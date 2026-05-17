---
name: platformscode-feedback
description: Feedback component specs — inline alert (left accent bar), modal (600px, blurred backdrop), notification
metadata:
  tags: platformscode, alert, modal, notification, css, design-spec
---

Source CSS: `@platformscode/core/dist/collection/components/dga-inline-alert/` and `dga-modal/`
Figma: https://www.figma.com/design/YGYwsEgALgfns9Maj8UbHX/

---

## Inline Alert

### Anatomy
```
┌──┬──────────────────────────────────────────┐
│  │ [icon]  Title text                        │
│  │         Supporting message text           │
│  │                          [action buttons] │
└──┴──────────────────────────────────────────┘
↑ 8px colored left accent bar (flips to right for RTL)
```

### CSS
```css
.alert {
  display: flex;
  width: 100%;
  padding: var(--spacing-xl) var(--spacing-3xl);  /* 24px 40px */
  flex-direction: column;
  gap: var(--spacing-xl);                          /* 24px */
  border-radius: var(--radius-md);                 /* 8px */
  background: var(--colors-base-white);
  border: 1px solid var(--border-neutral-primary);
  position: relative;
  overflow: hidden;
}

/* Left accent bar */
.alert::after {
  content: "";
  display: block;
  height: 100%;
  width: 8px;
  position: absolute;
  left: 0; top: 0;
}

/* RTL — bar flips to right */
html[dir="rtl"] .alert::after,
html[lang="ar"] .alert::after { right: 0; left: auto; }

.alert__header {
  display: flex;
  align-items: flex-start;
  gap: var(--spacing-lg); /* 18px */
  width: 100%;
}

.alert__title {
  font: 600 14px/20px "IBMPlexSansArabic";
  color: var(--text-default);
  margin-bottom: var(--spacing-xs); /* 4px */
}

.alert__message {
  font: 400 14px/20px "IBMPlexSansArabic";
  color: var(--text-secondary);
}
```

### Type variants (accent bar color + optional tinted bg)

| Type | Bar color | Background |
|------|-----------|------------|
| `neutral` | `var(--background-neutral-200)` | white |
| `info` | `var(--background-info)` | white |
| `error` | `var(--background-error)` | white |
| `warning` | `var(--background-warning)` | white |
| `success` | `var(--background-success)` | white |

With tinted background:
```css
.alert--info-bg   { background: var(--background-info-25);    border-color: var(--border-info-light); }
.alert--error-bg  { background: var(--background-error-25);   border-color: var(--border-error-light); }
.alert--warning-bg{ background: var(--background-warning-25); border-color: var(--border-warning-light); }
.alert--success-bg{ background: var(--background-success-25); border-color: var(--border-success-light); }
```

---

## Modal

### Anatomy
```
┌─────────────────────────────────────────┐
│ Title                            [close] │  ← header
├─────────────────────────────────────────┤
│                                         │
│  Body content                           │  ← body
│                                         │
├─────────────────────────────────────────┤
│                [Cancel] [Confirm]        │  ← actions
└─────────────────────────────────────────┘
       ↑ 600px wide, centered, blurred backdrop
```

### CSS
```css
/* Backdrop */
dialog {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  inset: 0;
  width: 100%; height: 100%;
  z-index: 1000;
  background: rgba(0, 0, 0, 0);
  border: none;
}

dialog::backdrop {
  background: rgba(0, 0, 0, 0.47);
  backdrop-filter: blur(3.1px);
}

/* Scroll lock when open */
body.modal-open { overflow: hidden; }

/* Modal panel */
.modal {
  display: flex;
  flex-direction: column;
  gap: var(--card-lg-gap, 24px);
  width: 600px;
  padding: var(--spacing-3xl);           /* 40px */
  background-color: var(--background-white);
  border-radius: var(--radius-md);       /* 8px */
}

@media (max-width: 56.25em) {
  .modal { width: 100%; border-radius: 0; }
}

/* Header */
.modal__header {
  width: 100%;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
}

.modal__heading {
  font: 600 20px/30px "IBMPlexSansArabic";
  color: var(--text-display);
}

/* Body */
.modal__body {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);               /* 16px */
  color: var(--text-primary-paragraph);
  padding-bottom: var(--spacing-xl);    /* 24px */
}

/* Actions row */
.modal__actions {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
}

@media (max-width: 56.25em) {
  .modal__actions {
    flex-direction: column-reverse;
  }
  .modal__actions .btn { width: 100%; }
}
```

### Implementation (plain HTML)
```html
<!-- Trigger -->
<button class="btn btn--md btn--primary-brand" onclick="document.getElementById('my-modal').showModal()">
  Open Modal
</button>

<!-- Modal -->
<dialog id="my-modal">
  <div class="modal">
    <div class="modal__header">
      <h2 class="modal__heading">Modal Title</h2>
      <button class="btn btn--sm btn--subtle btn--icon" onclick="document.getElementById('my-modal').close()">
        <!-- × icon -->
      </button>
    </div>
    <div class="modal__body">
      <p>Modal content goes here.</p>
    </div>
    <div class="modal__actions">
      <button class="btn btn--md btn--secondary-outline" onclick="document.getElementById('my-modal').close()">Cancel</button>
      <button class="btn btn--md btn--primary-brand">Confirm</button>
    </div>
  </div>
</dialog>

<script>
// Close on backdrop click
document.getElementById('my-modal').addEventListener('click', function(e) {
  if (e.target === this) this.close();
});
</script>
```

---

## Loading Spinner

```css
/* Circular */
.loading--circular {
  width: 40px; height: 40px; /* md */
  border-radius: var(--radius-full);
  border: 3px solid var(--border-neutral-primary);
  border-top-color: var(--colors-primary-sa-flag-600);
  animation: spin 0.8s linear infinite;
}

@keyframes spin { to { transform: rotate(360deg); } }

/* Sizes */
.loading--sm { width: 24px; height: 24px; border-width: 2px; }
.loading--md { width: 40px; height: 40px; border-width: 3px; }
.loading--lg { width: 56px; height: 56px; border-width: 4px; }
.loading--xl { width: 72px; height: 72px; border-width: 4px; }
```
