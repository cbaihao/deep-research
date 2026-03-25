# deep-research

An autonomous research agent that runs 4–8 hours without human intervention. Give it a tension statement — a contradiction or unresolved question — and it produces a fully sourced thesis paper.

Built on Claude and [Exa.ai](https://exa.ai).

---

## Setup

```bash
export ANTHROPIC_API_KEY=your_key
export EXA_API_KEY=your_key
```

Open the project in Claude Code:

```bash
claude
```

---

## Usage

```
/research-loop "Every attempt to own the payment intent layer failed — and now 6 teams are trying again. What's actually different this time?" 8h
```

Optional scope flags:

```
/research-loop "your tension" 6h --domain "fintech, open banking" --exclude "crypto"
```

Start from an existing draft (skips discovery):

```
/research-loop research/my-paper/draft-v2.md 4h
```

---

## How it works

```mermaid
flowchart TD
    START["/research-loop tension 8h"]
    START --> CONTROLLER

    subgraph CONTROLLER["research-loop  —  controller"]
        direction TB

        subgraph DISC["DISCOVERY LOOP  ~30% of budget"]
            D1["paper-depth-editor\nreads discovery-log\noutputs exploration directions"]
            D2["research-worker x N\nparallel Exa.ai search\none worker per direction"]
            D3[("discovery-log.md")]
            D1 --> D2 --> D3 --> D1
        end

        TRANSITION["TRANSITION\nsketch skeleton  →  draft-v1.md"]

        subgraph DEEP["DEEPENING LOOP  ~70% of budget"]
            P1["paper-depth-editor\nreads draft + revisions\noutputs evidence gap questions"]
            P2["research-worker x N\nparallel Exa.ai search\none worker per gap"]
            P3["paper-reviewer-adversarial\ngates each finding\nAPPROVE / REJECT"]
            P4[("draft-vN.md\nmerge approved findings")]
            P1 --> P2 --> P3 --> P4 --> P1
        end

        EDITORIAL["paper-reviewer-editorial\nfinal rewrite pass"]

        DISC -->|"skeleton ready"| TRANSITION --> DEEP
        DEEP -->|"saturated or budget exhausted"| EDITORIAL
    end

    EDITORIAL --> FINAL[/"draft-final.md"/]
```

### State files

```
research/<paper-slug>/
  discovery-log.md   — findings accumulated during discovery
  draft-v0.md        — thesis skeleton
  draft-v1.md        — first full draft
  draft-vN.md        — one version per deepening cycle
  draft-final.md     — final output
  revisions.md       — full cycle log (directions, findings, approvals, rejections)
```

Drop a `human-feedback.md` in the paper directory at any time — the depth editor picks it up each cycle.
