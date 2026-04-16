# Context engineering (MVC, just-in-time, compaction, memory, subagents)

## When to use / When to avoid

- **When to use**: any multi-step agentic workflow, especially in large codebases; whenever cost or hallucinations become issues.
- **When to avoid**: “dump everything into the context” as a first strategy. It’s almost always worse.

## Signals things are going wrong

- **Bloated context** and the agent forgets prior decisions.
- **Repeated searching** (same queries, same files) → missing external memory/notes.
- **Inconsistent answers** across iterations → missing compaction + faithful summaries.
- **Chaotic tool use** → large, overlapping toolset; unclear tool contracts.

## Operational checklist

### Minimum viable context (MVC)

- **Instructions**: goal + constraints + output format (short and unambiguous).
- **Evidence**: canonical paths/symbols + 1–2 examples of the correct pattern.
- **Oracle**: validation commands and acceptance criteria.
- **Limits**: scope (folders/files) and output limits.

### Just-in-time context

- Pass **references** (paths/IDs/links), not the full content.
- Use tools to **load on demand**:
  - read a file/snippet when needed
  - search for a symbol/pattern
  - run tests/lint

### Compaction (summaries for long-horizon work)

- Summarize while keeping:
  - architectural decisions
  - invariants and constraints
  - pending bugs / hypotheses
  - current plan and next steps
- Remove:
  - old tool outputs (noise)
  - discarded drafts and alternatives

### External memory (note-taking)

Maintain a state file (e.g., `NOTES.md`) with:
- current hypothesis + evidence
- list of touched files
- decisions and trade-offs
- validation checklist

### Subagents

Use subagents to isolate:
- heavy exploration (repo sweeping, web research)
- diagnosis (performance/bugs)
- audits (security, tests)

The lead agent should receive **only a synthesis** (1–2 pages), not dumps.

## Trade-offs and decisions

### More context vs more focus

- **More context** increases cost and can reduce precision.
- **More focus** (MVC + JIT) tends to:
  - reduce hallucinations,
  - improve consistency,
  - lower cost.

### “RAG” vs “filesystem references”

- **RAG** is useful when:
  - knowledge is not in the repo (internal docs, wikis)
  - you must retrieve from a large corpus
- **References + JIT** is better when:
  - the repo is the source of truth
  - you want to avoid bad chunking and stale context

## Examples (ready-to-use patterns)

### Recommended context structure

```text
## Goal
...

## Non-negotiables
...

## Canonical references (paths/symbols)
- ...

## Validation
- ...

## Output contract
...
```

### “Tool results clearing” (practical)

Rule of thumb: after using a tool output, **don’t re-inject** the raw content back into the context; keep only:
- the conclusion
- the minimal evidence (path + line + error)
- the next step

## References

- `https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents` — MVC, JIT, compaction, note-taking, subagents; warns about context rot.
- `https://cursor.com/blog/agent-best-practices` — context management in real agent workflows.

