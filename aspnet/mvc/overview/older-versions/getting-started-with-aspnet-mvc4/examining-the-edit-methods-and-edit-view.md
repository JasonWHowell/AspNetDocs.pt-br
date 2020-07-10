---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: Examinando os métodos de edição e o modo de exibição de edição | Microsoft Docs
author: Rick-Anderson
description: 'Observação: uma versão atualizada deste tutorial está disponível aqui que usa o ASP.NET MVC 5 e o Visual Studio 2013. É mais seguro, muito mais simples de seguir e demonstrar...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 85ad9a5758d70b5fe4ed792efb80217d7b3e2132
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162930"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Examinar os métodos de edição e a exibição de edição

por [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Uma versão atualizada deste tutorial está disponível [aqui](../../getting-started/introduction/getting-started.md) que usa o ASP.NET MVC 5 e o Visual Studio 2013. É mais seguro, muito mais simples de seguir e demonstra mais recursos.

Nesta seção, você examinará os métodos de ação e as exibições gerados para o controlador de filme. Em seguida, você adicionará uma página de pesquisa personalizada.

Execute o aplicativo e navegue até o `Movies` controlador acrescentando */Movies* à URL na barra de endereços do seu navegador. Mantenha o ponteiro do mouse sobre um link de **edição** para ver a URL à qual ele se vincula.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

O link de **edição** foi gerado pelo `Html.ActionLink` método na exibição *Views\Movies\Index.cshtml* :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

O `Html` objeto é um auxiliar que é exposto usando uma propriedade na classe base [System. Web. Mvc. WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) . O `ActionLink` método do auxiliar facilita a geração dinâmica de hiperlinks HTML que se vinculam a métodos de ação em controladores. O primeiro argumento para o `ActionLink` método é o texto do link a ser renderizado (por exemplo, `<a>Edit Me</a>` ). O segundo argumento é o nome do método de ação a ser invocado. O argumento final é um [objeto anônimo](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) que gera os dados da rota (nesse caso, a ID de 4).

O link gerado mostrado na imagem anterior é `http://localhost:xxxxx/Movies/Edit/4` . A rota padrão (estabelecida no *aplicativo \_ Start\RouteConfig.cs*) usa o padrão de URL `{controller}/{action}/{id}` . Portanto, o ASP.NET se traduz `http://localhost:xxxxx/Movies/Edit/4` em uma solicitação para o `Edit` método de ação do `Movies` controlador com o parâmetro `ID` igual a 4. Examine o código a seguir do *arquivo \_ Start\RouteConfig.cs do aplicativo* .

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

Você também pode passar parâmetros de método de ação usando uma cadeia de caracteres de consulta. Por exemplo, a URL `http://localhost:xxxxx/Movies/Edit?ID=4` também passa o parâmetro `ID` de 4 para o `Edit` método de ação do `Movies` controlador.

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

Abra o `Movies` controlador. Os dois `Edit` métodos de ação são mostrados abaixo.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

Observe se o segundo método de ação `Edit` é precedido pelo atributo `HttpPost`. Esse atributo especifica que a sobrecarga do `Edit` método pode ser invocada somente para solicitações post. Você pode aplicar o `HttpGet` atributo ao primeiro método de edição, mas isso não é necessário porque é o padrão. (Vamos nos referir aos métodos de ação que são atribuídos implicitamente ao `HttpGet` atributo como `HttpGet` métodos.)

O `HttpGet` `Edit` método usa o parâmetro ID do filme, pesquisa o filme usando o `Find` Método Entity Framework e retorna o filme selecionado para o modo de exibição Editar. O parâmetro ID especifica um [valor padrão](https://msdn.microsoft.com/library/dd264739.aspx) de zero se o `Edit` método for chamado sem um parâmetro. Se não for possível encontrar um filme, [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) será retornado. Quando o sistema de scaffolding criou a exibição de Edição, ele examinou a classe `Movie` e o código criado para renderizar os elementos `<label>` e `<input>` de cada propriedade da classe. O exemplo a seguir mostra a exibição de edição que foi gerada:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

Observe como o modelo de exibição tem uma `@model MvcMovie.Models.Movie` instrução na parte superior do arquivo — isso especifica que a exibição espera que o modelo para o modelo de exibição seja do tipo `Movie` .

O código com Scaffold usa vários *métodos auxiliares* para simplificar a marcação HTML. O [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) auxiliar exibe o nome do campo ( &quot; título &quot; , &quot; liberado &quot; , &quot; gênero &quot; ou &quot; preço &quot; ). O [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) auxiliar renderiza um elemento HTML `<input>` . O [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) auxiliar exibe todas as mensagens de validação associadas a essa propriedade.

Execute o aplicativo e navegue até a URL */Movies* . Clique em um link de **edição** . No navegador, exiba a origem da página. O HTML do elemento form é mostrado abaixo.

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

Os `<input>` elementos estão em um `<form>` elemento HTML cujo `action` atributo está definido como post para a URL */Movies/Edit* . Os dados do formulário serão postados no servidor quando o botão **Editar** for clicado.

## <a name="processing-the-post-request"></a>Processando a solicitação POST

A lista a seguir mostra a versão `HttpPost` do método de ação `Edit`.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

O [associador de modelo MVC do ASP.net](https://msdn.microsoft.com/magazine/hh781022.aspx) pega os valores de formulário postados e cria um `Movie` objeto que é passado como o `movie` parâmetro. O método `ModelState.IsValid` verifica se os dados enviados no formulário podem ser usados para modificar (editar ou atualizar) um objeto `Movie`. Se os dados forem válidos, os dados do filme serão salvos na `Movies` coleção da `db(MovieDBContext` instância do). Os novos dados de filme são salvos no banco de dado chamando o `SaveChanges` método de `MovieDBContext` . Depois de salvar os dados, o código redireciona o usuário para o `Index` método de ação da `MoviesController` classe, que exibe a coleção de filmes, incluindo as alterações feitas apenas.

Se os valores postados não forem válidos, eles serão exibidos novamente no formulário. Os `Html.ValidationMessageFor` auxiliares no modelo de exibição *Edit. cshtml* cuidam da exibição das mensagens de erro apropriadas.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> para dar suporte à validação do jQuery para localidades não inglesas que usam uma vírgula ( &quot; , &quot; ) para um ponto decimal, você deve incluir *globalize.js* e seu arquivo de *culturas/globalize.cultures.js* específico (de [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) e JavaScript para usar `Globalize.parseFloat` . O código a seguir mostra as modificações no arquivo Views\Movies\Edit.cshtml para trabalhar com a &quot; cultura fr-fr &quot; :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

O campo decimal pode exigir uma vírgula, não um ponto decimal. Como uma correção temporária, você pode adicionar o elemento Globalization ao arquivo de web.config raiz dos projetos. O código a seguir mostra o elemento Globalization com a cultura definida como Estados Unidos Inglês.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

Todos os `HttpGet` métodos seguem um padrão semelhante. Eles obtêm um objeto de filme (ou lista de objetos, no caso de `Index` ) e passam o modelo para a exibição. O `Create` método passa um objeto de filme vazio para o modo de exibição de criação. Todos os métodos que criam, editam, excluem ou, de outro modo, modificam dados fazem isso na sobrecarga `HttpPost` do método. A modificação de dados em um método HTTP GET é um risco de segurança, conforme descrito na entrada de postagem de blog [ASP.net a Tip do MVC #46 – não use os links de exclusão porque eles criam brechas de segurança](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). Modificar dados em um método GET também viola as práticas recomendadas de HTTP e o padrão de [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) arquitetônico, que especifica que as solicitações GET não devem alterar o estado do seu aplicativo. Em outras palavras, a execução de uma operação GET deve ser uma operação segura que não tem efeitos colaterais e não modifica os dados persistentes.

## <a name="adding-a-search-method-and-search-view"></a>Adicionando um método de pesquisa e uma exibição de pesquisa

Nesta seção, você adicionará um `SearchIndex` método de ação que permite pesquisar filmes por gênero ou por nome. Isso estará disponível usando a URL */Movies/SearchIndex* . A solicitação exibirá um formulário HTML que contém os elementos de entrada que um usuário pode inserir para pesquisar um filme. Quando um usuário envia o formulário, o método de ação Obtém os valores de pesquisa postados pelo usuário e usa os valores para pesquisar o banco de dados.

## <a name="displaying-the-searchindex-form"></a>Exibindo o formulário SearchIndex

Comece adicionando um `SearchIndex` método de ação à classe existente `MoviesController` . O método retornará uma exibição que contém um formulário HTML. O código é o seguinte:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

A primeira linha do `SearchIndex` método cria a seguinte consulta [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) para selecionar os filmes:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

A consulta é definida neste ponto, mas ainda não foi executada no armazenamento de dados.

Se o `searchString` parâmetro contiver uma cadeia de caracteres, a consulta de filmes será modificada para filtrar o valor da cadeia de caracteres de pesquisa, usando o seguinte código:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

O código `s => s.Title` acima é uma [Expressão Lambda](https://msdn.microsoft.com/library/bb397687.aspx). As Lambdas são usadas em consultas [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) baseadas em método como argumentos para métodos de operador de consulta padrão, como o método [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) usado no código acima. Consultas LINQ não são executadas quando são definidas ou quando são modificadas chamando um método como `Where` ou `OrderBy` . Em vez disso, a execução da consulta é adiada, o que significa que a avaliação de uma expressão é adiada até que seu valor percebido seja realmente iterado ou o [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) método seja chamado. No `SearchIndex` exemplo, a consulta é executada na exibição SearchIndex. Para obter mais informações sobre a execução de consulta adiada, consulte [Execução da consulta](https://msdn.microsoft.com/library/bb738633.aspx).

Agora você pode implementar a `SearchIndex` exibição que exibirá o formulário para o usuário. Clique com o botão direito do mouse dentro do `SearchIndex` método e clique em **Adicionar exibição**. Na caixa de diálogo **Adicionar exibição** , especifique que você vai passar um `Movie` objeto para o modelo de exibição como sua classe de modelo. Na lista **modelo de Scaffold** , escolha **lista**e clique em **Adicionar**.

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

Quando você clica no botão **Adicionar** , o modelo de exibição *Views\Movies\SearchIndex.cshtml* é criado. Como você selecionou **lista** na lista de **modelos Scaffold** , o Visual Studio gerou automaticamente (com scaffold) algumas marcações padrão na exibição. O scaffolding criou um formulário HTML. Ele examinou a `Movie` classe e criou o código para renderizar `<label>` elementos para cada propriedade da classe. A listagem a seguir mostra o modo de exibição de criação que foi gerado:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

Execute o aplicativo e navegue até */Movies/SearchIndex*. Acrescente uma cadeia de consulta, como `?searchString=ghost`, à URL. Os filmes filtrados são exibidos.

![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image6.png)

Se você alterar a assinatura do `SearchIndex` método para ter um parâmetro chamado `id` , o `id` parâmetro corresponderá ao `{id}` espaço reservado para as rotas padrão definidas no arquivo *global. asax* .

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

O `SearchIndex` método original tem esta aparência::

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

O `SearchIndex` método modificado seria semelhante ao seguinte:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

Agora você pode passar o título de pesquisa como dados de rota (um segmento de URL), em vez de como um valor de cadeia de consulta.

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

No entanto, você não pode esperar que os usuários modifiquem a URL sempre que desejarem pesquisar um filme. Agora, você adicionará a interface do usuário para ajudá-lo a filtrar filmes. Se você alterou a assinatura do `SearchIndex` método para testar como passar o parâmetro de ID de associação de rota, altere-o de volta para que o `SearchIndex` método aceite um parâmetro de cadeia de caracteres chamado `searchString` :

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

Abra o arquivo *Views\Movies\SearchIndex.cshtml* e, logo após `@Html.ActionLink("Create New", "Create")` , adicione o seguinte:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

O exemplo a seguir mostra uma parte do arquivo *Views\Movies\SearchIndex.cshtml* com a marcação de filtragem adicionada.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

O `Html.BeginForm` auxiliar cria uma marca de abertura `<form>` . O `Html.BeginForm` auxiliar faz com que o formulário seja Postado para si mesmo quando o usuário envia o formulário clicando no botão de **filtro** .

Execute o aplicativo e tente pesquisar um filme.

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

Não há `HttpPost` sobrecarga do `SearchIndex` método. Você não precisa dele, porque o método não está alterando o estado do aplicativo, apenas filtrando os dados.

Você poderá adicionar o método `HttpPost SearchIndex` a seguir. Nesse caso, o chamador de ação corresponderia ao `HttpPost SearchIndex` método e o `HttpPost SearchIndex` método seria executado conforme mostrado na imagem abaixo.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image9.png)

No entanto, mesmo se você adicionar esta versão `HttpPost` do método `SearchIndex`, haverá uma limitação na forma de como isso tudo foi implementado. Imagine que você deseja adicionar uma pesquisa específica como Favoritos ou enviar um link para seus amigos para que eles possam clicar para ver a mesma lista filtrada de filmes. Observe que a URL para a solicitação HTTP POST é igual à URL da solicitação GET (localhost: xxxxx/Movies/SearchIndex) – não há informações de pesquisa na própria URL. No momento, as informações de cadeia de caracteres de pesquisa são enviadas ao servidor como um valor de campo de formulário. Isso significa que você não pode capturar essas informações de pesquisa para indicar ou enviar para amigos em uma URL.

A solução é usar uma sobrecarga de `BeginForm` que especifica que a solicitação POST deve adicionar as informações de pesquisa à URL e que ela deve ser roteada para a versão HttpGet do `SearchIndex` método. Substitua o `BeginForm` método sem parâmetros existente pelo seguinte:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

Agora, quando você envia uma pesquisa, a URL contém uma cadeia de caracteres de consulta de pesquisa. A pesquisa também irá para o método de ação `HttpGet SearchIndex`, mesmo se você tiver um método `HttpPost SearchIndex`.

![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>Adicionando pesquisa por gênero

Se você adicionou a `HttpPost` versão do `SearchIndex` método, exclua-a agora.

Em seguida, você adicionará um recurso para permitir que os usuários pesquisem filmes por gênero. Substitua o método `SearchIndex` pelo seguinte código:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

Essa versão do `SearchIndex` método usa um parâmetro adicional, ou seja, `movieGenre` As primeiras linhas de código criam um `List` objeto para conter gêneros de filme do banco de dados.

O código a seguir é uma consulta LINQ que recupera todos os gêneros do banco de dados.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

O código usa o `AddRange` método da coleção genérica `List` para adicionar todos os gêneros distintos à lista. (Sem o `Distinct` modificador, os gêneros duplicados seriam adicionados; por exemplo, comédia seria adicionado duas vezes em nosso exemplo). Em seguida, o código armazena a lista de gêneros no `ViewBag` objeto.

O código a seguir mostra como verificar o `movieGenre` parâmetro. Se não estiver vazio, o código restringirá ainda mais a consulta de filmes para limitar os filmes selecionados ao gênero especificado.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>Adicionando marcação à exibição SearchIndex para dar suporte à pesquisa por gênero

Adicione um `Html.DropDownList` auxiliar ao arquivo *Views\Movies\SearchIndex.cshtml* , logo antes do `TextBox` auxiliar. A marcação concluída é mostrada abaixo:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

Execute o aplicativo e navegue até */Movies/SearchIndex*. Experimente uma pesquisa por gênero, por nome de filme e por ambos os critérios.

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

Nesta seção, você examinou os métodos de ação CRUD e as exibições geradas pela estrutura. Você criou um método de ação de pesquisa e uma exibição que permitem que os usuários pesquisem por título e gênero do filme. Na próxima seção, você examinará como adicionar uma propriedade ao `Movie` modelo e como adicionar um inicializador que criará automaticamente um banco de dados de teste.

> [!div class="step-by-step"]
> [Anterior](accessing-your-models-data-from-a-controller.md) 
>  [Avançar](adding-a-new-field-to-the-movie-model-and-table.md)
