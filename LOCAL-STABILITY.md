# LOCAL-STABILITY — when is design-os ready for daily local use?

> design-os is meant to be **stable locally and usable with confidence before publishing to GitHub**. This is the bar: a checklist that defines "locally ready". Re-check it before each release; ship to GitHub only when it passes.

## Definition
design-os is **locally ready** when an agent can take a real request, run it end-to-end via the protocols, and deliver a correct, system-compliant, accessible result — repeatedly — without the operator re-explaining the system, and with a clean, tagged tree.

## Checklist  (status as of v1.1.7)
- [x] **Protocol sequence complete** — `00–09` with **no gap** (`06` added in v1.1.7).
- [x] **`06` Accessibility exists** — baseline a11y protocol + QA, wired into AGENTS/RUNBOOK/07.
- [x] **Premium Visual Baseline active** — font (IBM Plex Sans Arabic chain), icon-system (Lucide), native-control prevention, visual-acceptance criteria (v1.1.6).
- [x] **Component Gallery usable** — renders cleanly, RTL, token-based, no native-control chrome.
- [x] **Core components covered** — all **27/27** documented components render in the gallery (completed in v1.1.8 — see [`playground/design-system-preview/coverage.md`](playground/design-system-preview/coverage.md)).
- [x] **No native/browser-looking controls in preview** — appearance reset in the gallery shim (v1.1.6 fix).
- [x] **No arbitrary Tailwind values in examples** — verified by grep on every fixture.
- [x] **RTL rules active** — logical utilities only; bidi-isolated numerals; mirrored directional icons.
- [x] **Manifests working** — `_TEMPLATE.md` + 3 worked fixtures.
- [x] **One-shot RUNBOOK working** — `RUNBOOK.md` + Auto Mode + `REQUEST`/`OUTPUT`; exercised by the Greenfield run.
- [x] **≥ 3 successful local stress tests** — `invoices` (System Fidelity), `consultation-requests` (Greenfield), `design-system-preview` (gallery). All passed DoD, zero arbitrary values, RTL pass.
- [x] **No untracked files** — clean working tree.
- [x] **Clean release tag** — `v1.1.7`.

**Verdict:** **locally ready ✅** — full gallery coverage (27/27) since v1.1.8. Remaining future work (backlog components, GitHub publish) is tracked, not blocking.

## What "locally ready" does NOT yet include (by design)
- GitHub remote / push (deliberately deferred — local stability first).
- Shipped component code (`impl: ✗`; library is spec-only).
- Dark mode tokens · enforced linting/CI/tests · real font files · real Lucide integration.
- The 12 backlog components (see [`design-system/components/BACKLOG.md`](design-system/components/BACKLOG.md)).

## Re-check cadence
Run this checklist before every release tag. Any unchecked **blocking** line (sequence, 06, native-control, arbitrary values, RTL, untracked, tag) holds the release.
