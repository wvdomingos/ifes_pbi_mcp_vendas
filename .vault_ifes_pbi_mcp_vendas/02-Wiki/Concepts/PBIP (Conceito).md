---
title: "PBIP"
tags:
  - concept
  - power-bi
  - developer-mode
date: 2026-10-19
status: active
fontes:
  - "[[CLAUDE]]"
---

# PBIP (Conceito)

**Power BI Project** — formato de projeto do [[Power BI (Entidade)|Power BI]] Developer Mode. Em vez de um `.pbix` binário, uma pasta com arquivos de texto: modelo em [[TMDL (Conceito)|TMDL]] (`*.SemanticModel/`) e relatório em [[PBIR (Conceito)|PBIR]] (`*.Report/`), ligados por `definition.pbir` e pelo `.pbip`.

## Neste projeto

```
dashboards/ifes-pbi-mcp-vendas.pbip
dashboards/ifes-pbi-mcp-vendas.SemanticModel/
dashboards/ifes-pbi-mcp-vendas.Report/
```

- Renomear/mover pastas exige atualizar `.pbip`, `definition.pbir` e `displayName` nos dois `.platform`.
- `.pbi/localSettings.json` e `.pbi/cache.abf` são artefatos locais (ignorados em `.gitignore`).
- Versionado em git público — [[Repositorio GitHub]]. `*.pbix` ignorado: o PBIP é a fonte de verdade.

Ver [[Modelo Semantico]], [[Relatorio PBIR]].
