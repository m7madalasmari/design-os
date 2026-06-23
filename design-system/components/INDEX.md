# Component Inventory — INDEX

> **Before creating a new component, check this index first.** If a documented spec (or a composition of existing ones) fits, use it. New components are documented here **before** use (forbidden #2).

**Implementation status:** the library is **spec-only** — every component has a documented `.md` contract but **no shipped code yet** (`impl: ✗`). Build per project against the spec + the executable tokens (`../tokens.css`). Tailwind usage column = the expected utility shape.
**Icons:** all components follow [`foundations/icon-system.md`](../foundations/icon-system.md) — **`lucide-react`** primary (`react-icons` only as a brand/social fallback); sizes via `--size-icon-*`; directional icons mirror in RTL.
**Spec:** ✅ full · 🟡 partial · ✗ missing entirely.

## Fields & actions
| Component | Spec / Impl | Required states | RTL / a11y | Expected Tailwind usage |
|---|---|---|---|---|
| [Button](button.md) | ✅ / ✗ | hover · focus · active · disabled · loading | one primary; real `<button>`; 44px target; `aria-label` if icon-only | `inline-flex items-center gap-2 h-10 px-4 rounded-md bg-primary text-primary-foreground focus-visible:ring-2` |
| [Input](input.md) | ✅ / ✗ | default · hover · focus · filled · error · disabled · readonly | label above; `dir=ltr` for email/url/number; icon `inline-end`; no native appearance | `h-10 px-3 bg-card border border-border rounded-md focus-visible:ring-2` |
| [Search Input](search-input.md) | ✅ / ✗ | default · hover · focus · filled · disabled · loading | search icon `inline-start` (not mirrored), clear `inline-end`; `aria-label`; **no inner native border** | group `inline-flex items-center gap-2 h-10 ps-3 pe-3 border rounded-md focus-within:ring`; input `bg-transparent outline-none` |
| [Select](select.md) | ✅ / ✗ | default · hover · focus · open · selected · option-hover · disabled · error · loading · **empty-options** | arrow `inline-end`, check `inline-start`; `role=combobox`+`listbox`; full keyboard (↑↓/Home/End/type-ahead/Esc); returns focus on close | trigger like Input; menu `bg-popover shadow-md z=var(--z-dropdown)`; selected `bg-primary-subtle` |
| [Checkbox](checkbox.md) | ✅ / ✗ | checked · indeterminate · focus · error · disabled | box `inline-start`; 44px hit; check not mirrored | `size-5 rounded-sm border-border-strong`; checked `bg-primary` |
| [Rating](rating.md) | ✅ / ✗ | empty · hover · selected · focus · readonly · error | fills from `inline-start` (right); `aria-valuenow` | `inline-flex gap-1`; filled `text-primary`, empty `text-border-strong` |
| [Scale](scale.md) | ✅ / ✗ | default · selected · hover · focus · error · disabled | 1→N from right; Latin numerals; `role=radiogroup` | `inline-flex gap-1`; item `size-8 rounded-sm`; selected `bg-primary text-primary-foreground` |
| [Stepper](stepper.md) | ✅ / ✗ | hover · focus · min · max · disabled · error | `+` `inline-start`, `−` `inline-end`; `tabular-nums` | `h-10 border border-border rounded-md`; buttons `bg-primary` ≥44px |
| [Form](form.md) (composition) | ✅ / ✗ | per-field states; validate on blur/submit | labels above; logical spacing; one primary | `flex flex-col gap-4` |

## Containers & headers
| Component | Spec / Impl | Required states | RTL / a11y | Expected Tailwind usage |
|---|---|---|---|---|
| [Card](card.md) | ✅ / ✗ | static · interactive · loading · empty (fills: surface/muted/dark/brand) | logical padding; title `inline-start` | `bg-card border border-border rounded-lg p-6` (shadow only if raised) |
| [Page Header](page-header.md) | ✅ / ✗ | default · breadcrumb · tabs · loading · sticky | title `inline-start`, action `inline-end`; one `h1` | `flex items-center justify-between`; `h1 text-3xl font-bold` |
| [Section Header](section-header.md) | ✅ / ✗ | default · action · count · collapsible | title `inline-start`, action `inline-end` | `flex justify-between`; `h2 text-xl font-semibold` |

## Data
| Component | Spec / Impl | Required states | RTL / a11y | Expected Tailwind usage |
|---|---|---|---|---|
| [Table](table.md) | ✅ / ✗ | loading(skeleton) · empty · no-results · error · row hover/selected · sorted | RTL column flow; `text-start`; numbers `text-end tabular-nums`; scroll on mobile | `w-full text-sm`; thead `bg-muted`; rows `border-b hover:bg-muted` |
| [Empty State](empty-state.md) | ✅ / ✗ | first-use · no-results · error · no-permission | **title is a heading** (not `<p>`); icon by context | `flex flex-col items-center text-center gap-2 py-12` |
| [Filter Bar](filter-bar.md) | ✅ / ✗ | default · active · loading · no-results | search `inline-start`; clear `inline-end` | `flex flex-wrap gap-2`; chips `rounded-sm` |
| [Status Badge](status-badge.md) | ✅ / ✗ | success · warning · danger · info · neutral | dot + text (not color alone); not mirrored | `inline-flex gap-1 px-2 py-0.5 rounded-md text-xs`; `text-success bg-success-soft` |
| [Pagination](pagination.md) | ✅ / ✗ | default · current · disabled · hover · focus · ellipsis | `nav aria-label`; `aria-current=page`; chevron **mirrored** in RTL; numbers tabular+bidi | `flex items-center gap-2`; btn `h-8 px-3 rounded-md border`; current `bg-primary-subtle text-primary` |

## Feedback & loading
| Component | Spec / Impl | Required states | RTL / a11y | Expected Tailwind usage |
|---|---|---|---|---|
| [Spinner](spinner.md) | ✅ / ✗ | spinning (reduced-motion → static) | `aria-hidden` if decorative, `role=status`+label if meaningful; not mirrored | `size-5 border-2 rounded-full animate-spin motion-reduce:animate-none` |
| [Skeleton](skeleton.md) | ✅ / ✗ | loading (pulse); variants: text-line · avatar · card · table-row · block | placeholders `aria-hidden` + parent `aria-busy`; not final content | `bg-muted rounded-sm animate-pulse motion-reduce:animate-none` |
| [Alert](alert.md) | ✅ / ✗ | info · success · warning · danger; static · dismissible · with-action | `role=alert` (critical) / `role=status`; icon+text (not color alone); close `inline-end` | `flex items-start gap-2 p-3 rounded-md border bg-info-soft text-info border-info-border` |

## Layers & navigation
| Component | Spec / Impl | Required states | RTL / a11y | Expected Tailwind usage |
|---|---|---|---|---|
| [Modal](modal.md) | ✅ / ✗ | open · loading · submitting | `✕` `inline-end`; focus-trap; Esc; no nested | `z=var(--z-modal)`; `bg-card rounded-lg shadow-lg`; overlay `bg-overlay` |
| [Drawer](drawer.md) | ✅ / ✗ | open · loading · submitting | slides from `inline-start` (RTL=right); logical | `z=var(--z-modal)`; `shadow-lg`; sticky footer |
| [Toast](toast.md) | ✅ / ✗ | success · error · info · warning · persistent | `aria-live`; icon `inline-start` | `z=var(--z-toast)`; `rounded-md shadow-md` |
| [Tabs](tabs.md) | ✅ / ✗ | default · active · focus · disabled · loading · overflow | flow from right; indicator not mirrored; arrow keys; `role=tablist` | `flex gap-4`; active `border-b-2 border-primary` |

## Marketing (non data-app)
| Component | Spec / Impl | Required states | RTL / a11y | Expected Tailwind usage |
|---|---|---|---|---|
| [Nav Bar](nav-bar.md) | ✅ / ✗ | default · sticky · scrolled · mobile | logo `inline-start`, CTA `inline-end` | `flex items-center justify-between`; sticky `z=var(--z-sticky)` |
| [Hero](hero.md) | ✅ / ✗ | default · with-cta · scroll-cue | logical; decorative svg `aria-hidden` | brand surface `rounded-lg p-12 text-center` |
| [Site Footer](site-footer.md) | ✅ / ✗ | default · link states | logical; light links on dark | `bg-foreground text-background py-12` |

## Compositions (NOT components — built from the above)
- **Description list (`<dl>`)** inside Card — key/value facts.
- **Brand highlight mark** — brand background behind text (themes).
- **Numbered feature list** (01/02 …) — section-header + grid.
- *(Pagination graduated to a documented component in v1.1.5 — see Data above.)*

## Known gaps (missing entirely — `Spec ✗`)
- **Data visualization** (chart · sparkline · legend · axis · tooltip-on-hover) — not in the library. *(deferred)*
- **Tooltip / Popover** — referenced by Select/Table, no spec yet. *(deferred)*
> Closed in v1.1.5: **Spinner · Skeleton · Alert** (now documented) and **Pagination** (graduated from composition → component). Remaining gaps above are intentionally deferred.
