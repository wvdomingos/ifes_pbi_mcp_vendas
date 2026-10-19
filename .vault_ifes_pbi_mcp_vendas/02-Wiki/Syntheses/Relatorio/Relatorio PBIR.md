---
title: "Relatório (PBIR)"
tags:
  - synthesis
  - relatorio
  - pbir
date: 2026-10-19
status: active
fontes:
  - "[[CLAUDE]]"
---

# Relatório (PBIR)

Síntese de `CLAUDE.md`, seção "Relatório (PBIR)". Relatório em formato [[PBIR (Conceito)|PBIR]] em `dashboards/ifes-pbi-mcp-vendas.Report/`.

## Estado

- 2 páginas em **1280×720**, conforme [[DESING - Contrato Visual]].
- `Capa`: card `txtAtualizacao`.
- `Visão Executiva` (ativa): caixa de texto (título), imagem, 2 **HTML Content** (`HTML KPIs Visão Executiva` e `HTML Narrativa Visão Executiva`, ver [[Medidas (Entidade)]]), slicers de Ano, MesNome, Regiao e Vendedor, combo coluna/linha Receita × Meta por mês, barras de Receita por Regiao e por Categoria, card `txtAtualizacao`.
- Custom visual registrado em `report.json` → `publicCustomVisuals`: `htmlContent443BE3AD55E043BF878BED274D3A6865`.

> [!WARNING]
> O combo usa `Meta` crua. Com slicer de Regiao, a linha de meta não se divide (meta é por vendedor × mês).

## Tema

- Base `Fluent2-CY26SU10` + custom `StaticResources/RegisteredResources/IFES_Com_rcio_Exterior…json`.
- Fonte editável: `assets/tema_ifes_comercio_exterior.json` — alterar lá e reimportar em Exibir → Temas.
- `dataColors` = séries da [[Paleta - Dashboard Power BI]]; visuais com fundo branco, borda `#D3E5D5` 1 px, raio 4, sem sombra, padding 16; HTML Content, imagem e caixa de texto sem fundo/borda.
- Recursos registrados: fundos `background_ifes_comercio_exter…png` e `IFES_Comercio_Exterior_PBI_IA_…png`, logo `logo-ifes-removebg-preview…png`.

## Estrutura de arquivos

- Um visual = `definition/pages/<pageId>/visuals/<visualId>/visual.json`.
- Ordem e página ativa em `pages.json`.
- IDs hexadecimais opacos — localizar por `displayName` e `visualType`.
- `definition.pbir` aponta ao modelo por caminho relativo (`../ifes-pbi-mcp-vendas.SemanticModel`). Renomear/mover pastas exige atualizar `.pbip`, `definition.pbir` e `displayName` nos dois `.platform`.

## Regras ao gerar PBIR

Ler [[DESING - Contrato Visual]] antes. Resumo:
- Visuais sobre superfícies brancas opacas; imagem de fundo só decorativa.
- Sem cor, fonte ou efeito fora do contrato; séries na ordem definida.
- Não inventar dados, metas, limiares, logotipo ou brasão.
- Nunca afirmar acessibilidade garantida.

Modelo que o relatório consome: [[Modelo Semantico]].
