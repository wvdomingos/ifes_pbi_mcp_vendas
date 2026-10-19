---
title: "Modelo Semântico (TMDL)"
tags:
  - synthesis
  - modelo
  - tmdl
  - dax
date: 2026-10-19
status: active
fontes:
  - "[[CLAUDE]]"
---

# Modelo Semântico (TMDL)

Síntese de `CLAUDE.md`, seções "Estado atual", "Arquitetura do modelo semântico", "Convenções" e "Armadilhas". Modelo em [[TMDL (Conceito)|TMDL]] dentro do projeto [[PBIP (Conceito)|PBIP]], em `dashboards/ifes-pbi-mcp-vendas.SemanticModel/definition/`.

## Estado

[[Star Schema (Conceito)|Star schema]] montado. 6 relacionamentos `*:1`, `OneDirection`, sem órfãs (validado no modelo vivo via MCP em 2026-10-19). `compatibilityLevel: 1606`, cultura `pt-BR`, `__PBI_TimeIntelligenceEnabled = 0`.

| Tabela | Grupo | Linhas | Período |
|---|---|---|---|
| [[fato_vendas (Entidade)\|fato_vendas]] | Fato | 4189 | 2025-01-01 → 2026-09-17 |
| [[metas_mensais (Entidade)\|metas_mensais]] | Fato | 288 | 2025-01-01 → 2026-12-01 |
| dim_clientes | Dimensão | 150 | — |
| dim_produtos | Dimensão | 36 | — |
| dim_vendedores | Dimensão | 12 | — |
| [[dim_calendario (Entidade)\|dim_calendario]] | Dimensão | 1095 | 2025-01-01 → 2027-12-31 |

```
fato_vendas[Data]          → dim_calendario[Data]
fato_vendas[ClienteID]     → dim_clientes[ClienteID]
fato_vendas[ProdutoID]     → dim_produtos[ProdutoID]
fato_vendas[VendedorID]    → dim_vendedores[VendedorID]
metas_mensais[DataMes]     → dim_calendario[Data]
metas_mensais[VendedorID]  → dim_vendedores[VendedorID]
```

**Medidas:** 28 em [[Medidas (Entidade)|Medidas]], pastas `0. Aux` a `4. HTML`, todas de negócio com `description`. Meta tem grão vendedor × mês e não se divide por cliente/produto/canal/status — ver a entidade.

## Quatro categorias de tabela

1. **Excel** (`Fato`, `Dimensão`) — 5 tabelas, mesmo M, só muda `Item=`. Caminho vem do parâmetro `pCaminhoExcel` em `expressions.tmdl`. Ver [[Fonte de Dados]].
2. **Gerada em M** — [[dim_calendario (Entidade)|dim_calendario]], parâmetros no topo do Power Query.
3. **Auxiliares** (`Aux`) — `Atualizacao` (`isHidden`, timestamp Brasília) e [[Medidas (Entidade)|Medidas]] (visível, container de medidas).
4. **Auto-documentação** — `Meta_Tables/Columns/Measures/Relationships` via `INFO.VIEW.*()` e [[documentacao (Entidade)|documentacao]] (UNION medidas + colunas visíveis).

> [!INFO]
> `description` de medidas e colunas alimenta a tabela `documentacao` exibida no relatório. Preencher sempre. Hoje: colunas do Excel e medidas de negócio têm descrição; `txtAtualizacao`, `Dummy` e `dim_calendario` não.

## Convenções

- Nomes em português; `dim_` / `fato_` em snake_case.
- Toda tabela nova precisa de `queryGroup` (`Aux` 0, `Fato` 1, `Dimensão` 2) e `ref table` em `model.tmdl`.
- Medidas na tabela `Medidas`, `displayFolder` numerado (`0. Aux`, `1. ...`).
- Colunas numéricas com `summarizeBy: none` de propósito — sem agregação implícita. Não trocar para `sum`.
- Descrições TMDL = comentário `///` na linha acima do objeto.

## Limites conhecidos (não são defeitos)

- `metas_mensais` liga ao calendário pelo dia 1 do mês. Total por mês/trimestre/ano funciona; filtro diário devolve meta vazia. Escolhido no lugar de `TREATAS`.
- `dim_calendario` termina no fim do ano seguinte ao atual (`yearsAhead = 1`); limite superior anda a cada virada de ano. Dados só até 2026-12.

## Armadilhas

- **Nunca editar TMDL com o projeto aberto no Desktop** — salvar sobrescreve o disco.
- `TMDLScripts/Script 1.tmdl` é scratchpad, não definição.
- `editorSettings.json` tem `autodetectRelationships: true` — conferir relacionamentos criados sozinhos.
- Dois PBIP na mesma sessão podem falhar com `PFE_IMBI_DB_COMPLEVEL_DOWNGRADE` (sem downgrade de 1606 → 1600).
- Relacionamento pela UI aceita coluna errada de nome único (`dim_vendedores[Vendedor]`); validar com `INFO.VIEW.RELATIONSHIPS()` e `ISBLANK(RELATED(...))`.

Ferramentas para editar: [[Ferramental MCP e Skills]].
