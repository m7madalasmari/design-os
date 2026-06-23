# 09 — SPA Build Standards  (Engineering Protocol)

> **A separate engineering layer — not a design protocol.** `00–08` govern *how the UI looks and is composed*; this file governs *how a real React/Vite application is engineered*. It is **conditional**: apply it only for SPA build / production / handover / Nx-integration tasks (triggers in [`AGENTS.md`](../AGENTS.md)). For design tasks and lightweight playgrounds, do **not** impose this stack unless the user asks.
>
> Pairs with the **Engineering Definition of Done** in [`07`](07-definition-of-done.md). Design rules (tokens, components, RTL, polish) still apply on top of this — this file adds the *technical* contract, it does not replace `00–08`.

## When to use
Apply `09` when the task is one of: create a new SPA · build a Vite + React app · prepare code for team handover · implement production-ready pages inside a real app · integrate with a future Nx monorepo. Otherwise skip it.

---

## 1. Stack (pinned — do not substitute)
These are **mandatory** and version-pinned. Do not swap a library for an equivalent without an explicit, documented request.

| Concern | Library | Version |
|---|---|---|
| UI runtime | React | **19** |
| Language | TypeScript (**strict**) | 5.x |
| Build / dev server | Vite | **6** |
| Routing | React Router | **6** |
| Server state | TanStack Query | **v5** |
| Client state | Zustand | **5** |
| Forms | React Hook Form **7** + Zod | RHF 7 / Zod 3.x |
| HTTP | Axios | **1.x** |
| Styling | Tailwind CSS | **4** (binds `design-system/tokens.css`) |
| i18n | i18next + react-i18next | latest 23.x / 14.x |
| Icons | **lucide-react** (primary) · react-icons (brand/social fallback only) | latest |
| Testing | Vitest (+ Testing Library) | latest |
| Quality | ESLint + Prettier | latest |

**Icons:** use **`lucide-react`** for all UI icons per [`design-system/foundations/icon-system.md`](../design-system/foundations/icon-system.md) — one icon style only; sizes via `--size-icon-*`; decorative `aria-hidden`, meaningful icons labelled; directional icons mirror in RTL. `react-icons` only for brand/social or icons missing from Lucide.

**Forbidden by default:** Redux/MobX/Recoil (use Zustand + TanStack Query), `fetch` scattered in components (use the Axios core), CRA/Webpack, Moment.js, CSS-in-JS runtime libs, `styled-components`, any UI kit that bypasses `design-system/`.

---

## 2. Required folder structure
Feature-first. The top level is fixed; features mirror the same internal shape.

```
src/
  app/
    App.tsx              # composes providers + router
    providers.tsx        # QueryClientProvider, I18nextProvider, AuthProvider, etc.
    router.tsx           # <RouterProvider> / route tree (lazy elements)
    app.paths.ts         # SINGLE source of route path constants
  core/
    api/
      client.ts          # the ONE axios instance + interceptors
      query-client.ts    # TanStack QueryClient config
      http.types.ts
    auth/                # auth abstraction (provider + hooks + service)
    config/
      env.ts             # typed access to import.meta.env (no raw access elsewhere)
    i18n/
      index.ts           # i18next init
      locales/ar/*.json  locales/en/*.json
    storage/
      storage.ts         # the ONLY localStorage/sessionStorage wrapper
    lib/                 # framework-agnostic utilities
  components/
    ui/                  # shared UI bound to design-system specs + tokens
  features/
    <feature>/
      api/               # query/mutation hooks (TanStack Query) — wrap core/api
      components/
      hooks/
      stores/            # <feature>.store.ts (Zustand client state only)
      schemas/           # <feature>.schema.ts (Zod)
      types/
  pages/                 # lazy route entry components (default export allowed here)
  styles/
    index.css            # @import "tailwindcss"; @import design-system/tokens.css
  types/                 # global/ambient types
  test/
    setup.ts
```
A new shared pattern is added at this level **first**, then reused — never forked per feature.

---

## 3. Naming conventions
- **Components / pages:** `PascalCase.tsx` (`UserTable.tsx`, `RequestsPage.tsx`).
- **Hooks:** `useThing.ts` (camelCase, `use` prefix).
- **Stores:** `<name>.store.ts`. **Schemas:** `<name>.schema.ts`. **API hooks:** `<name>.api.ts`. **Types:** `<name>.types.ts`.
- **Variables/functions:** `camelCase`. **Types/interfaces/enums:** `PascalCase`. **Constants:** `UPPER_SNAKE_CASE`.
- **Exports:** **named exports everywhere** — the *only* allowed default exports are lazy page modules in `pages/`.
- One primary unit per file; co-locate tests as `*.test.ts(x)`.

---

## 4. Routing rules
- Route **paths live only in `app/app.paths.ts`** as typed constants (e.g. `AppPaths.requests`, `AppPaths.requestDetail(id)`). **No route string literals inside components** — always reference `app.paths.ts`.
- **All pages are lazy-loaded** (`React.lazy` + `<Suspense>`), one default export per page module.
- Navigation via `<Link to={AppPaths.x}>` / `useNavigate()` — never hand-built hrefs.
- A 404 / not-found route and an error element are defined at the router level.

---

## 5. HTTP architecture
- **One centralized Axios instance** in `core/api/client.ts` (baseURL from `env`, interceptors for auth token + error normalization). **No `axios` import or `fetch` outside `core/api`.**
- **All server state goes through TanStack Query** (`useQuery`/`useMutation`) in feature `api/` hooks that call the core client. **No data fetching in `useEffect`.**
- Query keys are structured and centralized per feature. Mutations invalidate the right keys.
- **API responses are never stored in Zustand** — server state belongs to the Query cache only.

---

## 6. State management rules
- **Server/remote state → TanStack Query** (cache, refetch, invalidation).
- **Client/UI state → Zustand** (`<feature>.store.ts`): modals, filters, wizard steps, ephemeral selections.
- Stores are small and typed; no business/API data duplicated from the Query cache.
- No global "god store"; one store per concern/feature.

---

## 7. Form rules
- All forms use **React Hook Form 7 + Zod** (`zodResolver`).
- Validation schema lives in `schemas/<name>.schema.ts`; the inferred type (`z.infer`) is the form's type.
- Validate on blur/submit; show field errors via the design-system input error state; one primary submit action.
- No uncontrolled ad-hoc forms, no manual `useState` field soup.

---

## 8. Error handling
- A top-level **Error Boundary** (and per-route error elements) — no white screen on throw.
- Query/mutation errors surface through the design-system **toast** or the **empty-state `error`** pattern (`role="alert"`), with a recovery action. **Never swallow errors silently.**
- Axios interceptor normalizes errors to a typed shape; user-facing messages follow `04` (what happened + how to fix), and are **i18n keys**, not literals.

---

## 9. i18n + RTL
- **No hardcoded user-facing strings** — every label/message is an i18next key (`ar` default, `en` available). Keys are namespaced per feature.
- Document/`<html>` `dir` follows the active locale (`rtl` for `ar`).
- **RTL uses logical Tailwind utilities only** (`ms/me`, `ps/pe`, `start/end`, `text-start/end`) per [`04`](04-arabic-rtl-ux.md) — no directional utilities.
- Numbers/dates per `04` (Latin tabular numerals, one unified format), formatted through i18n where applicable.

---

## 10. Auth abstraction
- Auth lives behind an abstraction in `core/auth` (provider + `useAuth()` hook + a service) — components never read tokens directly.
- Token persistence goes through the **storage wrapper** (`core/storage`), never raw `localStorage`.
- Route guards (protected/public) are declared at the router level using the auth abstraction.

---

## 11. Environment handling
- All env access goes through **`core/config/env.ts`** (typed) — no raw `import.meta.env.*` scattered in code.
- Only `VITE_`-prefixed vars reach the client; **no secrets** in client env.
- A committed **`.env.example`** lists every required variable (no real values).

---

## 12. Code quality rules
- **TypeScript strict** on. **No `any`, no `@ts-ignore`/`@ts-expect-error`** (justify-and-isolate only with an explicit, reviewed exception).
- **ESLint + Prettier** enforced; lint passes with **0 errors**, build with **0 warnings**.
- No dead code, no commented-out blocks shipped, no `console.log` in committed code.

---

## 13. Path alias
- `@/` maps to `src/` (configured in both `tsconfig` `paths` and Vite `resolve.alias`). Use `@/…` imports for cross-area references; relative imports only within the same folder.

---

## 14. Tailwind conventions
- Tailwind 4 binds `design-system/tokens.css` (`@import`/`@theme`) — **semantic token classes** only (`bg-background`, `text-foreground`, `bg-primary`, `border-border`, …).
- **No arbitrary values** (`bg-[#…]`, `p-[…]`, `w-[…]`) — same rule as `00`/`02`. Tokens with no utility (z/duration/easing/size) use the documented **Token Var Exception** (`style`+`var()`), per [`02`](02-design-system-ssot.md).
- RTL = logical utilities only.

---

## 15. Commits
- **Conventional Commits**: `feat:`, `fix:`, `chore:`, `refactor:`, `docs:`, `test:`, `build:`, `ci:`. Scope optional (`feat(requests): …`). Imperative, concise.
- Small, focused commits; no unrelated changes bundled.

---

## 16. Deliverables
A completed SPA build hands over:
- A running Vite + React 19 app matching the structure above.
- `README.md` (setup, scripts, structure, env) + **`.env.example`**.
- Passing scripts: `dev` (port **5173**), `build` (0 warnings), `lint` (0 errors), `typecheck` (0 errors), `test`.
- i18n resources (`ar`/`en`) and RTL working.
- Clean git history (Conventional Commits), ready to drop into an Nx monorepo (`apps/<name>` shape; no app-specific assumptions that block Nx).

---

## 17. Rejection list (auto-reject in review)
- Off-stack library or unpinned major swap (Redux, CRA, fetch-in-component, CSS-in-JS, foreign UI kit).
- `any` / `@ts-ignore`; non-strict TS.
- Data fetching in `useEffect`; `axios`/`fetch` outside `core/api`.
- API responses stored in Zustand; server state duplicated outside the Query cache.
- Route string literals in components; missing `app.paths.ts`.
- Hardcoded user-facing strings (no i18n).
- Raw `localStorage`/`sessionStorage` outside the storage wrapper.
- Raw `import.meta.env` outside `core/config`.
- Arbitrary Tailwind values / directional RTL utilities.
- Mixed icon libraries / off-system UI icons / `react-icons` for a general UI icon available in Lucide.
- Non-lazy pages; default exports outside `pages/`.
- Build warnings, lint errors, failing tests, missing `.env.example`/README.

---

## Engineering Self-check  (run before declaring an SPA task done)
- [ ] **Stack matches pinned versions** (§1).
- [ ] **Folder structure matches the required tree** (§2).
- [ ] **All pages lazy-loaded** (one default export per page module).
- [ ] **`app/app.paths.ts` used** for every route constant — no literals in components.
- [ ] **Axios instance is centralized** (`core/api`); nothing imports `axios`/`fetch` elsewhere.
- [ ] **Server state uses TanStack Query**; no fetch-in-`useEffect`.
- [ ] **Client state uses Zustand**; no API responses stored in Zustand.
- [ ] **Forms use RHF + Zod** (schema-typed).
- [ ] **User-facing strings use i18next** (no literals).
- [ ] **RTL uses logical Tailwind classes** (`ms/me`, `ps/pe`, `start/end`, `text-start/end`).
- [ ] **No forbidden dependencies** (rejection list §17).
- [ ] **No default exports except lazy pages.**
- [ ] **No direct `localStorage`/`sessionStorage`** outside the storage wrapper.
- [ ] **No hardcoded routes.**
- [ ] **No API responses stored in Zustand.**

Any failed line blocks completion. The runnable gates live in the **Engineering Definition of Done** ([`07`](07-definition-of-done.md)).
