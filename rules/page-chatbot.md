---
name: dga-page-chatbot
description: DGA Chatbot widget — floating button and drawer pattern
metadata:
  tags: dga, chatbot, drawer, template
---


## SOURCE
Figma: https://www.figma.com/design/JShAEohGrQ5SBKzL8NqIa7/

---

## SECTIONS & COMPONENTS

**Trigger Button** — DgaButton (floating, icon-only) or DgaFloatingButton
**Chat Drawer** — DgaDrawer (position=right or bottom)
  - Header: DgaAvatar (bot), title, DgaButton (close)
  - Messages: DgaCard per message bubble
  - Input: DgaTextInput + DgaButton (send)
  - Quick replies: DgaChip row

---

## REACT TEMPLATE

```tsx
import {
  DgaButton, DgaDrawer, DgaAvatar, DgaCard,
  DgaTextInput, DgaChip, DgaGridContainer, DgaGridItem,
} from 'platformscode-new-react';
import 'platformscode-new-react/dist/style.css';
import { useState, useRef, useEffect } from 'react';

interface Message { id: number; role: 'user' | 'bot'; text: string; }

export function ChatbotWidget({ rtl = false, lang = 'en' }) {
  const [open, setOpen]       = useState(false);
  const [input, setInput]     = useState('');
  const [messages, setMessages] = useState<Message[]>([
    { id: 1, role: 'bot', text: lang === 'ar' ? 'مرحبًا! كيف يمكنني مساعدتك اليوم؟' : 'Hello! How can I help you today?' },
  ]);
  const bottomRef = useRef<HTMLDivElement>(null);

  const quickReplies = lang === 'ar'
    ? ['الخدمات المتاحة', 'تتبع طلبي', 'تواصل مع الدعم']
    : ['Available Services', 'Track My Request', 'Contact Support'];

  useEffect(() => { bottomRef.current?.scrollIntoView({ behavior: 'smooth' }); }, [messages]);

  function send(text?: string) {
    const msg = text || input;
    if (!msg.trim()) return;
    const id = Date.now();
    setMessages(m => [
      ...m,
      { id, role: 'user', text: msg },
      { id: id + 1, role: 'bot', text: lang === 'ar' ? 'شكرًا على سؤالك. سأبحث عن إجابة لك...' : 'Thank you for your question. Let me look that up for you...' },
    ]);
    setInput('');
  }

  return (
    <>
      {/* Floating trigger */}
      <div style={{ position: 'fixed', bottom: 'var(--spacing-6)', [rtl ? 'left' : 'right']: 'var(--spacing-6)', zIndex: 1000 }}>
        <DgaButton
          variant="primary-brand"
          size="lg"
          iconOnly={true}
          leadIcon={true}
          leadIconType="message-circle-01"
          leadIconProps={{ variant: 'solid', type: 'rounded', size: 24 }}
          onOnClick={() => setOpen(true)}
          sx={{ borderRadius: 'var(--radius-full)', width: '56px', height: '56px', boxShadow: 'var(--shadow-xl)' }}
        />
      </div>

      {/* Chat Drawer */}
      <DgaDrawer
        open={open}
        position={rtl ? 'left' : 'right'}
        size="400px"
        onClose={() => setOpen(false)}
      >
        {/* Drawer Header */}
        <div style={{
          display: 'flex', alignItems: 'center', gap: 'var(--spacing-3)',
          padding: 'var(--spacing-4)', borderBottom: '1px solid var(--border-primary)',
          background: 'var(--colors-primary-sa-flag-600)',
        }}>
          <DgaAvatar type="icon" icon={{ name: 'cpu-chip-01', variant: 'solid', type: 'rounded' }} size="md"
            sx={{ background: 'var(--colors-primary-sa-flag-400)' }} />
          <div style={{ flex: 1 }}>
            <p style={{ color: '#fff', fontWeight: 600, margin: 0 }}>{lang === 'ar' ? 'المساعد الذكي' : 'AI Assistant'}</p>
            <p style={{ color: 'var(--colors-primary-sa-flag-100)', fontSize: '12px', margin: 0 }}>
              {lang === 'ar' ? 'متاح الآن' : 'Online'}
            </p>
          </div>
          <DgaButton variant="subtle" size="sm" iconOnly={true}
            leadIcon={true} leadIconType="x-close"
            leadIconProps={{ variant: 'stroke', type: 'rounded', size: 20 }}
            sx={{ color: '#fff' }}
            onOnClick={() => setOpen(false)} />
        </div>

        {/* Messages */}
        <div style={{ flex: 1, overflowY: 'auto', padding: 'var(--spacing-4)', display: 'flex', flexDirection: 'column', gap: 'var(--spacing-3)' }}>
          {messages.map(msg => (
            <div key={msg.id} style={{
              display: 'flex',
              justifyContent: msg.role === 'user' ? (rtl ? 'flex-start' : 'flex-end') : (rtl ? 'flex-end' : 'flex-start'),
            }}>
              <div style={{
                maxWidth: '75%',
                background: msg.role === 'user' ? 'var(--colors-primary-sa-flag-600)' : 'var(--background-secondary)',
                color: msg.role === 'user' ? '#fff' : 'var(--text-primary)',
                padding: 'var(--spacing-3)',
                borderRadius: 'var(--radius-md)',
                fontSize: '14px',
                lineHeight: '1.5',
              }}>
                {msg.text}
              </div>
            </div>
          ))}
          <div ref={bottomRef} />
        </div>

        {/* Quick Replies */}
        <div style={{ padding: '0 var(--spacing-4)', display: 'flex', gap: 'var(--spacing-2)', flexWrap: 'wrap' }}>
          {quickReplies.map(r => (
            <DgaChip key={r} label={r} onOnClick={() => send(r)} sx={{ cursor: 'pointer' }} />
          ))}
        </div>

        {/* Input */}
        <div style={{
          display: 'flex', gap: 'var(--spacing-2)',
          padding: 'var(--spacing-4)', borderTop: '1px solid var(--border-primary)',
        }}>
          <DgaTextInput
            placeholder={lang === 'ar' ? 'اكتب رسالتك...' : 'Type your message...'}
            value={input}
            style={{ flex: 1 }}
            onOnChange={e => setInput(e.detail)}
          />
          <DgaButton variant="primary-brand" size="md" iconOnly={true}
            leadIcon={true} leadIconType="send-01"
            leadIconProps={{ variant: 'solid', type: 'rounded', size: 20 }}
            disabled={!input.trim()}
            onOnClick={() => send()} />
        </div>
      </DgaDrawer>
    </>
  );
}
```

## KEY NOTES
- `DgaDrawer` — `position`: `left` | `right` | `top` | `bottom` — use `right` for LTR, `left` for RTL
- Message bubbles are plain divs styled with CSS tokens — no DGA component wraps every bubble
- `DgaChip` for quick reply buttons — `onOnClick` event

## RTL
```tsx
<ChatbotWidget rtl={true} lang="ar" />
```
