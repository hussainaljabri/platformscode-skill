---
name: platformscode-section-cookies-banner
description: Cookies Banner — fixed bottom, slides up from viewport bottom. Three types (Default, Manage Cookies, Message) with LTR and RTL. Verified pattern on moj.gov.sa, mewa.gov.sa, ksau-hs.edu.sa.
metadata:
  tags: platformscode, cookies, banner, privacy, gdpr, section, fixed-bottom
---

Figma sources:
- https://www.figma.com/design/jZMvzmPvoDozAWBIHwJxyw/ (Cookies Banner Template — Platforms Code Community)
- https://www.figma.com/design/LmMpJkuUyYjmN7AbGrIfeF/ (Cookies Banner Template — added by user)

## Position

The Cookies Banner is **`position: fixed; bottom: 0`** — it slides up from the bottom of the viewport after a short delay on page load. It does **not** affect the sticky header's `top` value.

```css
#cookie-banner {
  position: fixed;
  bottom: 0; left: 0; right: 0;
  z-index: 200;
  border-top: 2px solid var(--brand-700);
  box-shadow: 0 -4px 24px rgba(0,0,0,.25);
  transform: translateY(100%);
  transition: transform .45s cubic-bezier(.4, 0, .2, 1);
}
#cookie-banner.visible   { transform: translateY(0); }
#cookie-banner.dismissed { transform: translateY(100%); pointer-events: none; }
```

Show it on page load with a delay:
```js
window.addEventListener('load', () => {
  setTimeout(() => document.getElementById('cookie-banner').classList.add('visible'), 900);
});
```

Dismiss it (accept/reject/close) by removing `.visible` and adding `.dismissed`:
```js
function hideCookie() {
  const cb = document.getElementById('cookie-banner');
  cb.classList.remove('visible');
  cb.classList.add('dismissed');
}
```

---

---

## SOURCE
Figma: https://www.figma.com/design/jZMvzmPvoDozAWBIHwJxyw/Cookies-Banner-Template---Platforms-Code--Community-

---

## COMPONENT OVERVIEW

The Cookies Banner is a composed UI template made of DGA components. It is **not** a single npm export — you build it by assembling DGA primitives as specified below.

**When to use:** Display at first visit to inform users about cookie usage and collect consent per privacy/legal requirements.

---

## VARIANTS

The banner has two axes:

| Prop | Values |
|------|--------|
| `type` | `default` \| `manage-cookies` \| `message` |
| `rtl` | `false` (LTR/EN) \| `true` (RTL/AR) |

This gives 6 total combinations.

---

## ANATOMY BY VARIANT

### Type: `default`
Shown on first visit. Explains cookie usage and collects initial consent.

```
┌──────────────────────────────────────────────────────────┐
│ [FeaturedIcon]  Cookies & Privacy         [×]CloseBtn   │  ← Header
│                                                          │
│ This site uses cookies to ensure ease of use...          │  ← Helper Text
│ [Privacy Policy link]                                    │  ← Optional link
│                                                          │
│ [Accept btn]  [Reject btn]  [Manage Cookies btn]         │  ← Actions
└──────────────────────────────────────────────────────────┘
```

**DGA components used:**
- `DgaFeaturedIcon` — `size="medium"`, `color="brand"`, `style="light"`, `circle={true}`
- Close button — `DgaButton` icon-only, `variant="subtle"`, `size="medium"` with ✕ icon
- `DgaLink` — `label="Privacy Policy"`, `style="primary"`, `size="medium"`
- Accept → `DgaButton` `variant="primary"` `size="medium"` `label="Accept"`
- Reject → `DgaButton` `variant="secondary-outline"` `size="medium"` `label="Reject"`
- Manage Cookies → `DgaButton` `variant="transparent"` `size="medium"` `label="Manage Cookies"`

**Boolean toggles (all default true):**
- `showLink` — shows/hides the Privacy Policy link
- `showSecondaryAction` — shows/hides Reject button
- `showTertiaryAction` — shows/hides Manage Cookies button
- `showCloseButton` — shows/hides the ✕ close button

**RTL (AR) text:**
- Lead: `"ملفات تعريف الارتباط والخصوصية"`
- Body: `"هذا الموقع يستخدم ملفات تعريف الارتباط الخاصة للتأكد من سهولة الاستخدام..."`
- Link: `"سياسة الخصوصية"`
- Accept: `"قبول"` | Reject: `"رفض"` | Manage: `"إدارة ملفات تعريف الارتباط"`

---

### Type: `manage-cookies`
Shown when user clicks "Manage Cookies". Allows granular cookie category consent.

```
┌──────────────────────────────────────────────────────────┐
│ [FeaturedIcon]  Manage Cookie Preferences   [×]CloseBtn │  ← Header
│                                                          │
│ When you visit any website, it may store...              │  ← Explanation text
│                                                          │
│ [Switch] Strictly Necessary Cookies (Always Active)      │
│          These cookies are necessary for the website...  │
│                                                          │
│ [Switch] Performance Cookies                             │
│          These cookies allow us to count visits...       │
│                                                          │
│ [Switch] Functional Cookies                              │
│          These cookies enable enhanced functionality...  │
│                                                          │
│ [Switch] Targeting Cookies                               │
│          These cookies may be set through our site...    │
│                                                          │
│ [Confirm My Choices btn]  [Reject All btn]               │
└──────────────────────────────────────────────────────────┘
```

**DGA components used:**
- `DgaFeaturedIcon` — same as Default
- Close button — same as Default
- 4× `DgaSwitch` with `label` and `helperText` props
- Confirm → `DgaButton` `variant="primary"` `label="Confirm My Choices"`
- Reject All → `DgaButton` `variant="secondary-outline"` `label="Reject All"`

**Cookie categories (from Figma spec):**

| # | Label EN | Label AR | Always Active |
|---|----------|----------|---------------|
| 1 | Strictly Necessary Cookies (Always Active) | ملفات تعريف الارتباط هذه ضرورية للغاية (نشطة دائماً) | Yes — disabled switch |
| 2 | Performance Cookies | ملفات تعريف الارتباط الخاصة بالأداء | No |
| 3 | Functional Cookies | ملفات تعريف الارتباط الوظيفية | No |
| 4 | Targeting Cookies | ملفات تعريف الارتباط المُستهدِفة | No |

**Helper text per category (from Figma spec):**
1. Strictly Necessary: "These cookies are necessary for the website to function and cannot be switched off in our systems. They are usually only set in response to actions made by you..."
2. Performance: "These cookies allow us to count visits and traffic sources so we can measure and improve the performance of our site..."
3. Functional: "These cookies enable the website to provide enhanced functionality and personalisation. They may be set by us or by third party providers..."
4. Targeting: "These cookies may be set through our site by our advertising partners. They may be used by those companies to build a profile of your interests..."

**RTL (AR) confirm:** `"تأكيد خياراتي"` | Reject All AR: `"رفض الكل"`

---

### Type: `message`
Shown after user makes a choice. Confirms their response was recorded.

```
┌──────────────────────────────────────────────────────────┐
│ [FeaturedIcon]  Response Recorded              [×]Close  │  ← Header
│                                                          │
│ Thank you! Your response has been successfully           │  ← Success message
│ recorded. If you wish to modify or change your answer,  │
│ you can go back by clicking the Undo button.             │
│                                                          │
│ [Undo btn]                                               │
└──────────────────────────────────────────────────────────┘
```

**DGA components used:**
- `DgaFeaturedIcon` — same as Default
- Close button — same as Default
- Undo → `DgaButton` `variant="subtle"` `label="Undo"`

**RTL (AR):**
- Body: `"شكرًا! تم تسجيل استجابتك بنجاح. إذا كنت ترغب في تعديل الإجابة أو تغييرها، يمكنك الرجوع عبر الضغط على زر تراجع."`
- Undo AR: `"تراجع"`

---

## CODE — REACT

```tsx
import React, { useState } from 'react';
import {
  DgaButton,
  DgaFeaturedIcon,
  DgaSwitch,
  DgaLink,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

type BannerType = 'default' | 'manage-cookies' | 'message';

interface CookieBannerProps {
  rtl?: boolean;
  showLink?: boolean;
  showSecondaryAction?: boolean;
  showTertiaryAction?: boolean;
  showCloseButton?: boolean;
  onAccept?: () => void;
  onReject?: () => void;
  onManage?: () => void;
  onConfirm?: (choices: Record<string, boolean>) => void;
  onUndo?: () => void;
  onClose?: () => void;
}

export function CookiesBanner({
  rtl = false,
  showLink = true,
  showSecondaryAction = true,
  showTertiaryAction = true,
  showCloseButton = true,
  onAccept,
  onReject,
  onManage,
  onConfirm,
  onUndo,
  onClose,
}: CookieBannerProps) {
  const [type, setType] = useState<BannerType>('default');
  const [cookieChoices, setCookieChoices] = useState({
    performance: false,
    functional: false,
    targeting: false,
  });

  const t = {
    leadText: rtl ? 'ملفات تعريف الارتباط والخصوصية' : 'Cookies & Privacy',
    bodyText: rtl
      ? 'هذا الموقع يستخدم ملفات تعريف الارتباط الخاصة للتأكد من سهولة الاستخدام وضمان تحسين تجربتك أثناء التصفح.'
      : 'Use of Cookies by this site is just to guarantee Ease of Access and better user experience while browsing. Continuation of your browsing acknowledges your approval for Terms and Conditions of this site and its use of Cookies.',
    privacyLink: rtl ? 'سياسة الخصوصية' : 'Privacy Policy',
    accept: rtl ? 'قبول' : 'Accept',
    reject: rtl ? 'رفض' : 'Reject',
    manage: rtl ? 'إدارة ملفات تعريف الارتباط' : 'Manage Cookies',
    confirm: rtl ? 'تأكيد خياراتي' : 'Confirm My Choices',
    rejectAll: rtl ? 'رفض الكل' : 'Reject All',
    manageExplain: rtl
      ? 'عند زيارة أي موقع على الويب، قد يخزّن هذا الأخير المعلومات على المستعرض أو يستردها على شكل ملفات تعريف ارتباط على الأغلب.'
      : 'When you visit any website, it may store or retrieve information on your browser, mostly in the form of cookies. This information might be about you, your preferences or your device.',
    successText: rtl
      ? 'شكرًا! تم تسجيل استجابتك بنجاح. إذا كنت ترغب في تعديل الإجابة أو تغييرها، يمكنك الرجوع عبر الضغط على زر تراجع.'
      : 'Thank you! Your response has been successfully recorded. If you wish to modify or change your answer, you can go back by clicking the Undo button.',
    undo: rtl ? 'تراجع' : 'Undo',
  };

  const categories = [
    {
      key: 'necessary',
      label: rtl ? 'ملفات تعريف الارتباط هذه ضرورية للغاية (نشطة دائماً)' : 'Strictly Necessary Cookies (Always Active)',
      helperText: rtl
        ? 'تُعدّ ملفات تعريف الارتباط هذه ضروريةً لكي يعمل موقع الويب ولا يمكن إيقاف تشغيلها في أنظمتنا.'
        : 'These cookies are necessary for the website to function and cannot be switched off in our systems.',
      alwaysActive: true,
    },
    {
      key: 'performance',
      label: rtl ? 'ملفات تعريف الارتباط الخاصة بالأداء' : 'Performance Cookies',
      helperText: rtl
        ? 'تسمح لنا ملفات تعريف الارتباط هذه باحتساب مصادر الزيارات وحركة المرور حتى نتمكن من قياس أداء موقعنا.'
        : 'These cookies allow us to count visits and traffic sources so we can measure and improve the performance of our site.',
      alwaysActive: false,
    },
    {
      key: 'functional',
      label: rtl ? 'ملفات تعريف الارتباط الوظيفية' : 'Functional Cookies',
      helperText: rtl
        ? 'تسمح ملفات تعريف الارتباط هذه بتوفير وظائف محسنة وإمكانية تخصيص.'
        : 'These cookies enable the website to provide enhanced functionality and personalisation.',
      alwaysActive: false,
    },
    {
      key: 'targeting',
      label: rtl ? 'ملفات تعريف الارتباط المُستهدِفة' : 'Targeting Cookies',
      helperText: rtl
        ? 'يتم تعيين ملفات تعريف الارتباط هذه من خلال موقعنا من قِبَل شركائنا من شركات الإعلان.'
        : 'These cookies may be set through our site by our advertising partners.',
      alwaysActive: false,
    },
  ];

  return (
    <div
      dir={rtl ? 'rtl' : 'ltr'}
      style={{
        position: 'fixed',
        bottom: 0,
        left: 0,
        right: 0,
        background: 'var(--background-primary)',
        borderTop: '1px solid var(--border-primary)',
        padding: 'var(--spacing-6)',
        boxShadow: 'var(--shadow-lg)',
        zIndex: 1000,
      }}
    >
      {/* Header */}
      <div style={{ display: 'flex', alignItems: 'center', gap: 'var(--spacing-3)', marginBottom: 'var(--spacing-4)' }}>
        <DgaFeaturedIcon size="medium" color="brand" style="light" circle={true} />
        <span style={{ flex: 1, fontWeight: 600, color: 'var(--text-primary)' }}>{t.leadText}</span>
        {showCloseButton && (
          <DgaButton
            variant="subtle"
            size="medium"
            iconOnly={true}
            leadIcon={true}
            leadIconType="x-close"
            leadIconProps={{ variant: 'stroke', type: 'rounded', size: 20 }}
            onOnClick={onClose}
          />
        )}
      </div>

      {/* Type: Default */}
      {type === 'default' && (
        <>
          <p style={{ color: 'var(--text-secondary)', marginBottom: 'var(--spacing-2)' }}>{t.bodyText}</p>
          {showLink && (
            <DgaLink label={t.privacyLink} href="/privacy-policy" style="primary" size="medium" />
          )}
          <div style={{ display: 'flex', gap: 'var(--spacing-3)', marginTop: 'var(--spacing-5)', flexWrap: 'wrap' }}>
            <DgaButton variant="primary" size="medium" label={t.accept} onOnClick={() => { onAccept?.(); setType('message'); }} />
            {showSecondaryAction && (
              <DgaButton variant="secondary-outline" size="medium" label={t.reject} onOnClick={() => { onReject?.(); setType('message'); }} />
            )}
            {showTertiaryAction && (
              <DgaButton variant="transparent" size="medium" label={t.manage} onOnClick={() => { onManage?.(); setType('manage-cookies'); }} />
            )}
          </div>
        </>
      )}

      {/* Type: Manage Cookies */}
      {type === 'manage-cookies' && (
        <>
          <p style={{ color: 'var(--text-secondary)', marginBottom: 'var(--spacing-4)' }}>{t.manageExplain}</p>
          <div style={{ display: 'flex', flexDirection: 'column', gap: 'var(--spacing-3)', marginBottom: 'var(--spacing-5)' }}>
            {categories.map(cat => (
              <DgaSwitch
                key={cat.key}
                label={cat.label}
                helperText={cat.helperText}
                checked={cat.alwaysActive || cookieChoices[cat.key as keyof typeof cookieChoices]}
                disabled={cat.alwaysActive}
                onOnChange={cat.alwaysActive ? undefined : (e) =>
                  setCookieChoices(prev => ({ ...prev, [cat.key]: e.detail }))
                }
              />
            ))}
          </div>
          <div style={{ display: 'flex', gap: 'var(--spacing-3)' }}>
            <DgaButton
              variant="primary"
              size="medium"
              label={t.confirm}
              onOnClick={() => { onConfirm?.(cookieChoices); setType('message'); }}
            />
            <DgaButton
              variant="secondary-outline"
              size="medium"
              label={t.rejectAll}
              onOnClick={() => { onReject?.(); setType('message'); }}
            />
          </div>
        </>
      )}

      {/* Type: Message */}
      {type === 'message' && (
        <>
          <p style={{ color: 'var(--text-secondary)', marginBottom: 'var(--spacing-4)' }}>{t.successText}</p>
          <DgaButton
            variant="subtle"
            size="medium"
            label={t.undo}
            onOnClick={() => { onUndo?.(); setType('default'); }}
          />
        </>
      )}
    </div>
  );
}
```

---

## CODE — HTML (web components)

```html
<!-- Setup (once in app entry) -->
<link rel="stylesheet" href="node_modules/@platformscode/core/dist/core/core.css">
<script type="module">
  import { defineCustomElements } from './node_modules/@platformscode/core/loader/index.es2017.js';
  defineCustomElements();
</script>

<!-- Default variant, LTR -->
<div id="cookies-banner" dir="ltr" style="
  position: fixed; bottom: 0; left: 0; right: 0;
  background: var(--background-primary);
  border-top: 1px solid var(--border-primary);
  padding: var(--spacing-6);
  box-shadow: var(--shadow-lg);
  z-index: 1000;
">
  <div style="display:flex; align-items:center; gap:var(--spacing-3); margin-bottom:var(--spacing-4)">
    <dga-featured-icon size="medium" color="brand" style="light" circle="true"></dga-featured-icon>
    <span style="flex:1; font-weight:600; color:var(--text-primary)">Cookies & Privacy</span>
    <dga-button id="close-btn" variant="subtle" size="medium" icon-only="true"
      lead-icon="true" lead-icon-type="x-close"></dga-button>
  </div>

  <div id="banner-default">
    <p style="color:var(--text-secondary); margin-bottom:var(--spacing-2)">
      Use of Cookies by this site is just to guarantee Ease of Access and better user experience...
    </p>
    <dga-link label="Privacy Policy" href="/privacy-policy" style="primary" size="medium"></dga-link>
    <div style="display:flex; gap:var(--spacing-3); margin-top:var(--spacing-5); flex-wrap:wrap">
      <dga-button id="accept-btn" variant="primary" size="medium" label="Accept"></dga-button>
      <dga-button id="reject-btn" variant="secondary-outline" size="medium" label="Reject"></dga-button>
      <dga-button id="manage-btn" variant="transparent" size="medium" label="Manage Cookies"></dga-button>
    </div>
  </div>
</div>

<script type="module">
  document.getElementById('accept-btn').addEventListener('onOnClick', () => showMessage());
  document.getElementById('reject-btn').addEventListener('onOnClick', () => showMessage());
  document.getElementById('manage-btn').addEventListener('onOnClick', () => showManage());
  document.getElementById('close-btn').addEventListener('onOnClick', () =>
    document.getElementById('cookies-banner').style.display = 'none');

  function showMessage() {
    document.getElementById('banner-default').innerHTML = \`
      <p style="color:var(--text-secondary); margin-bottom:var(--spacing-4)">
        Thank you! Your response has been successfully recorded...
      </p>
      <dga-button id="undo-btn" variant="subtle" size="medium" label="Undo"></dga-button>
    \`;
    document.getElementById('undo-btn').addEventListener('onOnClick', () => location.reload());
  }

  function showManage() { /* render manage-cookies variant */ }
</script>
```

---

## RTL NOTES

- Add `dir="rtl"` to the banner wrapper element — the design system handles layout mirroring automatically
- Reverse the action button order visually (CSS flex-direction handles this with RTL dir)
- Use the AR text strings from the anatomy section above
- The `DgaLink` has an `rtl` prop: `<DgaLink rtl={true} />`
- The `DgaSwitch` has an `rtl` prop: `<DgaSwitch rtl={true} />`

---

## PROPS SUMMARY

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `rtl` | boolean | `false` | Arabic RTL layout and text |
| `showLink` | boolean | `true` | Show/hide Privacy Policy link |
| `showSecondaryAction` | boolean | `true` | Show/hide Reject button |
| `showTertiaryAction` | boolean | `true` | Show/hide Manage Cookies button |
| `showCloseButton` | boolean | `true` | Show/hide ✕ close button |

---

## DGA COMPONENTS CHECKLIST

When implementing, verify you used:
- [ ] `DgaFeaturedIcon` (not a plain icon or img)
- [ ] `DgaButton` with correct variants (`primary`, `secondary-outline`, `transparent`, `subtle`)
- [ ] `DgaLink` for the Privacy Policy link (not an `<a>` tag)
- [ ] `DgaSwitch` for cookie category toggles (not `<input type="checkbox">`)
- [ ] `onOnClick` (not `onClick`) on all DgaButton instances
- [ ] CSS tokens for colors (`var(--background-primary)`) not hardcoded hex values
- [ ] `dir="rtl"` on wrapper for Arabic layout
