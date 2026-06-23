# AGENTS.md

You are working on a UI project where **visual references, design-system rules, and page manifests are treated as source-of-truth documents**. Read them before implementing any UI task — never implement from memory.

## Read first (in this order)

1. `design-protocols/00-operating-rules.md` ← start here
2. `design-protocols/01-image-to-ui-replication.md`
3. `design-protocols/02-design-system-ssot.md`
4. `design-protocols/03-pixel-qa.md`
5. `design-protocols/04-arabic-rtl-ux.md`
6. `design-protocols/05-visual-polish-and-motion.md`
7. `design-protocols/06-accessibility.md` — a11y baseline (WCAG AA), runs on every task
8. `design-protocols/07-definition-of-done.md`
9. `design-protocols/08-app-shell-and-routing-consistency.md`
10. `design-protocols/09-spa-build-standards.md` — **conditional: SPA build tasks only** (see *Engineering layer* below)
11. `design-system/` (README → foundations → components → rules → themes)
12. `page-manifests/` (the contract for the specific page)

If a referenced file is missing, say so — do not guess its contents.

## Engineering layer — `09` SPA Build Standards (conditional)
`00–08` are the design layer. [`09-spa-build-standards.md`](design-protocols/09-spa-build-standards.md) is a **separate engineering layer** with a pinned stack and technical architecture.

**Use `09` only when the task involves:**
- creating a new SPA,
- building a Vite + React app,
- preparing code for team handover,
- implementing production-ready pages inside a real app,
- integrating with a future Nx monorepo.

**Do not apply the full SPA build standards to lightweight design playgrounds unless explicitly requested.**

**Trigger phrases → activate `09`:** "build app" · "create SPA" · "Vite React" · "production-ready" · "handover" · "Nx monorepo" · "team standards" · "implement as real app". When `09` is active, completion is gated by the **Engineering Definition of Done** in [`07`](design-protocols/07-definition-of-done.md).

## Stack: Tailwind-first
This is a **Tailwind-first** project. Implement UI with Tailwind utility classes bound to the design tokens (Tailwind `theme` keys / CSS variables — per the project's setup). Do not build a separate CSS system.
- Default to **semantic token classes**: `bg-background` · `text-foreground` · `text-muted-foreground` · `border-border` · `bg-primary` (+ `text-primary-foreground`) · `rounded-lg`/`rounded-xl` · `p-4`/`p-6` · `gap-4`/`gap-6`.
- Use Tailwind's standard scale (its 4px spacing scale **is** the system's 4px base). **Avoid arbitrary values** (`bg-[#…]`, `p-[…]`, `rounded-[…]`, …).
- RTL: **logical utilities only** (`ms/me`, `ps/pe`, `start/end`, `text-start/text-end`) — never `ml/mr`, `left/right`, `text-left/right`.

Full rules: `00-operating-rules.md`. Arbitrary-value exception (Pixel Clone only): `01-image-to-ui-replication.md`.

## Modes (choose one before implementing; state it explicitly)

| Mode | Priority on conflict | Use when |
|------|----------------------|----------|
| **Auto** *(meta)* | resolves to one of the below | you don't want to pick; the agent decides from the inputs (see *Auto Mode*) |
| **Pixel Clone** | reference image **>** system | user wants an exact copy of the image |
| **System Fidelity** *(default)* | match reference **within** the system | "implement / build this design" |
| **Strict SSOT** | system **>** reference | system consistency matters most |
| **Improved** | reference **+** justified UX/a11y fixes | user explicitly asks to improve it |
| **Greenfield / System-First** | **system is the only source** (no reference) | no image / no prior design; build from a description |

Default is **System Fidelity** unless the user says otherwise. Announce the chosen mode before building.
**No visual reference?** System Fidelity *collapses into* **Greenfield / System-First**: the design system, component inventory, and UX clarity become the contract — priority **user intent → design system → component inventory → UX clarity → visual-polish rules**. **Pixel QA does not apply unless a reference image exists.**

### Auto Mode (default for one-shot runs)
If the request says `Mode: Auto` (or doesn't specify a mode), resolve it from the inputs:

| Inputs | Resolved mode |
|---|---|
| Image **+** "match / copy exactly" | **Pixel Clone** |
| Image **+** "apply within the system" | **System Fidelity** |
| No image **+** description only | **Greenfield / System-First** |
| Review only (no build) | **Strict SSOT — Review** (audit; list every conflict) |
| "Improve / enhance" an existing design | **Improved** |
| Build a full app | **SPA Build Standards (`09`) + Greenfield** |

Announce the resolved mode before building. **Ask only when a gap blocks implementation or changes a core decision; otherwise proceed with documented assumptions** (Ask-vs-Assume, [`00`](design-protocols/00-operating-rules.md)). For the full request→delivery flow and the one-shot prompt, see [`RUNBOOK.md`](RUNBOOK.md) (intake [`REQUEST.md`](REQUEST.md) · delivery [`OUTPUT.md`](OUTPUT.md)).

## Default Workflow

For any UI design, redesign, screenshot-to-code, page, component, dashboard, form, or UX-writing task:

1. Do not start implementation immediately.
2. Identify the required mode (table above).
3. If the user provides an image, treat it as a **visual contract, not inspiration**.
4. Create or update a page manifest in `page-manifests/` before implementation.
5. Map the UI to existing design-system tokens and components when applicable.
6. **Pixel Clone Mode** → prioritize reference-image fidelity over the design system.
7. **System Fidelity Mode** → match the reference as closely as the design system allows.
8. **Strict SSOT Mode** → prioritize the design system over the reference.
9. Never invent missing content silently.
10. Never add extra sections, cards, metrics, or decorative elements unless requested.
11. After implementation, run QA (`03-pixel-qa.md`) and document mismatches.

## Adding to the system

If a task needs a component or token that does not exist, **document it in `design-system/` first** (with its rationale), then use it. Brand changes go through a theme (`design-system/themes/`), not into components. Never use an undocumented component or value.

## Visual Polish Requirement

For any UI task, after layout and component implementation, run a **Visual Enhancement Audit**.

Check:
- SVG details
- Motion
- Micro-interactions
- Loading states
- Empty states
- Hover/focus/active states
- Surface depth
- Data visualization polish

Do not add decoration randomly. Every enhancement must serve a purpose (clarify hierarchy · improve feedback · brand expression · perceived quality · orientation · clearer empty/loading states · easier data).

- In **Pixel Clone Mode**, only reproduce visible or explicitly requested visual effects.
- In **Improved Mode**, actively propose polish and motion improvements.

Detailed protocol: [`design-protocols/05-visual-polish-and-motion.md`](design-protocols/05-visual-polish-and-motion.md). Report its output during QA (`03`).

## Done & token source
- **Do not mark any UI task as complete unless it passes the Definition of Done** ([`07`](design-protocols/07-definition-of-done.md)).
- **The agent must identify the executable token source before changing UI** — `design-system/tokens.css` (Tailwind v4 `@theme`) or the project's Tailwind theme. `tokens.md` is documentation, not the runtime source. If none exists, create or propose one (without touching product pages). See [`02`](design-protocols/02-design-system-ssot.md).
- **Focus ring and text links are decoupled from the brand accent** — never map `--color-focus-ring` / `--color-text-link` to a light accent without verifying contrast.
- A page must not introduce a new shell / navigation / layout rhythm unless requested ([`08`](design-protocols/08-app-shell-and-routing-consistency.md)).

## Non-Negotiable Constraints

Do not:

* Use random hex values unless Pixel Clone Mode requires them.
* Use random px values unless Pixel Clone Mode requires them.
* Add fake data, fake metrics, or fake actions.
* Redesign the reference image when the user asked for replication.
* Replace the user's visual intent with a generic AI/SaaS layout.
* Ignore RTL when the interface is Arabic.
* Fix unrelated parts of the project.
* Refactor unrelated code.
* Use arbitrary Tailwind values (`bg-[#…]`, `text-[#…]`, `border-[#…]`, `p-[…]`, `m-[…]`, `gap-[…]`, `rounded-[…]`, `shadow-[…]`, `w-[…]`, `h-[…]`) outside Pixel Clone Mode.
* Use directional utilities (`ml-*`, `mr-*`, `left-*`, `right-*`, `text-left`/`text-right`) in RTL — use logical utilities instead.

Always:

* Preserve the user's intent.
* Keep changes scoped.
* Document assumptions.
* Document conflicts.
* Document what was changed.
* Report visual mismatches after implementation.
