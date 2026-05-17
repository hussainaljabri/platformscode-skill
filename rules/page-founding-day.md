---
name: dga-page-founding-day
description: DGA Saudi Founding Day themed page template
metadata:
  tags: dga, founding-day, saudi, national, template
---


## SOURCE
Figma: https://www.figma.com/design/xkpukRxgKLFO7O7mZEUEr9/

---

## DESIGN NOTES

Founding Day (February 22) uses DGA components with a gold/amber color accent alongside the Saudi green brand.
- Saudi green: `var(--colors-primary-sa-flag-600)` (#1f7a4f)
- Gold accent: `var(--colors-yellow-600)` (#d97706) from DGA semantic tokens
- Heritage and history visual theme

## SECTIONS & COMPONENTS

**Hero** — Full-width banner with heritage imagery, heading, founding year "1727"
**Timeline** — DgaCard list (vertical timeline of historical milestones)
**Stats / Metrics** — DgaMetric (years of heritage, etc.)
**Activities / Events** — DgaCard grid, DgaTag, DgaButton
**Media Gallery** — DgaCarousel + DgaCarouselItem
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaButton, DgaCard,
  DgaTag, DgaMetric, DgaCarousel, DgaCarouselItem,
  DgaFeaturedIcon, DgaDivider, DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

export function FoundingDayPage({ rtl = false, lang = 'en' }) {
  const t = {
    title:    lang === 'ar' ? 'يوم التأسيس السعودي'        : 'Saudi Founding Day',
    sub:      lang === 'ar' ? '٢٢ فبراير ١٧٢٧ – جذور المجد' : 'February 22, 1727 – Roots of Glory',
    milestones: lang === 'ar' ? 'المحطات التاريخية'          : 'Historical Milestones',
    events:   lang === 'ar' ? 'فعاليات يوم التأسيس'         : 'Founding Day Events',
    register: lang === 'ar' ? 'سجّل'                         : 'Register',
    years:    lang === 'ar' ? 'عام من الإرث'                 : 'Years of Heritage',
  };

  const milestones = [
    { year: '1727', event: lang === 'ar' ? 'تأسيس الدولة السعودية الأولى على يد الإمام محمد بن سعود' : 'First Saudi State founded by Imam Muhammad bin Saud' },
    { year: '1818', event: lang === 'ar' ? 'نهاية الدولة السعودية الأولى'  : 'End of the First Saudi State' },
    { year: '1824', event: lang === 'ar' ? 'تأسيس الدولة السعودية الثانية' : 'Founding of the Second Saudi State' },
    { year: '1932', event: lang === 'ar' ? 'توحيد المملكة العربية السعودية' : 'Unification of the Kingdom of Saudi Arabia' },
  ];

  const events = [
    { type: lang === 'ar' ? 'تراثي'  : 'Heritage',    title: lang === 'ar' ? 'معرض التراث السعودي'     : 'Saudi Heritage Exhibition' },
    { type: lang === 'ar' ? 'ثقافي'  : 'Cultural',    title: lang === 'ar' ? 'ليالي التراث الشعبي'      : 'Folk Heritage Evenings' },
    { type: lang === 'ar' ? 'تاريخي' : 'Historical',  title: lang === 'ar' ? 'رحلة في أعماق التاريخ'    : 'Journey Through History' },
  ];

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main>
        {/* Hero */}
        <div style={{
          background: 'linear-gradient(135deg, var(--colors-primary-sa-flag-900) 0%, var(--colors-primary-sa-flag-600) 60%, var(--colors-yellow-600) 100%)',
          padding: 'var(--spacing-20) var(--spacing-8)',
          textAlign: 'center',
        }}>
          <p style={{ color: 'var(--colors-yellow-300)', letterSpacing: '4px', fontSize: '14px', marginBottom: 'var(--spacing-3)' }}>
            {lang === 'ar' ? '٢٢ فبراير' : 'February 22'}
          </p>
          <h1 style={{ color: '#fff', fontSize: '56px', fontWeight: 700, margin: '0 0 var(--spacing-2)' }}>{t.title}</h1>
          <p style={{ color: 'var(--colors-primary-sa-flag-200)', fontSize: '18px', margin: '0 0 var(--spacing-2)' }}>{t.sub}</p>
          <div style={{
            color: 'var(--colors-yellow-400)',
            fontSize: '72px',
            fontWeight: 700,
            lineHeight: 1,
            margin: 'var(--spacing-4) 0 var(--spacing-8)',
          }}>
            1727
          </div>
          <DgaButton variant="primary-neutral" size="lg"
            label={lang === 'ar' ? 'اكتشف الإرث' : 'Discover the Heritage'}
            onOnClick={() => {}} />
        </div>

        <div style={{ padding: 'var(--spacing-12) var(--spacing-8)' }}>
          <DgaGridContainer cols={12} gap="var(--spacing-6)">

            {/* Stats */}
            <DgaGridItem colSpan={4} style={{ textAlign: 'center' }}>
              <DgaMetric value={`${new Date().getFullYear() - 1727}+`} label={t.years} />
            </DgaGridItem>
            <DgaGridItem colSpan={4} style={{ textAlign: 'center' }}>
              <DgaMetric value="1727" label={lang === 'ar' ? 'سنة التأسيس' : 'Year of Founding'} />
            </DgaGridItem>
            <DgaGridItem colSpan={4} style={{ textAlign: 'center' }}>
              <DgaMetric value={lang === 'ar' ? '٢٢ فبراير' : 'Feb 22'} label={lang === 'ar' ? 'تاريخ الاحتفال' : 'Celebration Date'} />
            </DgaGridItem>

            <DgaGridItem colSpan={12}><DgaDivider /></DgaGridItem>

            {/* Timeline */}
            <DgaGridItem colSpan={12}>
              <h2 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-6)' }}>{t.milestones}</h2>
            </DgaGridItem>
            {milestones.map((m, i) => (
              <DgaGridItem key={i} colSpan={12}>
                <div style={{ display: 'flex', gap: 'var(--spacing-4)', alignItems: 'flex-start' }}>
                  <div style={{
                    background: 'var(--colors-primary-sa-flag-600)',
                    color: '#fff',
                    borderRadius: 'var(--radius-full)',
                    padding: 'var(--spacing-2) var(--spacing-4)',
                    fontWeight: 700,
                    whiteSpace: 'nowrap',
                    minWidth: '80px',
                    textAlign: 'center',
                  }}>{m.year}</div>
                  <p style={{ color: 'var(--text-secondary)', lineHeight: 1.6, margin: 'var(--spacing-1) 0 0' }}>{m.event}</p>
                </div>
                {i < milestones.length - 1 && (
                  <div style={{ marginLeft: rtl ? 0 : '40px', marginRight: rtl ? '40px' : 0, borderLeft: rtl ? 'none' : '2px dashed var(--border-primary)', borderRight: rtl ? '2px dashed var(--border-primary)' : 'none', height: '24px' }} />
                )}
              </DgaGridItem>
            ))}

            <DgaGridItem colSpan={12}><DgaDivider /></DgaGridItem>

            {/* Events */}
            <DgaGridItem colSpan={12}>
              <h2 style={{ marginBottom: 'var(--spacing-6)' }}>{t.events}</h2>
            </DgaGridItem>
            {events.map((ev, i) => (
              <DgaGridItem key={i} colSpan={4}>
                <DgaCard sx={{ borderTop: '3px solid var(--colors-yellow-500)' }}>
                  <DgaTag label={ev.type} />
                  <h3 style={{ margin: 'var(--spacing-3) 0' }}>{ev.title}</h3>
                  <DgaButton variant="secondary-outline" size="sm" label={t.register} onOnClick={() => {}} />
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
<FoundingDayPage rtl={true} lang="ar" />
```
