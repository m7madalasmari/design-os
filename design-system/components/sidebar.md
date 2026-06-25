# الشريط الجانبي — Sidebar (تنقّل التطبيق)

> التنقّل الأساسي لتطبيق بيانات متعدّد الصفحات. يحقّق نمط app-shell في [layout §App Shell](../foundations/layout.md). القيم من [tokens.md](../foundations/tokens.md). **رُقّي من BACKLOG #app-shell بعد أن أثبت dogfood «بوابة الطلبات» أنه حاجب لأي تطبيق متعدّد الصفحات.**

## 1. متى يُستخدم
تطبيق متعدّد الصفحات/الأقسام يحتاج تنقّلًا دائمًا (طلبات · لوحة · إعدادات). جهة البداية (`inline-start` = اليمين في RTL).

## 2. متى لا يُستخدم
- صفحة واحدة بلا أقسام → لا shell (08).
- موقع تسويقي → [nav-bar](nav-bar.md).
- تنقّل ثانوي داخل صفحة → [tabs](tabs.md).

## التشريح (Anatomy)
```
[ رأس: شعار/اسم التطبيق + زرّ طيّ ]
[ مجموعة تنقّل: عناصر (أيقونة + نصّ)، عنصر نشط ]
[ (اختياري) مجموعات بعناوين أقسام ]
[ تذييل: حساب/إعدادات ]
```

## 3. الأنواع/الحالات (Variants & States)
- **expanded** (≈`260px`) أيقونة+نصّ · **collapsed** (≈`64px`) أيقونة فقط + tooltip للنصّ.
- عنصر: `default` · `hover` (`--color-bg-hover`) · **`active`** (`--color-primary-subtle` خلفية + `--color-primary` نصّ/أيقونة + `aria-current="page"`) · `focus-visible` · `disabled`.
- **mobile** (`<lg`): يُطوى خلف زرّ في [app-header](app-header.md) ويُفتح كـ[drawer](drawer.md) (focus-trap + Esc).

## 4. المقاسات
عرض `260px`/`64px` (توكن تخطيط — layout)؛ ارتفاع العنصر `--size-control-lg`؛ حشو `--space-sm`/`-md`؛ أيقونة `--size-icon-md`؛ فجوة عناصر `--space-2xs`؛ زاوية العنصر `--radius-md`.

## 5. قواعد النصوص
- تسميات أقسام موجزة (اسم لا جملة)؛ عنوان قسم اختياري `--font-size-xs` خافت.
- العنصر النشط واحد لكل مسار.

## 6. قواعد RTL
- الشريط على **اليمين** (`inline-start`) — انعكاس تلقائي بالخصائص المنطقية، لا `left/right`.
- الأيقونة قبل النصّ في التدفّق؛ الأيقونات الاتجاهية (سهم طيّ) تُعكَس، الرمزية لا ([rtl-guidelines](../foundations/rtl-guidelines.md)).

## 7. الوصول
- حاوية `<nav aria-label="التنقّل الرئيسي">`؛ العناصر روابط؛ النشط `aria-current="page"`.
- طيّ: زرّ بـ`aria-expanded`؛ في collapsed النصّ المخفي يبقى accessible name (`aria-label`/tooltip).
- ترتيب تركيز يتبع القراءة RTL؛ هدف لمس ≥44px؛ على الموبايل focus-trap داخل الدرج.

## 8. أمثلة صحيحة / خاطئة
- **صحيح:** عنصر نشط واحد بخلفية `--color-primary-subtle`؛ طيّ لأيقونات مع tooltip؛ موبايل = درج.
- **خطأ:** أكثر من «نشط»؛ بناء بـ`left`؛ إخفاء التنقّل على الموبايل بلا زرّ معلن؛ حدّ أسود ثقيل (forbidden #19).

## 9. علاقته بالتوكنز (عقد الربط)
| الجزء/الحالة | التوكن الدلالي |
|---|---|
| سطح الشريط | `--color-bg-surface` (أو `-subtle`) · حدّ `--color-border-subtle` |
| عنصر hover | `--color-bg-hover` |
| عنصر **نشط** | خلفية `--color-primary-subtle` · نصّ/أيقونة `--color-primary` |
| نصّ خامل | `--color-text-secondary` |
| تركيز | `--shadow-focus` (`:focus-visible` فقط) |
| العرض/الطيّ | توكن تخطيط `260px`/`64px` (layout) |

## 10. القبول البصري
- **بلا مظهر native** ([component-visual-baseline](../foundations/component-visual-baseline.md))؛ العناصر روابط/أزرار مُعاد ضبطها.
- النشط بإشارة **خلفية + لون** (لا حدّ سميك)؛ تركيز عند `:focus-visible` فقط؛ كثافة مريحة لا مزدحمة. (Visual Polish Gate.)
