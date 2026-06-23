# Design System Preview — Component Gallery (test fixture)

> **A visual test fixture, not a product page.** It renders every documented design-os component and its states on one RTL page, so components can be reviewed — and gaps caught — **before** they are used in real pages.

- **Type:** Component gallery fixture for **design-os v1.1.2+**.
- **Not a product page** — built to exercise/inspect components, not to ship.
- **Do not copy to consumer projects** — fixtures stay in `playground/`.
- **Purpose:** surface component problems (missing/weak specs, thin states), **not** fix them. Findings are logged in `manifest.md`; no spec/token/component was changed.
- **Theme:** neutral (no brand inferred). **Preview runtime:** **shim mirror** (mirrors `design-system/tokens.css` + semantic classes 1:1; no Tailwind build). Not production code.

## Files
- **`preview.html`** — the gallery (9 sections). Open in a browser.
- **`manifest.md`** — components shown · forced-state demos · token-var exceptions · **component issues found** · QA.

## Sections
Foundations · Buttons · Inputs · Filter Bar · Status Badges · Table · Empty States · Feedback/Polish · RTL Examples.

## Issues surfaced → closed in v1.1.5
The 5 component gaps this gallery surfaced are now resolved (the gallery renders their states):
- **Spinner · Skeleton · Alert** — now documented standalone components.
- **Pagination** — graduated from composition → documented component.
- **Select** — strengthened (open/option-list/keyboard/loading/empty-options + close behavior).

Still deferred (not renderable here): **Tooltip/Popover** & **Data-viz** (INDEX "Known gaps").

## Test result
- **Test:** Design System Preview — Greenfield · **Result:** ✅ Passed (gallery renders; gaps documented)
- **DoD:** ✅ Passed (Pixel QA N/A) · **Arbitrary values:** Zero (component markup) · **RTL:** ✅ Passed · **Manual self-check:** ✅ Passed
- **Design-system updates:** the 5 surfaced gaps were closed in **v1.1.5** (specs added/strengthened); gallery updated to render the new states.
