# refactor: replace MVP concept with SLC across methodology

**Data:** 2026-04-13
**Commit:** (ver abaixo)
**Branch:** master
**Arquivos alterados:** 31 arquivos modificados + 2 novos (Canvas SLC.md em StartupRush/Templates/ e Metodologia_StartupRush/04_Templates/)

## O que foi feito

Substituição sistemática do conceito de MVP (Produto Mínimo Viável) por SLC (Simples, Adorável, Completo) em toda a metodologia ativa dos vaults StartupRush/ e Metodologia_StartupRush/. Os "5 tipos de MVP" foram renomeados para "5 tipos de protótipo/experimento", mantendo as técnicas intactas e removendo apenas o prefixo MVP de cada uma. Criado novo Canvas SLC.md com checklist S/L/C. Canvas MVP.md convertido em redirect para Canvas SLC.md (arquivo preservado, não deletado).

## Por que

SLC (Simple, Lovable, Complete — cunhado por Jason Cohen / WP Engine) é uma evolução conceitual do MVP que corrige a conotação problemática de "viável" como sinônimo de produto incompleto ou pela metade. O SLC enfatiza que o que se constrói deve ser simples no escopo, mas adorável na execução e completo no que promete. A mudança evita que participantes do evento construam produtos que são "viáveis" mas não encantam — o que é especialmente crítico num evento de 54h onde a primeira impressão com usuários define tudo.

## Decisões técnicas

- **"5 tipos de MVP" → "5 tipos de protótipo/experimento"** (Opção C escolhida pelo usuário): nome neutro que não carrega conotação de produto; mantém as técnicas concretas (landing page, concierge, smoke test, etc.) sem renomear cada uma individualmente.
- **Referências bibliográficas do Eric Ries mantidas intactas**: as citações ao livro The Lean Startup e ao conceito original de MVP foram preservadas nas notas de Referências/ e onde aparecem como contexto histórico, não como diretriz operacional.
- **Canvas MVP.md preservado como redirect**: arquivo mantido (não deletado) para preservar histórico e backlinks existentes; conteúdo substitui o canvas pela nota de que o conceito foi migrado para Canvas SLC.md.
- **LeanStartup/ e Reuniões/ não alterados**: material-fonte externo e atas de reunião ficaram fora do escopo da migração.

## Impacto

- Toda a terminologia operacional da metodologia agora usa SLC em vez de MVP
- Participantes e facilitadores encontrarão o framework SLC nos templates, guias e cronograma
- O grafo de wiki-links foi atualizado: [[Canvas SLC]] substitui [[Canvas MVP]] nas notas ativas; [[Canvas MVP]] permanece como nó redirect
- Reindex do vault RAG necessário após esta mudança para refletir novos links e títulos

## Próximos passos

- Rodar `reindex_vault` via MCP para atualizar o índice FTS5 com os novos conteúdos
- Verificar se há backlinks para [[Canvas MVP]] que precisam ser atualizados para [[Canvas SLC]]
- Considerar adicionar uma nota de glossário SLC em StartupRush/Referências/ explicando a origem do conceito (Jason Cohen, 2014)
