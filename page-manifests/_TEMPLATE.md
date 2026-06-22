# Page Manifest — <page name>

> Copy this file to `page-manifests/<page-name>.md` and fill it **before** implementation (see `design-protocols/01`).
> Label every reference-derived detail: **observed / inferred / approximate / unknown**. Never silently invent an unknown.
> Project is **Tailwind-first**: values map to tokens / Tailwind theme; no arbitrary values except Pixel Clone Mode (documented below).

- **Mode:** Pixel Clone | System Fidelity | Strict SSOT | Improved
- **Direction:** RTL (ar) | LTR (en)
- **Theme:** neutral | theme-<brand>
- **Reference:** <image / link / none>

## Intent
- 

## Users
- 

## Primary Action (one)
- 

## Secondary Actions
- 

## Reference Analysis  *(label each: observed/inferred/approximate/unknown)*
- Page type: 
- Layout structure / main regions: 
- Grid & alignment: 
- Spacing observations: 
- Typography observations: 
- Color observations (→ tokens): 
- Border radius: 
- Shadows / depth: 
- Components: 
- Icons / images: 
- Content density: 
- RTL/LTR direction: 
- Ambiguous details: 
- Implementation assumptions: 
- Arbitrary values used + justification *(Pixel Clone Mode only)*: 

## Components Used  *(from `design-system/components/` only)*
- 
- Missing component/token → documented first in `design-system/`: 

## Data States
- Loading: 
- Empty: 
- Filled: 
- Error: 
- No Permission: 

## Content Rules
- *(content from the user/reference only; no invented copy; numerals/dates per `04`)*

## Layout Rules
- *(logical Tailwind utilities; token spacing scale; max content width per `layout.md`)*

## Responsive Behavior  *(mandatory)*
- Desktop: 
- Tablet: 
- Mobile: 
- Table: *(must not break the page; → cards on mobile? document)*
- Navigation: *(→ menu / drawer on mobile?)*
- Form: 
- Card / list: 
- Overflow handling: 
- Sticky elements: *(tested on mobile?)*

## Visual Polish and Motion

### Observed in Reference
- 

### Needed for This Page
- 

### Not Needed
- 

### Motion
- 

### SVG / Illustration
- *(Empty-state illustration: data/admin = simple icon only; marketing = illustration if it serves identity/meaning. The component spec `empty-state.md` wins on conflict — see `05`.)*
- 

### Interaction Feedback
- 

### Reduced Motion Handling
- 

### Performance Risks
- 

## Forbidden (this page)
- *(colors/values outside tokens · undocumented components · invented content · arbitrary values outside Pixel Clone · directional utilities in RTL · >1 primary)*

## Out of Scope
- 

## Post-implementation
- QA per `design-protocols/03` (system + visual + Tailwind compliance + `05` Required Output). Record mismatches and documented deviations.
