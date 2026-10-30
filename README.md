# Projeto Next.js 16

Aplicação moderna construída com **Next.js 16**, **React 19**, **TypeScript** e **TailwindCSS 4**, seguindo padrões Server-First com App Router.

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
- **Linguagem**: TypeScript 5
- **Estilo**: [TailwindCSS 4](https://tailwindcss.com) com Turbopack
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

- **Server Components First**: componentes são Server por padrão
- **Rotas**: organizadas em `app/` com suporte a agrupamento `(grupo)/`
- **Mutações**: via Server Actions em `actions/` (nunca chamar DB em Client Components)
- **Styling**: apenas TailwindCSS, sem CSS-in-JS
- **Types**: compartilhados em `types/` com Zod schemas

## 📋 Scripts Disponíveis

```bash
npm run dev          # Servidor de desenvolvimento
npm run build        # Build de produção
npm start            # Rodar build em produção
npm run lint         # Executar ESLint
```

## 🔧 Configuração

### Variáveis de Ambiente

Criar arquivo `.env.local` (copiar `.env.example` se existir):

```bash
# Valores públicos (acessíveis no client)
NEXT_PUBLIC_API_URL=

# Segredos (apenas no servidor)
DATABASE_URL=
API_SECRET=
```

### Type Checking & Linting

Antes de commitar, executar:

```bash
npm run lint
npm run type-check  # se disponível
```

## 📚 Aprenda Mais

- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev)
- [TailwindCSS Documentation](https://tailwindcss.com/docs)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)

## 🚢 Deploy

Pronto para produção? Deployed fácil no [Vercel](https://vercel.com) (criadores do Next.js):

1. Push para GitHub
2. Conectar repositório no Vercel
3. Deploy automático em push para main

[Learn more about deploying on Vercel](https://nextjs.org/docs/app/building-your-application/deploying)
