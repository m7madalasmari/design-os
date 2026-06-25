# Component Backlog

> Documented-but-not-yet-specced components, prioritized. Adding any of these = a future `design-system` version (spec + INDEX + gallery). Check [`INDEX.md`](INDEX.md) before building; nothing here is approved for use until it has a spec.

## ✅ Shipped (out of backlog)
- **sidebar / app-shell nav** → [`sidebar.md`](sidebar.md) (v2.3.0 — request-portal dogfood proved it blocking for multi-page apps).
- **data-app header** → [`app-header.md`](app-header.md) (v2.3.0 — same dogfood).
- **avatar** → [`avatar.md`](avatar.md) (v2.1.1 — users-page dogfood).
- **detail-view / description-list** → [`detail-view.md`](detail-view.md) (v2.1.1 — was a loose composition; now a contract).
- Non-component closures: **inline-`style=` gate** (forbidden #18 + checks, v2.1.1), **filter-bar responsive contract** (v2.1.1), **modal/drawer footer order** (v2.1.1), **Visual Polish Gate** (6th gate, v2.2.0).

## Still deferred (need another test to prove necessity)
**textarea** (used in portal form via input rules; promote to *High next* — standalone auto-resize/counter) · breadcrumb (deeper paths) · radio/switch standalone · dark-mode tokens · data-viz · GitHub publish — **and the rows below.**

## Priority summary
| # | Component | Priority | Form | Gallery later |
|---|---|---|---|---|
| 1 | switch (toggle) | **High** | standalone (split from `checkbox.md`) | Yes |
| 2 | radio (group) | **High** | standalone (split from `checkbox.md`) | Yes |
| 3 | textarea | **High** | standalone (sibling of `input.md`) | Yes |
| 4 | action-menu | **High** | standalone (distinct from `select`) | Yes |
| 5 | breadcrumb | Medium | standalone (used by `page-header`) | Yes |
| 6 | chip / tag | Medium | standalone (used by `filter-bar`) | Yes |
| 7 | progress | Medium | standalone (pairs with `spinner`) | Yes |
| 8 | ~~avatar~~ | **✅ Done v2.1.1** | [`avatar.md`](avatar.md) | shipped |
| 9 | accordion | Medium | standalone | Yes |
| 10 | tooltip / popover | Medium | standalone (referenced by select/table) | Yes |
| 11 | date-picker | Low | standalone (composes calendar + input + popover) | Yes |
| 12 | data-viz | Low | set (chart · sparkline · legend · axis · tooltip) | Partial |

## Entries

### 1. switch (toggle) — High
- **Why:** instant on/off settings applied immediately (no "save"); currently only described as a sibling inside `checkbox.md`, no standalone contract.
- **Form:** standalone `switch.md`, split from `checkbox.md`.
- **Dependencies:** tokens (accent, control sizes); a11y `role="switch"` + `aria-checked` (`06`).
- **Gallery:** yes (states: on/off/disabled/focus).

### 2. radio (group) — High
- **Why:** single choice among 2–5 visible options; folded into `checkbox.md` as a sibling, no group/keyboard contract.
- **Form:** standalone `radio.md` (radiogroup).
- **Dependencies:** `06` (arrow-key roving, `role="radiogroup"`); tokens.
- **Gallery:** yes (group, selected, disabled, error).

### 3. textarea — High
- **Why:** multi-line input; `input.md` says "use textarea with the same rules" but there's no spec (auto-resize, rows, counter).
- **Form:** standalone `textarea.md` (sibling of `input.md`).
- **Dependencies:** input tokens; `06` (label/error wiring).
- **Gallery:** yes (default/focus/error/disabled).

### 4. action-menu — High
- **Why:** the "more" (⋯) trigger implies a menu of row/page actions; distinct from `select` (actions, not value selection). No spec → ambiguous.
- **Form:** standalone `action-menu.md`.
- **Dependencies:** popover/tooltip layer (#10), `06` (menu keyboard: ↑↓/Esc/typeahead, `role="menu"`), `--z-dropdown`.
- **Gallery:** yes (closed/open/disabled item).

### 5. breadcrumb — Medium
- **Why:** `page-header` references a `with-breadcrumb` state but there's no standalone spec (separator mirroring in RTL, current-page).
- **Form:** standalone `breadcrumb.md` (consumed by `page-header`).
- **Dependencies:** `04`/`06` (directional separator, `aria-current`).
- **Gallery:** yes.

### 6. chip / tag — Medium
- **Why:** `filter-bar` uses applied-filter chips; status/labels reuse the pattern; no standalone contract (removable, sizes).
- **Form:** standalone `chip.md` (used by `filter-bar`).
- **Dependencies:** tokens (subtle bg/border, radius-sm); `06` (removable chip is a labelled button).
- **Gallery:** yes (default/removable/selected).

### 7. progress — Medium
- **Why:** determinate progress for long operations; `spinner` covers short/indeterminate only.
- **Form:** standalone `progress.md` (linear; pairs with `spinner.md`).
- **Dependencies:** tokens; `06` (`role="progressbar"`, `aria-valuenow`); reduced motion.
- **Gallery:** yes (determinate/indeterminate).

### 8. avatar — Medium
- **Why:** user/account representation (image/initials/fallback); referenced by skeleton-avatar; no spec.
- **Form:** standalone `avatar.md`.
- **Dependencies:** tokens (radius-full, sizes); `06` (alt text / labelled).
- **Gallery:** yes (image/initials/sizes).

### 9. accordion — Medium
- **Why:** progressive disclosure for long forms/FAQ/dense detail; not covered (Tabs ≠ accordion).
- **Form:** standalone `accordion.md`.
- **Dependencies:** `06` (`aria-expanded`, keyboard); motion tokens.
- **Gallery:** yes (collapsed/expanded).

### 10. tooltip / popover — Medium
- **Why:** referenced by `select`/`table` (hints, helper, on-hover); a foundational layer for action-menu/date-picker.
- **Form:** standalone `tooltip.md` + `popover.md` (or one spec, two modes).
- **Dependencies:** `--z-dropdown`, `--shadow-md`; `06` (hover+focus+`Esc`, `aria-describedby`, not keyboard-trap).
- **Gallery:** yes.

### 11. date-picker — Low
- **Why:** date selection beyond a text field; calendar icon + date inputs exist but no picker.
- **Form:** standalone `date-picker.md` (composes calendar grid + input + popover #10).
- **Dependencies:** popover (#10), `04` (Hijri/Gregorian locale, numerals), `06` (grid keyboard).
- **Gallery:** yes.

### 12. data-viz — Low
- **Why:** dashboards need charts/sparklines/legends; explicitly out of the current library.
- **Form:** a **set** (chart · sparkline · legend · axis · tooltip) — likely a sub-section, not one spec.
- **Dependencies:** tooltip (#10), tokens (status/accent), `06` (non-color encoding, table fallback, labels).
- **Gallery:** partial (static examples only).
