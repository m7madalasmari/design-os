# design-os — Version

**Current: v2.1.0** (2026-06-24)

Bundles:
- **Run layer (root)** — `RUNBOOK.md` (one-shot request→delivery flow) + `REQUEST.md` (intake) + `OUTPUT.md` (handover) + `ROLES.md` (the review council — two-level: 9 Operating Roles + checklists; run procedure Fast→Gates→rest→manifest; **three hard gates**: Design System + Component Quality + Accessibility) + `LOCAL-STABILITY.md` (local-ready checklist); **Auto Mode** wired into `AGENTS.md`/`00`.
- `design-protocols/` — agent contract (**00–09 complete**, incl. `06` accessibility; + Greenfield/System-First mode; + conditional engineering layer `09` SPA build standards).
- `design-system/` **(v2.0.0)** — tokens.css (executable, **+`--brand-*` ramp tier**) + foundations (+icon-system **+color-system +component-tokens**) + components (+INDEX, 27 components) + rules (**+component-quality-gate**) + themes (seed→ramp model).
- `page-manifests/` — `_TEMPLATE.md` (+ Accessibility Notes) + `_GOLDEN_EXAMPLE.md`.
- `playground/` — outputs from testing design-os itself (not product pages); `design-system-preview` gallery now mirrors **27/27** documented components + `coverage.md`.

## Versioning policy
- **MAJOR** — breaking change to a semantic token, a component contract, or a protocol rule.
- **MINOR** — additive (new token/component/protocol/section), backward compatible.
- **PATCH** — clarifications, docs, non-behavioral fixes.

OS-level history is in [`CHANGELOG.md`](CHANGELOG.md); design-system detail in [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md). Every change records: what · why · affected · re-QA?

Git tag for this release: **`v2.1.0`**.
