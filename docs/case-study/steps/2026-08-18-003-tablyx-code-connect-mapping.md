# Step 003: Tablyx → code Code Connect mapping (proposal, plan-blocked)

- Date: 2026-08-18
- Session or task: Tablyx design-system Code Connect groundwork (paired with a Figma
  typography pass on the DS file)
- Owner and tools: Yaren; Claude Code + Figma MCP (Plugin API, read-only) + local repo read
- Type: decision
- Status: captured
- Relevant commit: branch `docs/code-connect-mapping`, this session (2026-08-18); docs-only, no app code

## Question or problem

Can the Tablyx (Figma) design-system components be linked to QRPOC code components via
Figma Code Connect, and if so, what is the component-to-component mapping? The originating
brief named `jarenoid-dev/qrpoc` as the repo target, which conflicts with this repo's rule
that the runnable app lives in `erkucman/qrpoc`.

## Starting evidence

- Source or artifact: Tablyx – Design System (fileKey `SznEOiskoPnC0o9GWd7DS9`); local code
  snapshot `loveable prototype/src/`; repo `CLAUDE.md` (repo-separation rule).
- Actual-product baseline screenshot: not applicable — no running-product UI change.
- Tested route, state, locale, viewport: not applicable.
- What was known: Tablyx has ~24 reusable components; the snapshot is shadcn/ui "new-york".
- What remained unknown: whether Code Connect is even available on the current Figma plan;
  whether the library is published; which repo should hold `.figma.ts` files.

## Alternatives and rationale

Three fallback directions were offered once the plan blocker surfaced (see below):
(a) produce the mapping as a document now; (b) write code-source pointers into each Figma
component `description` (no Code Connect); (c) stop and revisit after a plan upgrade.
**Yaren selected (a)** — a mapping document that is plan-independent and convertible to
`.figma.ts` later. Rationale: it satisfies the brief's "propose the mapping before writing"
step, produces reusable groundwork, and touches no code or Figma component definitions.

Repo-target sub-decision: the mapping was inventoried against the **local snapshot**
(pragmatic, on-disk) while explicitly flagging `erkucman/qrpoc` as canonical to re-verify
against at activation. No files were written to the canonical app repo.

## Change or experiment

Produced `docs/code-connect-mapping.md`: 18 direct shadcn-primitive mappings (HIGH), 6
bespoke/composition targets, and a code-only gap list. Verified `button`/`badge` `cva`
variant vocabularies to ground the HIGH rows. No `.figma.ts` file was created (blocked).

- Prototype or running-product reference: none (static mapping; no runtime artifact).
- Evidence directory: `docs/case-study/evidence/2026-08-18-003-tablyx-code-connect-mapping/`

## Validation and result

- Method and scenario: live Figma MCP calls to test Code Connect availability + component
  enumeration; local file reads for the code inventory.
- Actual-product result screenshots: not applicable.
- Observed result: **Code Connect is blocked** — `list_file_components_for_code_connect`
  and `get_code_connect_suggestions` both returned "You need a Dev or Full seat on an
  Organization or Enterprise plan to use Code Connect" (debug UUIDs in evidence). Second
  blocker: the Tablyx library is unpublished. The mapping itself is captured and internally
  consistent, but **unvalidated against the canonical app** and not activated.
- Feedback source and date: Yaren, 2026-08-18 — chose the mapping-document path.
- Failures or rejected details: cannot generate/publish `.figma.ts` on this plan; mapping
  against the local snapshot may drift from `erkucman/qrpoc`.

## Learning and next uncertainty

This step established the full Tablyx→code correspondence and the exact prerequisites that
gate Code Connect (Org/Enterprise + Dev/Full seat, plus a published library). It did **not**
validate any mapping against the canonical repo or activate Code Connect. Single next
question: **if/when the plan is upgraded and the library published, do the mapped code paths
and prop interfaces still hold in `erkucman/qrpoc`?**

## Provenance check

- [x] Claims are linked to current sources (live Figma API, local reads, this session's decision).
- [x] Observation, interpretation, stakeholder statement, and verified fact are distinguishable.
- [x] Required references attached (mapping doc, inventories, blocker output); no product
      screenshots apply and the reason is recorded.
- [x] No secrets or personal customer data are included.
- [x] `INDEX.md` contains this step.
