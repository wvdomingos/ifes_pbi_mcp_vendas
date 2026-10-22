---
title: "Fonte de Dados (Excel)"
tags:
  - synthesis
  - dados
  - power-query
date: 2026-10-22
status: active
fontes:
  - "[[CLAUDE]]"
---

# Fonte de Dados (Excel)

Síntese de `CLAUDE.md`: origem dos dados do [[Modelo Semantico]].

## Arquivo

`dados/Base de Dados.xlsx`, 6 planilhas, cada uma vira uma tabela do modelo:

| Planilha | Tabela | Linhas |
|---|---|---|
| `fato_vendas` | [[fato_vendas (Entidade)\|fato_vendas]] | 4189 |
| `metas_mensais` | [[metas_mensais (Entidade)\|metas_mensais]] | 288 |
| `dim_clientes` | dim_clientes | 150 (Sudeste 96, Nordeste 24, Sul 12, Centro-Oeste 10, Norte 8) |
| `dim_produtos` | dim_produtos | 36 |
| `dim_vendedores` | dim_vendedores | 12 |
| `fato_cotacao_moeda` | [[fato_cotacao_moeda (Entidade)\|fato_cotacao_moeda]] | 2873 na aba (2013 → 2026-10-07); 451 no modelo (≥ 2025) |

## Carga (Power Query)

Todas as 6 consultas seguem o mesmo M, mudando só `Item=`:

```m
let
    Fonte = Excel.Workbook(File.Contents(pCaminhoExcel), null, true),
    Planilha = Fonte{[Item="fato_vendas",Kind="Sheet"]}[Data],
    CabecalhoPromovido = Table.PromoteHeaders(Planilha, [PromoteAllScalars=true]),
    TipoAlterado = Table.TransformColumnTypes(CabecalhoPromovido,{...})
in
    TipoAlterado
```

> [!WARNING]
> `pCaminhoExcel` (`definition/expressions.tmdl`, grupo `Aux`) guarda caminho **absoluto**: `D:\Projetos\ifes_pbi_mcp_vendas\dados\Base de Dados.xlsx`. Ao mover projeto ou base, alterar só o parâmetro.

## Cobertura temporal

- Vendas: 2025-01-01 → 2026-09-17.
- Cotação do dólar: 2025-01-02 → 2026-10-07, dias úteis (2026-10-22: removidos da aba 4 valores zero e 2 datas duplicadas).
- Metas: 2025-01-01 → 2026-12-01 (grão mês × vendedor, data = dia 1).
- Calendário ([[dim_calendario (Entidade)|dim_calendario]]) vai além dos dados: eixos mostram período vazio à direita se não filtrados.
