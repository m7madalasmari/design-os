# Component Gallery — Coverage Audit

> Compares documented components ([`../../design-system/components/INDEX.md`](../../design-system/components/INDEX.md)) against what the gallery ([`preview.html`](preview.html)) actually renders. Goal: know the gap before expanding. Audit only — the gallery is **not** fully expanded here.

**Documented in INDEX:** 27 component specs (+ `form` composition). **Rendered in gallery:** 13. **Deferred (no spec):** 2.

## Displayed — states sufficient (10)
| Component | Notes |
|---|---|
| Button | primary · secondary · tertiary · icon · disabled · loading · sm/md · icon+label (RTL) |
| Checkbox | unchecked · checked · indeterminate · disabled · error |
| Status Badge | neutral · info · success · warning · danger (dot+text) |
| Filter Bar | search + chips + active + counts + clear |
| Search Input | icon inline-start · clear · no inner native border |
| Spinner | sm/md/lg + in-button |
| Skeleton | text-line · avatar · card |
| Alert | info · success · warning · danger (+ role=alert) |
| Pagination | numbered + current + disabled + RTL chevrons; prev/next footer |
| Empty State | first-use · no-results · error |

## Partial — shown, some states missing (3)
| Component | Shown | Missing in gallery |
|---|---|---|
| Input | text · focus · disabled · error · placeholder | readonly · hover |
| Select | trigger · open menu · selected | disabled · error · loading · empty-options |
| Table | default · sticky · sort · action · pagination · loading | in-body empty/no-results/error · selected row · sorted-active |

## Missing from Gallery — documented but not rendered (14)
| Component | Priority to add |
|---|---|
| Card | **High** (core container) |
| Page Header | **High** (every page) |
| Section Header | **High** |
| Modal | **High** (focus trap demo + a11y) |
| Drawer | **High** (RTL slide + a11y) |
| Toast | **High** (vs Alert distinction) |
| Tabs | **High** (RTL flow + keyboard) |
| Stepper | Medium |
| Rating | Medium |
| Scale | Medium |
| Form (composition) | Medium (compose Input/Select/Checkbox) |
| Nav Bar | Low (marketing, non data-app) |
| Hero | Low (marketing) |
| Site Footer | Low (marketing) |

## Deferred — no spec yet (2)
| Item | Status |
|---|---|
| Tooltip / Popover | deferred (INDEX Known gaps; in BACKLOG) |
| Data visualization | deferred (INDEX Known gaps; in BACKLOG) |

## Recommended expansion order
1. **Containers & headers:** Card · Page Header · Section Header (frame for everything; quick wins).
2. **Layers & nav:** Modal · Drawer · Toast · Tabs — highest a11y value (focus trap, live regions, keyboard) now that `06` exists.
3. **Complete the Partials:** Select (disabled/error/loading/empty-options) · Table (in-body empty/error/selected) · Input (readonly).
4. **Form-ish:** Stepper · Rating · Scale · Form composition.
5. **Marketing (low):** Nav Bar · Hero · Site Footer.

> Keep each addition token-only, RTL-logical, zero arbitrary values, and `06`-compliant. Expand in small fixture passes, not one giant edit.
