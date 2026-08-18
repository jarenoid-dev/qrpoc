# QRPOC Menu Workflow working context

**Document status:** MIXED AUTHORITY — the section labels below are controlling
**Last updated:** 2026-08-18
**Purpose:** One agent-discoverable context for the current Menu Workflow vertical slice without changing approved product scope

## Authority key

- **A — APPROVED / BINDING PRODUCT CONTEXT:** owned by the approved Product Summary, binding product brief, approved IA, and explicit binding stakeholder decisions.
- **B — FIXED MENU WORKFLOW STAKEHOLDER DECISIONS:** direct current decisions for this workflow. They do not authorize features outside approved scope.
- **C — PROVISIONAL PROTOTYPE HYPOTHESES:** ideas to test. They may change after observation.
- **D — IMPLEMENTATION EVIDENCE:** facts verified in a dated local prototype snapshot. They are not target requirements and do not prove the canonical app's current state.

Do not merge these levels or infer approval from proximity, repetition, implementation, or Figma folder membership.

## A — Approved / binding product context

Authority is owned elsewhere; this section links instead of duplicating it.

- [`PRODUCT-BRIEF.md`](PRODUCT-BRIEF.md) is the binding repository product brief. Its §2 source priority and §28 decision protocol apply.
- [`information-architecture.md`](information-architecture.md) is the approved Level 1 IA secondary reference. Menu Workflow is the existing `Admin / Menu ↔ Customer / Menu` vertical slice; it does not extend that IA.
- The binding device matrix is in Product Brief §14.
- The binding target UI direction is in Product Brief §22: **Next.js, TypeScript, Tailwind, shadcn/ui**.
- Product Summary and IA artifacts retain their own authority. Nothing in this working-context document replaces or edits them.

## B — Fixed Menu Workflow stakeholder decisions

**Authority:** FIXED MENU WORKFLOW STAKEHOLDER DECISIONS
**Source:** Yaren's 2026-08-18 Menu Workflow durable-context instruction
**Scope boundary:** These decisions clarify the approved vertical slice; they do not authorize new product capabilities.

### Product and ownership

- Menu Workflow is an **Admin process**.
- Long-term menu content and recipe maintenance belongs to the restaurant owner / manager. Onboarding may assist, but ongoing maintenance cannot depend on the QRPOC team.
- The design problem is the process by which a restaurant creates and maintains its digital menu, not merely displaying a menu.
- The customer-facing result must remain perceptually consistent with the restaurant's identity and level. A high-end restaurant must not be reduced to a cheap, disorderly, generic digital menu.
- The separate `poster / presentation menu → ordering menu` customer flow is eliminated. Premium visual presentation and ordering interaction belong in the same customer experience.

Core problem statement:

> How can a restaurant manager with low technical and design literacy create and maintain a restaurant-specific premium interactive menu while the system protects a minimum quality bar?

This question is not authorization for features beyond approved scope.

### Device-context clarification

The Product Brief §14 matrix remains the owner of the fixed device decisions. Current clarification:

- Admin is desktop-first and mobile-adaptable. Mobile adaptability means selected away-from-desk tasks remain usable; it does **not** mean compressing the entire menu editor into a phone.
- Service Manager is worst-case phone-first and may be moving on the floor with limited hands available.
- These are context decisions for existing product roles, not new roles.

### Figma working organization

- Fixed QRPOC working folder: [Figma folder 639857573](https://www.figma.com/files/folder/639857573)
- Current prototype file: [Tablyx — Prototypes](https://www.figma.com/design/sgUHid9WPP6iUhSOc9oKVj/Tablyx---Prototypes)
- Read-only verification on 2026-08-18 confirmed the file key and these pages:
  - `00 · PROVISIONAL - Prototype Hypotheses`
  - `01 · Admin Menu Editor`
  - `02 · Customer Menu`
  - `90 · Archive`
- The frame `Admin Menu Editor ↔ Customer Menu · v0.1` exists on the provisional page and labels itself `PROVISIONAL`, `NOT APPROVED`, `NOT A REQUIREMENT`, and `TO VALIDATE`.
- Available Figma APIs do not expose the parent folder, so the prototype file's membership in folder `639857573` is **not technically verified** by this audit.
- Folder membership is organizational only; it never grants approval, canonical status, or requirement authority.

### Eliminated, parked, and weak directions

**Eliminated:** `poster menu → ordering menu`, because it duplicates information, adds a customer step, and creates unnecessary friction.

**Parked — not the primary workflow:** recreate an original PDF/menu visually by detecting text and coordinates and placing interactive hotspots over it. Identified problems: unreliable detection, imprecise coordinates, poor alignment, non-structural editability, reprocessing for maintenance, and fragile content-to-product mapping. Do not revive it as the default without new evidence.

**Weak directions:** unrestricted blank-canvas editing and Canva/Figma-like free visual composition. Drag-and-drop does not imply free positioning.

## C — Provisional prototype hypotheses

**Status:** PROVISIONAL
**Approval:** NOT APPROVED
**Authority:** NOT A PRODUCT REQUIREMENT
**Purpose:** Prototype hypotheses to validate
**Last updated:** 2026-08-18

> **These hypotheses do not authorize new customization capabilities.**

For current prototype work only, this allocation supersedes the tier allocation recorded in case-study [Step 002](case-study/steps/2026-08-17-002-admin-menu-guardrails.md). Step 002 remains unchanged as historical evidence.

### Core principle

- Restaurant controls: **content and art direction**.
- System controls: **composition and interaction quality**.

### Control-allocation hypotheses

| Domain | Control | Provisional allocation |
| --- | --- | --- |
| Layout | Overall layout family | CHOOSABLE |
| Layout | Section order | CUSTOMIZABLE |
| Layout | Item order | CUSTOMIZABLE |
| Layout | Internal geometry | SYSTEM-CONTROLLED |
| Layout | Responsive rules | SYSTEM-CONTROLLED |
| Layout | Arbitrary x/y positioning | OUTSIDE V1 |
| Layout | Freeform page/canvas composition | OUTSIDE V1 |
| Typography | Typographic direction | CHOOSABLE |
| Typography | Font pairing | SYSTEM-CONTROLLED |
| Typography | Hierarchy | LOCKED |
| Typography | Scale | LOCKED |
| Typography | Fine typography controls | LOCKED |
| Typography | Custom font upload | OUTSIDE V1 |
| Color | Brand seed | CUSTOMIZABLE |
| Color | Palette direction | CHOOSABLE |
| Color | Actual UI color system | SYSTEM-CONTROLLED |
| Color | Contrast | SYSTEM-CONTROLLED |
| Color | Semantic color usage | SYSTEM-CONTROLLED |
| Color | Per-element color customization | OUTSIDE V1 |
| Imagery | Restaurant photography | CUSTOMIZABLE |
| Imagery | Image presence | CUSTOMIZABLE |
| Imagery | Focal point | CUSTOMIZABLE |
| Imagery | Image strategy | CHOOSABLE |
| Imagery | Crop | SYSTEM-CONTROLLED |
| Imagery | Sizing | SYSTEM-CONTROLLED |
| Imagery | Responsive treatment | SYSTEM-CONTROLLED |
| Imagery | Free positioning | OUTSIDE V1 |
| Imagery | Decorative effects | OUTSIDE V1 |
| Menu structure | Category creation | CUSTOMIZABLE |
| Menu structure | Category naming | CUSTOMIZABLE |
| Menu structure | Category order | CUSTOMIZABLE |
| Menu structure | Item order | CUSTOMIZABLE |
| Menu structure | Move item between categories | CUSTOMIZABLE |
| Menu structure | Section presentation | CHOOSABLE where justified |
| Menu structure | Visual geometry | SYSTEM-CONTROLLED |
| Menu structure | Responsive arrangement | SYSTEM-CONTROLLED |
| Menu structure | Arbitrary canvas composition | OUTSIDE V1 |
| Item presentation | Item content | CUSTOMIZABLE |
| Item presentation | Item image | CUSTOMIZABLE |
| Item presentation | Presentation family | DERIVED FROM LAYOUT |
| Item presentation | Safe variants | CHOOSABLE where justified |
| Item presentation | Interaction contract | SYSTEM-CONTROLLED / LOCKED |
| Item presentation | Tap affordance | SYSTEM-CONTROLLED |
| Item presentation | Spacing | SYSTEM-CONTROLLED |
| Item presentation | Typography | SYSTEM-CONTROLLED |
| Item presentation | Per-item free styling | OUTSIDE V1 |

Color nuance: a restaurant's brand color does not have to map directly to the UI accent. The system may derive quality-safe, accessible colors from restaurant input.

Image-strategy directions currently being considered are **Text-led**, **Selective imagery**, and **Image-led**. These are prototype directions, not approved options.

Item-presentation directions currently being considered are **Editorial / text-led**, **Visual / image-led**, and **Compact / dense**. These are conceptual directions, not approved template names or features. The same underlying `MenuItem` may render differently while preserving one interaction contract.

Core drag-and-drop rule:

> Drag & drop = structural ordering, not visual composition.

Shared conceptual customer contract:

```text
Menu → Item → Customize → Add / Order
```

Validation model:

```text
Theory → Prototype → Observe → Keep / revise / reject
```

These hypotheses survived a theoretical reasoning round only. They are not final design decisions.

### Provisional design / test personas

**Status:** PROVISIONAL DESIGN / TEST PERSONAS
**Role authority:** NOT PRODUCT ROLES
**Requirement authority:** NOT PRODUCT REQUIREMENTS

The canonical product role remains **Admin / İşletmeci / Restaurant operator**. The personas are contrasting test contexts for that one role.

| Persona | Known restaurant context | Current status |
| --- | --- | --- |
| 1 | High-end / premium restaurant operator | Context known; operational details not yet recorded |
| 2 | Casual / burger-style restaurant operator | Context known; operational details not yet recorded |
| 3 | Unresolved contrasting restaurant context | **DO NOT INVENT** — exact type and details were not reliably recovered |

Shared test assumptions already established for the canonical Admin role:

- Technical literacy may be low.
- Design literacy may be low.
- Blank-canvas freedom is not automatically desirable.
- Structured starting points and quality guardrails are likely necessary, while restaurant individuality still matters.
- Creation and ongoing maintenance must both be tested.

No names, demographics, biographies, quotations, psychographics, or missing Persona 3 details are inferred here. The persona set is incomplete until direct evidence supplies the remaining operational dimensions.

## D — Implementation evidence

**Authority:** IMPLEMENTATION EVIDENCE ONLY — NOT A TARGET REQUIREMENT
**Verification date:** 2026-08-18, Europe/Istanbul
**Evidence boundary:** source read of the local `loveable prototype/` snapshot and [`qrpoc-atlas.html`](qrpoc-atlas.html). No product code was run or changed. The connected GitHub account could not access `erkucman/qrpoc`, so canonical-app currentness remains unverified.

### Target direction versus older/current prototype snapshot

| Context | Verified direction or version | Authority / constraint |
| --- | --- | --- |
| Binding target UI direction | Next.js · TypeScript · Tailwind · shadcn/ui | Product Brief §22; exact canonical-app pins unverified |
| Local prototype snapshot | TanStack Start `1.167.50`; TanStack Router `1.168.25`; React `19.2.5`; Vite `7.3.2`; Cloudflare Vite plugin `1.33.1`; Tailwind `4.2.4`; TypeScript `5.9.3`; Supabase JS `2.105.4`; shadcn-generated Radix components | [`bun.lock`](<../loveable prototype/bun.lock>) and [`package.json`](<../loveable prototype/package.json>); evidence only |
| Local toolchain | macOS `26.5.2` (`25F84`); Node `26.0.0`; npm `11.12.1`; Bun not installed | Local detection on 2026-08-18 |
| Pre-release in snapshot | `nitro` `3.0.260603-beta` | Existing prototype evidence only; not an approved target dependency |

Official currentness check, not an upgrade recommendation:

- Next.js official July 2026 security guidance identifies `16.2.11` as Active LTS; `16.3` was still Preview. The exact QRPOC target remains **unverified** until the canonical app manifest and compatibility constraints are available.
- TypeScript `7.0` is stable; Tailwind CSS `4.3` is current; shadcn's current tooling supports Base UI, React Aria, and Radix, with Base UI the new-project default and Radix still supported.
- TanStack Start's official current documentation labels Start **RC**. That reinforces the boundary between the snapshot architecture and the binding Next.js target; it is not a reason to change product design.
- Vite's official support page lists `7.3` as receiving important/security fixes, while regular fixes are on `8.1`.

Official sources: [Next.js releases](https://nextjs.org/blog), [TypeScript releases](https://devblogs.microsoft.com/typescript/), [Tailwind releases](https://tailwindcss.com/blog), [shadcn changelog](https://ui.shadcn.com/docs/changelog), [TanStack Start status](https://tanstack.com/start/latest), [Vite support](https://vite.dev/releases), and [Cloudflare Vite plugin](https://developers.cloudflare.com/workers/vite-plugin/).

### Import, recipe, and PDF evidence

| Claim | Audit result | Source / limitation |
| --- | --- | --- |
| Menu CSV / JSON import | Confirmed in local snapshot: upload, column mapping, preview, insert; requires name, price, category | [`menu-editor/import-dialog.tsx`](<../loveable prototype/src/components/menu-editor/import-dialog.tsx>) |
| Ingredient CSV / JSON import | Confirmed in local snapshot: upload, mapping, preview, bulk insert; requires name and unit | [`inventory/import-dialog.tsx`](<../loveable prototype/src/components/inventory/import-dialog.tsx>) |
| Recipe editing and costing | Confirmed in local snapshot: per-menu-item ingredient rows, quantities, dish cost, suggested price, margin, save | [`inventory/recipes.tsx`](<../loveable prototype/src/components/inventory/recipes.tsx>) |
| Recipe spreadsheet import | **Stakeholder-reported — repository verification pending** | No recipe spreadsheet importer was found in the local snapshot; canonical app repo was inaccessible |
| PDF import | Confirmed as PDF text-layer extraction plus page rasterization and heuristic name/price block parsing | [`parse-pdf.ts`](<../loveable prototype/src/components/menu-editor/canva/parse-pdf.ts>) and [`recognize.ts`](<../loveable prototype/src/components/menu-editor/canva/recognize.ts>) |
| OCR | **Not present in the audited current PDF/image tooling** | PDF uses existing text content; images are re-encoded with no recognition and empty placeholders |
| PPTX import | Partial: reads slide XML text/tokens and produces a simplified fallback render; it is not OCR or high-fidelity slide rendering | [`parse-pptx.ts`](<../loveable prototype/src/components/menu-editor/canva/parse-pptx.ts>) |
| Canva/PDF menu tooling | Partial: upload/review, structured item matching/creation, design pages, hotspots, and manual mapping exist | Local `menu-editor/canva/` snapshot; implementation evidence only |

OCR/extraction is a workflow direction to evaluate as **structured content ingestion** (`Name → Description → Price → Category → Review → Database`), not authorization to add AI/OCR or to reproduce the original visual layout.

### Actual menu hierarchy and move/reorder support in the snapshot

```text
restaurant
├── restaurant_menu_config (one presentation/config row used by the editor)
├── menu_sections[]
│   └── category_key (string identity + name, visibility, sort_order)
└── menu_items[]
    └── category (string matched to menu_sections.category_key)
```

- The audited editor does not use a separate persisted `menu` entity as its structural parent; restaurant scope plus one config row forms the menu context.
- `menu_sections` supplies category/section presentation metadata. `menu_items.category` links by string, not foreign key. The core table DDL is absent locally, so the hosted Supabase schema remains the schema authority.
- Section creation, rename, visibility, deletion, and drag reorder are implemented.
- Item drag reorder is implemented **within one category**.
- Moving an item between categories is implemented through the item edit drawer's Category selector and save.
- Cross-category drag-and-drop is not implemented in the snapshot.
- Deleting a section does not delete its items; string-linked items can become invisible/orphaned in the editor and preview.
- This model is an implementation dependency to review before Menu Editor implementation. It must not reshape the target product model by default.

## Open verification dependencies

- Canonical app repository access is required to verify current stack pins, imports, schema use, and whether snapshot behavior has changed.
- Recipe spreadsheet import remains stakeholder-reported and technically unverified.
- Hosted Supabase schema access is required to verify the actual database hierarchy and constraints.
- Figma API evidence confirms the prototype file and pages, but not its parent folder membership.
- Persona 3 and the operational dimensions of all three test personas require direct evidence; do not invent them.
