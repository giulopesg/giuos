# GiuOS

**Sistema Operacional de Co-autoria de Produto para Claude Code.**

GiuOS transforma o Claude Code de um assistente de engenharia em um co-designer de produto. O agente raciocina junto com você, usa vocabulário metodológico, e espera sua aprovação em cada transição de fase -- do discovery ao produto no ar.

Este repositório funciona como **template**. Use-o para iniciar qualquer projeto de produto com um agente AI que segue processo real de design e engenharia.

---

## O que o GiuOS faz

Na prática, GiuOS impede que o agente faça o que a maioria dos agentes faz: pular direto para o código.

Em vez disso, ele segue um ciclo completo de produto:

1. **Discovery** -- entende o problema antes de propor solução
2. **Definicao** -- declara o problema em uma frase, valida personas
3. **PRD** -- formaliza o que sera construido, com limites claros
4. **Shaping** -- escreve o pitch Shape Up com solucao esbocada e rabbit holes
5. **Betting** -- voce decide o que entra no ciclo
6. **Spec** -- define comportamentos esperados (o que, nao como)
7. **Building** -- executa contra a spec aprovada
8. **Cooldown** -- retro antes do proximo ciclo

O agente so avanca de fase com aprovacao explicita. Nunca codifica sem spec assinada. Nunca inventa dados.

---

## Para quem e isso

- **Product designers** que querem um agente que respeite processo de design
- **Founders solos** que precisam de rigor metodologico sem ter equipe
- **Design engineers** que trabalham no ciclo completo -- do problema ao deploy
- **Qualquer pessoa** que queira impedir o agente de pular etapas

---

## Como usar

### 1. Crie um novo repositorio a partir do template

Clique em **"Use this template"** no GitHub, ou:

```bash
gh repo create meu-projeto --template giulopesg/giuos --public --clone
cd meu-projeto
```

### 2. Abra com Claude Code

```bash
claude
```

O agente le o `START-HERE.md` automaticamente e se orienta. Na primeira interacao, ele vai perguntar:

> "Estamos no inicio de uma ideia que ainda precisa de discovery, ou voce ja sabe o que quer construir?"

- **Modo Exploratorio** -- entra pelo discovery (Design Thinking, Double Diamond D1)
- **Modo Execucao** -- entra direto no PRD (voce ja sabe o problema)

### 3. Trabalhe junto

O agente propoe, voce revisa. Ele verbaliza o raciocinio antes de agir. Voce aprova antes de avancar. E assim ate o produto estar no ar.

---

## Metodologias integradas

GiuOS nao inventa metodologia. Combina frameworks consolidados, cada um ativado no momento certo do ciclo:

| Metodologia | Quando ativa | Para que |
|---|---|---|
| **Double Diamond** | Todo o ciclo | Frame macro -- orienta qual diamante e qual fase |
| **Design Thinking** | D1 -- Discover e Define | Empatia, personas, HMW, sintese de problema |
| **Service Design** | D1 -- quando ha multiplos atores | Jornada de servico, blueprint, pontos de contato |
| **Shape Up** | D2 -- Develop e Deliver | Shaping, betting, building -- ciclos com apetite definido |
| **Spec-Driven Development** | Antes de qualquer codigo | Spec de comportamento, nao de implementacao |

### Mapa visual do ciclo

```
D1 -- Problema                              D2 -- Solucao
--------------------------------------------------------------
Discover  -->  Define          -->         Develop  -->  Deliver
(diverge)     (converge)                  (diverge)    (converge)

Design Thinking                            Shape Up
Service Design (se aplicavel)              SDD + Spec

                      |
                     PRD
                (handoff D1-->D2)
```

O segundo diamante nao comeca antes do primeiro estar fechado.

---

## Estrutura do repositorio

```
projeto/
├── CLAUDE.md                    # Contrato do sistema -- comportamento do agente
├── START-HERE.md                # Primeiro arquivo que o agente le
├── WIZARD.md                    # Mapa de navegacao do ciclo completo
│
├── .claude/
│   ├── agents/                  # Agentes especializados por fase
│   │   ├── discovery-agent.md   # Conduz discovery com Design Thinking
│   │   ├── shaping-agent.md     # Escreve pitch Shape Up
│   │   ├── red-team-agent.md    # Ataca hipoteses frageis
│   │   └── build-agent.md       # Executa building contra a spec
│   │
│   ├── skills/                  # Skills invocaveis por slash command
│   │   ├── prd-generator/       # /prd -- constroi PRD campo a campo
│   │   ├── shape-up-shaping/    # /shape -- shaping + pitch
│   │   └── spec-generator/      # /spec -- gera spec de comportamento
│   │
│   ├── commands/                # Slash commands operacionais
│   │   ├── new-project.md       # /new-project -- inicia projeto
│   │   ├── decision.md          # /decision -- registra decisao no log
│   │   ├── shape.md             # /shape -- inicia shaping
│   │   ├── bet.md               # /bet -- conduz betting
│   │   ├── sprint-start.md      # /sprint-start -- inicia building
│   │   └── sprint-close.md      # /sprint-close -- encerra ciclo
│   │
│   └── rules/                   # Regras de comportamento do agente
│       ├── golden-rules.md      # 12 regras nao negociaveis
│       ├── methodology-map.md   # Quando usar qual metodologia
│       ├── co-authorship.md     # Como o agente raciocina junto
│       ├── design-to-code.md    # Figma primeiro para UI
│       └── documentation.md     # Frontmatter YAML + camadas de doc
│
├── docs/                        # Documentos do projeto (preenchidos no ciclo)
│   ├── DISCOVERY-SYNTHESIS.md
│   ├── PRD.md
│   ├── PITCH.md
│   ├── SPEC.md
│   └── PRODUCT-BRIEF.md
│
├── templates/                   # Templates com frontmatter YAML
│   ├── DISCOVERY-SYNTHESIS.md
│   ├── PRD.md
│   ├── PITCH.md
│   └── SPEC.md
│
├── stack-packs/                 # Decisoes tecnicas pre-validadas
│   └── nextjs-supabase/         # Next.js 14 + Supabase + Stripe + Tailwind
│
├── session-log/                 # Memoria de decisoes (max 20 linhas por entrada)
│   └── INDEX.md
│
└── src/                         # Codigo (so existe apos spec aprovada)
```

---

## Agentes

Cada fase do ciclo tem um agente especializado com comportamento definido.

### Discovery Agent
Ativo no D1 (Discover + Define). Conduz a exploracao do problema usando Design Thinking: mapeamento de contexto, personas, jobs to be done, pontos de dor, How Might We. Faz perguntas -- nao sugere solucoes. Produz `docs/DISCOVERY-SYNTHESIS.md`.

### Shaping Agent
Ativo apos PRD aprovado. Transforma o problema definido em pitch Shape Up: solucao esbocada (fat marker sketch), apetite, rabbit holes, no-gos. Conduz o betting. Produz `docs/PITCH.md`.

### Red Team Agent
Ativado antes de aprovacoes criticas. Ataca hipoteses frageis com tres perguntas: qual a hipotese mais fragil? Quem ja resolve isso? Qual o risco mais obvio que ninguem esta falando? Propoe mitigacoes, nao apenas riscos.

### Build Agent
Ativo apos spec assinada. Executa contra a spec, le o stack pack, respeita as regras de design-to-code (Figma MCP primeiro). Sinaliza rabbit holes e desvios antes de implementar. Registra decisoes no session log.

---

## Skills (slash commands)

| Comando | O que faz | Pre-condicao |
|---|---|---|
| `/new-project` | Inicia projeto, pergunta modo de entrada | -- |
| `/decision` | Registra decisao no session log | -- |
| `/shape` | Inicia shaping a partir do PRD | PRD aprovado |
| `/bet` | Conduz betting -- voce decide o que entra | Pitch escrito |
| `/sprint-start` | Inicia building do ciclo | Spec aprovada |
| `/sprint-close` | Encerra ciclo, retro, cooldown | Building concluido |

---

## Regras de ouro

Estas 12 regras definem o comportamento base do agente. Nao sao sugestoes.

1. Nunca codificar sem spec aprovada
2. Nunca avancar de fase sem aprovacao explicita
3. Ler antes de agir
4. Verbalizar o raciocinio antes de propor
5. Separar fato, inferencia, hipotese, e aberto
6. PRD antes de shaping. Spec antes de building
7. Session log para decisoes materiais
8. Frontmatter YAML em todos os documentos
9. Figma primeiro para UI (via Figma MCP)
10. Codigo modular -- arquivos abaixo de 200 linhas
11. Rabbit holes sao sinalizados, nao implementados
12. Voce e o dono do produto -- o agente propoe, voce decide

---

## Documentacao em camadas

Cada documento responde uma pergunta. Nao se misturam.

| Documento | Pergunta |
|---|---|
| `CLAUDE.md` | Como o agente se comporta? |
| `DISCOVERY-SYNTHESIS.md` | O que aprendemos sobre o problema? |
| `PRD.md` | O que vamos construir, para quem, com qual apetite? |
| `PITCH.md` | Como vamos construir? Qual o escopo? |
| `SPEC.md` | O que o sistema deve fazer? |
| `session-log/` | Por que cada decisao foi tomada? |

Todos os documentos usam **frontmatter YAML** -- campos estruturados para o agente parsear, corpo narrativo para humanos lerem.

---

## Stack Pack incluido

O template inclui um stack pack pre-configurado para **Next.js + Supabase SaaS**:

- **Framework:** Next.js 14+ App Router (TypeScript strict)
- **Banco:** Supabase (PostgreSQL + RLS)
- **Auth:** Supabase Auth (magic link + OAuth)
- **Estilizacao:** Tailwind CSS + shadcn/ui
- **Pagamentos:** Stripe Checkout + webhooks
- **Data fetching:** TanStack Query + Zod
- **Hosting:** Vercel

O stack pack inclui armadilhas conhecidas documentadas (middleware size limit, Stripe SDK v20 breaking changes, RLS) e uma ordem de execucao obrigatoria de 9 etapas.

Voce pode criar seus proprios stack packs em `stack-packs/`.

---

## Design-to-code

Para qualquer componente UI com referencia visual, o fluxo comeca no Figma:

```
Voce aponta o node no Figma
        |
Agente chama get_design_context via Figma MCP
        |
Agente le tokens, layout, componentes, variantes
        |
Agente gera codigo contra a spec visual
        |
Voce revisa o output
```

Tokens do Figma sao mapeados para Tailwind. Componentes usam shadcn/ui como base. Se nao houver referencia no Figma, o agente pergunta antes de inventar.

---

## Co-autoria, nao execucao

GiuOS nao e um agente que executa em silencio. E um co-designer que:

- Verbaliza o raciocinio antes de agir
- Usa vocabulario metodologico correto (apetite, nao estimativa; rabbit hole, nao risco tecnico)
- Faz perguntas de produto genuinas
- Discorda quando tem razao tecnica
- Espera aprovacao em cada transicao

O agente fala com voce como um co-designer senior -- nao como um assistente.

---

## Exemplo de interacao

```
Voce:   Modo Exploratorio -- tenho uma ideia mas preciso explorar o problema primeiro.

Agente: Modo Exploratorio confirmado. Estamos no Estagio 1 -- Discovery,
        primeiro diamante do Double Diamond, com Design Thinking ativo.
        Vamos comecar pelo mapeamento de contexto.
        Me conta: qual e a ideia que esta na tua cabeca?

[... discovery acontece ...]

Agente: Aqui esta a sintese do que descobrimos. O problema central que
        emerge e [x]. Voce concorda com essa leitura antes de fecharmos
        o primeiro diamante?

Voce:   Concordo. Avanca.

Agente: Primeiro diamante fechado. Vou construir o PRD com voce agora.
        Comecando pelo problema...
```

---

## Como contribuir

Este e um template pessoal em evolucao. Se voce quiser adaptar para seu contexto:

1. Faca fork
2. Ajuste as regras em `.claude/rules/` para o seu vocabulario
3. Crie seus proprios stack packs
4. Modifique os agents para o seu fluxo

---

## Creditos

Criado por **Giuliana Lopes Galvao** -- Lead UX Designer e Design Engineer.

GiuOS nasceu da conviccao de que agentes AI devem respeitar processo de design, nao substituir.
