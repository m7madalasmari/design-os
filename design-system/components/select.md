# القائمة المنسدلة — Select

> القيم من [tokens.md](../foundations/tokens.md). المشغّل يرث أبعاد [input](input.md). قُوّيت المواصفة في v1.1.5 (open/keyboard/loading/empty).

## الغرض (Purpose)
اختيار **قيمة واحدة** من مجموعة محدّدة معروفة (عادةً أكثر من ~5 خيارات).

## متى يُستخدم (When to use)
- اختيار واحد من قائمة معروفة (مدينة، تصنيف، حالة).
- قائمة طويلة جدًا → select قابل للبحث (combobox).

## متى لا يُستخدم (When not to use)
- خياران أو تشغيل/إيقاف → [checkbox](checkbox.md) أو مفتاح.
- 2–5 خيارات تُقارَن دفعةً → أزرار اختيار (radio).
- اختيار متعدّد كثيف → خانات/وسوم.

## التشريح (Anatomy)
**المشغّل (trigger)** كحقل + **سهم** في `inline-end` → **قائمة منبثقة (popover)** فيها **خيارات**، كلٌّ قد يحمل **علامة تحديد** في `inline-start`، و(اختياريًا) **حقل بحث** أعلى القائمة للقوائم الطويلة.

## الأنواع (Variants)
- `basic` — قائمة خيارات.
- `searchable` (combobox) — حقل بحث يفلتر الخيارات.
- `grouped` (اختياري) — خيارات تحت عناوين مجموعات.

## المقاسات (Sizes)
المشغّل `sm`/`md`/`lg` (`--size-control-*`)، حشو `--space-md`، زاوية `--radius-md`، سهم `--size-icon-sm`.

## الحالات (States)
`default` · `hover` (`--color-border-strong`) · `focus` (`--shadow-focus`) · `open` (قائمة `--color-bg-raised` + `--shadow-md` + `--z-dropdown`) · `selected` (الخيار `--color-accent-subtle` + علامة صحّ) · `option-hover` (`--color-bg-hover`) · `disabled` (`--color-bg-disabled`) · `error` (`--color-danger-border` + رسالة + `aria-invalid`) · `loading` (مؤشّر [spinner](spinner.md) داخل القائمة + `aria-busy`) · **`empty-options`** (نصّ هادئ «لا خيارات متاحة»، غير قابل للاختيار).

## سلوك لوحة المفاتيح (Keyboard behavior)
- **مغلق:** `Enter`/`Space`/`↓` يفتح القائمة ويركّز أول خيار (أو المحدّد).
- **مفتوح:** `↑`/`↓` تنقّل، `Home`/`End` للطرفين، **type-ahead** بالحرف الأول، `Enter` يختار، `Esc` يغلق ويعيد التركيز للمشغّل، `Tab` يغلق ويغادر.
- تركيز متنقّل (roving) أو `aria-activedescendant`.

## سلوك الإغلاق (Close behavior)
يغلق عند: الاختيار · `Esc` · فقدان التركيز · نقر خارج القائمة. **يعيد التركيز إلى المشغّل** بعد الإغلاق.

## سلوك RTL
السهم في `inline-end`، علامة التحديد في `inline-start`؛ القائمة تحاذي الحافة المنطقية للمشغّل وتنفتح في الاتجاه المتاح؛ الخيارات اللاتينية/الأرقام معزولة bidi ([rtl-guidelines](../foundations/rtl-guidelines.md)).

## الوصول (Accessibility)
- المشغّل `role="combobox"` (أو زر) + `aria-haspopup="listbox"` + `aria-expanded`.
- القائمة `role="listbox"`؛ كل خيار `role="option"` + `aria-selected`.
- تسمية ظاهرة فوق المشغّل؛ نصّ المشغّل الفارغ يصف الفعل («اختر مدينة») لا «—».
- **حلقة التركيز لا تُزال**؛ `loading` → `aria-busy`؛ `error` → `aria-invalid` + ربط الرسالة.

## استخدام Tailwind
المشغّل كـ[input](input.md): `inline-flex items-center justify-between h-10 px-3 bg-card border border-border rounded-md text-sm focus-visible:ring`؛ السهم `size-4` في `inline-end`. القائمة: `bg-popover shadow-md rounded-md` بـ`z-index:var(--z-dropdown)`؛ الخيار `px-3 py-2 hover:bg-hover`؛ المحدّد `bg-primary-subtle text-primary`.

## التوكنز (Token usage)
توكنز [input](input.md) (حدود/خلفية/قياس/تركيز) + `--color-bg-raised` · `--shadow-md` · `--z-dropdown` · `--color-accent-subtle` (محدّد) · `--color-bg-hover` (تمرير) · `--size-icon-sm` (السهم).

## معايير القبول البصري (Visual acceptance criteria)
- السهم في `inline-end`؛ التحديد = `--color-accent-subtle` + علامة في `inline-start`.
- القائمة بظلّ `--shadow-md` فوق `--z-dropdown`، محاذية لحافة المشغّل.
- تركيز ظاهر على المشغّل وداخل القائمة؛ `empty-options` نصّ هادئ غير قابل للنقر؛ `loading` لا يُحدث قفزًا.
- يعيد التركيز للمشغّل عند الإغلاق.
- **لا مظهر تحكّم أصلي** (`appearance:none` على المشغّل)؛ السهم وعلامة الصحّ من [icon-system](../foundations/icon-system.md)؛ الحدّ/التركيز من التوكنز لا حلقة المتصفّح.

## أنماط ممنوعة (Anti-patterns)
- select لخيارين (استخدم مفتاحًا/خانة).
- نصّ مشغّل غامض «—» بلا توجيه.
- قائمة بلا تحكّم لوحة مفاتيح أو بلا `role`.
- عدم إعادة التركيز للمشغّل بعد الإغلاق.
- لون تحديد بـhex يدوي (ممنوع #11).

## أمثلة (Examples)
- «المدينة» + مشغّل «اختر مدينة» + قائمة، المحدّد «الرياض» بعلامة صحّ.
- `searchable`: حقل بحث يفلتر قائمة طويلة.
- `loading`: spinner + «جارٍ الجلب…»؛ `empty-options`: «لا خيارات متاحة».
