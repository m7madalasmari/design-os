# Page Manifest — Design System Preview (Component Gallery)

> Test fixture (not a product page). Visual gallery to exercise design-os components + states **before** using them in pages. Purpose: **surface component problems**, not fix them.
> Preview: `preview.html`. Inside the template → `playground/` (template-vs-consumer rule).

- **Mode:** Greenfield / System-First (no reference)
- **Direction:** RTL (ar)
- **Theme:** neutral (no brand inferred)
- **Reference:** none
- **Preview runtime:** **shim mirror** (mirrors `tokens.css` + semantic classes 1:1; no Tailwind build)

## Intent
A single RTL page that renders every documented component and its states from `components/INDEX.md`, plus foundations, so components can be reviewed visually and gaps caught early.

## v1.1.8 — full coverage (27/27)
- **Added to gallery (14):** rating · scale · stepper · form · card · page-header · section-header · modal · drawer · toast · tabs · nav-bar · hero · site-footer.
- **Partials completed (3):** input (+filled/readonly) · select (+disabled/error/loading/empty-options) · table (+selected row/sorted-active; in-body empty/no-results/error rendered via the shared empty-state in §7).
- **Still partial:** none.
- **Still deferred (2):** Tooltip/Popover · Data-viz — no spec (BACKLOG), not invented.
- **Visual Acceptance Gate:** ✅ **complete for documented components** — every INDEX component is visible with core states, RTL-correct, token-only, zero arbitrary values, no native-control chrome. Caveat: it's a **shim mirror** (not a code/impl gate; library `impl: ✗`).

## Components shown  *(all from `components/INDEX.md`)*
- **Foundations:** system colors · status colors · typography scale (xs→4xl) · radius · shadows · spacing · **Icon System (Lucide-style, v1.1.6)** · **IBM Plex Sans Arabic fallback note (v1.1.6)**.
- **Button:** primary · secondary · tertiary · icon-button · disabled · loading · sm/md · icon+label (RTL placement).
- **Input:** text (default) · focus (forced) · disabled · error (+`aria-invalid`) · placeholder · search · select trigger · **select open menu** · checkbox (unchecked/checked/indeterminate/disabled/error).
- **Filter Bar:** search + status chips · active chip · count badges · clear-filters.
- **Status Badge:** neutral/info/success/warning/danger — dot+text — Arabic: جديدة/مجدولة/مكتملة/معلّقة/ملغية.
- **Table:** default · sticky header (scroll) · sortable header (`aria-sort`) · action column · pagination footer · loading skeleton.
- **Empty State:** first-use · no-results · error (`role=alert`) — simple icon only, heading element.
- **Feedback/Polish:** focus ring · hover · skeleton · inline alert · surface depth (border/sm/md/lg).
- **RTL:** text-start/end · ms/me/ps/pe · numerals/ids in `<bdi>` · button & search icon placement.

## Status mapping (status-badge)
جديدة→neutral · مجدولة→info · مكتملة→success · معلّقة→warning · ملغية→danger. (Maps cleanly to the 5 documented semantic states — no new color needed.)

## Demo Data Policy
- Uses demo data: Yes — table rows only (REQ-#### refs + amounts). PII risk: **none**. Labeling: gallery clearly marked "ليست صفحة منتج". Reason: visual component test.

## Forced-state demos (documented)
Some states can't show statically without interaction, so they are **forced** for display and labeled: input **focus** (`.ring`/`border-focus`), select **open menu**, button **loading** (spinner). These are display aids, not component logic.

## Token Var Exceptions  *(via shim from tokens.css)*
| Location | Token | Reason | Utility unavailable? |
|---|---|---|---|
| sticky table header | `--z-sticky` | layer order | Yes |
| transitions / spinner / pulse | `--duration-*`, `--ease-standard` | motion from tokens | Yes |

## Gallery scaffolding (not component values)
The gallery chrome uses a scaffolding style block + a few inline `style=` for layout only: swatch backgrounds via `var(--token)`, `grid-template-columns`, `max-height` (sticky demo), `min-width`/example widths, skeleton/bar widths. **These are preview layout, not component styling** — component examples themselves use semantic token classes only (zero arbitrary Tailwind values; verified by grep).

## Component gaps — found here → CLOSED in v1.1.5
The 5 gaps this fixture surfaced are now resolved by documented specs (the gallery renders their states):
1. **Spinner** — ✅ documented ([`spinner.md`](../../design-system/components/spinner.md)); gallery shows sizes sm/md/lg + in-button.
2. **Inline Alert** — ✅ documented ([`alert.md`](../../design-system/components/alert.md)) with Alert-vs-Toast distinction; gallery shows info/success/warning/danger (+ critical `role=alert`).
3. **Skeleton** — ✅ documented ([`skeleton.md`](../../design-system/components/skeleton.md)); gallery shows text-line / avatar / card.
4. **Pagination** — ✅ graduated from composition → component ([`pagination.md`](../../design-system/components/pagination.md)); gallery shows numbered + current + disabled + RTL-mirrored chevrons.
5. **Select** — ✅ strengthened ([`select.md`](../../design-system/components/select.md)): open/option-list/selected/keyboard/disabled/error/loading/empty-options + close behavior + RTL icon placement.

## Deferred gaps (still open, intentionally)
- **Tooltip / Popover** — referenced by Select/Table; no spec yet (INDEX "Known gaps").
- **Data visualization** — chart/sparkline/legend/axis; out of scope for now.

## Are component states sufficient?
**Yes** for the documented set — Button, Input, Checkbox, Status Badge, Empty State, Filter Bar, Table, **Spinner, Skeleton, Alert, Pagination, Select** all render their required states coherently in the gallery. No component now has a missing/thin spec among those shown. Remaining work is the two deferred gaps above (Tooltip/Popover, Data-viz), which the gallery cannot render.

## Which components still need a stronger spec?
None among those rendered (all closed in v1.1.5). Future spec passes: **Tooltip/Popover** and **Data-viz** (deferred).

## Out of Scope
Fixing any spec/token/component; Tooltip/Popover/Data-viz; real Tailwind build; brand theme; interactions/keyboard logic.

## QA  *(Greenfield → no Pixel QA)* · **QA Report Location:** Embedded
- System QA: tokens only ✅ · status badges dot+text ✅ · empty-state heading + simple icon ✅ · table sticky + `aria-sort` ✅ · one `<h1>` ✅ · AA contrast ✅.
- RTL QA (`04`): `dir=rtl` ✅ · logical utilities only (`ms/me/ps/pe`, `text-start/end`) ✅ · numerals/ids in `<bdi>` ✅ · icons inline-start ✅ · zero directional utilities ✅.
- Tailwind: semantic classes only · **zero arbitrary values in component markup** (grep ✅) · scaffolding isolated · token-var exceptions documented.
- Visual polish: focus ring / hover / skeleton / surface depth present; motion respects `prefers-reduced-motion`.
- **Design-system update:** the 5 gaps this gallery surfaced were **closed in v1.1.5** (Spinner/Skeleton/Alert documented, Pagination graduated, Select strengthened); the gallery was then updated to render their states.
- **DoD:** all boxes ✅ (Pixel QA N/A).
