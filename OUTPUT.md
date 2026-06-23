# OUTPUT — design-os delivery format

> The shape of the final handover the agent returns at the end of a run (per [`RUNBOOK.md`](RUNBOOK.md) step 12). Copy this structure into the final message; fill every field.

## What was built
*(One paragraph: the screen/component/app delivered, the resolved Mode, direction, theme.)*

## Files changed
*(Created / modified / moved — with paths. Note scope: only the files the task needed.)*

## Preview / runtime
*(How to see it: preview path + open command, or app run steps. **Preview runtime:** real Tailwind | shim mirror | static artifact | unknown.)*

## Manifest location
*(Consumer: `page-manifests/<page>.md`. Inside design-os: `playground/<name>/manifest.md`.)*

## QA report location
*(Embedded in the manifest, or a separate file — state the path. Which QA ran: System · RTL · Visual-Polish · Pixel (only if reference) · Engineering DoD (SPA).)*

## Definition of Done result
*(Pass / in-progress. List any unchecked box and why. SPA tasks: include the Engineering DoD gates.)*

## Known limitations
*(Documented assumptions, deviations, CSP/font fallbacks, out-of-scope items, shim-vs-real-Tailwind notes.)*

## Next actions
*(What the user can ask for next: wire real Tailwind, add a state, theme swap, integrate into a project, etc.)*
