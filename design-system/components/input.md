# حقل الإدخال — Input

> القيم من [tokens.md](../foundations/tokens.md). تركيب الحقول في نموذج: [form.md](form.md).

## 1. متى يُستخدم
لإدخال نصّ حرّ قصير في سطر واحد: اسم، بريد، هاتف، رقم، بحث. ولنصّ متعدّد الأسطر استخدم `textarea` بالقواعد نفسها.

## 2. متى لا يُستخدم
- لخيارات محدّدة من قائمة → [select](select.md) أو [checkbox](checkbox.md).
- كبديل عن التسمية: ممنوع استخدام `placeholder` تسميةً (ممنوع #5/§قواعد النصوص).
- لإجراء → [button](button.md).

## 3. الحالات
`default` (حدّ `--color-border-default`) · `hover` (`--color-border-strong`) · `focus` (`--color-border-focus` + `--shadow-focus`) · `filled` · `error` (`--color-danger-border` + رسالة + `aria-invalid`) · `disabled` (`--color-bg-disabled`) · `readonly`.
الخطأ يظهر في مكان ثابت تحت الحقل — **بلا قفز تخطيط**.

## 4. المقاسات
- الارتفاع `--size-control-md` (40)؛ مضغوط `--size-control-sm` (32).
- الحشو الأفقي `--space-md`، الزاوية `--radius-md`، الحدّ `--border-width`.
- نصّ `--font-size-md`؛ التسمية فوقه `--font-weight-medium`.
- مسافات القرب: تسمية↔حقل `--space-xs`، حقل↔حقل `--space-md`.

## 5. قواعد النصوص
- **التسمية دائمًا ظاهرة فوق الحقل.**
- `placeholder` = مثال تنسيق لا تعليمات: «مثال: 0512345678».
- المطلوب بـ`*`، أو الاختياري بـ«(اختياري)» — نهج واحد ثابت.
- الخطأ يصف الشرط الصحيح لا اللوم ([ux-writing](../foundations/ux-writing.md)).

## 6. قواعد RTL
- الحقل العربي `dir` يتبع الجذر (rtl)، المؤشّر يبدأ يمينًا.
- البريد/URL/الأرقام: `dir="ltr"` على الحقل، مع بقاء التسمية والخطأ RTL، وعزل bidi ([rtl-guidelines §4-5](../foundations/rtl-guidelines.md)).
- أيقونة الحالة/المسح في الجهة المنطقية (`inline-end`).

## 7. أمثلة صحيحة
- «البريد الإلكتروني» (تسمية) + حقل `dir="ltr"` + مساعدة «نرسل التأكيد إليه».
- حقل رقم بـ`tabular-nums` ومحاذاة مناسبة.
- خطأ: «أدخل رقمًا يبدأ بـ 05 ومكوّنًا من 10 أرقام.»

## 8. أمثلة خاطئة
- placeholder «الاسم» بلا تسمية (يختفي عند الكتابة).
- تحقّق فوري عند كل حرف (مزعج) — تحقّق عند blur/الإرسال.
- قفز التخطيط عند ظهور الخطأ.
- خطأ «إدخال غير صالح» بلا توجيه.

## 9. علاقته بالتوكنز
- الحدود: `--color-border-default`/`-strong`/`-focus`/`--color-danger-border`.
- الخلفية: `--color-bg-surface` / `--color-bg-disabled`.
- النصّ: `--color-text-primary` / `--color-text-tertiary` (مساعدة) / `--color-danger-fg` (خطأ).
- القياس: `--size-control-*` · `--space-*` · `--radius-md` · `--shadow-focus`.

## 10. منع التحكّم الأصلي + البصري (Native control prevention)
- **لا تحكّم بمظهر المتصفّح الأصلي**: أعد ضبط المظهر عند اللزوم (`appearance:none`)؛ لا حدّ/تركيز افتراضي للنظام.
- حالات `focus`/`hover`/`error` **من التوكنز** (`--shadow-focus`/`--color-border-strong`/`--color-danger-border`) — لا حلقة المتصفّح الزرقاء.
- placeholder بلون `--color-text-tertiary` (muted) لا أسود.
- أي أيقونة (حالة/مسح) من [icon-system](../foundations/icon-system.md)، في الجهة المنطقية (`inline-end`)؛ حقول البريد/الأرقام `dir="ltr"` مع بقاء التسمية RTL.
