# Projeto Next.js 16

Aplicação web moderna e produção-ready construída com **Next.js 16**, **React 19**, **TypeScript** e **TailwindCSS 4**. Implementa arquitetura Server-First com App Router, validação com **React Hook Form + Zod**, e componentes UI reutilizáveis com **shadcn/ui**.

## 🚀 Começando

### Pré-requisitos
- Node.js 18+
- npm (ou yarn/pnpm/bun)

### Instalação & Desenvolvimento

```bash
# Instalar dependências
npm install

# Rodar servidor local (porta 3000)
npm run dev
```

Abra [http://localhost:3000](http://localhost:3000) no navegador.

### Build & Produção

```bash
# Build otimizado
npm run build

# Rodar em produção localmente
npm start
```

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
- **Server Components por padrão** — São mais eficientes e seguras
- Adicione `'use client'` apenas quando precisar de:
  - Hooks (useState, useEffect, useContext, etc)
  - Event listeners (onClick, onChange, etc)
  - Browser APIs (localStorage, window, etc)

### Styling
- **Apenas TailwindCSS** — sem CSS modules, styled-components ou CSS inline
- Tokens customizados vão em `tailwind.config.ts`
- Classes reutilizáveis podem ir em `@apply` no `globals.css` (com moderação)

### Server Actions & Formulários
- Coloque Server Actions em `actions/`
- Combine com React Hook Form + Zod para validação robusta
- Sempre valide dados no servidor (nunca confie apenas na validação do client)

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

## ⚠️ Common Gotchas

- **`revalidatePath()` e `revalidateTag()`**: só funcionam dentro de Server Actions ou Route Handlers, não em componentes regulares
- **Middleware**: deve ficar em `middleware.ts` na **raiz do projeto**, não dentro de `app/`
- **Supabase em Dev**: no server use `createServerClient(cookies)`, no client use `createBrowserClient()`
- **Imagens externas**: precisam estar autorizadas em `next.config.ts` via `remotePatterns`
- **Dados sensíveis**: nunca exponha no client — use Server Actions para operações com banco/APIs

## 🚢 Deploy

Pronto para produção? Deploy automático no [Vercel](https://vercel.com) (criadores do Next.js):

1. Push para GitHub
2. Conecte o repositório no Vercel
3. Configure variáveis de ambiente
4. Deploy automático em cada push para `main`

**Alternativas**: Netlify, Railway, AWS Amplify, ou qualquer plataforma com suporte a Node.js.

[Saiba mais sobre deploy no Vercel](https://nextjs.org/docs/app/building-your-application/deploying)

## 📚 Documentações Importantes

- [Next.js 16 Docs](https://nextjs.org/docs)
- [React 19 Documentation](https://react.dev)
- [TailwindCSS 4](https://tailwindcss.com/docs)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [React Hook Form](https://react-hook-form.com/)
- [Zod Validation](https://zod.dev/)
- [shadcn/ui Components](https://ui.shadcn.com/docs)

## 📞 Suporte & Contribuição

Para dúvidas ou problemas:
- Consulte as documentações acima
- Abra uma issue no repositório
- Siga as convenções de código descritas acima

---

**Status**: Projeto em desenvolvimento ✨
