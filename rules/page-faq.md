---
name: dga-page-faq
description: DGA FAQ page with tabs and accordion
metadata:
  tags: dga, faq, accordion, tabs, template
---


## SOURCE
Figma: https://www.figma.com/design/PYP1ZoQMgYbRdIshLWD3P4/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Breadcrumbs** — DgaBreadcrumbs
**Hero** — Heading + DgaSearchBox (filter FAQs)
**Category Tabs** — DgaTabs (tabsList array) or DgaContentSwitcher
**FAQ List** — DgaAccordion (one per question), DgaDivider between groups
**Contact CTA** — DgaCard, DgaButton, DgaFeaturedIcon
**Footer** — DgaFooter

---

## RULES
1. `DgaTabs` takes `tabsList: ITab[]` — NOT children slots
2. Button events: `onOnClick` not `onClick`
3. DgaAccordion for each Q&A item

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaBreadcrumbs, DgaSearchBox,
  DgaTabs, DgaAccordion, DgaCard, DgaButton, DgaFeaturedIcon,
  DgaGridContainer, DgaGridItem, DgaDivider,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';
import { useState } from 'react';

const FAQS = {
  general: [
    { q: 'What services does the portal offer?', a: 'The portal offers a wide range of digital government services including...' },
    { q: 'How do I register?', a: 'Click the Register button and follow the on-screen instructions.' },
    { q: 'Is the portal available in Arabic?', a: 'Yes, the portal fully supports Arabic with RTL layout.' },
  ],
  account: [
    { q: 'How do I reset my password?', a: 'Click "Forgot Password" on the login page.' },
    { q: 'Can I update my profile information?', a: 'Yes, go to My Profile > Edit Profile.' },
  ],
  technical: [
    { q: 'Which browsers are supported?', a: 'We support the latest versions of Chrome, Firefox, Safari, and Edge.' },
    { q: 'What should I do if a page is not loading?', a: 'Try clearing your browser cache or contact our support team.' },
  ],
};

export function FAQPage({ rtl = false, lang = 'en' }) {
  const [activeTab, setActiveTab] = useState('general');
  const [search, setSearch] = useState('');

  const tabs = [
    { id: 'general',   label: lang === 'ar' ? 'عام'     : 'General' },
    { id: 'account',   label: lang === 'ar' ? 'الحساب'  : 'Account' },
    { id: 'technical', label: lang === 'ar' ? 'تقني'    : 'Technical' },
  ];

  const filtered = (FAQS[activeTab] || []).filter(f =>
    !search || f.q.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main style={{ padding: 'var(--spacing-8) 0' }}>
        <DgaGridContainer cols={12} gap="var(--spacing-6)">

          <DgaGridItem colSpan={12}>
            <DgaBreadcrumbs items={[
              { label: lang === 'ar' ? 'الرئيسية' : 'Home', href: '/' },
              { label: lang === 'ar' ? 'الأسئلة الشائعة' : 'FAQ' },
            ]} />
          </DgaGridItem>

          <DgaGridItem colSpan={12} style={{ textAlign: 'center', padding: 'var(--spacing-8) 0' }}>
            <h1 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-4)' }}>
              {lang === 'ar' ? 'الأسئلة الشائعة' : 'Frequently Asked Questions'}
            </h1>
            <DgaSearchBox
              placeholder={lang === 'ar' ? 'ابحث في الأسئلة...' : 'Search questions...'}
              onOnChange={e => setSearch(e.detail)}
              style={{ maxWidth: '500px', margin: '0 auto' }}
            />
          </DgaGridItem>

          <DgaGridItem colSpan={12}>
            <DgaTabs
              tabsList={tabs}
              activeTab={activeTab}
              direction="horizontal"
              onTabChange={e => setActiveTab(e.detail)}
            />
          </DgaGridItem>

          <DgaGridItem colSpan={12}>
            {filtered.length === 0 ? (
              <p style={{ color: 'var(--text-secondary)' }}>
                {lang === 'ar' ? 'لا توجد نتائج' : 'No results found'}
              </p>
            ) : (
              filtered.map((faq, i) => (
                <DgaAccordion key={i} title={faq.q} style={{ marginBottom: 'var(--spacing-2)' }}>
                  <p style={{ padding: 'var(--spacing-4)', color: 'var(--text-secondary)' }}>{faq.a}</p>
                </DgaAccordion>
              ))
            )}
          </DgaGridItem>

          {/* Contact CTA */}
          <DgaGridItem colSpan={12} style={{ marginTop: 'var(--spacing-8)' }}>
            <DgaCard style={{ textAlign: 'center', padding: 'var(--spacing-8)' }}>
              <DgaFeaturedIcon icon="message-circle-01" size="large" color="brand" style="light" circle={true} />
              <h3 style={{ margin: 'var(--spacing-4) 0 var(--spacing-2)' }}>
                {lang === 'ar' ? 'لم تجد ما تبحث عنه؟' : "Can't find what you're looking for?"}
              </h3>
              <p style={{ color: 'var(--text-secondary)', marginBottom: 'var(--spacing-4)' }}>
                {lang === 'ar' ? 'تواصل مع فريق الدعم' : 'Contact our support team'}
              </p>
              <DgaButton variant="primary-brand" size="md"
                label={lang === 'ar' ? 'تواصل معنا' : 'Contact Us'}
                onOnClick={() => {}} />
            </DgaCard>
          </DgaGridItem>

        </DgaGridContainer>
      </main>
      <DgaFooter />
    </div>
  );
}
```

## RTL / ARABIC
```tsx
<FAQPage rtl={true} lang="ar" />
```
