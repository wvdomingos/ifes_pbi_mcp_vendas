---
title: "Repositório GitHub"
tags:
  - synthesis
  - ferramental
  - git
  - github
date: 2026-10-19
status: active
fontes:
  - "[[README]]"
  - "[[CLAUDE]]"
---

# Repositório GitHub

Síntese de `README.md` e `CLAUDE.md`. Projeto versionado desde 2026-10-19.

## Remoto

- URL: `https://github.com/wvdomingos/ifes_pbi_mcp_vendas.git`
- Visibilidade: **público** — repositório de demonstração (evento IFES — Comércio Exterior).
- Branch: `main`, rastreando `origin/main`.
- Licença: **MIT** (`LICENSE`).
- Nasceu como cópia do projeto irmão `.net_cachoeiro_2026_pbi_mcp_vendas`; o histórico git começa do zero aqui.

## O que é versionado

PBIP completo (TMDL + PBIR + tema + imagens), `dados/Base de Dados.xlsx` (dados **sintéticos**), `assets/` (incluindo a fonte do tema `tema_ifes_comercio_exterior.json`), `CLAUDE.md`, `DESING.md`, `README.md`, `LICENSE` e este vault.

## `.gitignore` da raiz

| Padrão | Motivo |
|---|---|
| `**/.pbi/localSettings.json`, `**/.pbi/cache.abf` | artefatos locais do Power BI Desktop |
| `*.pbix`, `*.pbit` | binários; a fonte de verdade é o [[PBIP (Conceito)\|PBIP]] |
| `.vault_ifes_pbi_mcp_vendas/.obsidian/workspace*.json`, `.trash/` | estado local do Obsidian |
| `.claude/settings.local.json` | configuração local do Claude Code |
| `~$*`, `*.tmp`, `.vscode/`, `.idea/`, `.vs/`, `Thumbs.db`, `desktop.ini`, `.DS_Store` | lixo de Office, editores e SO |

## README (o que a audiência vê)

Três mensagens:
1. **Power BI como código** — TMDL/PBIR diffáveis ([[Modelo Semantico]], [[Relatorio PBIR]]).
2. **IA operando o modelo vivo** — `powerbi-modeling-mcp` ([[MCP (Conceito)]], [[Ferramental MCP e Skills]]).
3. **Contexto como ativo** — `CLAUDE.md`, `DESING.md` ([[DESING - Contrato Visual]]) e este vault.

Passos para rodar: clonar → ajustar `pCaminhoExcel` em `expressions.tmdl` ([[Fonte de Dados]]) → abrir `dashboards/ifes-pbi-mcp-vendas.pbip` → Atualizar.

> [!WARNING]
> `pCaminhoExcel` guarda caminho absoluto da máquina de origem; quem clona precisa trocar.
