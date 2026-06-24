# عقد التسليم — Delivery Contract

> **لا يُسلَّم أي مشروع/صفحة** ما لم تتحقّق كل الشروط أدناه. هذا يجعل البوّابات ([quality-gates](design-system/rules/quality-gates.md)) و[Definition of Done](design-protocols/07-definition-of-done.md) شرطًا تسليميًا لا أمنية. يُكمّل [OUTPUT.md](OUTPUT.md) (شكل التسليم).

## شروط الحجب (كلها إلزامية)

| # | الشرط | مرجع | الحالة قبل v2.1 |
|---|---|---|---|
| 1 | **توكنز فقط** — صفر قيم arbitrary، كل قيمة من النظام | DS Gate · 07:27 | كان مُنفَّذًا |
| 2 | **نظام الطباعة مُطبَّق** — السلّم + أدوار الأوزان + جسم عربي 1.7 | Typography Gate | **أُضيف** |
| 3 | **خطوط IBM** — IBM Plex Sans Arabic مُحمَّل ومُطبَّق (أو fallback معاينة موثّق) | Typography Gate · [typography-system](design-system/foundations/typography-system.md) | **أُضيف (أكبر ثغرة سابقة)** |
| 4 | **RTL مُطبَّق** — أدوات منطقية، bidi، لا اتجاهي | 07:15,28-29 | كان مُنفَّذًا |
| 5 | **حالات المكوّنات** — empty/loading/error/no-results + تفاعل، حيث ينطبق | Component Quality Gate | كان مُنفَّذًا |
| 6 | **Table/Form/Modal كاملة** — معايير القبول الخاصّة بكلٍّ | [component-quality-gate](design-system/rules/component-quality-gate.md) | كان مُنفَّذًا |
| 7 | **الصفحة ليست generic / لها تسلسل** — تمرّ Anti-Generic Gate (anti-bland 1–8) | [anti-bland-ui-rules](design-system/rules/anti-bland-ui-rules.md) | **أُضيف (كان stance فقط)** |
| 8 | **تقرير QA** موجود (مضمّن أو ملف) + Preview runtime مُعلَن | 03:3 · 07:22 | كان مُنفَّذًا |
| 9 | **README** لأي تسليم لإنسان (لا SPA فقط) | (وُسّع) | كان SPA فقط |
| 10 | **فحص ثابت مُسجَّل** — grep لـarbitrary + أدوات RTL اتجاهية، يُشغَّل وتُسجَّل نتيجته | 07:35 | **أُضيف (دليل لا ادّعاء)** |
| 11 | **build check** (SPA) — dev/build/lint/typecheck/test | 07:48-52 / `09` | كان SPA فقط |

## القاعدة
أي شرط غير محقّق → **العمل في تقدّم، لا منجَز**. يُذكَر الشرط الناقص وسببه في التسليم ([OUTPUT.md](OUTPUT.md)) — ولا يُقدَّم عمل جزئي على أنه مكتمل.

## بطاقة تسليم سريعة (انسخها في OUTPUT)
```
Delivery gate check:
[ ] tokens-only   [ ] typography system   [ ] IBM Plex loaded
[ ] RTL           [ ] component states     [ ] table/form/modal complete
[ ] anti-generic  [ ] QA report+runtime    [ ] README
[ ] static grep pass (arbitrary / directional) — result: ____
[ ] (SPA) build/lint/typecheck/test
```
