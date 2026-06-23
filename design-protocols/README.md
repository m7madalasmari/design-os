# Design Protocols — v1.1 (stable)

Agent operating contract. Entry point: root `AGENTS.md`. This set is **stable**; any change is recorded in the Changelog and bumps the version.

## Read order
`00` → `01` → `02` → `03` → `04` → `05` → `07` → `08` → `design-system/` → `page-manifests/<page>.md`
*(SPA build tasks only: also `09` — see Files. Conditional, not part of the design read order.)*

## Files
- **00-operating-rules** — constitution: read order, mode selection, mandatory sequence, scope discipline, Tailwind rules.
- **01-image-to-ui-replication** — image = visual contract; 4 modes; pre-implementation analysis; arbitrary-value rule.
- **02-design-system-ssot** — the design system is source of truth; Tailwind binding (token ↔ class).
- **03-pixel-qa** — system + visual + Tailwind QA; mismatch + polish/motion tables.
- **04-arabic-rtl-ux** — RTL + Arabic UX writing; Tailwind logical utilities.
- **05-visual-polish-and-motion** — polish/motion/SVG gated by purpose + mode; page-type polish rules.
- **07-definition-of-done** — the acceptance gate: when a UI task is actually complete.
- **08-app-shell-and-routing-consistency** — app-level contract (shell/nav/routes), not per-page only.
- **09-spa-build-standards** — *(conditional, engineering layer)* pinned stack + technical architecture for real Vite/React SPAs (handover/Nx). Applies only to SPA build tasks; gated by the Engineering DoD in `07`.
- **examples/golden-qa-report.md** — worked QA report (pairs with `page-manifests/_GOLDEN_EXAMPLE.md`).

## Modes
Pixel Clone · System Fidelity (default) · Strict SSOT · Improved · Greenfield/System-First (no reference). Announce before building.

## Companions
- `design-system/` — tokens, components, rules, themes (the values & specs).
- `page-manifests/` — per-page contract; start from `_TEMPLATE.md`.

## Stability / change policy
v1.1 is stable. To change a protocol: edit the file + add a Changelog line (date + what + why). Breaking changes bump the major version. Design-system changes are logged in `design-system/CHANGELOG.md`.

## Changelog
- **v1.1.3** (2026-06-23) — added **`09-spa-build-standards`** (conditional engineering layer: pinned stack — React 19/TS strict/Vite 6/Router 6/TanStack Query v5/Zustand 5/RHF 7+Zod/Axios 1/Tailwind 4/i18next/Vitest/ESLint+Prettier — folder structure, routing/HTTP/state/forms/error/i18n-RTL/auth/env/quality/alias/Tailwind/commits/deliverables/rejection list + Engineering Self-check); wired into `AGENTS.md` (trigger rules) and `07` (**Engineering Definition of Done**); `README`/`PROJECT-INSTALL` task-type split. No new design protocols, no product pages, no tooling, no deps. System version: **v1.1.3**.
- **v1.1.2** (2026-06-23) — close runtime-testing gaps from the invoices live-test: **Greenfield/System-First mode** (no-reference build; System Fidelity collapses into it; Pixel QA skipped); **Demo Data rule** (synthetic, PII-free, labeled); **template-vs-consumer** boundary (no product manifests inside design-os; outputs → `examples/`/`playground/`/`scratch/`); **Preview Strategy** (real Tailwind vs documented shim) + **Preview runtime** in QA; **Token Var Exceptions** (sanctioned `style`+`var()` for z/duration/easing/size); Pagination classification fixed in `INDEX`; **QA-report location** rule. No new protocols, no product pages, no tooling. System version: **v1.1.2**.
- **v1.1.1** (2026-06-23) — `tokens.css` completed to mirror `tokens.md` 1:1 (status triplets, shadows, motion, z, sizing, typography) + IBM Plex Sans Arabic as permanent default (all weights); `components/INDEX.md` strengthened (status/states/RTL-a11y/Tailwind usage); **Manual Self-check** added to `07`. System version: **v1.1.1**.
- **v1.1** (2026-06-22) — added `07` Definition of Done (acceptance gate) + `08` app-shell/routing; focus/link decoupled from accent; executable token source (`tokens.css`); `VERSION.md` + `CHANGELOG.md`; golden example + QA report; `components/INDEX.md`; Ask-vs-Assume rule; Responsive Behavior manifest section; Lint-ready Rules (no enforcement yet). System design-system version: **v1.1.0**.
- **v1.0** (2026-06-22) — initial stable set `00–05`; Tailwind-first; page-manifest `_TEMPLATE.md`; Empty-State illustration conflict resolved (context-aware).
