---
title: "documentacao"
tags:
  - entity
  - modelo
  - dax
  - documentacao
date: 2026-10-12
status: active
fontes:
  - "[[CLAUDE]]"
---

# documentacao (Entidade)

Camada de auto-documentação do [[Modelo Semantico]] — o traço mais incomum do modelo. Tabelas calculadas DAX:

- `Meta_Tables` = `INFO.VIEW.TABLES()`
- `Meta_Columns` = `INFO.VIEW.COLUMNS()`
- `Meta_Measures` = `INFO.VIEW.MEASURES()`
- `Meta_Relationships` = `INFO.VIEW.RELATIONSHIPS()`
- `documentacao` = `UNION` das medidas com as colunas visíveis (excluindo `Data Dictionary`), colunas Type / Name / Description / Location / Expression.

> [!INFO]
> `description` de medidas e colunas **não é decorativa**: alimenta esta tabela, exibida no [[Relatorio PBIR]]. Sempre preencher ao criar medida ou coluna visível.

Cobertura atual: colunas das 5 tabelas do Excel e todas as medidas de [[Medidas (Entidade)|Medidas]] completas; [[dim_calendario (Entidade)|dim_calendario]] sem nenhuma.

Em TMDL, descrição = comentário `///` na linha acima do objeto.
