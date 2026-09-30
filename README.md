# English Gym API

API REST para uma plataforma gratuita de treinos diários de inglês, criada no contexto do **ODS 4 – Educação de Qualidade**.

## Stack

- Node.js + TypeScript
- Express
- PostgreSQL
- Prisma ORM
- JWT
- bcrypt
- Zod
- Swagger/OpenAPI
- Docker Compose

## Funcionalidades

- Cadastro e login com JWT
- Perfis de usuário
- Níveis CEFR: A1, A2, B1, B2 e C1
- Treinos diários
- Exercícios por habilidade
- Correção e pontuação
- Streak diário
- Maior streak
- Área administrativa para CRUD de treinos e exercícios
- Documentação Swagger

## Como executar

### 1. Instale Node.js

Recomendado: Node.js 22+.

### 2. Configure o ambiente

```bash
cp .env.example .env
```

### 3. Suba o PostgreSQL

```bash
docker compose up -d
```

### 4. Instale as dependências

```bash
npm install
```

### 5. Gere o Prisma Client

```bash
npm run prisma:generate
```

### 6. Crie as tabelas

```bash
npm run prisma:migrate -- --name init
```

### 7. Popule dados iniciais

```bash
npm run prisma:seed
```

Admin inicial:

- E-mail: `admin@englishgym.local`
- Senha: `Admin123!`

**Altere/remova essas credenciais antes de qualquer publicação real.**

### 8. Rode a API

```bash
npm run dev
```

API: `http://localhost:3333`

Swagger: `http://localhost:3333/docs`

Health check: `http://localhost:3333/health`

## Principais endpoints

| Método | Endpoint | Acesso |
|---|---|---|
| POST | `/api/auth/register` | Público |
| POST | `/api/auth/login` | Público |
| GET | `/api/users/me` | Usuário |
| PUT | `/api/users/me` | Usuário |
| GET | `/api/trainings` | Usuário |
| GET | `/api/trainings/daily` | Usuário |
| GET | `/api/trainings/:id` | Usuário |
| POST | `/api/trainings` | Admin |
| PUT | `/api/trainings/:id` | Admin |
| DELETE | `/api/trainings/:id` | Admin |
| POST | `/api/exercises` | Admin |
| PUT | `/api/exercises/:id` | Admin |
| DELETE | `/api/exercises/:id` | Admin |
| POST | `/api/answers` | Usuário |
| POST | `/api/trainings/:trainingId/complete` | Usuário |
| GET | `/api/progress/me` | Usuário |

## Modelo de negócio

Cada usuário possui um nível CEFR. Os treinos são associados a um nível e possuem exercícios. Ao responder exercícios, a API calcula os pontos. Ao concluir um treino, a API atualiza o streak do usuário.

O conteúdo dos exercícios é armazenado no PostgreSQL. Isso mantém a primeira versão simples e permite futuramente adicionar um painel administrativo mais completo ou geração de conteúdo por IA sem alterar o núcleo da aplicação.
