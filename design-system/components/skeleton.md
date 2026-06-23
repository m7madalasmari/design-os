# الهيكل العظمي — Skeleton

> القيم من [tokens.md](../foundations/tokens.md). مكوّن موثّق (لم يعد وصفًا ضمنيًا داخل [table](table.md)). للتحميل القصير داخل زر استخدم [spinner](spinner.md).

## الغرض (Purpose)
عنصر نائب رمادي يحاكي **شكل المحتوى** أثناء جلبه، فيقلّل قفز التخطيط ويحسّن إدراك الانتظار.

## متى يُستخدم (When to use)
- تحميل محتوى **معروف الشكل** (جدول، كرت، قائمة، ملف تعريف) ومدّته أطول من لحظة.
- أول تحميل لمنطقة ستُملأ ببيانات بهيكل متوقّع.

## متى لا يُستخدم (When not to use)
- **محتوى نهائي** (ليس نائبًا).
- زخرفة (ممنوع #6).
- لا بيانات بعد الجلب → [empty-state](empty-state.md) (لا skeleton دائم).
- تحميل قصير داخل زر → [spinner](spinner.md).

## التشريح (Anatomy)
كتلة بخلفية `--color-bg-subtle`، زاوية تطابق ما تحاكيه (`--radius-sm` للنصّ، `--radius-full` للأفاتار)، مع نبض خفيف اختياري على الشفافية.

## الأنواع (Variants)
- `text-line` — سطر نصّ (ارتفاع ~`--font-size-md`/line-height، عرض متغيّر 60–90%).
- `avatar` — دائرة (`--radius-full`) بمقاس صورة رمزية.
- `card` — كتلة + أسطر نصّ داخلها.
- `table-row` — صفّ بخلايا تحاكي الأعمدة.
- `block` — مستطيل عام (صورة/رسم).

## المقاسات (Sizes)
يرث أبعاد ما يحاكيه؛ ارتفاع `text-line` يطابق `line-height`، والأفاتار يطابق مقاس الصورة الفعلي.

## الحالات (States)
`loading` (نبض لطيف). مع `prefers-reduced-motion: reduce` → ثابت بلا نبض.

## سلوك RTL
يتبع تدفّق المحتوى؛ أسطر النصّ تبدأ من `inline-start` (يمين)؛ بنيته غير اتجاهية فلا تُعكَس بصريًا ([rtl-guidelines](../foundations/rtl-guidelines.md)).

## الوصول (Accessibility)
- الكتل النائبة `aria-hidden="true"`.
- المنطقة الأصل `aria-busy="true"` أثناء التحميل + نصّ بديل لقارئ الشاشة («جارٍ التحميل»).
- يُزال فور وصول البيانات (لا يبقى عند الخطأ — اعرض [alert](alert.md)/[empty-state](empty-state.md) error).

## استخدام Tailwind
`bg-muted` · `rounded-sm`/`rounded-full` · `animate-pulse` · `motion-reduce:animate-none` · الأبعاد عبر أدوات الحجم/`w-*`.

## التوكنز (Token usage)
`--color-bg-subtle` · `--radius-sm`/`--radius-full` · `--duration-*`/`--ease-standard` (النبض).

## معايير القبول البصري (Visual acceptance criteria)
- اللون = `--color-bg-subtle` فقط (لا تدرّجات صاخبة).
- يطابق **شكل وعدد** عناصر المحتوى المتوقّع (عدد صفوف ≈ المتوقّع).
- نبض لطيف 1.2–1.6s؛ بلا أي نصّ حقيقي.
- يحترم `prefers-reduced-motion`؛ يُستبدل فورًا بالمحتوى لا بقفزة.

## أنماط ممنوعة (Anti-patterns)
- بقاء skeleton للأبد عند فشل الجلب (اعرض حالة خطأ).
- skeleton لمحتوى نهائي أو كزخرفة.
- استخدام [spinner](spinner.md) مكانه لتحميل جدول.
- عدد/أحجام عشوائية لا تطابق المحتوى المتوقّع (قفز عند الاستبدال).

## أمثلة (Examples)
- 6 صفوف `table-row` skeleton أثناء جلب الجدول.
- كرت ملف تعريف: `avatar` + سطرَا `text-line`.
- ثلاثة `text-line` بعروض 90% / 70% / 50%.
