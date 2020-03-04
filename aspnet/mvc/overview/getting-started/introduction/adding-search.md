---
uid: mvc/overview/getting-started/introduction/adding-search
title: Pesquisa | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: 7b49c1e6425080693229c6c132df3879504c835c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59379528"
---
# <a name="search"></a><span data-ttu-id="6c977-102">Pesquisar</span><span class="sxs-lookup"><span data-stu-id="6c977-102">Search</span></span>


[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="6c977-103">Adicionando um método de pesquisa e a exibição de pesquisa</span><span class="sxs-lookup"><span data-stu-id="6c977-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="6c977-104">Nesta seção, você adicionará a funcionalidade de pesquisa para o `Index` método de ação que lhe permite pesquisar filmes por gênero ou nome.</span><span class="sxs-lookup"><span data-stu-id="6c977-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c977-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c977-105">Prerequisites</span></span>

<span data-ttu-id="6c977-106">Para corresponder as capturas de tela desta seção, você precisa executar o aplicativo (F5) e adicione os seguintes filmes no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c977-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="6c977-107">Título</span><span class="sxs-lookup"><span data-stu-id="6c977-107">Title</span></span> | <span data-ttu-id="6c977-108">Data de lançamento</span><span class="sxs-lookup"><span data-stu-id="6c977-108">Release Date</span></span> | <span data-ttu-id="6c977-109">Gênero</span><span class="sxs-lookup"><span data-stu-id="6c977-109">Genre</span></span> | <span data-ttu-id="6c977-110">Preço</span><span class="sxs-lookup"><span data-stu-id="6c977-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="6c977-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="6c977-111">Ghostbusters</span></span> | <span data-ttu-id="6c977-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="6c977-112">6/8/1984</span></span> | <span data-ttu-id="6c977-113">Comédia</span><span class="sxs-lookup"><span data-stu-id="6c977-113">Comedy</span></span> | <span data-ttu-id="6c977-114">6.99</span><span class="sxs-lookup"><span data-stu-id="6c977-114">6.99</span></span> |
| <span data-ttu-id="6c977-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="6c977-115">Ghostbusters II</span></span> | <span data-ttu-id="6c977-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="6c977-116">6/16/1989</span></span> | <span data-ttu-id="6c977-117">Comédia</span><span class="sxs-lookup"><span data-stu-id="6c977-117">Comedy</span></span> | <span data-ttu-id="6c977-118">6.99</span><span class="sxs-lookup"><span data-stu-id="6c977-118">6.99</span></span> |
| <span data-ttu-id="6c977-119">Mundial da falta de sofisticação</span><span class="sxs-lookup"><span data-stu-id="6c977-119">Planet of the Apes</span></span> | <span data-ttu-id="6c977-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="6c977-120">3/27/1986</span></span> | <span data-ttu-id="6c977-121">Ação</span><span class="sxs-lookup"><span data-stu-id="6c977-121">Action</span></span> | <span data-ttu-id="6c977-122">5.99</span><span class="sxs-lookup"><span data-stu-id="6c977-122">5.99</span></span> |


## <a name="updating-the-index-form"></a><span data-ttu-id="6c977-123">Atualizando o formulário de índice</span><span class="sxs-lookup"><span data-stu-id="6c977-123">Updating the Index Form</span></span>

<span data-ttu-id="6c977-124">Comece Atualizando as `Index` método de ação existente `MoviesController` classe.</span><span class="sxs-lookup"><span data-stu-id="6c977-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="6c977-125">Aqui está o código:</span><span class="sxs-lookup"><span data-stu-id="6c977-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="6c977-126">A primeira linha do `Index` método cria o seguinte [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) consulta para selecionar os filmes:</span><span class="sxs-lookup"><span data-stu-id="6c977-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="6c977-127">A consulta é definida no momento, mas não ainda está sendo executada no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c977-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="6c977-128">Se o `searchString` parâmetro contém uma cadeia de caracteres, a consulta de filmes será modificada para filtrar o valor da cadeia de pesquisa, usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6c977-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="6c977-129">O código `s => s.Title` acima é uma [Expressão Lambda](https://msdn.microsoft.com/library/bb397687.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c977-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="6c977-130">Lambdas são usados em baseada em método [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) de consultas como argumentos para métodos de operador de consulta padrão como o [onde](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) método usado no código acima.</span><span class="sxs-lookup"><span data-stu-id="6c977-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="6c977-131">Consultas LINQ não são executadas quando são definidas ou quando eles forem modificados chamando um método como `Where` ou `OrderBy`.</span><span class="sxs-lookup"><span data-stu-id="6c977-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="6c977-132">Em vez disso, a execução da consulta é adiada, o que significa que a avaliação de uma expressão é atrasada até que seu valor realizado seja iterado, na verdade, ou o [ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx) método é chamado.</span><span class="sxs-lookup"><span data-stu-id="6c977-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="6c977-133">No `Search` amostra, em que a consulta é executada a *index. cshtml* exibição.</span><span class="sxs-lookup"><span data-stu-id="6c977-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="6c977-134">Para obter mais informações sobre a execução de consulta adiada, consulte [Execução da consulta](https://msdn.microsoft.com/library/bb738633.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c977-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6c977-135">O [Contains](https://msdn.microsoft.com/library/bb155125.aspx) método é executado no banco de dados, não o código c# acima.</span><span class="sxs-lookup"><span data-stu-id="6c977-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="6c977-136">Banco de dados, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) mapeia para [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), que diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6c977-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="6c977-137">Agora você pode atualizar o `Index` modo de exibição que exibirá o formulário ao usuário.</span><span class="sxs-lookup"><span data-stu-id="6c977-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="6c977-138">Execute o aplicativo e navegue até */Movies/Index*.</span><span class="sxs-lookup"><span data-stu-id="6c977-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="6c977-139">Acrescente uma cadeia de consulta, como `?searchString=ghost`, à URL.</span><span class="sxs-lookup"><span data-stu-id="6c977-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="6c977-140">Os filmes filtrados são exibidos.</span><span class="sxs-lookup"><span data-stu-id="6c977-140">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="6c977-142">Se você alterar a assinatura do `Index` método tenha um parâmetro denominado `id`, o `id` parâmetro corresponderá a `{id}` roteia o espaço reservado para o padrão definido no *aplicativo\_Start RouteConfig.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="6c977-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="6c977-143">Original `Index` método tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="6c977-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="6c977-144">Modificado `Index` método seria semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="6c977-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="6c977-145">Agora você pode passar o título de pesquisa como dados de rota (um segmento de URL), em vez de como um valor de cadeia de consulta.</span><span class="sxs-lookup"><span data-stu-id="6c977-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="6c977-146">No entanto, você não pode esperar que os usuários modifiquem a URL sempre que desejarem pesquisar um filme.</span><span class="sxs-lookup"><span data-stu-id="6c977-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="6c977-147">Portanto, agora você adicionará uma interface do usuário para ajudá-los a filtrar os filmes.</span><span class="sxs-lookup"><span data-stu-id="6c977-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="6c977-148">Se você tiver alterado a assinatura do `Index` método para testar como passar o parâmetro de ID associado à rota, alterá-la para que sua `Index` método utiliza um parâmetro de cadeia de caracteres denominado `searchString`:</span><span class="sxs-lookup"><span data-stu-id="6c977-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="6c977-149">Abra o *Views\Movies\Index.cshtml* do arquivo e apenas após `@Html.ActionLink("Create New", "Create")`, adicione a marcação de formulário realçada abaixo:</span><span class="sxs-lookup"><span data-stu-id="6c977-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="6c977-150">O `Html.BeginForm` auxiliar cria uma abertura `<form>` marca.</span><span class="sxs-lookup"><span data-stu-id="6c977-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="6c977-151">O `Html.BeginForm` auxiliar faz com que o formulário postar a mesmo quando o usuário envia o formulário clicando o **filtro** botão.</span><span class="sxs-lookup"><span data-stu-id="6c977-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="6c977-152">Visual Studio 2013 tem uma boa melhoria ao exibir e editar arquivos de exibição.</span><span class="sxs-lookup"><span data-stu-id="6c977-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="6c977-153">Quando você executar o aplicativo com um arquivo de exibição aberta, o Visual Studio 2013 invoca o método de ação do controlador correto para mostrar a exibição.</span><span class="sxs-lookup"><span data-stu-id="6c977-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="6c977-154">Com o modo de exibição de índice aberto no Visual Studio (conforme mostrado na imagem acima), toque Ctr F5 ou F5 para executar o aplicativo e, em seguida, tente pesquisar um filme.</span><span class="sxs-lookup"><span data-stu-id="6c977-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="6c977-155">Não há nenhuma `HttpPost` sobrecarga da `Index` método.</span><span class="sxs-lookup"><span data-stu-id="6c977-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="6c977-156">Você não precisa dele, porque o método não está alterando o estado do aplicativo, apenas filtrando os dados.</span><span class="sxs-lookup"><span data-stu-id="6c977-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="6c977-157">Você poderá adicionar o método `HttpPost Index` a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c977-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="6c977-158">Nesse caso, o chamador de ação corresponderia a `HttpPost Index` método e o `HttpPost Index` método será executado conforme mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="6c977-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="6c977-160">No entanto, mesmo se você adicionar esta versão `HttpPost` do método `Index`, haverá uma limitação na forma de como isso tudo foi implementado.</span><span class="sxs-lookup"><span data-stu-id="6c977-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="6c977-161">Imagine que você deseja adicionar uma pesquisa específica como Favoritos ou enviar um link para seus amigos para que eles possam clicar para ver a mesma lista filtrada de filmes.</span><span class="sxs-lookup"><span data-stu-id="6c977-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="6c977-162">Observe que a URL para a solicitação HTTP POST é o mesmo que a URL para a solicitação GET (localhost: XXXXX/Movies/Index) – não há nenhuma informação de pesquisa na URL em si.</span><span class="sxs-lookup"><span data-stu-id="6c977-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="6c977-163">Direita agora, as informações de cadeia de caracteres de pesquisa são enviadas ao servidor como um valor de campo do formulário.</span><span class="sxs-lookup"><span data-stu-id="6c977-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="6c977-164">Isso significa que não é possível capturar essas informações de pesquisa para marcar ou enviar a amigos em uma URL.</span><span class="sxs-lookup"><span data-stu-id="6c977-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="6c977-165">A solução é usar uma sobrecarga `BeginForm` que especifica que a solicitação POST deve adicionar as informações de pesquisa para a URL e que deve ser roteado para o `HttpGet` versão do `Index` método.</span><span class="sxs-lookup"><span data-stu-id="6c977-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="6c977-166">Substituir existente sem parâmetros `BeginForm` método com a seguinte marcação:</span><span class="sxs-lookup"><span data-stu-id="6c977-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="6c977-168">Agora, quando você enviar uma pesquisa, a URL contém uma cadeia de caracteres de consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="6c977-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="6c977-169">A pesquisa também irá para o método de ação `HttpGet Index`, mesmo se você tiver um método `HttpPost Index`.</span><span class="sxs-lookup"><span data-stu-id="6c977-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="6c977-171">Adicionando uma pesquisa por gênero</span><span class="sxs-lookup"><span data-stu-id="6c977-171">Adding Search by Genre</span></span>

<span data-ttu-id="6c977-172">Se você tiver adicionado a `HttpPost` versão do `Index` método, excluí-lo agora.</span><span class="sxs-lookup"><span data-stu-id="6c977-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="6c977-173">Em seguida, você adicionará um recurso para permitir que os usuários a pesquisar filmes por gênero.</span><span class="sxs-lookup"><span data-stu-id="6c977-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="6c977-174">Substitua o método `Index` pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6c977-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="6c977-175">Esta versão dos `Index` método utiliza um parâmetro adicional, ou seja, `movieGenre`.</span><span class="sxs-lookup"><span data-stu-id="6c977-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="6c977-176">As primeiras linhas de código é criar um `List` objeto para manter os gêneros de filme do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c977-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="6c977-177">O código a seguir é uma consulta LINQ que recupera todos os gêneros do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c977-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="6c977-178">O código usa o `AddRange` método de genérica `List` coleção para adicionar todos os gêneros distintos à lista.</span><span class="sxs-lookup"><span data-stu-id="6c977-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="6c977-179">(Sem o `Distinct` modificador, gêneros duplicados seriam adicionados — por exemplo, o comédia seria adicionada duas vezes em nosso exemplo).</span><span class="sxs-lookup"><span data-stu-id="6c977-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="6c977-180">O código, em seguida, armazena a lista de gêneros no `ViewBag.MovieGenre` objeto.</span><span class="sxs-lookup"><span data-stu-id="6c977-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="6c977-181">Armazenar dados de categoria (tal um gêneros de filme) como um [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) do objeto em um `ViewBag`, em seguida, acessar os dados de categoria em uma caixa de listagem suspensa é uma abordagem típica para aplicativos MVC.</span><span class="sxs-lookup"><span data-stu-id="6c977-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="6c977-182">O código a seguir mostra como verificar o `movieGenre` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6c977-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="6c977-183">Se não estiver vazia, o código ainda mais restringe a consulta de filmes para limitar os filmes selecionados para o gênero especificado.</span><span class="sxs-lookup"><span data-stu-id="6c977-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="6c977-184">Conforme mencionado anteriormente, a consulta não é executada no banco de dados até que a lista de filmes é iterada (o que ocorre no modo de exibição, após o `Index` retorna do método de ação).</span><span class="sxs-lookup"><span data-stu-id="6c977-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="6c977-185">Adicionando marcação para a exibição de índice para dar suporte à pesquisa por gênero</span><span class="sxs-lookup"><span data-stu-id="6c977-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="6c977-186">Adicionar um `Html.DropDownList` auxiliar para o *Views\Movies\Index.cshtml* do arquivo, antes de `TextBox` auxiliar.</span><span class="sxs-lookup"><span data-stu-id="6c977-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="6c977-187">A marcação concluída é mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="6c977-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="6c977-188">No código a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c977-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="6c977-189">O parâmetro "MovieGenre" fornece a chave para o `DropDownList` auxiliar para localizar um `IEnumerable<SelectListItem>` no `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="6c977-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="6c977-190">O `ViewBag` foi populada no método de ação:</span><span class="sxs-lookup"><span data-stu-id="6c977-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="6c977-191">O parâmetro "All" fornece um rótulo de opção.</span><span class="sxs-lookup"><span data-stu-id="6c977-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="6c977-192">Se você inspecionar essa escolha no seu navegador, você verá que o atributo "value" está vazio.</span><span class="sxs-lookup"><span data-stu-id="6c977-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="6c977-193">Uma vez que o nosso controlador apenas filtra `if` a cadeia de caracteres não é `null` ou vazio, enviando um valor vazio para `movieGenre` mostra todos os gêneros.</span><span class="sxs-lookup"><span data-stu-id="6c977-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="6c977-194">Você também pode definir uma opção a ser selecionado por padrão.</span><span class="sxs-lookup"><span data-stu-id="6c977-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="6c977-195">Se você quisesse "Comédia" como a opção padrão, altere o código no controlador da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6c977-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="6c977-196">Execute o aplicativo e navegue até */Movies/Index*.</span><span class="sxs-lookup"><span data-stu-id="6c977-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="6c977-197">Tente uma pesquisa por gênero, nome do filme e ambos os critérios.</span><span class="sxs-lookup"><span data-stu-id="6c977-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="6c977-198">Nesta seção, você criou um método de ação de pesquisa e uma exibição que permitem aos usuários a pesquisar por título do filme e gênero.</span><span class="sxs-lookup"><span data-stu-id="6c977-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="6c977-199">Na próxima seção, você verá como adicionar uma propriedade para o `Movie` modelo e como adicionar um inicializador que criará automaticamente um banco de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="6c977-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6c977-200">[Anterior](examining-the-edit-methods-and-edit-view.md)
> [Próximo](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="6c977-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
