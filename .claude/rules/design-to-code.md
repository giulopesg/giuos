# Design-to-Code Rule — GiuOS

Para qualquer componente ou tela com referência visual, o fluxo começa no Figma — não no código.

---

## Fluxo padrão

```
Giuliana aponta o node no Figma
        ↓
Agente chama get_design_context via Figma MCP
        ↓
Agente lê tokens, layout, componentes, variantes
        ↓
Agente gera código contra a spec visual
        ↓
Giuliana revisa output
```

---

## Regras

1. **Perguntar antes de inventar.** Se existe uma referência visual para o componente e não foi fornecida, perguntar antes de gerar.

2. **Figma MCP é o padrão.** Usar `get_design_context` para extrair tokens, propriedades de componente, e estrutura de layout. Não inferir visualmente a partir de screenshots quando o acesso ao Figma está disponível.

3. **Tokens antes de valores hardcoded.** Se o design usa variáveis de cor, espaçamento, ou tipografia, mapear para o equivalente em código (CSS vars, Tailwind tokens) — não hardcodar valores.

4. **Variantes e estados.** Identificar todas as variantes e estados do componente no Figma antes de gerar código. Um componente incompleto de estados cria dívida técnica imediata.

5. **Pixel fidelity não é o objetivo.** O objetivo é fidelidade de comportamento e token — não pixel perfect a qualquer custo. Quando há conflito entre o design e a implementação razoável, sinalizar antes de decidir.

---

## Quando não há referência no Figma

Se o componente não existe no Figma e Giuliana autorizou geração livre:
- Seguir o design system existente do projeto (tokens, paleta, tipografia)
- Propor o componente como draft antes de finalizar
- Registrar como "sem referência Figma" no session log

---

## Stack de design

- **Design tool:** Figma
- **MCP:** Figma MCP (`get_design_context`, `get_design_context`)
- **Estilo:** Tailwind CSS (tokens mapeados do Figma quando possível)
- **Componentes base:** shadcn/ui (quando stack nextjs-supabase está ativa)
