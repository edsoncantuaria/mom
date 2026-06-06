# MOM Context Index

Índice de memórias de **desenvolvimento** (agentes). Ler no **início** de cada sessão; atualizar no **fim**.

| Título | Arquivo | Status | Tags |
|--------|---------|--------|------|
| Dev local (sem rebuild Docker) | [dev-local-stack.md](./dev-local-stack.md) | active | dev docker frontend backend |
| Mestre adjudica + fila Gemini | [ia-gemini-adjudication.md](./ia-gemini-adjudication.md) | superseded | ia gemini ws fila |
| Auth JWT + WebSocket | [auth-token-ws.md](./auth-token-ws.md) | active | auth ws frontend |
| Arquiteto documentação | [documentation-architect.md](./documentation-architect.md) | active | docs |
| Worker → API WS relay | [ws-user-relay.md](./ws-user-relay.md) | superseded | ws fila |
| Workflow recall/distill MOM | [mom-context-workflow.md](./mom-context-workflow.md) | active | docs dev |
| Sprint doc architecture jun/2026 | [doc-sprint-architecture-2026-06.md](./doc-sprint-architecture-2026-06.md) | active | docs |
| Handshake sync entre PCs | [sync-handshake.md](./sync-handshake.md) | active | dev sync |
| Munição em ataque à distância | [combate-municao.md](./combate-municao.md) | active | combate memoria |
| Gemini single-attempt (sem retry) | [ia-gemini-single-attempt.md](./ia-gemini-single-attempt.md) | active | ia gemini penai |
| Death saves + game over PENAI | [combate-morte-death-saves.md](./combate-morte-death-saves.md) | active | combate frontend penai |
| BYOK no árbitro actionSense | [ia-byok-action-sense.md](./ia-byok-action-sense.md) | active | ia gemini auth penai |

**Superseded:** mover linha para seção abaixo com data.

## Superseded

| Título | Arquivo | Data | Motivo |
|--------|---------|------|--------|
| Mestre adjudica + fila Gemini | [ia-gemini-adjudication.md](./ia-gemini-adjudication.md) | 2026-06-06 | ADR 0001 — actionSense × motor; paths `ai-gemini/` removidos |
| Worker WS relay legado | [ws-user-relay.md](./ws-user-relay.md) | 2026-06-06 | PENAI usa `wsPubSub.ts` + canal `penai:ws:user` |
