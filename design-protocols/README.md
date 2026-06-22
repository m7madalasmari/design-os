# Design Protocols — v1.1 (stable)

Agent operating contract. Entry point: root `AGENTS.md`. This set is **stable**; any change is recorded in the Changelog and bumps the version.

## Read order
`00` → `01` → `02` → `03` → `04` → `05` → `07` → `08` → `design-system/` → `page-manifests/<page>.md`

## Files
- **00-operating-rules** — constitution: read order, mode selection, mandatory sequence, scope discipline, Tailwind rules.
- **01-image-to-ui-replication** — image = visual contract; 4 modes; pre-implementation analysis; arbitrary-value rule.
- **02-design-system-ssot** — the design system is source of truth; Tailwind binding (token ↔ class).
- **03-pixel-qa** — system + visual + Tailwind QA; mismatch + polish/motion tables.
- **04-arabic-rtl-ux** — RTL + Arabic UX writing; Tailwind logical utilities.
- **05-visual-polish-and-motion** — polish/motion/SVG gated by purpose + mode; page-type polish rules.
- **07-definition-of-done** — the acceptance gate: when a UI task is actually complete.
- **08-app-shell-and-routing-consistency** — app-level contract (shell/nav/routes), not per-page only.
- **examples/golden-qa-report.md** — worked QA report (pairs with `page-manifests/_GOLDEN_EXAMPLE.md`).

## Modes
Pixel Clone · System Fidelity (default) · Strict SSOT · Improved. Announce before building.

## Companions
- `design-system/` — tokens, components, rules, themes (the values & specs).
- `page-manifests/` — per-page contract; start from `_TEMPLATE.md`.

## Stability / change policy
v1.1 is stable. To change a protocol: edit the file + add a Changelog line (date + what + why). Breaking changes bump the major version. Design-system changes are logged in `design-system/CHANGELOG.md`.

## Changelog
- **v1.1** (2026-06-22) — added `07` Definition of Done (acceptance gate) + `08` app-shell/routing; focus/link decoupled from accent; executable token source (`tokens.css`); `VERSION.md` + `CHANGELOG.md`; golden example + QA report; `components/INDEX.md`; Ask-vs-Assume rule; Responsive Behavior manifest section; Lint-ready Rules (no enforcement yet). System design-system version: **v1.1.0**.
- **v1.0** (2026-06-22) — initial stable set `00–05`; Tailwind-first; page-manifest `_TEMPLATE.md`; Empty-State illustration conflict resolved (context-aware).
