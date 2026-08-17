# Evidence — 2026-08-17-002 Admin menu build: guardrails, tiers, setup vs maintenance

Supersedes the customer-side framing of step 001. Step 001 asked what the customer sees;
this step asks what the operator can build and how far they can go wrong.

## Files

| File | What it is | How to open |
| --- | --- | --- |
| `guardrail-model.html` | Interactive concept prototype, three tabs: (1) brand-differentiation test with a guardrail on/off switch, (2) LOCKED / CHOOSABLE / CUSTOMIZABLE draft, (3) setup-vs-maintenance lane map | Open directly in a browser; self-contained, no network, no build |

## What the prototype demonstrates

**Tab 1 — brand test.** Three placeholder restaurants (upmarket, casual, café) render through
the *same locked layout*. Only the identity inputs differ: logo mark, restaurant name, one brand
colour, a named type pairing, cover, photo policy, welcome line. The "Bugünkü editör (serbest)"
switch reconfigures the same three menus using only settings that today's `Customiser` actually
permits — three free hex fields, independently chosen heading and body fonts from a 10-font list,
free hero title. The result is the failure mode Erk described: contrast collapse, lost hierarchy,
invisible prices, ragged photo coverage.

The "Fotoğraf kapsamı" switch shows the half-covered-photos case, which reads as messy independently
of colour.

**Tab 2 — three tiers.** First draft of the LOCKED / CHOOSABLE / CUSTOMIZABLE split, with the
allocation rule stated: an option is CUSTOMIZABLE only if it distinguishes this restaurant from
another one; otherwise it is CHOOSABLE from a validated finite set, or LOCKED.

**Tab 3 — setup vs maintenance.** Six first-run stages, each mapped to the permanent editor
surface it lives in afterwards, plus the three recurring maintenance jobs and their frequency.

## Interaction and viewport context

- Tested in the in-app browser pane at 1120×900 (desktop) and 375×812 (mobile preset), locale TR.
- Interactions exercised: all three tabs, guardrail on/off, photo coverage full/half.
- Console: no errors or warnings.
- Layout: phone columns collapse to a single column below ~760 px; body never scrolls horizontally.

## Code observations this prototype is based on

All verified by reading the Lovable prototype source in this repo
(`loveable prototype/src/`, read-only; the running application lives in Erk's separate repo).

| Claim | Source |
| --- | --- |
| Menu appearance config is 3 free hex colours + 2 independent fonts from a 10-item list + free hero image/title/subtitle + 5 display toggles + 3 category-display modes | `components/menu-editor/types.ts`, `components/menu-editor/customiser.tsx` |
| There is no logo field anywhere in the product | repo-wide search for `logo`; `restaurants` is selected as `id, name, city, client_id` |
| There is no multilingual support: `menu_items` carries a single `name` and `description`, and no locale/translation table or field exists | `components/menu-editor/types.ts`, repo-wide search for `locale`/`language`/`translation`/`i18n` |
| Spreadsheet import works: CSV/JSON, column mapping, preview, requires name + price + category | `components/menu-editor/import-dialog.tsx` |
| The maintenance surface already exists: drag-to-reorder, per-item and bulk availability toggle, edit drawer | `components/menu-editor/item-editor.tsx` |
| PDF/PPTX text extraction is real text-layer parsing, not OCR; a flat image has no text recognition at all — `parseImage` only re-encodes the file and returns `placeholders: []` | `components/menu-editor/canva/parse-pdf.ts`, `parse-pptx.ts`, `parse-image.ts` |
| Tappable overlays are bounding boxes derived from text-fragment positions, correctable by hand in a mapper | `components/menu-editor/canva/recognize.ts`, `canva/mapper.tsx`, `canva/api.ts` |

## Capture gaps

- **No baseline screenshots of the running product.** The Lovable application was not run in this
  session: it requires Supabase credentials and an authenticated `restaurant_owner` account, and the
  running app belongs to Erk's separate repository. Evidence here is source-read plus concept
  prototype. Closing this gap requires a session with working credentials against
  `qrpoc.lovable.app`, capturing `/menu-editor` Template / Customise / Items / Canva tabs.
- **No operator test.** Every judgement in tab 1 is heuristic, not observed. The claim that the
  guarded version reads as "the restaurant's own" and the free version reads as "messy" has not been
  put in front of a real restaurant owner.
- **Figma Slides deck not read in this session.** The deck *QRPOC - Product Summary - UX* is the
  top-priority source (brief §2) and no file key for it is recorded in this repository. Nothing in
  this step contradicts the brief, but the deck has not been checked for menu-editor content.
