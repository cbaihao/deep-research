# deep-research

Autonomous multi-cycle research agent powered by Claude + Exa.ai. Takes a tension statement and produces a publication-ready thesis paper through iterative discovery and deepening cycles.

## Usage

```bash
# Open this project in Claude Code
cd ~/allinai/deep-research
claude
```

Then use the `/research-loop` command:

```
/research-loop "Every attempt to own the payment intent layer failed — and now 6 teams are trying again. What's actually different this time, if anything?" 8h
```

With domain scope:
```
/research-loop "tension here" 8h --domain "agentic payments, PFM history, open banking" --exclude "crypto speculation, Web3 hype"
```

From an existing draft (deepening only):
```
/research-loop research/my-paper/draft-v2.md 4h
```

## Other commands

| Command | What it does |
|---------|-------------|
| `/research-loop` | Autonomous discovery → deepening → editorial pipeline |
| `/research-brief` | Guided 4-step brief builder before launching research |
| `/review-paper` | 5-reviewer parallel review cycle on any draft |
| `/research` | Single-shot deep research investigation |

## How it works

**Discovery phase** (~30% of cycle budget): broad exploration, no anchoring. Each cycle the depth editor outputs exploration directions → research workers search in parallel → findings accumulated in `discovery-log.md`. After 3–4 cycles a draft skeleton is synthesized.

**Deepening phase** (~70% of cycle budget): each cycle identifies evidence gaps → workers fill them → adversarial agent gates findings before merge → next draft version produced.

**Editorial pass**: `paper-reviewer-editorial` enforces readability and thesis coherence → `draft-final.md`.

## Output structure

```
research/<paper-slug>/
  discovery-log.md    — accumulated findings (discovery phase)
  draft-v0.md         — skeleton
  draft-v1.md         — first full draft
  draft-vN.md         — deepening iterations
  draft-final.md      — publication-ready output
  revisions.md        — review cycle log
```

## Setup

```bash
export ANTHROPIC_API_KEY=your_key
export EXA_API_KEY=your_key   # optional — enables live web search
```

## Agent architecture

```
/research-loop
  └─ research-loop (controller)
       ├─ paper-depth-editor        (discovery directions / evidence gaps)
       ├─ research-worker ×N        (parallel search + extract)
       ├─ paper-review-orchestrator (adversarial gating)
       │    ├─ paper-reviewer-structural
       │    ├─ paper-reviewer-evidence
       │    ├─ paper-reviewer-prose
       │    ├─ paper-reviewer-adversarial
       │    └─ paper-reviewer-factcheck
       └─ paper-reviewer-editorial  (final pass)
```
