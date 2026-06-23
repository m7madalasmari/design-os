# Design System — CHANGELOG

> Every change records: **what · why · affected · re-QA?** Any design-system change (tokens, components, foundations, protocols, visual-polish rules, RTL rules) must be logged here.

---

## v1.1.1 — 2026-06-23
Patch: complete the executable token source and self-check. No product pages changed.

- **tokens.css now covers the full token set** — *what:* added the missing tokens (status triplets `-soft`/`-border`, shadows, motion durations/eases, z-index, sizing, full radii, typography) so `tokens.css` mirrors `tokens.md` 1:1; structured as `:root` values + `@theme inline` Tailwind mapping. *why:* the proven gap (status `-soft` missing) meant the "single executable source" was partial. *affected:* `tokens.css`, `foundations/tokens.md` (+ sync table). *re-QA:* none (additive); fixes the badge gap surfaced in the users-list test.
- **Default font = IBM Plex Sans Arabic (all weights 100–700)** — *what:* set as the permanent default in `tokens.css`/`tokens.md`; usage rule reframed (100–300 large-display only). *affected:* `tokens.css`, `tokens.md`, `typography.md`, `brand-foundation.md`. *re-QA:* visual only where pages load the font.
- **tokens.md → documentation that mirrors tokens.css** + a tokens.md ⇆ tokens.css ⇆ Tailwind **sync/mapping table**.
- **components/INDEX.md strengthened** — per component: spec/impl status, required states, RTL/a11y, expected Tailwind usage. (No code library built.)
- **Manual Self-check** added to `07-definition-of-done.md` (arbitrary values · directional utilities · text-left/right · undocumented components · out-of-scope · manifest+QA). No Stylelint/CI.

## v1.1.0 — 2026-06-22
Hardening pass: turn v1.0 guidance into a contract with an acceptance gate. No product pages changed.

- **Definition of Done** — *what:* new `design-protocols/07-definition-of-done.md` + AGENTS rule. *why:* compliance must be a gate, not memory. *affected:* `AGENTS.md`, protocols. *re-QA:* future tasks only.
- **focus / link decoupled from accent** — *what:* `--color-focus-ring` and `--color-text-link` are independent tokens; `--shadow-focus`/`--color-border-focus` reference `--color-focus-ring`, not `--color-accent`. *why:* a light-accent theme (e.g. lime) broke focus/link contrast (found in Moonli test). *affected:* `tokens.css`, `foundations/tokens.md`, `foundations/brand-foundation.md`. *re-QA:* themes with a light accent must set link/ring to a dark, contrast-verified value; existing dark-accent themes (Tuwaiq, Moonli) unaffected. **Product pages not updated (per scope).**
- **Executable token source** — *what:* added `design-system/tokens.css` (Tailwind v4 `@theme`); `tokens.md` is documentation only. *why:* single runtime source; stop per-page token drift. *affected:* `tokens.css`, `02`, `AGENTS.md`, `VERSION.md`. *re-QA:* none (additive).
- **Versioning & changelog** — *what:* `VERSION.md` + this file. *why:* track changes + re-QA impact. *re-QA:* none.
- **Golden example** — *what:* `page-manifests/_GOLDEN_EXAMPLE.md` + `design-protocols/examples/golden-qa-report.md`. *why:* anchor consistency. *re-QA:* none.
- **Component inventory** — *what:* `components/INDEX.md` + "check INDEX before creating a component" rule. *why:* fast "is it documented?" lookup. *re-QA:* none.
- **Ask vs Assume rule** — *what:* added to `00`. *why:* codify when to stop-and-ask vs assume-and-label. *re-QA:* none.
- **Responsive Behavior** — *what:* mandatory section in `_TEMPLATE.md`. *why:* responsive made a process step. *re-QA:* none.
- **App-shell & routing consistency** — *what:* `design-protocols/08`. *why:* app-level (not per-page) contract. *re-QA:* none.
- **Lint-ready Rules** — *what:* section in `03`. *why:* rules ready for a future linter; enforcement NOT enabled now. *re-QA:* none.

## v1.0 — 2026-06-22
- Initial design system (foundations/components/rules/themes) + agent protocols `00–05` + Tailwind-first + page-manifest `_TEMPLATE.md` + Empty-State illustration conflict resolved (context-aware, component spec wins).
