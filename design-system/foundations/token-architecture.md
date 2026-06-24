# معمارية التوكنز — Token Architecture (المرجع الموحّد)

> مرجع واحد يربط طبقات التوكنز. التفاصيل في: [color-system](color-system.md) (الاشتقاق) · [component-tokens](component-tokens.md) (عقود الربط) · [brand-foundation](brand-foundation.md) (الثيم) · [tokens.css](../tokens.css) (المصدر التنفيذي) · [tokens.md](tokens.md) (القاموس).

## الطبقات (من الخام للمكوّن)

```
①  Primitive        قيم خام محايدة + سلالم
       ↓
①ب Brand Ramp       --brand-50…950  (مشتقّ من بذرة — color-system §3)
       ↓ يُسنَد
②  Semantic         توكنز بالمعنى (background, foreground, primary, secondary, success…, focus-ring)
       ↓ يستهلكها (عقد ربط)
③  Component         كل جزء/حالة → توكن دلالي. لا يلمس ① أبدًا.
```

**القاعدة الذهبية:** المكوّن يربط بالطبقة ② فقط. ممنوع لمس hex خام، `--brand-*`، `--neutral-*` مباشرة. (تفصيل: [component-tokens §1](component-tokens.md).)

## ① Primitive (tokens.css)
- ألوان خام: neutral `1…12` (Radix-style) · status fg/bg/border ×4 (green/amber/red/blue) · **brand `50…950`** (تير الـramp).
- سلالم خام: font-size `xs…4xl` · spacing `0…4xl` (4px) · radius · shadow · border-width · duration · ease · z-index · sizing.
- **breakpoints** `sm…2xl` (في `@theme`، SSOT — أُضيفت v2.1).

## ② Semantic — الجرد المعتمد
- **أسطح:** background · card(surface) · popover · muted(surface-muted) · hover · overlay · disabled.
- **نص:** foreground · muted-foreground · faint-foreground(tertiary — زخرفي/كبير فقط) · on-accent.
- **حدود:** border(default) · border-subtle · border-strong · border-focus · input.
- **الفعل:** primary · primary-hover · **primary-active** · primary-subtle · primary-foreground.
- **الثانوي:** **secondary · secondary-hover · secondary-foreground** (مشتقّ من **المحايد** لا البراند — حفاظًا على 60-30-10؛ أُضيف v2.1).
- **الحالات:** success/warning/danger(destructive)/info × (fg + soft + border) — **وظيفية، لا تتبع البراند**.
- **التفاعل:** link (=brand-700، محقَّق التباين) · focus-ring (=brand-600، مفصول، ≥3:1).

> **ملاحظة معمارية:** `accent` ليس توكنًا ثانويًا منفصلًا — هو نفسه لون الفعل (primary = alias لـaccent). «الثانوي» الآن له توكن مُسمّى محايد (secondary). إن احتاج مشروع accent تزييني ثانٍ، يُضاف بقرار موثّق (نادر في تطبيق بيانات).

## ③ Component — عقود الربط
كل spec يحمل قسم «علاقته بالتوكنز» = عقد الربط (جزء/حالة → دلالي). الفهرس الموحّد في [component-tokens §3](component-tokens.md). مكوّن بلا عقد = **بوّابة الجودة لا تمرّ**.

## التتالي (الضمان)
بذرة واحدة → `--brand-*` → ② → ③. تبديل البذرة (ثيم) يحدّث **كل النظام** بلا لمس أي مكوّن (مثبت في [color-system §7](color-system.md)). الرمادي والحالات لا تتغيّر (وظيفية). **هذا ما يجعل «غيّر لونًا → ينعكس على النظام كامل» حقيقةً لا وعدًا.**

## ما يتغيّر مع البراند مقابل ما يثبت
| يتغيّر (ثيم) | يثبت (نظام) |
|---|---|
| `--brand-50…950` ومشتقّاتها (primary/link/focus/subtle) · الخط · `--radius-md` | المقياس الرمادي · secondary المحايد · ألوان الحالات · السلالم · breakpoints |
