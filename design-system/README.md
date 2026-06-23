# نظام التصميم — Design System (RTL-first)

> هذا المجلد هو **مصدر الحقيقة الوحيد (SSOT)** لكل قرار تصميمي في المشروع.
> أي مكوّن أو صفحة أو شاشة تُبنى لاحقًا **يجب** أن تستمد قيمها من هنا، ولا تُنشئ قيمًا من خارجه.

---

## القاعدة الأولى قبل أي شيء

> **ممنوع** كتابة أي قيمة لون أو مسافة أو حجم خط أو زاوية أو ظل **يدويًا** في أي مكوّن أو صفحة.
> كل قيمة تأتي من توكن مُوثَّق في [`foundations/tokens.md`](foundations/tokens.md). إن لم يوجد التوكن، يُضاف هنا أولًا مع توثيق سببه — ثم يُستخدم.

---

## كيف يُقرأ هذا النظام

الترتيب مقصود — اقرأ من الأعلى للأسفل عند أول تعرّف على النظام:

### 1. الأسس — `/foundations`
الطبقة التي يُبنى عليها كل شيء. لا قرار بصري خارجها.

| الملف | يجيب عن |
|---|---|
| [design-principles.md](foundations/design-principles.md) | لماذا نصمّم بهذه الطريقة — المبادئ الحاكمة التي تُحسم بها أي خلافات لاحقة |
| [brand-foundation.md](foundations/brand-foundation.md) | كيف تعمل طبقة الثيم المحايد، وكيف تُحقن هوية علامة فعلية فوقها |
| [tokens.md](foundations/tokens.md) | **القاموس** — كل لون/مسافة/زاوية/ظل/حركة كتوكن دلالي. المرجع الأول لأي قيمة |
| [typography.md](foundations/typography.md) | الخط، السلّم الطباعي، الأوزان، ارتفاع السطر، معالجة الأرقام |
| [spacing.md](foundations/spacing.md) | شبكة 4px، سلّم المسافات، متى تُستخدم كل خطوة |
| [layout.md](foundations/layout.md) | الشبكة، نقاط الكسر، هيكل التطبيق (app shell)، عرض المحتوى |
| [rtl-guidelines.md](foundations/rtl-guidelines.md) | قواعد العربية أولًا — الخصائص المنطقية، الانعكاس، ثنائية الاتجاه (bidi) |
| [ux-writing.md](foundations/ux-writing.md) | نبرة الكتابة، صياغة الأزرار والأخطاء والحالات الفارغة، المصطلحات |

### 2. المكوّنات — `/components`
مكتبة المكوّنات المعتمدة (19 مكوّنًا). **لا يُستخدم أي مكوّن غير موجود هنا.** الجرد الكامل مع الحالات/Tailwind في [components/INDEX.md](components/INDEX.md).

**حقول وأفعال:** [button](components/button.md) · [input](components/input.md) · [select](components/select.md) · [checkbox](components/checkbox.md)
**حاويات وعناوين:** [card](components/card.md) · [page-header](components/page-header.md) · [section-header](components/section-header.md)
**بيانات:** [table](components/table.md) · [empty-state](components/empty-state.md) · [filter-bar](components/filter-bar.md) · [status-badge](components/status-badge.md) · [pagination](components/pagination.md)
**تغذية راجعة وتحميل:** [spinner](components/spinner.md) · [skeleton](components/skeleton.md) · [alert](components/alert.md)
**طبقات وتنقّل:** [modal](components/modal.md) · [drawer](components/drawer.md) · [toast](components/toast.md) · [tabs](components/tabs.md)

> [form.md](components/form.md) = طبقة **تركيب** الحقول في نموذج (تخطيط/توقيت تحقّق/موضع الأزرار)، لا مكوّنًا ذرّيًا.

كل ملف مكوّن يلتزم بالقالب نفسه (9 أقسام): متى يُستخدم · متى لا · الحالات · المقاسات · قواعد النصوص · قواعد RTL · أمثلة صحيحة · أمثلة خاطئة · علاقته بالتوكنز.

### 3. القواعد — `/rules`
كيف يُستخدم النظام عمليًا، وما الذي يُرفض.

| الملف | الغرض |
|---|---|
| [ai-design-rules.md](rules/ai-design-rules.md) | قواعد إلزامية لأي مساعد ذكي أو إنسان يولّد واجهة من هذا النظام |
| [page-composition-rules.md](rules/page-composition-rules.md) | كيف تُركّب صفحة: التسلسل المعلوماتي، الإجراء الأساسي الواحد، الكثافة |
| [qa-checklist.md](rules/qa-checklist.md) | قائمة فحص قبل اعتماد أي شاشة |
| [forbidden-patterns.md](rules/forbidden-patterns.md) | **الممنوعات** صراحةً، وسبب المنع، والبديل الصحيح |

---

## نموذج العمل (workflow) لأي تصميم لاحق

1. اقرأ [design-principles.md](foundations/design-principles.md) و [page-composition-rules.md](rules/page-composition-rules.md).
2. ركّب الصفحة من مكوّنات `/components` الموجودة فقط.
3. استمد كل قيمة من [tokens.md](foundations/tokens.md).
4. طبّق [rtl-guidelines.md](foundations/rtl-guidelines.md) من البداية، لا كإصلاح لاحق.
5. مرّر العمل على [qa-checklist.md](rules/qa-checklist.md) و [forbidden-patterns.md](rules/forbidden-patterns.md) قبل الاعتماد.

---

## نوع المنتج المفترض

هذا النظام مُعدّ لـ **تطبيق بيانات / لوحة تحكّم إدارية** (وجود جدول، فلاتر، درج جانبي، نماذج يدل على ذلك)، لا لموقع تسويقي. القرارات (الكثافة، هدوء الظلال، الأرقام الجدولية) مبنية على هذا الافتراض. إن تغيّر نوع المنتج، تُراجَع القرارات المعلّمة بـ «لأن المنتج تطبيق بيانات».

## الإصدار

- **v0.1** — الأساس المحايد القابل للثيم. لم تُعتمد بعدُ هوية علامة فعلية.
- أي تغيير في توكن دلالي = تغيير كاسر (breaking) يُوثَّق هنا.
