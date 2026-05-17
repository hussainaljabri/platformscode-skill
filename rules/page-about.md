---
name: dga-page-about
description: DGA About The Entity page template
metadata:
  tags: dga, about, entity, leadership, template
---


## SOURCE
Figma: https://www.figma.com/design/sDwKaOESfulEABtGOUKQcS/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Breadcrumbs** — DgaBreadcrumbs
**Hero Banner** — Full-width banner, heading, description, DgaButton CTA
**Vision & Mission Cards** — DgaCard × 2 with DgaFeaturedIcon
**Stats / Metrics** — DgaMetric × 3–4 (key numbers)
**Leadership** — DgaCard grid with DgaAvatar (photo/initials), name, title
**Organizational Chart** — DgaCard, DgaDivider (or image)
**Partners / Logos** — DgaCarousel or grid of logo images
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaBreadcrumbs, DgaButton,
  DgaCard, DgaFeaturedIcon, DgaMetric, DgaAvatar,
  DgaCarousel, DgaCarouselItem, DgaDivider,
  DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

export function AboutPage({ rtl = false, lang = 'en' }) {
  const t = {
    about:    lang === 'ar' ? 'عن الجهة'       : 'About The Entity',
    vision:   lang === 'ar' ? 'رؤيتنا'         : 'Our Vision',
    mission:  lang === 'ar' ? 'رسالتنا'        : 'Our Mission',
    values:   lang === 'ar' ? 'قيمنا'          : 'Our Values',
    leaders:  lang === 'ar' ? 'القيادة'        : 'Leadership',
    partners: lang === 'ar' ? 'شركاؤنا'        : 'Our Partners',
    learnMore:lang === 'ar' ? 'اعرف المزيد'    : 'Learn More',
    heroTitle:lang === 'ar' ? 'نحو وطن رقمي طموح' : 'Towards an Ambitious Digital Nation',
    heroBody: lang === 'ar'
      ? 'هيئة الحكومة الرقمية تقود مسيرة التحول الرقمي في المملكة العربية السعودية.'
      : 'The Digital Government Authority leads the digital transformation journey in the Kingdom of Saudi Arabia.',
  };

  const stats = [
    { value: '500+', label: lang === 'ar' ? 'خدمة رقمية'    : 'Digital Services' },
    { value: '98%',  label: lang === 'ar' ? 'رضا المستخدمين' : 'User Satisfaction' },
    { value: '12M+', label: lang === 'ar' ? 'مستخدم نشط'    : 'Active Users' },
    { value: '2021', label: lang === 'ar' ? 'سنة التأسيس'    : 'Year Founded' },
  ];

  const leaders = [
    { name: lang === 'ar' ? 'اسم المسؤول'  : 'Director Name',  title: lang === 'ar' ? 'المدير العام'    : 'Director General',  initials: 'DG' },
    { name: lang === 'ar' ? 'اسم المسؤول'  : 'Deputy Name',    title: lang === 'ar' ? 'نائب المدير'     : 'Deputy Director',    initials: 'DD' },
    { name: lang === 'ar' ? 'اسم المسؤول'  : 'CTO Name',       title: lang === 'ar' ? 'مدير التقنية'    : 'Chief Technology Officer', initials: 'CT' },
    { name: lang === 'ar' ? 'اسم المسؤول'  : 'CFO Name',       title: lang === 'ar' ? 'مدير المالية'    : 'Chief Financial Officer', initials: 'CF' },
  ];

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main>
        {/* Hero */}
        <div style={{
          background: 'var(--colors-primary-sa-flag-600)',
          padding: 'var(--spacing-20) var(--spacing-8)',
          textAlign: 'center',
        }}>
          <h1 style={{ color: '#fff', marginBottom: 'var(--spacing-4)' }}>{t.heroTitle}</h1>
          <p style={{ color: 'var(--colors-primary-sa-flag-100)', maxWidth: '600px', margin: '0 auto var(--spacing-6)' }}>{t.heroBody}</p>
          <DgaButton variant="primary-neutral" size="lg" label={t.learnMore} onOnClick={() => {}} />
        </div>

        <div style={{ padding: 'var(--spacing-12) var(--spacing-8)' }}>
          <DgaGridContainer cols={12} gap="var(--spacing-6)">

            {/* Breadcrumbs */}
            <DgaGridItem colSpan={12}>
              <DgaBreadcrumbs items={[
                { label: lang === 'ar' ? 'الرئيسية' : 'Home', href: '/' },
                { label: t.about },
              ]} />
            </DgaGridItem>

            {/* Vision & Mission */}
            <DgaGridItem colSpan={6}>
              <DgaCard style={{ height: '100%' }}>
                <DgaFeaturedIcon icon="eye" size="large" color="brand" style="light" circle={true} />
                <h2 style={{ marginTop: 'var(--spacing-4)' }}>{t.vision}</h2>
                <p style={{ color: 'var(--text-secondary)', marginTop: 'var(--spacing-2)' }}>
                  {lang === 'ar'
                    ? 'بناء مجتمع رقمي متقدم يُمكّن المواطنين ويُحسّن جودة الخدمات الحكومية.'
                    : 'Building an advanced digital society that empowers citizens and improves government service quality.'}
                </p>
              </DgaCard>
            </DgaGridItem>
            <DgaGridItem colSpan={6}>
              <DgaCard style={{ height: '100%' }}>
                <DgaFeaturedIcon icon="target-04" size="large" color="brand" style="light" circle={true} />
                <h2 style={{ marginTop: 'var(--spacing-4)' }}>{t.mission}</h2>
                <p style={{ color: 'var(--text-secondary)', marginTop: 'var(--spacing-2)' }}>
                  {lang === 'ar'
                    ? 'تحقيق التحول الرقمي الشامل في الحكومة من خلال استراتيجيات مبتكرة وشاملة.'
                    : 'Achieving comprehensive digital transformation in government through innovative and inclusive strategies.'}
                </p>
              </DgaCard>
            </DgaGridItem>

            {/* Stats */}
            <DgaGridItem colSpan={12}><DgaDivider /></DgaGridItem>
            {stats.map((s, i) => (
              <DgaGridItem key={i} colSpan={3} style={{ textAlign: 'center' }}>
                <DgaMetric value={s.value} label={s.label} />
              </DgaGridItem>
            ))}

            {/* Leadership */}
            <DgaGridItem colSpan={12} style={{ marginTop: 'var(--spacing-8)' }}>
              <h2 style={{ marginBottom: 'var(--spacing-6)' }}>{t.leaders}</h2>
            </DgaGridItem>
            {leaders.map((l, i) => (
              <DgaGridItem key={i} colSpan={3} style={{ textAlign: 'center' }}>
                <DgaCard>
                  <DgaAvatar type="initials" initials={l.initials} size="lg" style={{ margin: '0 auto var(--spacing-3)' }} />
                  <h3 style={{ margin: '0 0 var(--spacing-1)' }}>{l.name}</h3>
                  <p style={{ color: 'var(--text-secondary)', fontSize: '14px', margin: 0 }}>{l.title}</p>
                </DgaCard>
              </DgaGridItem>
            ))}

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
<AboutPage rtl={true} lang="ar" />
```
