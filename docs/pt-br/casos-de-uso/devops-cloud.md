# Casos de uso: DevOps/Cloud (IaC, incidentes, observability-driven loops)

## Quando usar / Quando evitar

- **Quando usar**: IaC (Terraform/Helm), triagem de incidentes, análise de logs/métricas, geração de runbooks, hardening.
- **Quando evitar**: ações destrutivas sem “dry-run” e sem políticas (approval/gates).

## Sinais de que está dando errado

- **Mudança IaC derruba ambiente**: falta plan/diff review + gates + rollout.
- **Incidente vira “caça ao erro” infinita**: falta hipótese + evidência; tool outputs enormes.
- **Automação executa fora de escopo**: ausência de contratos e restrições (namespaces, contas, regiões).

## Checklist operacional

### 1) IaC (Terraform/Helm/K8s)

- sempre gerar **plan** (Terraform) / **diff** (Helm)
- gates por risco (dev → staging → prod)
- limitar permissões (least privilege)

### 2) Incident response “agentic”

- definir: sintoma + janela + blast radius
- pedir 3 hipóteses com sinais observáveis
- coletar evidência: logs, traces, métricas (com filtros)
- aplicar mitigação mínima e validar

### 3) Observabilidade

Exigir que qualquer automação registre:
- consultas feitas (queries)
- decisão tomada (por quê)
- ação executada (o quê) + resultado

## Trade-offs e decisões

- “Autonomia” em infra é perigosa: prefira **humano no gate** para ações de escrita.
- Mais dados (logs) não ajuda sem filtragem; use contexto mínimo + queries focadas.

## Exemplos

### Template: task IaC com gates

```text
Objetivo: ...
Escopo: cluster/namespace/region/account ...
Aceite:
- [ ] terraform plan sem destruição inesperada
- [ ] rollout em staging OK
- [ ] rollback documentado
```

## Referências

- [../arquitetura/agentic-architectures.md](../arquitetura/agentic-architectures.md) — contratos de tools e observabilidade.
- [../custos-e-performance/routing-e-controle-de-custos.md](../custos-e-performance/routing-e-controle-de-custos.md) — budgets, circuit breaker, retries.

