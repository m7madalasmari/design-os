# Component Inventory — INDEX

> **Before creating a new component, check this index first.** If a documented component (or a composition of existing ones) fits, use it. New components are documented here **before** use (forbidden #2).

Legend — Doc: ✅ full · 🟡 partial · States: ✅ defines loading/empty/error/disabled where applicable · RTL: ✅ logical/мirroring covered.

## Fields & actions
| Component | File | Use for | Doc | RTL | States |
|---|---|---|---|:--:|---|
| Button | `button.md` | actions (one primary/context) | ✅ | ✅ | hover/focus/active/disabled/loading |
| Input | `input.md` | single-line text/email/phone/number | ✅ | ✅ | hover/focus/filled/error/disabled/readonly |
| Select | `select.md` | one value from a known set | ✅ | ✅ | open/selected/error/disabled/loading |
| Checkbox | `checkbox.md` | multi-select / radio / toggle | ✅ | ✅ | checked/indeterminate/focus/error/disabled |
| Rating | `rating.md` | subjective star rating | ✅ | ✅ | empty/hover/selected/readonly/error |
| Scale | `scale.md` | numeric scale (NPS 1–N) | ✅ | ✅ | default/selected/focus/error/disabled |
| Stepper | `stepper.md` | small bounded integer | ✅ | ✅ | hover/focus/min/max/disabled/error |
| Form (composition) | `form.md` | assembling fields into a form | ✅ | ✅ | validation timing, layout, actions |

## Containers & headers
| Component | File | Use for | Doc | RTL | States |
|---|---|---|---|:--:|---|
| Card | `card.md` | grouped related content; KPI; fill variants | ✅ | ✅ | static/interactive/loading/empty |
| Page Header | `page-header.md` | top of a page (h1 + 1 primary action) | ✅ | ✅ | default/breadcrumb/tabs/loading/sticky |
| Section Header | `section-header.md` | a section within a page | ✅ | ✅ | default/action/count/collapsible |

## Data
| Component | File | Use for | Doc | RTL | States |
|---|---|---|---|:--:|---|
| Table | `table.md` | homogeneous records, compare/sort | ✅ | ✅ | loading/empty/no-results/error/hover/selected |
| Empty State | `empty-state.md` | no content (first-use/no-results/error/no-permission) | ✅ | ✅ | 4 types; heading rule; illustration policy |
| Filter Bar | `filter-bar.md` | narrow a list/table | ✅ | ✅ | default/active/loading/no-results |
| Status Badge | `status-badge.md` | entity status (semantic) | ✅ | ✅ | success/warning/danger/info/neutral |

## Layers & navigation
| Component | File | Use for | Doc | RTL | States |
|---|---|---|---|:--:|---|
| Modal | `modal.md` | short focused decision/confirm | ✅ | ✅ | open/loading/submitting |
| Drawer | `drawer.md` | longer side content/edit | ✅ | ✅ | open/loading/submitting |
| Toast | `toast.md` | non-blocking result feedback | ✅ | ✅ | success/error/info/warning/persistent |
| Tabs | `tabs.md` | parallel views of one entity | ✅ | ✅ | default/active/focus/disabled/loading/overflow |

## Marketing (non data-app)
| Component | File | Use for | Doc | RTL | States |
|---|---|---|---|:--:|---|
| Nav Bar | `nav-bar.md` | site/marketing top nav | ✅ | ✅ | default/sticky/scrolled/mobile |
| Hero | `hero.md` | marketing hero (brand moment) | ✅ | ✅ | default/with-cta/scroll-cue |
| Site Footer | `site-footer.md` | marketing footer | ✅ | ✅ | default/link states |

## Compositions (NOT components — built from the above)
- **Description list (`<dl>`)** inside Card — key/value facts. See `card.md`.
- **Brand highlight mark** — lime/brand background behind text. See `themes/`.
- **Numbered feature list** (01/02 …) — section-header + grid.

## Known gaps (documented; not yet built)
- **Data visualization** (chart, sparkline, legend, axis, tooltip) — not in the library yet.
- **Tooltip / Popover** — referenced by some components, not yet its own doc.
- **Pagination** — used by Table, not yet its own doc.
