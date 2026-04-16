# Fundamentals: operating modes (chat, pair, agent, swarm)

## When to use / When to avoid

- **Chat (Q&A)**: understand code/system, learn an API, explore alternatives.
  - Avoid for large changes without a spec: it tends to produce “nice text” with little verification.
- **Pair (AI + you)**: incremental implementation with you driving (small diffs).
  - Avoid when there’s lots of discovery/sweeping: it becomes expensive micromanagement.
- **Agent (autonomous execution with tools)**: multi-file tasks with validation in the loop.
  - Avoid without *oracles* (tests/lint/build): the agent is “walking in the dark”.
- **Swarm/Multi-agent (parallelism + synthesis)**: research, audits, migrations, incident response, decisions.
  - Avoid for simple tasks: high overhead and divergence risk.

## Signals things are going wrong

- **Chat turns into “implementation” with no real paths**: you should be in Agent mode with an impact map.
- **Agent makes huge changes per iteration**: tasks weren’t split into atomic units.
- **Swarm returns incompatible answers**: you’re missing a lead with decision criteria and an evaluation rubric.

## Operational checklist

- **Pick the mode based on the type of uncertainty**
  - **Uncertainty about “where to change”** → Swarm (explore) → impact map
  - **Uncertainty about “how to implement”** → Chat/Pair → spike/tests
  - **Low uncertainty + verifiable goal** → Agent + validation

- **Define oracles (objective signals)**
  - unit/integration tests
  - lint/typecheck
  - e2e (Playwright/Cypress)
  - performance budget / p95

- **Define autonomy limits**
  - What can it edit?
  - What requires human review (architecture, security, contracts)?

## Trade-offs and decisions

### Speed vs control

- **Chat/Pair**: more control, less throughput.
- **Agent**: more throughput, requires harness and gates.
- **Swarm**: maximum throughput for discovery, requires synthesis and criteria.

### Quality vs cost

- In **Agent mode**, cost explodes if:
  - the agent re-sweeps the repo repeatedly;
  - you don’t constrain scope;
  - there are no checkpoints.

## Examples (workflows)

### “Plan-first” workflow (when quality matters)

```text
1) Research: identify files/symbols and existing pattern
2) Impact map: list modules and files to touch
3) Task specs: 1 task per verifiable unit (real paths + acceptance + tests)
4) Implement: one task at a time
5) Validate: always run oracles and fix until green
```

### “Fast exploration” workflow (when you don’t know the path yet)

```text
Ask the swarm:
- Where does flow X live? Which modules participate? What invariants?
- Return: a map (components → responsibilities → extension points)
Then: turn the map into a verifiable impact map.
```

## References

- `https://cursor.com/blog/agent-best-practices` — plan-first, context management, and how to make goals verifiable.

