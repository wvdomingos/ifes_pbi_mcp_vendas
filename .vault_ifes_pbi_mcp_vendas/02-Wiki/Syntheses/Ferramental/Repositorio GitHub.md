---
title: "Repositório e Versionamento"
tags:
  - synthesis
  - ferramental
  - git
date: 2026-10-19
status: active
fontes:
  - "[[README]]"
  - "[[CLAUDE]]"
---

# Repositório e Versionamento

Síntese de `README.md` e `CLAUDE.md`. Nome da nota mantido por compatibilidade de links.

## Estado

- A pasta `ifes_pbi_mcp_vendas` **não é repositório git** e não tem remoto.
- Nasceu como cópia do projeto irmão `.net_cachoeiro_2026_pbi_mcp_vendas` (público no GitHub); o `.gitignore` e a `LICENSE` (MIT) vieram junto.
- `.gitignore` já exclui `.pbi/localSettings.json`, `.pbi/cache.abf` e `.obsidian/workspace.json`, pronto para quando for versionada.

## README (o que a audiência vê)

Projeto de demonstração para o evento **IFES — Comércio Exterior** (2026). Três mensagens:
1. **Power BI como código** — TMDL/PBIR diffáveis ([[Modelo Semantico]], [[Relatorio PBIR]]).
2. **IA operando o modelo vivo** — `powerbi-modeling-mcp` ([[MCP (Conceito)]], [[Ferramental MCP e Skills]]).
3. **Contexto como ativo** — `CLAUDE.md`, `DESING.md` ([[DESING - Contrato Visual]]) e este vault.

Passos para rodar: copiar a pasta → ajustar `pCaminhoExcel` em `expressions.tmdl` ([[Fonte de Dados]]) → abrir `dashboards/ifes-pbi-mcp-vendas.pbip` → Atualizar.

> [!WARNING]
> `pCaminhoExcel` guarda caminho absoluto da máquina de origem; quem copia precisa trocar.
