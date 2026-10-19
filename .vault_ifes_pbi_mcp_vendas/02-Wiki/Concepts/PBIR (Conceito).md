---
title: "PBIR"
tags:
  - concept
  - power-bi
  - pbir
date: 2026-10-12
status: active
fontes:
  - "[[CLAUDE]]"
---

# PBIR (Conceito)

**Power BI Enhanced Report Format** — relatório como árvore de JSON: `definition/report.json`, `pages/pages.json`, `pages/<pageId>/page.json`, `pages/<pageId>/visuals/<visualId>/visual.json`. Temas e imagens em `StaticResources/`.

## Regras práticas

- Um visual = um arquivo; IDs hexadecimais opacos — localizar por `displayName` e `visualType`.
- `pages.json` guarda ordem e página ativa.
- `definition.pbir` aponta ao modelo por caminho relativo.
- Cores de série vêm do tema (`dataColors`), não do visual.

Parte do [[PBIP (Conceito)|PBIP]]. Estado atual em [[Relatorio PBIR]]; regras visuais em [[DESING - Contrato Visual]].
