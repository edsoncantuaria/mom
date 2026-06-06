# Dev local — hot reload sem rebuild Docker

Status: active  
Atualizado: 2026-05-29  
Doc: ECOSSISTEMA (dev) · `npm run dev:local`

## Por quê

`compose:app` / profile `full` roda **produção** (`next build` + `node dist`) — cada fix exige `--build`.

## O quê

- **Infra:** `npm run dev:local` → Docker só MySQL, Redis, SRD, MinIO, Piper, Qdrant
- **Backend:** `npm run dev:backend` → `tsx watch` porta 8071 (+ worker BullMQ no mesmo processo)
- **Frontend:** `npm run dev` → `next dev` porta 9002, `NEXT_DIST_DIR=.next-dev` (evita `.next` root-owned do Docker)
- Env: `backend/.env` `DB_HOST=localhost`; raiz `.env.local` com `NEXT_PUBLIC_API_URL`

## Armadilhas

- Não usar `docker:up` / `compose:app` no dia a dia de código
- `.next/` criada como root pelo Docker → usar `.next-dev` ou `sudo rm -rf .next`
- `AI_ENGINE=gemini` no `backend/.env` (não `oss` sem OpenRouter)

## Comandos

```bash
npm run dev:local
npm run dev:backend   # terminal 2
npm run dev           # terminal 3
```
