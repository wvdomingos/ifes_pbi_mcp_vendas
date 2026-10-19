---
title: "Star Schema"
tags:
  - concept
  - modelagem
  - star-schema
date: 2026-10-12
status: active
fontes:
  - "[[CLAUDE]]"
---

# Star Schema (Conceito)

Modelagem dimensional: tabelas **fato** (eventos mensuráveis) no centro, ligadas a **dimensões** (contexto descritivo) por relacionamentos `*:1` de filtro em uma direção.

## Aplicação no projeto

- Fatos: [[fato_vendas (Entidade)|fato_vendas]], [[metas_mensais (Entidade)|metas_mensais]].
- Dimensões: [[dim_calendario (Entidade)|dim_calendario]], dim_clientes, dim_produtos, dim_vendedores.
- 6 relacionamentos, todos `*:1`, `OneDirection`, sem órfãs.
- Prefixos `fato_` / `dim_` em snake_case; grupos `Fato` / `Dimensão` em `model.tmdl`.
- Agregação implícita desligada (`summarizeBy: none`): métricas só via [[Medidas (Entidade)|Medidas]].

Dimensão compartilhada: `dim_calendario` e `dim_vendedores` filtram os dois fatos — base para comparar venda × meta.

Detalhes em [[Modelo Semantico]].
