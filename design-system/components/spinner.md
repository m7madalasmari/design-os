# المؤشّر الدوّار — Spinner

> القيم من [tokens.md](../foundations/tokens.md). بدائيّة تحميل قصيرة. للتحميل ذي الشكل المعروف استخدم [skeleton](skeleton.md).

## الغرض (Purpose)
مؤشّر دائري متحرّك يدلّ على عملية **قصيرة غير محدّدة المدة** جارية الآن (إرسال، جلب خفيف).

## متى يُستخدم (When to use)
- داخل زر أثناء الإرسال (محلّ الأيقونة، بعرض ثابت).
- تحميل خفيف قصير (~أقل من ثانية) لمنطقة صغيرة أو inline.
- مؤشّر «جارٍ…» في select/قائمة أثناء جلب الخيارات.

## متى لا يُستخدم (When not to use)
- **تحميل بيانات جدول/قائمة/كرت** → [skeleton](skeleton.md) (لا spinner دائم بديلًا عنه).
- تحميل صفحة كاملة طويل → skeleton أو شريط تقدّم.
- لا كزخرفة دائمة أو حركة بلا معنى (ممنوع #6).

## التشريح (Anatomy)
دائرة بحدّ بسماكة `--border-width-strong`؛ معظم المحيط بلون خافت (`--color-border-default`) وقوس واحد بلون `currentColor` يدور. القطر = أحد مقاسات الأيقونة.

## الأنواع (Variants)
- `default` — `currentColor` (يرث لون النص المحيط).
- `on-accent` — داخل زر primary، القوس `--color-text-on-accent`.
- `muted` — على سطح هادئ، القوس `--color-text-secondary`.

## المقاسات (Sizes)
`sm` 16 (`--size-icon-sm`) · `md` 20 (`--size-icon-md`) · `lg` 24 (`--size-icon-lg`). السماكة 2px ثابتة.

## الحالات (States)
حالة واحدة: `spinning`. مع `prefers-reduced-motion: reduce` يتوقّف الدوران (يظهر ثابتًا أو يُستبدل بنص «جارٍ…»).

## سلوك RTL
غير اتجاهي — **لا يُعكَس**؛ اتجاه الدوران ثابت في الاتجاهين ([rtl-guidelines §3](../foundations/rtl-guidelines.md)).

## الوصول (Accessibility)
- **زخرفي** (بجانب نصّ «جارٍ الحفظ…») → `aria-hidden="true"`.
- **يحمل المعنى وحده** (لا نصّ مصاحب) → `role="status"` + `aria-label` عربي («جارٍ التحميل»). لا يُترك بلا أي إعلان لقارئ الشاشة.

## استخدام Tailwind
`size-4`/`size-5`/`size-6` · `border-2` · `rounded-full` · `animate-spin` · `motion-reduce:animate-none`. القوس عبر `border-block-start-color: currentColor`.

## التوكنز (Token usage)
`--size-icon-sm/md/lg` · `--border-width-strong` · `--duration-*`/`--ease-standard` (الحركة) · ألوان عبر `currentColor` و`--color-border-default`.

## معايير القبول البصري (Visual acceptance criteria)
- القطر = مقاس الأيقونة المختار؛ السماكة 2px.
- دوران ناعم منتظم (~0.8s linear)، بلا قفزات.
- داخل الزر: **عرض الزر ثابت** لا يقفز عند ظهور/اختفاء المؤشّر.
- يحترم `prefers-reduced-motion`.

## أنماط ممنوعة (Anti-patterns)
- spinner لتحميل جدول طويل (استخدم skeleton).
- spinner لمدة طويلة بلا سقف (يوحي بالتعليق) → استخدم تقدّمًا/skeleton.
- spinner بلا `aria-hidden` ولا `role=status`.
- ألوان hex يدوية للقوس (ممنوع #11).

## أمثلة (Examples)
- زر primary «جارٍ الحفظ…» مع spinner `on-accent` محلّ الأيقونة، الزر معطّل.
- [select](select.md) `loading`: spinner `sm` + «جارٍ الجلب…» داخل القائمة.
- مؤشّر inline بجانب «جارٍ التحديث» في شريط أدوات.
