---
name: dga-page-home
description: DGA Home Page template
metadata:
  tags: dga, home, landing, hero, template
---


## SOURCE
Figma: https://www.figma.com/design/VjhvAXefnmgWMj4nBEShPM/

---

## PAGE SECTIONS & COMPONENTS (from Figma)

### Home Template - قالب الصفحة الرئيسية 

**Home Page - Desktop EN** (FRAME)
  DGA components: DgaFooter, DgaNavHeader
  - Digital Stamp (INSTANCE)
  - Nav Header-2 (FRAME)
  - Hero Section (FRAME)
  - About us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)
  - Feedback (FRAME)

**Home Page - Desktop AR** (FRAME)
  DGA components: DgaFooter, DgaNavHeader
  - Digital Stamp (INSTANCE)
  - Nav Header (FRAME)
  - Hero Section (FRAME)
  - About Us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)
  - Feedback Section (FRAME)

**Home Page - AR** (FRAME)
  DGA components: DgaNavHeader, DgaFooter
  - Digital Stamp (INSTANCE)
  - Nav Header (INSTANCE)
  - Hero Section (FRAME)
  - About Us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)
  - Feedback Section (FRAME)

**Footer** (FRAME)
  - Content (FRAME)

**Home Page - Desktop EN** (FRAME)
  DGA components: DgaFooter, DgaNavHeader
  - Digital Stamp (INSTANCE)
  - Nav Header-2 (FRAME)
  - Hero Section (FRAME)
  - About us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)
  - Feedback (FRAME)

**Home Page - Desktop AR** (FRAME)
  DGA components: DgaFooter, DgaNavHeader
  - Digital Stamp (INSTANCE)
  - Nav Header (FRAME)
  - Hero Section (FRAME)
  - About Us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)
  - Feedback Section (FRAME)

**Footer** (FRAME)
  - Content (FRAME)

**Home Page - Desktop EN** (FRAME)
  DGA components: DgaFooter, DgaNavHeader
  - Digital Stamp (INSTANCE)
  - Second Nav Header (INSTANCE)
  - Nav Header-2 (FRAME)
  - Hero Section (FRAME)
  - About us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)

**Home Page - Desktop** (FRAME)
  DGA components: DgaNavHeader, DgaFooter
  - Digital Stamp (INSTANCE)
  - Second Nav Header (INSTANCE)
  - Nav Header-2 (FRAME)
  - Hero Section (FRAME)
  - About us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)

**Footer** (FRAME)
  - Content (FRAME)

**Home Page - Desktop AR** (FRAME)
  DGA components: DgaFooter, DgaNavHeader
  - Digital Stamp (INSTANCE)
  - Second Nav Header (INSTANCE)
  - Nav Header (FRAME)
  - Hero Section (FRAME)
  - About Us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)

**Home Page - Desktop AR** (FRAME)
  DGA components: DgaFooter, DgaNavHeader
  - Digital Stamp (INSTANCE)
  - Second Nav Header (INSTANCE)
  - Nav Header (FRAME)
  - Hero Section (FRAME)
  - About Us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)

**Design system header** (INSTANCE)
  - Content (FRAME)

**Design system header** (INSTANCE)
  - Content (FRAME)

**Design system header** (INSTANCE)
  - Content (FRAME)

**Design system header** (INSTANCE)
  - Content (FRAME)

**Design system header** (INSTANCE)
  - Content (FRAME)

**Design system header** (INSTANCE)
  - Content (FRAME)

**Home page - EN** (FRAME)
  DGA components: DgaNavHeader, DgaFooter
  - Digital Stamp (INSTANCE)
  - Nav Header (INSTANCE)
  - Hero Section (FRAME)
  - About Us Section (FRAME)
  - Services Section (FRAME)
  - Articles and News Section (FRAME)
  - Partner Section (FRAME)
  - Feedback (FRAME)

**Footer** (FRAME)
  - Content (FRAME)

**Hero Section** (COMPONENT_SET)
  - RTL=No (COMPONENT)
  - RTL=Yes (COMPONENT)

**Card** (COMPONENT_SET)
  - RTL=No (COMPONENT)
  - RTL=Yes (COMPONENT)

**News Card** (COMPONENT_SET)
  - RTL=No (COMPONENT)
  - RTL=Yes (COMPONENT)

**Ai Logo** (COMPONENT_SET)
  - Style=Default (COMPONENT)
  - Style=White (COMPONENT)

**DGA - logo** (COMPONENT)
  - e4jjjukvk1dnxahckhrwjdup1wpq9m6q 1 (RECTANGLE)


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
  DgaFooter,
  DgaNavHeader
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

interface HomePagePageProps {
  rtl?: boolean;
  lang?: 'en' | 'ar';
}

export function HomePagePage({ rtl = false, lang = 'en' }: HomePagePageProps) {
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

          {/* ── Home Page - Desktop EN ── */}
          {/* Components: DgaFooter, DgaNavHeader */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Home Page - Desktop EN */}
          </DgaGridItem>

          {/* ── Home Page - Desktop AR ── */}
          {/* Components: DgaFooter, DgaNavHeader */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Home Page - Desktop AR */}
          </DgaGridItem>

          {/* ── Home Page - AR ── */}
          {/* Components: DgaNavHeader, DgaFooter */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Home Page - AR */}
          </DgaGridItem>

          {/* ── Footer ── */}
          {/* Components: layout only */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Footer */}
          </DgaGridItem>

          {/* ── Home Page - Desktop ── */}
          {/* Components: DgaNavHeader, DgaFooter */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Home Page - Desktop */}
          </DgaGridItem>

          {/* ── Design system header ── */}
          {/* Components: layout only */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Design system header */}
          </DgaGridItem>

          {/* ── Home page - EN ── */}
          {/* Components: DgaNavHeader, DgaFooter */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Home page - EN */}
          </DgaGridItem>

          {/* ── Hero Section ── */}
          {/* Components: layout only */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Hero Section */}
          </DgaGridItem>

          {/* ── Card ── */}
          {/* Components: layout only */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Card */}
          </DgaGridItem>

          {/* ── News Card ── */}
          {/* Components: layout only */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement News Card */}
          </DgaGridItem>

          {/* ── Ai Logo ── */}
          {/* Components: layout only */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement Ai Logo */}
          </DgaGridItem>

          {/* ── DGA - logo ── */}
          {/* Components: layout only */}
          <DgaGridItem colSpan={12}>
            {/* TODO: implement DGA - logo */}
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

      <!-- Home Page - Desktop EN | Components: DgaFooter, DgaNavHeader -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Home Page - Desktop EN -->
      </dga-grid-item>

      <!-- Home Page - Desktop AR | Components: DgaFooter, DgaNavHeader -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Home Page - Desktop AR -->
      </dga-grid-item>

      <!-- Home Page - AR | Components: DgaNavHeader, DgaFooter -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Home Page - AR -->
      </dga-grid-item>

      <!-- Footer | Components: layout -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Footer -->
      </dga-grid-item>

      <!-- Home Page - Desktop | Components: DgaNavHeader, DgaFooter -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Home Page - Desktop -->
      </dga-grid-item>

      <!-- Design system header | Components: layout -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Design system header -->
      </dga-grid-item>

      <!-- Home page - EN | Components: DgaNavHeader, DgaFooter -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Home page - EN -->
      </dga-grid-item>

      <!-- Hero Section | Components: layout -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Hero Section -->
      </dga-grid-item>

      <!-- Card | Components: layout -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Card -->
      </dga-grid-item>

      <!-- News Card | Components: layout -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement News Card -->
      </dga-grid-item>

      <!-- Ai Logo | Components: layout -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement Ai Logo -->
      </dga-grid-item>

      <!-- DGA - logo | Components: layout -->
      <dga-grid-item col-span="12">
        <!-- TODO: implement DGA - logo -->
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
<HomePagePage rtl={true} lang="ar" />

// HTML: change opening tags to:
// <html lang="ar" dir="rtl">
```
