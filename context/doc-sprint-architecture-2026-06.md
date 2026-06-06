# Sprint documentação sistema (multitask)

Status: active
Atualizado: 2026-06-06
Doc: docs/architecture/README.md · ECOSSISTEMA §19 · ADR 0001

## Por quê

ECOSSISTEMA descrevia stack legado BullMQ/MySQL; runtime PENAI (Temporal/Postgres) divergia. Auditoria paralela em 6 domínios.

## O quê (bullets)

- **6 módulos** em `docs/architecture/`: WS, IA, auth, memória, motor, frontend.
- **ECOSSISTEMA:** §1.3 stack, §1.4 mapa, §19 auth, links architecture.
- **DESIGN_FRONTEND:** §7–8 atualizados para `usePenaiTurnPipeline`.
- **ADR 0001:** actionSense × motor (retifica MOM adjudicação monolítica).
- **gaps.md:** consolidado P1–P3 pós-auditoria.

## Armadilhas

- §4–9 ECOSSISTEMA ainda têm texto BullMQ — ler módulos architecture antes de implementar.
- `mom/context/ia-gemini-adjudication.md` **obsoleto** — ver ADR 0001 + `architecture/ai-gemini-penai.md`.

## Comandos / paths

- Índice: `docs/architecture/README.md`
- Manutenção: skill `dndai-documentation`
