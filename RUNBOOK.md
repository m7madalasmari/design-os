# RUNBOOK — design-os one-shot flow

> How to run design-os end-to-end from a single request: detect the task, pick the mode, read the right protocols, build, QA, and deliver — **without re-explaining the protocols every time**. This is a run layer, not a new protocol; it orchestrates `AGENTS.md` + `design-protocols/` + `design-system/`.

## One-shot prompt (paste this)
```txt
Use design-os.
Read RUNBOOK.md.
Execute the request below end-to-end.

Task:
[اكتب المطلوب]

Mode: Auto
Direction: RTL Arabic
Output: Working preview + manifest + QA
```
The agent fills the rest from the protocols. Anything not stated → resolved by **Auto Mode** + documented assumptions (it asks only when a gap blocks execution — see step 5).

## Intake
A request may come as: the one-shot prompt above, a filled [`REQUEST.md`](REQUEST.md), or a free-text ask. Map it onto the REQUEST fields (Task · Mode · Direction · Reference · Output type · Notes · Constraints). Missing fields are inferred and **documented**, not interrogated.

## The pipeline (request → delivery)
1. **Read the contract.** `AGENTS.md` → this RUNBOOK. (Already loaded if continuing a session.)
2. **Detect task type:** Design (page/component/redesign) · SPA build (Vite/React app/handover/Nx) · Review · Playground/demo. SPA triggers: "build app", "create SPA", "Vite React", "production-ready", "handover", "Nx monorepo", "team standards", "implement as real app".
3. **Resolve the Mode** (if `Auto`, use the table below). Announce it.
4. **Read the right protocols:**
   - Design: `00 → 01 → 02 → 03 → 04 → 05 → 06 → 07 → 08` → `design-system/` → manifest.
   - SPA build: the above **+ `09-spa-build-standards.md`** (pinned stack + structure).
5. **Ask-vs-Assume gate** (`00`): ask **only** when a gap *blocks* implementation or changes a *core* decision (unreadable core text, cropped critical area, low-quality image under Pixel Clone, mode genuinely ambiguous, a core component/state that can't be reasonably assumed). Otherwise **proceed with documented assumptions** (label each `observed / inferred / approximate / unknown`).
6. **Write the manifest** from `page-manifests/_TEMPLATE.md`, **before** implementing.
   - **Consumer project:** `page-manifests/<page>.md`.
   - **Inside the design-os template repo:** `playground/<name>/manifest.md` (fixtures only — never product manifests here).
7. **Map components** to `design-system/components/INDEX.md`. A missing component/token is documented in `design-system/` **first**, then used. No new component without checking INDEX.
8. **Implement** — Tailwind-first, semantic token classes, logical RTL utilities, WCAG AA. No arbitrary values (Pixel Clone excepted, documented); token-only `var()` exceptions documented (`02`). SPA tasks also obey `09`.
9. **QA** (`03`): System QA + RTL QA (`04`) + **Accessibility QA (`06`, every interface)** + Visual-Polish QA (`05`). **Pixel QA only if a reference image exists.** SPA tasks also run the **Engineering DoD** gates (`07`).
10. **Manual self-check** (`07`): arbitrary values · directional RTL utilities · `text-left/right` · undocumented components · out-of-scope edits · manifest+QA present · token-var exceptions documented.
11. **Definition of Done gate** (`07`): the task is **not done** until every box passes. Report any unchecked box and why — never present partial work as complete.
12. **Deliver** per [`OUTPUT.md`](OUTPUT.md): what was built · files changed · preview/runtime · manifest location · QA location · DoD result · known limitations · next actions.

## Auto Mode — resolution
If `Mode: Auto`, resolve to a concrete mode by the inputs:

| Inputs | Resolved mode |
|---|---|
| Image **+** "match/copy exactly" | **Pixel Clone** |
| Image **+** "apply within the system" | **System Fidelity** |
| No image **+** description only | **Greenfield / System-First** |
| Review only (no build) | **Strict SSOT — Review** (system-compliance audit; list every conflict) |
| "Improve / enhance" an existing design | **Improved** |
| Build a full app | **SPA Build Standards (`09`) + Greenfield** |

Announce the resolved mode before building. If two rows could apply and the difference changes the output materially → that is a "core decision" → ask (step 5); otherwise pick the closest and document the assumption.

## Where outputs go
- **Consumer project:** real pages + `page-manifests/<page>.md` in the project.
- **Inside design-os (this template):** fixtures/demos only, under `playground/<name>/` (`manifest.md` + `preview.html` + `README.md`). Never product pages here.
- **Preview runtime** is always stated (real Tailwind / shim mirror / static artifact / unknown — `03`).

## Done means done
Completion = all Definition-of-Done boxes checked (`07`), plus the Engineering DoD for SPA tasks. The final message follows `OUTPUT.md`.
