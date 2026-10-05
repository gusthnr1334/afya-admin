# Afya Admin — Dashboard com Blazor WebAssembly e MudBlazor

## Identificação

| | |
|---|---|
| **Aluno(a)** | Gustavo Henrique Neves de Queiroz |
| **Matrícula** | 2637851 |
| **Faculdade** | Afya São Lucas |
| **Curso** | Ciência da computação |
| **Disciplina** | Programação para sistemas web |
| **Professor(a)** | Liluyoud Lacerda |
| **Semestre** | 2026.2 |

## Objetivo do projeto

É basicamente uma página de dashboard, ou como na própria atividade diz, um painel administrativo totalmente fictício feito especialmente pra essa atividade em questão, plataforma fictícia se chama "Afya Pedagógico". O objetivo dessa atividade foi basicamente mesclar diversas coisas que aprendemos nesse primeiro bimestre e fazer com que tenhamos uma profundidade e relação maior com dotnet github vscode e entre outra aplicações e comandos que precisamos pelo menos ter noção de como funcionam.

## Tecnologias utilizadas

- .NET 10 / Blazor WebAssembly
- MudBlazor 9
- VScode 

## Como executar

Passo a passo para outra pessoa clonar e rodar o projeto:

```bash
git clone https://github.com/gusthnr1334/afya-admin.git
cd afya-admin
dotnet watch
```

A versão 10. do .NET SDK é necessária.

## Telas

### Tema claro
<img width="1917" height="958" alt="image" src="https://github.com/user-attachments/assets/be3e18aa-e1f5-4fc5-b95d-08dae5cfaebe" />


### Tema escuro
<img width="1917" height="962" alt="image" src="https://github.com/user-attachments/assets/3f35789a-e23a-4d96-b933-6584183e713a" />


### Versão mobile
<img width="1021" height="961" alt="image" src="https://github.com/user-attachments/assets/64e26410-562e-403c-a79e-88c34ab14151" />


### HTML gerado (DevTools)
<img width="1917" height="962" alt="image" src="https://github.com/user-attachments/assets/c36481ee-0dbf-4df9-8dc1-ed928cf47919" />

Inspecionei no DevTools o botão do menu lateral (hambúrguer) do MudAppBar, que no código é um MudIconButton com o ícone Icons.Material.Filled.Menu, o mudblazor converteu ele em um <button> com um <span class="mud-icon-button-label"> e dentro dele, um <svg> de 24×24 px. O botão fica dentro de header.mud-appbar --> div.mud-toolbar, seguido de um hr divisor vertical e do nav do breadcrumb, e as classes que apareceram foram mud-button-root, mud-icon-button, mud-inherit-text, mud-ripple e mud-icon-button-edge-start no botão (esta última vem do Edge="Edge.Start"), e mud-icon-root, mud-svg-icon e mud-icon-size-medium no ícone, e no divisor aparecem as classes utilitárias mx-3 my-3, que foram escritas no código.


## Estrutura do projeto
<img width="435" height="655" alt="image" src="https://github.com/user-attachments/assets/c833ff93-12f5-4ec0-8516-f30306055755" />


--> Aqui nos temos as principais pastas do projeto. Abaixo seus papeis no projeto:

1. A components são peças reutilizáveis que são usadas nas páginas, como por exemplo, num dos desafios do projeto nós tínhamos que reutiliza-las em outras páginas sem ser a principal.

2. A data guarda os modelos de dados e os dados fictícios que alimentam a interface, sem nenhum código visual. No projeto, o DashboardData.cs define os records e as listas com os valores exibidos no Dashboard.

3. A pasta Layout contém a estrutura que vai ser utilizada em todas as páginas, como a área que tem conteúdo, barra de pesquisa, barra lateral.

4. A pages contém as páginas da aplicação, ou seja, os componentes que têm uma URL própria, declarada com o @page. No projeto, o Dashboard responde em / e a página de Clientes em /clientes.

5. A wwwroot contém arquivos estáticos, entregues diretamente ao navegador sem passar pelo C#, nela ficam o index.html, arquivos de CSS e imagens, como a foto do avatar, só o que está em wwwroot pode ser acessado por URL.


## Componentes criados

| Componente | Responsabilidade | Parâmetros que recebe |
|---|---|---|
| `DashboardCard` | Card base reutilizável (`MudPaper`) com título, subtítulo, ações, menu de três pontos opcional e área de conteúdo. | `Titulo`, `Subtitulo`, `Acoes`, `Menu`, `ChildContent` |
| `KpiCard` | Exibe um indicador (KPI) com título, valor, variação e mini-gráfico de tendência. | `Kpi` (`Kpi`) |
| `AtividadesRecentes` | Lista as últimas atividades da plataforma (quem fez o quê e quando). | `Atividades` (`List<Atividade>`) |
| `CabecalhoPagina` | Cabeçalho padrão das páginas, com título, subtítulo e área para botões de ação. | `Titulo`, `Subtitulo`, `Acoes` |
| `GraficoDistribuicaoClientes` | Gráfico de rosca com a distribuição dos clientes por segmento e o total no centro. | `Total` (`int`), `Segmentos` (`List<SegmentoCliente>`) |
| `GraficoReceita` | Gráfico de linha que compara a receita mensal com a meta. | `Meses` (`string[]`), `Receita` (`double[]`), `Meta` (`double[]`) |
| `PerformanceProjetos` | Mostra o progresso de cada projeto (percentual e tarefas concluídas/total). | `Projetos` (`List<ProjetoPerformance>`) |
| `ProjetosRecentes` | Tabela dos projetos recentes, com cliente, responsável, status, progresso e prazo. | `Projetos` (`List<ProjetoRecente>`) |
| `SeletorPeriodo` | Menu de seleção do período, que avisa a página quando o usuário escolhe outra opção. | `Opcoes`, `Valor`, `ValorChanged` |

## O que aprendi

1. Como uma aplicação Blazor WebAssembly inicia no navegador? Qual é o papel do `index.html`, da `<div id="app">` e do `Program.cs`?
O navegador abre o index.html, que é só uma casca quase vazia e dentro dele tá uma div com o id "app", que é o espaço onde o Blazor desenha tudo. O Program.cs é quem dá a largada: manda o App ir pra dentro dessa div e registra os serviços, tipo o MudBlazor.

2. Qual é a diferença entre um **Layout**, uma **Page** e um **Component** neste projeto? Dê um exemplo de cada.
é como uma casa. Layout é a estrutura que se repete, com menu e barra do topo (MainLayout). Page é um cômodo com endereço próprio, tipo o Dashboard com a rota "/". Component é um móvel reaproveitável, tipo o DashboardCard.

3. O que é um `RenderFragment` e como o `DashboardCard` usa esse recurso para ser reutilizado por vários cards?
É um buraco que o componente deixa pra você encaixar conteúdo dentro, o DashboardCard cuida da moldura e do título, e cada card coloca o que quiser no buraco (número, gráfico, lista). Um componente só, vários cards diferentes.

4. Como funciona o `@bind-Valor` no `SeletorPeriodo`? Qual é o papel do `ValorChanged`?
É uma via de mão dupla, como se  o pai manda o valor pro filho, e o filho avisa quando muda, e O ValorChanged é esse aviso. Quando o usuário troca o período, o SeletorPeriodo dispara ele com o valor novo, e o pai atualiza a variável.

5. Por que os dados ficam na pasta `Data`, separados dos componentes? Que vantagem isso traz se, no futuro, os dados vierem de uma API?
Pra separar "o que mostrar" de "como mostrar", se os dados passarem a vir de uma API, você troca só a fonte lá e os componentes nem percebem, não precisa mexer em tudo.

6. Como o `MudGrid` com `xs`, `sm` e `lg` faz os cards de KPI se reorganizarem em telas de tamanhos diferentes?
A tela tem 12 colunas, e cada card diz quantas ocupa por tamanho de tela. No celular (xs) ocupa a linha toda, em tela média (sm) cabem dois lado a lado, em tela grande (lg) cabem mais. O navegador escolhe a regra sozinho.

7. Como foi possível estilizar a página inteira sem escrever CSS? Explique o papel do tema (`MudTheme`) e das classes utilitárias.
O MudBlazor já vem com o CSS pronto, o MudTheme é o painel de controle onde você define cores e fontes uma vez só e as classes utilitárias (pa-4, mt-2, d-flex) são atalhos pros ajustes de espaço e alinhamento.

8. Por que o namespace do projeto é `afya_admin` e não `afya-admin`?
Porque em C# o hífen é lido como sinal de menos e quebraria o código. O .NET troca o hífen por underscore automaticamente.


## Dificuldades e soluções

Meus únicos problemas foram na hora de mexer com o dotnet pelo cmd, algumas vez a aba que abria no google bugava e não respondia mais e eu queria ver como a pagina tava deposi de atualizada mas não onseguia, até que entendi direito como funcionava o dotnet watch. E algumas dificuldades com linhas de comnandos na transcrição mas era sempre eu escrevendo algo errado e só me tocando depois.

## Melhorias futuras (opcional)

Acho que melhorias futuras seriam deixar a página mais completas e trocars os dados fictícios por talvez dados reais e realmente iniciar um projeto na prática, no mundo real. só fiz o desafio número 2. Eu tentei fazer o 1 mas não entendi direito, talvez esteja certo.
