# Workflow MOM — recall e distill

Status: active
Atualizado: 2026-05-28
Doc: MOM_DESENVOLVIMENTO · rule `dndai-mom-context.mdc`

## Por quê

Sessões longas no Cursor perdem contexto no chat. O MOM versiona o *por quê* tático (decisões, armadilhas, dev stack) separado da memória de partida (Qdrant/SQL).

## O quê (bullets)

- **Recall (início):** `mom/context/INDEX.md` → arquivos active por tag → trecho de docs vivos.
- **Distill (fim):** nova entrada `mom/context/<area>-<slug>.md` + linha no INDEX.
- **Prompts copiáveis:** `.cursor/prompts/mom-maintain-context.md` (RECALL, DISTILL, always-on).
- **Rule `alwaysApply`:** agentes devem recall/distill sem o usuário pedir.
- **Vault SQLite** (`mom/.vault/`): opcional local; markdown em `context/` é a fonte compartilhada no git.

## Armadilhas

- Não gravar `.env`, tokens ou dumps enormes de log.
- Não duplicar parágrafos inteiros de `ECOSSISTEMA.md`.
- Não usar MCP MOM no runtime do jogo (processPlayerTurn, worker para jogador).

## Comandos / paths

- Índice: `mom/context/INDEX.md`
- Prompts: `.cursor/prompts/mom-maintain-context.md`
- Skill: `.cursor/skills/dndai-mom-context/SKILL.md`
