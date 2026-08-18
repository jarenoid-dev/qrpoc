# Tablyx → code Code Connect mapping (proposal)

**Status:** proposed · not activated · 2026-08-18
**Owner:** Yaren · **Author tool:** Claude Code

> This is a **planning artifact**, not an activated Code Connect setup. It records how each
> published Tablyx (Figma) design-system component would map to a code component, so that
> Code Connect template files (`.figma.ts`) can be generated mechanically once the two
> hard prerequisites below are met. Nothing here is validated against a running product.

## Why Code Connect is not activated yet

Verified live from Figma's own MCP API on 2026-08-18 (two tools, identical response):

```
You need a Dev or Full seat on an Organization or Enterprise plan to use Code Connect.
```
(`list_file_components_for_code_connect` and `get_code_connect_suggestions`; Figma debug
UUIDs recorded in the case-study evidence.)

Code Connect has **two blocking prerequisites**, neither currently met:
1. **Plan/seat** — Organization or Enterprise plan with a Dev or Full seat. The current plan
   does not enable the feature at all.
2. **Published library** — Code Connect only maps components **published** to a Figma team
   library. The Tablyx file's components are not published.

Until both are resolved, `.figma.ts` files cannot be published, so this document stops at
the mapping proposal (the "propose before writing" step).

## Source-of-truth caveat (read before using this)

The **code side** of this mapping was inventoried against the **local snapshot** at
`loveable prototype/src/` inside this repo (a Vite + React 19 + TypeScript + shadcn/ui
"new-york" scaffold, package name `tanstack_start_ts`, icon library `lucide`).

Per this repo's `CLAUDE.md`, the **canonical application code lives in a separate repo,
`erkucman/qrpoc` (Erk's), intentionally kept separate and not mirrored.** The local snapshot
may drift from the canonical app. **When Code Connect is activated, re-verify every code
path and prop interface against `erkucman/qrpoc`** before writing `.figma.ts` files.

## Figma source

- File: **Tablyx – Design System**, fileKey `SznEOiskoPnC0o9GWd7DS9`
- Component URL pattern (for `.figma.ts` `// url=` headers):
  `https://www.figma.com/design/SznEOiskoPnC0o9GWd7DS9/Tablyx?node-id=<NODE-ID>`
  (convert node id colons to hyphens: `1:361` → `1-361`)

The 24 top-level, reusable Tablyx components were enumerated live (names, node ids, and
variant axes) on 2026-08-18. Assembled screens (Templates) and doc/specimen frames are
excluded — they are compositions, not individually connectable components.

---

## A. Direct primitive mapping (HIGH confidence) — 18 components

Verified against the snapshot's `ui/button.tsx` and `ui/badge.tsx` `cva` variant vocabularies
(`button`: variant `default|destructive|outline|secondary|ghost|link`, size
`default|sm|lg|icon`; `badge`: variant `default|secondary|destructive|outline`). Other rows
are matched by component name + prop shape and should be re-read at activation time.

| Tablyx component | node id | Code component | Prop / variant mapping |
| --- | --- | --- | --- |
| Button | `1:361` | `ui/button.tsx` | `Type`→`variant` (Primary→`default`, Secondary→`secondary`, Ghost→`ghost`, Destructive→`destructive`, **Destructive · outline→`outline` + destructive className** — shadcn `outline` is neutral by default); `Size` lg/md/sm→`lg`/**`default`**/`sm`; `State`→CSS states + `disabled` (only Disabled is a prop); `Label`→children |
| Icon button | `1:398` | `ui/button.tsx` `size="icon"` | `Icon` (INSTANCE_SWAP)→children (icon element); `Size`→`h/w` className; `State`→CSS + `disabled` |
| Input | `1:508` | `ui/input.tsx` | `Value`→`value`/`defaultValue`; `State`→`disabled`/focus; `Validity`=Error→`aria-invalid`; `Filled`→CSS state; `Size`→className (base shadcn input has no size prop) |
| Form field | `1:532` | `ui/form.tsx` (+ `ui/label.tsx`) | `Label`→`FormLabel`; `State`=Error→`FormMessage`/`aria-invalid`; wraps an `Input` |
| Switch | `1:407` | `ui/switch.tsx` | `Value` Off/On→`checked`; `State`=Disabled→`disabled`; Focus→CSS |
| Checkbox | `1:420` | `ui/checkbox.tsx` | `Value` Unchecked/Checked/Indeterminate→`checked` (`true`/`false`/`'indeterminate'`); Disabled→`disabled` |
| Radio | `1:425` | `ui/radio-group.tsx` (`RadioGroupItem`) | `Value` Selected→group `value` match; Disabled→`disabled` |
| Tab | `1:439` | `ui/tabs.tsx` (`TabsTrigger`) | `Label`/`Icon`→children; `State`=Selected→active (`data-state`); `Focus`→focus-visible |
| Counter badge | `1:446` | `ui/badge.tsx` | `Count`→children; `Tone` Neutral/Accent/Destructive→`variant` `secondary`/`default`/`destructive` |
| Sidebar row | `1:551` | `ui/sidebar.tsx` (`SidebarMenuButton`) | `Label`/`Icon`→children; `State`=Selected→`isActive`; `Focus`→focus-visible |
| Table | `1:687` | `ui/table.tsx` (`Table`) | wrapper composing header/body/rows |
| Table row | `1:622` | `ui/table.tsx` (`TableRow`) | `State`=Selected→`data-state="selected"`; Hover/Focus→CSS |
| Table header | `1:637` | `ui/table.tsx` (`TableHeader` / `TableHead`) | column head cells |
| Pagination | `1:660` | `ui/pagination.tsx` | `Pagination*` parts (`PaginationContent/Item/Link/Previous/Next`) |
| Dialog | `1:959` | `ui/dialog.tsx` (Neutral) / `ui/alert-dialog.tsx` (Destructive) | `Heading`→`DialogTitle`; `Description`→`DialogDescription`; `Width` lg/md/sm→`max-w` className; `Tone`=Destructive→`AlertDialog` (confirm pattern) |
| Side panel | `1:1052` | `ui/sheet.tsx` | `Heading`→`SheetTitle`; `Meta`→`SheetDescription`; `Width` lg/md→`className`; side drawer |
| Toast | `1:1087` | `ui/sonner.tsx` (Sonner) | `Title`→message; `Detail`→`description`; `Status icon`→`icon`; `Tone`→type (`toast.success/warning/error`, Undo→action toast); `Action icon`→`action` |
| Table skeleton | `1:1107` | `ui/skeleton.tsx` | skeleton rows |

## B. Bespoke / composition (no single primitive) — 6 components

| Tablyx component | node id | Proposed code target |
| --- | --- | --- |
| Status stamp | `1:471` | **Custom `StatusBadge`** on top of `ui/badge.tsx` — the 6 `Status` values (Preparing/Ready/Delayed/Paid/Unpaid/Sold out) exceed badge's 4 generic variants and need semantic color variants; `Density` comfortable/compact→size className |
| Top bar | `1:552` | App header composition (no shadcn primitive) — likely a layout/route-level component in the canonical app |
| Filter bar | `1:623` | Composition of `ui/input.tsx` + `ui/button.tsx` + `ui/select.tsx` |
| Selection bar | `1:676` | Bespoke bulk-actions toolbar; `Count`→children |
| Empty state | `1:1106` | Bespoke `EmptyState` (compose `ui/card.tsx` + icon + text); `Icon` INSTANCE_SWAP, `Tone` Empty/Error |
| Kitchen ticket | `1:1215` | Kitchen-surface feature card — **not present in the snapshot** (Kitchen surface is unbuilt per the 2026-08-18 DS audit) |

## C. Code primitives with no Figma counterpart (gap observation)

These shadcn/ui primitives exist in the snapshot but have no Tablyx component. Recorded as a
**gap observation only** — not a proposal to build anything:

`select`, `dropdown-menu`, `tooltip`, `popover`, `alert`, `card`, `textarea`, `progress`,
`avatar`, `accordion`, `slider`, `breadcrumb`, `calendar`, `command`, `context-menu`,
`drawer`, `hover-card`, `menubar`, `navigation-menu`, `resizable`, `scroll-area`,
`aspect-ratio`, `input-otp`, `toggle`, `toggle-group`, `separator`, `carousel`, `chart`,
`collapsible`, `label`.

This overlaps the DS audit's HIGH finding "no Select/Dropdown + no Menu in Tablyx."

---

## Activation checklist (when both prerequisites are met)

1. Upgrade Figma to Organization/Enterprise with a Dev or Full seat.
2. Publish the Tablyx library to a team library.
3. In the **canonical** code repo (`erkucman/qrpoc`), add `@figma/code-connect`, a
   `figma.config.json` (parser `react`, include glob for `.figma.ts`), and
   `@figma/code-connect/figma-types` to `tsconfig.json` `types`.
4. Re-verify each row above against the canonical component paths and `Props` interfaces.
5. For each component, run `get_code_connect_suggestions` → `get_context_for_code_connect`,
   then author a **parserless** `ComponentName.figma.ts` (`figma.code\`...\``) — **never**
   `.figma.tsx` / `figma.connect()`.
6. Map every VARIANT value exhaustively (unmapped values render `undefined`).
7. Resolve INSTANCE_SWAP slots dynamically (`getInstanceSwap()` + `executeTemplate()`),
   never hardcode icon children.
8. `figma connect publish` from the canonical repo.

## Provenance

- Figma component inventory: measured live via the Figma Plugin API on 2026-08-18.
- Code inventory: `loveable prototype/src/` (local snapshot) on 2026-08-18; canonical =
  `erkucman/qrpoc` (unverified here).
- Every mapping is **proposed and unvalidated**. No `.figma.ts` file was created.
