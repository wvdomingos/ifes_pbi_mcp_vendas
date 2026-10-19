---
title: "Protocolo de Ingestão"
tags:
  - system
  - protocol
date: 2026-10-12
status: active
---

# Protocolo de Ingestão

Regras para processar fontes colocadas em `01-Sources/Raw/`.

## Fluxo

1. **Deduplicação** — conferir em [[log]] se o arquivo/título já foi processado. Se sim, mover direto para `01-Sources/Archive/`.
2. **Síntese** — ler a fonte e criar/atualizar nota em `02-Wiki/Syntheses/<Categoria>/`. Se já existe síntese da mesma fonte, atualizar (idempotência).
3. **Entidades e Conceitos** — para cada entidade ou conceito citado, criar ou atualizar nota em `02-Wiki/Entities/<Nome> (Entidade).md` ou `02-Wiki/Concepts/<Nome> (Conceito).md`, sempre com link bidirecional para a síntese.
4. **Indexação** — registrar a síntese em [[index]] e incrementar as estatísticas.
5. **Log** — adicionar entrada no topo de [[log]] no formato `## [YYYY-MM-DD] ingest | Título`.
6. **Dashboard** — adicionar link em [[Dashboard]] e sincronizar as estatísticas com [[index]].
7. **Arquivamento** — mover a fonte para `01-Sources/Archive/`. `Raw/` fica vazio ao final.

## Padrões de nota

- Frontmatter YAML obrigatório: `title`, `tags`, `date`, `status`, `fontes` (lista de `[[links]]`).
- Links internos `[[Nota]]` ou `[[Nota|Rótulo]]`; embeds `![[Nota]]`.
- Callouts `> [!INFO]` para contexto e `> [!WARNING]` para armadilhas.

## Categorias de síntese previstas neste projeto

| Categoria | Conteúdo |
|---|---|
| `Modelo` | Modelo semântico (TMDL): tabelas, relacionamentos, medidas |
| `Relatorio` | Relatório (PBIR): páginas, visuais, tema |
| `Design` | Contrato visual, paleta, tipografia, layout |
| `Dados` | Fonte Excel, planilhas, grão, período |
| `Ferramental` | MCP, skills, Power BI Desktop, PBIP |

## Verificação

- Nenhum link quebrado.
- `Raw/` vazio após o ingest.
- Contagens em [[index]] = [[Dashboard]] = arquivos reais em `02-Wiki/`.
