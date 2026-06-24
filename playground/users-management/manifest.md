# Page Manifest — إدارة المستخدمين (Admin) · dogfood v2.1.0

> تشغيل dogfood للبروتوكول v2.1.0. صفحة إدارية/بيانات. لا مرجع بصري → Greenfield/System-First، Pixel QA غير مطبّق. المعاينة: `preview.html`. (داخل القالب → playground/.)

- **Mode:** Greenfield / System-First
- **Direction:** RTL (ar)
- **Theme:** neutral (الافتراضي — لا هوية مُعطاة)
- **Reference:** none

## Intent
إدارة حسابات المستخدمين: بحث/فلترة بالحالة، استعراض جدول، تفاصيل مستخدم، تعديل الحالة، ورسائل نجاح/خطأ.

## Primary Action (one)
**إضافة مستخدم** (primary في الرأس). الإجراء الصفّي «تعديل الحالة» = secondary. (إجراء أساسي واحد لكل سياق.)

## Component Mapping (INDEX — لا مكوّن جديد)
page-header · search-input · filter-bar (شرائح حالة + عقد responsive §11) · table (+caption/scope/aria-sort) · status-badge · **avatar** ([avatar.md](../../design-system/components/avatar.md)، الأحرف الأولى، decorative) · button (primary/secondary) · pagination · empty-state (×4) · **detail-view** ([detail-view.md](../../design-system/components/detail-view.md)، `dl` لا كروت) · modal (عقد a11y §6.5 + ترتيب أزرار §6.6) · select · رسائل success/error.
- Missing component/token documented first: **لا شيء** (v2.1.1: avatar وdetail-view صارا بعقد — لم يعودا ad-hoc).

## Data States (الخمسة)
Loading: skeleton · Empty (أول استخدام): «لا مستخدمين بعد» + دعوة · No-results (بعد فلترة): «لا نتائج» + مسح · Error: `role=alert` + إعادة · Filled: الافتراضي.

## Tokens (semantic فقط، صفر arbitrary)
الأسطح/النص/الحدود المحايدة · الأكسنت `--color-accent` (=brand-600) للإجراء/المحدّد · `--color-secondary` (محايد) لزر «تعديل الحالة» · حالات الشارات الوظيفية · link=`--brand-700` · focus=`--shadow-focus`. استثناءات `style`+قيمة: عروض skeleton + شبكة auto-fit + إزاحات صغيرة (موثّقة أدناه).

## Anti-Bland (Anti-Generic Gate — تطبيق فعلي)
- **presentation-by-content:** قائمة متجانسة→**جدول** · مستخدم واحد→**تخطيط تفصيل** (dl، لا كروت) · إجراء قصير→**modal**. ثلاثة أنماط عرض مختلفة.
- **≥2 علاقتي مسافات:** صفوف جدول كثيفة (`--space-sm`) + فواصل أقسام سخيّة (`--space-2xl`).
- **تسلسل ≥2 إشارة:** h1 (30/bold) + إجراء primary واحد ملوّن؛ بقية الإجراءات secondary محايدة.
- **الشبكة تتنوّع:** filter=flex · table=full-width · detail=dl (9rem/1fr) · states=auto-fit grid. لا شبكة واحدة مكرّرة.

## Accessibility Notes
- Keyboard / focus: كل عنصر تفاعلي `fv:ring`؛ المودال focus-trap + return-focus (عقد modal.md §6.5).
- Contrast: نص/سطح ~14:1 · ثانوي ~5.4:1 · on-accent ≥4.5:1 · شارات الحالة fg/bg ≥4.5:1 · link=brand-700 ~7:1.
- ARIA / semantic HTML: `<table>`+`<caption>`+`scope=col`+`aria-sort`؛ `role=dialog`+`aria-modal`+`aria-labelledby/describedby`؛ `role=group` للفلاتر؛ `role=status`/`alert` للرسائل؛ ✕ بـ`aria-label`.
- Reduced motion: `prefers-reduced-motion` يعطّل skeleton pulse والانتقالات.
- RTL accessibility: أدوات منطقية حصرًا؛ البريد `bdi dir=ltr`؛ المعرّفات tabular معزولة.
- Status: ✅ يجتاز أرضية AA (مراجعة، لا أداة).

## Token Var Exceptions
| Location | القيمة | السبب | utility غير متوفّر؟ |
|---|---|---|---|
| رأس الجدول اللاصق | `--z-sticky` | ترتيب الطبقة | Yes (token-var) |
| تذييل التفصيل | `padding-block-start:var(--space-lg)` | فاصل مجموعة | token-var (مسموح) |
| skeleton/grid (fixture) | `width:%` · `minmax(260px,1fr)` | تخطيط معاينة توضيحي لا توكن له — **fixture موثّق بتعليق** (forbidden #18 يسمح به) | يصير utility في Tailwind الحقيقي |
> **مُزال في v2.1.1 (forbidden #18):** `flex-direction:row-reverse` اليدوي (→ ترتيب أزرار §6.6) و`margin:2px` الخام. صفر inline style خام **غير موثّق**.

## Forbidden (this page) — مُحترَمة
لون/قيمة خارج التوكنز · مكوّن غير موثّق · بيانات PII حقيقية · arbitrary Tailwind · أدوات اتجاهية · أكثر من primary · أعمدة حشو · شارة بلا نص.

## Out of Scope
shell/تنقّل عام (08 — لم يُطلب) · CRUD حيّ · فرز/فلترة/ترقيم تفاعلي · تحميل خط Plex (CSP).

## Post-implementation
- QA per `03`: System + RTL + Accessibility + Visual-Polish. **Pixel QA: N/A (Greenfield).**
- **QA Report Location:** التقرير الكامل في `../../dogfood-v2.1.0-users-page-report.md`.
- **Preview runtime:** Shim mirror (ليس التنفيذ الإنتاجي).
