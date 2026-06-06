# BYOK no árbitro actionSense

Status: active
Atualizado: 2026-06-06
Doc: ADR 0001 · `architecture/auth-billing-byok.md` · `ai-gemini-penai.md`

## Por quê

actionSense (árbitro LLM) usava só `GEMINI_API_KEY` da plataforma — jogador com BYOK na narração não tinha árbitro quando o servidor não tinha chave global.

## O quê (bullets)

- `resolveInferenceApiKey(userId)` no motor antes do Gemini em intents `free`/`social`.
- Adapter `gemini/actionSense.ts` usa `resolveGeminiApiKey(userApiKey)` como narração.
- Fail-closed: sem `canInfer` → `actionRejected` (não heurística permissiva).
- Crédito bundled: só `consumePenaiNarrationCredit` no turnPipeline; árbitro não debita de novo.
- actionOptions: cleanup fallback `penaiEnv`; sem chave → registry.
- Bootstrap: mensagens `no_api_key` neutras; fluxo BYOK já existia em `buildSessionWorld`.

## Armadilhas

- Gate antigo `penaiEnv.GEMINI_API_KEY &&` impedia BYOK mesmo com adapter correto.
- `resolveGeminiApiKey('')` ainda cai na chave plataforma — motor deve passar chave **resolvida** do usuário, não string vazia com intenção de “usar plataforma” fora do billing.
- Intents estruturados bypassam árbitro LLM — não exigir chave neles.
- smoke BYOK não deve chamar Gemini real no árbitro (custo/latência).

## Comandos / paths

- Testes: `node --import tsx --test src/__tests__/penaiActionSenseByok.spec.ts`
- Smoke: `npm run penai:smoke:byok --prefix backend`
- Hot path: `motor/actionSense.ts`, `adapters/gemini/actionSense.ts`
