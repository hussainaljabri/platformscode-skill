---
name: dga-page-eparticipation
description: DGA e-Participation page — surveys, polls, ideas
metadata:
  tags: dga, e-participation, survey, poll, template
---


## SOURCE
Figma: https://www.figma.com/design/LShYfLMFZhZifBNi7JDfJR/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Breadcrumbs** — DgaBreadcrumbs
**Hero** — DgaFeaturedIcon, heading, description
**Participation Tabs** — DgaTabs (tabsList array): Surveys | Consultations | Polls | Ideas
**Survey / Consultation Cards** — DgaCard grid with DgaTag (status), DgaButton (participate), DgaLinearProgressBar (participation rate)
**Active Poll** — DgaRadioButton list + DgaButton (vote)
**Submit Idea** — DgaTextInput (title) + DgaTextarea (description) + DgaButton
**Footer** — DgaFooter

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaBreadcrumbs, DgaTabs,
  DgaCard, DgaTag, DgaButton, DgaLinearProgressBar,
  DgaRadioButton, DgaTextInput, DgaTextarea, DgaFeaturedIcon,
  DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';
import { useState } from 'react';

export function EParticipationPage({ rtl = false, lang = 'en' }) {
  const [activeTab, setActiveTab] = useState('surveys');
  const [pollChoice, setPollChoice] = useState('');
  const [idea, setIdea] = useState({ title: '', description: '' });

  const t = {
    title:      lang === 'ar' ? 'المشاركة الإلكترونية' : 'e-Participation',
    desc:       lang === 'ar' ? 'شاركنا رأيك وأسهم في صنع القرار'  : 'Share your opinion and contribute to decision-making',
    surveys:    lang === 'ar' ? 'الاستبيانات'       : 'Surveys',
    consults:   lang === 'ar' ? 'المشاورات'         : 'Consultations',
    polls:      lang === 'ar' ? 'التصويت'           : 'Polls',
    ideas:      lang === 'ar' ? 'اقتراح فكرة'       : 'Submit Idea',
    participate:lang === 'ar' ? 'شارك الآن'          : 'Participate Now',
    vote:       lang === 'ar' ? 'صوّت'              : 'Vote',
    submit:     lang === 'ar' ? 'إرسال الفكرة'       : 'Submit Idea',
    active:     lang === 'ar' ? 'نشط'               : 'Active',
    closed:     lang === 'ar' ? 'مغلق'              : 'Closed',
    ideaTitle:  lang === 'ar' ? 'عنوان الفكرة'       : 'Idea Title',
    ideaDesc:   lang === 'ar' ? 'وصف الفكرة'         : 'Idea Description',
  };

  const tabs = [
    { id: 'surveys', label: t.surveys },
    { id: 'consults', label: t.consults },
    { id: 'polls', label: t.polls },
    { id: 'ideas', label: t.ideas },
  ];

  const surveys = [
    { title: lang === 'ar' ? 'استبيان رضا المستخدمين' : 'User Satisfaction Survey', deadline: '2024-06-30', participation: 65, status: 'active' },
    { title: lang === 'ar' ? 'تقييم الخدمات الرقمية'  : 'Digital Services Evaluation', deadline: '2024-07-15', participation: 42, status: 'active' },
    { title: lang === 'ar' ? 'تحسين بوابة الخدمات'    : 'Services Portal Improvement', deadline: '2024-04-01', participation: 100, status: 'closed' },
  ];

  const pollOptions = [
    { value: 'a', label: lang === 'ar' ? 'ممتاز جداً'    : 'Excellent' },
    { value: 'b', label: lang === 'ar' ? 'جيد'            : 'Good' },
    { value: 'c', label: lang === 'ar' ? 'مقبول'          : 'Acceptable' },
    { value: 'd', label: lang === 'ar' ? 'يحتاج تحسين'   : 'Needs Improvement' },
  ];

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main style={{ padding: 'var(--spacing-8) 0' }}>
        <DgaGridContainer cols={12} gap="var(--spacing-6)">

          <DgaGridItem colSpan={12}>
            <DgaBreadcrumbs items={[
              { label: lang === 'ar' ? 'الرئيسية' : 'Home', href: '/' },
              { label: t.title },
            ]} />
          </DgaGridItem>

          {/* Hero */}
          <DgaGridItem colSpan={12} style={{ textAlign: 'center', padding: 'var(--spacing-8) 0' }}>
            <DgaFeaturedIcon icon="users-01" size="large" color="brand" style="light" circle={true} />
            <h1 style={{ marginTop: 'var(--spacing-4)', color: 'var(--text-primary)' }}>{t.title}</h1>
            <p style={{ color: 'var(--text-secondary)', maxWidth: '500px', margin: 'var(--spacing-2) auto 0' }}>{t.desc}</p>
          </DgaGridItem>

          {/* Tabs */}
          <DgaGridItem colSpan={12}>
            <DgaTabs tabsList={tabs} activeTab={activeTab} direction="horizontal"
              onTabChange={e => setActiveTab(e.detail)} />
          </DgaGridItem>

          {/* Surveys Tab */}
          {activeTab === 'surveys' && surveys.map((s, i) => (
            <DgaGridItem key={i} colSpan={4}>
              <DgaCard>
                <div style={{ display: 'flex', justifyContent: 'space-between', marginBottom: 'var(--spacing-3)' }}>
                  <DgaTag label={s.status === 'active' ? t.active : t.closed}
                    variant={s.status === 'active' ? 'success' : 'neutral'} />
                  <span style={{ color: 'var(--text-tertiary)', fontSize: '12px' }}>{s.deadline}</span>
                </div>
                <h3 style={{ marginBottom: 'var(--spacing-3)' }}>{s.title}</h3>
                <p style={{ color: 'var(--text-secondary)', fontSize: '14px', marginBottom: 'var(--spacing-3)' }}>
                  {lang === 'ar' ? `${s.participation}% نسبة المشاركة` : `${s.participation}% participation`}
                </p>
                <DgaLinearProgressBar value={s.participation} style={{ marginBottom: 'var(--spacing-4)' }} />
                <DgaButton variant={s.status === 'active' ? 'primary-brand' : 'secondary-outline'}
                  size="md" label={t.participate} disabled={s.status === 'closed'}
                  onOnClick={() => {}} />
              </DgaCard>
            </DgaGridItem>
          ))}

          {/* Polls Tab */}
          {activeTab === 'polls' && (
            <DgaGridItem colSpan={6}>
              <DgaCard>
                <h3 style={{ marginBottom: 'var(--spacing-4)' }}>
                  {lang === 'ar' ? 'كيف تقيّم جودة الخدمات الحكومية الرقمية؟' : 'How would you rate the quality of digital government services?'}
                </h3>
                {pollOptions.map(opt => (
                  <DgaRadioButton key={opt.value} name="poll" label={opt.label} value={opt.value}
                    checked={pollChoice === opt.value} onOnChange={() => setPollChoice(opt.value)}
                    style={{ marginBottom: 'var(--spacing-3)' }} />
                ))}
                <DgaButton variant="primary-brand" size="md" label={t.vote}
                  disabled={!pollChoice} onOnClick={() => {}} style={{ marginTop: 'var(--spacing-4)' }} />
              </DgaCard>
            </DgaGridItem>
          )}

          {/* Ideas Tab */}
          {activeTab === 'ideas' && (
            <DgaGridItem colSpan={8}>
              <DgaCard>
                <h3 style={{ marginBottom: 'var(--spacing-4)' }}>
                  {lang === 'ar' ? 'شاركنا فكرتك' : 'Share Your Idea'}
                </h3>
                <DgaTextInput label={t.ideaTitle} required style={{ marginBottom: 'var(--spacing-4)' }}
                  onOnChange={e => setIdea(i => ({ ...i, title: e.detail }))} />
                <DgaTextarea label={t.ideaDesc} rows={5} style={{ marginBottom: 'var(--spacing-4)' }}
                  onOnChange={e => setIdea(i => ({ ...i, description: e.detail }))} />
                <DgaButton variant="primary-brand" size="md" label={t.submit}
                  disabled={!idea.title} onOnClick={() => {}} />
              </DgaCard>
            </DgaGridItem>
          )}

        </DgaGridContainer>
      </main>
      <DgaFooter />
    </div>
  );
}
```

## KEY NOTES
- `DgaTabs` → `tabsList` array, `onTabChange` event
- `DgaRadioButton` → `name` groups them, `onOnChange` not `onChange`
- `DgaLinearProgressBar` → `value` 0–100

## RTL
```tsx
<EParticipationPage rtl={true} lang="ar" />
```
