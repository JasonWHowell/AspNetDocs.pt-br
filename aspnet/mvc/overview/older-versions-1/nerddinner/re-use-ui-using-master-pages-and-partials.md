---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: Reutilizar a ui usando páginas-mestre e parciais | Microsoft Docs
author: rick-anderson
description: A etapa 7 analisa maneiras de aplicar o 'Princípio SECO' em nossos modelos de exibição para eliminar a duplicação de código, usando modelos de exibição parcial e páginas-mestre.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542593"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>Reutilizar a interface do usuário usando páginas mestras e parciais

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 7 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> A etapa 7 analisa maneiras de aplicar o "Princípio SECO" em nossos modelos de exibição para eliminar a duplicação de código, usando modelos de exibição parcial e páginas-mestre.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner Passo 7: Parciais e Páginas-Mestre

Uma das filosofias de design que ASP.NET MVC abraça é o princípio "Não repita a si mesmo" (comumente referido como "DRY"). Um design DRY ajuda a eliminar a duplicação de código e lógica, o que, em última análise, torna os aplicativos mais rápidos de construir e mais fáceis de manter.

Já vimos o princípio DRY aplicado em vários de nossos cenários nerddinner. Alguns exemplos: nossa lógica de validação é implementada dentro da nossa camada de modelo, o que permite que ela seja aplicada tanto editando quanto criar cenários em nosso controlador; estamos reutilizando o modelo de exibição "NotFound" nos métodos de ação Editar, Detalhes e Excluir; estamos usando um padrão de nomeação de convenção com nossos modelos de exibição, o que elimina a necessidade de especificar explicitamente o nome quando chamamos o método de ajuda De exibição() e estamos reutilizando a classe DinnerFormViewModel para cenários de ação Edit e Create.

Vamos agora olhar para maneiras que podemos aplicar o "Princípio SECO" em nossos modelos de exibição para eliminar a duplicação de código lá também.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>Visitando revisitar nossos modelos de edição e criação

Atualmente, estamos usando dois modelos de exibição diferentes – "Edit.aspx" e "Create.aspx" – para exibir nossa ui de formulário de jantar. Uma rápida comparação visual deles destaca o quão semelhantes eles são. Abaixo está como a forma de criação se parece:

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

E aqui está como nossa forma de "Editar" se parece:

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

Não há muita diferença, não é? Além do título e do texto do cabeçalho, o layout do formulário e os controles de entrada são idênticos.

Se abrirmos os modelos de exibição "Edit.aspx" e "Create.aspx", descobriremos que eles contêm layout de formulário idêntico e código de controle de entrada. Essa duplicação significa que acabamos tendo que fazer mudanças duas vezes sempre que introduzimos ou mudamos uma nova propriedade do Jantar - o que não é bom.

### <a name="using-partial-view-templates"></a>Usando modelos de exibição parcial

ASP.NET MVC suporta a capacidade de definir modelos de "exibição parcial" que podem ser usados para encapsular a lógica de renderização de visualização para uma subparte de uma página. As "parciais" fornecem uma maneira útil de definir a lógica de renderização de visualização uma vez e, em seguida, reutilizá-la em vários lugares em um aplicativo.

Para ajudar a "DRY-up" nossa duplicação do modelo edit.aspx e create.aspx view, podemos criar um modelo de exibição parcial chamado "DinnerForm.ascx" que encapsula o layout do formulário e os elementos de entrada comuns a ambos. Faremos isso clicando com o botão direito do mouse no diretório&gt;/Views/Dinners e escolhendo o comando "Adicionar-Exibir":

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

Isso exibirá a caixa de diálogo "Adicionar exibição". Nomearemos a nova exibição que queremos criar "DinnerForm", selecionaremos a caixa de seleção "Criar uma exibição parcial" dentro da caixa de diálogo e indicaremos que passaremos uma classe DinnerFormViewModel:

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

Quando clicarmos no botão "Adicionar", o Visual Studio criará um novo modelo de exibição "DinnerForm.ascx" para nós dentro do diretório "\Views\Dinners".

Podemos então copiar/colar o layout do formulário duplicado / código de controle de entrada do nosso edit.aspx/ Create.aspx exibir modelos em nosso novo modelo de exibição parcial "DinnerForm.ascx":

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

Podemos então atualizar nossos modelos de edição e criação de visualização para chamar o modelo parcial dinnerForm e eliminar a duplicação do formulário. Podemos fazer isso chamando Html.RenderPartial ("DinnerForm") em nossos modelos de exibição:

##### <a name="createaspx"></a>Create.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Você pode qualificar explicitamente o caminho do modelo parcial que deseja ao chamar Html.RenderPartial (por exemplo: ~Views/Dinners/DinnerForm.ascx"). Em nosso código acima, porém, estamos aproveitando o padrão de nomeação baseado em convenções dentro de ASP.NET MVC, e apenas especificando "DinnerForm" como o nome da parcial para renderizar. Quando fizermos isso ASP.NET o MVC olhará primeiro no diretório de visualizações baseado em convenções (para dinnersController isso seria /Views/Dinners). Se ele não encontrar o modelo parcial lá, ele irá procurá-lo no diretório /Views/Compartilhado.

Quando Html.RenderPartial() é chamado apenas com o nome da exibição parcial, ASP.NET MVC passará para a exibição parcial dos mesmos objetos do dicionário Model e ViewData usados pelo modelo de exibição de chamada. Alternativamente, existem versões sobrecarregadas do Html.RenderPartial() que permitem que você passe um objeto modelo alternativo e/ou dicionário ViewData para a exibição parcial a ser usada. Isso é útil para cenários onde você só deseja passar um subconjunto do Modelo/Modelo de Visualização completo.

| **Tópico Lateral: &lt;Por&gt; que &lt;%&gt;% em vez de %= % ? ? ?** |
| --- |
| Uma das coisas sutis que você deve ter notado com &lt;o&gt; código acima &lt;é&gt; que estamos usando um % % de bloco em vez de um %= % de bloqueio ao chamar Html.RenderPartial(). &lt;%=&gt; % os blocos em ASP.NET indicam que um desenvolvedor &lt;deseja renderizar&gt; um valor especificado (por exemplo: %= "Olá" % renderizaria "Olá"). &lt;%&gt; % os blocos indicam que o desenvolvedor deseja executar o código, e que &lt;qualquer saída renderizada dentro deles&gt;deve ser feita explicitamente (por exemplo: % Resposta.Write("Hello") % . A razão pela &lt;qual&gt; estamos usando um % % de bloqueio com o nosso código Html.RenderPartial acima é porque o método Html.RenderPartial() não retorna uma string e, em vez disso, produz o conteúdo diretamente para o fluxo de saída do modelo de exibição de chamada. Ele faz isso por razões de eficiência de desempenho e, ao fazê-lo, evita a necessidade de criar um objeto de cadeia (potencialmente muito grande) temporário. Isso reduz o uso da memória e melhora o throughput geral do aplicativo. Um erro comum ao usar Html.RenderPartial() é esquecer de adicionar um ponto e &lt;vírgula no final da chamada quando estiver dentro de um % de&gt; bloco. Por exemplo, este código causará um &lt;erro de compilador: % Html.RenderPartial ("DinnerForm") %&gt; Você precisa escrever: &lt;% Html.RenderPartial ("DinnerForm"); %&gt; Isto &lt;é&gt; porque % dos blocos são declarações de código independentes, e ao usar as instruções de código C# precisam ser encerradas com um ponto e vírgula. |

### <a name="using-partial-view-templates-to-clarify-code"></a>Usando modelos de exibição parcial para esclarecer código

Criamos o modelo de exibição parcial "DinnerForm" para evitar a duplicação da lógica de renderização de visualização em vários lugares. Esta é a razão mais comum para criar modelos de exibição parcial.

Às vezes ainda faz sentido criar visões parciais mesmo quando elas estão sendo chamadas apenas em um único lugar. Modelos de visualização muito complicados podem muitas vezes se tornar muito mais fáceis de ler quando sua lógica de renderização de visualização é extraída e particionada em um ou mais modelos parciais bem nomeados.

Por exemplo, considere o trecho de código abaixo do arquivo Site.master em nosso projeto (que veremos em breve). O código é relativamente direto para ler – em parte porque a lógica de exibir um link de login/logout no canto superior direito da tela está encapsulada na parcial "LogOnUserControl":

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

Sempre que você se encontrar confuso tentando entender a marcação html/código dentro de um modelo de exibição, considere se não seria mais claro se alguns deles foram extraídos e refatorados em visualizações parciais bem nomeadas.

### <a name="master-pages"></a>Páginas mestras

Além de suportar visualizações parciais, ASP.NET MVC também suporta a capacidade de criar modelos de "página mestre" que podem ser usados para definir o layout comum e html de nível superior de um site. Os controles de espaço reservado de conteúdo podem ser adicionados à página-mestre para identificar regiões substituíveis que podem ser substituídas ou "preenchidas" por visualizações. Isso fornece uma maneira muito eficaz (e SECA) de aplicar um layout comum em um aplicativo.

Por padrão, novos projetos de MVC ASP.NET têm um modelo de página mestre adicionado automaticamente a eles. Esta página-mestre é chamada "Site.master" e vive dentro da pasta \Views\Shared\:

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

O arquivo padrão Site.master parece abaixo. Ele define o html externo do site, juntamente com um menu para navegação na parte superior. Ele contém dois controles de espaço reservado de conteúdo substituíveis – um para o título e outro para onde o conteúdo principal de uma página deve ser substituído:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

Todos os modelos de exibição que criamos para o nosso aplicativo NerdDinner ("Lista", "Detalhes", "Editar", "Criar", "Não Encontrado", etc. Isso é indicado através do atributo "MasterPageFile" que &lt;foi adicionado&gt; por padrão à diretiva superior % @ Page % quando criamos nossas visualizações usando a caixa de diálogo "Adicionar exibição":

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

O que isso significa é que podemos alterar o conteúdo do Site.master e fazer com que as alterações sejam automaticamente aplicadas e usadas quando renderizamos qualquer um de nossos modelos de visualização.

Vamos atualizar nossa seção de cabeçalho do Site.master para que o cabeçalho do nosso aplicativo seja "NerdDinner" em vez de "Meu aplicativo MVC". Vamos também atualizar nosso menu de navegação para que a primeira guia seja "Find a Dinner" (manipulado pelo método de ação Index() do HomeController, e vamos adicionar uma nova guia chamada "Host a Dinner" (tratada pelo método de ação Create() do DinnersController):

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Quando salvarmos o arquivo Site.master e atualizarmos nosso navegador, veremos nossas alterações de cabeçalho aparecerem em todas as visualizações dentro do nosso aplicativo. Por exemplo:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

E com a URL */Dinners/Edit/[id]:*

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>Próxima etapa

Parciais e páginas-mestre fornecem opções muito flexíveis que permitem organizar de forma limpa as visualizações. Você descobrirá que eles ajudam você a evitar a duplicação do conteúdo/código de exibição e tornar seus modelos de visualização mais fáceis de ler e manter.

Vamos agora revisitar o cenário de listagem que construímos anteriormente e habilitar suporte de paginação escalável.

> [!div class="step-by-step"]
> [Próximo](use-viewdata-and-implement-viewmodel-classes.md)
> [anterior](implement-efficient-data-paging.md)
