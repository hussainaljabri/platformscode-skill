---
name: dga-page-contact
description: DGA Contact Us page template
metadata:
  tags: dga, contact, form, template
---


## SOURCE
Figma: https://www.figma.com/design/jsFkhS8d9haJrdJWQd6Ra7/

---

## PAGE SECTIONS & COMPONENTS (from Figma)

### Contact Us Tempate - قالب صفحة  التواصل

**Contact us - EN** (FRAME)
  DGA components: DgaNavHeader, DgaFooter
  - Backround (FRAME)
  - Digital Stamp (INSTANCE)
  - Second Nav Header (INSTANCE)
  - Nav Header-2 (FRAME)
  - Contact Us (FRAME)
  - Feedback (FRAME)
  - Footer (INSTANCE)

**Contact us - AR** (FRAME)
  DGA components: DgaNavHeader, DgaFooter
  - Backround (FRAME)
  - Digital Stamp (INSTANCE)
  - Second Nav Header (INSTANCE)
  - Nav Header (FRAME)
  - Contact Us (FRAME)
  - Feedback (FRAME)
  - Footer (INSTANCE)

**Contact us - AR** (FRAME)
  DGA components: DgaNavHeader, DgaFooter
  - Digital Stamp (INSTANCE)
  - Background (FRAME)
  - Nav Header (INSTANCE)
  - Contact Us (FRAME)
  - Feedback Section (FRAME)
  - Footer (INSTANCE)

**Design system header** (INSTANCE)
  - Content (FRAME)

**Design system header** (INSTANCE)
  - Content (FRAME)

**Contact us - EN** (FRAME)
  DGA components: DgaNavHeader, DgaFooter
  - Digital Stamp (INSTANCE)
  - Background (FRAME)
  - Nav Header (INSTANCE)
  - Contact Us (FRAME)
  - Feedback (FRAME)
  - Footer (INSTANCE)

**Design system header** (INSTANCE)
  - Content (FRAME)


---

## RULES
1. Never use plain `<button>`, `<input>`, `<select>`, `<textarea>` — use DGA equivalents
2. CSS once at app root: `import 'platformscode-new-react/dist/style.css'`
3. All button click events: `onOnClick` (not `onClick`)
4. Colors/spacing from CSS tokens only — no hardcoded hex values
5. `DgaHeader` takes a `config` object — not children slots
6. `DgaModal` requires a `name` prop + uses `buttonsList` array
7. `DgaTabs` takes `tabsList` array — not children
8. RTL: add `dir="rtl"` to root element; design system handles mirroring

---

## REACT TEMPLATE

```tsx
import {
  DgaNavHeader,
  DgaFooter
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

interface ContactUsPageProps {
  rtl?: boolean;
  lang?: 'en' | 'ar';
}

export function ContactUsPage({ rtl = false, lang = 'en' }: ContactUsPageProps) {
  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader
        config={{
          logo: '/logo.png',
          menuItems: [],
          actions: [],
          rtl,
        }}
      />

      <main style={{ padding: 'var(--spacing-8) 0' }}>
        <DgaGridContainer cols={12} gap="var(--spacing-6)">
          {/*
            Build each section below based on the Figma structure above.
            Replace placeholder comments with actual DGA components.
          */}

          {/* ── Contact us - EN ── */}
          {/* Components: DgaNavHeader, DgaFooter */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Contact us - EN */}
          </DgaGridItem>

          {/* ── Contact us - AR ── */}
          {/* Components: DgaNavHeader, DgaFooter */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Contact us - AR */}
          </DgaGridItem>

          {/* ── Design system header ── */}
          {/* Components: layout only */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Design system header */}
          </DgaGridItem>
        </DgaGridContainer>
      </main>

      <DgaFooter />
    </div>
  );
}
```

---

## HTML / WEB COMPONENTS TEMPLATE

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="UTF-8" />
  <link rel="stylesheet" href="node_modules/@platformscode/core/dist/core/core.css" />
</head>
<body>
  <dga-header></dga-header>

  <main style="padding: var(--spacing-8) 0">
    <dga-grid-container cols="12" gap="var(--spacing-6)">

      <!-- Contact us - EN | Components: DgaNavHeader, DgaFooter -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Contact us - EN -->
      </dga-grid-item>

      <!-- Contact us - AR | Components: DgaNavHeader, DgaFooter -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Contact us - AR -->
      </dga-grid-item>

      <!-- Design system header | Components: layout -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Design system header -->
      </dga-grid-item>
    </dga-grid-container>
  </main>

  <dga-footer></dga-footer>

  <script type="module">
    import { defineCustomElements } from './node_modules/@platformscode/core/loader/index.es2017.js';
    defineCustomElements();
  </script>
</body>
</html>
```

---

## RTL / ARABIC

```tsx
// React:
<ContactUsPage rtl={true} lang="ar" />

// HTML: change opening tags to:
// <html lang="ar" dir="rtl">
```
