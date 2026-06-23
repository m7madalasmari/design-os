# PROJECT-INSTALL — using design-os in a project

Answers the practical questions, in order.

## 1. How do I use it in a new project?
Copy the four items to the **project root**:
```txt
cp -R design-os/AGENTS.md design-os/design-protocols design-os/design-system design-os/page-manifests /path/to/project
```
Then wire tokens (§3/§4), set the brand (§ brand), and give the first prompt (§5). Nothing else is required to start.

## 2. Where do the files go?
At the **repository root** (next to your app):
```
/your-project
  AGENTS.md            ← agents read this first (rename/symlink to CLAUDE.md if your tool needs it)
  design-protocols/
  design-system/
  page-manifests/
  src/ … (your app)
```
> **Template vs consumer.** `design-os` is an operating template, not a product repo. You **copy** it into your project; real `page-manifests/<page>.md` and product pages live in **your** project, never inside the design-os template. (Testing design-os itself → use `examples/` / `playground/` / `scratch/`.) See [`07`](design-protocols/07-definition-of-done.md).

## 3. Wire tokens.css with Tailwind v4
In your main stylesheet:
```css
@import "tailwindcss";
@import "./design-system/tokens.css";
```
`tokens.css` uses `@theme`, so utilities are generated automatically: `bg-background`, `text-foreground`, `bg-card`, `text-muted-foreground`, `bg-primary` / `text-primary-foreground`, `border-border`, `ring-ring`, `text-link`, `bg-destructive`, `rounded-md` / `rounded-lg`.

## 4. Wire tokens with Tailwind v3 (config)
Define the CSS variables once (e.g. a `:root` block mirroring `tokens.css`), then map them in config:
```js
// tailwind.config.js
module.exports = { theme: { extend: { colors: {
  background:'var(--color-background)', foreground:'var(--color-foreground)',
  card:'var(--color-card)', muted:{DEFAULT:'var(--color-muted)', foreground:'var(--color-muted-foreground)'},
  primary:{DEFAULT:'var(--color-primary)', foreground:'var(--color-primary-foreground)'},
  border:'var(--color-border)', input:'var(--color-input)', ring:'var(--color-ring)',
  link:'var(--color-link)', destructive:'var(--color-destructive)',
  success:'var(--color-success)', warning:'var(--color-warning)', info:'var(--color-info)',
}, borderRadius:{ md:'var(--radius-md)', lg:'var(--radius-lg)' } } } }
```
There must be **one** executable source; `foundations/tokens.md` is documentation only.

## Brand setup (any version)
Override in a theme block — note the v1.1 focus/link decoupling:
```css
:root[data-theme="tuwaiq"]{ --color-primary:#4F29B7; --color-primary-foreground:#fff;
  --color-link:#4F29B7; --color-ring:#4F29B7; }            /* dark accent → may reuse for link/ring */
:root[data-theme="moonli"]{ --color-primary:#1C1C24; --color-primary-foreground:#fff;
  --color-brand:#C6F24E; --color-brand-foreground:#15161A;
  --color-link:#1C1C24; --color-ring:#1C1C24; }            /* light brand → link/ring stay dark & readable */
```
Rule: **do not map link/ring to a light accent without verifying contrast** (link ≥ 4.5:1, ring ≥ 3:1).

## 5. The first prompt to the agent
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

## 6. How to choose a Mode
| Mode | Use when |
|---|---|
| Pixel Clone | exact copy of an image (arbitrary values allowed, documented) |
| System Fidelity *(default)* | match a design within the system |
| Strict SSOT | system consistency over the reference |
| Improved | you explicitly want polish/UX improvements |
Detail: `design-protocols/01-image-to-ui-replication.md`.

## 6b. Task type — design vs SPA build vs playground
- **Design task** (page/component/redesign): apply **`00–08`** only (usually). No build stack imposed.
- **SPA build task** (new app / Vite React / production-ready / handover / Nx monorepo): apply **`00–09`**, follow the pinned stack + structure in [`09-spa-build-standards.md`](design-protocols/09-spa-build-standards.md), and pass the **Engineering Definition of Done** in `07`. Activated by phrases like "build app", "create SPA", "Vite React", "production-ready", "handover", "Nx monorepo", "team standards", "implement as real app".
- **Playground task** (demo inside design-os): don't enforce the full SPA requirements unless explicitly requested; keep outputs in `playground/`.

## 7. How do I know the task is actually done?
Open `design-protocols/07-definition-of-done.md` and check every box: Mode stated · manifest · reference capture (if image) · component mapping · visual polish decision · responsive behavior · QA run · deviations documented · design-system updates identified · Required Output delivered. **Any unchecked box = in progress, not done.**

## 8. How to update the design-system without breaking projects
1. Edit in your **design-os source** (this repo), not per project.
2. Bump `VERSION.md` (semver: MAJOR = breaking token/component/rule; MINOR = additive; PATCH = docs/fixes).
3. Log in `CHANGELOG.md`: **what · why · affected files/components/pages · re-QA required?**
4. Projects pull the update; if `re-QA required`, re-run `03` on the affected pages only.
5. Brand differences stay in each project's theme block — never fork components.
