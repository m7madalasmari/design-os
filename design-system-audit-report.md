# Design System Audit Report — design-os Default DS

> تدقيق تنفيذي عميق للـ**Default Design System** بعد إصدار v2.0.0 (الطبقات الثلاث). مبني على قراءة فعلية لكل ملفات `design-system/` + البروتوكولات + ROLES. كل بند مدعوم بدليل `file:line`.
> **الهدف:** هل صار الـDefault DS قويًا بما يكفي ليكون الأساس الإجباري لأي مشروع — حتى بلا ألوان/هوية/مراجع من المستخدم؟
> **الحكم المختصر:** البنية **متينة** (RTL، توكنز، تتالي الألوان، 27 spec منضبطة). الثغرة الجوهرية ليست «فوضى/زينة» (مُغطّاة بإحكام) بل **الرتابة (monotony)**: النظام لا يمنع المخرجات الموحّدة الميتة. والطباعة IBM **مضبوطة افتراضيًا لكنها غير مبوّبة**. أُصلح الاثنين في هذا الإصدار (v2.1.0).

**مفتاح الأولوية:** P0 = حاجب للجودة كأساس إجباري · P1 = رفع جودة مهم · P2 = تحسين.

---

## 1. Foundation Audit

| الأساس | الجودة | ناقص | مخاطر | تحسين مطلوب | أولوية |
|---|---|---|---|---|---|
| **Color** | 4.5/5 | لا `--color-secondary`؛ accent ليس متمايزًا عن primary؛ لا dark mode | أسطح `#FFFFFF` صريحة لا تتتالى لو dark لاحقًا | إضافة secondary؛ خطة dark | P1 |
| **Typography** | 4/5 | لا `@font-face` في typography.md؛ غير مبوّبة | تسليم بـsystem-ui يمرّ | typography-system + gate | **P0** |
| **Spacing** | 5/5 | — | إيقاع موحّد ممل (لا قاعدة ضدّه) | (يُعالَج في anti-bland) | — |
| **Radius** | 5/5 | — | — | — | — |
| **Shadow** | 5/5 | — | — | — | — |
| **Border** | 4.5/5 | `--color-input` في @theme فقط | — | توكن إدخال دلالي | P2 |
| **Layout grid** | 4.5/5 | عرض sidebar/shell قيم حرفية لا توكنز | تنقّل data-app غير مُوصَّف كمكوّن | tokenize + sidebar spec | P1 |
| **Breakpoints** | 2.5/5 | **غير موجودة في tokens.css** (نثر في layout.md فقط) | انحراف عن Tailwind، تكسر SSOT | إضافة `--breakpoint-*` لـ@theme | **P0** |
| **Motion** | 4.5/5 | لا `--ease-accelerate` (خروج) | — | إضافة easing الخروج | P2 |
| **Icons** | 5/5 | — | — | — | — |
| **RTL/LTR** | 5/5 | — | — | — (مرجعي) | — |
| **A11y basics** | 4.5/5 | الافتراضي يخالف decoupling الموثّق | link/focus = accent في الافتراضي | link→brand-700 | P1 |

**P0 الأساسات:** (1) Breakpoints غائبة عن SSOT. (2) الطباعة غير مبوّبة.

---

## 2. Token Architecture Audit

النموذج ثلاثي الطبقات **حقيقي وموثّق** (`brand-foundation.md:10-18`) + تير ramp رابع فوق الدلالي (`color-system.md:9-19`).

**Primitive** ✓ (neutral 1–12 · status ×4 · brand-50…950 · raw sizes/spacing/radii/shadow/border-width). **ناقص:** breakpoints.

**Semantic** — مقابل قائمتك:
| مطلوب | الحالة |
|---|---|
| background/foreground/surface/border/border-strong/primary/-hover/-subtle/-foreground/success/warning/danger/info/focus-ring | ✅ موجود |
| surface-muted | ⚠️ موجود باسم `muted` |
| **primary-active** | ❌ في `:root` (accent-active) لكنه **غير مُصدَّر في @theme** — لا utility |
| **secondary** | ❌ غائب تمامًا (الوعد «من المحايد» بلا توكن مُسمّى) |
| **accent (متمايز عن primary)** | ❌ primary = alias للـaccent، لا accent ثانوي مستقل |

**Component (التير الثالث = عقود ربط):** ✓ button/input/table/card/modal/drawer/badge/link/nav. **ناقص من الفهرس:** tabs · alert · toast · form.

**التتالي (الحاسم):** ✅ **يعمل فعلًا**. تتبّع: `--brand-600`→`--accent-solid`(tokens.css:31)→`--color-accent`(45)→`--color-primary`(110)→ربط المكوّن. تبديل البذرة يحدّث كل النظام لا primary فقط (`color-system.md:115-128`). **لكن** الافتراضي يربط link/focus بـbrand-600 خلافًا للمندوب (link=brand-700) — تناقض يُصلَح.

---

## 3. Typography Audit

- **الخط الافتراضي ✅:** `tokens.css:60` = `"IBM Plex Sans Arabic", "IBM Plex Sans", system-ui…` — مطابق للمطلوب. **لا Tajawal/Inter/افتراضي متصفّح في أي مكان.**
- **التحميل ⚠️:** `@font-face` في تعليق tokens.css فقط، غائب عن typography.md — يُضاف (بيئة بلا أدوات).
- **fallback ✅** موثّق (preview فقط، مع ملاحظة ظاهرة).
- **السلّم ✅ متوازن لا مبالغ:** 12→14→16→18→20→24→30→36؛ 36 لـKPI نادرًا فقط (`typography.md:43`). لا أحجام hero 48/60/72.
- **line-height ✅** عربي: 1.7 جسم / 1.3 عناوين (مبرّر بمدّات/تشكيل العربية).
- **letter-spacing/weights ✅** (0 للعربية؛ 400–700؛ الفاتح للعرض الكبير فقط).
- **الكثافة ✅** (14px خلايا كثيفة + tabular-nums؛ density mode).
- **الثغرة الوحيدة:** الطباعة **غير مُنفَّذة كبوّابة** — لا صندوق DoD يتحقّق أن IBM مُحمَّل أو أن السلّم مُطبَّق. → typography-system.md + بوّابة (هذا الإصدار).

---

## 4. Component Structure Audit

27 spec، منضبطة بالتوكنز، قالبان (9-أقسام أقدم · مُسمّى أحدث/أقوى). GOOD: 9 · ADEQUATE: 17 · WEAK: 1.

**أقوى الـspecs:** empty-state · alert · spinner · skeleton · select · pagination · button · input · status-badge.

**ضعيف/يحتاج رفعًا (أهمّها):**
| المكوّن | المشكلة الهيكلية | أولوية |
|---|---|---|
| **modal / drawer** | عقد a11y غائب: `role=dialog`/`aria-modal`/focus-trap/return-focus نثرٌ لا عقد | **P0/P1** |
| **table** | responsive سطر نثر واحد؛ a11y wiring (caption/scope/aria-sort/aria-busy) ناقص | P1 |
| **form** | دورة الإرسال ناقصة (submit-loading · success · server-error recovery) | P1 |
| **checkbox** | يحشر checkbox+radio+switch؛ بلا عقد مجموعة/roving/`role=switch` | P1 |
| **site-footer** | **يحمل hex خام `#FFFFFF`** (يخالف tokens-only #11)؛ بلا anatomy/responsive | P2 |
| tabs/nav-bar/filter-bar/toast/page-header | a11y/responsive كنثر لا عقد | P2 |

**مكوّنات مفقودة (لأساس data-app):**
| مفقود | حالة | أولوية |
|---|---|---|
| **Sidebar / app-shell nav** | مؤجّل لـlayout.md، لا spec مكوّن | **P0** |
| **Header (data-app top-bar)** | nav-bar تسويقي فقط ويمنع data-app | P1 |
| Textarea · Radio · Switch | موعودة/محشورة، بلا spec مستقل | P1 |
| Breadcrumb | يعطّل page-header `with-breadcrumb` | P2 |
| Dashboard KPI Card (مستقل) | مدموج في card.md (كافٍ حاليًا) | P3 |

---

## 5. Anti-Rigidity / Anti-Bland Audit (أهم قسم)

**الاكتشاف المحوري:** النظام **يمنع الفوضى بإحكام، ولا يمنع الرتابة.** كل قواعده «إزالة/توحيد» (سلّم واحد، إيقاع واحد، هيكل صفحة واحد) — وهذا نفسه يُنتج الفشل المعاكس: كل قسم بنفس الشبكة، كل فجوة بنفس المقاس، كل صفحة بنفس الهيكل، كل سطح كرت مسطّح — **صحيح، على التوكنز، متاح، وميّت.**

| الخطر | الحالة الحالية | الدليل |
|---|---|---|
| card-for-everything | ✅ مُغطّى | forbidden #1 · gate §3 |
| نفس الشبكة لكل قسم | ❌ **غائب** | layout.md يَسرد شبكات لا يمنع تكرارها |
| نفس radius/shadow بلا سبب | ⚠️ جزئي | لا قاعدة تُلزم العمق بالتسلسل |
| حدود كثيرة/تعشيش | ✅ مُغطّى | forbidden #4 |
| كل الأزرار بنفس الوزن | ✅ مُغطّى | forbidden #14 |
| زينة بلا وظيفة | ✅ قوي جدًا | forbidden #6 · 05 · principles §1 |
| تسلسل بصري ضعيف | ⚠️ ترتيب مُغطّى، **عمق التباين لا** | ROLES stance فقط، لا اختبار |
| إيقاع مسافات ممل | ❌ **غائب (الثغرة الأساس)** | كل الضغط نحو التوحيد |
| كل الصفحات بنفس التركيب | ❌ **غائب** | page-composition هيكل واحد للكل |
| presentation لا يتنوّع بالمحتوى | ⚠️ جزئي (اختيار مكوّن فقط) | gate §3 على مستوى المكوّن لا الصفحة |
| لا density levels | ⚠️ مستويان فقط (toggle) | spacing.md:57-59 |
| جداول/نماذج زخرفية | ✅ مُغطّى | gate §2 · 05 |

→ **الحل: `anti-bland-ui-rules.md` بثماني قواعد قابلة للفحص** (نُفِّذت في هذا الإصدار) + ترقية «لا generic» من stance إلى **بوّابة رابعة (Anti-Generic Gate)**.

---

## 6. Critical Components Deep Review

**Table:** ✓ header/hover/selected/empty/loading/error/no-results/pagination/row-actions/RTL/cell-spacing · ~ filtering(لـfilter-bar)/hierarchy · ✗ **responsive contract** و**a11y wiring** (caption/scope/aria-sort binding/aria-busy). → يُرفع.

**Modal:** ✓ title/description/action-hierarchy/primary-secondary-cancel/close/width/padding/RTL/not-long-flows · ~ focus-trap (نثر) · ✗ **`role=dialog`/`aria-modal`/`aria-labelledby`/return-focus/scroll-lock**. → عقد a11y يُضاف.

**Form:** ✓ labels/helper/validation/required-optional/grouping/spacing/RTL/not-placeholder-only · ✗ **submit-loading** و**success/server-error recovery**. → دورة الإرسال تُضاف.

**Dashboard:** KPI داخل card.md (رقم+تسمية+اتجاه، ليس رقمًا عاريًا) ✓ · filter-bar ✓ · جداول ✓ · لكن **لا هيكل لوحة مستقل** ولا density-by-content — يُعالَج عبر anti-bland (presentation-by-content) + توصية KPI-card مستقل (P3).

---

## 7. Reference Quality Readiness

`01-image-to-ui` (عقد fidelity: لا تُعِد التصميم) + `03-pixel-qa` (QA لاحق) يغطّيان **نسخ المرئي**. لكن **لا طريقة إعادة بناء** (pixels → blueprint نظامي):
- ✗ إجراء **token-snapping** (قيمة مرصودة → أقرب توكن + تسامح + تصعيد).
- ✗ **blueprint synthesis** (شجرة مناطق → خطة تخطيط، لا قائمة مسطّحة).
- ✗ **gap-fill بلا تشويه** (إضافة حالات/responsive من DS دون تغيير البنية المرصودة).
- ✗ استنتاج density/rhythm وربطه بمستويات DS.

→ **مُبرَّر إنشاء `reference-driven-reconstruction.md`** (نُفِّذ في هذا الإصدار).

---

## 8. Quality Gates Integration

| شرط التسليم | الحالة | الدليل |
|---|---|---|
| توكنز (لا arbitrary) | **مُنفَّذ** | 07:27 · DS Gate |
| نظام الطباعة مُطبَّق | ❌ **غير مُنفَّذ** | لا صندوق DoD |
| خطوط IBM مُحمَّلة | ❌ **غير مُنفَّذ** (أكبر ثغرة غير محروسة) | typography.md يأمر، لا شيء يفحص |
| RTL | **مُنفَّذ** | 07:15,28-29 |
| حالات المكوّنات | **مُنفَّذ** | gate · forbidden #17 |
| Table/Form/Modal كاملة | **مُنفَّذ (مراجعة)** | component-quality-gate §2 |
| الصفحة ليست generic/لها hierarchy | ❌ **stance فقط** | ROLES:28-32، لا صندوق |
| QA report | **مُنفَّذ** | 03:3 · 07:22 |
| README | ⚠️ SPA فقط | 07:53 |
| build check | ⚠️ SPA فقط | 07:48-52 |

→ **ثلاث ثغرات تسليم:** الطباعة/IBM بلا بوّابة · «لا generic» بلا بوّابة · README/static-check لغير SPA. كلها تُسدّ في `delivery-contract.md` + صناديق DoD جديدة + Anti-Generic Gate.

---

## 9. Required Improvements (نُفِّذت — انظر v2.1.0)

| ملف | إجراء |
|---|---|
| `foundations/typography-system.md` | **جديد** — مندوب IBM + `@font-face` + إنفاذ |
| `foundations/token-architecture.md` | **جديد** — توحيد الطبقات الأربع + الفجوات |
| `rules/anti-bland-ui-rules.md` | **جديد** — 8 قواعد قابلة للفحص |
| `rules/quality-gates.md` | **جديد** — البوّابات الأربع موحّدة |
| `default-design-system-standard.md` | **جديد** — عقد «الأساس الإجباري» |
| `delivery-contract.md` | **جديد** — شروط «لا تُسلّم إلا إذا» |
| `reference-driven-reconstruction.md` | **جديد** — pixels → blueprint نظامي |
| `tokens.css` | **تحديث** — +breakpoints +secondary +primary-active@theme · link→brand-700 |
| `rules/qa-checklist.md` · `07-definition-of-done.md` | **تحديث** — صناديق طباعة/IBM/anti-generic |
| `ROLES.md` · `AGENTS.md` | **تحديث** — بوّابة Anti-Generic رابعة |
| `components/{modal,drawer,table,form,site-footer}.md` | **تحديث** — عقد a11y / responsive / submit-lifecycle / إزالة hex |

**مؤجّل موثّق (BACKLOG، P0/P1 للتالي):** sidebar/app-shell spec · data-app header · textarea/radio/switch مستقلة · breakpoints→tokenize sidebar/shell · dark-mode tokens.

---

## 10. الخلاصة في سطر
الأساس متين، والثغرة كانت **الرتابة لا الفوضى** و**طباعة غير محروسة**. هذا الإصدار يضيف قواعد قابلة للفحص تمنع البلادة، ويجعل IBM Plex Sans Arabic إجباريًا بوّابةً، ويرفع المودال/الدرج/الجدول/النموذج، ويضيف عقد إعادة البناء من المرجع — فيصبح الـDefault DS أساسًا إجباريًا يُنتج واجهات احترافية غير generic.
