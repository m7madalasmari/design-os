# الشريط العلوي — App Header (تطبيق بيانات)

> الشريط العلوي لتطبيق بيانات متعدّد الصفحات — يحقّق topbar في نمط [layout §App Shell](../foundations/layout.md). يختلف عن [nav-bar](nav-bar.md) **التسويقي** (هذا داخلي/مصادَق عليه، لا CTA تسويقي). القيم من [tokens.md](../foundations/tokens.md). **رُقّي من BACKLOG بعد أن أثبت dogfood «بوابة الطلبات» أنه حاجب.**

## 1. متى يُستخدم
أعلى shell التطبيق: سياق الصفحة + بحث عام + إشعارات + حساب. لاصق أعلى منطقة المحتوى.

## 2. متى لا يُستخدم
- موقع تسويقي → [nav-bar](nav-bar.md).
- التنقّل بين الأقسام → [sidebar](sidebar.md) (هذا ليس بديلًا عنه).

## التشريح (Anatomy)
```
[ inline-start: زرّ طيّ الشريط (موبايل: زرّ يفتح الدرج) + عنوان الصفحة / breadcrumb ]
[ ............ بحث عام (اختياري) ............ ]
[ inline-end: إشعارات (icon button) · حساب (avatar + قائمة) ]
```

## 3. الحالات
`default` · `sticky` (ملتصق عند التمرير) · `scrolled` (حدّ سفلي/ظلّ خفيف عند النزول) · فتح قائمة الحساب/الإشعارات (`--z-dropdown`) · `mobile` (زرّ يفتح [sidebar](sidebar.md) كـ[drawer](drawer.md)).

## 4. المقاسات
ارتفاع ≈ `--size-control-lg` + حشو رأسي؛ حشو أفقي `--space-md`/`-lg`؛ لاصق `--z-sticky`؛ أيقونات `--size-icon-md`؛ avatar `sm`/`md` ([avatar](avatar.md)).

## 5. قواعد النصوص
- عنوان الصفحة يطابق العنصر النشط في [sidebar](sidebar.md) (اتساق المعجم)؛ أو breadcrumb للمسارات العميقة ([page-header](page-header.md) للعنوان داخل المحتوى).
- لا شعارات/CTA تسويقية.

## 6. قواعد RTL
- العنوان/الطيّ في `inline-start` (يمين)، الحساب/الإشعارات في `inline-end` (يسار) — خصائص منطقية، لا `left/right`.
- أيقونة البحث غير معكوسة؛ سهم قائمة الحساب اتجاهي.

## 7. الوصول
- `<header>` landmark؛ زرّ الطيّ `aria-expanded`/`aria-controls` للـsidebar؛ الإشعارات/الحساب أزرار بـ`aria-haspopup`/`aria-expanded` + قائمة كيبورد (↑↓/Esc)؛ عدّاد الإشعارات ليس اللون وحده.
- البحث `aria-label`؛ ترتيب تركيز يتبع RTL.

## 8. أمثلة صحيحة / خاطئة
- **صحيح:** عنوان يطابق القسم النشط + بحث + إشعارات + حساب؛ موبايل = زرّ يفتح درج التنقّل.
- **خطأ:** CTA تسويقي؛ تكرار تنقّل الـsidebar كروابط في الهيدر؛ إخفاء البحث/الحساب دون بديل على الموبايل؛ مظهر native للأزرار (forbidden #20).

## 9. علاقته بالتوكنز (عقد الربط)
| الجزء/الحالة | التوكن الدلالي |
|---|---|
| سطح الشريط | `--color-bg-surface` · حدّ سفلي `--color-border-subtle` |
| العنوان | `--color-text-primary` · `--font-size-lg`/`-xl` |
| أزرار أيقونة (إشعارات) | ghost: شفّاف + `hover:--color-bg-hover` |
| عدّاد إشعارات | `--color-danger-fg`/`-bg` (+ رقم، لا لون وحده) |
| الحساب/القائمة | avatar + `--color-bg-raised` · `--shadow-md` · `--z-dropdown` |
| تركيز | `--shadow-focus` (`:focus-visible` فقط) · لاصق `--z-sticky` |

## 10. القبول البصري
- **بلا مظهر native** ([component-visual-baseline](../foundations/component-visual-baseline.md))؛ أزرار الأيقونة **ghost** subtle لا محاطة بحدّ ثقيل؛ تركيز عند `:focus-visible` فقط؛ ظلّ/حدّ خفيف عند التمرير لا ثقيل. (Visual Polish Gate.)
