---
name: prd-generator
description: Constrói o PRD junto com Giuliana. Ativa na transição D1→D2 (Modo Exploratório) ou como ponto de entrada (Modo Execução). Propõe cada campo — Giuliana revisa, corrige, aprova.
---

# PRD Generator

Constrói o PRD campo a campo com Giuliana. O agente propõe — Giuliana revisa e aprova.

## Pré-condições por modo

**Modo Exploratório:**
- [ ] `docs/DISCOVERY-SYNTHESIS.md` com `approved: true`
- [ ] Problema declarado e aprovado no discovery

**Modo Execução:**
- Giuliana declara o problema diretamente — o agente captura e confirma antes de avançar

## Prompt frame de abertura

**Modo Exploratório:**
> "Discovery aprovado. Problema declarado: '[problema]'. Vou construir o PRD com você agora. Vou propor cada campo — você revisa e ajusta. Começando pelo problema..."

**Modo Execução:**
> "Entendi o que você quer construir. Antes de ir para o shaping, precisamos formalizar o PRD. Vou propor cada campo a partir do que você me contou — você corrige o que não estiver certo."

## Sequência campo a campo

O agente propõe, apresenta, e espera confirmação de Giuliana antes de avançar para o próximo campo.

### 1. Problema
Propõe a declaração do problema em uma frase. Se vier do discovery, usa o problema declarado na síntese. Se vier do Modo Execução, sintetiza o que Giuliana descreveu.

Pergunta:
> "O problema que estamos resolvendo é: '[declaração]'. Está correto? Quer ajustar alguma palavra?"

### 2. Personas afetadas
Propõe as personas a partir do discovery (ou da descrição de Giuliana no Modo Execução).

Pergunta:
> "As personas afetadas são [lista]. Faz sentido? Tem alguém que faltou ou que não deveria estar aqui?"

### 3. Apetite
Apresenta as opções e ajuda Giuliana a decidir.

> "Para esse problema, vejo duas possibilidades de apetite: [small-batch 2 semanas] se resolvermos apenas [escopo reduzido], ou [standard 6 semanas] se incluirmos [escopo completo]. O que faz mais sentido agora?"

### 4. Solução esboçada
Propõe uma direção — não um spec. Uma abordagem.

> "Uma direção possível é [x]. Não estou especificando como — só a direção. Faz sentido para o problema?"

### 5. Rabbit holes
Identifica proativamente o que pode virar armadilha.

> "Já vejo potenciais rabbit holes: [lista]. Quer adicionar mais algum que está na sua cabeça?"

### 6. No-gos
Propõe o que deve ficar fora, baseado no apetite e na solução esboçada.

> "Para caber no apetite de [x], estes itens ficam fora deste ciclo: [lista]. Concorda? Tem algo que você definitivamente não quer incluir também?"

### 7. Critérios de sucesso
Traduz o problema em verificável.

> "Saberemos que o problema foi resolvido quando: [lista]. Esses critérios capturam o que importa?"

## Red team automático

Após todos os campos preenchidos, o agente ativa o `red-team-agent` para uma rodada leve antes de apresentar o PRD para aprovação final.

## Output

`docs/PRD.md` preenchido usando o template.
Frontmatter com `status: draft` até aprovação.
Após aprovação de Giuliana: `approved: true`, `approved-date: [data]`.
