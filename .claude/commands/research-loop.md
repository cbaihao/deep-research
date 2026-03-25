Run an autonomous multi-cycle research loop from a tension statement. No draft or pre-defined sources required.

## Usage

**From tension (recommended — open discovery):**
```
/research-loop "Every attempt to own the payment intent layer failed — and now 6 teams are trying again. What's actually different this time, if anything?" 8h
```

**From tension with domain scope:**
```
/research-loop "tension here" 8h --domain "agentic payments, PFM history, open banking" --exclude "crypto speculation, Web3 hype"
```

**From existing draft (skips discovery, deepening only):**
```
/research-loop research/payment-intent-layer/draft-v2.md 8h
```

Time budget → max cycles at 2 cycles/hour. Default: 4h.

## What this does

**Discovery phase** (no draft, ~30% of cycle budget):
Each cycle: depth editor reads accumulated findings → outputs exploration directions (biased toward surprising and contradictory) → research workers explore in parallel → findings appended to discovery log. After 3-4 cycles, depth editor synthesises a draft skeleton when enough material exists to form a coherent thesis.

**Transition:**
Skeleton expanded into full first draft (`draft-v1.md`) using discovery log as evidence base.

**Deepening phase** (draft exists, ~70% of cycle budget):
Each cycle: depth editor identifies evidence gaps → research workers fill them → adversarial agent gates findings before merge → approved findings integrated into next draft version.

**Final:**
`paper-reviewer-editorial` enforces style, thesis coherence, and readability. Produces `draft-final.md`.

Terminates early if: depth editor finds no more high-leverage gaps, or two consecutive cycles produce zero approved findings.

---

## Step 1 — Parse arguments

Determine start mode:

**If `$ARGUMENTS` starts with a quoted string or contains no `.md` path:**
→ discovery mode. Extract:
- tension: the quoted string (everything before the time value and flags)
- time_budget: e.g. `8h`, `4h` (default `4h`)
- domain: value after `--domain` flag (optional)
- exclude: value after `--exclude` flag (optional)
- paper_dir: derive from tension — slugify the first 4-5 words, e.g. `research/agentic-payment-intent/`

**If `$ARGUMENTS` starts with a file path ending in `.md`:**
→ deepening mode. Extract:
- draft_path: the file path
- time_budget: e.g. `8h`
- paper_dir: directory containing the draft

If no arguments: ask the user for their tension statement.

## Step 2 — Compute cycle budget

```
max_cycles = floor(hours * 2)   # ~30 min per cycle
discovery_cycles = min(4, floor(max_cycles * 0.3))
```

Minimum: 2 discovery + 2 deepening = 4 cycles total.

## Step 3 — Resolve revision log

The revision log is `revisions.md` in `paper_dir`.
The loop agent creates it if it does not exist.

## Step 4 — Confirm and launch

Tell the user:
> "Starting research loop on: **[tension or draft filename]**
> Mode: [discovery → deepening | deepening only]
> Budget: [max_cycles] cycles (~[hours]h) — [discovery_cycles] discovery + [max_cycles - discovery_cycles] deepening
> Output: [paper_dir]
> Running in background — I'll report back when complete."

Then invoke the `research-loop` agent as a general-purpose agent, with the full contents of `.claude/agents/research-loop.md` as instructions. Pass all resolved parameters.

Run in the background.

## Step 5 — On completion, report

- Final draft path
- Cycles run (discovery + deepening)
- How the thesis evolved from the original tension
- 5 most significant findings
- Any remaining open gaps
