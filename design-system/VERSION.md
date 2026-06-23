# Design System — Version

**Current: v1.1.5** (2026-06-23)

Covers the design system (`foundations/`, `components/`, `rules/`, `themes/`, `tokens.css`) and the agent protocol layer (`design-protocols/` v1.1).

## Versioning policy
- **MAJOR** — a breaking change to a semantic token, a component contract, or a protocol rule that invalidates existing usage.
- **MINOR** — additive: new token/component/protocol/section, backward-compatible.
- **PATCH** — clarifications, docs, non-behavioral fixes.

Every change is recorded in [`CHANGELOG.md`](CHANGELOG.md) with: what · why · affected files/components/pages · whether re-QA is required.

## Executable token source
Runtime values come from **`design-system/tokens.css`** (Tailwind v4 `@theme`) or the project's Tailwind theme — **not** from `foundations/tokens.md` (documentation). See [`design-protocols/02`](../design-protocols/02-design-system-ssot.md).
