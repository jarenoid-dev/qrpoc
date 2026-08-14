# QRPOC UX case-study evidence system

## Purpose and boundary

This directory preserves the product process needed to write a truthful UX case study later. It records what problem was addressed, what evidence informed the work, what changed, how the result was tested, and what was learned.

Capture is forward-only. It begins with the first QRPOC product task after this system is committed. Do not reconstruct previous steps from chat history, Git history, or memory, and do not present earlier artifacts as if they were captured through this process.

This is a process-evidence archive, not a product requirements source. A record may describe a decision or claim only with its source and verification status. `docs/DECISIONS.md` remains noncanonical until separately triaged.

## One task, one step record

Every future task that materially researches, defines, designs, prototypes, implements, tests, or revises QRPOC must:

1. Create `docs/case-study/steps/YYYY-MM-DD-NNN-short-slug.md` from `STEP-TEMPLATE.md`.
2. Add one chronological row to `INDEX.md`.
3. Save repository-safe evidence in `docs/case-study/evidence/YYYY-MM-DD-NNN-short-slug/`, or link a stable external prototype when the source artifact belongs in Figma or another design tool.
4. Complete the record before the task is considered done.

Use one record for one decision-sized task. Do not create an entry for every command or keystroke, and do not combine unrelated workstreams into one entry.

## Required evidence by task type

### UI or interaction work

- A baseline screenshot from the actual running product before the change.
- A runnable prototype reference: a tested application route and commit, or a stable Figma prototype/frame URL.
- Result screenshots from the actual running product after the change.
- The tested state, representative viewport sizes, interaction path, and observed result.
- Any feedback that changed the direction, with its source and date.

Static mockups, generated concepts, and annotated images may be supporting evidence. They do not replace the actual product or interactive prototype when one can reasonably be shown.

### Research or reference analysis

- Direct source links or repository paths.
- Screenshots for visual observations when relevant.
- Observations separated from QRPOC interpretations.
- The uncertainty reduced and the uncertainty that remains.

### Product or design decisions

- The decision question and its source.
- Alternatives considered.
- The selected direction and why.
- Decision owner and verification status.
- The artifact or experiment that can test the decision.

### Implementation or validation

- Relevant commit hash and tested route or scenario.
- Actual running-product screenshots for visible changes.
- Validation method, viewports or device, result, and failures.
- The next unresolved question rather than a speculative roadmap.

## Evidence quality rules

- Prefer original, unannotated captures. Keep annotations as separate files.
- Record enough context to reproduce the state: route, account or fixture type, viewport, locale, and relevant data condition. Never include secrets or personal customer data.
- Use descriptive lowercase ASCII filenames such as `01-baseline-orders-desktop.png`, `02-prototype-status-flow.mp4`, and `03-result-orders-mobile.webp`.
- Keep individual Git-tracked files below 25 MB. For larger prototypes or recordings, store the canonical artifact in the appropriate design or storage tool, add a stable URL to the step record, and commit representative screenshots.
- A link alone is not sufficient when the linked state can change. Pair it with dated screenshots and a commit, frame, or version identifier whenever possible.
- Failed experiments and rejected alternatives are valuable evidence. Record them without rewriting the outcome as inevitable.

## Definition of done

A task is not complete until its step record and index row exist and all available required evidence is linked. If a capture is impossible, the record must say exactly what is missing, why it is missing, and what would close the gap. An incomplete record must not claim a validated result.

The eventual UX case study should be synthesized from these records. It must not introduce metrics, research findings, user quotes, responsibilities, or outcomes that the evidence archive does not support.
