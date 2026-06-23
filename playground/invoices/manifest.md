# Page Manifest — الفواتير (Invoices list)

> اختبار حي للبروتوكول (v1.1.1). صفحة بيانات/لوحة إدارية. لا صورة مرجعية → النظام هو المصدر الوحيد.
> الصفحة (معاينة): `preview.html`. تقرير QA: نهاية هذا الملف + في رسالة الجلسة.

- **Mode:** System Fidelity (الافتراضي) — بلا مرجع بصري، فالنظام = SSOT (سلوك يقترب من Strict SSOT)
- **Direction:** RTL (ar)
- **Theme:** neutral
- **Reference:** none (بُنيت من النظام، لا صورة)

## Intent
عرض سجلّات الفواتير بشكل قابل للفرز/الفلترة في لوحة إدارية، مع إجراء أساسي واحد لإنشاء فاتورة، وتغطية حالات البيانات الخمس.

## Users
موظف مالية (مسجّل دخول)، عربي، على سطح المكتب غالبًا والجوال أحيانًا.

## Primary Action (one)
«أنشئ فاتورة» — زر أساسي واحد في ترويسة الصفحة (`inline-end`).

## Secondary Actions
«تصدير» (ثانوي/outline)؛ مسح الفلاتر (رابط داخل حالة no-results)؛ فرز الأعمدة.

## Reference Analysis  *(observed/inferred/approximate/unknown)*
- Page type: صفحة بيانات (جدول) — `inferred` (لا صورة؛ مشتقّ من نوع المنتج في README النظام)
- Layout / regions: ترويسة صفحة (عنوان + إجراء) → شريط فلاتر (بحث + شرائح حالة) → كرت يحتوي الجدول → عدّاد نتائج/ترقيم — `inferred`
- Grid & alignment: عمود واحد بعرض محتوى محدود؛ العناوين والنص `start`، الأرقام `end` — `inferred`
- Spacing: سلّم 4px؛ حشو خلية `space-sm`/`space-md`، فجوات قسم `space-lg` — `inferred`
- Typography: IBM Plex Sans Arabic (افتراضي tokens.css)؛ معاينة CSP → fallback لـ system-ui — `inferred`
- Color: محايد كامل؛ الإجراء = `--color-accent` (placeholder أزرق)؛ ألوان الحالة الوظيفية للشارات — `observed (tokens)`
- Border radius: كرت `radius-lg`، حقول/شارات `radius-sm/md` — `inferred`
- Shadows: كرت بظل ناعم `shadow-sm`؛ القائمة المنسدلة `shadow-md` — `inferred`
- Components: page-header, filter-bar, table, status-badge, button, empty-state — `observed (INDEX)`
- Icons: أيقونة بحث `inline-start` داخل الحقل؛ أيقونة فرز؛ أيقونة حالة فارغة وظيفية — `inferred`
- Content density: متوسطة (تطبيق بيانات) — `inferred`
- RTL: كامل؛ تدفّق الأعمدة من اليمين؛ أرقام لاتينية جدولية؛ عملة معزولة bidi — `observed (table.md/04)`
- Ambiguous: أعمدة الجدول الدقيقة وعددها — `inferred` (اخترت 5 أعمدة دلالية، بلا حشو أعمدة — forbidden #5)
- Data: **بيانات تجريبية صناعية بلا PII** (أسماء حسابات/شركات، لا أفراد ولا جوالات) — لا اختلاق بيانات حسّاسة (00 Ask-vs-Assume)

## Components Used  *(check `components/INDEX.md`)*
- page-header · filter-bar · table · status-badge · button · empty-state — كلها موثّقة (Spec ✅ / Impl ✗ → تُبنى ضد الـspec).
- Missing component/token → documented first: **لا شيء جديد**. (الترقيم: تركيبة موثّقة في INDEX «Compositions»، لا مكوّن — استُخدم كعدّاد + أزرار prev/next.)

## Data States  *(الخمسة — table.md §3)*
- Loading: صفوف هيكلية (skeleton) بعدد متوقّع (~6).
- Empty (first-use): empty-state داخل جسم الجدول — أيقونة بسيطة + عنوان heading + إجراء «أنشئ أول فاتورة».
- No-results (بعد فلترة): رسالة + رابط «امسح الفلاتر».
- Error: empty-state خطأ + «أعد المحاولة».
- Filled: الافتراضي (الحالة المعروضة رئيسيًا).
- No Permission: خارج النطاق (المستخدم مخوّل).

## Content Rules
- نص الواجهة عربي طبيعي (لا ترجمة حرفية، 04 §10). مصطلح حالة واحد ثابت لكل قيمة.
- أرقام لاتينية `tabular-nums`؛ تاريخ موحّد «22 يونيو 2026»؛ العملة «1,250.00 ر.س» معزولة bidi.
- بيانات الصفوف تجريبية وصناعية، بلا PII أو أرقام حسّاسة.

## Layout Rules
- خصائص Tailwind منطقية فقط؛ سلّم المسافات؛ عرض محتوى محدود (`layout.md`). الأكسنت للإجراء/المحدّد فقط.

## Visual Polish and Motion
### Observed in Reference
- لا شيء (لا صورة).
### Needed for This Page
- row hover (`hover:bg-muted`)؛ focus-visible ring على الحقول/الأزرار/الصفوف القابلة للفرز؛ `transition-colors` خفيف؛ skeleton للتحميل.
### Not Needed
- SVG زخرفية، scroll reveal، حركة هيرو، رسمة حالة فارغة كبيرة (تطبيق بيانات → أيقونة فقط، 05 + empty-state.md).
### Motion
- `transition-colors duration-150 ease-out`؛ `motion-reduce:transition-none`.
### SVG / Illustration
- أيقونات وظيفية فقط (بحث/فرز/حالة فارغة)، `aria-hidden`، `currentColor`. لا رسمة كبيرة (data app).
### Interaction Feedback
- زر hover/active/focus؛ حقل focus ring؛ صف hover؛ رأس قابل للفرز focus + `aria-sort`.
### Reduced Motion Handling
- `prefers-reduced-motion: reduce` يعطّل كل الانتقالات.
### Performance Risks
- لا شيء (أيقونات inline، بلا صور خارجية).

## Responsive Behavior  *(mandatory)*
- Desktop: جدول كامل داخل كرت.
- Tablet: نفسه؛ شريط الفلاتر يلتفّ (`flex-wrap`).
- Mobile: تمرير أفقي للجدول داخل حاوية `overflow-x-auto` (لا قصّ صامت — forbidden #16). (تحوّل بطاقة-لكل-صفّ = تحسين مستقبلي موثّق، خارج نطاق هذا الاختبار.)
- Table: لا تكسر الصفحة؛ تمرير أفقي على الجوال.
- Navigation: لا shell/تنقّل عام (08 — لم يُطلب shell؛ قسم مستقل فقط).
- Form: لا نماذج في هذه الصفحة (الإنشاء عبر زر يقود لمكان آخر — خارج النطاق).
- Card / list: الكرت يحوي الجدول.
- Overflow handling: `overflow-x-auto` للجدول؛ اقتطاع نص الخلايا بـ`truncate` مع إتاحة الكامل.
- Sticky elements: رأس الجدول لاصق (`--z-sticky`) — اختياري؛ مُطبّق.

## Forbidden (this page)
- لون/قيمة خارج التوكنز · مكوّن غير موثّق · محتوى مختلق/بيانات حسّاسة · قيم Tailwind عشوائية (لا Pixel Clone) · أدوات اتجاهية في RTL (`ml/mr/left/right/text-left/right`) · أكثر من إجراء أساسي واحد · أعمدة حشو · لون شارة بلا نص.

## Out of Scope
- شِل/تنقّل عام (`_APP.md`)؛ نموذج إنشاء الفاتورة؛ منطق فرز/فلترة حيّ؛ ترقيم حيّ؛ تحميل خط Plex (CSP).

## Post-implementation
- QA per `design-protocols/03` (system + visual-N/A + Tailwind compliance + `05` Required Output). انظر تقرير QA أدناه.

---

## QA Report  *(per `03` — لا صورة → لا Visual/Pixel QA)*

### System QA (`qa-checklist`)
توكنز فقط ✅ · إجراء أساسي واحد ✅ · أدوات RTL منطقية ✅ · أرقام لاتينية جدولية + عملة معزولة bidi ✅ · شارة حالة نقطة+نص (لا لون وحده) ✅ · رأس الجدول لاصق + فرز `aria-sort` ✅ · حالات البيانات الخمس موثّقة/مُمثّلة ✅ · حالة فارغة أيقونة بسيطة (لا رسمة) ✅ · لا بيانات حسّاسة مختلقة ✅ · تباين AA (نص أساسي ~16:1) ✅.

### Tailwind compliance
كلاسات دلالية فقط (`bg-card/muted/primary`, `text-foreground/muted-foreground`, `border-border`) + السلّم القياسي. لا قيم عشوائية. RTL منطقي فقط. الاستثناءات الموثّقة (var() لا Tailwind utility): `z-index` الرأس اللاصق + ارتفاعات التحكّم — قيم توكن عبر `var()`، ليست `*-[...]` عشوائية.

### Visual polish & motion QA
| Area | Match % | Issues | Fix |
|---|---:|---|---|
| Motion | 100 | transitions + reduced-motion مطبّقة | — |
| SVG / Motifs | 100 | أيقونات وظيفية فقط | — |
| Hover / Focus States | 100 | row hover + focus ring على الحقول/الأزرار | — |
| Loading / Empty States | 100 | skeleton + empty/no-results/error مُمثّلة | — |
| Surface Depth | 100 | كرت بظل ناعم؛ رأس بخلفية subtle | — |

### Deviations / assumptions
| Location | Difference | Type | Severity | Fix | Scope |
|---|---|---|---|---|---|
| الخط | Plex → system (CSP preview) | Typography | low | تحميل Plex محليًا في المشروع | page |
| الأعمدة | عددها/أسماؤها مُستنتجة (لا صورة) | Content | low | تُؤكَّد من متطلبات حقيقية | page |
| المعاينة | shim يعرّف الكلاسات من tokens.css (لا Tailwind build) | Build | med | تشغيل عبر Tailwind فعلي في المشروع | preview only |

### Done? (per `07`) — كل الصناديق ✅ (انظر رسالة الجلسة).
