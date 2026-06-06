# MOM — Memory Oriented Machine (dev)

Memória **para agentes de código** e sessões longas de Cursor — **não** é runtime da partida.

| Runtime do jogo | MOM dev |
|-----------------|---------|
| Qdrant + SessionFact + Redis | `mom/context/*.md` (+ vault SQLite local opcional) |

Documentação: **`docs/MOM_DESENVOLVIMENTO.md`**

## Estrutura

```
mom/
├── README.md           ← este arquivo
├── context/            ← contexto versionado no git (distill markdown)
│   ├── INDEX.md        ← índice — ler primeiro
│   └── *.md            ← entradas active/superseded
└── .vault/             ← SQLite MOM CLI (local, gitignored)
```

## Workflow agente

1. **Recall:** `INDEX.md` → arquivos relevantes → docs vivos
2. **Trabalho:** código + docs canônicos
3. **Distill:** nova/atualiza entrada em `context/` + INDEX

Rule: `.cursor/rules/dndai-mom-context.mdc`  
Prompts: `.cursor/prompts/mom-maintain-context.md`  
Skill: `dndai-mom-context`

## MOM CLI (opcional)

Vault local em `mom/.vault/` — não commitar. Distill **sempre** também em `mom/context/*.md` para o time.

## Sync entre PCs

```bash
make sair-pc                        # agente gera commit + push
make sair-pc MSG="distill: combate"  # mensagem manual
make chegar-pc
make contexto-status
```

Ordem do agente (`scripts/context-sync-commit-msg.mjs`): **Cursor Agent** (se logado) → **Gemini** (`GEMINI_API_KEY`) → heurística local.

**Handshake:** cada `make sair-pc` grava palavra em `mom/context/sync-handshake.md`. No outro PC, `make chegar-pc` imprime a palavra — confirme com o agente.
