---
name: dga-page-help
description: DGA Help and Support page template
metadata:
  tags: dga, help, support, accordion, template
---


## SOURCE
Figma: https://www.figma.com/design/9knzHVGJnIZRjPuCDGgpiO/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader (config object)
**Breadcrumbs** — DgaBreadcrumbs (items array)

**Hero / Search**
DGA components: DgaSearchBox, DgaFeaturedIcon
- Prominent search box: "How can we help you?" / "كيف يمكننا مساعدتك؟"

**Help Categories (Cards)**
DGA components: DgaCard, DgaFeaturedIcon, DgaLink, DgaGridContainer, DgaGridItem
- Grid of topic cards (e.g. Account, Payments, Technical Support)
- Each card has icon + title + description + link

**Popular Articles / FAQ**
DGA components: DgaAccordion, DgaDivider
- List of expandable FAQ items
- Each accordion: question as title, answer as content

**Contact Options**
DGA components: DgaCard, DgaFeaturedIcon, DgaButton, DgaGridContainer
- Phone, Email, Live Chat cards
- Each with icon, label, and action button

**Footer** — DgaFooter

---

## RULES
1. Never use `<button>`, `<input>`, `<select>`, `<textarea>` — use DGA equivalents
2. CSS once at root: `import 'platformscode-new-react/dist/style.css'`
3. Button events: `onOnClick` — NOT `onClick`
4. `DgaHeader` takes `config` object, not children
5. `DgaBreadcrumbs` takes `items` array, not children

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaBreadcrumbs, DgaSearchBox,
  DgaCard, DgaFeaturedIcon, DgaLink, DgaAccordion,
  DgaButton, DgaGridContainer, DgaGridItem, DgaDivider,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';

export function HelpSupportPage({ rtl = false, lang = 'en' }) {
  const t = {
    hero:      lang === 'ar' ? 'كيف يمكننا مساعدتك؟' : 'How can we help you?',
    search:    lang === 'ar' ? 'ابحث في المساعدة...'  : 'Search help articles...',
    categories:lang === 'ar' ? 'تصفح المواضيع'        : 'Browse Topics',
    faq:       lang === 'ar' ? 'الأسئلة الشائعة'      : 'Frequently Asked Questions',
    contact:   lang === 'ar' ? 'تواصل معنا'            : 'Contact Us',
  };

  const categories = [
    { icon: 'user-01',      title: lang === 'ar' ? 'الحساب'          : 'Account',          href: '/help/account' },
    { icon: 'credit-card-01', title: lang === 'ar' ? 'المدفوعات'    : 'Payments',         href: '/help/payments' },
    { icon: 'settings-01', title: lang === 'ar' ? 'الدعم التقني'    : 'Technical Support', href: '/help/technical' },
    { icon: 'file-01',     title: lang === 'ar' ? 'الوثائق'         : 'Documents',        href: '/help/documents' },
    { icon: 'shield-tick', title: lang === 'ar' ? 'الأمان والخصوصية': 'Security & Privacy',href: '/help/security' },
    { icon: 'info-circle', title: lang === 'ar' ? 'عام'             : 'General',           href: '/help/general' },
  ];

  const faqs = [
    {
      q: lang === 'ar' ? 'كيف أنشئ حسابًا جديدًا؟' : 'How do I create a new account?',
      a: lang === 'ar' ? 'يمكنك إنشاء حساب جديد من خلال النقر على زر التسجيل في الصفحة الرئيسية.' : 'Click the Register button on the homepage and follow the steps.',
    },
    {
      q: lang === 'ar' ? 'كيف أعيد تعيين كلمة المرور؟' : 'How do I reset my password?',
      a: lang === 'ar' ? 'انقر على "نسيت كلمة المرور" في صفحة تسجيل الدخول.' : 'Click "Forgot Password" on the login page.',
    },
    {
      q: lang === 'ar' ? 'كيف أتواصل مع الدعم؟' : 'How do I contact support?',
      a: lang === 'ar' ? 'يمكنك التواصل معنا عبر البريد الإلكتروني أو الهاتف أو الدردشة المباشرة.' : 'You can reach us via email, phone, or live chat below.',
    },
  ];

  return (
    <div dir={rtl ? 'rtl' : 'ltr'} lang={lang}>
      <DgaHeader config={{ logo: '/logo.png', menuItems: [], actions: [], rtl }} />

      <main style={{ padding: 'var(--spacing-8) 0' }}>
        <DgaGridContainer cols={12} gap="var(--spacing-6)">

          {/* Breadcrumbs */}
          <DgaGridItem colSpan={12}>
            <DgaBreadcrumbs items={[{ label: lang === 'ar' ? 'الرئيسية' : 'Home', href: '/' }, { label: t.contact }]} />
          </DgaGridItem>

          {/* Hero Search */}
          <DgaGridItem colSpan={12} style={{ textAlign: 'center', padding: 'var(--spacing-12) 0' }}>
            <h1 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-6)' }}>{t.hero}</h1>
            <DgaSearchBox placeholder={t.search} style={{ maxWidth: '600px', margin: '0 auto' }} />
          </DgaGridItem>

          {/* Categories */}
          <DgaGridItem colSpan={12}>
            <h2 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-6)' }}>{t.categories}</h2>
          </DgaGridItem>
          {categories.map(cat => (
            <DgaGridItem key={cat.href} colSpan={4}>
              <DgaCard>
                <DgaFeaturedIcon icon={cat.icon} size="medium" color="brand" style="light" circle={true} />
                <h3 style={{ marginTop: 'var(--spacing-3)' }}>{cat.title}</h3>
                <DgaLink label={lang === 'ar' ? 'اقرأ المزيد' : 'Learn more'} href={cat.href} />
              </DgaCard>
            </DgaGridItem>
          ))}

          {/* FAQ */}
          <DgaGridItem colSpan={12} style={{ marginTop: 'var(--spacing-8)' }}>
            <h2 style={{ color: 'var(--text-primary)', marginBottom: 'var(--spacing-6)' }}>{t.faq}</h2>
            {faqs.map((faq, i) => (
              <DgaAccordion key={i} title={faq.q} style={{ marginBottom: 'var(--spacing-2)' }}>
                <p style={{ color: 'var(--text-secondary)', padding: 'var(--spacing-4)' }}>{faq.a}</p>
              </DgaAccordion>
            ))}
          </DgaGridItem>

          {/* Contact */}
          <DgaGridItem colSpan={12} style={{ marginTop: 'var(--spacing-8)' }}>
            <h2 style={{ marginBottom: 'var(--spacing-6)' }}>{t.contact}</h2>
          </DgaGridItem>
          {[
            { icon: 'phone-01', label: lang === 'ar' ? 'اتصل بنا' : 'Call Us', action: lang === 'ar' ? 'اتصل الآن' : 'Call Now' },
            { icon: 'mail-01',  label: lang === 'ar' ? 'راسلنا'   : 'Email Us', action: lang === 'ar' ? 'أرسل بريدًا' : 'Send Email' },
            { icon: 'message-circle-01', label: lang === 'ar' ? 'الدردشة' : 'Live Chat', action: lang === 'ar' ? 'ابدأ المحادثة' : 'Start Chat' },
          ].map(c => (
            <DgaGridItem key={c.icon} colSpan={4}>
              <DgaCard>
                <DgaFeaturedIcon icon={c.icon} size="medium" color="brand" style="light" circle={true} />
                <h3 style={{ marginTop: 'var(--spacing-3)' }}>{c.label}</h3>
                <DgaButton variant="secondary-outline" size="md" label={c.action} onOnClick={() => {}} />
              </DgaCard>
            </DgaGridItem>
          ))}

        </DgaGridContainer>
      </main>

      <DgaFooter />
    </div>
  );
}
```

## RTL / ARABIC
```tsx
<HelpSupportPage rtl={true} lang="ar" />
```
