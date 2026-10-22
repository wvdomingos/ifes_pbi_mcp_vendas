---
title: "Moeda (parâmetro)"
tags:
  - entity
  - modelo
  - parametro
  - cambio
date: 2026-10-22
status: active
fontes:
  - "[[CLAUDE]]"
---

# Moeda (Entidade)

Tabela calculada **desconectada** do [[Modelo Semantico]] que funciona como parâmetro R$ / U$. Criada via [[MCP (Conceito)|MCP]] em 2026-10-22.

```dax
DATATABLE("Moeda", STRING, "Ordem", INTEGER, "Descricao", STRING,
    {{"R$", 1, "Real (R$)"}, {"U$", 2, "Dólar (US$)"}})
```

- `Moeda[Moeda]` ordenada por `Ordem` (oculta); `Descricao` é o campo para o segmentador.
- Sem seleção (ou as duas) → `[Moeda Selecionada]` = `"R$"`.

## Como converte

Só as 4 medidas-base mudam; o resto herda ([[Medidas (Entidade)|Medidas]]):

| Medida | Em U$ |
|---|---|
| `Receita`, `Receita Bruta`, `Custo` | `SUMX(VALUES(dim_calendario[Data]), DIVIDE([<base> R$], [Cotação Dólar]))` — cada dia pela cotação vigente |
| `Meta` | mesmo padrão; meta mora no dia 1 do mês → cotação vigente no dia 1 |

Bases em reais ficam ocultas em `5. Câmbio`: `Receita R$`, `Receita Bruta R$`, `Custo R$`, `Meta R$`. Fonte da cotação: [[fato_cotacao_moeda (Entidade)|fato_cotacao_moeda]].

- 13 medidas monetárias usam **format string dinâmica**: `"US$" #,##0.00` ou `"R$" #,##0.00` (o `formatString` estático precisou ser limpo — TOM não aceita os dois).
- Percentuais e contagens não mudam.
- `HTML KPIs` e `HTML Narrativa Visão Executiva` trocam o símbolo via `VAR _sim`.

> [!INFO]
> Validado no modelo vivo: Receita total R$ 46,59 mi = US$ 8,64 mi; atingimento 155,9% (R$) × 154,8% (U$). Em 2026 a variação anual inverte: −5,0% em R$, +4,4% em U$ (dólar mais barato em 2026).
