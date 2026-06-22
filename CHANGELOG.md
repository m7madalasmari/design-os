# design-os — CHANGELOG

OS-level history. Design-system detail (tokens/components) in [`design-system/CHANGELOG.md`](design-system/CHANGELOG.md).

---

## v1.1.0 — 2026-06-22
Packaged the system + protocols into a reusable, Tailwind-first git template, and closed v1.0's critical gaps.

- **Packaging:** assembled `AGENTS.md` + `design-protocols/` + `design-system/` + `page-manifests/` into `design-os/`; added `README`, `QUICKSTART`, `PROJECT-INSTALL`, OS-level `VERSION`/`CHANGELOG`.
- **Definition of Done** (`design-protocols/07`) — acceptance gate; AGENTS forbids marking work complete without it.
- **focus/link decoupled from accent** — `--color-focus-ring` / `--color-text-link` independent, contrast-verified; `--shadow-focus`/`--color-border-focus` use the ring token.
- **Executable token source** — `design-system/tokens.css` (Tailwind v4 `@theme`); `tokens.md` is documentation.
- **App-shell & routing consistency** (`design-protocols/08`).
- **Governance** — `VERSION.md` + `CHANGELOG.md` (system + OS).
- **Golden example** — `page-manifests/_GOLDEN_EXAMPLE.md` + `design-protocols/examples/golden-qa-report.md`.
- **Component inventory** — `design-system/components/INDEX.md`.
- **Ask-vs-Assume** rule (`00`); **Responsive Behavior** manifest section; **Lint-ready Rules** (`03`, not enforced).

## v1.0 — 2026-06-22
Initial system: foundations / components / rules / themes + agent protocols `00–05`, Tailwind-first, page-manifest `_TEMPLATE.md`, Empty-State illustration conflict resolved (context-aware; component spec wins).
