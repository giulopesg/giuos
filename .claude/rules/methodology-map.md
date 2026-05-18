# Methodology Map — GiuOS

O agente usa este mapa para identificar qual metodologia aplicar em cada momento do ciclo.

---

## Double Diamond — frame macro

Orienta o ciclo inteiro. O agente sempre sabe em qual diamante e ponto está.

```
D1 — Problema                         D2 — Solução
──────────────────────────────────────────────────────
Discover → Define          →         Develop → Deliver
(diverge)   (converge)               (diverge)  (converge)

Design Thinking                       Shape Up
Service Design (se aplicável)         SDD + Spec
                    ↓
                   PRD
              (handoff D1→D2)
```

**Regra:** O segundo diamante não começa antes do primeiro estar fechado. Fechado = problema declarado em uma frase, aprovado por Giuliana.

---

## Design Thinking — D1 Discover e Define

**Ativa quando:** Modo Exploratório, fase de discovery.

**Ferramentas:**
- Mapeamento de contexto — atores, cenário atual, tensões
- Personas — quem sente o problema, com qual profundidade
- Jobs to be done — o que as pessoas tentam realizar (não o que pedem)
- How Might We — reformulação do problema como oportunidade de design
- Insights — padrões que emergem do discovery

**Vocabulário que o agente usa:**
- "Qual é o job to be done aqui?"
- "Quem são os atores nesse sistema?"
- "Como poderíamos resolver isso para [persona]?"
- "Qual insight está por trás dessa dor?"

**Output:** `docs/DISCOVERY-SYNTHESIS.md`

---

## Service Design (SSD) — D1, quando aplicável

**Ativa quando:** O produto tem múltiplos atores, fluxos de serviço, ou pontos de contato além da interface digital.

**Ferramentas:**
- Jornada de serviço — o que cada ator vive em cada etapa
- Service blueprint básico — frontstage (o que o usuário vê) e backstage (o que acontece por trás)
- Pontos de dor sistêmicos — onde o serviço falha para quem

**Vocabulário que o agente usa:**
- "Quem são todos os atores nesse fluxo — não só o usuário final?"
- "O que acontece no backstage para que esse momento frontstage funcione?"
- "Onde a jornada quebra hoje?"

**Output:** seção de Service Design dentro do `docs/DISCOVERY-SYNTHESIS.md`

---

## Shape Up — D2 Develop e Deliver

**Ativa quando:** Problema definido, PRD aprovado, pronto para construir.

**Três movimentos:**

**Shaping** — antes do ciclo começar
- Escreve o pitch: problema, apetite, solução esboçada, rabbit holes, no-gos
- Produzido pelo agente com Giuliana, não por uma equipe de dev
- Output: `docs/PITCH.md`

**Betting** — decisão do que entra no ciclo
- O que entra agora? O que fica para depois?
- Giuliana decide o bet — o agente apresenta as opções
- Output: seção de Betting no `docs/PITCH.md`

**Building** — execução dentro do ciclo
- Time (ou agente) trabalha contra a SPEC aprovada
- Sem backlog infinito — o ciclo tem início, meio e fim
- Rabbit holes são sinalizados, não resolvidos sem aprovação
- Output: produto funcionando + session log do ciclo

**Vocabulário que o agente usa:**
- "Qual é o apetite para esse problema?" (não: quanto tempo vai levar)
- "Isso é um rabbit hole — não estava na SPEC. Quer registrar como no-go ou abre um novo pitch?"
- "O que apostamos para esse ciclo?"
- "O ciclo fechou. O que aprendemos antes de shaping do próximo?"

---

## PRD — handoff D1→D2

**Ativa quando:** Problema definido (Modo Exploratório) ou declarado por Giuliana (Modo Execução).

**Campos obrigatórios:**
- Problema
- Personas afetadas
- Apetite
- Solução esboçada
- Rabbit holes
- No-gos
- Critérios de sucesso

**Regra:** PRD aprovado por Giuliana é pré-requisito para Shaping. Sem PRD, sem pitch.

---

## Spec-Driven Development (SDD)

**Ativa quando:** Pitch aprovado, bet definido.

**Princípio:** Nenhum código existe sem spec que o justifique. A spec é o contrato entre o que foi decidido e o que será construído.

**O agente gera a spec a partir do PRD e do Pitch aprovados.**
**Giuliana revisa e assina. Sem assinatura, Building não começa.**

A spec define comportamento — não implementação. O que o sistema deve fazer, não como.

**Vocabulário que o agente usa:**
- "Gerando a spec a partir do PRD e pitch aprovados. Vou apresentar para tua revisão."
- "Este comportamento não estava na spec. Sinalizando antes de implementar."
- "A spec está completa. Precisamos da tua aprovação antes de começar o Building."

---

## Prompt Frames — execução AI

**Ativa quando:** O agente precisa gerar um output estruturado (PRD, SPEC, discovery synthesis, red team, componente UI).

Cada tipo de output tem um frame que garante consistência entre sessões. Os frames vivem nos SKILL.md de cada skill.

**Princípio:** O agente não improvisa formato. Usa o frame correto para o output correto.
