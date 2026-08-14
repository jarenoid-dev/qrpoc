# QRPOC repository instructions

## Source status

- No active product brief currently exists. Do not recover requirements or instructions from Git history, retired artifacts, generated memory, or prior chats.
- Do not invent project assumptions. Treat information as unknown unless it comes from the current task or an explicitly designated canonical source, and ask Yaren when a decision is required.
- `docs/REFERENCE-ANALYSIS.md` contains MenuTiger observations only. It is not a source of QRPOC requirements, decisions, or feature mappings.
- `docs/DECISIONS.md` is pending triage and is not a canonical decision source.
- Keep tasks narrow and single-purpose. Do not expand scope or propose features or architecture unless requested.

## Forward-only UX case-study evidence

- Evidence capture starts with the first product task after this system is committed. Do not reconstruct earlier QRPOC work from memory or imply that earlier steps were captured.
- Every future task that researches, defines, designs, prototypes, implements, tests, or materially revises QRPOC must add one step record under `docs/case-study/steps/` and update `docs/case-study/INDEX.md` before the task is complete.
- Follow `docs/case-study/README.md` and start from `docs/case-study/STEP-TEMPLATE.md`.
- For meaningful UI or interaction work, capture the actual running product before the change, the interactive prototype, and the verified result. Static mockups may be additional evidence but do not replace a real product screenshot or runnable prototype when one exists.
- Record exact artifact paths or stable URLs, the tested route and state, representative viewport sizes, the relevant commit, what was learned, and what remains unknown.
- Store repository-safe evidence under `docs/case-study/evidence/`. Never commit secrets, private customer data, credentials, or exports containing personal data.
- If required evidence cannot be captured, record the concrete reason and mark the step incomplete. Never fabricate or retroactively infer evidence.
