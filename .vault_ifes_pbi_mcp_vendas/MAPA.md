---
title: "MAPA do Vault"
tags:
  - system
  - map
date: 2026-10-19
status: active
---

# MAPA do Vault

Mapa estrutural do vault `.vault_ifes_pbi_mcp_vendas`, base de conhecimento (LLM Wiki) do projeto de dashboard de vendas em Power BI.

## Estrutura

```
.vault_ifes_pbi_mcp_vendas/
├── 00-System/
│   ├── index.md                # catálogo de sínteses, entidades, conceitos + estatísticas
│   ├── log.md                  # log append-only de operações
│   └── ingestion-protocol.md   # regras de ingestão
├── 01-Sources/
│   ├── Raw/                    # inbox: fontes ainda não processadas
│   └── Archive/                # fontes já processadas
├── 02-Wiki/
│   ├── Syntheses/              # sínteses por categoria (Modelo, Relatorio, Design, Dados, Ferramental)
│   ├── Entities/               # entidades: "<Nome> (Entidade).md"
│   └── Concepts/               # conceitos: "<Nome> (Conceito).md"
├── Dashboard.md                # hub de navegação
└── MAPA.md                     # este arquivo
```

## Navegação

| Nota | Função |
|---|---|
| [[Dashboard]] | Ponto de entrada; links para todas as sínteses, entidades e conceitos |
| [[index]] | Catálogo tabular e estatísticas (fonte de verdade das contagens) |
| [[log]] | Histórico de ingests e alterações |
| [[ingestion-protocol]] | Como processar uma fonte nova, passo a passo |

## Fluxo

```
01-Sources/Raw  →  síntese em 02-Wiki/Syntheses  →  entidades/conceitos  →  index + log + Dashboard  →  01-Sources/Archive
```

## Relação com o projeto

O vault vive dentro da pasta do projeto, ao lado de:

| Caminho | Conteúdo |
|---|---|
| `../CLAUDE.md` | Guia operacional para Claude Code: arquitetura do modelo, convenções, armadilhas |
| `../DESING.md` | Contrato visual (paleta, tipografia, layout). Sintetizado em [[DESING - Contrato Visual]]; seus links resolvem em [[Paleta - Dashboard Power BI]] e [[MCP (Conceito)]] |
| `../README.md`, `../LICENSE` | Apresentação do projeto e licença MIT. Sintetizados em [[Repositorio GitHub]] |
| `../dashboards/` | PBIP: modelo semântico (TMDL) e relatório (PBIR) |
| `../dados/Base de Dados.xlsx` | Fonte de dados (5 planilhas) |
| `../assets/` | Fundo 16:9 Comércio Exterior, capa e logos IFES |

> [!WARNING]
> `CLAUDE.md`, `DESING.md` e os arquivos TMDL/PBIR são as fontes primárias. O vault sintetiza; não substitui. Quando houver conflito, vale o arquivo do projeto.

## Conteúdo atual (2026-10-19)

| Categoria | Síntese |
|---|---|
| Modelo | [[Modelo Semantico]] |
| Relatorio | [[Relatorio PBIR]] |
| Design | [[DESING - Contrato Visual]] |
| Dados | [[Fonte de Dados]] |
| Ferramental | [[Ferramental MCP e Skills]], [[Repositorio GitHub]] |

Entidades e conceitos listados em [[index]].

## Pendências

- `DESING.md` usa `[[Power BI]]` e `[[Comércio Exterior]]`; a primeira resolve como [[Power BI (Entidade)]], a segunda não tem nota. `DESING.md` está com `status: proposta`. Reingerir se `CLAUDE.md` ou `DESING.md` mudarem (sínteses são idempotentes).
