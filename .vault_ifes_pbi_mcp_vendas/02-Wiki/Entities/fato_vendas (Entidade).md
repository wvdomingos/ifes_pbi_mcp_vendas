---
title: "fato_vendas"
tags:
  - entity
  - modelo
  - fato
date: 2026-10-19
status: active
fontes:
  - "[[CLAUDE]]"
---

# fato_vendas (Entidade)

Tabela fato principal do [[Modelo Semantico]]. Grupo `Fato`, `mode: import`.

- **Origem:** aba `fato_vendas` do Excel ([[Fonte de Dados]]).
- **Linhas:** 4189. **Período:** 2025-01-01 → 2026-09-17 (base sintética ampliada em 2026-10-19: vendas de set/2026 e histórico dos clientes Norte, Sul e Centro-Oeste).
- **Chaves:** `Data` → [[dim_calendario (Entidade)|dim_calendario]]; `ClienteID` → dim_clientes; `ProdutoID` → dim_produtos; `VendedorID` → dim_vendedores. Todos `*:1`, `OneDirection`, sem órfãs.
- Colunas numéricas com `summarizeBy: none` — exigem medida explícita em [[Medidas (Entidade)|Medidas]].
- Todas as colunas têm `description` (alimenta [[documentacao (Entidade)|documentacao]]).

Padrão [[Star Schema (Conceito)|star schema]].
