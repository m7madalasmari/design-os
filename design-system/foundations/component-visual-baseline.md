# الأساس البصري للمكوّنات — Component Visual Baseline

> **القرار:** لكل مكوّن **أرضية تنفيذ بصري** لا يُقبل دونها — لأن «وجود المكوّن ≠ جودته البصرية». ظهر في dogfood v2.1.0: مكوّنات صحيحة بنيويًا وa11y لكن تبدو native/default (حدود ثقيلة، select بسهم متصفّح، input مزدوج الحدّ). القواعد كانت متناثرة في specs المكوّنات لكن **لا بوّابة تفرضها على المُخرَج** — هذا الملف هو الأرضية، و[visual-polish-gate](../rules/visual-polish-gate.md) يفرضها.

## 0. القاعدة الأمّ: لا مظهر تحكّم أصلي (native control reset) — إلزامي
أي عنصر تحكّم أصلي (`<button>` · `<select>` · `<input>` · `<textarea>`) **يجب إعادة ضبط مظهره** قبل أي تنسيق:
```css
button,select,input,textarea{ appearance:none; -webkit-appearance:none;
  font:inherit; color:inherit; background:none; border:0; margin:0; }
button{ cursor:pointer; }
/* أخفِ زينة input[type=search] الأصلية */
input[type="search"]::-webkit-search-decoration,
input[type="search"]::-webkit-search-cancel-button{ -webkit-appearance:none; display:none; }
```
ثم يُبنى المظهر **بالكامل من التوكنز/utilities**. **بلا هذا الـreset، لا يمرّ المكوّن** (forbidden #20). في React/Tailwind الحقيقي: preflight + الكلاسات الدلالية تؤدّيه؛ في أي shim/preview **يجب تضمين الـreset صراحةً**.

## 1. الحدود (Borders)
- **خفيفة بمعنى:** `--color-border-subtle`/`-default` فقط. **ممنوع** حدّ أسود/ثقيل أو `border: …px solid black` (forbidden #19, #24).
- **لا حدود مزدوجة:** عنصر داخل wrapper ذي حدّ **لا يحمل حدًّا مستقلًّا** (مثل input داخل search wrapper) (forbidden #21).
- الحدّ يُستخدم للفصل/التسلسل لا للزينة؛ التعشيش حدّ واحد ([anti-bland §6](../rules/anti-bland-ui-rules.md)).

## 2. التركيز (Focus)
- حلقة التركيز **عند `:focus-visible` فقط** عبر `--shadow-focus` — **ليست ظاهرة دائمًا** ولا outline المتصفّح الأزرق (forbidden #15, #22).
- `outline:none` مسموح **فقط** مع بديل `--shadow-focus` ظاهر.

## 3. الأسطح والطبقات (Surfaces / overlays)
- overlay المودال/الدرج من توكن `--color-bg-overlay` (forbidden #23) — لا `rgba()` خام.
- السطح المرفوع بظلّ من التوكنز (`--shadow-md/lg`)؛ العمق يعبّر عن التسلسل لا الزينة.

## 4. الأيقونات (Icon weight)
- من [icon-system](icon-system.md)، `stroke-width` 1.5–1.6، `currentColor`، حجم من `--size-icon-*`.
- لا أيقونة ثقيلة/سوداء فجّة؛ أيقونات الأزرار الثانوية/الإغلاق بلون نصّ ثانوي لا أساسي صارخ.

## 5. الأزرار (Buttons) — أرضية
primary (تعبئة accent، بلا حدّ) · secondary (سطح + حدّ subtle) · ghost (شفّاف بلا حدّ) · destructive. وزن بصري متدرّج (primary > secondary > ghost). حشو متوازن من السلّم. حالات كاملة (hover/focus-visible/active/disabled). أيقونة `inline-start` بفجوة `--space-2xs`.

## 6. الحقول/البحث (Inputs / Search)
wrapper واضح بحدّ subtle؛ الحقل الداخلي **بلا حدّ** (القاعدة #1)؛ حلقة `focus-within` مؤقّتة؛ أيقونة start/end منطقية؛ ارتفاع ثابت `--size-control-md`؛ خط IBM؛ placeholder بلون tertiary لا أفتح.

## 7. القوائم (Select) — أرضية
`appearance:none` (القاعدة #0)؛ **سهم مخصّص** (chevron من icon-system) في `inline-end`، لا سهم المتصفّح؛ ارتفاع/حشو = الحقول؛ حدّ subtle واحد؛ تركيز مؤقّت؛ RTL.

## 8. الكثافة والنضج (Spacing maturity)
حشو/فجوات من السلّم؛ ارتفاع صفوف الجدول مريح لا مزدحم؛ توازن بصري للشارة/الـavatar في الصفّ؛ لا تظليل صاخب؛ تسلسل واضح. **لا يبدو كـHTML table/form افتراضي** ([anti-bland §1،7](../rules/anti-bland-ui-rules.md)).

## 9. الحالات والفكسچرات (States) — حتى التوضيحية
حالات empty/loading/error/no-results **مصقولة**: أيقونة tokenized داخل دائرة، عنوان heading، نصّ ثانوي، CTA بـvariant صحيح (لا native). skeleton مرئي بوضوح (`--color-bg-subtle`+ نبض، عرض متدرّج). **لا تبدو كـdebug demo** (forbidden #25).

---
**العلاقة:** هذه الأرضية تُفحَص في [visual-polish-gate](../rules/visual-polish-gate.md) (البوّابة السادسة)؛ مخالفاتها في [forbidden-patterns](../rules/forbidden-patterns.md) #19–#25؛ وكل قيمة من [tokens](tokens.md) عبر [component-tokens](component-tokens.md).
