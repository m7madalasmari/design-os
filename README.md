# design-os

Reusable, Tailwind-first **operating template** for building UI: an agent contract (`design-protocols/`) + a design system (`design-system/`) + page manifests. Copy it into any project; the agent reads `AGENTS.md` and follows the protocol.

**Version:** v2.2.0 · See [`VERSION.md`](VERSION.md) · [`CHANGELOG.md`](CHANGELOG.md)
**Deep install:** [`PROJECT-INSTALL.md`](PROJECT-INSTALL.md) · **Fast path:** [`QUICKSTART.md`](QUICKSTART.md)

---

## One-shot usage
Point an agent at this repo and let it run end-to-end — no need to re-explain the protocols:

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

The agent detects the task type, resolves the **Mode** (`Auto`), reads the right protocols, writes a manifest, builds, runs QA, and **only finishes after Definition of Done** — then hands over per [`OUTPUT.md`](OUTPUT.md). Full flow: [`RUNBOOK.md`](RUNBOOK.md) · intake template: [`REQUEST.md`](REQUEST.md).

## Quick usage

```txt
cp -R design-os/AGENTS.md design-os/design-protocols design-os/design-system design-os/page-manifests /path/to/project
```

## First prompt after install

```txt
اقرأ AGENTS.md وطبّق البروتوكولات المناسبة.

المهمة: [اكتب المهمة]
Mode: System Fidelity
الاتجاه: RTL عربي

قبل التنفيذ:
- أنشئ page manifest
- اربط المكونات
- طبّق Tailwind-first rules
- شغّل QA
- لا تعتبر المهمة مكتملة إلا بعد Definition of Done
```

## Project customization

Each project only needs to:

* Wire `design-system/tokens.css` into Tailwind (v4 `@import` or v3 config) — see [`PROJECT-INSTALL.md`](PROJECT-INSTALL.md).
* Set the brand: override `--color-primary`, `--color-link`, `--color-ring` (+ `--color-brand` for light brands), `--radius-*`, font — in a theme block.
* Update `design-system/components/INDEX.md` to match the components that actually exist in the project.
* Update the app shell / routing contract ([`design-protocols/08`](design-protocols/08-app-shell-and-routing-consistency.md)) if the project is multi-page.

---

## What's inside
```
AGENTS.md                 entry contract (read first)
ROLES.md                  the review council — 9 role mindsets worn across Think/Build/Review (lens sweep)
RUNBOOK.md                one-shot flow (request → delivery) · REQUEST.md (intake) · OUTPUT.md (handover)
design-protocols/         00 rules · 01 image→ui · 02 ssot · 03 qa · 04 rtl · 05 polish · 07 done · 08 app-shell · 09 spa-build (conditional) · examples/
design-system/            tokens.css (executable) · foundations/ · components/ (+INDEX) · rules/ · themes/ · VERSION · CHANGELOG
page-manifests/           _TEMPLATE.md · _GOLDEN_EXAMPLE.md
playground/               test fixtures (not product pages)
```

## The loop (every UI task)
read `AGENTS.md` → announce **Mode** → write manifest (`_TEMPLATE`) → map components (`INDEX`) → build with semantic Tailwind classes → run QA (`03`) → **done only when [`07` Definition of Done](design-protocols/07-definition-of-done.md) passes**.

## Task types (which protocols apply)
- **Design task** (a page, component, screenshot-to-UI, redesign): uses **`00–08`** (the design layer) — usually that's all. No build stack imposed.
- **SPA build task** (new app, Vite + React, production, handover, Nx): uses **`00–09`** — the design layer **plus** [`09` SPA Build Standards](design-protocols/09-spa-build-standards.md), and must follow the pinned stack + technical structure. Completion adds the **Engineering Definition of Done** ([`07`](design-protocols/07-definition-of-done.md)).
- **Playground task** (exploration/demo inside design-os): does **not** need the full SPA requirements enforced unless the user explicitly asks; keep outputs in `playground/`.

Trigger phrases that activate `09`: "build app", "create SPA", "Vite React", "production-ready", "handover", "Nx monorepo", "team standards", "implement as real app".

## Template vs consumer project
`design-os` is an **operating template, not a product**. Inside this repo: do **not** create real product `page-manifests/` or product pages — keep `page-manifests/` to `_TEMPLATE.md` + `_GOLDEN_EXAMPLE.md`. Worked outputs / artifacts from testing design-os itself go in `examples/`, `playground/`, or `scratch/`. In a **consumer project**, create `page-manifests/<page>.md` and build pages normally. (See [`07`](design-protocols/07-definition-of-done.md) · [`PROJECT-INSTALL.md`](PROJECT-INSTALL.md).)

## Preview strategy (Tailwind)
- **Consumer projects:** wire Tailwind normally — v3 config or v4 `@import`/`@theme` (see [`PROJECT-INSTALL.md`](PROJECT-INSTALL.md)). That is the production implementation.
- **design-os demos / artifacts:** if a Tailwind build is unavailable, a **documented preview shim** may be used — it must mirror `tokens.css` + the semantic classes, and it is **not** the production implementation. The QA report states the **Preview runtime** (real Tailwind / shim mirror / static artifact / unknown). See [`02`](design-protocols/02-design-system-ssot.md) · [`03`](design-protocols/03-pixel-qa.md).

## Constraints (by design)
No npm package / CLI / CI / Stylelint yet. This is a copyable template + git history, meant to be evolved.
