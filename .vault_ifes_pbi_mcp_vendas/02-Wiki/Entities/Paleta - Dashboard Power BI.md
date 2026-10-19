---
title: "Paleta - Dashboard Power BI"
tags:
  - entity
  - design
  - paleta
  - ifes
date: 2026-10-19
status: active
fontes:
  - "[[DESING]]"
---

# Paleta - Dashboard Power BI

Tokens de cor do [[DESING - Contrato Visual]]. Amostrados da imagem de referência (`#FEFEFE` centro, `#0E543A` verde escuro, `#88CE81` verde claro, `#FBE76F` amarelo); os demais derivados para legibilidade. Aproximações visuais, não identidade institucional oficial.

| Token | HEX | Aplicação |
|---|---|---|
| Fundo da página | `#F2FAF1` | Alternativa quando a imagem não estiver disponível |
| Superfície | `#FFFFFF` | Cards, gráficos, tabelas, filtros |
| Texto principal / título | `#0B4F35` | Títulos, valores principais |
| Texto secundário | `#475D52` | Contexto, unidades, rótulos, fontes |
| Verde primário | `#176B3A` | Série principal, botão primário, estado positivo |
| Verde complementar | `#167D3F` | Segunda ênfase, borda de foco |
| Verde claro decorativo | `#88CE81` | Só detalhe; nunca texto ou série isolada sobre branco |
| Amarelo de destaque | `#F8E35B` | Pequeno marcador/faixa; texto sempre verde escuro |
| Atenção | `#9C6500` | Texto/ícone de atenção |
| Crítico | `#A4262C` | Texto/ícone crítico |
| Borda sutil | `#D3E5D5` | Separação decorativa de cards |

**Séries categóricas (ordem):** `#176B3A`, `#456D95`, `#725A91`, `#956132`, `#475D52` — todas ≥ 3:1 contra branco.

## Contraste (WCAG, cores sólidas)

| Primeiro plano | Fundo | Razão |
|---|---|---:|
| `#0B4F35` | `#FFFFFF` | 9,62:1 |
| `#0B4F35` | `#F2FAF1` | 9,03:1 |
| `#475D52` | `#FFFFFF` | 7,11:1 |
| `#176B3A` ↔ `#FFFFFF` | | 6,56:1 |
| `#167D3F` | `#FFFFFF` | 5,20:1 |
| `#9C6500` | `#F2FAF1` | 4,61:1 |
| `#A4262C` | `#FFFFFF` | 7,26:1 |
| `#F8E35B` | `#FFFFFF` | 1,30:1 (só decoração) |

> [!WARNING]
> Contraste com o fundo não garante distinção entre séries nem adequação a daltonismo. Usar padrão de linha, rótulo direto ou legenda também.

## Onde está aplicada

Aplicada no tema custom do [[Relatorio PBIR]] (fonte `assets/tema_ifes_comercio_exterior.json`, registrado como `IFES_Com_rcio_Exterior…json`): `dataColors` = as 5 séries acima; `good`/`neutral`/`bad` = `#176B3A`/`#475D52`/`#A4262C`. As medidas HTML usam `#A4262C` para valores negativos (decisão do usuário).
