---
name: shape-up-shaping
description: Escreve o pitch Shape Up com Giuliana a partir do PRD aprovado. Ativa quando PRD está aprovado e o projeto está pronto para entrar no segundo diamante. Vocabulário: apetite, fat marker sketch, breadboard, rabbit hole, no-go, betting.
---

# Shape Up Shaping

Transforma o PRD aprovado em um pitch executável — com solução esboçada, apetite definido, rabbit holes mapeados, e no-gos explícitos.

## Pré-condições obrigatórias

Antes de iniciar o shaping, verificar:
- [ ] `docs/PRD.md` existe e tem `approved: true` no frontmatter
- [ ] O problema está declarado em uma frase clara
- [ ] O apetite está definido no PRD

Se alguma condição falhar: devolve para Giuliana com a explicação antes de avançar.

## Prompt frame do shaping

Ao iniciar um shaping, o agente verbaliza:

> "PRD aprovado. Vou iniciar o shaping do Ciclo [N]. O problema que estamos resolvendo é: [problema do PRD]. O apetite é [x]. Vou esboçar a solução e mapear os rabbit holes — você revisa e ajusta antes de escrevermos o pitch final."

## Sequência de trabalho

### 1. Confirma o problema e o apetite
Lê o PRD. Se algo parece inconsistente, sinaliza antes de avançar.

### 2. Esboça a solução (fat marker sketch em texto)
- Descreve a abordagem em alto nível
- Usa breadboards para fluxos: `[entrada] → [ação] → [resultado]`
- Não especifica implementação — esboça a direção
- Apresenta para Giuliana validar antes de continuar

### 3. Mapeia rabbit holes
Para cada rabbit hole identificado:
- Nomeia o risco
- Explica por que é perigoso para o apetite
- Propõe uma decisão: ignorar / resolver assim / decidir antes do Building

Apresenta para Giuliana — ela decide como tratar cada um.

### 4. Define no-gos
A partir dos no-gos do PRD + rabbit holes que serão ignorados + scope que ficou fora da solução esboçada.

### 5. Escreve o pitch completo
Usa o template `templates/PITCH.md`.
Apresenta para aprovação de Giuliana.

### 6. Conduz o Betting
Apresenta o pitch como candidato ao próximo ciclo.
Se houver outros pitches, apresenta comparação.
Giuliana faz o bet — o agente registra a decisão.

## Vocabulário em uso (o agente usa estes termos, não outros)

| Termo correto | Não usar |
|---|---|
| apetite | estimativa, prazo, velocidade |
| fat marker sketch | wireframe, mockup, protótipo |
| breadboard | fluxo detalhado, user flow |
| rabbit hole | risco técnico, débito |
| no-go | out of scope, won't have |
| betting | planning, prioritização, sprint planning |

## Output

`docs/PITCH.md` preenchido, com decisão de bet registrada no frontmatter.
Entrada no `session-log/` com o bet e a justificativa.
