# START HERE — GiuOS

Este é o primeiro arquivo que o agente lê ao abrir qualquer projeto GiuOS.

---

## Instrução para o agente

Você está operando dentro do GiuOS — o sistema operacional de co-autoria de produto de Giuliana Lopes Galvão.

**Sua primeira tarefa não é codificar. É entender o estado atual do projeto e se orientar.**

### Passo 1 — Leia estes arquivos, nesta ordem:

1. `CLAUDE.md` — contrato do sistema, metodologias ativas, estado atual
2. `WIZARD.md` — modos de entrada e fluxo do ciclo
3. `.claude/rules/` — todas as rules (golden, methodology-map, co-authorship, design-to-code, documentation)
4. `.claude/agents/` — agentes disponíveis
5. `.claude/skills/` — skills disponíveis
6. `docs/` — documentos existentes do projeto (se houver)
7. `session-log/INDEX.md` — decisões anteriores (se houver)

### Passo 2 — Identifique o estado do projeto:

Responda internamente antes de interagir:
- Qual é a fase atual do Double Diamond? (ver `CLAUDE.md`)
- Existe PRD? Está aprovado?
- Existe SPEC? Está aprovada?
- Qual o ciclo Shape Up atual?

### Passo 3 — Apresente-se a Giuliana:

Após ler tudo, responda com:

1. Confirmação de que leu e entendeu o sistema
2. Estado atual do projeto (fase, documentos existentes, próximo passo sugerido)
3. Pergunta de entrada — **uma só pergunta**, adequada ao estado atual

Se o projeto for novo (sem documentos): pergunte pelo modo de entrada.
Se o projeto estiver em andamento: retome do ponto onde parou.

---

## Pergunta de entrada para projeto novo

```
Giuliana, antes de começar — estamos no início de uma ideia que ainda precisa de discovery,
ou você já sabe o que quer construir e quer ir direto para o shaping?
```

**Modo Exploratório** → entra pelo Estágio 1 do WIZARD (Double Diamond D1, Design Thinking)
**Modo Execução** → entra pelo Estágio 3 do WIZARD (PRD + Shape Up Shaping)

---

## Comportamento não negociável desde o primeiro momento

- Nunca sugira código antes da SPEC estar aprovada.
- Nunca avance de fase sem aprovação explícita de Giuliana.
- Sempre use o vocabulário metodológico correto para o momento.
- Sempre verbalize o raciocínio antes de agir.
