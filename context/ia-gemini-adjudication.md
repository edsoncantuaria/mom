# Gemini adjudica; motor autoritativo

Status: superseded  
Atualizado: 2026-06-06  
Doc: ADR 0001 · `architecture/ai-gemini-penai.md`

## Por quê (histórico)

Tentativa de schema monolítico `adjudication` no JSON Gemini — paths `ai-gemini/adjudication/*` **nunca materializados** no PENAI.

## Substituído por

- **actionSense** (plausibilidade LLM) + **motor SRD** (rolls/bloqueios) — ADR `0001-action-sense-vs-motor.md`
- Código: `GameMaster/adapters/gemini/actionSense.ts`, `motor/validateAndApply.ts`
- Doc: `docs/architecture/ai-gemini-penai.md`

## Armadilhas (ainda válidas)

- Abertura exige chave resolvível (`canInfer`) — não bypass
- `AI_ENGINE=oss` local diverge do produto Gemini
