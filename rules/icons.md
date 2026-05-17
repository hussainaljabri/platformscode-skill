---
name: dga-icons
description: DGA icon system — variants, types, and usage with DGA components
metadata:
  tags: dga, icons, platformscode-icons, svg, featured-icon
---

Figma source: https://www.figma.com/design/cdPCadCUrZRTqG1ifzjAcQ/
Package: `@platformscode/icons`

## Variants

| Variant | Description |
|---------|-------------|
| `stroke` | Outlined line icons — default, most common |
| `solid` | Filled icons — stronger emphasis |
| `duotone` | Two-tone — decorative and featured use |
| `twotone` | Two distinct colors |
| `bulk` | Bold filled — high-contrast |

## Types (corner style)

`rounded` (default) | `sharp` | `standard`

---

## React usage

### Icon on a button

```tsx
// Leading icon
<DgaButton
  variant="primary-brand"
  label="Go Home"
  leadIcon={true}
  leadIconType="home-01"
  leadIconProps={{ variant: 'stroke', type: 'rounded', size: 20 }}
/>

// Trailing icon
<DgaButton
  variant="secondary-outline"
  label="Next"
  trailIcon={true}
  trailIconType="arrow-right"
  trailIconProps={{ variant: 'stroke', type: 'rounded', size: 20 }}
/>

// Icon-only button
<DgaButton
  variant="subtle"
  iconOnly={true}
  leadIcon={true}
  leadIconType="x-close"
  leadIconProps={{ variant: 'stroke', type: 'rounded', size: 20 }}
/>
```

### Featured icon (cards, banners, empty states)

```tsx
<DgaFeaturedIcon
  icon="shield-tick"
  size="medium"     // small | medium | large | huge
  color="brand"     // brand | gray | error | warning | success | info
  style="light"     // light | dark | outline
  circle={true}
/>
```

### Avatar with icon

```tsx
<DgaAvatar
  type="icon"
  icon={{ name: 'user-01', variant: 'stroke', type: 'rounded' }}
  size="md"
/>
```

---

## HTML usage

```html
<dga-button
  variant="primary-brand"
  label="Go Home"
  lead-icon="true"
  lead-icon-type="home-01">
</dga-button>

<dga-featured-icon
  icon="shield-tick"
  size="medium"
  color="brand"
  style="light"
  circle="true">
</dga-featured-icon>
```

---

## Common icon names

```
Navigation:    home-01  arrow-left  arrow-right  chevron-down  chevron-up  menu-01  x-close
Actions:       edit-01  trash-01  download-01  upload-01  copy-01  share-01  search-lg
Status:        check  check-circle  alert-triangle  info-circle  x-circle
UI:            settings-01  filter-lines  sort-desc  eye  eye-off  lock-01  unlock-01
User:          user-01  users-01  user-plus-01  log-in-01  log-out-01
Files:         file-01  file-plus-01  folder-01  attachment-01  image-01
Communication: mail-01  message-circle-01  phone-01  bell-01
Data:          bar-chart-01  pie-chart-01  trend-up-01  trend-down-01
Security:      shield-tick  shield-01  key-01  fingerprint-01
Government:    building-01  flag-01  globe-01  landmark-01
```
