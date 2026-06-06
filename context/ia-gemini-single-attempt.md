# Gemini single-attempt — anti-empilhamento de tokens

Status: active
Atualizado: 2026-06-06
Doc: `docs/architecture/ai-gemini-penai.md` · `penaiEnv.ts`

## Por quê

Retry em camadas (Gemini 12× + turnPipeline 3× + Temporal 3×) queimava quota em 429 e reexecutava turnos obsoletos.

## O quê

- `generateGeminiStructuredJson` — **uma** chamada HTTP, sem loop de retry
- `turnPipeline` — uma tentativa de narração; falhou → `abortPenaiTurnNarration` + rollback
- Temporal `narrationWorkflow` → `maximumAttempts: 1`
- `isStaleNarrationTurn` — skip LLM se `actionSequence` superseded ou já narrado
- Opening dedup: `sessionHasPlayableNarration` + lock em `wsHandlers` (replay, não novo `actionSequence`)
- `reconcileStaleNarrationLock` — rollback após 5 min sem narração (não auto-complete silencioso)
- `PENAI_ACTION_OPTIONS_LLM=false` — opções do registry, sem 2ª chamada Gemini por turno

## Armadilhas

- 429/503 falham o turno de imediato (`narrationFailed` + rollback cursor) — cliente pode reenviar ação manualmente
- Narração roda no Temporal: fechar aba não cancela; reconnect usa `syncPendingRoll` / `storyFeedReplay`
- Para reativar actionOptions LLM: `PENAI_ACTION_OPTIONS_LLM=true`

## Comandos / paths

- `backend/src/GameMaster/ai/geminiStructured.ts`
- `backend/src/GameMaster/engine/turnPipeline.ts`
- `backend/src/temporal/workflows/narrationWorkflow.ts`
