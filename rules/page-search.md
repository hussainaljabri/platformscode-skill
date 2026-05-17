---
name: dga-page-search
description: DGA Search Results page with filters and pagination
metadata:
  tags: dga, search, results, filters, template
---


## SOURCE
Figma: https://www.figma.com/design/FNzX2d1cRTRhnzLIyKTAH5/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Search Bar** — DgaSearchBox (large, prominent)
**Filters Sidebar** — DgaCheckbox groups, DgaDropdown (sort), DgaDivider
**Results Count** — text + DgaTag (active filters)
**Results List** — DgaCard per result (title, excerpt, metadata, DgaLink)
**No Results State** — DgaFeaturedIcon + message
**Pagination** — DgaPagination
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaSearchBox, DgaDropdown,
  DgaCheckbox, DgaCard, DgaLink, DgaTag, DgaButton,
  DgaPagination, DgaFeaturedIcon, DgaLoading,
  DgaGridContainer, DgaGridItem, DgaDivider,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';
import { useState } from 'react';

export function SearchPage({ rtl = false, lang = 'en', initialQuery = '' }) {
  const [query, setQuery]     = useState(initialQuery);
  const [loading, setLoading] = useState(false);
  const [page, setPage]       = useState(1);
  const [results] = useState([
    { id: 1, title: 'Digital Government Services Guide', excerpt: 'Learn about the range of services available through the digital government portal...', category: 'Guide', date: '2024-01-15', href: '/guides/digital-services' },
    { id: 2, title: 'How to Register for E-Services', excerpt: 'A step-by-step guide to registering your account and accessing government services...', category: 'Tutorial', date: '2024-02-10', href: '/tutorials/register' },
    { id: 3, title: 'Privacy Policy Update', excerpt: 'Important updates to our privacy policy regarding data collection and usage...', category: 'Policy', date: '2024-03-01', href: '/policies/privacy' },
  ]);

  const t = {
    placeholder: lang === 'ar' ? 'ابحث...'           : 'Search...',
    results:     lang === 'ar' ? 'نتائج البحث'        : 'Search Results',
    count:       lang === 'ar' ? `${results.length} نتيجة لـ "${query}"` : `${results.length} results for "${query}"`,
    noResults:   lang === 'ar' ? 'لا توجد نتائج'      : 'No results found',
    sort:        lang === 'ar' ? 'ترتيب حسب'          : 'Sort by',
    filter:      lang === 'ar' ? 'تصفية النتائج'      : 'Filter Results',
    category:    lang === 'ar' ? 'الفئة'              : 'Category',
    readMore:    lang === 'ar' ? 'اقرأ المزيد'         : 'Read More',
  };

  const sortOptions = [
    { label: lang === 'ar' ? 'الأحدث'     : 'Most Recent',  value: 'recent' },
    { label: lang === 'ar' ? 'الأكثر صلة' : 'Most Relevant', value: 'relevant' },
    { label: lang === 'ar' ? 'الأقدم'     : 'Oldest',        value: 'oldest' },
  ];

  const categories = ['Guide', 'Tutorial', 'Policy', 'News'].map(c => ({ label: c, value: c.toLowerCase() }));

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main style={{ padding: 'var(--spacing-8) 0' }}>
        <DgaGridContainer cols={12} gap="var(--spacing-6)">

          {/* Search Bar */}
          <DgaGridItem colSpan={12} style={{ padding: 'var(--spacing-6) 0' }}>
            <DgaSearchBox
              placeholder={t.placeholder}
              value={query}
              onOnChange={e => setQuery(e.detail)}
              style={{ width: '100%' }}
            />
          </DgaGridItem>

          {query && (
            <DgaGridItem colSpan={12}>
              <p style={{ color: 'var(--text-secondary)' }}>{t.count}</p>
            </DgaGridItem>
          )}

          {/* Filters */}
          <DgaGridItem colSpan={3}>
            <div style={{ background: 'var(--background-secondary)', padding: 'var(--spacing-4)', borderRadius: 'var(--radius-md)' }}>
              <h3 style={{ marginBottom: 'var(--spacing-4)' }}>{t.filter}</h3>
              <DgaDivider />
              <div style={{ marginTop: 'var(--spacing-4)' }}>
                <p style={{ fontWeight: 600, marginBottom: 'var(--spacing-3)' }}>{t.category}</p>
                {categories.map(cat => (
                  <DgaCheckbox key={cat.value} label={cat.label} style={{ marginBottom: 'var(--spacing-2)' }} />
                ))}
              </div>
            </div>
          </DgaGridItem>

          {/* Results */}
          <DgaGridItem colSpan={9}>
            <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 'var(--spacing-4)' }}>
              <h2>{t.results}</h2>
              <DgaDropdown label={t.sort} options={sortOptions} style={{ width: '200px' }} />
            </div>

            {loading ? (
              <DgaLoading size="lg" style="circular" />
            ) : results.length === 0 ? (
              <div style={{ textAlign: 'center', padding: 'var(--spacing-12)' }}>
                <DgaFeaturedIcon icon="search-lg" size="large" color="brand" style="light" circle={true} />
                <p style={{ marginTop: 'var(--spacing-4)', color: 'var(--text-secondary)' }}>{t.noResults}</p>
              </div>
            ) : (
              results.map(r => (
                <DgaCard key={r.id} style={{ marginBottom: 'var(--spacing-4)' }}>
                  <div style={{ display: 'flex', justifyContent: 'space-between', marginBottom: 'var(--spacing-2)' }}>
                    <DgaTag label={r.category} />
                    <span style={{ color: 'var(--text-tertiary)', fontSize: '14px' }}>{r.date}</span>
                  </div>
                  <h3 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-2)' }}>{r.title}</h3>
                  <p style={{ color: 'var(--text-secondary)', marginBottom: 'var(--spacing-4)' }}>{r.excerpt}</p>
                  <DgaLink label={t.readMore} href={r.href} />
                </DgaCard>
              ))
            )}

            <DgaPagination
              currentPage={page}
              totalPages={5}
              onPageChange={e => setPage(e.detail)}
              style={{ marginTop: 'var(--spacing-6)' }}
            />
          </DgaGridItem>

        </DgaGridContainer>
      </main>
      <DgaFooter />
    </div>
  );
}
```

## RTL
```tsx
<SearchPage rtl={true} lang="ar" initialQuery="الخدمات" />
```
