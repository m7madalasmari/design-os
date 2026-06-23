# Page Manifest — <page name>

> Copy this file to `page-manifests/<page-name>.md` and fill it **before** implementation (see `design-protocols/01`).
> Label every reference-derived detail: **observed / inferred / approximate / unknown**. Never silently invent an unknown.
> Project is **Tailwind-first**: values map to tokens / Tailwind theme; no arbitrary values except Pixel Clone Mode (documented below).

- **Mode:** Pixel Clone | System Fidelity | Strict SSOT | Improved | Greenfield/System-First
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

## Demo Data Policy  *(if the page shows any sample rows / metrics)*
- Uses demo data: Yes / No
- Data type: 
- PII risk: *(must be none)*
- Labeling: *(how it is marked demo/sample)*
- Reason: *(preview / example / test)*
- *(No invented production data — see `00`. Demo data must be synthetic, PII-free, labeled, never shown as real.)*

## Content Rules
- *(content from the user/reference only; no invented copy; numerals/dates per `04`)*

## Layout Rules
- *(logical Tailwind utilities; token spacing scale; max content width per `layout.md`)*

## Token Var Exceptions  *(tokens with no Tailwind utility — z-index / duration / easing / control sizes)*
> Preferred: semantic Tailwind class when the token is mapped. Allowed exception: `style`+`var(--token)` when no utility exists. Value from `tokens.css` only; never a raw value; never an arbitrary value where `var()` suffices. See `02`.

| Location | Token | Reason | Utility unavailable? |
|---|---|---|---|
|  |  |  |  |

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
- **QA Report Location:** Embedded (in this manifest) | Separate file · Path: ______  *(large task → separate `qa-reports/<page>.md` or `<page>.qa.md`; see `07`)*
- **Preview runtime:** Real Tailwind | Shim mirror | Static artifact | Unknown  *(see `03`)*
