# nest-clean

API de um fórum de perguntas feita com NestJS, Prisma e PostgreSQL. Fiz para praticar NestJS com autenticação JWT e validação com Zod.

## O que tem

- Criar conta, autenticar, criar pergunta e listar perguntas recentes
- Autenticação JWT com chaves RSA (RS256)
- Validação de entrada com Zod (pipe próprio)
- Prisma como ORM

## Estrutura

- `src/auth`: módulo, estratégia e guard do JWT
- `src/controllers`: rotas HTTP
- `src/pipes`: pipe de validação com Zod
- `src/prisma`: serviço do Prisma
- `src/env.ts`: validação das variáveis de ambiente
- `prisma/`: schema e migrations

## Como instalar

```bash
pnpm install        # o postinstall roda o prisma generate
cp .env.example .env
docker compose up -d
pnpm prisma migrate deploy
```

Gere as chaves e coloque em base64 no `.env`:

```bash
openssl genpkey -algorithm RSA -out private.pem -pkeyopt rsa_keygen_bits:2048
openssl rsa -in private.pem -pubout -out public.pem
base64 -w0 private.pem   # JWT_PRIVATE_KEY
base64 -w0 public.pem    # JWT_PUBLIC_KEY
```

## Como rodar

```bash
pnpm start:dev   # desenvolvimento
pnpm build && pnpm start:prod
```

As rotas de exemplo estão em `client.http`.

## Testes

O projeto ainda não tem testes. O que valido hoje é `pnpm build` e `pnpm lint`.
