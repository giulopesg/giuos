# Documentation Rule — GiuOS

Documentação no GiuOS serve dois consumidores: humanos (Giuliana e colaboradores) e agentes AI (Claude e futuros agentes). O formato deve funcionar para os dois sem sacrificar nenhum.

---

## Frontmatter YAML — obrigatório em todos os documentos

Todo documento de projeto tem um bloco YAML no topo com campos estruturados. O corpo depois do frontmatter é narrativo e livre.

**Por quê:** Markdown livre não é parseable de forma confiável por agentes. O frontmatter garante que qualquer agente futuro consiga extrair campos sem ter que ler e interpretar o corpo inteiro.

---

## Camadas de documentação — cada documento responde uma pergunta

| Documento | Pergunta que responde |
|---|---|
| `CLAUDE.md` | Como o agente deve se comportar neste projeto? |
| `DISCOVERY-SYNTHESIS.md` | O que aprendemos sobre o problema e as pessoas? |
| `PRD.md` | O que vamos construir, para quem, com qual apetite? |
| `PITCH.md` | Como vamos construir? Qual o escopo do ciclo? |
| `SPEC.md` | O que o sistema deve fazer? (comportamento, não implementação) |
| `PRODUCT-BRIEF.md` | Qual é a visão completa do produto? |
| `session-log/` | Por que cada decisão foi tomada? |
| `CHANGELOG.md` | O que mudou em cada versão? |

**Regra:** Cada documento responde uma pergunta. Não misturar responsabilidades.

---

## Session log — formato leve

Máximo 20 linhas por entrada. Estrutura:

```markdown
## YYYY-MM-DD — [título da decisão]

**Contexto:** [o que estava acontecendo]
**Decisão:** [o que foi decidido]
**Alternativas descartadas:** [o que foi considerado e rejeitado]
**Próxima ação:** [o que acontece agora]
```

Não é narrativa. É memória de decisão. Deve ser legível por um agente numa varredura rápida.

---

## Código — headers obrigatórios

Todo arquivo de código começa com:

```
// @file: [nome do arquivo]
// @concern: [responsabilidade única deste arquivo]
// @sprint: [sprint atual]
// @updated: [data]
```

---

## Regras gerais

- Documentos aprovados recebem `status: approved` no frontmatter — não modificar sem nova aprovação
- Versões anteriores de PRD e SPEC são arquivadas, não sobrescritas
- `session-log/INDEX.md` lista todas as entradas com data, título, e link
