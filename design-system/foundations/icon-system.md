# نظام الأيقونات — Icon System

> القيم من [tokens.md](tokens.md). يحكم اختيار الأيقونات وأحجامها وسلوكها (خاصةً RTL). يُربط من [09-spa-build-standards](../../design-protocols/09-spa-build-standards.md) (مكتبة المشروع الحقيقي) ومن مواصفات المكوّنات.

## الغرض
توحيد مصدر الأيقونات ونمطها وأحجامها وسلوكها في الاتجاهين، فلا تختلط أنماط ولا تتفاوت الأحجام.

## المكتبة الأساسية
- **`lucide-react`** هي المكتبة الأساسية لكل أيقونات الواجهة (نمط خطّي موحّد، `currentColor`).
- **`react-icons`** مسموحة **فقط** كبديل لأيقونات العلامات/التواصل الاجتماعي أو أيقونة غير متوفّرة في Lucide — لا للأيقونات العامة.
- **لا تخلط نمطين** من الأيقونات في الواجهة نفسها.

## مجموعة أيقونات الواجهة (Lucide)
استخدم Lucide لكل هذه: `search` (بحث) · `download`/`upload` (تصدير/استيراد) · `filter` (فلترة) · `chevron-down/left/right` (أسهم) · `arrow-up-down` (فرز) · `calendar` (تاريخ) · `alert-triangle` (تحذير) · `info` (معلومة) · `check-circle` (نجاح) · `x-circle`/`alert-circle` (خطأ) · `x` (إغلاق) · `more-horizontal`/`more-vertical` (المزيد).

## الأحجام (عبر التوكنز فقط)
- `--size-icon-sm` (16) · `--size-icon-md` (20) · `--size-icon-lg` (24).
- في Tailwind: `size-4` / `size-5` / `size-6`. لا أحجام خام أو عشوائية.
- السماكة البصرية موحّدة (Lucide ≈ 2px stroke، نهايات مستديرة)، واللون `currentColor`.

## الوصول (Accessibility)
- **زخرفية** (بجانب نصّ يكفي) → `aria-hidden="true"`.
- **ذات معنى** (وحدها تحمل المعنى، كزر أيقونة) → نصّ بديل: `aria-label` عربي على الزر، أو نصّ مخفي بصريًا.
- لا تُنقَل المعلومة باللون وحده؛ الأيقونة تدعم النصّ لا تستبدله في الحالات (انظر [status-badge](../components/status-badge.md)).

## RTL
- **الأيقونات الاتجاهية تُعكَس أو تُختار صحيحة:** chevrons، أسهم الفرز/السابق-التالي، الإرسال، التقدّم، الرجوع/التالي — تتبع اتجاه القراءة (`rtl:-scale-x-100` أو متغيّر منطقي).
- **غير الاتجاهية لا تُعكَس:** بحث، إعدادات، تقويم، علامة صحّ، معلومة، تحذير، إغلاق (×).
- التفاصيل في [rtl-guidelines §3](rtl-guidelines.md).

## الاستخدام داخل المكوّنات
- **زر/زر أيقونة:** الأيقونة في `inline-start`، فجوة `--space-2xs`، حجم يطابق حجم الزر ([button](../components/button.md)).
- **بحث/فلتر:** أيقونة البحث في `inline-start` غير معكوسة ([search-input](../components/search-input.md) · [filter-bar](../components/filter-bar.md)).
- **select:** سهم في `inline-end`، علامة التحديد في `inline-start` ([select](../components/select.md)).
- **رأس جدول قابل للفرز:** أيقونة الفرز من هذا النظام، بجانب العنوان ([table](../components/table.md)).
- **alert/toast/empty-state:** أيقونة الحالة تطابق النوع (info/success/warning/danger).

## في المعاينة (preview)
معرض `playground/` ليس فيه bundler، فيُمثَّل نمط Lucide بـ **inline SVG** (viewBox 24، stroke موحّد، `currentColor`) كـ**shim موثّق** — وليس استيرادًا حقيقيًا لـ`lucide-react`. `react-icons` لا يُستخدم في المعاينة إلا كتوضيح fallback.

## أنماط ممنوعة (Anti-patterns)
- خلط مكتبتي/نمطي أيقونات في الشاشة نفسها.
- أحجام أيقونات خام/عشوائية خارج توكنز الحجم.
- أيقونة ذات معنى بلا نصّ/تسمية بديلة.
- chevron/سهم فرز لا يُعكَس في RTL.
- أيقونة بلون hex بدل `currentColor`/توكن.
- استخدام `react-icons` لأيقونة واجهة عامة متوفّرة في Lucide.

## التوكنز
`--size-icon-sm/md/lg` · `--space-2xs` (فجوة الأيقونة↔النص) · الألوان عبر `currentColor` والتوكنز الدلالية.
