# توكنز المكوّنات — Component Token Bindings (الطبقة الثالثة)

> **القرار:** الطبقة الثالثة في المعمارية ليست متغيّرات CSS جديدة لكل مكوّن، بل **عقد ربط موثّق**: كل جزء/حالة في المكوّن مربوط بتوكن **دلالي** محدّد.
> **السبب:** النظام Tailwind-first — المكوّنات كلاسات utility مربوطة بالدلالي. سكّ مئات متغيّرات `--button-primary-bg` يصطدم بهذا النموذج ويضخّم الصيانة. عقد الربط يعطي **نفس الفائدة** (التتبّع + التتالي المتوقّع) بلا انفجار توكنز.
> يُكمّل [brand-foundation](brand-foundation.md) (الطبقات) و[color-system](color-system.md) (اشتقاق الدلالي) و[tokens.css](../tokens.css) (المصدر التنفيذي).

---

## 1. القاعدة الحاكمة

**المكوّنات تربط بالطبقة الدلالية فقط. ممنوع** أن يلمس مكوّن: قيمة hex خام · درجة ramp مباشرة (`--brand-600`) · `--neutral-*`. الربط دائمًا عبر اسم دلالي (`--color-primary`, `--color-bg-surface`, `--color-border-default`…).

**لماذا هذا هو «التير الثالث» صحيحًا:** لأن الدلالي يشتقّ من الـbrand ramp ([color-system](color-system.md))، فإن ربط المكوّن بالدلالي يجعل **تغيير البذرة يتتالى تلقائيًا** إلى المكوّن — دون لمسه ودون توكن مكوّن منفصل. عقد الربط = الطبقة الثالثة.

## 2. الصيغة القياسية (قسم في كل spec)

كل ملف مكوّن يحمل قسم **«علاقته بالتوكنز / Token Bindings»** بهذا الشكل: *جزء/حالة → توكن دلالي*. هذا القسم **إلزامي** (تفحصه [بوّابة جودة المكوّن](../rules/component-quality-gate.md)).

مثال (button):
| الجزء / الحالة | التوكن الدلالي |
|---|---|
| primary · تعبئة | `--color-primary` |
| primary · hover | `--color-primary-hover` |
| primary · نصّ | `--color-primary-foreground` |
| secondary · حدّ/سطح | `--color-border-default` + `--color-bg-surface` |
| focus-visible | `--shadow-focus` + `--color-focus-ring` |
| disabled | `--color-bg-disabled` + `--color-text-disabled` |

## 3. الفهرس الموحّد (المكوّنات الأساسية → الدلالي)

مرجع سريع؛ التفصيل في §9 «علاقته بالتوكنز» داخل كل spec.

| المكوّن | الأجزاء الرئيسة → الدلالي |
|---|---|
| **button** | تعبئة `--color-primary`/`-hover`/`-active` · نصّ `--color-primary-foreground` · حدّ `--color-border-default` · تركيز `--shadow-focus`/`--color-focus-ring` · danger `--color-destructive` |
| **input / field** | حدّ `--color-border-default` · hover `--color-border-strong` · تركيز `--color-border-focus`+`--shadow-focus` · خطأ `--color-destructive-border`+`--color-destructive` · معطّل `--color-bg-disabled`/`--color-text-disabled` |
| **table** | سطح `--color-bg-surface` · رأس `--color-bg-subtle` · فاصل `--color-border-subtle` · صفّ hover `--color-bg-hover` · صفّ محدّد `--color-primary-subtle` |
| **card** | سطح `--color-bg-surface` · حدّ `--color-border-subtle` · ظلّ `--shadow-sm` |
| **modal / drawer** | خلفية معتمة `--color-overlay` · لوح `--color-bg-surface` · ظلّ `--shadow-lg` · طبقات `--z-overlay`/`--z-modal` |
| **status-badge** | success/warning/danger/info × `fg`+`soft` (`--color-success-*`…) — **لا تتبع البراند** |
| **link** | `--color-link` (محقَّق التباين، مفصول عن accent) |
| **nav / app-shell** | سطح `--color-bg-surface`/`-subtle` · حدّ `--color-border-subtle` · عنصر نشط `--color-primary`/`--color-primary-subtle` |
| **tabs** | تبويب نشط `--color-primary` (نصّ/مؤشّر سفلي) · خامل `--color-text-secondary` · فاصل `--color-border-subtle` |
| **alert** | حسب النوع: `--color-{success,warning,destructive,info}` (fg) + `-soft` (خلفية) + `-border` |
| **toast** | سطح `--color-bg-surface` · ظلّ `--shadow-md` · طبقة `--z-toast` · لون النوع كـalert |
| **form** | حقول→ربط input · تسمية `--color-text-primary` · مساعدة `--color-text-tertiary` · خطأ `--color-destructive` · أساسي→ربط button · ثانوي `--color-secondary` |
| **secondary button / chip** | تعبئة `--color-secondary` · hover `--color-secondary-hover` · نصّ `--color-secondary-foreground` (محايد، لا براند) |

## 4. ما لا يُربط بالبراند (وظيفي ثابت)

`status-badge`، رسائل الخطأ/النجاح، المقياس الرمادي للأسطح/النصوص/الحدود — تربط بتوكنز **وظيفية** (status + neutral) لا بالبراند. تغيير العلامة لا يغيّرها (انظر [color-system §4](color-system.md)).

## 5. الإنفاذ

- كل spec يجب أن يحمل قسم Token Bindings (§9). مكوّن بلا عقد ربط واضح = **بوّابة الجودة لا تمرّ**.
- أي قيمة في مكوّن لا تعود لتوكن دلالي = مخالفة (تُلتقط في **بوّابة Design System**).
- مكوّن يلمس `--brand-*` أو `--neutral-*` أو hex مباشرة = مخالفة الطبقات (هذا الملف §1).
