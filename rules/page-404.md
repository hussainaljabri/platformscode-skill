---
name: dga-page-404
description: DGA Page Not Found (404) template
metadata:
  tags: dga, 404, error-page, template
---


## SOURCE
Figma: https://www.figma.com/design/e2vpOQ2Buy0hZasQ5h4sud/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Error Body** — DgaFeaturedIcon (error/large), Heading "404", subheading, DgaButton (go home), DgaLink (go back)
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaButton, DgaLink,
  DgaFeaturedIcon, DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

export function NotFoundPage({ rtl = false, lang = 'en' }) {
  const t = {
    heading:  lang === 'ar' ? 'الصفحة غير موجودة'                              : 'Page Not Found',
    sub:      lang === 'ar' ? 'عذرًا، الصفحة التي تبحث عنها غير موجودة أو تم نقلها.' : "Sorry, the page you're looking for doesn't exist or has been moved.",
    home:     lang === 'ar' ? 'العودة إلى الرئيسية'                             : 'Back to Home',
    back:     lang === 'ar' ? 'الرجوع للخلف'                                   : 'Go Back',
  };

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main style={{ padding: 'var(--spacing-20) 0', textAlign: 'center' }}>
        <DgaGridContainer cols={12} gap="var(--spacing-6)">
          <DgaGridItem colSpan={12}>

            <DgaFeaturedIcon icon="alert-circle" size="huge" color="error" style="light" circle={true} />

            <p style={{ fontSize: '96px', fontWeight: 700, color: 'var(--colors-primary-sa-flag-600)', margin: 'var(--spacing-4) 0 0' }}>
              404
            </p>

            <h1 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-4)' }}>
              {t.heading}
            </h1>

            <p style={{ color: 'var(--text-secondary)', maxWidth: '480px', margin: '0 auto var(--spacing-8)' }}>
              {t.sub}
            </p>

            <div style={{ display: 'flex', gap: 'var(--spacing-3)', justifyContent: 'center' }}>
              <DgaButton
                variant="primary-brand"
                size="md"
                label={t.home}
                leadIcon={true}
                leadIconType="home-01"
                leadIconProps={{ variant: 'stroke', type: 'rounded', size: 20 }}
                onOnClick={() => window.location.href = '/'}
              />
              <DgaButton
                variant="secondary-outline"
                size="md"
                label={t.back}
                onOnClick={() => window.history.back()}
              />
            </div>

          </DgaGridItem>
        </DgaGridContainer>
      </main>

      <DgaFooter />
    </div>
  );
}
```

## HTML
```html
<div dir="ltr">
  <dga-header></dga-header>
  <main style="text-align:center; padding:var(--spacing-20) 0">
    <dga-featured-icon icon="alert-circle" size="huge" color="error" style="light" circle="true"></dga-featured-icon>
    <p style="font-size:96px;font-weight:700;color:var(--colors-primary-sa-flag-600)">404</p>
    <h1>Page Not Found</h1>
    <p style="color:var(--text-secondary)">The page you're looking for doesn't exist.</p>
    <dga-button id="home" variant="primary-brand" size="md" label="Back to Home"></dga-button>
  </main>
  <dga-footer></dga-footer>
</div>
```

## RTL
```tsx
<NotFoundPage rtl={true} lang="ar" />
```
