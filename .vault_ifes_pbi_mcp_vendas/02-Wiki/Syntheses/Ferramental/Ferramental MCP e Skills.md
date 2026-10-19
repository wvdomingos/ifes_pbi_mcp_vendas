---
title: "Ferramental: MCP e Skills"
tags:
  - synthesis
  - ferramental
  - mcp
  - claude-code
date: 2026-10-19
status: active
fontes:
  - "[[CLAUDE]]"
---

# Ferramental: MCP e Skills

Síntese de `CLAUDE.md`, seção "Ferramental". Como Claude Code edita o [[Modelo Semantico]] e o [[Relatorio PBIR]].

## Ciclo de trabalho

Sem build, lint ou testes. Editar TMDL/PBIR → abrir `dashboards/ifes-pbi-mcp-vendas.pbip` no [[Power BI (Entidade)|Power BI Desktop]] → atualizar. Pasta ainda não versionada — ver [[Repositorio GitHub]].

## Skills

| Skill | Quando |
|---|---|
| `powerbi-modeling` | Trabalho no modelo: tabelas, relacionamentos, medidas, RLS, calculation groups. Workflow conectar → analisar → agir. |
| `powerbi-expert` | Referência DAX, M, star schema, time intelligence, anti-patterns. |
| `caveman` | Estilo de comunicação padrão: terse, sem filler. |

Invocar `powerbi-modeling` + `powerbi-expert` juntas antes de mexer no modelo. Ler [[DESING - Contrato Visual]] antes de mexer no relatório.

## MCP `powerbi-modeling-mcp`

Caminho preferencial: opera no modelo **vivo** aberto no Desktop. Ver [[MCP (Conceito)]].

```
connection_operations(operation: "ListLocalInstances")
connection_operations(operation: "Connect")
model_operations(operation: "Get")
table_operations / relationship_operations / measure_operations
```

> [!WARNING]
> Verificar se o MCP está carregado (`ToolSearch` por `connection_operations`). Já esteve configurado com escopo de projeto em outra pasta. Para adicionar:
> `claude mcp add powerbi-modeling-mcp --scope user -- npx -y @microsoft/powerbi-modeling-mcp@latest --start`
> Reiniciar a sessão depois.

## Fallbacks

1. **Editar TMDL direto** em `definition/tables/*.tmdl` + `ref table` em `model.tmdl`. Usuário atualiza no Desktop.
2. **Leitura via ADOMD** (só consulta). Porta do `msmdsrv` é dinâmica:

```powershell
$pid = (Get-Process msmdsrv).Id
$port = (Get-NetTCPConnection -OwningProcess $pid -State Listen)[0].LocalPort
Add-Type -Path "C:\Program Files\Microsoft.NET\ADOMD.NET\160\Microsoft.AnalysisServices.AdomdClient.dll"
$cn = New-Object Microsoft.AnalysisServices.AdomdClient.AdomdConnection("Data Source=localhost:$port")
$cn.Open()
```

Com a conexão: `EVALUATE INFO.VIEW.TABLES()` / `INFO.VIEW.RELATIONSHIPS()` / `INFO.VIEW.MEASURES()` para conferir disco × memória.
