# Image to UI Replication Protocol

Use this protocol whenever the user provides a UI screenshot, reference image, page image, dashboard image, form image, or visual design and asks to recreate, implement, match, copy, or apply it.

## Core Rule

The reference image is a visual contract, not inspiration.

Do not redesign it.
Do not modernize it.
Do not beautify it.
Do not simplify it.
Do not add missing sections.
Do not invent components.
Do not change the visual hierarchy.

## Modes

### Pixel Clone Mode

Use when the user says:

* طبق نفس الصورة
* مثل الصورة بالضبط
* نسخة طبق الأصل
* 100%
* لا تغيّر
* copy exactly

Priority:

1. Reference image fidelity
2. User intent
3. Implementation practicality
4. Design system only if it does not reduce fidelity

Rules:

* Custom CSS values are allowed.
* Arbitrary Tailwind values (`bg-[#…]`, `p-[…]`, `rounded-[…]`, …) are allowed **only in this mode**, and only when needed to match the image. Each must be: documented in the page manifest · not generalized into a shared pattern · kept out of shared components until a **Systemization Pass** (converting it to a token/component).
* Page-specific styles are allowed.
* Do not force the reference into the design system.
* Do not fix accessibility issues unless requested.
* Report accessibility issues separately.
* After implementation, run Pixel QA.

### System Fidelity Mode

Use when the user says:

* طبقها على النظام
* بناءً على نظام التصميم
* نفس الصورة لكن داخل النظام
* استخدم التوكنز والمكونات

Priority:

1. User intent
2. Design system
3. Reference image fidelity
4. Implementation practicality

Rules:

* Use existing tokens and components.
* Match the image as closely as the system allows.
* Document every deviation from the reference.
* If a needed token or component is missing, propose it before using it.
* Tailwind: semantic token classes (`bg-primary`, `text-foreground`, `border-border`, …) + the standard scale only. **No arbitrary values** — any new value becomes a token or a documented exception.
* RTL: logical utilities only (`ms/me`, `ps/pe`, `start/end`, `text-start/text-end`).

### Strict SSOT Mode

Use when the user says:

* التزم بالنظام
* لا تطلع عن التوكنز
* النظام أهم
* strict

Priority:

1. Design system
2. Accessibility
3. User intent
4. Reference image

Rules:

* Never break tokens.
* Never use undocumented components.
* Never add one-off styling unless documented back into the system.
* Tailwind: tokens + standard scale only; **arbitrary values are not allowed here under any condition**.
* Treat the image as structural guidance, not a pixel contract.

### Improved Mode

Use only when the user explicitly asks to improve the design.

Rules:

* Preserve the original intent.
* Improve usability, accessibility, spacing, hierarchy, or responsiveness.
* Document every intentional change from the reference.

## Tailwind & arbitrary values
Default **forbidden** in every mode except Pixel Clone: `bg-[#…]` · `text-[#…]` · `border-[#…]` · `p-[…]` · `m-[…]` · `gap-[…]` · `rounded-[…]` · `shadow-[…]` · `w-[…]` · `h-[…]` · `left-*`/`right-*` in RTL.

- **Pixel Clone Mode only:** arbitrary values are permitted when required for image fidelity. They must be documented in the manifest and never placed in shared components until a Systemization Pass.
- **Systemization Pass:** the step that converts a documented one-off arbitrary value into a proper token (Tailwind theme key) or component, so it can be reused safely. Until then it stays page-local and documented.
- **System Fidelity / Strict SSOT:** bind colors to tokens, use the Tailwind scale, reuse existing components; any new value becomes a token or a documented exception.

## Required Analysis Before Implementation

Before coding from an image, create or update:

`page-manifests/[page-name].md`

Include:

* Page type
* Layout structure
* Main regions
* Grid and alignment
* Spacing observations
* Typography observations
* Color observations
* Border radius
* Shadows
* Components
* Icons/images
* Content density
* RTL/LTR direction
* Ambiguous details
* Implementation assumptions
* Arbitrary values used + justification (Pixel Clone Mode only)

Every decision must be labeled:

* observed
* inferred
* approximate
* unknown

Never silently invent unknown details.

## Pixel QA After Implementation

After implementation, compare the result against the reference (see `03-pixel-qa.md`).

Report:

* Layout match
* Spacing match
* Typography match
* Color match
* Component match
* Hierarchy match
* Overall fidelity

For each mismatch, list:

* Location
* Difference
* Severity
* Exact fix

Then fix only the mismatches. Do not redesign the page.
