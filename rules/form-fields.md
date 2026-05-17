---
name: platformscode-form-fields
description: Form field visual specs — input, dropdown, checkbox, switch, radio — CSS and anatomy
metadata:
  tags: platformscode, form, input, checkbox, dropdown, switch, radio, css, design-spec
---

Source CSS: `@platformscode/core/dist/collection/components/dga-*/`
Figma: https://www.figma.com/design/YGYwsEgALgfns9Maj8UbHX/

---

## Text Input

### Anatomy
```
[Label text]
┌──────────────────────────────────────┐
│ [prefix icon?]  placeholder text  [suffix?] │
└──────────────────────────────────────┘
[Helper text / error message]
```

### CSS
```css
.field-wrapper {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs); /* 4px between label and input */
  width: 100%;
}

.field-label {
  font: 500 14px/20px "IBMPlexSansArabic";
  color: var(--text-default);
}

.field-input {
  height: 40px;                        /* md size */
  width: 100%;
  padding-inline: var(--spacing-xl);   /* 24px */
  border-radius: var(--radius-sm);     /* 4px */
  border: 1px solid var(--form-field-border-default);
  background-color: var(--form-field-background-default);
  color: var(--form-field-text-default);
  font: 400 14px/20px "IBMPlexSansArabic";
  box-sizing: border-box;
  outline: none;
  transition: border-color 0.2s;
}

.field-input::placeholder {
  color: var(--form-field-text-placeholder);
}

.field-input:hover {
  border-color: var(--form-field-border-hovered);
}

.field-input:focus {
  border-color: var(--form-field-border-pressed);
  border-bottom-width: 2px;
}

.field-input:disabled {
  border-color: var(--colors-gray-neutral-300);
  color: var(--form-field-text-placeholder);
  cursor: not-allowed;
}
```

### Sizes
| Size | Height | Font |
|------|--------|------|
| `sm` | 32px | 12px/18px |
| `md` | 40px | 14px/20px |
| `lg` | 48px | 16px/24px |

### Error state
```css
.field-input--error {
  border-color: var(--border-error);
}
.field-helper--error {
  color: var(--text-error);
  font: 400 12px/18px "IBMPlexSansArabic";
}
```

---

## Dropdown / Select

### CSS
```css
.dropdown {
  display: flex;
  flex-direction: column;
  width: 100%;
  min-width: 200px;
  position: relative;
  border-radius: var(--radius-sm);
}

.dropdown__btn {
  cursor: pointer;
  min-height: 40px;
  width: 100%;
  border-radius: var(--radius-sm);    /* 4px */
  border: 1px solid var(--form-field-border-default);
  background-color: var(--form-field-background-default);
  padding-inline: var(--spacing-xl);  /* 24px */
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: var(--form-field-text-placeholder);
  font: 400 14px/20px "IBMPlexSansArabic";
}

.dropdown__btn:hover { border-color: var(--form-field-border-hovered); }

/* Animated bottom border on open */
.dropdown__btn::after {
  content: "";
  position: absolute;
  bottom: 0; left: 50%;
  width: 0%; height: 2px;
  transform: translateX(-50%);
  background-color: var(--form-field-border-pressed);
  transition: width 0.2s ease-in-out;
}
.dropdown__btn.open::after { width: 100%; }

/* Rotated chevron on open */
.dropdown__btn.open .dropdown__chevron { transform: rotate(180deg) translateY(50%); }

.dropdown__list {
  display: flex;
  padding: var(--spacing-md);
  flex-direction: column;
  border-radius: var(--radius-sm);
  border: 1px solid var(--border-neutral-primary);
  background: var(--form-field-background-default);
  position: absolute;
  left: 0; right: 0; top: 42px;
  z-index: 100;
  box-shadow: var(--shadow-md);
}
```

---

## Checkbox

### Anatomy
```
[checkbox box 24×24] [Label text]
                     [Helper text — optional]
```

### CSS
```css
.checkbox {
  display: flex;
  gap: var(--spacing-xl); /* 24px */
  cursor: pointer;
  user-select: none;
  width: fit-content;
}

.checkbox-container {
  width: 24px; height: 24px;
  min-width: 24px;
  border-radius: var(--radius-xs); /* 2px */
  border: 1px solid var(--controls-control-border);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  background: transparent;
  transition: background-color 0.15s;
}

/* Checked state */
input:checked ~ .checkbox-container {
  background-color: var(--controls-control-neutral-checked);
  border-color: var(--controls-control-neutral-checked);
}

/* Hover ripple effect */
.checkbox-container::after {
  content: "";
  border-radius: var(--radius-full);
  background: var(--controls-control-ripple-effect);
  width: 40px; height: 40px;
  position: absolute;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%) scale(0);
  transition: transform 0.3s ease-in-out;
  z-index: -1;
}
input:hover ~ .checkbox-container::after { transform: translate(-50%, -50%) scale(1); }

/* Disabled */
input:disabled ~ .checkbox-container {
  border-color: var(--border-disabled);
  background-color: var(--background-disabled);
}
```

### Sizes
| Size | Box dimension |
|------|--------------|
| `lg` | 24×24 |
| `md` | 20×20 |
| `sm` | 16×16 |

---

## Radio Button

Same pattern as checkbox but:
```css
.radio-container {
  border-radius: var(--radius-full); /* fully circular */
  width: 20px; height: 20px;
  border: 1px solid var(--controls-control-border);
}

input:checked ~ .radio-container {
  border-color: var(--controls-control-neutral-checked);
}

/* Inner dot when checked */
input:checked ~ .radio-container::before {
  content: "";
  width: 10px; height: 10px;
  border-radius: var(--radius-full);
  background: var(--controls-control-neutral-checked);
  position: absolute;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
}
```

---

## Switch / Toggle

### CSS
```css
.switch-track {
  width: 44px; height: 24px;
  border-radius: var(--radius-full);
  background: var(--controls-control-border);
  position: relative;
  cursor: pointer;
  transition: background-color 0.2s;
}

/* Checked */
.switch-track--checked {
  background-color: var(--controls-control-neutral-checked);
}

/* Thumb */
.switch-thumb {
  width: 20px; height: 20px;
  border-radius: var(--radius-full);
  background: white;
  position: absolute;
  top: 2px; left: 2px;
  transition: transform 0.2s;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}
.switch-track--checked .switch-thumb {
  transform: translateX(20px);
}

/* sm size */
.switch-track--sm { width: 36px; height: 20px; }
.switch-track--sm .switch-thumb { width: 16px; height: 16px; }
.switch-track--sm.switch-track--checked .switch-thumb { transform: translateX(16px); }

/* Disabled */
.switch-track--disabled {
  background: var(--background-disabled);
  cursor: not-allowed;
}
```

---

## Helper Text & Labels

```css
.field-label {
  font: 500 14px/20px "IBMPlexSansArabic";
  color: var(--text-default);
  margin-bottom: 4px;
}

.field-helper {
  font: 400 12px/18px "IBMPlexSansArabic";
  color: var(--text-secondary);
  margin-top: 4px;
}

.field-helper--error {
  color: var(--text-error);
}

/* Required asterisk */
.field-label .required { color: var(--text-error); margin-inline-start: 2px; }
```
