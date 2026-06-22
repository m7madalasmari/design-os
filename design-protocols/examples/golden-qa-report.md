# Golden QA Report — Consultation Evaluation  *(reference only)*

> A worked QA report (per `03`) the agent can imitate. Page: `pages/consultation-evaluation.html`. Manifest: `page-manifests/_GOLDEN_EXAMPLE.md`. Mode: **System Fidelity**.

## Visual match summary
Layout ✅ · Spacing ✅ (approx) · Color ✅ · Component ✅ · Hierarchy ✅ · Typography ⚠️ (font fallback) · **Overall fidelity: high**.

## Visual polish & motion QA
| Area | Match % | Issues | Fix |
|---|---:|---|---|
| Motion | 100 | — | transitions present, reduced-motion handled |
| SVG / Motifs | 100 | banner image substituted (asset unavailable) | drop real asset later |
| Hover / Focus States | 100 | added hover/active to rating/scale/stepper | — |
| Loading / Empty States | 90 | details-card skeleton skipped (static) | add when async |
| Surface Depth | 100 | soft card shadow only | — |

## Mismatches / deviations
| Location | Difference | Type | Severity | Fix | Scope |
|---|---|---|---|---|---|
| `.details-banner` | hex → token | Token | med | **fixed** → `var(--color-accent)` | page |
| font | Plex → system (CSP) | Typography | low | load Plex locally | page |
| details banner / logo | real asset → substitute | Content/Asset | med | real asset later | page |
| header pattern | image → CSS motif | Layout | low | optional SVG | page |
| stepper buttons | raw `36px`, <44 touch | Token/a11y | med | **fixed** → token + 44px | page |

## System QA
Tokens only ✅ · one primary ✅ · logical RTL utilities ✅ · Latin tabular numerals ✅ · AA contrast (purple ~9:1) ✅ · focus ring visible + 44px targets ✅ · labels above fields ✅ · no invented required markers ✅.

## Tailwind compliance
Semantic classes intended (page is CSS-var demo; classes map 1:1 — see `02` binding). No arbitrary values after the `36px`/hex fixes. RTL logical only.

## Required Output (per `05`)
- **Polish added:** hover/active on rating/scale/stepper; subtle `transition-colors`.
- **Polish skipped:** SVG motifs, scroll reveal, decorative motion (Form page type).
- **Motion:** `duration-150 ease-out`, reduced-motion off.
- **SVGs:** functional field icons only (`aria-hidden`, currentColor).
- **Unknowns:** required-vs-optional fields (not invented).
- **Performance risks:** none significant.
- **Accessibility risks:** none open (focus/touch/contrast pass).

## Done?
All `07` boxes checked. Documented deviations: font fallback, substituted banner, skipped async skeleton. **Complete.**
