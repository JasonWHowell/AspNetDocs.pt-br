---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: Use controladores e visualizações para implementar uma ui de listagem/detalhes | Microsoft Docs
author: rick-anderson
description: O passo 4 mostra como adicionar um Controlador ao aplicativo que aproveita nosso modelo para fornecer aos usuários uma experiência de navegação de listagem/detalhes de dados...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541306"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>Usar controladores e exibições para implementar uma interface do usuário de listagem/detalhes

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 4 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O passo 4 mostra como adicionar um Controlador ao aplicativo que aproveita nosso modelo para fornecer aos usuários uma experiência de navegação de listagem/detalhes de dados para jantares em nosso site NerdDinner.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner Passo 4: Controladores e Visualizações

Com frameworks web tradicionais (ASP clássico, PHP, ASP.NET Formulários da Web, etc),as URLs de entrada são tipicamente mapeadas para arquivos em disco. Por exemplo: uma solicitação de uma URL como "/Products.aspx" ou "/Products.php" pode ser processada por um arquivo "Products.aspx" ou "Products.php".

As estruturas MVC baseadas na Web mapeiam URLs para código de servidor de uma maneira ligeiramente diferente. Em vez de mapear URLs de entrada para arquivos, eles, em vez disso, mapeiam URLs para métodos em classes. Essas classes são chamadas de "Controladores" e são responsáveis por processar as solicitações HTTP recebidas, lidar com a entrada do usuário, recuperar e salvar dados e determinar a resposta para enviar de volta ao cliente (exibir HTML, baixar um arquivo, redirecionar para uma URL diferente, etc).

Agora que construímos um modelo básico para o nosso aplicativo NerdDinner, nosso próximo passo será adicionar um Controller ao aplicativo que aproveita para fornecer aos usuários uma experiência de navegação de listagem/detalhes de dados para jantares em nosso site.

### <a name="adding-a-dinnerscontroller-controller"></a>Adicionando um controlador dinnerscontroller

Começaremos clicando com o botão direito do mouse na pasta "Controladores" dentro do nosso projeto web e, em seguida, selecionaremos o comando **&gt;'Adicionar-Controlador'** (você também pode executar este comando digitando Ctrl-M, Ctrl-C):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

Isso trará a caixa de diálogo "Adicionar controlador":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

Nomearemos o novo controlador de "DinnersController" e clicaremos no botão "Adicionar". O Visual Studio adicionará um arquivo DinnersController.cs em nosso diretório \Controllers:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

Ele também abrirá a nova classe DinnersController dentro do editor de código.

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>Adicionando métodos de ação de índice() e detalhes() à classe DinnersController

Queremos permitir que os visitantes que usam nosso aplicativo naveguem em uma lista de jantares próximos e permitir que eles cliquem em qualquer jantar da lista para ver detalhes específicos sobre ele. Faremos isso publicando as seguintes URLs do nosso aplicativo:

| **URL** | **Finalidade** |
| --- | --- |
| */Jantares/* | Exibir uma lista HTML de jantares próximos |
| */Jantares/Detalhes/[id]* | Exibir detalhes sobre um jantar específico indicado por um parâmetro de "id" incorporado na URL – que corresponderá ao DinnerID do jantar no banco de dados. Por exemplo: /Dinners/Details/2 exibiria uma página HTML com detalhes sobre o Jantar cujo valor de DinnerID é 2. |

Publicaremos implementações iniciais desses URLs adicionando dois "métodos de ação" públicos à nossa classe DinnersController como abaixo:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

Em seguida, executaremos o aplicativo NerdDinner e usaremos nosso navegador para invocá-los. Digitar a URL *"/Dinners/"* fará com que nosso método *Index()* seja executado e enviará de volta a seguinte resposta:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

Digitar a URL *"/Dinners/Details/2"* fará com que nosso método *Detalhes()* seja executado e envie de volta a seguinte resposta:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

Você deve estar se perguntando - como ASP.NET MVC sabia para criar nossa classe DinnersController e invocar esses métodos? Para entender isso, vamos dar uma olhada rápida em como o roteamento funciona.

### <a name="understanding-aspnet-mvc-routing"></a>Entendendo ASP.NET roteamento MVC

ASP.NET MVC inclui um poderoso mecanismo de roteamento de URL que fornece muita flexibilidade no controle de como as URLs são mapeadas para as classes de controlador. Ele nos permite personalizar completamente como ASP.NET MVC escolhe qual classe de controlador criar, qual método invocar nele, bem como configurar diferentes maneiras de que as variáveis possam ser automaticamente analisados a partir da URL/Querystring e passados para o método como argumentos de parâmetro. Ele oferece a flexibilidade para otimizar totalmente um site para SEO (otimização do mecanismo de pesquisa), bem como publicar qualquer estrutura de URL que queremos de um aplicativo.

Por padrão, novos projetos de ASP.NET MVC vêm com um conjunto pré-configurado de regras de roteamento de URL já registradas. Isso nos permite começar facilmente em um aplicativo sem ter que configurar explicitamente nada. Os registros de regras de roteamento padrão podem ser encontrados na classe "Aplicativo" de nossos projetos – que podemos abrir clicando duas vezes no arquivo "Global.asax" na raiz do nosso projeto:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

As regras de roteamento de MVC ASP.NET padrão são registradas no método "RegisterRoutes" desta classe:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

As "rotas". MapRoute()" chamada de método acima registra uma regra de roteamento padrão que mapeia URLs de entrada para classes de controlador usando o formato URL: "/{controller}/{action}/{id}" – onde "controller" é o nome da classe controladora para instanciar, "ação" é o nome de um método público para invocar nele, e "id" é um parâmetro opcional incorporado na URL que pode ser passado como um argumento para o método. O terceiro parâmetro passado para a chamada do método "MapRoute()" é um conjunto de valores padrão para usar para os valores de controlador/ação/id no caso de não estarem presentes na URL (Controller = "Home", Action="Index", Id=").

Abaixo está uma tabela que demonstra como uma variedade de URLs são mapeadas usando a regra de rota padrão "<em>/{controllers}/{action}/{id}":</em>

| **URL** | **Classe controladora** | **Método de ação** | **Parâmetros passados** |
| --- | --- | --- | --- |
| */Jantares/Detalhes/2* | JantaresController | Detalhes (id) | id=2 |
| */Jantares/Edição/5* | JantaresController | Editar (id) | id=5 |
| */Jantares/Criar* | JantaresController | Criar() | N/D |
| */Jantares* | JantaresController | Índice( () | N/D |
| */home* | Homecontroller | Índice( () | N/D |
| */* | Homecontroller | Índice( () | N/D |

As últimas três linhas mostram os valores padrão (Controlador = Home, Ação = Índice, Id = "") sendo utilizados. Como o método "Index" é registrado como o nome de ação padrão se não for especificado, os URLs "/Jantares" e "/Home" fazem com que o método de ação Index() seja invocado em suas classes de Controlador. Como o controlador "Home" é registrado como controlador padrão se não for especificado, a URL "/" faz com que o HomeController seja criado e o método de ação Index() nele seja invocado.

Se você não gosta dessas regras de roteamento de URL padrão, a boa notícia é que elas são fáceis de alterar - basta editá-las dentro do método RegisterRoutes acima. Para o nosso aplicativo NerdDinner, porém, não vamos alterar nenhuma das regras de roteamento de URL padrão – em vez disso, usaremos-as como estão.

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>Usando o DinnerRepository do nosso DinnersController

Vamos agora substituir nossa implementação atual dos métodos de ação Index() e Details() do DinnersController por implementações que usam nosso modelo.

Usaremos a aula de DinnerRepository que construímos antes para implementar o comportamento. Começaremos adicionando uma declaração de "uso" que faz referência ao namespace "NerdDinner.Models" e, em seguida, declararemos uma instância do nosso DinnerRepository como um campo em nossa classe DinnerController.

Mais tarde, neste capítulo, introduziremos o conceito de "Injeção de Dependência" e mostraremos outra maneira de nossos controladores obterem uma referência a um DinnerRepository que permite melhores testes unitários – mas por enquanto vamos criar apenas uma instância do nosso DinnerRepository inline como abaixo.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

Agora estamos prontos para gerar uma resposta HTML de volta usando nossos objetos de modelo de dados recuperados.

### <a name="using-views-with-our-controller"></a>Usando visualizações com nosso controlador

Embora seja possível escrever código dentro de nossos métodos de ação para montar HTML e, em seguida, usar o método de ajuda *Response.Write()* para enviá-lo de volta ao cliente, essa abordagem torna-se bastante desordenada rapidamente. Uma abordagem muito melhor é para que executemos apenas a lógica de aplicação e dados dentro de nossos métodos de ação DinnersController e, em seguida, passe os dados necessários para renderizar uma resposta HTML a um modelo de "visualização" separado que é responsável por superar a representação HTML dele. Como veremos em um momento, um modelo de "exibição" é um arquivo de texto que normalmente contém uma combinação de marcação HTML e código de renderização incorporado.

Separar nossa lógica de controlador da nossa visão de renderização traz vários grandes benefícios. Em particular, ajuda a impor uma clara "separação de preocupações" entre o código do aplicativo e o código de formatação/renderização de interface do usuário. Isso torna muito mais fácil testar a lógica do aplicativo em isolamento da lógica de renderização da interface do iu. Torna mais fácil modificar posteriormente os modelos de renderização de interface do usuário sem ter que fazer alterações no código do aplicativo. E isso pode tornar mais fácil para desenvolvedores e designers colaborarem juntos em projetos.

Podemos atualizar nossa classe DinnersController para indicar que queremos usar um modelo de exibição para enviar de volta uma resposta HTML UI alterando as assinaturas do método de nossos dois métodos de ação de ter um tipo de retorno de "vazio" para, em vez disso, ter um tipo de retorno de "ActionResult". Em seguida, podemos chamar o método de ajuda *'Exibir',* na classe base do Controlador, para retornar um objeto "ViewResult" como abaixo:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

A assinatura do método de ajuda *View()* que estamos usando acima parece abaixo:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

O primeiro parâmetro para o método de ajuda *Exibir()* é o nome do arquivo de modelo de exibição que queremos usar para renderizar a resposta HTML. O segundo parâmetro é um objeto modelo que contém os dados que o modelo de exibição precisa para renderizar a resposta HTML.

Dentro do nosso método de ação Index() estamos chamando o método de ajuda *View()* e indicando que queremos renderizar uma lista HTML de jantares usando um modelo de exibição "Index". Estamos passando o modelo de exibição de uma seqüência de objetos do Jantar para gerar a lista a partir de:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

Dentro do nosso método de ação Details() tentamos recuperar um objeto Dinner usando o id fornecido dentro da URL. Se um jantar válido for encontrado, chamamos o método de ajuda *'Exibir',* indicando que queremos usar um modelo de exibição "Detalhes" para renderizar o objeto Jantar recuperado. Se um jantar inválido for solicitado, renderizamos uma mensagem de erro útil que indica que o Jantar não existe usando um modelo de exibição "NotFound" (e uma versão sobrecarregada do método de ajuda *'Exibir()* que apenas leva o nome do modelo):

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

Vamos agora implementar os modelos de exibição "NotFound", "Details" e "Index".

### <a name="implementing-the-notfound-view-template"></a>Implementando o modelo de exibição "Não encontrado"

Começaremos implementando o modelo de exibição "NotFound" – que exibe uma mensagem de erro amigável indicando que o jantar solicitado não pode ser encontrado.

Criaremos um novo modelo de exibição posicionando nosso cursor de texto dentro de um método de ação do controlador e, em seguida, clique com o botão direito do mouse e escolha o comando menu "Adicionar exibição" (também podemos executar este comando digitando Ctrl-M, Ctrl-V):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

Isso trará uma caixa de diálogo "Adicionar visualização" como abaixo. Por padrão, a caixa de diálogo preencherá previamente o nome da exibição para criar para corresponder ao nome do método de ação em que o cursor estava quando a caixa de diálogo foi lançada (neste caso "Detalhes"). Como queremos primeiro implementar o modelo "NotFound", vamos substituir esse nome de exibição e defini-lo como "Não Encontrado":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

Quando clicamos no botão "Adicionar", o Visual Studio criará um novo modelo de exibição "NotFound.aspx" para nós dentro do diretório "\Views\Dinners" (que ele também criará se o diretório ainda não existir):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

Ele também abrirá nosso novo modelo de exibição "NotFound.aspx" dentro do editor de código:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

Exibir modelos por padrão tem duas "regiões de conteúdo" onde podemos adicionar conteúdo e código. O primeiro nos permite personalizar o "título" da página HTML enviada de volta. O segundo nos permite personalizar o "conteúdo principal" da página HTML enviada de volta.

Para implementar nosso modelo de exibição "NotFound", adicionaremos alguns conteúdos básicos:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

Podemos então experimentá-lo dentro do navegador. Para fazer isso, vamos solicitar a URL *"/Jantares/Detalhes/9999".* Isso se refere a um jantar que não existe atualmente no banco de dados e fará com que nosso método de ação DinnersController.Details() torne nosso modelo de exibição "NotFound":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

Uma coisa que você vai notar na captura de tela acima é que nosso modelo básico de visualização herdou um monte de HTML que envolve o conteúdo principal na tela. Isso porque nosso modelo de exibição está usando um modelo de "página mestre" que nos permite aplicar um layout consistente em todas as visualizações do site. Discutiremos como as páginas-mestre funcionam mais em uma parte posterior deste tutorial.

### <a name="implementing-the-details-view-template"></a>Implementação do modelo de exibição "Detalhes"

Vamos agora implementar o modelo de exibição "Detalhes" – que gerará HTML para um único modelo de Jantar.

Faremos isso posicionando nosso cursor de texto dentro do método de ação Detalhes e, em seguida, clique com o botão direito do mouse e escolha o comando menu "Adicionar exibição" (ou pressione Ctrl-M, Ctrl-V):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

Isso trará a caixa de diálogo "Adicionar visualização". Manteremos o nome de exibição padrão ("Detalhes"). Também selecionaremos a caixa de seleção "Criar uma exibição fortemente digitada" na caixa de diálogo e selecionar (usando a lista de entrada da caixa de combinação) o nome do tipo de modelo que estamos passando do Controlador para a Exibição. Para esta visão, estamos passando um objeto dinner (o nome totalmente qualificado para este tipo é: "NerdDinner.Models.Dinner"):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

Ao contrário do modelo anterior, onde escolhemos criar uma "Vista Vazia", desta vez optaremos por "andaime" automaticamente a exibição usando um modelo "Detalhes". Podemos indicar isso alterando a parada "Exibir conteúdo" na caixa de diálogo acima.

"Andaimes" gerará uma implementação inicial do nosso modelo de visualização de detalhes com base no objeto Dinner que estamos passando para ele. Isso fornece uma maneira fácil de começarmos rapidamente a implementação do modelo de visualização.

Quando clicarmos no botão "Adicionar", o Visual Studio criará um novo arquivo de modelo de exibição "Details.aspx" para nós em nosso diretório "\Views\Dinners":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

Ele também abrirá nosso novo modelo de exibição "Details.aspx" dentro do editor de código. Ele conterá uma implementação inicial de andaimes de uma visão de detalhes baseada em um modelo dinner. O motor de andaimes usa a reflexão .NET para olhar as propriedades públicas expostas na classe passada, e adicionará conteúdo apropriado com base em cada tipo encontrado:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

Podemos solicitar a URL *"/Dinners/Details/1"* para ver como é essa implementação de andaimes "detalhes" no navegador. O uso desta URL exibirá um dos jantares que adicionamos manualmente ao nosso banco de dados quando o criamos pela primeira vez:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

Isso nos faz funcionar rapidamente e nos fornece uma implementação inicial de nossa visão Details.aspx. Podemos então ir e ajustá-lo para personalizar a ui para nossa satisfação.

Quando olharmos para o modelo Details.aspx mais de perto, descobriremos que ele contém HTML estático, bem como código de renderização incorporado. &lt;%&gt; % os nuggets de código executam &lt;código&gt; quando o modelo de exibição renderiza, e %= % os nuggets de código executam o código contido neles e, em seguida, tornam o resultado para o fluxo de saída do modelo.

Podemos escrever código dentro da nossa exibição que acessa o objeto modelo "Jantar" que foi passado do nosso controlador usando uma propriedade "Modelo" fortemente digitada. O Visual Studio nos fornece um código-intellisense completo ao acessar essa propriedade "Modelo" dentro do editor:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

Vamos fazer alguns ajustes para que a fonte do nosso modelo de exibição de detalhes finais pareça abaixo:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

Quando acessarmos a URL *"/Jantares/Detalhes/1"* novamente, ela agora renderizará como abaixo:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>Implementação do modelo de exibição "Index"

Vamos agora implementar o modelo de exibição "Index" – que irá gerar uma listagem de jantares próximos. Para fazer isso, posicionaremos nosso cursor de texto dentro do método de ação Índice e, em seguida, clicare com o botão direito do mouse e escolha o comando menu "Adicionar exibição" (ou pressione Ctrl-M, Ctrl-V).

Na caixa de diálogo "Adicionar exibição", manteremos o modelo de exibição chamado "Index" e selecionaremos a caixa de seleção "Criar uma exibição fortemente digitada". Desta vez, escolheremos gerar automaticamente um modelo de exibição "Lista" e selecionar "NerdDinner.Models.Dinner" à medida que o tipo de modelo passou para a exibição (o que, por termos indicado, estamos criando um andaime "Lista" fará com que o diálogo Add View assuma que estamos passando uma seqüência de objetos do Jantar do nosso Controlador para a Exibição):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

Quando clicarmos no botão "Adicionar", o Visual Studio criará um novo arquivo de modelo de exibição "Index.aspx" para nós dentro do nosso diretório "\Views\Dinners". Ele vai "andaime" uma implementação inicial dentro dele que fornece uma lista de tabela HTML dos Jantares que passamos para a exibição.

Quando executarmos o aplicativo e acessarmos a URL *"/Jantares/"* ela renderizará nossa lista de jantares assim:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

A solução de tabela acima nos dá um layout em forma de grade de nossos dados do Jantar – que não é exatamente o que queremos para o nosso consumidor que enfrenta a lista do Jantar. Podemos atualizar o modelo de exibição Index.aspx e modificá-lo para listar menos colunas de dados e usar um &lt;elemento ul&gt; para torná-los em vez de uma tabela usando o código abaixo:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

Estamos usando a palavra-chave "var" dentro da declaração acima para cada declaração enquanto nos demos a volta sobre cada jantar em nosso Modelo. Aqueles que não estão familiarizados com c # 3.0 podem pensar que usar "var" significa que o objeto do jantar está atrasado. Em vez disso, significa que o compilador está usando a inferência de tipo contra a propriedade&lt;&gt;"Modelo" fortemente digitada (que é do tipo "Jantar IEnumerable") e compilando a variável local "jantar" como um tipo de Jantar – o que significa que temos total intellisense e verificação de tempo de compilação para ele dentro de blocos de código:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

Quando batemos na atualização da URL */Dinners* em nosso navegador nossa visualização atualizada agora parece abaixo:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

Isso parece melhor – mas ainda não está totalmente lá. Nosso último passo é permitir que os usuários finais cliquem em Jantares individuais na lista e vejam detalhes sobre eles. Vamos implementar isso renderizando elementos de hiperlink HTML que se ligam ao método de ação Detalhes em nosso DinnersController.

Podemos gerar esses hiperlinks dentro da nossa visão de Índice de duas maneiras. A primeira é criar &lt;manualmente HTML um&gt; elemento &lt;como&gt; abaixo, &lt;onde&gt; incorporamos % % de blocos dentro do elemento HTML:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

Uma abordagem alternativa que podemos usar é tirar proveito do método de ajuda incorporado "Html.ActionLink()" dentro &lt;&gt; ASP.NET MVC que suporta a criação programática de um HTML um elemento que se vincula a outro método de ação em um Controlador:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

O primeiro parâmetro para o método de ajuda Html.ActionLink é o link-texto a ser exibido (neste caso o título do jantar), o segundo parâmetro é o nome de ação Controller para o qual queremos gerar o link (neste caso o método Detalhes), e o terceiro parâmetro é um conjunto de parâmetros para enviar à ação (implementado como um tipo anônimo com nome/valores da propriedade). Neste caso, estamos especificando o parâmetro "id" do jantar ao qual queremos vincular, e como a regra de roteamento de URL padrão no mVC ASP.NET é "{Controller}/{Action}/{id}" o método de ajuda Html.ActionLink() gerará a seguinte saída:

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

Para nossa exibição Index.aspx, usaremos a abordagem do método de ajuda Html.ActionLink() e teremos cada jantar no link da lista para os detalhes apropriados URL:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

E agora, quando chegamos à *URL /Dinners* nossa lista de jantares parece abaixo:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

Quando clicarmos em qualquer um dos Jantares na lista, navegaremos para ver detalhes sobre ele:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>Nomeação baseada em convenções e a estrutura do diretório \Views

ASP.NET aplicativos MVC por padrão usam uma estrutura de nomeação de diretório baseada em convenções ao resolver modelos de exibição. Isso permite que os desenvolvedores evitem ter que qualificar totalmente um caminho de localização ao referenciar visualizações de uma classe Controller. Por padrão, ASP.NET O MVC procurará o\[arquivo de\* modelo de exibição dentro do diretório *\Views ControllerName] abaixo do aplicativo.

Por exemplo, estamos trabalhando na classe DinnersController – que faz referência explícita a três modelos de exibição: "Index", "Details" e "NotFound". ASP.NET MVC procurará por padrão essas exibições no diretório *\Views\Dinners* abaixo do nosso diretório raiz do aplicativo:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

Observe acima como existem atualmente três classes de controlador dentro do projeto (DinnersController, HomeController e AccountController – as duas últimas foram adicionadas por padrão quando criamos o projeto), e há três subdiretórios (um para cada controlador) dentro do diretório \Views.

As exibições referenciadas dos controladores Home e Accounts resolverão automaticamente seus modelos de exibição dos respectivos *diretórios \Views\Home* e *\Views\Account.* O *subdiretório \Views\Shared* fornece uma maneira de armazenar modelos de exibição que são reutilizados em vários controladores dentro do aplicativo. Quando ASP.NET MVC tentar resolver um modelo de exibição, ele primeiro verificará dentro do diretório específico *\[\Views Controller]* e se não conseguir encontrar o modelo de exibição lá, ele será exibido dentro do *diretório \Views\Shared.*

Quando se trata de nomear modelos de exibição individuais, a orientação recomendada é fazer com que o modelo de exibição compartilhe o mesmo nome do método de ação que o fez renderizar. Por exemplo, acima do nosso método de ação "Index" está usando a exibição "Index" para renderizar o resultado da exibição, e o método de ação "Detalhes" está usando a exibição "Detalhes" para renderizar seus resultados. Isso facilita a veja rapidamente qual modelo está associado a cada ação.

Os desenvolvedores não precisam especificar explicitamente o nome do modelo de exibição quando o modelo de exibição tiver o mesmo nome do método de ação que está sendo invocado no controlador. Em vez disso, podemos simplesmente passar o objeto modelo para o método de ajuda "Exibir()" (sem especificar o nome da exibição), e ASP.NET MVC inferirá automaticamente que queremos usar o modelo de exibição *Do Nome do Controlador de \Visualizações]\[\[* no disco para renderiza-lo.

Isso nos permite limpar um pouco nosso código do controlador e evitar duplicar o nome duas vezes em nosso código:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

O código acima é tudo o que é necessário para implementar uma boa experiência de listagem/detalhes do Jantar para o site.

#### <a name="next-step"></a>Próxima etapa

Agora temos uma boa experiência de navegação no jantar construída.

Vamos agora ativar o suporte de edição de formulários de formulário crud (Create, Read, Update, Delete).

> [!div class="step-by-step"]
> [Próximo](build-a-model-with-business-rule-validations.md)
> [anterior](provide-crud-create-read-update-delete-data-form-entry-support.md)
