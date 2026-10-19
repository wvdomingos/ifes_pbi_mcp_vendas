---
title: "Design do relatório Power BI — IFES Comércio Exterior"
tags:
  - power-bi
  - ifes
  - comercio-exterior
  - design
date: 2026-10-19
status: proposta
---

# Design do relatório Power BI — IFES Comércio Exterior

Guia para construir páginas em [[Power BI]] para o evento de [[Comércio Exterior]], tomando como referência visual `assets/background_ifes_comercio_exterior_16x9_v1.png`. A imagem representa conexões globais e atividade portuária; o relatório deve transmitir clareza, dinamismo e rigor analítico, com fundo claro e identidade predominantemente verde. Não adicionar logotipo nem atribuir valores ou indicadores sem fonte confirmada.

## 1. Identidade visual e cores

A referência possui centro quase branco, verdes suaves no globo e em circuitos, verde profundo na base e pontos amarelos. Os valores abaixo são **aproximações visuais**, não uma especificação institucional oficial. Na imagem, foram amostrados `#FEFEFE` no centro, `#0E543A` no verde escuro, `#88CE81` no verde claro e `#FBE76F` no amarelo. Os demais valores são derivados para legibilidade e funções semânticas.

| Token | Cor | Aplicação |
|---|---|---|
| Fundo da página | `#F2FAF1` | Alternativa clara quando a imagem não estiver disponível |
| Superfície | `#FFFFFF` | Cards, área de gráficos, tabelas e filtros |
| Texto principal / título | `#0B4F35` | Títulos, valores principais e texto sobre superfícies claras |
| Texto secundário | `#475D52` | Contexto, unidades, rótulos e fontes |
| Verde primário | `#176B3A` | Série principal, botão primário e estado positivo |
| Verde complementar | `#167D3F` | Segunda ênfase verde e borda de foco |
| Verde claro decorativo | `#88CE81` | Detalhes não essenciais; não usar para texto ou série isolada sobre branco |
| Amarelo de destaque | `#F8E35B` | Pequeno marcador, faixa ou fundo de destaque; texto sempre verde escuro |
| Atenção | `#9C6500` | Texto, ícone e marcador de atenção em fundo claro |
| Crítico | `#A4262C` | Texto, ícone e marcador de condição crítica em fundo claro |
| Borda sutil | `#D3E5D5` | Separação decorativa de cards, não usada como único indicador de limite ou foco |

Use amarelo com parcimônia: não o transforme em fundo dominante, cor padrão de série ou texto sobre branco. Empregue vermelho e âmbar apenas quando houver uma regra de negócio válida para o estado.

## 2. Tipografia e hierarquia

Use **Segoe UI**, disponível no ambiente Windows/Power BI; se indisponível, use Arial. Tamanhos iniciais no painel de formatação do Power BI:

| Elemento | Tamanho | Peso e cor |
|---|---:|---|
| Título da página | 26 pt | Semibold, `#0B4F35` |
| Mensagem principal / insight | 18 pt | Semibold, `#0B4F35` |
| Valor de KPI | 28 pt | Semibold, `#0B4F35` |
| Título de visual | 15 pt | Semibold, `#0B4F35` |
| Texto, filtro e rótulo | 12 pt | Regular, `#475D52` ou `#0B4F35` |
| Fonte e contexto secundário | 10 pt | Regular, `#475D52`; ampliar para projeção quando necessário |

Organize a leitura como **insight → contexto → ação**: título que declare a pergunta ou conclusão comprovada; em seguida, indicadores e gráficos que expliquem o contexto; por fim, filtros ou navegação para investigação. A ação deve ser uma possibilidade de exploração, não uma recomendação inventada. Exiba unidade, período e contexto de filtro quando necessários para interpretar números.

## 3. Canvas, grid e fundo

- Configure a página como **16:9, 1280 × 720 px**. A referência tem 1672 × 941 px, aproximadamente 16:9.
- No Power BI Desktop, selecione a página sem visual ativo, abra **Formatar página** e aplique a imagem em **Tela de fundo da página / Canvas background**, com ajuste de imagem e transparência de 0%. Mantenha o papel de parede externo neutro. Os nomes das opções podem variar por versão; confira o resultado no Desktop.
- Preserve a proporção e evite esticar ou cortar informação relevante. Imagem é decorativa: não a utilize para transmitir dados nem cubra texto com detalhes do globo, porto ou faixas.
- Use margem externa de 32 px, 12 colunas de aproximadamente 90 px com intervalos de 12 px e espaçamento vertical de 16 px. Dentro dos cards, reserve 16 px. Alinhe bordas e mantenha uma área de respiro entre o título e os indicadores.
- Distribuição inicial: cabeçalho até 80 px; indicadores em uma faixa de 112 px; área analítica entre aproximadamente `y = 216` e `y = 632`; rodapé/contexto até `y = 688`. Ajuste ao conteúdo real sem sobrepor os elementos.
- Coloque visuais sobre superfícies brancas opacas, sobretudo onde a imagem tiver detalhes. Não dependa da transparência sobre o fundo para alcançar contraste. Use borda sutil ou separação pelo espaçamento; não obscureça a imagem inteira desnecessariamente.
- Quando o formato ou a projeção comprometer a leitura, substitua a imagem nessa página por `#F2FAF1` e mantenha os demais tokens.

## 4. Componentes

### Cards e KPIs

Fundo `#FFFFFF`, borda `#D3E5D5` de 1 px, cantos de 4 px e sem sombra forte. Alinhe o rótulo à esquerda, o valor logo abaixo e a unidade junto ao valor. Inclua comparação ou variação somente se a medida e a base comparativa estiverem disponíveis. Use de 3 a 4 cards por linha quando houver espaço; não preencha a página com indicadores sem relação com a pergunta.

### Filtros e botões

Filtros em superfície branca, título e opções em verde escuro, com altura mínima de 40 px e rótulo explícito. Exiba o estado selecionado por texto ou marcação, além da cor; se houver seleção múltipla, torne-a visível. Botão primário: fundo `#176B3A`, texto branco, altura mínima de 40 px e largura adequada ao rótulo. Botão secundário: fundo branco, texto e contorno `#176B3A`. O foco deve ser visível com contorno `#167D3F` de 2 px, sem depender apenas da mudança de cor. Descreva ações reais, como “Limpar filtros”, apenas quando configuradas e testadas.

### Tabelas e matrizes

Cabeçalho branco ou `#F2FAF1`, texto `#0B4F35` semibold; corpo branco e texto `#475D52`, com linhas divisórias discretas. Alinhe números à direita e textos à esquerda; preserve casas decimais e unidades adequadas à medida. Formatação condicional deve combinar cor com sinal, ícone ou texto e respeitar a regra de negócio. Totais precisam estar identificados e ser semanticamente válidos.

### Gráficos e séries

Escolha o visual conforme a pergunta: barras para comparar categorias; linhas para evolução temporal; matriz para detalhe; mapa apenas com localização confiável. Evite 3D, excesso de rótulos e eixos truncados que distorçam comparações. Mantenha rótulos legíveis, legenda próxima e escala/unidade explícitas. Para barras, inicie o eixo quantitativo em zero; em linhas, justifique recortes de escala.

Para séries categóricas, use esta ordem inicial e mantenha a mesma associação categoria-cor entre páginas: `#176B3A`, `#456D95`, `#725A91`, `#956132`, `#475D52`. Todas atingem pelo menos 3:1 contra branco. Use padrão de linha, rótulo direto ou legenda também: contraste com o fundo não garante distinção entre séries ou acessibilidade para daltonismo. Reserve amarelo para anotações pequenas e não para uma série essencial sobre branco. Ordene categorias por valor quando a comparação exigir ranking e por tempo quando houver sequência temporal.

### Estados semânticos

| Estado | Cor em branco / fundo claro | Identificação adicional |
|---|---|---|
| Positivo | `#176B3A` | Texto “Positivo” ou ícone apropriado |
| Atenção | `#9C6500` | Texto “Atenção” e ícone de alerta |
| Crítico | `#A4262C` | Texto “Crítico” e ícone de alerta |
| Neutro / sem avaliação | `#475D52` | Texto “Neutro” ou “Sem avaliação” |

Defina limiares a partir da fonte ou de regra aprovada. Na ausência deles, mantenha o estado neutro; não classifique automaticamente uma variação como boa ou ruim.

## 5. Acessibilidade e contraste

Pares calculados pela razão de luminância relativa WCAG em cores sólidas, arredondados a duas casas. Texto normal deve atingir **4,5:1** e elementos gráficos/controles essenciais, **3:1** contra o fundo adjacente. Transparência, antisserrilhamento, imagem e interação podem alterar a aparência; valide no relatório renderizado.

| Primeiro plano | Fundo | Razão | Uso |
|---|---|---:|---|
| `#0B4F35` | `#FFFFFF` | 9,62:1 | Texto e títulos |
| `#0B4F35` | `#F2FAF1` | 9,03:1 | Texto e títulos |
| `#475D52` | `#FFFFFF` | 7,11:1 | Texto secundário |
| `#176B3A` | `#FFFFFF` | 6,56:1 | Texto, série e contorno |
| `#FFFFFF` | `#176B3A` | 6,56:1 | Texto em botão primário |
| `#167D3F` | `#FFFFFF` | 5,20:1 | Foco e elemento gráfico |
| `#9C6500` | `#F2FAF1` | 4,61:1 | Texto de atenção |
| `#A4262C` | `#FFFFFF` | 7,26:1 | Texto crítico |
| `#F8E35B` | `#FFFFFF` | 1,30:1 | Apenas decoração, insuficiente para texto ou gráfico essencial |

Não use cor como único canal de informação. Forneça título e texto alternativo úteis para cada visual, ordem de navegação coerente, foco identificável e rótulos compreensíveis. Teste navegação por teclado, seleção dos filtros, leitura em projeção e visualização ampliada. Confirme contraste para novos pares, inclusive estados de interação e elementos sobre a imagem.

## 6. Instruções para uma IA implementadora

1. Leia esta especificação e inspecione a imagem de referência antes de compor a página; preserve seu arquivo original.
2. Configure o canvas e aplique os tokens e componentes acima no Power BI. Confirme visualmente o enquadramento do fundo e mantenha dados sobre superfícies opacas claras.
3. Identifique perguntas, fontes, campos, unidades e filtros disponíveis antes de criar visuais. Não crie números, metas, interpretações, brasão ou logotipo fictícios.
4. Construa a hierarquia insight → contexto → ação com base nos dados reais. Uma conclusão no título só pode aparecer quando os dados e filtros a sustentarem.
5. Preserve a associação de cores das séries e configure títulos, unidades, estados e navegação conforme as regras acima. Não suponha que a cor seja a única maneira de interpretar um visual.
6. Verifique o arquivo em Desktop e em apresentação, com filtros ativos e sem dados; documente qualquer limitação ou decisão que dependa de validação do responsável.

## 7. Checklist de validação

- [ ] Página 16:9 e imagem proporcional, sem texto sobre detalhes de baixo contraste.
- [ ] Paleta clara aplicada; títulos verdes escuros e amarelo restrito a destaque.
- [ ] Texto e controles essenciais atendem aos contrastes definidos, inclusive nos estados de foco e seleção.
- [ ] Cada visual tem título, unidade, período e contexto necessários; texto alternativo e navegação por teclado revisados.
- [ ] Séries distinguíveis por cor e outro recurso; cores consistentes entre páginas.
- [ ] Filtros e botões executam as ações indicadas; estado selecionado é compreensível.
- [ ] Estados positivo, atenção e crítico obedecem a regras confirmadas; sem dados ou limiares inventados.
- [ ] Texto e valores permanecem legíveis em projeção e sem cortes; superfícies não ocultam informação.
- [ ] Fontes, cálculos e números conferidos com a base efetivamente disponibilizada.
