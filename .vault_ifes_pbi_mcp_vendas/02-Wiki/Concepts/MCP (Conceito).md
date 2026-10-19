---
title: "MCP"
tags:
  - concept
  - mcp
  - claude-code
date: 2026-10-12
status: active
fontes:
  - "[[CLAUDE]]"
  - "[[DESING]]"
---

# MCP (Conceito)

**Model Context Protocol** — protocolo que expõe ferramentas a um agente de IA. Neste projeto, o servidor `powerbi-modeling-mcp` (`@microsoft/powerbi-modeling-mcp`) permite ao Claude Code operar o modelo **vivo** aberto no [[Power BI (Entidade)|Power BI Desktop]] sem reabrir arquivos.

## Operações principais

`connection_operations` (ListLocalInstances, Connect) → `model_operations` (Get) → `table_operations`, `relationship_operations`, `measure_operations`, `dax_query_operations`.

## Regras do projeto

- Verificar carregamento antes de usar (`ToolSearch` por `connection_operations`); servidores só carregam na inicialização da sessão.
- Caminho preferencial para editar o [[Modelo Semantico]]; fallbacks em [[Ferramental MCP e Skills]].
- Integração via MCP **respeita os mesmos tokens** do [[DESING - Contrato Visual]] e confirma a configuração final dos visuais.
- Propriedade inexistente no Power BI → registrar limitação, não alegar aplicação.
