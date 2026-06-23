# design-os — CHANGELOG

OS-level history. Design-system detail (tokens/components) in [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md).

---

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
