---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
title: Examinando os métodos de edição e o modo de exibição de edição (C#) | Microsoft Docs
author: Rick-Anderson
description: Este tutorial ensinará as noções básicas da criação de um aplicativo Web ASP.NET MVC usando o Microsoft Visual Web Developer 2010 Express Service Pack 1, que é...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 1d266bf0-a61e-423b-a3d2-13773d7dafe2
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: baa300c66bfae9fe602a8fe597e21b0abbaf3a63
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044981"
---
# <a name="examining-the-edit-methods-and-edit-view-c"></a>Examinar os métodos de edição e a exibição de edição (C#)

por [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Uma versão atualizada deste tutorial está disponível [aqui](../../../getting-started/introduction/getting-started.md) que usa o ASP.NET MVC 5 e o Visual Studio 2013. É mais seguro, muito mais simples de seguir e demonstra mais recursos.
> 
> 
> Este tutorial ensinará as noções básicas da criação de um aplicativo Web ASP.NET MVC usando o Microsoft Visual Web Developer 2010 Express Service Pack 1, que é uma versão gratuita do Microsoft Visual Studio. Antes de começar, verifique se você instalou os pré-requisitos listados abaixo. Você pode instalar todos eles clicando no seguinte link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Como alternativa, você pode instalar os pré-requisitos individualmente usando os seguintes links:
> 
> - [Pré-requisitos do Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Atualização de ferramentas do ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(suporte + ferramentas de tempo de execução)
> 
> Se você estiver usando o Visual Studio 2010 em vez do Visual Web Developer 2010, instale os pré-requisitos clicando no seguinte link: [pré-requisitos do Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Um projeto do Visual Web Developer com código-fonte C# está disponível para acompanhar este tópico. [Baixe a versão C#](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Se preferir Visual Basic, alterne para a [versão Visual Basic](../vb/intro-to-aspnet-mvc-3.md) deste tutorial.

Nesta seção, você examinará os métodos de ação e as exibições gerados para o controlador de filme. Em seguida, você adicionará uma página de pesquisa personalizada.

Execute o aplicativo e navegue até o `Movies` controlador acrescentando */Movies* à URL na barra de endereços do seu navegador. Mantenha o ponteiro do mouse sobre um link de **edição** para ver a URL à qual ele se vincula.

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image2.png)](examining-the-edit-methods-and-edit-view/_static/image1.png)

O link de **edição** foi gerado pelo `Html.ActionLink` método na exibição *Views\Movies\Index.cshtml* :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image4.png)](examining-the-edit-methods-and-edit-view/_static/image3.png)

O `Html` objeto é um auxiliar que é exposto usando uma propriedade na `WebViewPage` classe base. O `ActionLink` método do auxiliar facilita a geração dinâmica de hiperlinks HTML que se vinculam a métodos de ação em controladores. O primeiro argumento para o `ActionLink` método é o texto do link a ser renderizado (por exemplo, `<a>Edit Me</a>` ). O segundo argumento é o nome do método de ação a ser invocado. O argumento final é um [objeto anônimo](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) que gera os dados da rota (nesse caso, a ID de 4).

O link gerado mostrado na imagem anterior é `http://localhost:xxxxx/Movies/Edit/4` . A rota padrão usa o padrão de URL `{controller}/{action}/{id}` . Portanto, o ASP.NET se traduz `http://localhost:xxxxx/Movies/Edit/4` em uma solicitação para o `Edit` método de ação do `Movies` controlador com o parâmetro `ID` igual a 4.

Você também pode passar parâmetros de método de ação usando uma cadeia de caracteres de consulta. Por exemplo, a URL `http://localhost:xxxxx/Movies/Edit?ID=4` também passa o parâmetro `ID` de 4 para o `Edit` método de ação do `Movies` controlador.

[![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image6.png)](examining-the-edit-methods-and-edit-view/_static/image5.png)

Abra o `Movies` controlador. Os dois `Edit` métodos de ação são mostrados abaixo.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

Observe se o segundo método de ação `Edit` é precedido pelo atributo `HttpPost`. Esse atributo especifica que a sobrecarga do `Edit` método pode ser invocada somente para solicitações post. Você pode aplicar o `HttpGet` atributo ao primeiro método de edição, mas isso não é necessário porque é o padrão. (Vamos nos referir aos métodos de ação que são atribuídos implicitamente ao `HttpGet` atributo como `HttpGet` métodos.)

O `HttpGet` `Edit` método usa o parâmetro ID do filme, pesquisa o filme usando o `Find` Método Entity Framework e retorna o filme selecionado para o modo de exibição Editar. Quando o sistema de scaffolding criou a exibição de Edição, ele examinou a classe `Movie` e o código criado para renderizar os elementos `<label>` e `<input>` de cada propriedade da classe. O exemplo a seguir mostra a exibição de edição que foi gerada:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

Observe como o modelo de exibição tem uma `@model MvcMovie.Models.Movie` instrução na parte superior do arquivo — isso especifica que a exibição espera que o modelo para o modelo de exibição seja do tipo `Movie` .

O código com Scaffold usa vários *métodos auxiliares* para simplificar a marcação HTML. O [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) auxiliar exibe o nome do campo ("título", "liberado", "gênero" ou "preço"). O [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) auxiliar exibe um `<input>` elemento HTML. O [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) auxiliar exibe todas as mensagens de validação associadas a essa propriedade.

Execute o aplicativo e navegue até a URL */Movies* . Clique em um link de **edição** . No navegador, exiba a origem da página. O HTML na página é semelhante ao exemplo a seguir. (A marcação do menu foi excluída para fins de clareza.)

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample4.html)]

Os `<input>` elementos estão em um `<form>` elemento HTML cujo `action` atributo está definido como post para a URL */Movies/Edit* . Os dados do formulário serão postados no servidor quando o botão **Editar** for clicado.

## <a name="processing-the-post-request"></a>Processando a solicitação POST

A lista a seguir mostra a versão `HttpPost` do método de ação `Edit`.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs)]

O associador de modelo do ASP.NET Framework pega os valores de formulário postados e cria um `Movie` objeto que é passado como o `movie` parâmetro. O `ModelState.IsValid` check-in do código verifica se os dados enviados no formulário podem ser usados para modificar um `Movie` objeto. Se os dados forem válidos, o código salvará os dados do filme na `Movies` coleção da `MovieDBContext` instância. Em seguida, o código salva os novos dados do filme no banco de dado chamando o `SaveChanges` método de `MovieDBContext` , que persiste as alterações no banco de dados. Depois de salvar os dados, o código redireciona o usuário para o `Index` método de ação da `MoviesController` classe, o que faz com que o filme atualizado seja exibido na lista de filmes.

Se os valores postados não forem válidos, eles serão exibidos novamente no formulário. Os `Html.ValidationMessageFor` auxiliares no modelo de exibição *Edit. cshtml* cuidam da exibição das mensagens de erro apropriadas.

[![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image8.png)](examining-the-edit-methods-and-edit-view/_static/image7.png)

> **Observação sobre localidades** Se você normalmente trabalha com uma localidade diferente do inglês, consulte [dando suporte à validação do ASP.NET MVC 3 com localidades não inglesas.](https://msdn.microsoft.com/library/gg674880(VS.98).aspx)

## <a name="making-the-edit-method-more-robust"></a>Tornando o método de edição mais robusto

O `HttpGet` `Edit` método gerado pelo sistema scaffolding não verifica se a ID passada para ele é válida. Se um usuário remover o segmento de ID da URL ( `http://localhost:xxxxx/Movies/Edit` ), o seguinte erro será exibido:

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image10.png)](examining-the-edit-methods-and-edit-view/_static/image9.png)

Um usuário também pode passar uma ID que não existe no banco de dados, como `http://localhost:xxxxx/Movies/Edit/1234` . Você pode fazer duas alterações no `HttpGet` `Edit` método de ação para resolver essa limitação. Primeiro, altere o `ID` parâmetro para ter um valor padrão de zero quando uma ID não for explicitamente passada. Você também pode verificar se o `Find` método realmente encontrou um filme antes de retornar o objeto de filme para o modelo de exibição. O `Edit` método atualizado é mostrado abaixo.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

Se nenhum filme for encontrado, o `HttpNotFound` método será chamado.

Todos os `HttpGet` métodos seguem um padrão semelhante. Eles obtêm um objeto de filme (ou lista de objetos, no caso de `Index` ) e passam o modelo para a exibição. O `Create` método passa um objeto de filme vazio para o modo de exibição de criação. Todos os métodos que criam, editam, excluem ou, de outro modo, modificam dados fazem isso na sobrecarga `HttpPost` do método. A modificação de dados em um método HTTP GET é um risco de segurança, conforme descrito na entrada de postagem de blog [ASP.net a Tip do MVC #46 – não use os links de exclusão porque eles criam brechas de segurança](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). Modificar dados em um método GET também viola as práticas recomendadas de HTTP e o padrão de REST arquitetônico, que especifica que as solicitações GET não devem alterar o estado do seu aplicativo. Em outras palavras, a execução de uma operação GET deve ser uma operação segura que não tenha efeitos colaterais.

## <a name="adding-a-search-method-and-search-view"></a>Adicionando um método de pesquisa e uma exibição de pesquisa

Nesta seção, você adicionará um `SearchIndex` método de ação que permite pesquisar filmes por gênero ou por nome. Isso estará disponível usando a URL */Movies/SearchIndex* . A solicitação exibirá um formulário HTML que contém os elementos de entrada que um usuário pode preencher para pesquisar um filme. Quando um usuário envia o formulário, o método de ação Obtém os valores de pesquisa postados pelo usuário e usa os valores para pesquisar o banco de dados.

## <a name="displaying-the-searchindex-form"></a>Exibindo o formulário SearchIndex

Comece adicionando um `SearchIndex` método de ação à classe existente `MoviesController` . O método retornará uma exibição que contém um formulário HTML. O código é o seguinte:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cs)]

A primeira linha do `SearchIndex` método cria a seguinte consulta [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) para selecionar os filmes:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cs)]

A consulta é definida neste ponto, mas ainda não foi executada no armazenamento de dados.

Se o `searchString` parâmetro contiver uma cadeia de caracteres, a consulta de filmes será modificada para filtrar o valor da cadeia de caracteres de pesquisa, usando o seguinte código:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

Consultas LINQ não são executadas quando são definidas ou quando são modificadas chamando um método como `Where` ou `OrderBy` . Em vez disso, a execução da consulta é adiada, o que significa que a avaliação de uma expressão é adiada até que seu valor percebido seja realmente iterado ou o [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) método seja chamado. No `SearchIndex` exemplo, a consulta é executada na exibição SearchIndex. Para obter mais informações sobre a execução de consulta adiada, consulte [Execução da consulta](https://msdn.microsoft.com/library/bb738633.aspx).

Agora você pode implementar a `SearchIndex` exibição que exibirá o formulário para o usuário. Clique com o botão direito do mouse dentro do `SearchIndex` método e clique em **Adicionar exibição**. Na caixa de diálogo **Adicionar exibição** , especifique que você vai passar um `Movie` objeto para o modelo de exibição como sua classe de modelo. Na lista **modelo de Scaffold** , escolha **lista**e clique em **Adicionar**.

[![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

Quando você clica no botão **Adicionar** , o modelo de exibição *Views\Movies\SearchIndex.cshtml* é criado. Como você selecionou **lista** na lista de **modelos Scaffold** , o Visual Web Developer gerou automaticamente (com scaffold) algum conteúdo padrão na exibição. O scaffolding criou um formulário HTML. Ele examinou a `Movie` classe e criou o código para renderizar `<label>` elementos para cada propriedade da classe. A listagem a seguir mostra o modo de exibição de criação que foi gerado:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

Execute o aplicativo e navegue até */Movies/SearchIndex*. Acrescente uma cadeia de consulta, como `?searchString=ghost`, à URL. Os filmes filtrados são exibidos.

[![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

Se você alterar a assinatura do `SearchIndex` método para ter um parâmetro chamado `id` , o `id` parâmetro corresponderá ao `{id}` espaço reservado para as rotas padrão definidas no arquivo *global. asax* .

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.txt)]

O `SearchIndex` método modificado seria semelhante ao seguinte:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cs)]

Agora você pode passar o título de pesquisa como dados de rota (um segmento de URL), em vez de como um valor de cadeia de consulta.

[![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

No entanto, você não pode esperar que os usuários modifiquem a URL sempre que desejarem pesquisar um filme. Agora, você adicionará a interface do usuário para ajudá-lo a filtrar filmes. Se você alterou a assinatura do `SearchIndex` método para testar como passar o parâmetro de ID de associação de rota, altere-o de volta para que o `SearchIndex` método aceite um parâmetro de cadeia de caracteres chamado `searchString` :

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample13.cs)]

Abra o arquivo *Views\Movies\SearchIndex.cshtml* e, logo após `@Html.ActionLink("Create New", "Create")` , adicione o seguinte:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cshtml)]

O exemplo a seguir mostra uma parte do arquivo *Views\Movies\SearchIndex.cshtml* com a marcação de filtragem adicionada.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cshtml)]

O `Html.BeginForm` auxiliar cria uma marca de abertura `<form>` . O `Html.BeginForm` auxiliar faz com que o formulário seja Postado para si mesmo quando o usuário envia o formulário clicando no botão de **filtro** .

Execute o aplicativo e tente pesquisar um filme.

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

Não há `HttpPost` sobrecarga do `SearchIndex` método. Você não precisa dele, porque o método não está alterando o estado do aplicativo, apenas filtrando os dados.

Você poderá adicionar o método `HttpPost SearchIndex` a seguir. Nesse caso, o chamador de ação corresponderia ao `HttpPost SearchIndex` método e o `HttpPost SearchIndex` método seria executado conforme mostrado na imagem abaixo.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

[![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

No entanto, mesmo se você adicionar esta versão `HttpPost` do método `SearchIndex`, haverá uma limitação na forma de como isso tudo foi implementado. Imagine que você deseja adicionar uma pesquisa específica como Favoritos ou enviar um link para seus amigos para que eles possam clicar para ver a mesma lista filtrada de filmes. Observe que a URL para a solicitação HTTP POST é igual à URL da solicitação GET (localhost: xxxxx/Movies/SearchIndex) – não há informações de pesquisa na própria URL. No momento, as informações de cadeia de caracteres de pesquisa são enviadas ao servidor como um valor de campo de formulário. Isso significa que você não pode capturar essas informações de pesquisa para indicar ou enviar para amigos em uma URL.

A solução é usar uma sobrecarga de `BeginForm` que especifica que a solicitação POST deve adicionar as informações de pesquisa à URL e que deve ser roteada para a versão HttpGet do `SearchIndex` método. Substitua o `BeginForm` método sem parâmetros existente pelo seguinte:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml)]

[![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image22.png)](examining-the-edit-methods-and-edit-view/_static/image21.png)

Agora, quando você envia uma pesquisa, a URL contém uma cadeia de caracteres de consulta de pesquisa. A pesquisa também irá para o método de ação `HttpGet SearchIndex`, mesmo se você tiver um método `HttpPost SearchIndex`.

[![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image24.png)](examining-the-edit-methods-and-edit-view/_static/image23.png)

## <a name="adding-search-by-genre"></a>Adicionando pesquisa por gênero

Se você adicionou a `HttpPost` versão do `SearchIndex` método, exclua-a agora.

Em seguida, você adicionará um recurso para permitir que os usuários pesquisem filmes por gênero. Substitua o método `SearchIndex` pelo seguinte código:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cs)]

Essa versão do `SearchIndex` método usa um parâmetro adicional, ou seja, `movieGenre` As primeiras linhas de código criam um `List` objeto para conter gêneros de filme do banco de dados.

O código a seguir é uma consulta LINQ que recupera todos os gêneros do banco de dados.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

O código usa o `AddRange` método da coleção genérica `List` para adicionar todos os gêneros distintos à lista. (Sem o `Distinct` modificador, os gêneros duplicados seriam adicionados; por exemplo, comédia seria adicionado duas vezes em nosso exemplo). Em seguida, o código armazena a lista de gêneros no `ViewBag` objeto.

O código a seguir mostra como verificar o `movieGenre` parâmetro. Se não estiver vazio, o código restringe ainda mais a consulta de filmes para limitar os filmes selecionados ao gênero especificado.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>Adicionando marcação à exibição SearchIndex para dar suporte à pesquisa por gênero

Adicione um `Html.DropDownList` auxiliar ao arquivo *Views\Movies\SearchIndex.cshtml* , logo antes do `TextBox` auxiliar. A marcação concluída é mostrada abaixo:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cshtml)]

Execute o aplicativo e navegue até */Movies/SearchIndex*. Experimente uma pesquisa por gênero, por nome de filme e por ambos os critérios.

Nesta seção, você examinou os métodos de ação CRUD e as exibições geradas pela estrutura. Você criou um método de ação de pesquisa e uma exibição que permitem que os usuários pesquisem por título e gênero do filme. Na próxima seção, você examinará como adicionar uma propriedade ao `Movie` modelo e como adicionar um inicializador que criará automaticamente um banco de dados de teste.

> [!div class="step-by-step"]
> [Anterior](accessing-your-models-data-from-a-controller.md) 
>  [Avançar](adding-a-new-field.md)
