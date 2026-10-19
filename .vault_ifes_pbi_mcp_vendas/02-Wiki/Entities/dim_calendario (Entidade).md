---
title: "dim_calendario"
tags:
  - entity
  - modelo
  - dimensao
  - power-query
date: 2026-10-12
status: active
fontes:
  - "[[CLAUDE]]"
---

# dim_calendario (Entidade)

Dimensão de tempo do [[Modelo Semantico]], gerada em M (sem fonte externa). Grupo `Dimensão`, `dataCategory: Time`, ~14 displayFolders.

## Parâmetros (topo do Power Query, ~linha 1178 do `.tmdl`)

| Parâmetro | Valor |
|---|---|
| `startDate` | `#date(2025,1,1)` |
| `yearsAhead` | `1` |
| `startOfWeek` | `Day.Monday` |
| `monthOfFiscalYearEnd` | `3` |
| `closingMonthStartDay` | `16` |
| `language` | `"pt-BR"` |

`endDate = Date.AddYears(Date.EndOfYear(DateTime.LocalNow()), yearsAhead)` — **limite superior anda a cada virada de ano**. Em 2026: 1095 linhas, até 2027-12-31.

> [!INFO]
> Ajustar o calendário = mexer nesses parâmetros, não nas ~1160 linhas de definição de coluna.

## Conteúdo

Feriados brasileiros fixos e móveis, dias úteis, estações, quinzena, bimestre, semestre, ano fiscal. Nomes de coluna em português (`MesAnoNome`, `MesAnoNumero`, `DiasParaHoje`, `AnoAtual`), não os nomes em inglês do M.

## Observações

- Dados só até 2026-12: eixos e slicers mostram período vazio à direita se não filtrados.
- Nenhuma coluna tem `description` (pendência para [[documentacao (Entidade)|documentacao]]).
- `TMDLScripts/Script 1.tmdl` contém `createOrReplace` desta tabela — scratchpad, pode estar defasado.
- Recebe [[fato_vendas (Entidade)|fato_vendas]][Data] e [[metas_mensais (Entidade)|metas_mensais]][DataMes].
