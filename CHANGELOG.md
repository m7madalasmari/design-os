# design-os — CHANGELOG

OS-level history. Design-system detail (tokens/components) in [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md).

---

## v1.1.5 — 2026-06-23 — strengthen core component specs
Design-system spec pass closing the gaps the Design System Preview fixture surfaced. No protocols (00–09) changed, no product pages, no fixtures changed except the preview, no tooling/deps. Tooltip/Popover & Data-viz intentionally **deferred**.
- **New specs:** **Spinner · Skeleton · Alert** — standalone, 14-section (Purpose → Examples).
- **Pagination** — graduated from composition → documented component.
- **Select** — strengthened (open · option list · keyboard · disabled · error · loading · empty-options · close behavior · RTL).
- **`components/INDEX.md` + `design-system/README.md`** — new *Feedback & loading* group; Pagination moved to *Data*; count 15 → 19.
- **`playground/design-system-preview`** — gallery + manifest updated to render the new states and mark the 5 gaps **closed**.
- design-system version → **v1.1.5**. Detail: [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md).

## v1.1.4 — 2026-06-23 — add one-shot run layer (RUNBOOK + Auto Mode)
Organizational/additive patch enabling "use design-os from GitHub and run end-to-end". **No CLI, no npm package, no GitHub Actions, no dependencies; no core protocol behavior changed; design-system untouched.**
- **New `RUNBOOK.md`** — the full request→delivery pipeline (intake → detect task type → resolve Mode → read protocols → ask-vs-assume gate → manifest → component mapping → implement → QA → manual self-check → Definition of Done → deliver) + the copy-paste **one-shot prompt**.
- **New `REQUEST.md`** — intake template (Task · Mode · Direction · Reference image · Output type · Notes · Constraints).
- **New `OUTPUT.md`** — handover template (What was built · Files changed · Preview/runtime · Manifest location · QA report location · Definition of Done result · Known limitations · Next actions).
- **Auto Mode** — a meta-mode: when `Mode: Auto` (or unspecified), resolve from inputs → Pixel Clone / System Fidelity / Greenfield / Strict-SSOT-Review / Improved / SPA-Build+Greenfield. Wired into `AGENTS.md` (modes table + resolution) and `00` (pick-a-mode). Re-states the Ask-vs-Assume rule (ask only when a gap blocks execution or changes a core decision; else proceed with documented assumptions).
- **`README.md`** — **One-shot usage** section + `RUNBOOK`/`REQUEST`/`OUTPUT`/`playground` added to "What's inside".

## v1.1.3 — 2026-06-23 — add SPA build standards protocol
Adds a **conditional engineering layer** (separate from the design protocols). No new design protocols, no product pages, no Vite project, no dependencies, no CLI/npm package, no token/component changes.
- **New: `design-protocols/09-spa-build-standards.md`** — SPA Build Brief as mandatory standards: pinned stack (React 19 · TS strict · Vite 6 · React Router 6 · TanStack Query v5 · Zustand 5 · RHF 7 + Zod · Axios 1 · Tailwind 4 · i18next/react-i18next · Vitest · ESLint + Prettier), folder structure, naming, routing (`app.paths.ts`, lazy pages), HTTP (centralized Axios + TanStack Query), state (Zustand client-only), forms (RHF+Zod), error handling, i18n+RTL, auth abstraction, env handling, code quality, path alias `@/`, Tailwind conventions, commits, deliverables, rejection list, **Engineering Self-check**.
- **`AGENTS.md`** — when-to-use rule + **trigger phrases** ("build app", "create SPA", "Vite React", "production-ready", "handover", "Nx monorepo", "team standards", "implement as real app"); `09` added to read order as conditional; playgrounds exempt unless requested.
- **`07-definition-of-done.md`** — new **Engineering Definition of Done** (runnable gates: dev@5173 · build 0 warnings · lint 0 errors · typecheck 0 errors · test pass · README · `.env.example` · no hardcoded strings/routes · no direct axios · no fetch-in-useEffect · no `any`/`@ts-ignore` · lazy pages · i18n+RTL · logical Tailwind).
- **`README.md` / `PROJECT-INSTALL.md`** — task-type split: **Design (00–08)** vs **SPA build (00–09)** vs **Playground** (not enforced unless asked).
- **`00` + `design-protocols/README.md`** — read order / files index updated; `09` marked conditional.

## v1.1.2 — 2026-06-23 — close runtime testing gaps
No new protocols, no product pages, no tooling (no OCR/Playwright/Stylelint/CI/npm). Closes the runtime frictions found by the invoices live-test.
- **Greenfield / System-First mode** — for no-reference, description-only builds; *System Fidelity collapses into Greenfield when no visual reference exists*; Pixel QA skipped. *affected:* `AGENTS.md`, `00`, `07`, `design-protocols/README.md`.
- **Demo Data rule** — no invented production data; demo data allowed only if synthetic, PII-free, labeled, never shown as real, for preview/test. *affected:* `00`, `_TEMPLATE.md` (new *Demo Data Policy*).
- **Template vs consumer** — design-os is an operating template: no product manifests/pages inside it; test outputs go to `examples/`/`playground/`/`scratch/`. *affected:* `README.md`, `PROJECT-INSTALL.md`, `07`. Moved the invoices live-test → `playground/`.
- **Preview Strategy** — consumer = real Tailwind; design-os demos may use a documented shim mirroring `tokens.css` (not production). QA reports state the **Preview runtime**. *affected:* `02`, `03`, `README.md`.
- **Token Var Exceptions** — sanctioned `style`+`var(--token)` for tokens with no utility (z-index/duration/easing/control sizes), with conditions; documented in a manifest table. *affected:* `02`, `tokens.md`, `07`, `_TEMPLATE.md`.
- **Pagination classification fixed** — single `composition-pattern` (`needs: component-spec`); removed the double-listing in `components/INDEX.md`.
- **QA report location** — embedded (small/medium) vs separate file (large); DoD must state where. *affected:* `07`, `_TEMPLATE.md`.

## v1.1.1 — 2026-06-23 — close critical protocol gaps
No product pages changed. No Stylelint/CI, no libraries.
- **`tokens.css` now covers `tokens.md`** — full token set (status triplets `-soft`/`-border`, shadows, motion, z-index, sizing, full radii, typography).
- **Added `@theme inline`** — Tailwind mapping layer generating `bg-*`/`text-*`/`border-*`/`ring`/`rounded-*`/`shadow-*`/`font-*` from the `:root` values.
- **Strengthened `components/INDEX.md`** — per component: spec/impl status · required states · RTL/a11y · expected Tailwind usage.
- **Added Manual Self-check** to `07-definition-of-done` (arbitrary values · directional utilities · text-left/right · undocumented components · out-of-scope · manifest+QA).
- **Decoupled `link`/`ring` from `accent`** — `--color-text-link` & `--color-focus-ring` are independent, contrast-verified tokens in the executable `tokens.css`.
- (also) IBM Plex Sans Arabic set as the permanent default font (all weights). Detail: `design-system/CHANGELOG.md`.

## v1.1.0 — 2026-06-22
Packaged the system + protocols into a reusable, Tailwind-first git template, and closed v1.0's critical gaps.

- **Packaging:** assembled `AGENTS.md` + `design-protocols/` + `design-system/` + `page-manifests/` into `design-os/`; added `README`, `QUICKSTART`, `PROJECT-INSTALL`, OS-level `VERSION`/`CHANGELOG`.
- **Definition of Done** (`design-protocols/07`) — acceptance gate; AGENTS forbids marking work complete without it.
- **focus/link decoupled from accent** — `--color-focus-ring` / `--color-text-link` independent, contrast-verified; `--shadow-focus`/`--color-border-focus` use the ring token.
- **Executable token source** — `design-system/tokens.css` (Tailwind v4 `@theme`); `tokens.md` is documentation.
- **App-shell & routing consistency** (`design-protocols/08`).
- **Governance** — `VERSION.md` + `CHANGELOG.md` (system + OS).
- **Golden example** — `page-manifests/_GOLDEN_EXAMPLE.md` + `design-protocols/examples/golden-qa-report.md`.
- **Component inventory** — `design-system/components/INDEX.md`.
- **Ask-vs-Assume** rule (`00`); **Responsive Behavior** manifest section; **Lint-ready Rules** (`03`, not enforced).

## v1.0 — 2026-06-22
Initial system: foundations / components / rules / themes + agent protocols `00–05`, Tailwind-first, page-manifest `_TEMPLATE.md`, Empty-State illustration conflict resolved (context-aware; component spec wins).
