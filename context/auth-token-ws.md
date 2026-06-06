# Auth — token único `token` no localStorage

Status: active  
Atualizado: 2026-05-29  
Doc: ECOSSISTEMA § auth (HTTP + WS)

## Por quê

HTTP 401 "Token não fornecido" com WS conectado; Settings usava `authToken` inexistente.

## O quê

- Chave canônica: `localStorage.token` via `src/lib/authToken.ts`
- HTTP: `apiClient` envia `Authorization: Bearer`
- WS: token na query `?token=` em `webSocketService.ts`
- `syncPendingRoll` no `connectionOpen` — importar `sendMessage` em `useGameWebSocket.ts`

## Armadilhas

- Sessão expirada: relogin; toast "Sessão expirada"
- Settings admin flush cache: usar `apiClient('/cache/flush')`, não `/api/cache/flush` com authToken errado
