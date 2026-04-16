# Ferramentas: landscape (como escolher sem vendor lock-in)

## Quando usar / Quando evitar

- **Quando usar**: para selecionar stack de produtividade (IDE/CLI/agentes/observabilidade/eval) por contexto (time, compliance, custo).
- **Quando evitar**: escolher ferramenta por demo. Critério tem que ser: *swap-ability* + integração com seu harness.

## Sinais de que está dando errado

- **Vendor lock-in silencioso**: workflow depende de features proprietárias sem alternativas.
- **Ferramenta vira “processo”**: time ajusta o trabalho à ferramenta, não o contrário.
- **Sem observabilidade**: você não sabe custo por feature, tool-use, nem onde falha.

## Checklist operacional

### Categorias (e o que exigir de cada uma)

- **IDE copilots / editors** (assistência no fluxo)
  - exigir: contexto por repo, navegação, execução de testes, PR review
- **CLI coding agents** (mudanças maiores, automation)
  - exigir: execução + iteração, diffs pequenos, integração com git/CI
- **Orchestrators (graphs/workflows)** (produtos com agentes)
  - exigir: controle de loops, retries, human checkpoints, estado
- **Observabilidade / tracing**
  - exigir: logs de prompts/tools/custos, replay, datasets de eval
- **Eval frameworks**
  - exigir: exec-based quando possível, CI gating, versionamento
- **AI gateways**
  - exigir: routing/caching/budgets, políticas e auditoria

### Critérios de escolha (ordem prática)

1) **Integração com oráculos**: testes/lint/typecheck/e2e
2) **Controle de contexto**: rules/context files, JIT loading
3) **Observabilidade**: tracing e custo por tarefa
4) **Portabilidade**: exportar configs; APIs abertas; protocolos
5) **Segurança/compliance**: isolamento, redaction, políticas

## Trade-offs e decisões

- Ferramentas “tudo em um” aceleram começo, mas aumentam lock-in.
- Stack modular reduz lock-in, mas exige mais engenharia de integração.

## Exemplos

### Perguntas que cortam 80% das escolhas ruins

```text
1) Consigo rodar testes/lint/typecheck no loop?
2) Consigo versionar rules/skills/workflows no repo?
3) Consigo ver tool calls e custo por tarefa?
4) Se eu trocar o fornecedor amanhã, o que quebra?
```

## Referências

- `https://cursor.com/blog/agent-best-practices` — boas práticas de harness/rules/skills e objetivos verificáveis em IDE.

