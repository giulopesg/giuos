---
project: ""
cycle: 1
prd-ref: "docs/PRD.md"
pitch-ref: "docs/PITCH.md"
status: draft
# status options: draft | approved | archived

generated-by: claude
generated-date: ""
approved-by: ""
approved-date: ""

stack-pack: ""
---

# SPEC — [Nome do Projeto / Feature] — Ciclo [N]

> Gerada pelo agente a partir do PRD e Pitch aprovados.
> Define **comportamento** — o que o sistema deve fazer, não como implementar.
> **Giuliana revisa e assina. Building não começa sem aprovação.**

---

## Escopo deste ciclo

> O que está dentro e o que está fora — derivado do Pitch aprovado.

**Dentro:**
- [item 1]
- [item 2]

**Fora (alinhado com no-gos do PRD):**
- [no-go 1]
- [no-go 2]

---

## Comportamentos esperados

> O que o sistema deve fazer. Um comportamento por bloco.
> Formato: dado [contexto], quando [ação], então [resultado esperado].

### [Nome do comportamento 1]

**Dado:** [contexto/estado inicial]
**Quando:** [ação do usuário ou evento]
**Então:** [o que deve acontecer]

**Casos excepcionais:**
- [caso 1]: [o que deve acontecer]
- [caso 2]: [o que deve acontecer]

---

### [Nome do comportamento 2]

**Dado:**
**Quando:**
**Então:**

**Casos excepcionais:**

---

## Estados e transições

> Se o comportamento envolve estados, mapear as transições.

```
[Estado A] → [ação] → [Estado B]
[Estado B] → [ação] → [Estado C]
[Estado B] → [ação alternativa] → [Estado A]
```

---

## Bordas e limites

> O que o sistema deve fazer nas extremidades — erros, limites, casos vazios.

| Situação | Comportamento esperado |
|---|---|
| [borda 1] | [o que acontece] |
| [borda 2] | [o que acontece] |
| Estado vazio (sem dados) | [o que o usuário vê] |
| Erro de conexão | [fallback] |

---

## Componentes UI envolvidos

> Lista de componentes que precisam ser criados ou modificados.
> Para cada um: referência no Figma (se existir) e comportamento esperado.

| Componente | Referência Figma | Comportamento | Status |
|---|---|---|---|
| [componente 1] | [node ID ou URL] | [descrever] | novo / modifica existente |

---

## Critérios de aceite

> Derivados dos critérios de sucesso do PRD. O ciclo só fecha quando todos estão atendidos.

- [ ] [critério 1]
- [ ] [critério 2]
- [ ] Sem regressões nos fluxos existentes
- [ ] Componentes UI revisados por Giuliana

---

## O que não está nesta spec

> Explícito para evitar scope creep durante o Building.

- [item 1] — motivo: [no-go do PRD / próximo ciclo / fora do apetite]
- [item 2]

---

## Aprovação

> **Building não começa sem esta assinatura.**

- [ ] Comportamentos cobrem o problema declarado no PRD
- [ ] Casos excepcionais fazem sentido
- [ ] Estados e transições estão corretos
- [ ] Bordas estão mapeadas
- [ ] Componentes UI identificados
- [ ] Critérios de aceite são verificáveis

**Aprovado por:** Giuliana Lopes Galvão
**Data:**
**Observações / ajustes solicitados:**
