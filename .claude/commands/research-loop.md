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

---

## Step 2 — Pre-flight: present sources and confirm settings

Before computing the cycle budget or launching anything, do all three of the following interactively.

### 2a — Present planned sources

Based on the tension statement and domain (if provided), derive the research areas and source types the workers will target. Present them clearly:

```
📚 **Planned research sources**

**Search domains:**
- [Derive 4–8 specific domains from the tension, e.g. "stablecoin adoption data", "USDC/USDT market share reports", "payment rails benchmarks"]

**Source types:**
- Exa web search (live — academic papers, news, analyst reports, company blogs)
- Direct URL fetches (when specific sources are known)
- [Any domain-specific outlets implied by the tension, e.g. "Fed/BIS publications" for macro topics, "GitHub/whitepapers" for technical topics]

**Excluded:** [exclusions if provided, else "none"]
```

### 2b — Ask for iteration count

Print the following deepening loop diagram, then the multiple-choice question, together in one message so the user has context on what a cycle means:

```
┌─────────────────────────────────────────────────────────┐
│              DEEPENING CYCLE  (repeats N times)         │
│                                                         │
│   draft-vN.md                                           │
│        │                                                │
│        ▼                                                │
│  ┌─────────────┐                                        │
│  │ Adversarial │  ← reads the full draft               │
│  │   Agent     │    finds the 3 weakest arguments       │
│  └──────┬──────┘                                        │
│         │  critique + research questions                │
│         ▼                                                │
│  ┌─────────────────────────────────────────────┐        │
│  │              Writer Agent                   │        │
│  │                                             │        │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐   │        │
│  │  │ Worker 1 │ │ Worker 2 │ │ Worker 3 │   │        │
│  │  │  (Exa)   │ │  (Exa)   │ │  (Exa)   │   │        │
│  │  └──────────┘ └──────────┘ └──────────┘   │        │
│  │         findings ↑  ↑  ↑                   │        │
│  │  synthesize → hybrid rewrite               │        │
│  └─────────────────┬───────────────────────── ┘        │
│                    │                                    │
│               draft-v(N+1).md                          │
│                    │                                    │
│                    └──── loop ↑ (until SATURATED)      │
└─────────────────────────────────────────────────────────┘
```

Then ask:

```
How many total cycles would you like to run?

  A)  2 cycles  (~1h)  — quick pass, light coverage
  B)  4 cycles  (~2h)  — recommended ✓
  C)  6 cycles  (~3h)  — deep coverage
  D)  8 cycles  (~4h)  — exhaustive

Enter A / B / C / D, or type a custom number (default: B):
```

Wait for user response. Map A→2, B→4, C→6, D→8, or use the number directly. Use result as `user_cycles`. Default to 4 if no input.

### 2c — Ask about auto source discovery

Ask the user:

> Should research workers be allowed to **auto-discover additional sources** beyond the planned domains above?
> This lets workers follow citations, find related papers, and expand into adjacent topics they encounter mid-search.
> (y/n, default: y):

Wait for user response. Store as `auto_discover` (true/false, default true).

---

## Step 3 — Compute cycle budget

Use `user_cycles` (from Step 2b) as `max_cycles`.

```
max_cycles = user_cycles   # from user input, default 4
discovery_cycles = min(4, floor(max_cycles * 0.3))
```

Minimum: 2 discovery + 2 deepening = 4 cycles total.

Pass `auto_discover` to the research-loop agent so workers know whether to follow new sources they find (true) or stay strictly within the declared domains (false).

---

## Step 4 — Resolve revision log

The revision log is `scratchpad/revisions.md` in `paper_dir`.
The loop agent creates it if it does not exist.

---

## Step 5 — Confirm and launch

Tell the user:

> "Starting research loop on: **[tension or draft filename]**
> Mode: [discovery → deepening | deepening only]
> Budget: [max_cycles] cycles (~[hours]h) — [discovery_cycles] discovery + [max_cycles - discovery_cycles] deepening
> Auto source discovery: [enabled | disabled]
> Output: [paper_dir]
>
> **Deepening**: adversarial reads the draft each cycle → writer agent owns the argument → hybrid rewrite (affected sections + all openers + transitions)
>
> Running in background — I'll report back when complete."

Then invoke the `research-loop` agent as a general-purpose agent, with the full contents of `.claude/agents/research-loop.md` as instructions. Pass all resolved parameters including `auto_discover`.

Run in the background.

---

## Step 6 — On completion, report

- Final draft path
- Cycles run (discovery + deepening)
- How the thesis evolved from the original tension
- 5 most significant findings
- Named patterns introduced by the writer agent across all cycles
- Any remaining open gaps
