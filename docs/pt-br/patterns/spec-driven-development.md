# Patterns: Spec-Driven Development (SDD) pragmático (com learning loop)

## Quando usar / Quando evitar

- **Quando usar**: features com risco (contratos, dados, segurança), mudanças multi-módulo, e qualquer coisa que você quer tornar “delegável” para agentes com previsibilidade.
- **Quando evitar**: “spec monolítica perfeita” antes de aprender. Prefira spec leve + feedback rápido.

## Sinais de que está dando errado

- **Spec vira burocracia**: documento cresce, mas não guia tasks nem testes.
- **Agente deriva do objetivo**: aceites vagos; tasks sem paths/símbolos reais.
- **Implementação contradiz spec**: falta gate “spec update first” e falta revisão por aceites.

## Checklist operacional

### Artefatos mínimos (por feature)

- **Spec**: o quê/por quê + aceites verificáveis (Given/When/Then quando fizer sentido).
- **Plan**: como (arquitetura, impactos, riscos, rollout).
- **Tasks**: decomposição em unidades verificáveis (PR-sized) com paths reais.
- **Oracle**: testes/gates e como provar pronto.

### Loop de aprendizagem (evitar “spec rígida”)

Regra: se durante implementação você aprende algo que muda requisito ou abordagem:
- atualize spec/plan
- depois atualize código

### Conexão direta com harness

Para cada task:
- referenciar padrão existente no repo
- listar arquivos a modificar
- listar aceites + testes obrigatórios

## Trade-offs e decisões

- SDD aumenta previsibilidade e reduz retrabalho, mas exige disciplina em atualizar artefatos.
- “Spec-as-source” (tudo gerado) só faz sentido em domínios muito estáveis e com eval/harness robustos.

## Exemplos

### Template: spec leve (delta spec)

```text
## Goal
...

## Non-goals
...

## Acceptance Criteria
- [ ] ...

## Risks / Rollout
...
```

### Template: task (pronto para agente)

Veja [../arquitetura/harness-engineering.md](../arquitetura/harness-engineering.md) (task spec).

## Referências

- [https://developer.microsoft.com/blog/spec-driven-development-spec-kit](https://developer.microsoft.com/blog/spec-driven-development-spec-kit) — visão prática de SDD e Spec Kit.
- [https://github.com/github/spec-kit](https://github.com/github/spec-kit) — toolkit de referência (specify/plan/tasks/implement).
- [https://martinfowler.com/fragments/2026-01-08.html](https://martinfowler.com/fragments/2026-01-08.html) — crítica a “spec rígida” e foco em feedback loops (TDD).

