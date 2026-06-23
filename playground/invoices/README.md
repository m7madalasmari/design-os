# Invoices — live-test fixture

> **This is a test fixture, not a product page.** It was the first live-test of the protocol (an invoices admin screen, no visual reference) — the run that surfaced the runtime gaps later closed in **v1.1.2**.

- **Type:** System Fidelity / no reference (Greenfield-leaning) test fixture for **design-os**.
- **Not a product page** — built to exercise the protocol, not to ship.
- **Do not copy to consumer projects** — fixtures stay in `playground/`; real pages live in a consumer project's `page-manifests/`.
- **Purpose:** validate the design system + protocols on a realistic data screen (page-header · filter bar · table · status badges · the five data states) from the system alone; the findings drove the v1.1.2 patch.
- **Preview runtime:** **shim mirror** — a documented shim mirrors `design-system/tokens.css` + the semantic Tailwind classes 1:1 (no Tailwind build here). **Not** the production implementation.

## Files
- **`manifest.md`** — the page manifest (no reference, RTL, neutral theme) + embedded QA report.
- **`preview.html`** — the rendered preview (open in a browser).

## Test result
- **Test:** Invoices — live-test
- **Result:** ✅ Passed
- **Definition of Done:** ✅ Passed (Pixel QA N/A — no reference)
- **Design-system updates required:** None
- **Arbitrary values:** Zero
- **RTL:** ✅ Passed (logical utilities only; bidi-isolated currency/ids)
- **Manual self-check:** ✅ Passed
- **Components:** all mapped to `components/INDEX.md` (page-header · filter-bar · table · status-badge · button · empty-state); pagination = documented composition. No new components.
