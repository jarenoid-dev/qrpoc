# Step 001: Menu workflow — customer poster vs list, two versions kept

- Date: 2026-08-17
- Session or task: Menu workflow brainstorm (branch `claude/menu-workflow-brainstorm-9f0e8f`)
- Owner and tools: Yaren (product decisions), Claude (facilitation + concept prototypes). Tools: live Lovable prototype via browser, inline interactive widgets, self-contained HTML prototypes.
- Type: decision
- Status: captured
- Relevant commit: uncommitted at time of writing; branch `claude/menu-workflow-brainstorm-9f0e8f`.

## Question or problem

How should the QRPOC **customer** menu present the menu and support ordering? The running Lovable
prototype renders the customer menu as a Canva-designed background image with tappable overlays. This
brainstorm asked whether that approach is appropriate, and, given the assumption that operators want
to use their own designed poster, what the interaction should be.

Scope note (brief §1, §27): this is UX of existing capability — no new menu feature. Ordering,
guest session, items, categories, and languages already exist in the product.

## Starting evidence

- Source or artifact: live Lovable prototype `qrpoc.lovable.app`; in-repo technical inventory
  `qrpoc-atlas.html`; brief §8 (customer menu: fast-scannable, clear prices, items + request CTAs,
  low friction) and §13 (MenuTiger is a behavioral reference, not authority).
- Actual-product baseline screenshot: viewed in-session, not persisted as files — see the capture gap
  in `../evidence/2026-08-17-001-menu-workflow-poster-vs-list/README.md`.
- Tested routes/state: `/` (entry), `/menu-editor` (admin, restaurant "Adanadayım Pub"),
  `/t/{token}` (customer, Table 1 guest session). Locale TR, desktop browser pane.
- What was known: customer enters via table QR; admin menu editor has Template/Customise/Items/Canva;
  Items are structured (name, price, availability toggle, image); the customer menu is an image with
  overlay hotspots that are misaligned, with prices baked into the image.
- What remained unknown: whether operators actually require their exact full poster as the menu, or
  whether brand + a structured list is enough; real customer behavior at a table.

## Alternatives and rationale

- Entry-screen framing (direct menu / welcome gate / menu + context strip) was explored first, then
  set aside once Yaren clarified the subject is the existing Lovable prototype, not a greenfield entry.
- Image-first (Canva image + overlay) vs data-first (structured list). Data-first serves brief §8
  (scannable, correct prices) and avoids the overlay-mapping problem; image-first preserves the
  operator's designed poster.
- Within "keep the full poster", two interaction methods:
  - Yol 1 — tap directly on the poster. **Rejected.** A poster reads as a picture, so users do not
    perceive it as tappable (discoverability failure that can block ordering), and mapping hotspots
    onto an arbitrary uploaded image is fragile — the same flaw that misaligns the current prototype.
  - Yol 2 — poster stays, ordering hangs off an explicit "Sipariş ver" button that opens a searchable
    list. Preferred among poster-keeping methods because the button is an unambiguous affordance.
- Decisions made by Yaren during the session:
  - For now, assume the operator wants the **full poster** (data-first is parked, not discarded).
  - Keeping the poster's printed prices current is the **operator's responsibility**.
- Outcome: keep **two versions** rather than pick one now.

## Change or experiment

Two low-fi, brand-neutral concept prototypes with placeholder Turkish menu data (16 items, live
search + category filter):

- Version A — full poster is the whole menu + "Sipariş ver" → searchable order list.
- Version B — poster as a brand cover/hero, with the actual menu as a single searchable list.

- Prototype or running-product reference: `../evidence/2026-08-17-001-menu-workflow-poster-vs-list/version-a-full-poster-menu.html` and `version-b-poster-cover-list.html`.
- Evidence directory: `docs/case-study/evidence/2026-08-17-001-menu-workflow-poster-vs-list/`.

## Validation and result

- Method and scenario: interaction walkthrough of the concept prototypes; heuristic UX review of the
  full-poster + order-list method. No user or operator test.
- Observed result: the explicit "Sipariş ver" button resolves the ordering-affordance problem that
  Yol 1 and the current overlay approach have. Search + categories make a many-item list usable.
- Failures / open risks recorded:
  - Redundancy at scale (Version A): poster and list are two full copies of the menu, so a customer
    finds an item on the poster and then searches for it again in the list; the poster tends to become
    a skippable cover.
  - Price drift: prices appear both on the poster image and in the list data; at scale these can
    diverge, and the customer sees the mismatch at the moment of ordering even though upkeep is the
    operator's responsibility.
  - Ordering is incomplete in the prototypes: add-to-cart increments only; no quantity control, cart
    review, total, or send step yet.
- Feedback source and date: Yaren, 2026-08-17 — chose to keep both versions and record them.

## Learning and next uncertainty

Established the central structural tension (a fixed poster image cannot reflect live price/stock and
cannot be reliably made tappable) and the affordance principle (ordering must hang off an explicit
control, not a tappable image). Did not establish which version is correct.

Single next question: **does a real operator actually require the full poster as the menu, or is a
brand cover + structured list enough?** That answer decides Version A vs B and cannot be resolved by
assumption — it needs input from a real operator.

## Provenance check

- [x] Claims are linked to current sources (brief, live prototype routes, atlas).
- [x] Observation, interpretation, stakeholder decision, and heuristic judgment are labeled distinctly.
- [ ] Required real screenshots attached — live-product screenshots are session-only; gap and remedy documented in the evidence README. Concept prototypes are attached as runnable HTML.
- [x] No secrets or personal customer data included.
- [x] `INDEX.md` contains this step.
