---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: Implementar paginação eficiente de dados | Microsoft Docs
author: rick-anderson
description: O passo 8 mostra como adicionar suporte de paginação à nossa URL /Dinners para que, em vez de exibir 1000 jantares de uma só vez, só vamos exibir 10 jantares próximos em...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541319"
---
# <a name="implement-efficient-data-paging"></a>Implementar a paginação eficiente de dados

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 8 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O passo 8 mostra como adicionar suporte de paginação à nossa URL /Dinners para que, em vez de exibir 1000 jantares de uma só vez, só exibamos 10 jantares próximos de cada vez - e permitiremos que os usuários finais se page de volta e adiante através de toda a lista de uma maneira amigável seo.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner Passo 8: Suporte à paginação

Se nosso site for bem sucedido, terá milhares de jantares próximos. Precisamos ter certeza de que nossas escalas de iue para lidar com todos esses jantares, e permite que os usuários naveguem por eles. Para habilitar isso, adicionaremos suporte de paginação à nossa URL */Dinners* para que, em vez de exibir 1000 jantares de uma só vez, só exibiremos 10 jantares próximos de cada vez - e permitiremos que os usuários finais voltem e encaminhem para frente toda a lista de uma maneira amigável ao SEO.

### <a name="index-action-method-recap"></a>Recapitulação do método de ação do índice()

O método de ação Index() dentro da nossa classe DinnersController atualmente parece abaixo:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

Quando uma solicitação é feita na URL */Dinners,* ela recupera uma lista de todos os jantares próximos e, em seguida, torna uma lista de todos eles:

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>Entendendo o&lt;T IQueryable&gt;

*IQueryable&lt;&gt; T* é uma interface que foi introduzida com LINQ como parte do .NET 3.5. Ele permite cenários poderosos de "execução diferida" que podemos aproveitar para implementar o suporte de paginação.

Em nosso DinnerRepository estamos retornando uma&lt;&gt; seqüência de jantar iqueryable do nosso método FindUpcomingDinners():

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

O objeto Jantar&lt;&gt; IQueryable retornado pelo nosso método FindUpcomingDinners() encapsula uma consulta para recuperar objetos do Jantar do nosso banco de dados usando LINQ para SQL. É importante ressaltar que ele não executará a consulta contra o banco de dados até tentarmos acessar/iterar sobre os dados na consulta, ou até chamarmos o método ToList() nele. O código que chama nosso método FindUpcomingDinners() pode optar opcionalmente por adicionar operações/filtros adicionais "encadeados" ao objeto Jantar&lt;&gt; IQueryable antes de executar a consulta. LINQ para SQL é então inteligente o suficiente para executar a consulta combinada contra o banco de dados quando os dados são solicitados.

Para implementar a lógica de paginação, podemos atualizar nosso método de ação DinnersController's Index() para que ele&lt;aplique&gt; operadores adicionais "Skip" e "Take" à seqüência de jantar iQueryable retornada antes de chamar toList() nele:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

O código acima pula sobre os primeiros 10 jantares futuros no banco de dados, e depois retorna 20 jantares. LinQ para SQL é inteligente o suficiente para construir uma consulta SQL otimizada que executa essa lógica de pular no banco de dados SQL – e não no servidor web. Isso significa que, mesmo que tenhamos milhões de jantares próximos no banco de dados, apenas os 10 que queremos serão recuperados como parte dessa solicitação (tornando-o eficiente e escalável).

### <a name="adding-a-page-value-to-the-url"></a>Adicionando um valor de "página" à URL

Em vez de codificar um intervalo de página específico, queremos que nossas URLs incluam um parâmetro de "página" que indique qual intervalo de jantar um usuário está solicitando.

#### <a name="using-a-querystring-value"></a>Usando um valor de consulta

O código abaixo demonstra como podemos atualizar nosso método de ação Index() para suportar um parâmetro de consulta string e habilitar URLs como */Dinners?page=2*:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

O método de ação Index() acima tem um parâmetro chamado "page". O parâmetro é declarado como um inteiro anulado (é isso que int? Isso significa que a URL */Dinners?page=2* fará com que um valor de "2" seja passado como o valor do parâmetro. A URL */Dinners* (sem um valor de consulta) fará com que um valor nulo seja passado.

Estamos multiplicando o valor da página pelo tamanho da página (neste caso 10 linhas) para determinar quantos jantares pular. Estamos usando o [operador c# nulo "coalescing" (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) que é útil ao lidar com tipos anulados. O código acima atribui à página o valor de 0 se o parâmetro da página for nulo.

#### <a name="using-embedded-url-values"></a>Usando valores de URL incorporados

Uma alternativa para usar um valor de consulta seria incorporar o parâmetro de página dentro da própria URL real. Por exemplo: */Jantares/Página/2* ou */Jantares/2*. ASP.NET MVC inclui um poderoso mecanismo de roteamento de URL que facilita o suporte a cenários como este.

Podemos registrar regras de roteamento personalizadas que mapeiam qualquer formato de URL ou URL de entrada para qualquer classe de controlador ou método de ação que quisermos. Tudo o que precisamos fazer é abrir o arquivo Global.asax dentro do nosso projeto:

![](implement-efficient-data-paging/_static/image2.png)

E, em seguida, registre uma nova regra de mapeamento usando o método auxiliar MapRoute() como a primeira chamada para rotas. MapRoute() abaixo:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

Acima estamos registrando uma nova regra de roteamento chamada "PróximosJantares". Estamos indicando que ele tem o formato de URL "Jantares/Página/{page}" – onde {page} é um valor de parâmetro incorporado na URL. O terceiro parâmetro para o método MapRoute() indica que devemos mapear URLs que correspondam a esse formato ao método de ação Index() na classe DinnersController.

Podemos usar exatamente o mesmo código de Índice () que tínhamos antes com nosso cenário de Querystring – exceto que agora nosso parâmetro "page" virá da URL e não da cadeia de consulta:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

E agora, quando executarmos a aplicação e digitar */Jantares* veremos os primeiros 10 jantares:

![](implement-efficient-data-paging/_static/image3.png)

E quando *digitarmos /Jantares/Página/1* veremos a próxima página de jantares:

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>Adicionando ui de navegação de página

O último passo para completar nosso cenário de paginação será implementar a ui de navegação "próxima" e "anterior" em nosso modelo de visualização para permitir que os usuários pulem facilmente os dados do Jantar.

Para implementar isso corretamente, precisamos saber o número total de Jantares no banco de dados, bem como quantas páginas de dados isso se traduz. Em seguida, precisamos calcular se o valor de "página" solicitado atualmente está no início ou no final dos dados, e mostrar ou ocultar a ui "anterior" e "próxima" em conformidade. Poderíamos implementar essa lógica dentro do nosso método de ação Index(). Alternativamente, podemos adicionar uma classe auxiliar ao nosso projeto que encapsula essa lógica de uma forma mais reutilizável.

Abaixo está uma classe simples de ajudante "PaginatedList" que deriva da classe de coleção Lista&lt;T&gt; incorporada ao Quadro .NET. Ele implementa uma classe de coleta reutilizável que pode ser usada para paginar qualquer seqüência de dados IQueryable. Em nosso aplicativo NerdDinner, teremos que trabalhar&lt;sobre&gt; os resultados do Jantar IQueryable,&lt;mas&gt; ele poderia&lt;ser&gt; facilmente usado contra produtos iQueryable product ou resultados de clientes iqueráveis em outros cenários de aplicativos:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

Observe acima como ele calcula e, em seguida, expõe propriedades como "PageIndex", "PageSize", "TotalCount" e "TotalPages". Em seguida, também expõe duas propriedades auxiliares "HasPreviousPage" e "HasNextPage" que indicam se a página de dados na coleção está no início ou no final da seqüência original. O código acima fará com que duas consultas SQL sejam executadas - a primeira para recuperar a contagem do número total de objetos do Jantar (isso não retorna os objetos – em vez disso, ele executa uma declaração "SELECT COUNT" que retorna um inteiro), e a segunda para recuperar apenas as linhas de dados que precisamos do nosso banco de dados para a página atual de dados.

Podemos então atualizar nosso método de ajuda DinnersController.Index() para&lt;&gt; criar um Jantar PaginatedList a partir do nosso DinnerRepository.FindUpcomingDinners() resultado, e passá-lo para o nosso modelo de visualização:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

Em seguida, podemos atualizar o modelo de exibição \Views\Dinners\Index.aspx para herdar&lt;&gt; &gt; do ViewPage&lt;&lt;&lt;NerdDinner.Helpers.PaginatedList Dinner em vez de ViewPage IEnumerable Dinner&gt;&gt;e, em seguida, adicionar o seguinte código à parte inferior do nosso modelo de exibição para mostrar ou ocultar a ui de navegação próxima e anterior:

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

Observe acima como estamos usando o método de ajuda Html.RouteLink() para gerar nossos hiperlinks. Este método é semelhante ao método de ajuda Html.ActionLink() que usamos anteriormente. A diferença é que estamos gerando a URL usando a regra de roteamento "UpcomingDinners" que configuramos em nosso arquivo Global.asax. Isso garante que geraremos URLs para o nosso método de ação Index() que tenham o formato: */Dinners/Page/{page}* – onde o valor {page} é uma variável que estamos fornecendo acima com base no PageIndex atual.

E agora, quando executarmos nosso aplicativo novamente, veremos 10 jantares de cada vez em nosso navegador:

![](implement-efficient-data-paging/_static/image5.png)

Também temos &lt; &lt; &lt; &gt; &gt; &gt; interface do ui de navegação na parte inferior da página que nos permite pular para frente e para trás sobre nossos dados usando URLs acessíveis do mecanismo de pesquisa:

![](implement-efficient-data-paging/_static/image6.png)

| **Tópico Lateral: Entendendo as implicações&lt;do IQueryable T&gt;** |
| --- |
| IQueryable&lt;&gt; T é um recurso muito poderoso que permite uma variedade de cenários interessantes de execução diferida (como consultas baseadas em paginação e composição). Como em todos os recursos poderosos, você quer ter cuidado com a forma como você usá-lo e certifique-se de que ele não é abusado. É importante reconhecer que o retorno de&lt;&gt; um Resultado T IQueryable do seu repositório permite que o código de chamada asejada em métodos de operador em cadeia para ele, e assim participar da execução final da consulta. Se você não quiser fornecer código de chamada essa capacidade,&gt; então você&lt;deve&gt; retornar os resultados t&lt;ou iEnumerable T - que contêm os resultados de uma consulta que já foi executada. Para cenários de paginação, isso exigiria que você empurrasse a lógica real de paginação de dados para o método de repositório que está sendo chamado. Neste cenário, podemos atualizar nosso método de localizador FindUpcomingDinners() para ter uma assinatura que&lt; retornou uma PaginatedList:&gt; PaginatedList Dinner FindUpcomingDinners&lt;&gt;(int pageIndex, int pageSize) { } Ou retornar&lt;&gt; um Jantar IList , e usar um param "totalCount" para retornar a contagem total de Jantares: IList Dinner FindUpcomingDinners (int pageIndex, int pageSize, out int totalCount) { } |

### <a name="next-step"></a>Próxima etapa

Vamos agora ver como podemos adicionar autenticação e suporte à autorização ao nosso aplicativo.

> [!div class="step-by-step"]
> [Próximo](re-use-ui-using-master-pages-and-partials.md)
> [anterior](secure-applications-using-authentication-and-authorization.md)
