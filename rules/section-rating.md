---
name: dga-section-rating
description: DGA Rating section — star rating with optional comment
metadata:
  tags: dga, rating, section
---


## SOURCE
Figma: https://www.figma.com/design/N36o6zH93fPvY5JwkopYFj/

---

## SECTIONS & COMPONENTS

**Rating Input** — DgaRating (1–5 stars), event: `onRatingChange`
**Optional Comment** — DgaTextarea
**Submit** — DgaButton variant="primary-brand"
**Confirmation** — DgaInlineAlert type="success"

---

## REACT TEMPLATE

```tsx
import {
  DgaRating, DgaTextarea, DgaButton, DgaInlineAlert,
  DgaFeaturedIcon, DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';
import { useState } from 'react';

export function RatingSection({ rtl = false, lang = 'en', onSubmit }) {
  const [rating, setRating] = useState(0);
  const [comment, setComment] = useState('');
  const [done, setDone] = useState(false);

  const t = {
    q:       lang === 'ar' ? 'كيف تقيّم هذه الصفحة؟' : 'How would you rate this page?',
    comment: lang === 'ar' ? 'أضف تعليقًا (اختياري)' : 'Add a comment (optional)',
    submit:  lang === 'ar' ? 'إرسال'                  : 'Submit',
    thanks:  lang === 'ar' ? 'شكرًا على تقييمك!'      : 'Thank you for your rating!',
  };

  return (
    <section dir={rtl ? 'rtl' : 'ltr'} style={{
      background: 'var(--background-secondary)',
      padding: 'var(--spacing-8)',
      borderRadius: 'var(--radius-md)',
      textAlign: 'center',
    }}>
      {done ? (
        <DgaInlineAlert type="success" title={t.thanks} />
      ) : (
        <DgaGridContainer cols={12} gap="var(--spacing-4)">
          <DgaGridItem colSpan={12}>
            <p style={{ color: 'var(--text-primary)', fontWeight: 600, marginBottom: 'var(--spacing-3)' }}>{t.q}</p>
            <DgaRating value={rating} max={5} size="lg" onRatingChange={e => setRating(e.detail)} />
          </DgaGridItem>
          {rating > 0 && (
            <DgaGridItem colSpan={12}>
              <DgaTextarea label={t.comment} rows={3} onOnChange={e => setComment(e.detail)} />
            </DgaGridItem>
          )}
          <DgaGridItem colSpan={12}>
            <DgaButton variant="primary-brand" size="md" label={t.submit}
              disabled={rating === 0}
              onOnClick={() => { onSubmit?.({ rating, comment }); setDone(true); }} />
          </DgaGridItem>
        </DgaGridContainer>
      )}
    </section>
  );
}
```

## RTL
```tsx
<RatingSection rtl={true} lang="ar" />
```
