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

## Components shown  *(all from `components/INDEX.md` — no new components added)*
- **Foundations:** system colors · status colors · typography scale (xs→4xl) · radius · shadows · spacing.
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

## Component issues found  *(documented, NOT fixed — per task)*
1. **Spinner — undocumented.** Button/Select `loading` states reference "دوّار" but there is **no Spinner spec** in INDEX. Rendered from tokens here. → needs a spec (or graduate from a primitive).
2. **Inline Alert/banner — undocumented.** Feedback "Alert" has no standalone spec; only **Toast** (`z-toast`) and **empty-state `error`** (`role=alert`) exist. Rendered inline here as `role=status`. → decide: is inline alert a Toast variant or its own component?
3. **Skeleton — not a standalone component.** Described only inside `table.md` loading; reused for inputs/cards here. → consider a documented Skeleton primitive.
4. **Pagination — composition only.** Already flagged `composition-pattern · needs: component-spec` (v1.1.2); the gallery confirms it behaves like a component (counter + prev/next) and would benefit from a real spec.
5. **Tooltip / Popover & Data-viz — known INDEX gaps.** Not renderable in the gallery (Select/Table reference tooltip-on-hover). Out of this fixture's scope; tracked in INDEX "Known gaps".
6. **Select open-menu / keyboard.** Spec describes states but the open-menu structure + keyboard contract are light; the gallery's open menu is an inferred rendering → spec could be stronger (focus order, type-ahead, checkmark placement).

## Are component states sufficient?
- **Sufficient:** Button, Input, Checkbox, Status Badge, Empty State, Filter Bar, Table — each has the states the gallery needed and they render coherently.
- **Thin / needs more:** Select (open-menu + keyboard + loading), and the **undocumented** Spinner/Alert/Skeleton primitives.

## Which components need a stronger spec?
Priority: **Spinner** (missing), **Alert vs Toast** (overlap/missing), **Skeleton** (implicit), **Pagination** (composition→spec), **Select** (open/keyboard detail). None blocked this fixture; logged for a future, separate spec pass — **not changed now**.

## Out of Scope
Fixing any spec/token/component; Tooltip/Popover/Data-viz; real Tailwind build; brand theme; interactions/keyboard logic.

## QA  *(Greenfield → no Pixel QA)* · **QA Report Location:** Embedded
- System QA: tokens only ✅ · status badges dot+text ✅ · empty-state heading + simple icon ✅ · table sticky + `aria-sort` ✅ · one `<h1>` ✅ · AA contrast ✅.
- RTL QA (`04`): `dir=rtl` ✅ · logical utilities only (`ms/me/ps/pe`, `text-start/end`) ✅ · numerals/ids in `<bdi>` ✅ · icons inline-start ✅ · zero directional utilities ✅.
- Tailwind: semantic classes only · **zero arbitrary values in component markup** (grep ✅) · scaffolding isolated · token-var exceptions documented.
- Visual polish: focus ring / hover / skeleton / surface depth present; motion respects `prefers-reduced-motion`.
- **Design-system update required? No** (gaps documented, nothing changed — per task).
- **DoD:** all boxes ✅ (Pixel QA N/A).
