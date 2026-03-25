Run a deep research investigation into a specific topic or domain.

Use the deep-research-agent defined in .claude/agents/deep-research-agent.md.

The research topic is: $ARGUMENTS

The agent should:
1. Decompose the topic into 4–6 research angles before searching
2. Run 8–12 targeted Exa searches covering market landscape, timing signals, technical depth, customer/distribution, and risk
3. Synthesize findings into a structured Deep Research Report (NOT a list of search results)
4. Save the report to memory/research-[slug]-[date].md
5. Output a handoff summary and, if a clear opportunity emerged, format it as a Scout-compatible HANDOFF block for the researcher agent

Focus on depth and insight — not opportunity scoring. The goal is comprehensive domain knowledge.

Working directory: /Users/James/allinai/money-scout
