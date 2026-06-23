# Page Manifest — طلبات الإرشاد (Admin)

> تشغيل Greenfield للبروتوكول (v1.1.2). صفحة إدارية/بيانات. لا صورة مرجعية → النظام هو المصدر الوحيد، Pixel QA غير مطبّق.
> المعاينة: `preview.html`. (داخل القالب → playground/، لا page-manifests/ — قاعدة template-vs-consumer.)

- **Mode:** Greenfield / System-First
- **Direction:** RTL (ar)
- **Theme:** neutral
- **Reference:** none (built from the system, no image)

## Intent
لوحة أدمن لإدارة طلبات الإرشاد: تصفية بالحالة، استعراض الطلبات، تعيين مرشد للطلبات الجديدة، وتصدير القائمة.

## Users
أدمن/منسّق الإرشاد (مسجّل دخول)، عربي، سطح المكتب غالبًا.

## Primary Action (one)
**تعيين مرشد** — الإجراء الأساسي للشاشة (زر primary `sm` على صفوف «جديدة»). لا يوجد إجراء primary على مستوى الرأس.

## Secondary Actions
تصدير (secondary/outline في الرأس) · عرض (tertiary/link لبقية الصفوف) · مسح الفلاتر (داخل no-results) · فرز عمود التاريخ.

## Reference Analysis  *(Greenfield — no image; كل القرارات inferred من النظام)*
- Page type: صفحة بيانات (جدول + فلترة) — `inferred`
- Layout / regions: page-header (عنوان + تصدير) → filter-bar (بحث + شرائح حالة بعدّادات) → كرت يحوي الجدول → عدّاد + ترقيم — `inferred`
- Grid & alignment: عمود واحد، عرض محتوى محدود؛ النص `start`، التاريخ/المعرّفات معزولة bidi — `inferred`
- Spacing: سلّم 4px؛ خلية `space-sm`/`space-md`، فجوات أقسام `space-lg`/`space-xl` — `inferred`
- Typography: IBM Plex Sans Arabic (tokens.css)؛ CSP preview → fallback system-ui — `inferred`
- Color: محايد؛ الإجراء = `--color-accent`؛ ألوان الحالة الوظيفية للشارات — `observed (tokens)`
- Components: page-header, filter-bar, table, status-badge, button, empty-state — `observed (INDEX)`
- RTL: كامل؛ تدفّق أعمدة من اليمين؛ أرقام لاتينية جدولية — `observed (table.md/04)`
- Ambiguous: أعمدة الجدول الدقيقة — `inferred` (6 أعمدة دلالية، بلا حشو — forbidden #5)

## Component Mapping  *(check `components/INDEX.md` — لا مكوّن جديد)*
- **page-header** — عنوان h1 «طلبات الإرشاد» + وصف فرعي + تصدير (`inline-end`).
- **filter-bar** — بحث (`inline-start`) + شرائح حالة بعدّادات: الكل/جديدة/مجدولة/مكتملة/ملغية.
- **table** — أعمدة: رقم الطلب · المستفيد · نوع الإرشاد · تاريخ الطلب · المرشد المعيّن · الحالة · إجراء.
- **status-badge** — نقطة+نص؛ تعيين دلالي ثابت: جديدة→neutral · مجدولة→info · مكتملة→success · ملغية→danger.
- **button** — تعيين مرشد (primary sm) · تصدير (secondary) · عرض (tertiary).
- **empty-state** — first-use / no-results / error (عنوان heading حقيقي؛ أيقونة بسيطة — تطبيق بيانات).
- **Pagination** — `composition-pattern` (counter + prev/next)، ليست مكوّنًا (INDEX).
- Missing component/token documented first: **لا شيء**.

## Data States  *(table.md §3 — الخمسة)*
- Loading: skeleton صفوف (~6).
- Empty (first-use): «لم تصل أي طلبات إرشاد بعد» + إجراء «تحديث».
- No-results (بعد فلترة): «لا نتائج تطابق هذه الفلاتر» + «امسح الفلاتر».
- Error: `role="alert"` «تعذّر تحميل الطلبات» + «أعد المحاولة».
- Filled: الافتراضي (مزيج حالات).
- No Permission: خارج النطاق (أدمن مخوّل).

## Demo Data Policy
- Uses demo data: **Yes**
- Data type: طلبات إرشاد تجريبية — رقم طلب (REQ-####)، رمز مستفيد مُقنّع (مستفيد #####)، رمز مرشد (مرشد ##)، نوع، تاريخ، حالة.
- PII risk: **none** — لا أسماء/جوالات/إيميلات/هويات حقيقية؛ رموز مُقنّعة صناعية فقط.
- Labeling: شريط أعلى الصفحة «بيانات تجريبية صناعية — لا تمثّل أشخاصًا حقيقيين».
- Reason: معاينة/اختبار Greenfield (لا بيانات إنتاجية — `00`).

## Content Rules
- عربي طبيعي (لا ترجمة حرفية)؛ مصطلح حالة ثابت لكل قيمة؛ أرقام لاتينية `tabular-nums`؛ تاريخ موحّد «22 يونيو 2026».

## Layout Rules
- أدوات Tailwind منطقية فقط؛ سلّم المسافات؛ عرض محتوى محدود؛ الأكسنت للإجراء/المحدّد فقط.

## Token Var Exceptions  *(tokens بلا Tailwind utility — عبر `style`/shim من tokens.css)*
| Location | Token | Reason | Utility unavailable? |
|---|---|---|---|
| رأس الجدول اللاصق | `--z-sticky` | ترتيب الطبقة عند التمرير | Yes (z-index غير مولّد) |
| الانتقالات | `--duration-fast` (120ms) | مدّة hover/focus من التوكن | Yes (لا utility بقيمة 120ms دقيقة) |
> القيم من `tokens.css` فقط، لا قيم خام، ولا arbitrary حيث يكفي `var()` (02).

## Responsive Behavior
- Desktop: جدول كامل داخل كرت. Tablet: شريط الفلاتر يلتفّ (`flex-wrap`).
- Mobile: تمرير أفقي للجدول داخل `overflow-x-auto` (لا قصّ صامت — #16). تحوّل بطاقة-لكل-صفّ = تحسين مستقبلي موثّق، خارج النطاق.
- Navigation: لا shell/تنقّل عام (08 — لم يُطلب). Sticky: رأس الجدول لاصق.

## Visual Polish and Motion
- **Needed:** row hover (`hover:bg-hover`) · focus-visible ring على الحقول/الأزرار/رأس الفرز · `transition-colors duration-fast` · skeleton للتحميل · شريحة فلتر نشطة.
- **Not needed:** SVG زخرفي، scroll reveal، رسمة حالة فارغة كبيرة (تطبيق بيانات → أيقونة بسيطة، empty-state.md).
- **Motion:** `transition-colors` + `ease-standard`؛ skeleton pulse؛ `motion-reduce` يعطّل.
- **SVG:** أيقونات وظيفية فقط (`aria-hidden`, `currentColor`).
- **Interaction:** زر hover/active/focus؛ حقل focus ring؛ صف hover؛ فرز `aria-sort`.
- **Reduced motion:** `prefers-reduced-motion: reduce` يعطّل كل الانتقالات/الـpulse.
- **Performance:** لا مخاطر (أيقونات inline).

## Forbidden (this page)
- لون/قيمة خارج التوكنز · مكوّن غير موثّق · بيانات إنتاجية/PII مختلقة · قيم Tailwind عشوائية · أدوات اتجاهية في RTL · أكثر من primary واحد في السياق · أعمدة حشو · لون شارة بلا نص.

## Out of Scope
- shell/تنقّل عام · مودال تعيين المرشد · فرز/فلترة/ترقيم حيّ · تحميل خط Plex (CSP).

## Post-implementation
- QA per `03` (System + RTL + Tailwind + `05` Required Output). **Pixel QA: N/A (Greenfield)**. انظر تقرير QA أدناه.
- **QA Report Location:** Embedded (in this manifest) · Path: —  *(مهمة متوسطة → مضمّن، 07)*
- **Preview runtime:** Shim mirror

---

## QA Report  *(per `03` — Greenfield → no Pixel/Visual-reference QA)*

### System QA (`qa-checklist`)
توكنز فقط ✅ · إجراء primary واحد في السياق (تعيين مرشد) ✅ · أدوات RTL منطقية ✅ · أرقام لاتينية جدولية + معرّفات/تواريخ معزولة bidi ✅ · شارة حالة نقطة+نص (لا لون وحده)، تعيين دلالي ثابت ✅ · رأس جدول لاصق + فرز `aria-sort` ✅ · حالات البيانات الخمس ✅ · حالة فارغة: عنوان heading حقيقي + أيقونة بسيطة (لا رسمة) ✅ · خطأ داخل `role="alert"` ✅ · لا بيانات PII/إنتاجية ✅ · تباين AA (نص أساسي/سطح ~14:1، ثانوي ~5.4:1، on-accent ≥4.5:1) ✅.

### RTL QA (`04`)
`dir="rtl"` على الحاوية ✅ · `text-start/end` فقط ✅ · أيقونة البحث `inline-start` ✅ · المبالغ/الأرقام `tabular-nums` ✅ · لا `ml/mr/left/right/text-left/right` ✅ · نبرة عربية طبيعية، أزرار أفعال ✅.

### Tailwind compliance
كلاسات دلالية + السلّم القياسي ✅ · صفر arbitrary value في الـmarkup ✅ · RTL منطقي ✅ · استثناءات توكن (z-sticky، duration) موثّقة أعلاه عبر shim من tokens.css، لا قيم خام ✅.

### Visual polish & motion QA
| Area | Match % | Issues | Fix |
|---|---:|---|---|
| Motion | 100 | transitions + reduced-motion | — |
| SVG / Motifs | 100 | أيقونات وظيفية فقط | — |
| Hover / Focus States | 100 | row hover + focus ring | — |
| Loading / Empty States | 100 | skeleton + 4 حالات | — |
| Surface Depth | 100 | كرت ظل ناعم، رأس subtle | — |

### Deviations / assumptions
| Location | Difference | Type | Severity | Fix | Scope |
|---|---|---|---|---|---|
| الخط | Plex → system (CSP) | Typography | low | تحميل Plex محليًا | page |
| الأعمدة | عددها/أسماؤها مُستنتجة (Greenfield) | Content | low | تُؤكَّد من متطلبات حقيقية | page |
| المعاينة | shim يطابق tokens.css (لا Tailwind build) | Build | med | Tailwind فعلي في المشروع المستهلك | preview only |

### Design System update required?
**لا.** كل الكتل غطّتها مكوّنات/توكنز موجودة؛ لا حاجة لمكوّن أو توكن جديد. (الترقيم composition موثّقة.)

### Done? (per `07`) — كل الصناديق ✅ (انظر رسالة الجلسة).
