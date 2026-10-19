---
title: "metas_mensais"
tags:
  - entity
  - modelo
  - fato
date: 2026-10-12
status: active
fontes:
  - "[[CLAUDE]]"
---

# metas_mensais (Entidade)

Segunda tabela fato do [[Modelo Semantico]]. Grupo `Fato`.

- **Origem:** aba `metas_mensais` ([[Fonte de Dados]]).
- **Linhas:** 288. **Período:** 2025-01-01 → 2026-12-01.
- **Grão:** mês × vendedor. `DataMes` = dia 1 do mês.
- **Chaves:** `DataMes` → [[dim_calendario (Entidade)|dim_calendario]]; `VendedorID` → dim_vendedores.

> [!WARNING]
> Liga ao calendário pelo dia 1. Total por mês/trimestre/ano funciona; filtrar um dia específico ou intervalo sem o dia 1 devolve meta vazia. Escolha deliberada no lugar de `TREATAS`. Se um visual precisar de meta em grão diário, é aqui que quebra.

> [!WARNING]
> Ao criar relacionamento pela UI, o Desktop aceita `metas_mensais[VendedorID] → dim_vendedores[Vendedor]` (nome único) e todas as metas caem na linha em branco. Validar com `INFO.VIEW.RELATIONSHIPS()`.
