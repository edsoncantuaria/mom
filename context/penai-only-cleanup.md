# Cleanup PENAI-only (jun/2026)

Status: active  
Atualizado: 2026-06-06  
Doc: ECOSSISTEMA § PENAI | ADR 0002 | gaps.md

## Por quê

Dois runtimes (Express/MySQL/BullMQ vs Fastify/Postgres/Temporal) geravam imports quebrados, docs falsas e bloqueio de homolog PENAI. Homolog sem prod → corte limpo sem migração de dados.

## O quê (bullets)

- Docker: `docker-compose.yml` auxiliares; app = `docker-compose.penai.yml` + `cloudive`.
- Backend deletado: `entities/`, `actionService`, `narration/*`, Genkit, BullMQ deps, migrations MySQL.
- Backend consolidado: billing Postgres-only, WS só `?token=`, `responseParser` em `GameMaster/ai/`.
- Tipos mapa/sessão: `src/types/worldMap.ts` (extraídos de `gameService.ts`).
- Órfãos removidos: `backend/src/game/`, `validators/`, `schemaIntegrityService.ts`.
- `resolveGeminiApiKey`: BYOK fail-closed; servidor só com `AI_PLATFORM_BILLING_ENABLED=true`.
- Frontend: órfãos v1 removidos; `dedupeSensoryTail` no `PenaiStoryFeed`; sem `penaiBootstrap` / WS v1 `payload`; BYOK = `geminiApiKeyStorage` (sem OpenRouter).

## Armadilhas

- `npm run test --prefix backend` inclui specs de integração — falham sem Postgres local (:5433).
- `gameService.ts` ainda é facade para mapa/personagens; gameplay PENAI importa `penaiApi` direto.
- Não reintroduzir `worker:narration`, `SKIP_NARRATION_WORKERS`, profile Docker `full` MySQL.

## Comandos / paths

```bash
npm run dev:local          # Postgres + Redis + Temporal
npm run dev:all              # infra + API + worker + frontend
npm run penai:db:prepare --prefix backend
npm run test --prefix backend
npm run test:frontend
```

- ADR: `docs/adr/0002-penai-only-cut.md`
- Env backend: `backend/.env.penai.example`
- Env frontend: `.env.local.example`
