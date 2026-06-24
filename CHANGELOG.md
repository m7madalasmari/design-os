# design-os — CHANGELOG

OS-level history. Design-system detail (tokens/components) in [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md).

---

## v2.2.1 — 2026-06-24 — modal/drawer initial-focus order
**PATCH.** Visual review found the modal close ✕ taking focus (blue ring) **on open** because it was the first focusable element. Fixed contract + fixture: initial focus → first meaningful field (not close); close ✕ placed late in DOM (positioned visually top-inline-end). `modal.md` §6.5 + `drawer.md` + users-page preview.

## v2.2.0 — 2026-06-24 — Visual Polish Gate (6th gate)
**MINOR.** A **visual** review of the v2.1.0 users-page preview found **native/default-looking controls** that every prior gate missed — the gates checked structure/a11y/tokens, **not visual execution**. Root cause: the preview shim omitted the native-control reset (violating the system's own button/select/search specs). Adds the 6th gate; corrects the earlier (wrong) "pass". design-system → v2.2.0.
- **New:** `foundations/component-visual-baseline.md` (mandatory native-control reset, subtle borders, focus-visible-only, tokenized overlay) + `rules/visual-polish-gate.md` (6th gate, visual review of rendered output).
- `forbidden-patterns.md` **#19–#24** (heavy/black strokes · native controls · double borders · always-visible focus · un-tokenized overlays · debug fixtures); `component-quality-gate.md` now checks visual execution; `quality-gates.md` = **6 gates**; `qa-checklist.md` §11; ROLES/AGENTS.
- **Fixed** the users-page preview (native reset + styled select + ghost close + visible skeleton).
- Visual regression report: `dogfood-v2.1.0-visual-regression-report.md`.

## v2.1.1 — 2026-06-24 — close high-impact gaps from users-page dogfood
Additive, back-compatible. Closes the 3 high-impact gaps from the v2.1.0 dogfood + 2 small contracts. **Components 27 → 29.** design-system → v2.1.1 (detail: `design-system/CHANGELOG.md`).
- **avatar.md** (new component) — initials/image/icon-fallback/status-dot, sizes, circle/rounded, fallback chain, decorative-when-named a11y, semantic colors. Closes ad-hoc `.avatar`.
- **detail-view.md** (new composition) — description-list pattern for a single entity (no card-per-field, no table-for-key-value). Closes ad-hoc `dl`.
- **inline-`style=` gate** — forbidden #18 + wired into quality-gates / qa-checklist / 07 DoD (box + grep) / LOCAL-STABILITY. Closes the gap `[...]`-only checks missed.
- **filter-bar responsive contract** + **modal/drawer footer order** (no manual row-reverse).
- Regression dogfood on the users page **passed** — `dogfood-v2.1.1-regression-report.md`.

## v2.1.0 — 2026-06-24 — Default DS audit uplift (anti-bland + IBM typography gated)
**MINOR.** Executive deep audit of the default DS (report: `design-system-audit-report.md`) + fixes. Core finding: the system prevented *slop* but not *blandness*, and IBM typography was default-but-ungated. Back-compatible; default rendering preserved (link brand-600→700 for AA). design-system → v2.1.0 (detail: `design-system/CHANGELOG.md`).
- **Anti-Generic Gate** — new `design-system/rules/anti-bland-ui-rules.md`: 8 checkable rules vs monotony/generic UI (measurable hierarchy · ≥2 spacing relationships · grid/composition/presentation vary by content & page type · named density levels). Promoted to a hard gate.
- **Typography Gate** — new `design-system/foundations/typography-system.md`: IBM Plex Sans Arabic (ar) + IBM Plex Sans (latin) mandated as permanent default + loading + enforcement; no Tajawal/Inter/browser-default.
- **Token fixes** — breakpoints into SSOT `@theme`; +secondary/+primary-active/+inverse semantic tokens; link→brand-700.
- **New standards** — `token-architecture.md`, `quality-gates.md` (5 gates), root `delivery-contract.md`, `default-design-system-standard.md`, `design-protocols/reference-driven-reconstruction.md`.
- **Component contracts** — modal/drawer a11y contract, form submit lifecycle, table responsive + a11y wiring, site-footer raw-hex → semantic inverse tokens.
- **Gates now five:** Design System · Typography · Component Quality · Anti-Generic · Accessibility — wired into `ROLES.md`/`AGENTS.md`/`07-definition-of-done.md`/`qa-checklist.md`.

## v2.0.0 — 2026-06-24 — Default Design System uplift (3 layers)
**MAJOR.** Raises the default DS to a real systems level (Material/Atlassian/Carbon/Polaris *thinking*, not imitation): a smart color cascade, an explicit component-token tier, and an enforced quality gate. Default rendering is **byte-for-byte preserved** (old accent values = ramp stops 50/600/700/800); what changed is the **contracts** and the theming model. design-system → **v2.0.0** (detail: [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md)).
- **Layer 2 — Smart color system** (the quality lever): new `foundations/color-system.md` — any brand **seed** derives a full `--brand-50…950` ramp (agent-executed OKLCH protocol, no tooling) → semantic tokens → all components, with **mandatory contrast guards** + light-brand branch + worked example. Changing one color now cascades through the whole system, not just `primary`. `tokens.css` gains the ramp tier; theming is now **seed→ramp**.
- **Layer 1 — Component-token tier**: new `foundations/component-tokens.md` — the third tier as a **binding contract** (part/state → semantic token), fit for Tailwind-first (no CSS-var explosion). Components bind to semantic only.
- **Layer 3 — Component Quality Gate**: new `rules/component-quality-gate.md` — mandatory acceptance criteria per component (Table/Modal/Form/Button/Input) + component-selection matrix (Modal vs Drawer vs Page; Table vs Card vs List). Now a **third enforced gate** (Design System · Component Quality · Accessibility).
- **Wired:** `ROLES.md` (3 gates), `AGENTS.md`, `RUNBOOK.md` (step 8), `00-operating-rules.md`, `design-system/README.md`, `VERSION.md`, `README.md`, `LOCAL-STABILITY.md`.
- **Back-compat:** the manual 4-step accent override still works; existing pages render identically until a brand seed is applied.

## v1.3.0 — 2026-06-24 — roles layer: run procedure, gates, anti-generic stance
Hardening of the v1.2.0 roles layer after a live dogfood on the `consultation-requests` fixture. Additive; no protocol/token/component behavior changed; design-system untouched.
- **`ROLES.md` — new "How to run a role sweep"** (replaces the prose *Runtime rule* — single source for sweep mechanics): ordered flow **Fast sweep → Gates → remaining roles → manifest**, with **defined Fast-sweep outputs** — Product & Strategy: intent/scope/primary action · UX & IA: structure/task flow/states · Visual & Experience: composition/rhythm/polish risk.
- **Two explicit hard gates that block the pipeline:** **Design System Gate** (must pass before implementation is valid — tokens-only, all blocks mapped, anything new documented first; RUNBOOK step 7) and **Accessibility Gate** (must pass before delivery is acceptable — WCAG-AA floor; RUNBOOK step 9). Consistent with *Precedence* (hard floors, never traded). Named + wired in `AGENTS.md` and `RUNBOOK.md` (steps 7, 9).
- **"Output stance (anti-generic)":** do not stack components — compose the experience around the primary task; reject generic/default UI; demand hierarchy, rhythm, depth, purposeful polish. Owned by UX & IA (structure) + Visual & Experience (polish); reinforced in both role specs. A flat stack of default cards fails the sweep even if each component is individually valid.
- **"One finding, one owner"** sweep rule + **fixture-vs-consumer** scope note (Product & Strategy) — surfaced by the dogfood (a detail seen by several lenses is logged once; a demo/states block is legitimate in a `playground/` fixture but scope creep in a product page).
- **`page-manifests/_TEMPLATE.md`** — new **Accessibility Notes** section (keyboard/focus · contrast · ARIA/semantic HTML · reduced motion · RTL accessibility · status) — an explicit manifest home for the Accessibility role.
- **Dogfood result (for the record):** the sweep stayed fast (3-line fast / 9-line full, no debate) and caught two issues the fixture's embedded QA missed (tertiary text token ~3.3:1 used for visible labels; raw `style=` values vs a "zero arbitrary" claim) — validating that the layer adds value over the existing QA checklist. Fixture left as-is.
- **Consistency:** `README.md` + `VERSION.md` + `LOCAL-STABILITY.md` → v1.3.0.
- **MINOR** — additive (new manifest section, explicit gates, run procedure), backward compatible.

## v1.2.0 — 2026-06-24 — roles layer (the review council)
Additive run-layer feature: an **accountability layer** over the protocols. The protocols (`00–09`) are the *rulebooks*; roles are *who owns each one*. No protocol behavior, token, or component changed; design-system untouched.
- **New `ROLES.md`** — a **two-level** review council: a fast pass with each role's mindset, not extra agents and not a debate.
  - **Level 1 — 9 Operating Roles** (the only voices that run in the sweep): Product & Strategy · UX & Information Architecture · Visual & Experience Design · Design System · Content & UX Writing · Accessibility · Frontend & Implementation · QA & Validation · Documentation & Handoff. Each carries **Purpose · Owns · Decisions it can challenge · Checklist · Output in manifest · Anti-patterns**, plus its rulebook + phase.
  - **Level 2 — Checklists:** the detailed reviewers (≈45) become **checklist items** inside the role that owns them — never runtime voices.
  - **Separation rule:** *can it disagree with another role and need arbitration → Operating Role; just a verification dimension inside a larger role → Checklist Item.*
  - **Cross-cutting resolutions:** **RTL** is not a role (checklist under Design System · Content · Frontend · QA, governed by `04`); **Interaction** splits (UX = behavior/task-flow, Visual = polish/motion); **Performance** is a Frontend checklist tied to `09` (SPA-gate only); **Requirements Clarifier** → Product checklist; **Manifest/Changelog/Release/Handoff** → Documentation checklist.
  - **Runtime rule:** Full sweep = 9 roles max · Fast sweep = 3 minimum on every task (Product & Strategy · UX & IA · Visual & Experience); the rest run as QA/validation when needed, with Design System + Accessibility as non-skippable gates for any real interface.
  - **Precedence on conflict:** intent → accessibility floor → SSOT → reference fidelity → visual polish (Product & Strategy breaks ties).
- **Wired in:** `AGENTS.md` (*Roles — the review council* section, two-level + sweep rule), `RUNBOOK.md` (ROLES.md added to step 1 *Read the contract*; Review-phase sweep folded into step 9 *QA*), `00-operating-rules.md` (*Roles* pointer). No duplication — each touchpoint links to `ROLES.md`.
- **Consistency:** `README.md` (*What's inside* + version line `v1.1.0` → `v1.2.0`), `VERSION.md` (run-layer bundle + tag → `v1.2.0`).
- **MINOR** (additive, backward compatible): existing runs behave the same; the sweep makes the implicit ownership explicit.

## v1.1.9 — 2026-06-23 — docs consistency (full-review fixes)
Documentation-consistency pass from a full review. No spec/token/protocol behavior changed; no design-system version bump (specs unchanged at v1.1.6).
- **Component count fixed 20 → 27** — `design-system/README.md` (count + added the 7 missing from its list: rating · scale · stepper · form · nav-bar · hero · site-footer) and root `VERSION.md` bundle line. Now matches INDEX / coverage / gallery / CHANGELOG.
- **`LOCAL-STABILITY.md`** — "core components covered" flipped to `[x]` **27/27** (was a stale `[~]` 13/27 after v1.1.8); verdict + note updated (no partial-coverage caveat).
- **`design-system/README.md`** — removed stale "v0.1 / no brand identity yet" note → points to VERSION/CHANGELOG + notes real themes exist.
- **`design-system/VERSION.md`** — protocol-layer label `v1.1` → `00–09`; clarified it tracks design-system changes and may lag the OS release (by design).
- **Gallery `preview.html`** — renumbered sections **1–14 with Latin numerals** (was inconsistent: unnumbered new sections + Arabic-Indic numerals mixing with Latin data — also fixes a one-numeral-system violation).
- Verified clean: 0 broken links, read-order consistent (06 present, 1–12), tokens.css↔tokens.md font match, all 27 specs linked in INDEX, no TODO/stale refs.

## v1.1.8 — 2026-06-23 — complete component gallery coverage
Make `playground/design-system-preview/preview.html` a full mirror of `components/INDEX.md`: **27/27** documented components now render with core states. **Playground/docs only — no new specs, no Backlog, no React impl, no deps, no SPA starter, no GitHub, no dark mode, no Data-viz, no Tooltip/Popover, no token changes.**
- **Added 14 components to the gallery:** rating · scale · stepper · form · card · page-header · section-header · modal (preview-open) · drawer (preview-open) · toast · tabs · nav-bar · hero · site-footer.
- **Completed 3 partials:** input (+filled/readonly) · select (+disabled/error/loading/empty-options) · table (+selected row/sorted-active; in-body empty/no-results/error via shared empty-state).
- **Shim additions** for the new states (overlay/dark-fill/border-primary/border-b-2/size-8/stage/etc.) — still token-mirroring, **zero arbitrary values**, RTL-logical, no native-control chrome.
- **`coverage.md`** rewritten: 27/27 displayed · 0 missing · 0 partial · 2 deferred (Tooltip/Popover, Data-viz — no spec). **`manifest.md`** updated: Visual Acceptance Gate now complete for documented components (shim mirror, not an impl gate).
- No version change to `design-system` (no spec/token change) or protocols.

## v1.1.7 — 2026-06-23 — local stability and accessibility baseline
Make design-os stable and usable locally before any GitHub publish. No remote/push; no product pages; no tooling/deps.
- **New `design-protocols/06-accessibility.md`** — WCAG-AA baseline (semantic HTML · keyboard/focus order/focus-visible/focus-management · focus-trap for modal/drawer · ARIA roles/names/states · form validation & errors · contrast · reduced motion · screen-reader · accessible loading · alerts/toasts · accessible tables · RTL & icon a11y · do/don't · QA checklist). **Fills the protocol-sequence gap → `00–09` now complete.** Runs on **every** task.
- **Linked `06`** into `AGENTS.md` (read order), `RUNBOOK.md` (read + QA steps), `00` (read order), `07` (Accessibility QA in Definition of Done), `design-protocols/README.md` (read order + files + changelog).
- **New `playground/design-system-preview/coverage.md`** — gallery coverage audit: 13/27 displayed · 3 partial · 14 missing · 2 deferred + expansion priorities.
- **New `design-system/components/BACKLOG.md`** — 12 missing components (switch · radio · textarea · action-menu · breadcrumb · chip · progress · avatar · accordion · tooltip/popover · date-picker · data-viz) with why / priority / standalone-vs-within / dependencies / gallery.
- **New `LOCAL-STABILITY.md`** — definition + checklist for "locally ready"; current verdict: **locally ready** with one tracked caveat (partial gallery coverage).

## v1.1.6 — 2026-06-23 — visual foundation + icon system
Strengthen the visual foundation the gallery surfaced. No general protocols changed beyond a light `09` icon link; no product pages; **no real deps** (Lucide standardized for real projects only; preview uses an inline-SVG Lucide-style shim); no OCR/screenshot/GitHub/CLI/npm.
- **Font** — standard IBM Plex Sans Arabic fallback chain in tokens + `typography.md` rules (Arabic must use Plex; `system-ui` first only in preview, documented; no unlicensed fonts committed).
- **Icon system** — new `foundations/icon-system.md` (lucide-react primary, react-icons brand/social fallback, size tokens, RTL mirroring, a11y); wired into `09` + INDEX.
- **Native-control prevention + visual acceptance** — added to button, table (incl. column sizing), filter-bar, select, input; new `search-input.md`.
- **INDEX/README** — Search Input + icon-system; components 19 → 20.
- **Gallery** — Icon System section (Lucide-style) + font fallback note.
- design-system version → **v1.1.6**. Detail: [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md).

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
