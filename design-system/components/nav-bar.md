# شريط التنقّل — Nav Bar

> القيم من [tokens.md](../foundations/tokens.md). مكوّن تسويقي/موقعي (أُضيف لتغطية الصفحات التسويقية، لا تطبيقات البيانات التي تستخدم [app shell](../foundations/layout.md)).

## 1. متى يُستخدم
أعلى صفحة تسويقية/موقعية: شعار + روابط أقسام + إجراء أساسي واحد (CTA).

## 2. متى لا يُستخدم
- داخل تطبيق بيانات → استخدم [app shell](../foundations/layout.md) (شريط جانبي + علوي).
- لأكثر من ‎~6‎ روابط (يُختصر في قائمة على الجوال).
- لأكثر من زر `primary` واحد.

## 3. الحالات
`default` · `sticky` (يلتصق عند التمرير، `--z-sticky`) · `scrolled` (خلفية/حدّ يظهران بعد التمرير) · `mobile` (الروابط تُطوى خلف زر قائمة) · رابط `hover`/`active`/`focus-visible`.

## 4. المقاسات
- ارتفاع ‎~`--size-control-lg`‎ + حشو رأسي `--space-md`؛ حشو أفقي = حشو الحاوية.
- الروابط `--font-size-sm`/`-md` `--color-text-secondary`، النشط `--color-text-primary`.
- الشعار `--font-size-lg` `--font-weight-bold`. CTA = [button](button.md) `primary`.

## 5. قواعد النصوص
- روابط بأسماء أقسام موجزة (اسم لا جملة).
- CTA بفعل: «Stake Now»/«ابدأ».

## 6. قواعد RTL
- الشعار في `inline-start`، الروابط وسطًا/تتبع، الـCTA في `inline-end` — بخصائص منطقية.
- في LTR ينعكس تلقائيًا (المكوّن لا يفترض اتجاهًا).

## 7. أمثلة صحيحة
- شعار + 5 روابط + زر CTA واحد بارز.
- لاصق مع ظهور حدّ خفيف بعد التمرير.

## 8. أمثلة خاطئة
- زرّان CTA متنافسان (forbidden #14).
- روابط بلون tertiary (دون AA).
- استخدامه داخل لوحة تطبيق بيانات.

## 9. علاقته بالتوكنز
- النصّ: `--color-text-secondary`/`-primary`. الخلفية: `--color-bg-base`/`-surface` + `--color-border-subtle` (عند التمرير).
- القياس: `--size-control-lg` · `--space-md` · `--z-sticky`. الـCTA: توكنز [button](button.md).
