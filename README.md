# design-os

Reusable, Tailwind-first **operating template** for building UI: an agent contract (`design-protocols/`) + a design system (`design-system/`) + page manifests. Copy it into any project; the agent reads `AGENTS.md` and follows the protocol.

**Version:** v1.1.0 · See [`VERSION.md`](VERSION.md) · [`CHANGELOG.md`](CHANGELOG.md)
**Deep install:** [`PROJECT-INSTALL.md`](PROJECT-INSTALL.md) · **Fast path:** [`QUICKSTART.md`](QUICKSTART.md)

---

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
design-protocols/         00 rules · 01 image→ui · 02 ssot · 03 qa · 04 rtl · 05 polish · 07 done · 08 app-shell · examples/
design-system/            tokens.css (executable) · foundations/ · components/ (+INDEX) · rules/ · themes/ · VERSION · CHANGELOG
page-manifests/           _TEMPLATE.md · _GOLDEN_EXAMPLE.md
```

## The loop (every UI task)
read `AGENTS.md` → announce **Mode** → write manifest (`_TEMPLATE`) → map components (`INDEX`) → build with semantic Tailwind classes → run QA (`03`) → **done only when [`07` Definition of Done](design-protocols/07-definition-of-done.md) passes**.

## Constraints (by design)
No npm package / CLI / CI / Stylelint yet. This is a copyable template + git history, meant to be evolved.
