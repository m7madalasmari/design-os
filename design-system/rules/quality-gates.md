# البوّابات — Quality Gates (المرجع الموحّد)

> المرجع التفصيلي لكل البوّابات الحاجبة. [ROLES](../../ROLES.md) يصف *إجراء التشغيل*؛ هذا الملف يصف *كل بوّابة*: ماذا تفحص · متى · مالكها · ماذا تحجب. **بوّابة فاشلة تحجب الـpipeline — ليست flag يُوازَن.** القيد: مراجعة موثّقة (يدوية/grep)، لا أداة آلية إلزامية خارج SPA.

## نظرة عامة (التسلسل)
البداية → **DS Gate** (قبل التنفيذ) → بناء → **Component Quality Gate** + **Visual Polish Gate** (لكل مكوّن) → **Anti-Generic Gate** (الصفحة) → QA → **Typography Gate** + **Accessibility Gate** (قبل التسليم) → DoD → تسليم. **(ست بوّابات.)**

---

## 1. Design System Gate — *قبل صحّة التنفيذ*
يفحص: توكنز فقط (صفر arbitrary، **بما فيها inline `style=` الخام** — forbidden #18، لا px/hex/minmax/transform/row-reverse إلا token-var/ديناميكي/fixture موثّق) · كل كتلة مربوطة بـ`INDEX` · أي جديد موثّق أولًا · البراند مطبّق **كـramp كامل متتالٍ** لا تبديل primary (color-system) · المكوّنات تربط بالـsemantic فقط (لا `--brand-*`/`--neutral-*`/hex).
المالك: **Design System**. المرجع: [02](../../design-protocols/02-design-system-ssot.md) · [component-tokens](../foundations/component-tokens.md) · [color-system](../foundations/color-system.md).

## 2. Typography Gate — *قبل التسليم* (جديد v2.1)
يفحص: `--font-family-base` يبدأ بـ**IBM Plex Sans Arabic** (أو ثيم بديل مطلوب صراحةً+موثّق) · الخط **مُحمَّل فعلًا** (fontsource/@font-face) أو fallback معاينة موثّق CSP-only · السلّم مُطبَّق (أحجام من السلّم · أدوار أوزان · جسم عربي 1.7) · **لا Tajawal/Inter/افتراضي متصفّح**.
المالك: **Design System + Content**. المرجع: [typography-system](../foundations/typography-system.md).

## 3. Component Quality Gate — *قبل اعتبار المكوّن منجَزًا*
يفحص: كل مكوّن يحقّق معاييره (حالات · RTL · لا ازدحام · primary واحد · عقد ربط) **و**هو المكوّن الصحيح للمهمة (Modal/Drawer/Page · Table/Card/List).
المالك: **UX & IA + Visual + Design System**. المرجع: [component-quality-gate](component-quality-gate.md).

## 4. Anti-Generic Gate — *قبل التسليم* (جديد v2.1)
يفحص أن الصفحة **ليست رتيبة/generic** عبر قواعد [anti-bland-ui-rules](anti-bland-ui-rules.md) الثماني:
- تسلسل قابل للقياس (≥2 إشارة) · ≥2 علاقتي مسافات · الشبكة تتنوّع بالمحتوى · التركيب يتنوّع بنوع الصفحة · مستويات كثافة مُسمّاة · العمق يعبّر عن التسلسل · صيغة العرض تطابق المحتوى · اختبار «هل تبدو كأي AI UI؟».
المالك: **Visual & Experience + UX & IA**. يرقّي Output stance من موقف إلى بوّابة.

## 5. Accessibility Gate — *قبل قبول التسليم* (أرضية صلبة)
يفحص: WCAG-AA (تباين · كيبورد · تركيز/focus-visible · ARIA · reduced-motion · focus-trap للمودال/الدرج · RTL a11y). لا يُقايَض بالبراند أو المطابقة.
المالك: **Accessibility**. المرجع: [06](../../design-protocols/06-accessibility.md).

## 6. Visual Polish Gate — *لكل مكوّن، مراجعة بصرية للمُخرَج* (جديد v2.2)
يفحص **جودة التنفيذ البصري** على الـpreview المُصيَّر: لا مظهر native/default (أزرار/select/input)، لا حدّ أسود/ثقيل، لا حدّ مزدوج، لا focus دائم، overlay مُوكَّن، close ghost، كثافة جدول متوازنة، حالات/fixtures مصقولة. **«وجود المكوّن ≠ جودته البصرية».**
المالك: **Visual & Experience + Design System**. المرجع: [visual-polish-gate](visual-polish-gate.md) · [component-visual-baseline](../foundations/component-visual-baseline.md). فحص مساعد: غياب native-control reset في أي preview = انحدار.

---

## ترتيب الحَكم عند تعارض بوّابتين
نيّة المستخدم/الـMode → **أرضية الوصول** → SSOT → مطابقة المرجع → الصقل/التمايز. (الـAnti-Generic لا يُقدَّم على الوصول أو الوضوح.) Product & Strategy يكسر التعادل. (مطابق [Precedence في ROLES](../../ROLES.md).)

## العلاقة بالتسليم
لا يُسلَّم عمل وأي بوّابة لم تمرّ. شروط التسليم الكاملة في [delivery-contract](../../delivery-contract.md) وصناديق [07-definition-of-done](../../design-protocols/07-definition-of-done.md).
