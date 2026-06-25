# Design System — CHANGELOG

> Every change records: **what · why · affected · re-QA?** Any design-system change (tokens, components, foundations, protocols, visual-polish rules, RTL rules) must be logged here.

---

## v2.3.0 — 2026-06-24 — app shell: sidebar + app-header (multi-page proven)
The **request-portal dogfood** (a real interactive multi-page app) proved that **sidebar/app-shell + a data-app header are BLOCKING** for any multi-page app — `layout.md` described the *pattern* but there were no component specs. Promoted from BACKLOG, specced, then the shell was built on them. Additive. **Components 29 → 31.**
- **New `components/sidebar.md`:** app navigation — expanded/collapsed, item states (default/hover/**active** `aria-current`/focus/disabled), RTL `inline-start` (right), mobile drawer, a11y (`<nav>`), token bindings, visual baseline (active = bg+color not heavy border).
- **New `components/app-header.md`:** data-app topbar — page title (matches active nav) + search + notifications + account; sticky; RTL; **ghost** icon buttons; a11y landmarks. Distinct from the marketing `nav-bar.md`.
- **INDEX:** new **"App shell"** group (31 total); **README** +app-shell line + count 29→31; **BACKLOG:** sidebar/app-shell + data-app header marked **shipped** (deferred question resolved).
- **Dogfood:** `playground/request-portal/` (interactive shell + 4 pages — dashboard/requests/detail/new — vanilla JS, no build) + report `dogfood-request-portal-report.md`. **Verdict:** design-os scales from one page to a full multi-page app via the new shell + full library reuse, keeping all **six gates** (incl. zero raw inline style, native-control reset, ghost icon buttons, RTL `inline-start` sidebar).

## v2.2.1 — 2026-06-24 — modal/drawer initial-focus order (close ✕ ≠ first focus)
Visual review of the v2.2.0 modal preview showed the close ✕ taking a `:focus-visible` ring **on open** — because it was the **first focusable element** in the DOM. PATCH: contract + fixture.
- **`modal.md` §6.5 / `drawer.md`:** initial focus → **first meaningful field** (or dialog container `tabindex="-1"`), **NOT the close button**; the close ✕ **must not be the first tab stop** — place it **late in the DOM**, positioned visually top-`inline-end`.
- **Fixed `playground/users-management/preview.html`:** moved ✕ to last-in-DOM (absolute top-inline-end); first focusable is now the select → no stray corner ring on open.

## v2.2.0 — 2026-06-24 — Visual Polish Gate (6th gate) + native-control fix
A **visual** review of the v2.1.0 users-page preview exposed that the gates checked structure/a11y/tokens but **not visual execution** — the preview rendered **native/default controls** (browser button borders, native `<select>` arrow, double-bordered search) because the shim omitted the native-control reset (violating the system's own button/select/search specs). Adds a sixth gate. Additive; one fixture fixed.
- **New `foundations/component-visual-baseline.md`:** mandatory **native-control reset** (`appearance:none`) + subtle borders + focus-visible-only + tokenized overlay + icon weight + mature spacing.
- **New `rules/visual-polish-gate.md` (6th gate):** visual review of the **rendered output** for Buttons/Inputs/Modal/Select/Table/States — no native/default look, black/heavy or double borders, always-visible focus, un-tokenized overlays, debug-looking fixtures.
- **`forbidden-patterns.md` #19–#24:** heavy/black strokes · native/default controls · double borders · always-visible focus · un-tokenized overlays · debug-looking fixtures.
- **`component-quality-gate.md`** now checks **visual execution** ("component present ≠ visually good"); **`quality-gates.md`** = **6 gates**; **`qa-checklist.md`** §11; `ROLES.md`/`AGENTS.md` updated to six gates.
- **Fixed `playground/users-management/preview.html`:** native-control reset, styled select (custom chevron), search without double border, ghost close button, tokenized overlay, more-visible skeleton.
- **Visual regression report:** root `dogfood-v2.1.0-visual-regression-report.md` — corrects the earlier (wrong) "pass" verdict via actual visual comparison.

## v2.1.1 — 2026-06-24 — close high-impact gaps from users-page dogfood
Targeted closure of the 3 high-impact gaps surfaced by the v2.1.0 users-page dogfood + 2 small contracts. Additive, back-compatible. **Components 27 → 29.**
- **`components/avatar.md` (new):** initials/image/icon-fallback/status-dot · sizes xs–lg · circle/rounded · image-failed → initials → icon fallback · a11y (decorative when the name is beside it — never repeat the name) · semantic, low-emphasis colors only. Closes the ad-hoc `.avatar` gap.
- **`components/detail-view.md` (new composition):** description-list (`dl/dt/dd`) for a single entity — anatomy, variants (simple/grouped/summary/with-actions/with-status), responsive (2-col→stacked), RTL, a11y, visual rules (no card-per-field, no table-for-key-value). Closes the ad-hoc `dl` gap.
- **inline-`style=` gate:** forbidden **#18** (raw px/hex/minmax/transform/row-reverse in inline style); wired into `rules/quality-gates.md` (DS Gate), `rules/qa-checklist.md` §1, `07-definition-of-done.md` (box + grep helper), `LOCAL-STABILITY.md`. Closes the gap that `[...]`-only checks missed (surfaced twice).
- **`filter-bar.md` §11 — responsive contract:** desktop row / tablet wrap / mobile (search stays + filters → drawer/sheet) / RTL; no silent crop.
- **`modal.md` §6.6 + `drawer.md` — footer order:** canonical rule — inline-end alignment, DOM [secondary, primary], destructive takes the primary slot, **no manual `row-reverse`**.
- INDEX +avatar +detail-view (29); BACKLOG: avatar + detail-view marked shipped.
- Regression dogfood re-run on the users page (report: root `dogfood-v2.1.1-regression-report.md`).

## v2.1.0 — 2026-06-24 — Default DS audit uplift (anti-bland + IBM typography gated)
Executive DS audit + fixes. Additive/back-compatible (MINOR); default rendering largely preserved (link default brand-600→brand-700 for AA). Audit report: root `design-system-audit-report.md`. *re-QA:* link color; anti-bland review of existing fixtures.
- **Anti-bland (core gap):** new `rules/anti-bland-ui-rules.md` — 8 checkable rules vs monotony/generic output (measurable hierarchy ≥2 signals · ≥2 spacing relationships · grid varies by content · composition by page type · named density levels · depth=hierarchy · presentation by content · "add-intent" test). Promoted to a hard **Anti-Generic Gate**.
- **Typography enforced:** new `foundations/typography-system.md` — IBM Plex Sans Arabic (Arabic) + IBM Plex Sans (Latin) as permanent default + @font-face/fontsource loading; no Tajawal/Inter/browser-default. Made a **Typography Gate** (was mandated but ungated — the biggest unguarded mandate).
- **Token fixes (tokens.css):** +`--breakpoint-*` in `@theme` (were prose-only — SSOT gap); +`--color-secondary`/`-hover`/`-foreground` (neutral-derived); +`--color-primary-active` utility; +`--color-bg-inverse`/`--color-text-on-dark*`; **link default brand-600→brand-700** (honors documented decoupling/AA).
- **New references:** `foundations/token-architecture.md` (unified 4-tier), `rules/quality-gates.md` (5 gates), `../delivery-contract.md`, `../default-design-system-standard.md`, `../design-protocols/reference-driven-reconstruction.md`.
- **Component contracts strengthened:** modal+drawer a11y contract (role=dialog/aria-modal/focus-trap/return-focus/scroll-lock); form submit lifecycle (loading/success/server-error recovery); table responsive + a11y wiring (caption/scope/aria-sort/aria-busy); site-footer raw `#FFFFFF`/`--neutral-12` → semantic inverse tokens; component-tokens index +tabs/alert/toast/form/secondary.
- **Enforcement wired:** ROLES (5 gates), AGENTS, 07 DoD (+typography/anti-generic/README/static-grep boxes), qa-checklist (+§6 typography, +§10 anti-generic).
- **Backlog (P0/P1 next):** sidebar/app-shell spec, data-app header, textarea/radio/switch standalone, breadcrumb, dark-mode tokens.

## v2.0.0 — 2026-06-24 — Default DS uplift (3 layers)
**BREAKING (token architecture + theming model).** Raises the default design system: a smart color cascade, an explicit component-token tier, and an enforced quality gate. No component **values** changed at default (placeholder rendering preserved exactly); the *contracts* changed. *re-QA:* re-run color QA on any brand theme; re-confirm component acceptance criteria.

- **Layer 2 — Smart color system.** New [`foundations/color-system.md`](foundations/color-system.md): any brand **seed** derives a full 11-step ramp (`--brand-50…950`) via an agent-executed OKLCH lightness/chroma protocol → maps to semantic tokens → cascades to all components, with **mandatory contrast guards** + light-brand branch + worked example (#1277A1). `tokens.css` gains the `--brand-*` ramp tier; accent now derives from it (old values = stops 50/600/700/800, so default rendering is identical). Theming model in [`brand-foundation.md`](foundations/brand-foundation.md) is now **seed → ramp** (manual 4-step override still back-compatible). [`theme-tuwaiq.md`](themes/theme-tuwaiq.md) updated to the ramp model.
- **Layer 1 — Component-token tier.** New [`foundations/component-tokens.md`](foundations/component-tokens.md): the third tier expressed for a Tailwind-first system — a **binding contract** (component part/state → semantic token), not a CSS-var explosion. Rule: components bind to semantic tokens only (never `--brand-*`/`--neutral-*`/hex). Each spec's "علاقته بالتوكنز" section **is** this contract.
- **Layer 3 — Component Quality Gate.** New [`rules/component-quality-gate.md`](rules/component-quality-gate.md): mandatory universal + per-component acceptance criteria (Table · Modal · Form · Button · Input spelled out) + a **component-selection matrix** (Modal vs Drawer vs Page; Table vs Card vs List). Promoted to an enforced **third gate** alongside Design System + Accessibility gates.
- **Wired:** `ROLES.md` (3rd gate), `AGENTS.md`, `RUNBOOK.md` (step 8), `00-operating-rules.md`, `design-system/README.md` (foundations + rules index; spec template now includes Visual Acceptance + token-binding contract).

## v1.1.6 — 2026-06-23
Visual foundation + icon system (from gallery findings). Light `09` link only; no general-protocol behavior changed; no product pages; no real deps (Lucide standardized for real projects; preview uses inline-SVG Lucide-style shim); no tokens’ values changed except the font fallback chain.
- **Typography/Font** — standard fallback chain `IBM Plex Sans Arabic, IBM Plex Sans, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif` in `tokens.css`/`tokens.md`; `typography.md` rules: Arabic UI must use IBM Plex Sans Arabic; `system-ui` first only in preview (CSP, documented); no unlicensed font files committed. *re-QA:* visual only where the font loads.
- **New foundation `icon-system.md`** — `lucide-react` primary (`react-icons` brand/social fallback only); one style; sizes via `--size-icon-*`; decorative `aria-hidden` / meaningful labelled; RTL mirroring; preview = inline-SVG Lucide-style shim.
- **New component `search-input.md`** — control-height; RTL icon (`inline-start`, not mirrored); muted placeholder; **no inner native border**; token focus ring; optional clear; filter-bar alignment; disabled/error/loading.
- **Button** — Visual Acceptance Criteria (no native/black borders; primary/secondary/tertiary token mapping; token focus; disabled not active; compact table-action style; RTL icon).
- **Table** — Visual rules + **column sizing** (ID/name/status/date/action); sort header not native; sort icon from icon-system; tokenized sticky z; subtle token row hover; footer/pagination alignment.
- **Filter Bar** — alignment with `search-input` + icon-system.
- **Select / Input** — native-control prevention (appearance reset; token focus/hover/error; icons from icon-system; RTL placement).
- **INDEX** — Search Input row + icon-system note; **README** components 19 → 20 + icon-system foundation. *re-QA:* none (additive).

## v1.1.5 — 2026-06-23
Strengthen core component specs (spec pass closing the gaps the Design System Preview fixture surfaced). No protocols (00–09) changed, no product pages, no tooling/deps; no tokens changed.
- **New components:** `spinner.md`, `skeleton.md`, `alert.md` — *what:* full standalone specs (Purpose · When to/not · Anatomy · Variants · Sizes · States · RTL · a11y · Tailwind · Tokens · Visual acceptance · Anti-patterns · Examples). *why:* gallery surfaced them as undocumented primitives. *re-QA:* none (additive; spec-only, no code).
- **`pagination.md` — graduated** from composition-pattern → documented component (prev/next · numbered · current · disabled · result summary · RTL chevron mirroring · vs infinite-scroll/load-more).
- **`select.md` — strengthened:** trigger · open · option list · selected · keyboard · disabled · error · loading · empty-options · close behavior · RTL icon placement · focus/ring.
- **`components/INDEX.md`:** new *Feedback & loading* table (Spinner/Skeleton/Alert); Pagination added to *Data*; Select states expanded; Pagination removed from Compositions/Known-gaps. Tooltip/Popover & Data-viz marked **deferred**.
- **`README.md`:** component count 15 → 19; added Feedback & loading + Pagination.
- *re-QA:* none required for existing pages (additive specs). Playground `design-system-preview` gallery+manifest updated to render the new states (fixture only).

## v1.1.2 — 2026-06-23
Patch (docs/clarification). No tokens/components changed behaviorally; no product pages.
- **components/INDEX.md** — *what:* resolved the Pagination double-listing → single `composition-pattern` (`needs: component-spec`). *why:* the same item was listed as both a composition and a gap (found in the invoices test). *re-QA:* none.
- **foundations/tokens.md** — *what:* documented the **Token Var Exception** rule for non-utility tokens (z-index/duration/easing/control sizes) consumed via `style`+`var()`, with conditions. *why:* the "no arbitrary values" rule had no sanctioned path for tokens Tailwind doesn't generate. *re-QA:* none.
- Protocol-layer changes (Greenfield mode, demo-data, preview strategy, QA-report location) are logged in the OS-level [`CHANGELOG.md`](../CHANGELOG.md).

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
