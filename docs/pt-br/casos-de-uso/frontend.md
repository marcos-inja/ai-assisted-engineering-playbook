# Casos de uso: frontend (UI, a11y, e2e, regressão visual)

## Quando usar / Quando evitar

- **Quando usar**: implementação de componentes seguindo design system, refactors de UI, correções de a11y, e2e e regressão visual.
- **Quando evitar**: “design-to-code” sem specs (tokens, espaçamentos, breakpoints) e sem validação visual.

## Sinais de que está dando errado

- **UI “parece ok” mas quebra em edge cases**: falta de estados (loading/empty/error) e falta de e2e.
- **A11y regressiva**: falta de checks automatizados (axe) e critérios de teclado/foco.
- **Mudanças visuais furtivas**: falta de snapshot/visual regression e budgets.

## Checklist operacional

### 1) Constraints-first (UI)

- componentes/padrões canônicos a seguir
- tokens (spacing, typography, colors)
- responsividade (breakpoints)
- estados obrigatórios (loading/empty/error)

### 2) Oráculos

- unit (component logic)
- e2e (fluxo usuário)
- a11y (axe + navegação teclado)
- visual regression (quando disponível)

### 3) Refactors

- preferir “mudança mecânica” em etapas (codemod quando útil)
- limitar escopo por pasta/feature

## Trade-offs e decisões

- Visual regression aumenta confiança, mas custa infra e manutenção de snapshots.
- E2E cobre fluxo real, mas é mais lento; use smoke suite curta.

## Exemplos

### Template de prompt “UI verificável”

```text
Implemente o componente X seguindo o padrão de Y em <arquivo>.

Aceite:
- [ ] estados: loading/empty/error
- [ ] teclado: tab order correto, foco visível
- [ ] a11y: labels/aria onde necessário
- [ ] e2e: fluxo Z passa
```

## Referências

- [../prompt-engineering/prompts-avancados.md](../prompt-engineering/prompts-avancados.md) — templates para rubricas e objetivos verificáveis.
- [../avaliacao-e-harness/ci-gates-e-regressao.md](../avaliacao-e-harness/ci-gates-e-regressao.md) — gates por risco.

