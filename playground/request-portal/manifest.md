# Page Manifest — بوابة الطلبات (Request Portal · multi-page)

> dogfood v2.3.0 — **تطبيق متعدّد الصفحات** يختبر app-shell. Greenfield/System-First · RTL · neutral. داخل القالب → `playground/`.

- **Mode:** Greenfield / System-First · **Direction:** RTL (ar) · **Theme:** neutral · **Reference:** none

## Intent
بوابة أدمن لإدارة الطلبات الواردة عبر **عدّة صفحات**: لوحة مؤشّرات · قائمة طلبات · تفاصيل طلب + معالجة (موافقة/رفض) · إنشاء طلب. الغرض الأساسي: **اختبار هل sidebar/app-shell + app-header حاجبان** (BACKLOG).

## App Shell (08 · layout §App Shell)
- **Sidebar** (`inline-start`=يمين): لوحة · الطلبات · طلب جديد؛ عنصر نشط `aria-current` + خلفية `--color-primary-subtle`. موبايل = درج عبر زرّ الهيدر.
- **App Header**: عنوان الصفحة (يطابق النشط) + بحث عام + إشعارات (icon ghost + عدّاد) + حساب (avatar). لاصق.
- منطقة المحتوى: max `1536px`، حشو `--space-lg`، تمرير مستقل.

## Component Mapping (من INDEX؛ +المكوّنان الجديدان)
**sidebar** · **app-header** (جديدان v2.3.0) · table · filter-bar (بحث+شرائح) · status-badge · avatar · card (KPI) · detail-view (dl) · form (طلب جديد: input/textarea/select) · modal (تأكيد موافقة/رفض، a11y §6.5+§6.6) · button (primary/secondary/ghost/danger) · empty-state (لا نتائج) · toast (نجاح/خطأ).
- Missing documented first: **sidebar.md + app-header.md** (رُقّيا من BACKLOG لأن الـdogfood أثبت أنهما حاجبان).

## Data States (حيّة)
filled · no-results (فلترة) · success/error toast · معالَج (يُعطّل أزرار الموافقة/الرفض). loading/error للصفحة: خارج نطاق العرض (لا backend).

## Interactions (live JS — vanilla، بلا أداة بناء)
تنقّل sidebar بين 4 صفحات (يحدّث النشط + عنوان الهيدر) · بحث عام في الهيدر يقفز للطلبات · بحث+شرائح فلترة في الطلبات · فتح تفاصيل من صفّ · موافقة/رفض عبر modal (focus-trap/Esc/overlay/return-focus/init-focus≠close) · إرسال طلب جديد (تحقّق العنوان مطلوب + toast + يضيف) · درج موبايل + scrim.

## QA / Gates (الست)
DS (توكنز فقط، صفر arbitrary، صفر inline style خام) · Typography (IBM + سلّم) · Component Quality (حالات + المكوّن الصحيح) · **Visual Polish** (native-control reset · ghost icon buttons · select بسهم مخصّص · لا حدّ ثقيل · sidebar نشط بخلفية+لون لا حدّ) · Anti-Generic (تركيب يتنوّع بنوع الصفحة: لوحة KPI ≠ جدول ≠ تفصيل ≠ نموذج) · Accessibility (nav/header landmarks · aria-current · focus-visible · focus-trap · 44px).

- **Preview runtime:** Shim mirror + JS تفاعلي مضمّن. ليس التنفيذ الإنتاجي.
- **QA Report:** انظر `../../dogfood-request-portal-report.md`.
