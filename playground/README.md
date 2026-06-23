# playground — testing design-os itself

> Worked outputs produced while **testing design-os**, kept out of `page-manifests/` (which is template-only: `_TEMPLATE.md` + `_GOLDEN_EXAMPLE.md`). See the *template vs consumer* rule in [`../README.md`](../README.md) and [`../design-protocols/07-definition-of-done.md`](../design-protocols/07-definition-of-done.md).

These are **not** product pages and **not** the production implementation.

## Contents
- **`invoices.md` / `invoices.html`** — page manifest + rendered preview from the v1.1.2 live-test (Mode: System Fidelity / no reference → Greenfield-leaning; theme: neutral; demo data: synthetic, PII-free). **Preview runtime: shim mirror** (mirrors `tokens.css` + semantic classes 1:1; no Tailwind build). Not production code.
- **`consultation-requests/`** — Greenfield / System-First test fixture (admin requests screen). See [`consultation-requests/README.md`](consultation-requests/README.md).

## Test fixtures — results
| Fixture | Mode | DoD | Arbitrary values | RTL | Manual self-check | DS update | Result |
|---|---|---|---|---|---|---|---|
| Consultation Requests | Greenfield / System-First | Passed (Pixel QA N/A) | Zero | Passed | Passed | None | ✅ Passed |
| Invoices | System Fidelity (no ref) | Passed (Pixel QA N/A) | Zero | Passed | Passed | None | ✅ Passed |

> Fixtures prove design-os on realistic screens; they are **not** product pages and are **not** copied to consumer projects.
