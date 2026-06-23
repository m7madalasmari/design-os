# 07 — Definition of Done

> A UI task is **not complete** until every item below is satisfied. `AGENTS.md` forbids marking a task done otherwise. This is the acceptance gate that turns the protocol from guidance into a contract.

## Done checklist
- [ ] **Mode** identified and stated (Pixel Clone / System Fidelity / Strict SSOT / Improved / Greenfield-System-First).
- [ ] **Page manifest** created/updated in `page-manifests/` (from `_TEMPLATE.md`).
- [ ] **Reference Capture** documented *(if from an image)*: layout / spacing / type / color / radius / shadows / components observed, each labeled `observed / inferred / approximate / unknown`.
- [ ] **Component Mapping** documented: each block → an existing component (checked against [`components/INDEX.md`](../design-system/components/INDEX.md)); any missing component/token documented in `design-system/` **first**.
- [ ] **Visual Polish Decision** documented (polish/motion added · skipped · why — per [`05`](05-visual-polish-and-motion.md)).
- [ ] **Responsive Behavior** documented (desktop / tablet / mobile + table / nav / form / overflow — manifest section).
- [ ] **QA run** — the applicable ones:
  - **Pixel QA** — when there is a reference image.
  - **Design System QA** — System Fidelity / Strict SSOT.
  - **RTL QA** — Arabic / bilingual interfaces ([`04`](04-arabic-rtl-ux.md)).
  - **Accessibility QA** — **every interface** (the [`06`](06-accessibility.md) checklist; WCAG AA).
  - **Visual Polish QA** — any interactive interface ([`05`](05-visual-polish-and-motion.md) table in [`03`](03-pixel-qa.md)).
  - **Greenfield / System-First** (no reference) → **skip Pixel QA**; run Design-System + RTL + Visual-Polish QA.
- [ ] **Deviations / assumptions** documented and labeled.
- [ ] **Design-system updates** identified: needed? which files/components? **re-QA required?** — logged in [`CHANGELOG.md`](../design-system/CHANGELOG.md).
- [ ] **Required Output** delivered (the `05` report + QA tables + scope/deviations).
- [ ] **QA Report location** stated (embedded in this manifest, or a separate file) — see *QA report storage* below.
- [ ] **Token Var Exceptions** documented (if any `style`+`var()` token use) — manifest *Token Var Exceptions* table.

## Manual Self-check  (run before declaring done — no tooling required)
A quick pass the agent performs by hand (these are the same as the `03` Lint-ready Rules):
- [ ] **No undocumented arbitrary Tailwind values** (`bg-[#…]`, `p-[…]`, `w-[…]`, `rounded-[…]`…). Any used in Pixel Clone Mode are documented in the manifest.
- [ ] **No `left-*` / `right-*` / `ml-*` / `mr-*` / `pl-*` / `pr-*`** in RTL — logical utilities only (`ms/me`, `ps/pe`, `start/end`).
- [ ] **No `text-left` / `text-right`** — `text-start` / `text-end` instead.
- [ ] **No undocumented component** — every block maps to `components/INDEX.md` (or was documented first).
- [ ] **No out-of-scope changes** — only the files this task needed were touched.
- [ ] **Manifest + QA report present** — `page-manifests/<page>.md` exists and a `03` QA report was produced.
- [ ] **Token var exceptions documented** — any `style`+`var(--token)` for a token without a Tailwind utility (z-index/duration/easing/size) is listed in the manifest; no raw values, no arbitrary value where `var()` suffices.

Any failed line blocks completion. (Grep helpers, e.g. `\b(ml|mr|pl|pr)-` and `(bg|text|p|m|w|h|rounded)-\[` — purely manual, no Stylelint/CI added.)

## QA report storage
- **Small / medium task:** the QA report **may be embedded** inside the page manifest.
- **Large task:** create a **separate** report — `page-manifests/<page>.qa.md` or `qa-reports/<page>.md`.
- Definition of Done **must state where the QA report is stored** (manifest field: *QA Report Location*).

## Where outputs live (template vs consumer)
- **In a consumer project:** create `page-manifests/<page>.md`, build pages in the project, run QA on project pages — normally.
- **Inside the design-os template repo itself:** do **not** create production page manifests or product pages. When **testing design-os**, put worked outputs in `examples/`, `playground/`, or `scratch/` — never as production output in `page-manifests/` (which holds only `_TEMPLATE.md` + `_GOLDEN_EXAMPLE.md`). See [`README.md`](../README.md).

## Engineering Definition of Done  (SPA build tasks — gated by [`09`](09-spa-build-standards.md))
Applies **only** when `09-spa-build-standards.md` is active (SPA / Vite React / production / handover / Nx). In addition to the design DoD above, an SPA task is **not** complete unless:
- [ ] `npm install && npm run dev` works on **port 5173**.
- [ ] `npm run build` succeeds with **no warnings**.
- [ ] `npm run lint` passes with **no errors**.
- [ ] `npm run typecheck` passes with **no errors**.
- [ ] `npm run test` passes.
- [ ] `README.md` updated (setup / scripts / structure / env).
- [ ] `.env.example` present (every required var, no real values).
- [ ] **No hardcoded user-facing strings** (i18n only).
- [ ] **No route strings inside components** (use `app/app.paths.ts`).
- [ ] **No direct `axios` outside `core/api`.**
- [ ] **No `useEffect` for data fetching** (TanStack Query only).
- [ ] **No `any` / `@ts-ignore`.**
- [ ] **All pages lazy-loaded.**
- [ ] **i18n and RTL applied.**
- [ ] **Tailwind logical utilities used for RTL.**

Run the **Engineering Self-check** in [`09`](09-spa-build-standards.md) before these gates.

## Gate
If any box is unchecked, the task is **in progress**, not done. Report which boxes remain and why. Never present partial work as complete.
