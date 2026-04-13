---
tags:
  - startup-rush
  - metodologia
  - diagrama
  - visual
aliases:
  - Diagramas
  - Mapas Visuais
---

# DIAGRAMAS VISUAIS — STARTUP RUSH

> Coleção de diagramas para uso em apresentações, slides, materiais impressos e no Obsidian (os diagramas em **Mermaid** renderizam automaticamente na visualização).
> Cada diagrama vem em 2 formatos: **Mermaid** (para uso no Obsidian/docs) e **Descrição detalhada** (para designer produzir versão visual).

---

## 1. CICLO BUILD-MEASURE-LEARN (BML)

### Versão Mermaid

```mermaid
flowchart LR
    A[IDEIA] -->|Construir| B[PRODUTO / MVP]
    B -->|Medir| C[DADOS]
    C -->|Aprender| A
    
    style A fill:#FFE66D,stroke:#000,stroke-width:2px,color:#000
    style B fill:#FF6B6B,stroke:#000,stroke-width:2px,color:#fff
    style C fill:#4ECDC4,stroke:#000,stroke-width:2px,color:#000
```

### Descrição para designer

Círculo com 3 nós conectados em loop contínuo (sentido horário):

1. **IDEIA** (topo) — cor: amarelo vibrante. Ícone: lâmpada. Texto abaixo: "O que acreditamos ser verdade"
2. **CONSTRUIR → PRODUTO/MVP** (direita) — cor: vermelho coral. Ícone: ferramenta/martelo. Texto: "O mínimo para aprender"
3. **MEDIR → DADOS** (base) — cor: turquesa. Ícone: gráfico. Texto: "Reação real de clientes"
4. **APRENDER** (retorno ao topo) — seta grossa curva. Texto: "Validar ou pivotar"

Setas direcionais bem evidentes entre cada etapa. O loop deve sugerir movimento contínuo — pode ter uma indicação tipo "2-3x no evento" no centro.

**Uso:** Slide 5 da [[Apresentação de Abertura]], materiais impressos, Canvas.

---

## 2. AS 4 FASES DO EVENTO

### Versão Mermaid

```mermaid
flowchart LR
    F1[🔥 IGNIÇÃO<br/>Sexta à noite<br/>~5h]
    F2[🔨 CONSTRUÇÃO<br/>Sábado inteiro<br/>~14h]
    F3[📊 MEDIÇÃO<br/>Domingo manhã<br/>~5h]
    F4[🎤 APRESENTAÇÃO<br/>Domingo tarde<br/>~4h]
    
    F1 --> F2 --> F3 --> F4
    
    F1 -.-> O1[Problemas<br/>Equipes<br/>Hipóteses]
    F2 -.-> O2[MVP<br/>Saia do Prédio<br/>Ciclos BML]
    F3 -.-> O3[Análise dados<br/>Pivotar/Perseverar]
    F4 -.-> O4[Pitch<br/>Júri<br/>Premiação]
    
    style F1 fill:#FF6B35,color:#fff,stroke:#000,stroke-width:2px
    style F2 fill:#F7931E,color:#fff,stroke:#000,stroke-width:2px
    style F3 fill:#4ECDC4,color:#000,stroke:#000,stroke-width:2px
    style F4 fill:#95E1D3,color:#000,stroke:#000,stroke-width:2px
```

### Descrição para designer

Linha do tempo horizontal com 4 blocos grandes conectados por setas.

- **Bloco 1 — IGNIÇÃO** (laranja quente, ícone 🔥): "Sexta à noite" + barras mostrando subfases
- **Bloco 2 — CONSTRUÇÃO** (laranja, ícone 🔨): "Sábado inteiro" — bloco maior que os outros (é o mais longo)
- **Bloco 3 — MEDIÇÃO** (turquesa, ícone 📊): "Domingo manhã"
- **Bloco 4 — APRESENTAÇÃO** (verde-água, ícone 🎤): "Domingo tarde"

Abaixo de cada bloco, 3 ícones/pictogramas mostrando as atividades principais. Acima, o tempo total de cada fase.

**Uso:** Slide 7 da Apresentação de Abertura, Guia do Participante, materiais de divulgação.

---

## 3. PIRÂMIDE DE EARLY ADOPTERS

### Versão Mermaid

```mermaid
flowchart TB
    subgraph topo[" "]
        EA["🎯 EARLY ADOPTERS<br/>~2.5% do mercado<br/>Aceitam soluções 80% prontas<br/>DÃO FEEDBACK ÚTIL PARA MVP"]
    end
    subgraph meio[" "]
        EM["⚡ EARLY MAJORITY<br/>~13.5% — pragmáticos<br/>Querem produto funcional<br/>Esperam prova social"]
    end
    subgraph base[" "]
        LM["🐢 LATE MAJORITY / LAGGARDS<br/>~84% — céticos<br/>Só adotam quando é padrão<br/>FEEDBACK INÚTIL PARA MVP"]
    end
    
    EA --> EM
    EM --> LM
    
    style EA fill:#06D6A0,color:#000,stroke:#000,stroke-width:3px
    style EM fill:#FFD166,color:#000,stroke:#000,stroke-width:2px
    style LM fill:#EF476F,color:#fff,stroke:#000,stroke-width:2px
```

### Descrição para designer

Pirâmide invertida (triângulo com a ponta para baixo) dividida em 3 faixas horizontais, de cima para baixo:

1. **Topo (mais estreito, verde/turquesa):** "EARLY ADOPTERS — ~2,5%" — adjetivos: "curiosos, tolerantes, engajados". Texto: "São eles que vocês procuram no 'Saia do Prédio'"
2. **Meio (amarelo):** "EARLY MAJORITY — ~13,5%" — adjetivos: "pragmáticos, esperam prova". Texto: "Vão entrar depois"
3. **Base (vermelho, mais largo):** "LATE MAJORITY + LAGGARDS — ~84%" — "céticos, conservadores". Texto: "Não servem para validar MVP"

Ao lado da pirâmide, lista em bullet points:
- ✅ Já tentou resolver o problema por conta própria
- ✅ Usa gambiarras/workarounds
- ✅ Fica animado com solução tosca
- ✅ Deixa contato, quer ser avisado

**Uso:** Briefing do "Saia do Prédio" pelo facilitador, slides de treinamento de facilitadores.

---

## 4. FUNIL DE VALIDAÇÃO (DO PROBLEMA AO PAGAMENTO)

### Versão Mermaid

```mermaid
flowchart TB
    A[100 pessoas abordadas] --> B[30 aceitam conversar]
    B --> C[15 confirmam ter o problema]
    C --> D[8 gostam da solução]
    D --> E[3 dizem que pagariam]
    E --> F[1 paga de verdade]
    
    style A fill:#E0F7FA,stroke:#000,stroke-width:2px
    style B fill:#B2EBF2,stroke:#000,stroke-width:2px
    style C fill:#80DEEA,stroke:#000,stroke-width:2px
    style D fill:#4DD0E1,stroke:#000,stroke-width:2px
    style E fill:#26C6DA,stroke:#000,stroke-width:2px
    style F fill:#00ACC1,color:#fff,stroke:#000,stroke-width:3px
```

### Descrição para designer

Funil clássico com 6 níveis descendentes, cada um mais estreito. Cores em gradiente do azul claro ao azul escuro.

**Mensagem-chave (texto ao lado do funil):** "Só o último nível é dado real. Os outros são indicadores parciais. Mire sempre no compromisso mais forte que conseguir em 54h — idealmente, um pagamento (pré-venda)."

**Uso:** Workshop "Métricas que Importam" (Fase 3), guia de interpretação de dados para equipes.

---

## 5. TIPOS DE PIVÔ (MATRIZ)

### Versão Mermaid

```mermaid
flowchart TB
    subgraph foco[PIVÔS DE FOCO]
        P1[Zoom-in:<br/>1 feature vira tudo]
        P2[Zoom-out:<br/>produto maior que pensado]
    end
    
    subgraph alvo[PIVÔS DE ALVO]
        P3[Segmento de Cliente:<br/>público errado]
        P4[Necessidade:<br/>dor errada]
    end
    
    subgraph entrega[PIVÔS DE ENTREGA]
        P5[Solução:<br/>abordagem errada]
        P6[Canal:<br/>forma de chegar errada]
        P7[Tecnologia:<br/>ferramenta errada]
    end
    
    subgraph modelo[PIVÔS DE MODELO]
        P8[Captura de Valor:<br/>monetização errada]
        P9[Motor de Crescimento:<br/>como cresce errado]
    end
    
    style foco fill:#FFE66D,stroke:#000
    style alvo fill:#FF6B6B,stroke:#000
    style entrega fill:#4ECDC4,stroke:#000
    style modelo fill:#95E1D3,stroke:#000
```

### Descrição para designer

Grade 2×2 com 4 categorias, cada categoria contém 2-3 cards:

| | |
|---|---|
| 🎯 **FOCO** (amarelo)<br/>Zoom-in / Zoom-out | 👥 **ALVO** (vermelho)<br/>Segmento / Necessidade |
| 🚚 **ENTREGA** (turquesa)<br/>Solução / Canal / Tecnologia | 💰 **MODELO** (verde)<br/>Captura de Valor / Motor |

Cada card com ícone + nome + 1 frase descritiva. Fácil de imprimir em A4 como referência rápida para facilitadores.

**Uso:** Parede da sala durante Fase 3 ("Reunião Pivotar ou Perseverar"), Guia do Facilitador.

---

## 6. OS 3 MOTORES DE CRESCIMENTO

### Versão Mermaid

```mermaid
flowchart LR
    subgraph S[STICKY]
        S1[Alta Retenção]
        S2[Cliente volta]
        S3[Churn baixo]
    end
    
    subgraph V[VIRAL]
        V1[Cliente traz cliente]
        V2[Coef. viral > 1]
        V3[Produto compartilha]
    end
    
    subgraph P[PAID]
        P1[Receita > Custo]
        P2[LTV ≥ 3x CAC]
        P3[Marketing pago]
    end
    
    style S fill:#A8DADC,stroke:#000,stroke-width:2px
    style V fill:#F1FAEE,stroke:#000,stroke-width:2px
    style P fill:#E63946,color:#fff,stroke:#000,stroke-width:2px
```

### Descrição para designer

3 colunas paralelas, cada uma com um motor. Cada coluna tem:

1. **Título grande** com cor distintiva
2. **Ícone central** (Sticky = ímã, Viral = raio, Paid = cifrão)
3. **3 bullet points** com características
4. **Pergunta-chave** na base: "Seu cliente volta?" / "Seu cliente convida?" / "Sua receita paga o marketing?"

**Uso:** Workshop de motores de crescimento (Fase 1 ou Fase 3), [[Canvas de Hipóteses]].

---

## 7. FLUXO "SAIA DO PRÉDIO"

### Versão Mermaid

```mermaid
flowchart TB
    Start([Equipe tem Canvas de Hipóteses]) --> Plan[Definir quem abordar<br/>ver Early Adopters]
    Plan --> Go[Sair fisicamente/digitalmente]
    Go --> Talk[Abordar 5-10 pessoas<br/>usar Roteiro de Entrevista]
    Talk --> Record[Registrar TUDO<br/>no Diário de Aprendizado]
    Record --> Check{Dados suficientes?}
    Check -->|Não| Plan
    Check -->|Sim| Analyze[Checkpoint BML<br/>analisar padrões]
    Analyze --> Decision{Hipótese<br/>confirmada?}
    Decision -->|Sim| Persevere[PERSEVERAR<br/>refinar e aprofundar]
    Decision -->|Parcial| Iterate[ITERAR MVP<br/>testar de novo]
    Decision -->|Não| Pivot[PIVOTAR<br/>usar Five Whys]
    
    style Start fill:#FFE66D
    style Persevere fill:#06D6A0,color:#000
    style Iterate fill:#FFD166,color:#000
    style Pivot fill:#EF476F,color:#fff
```

### Descrição para designer

Fluxograma vertical com decision points (losangos). Estilo limpo, apenas retângulos e setas. Cores semafóricas nas decisões finais: verde (perseverar), amarelo (iterar), vermelho (pivotar).

**Uso:** Briefing do facilitador antes da Fase 2, material de parede da sala.

---

## NOTAS DE USO

1. **No Obsidian:** Os blocos Mermaid renderizam automaticamente no modo Preview. Basta abrir esta nota.
2. **Em slides:** Os diagramas Mermaid podem ser exportados como PNG/SVG de ferramentas online (mermaid.live, diagrams.net).
3. **Para designer:** As descrições textuais abaixo de cada diagrama são o briefing — incluir quando contratar designer para criar versões finais com a identidade visual do evento.
4. **Impressos A3:** Os diagramas 1, 2, 5 e 6 funcionam bem como pôsteres de parede para a sala do evento.

---

*Uma imagem vale mais que mil parágrafos. Esses diagramas devem aparecer em tudo: slides, templates, paredes da sala, Instagram, vídeo introdutório.*
