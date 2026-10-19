---
title: "Power BI"
tags:
  - entity
  - power-bi
  - ferramenta
date: 2026-10-19
status: active
fontes:
  - "[[CLAUDE]]"
  - "[[DESING]]"
---

# Power BI (Entidade)

Plataforma do projeto. Usada em **Developer Mode** ([[PBIP (Conceito)|PBIP]]): modelo em [[TMDL (Conceito)|TMDL]], relatório em [[PBIR (Conceito)|PBIR]], tudo texto plano editável fora do Desktop.

## Power BI Desktop

- Abre `dashboards/ifes-pbi-mcp-vendas.pbip`.
- Hospeda o modelo vivo (`msmdsrv`, porta dinâmica) que o [[MCP (Conceito)|MCP]] e o ADOMD acessam — ver [[Ferramental MCP e Skills]].
- Salvar com o projeto aberto sobrescreve edições de TMDL em disco.
- Dois PBIP na mesma sessão: risco de `PFE_IMBI_DB_COMPLEVEL_DOWNGRADE`.

## Regras visuais

Contrato em [[DESING - Contrato Visual]]; cores em [[Paleta - Dashboard Power BI]].

> [!INFO]
> `DESING.md` usa o link `[[Power BI]]` sem sufixo; esta nota segue o padrão `(Entidade)`.
