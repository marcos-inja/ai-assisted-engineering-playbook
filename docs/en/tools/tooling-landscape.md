# Tools: landscape (how to choose without vendor lock-in)

## When to use / When to avoid

- **When to use**: selecting a productivity stack (IDE/CLI/agents/observability/evals) based on your context (team, compliance, cost).
- **When to avoid**: choosing tools by demo. The bar should be: *swap-ability* + integration with your harness.

## Signals things are going wrong

- **Silent vendor lock-in**: workflows depend on proprietary features with no escape hatch.
- **Tool becomes “the process”**: the team adapts work to the tool, not the other way around.
- **No observability**: you can’t see cost per feature, tool-use, or where it fails.

## Operational checklist

### Categories (and what to demand from each)

- **IDE copilots / editors** (in-flow assistance)
  - demand: repo-aware context, navigation, test execution, PR review
- **CLI coding agents** (bigger changes, automation)
  - demand: execution + iteration, small diffs, git/CI integration
- **Orchestrators (graphs/workflows)** (agent-powered products)
  - demand: loop control, retries, human checkpoints, state
- **Observability / tracing**
  - demand: logs for prompts/tools/costs, replay, eval datasets
- **Eval frameworks**
  - demand: execution-based when possible, CI gating, versioning
- **AI gateways**
  - demand: routing/caching/budgets, policies and auditability

### Selection criteria (practical order)

1) **Oracle integration**: tests/lint/typecheck/e2e  
2) **Context control**: rules/context files, JIT loading  
3) **Observability**: tracing and cost per task  
4) **Portability**: exportable configs; open APIs; protocols  
5) **Security/compliance**: isolation, redaction, policies  

## Trade-offs and decisions

- “All-in-one” tools speed up the start, but increase lock-in.
- A modular stack reduces lock-in, but requires more integration engineering.

## Examples

### Questions that eliminate 80% of bad choices

```text
1) Can I run tests/lint/typecheck in the loop?
2) Can I version rules/skills/workflows in the repo?
3) Can I see tool calls and cost per task?
4) If I switch vendors tomorrow, what breaks?
```

## References

- [https://cursor.com/blog/agent-best-practices](https://cursor.com/blog/agent-best-practices) — practical harness/rules/skills guidance and verifiable goals in IDE workflows.

