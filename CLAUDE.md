# QRPOC working rules

- The binding product brief is `docs/PRODUCT-BRIEF.md` (QRPOC UI/UX Product Brief, 2026-08-15). Scope is locked: follow its §2 source-of-truth priority order and §28 decision protocol. Do not recover requirements from Git history, retired artifacts, or prior chats.
- `qrpoc-atlas.html` (repo root) is the technical inventory of the current prototype's implementation state. It is evidence of existing behavior, not a source of target requirements (brief §2, item 5).
- Do not modify this repository beyond the task Yaren has assigned.
- Do not invent project assumptions. Treat information as unknown unless it comes from the current task or an explicitly designated canonical source, and ask Yaren when a decision is required.
- `docs/REFERENCE-ANALYSIS.md` contains MenuTiger observations only. It is not a source of QRPOC requirements, decisions, or feature mappings.
- `docs/DECISIONS.md` is pending triage and is not a canonical decision source.
- Keep tasks narrow and single-purpose. Do not expand scope or propose features or architecture unless requested.
- Forward-only UX case-study capture starts with the first product task after the evidence system is committed; do not reconstruct earlier work.
- Before completing every future QRPOC research, definition, design, prototype, implementation, or validation task, follow `docs/case-study/README.md`: add one step record, update the index, and attach the required real screenshots, prototype reference, validation context, and relevant commit. If evidence is unavailable, mark the step incomplete and state why; never fabricate it.
