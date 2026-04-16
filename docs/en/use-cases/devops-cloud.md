# Use cases: DevOps/Cloud (IaC, incidents, observability-driven loops)

## When to use / When to avoid

- **When to use**: IaC (Terraform/Helm), incident triage, log/metric analysis, runbook generation, hardening.
- **When to avoid**: destructive actions without dry-run and policies (approvals/gates).

## Signals things are going wrong

- **IaC change takes down the environment**: missing plan/diff review + gates + rollout.
- **Incidents become endless “error hunting”**: missing hypotheses + evidence; huge tool outputs.
- **Automation runs out of scope**: missing contracts and constraints (namespaces, accounts, regions).

## Operational checklist

### 1) IaC (Terraform/Helm/K8s)

- always produce a **plan** (Terraform) / **diff** (Helm)
- risk-based gates (dev → staging → prod)
- least-privilege permissions

### 2) Agentic incident response

- define: symptom + time window + blast radius
- ask for 3 hypotheses with observable signals
- collect evidence: logs, traces, metrics (with filters)
- apply minimal mitigation and validate

### 3) Observability

Require any automation to log:
- queries performed
- decision taken (why)
- action executed (what) + result

## Trade-offs and decisions

- “Autonomy” in infra is risky: prefer **human-in-the-gate** for write actions.
- More data (logs) doesn’t help without filtering; use minimum context + focused queries.

## Examples

### IaC task template with gates

```text
Goal: ...
Scope: cluster/namespace/region/account ...
Acceptance:
- [ ] terraform plan without unexpected destruction
- [ ] rollout in staging OK
- [ ] rollback documented
```

## References

- `docs/en/architecture/agentic-architectures.md` — tool contracts and observability.
- `docs/en/costs-and-performance/routing-and-cost-controls.md` — budgets, circuit breaker, retries.

