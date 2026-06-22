# الزر — Button

> القيم من [tokens.md](../foundations/tokens.md). القالب: 9 أقسام موحّدة عبر كل المكوّنات.

## 1. متى يُستخدم
لإطلاق **إجراء**: حفظ، إرسال، حذف، فتح مودال/درج، تنفيذ عملية. نصّه فعل يصف النتيجة.

## 2. متى لا يُستخدم
- للانتقال بين الصفحات → استخدم رابطًا (`<a>`)، لا زرًا.
- كزينة أو لتعمير فراغ.
- أكثر من زر `primary` واحد في السياق (استخدم ثانويًا للبقية).

## 3. الحالات
`default` · `hover` (`--color-accent-hover` / `--color-bg-hover`) · `active` (`-active`) · `focus-visible` (`--shadow-focus` + `--color-border-focus`، **لا تُزال**) · `disabled` (`--color-bg-disabled`/`--color-text-disabled` + `aria-disabled`) · `loading` (دوّار محلّ الأيقونة، عرض ثابت بلا قفز، تعطيل التفاعل).

## 4. المقاسات
| الحجم | الارتفاع | الحشو الأفقي | الخط |
|---|---|---|---|
| `sm` | `--size-control-sm` 32 | `--space-sm` | `--font-size-sm` |
| `md` (افتراضي) | `--size-control-md` 40 | `--space-md` | `--font-size-md` |
| `lg` | `--size-control-lg` 48 | `--space-lg` | `--font-size-md` |

الزاوية `--radius-md`. منطقة اللمس ≥ `--size-touch-min` (44) ولو صغُر بصريًا.
الأنواع: `primary` · `secondary` · `tertiary` · `danger` (انظر §9).

## 5. قواعد النصوص
- فعل مباشر يصف النتيجة: «احفظ»، «أضف مستخدمًا»، «احذف الطلب».
- لا «موافق/إلغاء» الغامضة في الأفعال الخطرة → «احذف» / «تراجع».
- بلا مبالغة أو إيموجي ([ux-writing](../foundations/ux-writing.md)).

## 6. قواعد RTL
- الأيقونة في `inline-start`، فجوة `--space-2xs`، بخصائص منطقية.
- الأيقونات الاتجاهية (سهم إرسال/تالٍ) تُعكَس؛ غير الاتجاهية لا ([rtl-guidelines](../foundations/rtl-guidelines.md)).

## 7. أمثلة صحيحة
- شاشة بها زر `primary` واحد «احفظ» + `secondary` «تراجع».
- زر أيقونة فقط مع `aria-label="حذف"` ومنطقة لمس 44px.
- زر تحميل يحفظ عرضه ويعطّل النقر.

## 8. أمثلة خاطئة
- زرّان `primary` متجاوران بنفس الوزن (ممنوع #14).
- `<div onClick>` بدل `<button>` (يكسر الوصول).
- إزالة `outline` بلا حلقة بديلة (ممنوع #15).
- لون زر بـhex يدوي (ممنوع #11).

## 9. علاقته بالتوكنز
- اللون: `--color-accent` / `-hover` / `-active` / `--color-text-on-accent` (primary)؛ `--color-bg-surface` + `--color-border-default` (secondary)؛ شفّاف (tertiary)؛ `--color-danger-fg` (danger).
- القياس: `--size-control-*` · `--space-*` · `--radius-md`.
- التركيز: `--shadow-focus` · `--color-border-focus`.
- الخط: `--font-size-*` · `--font-weight-semibold`.
