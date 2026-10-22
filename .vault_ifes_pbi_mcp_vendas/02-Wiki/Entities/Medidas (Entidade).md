---
title: "Medidas"
tags:
  - entity
  - modelo
  - dax
date: 2026-10-22
status: active
fontes:
  - "[[CLAUDE]]"
---

# Medidas (Entidade)

Tabela vazia do [[Modelo Semantico]] que serve só de **container de medidas**. Grupo `Aux`, tabela visível (só a coluna `Coluna 1` é oculta). Toda medida nova vai aqui. Criadas via [[MCP (Conceito)|MCP]] em 2026-10-19 sobre [[fato_vendas (Entidade)|fato_vendas]] e [[metas_mensais (Entidade)|metas_mensais]].

## Medidas existentes (40)

| Pasta | Medidas |
|---|---|
| `0. Aux` | `txtAtualizacao`, `Dummy` (sem `description`), `Cor Atingimento`, `Cor Atingimento Degradê` |
| `1. Vendas` | Receita, Receita Bruta, Desconto, Desconto %, Custo, Margem Bruta, Margem Bruta %, Quantidade Vendida, Pedidos, Pedidos Cancelados, Taxa de Cancelamento %, Ticket Médio, Clientes Ativos |
| `2. Meta` | Meta, Meta Comparável, Atingimento %, Gap Meta, Meta Max (criada pelo usuário, `= 1`) |
| `3. Tempo` | Receita Ano Anterior, Receita Var. Anual %, Receita Mês Anterior, Receita Var. Mensal %, Receita Acumulada Ano, Meta Acumulada Ano, Atingimento Acumulado Ano % |
| `4. HTML` | HTML KPIs / Narrativa Visão Executiva, HTML KPIs / Narrativa Desempenho Comercial |
| `5. Câmbio` | Moeda Selecionada, Cotação Dólar, Cotação Média; ocultas: Receita R$, Receita Bruta R$, Custo R$, Meta R$ |

## Câmbio R$ / U$ (2026-10-22)

`Receita`, `Receita Bruta`, `Custo` e `Meta` convertem pela cotação diária quando o parâmetro [[Moeda (Entidade)|Moeda]] = U$; todas as derivadas herdam. Medidas monetárias têm format string dinâmica (`R$` / `US$`). Detalhes em [[Moeda (Entidade)]] e [[fato_cotacao_moeda (Entidade)]].

## Cores condicionais (2026-10-22)

Para formatação condicional por **valor do campo** (fx → Estilo: Valor do campo):

| Medida | Regra |
|---|---|
| `Cor Atingimento` | `[Atingimento %]` < 100% → `#A4262C`; ≥ 100% → `#176B3A`; vazio sem atingimento |
| `Cor Atingimento Degradê` | Interpolação RGB: ≤ 50% `#A4262C` → 100% `#9C6500` → ≥ 150% `#0B4F35` |

> [!WARNING]
> Pontos 50% / 100% / 150% do degradê foram escolha do Claude para a demonstração, sem limiar de negócio confirmado (o [[DESING - Contrato Visual]] pede não inventar limiares). Ajuste as variáveis `_min`, `_meio`, `_max` se o negócio definir outros.

## Regras

- Medidas de venda filtram `fato_vendas[Status] = "Faturado"`; Receita = Σ Quantidade × PrecoUnitario × (1 − DescontoPct).
- Variações retornam BLANK sem valor atual ou base (mês futuro não vira −100%).
- Acumulados retornam BLANK após a última data com venda (meses futuros não acumulam meta).

> [!WARNING]
> **Meta tem grão vendedor × mês** e não se divide por cliente, produto, canal ou status. `Meta Comparável`, `Atingimento %`, `Gap Meta`, `Atingimento Acumulado Ano %` e os HTML ficam vazios (ou avisam) quando há filtro nessas dimensões. `Meta` crua não tem a proteção — o combo Receita × Meta do [[Relatorio PBIR]] a usa.

`Meta Comparável` e os HTML recortam meta e ano anterior até a última data com venda, para não comparar ano parcial com ano cheio.

## Medidas HTML

Strings HTML com tokens do [[DESING - Contrato Visual]], renderizadas pelo custom visual **HTML Content**.

| Medida | Conteúdo |
|---|---|
| `HTML KPIs Visão Executiva` | 4 cards em linha: Receita, Atingimento da meta, Pedidos faturados, Ticket médio; comparação vs. mesmo período do ano anterior; período com vendas no rodapé |
| `HTML Narrativa Visão Executiva` | Cabeçalho "Resumo executivo · período" + uma frase: receita, variação anual, atingimento com folga/falta |

Decisões do usuário (2026-10-19):
- Narrativa ficou só com a frase de insight; seções Contexto, Pontos de atenção e Para explorar foram removidas.
- Negativos (variação, gap, atingimento < 100%) em vermelho `#A4262C`, sempre com sinal ou palavra ("abaixo", "faltam"); positivos em negrito.

Trechos somem quando falta base; sem receita → "Sem dados para os filtros atuais".

## Convenções

- `displayFolder` prefixado por número para ordenar o painel.
- Preencher `description` — alimenta [[documentacao (Entidade)|documentacao]].
- Agregação implícita desligada (`summarizeBy: none`); toda métrica é medida explícita.
