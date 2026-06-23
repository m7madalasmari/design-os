# حقل البحث — Search Input

> القيم من [tokens.md](../foundations/tokens.md). تخصيص لـ[input](input.md) لحالة البحث. يصاحب [filter-bar](filter-bar.md). الأيقونات من [icon-system](../foundations/icon-system.md).

## الغرض (Purpose)
حقل لإدخال نصّ بحث يضيّق قائمة/جدولًا، بأيقونة بحث وزر مسح اختياري.

## متى يُستخدم (When to use)
- أعلى جدول/قائمة كبيرة (داخل [filter-bar](filter-bar.md) أو مستقلًّا).
- بحث فوري أو عند الإرسال ضمن نطاق محدّد.

## متى لا يُستخدم (When not to use)
- إدخال نصّ عام (اسم/بريد) → [input](input.md).
- اختيار من قائمة معروفة → [select](select.md) قابل للبحث.

## التشريح (Anatomy)
مجموعة (input-group) بحدّ وزاوية: **أيقونة بحث** (`search` من icon-system) في `inline-start` + **حقل** بلا حدّ داخلي + **زر مسح** (`x`) اختياري في `inline-end`. الحدّ وحلقة التركيز على **المجموعة** لا على الحقل الداخلي.

## الأنواع (Variants)
- `basic` — أيقونة + حقل.
- `with-clear` — + زر مسح يظهر عند وجود قيمة.

## المقاسات (Sizes)
الارتفاع `--size-control-md` (40) أو `--size-control-sm` (32)؛ ليطابق ارتفاع الأزرار/الشرائح في filter-bar. حشو أفقي `--space-sm`/`--space-md`، زاوية `--radius-md`.

## الحالات (States)
`default` · `hover` (`--color-border-strong`) · `focus` (حلقة `--shadow-focus` على المجموعة) · `filled` (يظهر زر المسح) · `disabled` (`--color-bg-disabled`) · `loading` (مؤشّر [spinner](spinner.md) `sm` محلّ أيقونة البحث) · `error` (نادر — `--color-danger-border` إن كان البحث مُتحقَّقًا).

## سلوك RTL
- أيقونة البحث في `inline-start` (يمين)، **غير اتجاهية فلا تُعكَس**.
- زر المسح `×` في `inline-end` (يسار).
- النصّ والمؤشّر يبدآن من اليمين؛ حشو بخصائص منطقية ([rtl-guidelines](../foundations/rtl-guidelines.md)).

## الوصول (Accessibility)
- `aria-label` عربي على الحقل («بحث») إن لم تكن هناك تسمية ظاهرة.
- زر المسح زرّ حقيقي بـ`aria-label="مسح البحث"`.
- أيقونة البحث `aria-hidden="true"`.
- حلقة التركيز ظاهرة ولا تُزال.

## استخدام Tailwind
المجموعة: `inline-flex items-center gap-2 h-10 ps-3 pe-3 bg-card border border-border rounded-md transition-colors focus-within:ring`؛ الحقل: `bg-transparent outline-none text-sm w-full` (بلا حدّ داخلي)؛ الأيقونة `size-5 text-muted-foreground`؛ المسح `size-5`.

## التوكنز (Token usage)
`--size-control-sm/md` · `--space-sm`/`-md`/`-2xs` · `--radius-md` · `--color-bg-surface` · `--color-border-default`/`-strong` · `--color-text-primary` (النصّ) · `--color-text-tertiary` (placeholder) · `--shadow-focus` · `--size-icon-md`.

## معايير القبول البصري (Visual acceptance criteria)
- **لا حدّ أصلي داخلي** للحقل (`appearance:none`, `outline:none`, `border:0`)؛ الحدّ على المجموعة فقط.
- placeholder بلون `--color-text-tertiary` (muted) لا أسود.
- حلقة التركيز من التوكن (`--shadow-focus`) لا حلقة المتصفّح الافتراضية.
- يحاذي ارتفاعُه أزرارَ/شرائحَ filter-bar (نفس control token).
- أيقونة البحث `inline-start`، المسح `inline-end`.

## أنماط ممنوعة (Anti-patterns)
- حدّ أصلي مزدوج (حدّ المجموعة + حدّ الحقل الداخلي).
- placeholder كتسمية (يختفي عند الكتابة) → استخدم تسمية/`aria-label`.
- أيقونة بحث معكوسة في RTL.
- حلقة تركيز المتصفّح الزرقاء بدل توكن الحلقة.
- ارتفاع لا يطابق بقية عناصر filter-bar (محاذاة مكسورة).

## أمثلة (Examples)
- «ابحث في الطلبات» مع أيقونة بحث يمينًا، يحاذي شرائح الحالة.
- `with-clear`: تظهر «×» عند الكتابة، تمسح وتعيد التركيز للحقل.
- `loading`: spinner محلّ أيقونة البحث أثناء الجلب.
