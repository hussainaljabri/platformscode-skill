---
name: dga-page-form
description: DGA multi-step government form page template
metadata:
  tags: dga, form, application, multi-step, template
---


If no framework specified, ask: "Which framework? (react / angular / vue / svelte / html)"
If no form type specified, generate a general-purpose government service form.

## SOURCE
Figma: https://www.figma.com/design/YeaDX1gteyFjRxdldJGpA3/

---

## SECTIONS & COMPONENTS

**Header** — DgaHeader
**Breadcrumbs** — DgaBreadcrumbs
**Form Header** — Heading, DgaFeaturedIcon, description text
**Progress Indicator** (multi-step forms) — DgaProgressIndicator, DgaProgressIndicatorStep
**Form Fields** — DgaTextInput, DgaDropdown, DgaDatepicker, DgaTextarea, DgaCheckbox, DgaRadioButton, DgaFileUpload
**Form Actions** — DgaButton (primary=Submit, secondary=Cancel/Back)
**Helper Text** — DgaInlineAlert type="info" for field instructions
**Footer** — DgaFooter

---

## RULES
1. Never use `<input>`, `<select>`, `<textarea>` — use DGA equivalents
2. All form field events: `onOnChange` (except DgaDatepicker which uses `onChange`)
3. Button events: `onOnClick` — NOT `onClick`
4. Required fields: use `required` prop on DgaTextInput, not HTML `required` attribute
5. Error states: use `error` boolean + `helperText` string on form fields
6. `DgaProgressIndicator` takes step objects array

---

## REACT TEMPLATE

```tsx
import {
  DgaHeader, DgaFooter, DgaBreadcrumbs,
  DgaTextInput, DgaDropdown, DgaDatepicker, DgaTextarea,
  DgaCheckbox, DgaRadioButton, DgaFileUpload,
  DgaButton, DgaFeaturedIcon, DgaInlineAlert,
  DgaProgressIndicator, DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';
import { useState } from 'react';

export function FormPage({ rtl = false, lang = 'en' }) {
  const [step, setStep] = useState(0);
  const [form, setForm] = useState({
    fullName: '', idNumber: '', email: '', phone: '',
    dob: null, gender: '', city: '', details: '',
    attachments: null, agree: false,
  });
  const [errors, setErrors] = useState({});
  const [submitted, setSubmitted] = useState(false);

  const t = {
    title:    lang === 'ar' ? 'تقديم طلب'         : 'Submit Application',
    step1:    lang === 'ar' ? 'المعلومات الشخصية'  : 'Personal Information',
    step2:    lang === 'ar' ? 'تفاصيل الطلب'       : 'Request Details',
    step3:    lang === 'ar' ? 'المستندات'           : 'Documents',
    fullName: lang === 'ar' ? 'الاسم الكامل'        : 'Full Name',
    idNumber: lang === 'ar' ? 'رقم الهوية'          : 'ID Number',
    email:    lang === 'ar' ? 'البريد الإلكتروني'   : 'Email Address',
    phone:    lang === 'ar' ? 'رقم الجوال'          : 'Phone Number',
    dob:      lang === 'ar' ? 'تاريخ الميلاد'       : 'Date of Birth',
    gender:   lang === 'ar' ? 'الجنس'              : 'Gender',
    city:     lang === 'ar' ? 'المدينة'             : 'City',
    details:  lang === 'ar' ? 'تفاصيل الطلب'        : 'Request Details',
    attach:   lang === 'ar' ? 'إرفاق المستندات'     : 'Attach Documents',
    agree:    lang === 'ar' ? 'أوافق على الشروط والأحكام' : 'I agree to the Terms and Conditions',
    next:     lang === 'ar' ? 'التالي'              : 'Next',
    back:     lang === 'ar' ? 'السابق'              : 'Back',
    submit:   lang === 'ar' ? 'تقديم الطلب'         : 'Submit Application',
    success:  lang === 'ar' ? 'تم تقديم طلبك بنجاح!' : 'Your application was submitted successfully!',
  };

  const steps = [
    { id: 'personal', label: t.step1 },
    { id: 'details',  label: t.step2 },
    { id: 'docs',     label: t.step3 },
  ];

  const cities = lang === 'ar'
    ? [{ label: 'الرياض', value: 'riyadh' }, { label: 'جدة', value: 'jeddah' }, { label: 'الدمام', value: 'dammam' }]
    : [{ label: 'Riyadh', value: 'riyadh' }, { label: 'Jeddah', value: 'jeddah' }, { label: 'Dammam', value: 'dammam' }];

  function update(field, value) { setForm(f => ({ ...f, [field]: value })); }

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

          <DgaGridItem colSpan={12} style={{ textAlign: 'center', marginBottom: 'var(--spacing-4)' }}>
            <DgaFeaturedIcon icon="file-plus-01" size="large" color="brand" style="light" circle={true} />
            <h1 style={{ marginTop: 'var(--spacing-4)' }}>{t.title}</h1>
          </DgaGridItem>

          {/* Progress */}
          <DgaGridItem colSpan={12}>
            <DgaProgressIndicator currentStep={step} onStepChange={e => setStep(e.detail)}>
              {steps.map((s, i) => <DgaProgressIndicatorStep key={s.id} label={s.label} />)}
            </DgaProgressIndicator>
          </DgaGridItem>

          {submitted ? (
            <DgaGridItem colSpan={12}>
              <DgaInlineAlert type="success" title={t.success} />
            </DgaGridItem>
          ) : (
            <>
              {/* Step 1: Personal Info */}
              {step === 0 && (
                <>
                  <DgaGridItem colSpan={6}>
                    <DgaTextInput label={t.fullName} required error={!!errors.fullName} helperText={errors.fullName}
                      onOnChange={e => update('fullName', e.detail)} />
                  </DgaGridItem>
                  <DgaGridItem colSpan={6}>
                    <DgaTextInput label={t.idNumber} required onOnChange={e => update('idNumber', e.detail)} />
                  </DgaGridItem>
                  <DgaGridItem colSpan={6}>
                    <DgaTextInput label={t.email} type="email" required onOnChange={e => update('email', e.detail)} />
                  </DgaGridItem>
                  <DgaGridItem colSpan={6}>
                    <DgaTextInput label={t.phone} type="tel" required onOnChange={e => update('phone', e.detail)} />
                  </DgaGridItem>
                  <DgaGridItem colSpan={6}>
                    <DgaDatepicker label={t.dob} onChange={e => update('dob', e.detail)} />
                  </DgaGridItem>
                  <DgaGridItem colSpan={6}>
                    <DgaDropdown label={t.city} options={cities} onOnChange={e => update('city', e.detail)} />
                  </DgaGridItem>
                </>
              )}

              {/* Step 2: Details */}
              {step === 1 && (
                <DgaGridItem colSpan={12}>
                  <DgaTextarea label={t.details} rows={6} onOnChange={e => update('details', e.detail)} />
                </DgaGridItem>
              )}

              {/* Step 3: Documents */}
              {step === 2 && (
                <>
                  <DgaGridItem colSpan={12}>
                    <DgaFileUpload label={t.attach} multiple accept=".pdf,.jpg,.png"
                      onOnChange={e => update('attachments', e.detail)} />
                  </DgaGridItem>
                  <DgaGridItem colSpan={12}>
                    <DgaCheckbox label={t.agree} onOnChange={e => update('agree', e.detail)} />
                  </DgaGridItem>
                </>
              )}

              {/* Navigation */}
              <DgaGridItem colSpan={12} style={{ display: 'flex', gap: 'var(--spacing-3)', justifyContent: 'flex-end' }}>
                {step > 0 && (
                  <DgaButton variant="secondary-outline" size="md" label={t.back} onOnClick={() => setStep(s => s - 1)} />
                )}
                {step < steps.length - 1 ? (
                  <DgaButton variant="primary-brand" size="md" label={t.next} onOnClick={() => setStep(s => s + 1)} />
                ) : (
                  <DgaButton variant="primary-brand" size="md" label={t.submit}
                    disabled={!form.agree} onOnClick={() => setSubmitted(true)} />
                )}
              </DgaGridItem>
            </>
          )}

        </DgaGridContainer>
      </main>
      <DgaFooter />
    </div>
  );
}
```

## RTL / ARABIC
```tsx
<FormPage rtl={true} lang="ar" />
```
