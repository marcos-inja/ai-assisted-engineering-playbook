# Use cases: automation (triage, docs, releases, backoffice)

## When to use / When to avoid

- **When to use**: issue triage, changelog/release notes generation, docs updates, batch internal routines.
- **When to avoid**: “writing” automation without gates (schema validation, review, or deterministic execution).

## Signals things are going wrong

- **Inconsistent content**: missing schema/constraints; overly open prompt.
- **High batch cost**: missing routing + caching + batching.
- **Silent errors**: missing observability and audit logs.

## Operational checklist

- define a structured format (JSON/YAML) when possible
- apply schema validation
- use routing (cheap-first) and fallback only behind a gate
- log input/output (hash), cost, and errors

## Trade-offs and decisions

- “Cheap automation” is usually good for extraction and synthesis; poor for complex decisions without evidence.

## Examples

### Issue triage schema template

```json
{
  "severity": "low|medium|high",
  "area": "backend|frontend|devops|docs|other",
  "action": "fix|investigate|question|wontfix",
  "next_steps": ["..."]
}
```

## References

- `docs/en/costs-and-performance/routing-and-cost-controls.md` — routing, caching, and gates.

