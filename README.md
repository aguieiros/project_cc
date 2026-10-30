# 🎯 Project CC - Next.js 16 Starter Kit

[![Next.js 16](https://img.shields.io/badge/Next.js-16.4-black?style=flat-square&logo=next.js)](https://nextjs.org)
[![React 19](https://img.shields.io/badge/React-19.3-blue?style=flat-square&logo=react)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![TailwindCSS 4](https://img.shields.io/badge/TailwindCSS-4-38B2AC?style=flat-square&logo=tailwindcss)](https://tailwindcss.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)

Sistema web moderno, produção-ready e altamente escalável construído com as tecnologias mais recentes do ecossistema JavaScript/React. 

Implementa **Server-First Architecture** com App Router, validação robusta com React Hook Form + Zod, e componentes UI reutilizáveis com shadcn/ui. Perfeito como starter kit para projetos empresariais, SaaS, dashboards e aplicações web complexas.

### ✨ Características

- ⚡ **Server-First Architecture** — Performance otimizada com Server Components
- 🎨 **Design System Ready** — shadcn/ui + TailwindCSS 4 (Turbopack)
- 📝 **Form Validation** — React Hook Form + Zod para validação type-safe
- 🔒 **Type Safety** — TypeScript 5 em 100% do código
- 🚀 **Produção Ready** — ESLint, configuração otimizada, best practices
- 📦 **Moderna Stack** — Next.js 16, React 19, TailwindCSS 4
- 🔄 **CI/CD Ready** — Deploy fácil no Vercel (ou qualquer plataforma Node.js)

## 🚀 Quick Start

### Pré-requisitos
- **Node.js 18+** ([Download](https://nodejs.org))
- **npm**, yarn, pnpm ou bun (qualquer gerenciador de pacotes)
- **Git** (para clonar o repositório)

### 1️⃣ Clonar & Instalar

```bash
# Clonar repositório
git clone https://github.com/aguieiros/project_cc.git
cd project_cc

# Instalar dependências
npm install
```

### 2️⃣ Desenvolvimento Local

```bash
npm run dev
```

Abra **[http://localhost:3000](http://localhost:3000)** no navegador. A página recarrega automaticamente ao editar arquivos.

### 3️⃣ Build & Produção

```bash
# Criar build otimizado
npm run build

# Testar build localmente
npm start
```

Acesse [http://localhost:3000](http://localhost:3000) para testar a build de produção.

## 📦 Tech Stack

- **Framework**: [Next.js 16](https://nextjs.org) (App Router)
- **React**: 19.3.0
- **Linguagem**: [TypeScript 5](https://www.typescriptlang.org/)
- **Estilo**: [TailwindCSS 4](https://tailwindcss.com) com Turbopack
- **Componentes UI**: [shadcn/ui](https://ui.shadcn.com/)
- **Validação**: [React Hook Form](https://react-hook-form.com/) + [Zod](https://zod.dev/)
- **Linting**: ESLint 9
- **Build**: Turbopack (suporte nativo no Next.js 16)

## 📁 Estrutura do Projeto

```
projeto-1/
├── app/                    # App Router - rotas e layout
│   ├── layout.tsx         # Layout raiz
│   ├── page.tsx           # Página inicial
│   └── globals.css        # Estilos globais
├── components/            # Componentes reutilizáveis (criar conforme necessário)
│   └── ui/               # Primitivos shadcn/ui
├── lib/                   # Helpers, clients, configs
├── types/                 # Types globais e schemas Zod
├── actions/               # Server Actions
├── public/                # Assets estáticos
├── tailwind.config.ts     # Configuração TailwindCSS
├── tsconfig.json          # TypeScript config
├── next.config.ts         # Next.js config
└── package.json           # Dependências

```

## 🎯 Arquitetura

### Server-First Pattern
- **Server Components First**: componentes são Server por padrão — adicionar `'use client'` apenas quando necessário (hooks, eventos, browser APIs)
- **Rotas**: organizadas em `app/` com suporte a agrupamento `(grupo)/` para melhor organização
- **Mutações**: via Server Actions em `actions/` — **NUNCA** chamar banco de dados diretamente em Client Components
- **Validação**: esquemas Zod em `types/` + React Hook Form para formulários
- **Styling**: apenas TailwindCSS, sem CSS-in-JS ou inline styles

### Estrutura de Pastas
- `app/` — rotas, layout raiz, Server Components
- `components/ui/` — primitivos reutilizáveis do shadcn/ui
- `components/` — componentes de feature (específicos de funcionalidades)
- `lib/` — helpers, utilitários, configurações de clientes (Supabase, Stripe, etc)
- `types/` — tipos TypeScript globais e schemas Zod compartilhados
- `actions/` — Server Actions para mutações e operações do servidor
- `public/` — assets estáticos (SVGs, imagens, fonts)

## 📋 Scripts Disponíveis

```bash
npm run dev          # Servidor de desenvolvimento (porta 3000)
npm run build        # Build de produção otimizado
npm start            # Rodar build em produção
npm run lint         # Executar ESLint
```

## 🎨 Convenções de Código

### Nomes de Arquivos & Pastas
- **Pastas**: `kebab-case` (ex: `user-profile`, `payment-gateway`)
- **Componentes**: `PascalCase` (ex: `UserCard.tsx`, `LoginForm.tsx`)
- **Utilitários/Helpers**: `camelCase` (ex: `formatDate.ts`, `calculateTotal.ts`)

### TypeScript
- **Nunca** use `any` explícito — use `unknown` + type guard ou `as const`
- Prefira type-safety: tipos implícitos são aceitáveis, mas erros devem ser tipados
- Compartilhe tipos globais em `types/` com Zod schemas quando apropriado

### Componentes React

**Server Components por padrão** — São mais eficientes, seguras e reduzem tamanho do bundle JavaScript.

**Quando adicionar `'use client'`** (apenas quando necessário):
```typescript
// ✅ USE CLIENT QUANDO:
- Usar hooks (useState, useEffect, useContext, etc)
- Adicionar event listeners (onClick, onChange, etc)
- Acessar Browser APIs (localStorage, window, navigator, etc)
- Implementar cliente-side interatividade

// ❌ NÃO USE QUANDO:
- Buscar dados do servidor (use Server Components)
- Chamar banco de dados (use Server Actions)
- Usar credenciais/secrets (ficam expostas!)
```

**Exemplo - Server Component (padrão):**
```tsx
// app/posts/page.tsx
export default async function Posts() {
  const posts = await fetch('api/posts') // ✅ Seguro no servidor
  return <div>{/* render posts */}</div>
}
```

**Exemplo - Client Component (quando necessário):**
```tsx
// components/Counter.tsx
'use client'
import { useState } from 'react'

export default function Counter() {
  const [count, setCount] = useState(0) // ✅ Hook necessário
  return <button onClick={() => setCount(count + 1)}>{count}</button>
}
```

### Styling
- **Apenas TailwindCSS** — sem CSS modules, styled-components ou CSS inline
- Tokens customizados vão em `tailwind.config.ts`
- Classes reutilizáveis podem ir em `@apply` no `globals.css` (com moderação)

### Server Actions & Formulários

Coloque Server Actions em `actions/` e combine com React Hook Form + Zod para validação robusta.

**Sempre valide dados no servidor** — nunca confie apenas na validação do client!

**Exemplo - Schema Zod:**
```typescript
// types/user.ts
import { z } from 'zod'

export const createUserSchema = z.object({
  name: z.string().min(2, 'Nome deve ter pelo menos 2 caracteres'),
  email: z.string().email('Email inválido'),
  password: z.string().min(8, 'Senha deve ter no mínimo 8 caracteres'),
})

export type CreateUserInput = z.infer<typeof createUserSchema>
```

**Exemplo - Server Action:**
```typescript
// actions/user.ts
'use server'
import { createUserSchema } from '@/types/user'

export async function createUser(data: unknown) {
  // Validar dados (type-safe!)
  const validated = createUserSchema.parse(data)
  
  // Chamar banco de dados
  const user = await db.user.create({ data: validated })
  
  return { success: true, user }
}
```

**Exemplo - Client Form:**
```tsx
// components/CreateUserForm.tsx
'use client'
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { createUserSchema } from '@/types/user'
import { createUser } from '@/actions/user'

export default function CreateUserForm() {
  const { register, handleSubmit } = useForm({
    resolver: zodResolver(createUserSchema),
  })

  return (
    <form onSubmit={handleSubmit(async (data) => {
      const result = await createUser(data)
      if (result.success) alert('Usuário criado!')
    })}>
      <input {...register('name')} placeholder="Nome" />
      <input {...register('email')} placeholder="Email" />
      <input {...register('password')} type="password" />
      <button type="submit">Criar Usuário</button>
    </form>
  )
}
```

## 🔧 Configuração

### Variáveis de Ambiente

Criar arquivo `.env.local` (copiar `.env.example` se existir):

```bash
# Valores públicos (acessíveis no client)
NEXT_PUBLIC_API_URL=https://api.example.com

# Segredos (apenas no servidor - NUNCA exponha no client)
DATABASE_URL=postgresql://...
API_SECRET=seu-secret-key
STRIPE_SECRET_KEY=sk_...
```

**⚠️ Importante**: Variáveis com prefixo `NEXT_PUBLIC_` ficam visíveis no bundle do cliente — use apenas para valores não-sensíveis (URLs públicas, IDs de aplicação, etc).

### Type Checking & Linting

Antes de commitar, executar:

```bash
npm run lint
```

## 🔄 Git Workflow

### Branch Naming
```bash
feat/feature-name       # Nova funcionalidade
fix/bug-description     # Correção de bug
chore/task-description  # Tarefas de manutenção
```

### Commits
- Use mensagens **imperativas** em inglês
- Exemplo: `add user authentication`, `fix loading state`, `update dependencies`

### Process
1. Crie branch a partir de `main`: `git checkout -b feat/sua-feature`
2. Faça commits pequenos e significativos
3. Push para o repositório
4. Abra Pull Request com descrição clara
5. Aguarde review e merge

## ⚠️ Troubleshooting & Common Gotchas

### 🔄 Revalidação de Cache

❌ **ERRADO:** Usar `revalidatePath()` em um componente
```typescript
// ❌ Isso não funciona!
export default function Page() {
  revalidatePath('/') // ERROR: revalidatePath only works in Server Actions
}
```

✅ **CORRETO:** Usar em Server Action
```typescript
// ✅ Funciona!
'use server'
export async function updatePost(id: string) {
  await db.post.update({ where: { id } })
  revalidatePath(`/posts/${id}`)
}
```

### 🛣️ Middleware

❌ **ERRADO:** `middleware.ts` dentro de `app/`
```
app/
  middleware.ts  ❌
```

✅ **CORRETO:** `middleware.ts` na raiz do projeto
```
projeto-1/
  middleware.ts  ✅
  app/
```

### 🖼️ Imagens Externas

```typescript
// next.config.ts
export default {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'example.com',
      },
    ],
  },
}
```

### 🔐 Dados Sensíveis

```typescript
// ❌ NUNCA faça isso!
export default function Page() {
  const apiKey = process.env.STRIPE_SECRET_KEY // Exposto no client!
}

// ✅ Use Server Actions
'use server'
export async function processPayment(amount: number) {
  const apiKey = process.env.STRIPE_SECRET_KEY // Seguro no servidor
  // processar pagamento...
}
```

### 📦 Supabase Client

```typescript
// lib/supabase-server.ts
'use server'
import { createServerClient } from '@supabase/ssr'
import { cookies } from 'next/headers'

export async function getSupabaseServer() {
  return createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY,
    { cookies }
  )
}
```

```typescript
// lib/supabase-client.ts
'use client'
import { createBrowserClient } from '@supabase/ssr'

export const supabase = createBrowserClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY,
)

## 🚢 Deployment

### 🔷 Vercel (Recomendado)

[Vercel](https://vercel.com) é criada pelo time do Next.js e oferece a melhor integração:

1. **Fazer push para GitHub** (já feito!)
2. **Criar conta no Vercel** e conectar GitHub
3. **Importar projeto** — Vercel detecta Next.js automaticamente
4. **Configurar variáveis de ambiente** no Vercel Dashboard
5. **Deploy automático** em cada push para `main`

[📖 Guia completo de deployment no Vercel](https://nextjs.org/docs/app/building-your-application/deploying)

### 🟢 Alternativas

| Plataforma | Tipo | Custo | Melhor para |
|-----------|------|-------|-----------|
| **Vercel** | Serverless | Freemium | Next.js (melhor integração) |
| **Railway** | PaaS | Pay-as-you-go | Começar rápido, ótima DX |
| **Netlify** | Serverless | Freemium | Sites estáticos/dinâmicos |
| **AWS Amplify** | Managed | Freemium | Escala corporativa |
| **Render** | PaaS | Freemium | Simples e confiável |

### Variáveis de Ambiente em Produção

Exemplo para Vercel:
```bash
NEXT_PUBLIC_API_URL=https://api.seu-dominio.com
DATABASE_URL=postgresql://user:pass@host:5432/dbname
STRIPE_SECRET_KEY=sk_live_xxxxx
JWT_SECRET=seu-secret-muito-seguro-aqui
```

⚠️ **NUNCA commit `.env.local`** — use `.env.example` versionado

## 📚 Recursos & Documentações

### 🔗 Documentações Oficiais
- **[Next.js 16 Docs](https://nextjs.org/docs)** — Guia completo, App Router, deployment
- **[React 19 Documentation](https://react.dev)** — Aprenda React, hooks, patterns
- **[TypeScript Handbook](https://www.typescriptlang.org/docs/)** — Type safety em profundidade

### 🎨 Design & Styling
- **[TailwindCSS 4](https://tailwindcss.com/docs)** — Utility-first CSS framework
- **[shadcn/ui](https://ui.shadcn.com/docs)** — Componentes reutilizáveis em React
- **[Heroicons](https://heroicons.com/)** — Ícones de alta qualidade (vai bem com shadcn)

### 🛠️ Ferramentas & Validação
- **[React Hook Form](https://react-hook-form.com/)** — Forms performáticas
- **[Zod](https://zod.dev/)** — TypeScript-first schema validation
- **[@hookform/resolvers](https://github.com/react-hook-form/resolvers)** — Integradores Zod + React Hook Form

### 🌐 Integração com Serviços
- **[Supabase Docs](https://supabase.com/docs)** — PostgreSQL + Auth + Realtime
- **[Stripe Docs](https://stripe.com/docs)** — Pagamentos online
- **[Auth0 Docs](https://auth0.com/docs)** — Autenticação empresarial

### 📖 Blogs & Aprendizado
- **[Vercel Blog](https://vercel.com/blog)** — News sobre Next.js, performance, patterns
- **[Kent C. Dodds](https://kentcdodds.com/)** — React expert, artigos profundos
- **[Lee Robinson](https://leerob.io/)** — Next.js specialist, tutorials

## 💡 Próximos Passos (Após Clonar)

```bash
# 1. Instalar dependências
npm install

# 2. Copiar exemplo de env
cp .env.example .env.local  # (criar se não existir)

# 3. Iniciar desenvolvimento
npm run dev

# 4. Criar primeira feature em nova branch
git checkout -b feat/minha-primeira-feature

# 5. Fazer mudanças, commit, push, PR
```

## 📞 Suporte & Contribuição

Dúvidas ou quer contribuir?

1. **Consulte as documentações** listadas acima (resolvem 90% dos problemas)
2. **Abra uma issue** no [repositório](https://github.com/aguieiros/project_cc/issues)
3. **Siga as convenções** de código descritas acima
4. **Faça um Pull Request** — siga o Git Workflow

### Código de Conduta
Somos um espaço inclusivo. Tratamos todos com respeito e valorizamos contribuições de qualquer nível.

---

## 📊 Status do Projeto

| Componente | Status | Notas |
|-----------|--------|-------|
| **Setup Inicial** | ✅ Completo | Next.js 16, React 19, TypeScript |
| **UI Components** | 🟡 Em Desenvolvimento | shadcn/ui pronto, adicione conforme necessário |
| **Autenticação** | ⏳ Planejado | Integrar Auth0, Supabase ou NextAuth |
| **Banco de Dados** | ⏳ Planejado | Supabase recomendado |
| **Testes** | ⏳ Planejado | Vitest + Testing Library |

---

**criado com ❤️ usando [Claude Code](https://claude.com/claude-code)**

© 2024 Project CC. Licença MIT.
