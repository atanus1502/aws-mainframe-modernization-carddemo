# LinkedIn Post — graphify on a mainframe modernization repo

I pointed graphify at AWS's CardDemo sample repo this week — a mainframe modernization codebase mixing COBOL, CICS, IMS, DB2, MQ, and JCL with shell scripts, READMEs, sample data, and architecture diagrams. Here's what actually happened, numbers included.

**The result:** a 365-node, 471-edge knowledge graph built from 36 files, with community detection grouping them into 33 coherent clusters — no manual re-reading required to get oriented.

**What it surfaced that I wouldn't have caught skimming:** the root README turned out to be the single most-connected node in the whole graph (82 edges), and a VSAM catalog listing (LISTCAT output) was the #2 hub (52 edges) — it tied together nearly every dataset referenced elsewhere in the repo. The extractor also flagged genuinely uncertain relationships instead of silently guessing (e.g., whether a "Discount Group" data file really joins to "Account" data) — an honesty rule I didn't expect from a code-analysis tool.

**The honest part:** semantic extraction of docs and images needs an LLM pass, and two of my batched extraction attempts stalled for 10-20+ minutes with no output. Splitting the retry into one file per subagent instead of one big batch fixed it immediately — a good reminder that granularity matters when delegating LLM work, batching isn't free.

**The real payoff isn't the one-time build — it's every session after.** Building this graph cost ~815K tokens, spent once. A future session can now answer "how does X connect to Y" for ~1,500 tokens via `graphify query`, instead of re-reading ~200K tokens of raw files cold. That's roughly a 130x cost reduction per question, and the break-even point (~4 sessions of reuse) is easily cleared on any actively-worked repo.

**The limit worth naming:** graphify has no COBOL/JCL parser, so the 286 files that are the actual mainframe application logic here aren't in the graph at all — only the surrounding scripts, docs, diagrams, and sample data are. It's a real force multiplier for understanding a codebase's shape and documentation, not a substitute for reading the legacy code itself.

#AI #KnowledgeGraphs #MainframeModernization #ClaudeCode #DeveloperTools #LegacyModernization
