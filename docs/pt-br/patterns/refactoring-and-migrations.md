# Patterns: refactors e migrações (mudanças grandes com controle)

## Quando usar / Quando evitar

- **Quando usar**: upgrades, migrações de API, mudanças de infra, refactors multi-arquivo, mudanças repetitivas (codemod).
- **Quando evitar**: “big bang” sem gates e sem rollout. Com IA, isso piora.

## Sinais de que está dando errado

- **Diff gigantesco**: tarefas não foram particionadas.
- **Falta de compatibilidade**: quebra de contrato (API/DB/eventos).
- **Regressões difíceis de rastrear**: sem etapas, sem checkpoints, sem F2P/P2P.

## Checklist operacional

### Estratégia recomendada (staged)

- **Mapear impacto** (impact map)
- **Criar tarefas atômicas** (1 mudança verificável por PR)
- **Codemod quando for mecânico**
- **Gates por etapa** (lint/typecheck/tests/e2e subset)
- **Rollout com compat**:
  - dual-read / dual-write (quando necessário)
  - feature flags
  - canary

### Migrações de dados

- dry-run
- backfill idempotente
- monitoramento e rollback plan

## Trade-offs e decisões

- Codemod reduz custo e risco; IA ajuda a projetar e ajustar o codemod, mas não substitui gates.
- Dual-write aumenta complexidade temporária, mas reduz risco de downtime.

## Exemplos

### Template de PR para refactor grande

```text
Objetivo: <1 frase>
Escopo: <pastas/arquivos>
Aceite:
- [ ] tests verdes
- [ ] nenhuma mudança de comportamento (ou especificar qual muda)
Plano de rollout: <se aplicável>
```

## Referências

- [../arquitetura/harness-engineering.md](../arquitetura/harness-engineering.md) — impact map + task specs.
- [../avaliacao-e-harness/ci-gates-e-regressao.md](../avaliacao-e-harness/ci-gates-e-regressao.md) — gates e regressão.

