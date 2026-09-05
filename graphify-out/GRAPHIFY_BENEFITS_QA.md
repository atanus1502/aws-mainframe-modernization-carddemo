# Benefits of Using graphify — Q&A

## Q: What is the benefit of using graphify?

Concretely, from this session: graphify turns loose files (diagrams, docs, code) into a structured, queryable map — instead of eyeballing 11 separate PNGs, you get one graph showing that "Menu" is the hub for 5 feature branches, that Transactions is the most densely-documented one, and 4 specific edges the extractor wasn't confident about (worth a human look). That's the value: surfacing structure, hubs, and gaps you wouldn't notice reading files one at a time, plus a `graphify query`/`explain`/`path` CLI to navigate it afterward instead of re-reading everything.

The tradeoff we hit directly: it's only as good as what it can parse. Tree-sitter code (Python, JS, Go, etc.) gets free, instant structural extraction; docs and images need an LLM pass (subagents here, which can be slow or stall — like the docs chunk did); and anything outside its language list — COBOL, JCL, BMS, DDL in this repo's case — is invisible to it entirely. So it's strongest on modern polyglot codebases plus their surrounding docs/diagrams, and much weaker as a tool for understanding mainframe application logic itself.

## Q: What about the agent not having to start afresh with each session to understand the codebase?

That's real and probably the biggest practical win: `graphify-out/graph.json`, `.graphify_manifest.json`, and the semantic cache persist to disk, so a future Claude session in this repo doesn't need to re-read and re-reason over every file from scratch — it can run `graphify query "<question>"` or `graphify explain "X"` and get an answer straight from the pre-built structure, and `--update` re-extracts only changed files instead of rebuilding everything. The skill even wires this in: if `graphify-out/graph.json` already exists, a natural-language question skips straight to querying it rather than re-running detection.

The caveat, given what we saw in this session: the graph only knows what got extracted, so it's only as fresh and complete as the last successful build — this repo's version (at that point in the session) still didn't cover the COBOL/JCL logic or the docs that had been abandoned, so a future session querying it would get confident-sounding answers that are silently incomplete unless someone tells it that.

## Q: What is the benefit of using graphify in numbers when I start a new Claude Code session?

Here are the concrete numbers, based on what this build actually produced (not a hypothetical):

**One-time build cost (already paid, sunk):**
- 440,557 input tokens across the two extraction runs at that point in the session (image/data/script analysis by subagents)
- This is a cost paid *once*. Every future session reuses it for free until something changes.

**What a fresh, memory-less session would otherwise have to read:**
- Raw corpus: 150,685 words ≈ **~195,000 tokens** just to ingest the 36 supported files (scripts, diagrams, sample data) well enough to reason about them — and that's *before* touching the 286 COBOL/JCL files this graph doesn't even cover.

**What a session reading the persisted graph instead pays:**
- `GRAPH_REPORT.md` (the audit summary — god nodes, communities, surprising connections, suggested questions): 7,737 bytes ≈ **~1,900 tokens**. That's **~100x cheaper** than re-reading the raw corpus, for a comparable "what's in here and how does it connect" understanding.
- `graph.json` (full structured data, if a session needs to query programmatically): 103,685 bytes ≈ **~26,000 tokens** — still **~7.5x cheaper** than the raw corpus, and it's structured (nodes/edges/communities) rather than prose an agent has to re-parse.
- A single `graphify query "<question>"` call: capped by `--budget` (default reasonable, e.g. 1,500 tokens) — answers *one specific question* for **~1,500 tokens** instead of grepping/reading multiple files to find the same answer.

**Break-even math:** the 440,557-token build cost pays for itself once roughly **2.3 future sessions** would otherwise each need a full ~195K-token comprehension pass over the same files (440,557 / 195,000 ≈ 2.3). Every session beyond that is pure savings — and per-question queries (~1,500 tokens vs. an open-ended multi-file search) save far more than that in normal day-to-day use.

**Caveat that matters here:** these numbers only hold for the 36 files graphify actually parsed. For the 286 COBOL/JCL/copybook files, there's no graph to query at all — a fresh session still has to read those cold every time, same as without graphify.

---

## Q: What is the benefit of using graphify in numbers, now that the graph is fully built (final numbers)?

The figures above were computed mid-session, before the docs and sample-data files were added. Here's the same math recomputed against the final, complete graph (365 nodes, 471 edges, 33 communities, all 36 supported files covered, 0 files outstanding).

**One-time build cost (already paid, sunk):**
- **814,806 input tokens** total across all 3 extraction runs (initial images/scripts, sample-data retry, full readmes retry). This is a cost paid *once* — it grew from the earlier 440,557 because closing the docs gap took two more rounds of subagent dispatches (including retries after two stalled attempts), but it bought a graph with zero remaining gaps in the supported corpus.

**What a fresh, memory-less session would otherwise have to read:**
- Raw corpus: 150,685 words ≈ **~195,900 tokens** (words × 1.3) to ingest the same 36 files — unchanged from before, since the corpus itself didn't grow, only how much of it graphify actually processed did.

**What a session reading the persisted graph instead pays:**
- `GRAPH_REPORT.md` (audit summary — god nodes, communities, surprising connections, suggested questions): 11,780 bytes ≈ **~2,945 tokens**. That's **~66.5x cheaper** than re-reading the raw corpus, and now the summary actually reflects the complete picture (e.g. the root README and VSAM catalog are now the top two "god nodes," which the earlier partial graph couldn't show).
- `graph.json` (full structured data): 314,590 bytes ≈ **~78,650 tokens** — **~2.5x cheaper** than the raw corpus. The ratio shrank from the earlier ~7.5x because the graph itself is now much richer (365 vs. 127 nodes), but it's still cheaper than raw text and, unlike raw text, it's machine-queryable.
- A single `graphify query "<question>"` call: still capped around **~1,500 tokens** per answer regardless of how big the underlying graph gets — **~130x cheaper** than a full re-read, and this ratio only improves as the corpus grows since the query cost stays flat.

**Break-even math:** 814,806 / 195,900 ≈ **4.2 future sessions**. Since the raw-corpus-read cost is unchanged (~195,900 tokens) but the build cost roughly doubled to close the docs gap, the break-even point moved from ~2.3 to ~4.2 sessions of reuse. Every session after that is pure savings — and because per-question queries stay flat at ~1,500 tokens no matter how large the graph grows, that saving compounds fastest in normal day-to-day use (asking specific questions), not in doing full re-reads.

**Caveat, unchanged:** these numbers only cover the 36 files graphify actually parsed. The 286 COBOL/JCL/copybook files still have no graph to query — a fresh session reads those cold every time, same as without graphify.

---

## Q: Does graphify use an LLM?

Yes and no — depends on the step:

- **Structural extraction (code files):** No LLM at all. It uses tree-sitter parsers (deterministic AST parsing) to pull functions, classes, imports, calls, etc. Free, instant, no API key — this is what built the graph from the 9 shell scripts.
- **Graph building, clustering, diagnostics:** Also no LLM — standard graph algorithms (community detection, centrality, etc.) via NetworkX.
- **Semantic extraction (docs, papers, images):** This *does* need an LLM, since it requires actual reading/vision, not parsing. But graphify itself doesn't call an LLM API directly by default. It checks for `GEMINI_API_KEY`/`GOOGLE_API_KEY` — if set, it calls Gemini directly. If not set (our case), it delegates the work to **the host agent** — which is why Claude subagents were dispatched all session to read the images and docs and write the extraction JSON, rather than graphify making any API call on its own.

Notably, it never reads `ANTHROPIC_API_KEY` or `OPENAI_API_KEY` — it's designed to be host-agnostic for the LLM step, assuming whatever agent is running it (Claude Code, in this case) does that work itself. Every subagent dispatch this session *was* the "LLM" graphify needed.

## Q: If I had a Gemini key, what was the benefit?

The main benefit: **the extraction cost would come out of Gemini's API bill instead of this Claude Code session's own token budget**, and it would run as fast, direct API calls from graphify's own code instead of manually dispatching, monitoring, and retrying Claude subagents.

Concretely, what would have changed in this session:
- **No subagent choreography.** With `GEMINI_API_KEY`/`GOOGLE_API_KEY` set, graphify calls `graphify.llm.extract_corpus_parallel(files, backend="gemini")` directly — it splits/parallelizes the doc and image extraction internally. No need to write per-chunk prompts, dispatch 20+ Agent calls, patch token counts by hand, or babysit stalls.
- **No stalls (likely).** The two multi-minute hangs hit during this build (the combined 16-file docs chunk, then the solo root-README chunk) were subagent/tool-loop behavior — a full agentic loop reading files, reasoning, and writing JSON via tools. A direct Gemini API call per file is much simpler plumbing, so that specific failure mode probably wouldn't have shown up.
- **814,806 tokens wouldn't have touched this session's context/budget at all.** That's the real number worth highlighting — the entire build cost was paid in this session's own compute. With Gemini doing the work, it becomes a separate, likely much cheaper, external bill instead of consuming Claude session tokens.
- **Same AST/code extraction either way** — that part never uses an LLM regardless of key.

The tradeoff: it requires an external Gemini API key and `pip install 'graphifyy[gemini]'`, and there's no way to say with confidence whether Gemini's extraction quality would match, exceed, or fall short of what the Claude subagents produced — that would need an actual side-by-side comparison, not something this session can assert.

---

*Note: the first three Q&As above reflect the graph state mid-session (before the docs/sample-data completion); the fourth Q&A recomputes the "numbers" answer against the completed graph. See `graphify-out/GRAPH_REPORT.md` and `graphify-out/cost.json` for the live, current figures going forward.*
