# deep-research

An autonomous research agent that runs 4–8 hours without human intervention. Give it a topic and it produces a fully sourced thesis paper.

Built on Claude and [Exa.ai](https://exa.ai).

---

## Setup

**Anthropic access** — one of:
- Enterprise / SSO users: run `claude` and log in via your organisation's SSO. No API key needed.
- Individual users: get an API key from [console.anthropic.com](https://console.anthropic.com) and set it:
  ```bash
  export ANTHROPIC_API_KEY=your_key
  ```

**Exa access** (optional — enables live web search):
Get an API key from [dashboard.exa.ai](https://dashboard.exa.ai) and add the MCP server to your Claude Code settings (`~/.claude/settings.json`):
```json
{
  "mcpServers": {
    "exa": {
      "command": "npx",
      "args": ["-y", "exa-mcp-server"],
      "env": {
        "EXA_API_KEY": "your_exa_key"
      }
    }
  }
}
```
Without Exa, research workers fall back to fetching URLs directly — live search is disabled.

## Usage

```bash
claude
```

```
/research-loop "your topic here" 8h
```

---

## How it works

```
  /research-loop
         │
         ▼
  ┌──────────────────────┐
  │   research-loop      │
  │       agent          │
  └───────────┬──────────┘
              │
       ┌──────┴──────┐
       │    PARSE    │  tension → paper_dir, cycle budget
       └──────┬──────┘
              │
              ▼
╔═════════════════════════════════════════════╗
║           DISCOVERY LOOP × N               ║
║                                            ║
║  ┌──────────────┐                          ║
║  │ Depth Editor │                          ║
║  └──────┬───────┘                          ║
║         │ parallel                         ║
║  ┌──────┴──────────────────┐               ║
║  │ Worker │ Worker │Worker │               ║
║  └──────┬──────────────────┘               ║
║         ▼                                  ║
║  [discovery-log.md]                        ║
║                                            ║
║  repeat until READY                        ║
╚══════════╪══════════════════════════════════╝
           │ [discovery-log.md]
           ▼
╔═════════════════════════════════════════════╗
║           DEEPENING LOOP × N (~70%)        ║
║                                            ║
║  ┌─────────────────────────────────────┐   ║
║  │              Writer                 │   ║
║  │  [discovery-log.md]                 │   ║
║  │  [draft-vN.md]                      │   ║
║  │  [revisions.md]                     │   ║
║  │                                     │   ║
║  │  ┌───────────────────────────────┐  │   ║
║  │  │  Worker │ Worker │ Worker    │  │   ║
║  │  └───────────────────────────────┘  │   ║
║  └──────────────────┬──────────────────┘   ║
║                     │                      ║
║              [draft-vN.md]                 ║
║                     │                      ║
║              ┌──────▼──────┐               ║
║              │ Adversarial │               ║
║              └──────┬──────┘               ║
║                     │                      ║
║              [revisions.md]                ║
║                     │                      ║
║              └─────────────── Writer ↑     ║
║                                            ║
║  repeat until SATURATED                    ║
╚══════════╪══════════════════════════════════╝
           │
           ▼
    ┌──────────────────┐
    │ Editorial Agent  │ → [draft-final.md]
    └──────────────────┘
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
