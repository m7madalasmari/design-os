# معيار الطباعة — Typography System (IBM Plex, إجباري)

> **المعيار المعتمد الدائم** لكل مشروع يولّده design-os. يُكمّل [typography.md](typography.md) (السبب + السلّم) ويجعل الخط **مُلزِمًا ومحروسًا ببوّابة**. القيم التنفيذية في [tokens.css](../tokens.css).

## 1. القرار الإجباري (الخط الافتراضي)

| النص | الخط |
|---|---|
| **العربية** | **IBM Plex Sans Arabic** |
| **اللاتيني/الإنجليزي** | **IBM Plex Sans** (وIBM Plex Sans Arabic يغطّي اللاتيني أيضًا كاحتياط أول) |

سلسلة `--font-family-base` المعتمدة (tokens.css):
```
"IBM Plex Sans Arabic", "IBM Plex Sans", system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif
```

**القاعدة:** هذا هو الافتراضي **لكل المشاريع القادمة** — ما لم يطلب المستخدم خطًا مختلفًا صراحةً، أو يرفق هوية تحوي خطوطًا أخرى. عندها فقط يُبدَّل الخط عبر **ثيم** (يبقى `--font-family-base` قابلًا للثيم).

**ممنوع صراحةً كافتراضي:** خط المتصفّح الافتراضي · `system-ui` كخيار أول للعربية (إلا في معاينة CSP موثّقة) · **Tajawal** · **Inter** · أي خط عشوائي. (مُدرَج في [forbidden-patterns](../rules/forbidden-patterns.md).)

## 2. التحميل (بيئة بلا أدوات بناء)

**الخيار أ — fontsource (مشروع به حزم):**
```
npm i @fontsource/ibm-plex-sans-arabic
// ثم استورد الأوزان المستخدمة: 400 500 600 700
import "@fontsource/ibm-plex-sans-arabic/400.css"; /* …500/600/700 */
```

**الخيار ب — `@font-face` محلّي (لا حزم):**
```css
@font-face{
  font-family:"IBM Plex Sans Arabic";
  font-style:normal; font-weight:100 700;        /* متغيّر/مدى الأوزان */
  src:url("/fonts/IBMPlexSansArabic.woff2") format("woff2");
  font-display:swap;                               /* يمنع وميض النص المحجوب */
}
```
- حمّل **400/500/600/700** على الأقل (النظام يعتمدها بالكامل).
- **لا تُلتزَم ملفات خط في الريبو** إلا مرخّصة وبقرار صريح. (IBM Plex مرخّص OFL.)
- **المعاينة (playground/CSP):** يُسمح بـfallback `system-ui` **موثّقًا بملاحظة ظاهرة فقط** — ليس تسليمًا إنتاجيًا.

## 3. السلّم والكثافة (مرجع تنفيذي مختصر)
التفصيل والسبب في [typography.md](typography.md). الملزِم هنا:
- **العناوين متوازنة لا ضخمة:** h1=30 · h2=24 · h3=20px؛ 36px لأرقام KPI نادرًا فقط. **لا أحجام hero 48/60/72** في تطبيق بيانات.
- **النص:** جسم 16 · ثانوي/خلايا كثيفة 14 · أرضية مطلقة 12px (دونها يضيع تشكيل العربية).
- **ارتفاع السطر:** جسم عربي **1.7** · واجهة بسطر 1.5 · عناوين 1.3.
- **الأوزان:** 400 جسم · 500 تسميات/رؤوس · 600 عناوين/زر أساسي · 700 نادر. **الأوزان 100–300 للعرض الكبير فقط** (تتكسّر في النص العربي الصغير).
- **بلا `letter-spacing`** على العربية · بلا `italic` · بلا `justify` · بلا `text-transform`.
- **الأرقام لاتينية + `tabular-nums`** في الأعمدة الرقمية (محاذاة `end`).

## 4. الإنفاذ (بوّابة)
يُفحَص في **Typography Gate** ضمن [quality-gates](../rules/quality-gates.md) و[07-definition-of-done](../../design-protocols/07-definition-of-done.md):
- [ ] `--font-family-base` يبدأ بـ`IBM Plex Sans Arabic` (أو ثيم بديل مطلوب صراحةً + موثّق).
- [ ] الخط **مُحمَّل فعلًا** (fontsource/@font-face) — أو fallback المعاينة موثّق كـCSP-only.
- [ ] السلّم الطباعي مُطبَّق (أحجام من السلّم، أدوار الأوزان صحيحة، جسم عربي 1.7).
- [ ] لا Tajawal/Inter/افتراضي متصفّح كافتراضي.
**أي بند يفشل = التسليم غير مقبول.**
