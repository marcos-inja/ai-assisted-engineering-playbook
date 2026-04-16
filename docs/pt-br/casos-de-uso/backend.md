# Casos de uso: backend (APIs, banco, testes, migrações, performance)

## Quando usar / Quando evitar

- **Quando usar**: CRUD/API, integrações, refactors com cobertura, debug de regressão, otimização de queries/hot paths.
- **Quando evitar**: decisões de domínio sem spec (contratos, invariantes). Primeiro escreva spec/aceites/testes.

## Sinais de que está dando errado

- **Mudança passa unit mas quebra integração**: faltou integration tests e fixtures realistas.
- **SQL/ORM “parece ok” mas é lento**: faltou plano de execução e benchmark.
- **Migração perigosa**: faltou estratégia de rollout e compatibilidade (dual-write/dual-read).

## Checklist operacional

### 1) API changes (contratos e compat)

- declare contratos (OpenAPI/JSON schema) e invariantes
- defina compatibilidade (backward/forward)
- defina versões e deprecações

### 2) Testes como oráculo

- unit para lógica pura
- integration para DB/IO
- contract tests para integrações
- smoke para endpoints críticos

### 3) Debugging e regressão

- pedir ao agente: 3 hipóteses + instrumentação mínima
- exigir evidência (logs/test output) antes de mudar código

### 4) Performance

- exigir: baseline e “budget” (p95, throughput)
- pedir análise: N+1, índices, caches, serialização

## Trade-offs e decisões

- **Mockar DB** acelera, mas reduz confiança; use DB real em integration quando risco for médio/alto.
- **Refactor + feature** juntos: tende a explodir diffs e custo; prefira separar.

## Exemplos

### Task spec para endpoint

```text
## Description
Adicionar endpoint GET /v1/foo?bar=...

## Files to Modify
- <path> controller/router
- <path> service
- <path> repository

## Acceptance Criteria
- [ ] retorna 200 com payload conforme schema
- [ ] retorna 400 para input inválido

## Test Requirements
- [ ] integration test com DB/fixtures
```

## Referências

- [../arquitetura/harness-engineering.md](../arquitetura/harness-engineering.md) — impact map + task specs para evitar “módulo errado”.
- [../avaliacao-e-harness/ci-gates-e-regressao.md](../avaliacao-e-harness/ci-gates-e-regressao.md) — gates e F2P/P2P para reduzir regressão.

