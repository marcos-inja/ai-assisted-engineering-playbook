# Patterns: review & safety (PRs geradas por IA, segurança e compliance)

## Quando usar / Quando evitar

- **Quando usar**: sempre que IA gera código, IaC, pipelines, ou configs.
- **Quando evitar**: “aprovar porque compila”. IA tende a errar de forma plausível.

## Sinais de que está dando errado

- **Mudança grande sem motivo**: refactor não solicitado, diffs amplos.
- **Alterações de segurança silenciosas**: authz relaxada, logs sensíveis, validação removida.
- **Dependências adicionadas sem critério**: supply chain risk.

## Checklist operacional (rubrica de revisão)

### Correção e manutenção

- invariantes preservados?
- edge cases e estados nulos?
- concorrência/idempotência/timeouts?
- contrato de API/DB preservado?

### Segurança

- secrets em código/logs?
- injection (SQL/command/template)?
- SSRF/path traversal/deserialization?
- authn/authz corretos? (fail closed)

### Confiabilidade

- retries e timeouts definidos?
- erros tratados com contexto?
- observabilidade (logs/metrics/traces) adequada?

### Testes

- testes cobrem a mudança? (F2P quando aplicável)
- evita mocks frágeis?
- regressão (P2P) suficiente?

## Trade-offs e decisões

- Revisão humana é o “último gate” para risco alto.
- Automatize o que dá: secret scan, SAST, lint, typecheck, unit/integration.

## Exemplos

### Checklist “anti-vibe”

```text
- Qual arquivo canônico isso segue?
- Qual teste prova que isso está certo?
- Qual regressão isso poderia introduzir?
- Qual parte é irreversível/arriscada?
```

## Referências

- `docs/avaliacao-e-harness/ci-gates-e-regressao.md` — como estruturar gates por risco.

