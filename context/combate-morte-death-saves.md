# Death saves + morte permanente PENAI

Status: active
Atualizado: 2026-06-06
Doc: `architecture/motor-combat-dm.md` · `DESIGN_FRONTEND.md` §7 · `frontend-turn-pipeline.md`

## Por quê

HP clampava em 0 sem inconsciência, death saves nem fim de sessão — campanha não tinha derrota jogável nem opções pós-morte no cofre.

## O quê (bullets)

- Regras SRD em `backend/src/rules/deathSaves.ts` (9 testes unitários).
- `HeroSessionStats` + `GameSession.sessionStatus` / `vaultTemplateId` (migration `1748920000000-SessionDeathAndVault`).
- `heroVitalsService` — sync pós-HP, `buildDeathSaveRollRequest`, `markHeroPermanentlyDead`, WS `heroPermanentlyDead`.
- Motor: gate `validateAndApply` (`HERO_DEAD`), death save roll em `rollResolution`, herói 0 HP permanece na iniciativa (`phaseGate`).
- Frontend: `HeroDeathSavesBanner`, `HeroDeathScreen`, `LOCKED_UNCONSCIOUS`, `PenaiMechanicalSync` espelha `deathSaves`/`heroStatus`.
- APIs: `POST /api/v2/sessions/:id/export-hero-to-vault`, `POST /api/v2/characters/:id/reset-progress`.

## Armadilhas

- `enterUnconscious` zera death saves — testes de dano em 0 HP não devem chamar `enterUnconscious` de novo.
- `mapGateFromPhase` e `usePenaiMechanicalSync` competem no `InputGate` — sinais vitals em `turnPipelineStore.setVitalsInputSignals`.
- `createAndLoadPenaiSession` exige `heroRef.id` UUID (`heroWorldEntityId`) para clonar do cofre.
- Morte permanente: `submitRollResult` retorna cedo; não enfileirar narração.

## Comandos / paths

- Testes: `node --import tsx --test src/__tests__/deathSaves.spec.ts` (backend)
- Migration: `npm run penai:migration:run --prefix backend`
- Módulos: `heroVitalsService.ts`, `HeroDeathScreen.tsx`, `usePenaiTurnPipeline.ts` (`heroPermanentlyDead`)
