# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## O que é este repositório

Projeto de demonstração (evento **IFES — Comércio Exterior**, 2026) de um dashboard de **vendas** em
Power BI mantido no formato **PBIP / Developer Mode** — modelo em TMDL e relatório em PBIR, tudo texto
plano e editável fora do Power BI Desktop.

```
dados/Base de Dados.xlsx                              # fonte de dados (5 planilhas)
dashboards/ifes-pbi-mcp-vendas.pbip                   # ponto de entrada (abre no Power BI Desktop)
dashboards/ifes-pbi-mcp-vendas.SemanticModel/         # modelo semântico (TMDL)
dashboards/ifes-pbi-mcp-vendas.Report/                # relatório (PBIR, um JSON por visual)
DESING.md                                             # contrato visual (paleta, tipografia, layout)
assets/                                               # fundo 16:9, capa e logos do IFES
.vault_ifes_pbi_mcp_vendas/                           # vault Obsidian (LLM Wiki): MAPA.md, Dashboard.md, 02-Wiki/
```

Não há build, lint ou testes. O ciclo é: editar TMDL/PBIR → abrir o `.pbip` no Power BI Desktop →
atualizar. Repositório git em `main`, remoto `origin` =
`https://github.com/wvdomingos/ifes_pbi_mcp_vendas.git` (**público**). O `.gitignore` exclui
`.pbi/localSettings.json`, `.pbi/cache.abf` e o estado local do Obsidian.

O projeto nasceu como cópia de um projeto irmão (`.net_cachoeiro_2026_pbi_mcp_vendas`), mais avançado.
Medidas, páginas e regras daquele projeto **não existem aqui** — não assuma que existem.

## Estado atual

Star schema montado: 6 abas do Excel viram tabelas via Power Query, mais `dim_calendario` gerada em M.
7 relacionamentos em `relationships.tmdl`, `*:1`, `OneDirection`:

```
fato_vendas[Data]          → dim_calendario[Data]
fato_vendas[ClienteID]     → dim_clientes[ClienteID]
fato_vendas[ProdutoID]     → dim_produtos[ProdutoID]
fato_vendas[VendedorID]    → dim_vendedores[VendedorID]
metas_mensais[DataMes]     → dim_calendario[Data]
metas_mensais[VendedorID]  → dim_vendedores[VendedorID]
fato_cotacao_moeda[data_cotacao] → dim_calendario[Data]
```

**Dados (Excel, sintéticos):** `fato_vendas` 4189 linhas, 2025-01-01 → 2026-09-17; `dim_clientes`
150 (Sudeste 96, Nordeste 24, Sul 12, Centro-Oeste 10, Norte 8 — C121…C150 adicionados em 2026-10-19
com vendas em todo o período); `dim_produtos` 36; `dim_vendedores` 12; `metas_mensais` 288
(2025-01 → 2026-12); `dim_calendario` 1095; `fato_cotacao_moeda` 451 no modelo (cotação diária do dólar, dias úteis,
2025-01-02 → 2026-10-07; a aba guarda desde 2013 e o Power Query corta em 2025 — em 2026-10-22 foram
removidos da aba 4 valores zero e 2 datas duplicadas). Sem órfãs (validado no modelo vivo).

**Medidas:** 40 em `Medidas`, todas de negócio com `description`:

| Pasta | Medidas |
|---|---|
| `0. Aux` | `txtAtualizacao`, `Dummy` (sem `description`), `Cor Atingimento`, `Cor Atingimento Degradê` |
| `1. Vendas` | Receita, Receita Bruta, Desconto, Desconto %, Custo, Margem Bruta, Margem Bruta %, Quantidade Vendida, Pedidos, Pedidos Cancelados, Taxa de Cancelamento %, Ticket Médio, Clientes Ativos |
| `2. Meta` | Meta, Meta Comparável, Atingimento %, Gap Meta, Meta Max (`= 1`, criada pelo usuário) |
| `3. Tempo` | Receita Ano Anterior, Receita Var. Anual %, Receita Mês Anterior, Receita Var. Mensal %, Receita Acumulada Ano, Meta Acumulada Ano, Atingimento Acumulado Ano % |
| `4. HTML` | HTML KPIs / Narrativa Visão Executiva, HTML KPIs / Narrativa Desempenho Comercial |
| `5. Câmbio` | Moeda Selecionada, Cotação Dólar, Cotação Média; ocultas: Receita R$, Receita Bruta R$, Custo R$, Meta R$ |

Regras:

- Toda medida de venda filtra `fato_vendas[Status] = "Faturado"`; Receita = Σ Quantidade ×
  PrecoUnitario × (1 − DescontoPct).
- Variações retornam BLANK sem valor atual ou base; acumulados retornam BLANK após a última data com
  venda (meses futuros não acumulam meta).
- **Meta tem grão vendedor × mês e não se divide por cliente, produto, canal ou status.** `Meta
  Comparável`, `Atingimento %`, `Gap Meta`, `Atingimento Acumulado Ano %` e os HTML ficam vazios (ou
  avisam) quando há filtro nessas dimensões — não "conserte" isso. `Meta` crua não tem essa proteção.
- `Meta Comparável` e os HTML recortam meta e ano anterior até a última data com venda, para não
  comparar ano parcial com ano cheio.
- **HTML** (custom visual **HTML Content**, tokens do `DESING.md`): `HTML KPIs` = 4 cards (Receita,
  Atingimento da meta, Pedidos, Ticket médio) com comparação vs. mesmo período; `HTML Narrativa` = só
  cabeçalho com período + uma frase (receita, variação anual, atingimento com folga/falta) — seções
  Contexto/Pontos de atenção/Para explorar foram removidas por decisão do usuário. Por decisão do
  usuário, negativos (variação, gap, atingimento < 100%) em vermelho `#A4262C` com sinal/palavra,
  positivos em negrito. Trechos somem quando falta base.
- **Câmbio R$ / U$:** tabela calculada desconectada `Moeda` (`R$`, `U$`; segmentador em
  `Moeda[Descricao]`; sem seleção = R$). Só `Receita`, `Receita Bruta`, `Custo` e `Meta` convertem —
  `SUMX(VALUES(dim_calendario[Data]), DIVIDE([<base> R$], [Cotação Dólar]))`; o resto herda. `Cotação
  Dólar` = última cotação válida até a data (cobre fim de semana/feriado; antes da primeira, usa a
  primeira). Meta converte pela cotação do dia 1 do mês. As 13 medidas monetárias usam format string
  dinâmica (`"R$"`/`"US$"`) — o `formatString` estático tem de ficar vazio (TOM rejeita os dois). Os
  HTML da Visão Executiva trocam o símbolo via `VAR _sim`. Variação anual muda de sinal entre moedas
  (2026: −5,0% em R$, +4,4% em U$): é câmbio, não bug.
- **Cores condicionais** (formatação por valor do campo): `Cor Atingimento` = `#A4262C` < 100%,
  `#176B3A` ≥ 100%; `Cor Atingimento Degradê` interpola RGB `#A4262C` (≤ 50%) → `#9C6500` (100%) →
  `#0B4F35` (≥ 150%). Pontos 50/100/150 são escolha de demonstração, não limiar de negócio.
- Base sintética tem receita bem acima da meta (≈190% em 2025, ≈165% em 2026 até 17/09): atingimento
  alto é dado, não bug. Setembro/2026 é mês parcial, então suas variações mensais saem negativas.

**Relatório:** 2 páginas em **1280×720**. `Capa`: card `txtAtualizacao`. `Visão Executiva` (ativa):
caixa de texto (título), imagem, 2 HTML Content (`HTML KPIs` e `HTML Narrativa`), slicers de Ano,
MesNome, Regiao e Vendedor, combo coluna/linha Receita × Meta por mês, barras de Receita por Regiao e
por Categoria, card `txtAtualizacao`. O combo usa `Meta` crua: com slicer de Regiao, a linha de meta
não se divide (ver regra acima).

**Tema:** base `Fluent2-CY26SU10` + custom `StaticResources/RegisteredResources/IFES_Com_rcio_Exterior…json`,
importado de `assets/tema_ifes_comercio_exterior.json` (fonte editável — altere lá e reimporte em
Exibir → Temas). `dataColors` = séries do `DESING.md`; visuais com fundo branco, borda `#D3E5D5` 1 px,
raio 4, sem sombra; HTML Content, imagem e caixa de texto sem fundo/borda. Fundos de página
registrados: `background_ifes_comercio_exter…png`, `IFES_Comercio_Exterior_PBI_IA_…png`; logo
`logo-ifes-removebg-preview…png`.

Limites conhecidos do desenho (não são defeitos a corrigir às cegas):

- `metas_mensais` tem grão mês × vendedor e liga ao calendário pelo **dia 1** do mês. Total por
  mês/trimestre/ano funciona; filtrar dia específico ou intervalo sem o dia 1 devolve meta vazia.
- `dim_calendario` vai de 2025-01-01 até o fim do ano seguinte ao atual (`endDate` deriva de
  `DateTime.LocalNow()` com `yearsAhead = 1`), então o limite superior anda sozinho a cada virada de
  ano. Eixos e slicers mostram período vazio à direita se não forem filtrados.

## Arquitetura do modelo semântico

Tabelas em `dashboards/ifes-pbi-mcp-vendas.SemanticModel/definition/tables/`, todas `mode: import`,
em quatro categorias:

**1. Tabelas do Excel (grupos `Fato` e `Dimensão`)** — `fato_vendas`, `metas_mensais`,
`fato_cotacao_moeda`, `dim_clientes`, `dim_produtos`, `dim_vendedores`. Mesmo M, mudando só o `Item=`
(`fato_cotacao_moeda` acrescenta `CotacaoValida` > 0, `APartirDe2025` e `SemDuplicatas`):

```m
let
    Fonte = Excel.Workbook(File.Contents(pCaminhoExcel), null, true),
    Planilha = Fonte{[Item="fato_vendas",Kind="Sheet"]}[Data],
    CabecalhoPromovido = Table.PromoteHeaders(Planilha, [PromoteAllScalars=true]),
    TipoAlterado = Table.TransformColumnTypes(CabecalhoPromovido,{...})
in
    TipoAlterado
```

O caminho vem do parâmetro `pCaminhoExcel` em `definition/expressions.tmdl` (grupo `Aux`), hoje
`D:\Projetos\ifes_pbi_mcp_vendas\dados\Base de Dados.xlsx`. É absoluto: **ao mover a pasta, altere só
o parâmetro**.

**2. `dim_calendario` (grupo `Dimensão`)** — gerador parametrizado no topo do Power Query (~linha
1178 do `.tmdl`: `startDate`, `yearsAhead`, `startOfWeek`, `monthOfFiscalYearEnd`,
`closingMonthStartDay`, `language = "pt-BR"`). Feriados brasileiros, dias úteis, estações, ano fiscal.
**Ajustar o calendário = mexer nesses parâmetros**, não nas ~1160 linhas de coluna acima.

**3. Auxiliares (grupo `Aux`)** — `Moeda` (calculada DAX, parâmetro R$/U$, sem relacionamento); `Atualizacao` (oculta; `DateTime.LocalNow()` em horário de
Brasília via `DateTimeZone.SwitchZone(...,-3)`) e `Medidas` (tabela vazia, **container de toda
medida nova**).

**4. Auto-documentação (tabelas calculadas DAX)** — `Meta_Tables`, `Meta_Columns`, `Meta_Measures`,
`Meta_Relationships` = `INFO.VIEW.*()`; `documentacao` = `UNION` de medidas e colunas visíveis
(Type / Name / Description / Location / Expression). Logo, **`description` não é decorativa**:
alimenta `documentacao`. Preencha em toda medida/coluna visível nova.

## Convenções

- Cultura `pt-BR`; nomes de objetos em português.
- Dimensões `dim_` + `snake_case`; fatos `fato_`.
- Toda tabela nova precisa de `queryGroup:` — `Aux` (0), `Fato` (1) ou `Dimensão` (2), declarados em
  `model.tmdl`.
- Medidas na tabela `Medidas`, `displayFolder` prefixado por número (`0. Aux`, `1. …`).
- `model.tmdl` mantém a lista `ref table ...`; `.tmdl` novo sem o `ref` é ignorado.
- `compatibilityLevel: 1606`; `__PBI_TimeIntelligenceEnabled = 0`.
- Colunas numéricas usam `summarizeBy: none` de propósito (obriga medida explícita). Não trocar para `sum`.
- Descrições em TMDL são comentários `///` na linha acima do objeto.
- Colunas de `dim_calendario` têm nomes em português (`MesAnoNome`, `DiasParaHoje`…).

## Relatório (PBIR)

- `definition.pbir` aponta para `../ifes-pbi-mcp-vendas.SemanticModel` por caminho relativo. Renomear
  ou mover uma das pastas exige atualizar `.pbip`, `definition.pbir` e `displayName` dos `.platform`.
- Um visual = `definition/pages/<pageId>/visuals/<visualId>/visual.json`; ordem e página ativa em
  `pages.json`. IDs são hex opacos — localize por `displayName`/`visualType`.

## Contrato visual: `DESING.md`

`DESING.md` (grafia com typo, preservar; `status: proposta`) é o contrato para qualquer trabalho no
relatório. Identidade **clara e verde** derivada de `assets/background_ifes_comercio_exterior_16x9_v1.png`:
texto `#0B4F35`, superfície `#FFFFFF`, fundo alternativo `#F2FAF1`, verde primário `#176B3A`, amarelo
`#F8E35B` só decorativo. Segoe UI; canvas 1280×720, margem 32 px, grid de 12 colunas; ordem de
séries `#176B3A`, `#456D95`, `#725A91`, `#956132`, `#475D52`. Regras que mais importam:

- Visuais sobre superfícies brancas opacas; imagem de fundo é decorativa.
- Leitura **insight → contexto → ação**; título só afirma conclusão sustentada pelos dados.
- Não inventar números, metas, limiares, logotipo ou brasão; sem regra confirmada, estado fica neutro.
- Cor nunca é o único canal; contraste vale só para os pares listados — não afirmar acessibilidade garantida.

Os wikilinks do arquivo resolvem em `.vault_ifes_pbi_mcp_vendas/02-Wiki/` (padrão LLM Wiki; `MAPA.md`
descreve a estrutura, `00-System/` o protocolo). Em conflito, vale o arquivo do projeto. Ao alterar
`CLAUDE.md` ou `DESING.md`, reingira no vault (skill `obsidian-vault-manager`).

## Armadilhas conhecidas

- `SemanticModel/TMDLScripts/` é scratchpad do TMDL View; a fonte de verdade é `definition/`.
- `.pbi/localSettings.json` e `.pbi/cache.abf` são artefatos locais. `.pbi/editorSettings.json` tem
  `autodetectRelationships: true`: ao carregar tabela nova, confira relacionamentos criados sozinhos.
- **Nunca edite TMDL com o projeto aberto no Desktop** — ao salvar, ele sobrescreve os arquivos.
- Abrir dois PBIP na mesma sessão pode falhar com `PFE_IMBI_DB_COMPLEVEL_DOWNGRADE` (modelo 1606 já
  carregado + outro em 1600). Feche tudo e abra só um.
- Ao ligar relacionamento pela UI, confira a coluna de destino (ex.: `VendedorID → Vendedor` é aceito
  e não casa nada). Valide com `INFO.VIEW.RELATIONSHIPS()` e conte órfãs com `ISBLANK(RELATED(...))`.

## Ferramental: MCP e skills

| Skill | Quando |
|---|---|
| `powerbi-modeling` | Trabalho no modelo: tabelas, relacionamentos, medidas, RLS, performance. Define o workflow. |
| `powerbi-expert` | Referência de DAX, M, star schema, time intelligence. Complementa a anterior. |
| `caveman` | Estilo de comunicação padrão: terse, sem filler. Código e docs seguem escrita normal. |

Invoque `powerbi-modeling` e `powerbi-expert` juntas antes de mexer no modelo; leia `DESING.md` antes
de mexer no relatório.

### MCP `powerbi-modeling-mcp`

Caminho preferencial: opera no modelo **vivo** aberto no Desktop.

```
connection_operations(operation: "ListLocalInstances")
connection_operations(operation: "Connect")
model_operations(operation: "Get")
table_operations / relationship_operations / measure_operations
```

Verifique antes que está carregado (`ToolSearch` por `connection_operations`). Se não estiver:
`claude mcp add powerbi-modeling-mcp --scope user -- npx -y @microsoft/powerbi-modeling-mcp@latest --start`
e reinicie a sessão.

### Fallbacks

1. **Editar TMDL direto** em `definition/tables/*.tmdl` + `ref table` em `model.tmdl`; o usuário
   atualiza no Desktop.
2. **Leitura via ADOMD** (só consulta). Porta do `msmdsrv` é dinâmica:

```powershell
$pid = (Get-Process msmdsrv).Id
$port = (Get-NetTCPConnection -OwningProcess $pid -State Listen)[0].LocalPort
Add-Type -Path "C:\Program Files\Microsoft.NET\ADOMD.NET\160\Microsoft.AnalysisServices.AdomdClient.dll"
$cn = New-Object Microsoft.AnalysisServices.AdomdClient.AdomdConnection("Data Source=localhost:$port")
$cn.Open()
```

`EVALUATE INFO.VIEW.TABLES()` / `RELATIONSHIPS()` / `MEASURES()` mostram o estado real do modelo.
