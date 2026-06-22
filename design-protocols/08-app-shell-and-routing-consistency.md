# 08 — App Shell & Routing Consistency

> The protocol is not per-page only. Pages share an app-level contract; a page must not silently invent shell / navigation / rhythm.

## Document once per app  *(app-level manifest — `page-manifests/_APP.md` recommended)*
- **App shell:** structure (sidebar / header / content / footer), container widths, sticky behavior.
- **Navigation:** primary nav items, active state, breadcrumb pattern.
- **Sidebar / Header / Footer:** contents, collapse behavior, RTL placement.
- **Route map:** the pages and how they relate.
- **Shared layout rules:** container width, section rhythm, spacing scale.
- **Shared responsive behavior:** breakpoints, nav → menu, table → cards, filters → drawer.
- **Shared states:** empty / loading / error patterns reused across pages.
- **Shared RTL behavior:** direction, logical utilities, what mirrors vs not.

## Rule
**A page must not introduce a new shell, navigation pattern, or layout rhythm unless explicitly requested.** A genuinely new shared pattern is documented at the app level **first**, then reused — never forked per page.

## Per-page vs app-level
- **App-level** (this file / `_APP.md`): shell, navigation, route map, shared patterns.
- **Per-page** (page manifest): content, page-specific components, page states.

## QA hook
`03` checks shell/nav consistency: a page reusing the documented shell passes; a page inventing one is flagged unless the manifest records an explicit request.
