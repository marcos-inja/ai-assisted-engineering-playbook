# Harness engineering (impact map → task specs → validação)

## Quando usar / Quando evitar

- **Quando usar**: qualquer trabalho multi-repo / multi-módulo (monorepo, microserviços, infra + app), ou quando o agente costuma errar “onde mexer”.
- **Quando evitar**: tarefas triviais de 1 arquivo e sem risco — o overhead não paga.

## Sinais de que está dando errado

- **Planos com caminhos inventados**: impact map não foi gerado a partir do repo real.
- **O agente resolve “no módulo errado”**: faltou checkpoint humano após impact map.
- **PR grande e difícil de revisar**: tasks não são atômicas; falta de “um objetivo verificável por task”.

## Checklist operacional

### Fase 1 — Repository impact map (planejamento ancorado no código)

Entregável: um mapa curto revisável (não um texto longo) contendo:
- repos/módulos afetados
- arquivos prováveis (paths reais)
- símbolos/padrões existentes a seguir
- riscos (migração, compatibilidade, dados, performance)

**Gate humano**: revisar o mapa antes de criar tasks/PR.

### Fase 2 — Task specs estruturadas (contrato de implementação)

Cada task deve ter:
- **Repository** (ou módulo): delimita escopo
- **Files to modify**: paths reais
- **Implementation notes**: referência a símbolos/padrões existentes
- **Acceptance criteria**: checklist pass/fail
- **Test requirements**: quais testes e onde ficam

### Fase 3 — Implementação com validação no loop

Regras:
- uma task por vez
- mudanças mínimas para passar os aceites
- sempre rodar oráculos (test/lint/typecheck/build) antes de declarar “done”

## Trade-offs e decisões

- **Mais estrutura** ↓ criatividade, ↑ previsibilidade (quase sempre bom em produção).
- **Impact map detalhado demais** vira “documentação falsa”; mantenha curto e verificável.

## Exemplos (templates)

### Template: impact map (curto e revisável)

```text
<repoA>:
  changes:
    - ...
  touch:
    - <path>
  follow-pattern:
    - <symbol in file>

<repoB>:
  changes:
    - ...
```

### Template: task spec (pronto para execução)

```text
## Repository
<repo/module>

## Description
<1–2 frases>

## Files to Modify
- `<real/path>` — <o que mudar>

## Implementation Notes
- Siga o padrão de `<symbol>` em `<file>`
- Reuse `<type>` de `<file>`

## Acceptance Criteria
- [ ] <critério pass/fail>

## Test Requirements
- [ ] <teste/unit/integration> em `<path>`
```

## Referências

- `https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development` — descreve impact map + task template + checkpoint humano como redução de “erros estruturais”.
- `https://arxiv.org/html/2604.01527v1` — evidencia que harness IDE-like + validação (tests/static checks) aumenta solve rate e reduz gap entre modelos.

