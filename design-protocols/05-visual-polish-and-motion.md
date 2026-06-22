# Visual Polish and Motion Protocol

> Use beyond basic layout/components. Every enhancement must serve a purpose (below), obey the active **mode**, and respect `prefers-reduced-motion`. Motion/elevation tokens: [`tokens.md §7`](../design-system/foundations/tokens.md). Anti-decoration stance: [`forbidden-patterns`](../design-system/rules/forbidden-patterns.md) #6. When this protocol and a component spec disagree, the design system wins ([`02`](02-design-system-ssot.md)).

Use this protocol when designing, recreating, improving, or reviewing UI quality beyond basic layout and components.

## Purpose

Ensure the UI does not stop at basic layout implementation.

Check for missing visual polish, motion, SVG details, micro-interactions, depth, and state quality.

## Important Rule

Do not add decorative elements randomly.

Every visual enhancement must serve one of these purposes:

- Clarify hierarchy
- Improve feedback
- Support brand expression
- Improve perceived quality
- Improve orientation
- Make empty/loading states clearer
- Make data easier to understand

## Page Type Polish Rules

| Page Type | Recommended Polish | Avoid |
|---|---|---|
| Admin Dashboard | subtle hover, skeletons, chart tooltips, clear focus | heavy animation, decorative SVGs |
| Data Table | row hover, filter feedback, empty state, loading | animated rows, excessive shadows |
| Form | focus states, validation, helper text, progress | decorative motion |
| Landing Page | SVG motifs, scroll reveal, hero motion, brand depth | slow animations, content delay |
| Empty State | data/admin → simple icon or simple visual · marketing/landing → illustration if it serves identity/meaning; clear CTA; gentle motion optional | large decorative illustration in data apps · generic/meaningless icons · excessive copy |
| Detail Page | section hierarchy, sticky summary, state badges | too many cards |
| Marketing Hero | background motif, subtle motion, strong visual rhythm | random gradients, heavy particles |

> **Empty-state illustration — resolved rule:**
> 1. **Data apps / admin pages:** a simple icon or simple visual only — **no large decorative illustration**.
> 2. **Marketing / landing pages:** illustration is allowed if it serves the identity or clarifies the meaning.
> 3. **Pixel Clone Mode:** reproduce the illustration if it appears in the image; if it is not in the image, do not add one.
> 4. **System Fidelity Mode:** follow the documented [`empty-state.md`](../design-system/components/empty-state.md) first — if the component forbids illustrations, do not add them.
> 5. **Improved Mode:** an illustration may be proposed, but it must be justified in the Visual Polish Decision (Required Output).
> 6. **On any conflict between this protocol and `empty-state.md`, the component spec wins.**

## Mode Behavior

### Pixel Clone Mode

- Do not invent visual polish.
- Only implement SVGs, patterns, animations, or effects visible in the reference.
- If motion cannot be inferred from a static image, mark it as unknown.
- Do not add hover or animation unless it is required by the component behavior.

### System Fidelity Mode

- Add only subtle, system-compatible polish.
- Use existing motion tokens if available.
- Use minimal transitions for hover/focus/active states.
- Add SVG or visual motifs only if they match the design system and page intent.
- Document every added visual enhancement.

### Strict SSOT Mode

- Use only documented motion, elevation, illustration, and SVG patterns.
- Do not create new visual effects unless they are added to the design system first.

### Improved Mode

- Actively propose improvements for polish, motion, depth, SVG motifs, and micro-interactions.
- Preserve the user's intent and core layout.
- Document every difference from the original reference.

## Visual Polish Checklist

Check whether the UI needs:

### 1. Motion
- Hover transitions
- Active states
- Focus states
- Page entrance
- Section reveal
- Drawer/modal transitions
- Tab transitions
- Loading transitions
- Empty state motion
- Data visualization animation

### 2. SVG and Visual Motifs
- Background SVG pattern
- Brand motif
- Decorative linework
- Geometric shape
- Abstract illustration
- Empty state illustration
- Icon set consistency
- Data-related visual element

### 3. Depth and Surface
- Elevation
- Border treatment
- Subtle shadow
- Layer separation
- Background contrast
- Surface hierarchy
- Glass/blur only if appropriate

### 4. Interaction Feedback
- Button hover
- Button pressed state
- Disabled state
- Input focus
- Input error
- Select open state
- Row hover
- Card hover
- Tooltip behavior
- Toast feedback

### 5. Loading and Empty States
- Skeleton loading
- Spinner only when appropriate
- Empty state illustration
- Clear empty state title
- Helpful description
- Primary next action
- Error recovery action

### 6. Data UI
- Chart loading
- Chart empty state
- Tooltip
- Legend
- Axis readability
- Highlight on hover
- Number transition only if appropriate

## Motion Rules

Motion must be:

- Subtle
- Fast
- Purposeful
- Non-distracting
- Respectful of reduced motion preferences

Use:
- duration-150
- duration-200
- duration-300
- ease-out
- ease-in-out

Avoid:
- Slow animations
- Infinite decorative motion
- Large bouncing effects
- Random parallax
- Heavy blur/glow
- Motion that delays content visibility

Always support:

prefers-reduced-motion

## Tailwind Motion Rules

Allowed examples:

- transition-colors
- transition-opacity
- transition-transform
- duration-200
- ease-out
- hover:bg-*
- hover:shadow-sm
- focus-visible:ring-2
- motion-safe:animate-*
- motion-reduce:transition-none
- motion-reduce:animate-none

Avoid unless justified:

- animate-bounce
- animate-pulse for non-loading elements
- huge custom keyframes
- arbitrary animation values
- decorative infinite loops

## SVG Rules

SVGs are allowed when they are:

- Part of the reference image
- Part of brand expression
- Useful for empty states
- Useful as subtle background motif
- Lightweight and accessible

SVGs must:

- Use currentColor or design tokens when possible
- Be responsive
- Not block content
- Have aria-hidden="true" if decorative
- Have accessible labels if meaningful
- Not contain random hardcoded colors unless Pixel Clone Mode

## Required Output

After implementation or review, report:

- Visual polish added
- Visual polish intentionally skipped
- Motion added
- SVGs added
- Unknowns
- Performance risks
- Accessibility risks
