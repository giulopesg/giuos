---
name: spec-generator
description: Gera a SPEC a partir do PRD e Pitch aprovados. Ativa após bet aceito. Define comportamentos esperados, estados, bordas, e critérios de aceite. Giuliana revisa e assina — Building não começa sem aprovação.
---

# Spec Generator

Gera a SPEC de comportamento a partir do PRD e Pitch aprovados. A spec define o que o sistema deve fazer — não como implementar.

## Pré-condições obrigatórias

- [ ] `docs/PRD.md` com `approved: true`
- [ ] `docs/PITCH.md` com `bet-decision: accepted`
- [ ] Stack pack ativo identificado no `CLAUDE.md`

Se alguma condição falhar: para e informa Giuliana antes de gerar qualquer coisa.

## Prompt frame de abertura

> "Bet aceito. Vou gerar a SPEC do Ciclo [N] a partir do PRD e Pitch aprovados. A spec vai cobrir os comportamentos esperados, estados e transições, bordas, e critérios de aceite. **Você revisa e assina antes do Building começar.** Gerando agora..."

## O que a SPEC define

**Define:**
- Comportamentos esperados (dado / quando / então)
- Estados e transições
- Casos excepcionais e bordas
- Componentes UI envolvidos (com referência Figma quando disponível)
- Critérios de aceite verificáveis
- O que está explicitamente fora

**Não define:**
- Como implementar (isso é decisão do Building)
- Stack ou arquitetura detalhada (isso é responsabilidade do stack pack)
- Estimativas de tempo

## Processo de geração

### 1. Lê PRD e Pitch
Extrai: problema, personas, apetite, solução esboçada, rabbit holes, no-gos, critérios de sucesso.

### 2. Traduz solução esboçada em comportamentos
Para cada aspecto da solução esboçada no Pitch:
- Identifica os atores envolvidos
- Mapeia o comportamento em formato dado/quando/então
- Identifica casos excepcionais relevantes

### 3. Mapeia estados (se aplicável)
Se a feature envolve estados (ex: rascunho → publicado, pendente → aprovado), mapeia as transições.

### 4. Define bordas
Para cada comportamento: o que acontece nos extremos?
- Estado vazio (sem dados)
- Erro de sistema
- Permissão negada
- Limite atingido

### 5. Identifica componentes UI
Para cada componente UI que precisará ser criado ou modificado:
- Nome do componente
- Comportamento esperado
- Referência no Figma (pergunta a Giuliana se não souber)

### 6. Deriva critérios de aceite
A partir dos critérios de sucesso do PRD — traduz para verificável no nível da implementação.

### 7. Declara o que está fora
Tudo que está nos no-gos do Pitch + scope que ficou além da solução esboçada.

## Apresentação para revisão

O agente apresenta a SPEC completa e chama atenção para:
- Comportamentos que podem ter interpretação ambígua
- Casos excepcionais que precisam de decisão de Giuliana
- Componentes sem referência Figma

> "SPEC gerada. Antes de você assinar, quero chamar atenção para: [pontos de ambiguidade]. E estes componentes não têm referência no Figma ainda: [lista]. Quer resolver isso antes de aprovar ou seguimos com geração livre para eles?"

## Output

`docs/SPEC.md` preenchido usando o template.
Frontmatter atualizado com `status: draft` até aprovação.
Após aprovação: `status: approved`, `approved-by: Giuliana`, `approved-date: [data]`.
