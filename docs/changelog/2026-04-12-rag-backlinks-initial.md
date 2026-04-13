# feat: initial Obsidian-aware RAG (BM25 + wiki-link graph)

**Data:** 2026-04-12
**Commit:** (pendente)
**Branch:** main
**Arquivos alterados:** rag/__init__.py, rag/schema.sql, rag/parser.py, rag/index_vault.py, rag/query.py, rag/cli.py, requirements.txt, .gitignore

## O que foi feito

Criado sistema RAG local para o vault StartupRush que respeita os backlinks do Obsidian. Implementação da **Opção A** do plano em `~/.claude/plans/iterative-swimming-codd.md`:

- Parser de markdown (stdlib-only) extraindo frontmatter (tags/aliases), chunks por heading e wiki-links `[[Nota]]` / `[[Nota|label]]`
- Índice SQLite com FTS5 (BM25 nativo, tokenizer `unicode61 remove_diacritics 2` para PT-BR)
- Tabela `links(source, target)` materializando o grafo bidirecional; resolução por title OU alias
- Pipeline de retrieval: FTS5 MATCH → expansão 1-hop no grafo → rerank com boost de conectividade → pack por token budget
- CLI com modos: query natural, `--backlinks TITLE`, `--tags`, `--json`
- Reindex incremental via `notes.mtime`

## Por que

O vault tem 45 arquivos `.md` extensivamente interligados com wiki-links hand-curados e frontmatter estruturado. Tratar cada nota como ilha em um RAG ingênuo desperdiça o grafo de conhecimento pré-existente. O objetivo foi aproveitar 100% dos backlinks para expansão de contexto, minimizando custo de tokens e latência.

## Decisões técnicas

- **Stdlib-only**: sem PyYAML, sem markdown-it-py. Parser de frontmatter suporta apenas `tags`/`aliases` (as únicas chaves usadas no vault) — suficiente e zero deps
- **SQLite FTS5 > vector DB**: para 45 arquivos hand-curados, BM25 + grafo bate vector search em custo/latência. Opção B (embeddings locais via Ollama) fica documentada como caminho futuro
- **Chunks por heading**: granularidade natural do markdown; preserva contexto semântico do autor
- **Graph expansion 1-hop bidirecional**: forward-links E backlinks. Neighbors com overlap lexical ganham BM25 contra query; neighbors sem overlap lexical ainda recebem preamble (fallback) — evita perder links pura/topicamente relacionados
- **Ranking híbrido**: `0.7 * bm25 + 0.3 * graph_connectivity_boost`. Chunks que aparecem via FTS *e* via grafo recebem bônus adicional
- **bm25() quirk**: FTS5 só permite `bm25()` no SELECT direto da virtual table. Tentativa inicial com CTE + ROW_NUMBER falhou com `OperationalError`. Resolvido materializando top-200 scored rows e filtrando por `note_id` em Python
- **Alternativa descartada — LightRAG/GraphRAG**: gastaria 50k–150k tokens de LLM indexando um vault que já tem grafo hand-curado superior. Antieconômico

## Impacto

- **Nenhum arquivo do vault foi modificado** — sistema é puramente aditivo
- **Zero custo recorrente** (sem chamadas LLM, sem embeddings pagos)
- **Performance medida**:
  - Full index (45 arquivos, 469 chunks, 148 links): **0.09s**
  - Reindex incremental (1 arquivo): **0.04s**
  - Query end-to-end (inclui startup Python): **~6ms** para a parte de retrieval
- **Qualidade medida**:
  - 147/148 links resolvidos (1 quebrado: link para PDF, esperado)
  - Backlinks gerados casam com a view Backlinks do Obsidian (validado para "Canvas de Hipóteses" — 12 backlinks)
  - Query `"Canvas de Hipoteses"` retorna 6 hits diretos (FTS) + 3 via grafo (notas relacionadas sem match lexical direto)

## Integração Claude Code (MCP)

Adicionado em seguida: servidor MCP global em `~/.claude/tools/vault-rag/` que
expõe o retrieval para o Claude Code via stdio. Registrado no projeto via
`.mcp.json`. Reusável em outros projetos alterando apenas `VAULT_PATH`.

Tools expostas: `search_vault`, `get_backlinks`, `get_forward_links`,
`list_notes_by_tag`, `reindex_vault`, `vault_info`. Dependência adicional:
`pip install mcp` (fora do `requirements.txt` — o pacote `rag` em si continua
stdlib-only; o MCP é camada opcional de integração).

Arquivos novos: `.mcp.json`, `~/.claude/tools/vault-rag/server.py`,
`~/.claude/tools/vault-rag/rag/*` (cópia do pacote), `~/.claude/tools/vault-rag/README.md`.

## Próximos passos

- **Opção B (se necessário)**: adicionar `sqlite-vec` + embeddings locais via Ollama para queries semânticas de alto nível. Reusa 100% do schema atual
- **Watchdog**: reindex automático em file-save (atualmente é incremental no startup do MCP server ou manual via `python -m rag.index_vault`)
- **Detecção de links quebrados**: relatório de `links WHERE target_note_id IS NULL` como lint do vault
- **Registrar em outros projetos**: copiar `.mcp.json` alterando `VAULT_PATH`
