# الترقيم — Pagination

> القيم من [tokens.md](../foundations/tokens.md). **رُقّي من «composition» (v1.1.2) إلى مكوّن موثّق (v1.1.5).** يبنى من [button](button.md). يصاحب [table](table.md)/القوائم.

## الغرض (Purpose)
التنقّل بين صفحات نتائج مقسّمة، مع ملخّص يوضّح الموضع وإجمالي النتائج.

## متى يُستخدم (When to use)
- قوائم/جداول كبيرة مقسّمة حيث **الموضع والعدد مهمّان** والمستخدم قد يقفز بين الصفحات (لوحات إدارة، نتائج بحث).
- عندما يحتاج المستخدم معرفة «أين هو» و«كم بقي».

## متى لا يُستخدم (When not to use)
- تصفّح استكشافي مستمرّ (موجز/خلاصة) → **infinite scroll**.
- قائمة متوسطة لا يحتاج فيها قفزًا → **«تحميل المزيد» (Load more)**.
- قائمة قصيرة تظهر كاملة → لا ترقيم.
> القاعدة: **Pagination** لمهام البحث/الإدارة (الموضع مهمّ) · **Load more/Infinite** للتصفّح المتدفّق. لا تخلط نمطين في القائمة نفسها.

## التشريح (Anatomy)
ملخّص النتائج («عرض 1–20 من 240») + زرّا **السابق/التالي** + (اختياري) **أرقام الصفحات** مع **الصفحة الحالية** مميّزة + فاصل «…» للفجوات.

## الأنواع (Variants)
- `prev-next` — السابق/التالي فقط (مدمج).
- `numbered` — أرقام صفحات + سابق/تالٍ (+ «…»).
- `with-summary` — أيٌّ منهما + ملخّص النتائج.

## المقاسات (Sizes)
أزرار `sm` (`--size-control-sm`) أو `md` (`--size-control-md`)؛ منطقة لمس ≥ `--size-touch-min` (44).

## الحالات (States)
`default` · `current` (الصفحة الحالية: `--color-accent-subtle` + `aria-current="page"`) · `disabled` (السابق في الصفحة الأولى، التالي في الأخيرة: `aria-disabled` + غير قابل للنقر) · `hover` (`--color-bg-hover`) · `focus-visible` (`--shadow-focus`) · `ellipsis` (فاصل «…» غير تفاعلي).

## سلوك RTL
- التدفّق من اليمين؛ «السابق» منطقيًا أوّلًا (يمين) و«التالي» في `inline-end` (يسار).
- **أيقونات chevron اتجاهية فتُعكَس**: سهم «التالي» يشير لليسار في RTL (`rtl:-scale-x-100` أو أيقونة منطقية) — لا تُثبَّت جهة.
- أرقام الصفحات والإجمالي **لاتينية `tabular-nums` معزولة bidi** ([rtl-guidelines §4-5](../foundations/rtl-guidelines.md)).

## الوصول (Accessibility)
- حاوية `<nav aria-label="ترقيم الصفحات">`.
- الصفحة الحالية `aria-current="page"` (لا تُعرف باللون وحده).
- أزرار حقيقية (`<button>`/`<a>`)؛ المعطّل `aria-disabled="true"`.
- الملخّص نصّ مقروء؛ «…» `aria-hidden`.

## استخدام Tailwind
`nav` → `flex items-center gap-2`؛ زر `inline-flex items-center justify-center h-8 px-3 rounded-md bg-card border border-border text-sm focus-visible:ring`؛ current `bg-primary-subtle text-primary`؛ chevron `size-4 rtl:-scale-x-100`؛ الملخّص `text-sm text-muted-foreground`.

## التوكنز (Token usage)
`--size-control-sm/md` · `--size-touch-min` · `--space-2xs`/`-xs` · `--radius-md` · `--color-accent-subtle` (current) · `--color-bg-hover` · `--color-text-secondary` (الملخّص) · `--color-border-default`.

## معايير القبول البصري (Visual acceptance criteria)
- **حالة current واحدة فقط** واضحة بصريًا + `aria-current`.
- السابق/التالي يُعطّلان عند الحدّين بشكل ظاهر.
- chevrons **تُعكَس** في RTL.
- أرقام `tabular-nums` (لا قفز عرض)؛ منطقة لمس ≥44.

## أنماط ممنوعة (Anti-patterns)
- chevron لا يُعكَس في RTL (يشير للجهة الخطأ).
- تمييز current باللون وحده بلا `aria-current`.
- ترقيم لقائمة قصيرة (ضوضاء).
- خلط Pagination مع Infinite scroll في القائمة ذاتها.
- أرقام شرقية (٠-٩) ممزوجة بالغربية (ممنوع — نظام واحد).

## أمثلة (Examples)
- `with-summary`: «عرض 1–20 من 240» + سابق/تالٍ.
- `numbered`: «السابق ‹ 1 2 [3] 4 … 12 › التالي».
- `prev-next` مدمج أسفل جدول قصير نسبيًا.
