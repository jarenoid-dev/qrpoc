# Evidence — 2026-08-17-001 menu workflow: poster vs list

Two candidate versions kept from the menu-workflow brainstorm. Both are low-fi, brand-neutral
concept prototypes with placeholder Turkish menu data. Open each `.html` directly in a browser.

## Prototypes

- `version-a-full-poster-menu.html` — Full poster is the whole menu (operator's designed image,
  all items). A persistent "Sipariş ver" button opens a searchable, category-filtered order list.
  This is the version under the locked assumption "operator wants the full poster."
- `version-b-poster-cover-list.html` — Poster is used only as a cover/brand hero at the top; the
  actual menu is a single searchable, category-filtered list (data-first). No separate order gate.

Both order lists carry 16 placeholder items across 4 categories to represent a real menu at some
scale; search and category chips are live.

## Current-product baseline observed (live Lovable prototype, `qrpoc.lovable.app`)

Read-only observations from the running product on 2026-08-17. Observation is separated from
QRPOC interpretation.

- Entry `/` shows "Restaurant POC" + "Staff sign in"; customer enters via a table QR at `/t/{token}`
  (guest session find-or-create). `/menu` without a table context redirects to `/`.
- Admin `/menu-editor` (restaurant "Adanadayım Pub") has tabs: Template · Customise · Items · Canva,
  plus Import. Items tab: "23 items", categories Starters (1) and Main (22); item rows carry image,
  name, price (shown in `$`), an availability toggle, edit, delete, drag-reorder, bulk-select.
- Customer menu at a table QR renders as a Canva-designed background image ("Fauget Coffee" template)
  with tappable pill overlays positioned over the printed items. Overlays are misaligned with the
  printed text; the printed prices are baked into the image.

Interpretation (QRPOC, not observed fact): the current customer menu couples a fixed design image
with an interactive overlay, so the visual layer and the live data layer are not reconciled, and the
overlay hotspots do not reliably map onto the image.

## Capture gap

Live-product screenshots (entry, menu-editor Items, customer poster menu) were viewed in-session via
the browser tool but not persisted as image files here, because that tool returns screenshots inline
rather than to disk. To close the gap: re-capture those routes and commit the PNGs, or reference the
in-repo technical inventory `qrpoc-atlas.html`. The routes and the live URL above make the states
reproducible for a fresh capture.
