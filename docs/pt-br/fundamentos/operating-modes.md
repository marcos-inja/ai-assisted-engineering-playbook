# Fundamentos: modos de operação (chat, pair, agent, swarm)

## Quando usar / Quando evitar

- **Chat (perguntas/respostas)**: entender código/sistema, aprender API, explorar alternativas.
  - Evite para mudanças grandes sem especificação: tende a produzir “texto bonito” e pouca verificação.
- **Pair (pareamento IA + você)**: implementação incremental com você dirigindo (pequenos diffs).
  - Evite quando há muita varredura/descoberta: vira “microgerenciamento” caro.
- **Agent (execução autônoma com ferramentas)**: tasks multi-arquivo com validação no loop.
  - Evite sem *oracles* (test/lint/build): agente “anda no escuro”.
- **Swarm/Multiagente (paralelismo + síntese)**: pesquisa, auditoria, migrações, incident response, decisões.
  - Evite para tarefas simples: overhead alto e risco de divergência.

## Sinais de que está dando errado

- **Chat vira “implementação” sem paths reais**: você deveria estar em Agent com impact map.
- **Agent faz mudanças enormes por iteração**: faltou particionar em tarefas atômicas.
- **Swarm retorna 4 respostas incompatíveis**: falta um “lead” com critérios de decisão e rubrica de avaliação.

## Checklist operacional

- **Escolha o modo pelo tipo de incerteza**
  - **Incerteza sobre “onde mexer”** → Swarm (exploração) → impact map
  - **Incerteza sobre “como implementar”** → Chat/Pair → spike/testes
  - **Incerteza baixa e objetivo verificável** → Agent + validação

- **Defina “oráculos” (sinais objetivos)**
  - unit/integration tests
  - lint/typecheck
  - e2e (Playwright/Cypress)
  - performance budget / p95

- **Defina limites de autonomia**
  - O que pode editar?
  - O que deve pedir review humano (arquitetura, segurança, contratos)?

## Trade-offs e decisões

### Velocidade vs controle

- **Chat/Pair**: mais controle, menos throughput.
- **Agent**: mais throughput, exige harness e gates.
- **Swarm**: máximo throughput em discovery, exige síntese e critérios.

### Qualidade vs custo

- No “modo Agent”, custo explode se:
  - o agente re-varre o repo repetidamente;
  - você não restringe escopo;
  - não há checkpoints.

## Exemplos (workflows)

### Workflow “plan-first” (quando importa qualidade)

```text
1) Pesquisa: identificar arquivos/símbolos e padrão existente
2) Impact map: listar módulos e arquivos a tocar
3) Task specs: 1 tarefa por unidade verificável (paths reais + aceites + testes)
4) Implementar: uma tarefa por vez
5) Validar: sempre rodar oráculos e corrigir até verde
```

### Workflow “exploração rápida” (quando você não sabe o caminho)

```text
Pergunta para o swarm:
- Onde fica o fluxo X? Quais módulos participam? Quais invariantes?
- Devolva: mapa (componentes → responsabilidades → pontos de extensão)
Depois: transformar mapa em impact map verificável.
```

## Referências

- [https://cursor.com/blog/agent-best-practices](https://cursor.com/blog/agent-best-practices) — descreve plan-first, gestão de contexto e como tornar objetivos verificáveis.

