# Design Protocols — v1.1 (stable)

Agent operating contract. Entry point: root `AGENTS.md`. This set is **stable**; any change is recorded in the Changelog and bumps the version.

## Read order
`00` → `01` → `02` → `03` → `04` → `05` → `06` → `07` → `08` → `design-system/` → `page-manifests/<page>.md`
*(SPA build tasks only: also `09` — see Files. Conditional, not part of the design read order.)*

## Files
- **00-operating-rules** — constitution: read order, mode selection, mandatory sequence, scope discipline, Tailwind rules.
- **01-image-to-ui-replication** — image = visual contract; 4 modes; pre-implementation analysis; arbitrary-value rule.
- **02-design-system-ssot** — the design system is source of truth; Tailwind binding (token ↔ class).
- **03-pixel-qa** — system + visual + Tailwind QA; mismatch + polish/motion tables.
- **04-arabic-rtl-ux** — RTL + Arabic UX writing; Tailwind logical utilities.
- **05-visual-polish-and-motion** — polish/motion/SVG gated by purpose + mode; page-type polish rules.
- **06-accessibility** — a11y baseline (WCAG AA): semantic HTML, keyboard/focus/focus-trap, ARIA, forms, contrast, reduced motion, SR, loading/alerts/tables, RTL/icon a11y + QA checklist. Runs on every task.
- **07-definition-of-done** — the acceptance gate: when a UI task is actually complete.
- **08-app-shell-and-routing-consistency** — app-level contract (shell/nav/routes), not per-page only.
- **09-spa-build-standards** — *(conditional, engineering layer)* pinned stack + technical architecture for real Vite/React SPAs (handover/Nx). Applies only to SPA build tasks; gated by the Engineering DoD in `07`.
- **examples/golden-qa-report.md** — worked QA report (pairs with `page-manifests/_GOLDEN_EXAMPLE.md`).

## Modes
Auto (meta) · Pixel Clone · System Fidelity (default) · Strict SSOT · Improved · Greenfield/System-First (no reference). Announce before building. **Auto** resolves from the inputs — see [`../RUNBOOK.md`](../RUNBOOK.md).

## Companions
- `design-system/` — tokens, components, rules, themes (the values & specs).
- `page-manifests/` — per-page contract; start from `_TEMPLATE.md`.

## Stability / change policy
v1.1 is stable. To change a protocol: edit the file + add a Changelog line (date + what + why). Breaking changes bump the major version. Design-system changes are logged in `design-system/CHANGELOG.md`.

## Changelog
- **v1.1.7** (2026-06-23) — added **`06-accessibility`** (WCAG-AA baseline: semantic HTML · keyboard/focus/focus-trap · ARIA · forms · contrast · reduced motion · SR · loading/alerts/tables · RTL/icon a11y + QA checklist), filling the protocol-sequence gap (now `00–09` complete). Wired into `AGENTS.md`, `RUNBOOK.md`, `00`, `07`. Runs on **every** task. No product pages, no tooling.
- **v1.1.4** (2026-06-23) — run layer for one-shot usage: root **`RUNBOOK.md`** (request→delivery flow) + **`REQUEST.md`** + **`OUTPUT.md`**, and **Auto Mode** (meta-mode resolving to a concrete mode from inputs) wired into `AGENTS.md` + `00`. No core protocol behavior changed; no tooling/deps.
- **v1.1.3** (2026-06-23) — added **`09-spa-build-standards`** (conditional engineering layer: pinned stack — React 19/TS strict/Vite 6/Router 6/TanStack Query v5/Zustand 5/RHF 7+Zod/Axios 1/Tailwind 4/i18next/Vitest/ESLint+Prettier — folder structure, routing/HTTP/state/forms/error/i18n-RTL/auth/env/quality/alias/Tailwind/commits/deliverables/rejection list + Engineering Self-check); wired into `AGENTS.md` (trigger rules) and `07` (**Engineering Definition of Done**); `README`/`PROJECT-INSTALL` task-type split. No new design protocols, no product pages, no tooling, no deps. System version: **v1.1.3**.
- **v1.1.2** (2026-06-23) — close runtime-testing gaps from the invoices live-test: **Greenfield/System-First mode** (no-reference build; System Fidelity collapses into it; Pixel QA skipped); **Demo Data rule** (synthetic, PII-free, labeled); **template-vs-consumer** boundary (no product manifests inside design-os; outputs → `examples/`/`playground/`/`scratch/`); **Preview Strategy** (real Tailwind vs documented shim) + **Preview runtime** in QA; **Token Var Exceptions** (sanctioned `style`+`var()` for z/duration/easing/size); Pagination classification fixed in `INDEX`; **QA-report location** rule. No new protocols, no product pages, no tooling. System version: **v1.1.2**.
- **v1.1.1** (2026-06-23) — `tokens.css` completed to mirror `tokens.md` 1:1 (status triplets, shadows, motion, z, sizing, typography) + IBM Plex Sans Arabic as permanent default (all weights); `components/INDEX.md` strengthened (status/states/RTL-a11y/Tailwind usage); **Manual Self-check** added to `07`. System version: **v1.1.1**.
- **v1.1** (2026-06-22) — added `07` Definition of Done (acceptance gate) + `08` app-shell/routing; focus/link decoupled from accent; executable token source (`tokens.css`); `VERSION.md` + `CHANGELOG.md`; golden example + QA report; `components/INDEX.md`; Ask-vs-Assume rule; Responsive Behavior manifest section; Lint-ready Rules (no enforcement yet). System design-system version: **v1.1.0**.
- **v1.0** (2026-06-22) — initial stable set `00–05`; Tailwind-first; page-manifest `_TEMPLATE.md`; Empty-State illustration conflict resolved (context-aware).
