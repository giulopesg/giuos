# Stack Pack — Next.js + Supabase SaaS

> Inteligência operacional para projetos SaaS com Next.js 14+ App Router + Supabase.
> Baseado em decisões validadas em produção — inclui armadilhas conhecidas e suas soluções.
> **Ativado pelo agente após bet aceito e SPEC aprovada. Lido pelo build-agent antes de qualquer código.**

---

## Stack completa

| Camada | Tecnologia | Versão |
|---|---|---|
| Framework | Next.js App Router | 14+ (stable) |
| Linguagem | TypeScript | strict mode |
| Banco | Supabase (PostgreSQL + RLS) | latest stable |
| Auth | Supabase Auth (magic link + OAuth) | — |
| Estilização | Tailwind CSS | 4 |
| Componentes UI | shadcn/ui | latest |
| Data fetching | TanStack Query | latest |
| Validação | Zod | latest |
| Pagamentos | Stripe Checkout + webhooks | SDK v20+ |
| Email | Resend | latest |
| Hosting | Vercel | free tier |
| Design | Figma → Figma MCP → código | — |

---

## Ordem de execução (obrigatória)

O build-agent executa nesta ordem. Não pula etapas.

### Etapa 0 — Infraestrutura (PRIMEIRO)
1. Criar repositório no GitHub
2. Conectar Vercel ao repo (deploy automático)
3. Criar banco PostgreSQL no Supabase
4. Subir hello world — confirmar que o site está no ar
5. Configurar domínio (opcional)

**Critério de conclusão:** URL funcionando em `https://projeto.vercel.app`

---

### Etapa 1 — Schema do banco (Supabase)

Entidades obrigatórias no schema:
- **profiles** — id (refs auth.users), name, email, stripe_customer_id, stripe_price_id, stripe_subscription_id, stripe_current_period_end, trial_ends_at, plan (enum: FREE/TRIAL/PRO)
- **Entidades do produto** — definidas na SPEC

RLS ativo desde o início. Service role key apenas em `lib/supabase/server.ts` (server-side).

---

### Etapa 2 — Autenticação (Supabase Auth)

- Magic link via Resend + Google OAuth
- Primeiro login → `plan=TRIAL`, `trial_ends_at=now+14dias`
- Middleware protegendo `/dashboard/*`, `/app/*`, `/settings/*`

**Armadilha conhecida — Middleware e tamanho:**
O middleware NÃO deve importar o cliente Supabase completo com todas as dependências. Estourar 1MB no Vercel free tier quebra o deploy silenciosamente. Usar verificação leve de cookie no middleware — cliente completo só nas Server Actions e Route Handlers.

---

### Etapa 3 — Trial e assinatura

Funções em `lib/subscription.ts`:
- `isTrialActive(profile)` — trial_ends_at > now E plan === TRIAL
- `isSubscribed(profile)` — plan === PRO E stripe_current_period_end > now
- `hasAccess(profile)` — isTrialActive OR isSubscribed
- `daysLeftInTrial(profile)` — dias restantes

---

### Etapa 4 — Paywall e limites

- Constante `PLAN_LIMITS` com limites por plano
- Função `checkUsageLimit(profile, resource)`
- Componente `<PaywallGate>` que bloqueia com CTA de upgrade

---

### Etapa 5 — Stripe (pagamentos)

- Checkout Session (subscription)
- Customer Portal
- Webhooks: `checkout.session.completed`, `invoice.payment_succeeded`, `customer.subscription.deleted`, `customer.subscription.updated`

**Armadilha conhecida — Stripe SDK v20:**
`current_period_end` foi removido do objeto Subscription. Usar `invoice.period_end` via `latest_invoice`. `invoice.subscription` virou `invoice.parent.subscription_details.subscription`. API version: `2026-02-25.clover`.

**Armadilha conhecida — Stripe client:**
Inicializar com lazy init (proxy pattern) para evitar crash no build quando `STRIPE_SECRET_KEY` não está configurada.

**Upgrade durante trial:**
O checkout NÃO define `trial_period_days` em `subscription_data` — usuário TRIAL pode virar PRO imediatamente passando o cartão. Webhook `checkout.session.completed` atualiza `plan: PRO` no banco.

---

### Etapa 6 — Features do produto

Implementar features definidas na SPEC com:
- Server Actions para mutations
- TanStack Query para data fetching client-side
- Zod para validação de inputs
- RLS como primeira linha de defesa no banco

---

### Etapa 7 — Landing page

Seções: Hero → Features → Screenshots → Pricing → Footer

---

### Etapa 8 — Screenshots reais

Tirar screenshots do app funcionando e colocar na landing.

---

### Etapa 9 — Configuração final

- `.env.example` completo com todos os secrets documentados
- `README.md` com setup passo a passo

---

## Estrutura de pastas

```
projeto/
├── app/
│   ├── (public)/           # landing, pricing, login
│   ├── (app)/              # rotas autenticadas
│   └── api/
│       └── stripe/
│           └── webhook/route.ts
├── features/               # organizado por domínio, não por camada técnica
│   ├── auth/
│   │   ├── components/
│   │   ├── actions/
│   │   └── index.ts
│   └── billing/
├── lib/
│   ├── supabase/
│   │   ├── client.ts       # browser
│   │   └── server.ts       # server (service role apenas aqui)
│   ├── stripe.ts           # lazy init
│   ├── subscription.ts
│   └── validations.ts
├── components/
│   └── ui/                 # shadcn/ui
└── middleware.ts            # leve — sem imports pesados
```

---

## Variáveis de ambiente

```bash
# Supabase
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=      # nunca NEXT_PUBLIC_

# Auth
SUPABASE_AUTH_EXTERNAL_GOOGLE_CLIENT_ID=
SUPABASE_AUTH_EXTERNAL_GOOGLE_SECRET=

# Stripe
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
STRIPE_PRICE_ID_PRO=

# Email
RESEND_API_KEY=

# App
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

---

## Armadilhas documentadas

| Armadilha | Problema | Solução |
|---|---|---|
| Middleware pesado | Estourar 1MB Vercel free tier | Não importar Supabase client completo no middleware — verificar cookie diretamente |
| Stripe SDK v20 | `current_period_end` removido | Usar `invoice.period_end` via `latest_invoice` |
| Stripe subscription field | `invoice.subscription` mudou | Usar `invoice.parent.subscription_details.subscription` |
| Stripe client init | Crash no build sem secret key | Lazy init com proxy pattern |
| Vercel env vars | Build compila mas falha no deploy | Todas as vars do `.env.example` devem estar na Vercel antes do deploy |
| RLS desabilitado | Exposição de dados de outros usuários | RLS ativo desde o início, testado antes de qualquer dado real |
| Server actions com Supabase | Usar cliente errado (browser no server) | `lib/supabase/server.ts` para server, `lib/supabase/client.ts` para browser |

---

## Design-to-code nesta stack

Para componentes UI:
1. Giuliana aponta o frame ou component no Figma
2. Build-agent chama `get_design_context` via Figma MCP
3. Mapeia tokens do Figma para Tailwind
4. Gera o componente usando shadcn/ui como base quando aplicável
5. Giuliana revisa antes de finalizar
