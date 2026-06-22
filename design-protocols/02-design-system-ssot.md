# Design System SSOT Protocol

The design system is the source of truth for System Fidelity Mode and Strict SSOT Mode.

Check:

- `design-system/foundations/tokens.md`
- `design-system/foundations/typography.md`
- `design-system/foundations/spacing.md`
- `design-system/foundations/layout.md`
- `design-system/foundations/rtl-guidelines.md`
- `design-system/components/`
- `design-system/rules/forbidden-patterns.md`

If design-system files are missing:

- Create a neutral foundation.
- Do not invent a final brand identity.
- Mark all brand choices as placeholders.

## Executable token source (identify before changing UI)
`foundations/tokens.md` is **documentation**, not the runtime source. The executable source is **`design-system/tokens.css`** (Tailwind v4 `@theme`) or the project's Tailwind theme:
- **Tailwind v4:** CSS variables / `@theme` per project structure.
- **Tailwind config (v3):** bind `theme.extend` to the tokens (same names, same values).

**The agent must identify the executable token source before changing UI.** If none exists, create or propose one (without touching product pages). `tokens.md` and the executable source must agree; a change to one updates the other (logged in `CHANGELOG.md`).

## Tailwind binding (Tailwind-first)
Tokens are exposed to Tailwind as `theme` keys backed by CSS variables (per project setup, e.g. shadcn-style `:root` variables + `tailwind.config` referencing them). Implement with the **semantic classes**, not raw values. `tokens.md` documents the source; the Tailwind theme is how it is consumed.

| Design-system token | Tailwind class / theme key |
|---|---|
| `--color-bg-base` | `bg-background` |
| `--color-bg-surface` | `bg-card` / `bg-popover` |
| `--color-bg-subtle` | `bg-muted` |
| `--color-text-primary` | `text-foreground` |
| `--color-text-secondary` | `text-muted-foreground` |
| `--color-accent` (action) | `bg-primary` / `text-primary` (+ `text-primary-foreground`) |
| `--color-border-default` | `border-border` |
| focus ring | `ring` / `ring-ring` |
| `--color-danger-*` | `destructive` |
| spacing (4px base) | Tailwind spacing scale (`p-4`=16px=`space-md`, `p-6`=24px=`space-lg`) |
| `--radius-md` / `--radius-lg` | `rounded-lg` / `rounded-xl` |

Rules: bind colors to tokens; use the Tailwind scale; new value → token or documented exception. Brand changes live in the theme (CSS variables / Tailwind theme), never hard-coded in components.

