---
name: dga-page-national-day
description: DGA Saudi National Day 95 themed page template
metadata:
  tags: dga, national-day, saudi, celebration, template
---


## SOURCE
Figma: https://www.figma.com/design/sj9rSDh3fjjEDsLGDhUD8n/

---

## DESIGN NOTES

National Day pages use the DGA component library with Saudi green brand colors and celebratory visual treatment.
- Primary color: `var(--colors-primary-sa-flag-600)` (#1f7a4f — Saudi green)
- Accent: `var(--colors-primary-sa-flag-300)` (#6ec598 — light green)
- Keep DGA components — style via sx prop, not custom CSS classes

## SECTIONS & COMPONENTS

**Hero** — Full-width green banner, DgaFeaturedIcon or image, National Day badge/number "95", DgaButton
**Countdown or Date Display** — DgaMetric or styled card
**Events / Activities Grid** — DgaCard × grid, DgaTag (event type), DgaButton (register)
**Media Carousel** — DgaCarousel + DgaCarouselItem
**Share Section** — DgaButton (social share), DgaLink
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaButton, DgaCard,
  DgaTag, DgaMetric, DgaCarousel, DgaCarouselItem,
  DgaFeaturedIcon, DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

export function NationalDay95Page({ rtl = false, lang = 'en' }) {
  const t = {
    tagline:    lang === 'ar' ? 'نحتفل معاً'          : 'We Celebrate Together',
    title:      lang === 'ar' ? 'اليوم الوطني السعودي' : 'Saudi National Day',
    sub:        lang === 'ar' ? 'الذكرى الخامسة والتسعون' : '95th Anniversary',
    events:     lang === 'ar' ? 'الفعاليات والأنشطة'   : 'Events & Activities',
    register:   lang === 'ar' ? 'سجّل الآن'             : 'Register Now',
    share:      lang === 'ar' ? 'شارك الاحتفال'         : 'Share the Celebration',
    explore:    lang === 'ar' ? 'استكشف الفعاليات'      : 'Explore Events',
    date:       lang === 'ar' ? '٢٣ سبتمبر ٢٠٢٥'      : '23 September 2025',
  };

  const events = [
    { type: lang === 'ar' ? 'ثقافي'    : 'Cultural',    title: lang === 'ar' ? 'عرض الفنون السعودية' : 'Saudi Arts Exhibition' },
    { type: lang === 'ar' ? 'رياضي'    : 'Sports',      title: lang === 'ar' ? 'بطولة الألعاب الشعبية' : 'Traditional Games Tournament' },
    { type: lang === 'ar' ? 'ترفيهي'   : 'Entertainment',title: lang === 'ar' ? 'الحفل الوطني الكبير' : 'Grand National Concert' },
    { type: lang === 'ar' ? 'تقني'     : 'Technology',  title: lang === 'ar' ? 'معرض الابتكار الرقمي' : 'Digital Innovation Expo' },
    { type: lang === 'ar' ? 'تعليمي'   : 'Education',   title: lang === 'ar' ? 'ملتقى التعليم المستقبلي' : 'Future Education Forum' },
    { type: lang === 'ar' ? 'اجتماعي'  : 'Community',   title: lang === 'ar' ? 'فعاليات التطوع الوطني' : 'National Volunteering Events' },
  ];

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main>
        {/* Hero */}
        <div style={{
          background: 'linear-gradient(135deg, var(--colors-primary-sa-flag-800) 0%, var(--colors-primary-sa-flag-500) 100%)',
          padding: 'var(--spacing-20) var(--spacing-8)',
          textAlign: 'center',
          position: 'relative',
          overflow: 'hidden',
        }}>
          <p style={{ color: 'var(--colors-primary-sa-flag-200)', fontSize: '18px', marginBottom: 'var(--spacing-2)' }}>
            {t.tagline}
          </p>
          <h1 style={{ color: '#fff', fontSize: '64px', fontWeight: 700, margin: '0 0 var(--spacing-2)' }}>
            {t.title}
          </h1>
          <div style={{
            display: 'inline-block',
            background: '#fff',
            color: 'var(--colors-primary-sa-flag-600)',
            borderRadius: 'var(--radius-full)',
            padding: 'var(--spacing-2) var(--spacing-6)',
            fontSize: '24px',
            fontWeight: 700,
            margin: 'var(--spacing-4) 0',
          }}>
            95
          </div>
          <p style={{ color: 'var(--colors-primary-sa-flag-100)', fontSize: '20px', margin: '0 0 var(--spacing-8)' }}>
            {t.sub} — {t.date}
          </p>
          <DgaButton variant="primary-neutral" size="lg" label={t.explore} onOnClick={() => {}} />
        </div>

        <div style={{ padding: 'var(--spacing-12) var(--spacing-8)' }}>
          <DgaGridContainer cols={12} gap="var(--spacing-6)">

            {/* Events */}
            <DgaGridItem colSpan={12}>
              <h2 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-6)' }}>{t.events}</h2>
            </DgaGridItem>
            {events.map((ev, i) => (
              <DgaGridItem key={i} colSpan={4}>
                <DgaCard sx={{ borderTop: '3px solid var(--colors-primary-sa-flag-500)' }}>
                  <DgaTag label={ev.type} />
                  <h3 style={{ margin: 'var(--spacing-3) 0' }}>{ev.title}</h3>
                  <DgaButton variant="secondary-outline" size="sm" label={t.register} onOnClick={() => {}} />
                </DgaCard>
              </DgaGridItem>
            ))}

            {/* Share */}
            <DgaGridItem colSpan={12} style={{ textAlign: 'center', marginTop: 'var(--spacing-8)' }}>
              <DgaFeaturedIcon icon="share-01" size="large" color="brand" style="light" circle={true} />
              <h3 style={{ marginTop: 'var(--spacing-4)' }}>{t.share}</h3>
              <div style={{ display: 'flex', gap: 'var(--spacing-3)', justifyContent: 'center', marginTop: 'var(--spacing-4)' }}>
                {['Twitter/X', 'Instagram', 'Snapchat'].map(platform => (
                  <DgaButton key={platform} variant="secondary-outline" size="md" label={platform}
                    onOnClick={() => {}} />
                ))}
              </div>
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
<NationalDay95Page rtl={true} lang="ar" />
```
