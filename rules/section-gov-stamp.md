---
name: platformscode-section-gov-stamp
description: Government Verification Stamp — the topmost sticky bar on every Saudi government portal page confirming official authenticity, collapsible with verification tips
metadata:
  tags: platformscode, government, verification, stamp, official, saudi, top-bar, sticky
---

## What it is

The **Government Verification Stamp** is the topmost element on every Saudi government portal page. It is a slim sticky bar that:

- Confirms the page is an official Saudi government website (bilingual EN + AR)
- Displays a simplified Saudi emblem (palm tree + crossed swords)
- Expands on demand to show 3 verification tips: official `.gov.sa` domain, HTTPS padlock, NCA digital trust seal
- Can be dismissed by the user (×), at which point the header adjusts its sticky position

It must appear **above the cookies banner and above the site header** — always the first element in `<body>`.

---

## Stacking order (top to bottom)

```
z-index: 300  ←  Government Stamp        (topmost — this file)
z-index: 200  ←  Cookies Banner          (section-cookies-banner.md)
z-index:  99  ←  Site Header             (72px, sticky below both bars)
              ←  Page content
```

When either bar is dismissed **or when the stamp panel expands/collapses**, `recalcLayout()` must be called. It sets:
- Cookie banner `top` = stamp's current rendered height
- Site header `top` = stamp height + cookie banner height

Never hardcode these as magic numbers — they change when bars are dismissed or when the stamp panel expands.

---

## Anatomy

### Collapsed (default)

```
┌─────────────────────────────────────────────────────────────────┐
│  [🌴 emblem]  An official website of the Saudi Government       │  ~40px
│               موقع حكومي رسمي  |  Here's how you know ∨  [×]  │
└─────────────────────────────────────────────────────────────────┘
```

### Expanded (after clicking "Here's how you know")

```
┌─────────────────────────────────────────────────────────────────┐
│  [slim bar — same as above]                              [×]    │
├─────────────────────────────────────────────────────────────────┤
│  [🌐 icon]              [🔒 icon]              [🛡 icon]          │
│  Official .gov.sa        Secure HTTPS           NCA Digital      │
│  domain                  connection             Trust Seal       │
│  Saudi gov websites...   A padlock icon...      All official...  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Design spec

### Outer container

```css
#gov-stamp {
  background: var(--brand-800);          /* #114530 — dark Saudi green */
  border-bottom: 1px solid var(--brand-700); /* #196040 */
  position: sticky;
  top: 0;
  z-index: 300;
  font-family: "IBM Plex Sans Arabic", sans-serif;
}
#gov-stamp.dismissed { display: none; }
```

### Slim bar

```css
.gs-bar {
  max-width: 1280px;
  margin-inline: auto;
  padding: 6px 24px;                     /* 6px vertical, 24px sides */
  display: flex;
  align-items: center;
  gap: 16px;
}
```

### Emblem (28×28)

Simplified Saudi palm + swords SVG in `var(--brand-300)` (#6ec598) on a dark bg.
Wrapped in a 28×28 flex container.

### Official text (bilingual)

```css
.gs-official {
  font: 600 12px/18px "IBM Plex Sans Arabic";
  color: #fff;
  display: flex; align-items: center; gap: 8px;
}
/* Green dot separator */
.gs-official span {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: var(--brand-300);
}
```

Content: `An official website of the Saudi Government &nbsp;|&nbsp; موقع حكومي رسمي للمملكة العربية السعودية`

### "Here's how you know" toggle

```css
.gs-verify-btn {
  background: transparent; border: none; cursor: pointer;
  font: 400 11px/18px "IBM Plex Sans Arabic";
  color: rgba(255,255,255,.7);
  display: flex; align-items: center; gap: 4px;
  transition: color .15s;
}
.gs-verify-btn:hover { color: #fff; }
.gs-verify-btn svg   { transition: transform .25s; }
.gs-verify-btn.open svg { transform: rotate(180deg); }
```

### Dismiss button (×)

```css
.gs-close {
  background: transparent; border: none; cursor: pointer;
  color: rgba(255,255,255,.5); padding: 4px;
  border-radius: 2px; transition: color .15s, background .15s;
}
.gs-close:hover { color: #fff; background: rgba(255,255,255,.1); }
```

### Expandable verification panel

```css
#gs-panel {
  max-height: 0;
  overflow: hidden;
  transition: max-height .35s cubic-bezier(.4, 0, .2, 1);
  background: var(--brand-900);          /* #0b3323 — deepest green */
  border-top: 1px solid rgba(255,255,255,.08);
}
#gs-panel.open { max-height: 240px; }
```

Inner grid — 3-column:

```css
.gs-panel-inner {
  max-width: 1280px; margin-inline: auto;
  padding: 20px 24px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
```

Each tip:

```css
.gs-tip { display: flex; gap: 12px; }

.gs-tip-icon {
  width: 32px; height: 32px;
  border-radius: 8px;
  background: rgba(255,255,255,.1);
  flex-shrink: 0;
  display: flex; align-items: center; justify-content: center;
  color: var(--brand-300);
}

.gs-tip-title { font: 600 12px/18px "IBM Plex Sans Arabic"; color: #fff; }
.gs-tip-desc  { font: 400 11px/16px "IBM Plex Sans Arabic"; color: rgba(255,255,255,.6); margin-top: 2px; }
```

---

## The three verification tips

| # | Icon | Title | Body |
|---|------|-------|------|
| 1 | Globe | Official .gov.sa domain | "Saudi government websites always use a `.gov.sa` domain. Look for this in your browser's address bar before entering any information." |
| 2 | Padlock | Secure HTTPS connection | "A padlock icon and `https://` in the address bar confirm your connection is encrypted and secure." |
| 3 | Shield-check | NCA Digital Trust Seal | "All official portals carry the National Cybersecurity Authority digital trust seal. Verify at nca.gov.sa." |

---

## JavaScript

```js
function toggleGsPanel() {
  const panel  = document.getElementById('gs-panel');
  const btn    = document.getElementById('gs-toggle');
  const isOpen = panel.classList.contains('open');
  panel.classList.toggle('open', !isOpen);
  btn.classList.toggle('open',   !isOpen);
  btn.setAttribute('aria-expanded', String(!isOpen));
  // Stamp height changes during the 350ms max-height transition.
  // Recalc after it finishes so cookie and header top values are correct.
  setTimeout(recalcLayout, 360);
}

function recalcLayout() {
  const stamp  = document.getElementById('gov-stamp');
  const cookie = document.getElementById('cookie-banner');
  const header = document.querySelector('.header');
  const sh = stamp  && !stamp.classList.contains('dismissed')  ? stamp.offsetHeight  : 0;
  const ch = cookie && !cookie.classList.contains('dismissed') ? cookie.offsetHeight : 0;
  // Cookie banner: flush below gov stamp
  if (cookie) cookie.style.top = sh + 'px';
  // Site header: flush below both bars (omit on pages with no header, e.g. login)
  if (header) header.style.top = (sh + ch) + 'px';
}
```

Call `recalcLayout()` on:
- `window load`
- `window resize`
- Dismissing the stamp bar
- Dismissing the cookies banner
- `toggleGsPanel()` — already wired via `setTimeout` above

```js
window.addEventListener('load',   recalcLayout);
window.addEventListener('resize', recalcLayout);
```

CSS `top` for cookie banner and header must be `0` as the initial value — JS sets the real value immediately on load.

---

## Complete HTML block

```html
<div id="gov-stamp" role="banner" aria-label="Official government website verification">

  <div class="gs-bar">
    <!-- Saudi emblem SVG -->
    <div class="gs-emblem" aria-hidden="true">
      <svg viewBox="0 0 28 28" fill="none" width="28" height="28">
        <circle cx="14" cy="14" r="13" stroke="rgba(110,197,152,.4)" stroke-width="1"/>
        <line x1="14" y1="22" x2="14" y2="10" stroke="#6ec598" stroke-width="1.5" stroke-linecap="round"/>
        <path d="M14 12 C11 9 8 10 7 8"  stroke="#6ec598" stroke-width="1.2" fill="none" stroke-linecap="round"/>
        <path d="M14 12 C17 9 20 10 21 8" stroke="#6ec598" stroke-width="1.2" fill="none" stroke-linecap="round"/>
        <path d="M14 14 C11 12 9 13 7 12" stroke="#6ec598" stroke-width="1.2" fill="none" stroke-linecap="round"/>
        <path d="M14 14 C17 12 19 13 21 12" stroke="#6ec598" stroke-width="1.2" fill="none" stroke-linecap="round"/>
        <line x1="8"  y1="23" x2="20" y2="19" stroke="#6ec598" stroke-width="1.2" stroke-linecap="round"/>
        <line x1="20" y1="23" x2="8"  y2="19" stroke="#6ec598" stroke-width="1.2" stroke-linecap="round"/>
      </svg>
    </div>

    <div class="gs-text">
      <div class="gs-official">
        <span aria-hidden="true"></span>
        An official website of the Saudi Government &nbsp;|&nbsp; موقع حكومي رسمي للمملكة العربية السعودية
      </div>
      <button class="gs-verify-btn" id="gs-toggle"
        onclick="toggleGsPanel()" aria-expanded="false" aria-controls="gs-panel">
        Here's how you know
        <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
          <polyline points="6 9 12 15 18 9"/>
        </svg>
      </button>
    </div>

    <button class="gs-close"
      onclick="document.getElementById('gov-stamp').classList.add('dismissed');recalcLayout()"
      aria-label="Dismiss" title="Dismiss">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/>
      </svg>
    </button>
  </div>

  <!-- Expandable panel -->
  <div id="gs-panel" role="region" aria-label="Website verification information">
    <div class="gs-panel-inner">
      <div class="gs-tip">
        <div class="gs-tip-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="12" cy="12" r="10"/>
            <line x1="2" y1="12" x2="22" y2="12"/>
            <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>
          </svg>
        </div>
        <div>
          <div class="gs-tip-title">Official .gov.sa domain</div>
          <div class="gs-tip-desc">Saudi government websites always use a <strong style="color:var(--brand-300)">.gov.sa</strong> domain. Look for this in your browser's address bar.</div>
        </div>
      </div>
      <div class="gs-tip">
        <div class="gs-tip-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <rect x="3" y="11" width="18" height="11" rx="2"/>
            <path d="M7 11V7a5 5 0 0 1 10 0v4"/>
          </svg>
        </div>
        <div>
          <div class="gs-tip-title">Secure HTTPS connection</div>
          <div class="gs-tip-desc">A <strong style="color:var(--brand-300)">padlock icon</strong> and <strong style="color:var(--brand-300)">https://</strong> confirm your connection is encrypted.</div>
        </div>
      </div>
      <div class="gs-tip">
        <div class="gs-tip-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
            <polyline points="9 12 11 14 15 10"/>
          </svg>
        </div>
        <div>
          <div class="gs-tip-title">NCA Digital Trust Seal</div>
          <div class="gs-tip-desc">All official portals carry the National Cybersecurity Authority <strong style="color:var(--brand-300)">digital trust seal</strong>.</div>
        </div>
      </div>
    </div>
  </div>

</div>
```

---

## RTL note

The bar text is already bilingual inline. For a fully RTL (`dir="rtl"`) page, the bar layout reverses automatically. The emblem stays on the left (inline-start) side, which becomes the right in RTL. No additional CSS is needed — the flex layout responds to `dir` on the `<html>` element.
