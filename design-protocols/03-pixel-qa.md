# 03 — Pixel QA

> Run after every implementation. No work ships without a QA report. Completion is gated by [`07-definition-of-done.md`](07-definition-of-done.md).

## Two layers
1. **System QA** — run the full [`design-system/rules/qa-checklist.md`](../design-system/rules/qa-checklist.md) (tokens, hierarchy, components, states, RTL, typography, accessibility, honesty).
2. **Visual QA** — compare the result against the reference image.

If the interface is Arabic/RTL, also apply [`04-arabic-rtl-ux.md`](04-arabic-rtl-ux.md). For polish / motion / SVG quality, also apply [`05-visual-polish-and-motion.md`](05-visual-polish-and-motion.md) and include its **Required Output** (polish added / skipped · motion · SVGs · unknowns · perf & a11y risks) in the report.

## Acceptance threshold by mode
- **Pixel Clone** — tight visual match; any noticeable difference is a defect to fix. Accessibility issues are **reported separately**, not silently fixed.
- **System Fidelity** — match within the system; **every deviation** from the reference is documented and justified.
- **Strict SSOT** — full system compliance; **list every conflict** with the reference.
- **Improved** — compliance + a list of intentional improvements, each justified.

## Visual match summary (report each)
Layout · Spacing · Typography · Color · Component · Hierarchy · Overall fidelity.

## Per-mismatch format (required)
- **Location** (file / element)
- **Difference** (reference vs result)
- **Type:** Token / Component / Layout / Content / Interaction / UX Writing
- **Severity**
- **Exact fix**
- **Scope:** a `design-system/` change, or page-only?

Cite [`forbidden-patterns`](../design-system/rules/forbidden-patterns.md) numbers on rejection (e.g., "rejected — #11 color outside tokens").

## Tailwind compliance check (Tailwind-first)
- **No arbitrary values** (`bg-[#…]`, `p-[…]`, `rounded-[…]`, `w-[…]`, …) outside Pixel Clone Mode.
- Every arbitrary value used in Pixel Clone Mode is **documented in the page manifest** (value + reason + location). An undocumented arbitrary value is a defect.
- Colors / spacing / radius use **semantic token classes** and the standard Tailwind scale.
- RTL uses **logical utilities** (`ms/me`, `ps/pe`, `start/end`, `text-start/text-end`) — flag any `ml/mr`, `left/right`, `text-left/right`.
- Any arbitrary value that belongs in shared components → flag a **Systemization Pass** (convert to token/component).

## Visual polish & motion QA (score each)

| Area | Match % | Issues | Fix |
|---|---:|---|---|
| Motion |  |  |  |
| SVG / Motifs |  |  |  |
| Hover / Focus States |  |  |  |
| Loading / Empty States |  |  |  |
| Surface Depth |  |  |  |

Pairs with the **Required Output** of [`05`](05-visual-polish-and-motion.md); page-type expectations: `05` → **Page Type Polish Rules**.

**Empty-state illustration check:** data/admin → simple icon only (no large decorative illustration); marketing → allowed if it serves identity/meaning. The component spec ([`empty-state.md`](../design-system/components/empty-state.md)) wins on conflict — flag violations.

## Lint-ready Rules  (defined now; enforcement NOT enabled yet)
Ready to encode in a linter when the project already has one — until then, checked here at QA time:
- No direct hex/rgb outside the token source (in component/page styles).
- No arbitrary Tailwind values outside Pixel Clone Mode (or without manifest documentation).
- No `left-*` / `right-*` in RTL — logical utilities only.
- No `text-left` / `text-right` in bilingual UI — use `text-start` / `text-end`.
- No edits to files outside the task scope.
- No new component when a documented one exists (check [`components/INDEX.md`](../design-system/components/INDEX.md)).

## After reporting
Fix **only** the mismatches. Do not redesign the page. If a mismatch's root cause is in the system (not the page), fix it in `design-system/` so every page benefits — then re-apply to the page.

## Optional review tool
A **Design QA Overlay** can be embedded in the page behind a review gate (`data-env="review"`): layout grid, component borders, numbered red markers, and a side issue list. It must never appear in production.
