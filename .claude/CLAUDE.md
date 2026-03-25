# Deep Research — Project Claude Instructions

## Purpose
Autonomous multi-cycle research agent. Takes a tension statement and produces a publication-ready thesis paper through iterative discovery and deepening cycles.

## Key commands
- `/research-loop` — Main autonomous research loop (discovery → deepening → editorial)
- `/research-brief` — Guided research brief builder with source curation
- `/review-paper` — Full 5-reviewer parallel review cycle on a draft
- `/research` — Single-shot deep research investigation

## Project structure
```
.claude/
  CLAUDE.md               — this file
  agents/
    research-loop.md      — main loop controller (discovery ↔ deepening)
    paper-depth-editor.md — direction setter for each cycle
    research-worker.md    — parallel per-section search/extract worker
    research-orchestrator.md — orchestrates workers into full draft
    paper-review-orchestrator.md — spawns 5 reviewers in parallel
    paper-reviewer-structural.md
    paper-reviewer-evidence.md
    paper-reviewer-prose.md
    paper-reviewer-adversarial.md
    paper-reviewer-factcheck.md
    paper-reviewer-editorial.md — final rewrite before delivery
  commands/
    research-loop.md
    research-brief.md
    research.md
    review-paper.md
  research/
    style-reference.md    — writing style guide (Aschenbrenner / PG / Altman)
research/                 — output directory for all drafts and revision logs
```

## Research loop phases
1. **Discovery** (~30% of cycle budget): explore broadly, accumulate findings, form thesis skeleton
2. **Transition**: skeleton → full first draft via research-orchestrator
3. **Deepening** (~70% of cycle budget): fill evidence gaps, adversarial review gates each cycle
4. **Editorial**: final paper-reviewer-editorial pass → `draft-final.md`

## Termination conditions
- Depth editor signals TERMINATE after widening directions find no new material
- Two consecutive cycles with zero adversarially-approved findings
- Cycle budget exhausted

## Writing standards (non-negotiable)
- Every empirical claim must have inline citation
- No unsourced assertions
- Show logic chain explicitly for every major argument
- Steelman strongest objection in at least one section
- 400–700 words per section
- Style: direct claim openings, named concrete examples, non-consensus thesis

## Output
All drafts written to `research/<paper-slug>/`:
- `discovery-log.md` — accumulated findings during discovery phase
- `draft-v0.md`, `draft-v1.md`, … — versioned drafts
- `draft-final.md` — publication-ready output
- `revisions.md` — revision log from review cycles

## Env vars required
- `ANTHROPIC_API_KEY` — Claude API key
- `EXA_API_KEY` — Exa.ai API key (for web search in research workers)
