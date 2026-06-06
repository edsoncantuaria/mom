# Worker narração → relay WS via Redis

Status: superseded  
Atualizado: 2026-06-06  
Doc: architecture/ws-pipeline-temporal.md · ECOSSISTEMA §8.6

## Por quê (histórico)

Worker BullMQ em processo separado não tinha sockets do API; relay `wsUserRelay.ts` publicava em `dndai:ws:user:{userId}`.

## Substituído por (PENAI)

- `GameMaster/transport/wsPubSub.ts` — canal `penai:ws:user`, envelope `{ userId, payload }`
- API: `startWsPubSubSubscriber()` em `penaiServer.ts`
- Worker Temporal publica via `publishWsToUser`

## Armadilhas (ainda válidas)

- Worker sem subscriber Redis = UI não recebe narração
- Ordem entrega narrativa: `storyFeed` → `gameStateUpdate` → `narrationComplete`
