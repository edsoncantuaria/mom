# PENAI melhorias 1–6 (jun/2026)

Status: active
Atualizado: 2026-06-06
Doc: PENAI.md · gaps.md · frontend-turn-pipeline.md

## Por quê
- UI BYOK-only (sem créditos confusos)
- Triggers narrativos declarativos vs lógica inline
- Coerência narrativa pós-cleanup (validator legado removido)
- F.1 autoridade única de fase no frontend

## O quê
- `narrative/triggerEngine.ts` + `data/narrativeTriggers.pt-BR.json` — hook em `applyEventProjection`
- `narration/consistencyCheck.ts` — heurística HP/grant; WS `consistencyNote` debug
- `useGameNarrationSlice` — `isLoading = apiLoading || phase !== idle`
- Redis snapshot `gz1:` — won't fix; canônico = `session_snapshots` Postgres
- `npm run typecheck:penai` + CI frontend-check

## Armadilhas
- Não reintegrar `maybeTransitionPoliticsAfterFactionTick` inline — politics via triggers
- `typecheck:penai` escopo narrow — full `tsc` ainda ~261 erros legado utils

## Comandos
- `npm run typecheck:penai`
- `npm run test --prefix backend`
