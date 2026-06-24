# ROLES.md — the design-os review council

> A lightweight set of **mindsets the agent wears while passing over the work** — not extra
> agents, not a debate. The protocols (`00–09`) are the *rulebooks*; the roles are *who is
> accountable* for each one: who notices a rule is being broken, who owns a gate, and who
> arbitrates when two rules collide.
>
> **The point is a fast pass through the project with each role's mindset — not a long discussion.**

## The model: two levels

- **Level 1 — Operating Roles (9).** The only voices that run in the sweep. Each can *disagree* with
  another role and force an arbitration. Each emits one line per pass: `pass` or `flag: <what + where>`.
- **Level 2 — Checklists.** The detailed concerns live *inside* a role as its internal scan. A
  checklist item is **not** a separate voice — it's how a role decides its single verdict.

### Separation rule (Operating Role vs Checklist Item)
> **If it can disagree with another role and needs arbitration → it is an Operating Role.**
> **If it is just a dimension of verification inside a larger role → it is a Checklist Item.**

Test it: *Contrast Reviewer* and *ARIA Reviewer* never disagree — both serve Accessibility → checklist
items. *Visual & Experience Design* (wants a warm brand hero) and *Accessibility* (contrast floor) **can**
disagree → two Operating Roles, resolved by precedence.

### Output stance (anti-generic — governs every sweep)
> **Do not stack components. Compose the experience around the primary task.**
> **Reject generic / default UI** — the result must show hierarchy, rhythm, depth, and purposeful polish.

Owned operationally by **UX & Information Architecture** (structure the layout around the primary task)
and **Visual & Experience Design** (hierarchy, rhythm, depth, polish — no default look). A page that is a
flat stack of default cards **fails the sweep even if every component is individually valid.**

---

## Level 1 — Operating Roles

| # | Operating Role | Rulebook | Phase |
|---|----------------|----------|-------|
| 1 | Product & Strategy | `00` · RUNBOOK · REQUEST | Think (+ tiebreak) |
| 2 | UX & Information Architecture | `08` · page-manifests · `05` (states) · `06` (focus order) | Think → Build |
| 3 | Visual & Experience Design | `05` · tokens application · brand-foundation | Build → Review |
| 4 | Design System | `02` · `design-system/` | all |
| 5 | Content & UX Writing | `04` · `00` (no invented data) | Build → Review |
| 6 | Accessibility | `06` · `04` | Review (constrains Build) — **hard floor** |
| 7 | Frontend & Implementation | `00` (stack) · `09` (conditional) · `08` | Build |
| 8 | QA & Validation | `03` | Review |
| 9 | Documentation & Handoff | `07` · OUTPUT | Close |

---

### 1. Product & Strategy
- **Purpose:** ensure we are building the *right thing*, for the real intent, within scope.
- **Owns:** intent, scope boundary, Mode resolution, the **Ask-vs-Assume** gate, prioritization.
- **Decisions it can challenge:** "this section/metric/action wasn't requested"; "wrong Mode"; "this
  must be asked before building"; "this isn't the user's actual problem"; "out of scope for this task."
- **Checklist:**
  - *Business Analyst* — the problem and outcome are clear and worth solving.
  - *Scope Manager* — nothing built beyond the request (no extra sections/metrics/actions). Judge
    scope against the **template-vs-consumer** context (RUNBOOK · README): a demo/states block is
    legitimate in a `playground/` fixture but is scope creep in a consumer product page.
  - *Requirements Clarifier* — ambiguities resolved via Ask-vs-Assume: ask only when a gap blocks or
    changes a core decision; otherwise proceed with a **documented** assumption (`observed / inferred /
    approximate / unknown`).
  - *Prioritization Lead* — must-haves done before nice-to-haves.
- **Output in manifest:** *Intent · Mode · Primary/Secondary Action · Out of Scope · Implementation
  assumptions (labeled)*.
- **Anti-patterns:** scope creep; silent assumptions; solving the wrong problem; interrogating the
  user for things that can be assumed-and-documented.

### 2. UX & Information Architecture
- **Purpose:** structure, flows, and state coverage are complete and logical.
- **Owns:** information architecture, user/task flows, navigation & shell consistency, the manifest's
  structure, completeness of states. **Composes the layout around the primary task — never a generic
  stack of components** (see *Output stance*). **Owns interaction *behavior and task flow*** (polish belongs to Visual).
- **Decisions it can challenge:** "a state is missing (empty/loading/error/edge)"; "the hierarchy
  buries the primary action"; "this breaks the app-shell/nav rhythm"; "the flow has a dead end."
- **Checklist:**
  - *User Flow Designer* — entry → task → success/failure paths all defined.
  - *Information Architect* — grouping, labels, hierarchy reflect the content model.
  - *Interaction Designer (behavior)* — what each control *does* on click/submit/error is defined.
  - *Task Flow Reviewer* — no dead ends; back / cancel / empty paths exist.
- **Output in manifest:** *Reference Analysis (layout/regions) · Data States · Responsive Behavior ·
  Components Used*.
- **Anti-patterns:** happy-path only; missing empty/error states; inventing a new shell/nav without
  need; hierarchy that hides the primary task; stacking components instead of composing around the task.

### 3. Visual & Experience Design
- **Purpose:** composition, rhythm, and polish at quality — and on-brand. **Reject generic / default
  UI; demand hierarchy, rhythm, depth, and purposeful polish** (see *Output stance*).
- **Owns:** visual composition, layout rhythm, spacing/type-scale application, brand expression.
  **Owns interaction *polish, motion, and perceived quality*** (behavior belongs to UX).
- **Decisions it can challenge:** "spacing breaks the 4px rhythm"; "brand misused (warm promoted to
  primary; 60-30-10 violated)"; "this reads as generic AI-SaaS"; "this is a flat stack of default
  components with no hierarchy/depth"; "feedback/motion missing here."
- **Checklist:**
  - *UI Composition Designer* — alignment, grouping, balance hold across breakpoints.
  - *Layout & Rhythm Designer* — spacing/type on the system scale, no drift.
  - *Interaction Polish Designer (polish/motion)* — hover/focus/active feedback, transitions, micro-interactions.
  - *Premium Experience Reviewer* — surface depth, empty/loading polish, no template feel; brand
    60-30-10 respected, warm as a *second* hero, no emoji / AI-template aesthetic.
- **Output in manifest:** *Visual Polish and Motion (all sub-sections) · brand application*.
- **Anti-patterns:** decoration without purpose; brand color as primary; arbitrary spacing; motion
  that fights reduced-motion.

### 4. Design System
- **Purpose:** every value and block comes from the system.
- **Owns:** tokens, component specs, patterns, document-before-use, brand-via-theme.
- **Decisions it can challenge:** "arbitrary value used"; "undocumented component/token"; "brand
  hard-coded into a component instead of a theme"; "used before documenting."
- **Checklist:**
  - *Token Guardian* — colors/spacing/radius/shadow are tokens; no arbitrary values (Pixel-Clone
    exception documented).
  - *Component Spec Owner* — components map to `INDEX`; any new one documented first.
  - *Pattern Owner* — composition follows the documented patterns/rules.
  - *RTL Design Reviewer (cross-cutting · `04`)* — logical structure & mirrored layout decisions at the
    design level.
- **Output in manifest:** *Components Used · Token Var Exceptions · Forbidden (this page)*.
- **Anti-patterns:** arbitrary values; undocumented one-offs; brand baked into components; bypassing `INDEX`.

### 5. Content & UX Writing
- **Purpose:** copy is clear, correct Arabic, and real.
- **Owns:** microcopy, labels, error/empty text, tone, Arabic correctness, numeral-system
  consistency, **no fabricated data**.
- **Decisions it can challenge:** "fake/placeholder data shown as real"; "label is vague"; "tone is
  off"; "English leaking into an Arabic UI"; "mixed numeral systems."
- **Checklist:**
  - *Arabic UX Writer (cross-cutting · `04`)* — correct, natural Arabic; one numeral system; RTL-correct punctuation.
  - *Error & Empty State Writer* — every error/empty has helpful, specific text.
  - *Form Labels Reviewer* — labels, hints, validation messages clear and consistent.
  - *Microcopy Reviewer* — buttons/tooltips/states concise and action-oriented.
- **Output in manifest:** *Content Rules · Demo Data Policy*.
- **Anti-patterns:** lorem/placeholder shown as real; fabricated records/metrics; vague "Error
  occurred"; English fallbacks in an Arabic UI.

### 6. Accessibility  *(hard floor)*
- **Purpose:** works for keyboard, screen reader, and low vision.
- **Owns:** the WCAG-AA floor — contrast, focus, keyboard, ARIA, reduced motion, accessible RTL.
- **Decisions it can challenge:** anything below the AA floor — and **it cannot be overruled by brand
  or fidelity** (see Precedence).
- **Checklist:**
  - *Keyboard Navigation Reviewer* — every control reachable & operable by keyboard, logical order.
  - *Focus Management Reviewer* — visible focus; focus trap on modal/drawer; focus returns on close.
  - *Contrast Reviewer* — text/UI meets AA; focus-ring & links not mapped to a low-contrast accent.
  - *ARIA & Semantic HTML Reviewer* — correct roles/names/states; semantic elements first.
- **Output in manifest:** *Reference Analysis (color → contrast) · Post-implementation QA (`06`)*.
- **Anti-patterns:** trading contrast/focus for brand; div-buttons; focus traps without escape; motion
  ignoring reduced-motion.

### 7. Frontend & Implementation
- **Purpose:** implementation is Tailwind-first, RTL-logical, well-structured, and (SPA) on the pinned stack.
- **Owns:** Tailwind-first implementation, logical RTL utilities, component composition, responsive
  implementation, **performance budget**, SPA structure (`09`).
- **Decisions it can challenge:** "directional utilities in RTL"; "a separate CSS layer"; "arbitrary
  values"; "component not composed/reused"; "(SPA) off the pinned stack/structure"; "performance budget at risk."
- **Checklist:**
  - *React Architect* — composition, reuse, state handling (SPA → `09` stack/structure).
  - *Tailwind Implementation Reviewer* — semantic token classes; no arbitrary values; no parallel CSS.
  - *Responsive Layout Reviewer* — layout holds across breakpoints.
  - *RTL Implementation Reviewer (cross-cutting · `04`)* — logical utilities only (`ms/me`, `ps/pe`,
    `start/end`); never `ml/mr` / `left/right`.
  - *Performance Reviewer (cross-cutting · `09`)* — bundle size, lazy pages, image weight, avoidable
    re-renders. **Checklist item, not a standalone role; enforced as a gate only on SPA tasks.**
- **Output in manifest:** *Preview runtime · Responsive Behavior · Performance Risks*.
- **Anti-patterns:** `ml/mr`/`left/right` in RTL; `bg-[#…]` etc.; a second CSS system; copy-pasted
  components; (SPA) deviating from `09`.

### 8. QA & Validation
- **Purpose:** matches the contract (reference/manifest) across sizes and states.
- **Owns:** pixel QA vs reference (if any), responsive QA, component-state QA, edge-case QA, the QA report.
- **Decisions it can challenge:** "doesn't match the reference here"; "breaks at this breakpoint";
  "this state is wrong/missing"; "regression"; "diverges from the manifest."
- **Checklist:**
  - *Visual QA Reviewer* — matches reference/manifest; spacing/type/color correct.
  - *RTL QA Reviewer (cross-cutting · `04`)* — mirrored layout, alignment, icon direction correct in RTL.
  - *Component QA Reviewer* — each component renders all required states.
  - *Edge Case Reviewer* — long text, empty, overflow, error, slow network.
- **Output in manifest:** *Post-implementation (QA Report Location · Preview runtime)*.
- **Anti-patterns:** "looks fine" without checking states/breakpoints; skipping RTL QA; passing
  partial work as complete.

### 9. Documentation & Handoff
- **Purpose:** documented and *truly* done.
- **Owns:** Definition-of-Done sign-off, manifest finalization, changelog, release readiness,
  developer handover.
- **Decisions it can challenge:** "a DoD box is unchecked"; "manifest/QA location missing"; "no
  known-limitations/next-actions"; "not release-ready."
- **Checklist:**
  - *Manifest Owner* — manifest complete and matches what was built.
  - *Change Log Owner* — change recorded (what / why / affected / re-QA?) when versioned.
  - *Release Reviewer* — semver + git-tag policy followed if it's a release (`VERSION.md`).
  - *Developer Handoff Reviewer* — `OUTPUT.md` filled: files changed, preview, limitations, next actions.
- **Output in manifest:** *Post-implementation · the `OUTPUT.md` handover*.
- **Anti-patterns:** marking done with unchecked boxes; missing manifest/QA; presenting partial work
  as complete.

---

## Level 2 — how checklists work
- A checklist is the role's **internal scan**, not separate voices. The role emits **one** `pass` /
  `flag` line for itself; the checklist is how it reaches that verdict.
- The 45 named reviewers above are **checklist items**, never runtime voices. The org chart can show
  45 boxes; the runtime sweep is at most **9**.
- **Cross-cutting items** (RTL, Performance) appear under several roles by design — each from its own
  angle — but are **governed by one protocol** so there is a single source of truth.

## Cross-cutting resolutions
1. **RTL is not a role.** It is a cross-cutting checklist item under **Design System**, **Content & UX
   Writing**, **Frontend & Implementation**, and **QA & Validation**, governed by **`04`**.
2. **Interaction splits cleanly:** **UX & IA owns behavior and task flow**; **Visual & Experience owns
   polish, motion, and perceived quality**.
3. **Performance is not a standalone role now.** Checklist item under **Frontend & Implementation**,
   tied to **`09`**; enforced as a gate only on SPA tasks.
4. **Requirements Clarifier is not a role.** Checklist item under **Product & Strategy** (the
   Ask-vs-Assume gate).
5. **Manifest / Changelog / Release / Handoff are not roles.** All checklist items under
   **Documentation & Handoff**.

## How to run a role sweep
A sweep is a fast pass, not a meeting. Order: **Fast sweep → Gates → remaining roles → manifest.**

**1 · Fast sweep — 3 roles, on every task.** They *shape* the work; each emits one line with a defined output:

| Role | Output (one line) |
|------|-------------------|
| Product & Strategy | intent · scope · primary action |
| UX & Information Architecture | structure · task flow · states |
| Visual & Experience Design | composition · rhythm · polish risk |

**2 · Gates — five checkpoints that cannot be skipped** (full reference: `design-system/rules/quality-gates.md`):
- **Design System Gate** — *before implementation is valid.* No arbitrary values; every block mapped to
  `INDEX`; anything new documented first (`02`); brand applied as a full ramp cascade, not a primary swap
  (`color-system`). RUNBOOK step 7.
- **Typography Gate** — *before delivery.* IBM Plex Sans Arabic loaded & applied (or a brand theme
  explicitly requested + documented), type scale applied, Arabic body 1.7; no Tajawal/Inter/browser-default
  (`typography-system`).
- **Component Quality Gate** — *before a component is done.* Meets acceptance criteria (states · RTL · no
  clutter · one primary · token bindings) **and** is the right component for the job
  (`component-quality-gate`). Per component during build/review.
- **Anti-Generic Gate** — *before delivery.* Page passes `anti-bland-ui-rules` (measurable hierarchy ≥2
  signals · ≥2 spacing relationships · grid varies by content · composition matches page type · presentation
  matches content). A bland-but-valid page fails. Promotes the *Output stance* from mindset to gate.
- **Accessibility Gate** — *before delivery is acceptable.* WCAG-AA floor: contrast · keyboard · focus ·
  ARIA · reduced motion (`06`). RUNBOOK step 9.

All five are **hard floors** — never traded for brand or fidelity (see *Precedence*; Accessibility and
clarity outrank Anti-Generic). A failed gate **blocks the pipeline**; it is not a flag to weigh.

**3 · Remaining roles — run as validation when there is something to validate.** Content, Frontend, QA,
and Documentation scale with the task (a one-component tweak may not need Documentation).

**4 · Write it to the manifest.** Each verdict and flag lands in the role's mapped section (see each
role's *Output in manifest*); the Accessibility Gate fills *Accessibility Notes*.

### Rules of the sweep
- **Full sweep = 9 roles maximum** — the 45 are checklists, not voices.
- Each role emits one `pass` / `flag: <what + where>` line; roles only "talk" on conflict.
- **One finding, one owner** — a detail seen by several lenses is logged once, under the role that owns
  the *rule* it breaks (Design System for an undocumented value, Accessibility for a contrast failure, …).
  Other roles reference it; they do not re-report it. Keeps the sweep terse.

## Precedence (on conflict — Product & Strategy breaks remaining ties)
1. **User intent / chosen Mode**
2. **Accessibility hard floor** — contrast, focus, keyboard. *Never* traded for brand or fidelity
   (matches the focus-ring / text-link decoupling in `AGENTS.md`).
3. **Design-system SSOT** (`02`)
4. **Reference fidelity** — per the active Mode (`01`)
5. **Visual polish** (`05`)
