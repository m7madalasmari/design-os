# Visual Regression Report — صفحة المستخدمين (Visual Polish Gate)

> **هذا التقرير يصحّح حكمًا سابقًا خاطئًا.** تقرير dogfood v2.1.0 قال «نجح» اعتمادًا على البنية/الوصول/التوكنز — **دون مراجعة بصرية للمُخرَج المُصيَّر**. مراجعتك البصرية للـpreview كشفت فجوات حقيقية. هذا التقرير مبني على **مقارنة بصرية فعلية** قبل/بعد، ولا يقول «نجح» إلا بعدها. المعاينة (مُصلَحة، نفس الرابط): artifact `7d5638c5`.

## 1. الاعتراف بالفجوات (مع السبب الجذري)
السبب الجذري **واحد ومحدّد**: shim المعاينة **أغفل native-control reset** — فالأزرار و`<select>` و`<input type=search>` ورثت مظهر المتصفّح الافتراضي. هذا **يخالف قواعد design-os نفسها** (button.md §10، select.md، search-input.md «لا مظهر أصلي») — لكن **لا بوّابة كانت تفرضه على المُخرَج**، وتقريري قاس البنية لا التنفيذ البصري.

| ما رصدتَه | السبب الجذري | حقيقي أم shim؟ |
|---|---|---|
| أزرار بـstroke أسود ثقيل | حدّ زرّ المتصفّح الافتراضي (لا `appearance:none`) | **حقيقي — خلل** |
| حقل بحث بحدّ/إدخال داخلي مزدوج | `<input type=search>` يحمل حدّه الأصلي داخل wrapper ذي حدّ | **حقيقي — خلل** |
| select ضعيف/native | `<select>` بسهم وchrome المتصفّح | **حقيقي — خلل** |
| close ثقيل وغير متوازن | حدّ زرّ أصلي حول أيقونة الإغلاق | **حقيقي — خلل** |
| أزرار المودال native/default | نفس سبب الأزرار | **حقيقي — خلل** |
| المودال بدائي بصريًا | تراكم الأعلى (footer أزرار native + select native) | **حقيقي — خلل** |
| الحالات/الفكسچر بدائية | skeleton بالكاد مرئي + CTA native | **حقيقي — جزئيًا** |

**الخلاصة:** فجوات بصرية حقيقية، لا مجرد قيود shim. والتقرير السابق كان يجب ألا يقول «نجح».

## 2. الإصلاح في البروتوكول (Visual Polish Gate — البوّابة السادسة)
| ملف | التغيير |
|---|---|
| `foundations/component-visual-baseline.md` (جديد) | الأرضية: **native-control reset** إلزامي + حدود خفيفة + focus-visible فقط + overlay مُوكَّن + وزن أيقونة + كثافة ناضجة |
| `rules/visual-polish-gate.md` (جديد) | **البوّابة السادسة** — تُفحَص بصريًا على المُخرَج لكل من Buttons/Inputs/Modal/Select/Table/States |
| `rules/forbidden-patterns.md` | **#19–#24**: حدّ أسود/ثقيل · عناصر native · حدّ مزدوج · focus دائم · overlay خام · fixtures بدائية |
| `rules/component-quality-gate.md` | يفحص الآن **جودة التنفيذ البصري** لا الوجود فقط («وجود المكوّن ≠ جودته») |
| `rules/quality-gates.md` · `qa-checklist.md` · `ROLES.md` · `AGENTS.md` | البوّابات صارت **ست**؛ §11 بصري في الـchecklist |

## 3. إصلاح الـpreview نفسه (قبل/بعد)
| العنصر | قبل | بعد |
|---|---|---|
| **Buttons** | حدّ متصفّح أسود، مظهر native | `appearance:none` + variants توكنز (primary تعبئة / secondary حدّ subtle / ghost) + focus-visible فقط |
| **Search** | حدّ مزدوج (input أصلي داخل wrapper) | الحقل `border:0` داخل wrapper بحدّ subtle + `focus-within` ring + إخفاء زينة search الأصلية |
| **Select** | سهم وchrome المتصفّح | `appearance:none` + **سهم chevron مخصّص** محاذى `inline-end` + حدّ subtle واحد |
| **Modal close** | زرّ بحدّ أصلي ثقيل | **icon button ghost** subtle (بلا حدّ) |
| **Modal footer** | أزرار native + `row-reverse` يدوي | أزرار توكنز + ترتيب قانوني §6.6 (`justify-end`، DOM [ثانوي,أساسي]) |
| **Overlay** | — | `--color-bg-overlay` (توكن) |
| **Skeleton** | بالكاد مرئي (bg-subtle) | أوضح (`--color-bg-hover`) + عرض متدرّج |
| **States CTAs** | تبدو native | بعد الـreset → variants مصقولة |

## 4. إثباتات الانحدار المطلوبة
| المطلوب | الحالة | الإثبات |
|---|---|---|
| لا button بـblack stroke دائم | ✅ | grep: لا `border:…black`/`solid #000`؛ reset أزال حدّ المتصفّح |
| لا input مزدوج border | ✅ | reset → `input{border:0}` داخل wrapper ذي حدّ واحد |
| لا select native/default | ✅ | grep: `appearance:none` + `select-chevron` موجودان |
| لا modal close ثقيل | ✅ | ghost icon button بلا حدّ |
| لا أزرار native في footer | ✅ | reset + ترتيب §6.6 (لا row-reverse) |
| table visual density متوازن | ✅ | حدود subtle + حشو من السلّم + أزرار/شارات مصقولة |
| states/fixtures ليست بدائية | ✅ | skeleton أوضح + CTA variants + أيقونات tokenized |
| كل styles tokens/utilities | ✅ | صفر arbitrary · inline موثّق فقط (forbidden #18) |
| **فحص يلتقط هذا مستقبلًا** | ✅ | **helper grep لغياب `appearance:none`** في أي preview + بوّابة Visual Polish (مراجعة بصرية) + forbidden #19–#24 + LOCAL-STABILITY |

## 5. الحكم (بعد المقارنة البصرية)
- الفجوات البصرية الحقيقية السبع **أُغلقت** في الـpreview، وسببها الجذري (غياب native-control reset) **صار ممنوعًا ومُبوَّبًا** فلا يتكرّر صامتًا.
- **v2.1.0 لم يكن «ناجحًا بالكامل»** كما ادّعى التقرير الأول — كان ناجحًا بنيويًا/a11y، **فاشلًا بصريًا**. الآن بعد إضافة Visual Polish Gate وإصلاح المعاينة: **يجتاز المراجعة البصرية**.
- **الدرس المنهجي المثبّت:** لا يُقال «نجح» بناءً على «المكوّن من INDEX» أو «a11y مرّ» — تُضاف مراجعة بصرية للمُخرَج المُصيَّر كبوّابة إلزامية. (هذا ما تطلبه، وأُنفِّذ.)

> **شكرًا على النقد البصري** — كشف فجوة منهجية حقيقية (تقييم البنية بدل التنفيذ). البوّابة السادسة هي الإصلاح الدائم.
