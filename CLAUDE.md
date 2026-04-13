# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Natureza do repositório

Este **não é um repositório de código**. É um **vault Obsidian** em português com a metodologia de um evento imersivo de 54h ("Startup Rush") baseado no Lean Startup. Conteúdo é tudo — notas `.md` com frontmatter (`tags`, `aliases`) e wiki-links `[[Nota]]` / `[[Nota|label]]` hand-curados.

Ao editar notas, **preserve wiki-links e aliases**. Eles alimentam o grafo de conhecimento e a view de Backlinks do Obsidian. Links quebrados degradam a navegação e o retrieval.

## Estrutura de alto nível

Dois vaults paralelos coexistem — não são duplicatas, têm propósitos distintos:

- **`StartupRush/`** — Vault ativo do Obsidian. Entry point: `StartupRush/Home.md` (MOC). Organizado em `Metodologia/`, `Templates/`, `Avaliação/`, `Pré-Evento/`, `Pós-Evento/`, `Referências/`, `Reuniões/`. Esta é a fonte canônica — edite aqui.
- **`Metodologia_StartupRush/`** — Reorganização derivada em estrutura numerada (`01_Metodologia`, `02_Cronograma`, …). Consultar como referência cruzada.
- **`LeanStartup/`** — Material-fonte (livro de Eric Ries em PDF, briefings, mind maps). Somente leitura — é referência externa.
- **`docs/changelog/`** — Registro de decisões por commit (regra global do usuário em `~/.claude/rules/commit-docs.md`). **Antes de implementar qualquer mudança estrutural, faça grep aqui** para entender decisões passadas.

Arquivos `.txt` na raiz (`Avaliação Marcas e Domínios *.txt`, `Talk Liderança SW *.txt`) são transcrições/summaries brutos de reuniões — as versões curadas vivem em `StartupRush/Reuniões/`.

## Sistema RAG (vault-rag MCP)

O vault tem um sistema de retrieval Obsidian-aware: **SQLite FTS5 (BM25) + expansão 1-hop pelo grafo de wiki-links**. O pacote Python **não vive neste repo** — é uma cópia global em `~/.claude/tools/vault-rag/`, exposta via MCP server. As ferramentas chegam ao Claude Code como `mcp__vault-rag__*`:

- `search_vault` — query natural (FTS5 + rerank por conectividade de grafo)
- `get_backlinks` / `get_forward_links` — grafo bidirecional por título ou alias
- `list_notes_by_tag` — filtro por tag do frontmatter
- `reindex_vault` — reindex incremental (usa `notes.mtime`)
- `vault_info` / `vault_status` — health do índice

**Use essas ferramentas ao invés de Grep em massa** quando a pergunta for sobre conteúdo, relações entre notas, ou backlinks. Grep só para buscas literais (strings exatas, nomes de arquivo).

Config: `.vaultrag.json` aponta `vault_path: .` e `db_path: rag.db`. O arquivo `rag.db` (SQLite) é gerado e está no `.gitignore`. Reindex é incremental; só rode full reindex se o schema mudar.

Detalhes de design, decisões e trade-offs (inclusive o quirk do `bm25()` em CTEs e o porquê de **não** usar LightRAG/GraphRAG): `docs/changelog/2026-04-12-rag-backlinks-initial.md`.

## Convenções do conteúdo

- **Idioma**: conteúdo das notas em pt-BR. Termos técnicos do Lean Startup em inglês quando canônicos (BML, MVP, pivot, cohort analysis).
- **Frontmatter**: as únicas chaves usadas no vault são `tags` e `aliases`. O parser do RAG só entende essas duas — adicionar outras não quebra nada, mas não serão indexadas.
- **Wiki-links**: sempre `[[Título Exato da Nota]]` ou `[[Título|texto visível]]`. Links que apontam para PDF (ex.: `![[The Lean Startup - Erick Ries.pdf]]`) são intencionalmente não-resolvíveis pelo RAG.
- **Nomes de arquivo**: com espaços e acentos. Ao referenciar caminhos no shell, sempre entre aspas duplas.

## Workflow de mudanças

1. **Antes de editar conteúdo de metodologia**: leia `StartupRush/Home.md` (MOC) para entender a topologia e `docs/changelog/` para contexto histórico.
2. **Ao adicionar/renomear uma nota**: atualize os wiki-links que apontam para ela e, se for um nó importante, referencie-a em `Home.md`. Depois, rode `reindex_vault` via MCP.
3. **Commits**: Conventional Commits em inglês (`feat:`, `fix:`, `docs:`, `refactor:`). Para mudanças não-triviais, crie/atualize um doc em `docs/changelog/YYYY-MM-DD-descricao-curta.md` seguindo o template em `~/.claude/rules/commit-docs.md`.
4. **Código RAG**: se precisar alterar o pacote `rag`, ele está em `~/.claude/tools/vault-rag/` — **não** neste repo. Mudanças lá afetam qualquer projeto que use o MCP server.

## Commit de sessão (obrigatório)

**Ao final de cada sessão que produziu mudanças**, invoque um agente Sonnet para fazer o commit. Isso garante histórico granular e rollback confiável.

```
Agent({
  subagent_type: "fullstack-developer",
  model: "sonnet",
  description: "Session commit",
  prompt: "Faça um commit git com todas as mudanças desta sessão no repositório C:/Users/conta/Desktop/StartupRush. Use `git status` e `git diff` para ver o que mudou. Escreva a mensagem de commit em inglês com Conventional Commits (feat/fix/docs/refactor). O corpo deve detalhar: (1) quais arquivos foram alterados, (2) o que mudou em cada um, (3) motivação. Em seguida, crie ou atualize um doc em docs/changelog/YYYY-MM-DD-descricao-curta.md conforme o template em ~/.claude/rules/commit-docs.md."
})
```

**Quando disparar**: quando o usuário sinalizar fim de sessão ("pronto", "pode fechar", "commit isso", "salva") ou quando você identificar que um conjunto coeso de mudanças foi concluído.

**O agente deve**:
- Rodar `git status` e `git diff` antes de qualquer coisa
- Escrever mensagem de commit detalhada no body (não só o subject)
- Criar/atualizar `docs/changelog/` para mudanças não-triviais
- Fazer um commit por unidade lógica — se a sessão tocou domínios distintos, separar em commits diferentes

## O que NÃO fazer

- Não modifique arquivos em `LeanStartup/` — é material-fonte externo.
- Não duplique conteúdo entre `StartupRush/` e `Metodologia_StartupRush/` sem checar o propósito — a segunda é uma reorganização, não um espelho.
- Não commite `rag.db*` nem `__pycache__` (já no `.gitignore`).
- Não quebre wiki-links existentes sem atualizar todos os callers — use `get_backlinks` antes de renomear.
