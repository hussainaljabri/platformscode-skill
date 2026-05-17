---
name: dga-page-hajj
description: DGA Hajj and Umrah portal page template
metadata:
  tags: dga, hajj, umrah, portal, template
---


## SOURCE
Figma: https://www.figma.com/design/ndctEiDUB235XcCdn2qeLY/

---

## DESIGN NOTES

Hajj season pages use DGA components with the brand green (sacred colors). These are typically government service portals for Hajj registration, permits, and guidance.

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Hero** — Celebratory banner, countdown/date, DgaButton (apply/register)
**Quick Services** — DgaCard grid (permit application, health requirements, accommodation, transport)
**Steps / Process** — DgaProgressIndicator (application steps)
**News / Updates** — DgaCard list with DgaTag, DgaLink
**Contact / Support** — DgaCard + DgaButton
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaButton, DgaCard,
  DgaTag, DgaFeaturedIcon, DgaLink,
  DgaProgressIndicator, DgaProgressIndicatorStep,
  DgaGridContainer, DgaGridItem, DgaDivider,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

export function HajjPage({ rtl = false, lang = 'en' }) {
  const t = {
    title:    lang === 'ar' ? 'بوابة الحج والعمرة'         : 'Hajj & Umrah Portal',
    sub:      lang === 'ar' ? 'خدمات الحج والعمرة الإلكترونية' : 'Digital Hajj & Umrah Services',
    apply:    lang === 'ar' ? 'تقديم الطلب'                 : 'Apply Now',
    services: lang === 'ar' ? 'الخدمات المتاحة'              : 'Available Services',
    steps:    lang === 'ar' ? 'خطوات التقديم'               : 'Application Steps',
    news:     lang === 'ar' ? 'آخر الأخبار والتحديثات'       : 'Latest News & Updates',
    support:  lang === 'ar' ? 'الدعم والمساعدة'              : 'Support & Assistance',
    readMore: lang === 'ar' ? 'اقرأ المزيد'                  : 'Read More',
    contact:  lang === 'ar' ? 'تواصل معنا'                   : 'Contact Us',
    year:     lang === 'ar' ? '١٤٤٦ هـ'                     : '1446 AH',
  };

  const services = [
    { icon: 'file-plus-01',  title: lang === 'ar' ? 'تصريح الحج'         : 'Hajj Permit',          href: '/hajj/permit' },
    { icon: 'heart-01',      title: lang === 'ar' ? 'المتطلبات الصحية'    : 'Health Requirements',  href: '/hajj/health' },
    { icon: 'building-01',   title: lang === 'ar' ? 'الإقامة والسكن'      : 'Accommodation',        href: '/hajj/accommodation' },
    { icon: 'bus',           title: lang === 'ar' ? 'خدمات النقل'         : 'Transportation',       href: '/hajj/transport' },
    { icon: 'map-01',        title: lang === 'ar' ? 'دليل المناسك'         : 'Rituals Guide',        href: '/hajj/guide' },
    { icon: 'phone-01',      title: lang === 'ar' ? 'التواصل مع البعثة'   : 'Mission Contact',      href: '/hajj/contact' },
  ];

  const steps = [
    { label: lang === 'ar' ? 'التسجيل'     : 'Register' },
    { label: lang === 'ar' ? 'رفع المستندات': 'Upload Documents' },
    { label: lang === 'ar' ? 'الدفع'        : 'Payment' },
    { label: lang === 'ar' ? 'التأكيد'      : 'Confirmation' },
  ];

  const news = [
    { title: lang === 'ar' ? 'إعلان قرعة الحج ١٤٤٦ هـ'             : 'Hajj 1446 AH Lottery Announcement',      tag: lang === 'ar' ? 'إعلان' : 'Announcement', date: '2024-03-01' },
    { title: lang === 'ar' ? 'اشتراطات السلامة لموسم الحج القادم'   : 'Safety Requirements for Upcoming Hajj Season', tag: lang === 'ar' ? 'صحة'    : 'Health',        date: '2024-02-15' },
    { title: lang === 'ar' ? 'تحديث منظومة خدمات الحج الإلكترونية' : 'Update to e-Hajj Services System',       tag: lang === 'ar' ? 'تحديث'  : 'Update',        date: '2024-02-01' },
  ];

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main>
        {/* Hero */}
        <div style={{
          background: 'linear-gradient(180deg, var(--colors-primary-sa-flag-700) 0%, var(--colors-primary-sa-flag-500) 100%)',
          padding: 'var(--spacing-16) var(--spacing-8)',
          textAlign: 'center',
        }}>
          <p style={{ color: 'var(--colors-primary-sa-flag-200)', marginBottom: 'var(--spacing-2)' }}>{t.year}</p>
          <h1 style={{ color: '#fff', fontSize: '48px', fontWeight: 700, marginBottom: 'var(--spacing-2)' }}>{t.title}</h1>
          <p style={{ color: 'var(--colors-primary-sa-flag-100)', fontSize: '18px', marginBottom: 'var(--spacing-8)' }}>{t.sub}</p>
          <DgaButton variant="primary-neutral" size="lg" label={t.apply}
            leadIcon={true} leadIconType="file-plus-01"
            leadIconProps={{ variant: 'stroke', type: 'rounded', size: 20 }}
            onOnClick={() => {}} />
        </div>

        <div style={{ padding: 'var(--spacing-12) var(--spacing-8)' }}>
          <DgaGridContainer cols={12} gap="var(--spacing-6)">

            {/* Services */}
            <DgaGridItem colSpan={12}>
              <h2 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-6)' }}>{t.services}</h2>
            </DgaGridItem>
            {services.map((svc, i) => (
              <DgaGridItem key={i} colSpan={4}>
                <DgaCard sx={{ textAlign: 'center', cursor: 'pointer', ':hover': { boxShadow: 'var(--shadow-md)' } }}>
                  <DgaFeaturedIcon icon={svc.icon} size="medium" color="brand" style="light" circle={true}
                    sx={{ margin: '0 auto var(--spacing-3)' }} />
                  <h3 style={{ fontSize: '16px', margin: '0 0 var(--spacing-3)' }}>{svc.title}</h3>
                  <DgaLink label={lang === 'ar' ? 'اعرف المزيد' : 'Learn More'} href={svc.href} />
                </DgaCard>
              </DgaGridItem>
            ))}

            <DgaGridItem colSpan={12}><DgaDivider /></DgaGridItem>

            {/* Application Steps */}
            <DgaGridItem colSpan={12}>
              <h2 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-6)' }}>{t.steps}</h2>
              <DgaProgressIndicator currentStep={0}>
                {steps.map((s, i) => <DgaProgressIndicatorStep key={i} label={s.label} />)}
              </DgaProgressIndicator>
            </DgaGridItem>

            <DgaGridItem colSpan={12}><DgaDivider /></DgaGridItem>

            {/* News */}
            <DgaGridItem colSpan={12}>
              <h2 style={{ marginBottom: 'var(--spacing-6)' }}>{t.news}</h2>
            </DgaGridItem>
            {news.map((n, i) => (
              <DgaGridItem key={i} colSpan={4}>
                <DgaCard>
                  <div style={{ display: 'flex', justifyContent: 'space-between', marginBottom: 'var(--spacing-3)' }}>
                    <DgaTag label={n.tag} />
                    <span style={{ color: 'var(--text-tertiary)', fontSize: '12px' }}>{n.date}</span>
                  </div>
                  <h3 style={{ fontSize: '15px', marginBottom: 'var(--spacing-3)' }}>{n.title}</h3>
                  <DgaLink label={t.readMore} href="#" />
                </DgaCard>
              </DgaGridItem>
            ))}

            {/* Support CTA */}
            <DgaGridItem colSpan={12} style={{ marginTop: 'var(--spacing-4)' }}>
              <DgaCard sx={{
                background: 'var(--colors-primary-sa-flag-50)',
                border: '1px solid var(--colors-primary-sa-flag-200)',
                display: 'flex', alignItems: 'center', gap: 'var(--spacing-4)' }}>
                <DgaFeaturedIcon icon="phone-01" size="medium" color="brand" style="light" circle={true} />
                <div style={{ flex: 1 }}>
                  <h3 style={{ margin: '0 0 var(--spacing-1)' }}>{t.support}</h3>
                  <p style={{ color: 'var(--text-secondary)', margin: 0 }}>
                    {lang === 'ar' ? 'فريق الدعم متاح على مدار الساعة' : 'Support team available 24/7'}
                  </p>
                </div>
                <DgaButton variant="primary-brand" size="md" label={t.contact} onOnClick={() => {}} />
              </DgaCard>
            </DgaGridItem>

          </DgaGridContainer>
        </div>
      </main>
      <DgaFooter />
    </div>
  );
}
```

## RTL
```tsx
<HajjPage rtl={true} lang="ar" />
```
