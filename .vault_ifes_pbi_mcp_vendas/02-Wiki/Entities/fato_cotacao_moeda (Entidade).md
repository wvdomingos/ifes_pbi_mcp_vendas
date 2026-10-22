---
title: "fato_cotacao_moeda"
tags:
  - entity
  - modelo
  - fato
  - cambio
date: 2026-10-22
status: active
fontes:
  - "[[CLAUDE]]"
---

# fato_cotacao_moeda (Entidade)

Fato de **cotação diária do dólar** (R$ por US$ 1) no [[Modelo Semantico]]. Adicionada pelo usuário em 2026-10-22; analisada e corrigida via [[MCP (Conceito)|MCP]]. Base da conversão R$ ↔ U$ do parâmetro [[Moeda (Entidade)|Moeda]].

## Estrutura

| Coluna | Tipo | Uso |
|---|---|---|
| `id_moeda` | int64 | código da moeda na origem (4 = dólar) |
| `moeda` / `nome` / `formatacao` | texto | `U$`, "Dólar dos Estados Unidos", format string sugerida — repetidos em toda linha |
| `data_cotacao` | data | liga em `dim_calendario[Data]` |
| `valor_cotacao` | decimal | R$ por US$ 1, formato `#,##0.0000` |
| `data_carga` | data/hora | carimbo da carga na origem |

Grupo `Fato`, mesmo M das outras abas do Excel ([[Fonte de Dados]]), aba `fato_cotacao_moeda`. Colunas numéricas com `summarizeBy: none`; todas com `description`.

## Relacionamento

`fato_cotacao_moeda[data_cotacao]` → `dim_calendario[Data]`, `*:1`, `OneDirection`, ativo. Sem órfãs após o filtro de 2025.

## Dados

- 451 linhas, **2025-01-02 → 2026-10-07**, só dias úteis (fim de semana e feriado sem linha).
- Aba do Excel guarda histórico desde 2013; o Power Query corta em 2025-01-01 (início do [[dim_calendario (Entidade)|calendário]]).

## Correções (2026-10-22)

> [!INFO]
> Projeto de demonstração: correções feitas **na planilha** e reforçadas no Power Query.

- Excel: removidas 4 cotações com valor 0 (15/11/2024, 20/11/2024, 03/03/2025, 04/03/2025) e 2 datas duplicadas (16/01/2023, 01/02/2023).
- Power Query, passos após `TipoAlterado`:

```m
CotacaoValida = Table.SelectRows(TipoAlterado, each [data_cotacao] <> null and [valor_cotacao] <> null and [valor_cotacao] > 0),
APartirDe2025 = Table.SelectRows(CotacaoValida, each [data_cotacao] >= #date(2025, 1, 1)),
SemDuplicatas = Table.Distinct(APartirDe2025, {"moeda", "data_cotacao"})
```

- `description` da tabela corrigida (vinha copiada de `metas_mensais`).

## Consumo

Medidas da pasta `5. Câmbio` em [[Medidas (Entidade)|Medidas]]: `Cotação Dólar` (última cotação válida até a data do contexto; antes da primeira usa a primeira) e `Cotação Média`.
