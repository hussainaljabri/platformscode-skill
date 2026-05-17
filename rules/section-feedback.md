---
name: dga-section-feedback
description: DGA Feedback section — rating, comment, submit
metadata:
  tags: dga, feedback, rating, section
---


## SOURCE
Figma: https://www.figma.com/design/CczWzUDCmWMCCA1JwTbqX1/

---

## SECTIONS & COMPONENTS

**Hero / Heading**
DGA components: DgaFeaturedIcon, DgaGridContainer, DgaGridItem

**Rating Input**
DGA components: DgaRating
- 5-star rating (1–5)
- Label: "How would you rate your experience?" / "كيف تقيّم تجربتك؟"
- `onRatingChange` event handler

**Feedback Form**
DGA components: DgaTextarea, DgaDropdown, DgaCheckbox, DgaButton variant="primary"
- Optional category dropdown (e.g., "General", "Technical", "Content")
- Optional comment textarea
- Submit button

**Confirmation Message**
DGA components: DgaInlineAlert type="success", DgaFeaturedIcon
- Shown after submission
- "Thank you for your feedback!" / "شكرًا على ملاحظاتك!"

---

## RULES
1. Never use `<button>`, `<input>`, `<select>`, `<textarea>` — use DGA equivalents
2. CSS once at root: `import 'platformscode-new-react/dist/style.css'`
3. Button events: `onOnClick` — NOT `onClick`
4. `DgaRating` event: `onRatingChange` — NOT `onChange`
5. Colors/spacing from CSS tokens only

---

## REACT TEMPLATE

```tsx
import {
  DgaRating,
  DgaTextarea,
  DgaDropdown,
  DgaButton,
  DgaInlineAlert,
  DgaFeaturedIcon,
  DgaGridContainer,
  DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';
import { useState } from 'react';

interface FeedbackSectionProps {
  rtl?: boolean;
  lang?: 'en' | 'ar';
  onSubmit?: (data: { rating: number; category: string; comment: string }) => void;
}

export function FeedbackSection({ rtl = false, lang = 'en', onSubmit }: FeedbackSectionProps) {
  const [rating, setRating] = useState(0);
  const [category, setCategory] = useState('');
  const [comment, setComment] = useState('');
  const [submitted, setSubmitted] = useState(false);

  const t = {
    heading:    lang === 'ar' ? 'شاركنا رأيك'        : 'Share Your Feedback',
    ratingLabel:lang === 'ar' ? 'كيف تقيّم تجربتك؟'  : 'How would you rate your experience?',
    category:   lang === 'ar' ? 'الفئة'               : 'Category',
    comment:    lang === 'ar' ? 'تعليقاتك'            : 'Your Comments',
    submit:     lang === 'ar' ? 'إرسال'               : 'Submit',
    thanks:     lang === 'ar' ? 'شكرًا على ملاحظاتك!' : 'Thank you for your feedback!',
  };

  const categories = lang === 'ar'
    ? [{ label: 'عام', value: 'general' }, { label: 'تقني', value: 'technical' }, { label: 'محتوى', value: 'content' }]
    : [{ label: 'General', value: 'general' }, { label: 'Technical', value: 'technical' }, { label: 'Content', value: 'content' }];

  function handleSubmit() {
    onSubmit?.({ rating, category, comment });
    setSubmitted(true);
  }

  return (
    <section dir={rtl ? 'rtl' : 'ltr'} style={{ padding: 'var(--spacing-12) 0' }}>
      <DgaGridContainer cols={12} gap="var(--spacing-6)">
        <DgaGridItem colSpan={12} style={{ textAlign: 'center', marginBottom: 'var(--spacing-6)' }}>
          <DgaFeaturedIcon size="large" color="brand" style="light" circle={true} />
          <h2 style={{ color: 'var(--text-primary)', marginTop: 'var(--spacing-4)' }}>{t.heading}</h2>
        </DgaGridItem>

        {submitted ? (
          <DgaGridItem colSpan={12}>
            <DgaInlineAlert type="success" title={t.thanks} />
          </DgaGridItem>
        ) : (
          <>
            <DgaGridItem colSpan={12} style={{ textAlign: 'center' }}>
              <p style={{ color: 'var(--text-secondary)', marginBottom: 'var(--spacing-4)' }}>{t.ratingLabel}</p>
              <DgaRating value={rating} max={5} size="lg" onRatingChange={e => setRating(e.detail)} />
            </DgaGridItem>

            <DgaGridItem colSpan={6}>
              <DgaDropdown
                label={t.category}
                options={categories}
                onOnChange={e => setCategory(e.detail)}
              />
            </DgaGridItem>

            <DgaGridItem colSpan={12}>
              <DgaTextarea
                label={t.comment}
                rows={4}
                onOnChange={e => setComment(e.detail)}
              />
            </DgaGridItem>

            <DgaGridItem colSpan={12}>
              <DgaButton
                variant="primary-brand"
                size="md"
                label={t.submit}
                disabled={rating === 0}
                onOnClick={handleSubmit}
              />
            </DgaGridItem>
          </>
        )}
      </DgaGridContainer>
    </section>
  );
}
```

---

## HTML TEMPLATE

```html
<section dir="ltr" style="padding: var(--spacing-12) 0">
  <dga-grid-container cols="12" gap="var(--spacing-6)">

    <!-- Heading -->
    <dga-grid-item col-span="12" style="text-align:center">
      <dga-featured-icon size="large" color="brand" style="light" circle="true"></dga-featured-icon>
      <h2>Share Your Feedback</h2>
    </dga-grid-item>

    <!-- Rating -->
    <dga-grid-item col-span="12" style="text-align:center">
      <p>How would you rate your experience?</p>
      <dga-rating id="rating" value="0" max="5" size="lg"></dga-rating>
    </dga-grid-item>

    <!-- Category -->
    <dga-grid-item col-span="6">
      <dga-dropdown id="category" label="Category"></dga-dropdown>
    </dga-grid-item>

    <!-- Comment -->
    <dga-grid-item col-span="12">
      <dga-textarea id="comment" label="Your Comments" rows="4"></dga-textarea>
    </dga-grid-item>

    <!-- Submit -->
    <dga-grid-item col-span="12">
      <dga-button id="submit-btn" variant="primary-brand" size="md" label="Submit"></dga-button>
    </dga-grid-item>

  </dga-grid-container>
</section>

<script type="module">
  import { defineCustomElements } from './node_modules/@platformscode/core/loader/index.es2017.js';
  defineCustomElements();
  document.getElementById('submit-btn').addEventListener('onOnClick', () => {
    document.getElementById('submit-btn').disabled = true;
    // handle submission
  });
</script>
```

---

## RTL / ARABIC
```tsx
<FeedbackSection rtl={true} lang="ar" />
// HTML: <section dir="rtl"> and use Arabic labels
```
