Guide the user through a structured 4-step research brief before launching autonomous research.

**IMPORTANT: Run steps 1–3 interactively in this conversation, then invoke the `research-orchestrator` agent for step 4. Do not skip approval gates. Do not combine steps.**

---

## Step 1 — Intake

The user has provided input via: $ARGUMENTS

If no arguments provided, ask:
> "What topic, thesis, or area would you like to research? Include any specific questions you want answered."

Wait for the user's response before continuing.

---

## Step 2 — Intent Definition

Based on the user's input, draft and present two things together:

**A. Research objective + angle**
A short paragraph (3–5 sentences) covering:
- What question or problem this research addresses
- The angle or framing that makes sense for this topic — infer it from context (e.g. understanding a historical precedent, mapping the current landscape, surveying existing solutions, explaining a concept accessibly, exploring what comes next). These are examples, not fixed categories. Describe the angle naturally as part of the objective.
- What the reader will come away knowing

**B. Proposed table of contents**
The key sections of the final article/output. Each section is a distinct topic the reader will understand after reading it.

```
1. [Section title] — [one sentence: what this covers and why it belongs]
2. [Section title] — ...
...
```

Aim for 4–7 sections. No filler sections.

Present A and B together, then offer this menu:

---
> **Does this capture your intent?**
>
> **A** — Approved, move to sources
> **B [numbers]** — Remove sections (e.g. "B 2 4" removes sections 2 and 4)
> **C** — Revise the objective or angle (describe what to change)
> **D** — Custom feedback
---

Rules:
- If B: remove the specified sections, renumber, re-present the full intent for one more confirmation before proceeding.
- If C or D: revise and re-present.
- Only proceed to Step 3 when the user picks **A** or a clear equivalent.

---

## Step 3 — Source Curation

Based on the approved intent and table of contents, compile a curated list of **10–20 sources**.

**Each source must meet at least one criterion:**
1. **Specific information** — directly answers a question that one of the approved sections needs (data, stats, case studies, primary accounts, original reporting)
2. **High-quality perspective** — an authoritative piece from a respected voice: founder or investor blog posts, academic papers, long-form journalism, notable interviews. If a recognised expert published something directly relevant, it belongs here.

**For each source, include:**
- Sequential ID number
- Title and author/outlet
- Which section(s) it serves (by number)
- One sentence on what it contributes
- URL if known, or a search query that will retrieve it

Write the full source list to `.claude/research/brief.json` under the `sources` key (create the `.claude/research/` directory if needed), using this schema per source:

```json
{
  "id": 1,
  "title": "<source title>",
  "author_outlet": "<author or outlet>",
  "serves_sections": [1, 3],
  "contribution": "<what this source provides>",
  "url_or_query": "<url or search query>"
}
```

Then tell the user:
> "I've compiled [N] sources. Launching the source review — use ↑↓ to navigate, Space to mark sources for removal, Enter to confirm."

Then run the interactive source selector:

```bash
npx ts-node scripts/select-sources.ts
```

After the script completes, read the updated `.claude/research/brief.json` to see which sources remain.

Then present the trimmed source list to the user and offer the final menu:

---
> **Final check:**
>
> **A** — Approved, lock brief and launch research
> **B** — Add sources (paste URLs or describe what to add)
---

If B: append the user's sources to the list in brief.json (assign sequential IDs), confirm additions, then proceed.
Only proceed to Step 4 when the user picks **A** or a clear equivalent.

---

## Step 4 — Lock Brief and Launch Agent

Once sources are approved:

**4a. Ensure `.claude/research/brief.json` is complete** with the full approved schema:

```json
{
  "topic": "<topic>",
  "intent": "<approved objective + angle from step 2>",
  "table_of_contents": [
    { "section": 1, "title": "<title>", "description": "<what this section covers>" }
  ],
  "sources": [ ... ],
  "approved_at": "<YYYY-MM-DD>"
}
```

**4b. Confirm to the user:**
> "Brief locked — [N] sections, [N] sources. Launching research agent."

**4c. Invoke the `research-orchestrator` agent** to execute the research autonomously.
