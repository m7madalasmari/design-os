# بوّابة الصقل البصري — Visual Polish Gate

> **البوّابة السادسة.** تمنع تسليم أي واجهة فيها مكوّنات تبدو **default/native/generic**، أو حدود ثقيلة/سوداء، أو focus ظاهر دائمًا، أو spacing غير ناضج، أو تسلسل بصري ضعيف. تُكمّل [Component Quality Gate](component-quality-gate.md) (التي تفحص *الوجود والاكتمال*) بفحص **جودة التنفيذ البصري**. الأرضية المرجعية: [component-visual-baseline](../foundations/component-visual-baseline.md).
> **سبب وجودها:** dogfood v2.1.0 سلّم صفحة تجتاز a11y/البنية/التوكنز لكن تبدو native (أزرار بحدّ متصفّح، select بسهم افتراضي، input مزدوج الحدّ، close ثقيل). لا بوّابة كانت تلتقط ذلك. **تُفحَص بصريًا على المُخرَج المُصيَّر، لا على النصّ فقط.**

## القاعدة المركزية
> **راجع الـpreview المُصيَّر بصريًا. مكوّن يبدو native/default/generic = البوّابة لا تمرّ — حتى لو اجتاز كل البوّابات الأخرى.**

## 1. Buttons
**يُرفض:** حدّ أسود/ثقيل دائم · مظهر زرّ متصفّح · primary بوزن مبالغ · secondary غير واضح/native · focus ظاهر دائمًا (لا عند التفاعل) · حشو غير متوازن.
**يُطلب:** مبني بالكامل على التوكنز · variants واضحة (primary/secondary/ghost/destructive) · hover/focus-visible/active/disabled · حدّ subtle · **focus ring عند `:focus-visible` فقط** · فجوة أيقونة صحيحة RTL/LTR.

## 2. Inputs / Search
**يُرفض:** input داخل input · حدّ مزدوج · outline دائم · مظهر متصفّح · محاذاة أيقونة سيئة · placeholder رديء · حشو غير متوازن.
**يُطلب:** wrapper واضح · الحقل الداخلي **بلا حدّ مستقلّ** داخل wrapper · `focus-within` ring مؤقّت · أيقونة start/end منطقية · ارتفاع ثابت · خط IBM · حالات default/hover/focus/error/disabled.

## 3. Modal / Dialog
**يُرفض:** close ثقيل بصريًا · overlay خام بلا توكن · أزرار native · footer غير منظّم · حشو عشوائي · عرض غير متوازن · select/input افتراضي داخله.
**يُطلب:** سطح واضح · overlay من `--color-bg-overlay` · **close = icon button ghost subtle** · تسلسل title/description · footer مرتّب قانونيًا ([modal §6.6](../components/modal.md)) · حقول مصقولة · focus-trap + return-focus · responsive.

## 4. Select
**يُرفض:** مظهر select أصلي · سهم غير مضبوط (سهم المتصفّح) · ارتفاع/حشو غير متّسق · حدّ مزدوج · focus غير واضح.
**يُطلب:** مُنسَّق من النظام (`appearance:none`) · trigger واضح · **سهم مخصّص** محاذى `inline-end` · حالات كاملة · RTL.

## 5. Table (جودة بصرية — لا يكفي caption/scope/aria-sort)
**يُفحَص:** نمط الرأس · ارتفاع الصفّ · حشو الخلية · زرّ الإجراء داخل الصفّ (مدمج متّسق) · توازن شارة الحالة · توازن الـavatar · خفّة الحدود · hover · الكثافة · المحاذاة · **ألّا يبدو كـHTML table افتراضي**.

## 6. States / Fixtures (حتى التوضيحية)
**يُرفض:** 4 بطاقات متطابقة بلا صقل · أيقونات ضعيفة/عشوائية · empty/error/loading generic · skeleton بالكاد مرئي · CTA native.
**يُطلب:** بطاقات حالات مصقولة · تسلسل واضح · معالجة أيقونات tokenized · إجراءات متّسقة · **لا تبدو debug demo**.

## الإنفاذ
- **متى:** مراجعة بصرية للمُخرَج المُصيَّر قبل التسليم (بعد البناء، ضمن مرور الأدوار — Visual & Experience يملكها مع Design System).
- **الفشل يحجب:** أي بند أعلاه = **بوّابة لا تمرّ**، والعمل غير منجَز.
- **فحص ثابت مساعد:** أي preview/shim يستخدم `<button>/<select>/<input>` **يجب** أن يحوي كتلة native-control reset (`appearance:none`) — grep لغيابها يلتقط الانحدار. (لا يُغني عن المراجعة البصرية.)
- مرجع المخالفات: [forbidden-patterns](forbidden-patterns.md) #19–#25.
