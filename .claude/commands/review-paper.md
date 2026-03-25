Run a full review cycle on a research paper draft using 5 specialist reviewer agents in parallel.

## Usage
- `/review-paper` — reviews the most recently modified draft found in `research/`
- `/review-paper research/payment-intent-layer/draft-v1.md` — review a specific draft

## What this does
Invokes `paper-review-orchestrator` which spawns 5 reviewers simultaneously:
1. **Structural** — argument coherence, section ordering, internal contradictions
2. **Evidence** — citation gaps, vague sources, evidence-claim mismatches
3. **Prose** — filler, empty language, bloat, tonal inconsistency
4. **Adversarial** — strongest objections, weak assumptions, incumbent response
5. **Fact-check** — verifies specific numbers against primary sources via web search

Results are compiled into a unified review report, appended to the paper's `revisions.md` log, and a revised draft is written as the next version (e.g. `draft-v2.md`).

---

## Step 1 — Resolve the draft path

If `$ARGUMENTS` is provided and is a file path, use it directly.

If no arguments provided, find the most recently modified `.md` file under `research/` that is not named `revisions.md`:
```bash
find research/ -name "*.md" ! -name "revisions.md" -newer research/ | head -1
```
If multiple papers exist, list them and ask the user which one to review.

## Step 2 — Resolve the revision log path

The revision log lives in the same directory as the draft, named `revisions.md`.
- If it exists, pass it to the orchestrator.
- If it does not exist, create it with a minimal header:

```markdown
# Revision Log — [paper title]

## How to use this file
Each review round appends a new entry. Agents read this before each pass to avoid repeating resolved issues.

---
```

## Step 3 — Determine round number

Count the number of `## Round` entries in the revision log. The new round number is that count + 1.

## Step 4 — Confirm and launch

Tell the user:
> "Reviewing **[draft filename]** — Round [N]. Running 5 specialist reviewers in parallel (structural, evidence, prose, adversarial, fact-check). Will update `revisions.md` when complete."

Then invoke `paper-review-orchestrator` with:
- `draft_path`: the resolved draft path
- `revision_log_path`: the resolved revision log path
- `round_number`: the determined round number

Run it in the background. When the review completes, proceed immediately to Step 5.

## Step 5 — Produce the next draft

Once the review report and revision log are complete, produce the next draft version.

**Determine the next draft filename:** increment the version number from the current draft (e.g. `draft-v1.md` → `draft-v2.md`, `draft-v2.md` → `draft-v3.md`). Save to the same directory.

**Invoke a general-purpose agent** with the following task:

> You are a research paper editor. Your job is to produce a revised draft by applying all must-fix and should-fix items from the revision log to the current draft. Do not rewrite for style — only change what the revision log says to change.
>
> Inputs:
> - Current draft: [draft_path]
> - Revision log: [revision_log_path] — read the most recent Round N review section carefully
> - Output path: [next_draft_path]
>
> Process:
> 1. Read the full current draft
> 2. Read the revision log — extract all must-fix and should-fix items from the most recent round
> 3. Apply each fix in order:
>    - Correct factual errors (wrong numbers, wrong dates, wrong attributions)
>    - Fix internal contradictions
>    - Add missing arguments where the revision log specifies what the argument should be
>    - Remove or replace flagged examples (e.g. outdated DoNotPay)
>    - Reframe sections where the revision log specifies a new framing
>    - Reorder sections if structural fixes require it
>    - Fix redundancy (remove duplicate data blocks, consolidate repeated citations)
>    - Do NOT apply nice-to-fix/polish items — those are for a later pass
> 4. Write the full revised draft to [next_draft_path]
> 5. Return a change summary: list every fix applied, with the before/after for factual corrections

Tell the user when the new draft is ready, including its path and a brief summary of the most significant changes made.
