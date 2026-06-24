# Dogfood Report — v2.1.0 · صفحة إدارة المستخدمين

> اختبار عملي كامل لـdesign-os **v2.1.0 كما هو** على طلب واقعي. المخرجات: [`playground/users-management/`](playground/users-management/) (`preview.html` + `manifest.md`). المعاينة: artifact `7d5638c5`. **الهدف: كشف الضعف الحقيقي، لا إثبات النجاح.**

## 1. ملخص الطلب
«صفحة مستخدمين عربية: جدول · فلترة · بحث · حالات مستخدم · صفحة تفاصيل · أكشن تعديل الحالة · رسائل نجاح/خطأ.»

## 2. كيف فُسِّر الطلب
- **Mode:** لا هوية/لون/مرجع → **Greenfield/System-First**، الثيم الافتراضي neutral، IBM Plex.
- **presentation-by-content** (anti-bland §7) قاد القرار: قائمة متجانسة→**Table** · مستخدم واحد→**تخطيط تفصيل** (key-value) · «تعديل الحالة» إجراء قصير مركّز→**Modal** · النجاح/الخطأ→**رسائل** (status/alert).
- لا shell عام (08 — لم يُطلب). إجراء أساسي واحد: «إضافة مستخدم».

## 3. المكوّنات المولّدة (كلها من INDEX — لا مكوّن جديد)
page-header · search-input · filter-bar (شرائح حالة + عدّادات) · table (+caption/scope/aria-sort) · status-badge (نشط/مدعو/موقوف) · button (primary + secondary) · pagination · empty-state (×4) · select · modal (عقد a11y) · رسائل success/error · **تخطيط تفصيل** (تركيب: page-header + `dl` + status-badge).

## 4. الـTokens المستخدمة
semantic فقط: أسطح/نص/حدود محايدة · `--color-accent`(=brand-600) للإجراء/المحدّد · **`--color-secondary`** (محايد — جديد v2.1.0) لزر «تعديل الحالة» · شارات الحالة الوظيفية · `--color-text-link`=**brand-700** · `--shadow-focus`. **صفر قيم Tailwind arbitrary.**

## 5. تطبيق البوّابات الخمس
| البوّابة | النتيجة | الدليل |
|---|---|---|
| **Design System** | ✅ | توكنز فقط، صفر arbitrary، كل كتلة من INDEX، secondary محايد لا براند |
| **Typography** | ✅ | `--font-family-base` يبدأ بـIBM Plex Sans Arabic؛ سلّم متوازن (h1=30، لا hero)؛ جسم 1.7 · *(المعاينة CSP→system-ui موثّق)* |
| **Component Quality** | ✅ | الجدول: 7 حالات + a11y wiring؛ المودال: عقد `role=dialog`/focus-trap/return-focus؛ المكوّن الصحيح للمهمة |
| **Anti-Generic** | ✅ | 3 أنماط عرض · ≥2 علاقتي مسافات · شبكات متنوّعة · تسلسل ≥2 إشارة |
| **Accessibility** | ✅ | AA تباين · كيبورد/focus ring · ARIA/semantic · reduced-motion · RTL منطقي |

## 6. ما الذي نجح
- **البوّابات الخمس طبّقت كلها** على طلب حقيقي دون افتعال.
- **الـDefault DS كافٍ:** الصفحة بُنيت بالكامل من النظام، **بلا أي مكوّن جديد**.
- **`--color-secondary` (المُضاف في v2.1.0) أثبت لزومه فورًا** — زر الإجراء الصفّي احتاج توكن ثانوي محايد؛ لولاه لاستُخدم accent (خطأ تسلسل) أو hex.
- **anti-bland قابل للتطبيق فعليًا:** القواعد قادت قرارات ملموسة (الجدول للقائمة، dl للتفصيل، modal للإجراء) — ليست شعارًا.
- **a11y صار عقدًا:** caption/scope/aria-sort للجدول وrole=dialog/aria-modal للمودال طُبّقت لأن v2.1.0 جعلتها عقدًا لا نثرًا.

## 7. ما الذي فشل أو ظهر ضعيفًا
1. **لا spec لـ«تخطيط تفصيل / description-list».** التفصيل رُكّب يدويًا (`dl` + page-header + badge) — نجح لكن **بلا عقد** → خطر تباين بين مشاريع. (متوسط-عالٍ، غير حاجب.)
2. **لا spec لـAvatar/الأحرف الأولى.** جدول المستخدمين احتاج avatar (أحرف أولى) — صُنع ad-hoc بكلاس `.avatar`. كل صفحة أشخاص تحتاجه. (عالي الأثر.)
3. **قيم خام عبر `style=` تتكرّر** (عروض skeleton · `minmax(260px,1fr)` · إزاحات 2px · `row-reverse`). فحص v2.1.0 يلتقط Tailwind `[...]` **لا** inline-style الخام. تكرّرت في dogfood «الفواتير/الاستشارات» أيضًا → **ثغرة بوّابة موثّقة.** (في Tailwind حقيقي تصير utilities؛ هنا shim.)
4. **ترتيب أزرار تذييل المودال** عُمل بـ`row-reverse` يدويًا — modal.md يقول «ترتيب ثابت منطقي» دون **ترتيب قانوني محدّد**. ad-hoc صغير. (منخفض.)
5. **معرض الحالات (states demo)** أربع بطاقات بنفس الشبكة — لو كان قسم منتج لخالف anti-bland #1/#2؛ مقبول هنا لأنه fixture توضيحي مُعلَّم (قاعدة fixture-vs-consumer). **ملاحظة:** anti-bland لم «يُرفَض» هذا لأنه استثناء fixture — صحيح، لكن جدير بالانتباه.

## 8. هل ظهر generic / bland UI؟
**لا في صفحة المنتج.** التمايز حقيقي: جدول كثيف + تفصيل key-value + مودال + رسائل ملوّنة وظيفيًا، بإيقاع متنوّع وتسلسل واضح. **الاستثناء الوحيد** هو معرض الحالات (4 كروت متطابقة) — مبرّر كـfixture، لكنه يذكّر أن anti-bland يحتاج يقظة في الأقسام التوضيحية.

## 9. هل الجداول والفلاتر قوية بما يكفي؟
**نعم، قوية:** الجدول فيه caption/scope/aria-sort + رأس لاصق + 7 حالات + شارات نقطة+نص + إجراء صفّي متّسق + RTL (بريد bdi ltr، أرقام tabular) + عقد responsive (موثّق). الفلاتر: بحث + شرائح حالة بعدّادات — كافٍ لعدد حالات قليل. **ضعف كامن:** filter-bar ينقصه عقد **انهيار responsive** (شريط→ورقة على الموبايل) — لم يُختبر هنا لكنه مرصود في التدقيق.

## 10. هل احتجنا spec مؤجّلًا من الـBACKLOG؟
**لا شيء حاجب.** الصفحة شُحنت كاملة من v2.1.0. لكن ظهرت حاجة **عالية الأثر** لـ: Avatar · detail/description-list · (لتطبيق متعدّد الصفحات) sidebar/app-shell. لم يُحتَج textarea/radio/switch (select + chips غطّيا)، ولا dark-mode.

## 11. Bugs / Gaps
- **Gap-1 (عالٍ):** لا spec Avatar.
- **Gap-2 (عالٍ):** لا spec detail-view/description-list.
- **Gap-3 (متوسط):** ثغرة بوّابة — inline `style=` الخام لا يلتقطه فحص arbitrary (تكرّر مرّتين).
- **Gap-4 (متوسط):** filter-bar بلا عقد responsive.
- **Gap-5 (منخفض):** لا ترتيب قانوني لأزرار تذييل modal/drawer.
- **Bug:** لا أخطاء وظيفية حاجبة. (الصفحة ساكنة—shim؛ لا منطق حيّ.)

## 12. توصيات v2.1.1
1. **Avatar spec** (أحرف أولى/صورة/أحجام/RTL/fallback) — ترقية من BACKLOG.
2. **detail-view / description-list spec** (نمط `dl` key-value + تركيب الأقسام + responsive).
3. **إغلاق ثغرة البوّابة:** في `forbidden-patterns` + الفحص الثابت: «قيم `style=` الخام arbitrary ما لم تكن token-var exception موثّقة».
4. **ترتيب قانوني لأزرار تذييل modal/drawer** (الأساسي في جهة محدّدة) في modal.md/drawer.md.
5. **عقد responsive لـfilter-bar** (انهيار لورقة على الموبايل).
6. (لاحقًا، ليس v2.1.1) sidebar/app-shell + data-app header للتطبيقات متعددة الصفحات.

## 13. تصنيف المؤجّلات (بعد الاختبار)
| التصنيف | العناصر |
|---|---|
| **Blocking** (قبل أي طلب جديد) | **لا شيء** — v2.1.0 ولّد الصفحة كاملة |
| **High impact** (لـv2.1.1) | Avatar spec · detail/description-list spec · إغلاق ثغرة inline-style |
| **Nice to have** | filter-bar responsive · ترتيب أزرار المودال · breadcrumb · textarea/radio/switch مستقلة |
| **Not needed yet** | sidebar/app-shell + data-app header (يصبح High عند أول تطبيق متعدّد الصفحات) · dark-mode tokens |

## الحكم النهائي
**v2.1.0 يجتاز الـdogfood.** الأساس الافتراضي الإجباري أنتج صفحة مستخدمين عربية احترافية، متّسقة، متاحة، **غير generic** — بلا أي إدخال من المستخدم وبلا مكوّن جديد. الثغرات الثلاث عالية الأثر (Avatar · detail pattern · inline-style gate) **تحسينات لا حواجز**، تُعالَج في v2.1.1.
