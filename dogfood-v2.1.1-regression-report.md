# Dogfood Regression Report — v2.1.1 · صفحة المستخدمين

> اختبار انحدار (regression) على **نفس صفحة المستخدمين** بعد v2.1.1، لإثبات إغلاق الثغرات الثلاث عالية الأثر دون كسر جديد. المعاينة (محدّثة، نفس الرابط): artifact `7d5638c5`. المصدر: [`playground/users-management/`](playground/users-management/).

## 1. ما الذي تغيّر من v2.1.0 إلى v2.1.1 (ضمن النطاق فقط)
| التغيير | الملف |
|---|---|
| **avatar spec** (جديد) | `components/avatar.md` + INDEX + README + BACKLOG(✅) |
| **detail-view spec** (تركيب جديد) | `components/detail-view.md` + INDEX + README |
| **inline-`style=` gate** | forbidden **#18** + quality-gates(DS Gate) + qa-checklist §1 + 07 DoD(box+grep) + LOCAL-STABILITY |
| **filter-bar responsive contract** | `filter-bar.md` §11 |
| **modal/drawer footer order** | `modal.md` §6.6 + `drawer.md` |
| المكوّنات 27 → **29** | INDEX · README · VERSION |
| تحديث الصفحة لتعكس العقود | `playground/users-management/preview.html` + `manifest.md` |

**لم يُمسّ** (بقي في BACKLOG): sidebar/app-shell · data-app header · dark-mode · textarea/radio/switch · breadcrumb · Request Portal · GitHub Review.

## 2. هل أُغلقت الثغرات الثلاث؟
| الثغرة (من dogfood v2.1.0) | الحالة | الإثبات |
|---|---|---|
| **Avatar ad-hoc** | ✅ مُغلقة | الصفحة تستخدم avatar بعقد [avatar.md](design-system/components/avatar.md) (decorative `aria-hidden`، أحرف أولى، خلفية low-emphasis دلالية)؛ forbidden يمنع `.avatar` بلا عقد |
| **Detail بلا spec** | ✅ مُغلقة | رأس التفاصيل + `dl` يتبع [detail-view.md](design-system/components/detail-view.md) (لا كرت لكل حقل، لا جدول key-value) |
| **inline-`style=` خام** | ✅ مُغلقة | forbidden #18 + الفحص الموسّع؛ أُزيل `row-reverse` و`2px` الخام؛ المتبقّي **fixture موثّق بتعليق + token-var** فقط (صفر خام غير موثّق) |
| (+) filter-bar responsive | ✅ أُضيف | §11 عقد desktop/tablet/mobile(drawer)/RTL |
| (+) modal footer order | ✅ أُضيف | §6.6: محاذاة inline-end + DOM [ثانوي,أساسي]، **لا row-reverse** |

## 3. هل ظهر كسر جديد؟
**لا.** التغييرات إضافية ومتوافقة خلفيًا. الصفحة تُصيّر كما قبل (التعديلان السلوكيان: ترتيب أزرار المودال صار قانونيًا بدل row-reverse؛ والأيقونات بلا إزاحة 2px — كلاهما تحسين بصري طفيف لا كسر). لا منطق حيّ (shim).

## 4. هل مرّت الفحوص؟ (إثبات أن LOCAL-STABILITY يلتقط المخالفات الجديدة)
| الفحص | النتيجة |
|---|---|
| arbitrary Tailwind `[...]` | **PASS** (صفر) |
| أدوات RTL اتجاهية | **PASS** (منطقي فقط) |
| **inline-`style=` raw (الفحص الجديد)** | **يلتقطها فعلًا** — كشف 3: `minmax` + skeleton widths (fixture موثّق) + `padding:var()` (token-var مسموح)؛ **صفر خام غير موثّق**. وكشف وأزال `row-reverse` و`2px` |
| الخط IBM | **PASS** (`--font-family-base` يبدأ بـIBM Plex Sans Arabic؛ المعاينة CSP→system موثّق) |
| الأوسمة/الإصدار | v2.1.1 موحّد عبر VERSION ×2 / README / LOCAL-STABILITY / CHANGELOG ×2 |

> **برهان أن البوّابة تعمل:** الفحص القديم (Tailwind `[...]` فقط) كان يمرّ على `row-reverse`/`2px`؛ الفحص الجديد **التقطهما**، فأُزيلا أو وُثّقا. هذا بالضبط الـgap الذي ظهر في dogfood v2.1.0.

## 5. الإثباتات المطلوبة صراحةً
- ✅ **avatar لم يعد ad-hoc** — بعقد avatar.md، مُسجّل في INDEX، ممنوع بلا spec.
- ✅ **detail view يستخدم spec واضح** — detail-view.md (dl دلالي، قواعد بصرية).
- ✅ **لا inline styles raw غير موثقة** — الباقي fixture موثّق بتعليق + token-var؛ row-reverse/2px أُزيلا.
- ✅ **filter-bar responsive contract موجود** — §11.
- ✅ **modal footer لم يعد row-reverse يدوي** — §6.6 + الصفحة تستخدم `justify-end` + ترتيب DOM.
- ✅ **LOCAL-STABILITY يلتقط المخالفات الجديدة** — الفحص الموسّع يكشف inline-style، موثّق في 07/LOCAL-STABILITY.

## 6. هل v2.1.1 جاهز كقاعدة قبل Request Portal؟
**نعم.** الثغرات الثلاث عالية الأثر مُغلقة، +2 عقد صغيران، صفر كسر، كل الفحوص الحاجبة مرّت، الإصدار موحّد. المؤجّلات الباقية **ليست حاجبة** لصفحة واحدة؛ أوّلها (sidebar/app-shell + data-app header) يصبح ضروريًا فقط عند أول **تطبيق متعدّد الصفحات** (مثل Request Portal بشاشاته) — وهذا هو الاختبار التالي الذي يقرّر ترقيته.

## الحكم النهائي
**v2.1.1 يجتاز الـregression وجاهز كأساس.** التوصية: الانتقال إلى Request Portal **سيكون أول اختبار يثبت إن كان sidebar/app-shell + data-app header حاجبَين** — عندها يُرقّيان من BACKLOG؛ وإلا يبقيان مؤجّلَين.
