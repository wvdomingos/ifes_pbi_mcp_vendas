---
title: "Dashboard"
tags:
  - dashboard
  - hub
date: 2026-10-19
status: active
---

# Dashboard — Vault IFES PBI MCP Vendas

Hub de navegação do conhecimento do projeto **ifes-pbi-mcp-vendas** (evento IFES — Comércio Exterior) (dashboard de vendas em Power BI, formato PBIP, modelo TMDL + relatório PBIR).

> [!INFO]
> Estrutura e fluxo de trabalho do vault: [[MAPA]]. Regras de ingestão: [[ingestion-protocol]].

## Sistema

- [[MAPA]] — mapa do vault
- [[index]] — catálogo de conteúdo
- [[log]] — log de operações
- [[ingestion-protocol]] — protocolo de ingestão

## Sínteses

### Modelo
- [[Modelo Semantico]] — star schema, 4 categorias de tabela, convenções, armadilhas

### Relatorio
- [[Relatorio PBIR]] — 2 páginas 1280×720, tema custom IFES, HTML Content, estrutura de arquivos

### Design
- [[DESING - Contrato Visual]] — identidade clara e verde, tipografia, canvas 1280×720, componentes, guardrails

### Dados
- [[Fonte de Dados]] — Excel com 5 planilhas, M de carga, `pCaminhoExcel`

### Ferramental
- [[Ferramental MCP e Skills]] — skills, MCP `powerbi-modeling-mcp`, fallbacks TMDL/ADOMD
- [[Repositorio GitHub]] — remoto público, `.gitignore`, licença MIT, README

## Entidades

- [[fato_vendas (Entidade)]]
- [[metas_mensais (Entidade)]]
- [[dim_calendario (Entidade)]]
- [[fato_cotacao_moeda (Entidade)]]
- [[Moeda (Entidade)]]
- [[Medidas (Entidade)]]
- [[documentacao (Entidade)]]
- [[Power BI (Entidade)]]
- [[Paleta - Dashboard Power BI]]

## Conceitos

- [[MCP (Conceito)]]
- [[PBIP (Conceito)]]
- [[TMDL (Conceito)]]
- [[PBIR (Conceito)]]
- [[Star Schema (Conceito)]]

## Fontes arquivadas

- [[CLAUDE]] — guia operacional para Claude Code
- [[DESING]] — contrato visual
- [[README]] — apresentação do projeto

## Estatísticas

| Métrica | Valor |
|---|---|
| Total de Sínteses | 6 |
| Total de Entidades | 9 |
| Total de Conceitos | 5 |
| Fontes processadas | 3 |
| Último ingest | 2026-10-22 |
