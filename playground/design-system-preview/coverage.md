# Component Gallery — Coverage Audit

> Compares documented components ([`../../design-system/components/INDEX.md`](../../design-system/components/INDEX.md)) against what the gallery ([`preview.html`](preview.html)) renders. **As of v1.1.8 the gallery is a full mirror: every documented component appears with at least its core states.**

**Documented in INDEX:** 27 component specs (+ `form` composition). **Rendered in gallery:** **27/27**. **Missing:** 0. **Deferred (no spec):** 2.

## Displayed — every documented component (27/27)
| Category | Components (states shown) |
|---|---|
| Fields & actions | button (primary/secondary/tertiary/icon/disabled/loading/sm-md/icon+label) · input (default/focus/filled/error/disabled/readonly) · search-input · select (trigger/open/selected/disabled/error/loading/empty-options) · checkbox (5) · **rating** (empty/selected/readonly) · **scale** (selected/error) · **stepper** (default/min-reached) · **form** (layout/required/error/helper/submit) |
| Containers & headers | **card** (static/interactive/loading/empty) · **page-header** (title/desc/breadcrumb/action) · **section-header** (title/count/action) |
| Data | table (default/sticky/sort/action/pagination/loading/**selected**/**sorted-active**) · empty-state (first-use/no-results/error) · filter-bar · status-badge (5) · pagination (numbered/current/disabled/prev-next) |
| Feedback & loading | spinner (sm/md/lg) · skeleton (text/avatar/card) · alert (info/success/warning/danger) |
| Layers & navigation | **modal** (open/title/body/footer/close) · **drawer** (open/title/body/footer) · **toast** (success/error/info/warning) · **tabs** (active/default/disabled/overflow) |
| Marketing | **nav-bar** (logo/active-link/CTA) · **hero** (title/desc/CTA/secondary) · **site-footer** (links/copyright/secondary) |

**Note on table body states:** `empty` / `no-results` / `error` are rendered once in the **Empty States** section (they reuse the shared `empty-state` component) rather than duplicated inside each table — documented, not missing.

## Partial — none
No documented component is partial after v1.1.8. (Earlier partials — input, select, table — completed.)

## Deferred — no spec yet (2)
| Item | Reason |
|---|---|
| Tooltip / Popover | No spec yet — referenced by select/table; tracked in INDEX Known gaps + [`BACKLOG.md`](../../design-system/components/BACKLOG.md). Not rendered to avoid inventing an un-specced component. |
| Data visualization | No spec (chart/sparkline/legend/axis); tracked in Known gaps + BACKLOG. |

## Notes
- The gallery is a **visual-acceptance mirror** built with the **shim** (mirrors `tokens.css` + semantic classes) — it is **not** a code/impl gate (library is still `impl: ✗`).
- Marketing components (nav-bar/hero/site-footer) render with the neutral **dark** fill; the `brand` fill requires a theme and is intentionally not inferred here.
- Modal/Drawer are shown as **preview-only open states** on a stage (not real overlays); focus-trap is a runtime behavior verified in a real app (`06`).
