# Roadmap (30/60/90 dias): evoluir uso de IA sem virar “vibe coding”

## Quando usar / Quando evitar

- **Quando usar**: para criar um plano de adoção individual/time com marcos verificáveis.
- **Quando evitar**: “adotar ferramenta” como objetivo. O objetivo é throughput com qualidade e governança.

## 30 dias (individual): base de harness e feedback loops

- **Artefatos**
  - templates de task spec (aceites + testes)
  - regras mínimas de contexto (paths canônicos, comandos)
  - checklist de review (segurança, regressão)
- **Sinais de pronto**
  - PRs pequenas e revisáveis
  - menos “erros estruturais” (módulo errado)
  - custo por tarefa estável

## 60 dias (time): padronização e CI gates

- **Artefatos**
  - biblioteca de prompts/templates (por cenário)
  - CI gates por risco (unit/integration/e2e)
  - observabilidade básica (custo, tool-use, falhas)
- **Sinais de pronto**
  - qualidade consistente entre devs
  - regressão reduzida após adoção

## 90 dias (org): eval contínua e roteamento em escala

- **Artefatos**
  - datasets internos (tarefas reais) para eval
  - política de roteamento (cheap-first + gates)
  - playbooks para incidentes/segurança
- **Sinais de pronto**
  - decisões de modelo/harness baseadas em dados
  - custo previsível por feature
  - incidentes reduzidos / tempo de resolução menor

## Referências

- [../custos-e-performance/routing-e-controle-de-custos.md](../custos-e-performance/routing-e-controle-de-custos.md)
- [../avaliacao-e-harness/eval-taxonomy.md](../avaliacao-e-harness/eval-taxonomy.md)

