# 06 — Accessibility

> The accessibility baseline for every UI task. `04` covers Arabic/RTL specifics; this file is the **general a11y contract** that applies to all interfaces. Component specs hold per-component a11y rules; this protocol governs how they're applied and verified. Target: **WCAG 2.1 AA**.

## When to apply
**Always** — accessibility is not optional and not a "polish" add-on. Every page/component task runs the Accessibility QA in this file (gated by [`07`](07-definition-of-done.md)). It composes with `04` (RTL) and `05` (motion).

## 1. Semantic HTML first
- Use the right element for the job: `<button>` for actions, `<a>` for navigation, `<nav>/<main>/<header>/<footer>/<section>`, `<table>` for tabular data, `<ul>/<ol>/<dl>`, headings `<h1>`–`<h6>`.
- **One `<h1>` per page**; heading levels nest without skipping (h2→h3, never h2→h4). Empty-state titles are real headings (see [`empty-state.md`](../design-system/components/empty-state.md)).
- Never `<div onClick>` as a button; never a clickable `<span>`. ARIA is a last resort — prefer native semantics.

## 2. Keyboard navigation
- **Everything interactive is reachable and operable by keyboard** (Tab/Shift+Tab, Enter/Space, arrows where applicable).
- Logical **focus order** follows the visual/reading order (RTL: right→left, top→bottom).
- No keyboard traps (except an intentional, escapable modal focus trap — §4).
- Composite widgets use the expected keys: Tabs (arrows + Home/End), Select/listbox (↑↓/Home/End/type-ahead/Esc), Menu, Stepper, Rating, Scale — per each component spec.
- Don't override native keys; don't use positive `tabindex` (only `0`/`-1`).

## 3. Focus: visible · order · management
- **Focus-visible is mandatory** and uses the token ring (`--shadow-focus` / `--color-focus-ring`) — **never remove the outline without a replacement** (forbidden). Decoupled from accent (a light accent must not weaken the ring).
- **Focus management:** on route change move focus to the main heading/region; after closing an overlay, **return focus to the trigger**; after deleting a row, move focus to a sensible neighbor.
- **Focus trap (modal/drawer):** while open, Tab cycles **within** the overlay; `Esc` closes; focus returns to the opener. Background is inert (`aria-hidden`/`inert`). See [`modal.md`](../design-system/components/modal.md) / [`drawer.md`](../design-system/components/drawer.md).

## 4. ARIA: roles, names, states
- Prefer semantics; add ARIA only to fill gaps. Don't duplicate native roles.
- **Accessible name** for every control: visible label, `aria-label`, or `aria-labelledby`. Icon-only controls **require** an Arabic `aria-label` ([`icon-system.md`](../design-system/foundations/icon-system.md)).
- Reflect **state**: `aria-expanded`, `aria-selected`, `aria-checked`, `aria-current`, `aria-disabled`, `aria-invalid`, `aria-busy` — kept in sync with the visual state.
- Overlays: `role="dialog"` + `aria-modal="true"` + a labelled title.

## 5. Forms: labels, validation, errors
- **Label always visible above the field** (never placeholder-as-label). Placeholder = format example only.
- Associate label↔field (`<label for>`/wrapping); group related fields with `<fieldset>`/`legend` or `role="group"`.
- Errors: `aria-invalid="true"` + error text linked via `aria-describedby`; the message is **persistent, no layout jump**, and says what + how to fix (`04`). Required marked consistently (`*` or "(اختياري)").
- Validate on blur/submit, not every keystroke.

## 6. Color & contrast
- Text/UI must meet **AA**: body text ≥ 4.5:1, large text/UI components/focus indicator ≥ 3:1. Use the documented token pairs ([`tokens.md` §2](../design-system/foundations/tokens.md)); `text-tertiary` is for large/decorative only (≈3.4:1 — never body).
- **Never encode meaning by color alone** — pair with text/icon/shape (status badges = dot **and** text; chart series get labels/patterns).

## 7. Motion & reduced motion
- Honor `prefers-reduced-motion: reduce`: disable non-essential animation (skeleton pulse, spinners reduce, transitions ~0). Motion must never be the only way info is conveyed. See [`05`](05-visual-polish-and-motion.md).

## 8. Screen-reader support
- Meaningful reading order in the DOM (don't rely on CSS order to fix it).
- Decorative icons/images `aria-hidden="true"`; meaningful ones have text alternatives.
- Visually-hidden helper text (`.sr-only`) where context needs it; don't hide essential text from SR.
- **Live regions:** `aria-live="polite"` for status, `role="alert"`/`aria-live="assertive"` for critical errors.

## 9. Accessible loading states
- Loading region: `aria-busy="true"`; skeletons are `aria-hidden` placeholders with a SR text ("جارٍ التحميل") — see [`skeleton.md`](../design-system/components/skeleton.md).
- Spinner: decorative → `aria-hidden`; if it alone conveys loading → `role="status"` + label ([`spinner.md`](../design-system/components/spinner.md)).
- Don't strand the user: every loading resolves to content, empty, or an error state.

## 10. Alerts & toasts
- **Critical/error** that appears dynamically → `role="alert"` (assertive), injected into the DOM on occurrence ([`alert.md`](../design-system/components/alert.md)).
- **Non-critical** status → `role="status"` / `aria-live="polite"`.
- **Toast** → `aria-live` region; never the *only* place a critical message appears; dismissible and not auto-hidden too fast to read ([`toast.md`](../design-system/components/toast.md)).

## 11. Accessible tables
- Real `<table>` with `<thead>/<tbody>`, `<th scope="col|row">`, and a caption or labelled region.
- Sort: `aria-sort` on the active column header; the sort control is a real `<button>` (no native-button chrome — see [`table.md`](../design-system/components/table.md)).
- Selection: row checkboxes have accessible names; header checkbox supports `indeterminate`.
- Horizontal scroll containers are keyboard-scrollable and labelled; never silently clip columns.

## 12. RTL accessibility
- `dir="rtl"` + `lang="ar"`; focus/arrow order follows reading direction; directional icons mirror; numerals/IDs bidi-isolated. Full rules in [`04`](04-arabic-rtl-ux.md).

## 13. Icon accessibility
- Decorative → `aria-hidden="true"`; meaningful → accessible name; never meaning-by-icon-alone without text. Sizes via tokens; directional icons mirror in RTL ([`icon-system.md`](../design-system/foundations/icon-system.md)).

## Do / Don't
**Do:** native elements · visible focus ring (token) · labels above fields · `aria-*` synced to state · return focus on close · contrast ≥ AA · respect reduced motion · `role=alert` for critical errors.
**Don't:** `<div>` buttons · remove outline with no replacement · placeholder-as-label · color-only meaning · positive `tabindex` · keyboard traps (non-modal) · auto-hide critical messages · icon-only controls without a label.

## Accessibility QA checklist  (run every task — manual, no tooling)
- [ ] Semantic elements; one `<h1>`; headings don't skip levels.
- [ ] All interactive elements keyboard-reachable & operable; logical focus order; no non-modal traps.
- [ ] Focus-visible present everywhere (token ring); outline never removed without replacement.
- [ ] Modal/drawer trap focus, `Esc` closes, focus returns to trigger; background inert.
- [ ] Every control has an accessible name; icon-only controls labelled (Arabic).
- [ ] States exposed (`aria-expanded/selected/checked/current/invalid/busy/disabled`).
- [ ] Form labels visible above; errors linked (`aria-describedby`) + `aria-invalid`; no layout jump.
- [ ] Contrast ≥ AA (token pairs); no meaning by color alone.
- [ ] `prefers-reduced-motion` respected.
- [ ] Loading uses `aria-busy`; resolves to content/empty/error; skeleton/spinner labelled correctly.
- [ ] Critical errors `role=alert`; status `role=status`/`aria-live=polite`.
- [ ] Tables: `th scope`, `aria-sort`, labelled, scrollable not clipped.
- [ ] RTL: `dir`/`lang`, mirrored directional icons, bidi-isolated numerals.

**Gate:** any failed line blocks completion (`07`). This checklist is part of the Definition of Done for every interface.
