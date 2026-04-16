# Roadmap (30/60/90 days): evolve AI usage without “vibe coding”

## When to use / When to avoid

- **When to use**: to create an adoption plan (individual/team) with verifiable milestones.
- **When to avoid**: treating “adopting a tool” as the goal. The goal is throughput with quality and governance.

## 30 days (individual): harness baseline and feedback loops

- **Artifacts**
  - task spec templates (acceptance + tests)
  - minimal context rules (canonical paths, commands)
  - review checklist (security, regressions)
- **Ready signals**
  - small, reviewable PRs
  - fewer “structural errors” (wrong module)
  - stable cost per task

## 60 days (team): standardization and CI gates

- **Artifacts**
  - prompt/template library (by scenario)
  - risk-based CI gates (unit/integration/e2e)
  - basic observability (cost, tool-use, failures)
- **Ready signals**
  - consistent quality across devs
  - fewer regressions after adoption

## 90 days (org): continuous evals and routing at scale

- **Artifacts**
  - internal datasets (real tasks) for eval
  - routing policy (cheap-first + gates)
  - security/incident playbooks
- **Ready signals**
  - model/harness decisions backed by data
  - predictable cost per feature
  - fewer incidents / faster resolution

## References

- `docs/en/costs-and-performance/routing-and-cost-controls.md`
- `docs/en/evaluation-and-harness/eval-taxonomy.md`

