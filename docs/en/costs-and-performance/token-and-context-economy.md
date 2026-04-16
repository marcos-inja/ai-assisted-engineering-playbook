# Token & context economy (reduce cost without losing quality)

## When to use / When to avoid

- **When to use**: whenever cost or latency matters — especially for agents (multiple iterations).
- **When to avoid**: “compression” that removes invariants/decisions; cutting context without oracles increases rework.

## Signals things are going wrong

- **Prompts grow every iteration**: missing compaction; old tool outputs get re-injected.
- **Verbose outputs**: missing `max_tokens`/limits and missing a structured format.
- **Too much searching**: poor navigation, confusing toolset, missing notes/memory.

## Operational checklist

### 1) Stop paying for unnecessary text

- **Limit output**: “answer in up to N bullets” + `max_tokens`.
- **Format**: prefer short JSON/Markdown when you need to parse.
- **No duplication**: don’t ask for “long explanations” alongside a patch.

### 2) Context by reference

- Pass:
  - real paths
  - symbols
  - issue/PR IDs
  - commands to run
- Avoid:
  - pasting huge logs
  - pasting full files when only 30 lines matter

### 3) Summaries (compaction) as part of the workflow

When the conversation gets long:
- summarize decisions + plan + open items
- restart with the summary + the latest relevant files

### 4) Typical token cost drivers in engineering

- **Tool outputs**: search results and massive logs.
- **Chat history**: repeating context that is already “resolved”.
- **Bad RAG chunking**: large irrelevant chunks.

Mitigations:
- tools with “top-k” and “files-only” outputs
- clearing old outputs (“tool result clearing”)
- persistent notes outside the context window

### 5) Savings that don’t break quality

- **Retrieval/tool-output caching** with TTL.
- **Batching** (when applicable) for embeddings and repeated calls.
- **Routing** (cheap-first + gate) for trivial tasks.

## Trade-offs and decisions

- **More context** can reduce hallucinations *up to a point*; after that it increases confusion and cost.
- **Less context** requires a better harness (tools + oracles) to avoid guesswork.

## Examples

### “Token-efficient” review prompt

```text
Review this diff focusing on risks.

Output:
- max 10 findings
- each finding: risk (high/medium/low) + suggested action + recommended test
No long explanations.
```

### “Tool output contract” (for internal scripts)

```text
For any diagnostic command:
- return only: 1) summary, 2) top-10 relevant lines, 3) path/line/error
- provide a --full mode only on demand
```

## References

- [https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — context as a finite resource; compaction, note-taking, subagents.
- [https://redis.io/blog/llm-token-optimization-speed-up-apps/](https://redis.io/blog/llm-token-optimization-speed-up-apps/) — practical sources of token waste and containment strategies.

