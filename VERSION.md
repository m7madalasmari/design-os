# design-os — Version

**Current: v1.1.6** (2026-06-23)

Bundles:
- **Run layer (root)** — `RUNBOOK.md` (one-shot request→delivery flow) + `REQUEST.md` (intake) + `OUTPUT.md` (handover); **Auto Mode** wired into `AGENTS.md`/`00`.
- `design-protocols/` — agent contract (v1.1: 00–05, 07, 08; + Greenfield/System-First mode; + conditional engineering layer `09` SPA build standards).
- `design-system/` — tokens.css (executable) + foundations (+icon-system) + components (+INDEX, 20 components) + rules + themes (v1.1.6).
- `page-manifests/` — `_TEMPLATE.md` + `_GOLDEN_EXAMPLE.md`.
- `playground/` — outputs from testing design-os itself (not product pages).

## Versioning policy
- **MAJOR** — breaking change to a semantic token, a component contract, or a protocol rule.
- **MINOR** — additive (new token/component/protocol/section), backward compatible.
- **PATCH** — clarifications, docs, non-behavioral fixes.

OS-level history is in [`CHANGELOG.md`](CHANGELOG.md); design-system detail in [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md). Every change records: what · why · affected · re-QA?

Git tag for this release: **`v1.1.6`**.
