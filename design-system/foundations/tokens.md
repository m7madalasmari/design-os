# التوكنز — Design Tokens (المرجع الأول لأي قيمة)

> هذا القاموس هو **مصدر الحقيقة الوحيد للقيم**. أي لون/مسافة/زاوية/ظل/مدّة في أي مكوّن أو صفحة يأتي من هنا.
> الصيغة CSS Custom Properties. الأسماء ثابتة؛ القيم وراء `--color-accent` و`--font-family-base` فقط هي القابلة للثيم (انظر [brand-foundation](brand-foundation.md)).

**قاعدة لا استثناء لها:** لا يُكتب لون hex أو px في مكوّن. إن احتجت قيمة غير موجودة، أضِفها هنا أولًا مع سببها.

---

## 1. الألوان — Primitives (الطبقة 1: محايدة، لا تُستهلك مباشرة)

مقياس رمادي من 12 خطوة على نمط Radix. **السبب في 12 خطوة:** يغطي الأدوار الوظيفية كلها (خلفيات/سطوح/حدود/نص) بفواصل تباين كافية دون فجوات، فلا يحتاج المصمم لخطوات وسيطة مرتجلة. الخطوات 1–2 خلفيات، 3–5 سطوح وعناصر، 6–8 حدود، 9–10 لون صلب/نص خافت، 11–12 نص.

```css
:root {
  --neutral-1:  #FCFCFD;  /* خلفية التطبيق */
  --neutral-2:  #F9F9FB;  /* خلفية فرعية */
  --neutral-3:  #F0F0F3;  /* سطح خفيف، تمرير */
  --neutral-4:  #E8E8EC;  /* سطح، تعطيل */
  --neutral-5:  #E0E0E6;  /* حدود عناصر */
  --neutral-6:  #D8D8DF;  /* حدود */
  --neutral-7:  #CECED6;  /* حدود قوية، فاصل */
  --neutral-8:  #B9B9C3;  /* حدود تفاعلية، مؤشر */
  --neutral-9:  #8B8B96;  /* نص خافت، أيقونة ثانوية */
  --neutral-10: #6E6E79;  /* نص ثانوي */
  --neutral-11: #50505B;  /* نص ثانوي قوي */
  --neutral-12: #1C1C24;  /* نص أساسي */
}
```

> الأرقام الخام أعلاه **محايدة وثابتة** (قرار نظام، غير قابلة للثيم). لا تُستهلك في المكوّنات — تُستهلك عبر الدلالي أدناه.

ألوان الحالات (وظيفية، ثابتة، غير تجارية). لكلٍّ ثلاث أدوار: `-fg` (نص/أيقونة)، `-bg` (خلفية خفيفة)، `-border`. القيم مختارة لتحقق التباين المطلوب فوق `--neutral-1`:

```css
:root {
  --green-fg:    #1A7F4B;  --green-bg:   #E7F6EE;  --green-border:  #A6E0C0;  /* نجاح */
  --amber-fg:    #9A6700;  --amber-bg:   #FCF3E2;  --amber-border:  #ECCB8A;  /* تحذير */
  --red-fg:      #C12A2A;  --red-bg:     #FCEDED;  --red-border:    #F0B5B5;  /* خطأ/خطر */
  --blue-fg:     #15609E;  --blue-bg:    #E9F2FB;  --blue-border:   #ABCFF0;  /* معلومة */
}
```

اللون المميِّز (الطبقة 1 منه قابلة للثيم — نائب الآن، انظر [brand-foundation](brand-foundation.md)):

```css
:root {
  --accent-solid:   #3B5BDB;  /* نائب — يُستبدل عند اعتماد علامة */
  --accent-hover:   #3450C4;
  --accent-active:  #2C44A8;
  --accent-tint:    #ECF0FD;
  --on-accent:      #FFFFFF;
}
```

---

## 2. الألوان — Semantic (الطبقة 2: تُستهلك في المكوّنات)

**هذه فقط** هي ما تستخدمه المكوّنات والصفحات. الاسم يصف الدور لا اللون.

```css
:root {
  /* الأسطح والخلفيات */
  --color-bg-base:      var(--neutral-1);   /* خلفية الصفحة */
  --color-bg-subtle:    var(--neutral-2);   /* مناطق مُجمَّعة، رؤوس */
  --color-bg-surface:   #FFFFFF;            /* الكروت، النماذج، الجداول */
  --color-bg-raised:    #FFFFFF;            /* قوائم منسدلة، popover (مع ظل) */
  --color-bg-hover:     var(--neutral-3);   /* تمرير على صف/عنصر */
  --color-bg-active:    var(--neutral-4);   /* عنصر محدد/مضغوط */
  --color-bg-overlay:   rgba(28,28,36,0.45);/* خلفية المودال */
  --color-bg-disabled:  var(--neutral-3);

  /* النص */
  --color-text-primary:   var(--neutral-12);
  --color-text-secondary: var(--neutral-10);
  --color-text-tertiary:  var(--neutral-9);  /* تلميحات/أيقونات خافتة أو نصّ كبير فقط — تباينه ≈3.4:1 دون AA للنصّ العادي؛ ممنوع لنصّ تفاعلي/أساسي */
  --color-text-disabled:  var(--neutral-8);
  --color-text-on-accent: var(--on-accent);
  --color-text-link:      var(--accent-solid);

  /* الحدود */
  --color-border-subtle:  var(--neutral-5);  /* فواصل خفيفة */
  --color-border-default: var(--neutral-6);  /* حدود الحقول والكروت */
  --color-border-strong:  var(--neutral-8);  /* حدود تفاعلية، تمرير */
  --color-border-focus:   var(--color-focus-ring);  /* مفصول عن accent (v1.1) */

  /* المميِّز (للأفعال فقط) */
  --color-accent:         var(--accent-solid);
  --color-accent-hover:   var(--accent-hover);
  --color-accent-active:  var(--accent-active);
  --color-accent-subtle:  var(--accent-tint);
  --color-text-accent:    var(--accent-solid);

  /* الحالات */
  --color-success-fg: var(--green-fg);  --color-success-bg: var(--green-bg);  --color-success-border: var(--green-border);
  --color-warning-fg: var(--amber-fg);  --color-warning-bg: var(--amber-bg);  --color-warning-border: var(--amber-border);
  --color-danger-fg:  var(--red-fg);    --color-danger-bg:  var(--red-bg);    --color-danger-border:  var(--red-border);
  --color-info-fg:    var(--blue-fg);   --color-info-bg:    var(--blue-bg);   --color-info-border:    var(--blue-border);

  /* حلقة التركيز */
  --color-focus-ring: var(--accent-solid);
}
```

**أزواج التباين المضمونة (WCAG AA):** `text-primary/bg-surface` ≈ 14:1، `text-secondary/bg-surface` ≈ 5.4:1، `text-on-accent/accent` ≥ 4.5:1 (شرط على أي ثيم). كل لون `-fg` فوق `-bg` نظيره يحقق ≥ 4.5:1.
**تحذير:** `text-tertiary/bg-surface` ≈ 3.4:1 — **دون AA للنصّ العادي**؛ يُقتصر على التلميحات/الأيقونات/النصّ الكبير، ولا يُستخدم لنصّ تفاعلي أو أساسي.

**فصل link/focus عن accent (v1.1، إلزامي):** `--color-text-link` و`--color-focus-ring` توكنان **مستقلّان** — لا يُربطان مباشرة بـ`--color-accent`. accent قد يكون تعبيريًا/فاتحًا، أمّا الرابط وحلقة التركيز فيجب أن يحقّقا التباين (رابط ≥4.5:1، حلقة ≥3:1). `--shadow-focus` و`--color-border-focus` يستهلكان `--color-focus-ring`. **Do not map focus ring or text link directly to accent unless contrast is verified** — في الثيمات ذات accent الفاتح اضبطهما على تنويعة داكنة. (المصدر التنفيذي: [`tokens.css`](../tokens.css).)

---

## 3. المسافات — Spacing (أساس 4px)

**السبب في أساس 4px:** أصغر وحدة ذات معنى عند كثافة 1x، وتقسم بانتظام على مقاسات الأيقونات (16/20/24) وارتفاعات الأسطر، فتختفي المحاذاة العشوائية. التفصيل الكامل ومتى تُستخدم كل خطوة في [spacing.md](spacing.md).

```css
:root {
  --space-0:    0;
  --space-3xs:  2px;   /* استثناء: حدود/فواصل شعرية فقط */
  --space-2xs:  4px;
  --space-xs:   8px;
  --space-sm:   12px;
  --space-md:   16px;  /* الوحدة الأكثر استخدامًا */
  --space-lg:   24px;
  --space-xl:   32px;
  --space-2xl:  48px;
  --space-3xl:  64px;
  --space-4xl:  96px;
}
```

**السبب في هذه التوقفات تحديدًا:** نموّ شبه هندسي (كل خطوة ≈ 1.5× السابقة) — كافٍ لتغطية من حشو زر إلى فصل أقسام، دون كثرة خيارات تُغري بالعشوائية.

---

## 4. الطباعة — Typography

القيم كاملةً ومبرَّرة (لماذا 12px أرضية، ولماذا ارتفاع سطر 1.7 للعربي) في [typography.md](typography.md).

```css
:root {
  --font-family-base: system-ui, "Segoe UI", Tahoma, sans-serif; /* قابل للثيم */
  --font-family-mono: ui-monospace, "SF Mono", monospace;        /* أرقام/أكواد */

  --font-size-xs:   0.75rem;  /* 12px — الأرضية، لا أصغر */
  --font-size-sm:   0.875rem; /* 14px */
  --font-size-md:   1rem;     /* 16px — نص الجسم */
  --font-size-lg:   1.125rem; /* 18px */
  --font-size-xl:   1.25rem;  /* 20px */
  --font-size-2xl:  1.5rem;   /* 24px */
  --font-size-3xl:  1.875rem; /* 30px */
  --font-size-4xl:  2.25rem;  /* 36px */

  --line-height-tight:   1.3;  /* عناوين */
  --line-height-snug:    1.5;  /* عناصر واجهة سطر واحد */
  --line-height-base:    1.7;  /* نص عربي متعدد الأسطر */

  --font-weight-regular:  400;
  --font-weight-medium:   500;
  --font-weight-semibold: 600;
  --font-weight-bold:     700;

  --letter-spacing-normal: 0;  /* العربية لا تُباعَد حروفها — انظر typography */
}
```

---

## 5. الزوايا — Radii

```css
:root {
  --radius-none: 0;
  --radius-sm:   4px;    /* وسوم، شارات، حقول صغيرة */
  --radius-md:   8px;    /* الأزرار، الحقول، الكروت — القابل للثيم */
  --radius-lg:   12px;   /* مودال، درج، حاويات كبيرة */
  --radius-full: 9999px; /* الصور الرمزية والحبّات (pills) فقط */
}
```
**السبب:** أربع خطوات تكفي. `full` محصور في الدوائر/الحبّات حتى لا تُدوَّر الحاويات المستطيلة بإفراط فتفقد جدّية تطبيق البيانات.

---

## 6. الظلال — Elevation

**لأن المنتج تطبيق بيانات:** الارتفاع يُبنى أولًا بالحدود (1px) لا بالظلال. الظلال خفيفة ومحصورة في العناصر الطافية فعلًا. لا ظلال على الكروت الساكنة.

```css
:root {
  --shadow-sm: 0 1px 2px rgba(28,28,36,0.06);                          /* عنصر طافٍ خفيف */
  --shadow-md: 0 4px 12px rgba(28,28,36,0.10);                         /* قائمة منسدلة، popover */
  --shadow-lg: 0 12px 32px rgba(28,28,36,0.16);                        /* مودال، درج */
  --shadow-focus: 0 0 0 2px var(--color-bg-surface), 0 0 0 4px var(--color-focus-ring); /* يستخدم focus-ring المفصول عن accent — لا يُكسَر مع accent فاتح (v1.1) */
}
```

---

## 7. الحركة — Motion

```css
:root {
  --duration-fast:   120ms;  /* تمرير، تركيز، تبديل حالة */
  --duration-base:   200ms;  /* فتح قائمة، إظهار/إخفاء */
  --duration-slow:   320ms;  /* درج/مودال */
  --ease-standard:   cubic-bezier(0.2, 0, 0, 1);   /* الافتراضي */
  --ease-decelerate: cubic-bezier(0, 0, 0, 1);     /* دخول عنصر */
}
```
**قاعدة:** كل حركة تحترم `prefers-reduced-motion` (تُختصر إلى ~0ms). الحركة تُوضّح علاقة لا تُزيِّن.

---

## 8. الطبقات — Z-index

سلّم مُسمّى يمنع حرب `z-index: 9999`:

```css
:root {
  --z-base:     0;
  --z-sticky:   100;  /* رأس جدول لاصق، شريط أدوات */
  --z-dropdown: 200;  /* قوائم، popover */
  --z-overlay:  300;  /* خلفية المودال */
  --z-modal:    310;  /* المودال/الدرج */
  --z-toast:    400;  /* تنبيهات لحظية */
}
```

---

## 9. المقاسات الثابتة — Sizing

```css
:root {
  --size-touch-min:   44px;   /* أصغر هدف لمس — غير قابل للتفاوض (a11y) */
  --size-control-sm:  32px;   /* ارتفاع زر/حقل صغير */
  --size-control-md:  40px;   /* الافتراضي */
  --size-control-lg:  48px;   /* بارز */
  --size-icon-sm:     16px;
  --size-icon-md:     20px;
  --size-icon-lg:     24px;
  --border-width:     1px;
  --border-width-strong: 2px; /* حلقة تركيز، حدّ تفاعلي */
}
```

> أي عنصر تفاعلي يصغر بصريًا عن 44px يجب أن تبلغ منطقة لمسه 44px عبر الحشو (انظر [button](../components/button.md)).
