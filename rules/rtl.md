---
name: dga-rtl
description: RTL (right-to-left) and Arabic language support in the DGA design system
metadata:
  tags: dga, rtl, arabic, i18n, direction, bilingual
---

## Enabling RTL

Add `dir="rtl"` to the root element. The design system handles all layout mirroring automatically.

```tsx
// React
<div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
  ...
</div>
```

```html
<!-- HTML -->
<html lang="ar" dir="rtl">
```

No additional CSS is needed — the DGA design system's components respond to the `dir` attribute on any ancestor element.

## Typography

The primary font is **IBM Plex Sans Arabic**, which supports both LTR and RTL natively. No font switching is required.

## Component RTL props

Some components have an explicit `rtl` prop that should match the page direction:

```tsx
<DgaLink rtl={true} label="رابط" href="/page" />
<DgaSwitch rtl={true} label="تفعيل" />
<DgaBreadcrumbs rtl={true} items={[...]} />
```

## Drawer position

Flip the `position` prop for RTL layouts:

```tsx
// LTR — drawer slides in from the right
<DgaDrawer position="right" open={open} />

// RTL — drawer slides in from the left
<DgaDrawer position="left" open={open} />
```

## Bilingual text pattern

Pass both EN and AR strings through a translation object:

```tsx
interface PageProps {
  rtl?: boolean;
  lang?: 'en' | 'ar';
}

export function MyPage({ rtl = false, lang = 'en' }: PageProps) {
  const t = {
    title:  lang === 'ar' ? 'العنوان'       : 'Title',
    submit: lang === 'ar' ? 'إرسال'         : 'Submit',
    cancel: lang === 'ar' ? 'إلغاء'         : 'Cancel',
  };

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <h1>{t.title}</h1>
      <DgaButton variant="primary-brand" label={t.submit} onOnClick={fn} />
      <DgaButton variant="secondary-outline" label={t.cancel} onOnClick={fn} />
    </div>
  );
}
```

## DgaHeader RTL

Pass `rtl` inside the config object:

```tsx
<DgaHeader
  config={{
    logo: '/logo.png',
    menuItems: [],
    actions: [],
    rtl: true,
  }}
/>
```

## Icon direction

Icons that indicate direction (arrows, chevrons) are mirrored automatically by the browser when `dir="rtl"` is set on the element. No manual flipping needed.

## Flexbox and layout

Flexbox direction is relative to the text direction when using `dir`. `margin-inline-start` / `margin-inline-end` resolve correctly in both directions. Prefer these over `margin-left` / `margin-right` when possible:

```tsx
// Adapts to LTR and RTL automatically
sx={{ marginInlineStart: 'var(--spacing-4)' }}
```
