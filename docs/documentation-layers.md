# Camadas de Documentação — GiuOS

Cada documento responde uma pergunta. Não misturar responsabilidades.

| Documento | Pergunta que responde | Quem preenche | Aprovação |
|---|---|---|---|
| `CLAUDE.md` | Como o agente deve se comportar neste projeto? | Agente + Giuliana | Giuliana |
| `DISCOVERY-SYNTHESIS.md` | O que aprendemos sobre o problema e as pessoas? | Agente (discovery-agent) | Giuliana |
| `PRD.md` | O que vamos construir, para quem, com qual apetite? | Agente (prd-generator) | Giuliana obrigatório |
| `PITCH.md` | Como vamos construir? Qual o escopo do ciclo? | Agente (shaping-agent) | Giuliana obrigatório |
| `SPEC.md` | O que o sistema deve fazer? | Agente (spec-generator) | Giuliana obrigatório — sem isso Building não começa |
| `PRODUCT-BRIEF.md` | Qual é a visão completa do produto? | Agente | Giuliana |
| `session-log/` | Por que cada decisão foi tomada? | Agente + Giuliana | — |
| `CHANGELOG.md` | O que mudou em cada versão/ciclo? | Agente | — |

---

## Regra de ouro

Se você está procurando "o que construir" → PRD
Se você está procurando "o que o sistema deve fazer neste ciclo" → SPEC
Se você está procurando "por que foi decidido assim" → session-log
Se você está procurando "o que mudou" → CHANGELOG

Não existe um documento que responde tudo. A separação é intencional.
