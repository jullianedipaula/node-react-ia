# 🎣 Webhook Inspector

Uma aplicação fullstack moderna para capturar, inspecionar e gerar handlers TypeScript para webhooks usando IA.

## 📋 Sobre o Projeto

O Webhook Inspector é uma ferramenta que permite capturar webhooks de qualquer origem, visualizar seus detalhes e, melhor ainda, usar IA (Google Gemini) para gerar automaticamente handlers TypeScript com validação Zod baseados nos webhooks capturados.

### ✨ Funcionalidades

- 🎯 **Captura de Webhooks**: Endpoint universal para capturar qualquer tipo de webhook
- 📊 **Visualização Detalhada**: Interface moderna para visualizar método, headers, body, IP e timestamp
- 🤖 **Geração de Código com IA**: Use Google Gemini para gerar handlers TypeScript automaticamente
- ✅ **Validação com Zod**: Handlers gerados incluem schemas Zod para validação
- 📚 **API Documentada**: Documentação interativa com Swagger/Scalar
- 🎨 **Interface Moderna**: UI construída com React, TailwindCSS e Radix UI
- 🔄 **Monorepo**: Estrutura organizada com pnpm workspaces

## 🏗️ Arquitetura

Este projeto é um monorepo que contém:

### Backend (`api/`)
- **Framework**: Fastify com TypeScript
- **Banco de Dados**: PostgreSQL + Drizzle ORM
- **IA**: Google Gemini (via AI SDK)
- **Documentação**: Swagger/Scalar API Reference
- **Validação**: Zod + fastify-type-provider-zod

### Frontend (`web/`)
- **Framework**: React 19 + Vite
- **Roteamento**: TanStack Router
- **Estado**: TanStack Query
- **Estilização**: TailwindCSS 4 + Radix UI
- **Syntax Highlighting**: Shiki

## 🚀 Começando

### Pré-requisitos

- Node.js 18+ 
- pnpm 10+
- Docker e Docker Compose

### Instalação

1. **Clone o repositório**
```bash
git clone <url-do-repositorio>
cd node-react
```

2. **Instale as dependências**
```bash
pnpm install
```

3. **Configure as variáveis de ambiente**

Crie um arquivo `.env` na pasta `api/`:

```env
NODE_ENV=development
PORT=3333
DATABASE_URL=postgres://docker:docker@localhost:5433/webhooks
GEMINI_API_KEY=sua_chave_api_do_gemini
```

> 💡 Obtenha sua chave do Gemini em: https://aistudio.google.com/apikey

4. **Inicie o banco de dados**
```bash
cd api
docker-compose up -d
```

5. **Execute as migrations**
```bash
cd api
pnpm db:migrate
```

6. **[Opcional] Popule o banco com dados de exemplo**
```bash
cd api
pnpm db:seed
```

### Executando o Projeto

#### Desenvolvimento

Execute ambos os serviços simultaneamente:

**Terminal 1 - Backend:**
```bash
cd api
pnpm dev
```

**Terminal 2 - Frontend:**
```bash
cd web
pnpm dev
```

A API estará disponível em: `http://localhost:3333`  
A documentação em: `http://localhost:3333/docs`  
O frontend em: `http://localhost:5173`

## 📝 Como Usar

### 1. Capturando Webhooks

Envie qualquer requisição HTTP para:
```
POST http://localhost:3333/capture/<seu-endpoint>
```

Exemplo:
```bash
curl -X POST http://localhost:3333/capture/github/push \
  -H "Content-Type: application/json" \
  -d '{"event": "push", "repository": "my-repo"}'
```

### 2. Visualizando Webhooks

Acesse `http://localhost:5173` para ver todos os webhooks capturados com seus detalhes.

### 3. Gerando Handlers com IA

1. Selecione um ou mais webhooks na interface
2. Clique em "Generate Handler"
3. A IA gerará um handler TypeScript completo com:
   - Schemas Zod para cada tipo de evento
   - Função de validação
   - Tratamento de erros
   - Tipagem TypeScript completa

## 🛠️ Scripts Disponíveis

### API
```bash
pnpm dev          # Inicia o servidor em modo desenvolvimento
pnpm start        # Inicia o servidor em produção
pnpm format       # Formata o código com Biome
pnpm db:generate  # Gera migrations do Drizzle
pnpm db:migrate   # Executa migrations
pnpm db:studio    # Abre o Drizzle Studio
pnpm db:seed      # Popula o banco com dados de exemplo
```

### Web
```bash
pnpm dev          # Inicia o servidor de desenvolvimento
pnpm build        # Compila para produção
pnpm preview      # Preview da build de produção
pnpm format       # Formata o código com Biome
```

## 🗄️ Estrutura do Banco de Dados

A tabela `webhooks` armazena:
- `id`: UUID v7
- `method`: Método HTTP (GET, POST, etc.)
- `pathname`: Caminho da requisição
- `headers`: Headers da requisição
- `body`: Corpo da requisição
- `contentType`: Content-Type
- `contentLength`: Tamanho do conteúdo
- `ip`: Endereço IP de origem
- `createdAt`: Timestamp da captura

## 📡 API Endpoints

- `GET /api/webhooks` - Lista todos os webhooks
- `GET /api/webhooks/:id` - Detalhes de um webhook específico
- `DELETE /api/webhooks/:id` - Remove um webhook
- `ALL /capture/*` - Captura webhooks de qualquer método HTTP
- `POST /api/generate` - Gera handler TypeScript com IA

Documentação completa disponível em: `http://localhost:3333/docs`

## 🛡️ Tecnologias Utilizadas

### Backend
- [Fastify](https://fastify.dev/) - Framework web rápido e de baixo overhead
- [Drizzle ORM](https://orm.drizzle.team/) - ORM TypeScript-first
- [PostgreSQL](https://www.postgresql.org/) - Banco de dados relacional
- [Zod](https://zod.dev/) - Validação de schemas TypeScript-first
- [AI SDK](https://sdk.vercel.ai/) - SDK para integração com IA
- [Google Gemini](https://ai.google.dev/) - Modelo de IA generativa
- [Biome](https://biomejs.dev/) - Linter e formatador

### Frontend
- [React 19](https://react.dev/) - Biblioteca UI
- [Vite](https://vitejs.dev/) - Build tool e dev server
- [TanStack Router](https://tanstack.com/router) - Roteamento type-safe
- [TanStack Query](https://tanstack.com/query) - Gerenciamento de estado assíncrono
- [TailwindCSS](https://tailwindcss.com/) - Framework CSS utility-first
- [Radix UI](https://www.radix-ui.com/) - Componentes acessíveis
- [Lucide React](https://lucide.dev/) - Ícones
- [Shiki](https://shiki.style/) - Syntax highlighting


