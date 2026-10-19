---
title: "Log de Operações"
tags:
  - system
  - log
date: 2026-10-12
status: active
---

# Log de Operações

Append-only. Entradas mais recentes no topo.

## [2026-10-19] reingest | Base ampliada, 28 medidas, HTML e tema IFES

- **Operação:** registrar trabalho do dia: base sintética ampliada (30 clientes Norte/Sul/Centro-Oeste, vendas até 2026-09-17, 4189 linhas); 26 medidas novas via MCP (`1. Vendas`, `2. Meta` com `Meta Comparável`, `3. Tempo`, `4. HTML`); regra de meta por vendedor × mês; HTML KPIs e Narrativa na `Visão Executiva` com destaques negativo vermelho / positivo negrito (decisão do usuário); narrativa reduzida à frase de insight (decisão do usuário); tema custom `assets/tema_ifes_comercio_exterior.json` aplicado
- **Fontes processadas:** `CLAUDE.md` (cópia arquivada atualizada); `visual.json` da `Visão Executiva`; modelo vivo via MCP
- **Artefatos atualizados:** `Medidas (Entidade)`, `Relatorio PBIR`, `Modelo Semantico`, `Fonte de Dados`, `fato_vendas (Entidade)`, `Paleta - Dashboard Power BI`, `DESING - Contrato Visual`
- **Pendência:** combo Receita × Meta usa `Meta` crua, que não se divide por região
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-19] reingest | Projeto IFES: CLAUDE.md, DESING.md e README reescritos

- **Operação:** vault herdado do projeto irmão `.net_cachoeiro_2026_pbi_mcp_vendas`; reingestão para o estado real de `ifes_pbi_mcp_vendas` (evento IFES — Comércio Exterior): nomes `ifes-pbi-mcp-vendas`, 2 medidas, 2 páginas 1280×720, pasta sem git, novo contrato visual claro/verde. Entradas abaixo desta descrevem o projeto irmão
- **Fontes processadas:** `CLAUDE.md`, `DESING.md`, `README.md` (cópias em `01-Sources/Archive/`)
- **Artefatos atualizados:** `MAPA.md`, `Dashboard.md`, `00-System/index.md`, `DESING - Contrato Visual`, `Paleta - Dashboard Power BI`, `Relatorio PBIR`, `Modelo Semantico`, `Medidas (Entidade)`, `Fonte de Dados`, `Repositorio GitHub`, `Ferramental MCP e Skills`, `PBIP (Conceito)`, `Power BI (Entidade)`
- **Pendências:** contagens de linhas e ausência de órfãs herdadas, não reconferidas no modelo vivo
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-17] reingest | Slides da talk publicados em docs/apresentacao

- **Operação:** registrar `docs/apresentacao/NET_Cachoeiro_2026_IA_MCP_v3.pdf` como slides da talk; o PDF entrou no commit 533e2d6 sem revisão e o usuário decidiu mantê-lo publicado. Conteúdo do PDF não ingerido
- **Fontes processadas:** `CLAUDE.md` e `README.md` (cópias arquivadas atualizadas)
- **Artefatos atualizados:** `MAPA.md`, `02-Wiki/Syntheses/Ferramental/Repositorio GitHub.md`
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-17] atualização | Visuais da Overview e decisão sobre HTML Narrativa

- **Operação:** documentar os 11 visuais da `Overview` após edição no Desktop; registrar que `HTML Narrativa Visão Geral` fica no modelo sem visual
- **Fontes processadas:** `CLAUDE.md` (cópia arquivada atualizada); `visual.json` da página `Overview`
- **Artefatos atualizados:** `02-Wiki/Syntheses/Relatorio/Relatorio PBIR.md`, `02-Wiki/Entities/Medidas (Entidade).md`
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-17] reingest | CLAUDE.md após medidas HTML Narrativa e Insight

- **Operação:** reingest de `CLAUDE.md` (28 medidas; novas `HTML Narrativa Visão Geral` e `HTML Insight Visão Geral` criadas via MCP)
- **Fontes processadas:** `CLAUDE.md` (cópia arquivada atualizada)
- **Artefatos atualizados:** `02-Wiki/Entities/Medidas (Entidade).md`, `02-Wiki/Syntheses/Modelo/Modelo Semantico.md`
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-12] reingest | CLAUDE.md após medidas DAX e visual HTML

- **Operação:** reingest de `CLAUDE.md` (26 medidas criadas via MCP; página Overview com HTML Content, slicers e combo)
- **Fontes processadas:** `CLAUDE.md` (cópia arquivada atualizada)
- **Artefatos atualizados:** `02-Wiki/Entities/Medidas (Entidade).md`, `02-Wiki/Entities/documentacao (Entidade).md`, `02-Wiki/Syntheses/Modelo/Modelo Semantico.md`, `02-Wiki/Syntheses/Relatorio/Relatorio PBIR.md`
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-12] correção | Medidas não é isHidden

- **Operação:** correção factual após validar modelo vivo via MCP (`GetStats`: `Medidas.isHidden = false`)
- **Fontes processadas:** `CLAUDE.md` (corrigido e cópia arquivada atualizada)
- **Artefatos atualizados:** `02-Wiki/Syntheses/Modelo/Modelo Semantico.md`, `02-Wiki/Entities/Medidas (Entidade).md`
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-12] ingest | README.md e reingest de CLAUDE.md (versionamento)

- **Operação:** ingest de `README.md`; reingest de `CLAUDE.md` após criação do repositório git
- **Fontes processadas:** `README.md` (nova), `CLAUDE.md` (cópia arquivada substituída pela versão atual)
- **Artefatos criados:** `02-Wiki/Syntheses/Ferramental/Repositorio GitHub.md`
- **Artefatos atualizados:** `02-Wiki/Syntheses/Ferramental/Ferramental MCP e Skills.md` e `02-Wiki/Concepts/PBIP (Conceito).md` (removido "não é repositório git"), `00-System/index.md`, `Dashboard.md`, `MAPA.md`
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-12] ingest | DESING.md e CLAUDE.md

- **Operação:** ingest inicial das fontes primárias do projeto
- **Fontes processadas:** `DESING.md`, `CLAUDE.md` (copiadas de `D:\Projetos\.net_cachoeiro_2026_pbi_mcp_vendas\`, arquivadas em `01-Sources/Archive/`)
- **Artefatos criados:**
  - Sínteses: `02-Wiki/Syntheses/Design/DESING - Contrato Visual.md`, `02-Wiki/Syntheses/Modelo/Modelo Semantico.md`, `02-Wiki/Syntheses/Relatorio/Relatorio PBIR.md`, `02-Wiki/Syntheses/Dados/Fonte de Dados.md`, `02-Wiki/Syntheses/Ferramental/Ferramental MCP e Skills.md`
  - Entidades: `Paleta - Dashboard Power BI.md`, `fato_vendas (Entidade).md`, `metas_mensais (Entidade).md`, `dim_calendario (Entidade).md`, `Medidas (Entidade).md`, `documentacao (Entidade).md`, `Power BI (Entidade).md`
  - Conceitos: `MCP (Conceito).md`, `PBIP (Conceito).md`, `TMDL (Conceito).md`, `PBIR (Conceito).md`, `Star Schema (Conceito).md`
- **Artefatos atualizados:** `00-System/index.md`, `Dashboard.md`, `MAPA.md`
- **Observações:** `Paleta - Dashboard Power BI` criada sem sufixo `(Entidade)` para resolver o wikilink de `DESING.md`. Links `[[Power BI]]` e `[[capa_1_fundo.png]]` de `DESING.md` seguem sem alvo direto (nota é `Power BI (Entidade)`; imagem vive em `../assets/`).
- **Realizado por:** Claude Code
- **Aprovado por:** Wander

## [2026-10-12] init | Criação do vault

- **Operação:** inicialização da estrutura LLM Wiki
- **Fontes processadas:** nenhuma
- **Artefatos criados:** `00-System/index.md`, `00-System/log.md`, `00-System/ingestion-protocol.md`, `01-Sources/Raw/`, `01-Sources/Archive/`, `02-Wiki/Syntheses/`, `02-Wiki/Entities/`, `02-Wiki/Concepts/`, `Dashboard.md`, `MAPA.md`
- **Realizado por:** Claude Code
- **Aprovado por:** Wander
