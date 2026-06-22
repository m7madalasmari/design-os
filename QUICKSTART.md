# QUICKSTART — design-os in 3 steps

## 1. Copy into your project root
```txt
cp -R design-os/AGENTS.md design-os/design-protocols design-os/design-system design-os/page-manifests /path/to/project
```
Result at the project root: `AGENTS.md` · `design-protocols/` · `design-system/` · `page-manifests/`.

## 2. Wire tokens into Tailwind
**Tailwind v4** — in your main CSS:
```css
@import "tailwindcss";
@import "./design-system/tokens.css";   /* @theme → bg-background, text-foreground, bg-primary, ring-ring, text-link … */
```
**Tailwind v3** — mirror the same names in `tailwind.config.js` (`theme.extend.colors`), each `var(--color-…)`. See `PROJECT-INSTALL.md`.

Set your brand in a theme block (override `--color-primary`, `--color-link`, `--color-ring`, optional `--color-brand`, `--radius-*`, font).

## 3. Give the agent the first prompt
```txt
اقرأ AGENTS.md وطبّق البروتوكولات المناسبة.

المهمة: [اكتب المهمة]
Mode: System Fidelity
الاتجاه: RTL عربي

قبل التنفيذ:
- أنشئ page manifest
- اربط المكونات
- طبّق Tailwind-first rules
- شغّل QA
- لا تعتبر المهمة مكتملة إلا بعد Definition of Done
```

That's it. The agent now: announces Mode → writes a manifest → maps components → builds with semantic classes → runs QA → reports, and only marks the task done when `design-protocols/07-definition-of-done.md` passes.
