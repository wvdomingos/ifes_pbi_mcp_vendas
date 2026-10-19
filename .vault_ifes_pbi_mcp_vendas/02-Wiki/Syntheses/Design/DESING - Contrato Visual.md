---
title: "DESING - Contrato Visual do Dashboard"
tags:
  - synthesis
  - design
  - acessibilidade
  - power-bi
  - ifes
date: 2026-10-19
status: active
fontes:
  - "[[DESING]]"
---

# DESING - Contrato Visual do Dashboard

Síntese de `DESING.md` (grafia com typo, preservada; `status: proposta`). Guia para construir páginas do relatório [[Power BI (Entidade)|Power BI]] do evento **IFES — Comércio Exterior**, tomando como referência `assets/background_ifes_comercio_exterior_16x9_v1.png`. Paleta detalhada em [[Paleta - Dashboard Power BI]].

> [!WARNING]
> As cores são **aproximações visuais** amostradas da imagem, não especificação institucional oficial. O contrato orienta; não comprova acessibilidade — contraste vale só para os pares listados.

## Atmosfera

- Fundo **claro**, identidade predominantemente **verde**; amarelo só como destaque pequeno.
- Transmitir clareza, dinamismo e rigor analítico (conexões globais, atividade portuária).
- Não adicionar logotipo, brasão nem valores/indicadores sem fonte confirmada.
- Hierarquia de leitura: **insight → contexto → ação**. Ação = possibilidade de exploração, não recomendação inventada.

## Tipografia (Segoe UI; fallback Arial)

| Elemento | Tamanho | Peso e cor |
|---|---:|---|
| Título da página | 26 pt | Semibold, `#0B4F35` |
| Mensagem principal / insight | 18 pt | Semibold, `#0B4F35` |
| Valor de KPI | 28 pt | Semibold, `#0B4F35` |
| Título de visual | 15 pt | Semibold, `#0B4F35` |
| Texto, filtro e rótulo | 12 pt | Regular, `#475D52` ou `#0B4F35` |
| Fonte e contexto secundário | 10 pt | Regular, `#475D52` |

## Canvas e layout

- 16:9, **1280 × 720 px**. Imagem como *Canvas background*, transparência 0%, sem esticar.
- Margem 32 px; 12 colunas de ~90 px com intervalo 12 px; espaçamento vertical 16 px; padding de card 16 px.
- Cabeçalho até 80 px; faixa de KPIs de 112 px; área analítica `y ≈ 216–632`; rodapé até `y = 688`.
- Visuais sobre superfícies **brancas opacas**; imagem é decorativa. Se a leitura sofrer, trocar a imagem por `#F2FAF1`.

## Componentes

- **Card KPI**: fundo `#FFFFFF`, borda `#D3E5D5` 1 px, cantos 4 px, sem sombra forte. Rótulo → valor (+ unidade). Comparação só com medida e base disponíveis. 3–4 cards por linha.
- **Filtros/botões**: altura mínima 40 px, rótulo explícito, estado selecionado por texto/marcação. Primário `#176B3A` com texto branco; secundário branco com contorno `#176B3A`; foco contorno `#167D3F` 2 px.
- **Tabelas**: cabeçalho branco ou `#F2FAF1`, texto `#0B4F35` semibold; números à direita.
- **Gráficos**: barras comparam categorias (eixo em zero), linhas mostram evolução; sem 3D. Ordem de séries `#176B3A`, `#456D95`, `#725A91`, `#956132`, `#475D52`, mesma cor por categoria entre páginas.
- **Estados**: Positivo `#176B3A`, Atenção `#9C6500`, Crítico `#A4262C`, Neutro `#475D52`, sempre com texto/ícone. Sem limiar aprovado → neutro.

## Guardrails para IA

- Inspecionar a imagem de referência antes de compor; preservar o arquivo original.
- Identificar perguntas, fontes, campos, unidades e filtros antes de criar visuais.
- Não criar números, metas, interpretações, brasão ou logotipo fictícios.
- Cor nunca é o único canal; validar no Desktop e em projeção, com e sem dados.

## Relação com o relatório atual

[[Relatorio PBIR]] já usa 1280×720 e o fundo registrado. Tema custom aplicado com a paleta (fonte `assets/tema_ifes_comercio_exterior.json`). Por decisão do usuário, as medidas HTML marcam negativos em vermelho `#A4262C` (com sinal/palavra) e positivos em negrito.

Referências: WCAG 1.4.3 (texto), 1.4.11 (não textual), 1.4.1 (uso de cor).
