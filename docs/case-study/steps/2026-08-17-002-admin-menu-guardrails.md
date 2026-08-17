# Step 002: Admin menu build — guardrail model, customization tiers, setup vs maintenance

- Date: 2026-08-17
- Session or task: Admin menu-creation workflow (follow-up that supersedes step 001's framing)
- Owner and tools: Yaren (product decisions), Erk (technical reality and product direction),
  Claude (source reading, structure proposal, concept prototype). Tools: read-only source read of the
  Lovable prototype copy in this repo, in-app browser pane, self-contained HTML prototype, npm
  registry and GitHub API for dependency verification.
- Type: decision
- Status: captured
- Relevant commit: recorded at commit time; evidence directory
  `docs/case-study/evidence/2026-08-17-002-admin-menu-guardrails/`.
- Supersedes: step 001 `2026-08-17-001-menu-workflow-poster-vs-list`. Step 001 remains valid as a
  record of the customer-side poster-vs-list exploration; its framing of "menu workflow" as a
  customer-screen question is replaced here.

## Question or problem

Erk clarified on 2026-08-17 that "menu workflow" does not mean the customer's menu screen. It means
the process by which a restaurant owner with no technical or design skill sets up their own menu and
keeps it maintained, so that the result is easy to produce, correct, and recognisably *theirs*.

Two forces pull against each other:

- More freedom for the operator produces a stronger sense of ownership, and more ways to produce a
  messy result.
- Less freedom produces a safe result that belongs to no one in particular.

Erk's constraint: an upmarket restaurant must not end up with a menu that shifts how it is perceived.
Erk stated he has no concrete solution for this either.

The concrete design question: **where does the editor need guardrails, and what exactly stays free?**

## Starting evidence

- Source or artifact:
  - `docs/PRODUCT-BRIEF.md` §12 (Admin is the operator's real working surface; calm, predictable,
    high capability with controlled density), §14 device matrix (Admin desktop-first,
    mobile-adaptable), §17 (1..n content languages, at least one; add a language and bind content;
    store and render characters correctly; no automatic translation; editor UI must not hardcode two
    fixed TR/EN columns), §25 Step 3 (Menu is the first full vertical slice: Admin Menu Editor and
    Customer Menu designed together), §28 (if the brief, backend and MenuTiger do not answer, leave
    the question open rather than inventing a feature).
  - Read-only source read of the Lovable prototype copy in this repo (`loveable prototype/src/`).
    The running application belongs to Erk's separate repository.
  - MenuTiger reference captures in `references/customer/` including
    `customer-04-localizations.png` and `customer-05-turkish.png`.
- Actual-product baseline screenshot: **not captured.** See the capture gap in the evidence README —
  the app was not run in this session (Supabase credentials and an authenticated operator account
  are required, and the running app is in Erk's repo).
- Tested route, state, locale, and viewport: concept prototype only, opened in the in-app browser at
  1120×900 and 375×812, locale TR.
- What was known, verified from source:
  - The menu appearance model is `MenuConfig`: three free hex colour fields, a heading font and a
    body font chosen independently from a 10-font list, a free hero image, hero title and subtitle,
    five display toggles, and one of three category-display modes. There is no contrast check and no
    type-pairing constraint. A 10×10 independent font choice permits, for example, Bebas Neue as
    body text.
  - There is **no logo field anywhere in the product.** Restaurant identity is `name` and `city`.
  - There is **no multilingual support anywhere in the product.** `menu_items` carries a single
    `name` and `description`, and no locale column, translation table, or language switcher exists.
  - Spreadsheet import works today (CSV/JSON, column mapping, preview; requires name, price,
    category).
  - A maintenance surface already exists and works: the Items tab has drag-to-reorder, per-item and
    bulk availability toggles, and an edit drawer.
  - The "Canva" tab is exactly the approach Erk set aside: upload a design, auto-recognise blocks,
    store bounding-box placeholders, render the customer menu as the image with tappable overlays,
    with a manual mapper for correcting boxes.
- What remained unknown: whether a first-run guided sequence is in scope; how many templates;
  whether logo capture is in scope; what a real operator considers "theirs".

## Alternatives and rationale

### Reviewing the proposal brought in from ChatGPT

The incoming proposal (structured content plus a guardrailed layout composer, six steps: fetch
content → structure → choose direction → add brand → preview → publish) was reviewed. **The
architectural call is sound and is kept**: separate the content model from the presentation, and
compose presentation from validated parts rather than from free-form editing.

Three gaps were identified in review and are addressed below.

### Gap 1 — brand differentiation

The proposal's own "premium menu" example carried no trace of any specific restaurant: no logo, no
name treatment, no colour of its own. Elegant and generic. That does not demonstrate Erk's
requirement that perception must not shift.

Direction proposed: **freedom is spent on identity, not on layout.** The operator gets wide latitude
in the inputs that say who they are (logo, restaurant name, cover, photography, one brand colour,
their own words) and effectively none in how those are arranged (scale, spacing, contrast, alignment,
component structure). Differentiation then comes from the CUSTOMIZABLE tier and consistency from the
LOCKED tier, rather than the two competing.

This is testable, and tab 1 of the prototype is the test: three placeholder restaurants render
through one locked layout and read as three different businesses.

The single missing input that makes this work is **a logo**, which the product does not have today.
Whether adding it is in scope is a Yaren/Erk decision, not an assumption to make here (brief §28).

### Gap 2 — multilingual

Brief §17 requires a 1..n language model. The prototype has none, so this is a data-model question
before it is a UI question. Recorded as a proposal, not a lock:

- Content is authored in one **default language**, set once. That is the spine and must be complete.
- Additional languages are a **per-item overlay**, edited in a view driven by a completeness meter
  rather than by fixed TR/EN columns (§17 forbids hardcoding two columns).
- An untranslated item **falls back to the default language.** It is never hidden and never renders
  with an empty name.
- On the customer side, the language switcher's position is LOCKED; which languages are enabled is
  CUSTOMIZABLE.

Two typography consequences follow, and they constrain the CHOOSABLE tier directly:

1. Every offered type pairing must be verified for the character sets of the enabled languages.
   Turkish `ğ ş ı İ ç ö ü` is the immediate case, and `İ`/`ı` in particular is where display faces
   fail. Of the ten fonts offered today, at least one (Bebas Neue) is an uppercase-only display face,
   which cannot render the lowercase dotless `ı` distinction at all.
2. Translated strings change length substantially. A locked layout must survive two-line item names
   without breaking — which is an argument *for* locking layout rather than exposing it.

Open question left for Yaren/Erk: does the operator enter every language during first setup, or
publish in one language and add others later? Recommendation is the latter, so translation never
blocks the first publish, but this is not locked.

### Gap 3 — first setup versus daily maintenance

Erk stated maintenance sits with the restaurant owner, and a working maintenance surface already
exists in the prototype (Items tab). Resolution proposed:

- The guided sequence, if it exists at all, runs **once**. It is scaffolding to get from zero to a
  publishable menu.
- After publishing, the home is the **existing tabbed editor**. Daily work — mark an item sold out,
  correct a price, reorder, add an item — happens in the Items list and never re-enters a wizard.
- Every setup stage maps to a permanent editor tab. The sequence is an ordering over surfaces that
  already exist, not a separate product.
- Device consequence, consistent with the locked matrix in brief §14: the full editor is
  desktop-first, but the daily availability toggle must work on a phone, because that is the action
  an operator performs while standing in the restaurant.

**Decision — Yaren, 2026-08-17:** a first-run guided sequence **is** in scope, in the
"wizard plus tabs" form above. The guided sequence runs once for a new operator; the tabbed editor
remains the permanent home and the only maintenance surface. This is an ordering over surfaces that
already exist, not a new capability. Not yet reviewed by Erk.

### Guardrail mechanics considered

Four mechanisms, in decreasing order of confidence:

1. **Derived palette instead of a free palette.** The operator supplies one brand colour (or it is
   sampled from the uploaded logo) and the system derives the surface, text and accent roles with
   contrast checked. A colour that fails on small text is used only where it passes. A broken
   combination cannot be expressed, so it never has to be rejected. This replaces three free hex
   fields.
2. **Curated type pairings instead of two font dropdowns.** Three or four named pairings replace 100
   possible combinations, and the pairing set is filtered by the character sets of enabled languages.
3. **Photo policy per section, all-or-nothing.** Partially covered photography reads as messier than
   no photography. Demonstrated by the "Fotoğraf kapsamı" switch in tab 1.
4. **Content-quality nudges rather than blocks** — items missing prices, a section with far too many
   items, descriptions of wildly uneven length. Inconsistent content is a larger contributor to a
   messy result than colour is. Lowest confidence of the four; not proposed for locking.

### Rejected

- **Free-form drag-and-drop page building.** Erk raised Craft.js. A page-builder framework grants the
  operator more layout freedom, which is the opposite of the stated requirement. Adding a builder in
  order to prevent messy output is backwards. See the feasibility note below.
- **Rendering the customer menu as an uploaded design with tappable overlays.** Already rejected in
  step 001 on affordance grounds, and independently confirmed here in source: overlay boxes are
  derived from text-fragment positions, which is not the same shape as a tap target and moves under
  any scaling.

## Change or experiment

An interactive concept prototype with three tabs:

1. **Brand test** — three placeholder restaurants through one locked layout, with a switch between
   the proposed guarded system and the freedom today's `Customiser` actually permits, plus a photo
   coverage switch.
2. **Three tiers** — first draft of LOCKED / CHOOSABLE / CUSTOMIZABLE with the allocation rule.
3. **Setup ↔ maintenance** — six first-run stages each mapped to its permanent editor surface, and
   the three recurring maintenance jobs.

- Prototype reference: `../evidence/2026-08-17-002-admin-menu-guardrails/guardrail-model.html`
- Evidence directory: `docs/case-study/evidence/2026-08-17-002-admin-menu-guardrails/`

## Technology feasibility note

Verification date 2026-08-17, Europe/Istanbul.

**Application stack, read from `loveable prototype/package.json`:** React 19.2, TanStack Start 1.167
and Router 1.168, Vite 7.3, Tailwind 4.2, Supabase JS 2.105, TypeScript 5.8.
Already present and relevant: `@dnd-kit/core` 6.3.1 and `@dnd-kit/sortable` 10.0 (drag-and-drop,
already used for section and item reordering), `pdfjs-dist` 5.7 (PDF text layer), `papaparse` 5.5
(CSV).

**Craft.js.** `@craftjs/core` latest published version is **0.2.12, published 2025-02-14**
(npm registry). Its declared peer range is `react: ^16.8.0 || ^17 || ^18 || ^19`, so it would install
against React 19.2. However, the newest commit in `prevwong/craft.js` is also **2025-02-14**
("chore: release (#729)", preceded by "feat: add support for react 19 (#726)"), meaning the project
has had **no release and no commit for roughly eighteen months** and is still pre-1.0.

Recommendation: **do not add it.** Two reasons, in order of weight. First, it solves the wrong
problem — it is a framework for building free-form page editors, and the requirement here is to
constrain the operator. Second, a dormant pre-1.0 dependency at the centre of the editor is a poor
trade when the reordering the guarded editor actually needs is already covered by `@dnd-kit`, which
is in the stack and already in use. This should be re-checked before any final technology decision.

**OCR.** Erk's summary is accurate, with one correction that matters:

- PDF and PPTX are handled by reading the **existing text layer**, not by optical recognition.
  `recognize.ts` buckets text fragments into rows by Y coordinate and splits at price tokens. This
  works and is genuinely useful.
- A flat image export (PNG/JPG straight out of Canva) has **no text recognition at all** in the app
  today. `parseImage` re-encodes the file through a canvas and returns `placeholders: []`. So "OCR
  reads my menu picture" is not currently true for images; it is true for PDFs and PPTX files.
- The overlay-mapping failure has a structural cause, visible in `recognize.ts`: placeholder boxes
  are the bounding boxes of *text fragments*. The box that contains a price string is not the region
  a customer would tap, and it moves whenever the image is scaled or the viewport changes.

Recommendation: keep the extraction as an **import accelerator** that produces structured items, and
drop the overlay rendering path. This is consistent with step 001's conclusion that ordering must
hang off an explicit control rather than a tappable picture.

Sources: <https://registry.npmjs.org/@craftjs/core>, <https://github.com/prevwong/craft.js>,
<https://api.github.com/repos/prevwong/craft.js/commits>.

## Validation and result

- Method and scenario: source read of the prototype's menu-editor implementation; interaction
  walkthrough of the concept prototype at two viewports; dependency verification against the npm
  registry and the GitHub API. No operator test, no user test.
- Actual-product result screenshots: **not captured** — see capture gaps in the evidence README.
- Observed result:
  - The same locked layout produces three visibly different restaurant identities from identity
    inputs alone. The proposition that guardrails and differentiation are compatible therefore
    survives a first heuristic check.
  - The free-configuration switch reproduces the failure mode Erk described using nothing but
    settings the current editor already offers, which supports treating unconstrained colour and font
    choice as the primary risk rather than as an edge case.
  - The prototype rendered cleanly at 1120×900 and 375×812 with no console errors.
- Feedback source and date: Erk, 2026-08-17, on the framing and technical constraints. The structure
  proposed here has **not** yet been reviewed by Erk or approved by Yaren.
- Failures or rejected details:
  - Nothing in the three-tier table is locked. It is a first draft for review.
  - Template count, "premium" definition, logo scope, and editor technology all remain open.
  - The demonstration uses placeholder restaurants invented for the prototype. It shows that the
    mechanism *can* differentiate; it does not show that a real operator would feel it does.

## Learning and next uncertainty

Established: the guardrail question has a workable shape — allocate every option to one of three
tiers using a single rule (does this distinguish this restaurant from another?), spend freedom on
identity inputs and lock arrangement. Established from source rather than assumption: the two
concrete blockers are the absence of a logo field and the total absence of a language model, and the
maintenance surface already exists so it does not need to be designed from scratch.

Decided during this step: the flow shape. Yaren selected wizard-plus-tabs on 2026-08-17, so the
first-run sequence is in scope and the tabbed editor stays the permanent home.

Not established: whether operators agree, how many templates are enough, what "premium" concretely
means in this product, and whether logo capture is in scope.

Single next question: **is adding a logo field in scope?** The brand-differentiation mechanism
proposed here depends on it — it is the one identity input the product does not have, and without it
the CUSTOMIZABLE tier cannot carry the differentiation the LOCKED tier gives up. It is a scope call
for Yaren and Erk, not a design decision, and it gates the tier table being locked.

## Provenance check

- [x] Claims are linked to current sources — brief sections, named source files in the prototype, and
      dated registry/API lookups.
- [x] Observation, interpretation, stakeholder statement, and verified fact are distinguishable:
      Erk's statements are attributed, source-verified facts are cited by file, and proposals are
      labelled as proposals.
- [ ] Required real screenshots and prototype references are attached — the concept prototype is
      attached and runnable; **running-product baseline screenshots are missing** and the gap, its
      cause, and its remedy are recorded in the evidence README.
- [x] No secrets or personal customer data are included.
- [x] `INDEX.md` contains this step.
