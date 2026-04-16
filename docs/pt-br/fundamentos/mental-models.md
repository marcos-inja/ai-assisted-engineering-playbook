# Fundamentos: modelo mental operacional (prompt vs contexto vs harness)

## Quando usar / Quando evitar

- **Quando usar**: sempre que você quer previsibilidade (menos “vibe coding”) e precisa decidir **qual modo, qual modelo, qual evidência** e **qual mecanismo de validação**.
- **Quando evitar**: não evita — é o mapa. O que você evita é “copiar e colar teoria”; aqui só entra o que muda decisão.

## Sinais de que está dando errado (e como diagnosticar)

- **O agente inventa caminhos, APIs, ou símbolos**: falta de “fonte da verdade” (repo) e ausência de *impact map*; você está alimentando com “ticket”, não com código.
- **A saída parece boa mas quebra em integração**: falta de *oracle* (test/lint/typecheck) no loop; validação não está acoplada ao workflow.
- **Quanto mais contexto você joga, pior fica**: *context rot* / perda de foco; você passou “ruído” em vez de sinal.
- **Mudanças grandes e incoerentes**: tarefas não estão “atomicizadas”; falta de gates (plan → implement → verify).

## Checklist operacional (o mínimo para resultados consistentes)

- **Defina o objetivo em termos verificáveis**
  - O que muda no comportamento?
  - Qual teste/checagem prova que está certo?
  - Qual regressão é inaceitável?
- **Escolha o modo de trabalho**
  - Chat/pareamento (exploração)
  - Agente (execução multi-arquivo)
  - Multiagente (pesquisa/varredura paralela + síntese)
- **Forneça contexto por referência, não por dumping**
  - Caminhos reais de arquivos, símbolos, exemplos canônicos
  - “Busque X e siga o padrão Y”, em vez de colar 2k linhas
- **Coloque validação dentro do loop**
  - Testes, lint, typecheck, build, e2e, smoke
  - “Falhou → corrigir → revalidar” como rotina

## Trade-offs e decisões

### Prompt engineering vs Context engineering vs Harness engineering

- **Prompt engineering**: como você expressa instruções e formato de saída.
  - **Bom para**: orientar estilo, formato, passos e restrições.
  - **Limite**: não substitui evidência; não corrige desconhecimento do repo.

- **Context engineering**: como você **cura tokens** (instruções + ferramentas + dados + histórico) para maximizar sinal.
  - **Bom para**: reduzir alucinação e drift; manter foco; controlar custo.
  - **Técnicas**: contexto mínimo viável (MVC), *just-in-time context*, compaction, note-taking, subagents.

- **Harness engineering**: desenhar o **ambiente de trabalho** (processo + ferramentas + gates) que torna o agente confiável.
  - **Bom para**: previsibilidade e escala em equipe; reduzir “erros estruturais”.
  - **Núcleo**: impacto (impact map) → tarefas estruturadas → validação.

### A ideia central: “contexto é recurso finito”

Quanto mais tokens, maior o custo e maior a chance de:
- perder precisão de recuperação,
- misturar instruções,
- ancorar em informação desatualizada.

Conclusão prática: **prefira referências + tool-use** a colar conteúdo.

## Exemplos (artefatos que você pode copiar)

### Template: pedido “verificável”

```text
Objetivo: <mudança de comportamento em 1 frase>

Contexto mínimo:
- Arquivos/símbolos relevantes: <paths e symbols reais>
- Padrão a seguir: <referência a implementação existente>

Restrições:
- Não alterar: <o que não pode mudar>
- Performance/SLA: <se aplicável>
- Segurança: <se aplicável>

Aceite (verificável):
- [ ] <critério 1>
- [ ] <critério 2>

Validação:
- Rodar: <comandos/tests>
```

### “Se a saída estiver errada, corrija o harness”

Regra operacional: quando falhar, registre **qual gate** não existia:
- faltou impact map?
- faltou tarefa com paths reais?
- faltou teste?
- faltou limitação de escopo?

## Referências

- `https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents` — define “context engineering”, MVC, compaction, note-taking e subagents; explica por que mais contexto pode piorar.
- `https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development` — blueprint prático de harness (impact map + task template + checkpoint).

