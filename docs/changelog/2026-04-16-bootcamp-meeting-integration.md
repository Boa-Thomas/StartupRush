# docs: integrate 2026-04-15 bootcamp meeting decisions into vault

**Data:** 2026-04-16
**Commit:** (ver hash abaixo)
**Branch:** chore/obsidian-workspace-settings
**Arquivos alterados:** 18 arquivos (9 criados, 9 modificados)

## O que foi feito

Processamento completo da reunião de 15/04/2026 ("Bootcamp Simples Adorável Completo") no vault Obsidian. A transcrição e o summary brutos (`.txt` na raiz) foram curados e materializados em notas estruturadas.

Notas criadas:
- `StartupRush/Reuniões/2026-04-15 Bootcamp Simples Adorável Completo.md` — ata curada com decisões, participantes e action items
- `StartupRush/Reuniões/2026-04-15 Bootcamp Simples Adorável Completo - Transcript.md` — transcrição estruturada da reunião
- `StartupRush/Metodologia/Tipos de Protótipo.md` — nota dedicada aos 3 tipos de protótipo aprovados (digital, físico, roleplay)
- `StartupRush/Pré-Evento/Identidade e Marca.md` — marca "Startup Go", posicionamento, paleta visual
- `StartupRush/Pré-Evento/Posicionamento e Comunicação.md` — canais, público-alvo, mensagem central
- `StartupRush/Pré-Evento/Equipe e Parcerias.md` — divisão de papéis, parceiros estratégicos, EuroValley
- `StartupRush/Pré-Evento/Datas e Cronograma de Lançamento.md` — data confirmada 19/09/2026, milestones
- `StartupRush/Pré-Evento/Action Items 2026-04-15.md` — todos os action items por responsável com prazo
- `StartupRush/Referências/Referências.md` — nota de referências externas do vault

Notas modificadas:
- `Metodologia/Metodologia StartupRush.md` — mentores fixos+rotativos, organizadores facilitam 1ª edição, lista dos 3 tipos de protótipo
- `Metodologia/Cronograma 54h.md` — medição/pivot movidos para sábado à noite, app digital, seção de tipos de protótipo
- `Metodologia/Plano de Contingência.md` — decisão evento fechado vs aberto, validação digital como padrão
- `Pré-Evento/Checklist Pré-Evento (Organização).md` — Startup Go, app digital, checklist de patrocínio
- `Pré-Evento/Treinamento de Facilitadores.md` — callout para próxima reunião, leituras obrigatórias, Bloco 5.5 Simulação Mental
- `Pós-Evento/Plano de Continuidade.md` — trilha premiados, parceria EuroValley, cadência de follow-ups
- `Home.md` — novas notas indexadas + bloco de decisões-chave atualizado
- `.obsidian/` — workspace, graph e app.json atualizados pelo Obsidian

## Por que

A reunião de 15/04 produziu decisões estruturais sobre a 1ª edição do Startup Rush: nome definitivo da marca, data do evento, modelo de mentoria, tipos de protótipo e parceria com EuroValley. Todas essas decisões precisavam estar refletidas nas notas canônicas do vault para manter coerência e alimentar o grafo de conhecimento.

## Decisões técnicas

- **SLC em vez de MVP**: mantida a terminologia já migrada em 87f19a2; a reunião reforçou o conceito de "Simples Adorável Completo"
- **Mentoria híbrida (fixos + rotativos)**: cada startup recebe 1 mentor fixo + acesso a pool de rotativos por bloco temático
- **Simulação Mental como Bloco 5.5**: inserido entre Bloco 5 (pitch) e Bloco 6 (apresentação final) no Cronograma 54h — não é um bloco oficial numerado para não quebrar a sequência atual
- **App digital como padrão**: substituição de planilhas físicas por app; fallback em papel mantido no Plano de Contingência
- **Trilha EuroValley**: premiados top-3 entram em pipeline da EuroValley — decisão registrada em Plano de Continuidade
- **Arquivos .txt mantidos na raiz**: transcrição e summary brutos preservados como fonte (não deletados); curadoria fica nas notas de Reuniões/

## Impacto

- Todas as notas de Metodologia e Pré-Evento tocadas
- Home.md atualizado — MOC continua como entry point principal
- Nenhum wiki-link existente quebrado (verificado via backlinks antes de renomear)
- Nenhum breaking change no schema de frontmatter

## Próximos passos

Action items pendentes por responsável (ver `Pré-Evento/Action Items 2026-04-15.md`):
- **Thomas**: fechar proposta EuroValley, definir estrutura de patrocínio
- **Equipe**: agendar próxima reunião de facilitadores (callout em Treinamento de Facilitadores)
- **Design**: validar paleta e identidade visual da marca Startup Go
- **Todos**: confirmar disponibilidade para 19/09/2026
