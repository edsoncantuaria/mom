# Dev local — PENAI (Postgres + Temporal)

Status: active
Atualizado: 2026-06-06
Doc: `scripts/dev-local.sh` · `docker-compose.penai.yml`

## Por quê

Stack canônico é Fastify/Postgres/Temporal — não MySQL/BullMQ legado.

## O quê

- **Infra:** `npm run dev:local` → Postgres:5433, Redis:6381, Temporal, Qdrant, SRD
- **API:** `cd backend && npm run dev:penai` → `:8071`
- **Worker:** `cd backend && npm run worker:temporal` (obrigatório para narração)
- **Frontend:** `npm run dev` → `:9002` com `NEXT_PUBLIC_PENAI_UI=true`
- Tudo-Docker hot reload: `npm run dev:all`

## Armadilhas

- Sem worker Temporal → narração não completa (a menos que `TEMPORAL_DISABLED=true`)
- `.next/` root-owned do Docker → `NEXT_DIST_DIR=.next-dev`
- `GEMINI_MAX_ATTEMPTS=1` — 429 falha o turno; não há retry automático

## Comandos

```bash
npm run dev:local
npm run penai:import:foundry-bundle --prefix backend
cd backend && npm run dev:penai
cd backend && npm run worker:temporal
npm run dev
```
