# QRPOC repository instructions

## Source status

- The binding product brief is `docs/PRODUCT-BRIEF.md` (QRPOC UI/UX Product Brief, 2026-08-15). Scope is locked: follow its §2 source-of-truth priority order and §28 decision protocol. Do not recover requirements from Git history, retired artifacts, generated memory, or prior chats.
- Start documentation discovery at `docs/README.md`. Its binding, working-context, implementation-evidence, reference, and process-evidence groups must remain separate.
- `docs/MENU-WORKFLOW-CONTEXT.md` is the current shared context for Menu Workflow prototype validation. Its provisional sections are explicitly non-binding, not approved, and not product requirements.
- This repository holds product/design documentation and case-study evidence. The canonical Lovable-connected application lives in the separate `erkucman/qrpoc` repository; the two repositories are intentionally not mirrors (2026-08-17).
- `docs/qrpoc-atlas.html` and `loveable prototype/` are evidence of an older/current prototype snapshot, not sources of target requirements or proof of the canonical app's current state.
- Do not invent project assumptions. Treat information as unknown unless it comes from the current task or an explicitly designated canonical source, and ask Yaren when a decision is required.
- `docs/REFERENCE-ANALYSIS.md` contains MenuTiger observations only. It is not a source of QRPOC requirements, decisions, or feature mappings.
- `docs/DECISIONS.md` is pending triage and is not a canonical decision source.
- Keep tasks narrow and single-purpose. Do not expand scope or propose features or architecture unless requested.

## Forward-only UX case-study evidence

- Evidence capture is forward-only. Do not reconstruct earlier QRPOC work from memory or imply that earlier steps were captured.
- Every future task that materially researches, defines, designs, prototypes, implements, tests, or revises QRPOC must add one step record under `docs/case-study/steps/` and update `docs/case-study/INDEX.md` before the task is complete.
- Follow `docs/case-study/README.md` and start from `docs/case-study/STEP-TEMPLATE.md`.
- Store repository-safe evidence under `docs/case-study/evidence/`. Never commit secrets, private customer data, credentials, or exports containing personal data.
- If required evidence cannot be captured, record the concrete reason and mark the step incomplete. Never fabricate or retroactively infer evidence.
