# Step 004: Menu Workflow durable context, governance currentness, and persona audit

- Date: 2026-08-18
- Session or task: Menu Workflow durable context + currentness + persona audit
- Owner and tools: Yaren (stakeholder context); Codex (repository/source audit, documentation); Figma MCP (read-only); GitHub connector (read-only access check); official vendor/project documentation
- Type: research
- Status: captured
- Relevant commit: this documentation commit on `main`; the repository was already dirty before this task

## Question or problem

How can the current Menu Workflow context remain discoverable across Codex and Claude Code without promoting prototype hypotheses to requirements, duplicating binding sources, rewriting historical evidence, or treating an older prototype snapshot as the target product?

## Starting evidence

- Source or artifact: binding [`PRODUCT-BRIEF.md`](../../PRODUCT-BRIEF.md), approved Level 1 [`information-architecture.md`](../../information-architecture.md), root `CLAUDE.md`, stale/deleted root `AGENTS.md`, untracked stale `docs/AGENTS.md`, case-study Steps 001–003, local `loveable prototype/` source snapshot, `docs/qrpoc-atlas.html`, and Yaren's dated 2026-08-18 task instruction.
- Actual-product baseline screenshot: not applicable; this was a documentation/governance and source-audit task with no UI change.
- Tested route, state, locale, and viewport: not applicable. Figma file `sgUHid9WPP6iUhSOc9oKVj` was inspected read-only for pages and metadata.
- What was known: the product brief was committed as binding on 2026-08-15; `CLAUDE.md` routed to it; the old `AGENTS.md` still said no active brief; Menu Workflow hypotheses existed visually in Figma; Steps 001 and 002 were historical evidence.
- What remained unknown: whether an existing durable working-context/persona artifact existed; whether the canonical app could be accessed; whether recipe spreadsheet import was technically confirmed; whether the Figma API could prove folder membership.

## Alternatives and rationale

- Copy all facts into both agent rule files: rejected because it would multiply product context and risk authority drift.
- Add the provisional hypotheses to the binding brief or approved IA: rejected because it would promote working hypotheses into the approved hierarchy.
- Rewrite Step 002 with the new allocation: rejected because historical evidence must remain historical.
- Selected direction: one mixed-authority working-context document whose sections carry explicit A/B/C/D labels, one small documentation map, and narrow agent-routing references. This keeps facts in one durable home while preserving authority boundaries.
- Persona direction: keep the two known contexts short and operationally incomplete; leave Persona 3 explicitly unresolved instead of inventing it.

## Change or experiment

- Created `docs/MENU-WORKFLOW-CONTEXT.md` as the single current context artifact.
- Created `docs/README.md` as a documentation router that separates binding, working, implementation-evidence, reference, and process-evidence artifacts.
- Restored and currentized root `AGENTS.md`; aligned root `CLAUDE.md`; reduced nested `docs/AGENTS.md` and `docs/CLAUDE.md` to non-overriding routing files.
- Added this Step 004 record and evidence README. Step 002 and all earlier evidence were left unchanged.

- Prototype or running-product reference: [Tablyx — Prototypes](https://www.figma.com/design/sgUHid9WPP6iUhSOc9oKVj/Tablyx---Prototypes), inspected read-only.
- Evidence directory: `docs/case-study/evidence/2026-08-18-004-menu-workflow-context-audit/`

## Validation and result

- Method and scenario: repository inventory; complete read of current governance and evidence rules; targeted source verification of menu/ingredient imports, recipe editing, PDF/PPTX/image parsing, menu hierarchy, and reorder/move code; read-only Figma page/frame metadata; attempted read-only GitHub access to `erkucman/qrpoc`; official documentation currentness check; final Markdown-link and diff validation.
- Actual-product result screenshots: not applicable; no product or Figma UI was modified.
- Observed result: one context artifact now preserves all four authority levels; Codex and Claude route through the same docs map; the old `AGENTS.md`/`CLAUDE.md` source conflict is removed without making provisional content binding.
- Feedback source and date: Yaren's task instruction, 2026-08-18.
- Failures or rejected details:
  - Connected GitHub access to `erkucman/qrpoc` returned 404, so canonical-app currentness remains unverified.
  - Figma APIs verified the file key, pages, and provisional hypothesis frame, but did not expose parent-folder membership.
  - No repository or Figma persona artifact supplied Persona 3; it remains unresolved.
  - Recipe spreadsheet import was not found in the local snapshot and remains stakeholder-reported pending canonical verification.

## Learning and next uncertainty

The implementation snapshot supports structured menu and ingredient imports, recipe editing/costing, PDF text-layer extraction, section/item reordering, and category moves through item editing; it does not confirm recipe spreadsheet import or OCR. The canonical target remains Next.js/TypeScript/Tailwind/shadcn/ui, while the local TanStack/Vite/Cloudflare source is implementation evidence only.

The single next verification need is access to the canonical app repository and hosted schema before implementation decisions are made around the existing hierarchy or capabilities.

## Provenance check

- [x] Claims are linked to current sources and dated where currentness matters.
- [x] Binding context, stakeholder decisions, provisional hypotheses, and implementation evidence are explicitly distinguishable.
- [x] No UI screenshots apply; the read-only Figma and source-verification limits are recorded.
- [x] No secrets or personal customer data are included.
- [x] `INDEX.md` contains this step.
