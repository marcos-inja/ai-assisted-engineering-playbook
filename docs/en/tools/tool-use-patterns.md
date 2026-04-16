# Tool use (function calling, RAG, agents) — engineering patterns

## When to use / When to avoid

- **When to use**: whenever the agent needs evidence (repo, logs, metrics) or needs to act (run tests, open a PR, query a DB).
- **When to avoid**: bloated, overlapping toolsets. Fewer well-defined tools beat “a tool for every idea”.

## Signals things are going wrong

- **The agent can’t pick the right tool**: functional overlap; poor names/descriptions.
- **Argument hallucinations**: weak parameter validation; missing enums and constraints.
- **Huge outputs**: tool isn’t token-efficient; missing “top-k” and “files-only”.

## Operational checklist

### Tool design (contract)

- **Atomicity**: one responsibility per tool.
- **Restricted parameters**: enums, limits, formats.
- **Recoverable errors**: clear, action-oriented messages.
- **Minimal output**: summary + pointers (path/line/ID).

### Healthy agent loop

1) plan (impact map / task)  
2) act (edit/execute)  
3) observe (test/lint/query output)  
4) correct (until the oracle is green)  

### RAG vs JIT file refs

- **RAG**: best for scattered docs and knowledge outside the repo.
- **JIT file refs**: best when the repo is the source of truth (avoids bad chunking and stale context).

## Trade-offs and decisions

- More tools increases capability, but increases ambiguity and cost.
- Good tool errors enable fast self-correction with fewer iterations.

## Examples

### Pattern: “summary + evidence”

```text
Tool output:
- summary: <3–5 lines>
- evidence:
  - file: <path>
    lines: <n..m>
    note: <why it matters>
```

### Pattern: argument validation (anti-hallucination)

```text
- reject parameters outside an enum
- reject nonexistent paths (or require discovery first)
- require dry-run for destructive actions
```

## References

- [https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — minimal toolsets, low overlap, JIT context.
- [https://www.promptingguide.ai/agents/function-calling](https://www.promptingguide.ai/agents/function-calling) — practical overview of function calling in agents.

