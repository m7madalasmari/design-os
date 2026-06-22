# 00 — Operating Rules

> The operating constitution. Read first, before any UI task. `AGENTS.md` is the index; this file is the detailed contract. Design rules live in `design-system/`; this file governs **how** the agent works, not what the tokens are.

## Source of truth & precedence
Visual references + `design-system/` + `page-manifests/` are source-of-truth. Never implement from memory or before reading them. If a referenced file is missing, say so — do not guess its contents.

## Read order (before any UI task)
1. `00-operating-rules.md` (this file)
2. `01-image-to-ui-replication.md`
3. `02-design-system-ssot.md`
4. `03-pixel-qa.md`
5. `04-arabic-rtl-ux.md`
6. `05-visual-polish-and-motion.md`
7. `07-definition-of-done.md`
8. `08-app-shell-and-routing-consistency.md`
9. `design-system/README.md` → foundations → components → rules → themes
10. `page-manifests/<page>.md`

## Pick a mode (announce it before building)
**Pixel Clone · System Fidelity (default) · Strict SSOT · Improved.**
Detection phrases and per-mode behavior: see [`01-image-to-ui-replication.md`](01-image-to-ui-replication.md). Default is **System Fidelity** unless the user signals otherwise.

## Mandatory sequence
1. Do not implement immediately.
2. Identify and **state** the mode.
3. Treat any reference image as a **visual contract**, not inspiration (see 01).
4. Create/update `page-manifests/<page>.md` **before** implementation.
5. Map every value to a token and every block to an existing component (see [`02-design-system-ssot.md`](02-design-system-ssot.md)).
6. Missing token/component → document it in `design-system/` (or a theme) **first**, then use it. Never use undocumented values or components (forbidden #2 / #11).
7. Implement with logical properties and WCAG AA. Arabic/RTL → follow [`04-arabic-rtl-ux.md`](04-arabic-rtl-ux.md).
8. Run QA (see [`03-pixel-qa.md`](03-pixel-qa.md)) and report.

## Scope discipline
- Do not fix or refactor unrelated parts of the project.
- Do not add sections, cards, metrics, actions, or decoration that were not requested or not in the reference.
- Do not invent content; content comes from the user or the image. Label every detail **observed / inferred / approximate / unknown** — never silently invent an unknown.

## Ask vs Assume
**Ask the user only when the gap blocks implementation or changes the core decision.**

Ask when:
- The core/primary text is unreadable.
- The image is cropped in a critical area.
- Pixel Clone is requested but the image is low quality.
- The mode is unclear and changes how you implement.
- A core component or state is not visible and cannot be reasonably assumed.

Assume **and document** when:
- Radius / shadow / spacing is approximate.
- Hover / focus is not visible.
- Responsive behavior is not visible (document it).
- Table data is incomplete — **never invent sensitive or fake data**.

Every assumption is labeled: `observed / inferred / approximate / unknown`.

## Always report
Assumptions · conflicts · what changed · visual mismatches (format in [`03-pixel-qa.md`](03-pixel-qa.md)).

## Brand & theming
Brand changes go through a theme in `design-system/themes/`, never hard-coded into components. `--color-accent` is a high-contrast **action** color; light brand colors use a `--color-brand` **surface** token (see `design-system/foundations/brand-foundation.md`).

## Tailwind rules (general)
This project is **Tailwind-first**. Tailwind is the implementation; the design system is the source of truth for the values behind it.
- **Tokens → Tailwind:** colors / spacing / radius / shadow are exposed as Tailwind `theme` keys backed by CSS variables (per project setup). Implement by using those classes, not by re-declaring values, and not by building a separate CSS layer.
- **Default = semantic classes:** `bg-background` · `text-foreground` · `text-muted-foreground` · `border-border` · `bg-primary` (+ `text-primary-foreground`) · `rounded-lg`/`xl` · `p-4`/`p-6` · `gap-4`/`gap-6`. Use the standard Tailwind scale.
- **Arbitrary values are forbidden by default:** `bg-[#…]` · `text-[#…]` · `border-[#…]` · `p-[…]` · `m-[…]` · `gap-[…]` · `rounded-[…]` · `shadow-[…]` · `w-[…]` · `h-[…]` · `left-*`/`right-*` in RTL. Allowed **only** in Pixel Clone Mode under the conditions in [`01`](01-image-to-ui-replication.md).
- **New value?** It becomes a token (Tailwind theme key) or stays a **documented exception** in the page manifest — never a silent one-off.
- **RTL:** logical utilities only (`ms/me`, `ps/pe`, `start/end`, `text-start/text-end`). See [`04`](04-arabic-rtl-ux.md).
- **Enforcement:** if the project already uses a linter (e.g., `eslint-plugin-tailwindcss`), encode the arbitrary-value ban there. Do **not** add new tooling otherwise — these are checked at QA time ([`03`](03-pixel-qa.md)).

## References (no duplication)
Detailed design rules: `design-system/rules/` ([ai-design-rules](../design-system/rules/ai-design-rules.md) · [page-composition-rules](../design-system/rules/page-composition-rules.md) · [qa-checklist](../design-system/rules/qa-checklist.md) · [forbidden-patterns](../design-system/rules/forbidden-patterns.md)) and `foundations/`. This file governs their application, it does not replace them.
