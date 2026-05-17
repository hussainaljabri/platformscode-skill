---
name: dga-page-content
description: DGA Content and Article page template
metadata:
  tags: dga, article, content, toc, template
---


## SOURCE
Figma: https://www.figma.com/design/QOMlLbvdxlWGgUpo7tkygc/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Breadcrumbs** — DgaBreadcrumbs
**Article Header** — Heading, DgaTag (category), DgaAvatar (author), metadata (date, read time)
**Table of Contents** — DgaTableOfContent (sidebar, sticky)
**Article Body** — DgaDivider between sections, DgaInlineAlert for callouts
**Share / Actions** — DgaButton (share), DgaLink
**Related Content** — DgaCard grid (3 related articles)
**Rating Section** — DgaRating (page satisfaction)
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaBreadcrumbs, DgaTag,
  DgaAvatar, DgaCard, DgaButton, DgaLink, DgaRating,
  DgaInlineAlert, DgaDivider, DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';
import { useState } from 'react';

export function ContentPage({ rtl = false, lang = 'en', article = null }) {
  const [rating, setRating] = useState(0);

  const t = {
    readTime:  lang === 'ar' ? 'دقيقة للقراءة' : 'min read',
    author:    lang === 'ar' ? 'بقلم'            : 'By',
    share:     lang === 'ar' ? 'مشاركة'          : 'Share',
    related:   lang === 'ar' ? 'مقالات ذات صلة'  : 'Related Articles',
    ratingQ:   lang === 'ar' ? 'هل كانت هذه الصفحة مفيدة؟' : 'Was this page helpful?',
    toc:       lang === 'ar' ? 'جدول المحتويات'  : 'Table of Contents',
  };

  const content = article || {
    title:      lang === 'ar' ? 'عنوان المقال' : 'Article Title',
    category:   lang === 'ar' ? 'الفئة'        : 'Category',
    date:       '2024-03-01',
    readTime:   5,
    author:     { name: lang === 'ar' ? 'اسم الكاتب' : 'Author Name', initials: 'AU' },
    sections: [
      { id: 'intro',   title: lang === 'ar' ? 'مقدمة'     : 'Introduction',   body: lang === 'ar' ? 'نص المقدمة هنا...' : 'Introduction content here...' },
      { id: 'details', title: lang === 'ar' ? 'التفاصيل'  : 'Details',        body: lang === 'ar' ? 'تفاصيل إضافية...' : 'Detailed content here...' },
      { id: 'summary', title: lang === 'ar' ? 'الخلاصة'   : 'Summary',        body: lang === 'ar' ? 'ملخص المقال...'   : 'Summary content here...' },
    ],
  };

  const related = [
    { title: lang === 'ar' ? 'مقال ذو صلة ١' : 'Related Article 1', href: '/article/1' },
    { title: lang === 'ar' ? 'مقال ذو صلة ٢' : 'Related Article 2', href: '/article/2' },
    { title: lang === 'ar' ? 'مقال ذو صلة ٣' : 'Related Article 3', href: '/article/3' },
  ];

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main style={{ padding: 'var(--spacing-8) 0' }}>
        <DgaGridContainer cols={12} gap="var(--spacing-6)">

          {/* Breadcrumbs */}
          <DgaGridItem colSpan={12}>
            <DgaBreadcrumbs items={[
              { label: lang === 'ar' ? 'الرئيسية' : 'Home', href: '/' },
              { label: content.category, href: '/category' },
              { label: content.title },
            ]} />
          </DgaGridItem>

          {/* Article Header */}
          <DgaGridItem colSpan={12}>
            <DgaTag label={content.category} style={{ marginBottom: 'var(--spacing-3)' }} />
            <h1 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-4)' }}>{content.title}</h1>
            <div style={{ display: 'flex', alignItems: 'center', gap: 'var(--spacing-3)', color: 'var(--text-secondary)' }}>
              <DgaAvatar type="initials" initials={content.author.initials} size="sm" />
              <span>{t.author} {content.author.name}</span>
              <DgaDivider orientation="vertical" />
              <span>{content.date}</span>
              <DgaDivider orientation="vertical" />
              <span>{content.readTime} {t.readTime}</span>
              <DgaButton variant="subtle" size="sm" label={t.share}
                leadIcon={true} leadIconType="share-01"
                leadIconProps={{ variant: 'stroke', type: 'rounded', size: 16 }}
                onOnClick={() => navigator.share?.({ title: content.title, url: window.location.href })} />
            </div>
            <DgaDivider style={{ marginTop: 'var(--spacing-4)' }} />
          </DgaGridItem>

          {/* TOC + Body */}
          <DgaGridItem colSpan={3} style={{ position: 'sticky', top: 'var(--spacing-8)', alignSelf: 'flex-start' }}>
            <h4 style={{ marginBottom: 'var(--spacing-3)' }}>{t.toc}</h4>
            <ul style={{ listStyle: 'none', padding: 0 }}>
              {content.sections.map(s => (
                <li key={s.id} style={{ marginBottom: 'var(--spacing-2)' }}>
                  <DgaLink label={s.title} href={`#${s.id}`} size="medium" />
                </li>
              ))}
            </ul>
          </DgaGridItem>

          <DgaGridItem colSpan={9}>
            {content.sections.map((sec, i) => (
              <div key={sec.id} id={sec.id} style={{ marginBottom: 'var(--spacing-8)' }}>
                <h2 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-4)' }}>{sec.title}</h2>
                <p style={{ color: 'var(--text-secondary)', lineHeight: '1.7' }}>{sec.body}</p>
                {i < content.sections.length - 1 && <DgaDivider style={{ marginTop: 'var(--spacing-6)' }} />}
              </div>
            ))}

            {/* Rating */}
            <div style={{ textAlign: 'center', padding: 'var(--spacing-6)', background: 'var(--background-secondary)', borderRadius: 'var(--radius-md)', marginTop: 'var(--spacing-8)' }}>
              <p style={{ fontWeight: 600, marginBottom: 'var(--spacing-3)' }}>{t.ratingQ}</p>
              <DgaRating value={rating} max={5} size="md" onRatingChange={e => setRating(e.detail)} />
            </div>
          </DgaGridItem>

          {/* Related Articles */}
          <DgaGridItem colSpan={12} style={{ marginTop: 'var(--spacing-8)' }}>
            <h2 style={{ marginBottom: 'var(--spacing-6)' }}>{t.related}</h2>
          </DgaGridItem>
          {related.map((r, i) => (
            <DgaGridItem key={i} colSpan={4}>
              <DgaCard>
                <DgaTag label={content.category} />
                <h3 style={{ margin: 'var(--spacing-3) 0' }}>{r.title}</h3>
                <DgaLink label={lang === 'ar' ? 'اقرأ المزيد' : 'Read More'} href={r.href} />
              </DgaCard>
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
<ContentPage rtl={true} lang="ar" />
```
