# 04 — Arabic RTL & UX Writing

> Apply whenever the interface is Arabic (or mixes Arabic with Latin/numbers). This is the agent checklist; deeper rules live in [`rtl-guidelines.md`](../design-system/foundations/rtl-guidelines.md), [`ux-writing.md`](../design-system/foundations/ux-writing.md), [`typography.md`](../design-system/foundations/typography.md). This file is self-contained on the points below.

## 1. Page direction (RTL)
- Root: `<html dir="rtl" lang="ar">` (or `dir="rtl"` on the Arabic block).
- **Logical properties only**: `margin-inline-start`, `padding-inline-end`, `inset-inline-*`, `border-inline-*`. Never `left`/`right` for layout.
- **Tailwind (logical utilities only):** `ms-*`/`me-*` (not `ml`/`mr`) · `ps-*`/`pe-*` (not `pl`/`pr`) · `start-*`/`end-*` (not `left`/`right`) · `text-start`/`text-end` (not `text-left`/`text-right`) · `border-s`/`border-e`. Never directional utilities in RTL.
- Mirror: layout, sidebars, directional icons (arrows, chevrons, back/next, send, progress). Do **not** mirror: numbers, logos, media controls, checkmarks, non-directional icons, Latin text.

## 2. Text alignment
- Default `text-align: start` → resolves to the right in RTL. **Never hard-code `text-align: right`** (breaks if the block flips to LTR).
- No `justify` in UI (creates rivers, hurts Arabic readability).
- Tailwind: `text-start` / `text-end` — never `text-left` / `text-right`.

## 3. Icon position inside buttons
- Icon at `inline-start` (logical) → renders to the **right** of the Arabic label. Gap `--space-2xs`.
- Directional icons (send, next) mirror with direction; non-directional (search, settings) do not.
- Icon-only button requires an Arabic `aria-label`.
- Tailwind: position the icon with `ms-*`/`me-*`; mirror directional icons with `rtl:-scale-x-100` (or a logical icon variant) — never by hard-coding a side.

## 4. The "+" sign — two cases
- **Action affordance** (add): the "+" is a leading icon at `inline-start` → sits to the **right** of the label. Button reads «إضافة» with the + on its right side. Never hard-position it left/right; let direction place it.
- **Numeric sign** (`+12%`, `+5`): the sign stays glued to its number, and the whole token is LTR-isolated (`<bdi>` / `unicode-bidi: isolate`) so it never reorders. Use Latin tabular numerals.

## 5. Numbers & dates
- Latin digits (0–9) with `font-variant-numeric: tabular-nums` by default. **One numeral system per screen** — never mix Western (0-9) and Eastern (٠-٩).
- One unified date format across the app, e.g. «22 يونيو 2026». Hijri only as a locale-level option, never ad-hoc per element.
- Currency/percent symbols stay attached to the number, bidi-isolated: «1,250.00 ر.س» · «85%».

## 6. Empty states
- Structure: title (a real heading — see [`empty-state.md`](../design-system/components/empty-state.md)) + one-line description + one action.
- Tone: calm, professional. No marketing, no emoji.
- Examples:
  - First use: «لم تُضِف أي عميل بعد» + زر «أضف أول عميل».
  - No results: «لا نتائج تطابق هذه الفلاتر» + رابط «امسح الفلاتر».
  - Error: «تعذّر تحميل البيانات» + زر «أعد المحاولة».

## 7. Labels & placeholders
- The **label is always visible**, above the field. Never use a placeholder as the label (it disappears on input and fails accessibility).
- Placeholder = a **format example**, not an instruction: «مثال: 0512345678».
- Mark required with `*` (or mark optional with «(اختياري)») — pick one convention, do not mix.

## 8. Error messages
- Pattern: **[what happened] + [how to fix]**. No blame, no error codes, no jargon.
- Bad: «إدخال غير صالح».  Good: «أدخل رقم جوال يبدأ بـ 05 ويتكوّن من 10 أرقام.»
- System error: brief, with a next step: «تعذّر الاتصال بالخادم. حدّث الصفحة، وإن تكرّر تواصل مع الدعم.»

## 9. Primary vs secondary button
- **One primary action** per context/screen — filled, the brand action color. Everything else is secondary (outlined) or tertiary (ghost). Destructive = danger style + confirmation.
- Labels are **verbs**: «احفظ» · «أضف مستخدمًا» · «احذف». In confirmations use the verb, not «نعم/لا» (e.g., «احذف» / «تراجع»).
- Multiple buttons must show a clear visual priority — no row of equal-weight buttons (forbidden #14).

## 10. No literal translation
- Do not translate English UI strings word-for-word. Use natural, idiomatic Arabic.
- «Get started» → «ابدأ الآن» (not «احصل على البدء») · «Learn more» → «اعرف المزيد» · «Submit» → «أرسِل» · «Back» → «رجوع».
- One term per concept (glossary in [`ux-writing.md`](../design-system/foundations/ux-writing.md)) — no synonyms for the same action.

## 11. No long text in buttons
- A button holds a short **verb** (1–3 words), not a sentence. Move explanation to helper text or context.
- Bad: «اضغط هنا لإضافة عميل جديد إلى النظام».  Good: «أضف عميلًا».
- Truncate overflow with ellipsis; never let a button wrap to three lines.

## QA hook
These points are verified in [`03-pixel-qa.md`](03-pixel-qa.md) and the RTL + UX-writing sections of [`qa-checklist.md`](../design-system/rules/qa-checklist.md).
