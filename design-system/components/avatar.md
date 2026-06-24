# الصورة الرمزية — Avatar

> تمثيل بصري لكيان (مستخدم/شركة/مرشد). القيم من [tokens.md](../foundations/tokens.md). **ممنوع إنشاء avatar ad-hoc بكلاس `.avatar` بلا هذا العقد** (ظهر في dogfood v2.1.0 — أُغلق هنا).

## 1. متى يُستخدم
لتمثيل شخص/كيان بجانب اسمه أو بدلًا عنه: صفّ جدول، رأس تفاصيل، assignee chip، قائمة أعضاء.

## 2. متى لا يُستخدم
- أيقونة وظيفية عامة (استخدم [icon-system](../foundations/icon-system.md)).
- شعار علامة في الرأس/الفوتر (ليس avatar).
- حشو بصري بلا كيان حقيقي.

## التشريح (Anatomy)
```
[ الحاوية (دائرة) ]  ← صورة | أحرف أولى | أيقونة fallback
   └ (اختياري) نقطة حالة في الزاوية المنطقية
```

## 3. الأنواع (Variants)
- **initials** — أول حرفين من الاسم؛ خلفية منخفضة التوكيد (`--color-accent-subtle`)، نصّ `--color-accent`. الافتراضي حين لا صورة.
- **image** — صورة الكيان (`object-fit: cover`، نسبة 1:1).
- **icon fallback** — أيقونة شخص محايدة حين لا صورة ولا اسم (`--color-bg-subtle` + `--color-text-tertiary`).
- **status indicator** (عند الحاجة فقط) — نقطة في الزاوية المنطقية بألوان الحالة الدلالية.

## 4. المقاسات (Sizes)
| الحجم | القطر | الاستخدام |
|---|---|---|
| `xs` | 24px | داخل chip / كثافة عالية |
| `sm` | 32px (`--size-control-sm`) | صفّ جدول |
| `md` | 40px (`--size-control-md`) | افتراضي / قوائم |
| `lg` | 48px | رأس تفاصيل |
حجم الأحرف الأولى يتبع المقاس (`--font-size-xs` لـxs/sm، `--font-size-sm`/`-base` للأكبر). نقطة الحالة ≈ ربع القطر.

## الأشكال (Shapes)
- **circle** (`--radius-full`) — الافتراضي للأشخاص.
- **rounded** (`--radius-md`) — للكيانات/الشركات (يميّزها عن الأشخاص).

## 5. الحالات (States)
- `image loaded` — تظهر الصورة.
- `image failed` — يسقط تلقائيًا إلى **initials** ثم **icon fallback** (لا مربّع مكسور).
- `missing image` — initials مباشرة.
- `loading/skeleton` — دائرة skeleton بنفس القطر ([skeleton](skeleton.md)).

## 6. قواعد RTL
- نقطة الحالة في الزاوية المنطقية (`inset-block-end`/`inset-inline-end`)، لا `right` ثابت.
- الأحرف الأولى للاسم العربي طبيعية؛ في صفّ، الـavatar يسبق الاسم في تدفّق RTL (`inline-start`).

## 7. الوصول (Accessibility)
- **decorative حين الاسم بجانبه:** الـavatar `aria-hidden="true"` — **لا تكرّر اسم المستخدم** (ظاهر نصًّا).
- **يحتاج accessible name حين يقف وحده** (بلا نصّ اسم): `<img alt="سارة الفهد">` أو `aria-label` على الحاوية.
- نقطة الحالة ليست اللون وحده — تقترن بنصّ/شارة حالة في مكان قريب (لا تعتمد عليها مفردة لنقل الحالة).

## 8. قواعد اللون
- **لا ألوان عشوائية / لا hex.** توكنز دلالية فقط.
- خلفية الأحرف الأولى **منخفضة التوكيد** (`--color-accent-subtle` أو `--color-bg-subtle`) — لا تنافس الأكسنت كإجراء.
- نقطة الحالة من توكنز الحالة الدلالية (`--color-success-fg`…)، لا تتبع البراند.
- لا حدّ أسود؛ حدّ خفيف اختياري `--color-border-subtle` لفصل الصورة عن سطح فاتح.

## Do / Don't
- **Do:** اجعله decorative متى وُجد الاسم؛ اسقط برشاقة عند فشل الصورة؛ التزم مقاسات/أشكال التوكنز.
- **Don't:** ألوان عشوائية للأحرف؛ تكرار الاسم لقارئ الشاشة؛ نقطة حالة تنقل المعنى وحدها؛ مربّع صورة مكسور؛ كلاس `.avatar` بلا هذا العقد.

## ملاحظات Tailwind
- دائرة: `rounded-full`؛ كيان: `rounded-md`. المقاس عبر `size-*` المربوط بـ`--size-control-*`/توكن.
- الأحرف: `inline-flex items-center justify-center` + `font-semibold` + خلفية/نصّ دلاليان. الصورة: `w-full h-full object-cover`.
- لا قيم arbitrary؛ القطر من توكن (راجع [component-tokens](../foundations/component-tokens.md)).

## أمثلة
- **صفّ جدول:** `sm` initials + اسم بجانبه (الـavatar `aria-hidden`).
- **رأس تفاصيل:** `lg` + اسم + شارة حالة.
- **assignee chip:** `xs` + اسم مختصر داخل [chip](BACKLOG.md) (عند توفّره).

## 9. علاقته بالتوكنز (عقد الربط)
| الجزء/الحالة | التوكن الدلالي |
|---|---|
| خلفية الأحرف | `--color-accent-subtle` (أو `--color-bg-subtle`) |
| نصّ الأحرف | `--color-accent` (أو `--color-text-secondary`) |
| fallback أيقونة | `--color-bg-subtle` + `--color-text-tertiary` |
| حدّ اختياري | `--color-border-subtle` |
| نقطة الحالة | `--color-{success,warning,danger,info}-fg` |
| القطر/الزاوية | `--size-control-*` · `--radius-full`/`--radius-md` |
