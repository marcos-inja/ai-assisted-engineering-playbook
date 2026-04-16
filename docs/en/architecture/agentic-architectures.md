# Agentic architectures (single agent, multi-agent, contracts, observability)

## When to use / When to avoid

- **Single agent**: implement small/medium tasks with validation in the loop.
- **Multi-agent**: broad research, audits, migrations, incidents, and problems with high search depth.
- **Avoid multi-agent** when the problem is simple and local: cost and divergence increase.

## Signals things are going wrong

- **Agent stuck searching**: missing better navigation (LSP), missing indexing, or the request isn’t grounded.
- **Wrong tool choice**: overlapping toolset; unclear tool contracts.
- **“Black box” execution**: no tracing/logs of tool calls; impossible to tune.

## Operational checklist

### Tool contracts

For each tool (including internal scripts):
- **single responsibility** (atomic)
- **validated inputs** (enums/constraints)
- **recoverable errors** (clear, actionable messages)
- **token-efficient output** (summary + pointers)
- **low overlap** with other tools

### “Generator → evaluator” pattern

Separate roles:
- **Generator**: proposes and implements changes.
- **Evaluator**: validates against rubric and oracles (tests/lint/security).

### Observability

Record at minimum:
- model, version, temperature (if applicable)
- prompt + context (hash/version)
- tools called + args + duration
- cost (tokens) per step
- validation results (tests, lint, etc.)

## Trade-offs and decisions

- **More tools** ≠ better. Large toolsets increase ambiguity and cost.
- **Subagents** reduce context pollution for the lead agent, but require synthesis and decision criteria.

## Examples (architecture patterns)

### Multi-agent for discovery + implementation

```text
Lead:
  - defines goal and acceptance
  - delegates discovery to subagent A (codebase map)
  - delegates risks/security to subagent B
  - consolidates and produces impact map + tasks

Builder:
  - implements one task
  - runs tests and fixes until green

Reviewer:
  - applies rubric and suggests adjustments
```

### “Tool output minimization”

When designing internal tools, prefer:
- returning **IDs/paths/line ranges** instead of dumps
- returning **top-k** results
- supporting **count/files_only** modes for searches

## References

- `https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents` — minimal toolsets, JIT context, subagents.
- `https://arxiv.org/html/2604.01527v1` — strong (IDE-like) harness improves performance; validation tool usage correlates with solve rate.

