# Consultation Requests — Greenfield test fixture

> **This is a test fixture, not a product page.** It exists to prove that **Greenfield / System-First** mode produces a correct, system-compliant admin screen with no visual reference.

- **Type:** Greenfield / System-First test fixture for **design-os v1.1.2+**.
- **Not a product page** — built to exercise the protocol, not to ship.
- **Do not copy to consumer projects** — fixtures stay in `playground/`; real pages live in a consumer project's `page-manifests/`.
- **Purpose:** validate that the design system + protocols cover a realistic admin page (filter bar · table · status badges · assign action · export · the five data states) from the system alone.
- **Preview runtime:** **shim mirror** — a documented shim mirrors `design-system/tokens.css` + the semantic Tailwind classes 1:1 (no Tailwind build here). **Not** the production implementation.

## Files
- **`manifest.md`** — the page manifest (Greenfield, RTL, neutral theme) + embedded QA report.
- **`preview.html`** — the rendered preview (open in a browser).

## Test result
- **Test:** Consultation Requests — Greenfield
- **Result:** ✅ Passed
- **Definition of Done:** ✅ Passed (Pixel QA N/A — Greenfield)
- **Design-system updates required:** None
- **Arbitrary values:** Zero
- **RTL:** ✅ Passed (logical utilities only; bidi-isolated numerals/ids)
- **Manual self-check:** ✅ Passed
- **Components:** all mapped to `components/INDEX.md` (page-header · filter-bar · table · status-badge · button · empty-state); pagination = documented composition. No new components.
