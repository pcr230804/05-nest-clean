# 05 Nest Clean

API de fórum Q&A construída com NestJS seguindo Clean Architecture e DDD.

## Stack

- **NestJS** + **TypeScript**
- **Prisma** + **PostgreSQL**
- **JWT** (Passport) para autenticação
- **Zod** para validação
- **Redis** para cache
- **AWS S3 / Cloudflare R2** para upload de arquivos
- **Vitest** para testes (unitários e e2e)

## Arquitetura

```
src/
├── core/          # blocos base: entidades, either, eventos de domínio
├── domain/        # lógica de negócio por contexto (forum, notification)
│   ├── application/   # casos de uso e interfaces de repositório
│   └── enterprise/    # entidades e value objects de domínio
└── infra/         # detalhes de implementação
    ├── auth/
    ├── cache/
    ├── cryptography/
    ├── database/
    ├── env/
    ├── events/
    ├── http/
    └── storage/
```

## Endpoints

| Método | Rota | Descrição |
|--------|------|-----------|
| POST | /accounts | Criar conta |
| POST | /sessions | Autenticar |
| POST | /questions | Criar pergunta |
| GET | /questions | Listar perguntas recentes |
| GET | /questions/:slug | Buscar pergunta por slug |
| PUT | /questions/:id | Editar pergunta |
| DELETE | /questions/:id | Deletar pergunta |
| POST | /questions/:id/answers | Responder pergunta |
| GET | /questions/:id/answers | Listar respostas |
| PUT | /answers/:id | Editar resposta |
| DELETE | /answers/:id | Deletar resposta |
| PATCH | /answers/:id/choose-as-best | Escolher melhor resposta |
| POST | /questions/:id/comments | Comentar em pergunta |
| GET | /questions/:id/comments | Listar comentários da pergunta |
| DELETE | /questions/comments/:id | Deletar comentário de pergunta |
| POST | /answers/:id/comments | Comentar em resposta |
| GET | /answers/:id/comments | Listar comentários da resposta |
| DELETE | /answers/comments/:id | Deletar comentário de resposta |
| POST | /attachments | Upload de anexo |
| PATCH | /notifications/:id/read | Marcar notificação como lida |

## Rodando o projeto

```bash
# dependências
pnpm install

# variáveis de ambiente
cp .env.example .env

# banco e cache via docker
docker-compose up -d

# migrations
pnpm db:migrate

# dev
pnpm start:dev
```

## Testes

```bash
pnpm test        # unitários
pnpm test:e2e    # end-to-end
```
