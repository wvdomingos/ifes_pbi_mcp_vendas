---
title: "TMDL"
tags:
  - concept
  - power-bi
  - tmdl
date: 2026-10-12
status: active
fontes:
  - "[[CLAUDE]]"
---

# TMDL (Conceito)

**Tabular Model Definition Language** — formato texto do modelo semântico tabular. Um arquivo por tabela em `definition/tables/`, mais `model.tmdl`, `database.tmdl`, `relationships.tmdl`, `expressions.tmdl`, `cultures/`.

## Regras práticas neste projeto

- `model.tmdl` mantém `ref table ...`; `.tmdl` novo sem `ref` é ignorado.
- Descrição = comentário `///` acima do objeto (alimenta [[documentacao (Entidade)|documentacao]]).
- `compatibilityLevel: 1606` em `database.tmdl`; sem downgrade.
- **Nunca editar com o projeto aberto no Desktop** — o Desktop sobrescreve ao salvar.
- `TMDLScripts/` é scratchpad do TMDL View, não definição.

Parte do [[PBIP (Conceito)|PBIP]]. Detalhes em [[Modelo Semantico]].
