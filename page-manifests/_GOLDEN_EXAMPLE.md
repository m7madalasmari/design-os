# Page Manifest — Consultation Evaluation  *(GOLDEN EXAMPLE — reference only)*

> A worked, filled manifest the agent can imitate. Real page: `pages/consultation-evaluation.html`. QA report: `design-protocols/examples/golden-qa-report.md`.

- **Mode:** System Fidelity
- **Direction:** RTL (ar)
- **Theme:** theme-tuwaiq (action = purple `#4F29B7`)
- **Reference:** screenshot (Tuwaiq consultation evaluation form)

## Intent
Post-session consultation evaluation; capture rating + satisfaction + contact, one primary action (إرسال).

## Users
The consultee (logged-in), Arabic, on desktop or mobile.

## Primary Action (one)
«إرسال» — submit the evaluation.

## Secondary Actions
«الرجوع إلى المواعيد» (back link).

## Reference Analysis  *(observed/inferred/approximate/unknown)*
- Page type: form page — `observed`
- Layout: back link → header card (title+subtitle+pattern) → 2-col (form right / details left) — `observed`
- Grid & alignment: form 2fr / details 1fr; labels & headings `start` (right) — `observed`
- Spacing: generous; mapped to scale (~`space-lg` between fields) — `approximate`
- Typography: Tuwaiq → IBM Plex Sans Arabic; CSP fallback to system — `inferred`
- Color: purple action `#4F29B7` from Tuwaiq tokens — `inferred`
- Border radius: cards ~`radius-lg`, fields ~`radius-md` — `approximate`
- Shadows: soft card shadow — `observed`
- Components: rating, scale, inputs, stepper, button, card+dl — `observed`
- Icons: field icons at `inline-end`; details-card banner image — `observed`
- Content density: medium — `observed`
- RTL: full; numerals Latin; rating/scale fill from right — `observed`
- Ambiguous: required vs optional fields — `unknown` (not shown → no `*` invented)
- Selected states (2 stars / scale 6): image display state, not user data — `inferred`

## Components Used  *(check `components/INDEX.md`)*
- nav back-link, section-header, card (+ `<dl>` composition), input ×5, rating, scale, stepper, button.
- New components documented first: rating, scale, stepper. Theme: theme-tuwaiq.

## Data States
- Loading: skeleton for details card if async (static demo → skipped, documented).
- Empty: N/A page-level (form always renders).
- Filled: default.
- Error: details fetch error → empty-state error (out of static scope).
- No Permission: N/A (authed consultee).

## Content Rules
- All copy transcribed from the reference; no invented content; Latin numerals; date verbatim.

## Layout Rules
- Logical Tailwind utilities; token spacing; max content width; purple used sparingly (action + selected states only).

## Visual Polish and Motion
### Observed in Reference
- soft card shadow; selected (purple) states for stars/scale.
### Needed for This Page
- hover/active on rating/scale/stepper; focus-visible rings; subtle `transition-colors`.
### Not Needed
- SVG motifs, background pattern, scroll reveal, decorative motion (Form page type).
### Motion
- `transition-colors duration-150` on interactive elements; `motion-reduce` off.
### SVG / Illustration
- field icons only (functional). Empty-state: simple icon only (data app) — see `empty-state.md`.
### Interaction Feedback
- button hover/active, input focus-within ring, stepper/scale/rating hover + focus.
### Reduced Motion Handling
- `prefers-reduced-motion: reduce` disables all transitions.
### Performance Risks
- none significant (no images beyond substituted banner; inline SVG icons).

## Responsive Behavior
- Desktop: 2-col (form/details). Tablet: 2-col or stack. Mobile: single column, details below form.
- Form: fields full-width; stepper/scale wrap. Overflow: none. Sticky: none.

## Forbidden (this page)
- color outside tokens/theme; undocumented components; invented required markers; fabricated assets; arbitrary values; directional utilities in RTL; >1 primary.

## Out of Scope
- live submit/validation; original tech banner image; loaded Plex font (CSP).

## Done?  (per `design-protocols/07`)
- All DoD boxes checked; QA in the golden QA report; deviations documented (font fallback, substituted banner).
