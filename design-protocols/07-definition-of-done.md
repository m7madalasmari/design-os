# 07 — Definition of Done

> A UI task is **not complete** until every item below is satisfied. `AGENTS.md` forbids marking a task done otherwise. This is the acceptance gate that turns the protocol from guidance into a contract.

## Done checklist
- [ ] **Mode** identified and stated (Pixel Clone / System Fidelity / Strict SSOT / Improved).
- [ ] **Page manifest** created/updated in `page-manifests/` (from `_TEMPLATE.md`).
- [ ] **Reference Capture** documented *(if from an image)*: layout / spacing / type / color / radius / shadows / components observed, each labeled `observed / inferred / approximate / unknown`.
- [ ] **Component Mapping** documented: each block → an existing component (checked against [`components/INDEX.md`](../design-system/components/INDEX.md)); any missing component/token documented in `design-system/` **first**.
- [ ] **Visual Polish Decision** documented (polish/motion added · skipped · why — per [`05`](05-visual-polish-and-motion.md)).
- [ ] **Responsive Behavior** documented (desktop / tablet / mobile + table / nav / form / overflow — manifest section).
- [ ] **QA run** — the applicable ones:
  - **Pixel QA** — when there is a reference image.
  - **Design System QA** — System Fidelity / Strict SSOT.
  - **RTL QA** — Arabic / bilingual interfaces ([`04`](04-arabic-rtl-ux.md)).
  - **Visual Polish QA** — any interactive interface ([`05`](05-visual-polish-and-motion.md) table in [`03`](03-pixel-qa.md)).
- [ ] **Deviations / assumptions** documented and labeled.
- [ ] **Design-system updates** identified: needed? which files/components? **re-QA required?** — logged in [`CHANGELOG.md`](../design-system/CHANGELOG.md).
- [ ] **Required Output** delivered (the `05` report + QA tables + scope/deviations).

## Manual Self-check  (run before declaring done — no tooling required)
A quick pass the agent performs by hand (these are the same as the `03` Lint-ready Rules):
- [ ] **No undocumented arbitrary Tailwind values** (`bg-[#…]`, `p-[…]`, `w-[…]`, `rounded-[…]`…). Any used in Pixel Clone Mode are documented in the manifest.
- [ ] **No `left-*` / `right-*` / `ml-*` / `mr-*` / `pl-*` / `pr-*`** in RTL — logical utilities only (`ms/me`, `ps/pe`, `start/end`).
- [ ] **No `text-left` / `text-right`** — `text-start` / `text-end` instead.
- [ ] **No undocumented component** — every block maps to `components/INDEX.md` (or was documented first).
- [ ] **No out-of-scope changes** — only the files this task needed were touched.
- [ ] **Manifest + QA report present** — `page-manifests/<page>.md` exists and a `03` QA report was produced.

Any failed line blocks completion. (Grep helpers, e.g. `\b(ml|mr|pl|pr)-` and `(bg|text|p|m|w|h|rounded)-\[` — purely manual, no Stylelint/CI added.)

## Gate
If any box is unchecked, the task is **in progress**, not done. Report which boxes remain and why. Never present partial work as complete.
