---
name: dga-page-sitemap
description: DGA Site Map page template
metadata:
  tags: dga, sitemap, navigation, template
---


## SOURCE
Figma: https://www.figma.com/design/kYHATLdDX5T40nHQ1XB3T4/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Breadcrumbs** — DgaBreadcrumbs
**Page Title** — Heading + description
**Sitemap Grid** — DgaGridContainer, DgaGridItem, DgaLink, DgaDivider
  - Organized by section (each column = a category)
  - Category heading + list of DgaLink items
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaBreadcrumbs, DgaLink,
  DgaGridContainer, DgaGridItem, DgaDivider,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

const SITE_MAP = [
  {
    category: { en: 'Home', ar: 'الرئيسية' },
    links: [
      { en: 'Portal Home', ar: 'الصفحة الرئيسية', href: '/' },
      { en: 'News', ar: 'الأخبار', href: '/news' },
      { en: 'Announcements', ar: 'الإعلانات', href: '/announcements' },
    ],
  },
  {
    category: { en: 'Services', ar: 'الخدمات' },
    links: [
      { en: 'All Services', ar: 'جميع الخدمات', href: '/services' },
      { en: 'E-Services', ar: 'الخدمات الإلكترونية', href: '/e-services' },
      { en: 'Service Status', ar: 'حالة الخدمة', href: '/status' },
    ],
  },
  {
    category: { en: 'About', ar: 'من نحن' },
    links: [
      { en: 'About the Entity', ar: 'عن الجهة', href: '/about' },
      { en: 'Leadership', ar: 'القيادة', href: '/leadership' },
      { en: 'Organizational Structure', ar: 'الهيكل التنظيمي', href: '/structure' },
      { en: 'Vision & Mission', ar: 'الرؤية والرسالة', href: '/vision' },
    ],
  },
  {
    category: { en: 'Resources', ar: 'الموارد' },
    links: [
      { en: 'Publications', ar: 'المنشورات', href: '/publications' },
      { en: 'Reports', ar: 'التقارير', href: '/reports' },
      { en: 'Policies', ar: 'السياسات', href: '/policies' },
      { en: 'Data', ar: 'البيانات', href: '/data' },
    ],
  },
  {
    category: { en: 'Support', ar: 'الدعم' },
    links: [
      { en: 'Help Center', ar: 'مركز المساعدة', href: '/help' },
      { en: 'FAQ', ar: 'الأسئلة الشائعة', href: '/faq' },
      { en: 'Contact Us', ar: 'تواصل معنا', href: '/contact' },
    ],
  },
  {
    category: { en: 'Legal', ar: 'القانوني' },
    links: [
      { en: 'Privacy Policy', ar: 'سياسة الخصوصية', href: '/privacy' },
      { en: 'Terms of Use', ar: 'شروط الاستخدام', href: '/terms' },
      { en: 'Accessibility', ar: 'إمكانية الوصول', href: '/accessibility' },
    ],
  },
];

export function SiteMapPage({ rtl = false, lang = 'en' }) {
  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main style={{ padding: 'var(--spacing-8) 0' }}>
        <DgaGridContainer cols={12} gap="var(--spacing-6)">

          <DgaGridItem colSpan={12}>
            <DgaBreadcrumbs items={[
              { label: lang === 'ar' ? 'الرئيسية' : 'Home', href: '/' },
              { label: lang === 'ar' ? 'خريطة الموقع' : 'Site Map' },
            ]} />
          </DgaGridItem>

          <DgaGridItem colSpan={12}>
            <h1 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-2)' }}>
              {lang === 'ar' ? 'خريطة الموقع' : 'Site Map'}
            </h1>
            <p style={{ color: 'var(--text-secondary)', marginBottom: 'var(--spacing-8)' }}>
              {lang === 'ar' ? 'نظرة عامة على جميع صفحات الموقع' : 'An overview of all pages on this site'}
            </p>
            <DgaDivider />
          </DgaGridItem>

          {SITE_MAP.map((section, i) => (
            <DgaGridItem key={i} colSpan={4} style={{ marginBottom: 'var(--spacing-6)' }}>
              <h3 style={{
                color: 'var(--colors-primary-sa-flag-600)',
                marginBottom: 'var(--spacing-4)',
                paddingBottom: 'var(--spacing-2)',
                borderBottom: '2px solid var(--colors-primary-sa-flag-200)',
              }}>
                {lang === 'ar' ? section.category.ar : section.category.en}
              </h3>
              <ul style={{ listStyle: 'none', padding: 0, margin: 0 }}>
                {section.links.map((link, j) => (
                  <li key={j} style={{ marginBottom: 'var(--spacing-2)' }}>
                    <DgaLink
                      label={lang === 'ar' ? link.ar : link.en}
                      href={link.href}
                      style="primary"
                      size="medium"
                    />
                  </li>
                ))}
              </ul>
            </DgaGridItem>
          ))}

        </DgaGridContainer>
      </main>
      <DgaFooter />
    </div>
  );
}
```

## RTL
```tsx
<SiteMapPage rtl={true} lang="ar" />
```
