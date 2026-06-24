# المعيار الافتراضي الإجباري — Default Design System Standard

> **القرار:** هذا الـDefault Design System هو **الأساس الإجباري** لأي واجهة يولّدها design-os — حتى لو **لم** يقدّم المستخدم ألوانًا أو هوية أو مراجع. لا يبدأ أي بناء من فراغ ولا من ذوق اللحظة؛ يبدأ من هنا.
> هذا الملف هو نقطة الدخول للنظام: يربط الطبقات والبوّابات والقواعد في عقد واحد. للتشغيل: [AGENTS.md](AGENTS.md) → [RUNBOOK.md](RUNBOOK.md) → [ROLES.md](ROLES.md).

## 1. متى يُطبَّق الافتراضي تلقائيًا
- **لا هوية/لون:** يُطبَّق الأساس المحايد (ramp أزرق نائب) + IBM Plex. لا تُختَرع ألوان عشوائية.
- **لون/هوية مُعطاة:** البذرة تدخل [color-system](design-system/foundations/color-system.md) → ramp كامل → النظام كله. لا تبديل primary فقط.
- **مرجع/صورة:** [reference-driven-reconstruction](design-protocols/reference-driven-reconstruction.md) يحوّله لـblueprint نظامي، والافتراضي يسدّ النواقص بلا تشويه.

## 2. ما يضمنه الافتراضي (الإجباري)
| الطبقة | المعيار | المرجع |
|---|---|---|
| **الطباعة** | IBM Plex Sans Arabic (عربي) + IBM Plex Sans (لاتيني)، سلّم متوازن، جسم عربي 1.7 | [typography-system](design-system/foundations/typography-system.md) |
| **اللون** | معمارية 4 طبقات + اشتقاق بذرة→ramp→semantic→مكوّن، بحُرّاس تباين | [token-architecture](design-system/foundations/token-architecture.md) · [color-system](design-system/foundations/color-system.md) |
| **المسافات/الشبكة/الكثافة** | سلّم 4px · شبكة 12 · مستويات كثافة مُسمّاة · breakpoints في SSOT | [spacing](design-system/foundations/spacing.md) · [layout](design-system/foundations/layout.md) |
| **المكوّنات** | 27 spec بحالات/RTL/a11y/عقد ربط؛ المكوّن الصحيح للمهمة | [components/INDEX](design-system/components/INDEX.md) · [component-quality-gate](design-system/rules/component-quality-gate.md) |
| **RTL** | عربي أولًا، أدوات منطقية حصرًا، bidi مُخطَّط | [rtl-guidelines](design-system/foundations/rtl-guidelines.md) |
| **الوصول** | WCAG-AA أرضية صلبة | [06](design-protocols/06-accessibility.md) |
| **ضدّ الرتابة** | 8 قواعد تمنع الـgeneric/الموناتون | [anti-bland-ui-rules](design-system/rules/anti-bland-ui-rules.md) |

## 3. البوّابات الخمس (لا تسليم بدونها)
Design System · Typography · Component Quality · **Anti-Generic** · Accessibility. التفصيل: [quality-gates](design-system/rules/quality-gates.md). شروط التسليم: [delivery-contract](delivery-contract.md).

## 4. الوعد
الأساس الافتراضي وحده — بلا أي إدخال من المستخدم — يُنتج واجهة عربية RTL، احترافية، متّسقة، متاحة، **وغير generic**، جاهزة كنقطة انطلاق صلبة. الهوية والمرجع يرفعانها، لا يصنعانها من الصفر.
