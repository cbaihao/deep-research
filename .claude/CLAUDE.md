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
    research-loop.md      — main loop controller (discovery ↔ deepening, v2)
    paper-depth-editor.md — direction setter for discovery cycles
    paper-writer.md       — argument-owning writer for deepening cycles
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
research/                 — output directory
  <paper-slug>/
    draft-final.md        — publication-ready output (only file at top level)
    scratchpad/
      discovery-log.md    — accumulated findings during discovery phase
      revisions.md        — revision log from all cycles
      draft-v0.md, draft-v1.md, … — intermediate versioned drafts
```

## Research loop phases
1. **Discovery** (~30% of cycle budget): explore broadly, accumulate findings, form thesis skeleton
2. **Transition**: skeleton written to `scratchpad/draft-v0.md`; writer agent expands on first deepening cycle
3. **Deepening** (~70% of cycle budget): adversarial reads draft → identifies 3 weakest arguments → writer agent owns each argument, spawns workers, hybrid-rewrites
4. **Editorial**: final paper-reviewer-editorial pass → `draft-final.md`

## Termination conditions
- Adversarial agent signals SATURATED (no web-researchable gaps remain)
- Two consecutive deepening cycles with zero new findings or argument changes
- Cycle budget exhausted

## Writing standards (non-negotiable)
- Every empirical claim must have inline citation
- No unsourced assertions
- Show logic chain explicitly for every major argument
- Steelman strongest objection in at least one section
- 400–700 words per section
- Style: direct claim openings, named concrete examples, non-consensus thesis

## Env vars required
- `ANTHROPIC_API_KEY` — Claude API key
- `EXA_API_KEY` — Exa.ai API key (for web search in research workers)
