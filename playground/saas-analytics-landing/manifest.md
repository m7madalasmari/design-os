# Page Manifest — صفحة هبوط «نبض» (منصة تحليلات SaaS)

> Playground fixture لاختبار **System Fidelity Mode** على صفحة هبوط تسويقية عربية RTL، مستوحاة من صورة مرجعية (وكالة تسويق WizardZ) ومطبَّقة داخل نظام التصميم. ليست صفحة منتج ولا تُنسخ لمشروع مستهلك.

- **Mode:** System Fidelity *(الطلب «مستوحاة … داخل النظام»؛ مرجع بصري موجود → Auto حُلَّ إلى System Fidelity)*
- **Direction:** RTL (ar)
- **Theme:** `theme-moonli` *(أسود فعل + ليموني سطح علامة — وهو بالضبط لوحة «الأسود/الأخضر» في المرجع، وتباينه مُثبَت مسبقًا)*
- **Reference:** صورة مرفقة — صفحة هبوط وكالة تسويق رقمي (WizardZ): أبيض + أسود + أخضر ليموني، كروت متناوبة، تسميات أقسام مظلَّلة، رسوم خطية مجرّدة.
- **Preview runtime:** **Shim mirror** — shim موثّق يطابق `design-system/tokens.css` + الكلاسات الدلالية 1:1 (لا توجد بنية Tailwind هنا). **ليس** التنفيذ الإنتاجي.

## Intent
صفحة هبوط لمنتج تقني (منصة تحليلات بيانات باسم **«نبض»**) تنقل من المرجع: **البنية** (ترتيب الأقسام والإيقاع)، و**لوحة الأسود/الأخضر**، و**أسلوب الرسوم الخطية المجرّدة** — مع صياغة عربية أصيلة ومحتوى صادق (بلا شعارات عملاء مختلَقة، بلا أرقام تُعرض كأنها حقيقية).

## Users
زوّار يقيّمون منتج تحليلات: مسؤولو منتج/تسويق/عمليات يبحثون عن لوحة واحدة لمقاييسهم. الهدف: فهم القيمة بسرعة ثم بدء تجربة.

## Primary Action (one)
**«ابدأ مجانًا»** — زر `primary` (تعبئة accent سوداء + نصّ أبيض). يتكرّر بصفته الإجراء المهيمن في الـHero وكتلة الدعوة الوسطى — إجراء أساسي **واحد** متّسق عبر الصفحة.

## Secondary Actions
- شريط التنقّل: **«اطلب عرضًا»** — زر `secondary` (مُحاط بحدّ). فعلٌ مختلف عن الأساسي → لا تنافس على إجراءٍ واحد.
- Hero: **«جولة سريعة»** — `tertiary` (رابط خفيف) بأولوية بصرية أدنى من الأساسي.
- كروت المزايا/الحالات: **«اعرف المزيد»** — روابط `tertiary` بسهم اتجاهي (RTL → يشير لنهاية السطر/اليسار).
- التذييل: تكرار «ابدأ مجانًا» (نفس الإجراء، سياق ختامي).

## Reference Analysis  *(label each)*
- **Page type:** صفحة هبوط تسويقية طويلة (one-pager). *(observed)*
- **Layout structure / main regions:** Nav → Hero (نصّ + رسم) → شريط ثقة/مصادر → قسم مزايا (4 كروت 2×2 متناوبة) → كتلة دعوة وسطى → قسم حالات استخدام (3 كروت داكنة) → تذييل داكن. *(observed)* — نُقلت 1:1 دون إضافة أقسام.
- **Grid & alignment:** عمود محتوى موسّط بعرض محكوم؛ شبكة كروت 2×2 و3 أعمدة؛ المحاذاة الافتراضية `start` (يمين في RTL). *(observed/inferred)*
- **Spacing observations:** فصل أقسام واسع، حشو كروت مريح، إيقاع منتظم. ضُبط على سلّم 4px (`--space-xl`/`-2xl`/`-3xl` بين الأقسام). *(approximate → token scale)*
- **Typography observations:** عنوان hero كبير ثقيل، نصوص داعمة رمادية، تسميات أقسام صغيرة داخل تظليل. مطبّق على السلّم الطباعي (≤ `4xl`) — لا حجم خارج التوكنز. *(observed → tokens)*
- **Color observations (→ tokens):** أبيض خلفية، أسود للنصّ/الأفعال، أخضر ليموني للتظليل والشارات والأسطح المعدودة، كروت سوداء معتمة. → خريطة على **theme-moonli**: `--color-accent` أسود (#1C1C24)، `--color-brand` ليموني (#C6F24E، سطح فقط)، تعبئة كرت `dark` = `--neutral-12`. *(observed → tokens)*
- **Border radius:** زوايا واضحة على الكروت/الأزرار. → `--radius-md` (12) للأزرار/الكروت الصغيرة، `--radius-lg` (24 في moonli) للكروت الكبيرة/اللوح. *(approximate)*
- **Shadows / depth:** الارتفاع بالحدّ غالبًا؛ ظلّ خفيف على اللوح العائم. → `--shadow-sm`/`-lg`. *(approximate)*
- **Components:** nav-bar · hero · card (fills: surface/dark/brand) · section-header + brand-highlight-mark · button · site-footer. *(observed)*
- **Icons / images:** رسوم خطية مجرّدة (حلقات مدارية، خطّ نبض، نجمة رباعية، عُقد) + شارات ليمونية صغيرة. أُعيد تأليفها كزخرفة علامة متّسقة (نبض/تحليلات)، لا نسخًا حرفيًا. *(inferred — System Fidelity)*
- **Content density:** متوسطة-منخفضة (تسويقي)، فراغ متعمّد. *(observed)*
- **RTL/LTR direction:** المرجع LTR؛ الهدف **RTL** — انعكاس كامل للتخطيط والرسوم والأسهم. *(decision)*
- **Ambiguous details:** ألوان hex الدقيقة، الزوايا، الظلال، سلوك hover/التجاوب — غير مقاسة من الصورة → استُمدّت من التوكنز ووُثّقت كـ approximate.
- **Implementation assumptions:** انظر «Deviations / Assumptions» أدناه.
- **Arbitrary values used + justification:** **صفر** (System Fidelity لا يسمح بها).

## Components Used  *(from `design-system/components/` only)*
- [nav-bar](../../design-system/components/nav-bar.md) — شعار + روابط + CTA ثانوي واحد؛ sticky؛ قائمة جوال عبر `<details>` (إفصاح بلا JS).
- [hero](../../design-system/components/hero.md) — عنوان قيمة + جملة + إجراء أساسي + رسم زينة `aria-hidden`.
- [card](../../design-system/components/card.md) — تعبئات `surface` (كروت بيضاء) و`dark` (كروت سوداء)؛ نصّ on-dark أبيض.
- [section-header](../../design-system/components/section-header.md) + **Brand highlight mark** (تركيب موثّق في INDEX: خلفية `--color-brand` خلف نصّ التسمية).
- [button](../../design-system/components/button.md) — `primary` (accent أسود) · `secondary` (محاط) · `tertiary` (رابط+سهم).
- [site-footer](../../design-system/components/site-footer.md) — تعبئة داكنة، روابط فاتحة، حقوق نشر.
- **Missing component/token documented first:** لا جديد. كل الكتل تُخرَّط على INDEX. لوحة الليموني موجودة أصلًا في [theme-moonli](../../design-system/themes/theme-moonli.md) (إعادة استخدام، لا توكن جديد).

## Data States
صفحة تسويقية ثابتة (لا جلب بيانات حيّ) — الحالات التطبيقية الخمس لا تنطبق:
- Loading: لا ينطبق (محتوى ثابت). · Empty: لا ينطبق. · Filled: الحالة الوحيدة (محتوى تسويقي). · Error: لا ينطبق. · No Permission: لا ينطبق.
- نموذج النشرة/البدء (إن فُعِّل لاحقًا) سيتبع [form](../../design-system/components/form.md) — خارج نطاق هذه المعاينة الثابتة.

## Demo Data Policy
- **Uses demo data:** نعم — أرقام «حالات الاستخدام» فقط.
- **Data type:** مؤشّرات أداء توضيحية (مثل «‎−32% زمن اكتشاف العطل»).
- **PII risk:** لا شيء (لا أسماء/بريد/أرقام تواصل/معرّفات حقيقية).
- **Labeling:** القسم يحمل شارة ظاهرة **«الأرقام عيّنة توضيحية»**، وكلّ رقم معزول bidi بأرقام لاتينية جدولية.
- **Reason:** معاينة/مثال — لإظهار طاقة «كرت الإحصاء» في المرجع **دون** عرض أرقام كأنها حقيقية.
- **شعارات العملاء:** المرجع يعرض شعارات شركات حقيقية (Amazon/Netflix…). **استُبدلت** بشريط **مصادر/تكاملات** صادق (SQL · API · CSV · Webhooks · جداول) — وصفُ قدرة لا ادّعاء رعاية (تجنّب اختلاق تأييد — ممنوع #5/#6).

## Content Rules
- كل النصوص عربية أصيلة (لا ترجمة حرفية): «ابدأ مجانًا»، «اعرف المزيد»، «اطلب عرضًا».
- أرقام لاتينية جدولية معزولة bidi؛ نظام أرقام واحد؛ السنة «2026».
- نبرة مهنية موجزة، بلا مبالغة/إيموجي (ux-writing، ممنوع #6/#7).

## Layout Rules
- أدوات Tailwind منطقية فقط (`ms/me`, `ps/pe`, `start/end`, `text-start/end`).
- عرض المحتوى محكوم (`max-w-6xl`) موسّط؛ الانهيار لعمود واحد على الجوال.
- **سطح اللوح العائم (page-level):** الخلفية الخارجية تستخدم `var(--neutral-4)` (توكن primitive) كـ«canvas» يطفو فوقه لوحٌ أبيض (`--color-bg-surface`) — قرار تخطيط على مستوى الصفحة (ليس مكوّنًا يلمس primitive)، موثّق هنا. يحاكي «اللوح الأبيض العائم على رمادي» في المرجع، بدرجة أهدأ.

## Token Var Exceptions  *(tokens with no Tailwind utility)*
| Location | Token | Reason | Utility unavailable? |
|---|---|---|---|
| nav (sticky) | `--z-sticky` | لا توكن z مُولَّد كأداة — يُستهلك عبر `var()` | نعم |
| المعاينة (canvas) | `--neutral-4` | سطح صفحة عام يحاكي رمادي المرجع؛ لا أداة دلالية له | نعم (primitive موثّق على مستوى الصفحة) |
| نصّ خافت على داكن | `--neutral-7` | نصّ ثانوي فوق الكروت/التذييل الداكنة (≈9:1) | نعم (لا أداة on-dark-muted) |
| شارة «عيّنة توضيحية» (نقطة) | `--color-warning-fg` | لون حالة لنقطة وسم البيانات التجريبية؛ لا أداة `bg-warning` في الـshim | نعم |
| سطر المعاينة (ملاحظة) | `--color-danger-fg` | لون تنبيه لنصّ وسم «أرقام عيّنة توضيحية» (scaffolding) | نعم |
| رسوم SVG | `--color-brand` · `--color-text-primary` · `--color-on-brand` · `--color-border-strong` · `--color-bg-surface` | تعبئة/حدّ الرسوم بتوكنز (مسموح صراحةً في `05`: SVG يستخدم currentColor أو توكنز) — ليست قيمًا عشوائية | غير منطبق (SVG attr) |

## Responsive Behavior
- **Desktop (≥768px):** Hero عمودان (نصّ/رسم)؛ مزايا 2×2؛ حالات 3 أعمدة؛ روابط nav ظاهرة.
- **Tablet:** نفس البنية مع تضييق العرض؛ الشبكات قد تنهار مبكرًا.
- **Mobile (<768px):** عمود واحد لكل الشبكات؛ روابط nav تُطوى خلف زر قائمة (`<details>`)؛ يبقى CTA الأساسي ظاهرًا.
- **Table:** لا جداول.
- **Navigation:** قائمة `<details>` على الجوال (إفصاح، كيبورد-وصول).
- **Form:** لا نماذج في هذه المعاينة.
- **Card / list:** الكروت تنهار لعمود واحد؛ يبقى الترتيب = ترتيب الأهمية.
- **Overflow handling:** لا قصّ؛ النصوص تلتفّ.
- **Sticky elements:** nav لاصق (`--z-sticky`) — يعمل ضمن اللوح.

## Visual Polish and Motion
### Observed in Reference
- تظليل ليموني خلف تسميات الأقسام؛ كروت متناوبة أبيض/أسود؛ رسوم خطية مجرّدة + شارات ليمونية؛ سهم «↗» في «Learn more».

### Needed for This Page
- علامة تظليل العلامة (brand highlight) للتسميات. · رسوم خطية مجرّدة متّسقة (حلقات + خطّ نبض + نجمة رباعية + عُقد) تعبّر عن «التحليلات/النبض». · شارات ليمونية صغيرة في الـHero.

### Not Needed
- لا تدرّجات، لا particles، لا blur ثقيل، لا حركة لانهائية زخرفية (ممنوع #6).

### Motion
- `transition-colors` على كل تفاعلي (مدّة `--duration-fast`، `--ease-standard`).
- رفعة خفيفة + سهم يتحرّك عند hover على الكروت/«اعرف المزيد» (تغذية راجعة، لا زينة).
- **لا حركة دخول تُخفي المحتوى** (احترام «لا تأخير لظهور المحتوى»).
- كلّها داخل `motion-reduce` → تتعطّل عند تفضيل تقليل الحركة.

### SVG / Illustration
- كلّها inline، `stroke=currentColor` + توكنات brand، **`aria-hidden="true"`** (زينة علامة لا تحمل معلومة) — مطابق لقاعدة hero/05.

### Interaction Feedback
- أزرار: hover (`--color-accent-hover`)، focus-visible (`--shadow-focus`)، active.
- روابط: underline عند hover؛ كروت داكنة: الرابط يتحوّل لليموني (`--color-brand-strong`) على الداكن (تباين ≈11:1).

### Reduced Motion Handling
- `@media (prefers-reduced-motion: reduce)` يعطّل الانتقالات والرفعات والحركة.

### Performance Risks
- منخفضة: SVG inline خفيف، بلا صور خارجية (CSP)، بلا JS (عدا `<details>` الأصلي).

## Accessibility Notes
- **Keyboard / focus:** كل تفاعلي `<a>`/`<button>`/`<summary>` أصلي؛ ترتيب تركيز = ترتيب القراءة RTL؛ حلقة `--shadow-focus` ظاهرة على الفاتح والداكن.
- **Contrast:** نصّ/أفعال أسود على أبيض (≈16:1)؛ أبيض على الكروت/التذييل الداكنة (≈16:1)؛ on-brand داكن على ليموني (≈14:1)؛ ليموني كنصّ على داكن فقط (≈11:1) — **لا ليموني كنصّ على أبيض**.
- **ARIA / semantic HTML:** `<header><nav><main><section><footer>`، عنوان `h1` واحد، تدرّج عناوين بلا قفز، أيقونات زينة `aria-hidden`، زر القائمة باسم وصول.
- **Reduced motion:** مُحترَم (أعلاه).
- **RTL accessibility:** `dir=rtl` + `lang=ar`؛ أسهم اتجاهية معكوسة؛ أرقام معزولة bidi.
- **Status:** ✅ يجتاز بوابة الوصول (WCAG AA) — انظر QA.

## Forbidden (this page)
ألوان خارج التوكنز · مكوّنات غير موثّقة · محتوى/أرقام مختلَقة تُعرض كحقيقية · قيم Tailwind عشوائية · أدوات اتجاهية في RTL · أكثر من إجراء `primary` واحد · شعارات عملاء وهمية.

## Out of Scope
- نموذج تسجيل فعلي، صفحات أسعار/مدوّنة، روابط حقيقية، تكامل خلفي، أكثر من صفحة.

## Post-implementation
- QA per `design-protocols/03` (System + RTL `04` + Accessibility `06` + Visual-Polish `05`). **Pixel QA:** لا ينطبق صارمًا (System Fidelity، لا نسخ بكسلي) — يُسجَّل تطابق البنية/التسلسل بدل تطابق البكسل.
- **QA Report Location:** Embedded (أدناه).
- **Preview runtime:** **Shim mirror** (يطابق `tokens.css` + الكلاسات الدلالية 1:1).

---

# QA Report  *(embedded)*

**Preview runtime:** Shim mirror · **Mode:** System Fidelity · **Theme:** moonli · **Direction:** RTL

## Role sweep (ROLES.md)
- **Product & Strategy:** `pass` — البنية = المرجع بلا أقسام زائدة؛ إجراء أساسي واحد؛ المجال (تحليلات SaaS) واللوحة مؤكَّدان من المستخدم.
- **UX & Information Architecture:** `pass` — تسلسل القيمة (Hero → قيمة → إثبات → دعوة)؛ تركيب حول المهمة (بدء التجربة)، لا تكديس كروت.
- **Visual & Experience Design:** `pass` — تسلسل/إيقاع/عمق؛ ليموني بشُحّ (60-30-10): تظليل تسميات + شارات + أسطح معدودة، لا ملء كامل؛ دافئ/علامة كبطل ثانٍ لا منافس للفعل.
- **Design System Gate:** ✅ **pass (before impl)** — صفر قيم عشوائية؛ كل كتلة على INDEX؛ لا توكن/مكوّن جديد (إعادة استخدام moonli).
- **Content & UX Writing:** `pass` — عربية أصيلة، نظام أرقام واحد، لا أرقام/شعارات تُعرض كحقيقية (عيّنة موسومة).
- **Accessibility Gate:** ✅ **pass (before delivery)** — انظر القائمة أدناه.
- **Frontend & Implementation:** `pass` — Tailwind-first دلالي، أدوات RTL منطقية فقط، لا CSS موازٍ، بلا JS عدا `<details>`.
- **QA & Validation:** `pass` — انظر الجداول.
- **Documentation & Handoff:** `pass` — manifest + README + DoD.

## Design System QA
- قيم عشوائية (`bg-[#…]`/`p-[…]`/`rounded-[…]`…): **صفر**.
- كل لون/مسافة/زاوية/ظلّ من توكن أو ثيم moonli.
- المكوّنات كلّها من INDEX؛ «Brand highlight mark» تركيب موثّق؛ لا مكوّن جديد.

## RTL QA (`04`)
- `dir="rtl" lang="ar"` على الجذر. · أدوات منطقية فقط (`ms/me`, `ps/pe`, `start/end`, `text-start/end`) — لا `ml/mr/left/right/text-left/right`.
- الشعار `inline-start`، CTA `inline-end`؛ الرسوم على `inline-end` (انعكاس المرجع).
- أسهم «اعرف المزيد»/«جولة» اتجاهية ومعكوسة؛ النجمة/الحلقات غير اتجاهية لا تُعكَس.
- أرقام لاتينية جدولية داخل `<bdi>` (`+/−` ملتصق بالرقم ومعزول).

## Accessibility QA (`06` — WCAG AA)
- [x] عناصر دلالية؛ `h1` واحد؛ عناوين بلا قفز مستوى.
- [x] كل تفاعلي بلوحة المفاتيح وبترتيب منطقي؛ لا فخّ تركيز.
- [x] focus-visible (حلقة التوكن) على الفاتح والداكن؛ لا إزالة outline بلا بديل.
- [x] لكل عنصر اسم وصول؛ زر القائمة والأيقونات الوظيفية موسومة بالعربية.
- [x] التباين ≥ AA (أزواج التوكنز موثّقة أعلاه)؛ لا معنى باللون وحده.
- [x] `prefers-reduced-motion` مُحترَم.
- [x] الرسوم الزخرفية `aria-hidden`.
- [x] RTL: اتجاه/لغة، أسهم معكوسة، أرقام معزولة bidi.

## Visual Polish QA (`05`)
- **أُضيف:** تظليل علامة للتسميات · رسوم خطية مجرّدة متّسقة + شارات ليمونية · رفعة/سهم متحرّك عند hover · حلقة تركيز واضحة.
- **تُرك عمدًا:** لا تدرّجات/particles/حركة دخول تُخفي المحتوى/blur ثقيل.
- **حركة:** انتقالات سريعة فقط، كلّها `motion-reduce`-آمنة.
- **مخاطر أداء:** منخفضة (SVG inline، بلا صور خارجية/JS ثقيل).

## Deviations / Assumptions (labeled)
- لوحة المرجع (أسود/ليموني) → أُسندت لثيم **moonli** الموجود بدل توكن جديد. *(decision — SSOT reuse)*
- شعارات عملاء حقيقية → شريط مصادر/تكاملات صادق. *(decision — تجنّب اختلاق تأييد)*
- أرقام إحصاء حقيقية → عيّنة توضيحية موسومة. *(decision — سياسة بيانات تجريبية)*
- رمادي المرجع الخارجي → `--neutral-4` أهدأ. *(approximate — توثيق انحراف)*
- زوايا/ظلال/hover/تجاوب غير مقاسة من الصورة → من التوكنز. *(approximate)*
- حجم عنوان الـHero مقيّد بـ`--font-size-4xl` (لا قيمة أكبر خارج التوكنز). *(decision — SSOT)*

## Design-system updates required
- **لا شيء.** صفر توكنات/مكوّنات جديدة؛ لا تغيير في `tokens.css` ولا CHANGELOG.

## Result
- **Test:** صفحة هبوط «نبض» — System Fidelity (RTL، ثيم moonli)
- **Result:** ✅ Passed
- **Definition of Done:** ✅ Passed (Pixel QA غير صارم — System Fidelity؛ سُجِّل تطابق البنية/التسلسل)
- **Arbitrary values:** صفر · **Manual self-check:** ✅ · **Components:** كلّها على INDEX، لا جديد.
