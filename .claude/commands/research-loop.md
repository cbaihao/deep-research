Run an autonomous multi-cycle research loop from a tension statement. No draft or pre-defined sources required.

## What's different from the original research-loop

- **Adversarial reads the draft**, not findings — identifies the 3 weakest arguments → those become the research agenda
- **Writer agent owns the argument** in deepening: receives adversarial critique, spawns research workers, gets findings back, synthesizes, rewrites
- **Hybrid rewrite**: affected sections rewritten in full + all section openers + all transitions; unaffected bodies left alone
- **Discovery phase unchanged** from classic loop

## Usage

**From tension (recommended):**
```
/research-loop "Every attempt to own the payment intent layer failed — and now 6 teams are trying again. What's actually different this time, if anything?" 8h
```

**With domain scope:**
```
/research-loop "tension here" 8h --domain "agentic payments, PFM history, open banking" --exclude "crypto speculation, Web3 hype"
```

**From existing draft (skips discovery, deepening only):**
```
/research-loop research/payment-intent-layer/draft-v2.md 8h
```

Time budget → max cycles at 2 cycles/hour. Default: 4h.

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

The revision log is `scratchpad/revisions.md` in `paper_dir`.
The loop agent creates it if it does not exist.

## Step 4 — Confirm and launch

Tell the user:
> "Starting research loop on: **[tension or draft filename]**
> Mode: [discovery → deepening | deepening only]
> Budget: [max_cycles] cycles (~[hours]h) — [discovery_cycles] discovery + [max_cycles - discovery_cycles] deepening
> Output: [paper_dir]
>
> **Deepening**: adversarial reads the draft each cycle → writer agent owns the argument → hybrid rewrite (affected sections + all openers + transitions)
>
> Running in background — I'll report back when complete."

Then invoke the `research-loop` agent as a general-purpose agent, with the full contents of `.claude/agents/research-loop.md` as instructions. Pass all resolved parameters.

Run in the background.

## Step 5 — On completion, report

- Final draft path
- Cycles run (discovery + deepening)
- How the thesis evolved from the original tension
- 5 most significant findings
- Named patterns introduced by the writer agent across all cycles
- Any remaining open gaps
