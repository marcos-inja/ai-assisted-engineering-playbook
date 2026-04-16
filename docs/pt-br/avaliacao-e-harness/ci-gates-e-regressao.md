# CI gates e regressão (tornar IA segura para produção)

## Quando usar / Quando evitar

- **Quando usar**: toda vez que IA gera ou altera código, testes, infra ou configurações.
- **Quando evitar**: não evitar. O que muda é o “tamanho” do gate (leve vs pesado) por risco.

## Sinais de que está dando errado

- **PRs verdes mas quebram depois**: gates incompletos (falta integration/e2e), ou flakiness mascarando falhas.
- **Agentes geram regressões**: tasks grandes demais; ausência de impact analysis; TDD “procedural” sem contexto.
- **CI lenta demais**: sem seleção de testes relevante; falta de caching/parallelização.

## Checklist operacional

### 1) Gates por nível de risco

- **Baixo risco** (docs, refactor mecânico):
  - lint + unit tests rápidos
- **Médio risco** (mudança de comportamento local):
  - unit + integration subset + typecheck/build
- **Alto risco** (auth, pagamentos, infra, migrações):
  - integration + e2e + security checks + canary/perf

### 2) Fail-to-pass (F2P) como sinal forte

Para bugfix/feature:
- identifique testes que **falham antes e passam depois**
- mantenha um conjunto P2P (pass-to-pass) para regressão

### 3) Impact analysis (reduzir regressão sem explodir CI)

Estratégias:
- seleção de testes por dependência (import graph)
- mapeamento por paths/padrões
- heurísticas + validação (executar top-k)

### 4) Antiflakiness

- execute testes candidatos múltiplas vezes quando estiver curando suites
- se flakey: isolar, marcar, ou remover do gate crítico

## Trade-offs e decisões

- **TDD como forcing function**: melhora entendimento humano e dá oráculo claro, mas pode virar ritual vazio se o agente estiver “seguindo passos” sem contexto.
- **Seleção de testes** reduz custo, mas aumenta risco de falso negativo; mitigar com P2P + smoke.

## Exemplos (gates prontos)

### Gate mínimo para “agent PR”

```text
- lint/format
- typecheck
- unit tests (subset)
- build
```

### Gate alto risco (exemplo)

```text
- unit + integration
- e2e smoke
- SAST/secret scan
- migration dry-run (se aplicável)
```

## Referências

- `https://arxiv.org/html/2604.01527v1` — mostra valor de validação (tests/static analysis) no loop e de sinais exec-based (F2P).
- `https://arxiv.org/html/2603.17973v1` — TDAD: impacto de prompting TDD “procedural” vs fornecer contexto/impact analysis para reduzir regressões.

