---
ms.openlocfilehash: a0546c44284a78ce0e8d06b0f2b9f65ecf66fac7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031683"
---

<span data-ttu-id="d1773-101">A anotação de dados `[Column(TypeName = "decimal(18, 2)")]` é necessária para que o Entity Framework Core possa mapear corretamente o `Price` para a moeda no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d1773-101">The `[Column(TypeName = "decimal(18, 2)")]` data annotation is required so Entity Framework Core can correctly map `Price` to currency in the database.</span></span> <span data-ttu-id="d1773-102">Para obter mais informações, veja [Tipos de Dados](/ef/core/modeling/relational/data-types).</span><span class="sxs-lookup"><span data-stu-id="d1773-102">For more information, see [Data Types](/ef/core/modeling/relational/data-types).</span></span>

<span data-ttu-id="d1773-103">O modelo concluído:</span><span class="sxs-lookup"><span data-stu-id="d1773-103">The completed model:</span></span>

[!code-csharp[Main](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/MovieDateFixed.cs?name=snippet_1)]

<span data-ttu-id="d1773-104">[DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) é abordado no próximo tutorial.</span><span class="sxs-lookup"><span data-stu-id="d1773-104">[DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) is covered in the next tutorial.</span></span> <span data-ttu-id="d1773-105">O atributo [Display](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.metadata.displaymetadata) especifica o que deve ser exibido no nome de um campo (neste caso, “Release Date” em vez de “ReleaseDate”).</span><span class="sxs-lookup"><span data-stu-id="d1773-105">The [Display](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.metadata.displaymetadata) attribute specifies what to display for the name of a field (in this case "Release Date" instead of "ReleaseDate").</span></span> <span data-ttu-id="d1773-106">O atributo [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) especifica o tipo de dados (Data) e, portanto, as informações de hora armazenadas no campo não são exibidas.</span><span class="sxs-lookup"><span data-stu-id="d1773-106">The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (Date), so the time information stored in the field isn't displayed.</span></span>

<span data-ttu-id="d1773-107">Procure Pages/Movies e focalize um link **Editar** para ver a URL de destino.</span><span class="sxs-lookup"><span data-stu-id="d1773-107">Browse to Pages/Movies and  hover over an **Edit** link to see the target URL.</span></span>

![São mostrados uma janela do navegador com o mouse sobre o link de edição e um link da URL http://localhost:1234/Movies/Edit/5](~/tutorials/razor-pages/da1/edit7.png)

<span data-ttu-id="d1773-109">Os links **Editar**, **Detalhes** e **Excluir** são gerados pelo [Auxiliar de Marcação de Âncora](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) no arquivo *Pages/Movies/Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="d1773-109">The **Edit**, **Details**, and **Delete** links are generated by the [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) in the *Pages/Movies/Index.cshtml* file.</span></span>

[!code-cshtml[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?highlight=16-18&range=32-)]

<span data-ttu-id="d1773-110">Os [Auxiliares de Marcação](xref:mvc/views/tag-helpers/intro) permitem que o código do servidor participe da criação e renderização de elementos HTML em arquivos do Razor.</span><span class="sxs-lookup"><span data-stu-id="d1773-110">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span> <span data-ttu-id="d1773-111">No código anterior, o `AnchorTagHelper` gera dinamicamente o valor do atributo `href` HTML da página Razor (a rota é relativa), o `asp-page` e a ID da rota (`asp-route-id`).</span><span class="sxs-lookup"><span data-stu-id="d1773-111">In the preceding code, the `AnchorTagHelper` dynamically generates the HTML `href` attribute value from the Razor Page (the route is relative), the `asp-page`,  and the route id (`asp-route-id`).</span></span> <span data-ttu-id="d1773-112">Consulte [Geração de URL para Páginas](xref:razor-pages/index#url-generation-for-pages) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d1773-112">See [URL generation for Pages](xref:razor-pages/index#url-generation-for-pages) for more information.</span></span>

<span data-ttu-id="d1773-113">Use **Exibir Código-fonte** em seu navegador favorito para examinar a marcação gerada.</span><span class="sxs-lookup"><span data-stu-id="d1773-113">Use **View Source** from your favorite browser to examine the generated markup.</span></span> <span data-ttu-id="d1773-114">Uma parte do HTML gerado é mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="d1773-114">A portion of the generated HTML is shown below:</span></span>

```html
<td>
  <a href="/Movies/Edit?id=1">Edit</a> |
  <a href="/Movies/Details?id=1">Details</a> |
  <a href="/Movies/Delete?id=1">Delete</a>
</td>
```

<span data-ttu-id="d1773-115">Os links gerados dinamicamente passam a ID de filme com uma cadeia de consulta (por exemplo, `http://localhost:5000/Movies/Details?id=2`).</span><span class="sxs-lookup"><span data-stu-id="d1773-115">The dynamically-generated links pass the movie ID with a query string (for example, `http://localhost:5000/Movies/Details?id=2`).</span></span>

<span data-ttu-id="d1773-116">Atualize as Páginas Editar, Detalhes e Excluir do Razor para que elas usem o modelo de rota “{id:int}”.</span><span class="sxs-lookup"><span data-stu-id="d1773-116">Update the Edit, Details, and Delete Razor Pages to use the "{id:int}" route template.</span></span> <span data-ttu-id="d1773-117">Altere a diretiva de página de cada uma dessas páginas de `@page` para `@page "{id:int}"`.</span><span class="sxs-lookup"><span data-stu-id="d1773-117">Change the page directive for each of these pages from `@page` to `@page "{id:int}"`.</span></span> <span data-ttu-id="d1773-118">Execute o aplicativo e, em seguida, exiba o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="d1773-118">Run the app and then view source.</span></span> <span data-ttu-id="d1773-119">O HTML gerado adiciona a ID à parte do caminho da URL:</span><span class="sxs-lookup"><span data-stu-id="d1773-119">The generated HTML adds the ID to the path portion of the URL:</span></span>

```html
<td>
  <a href="/Movies/Edit/1">Edit</a> |
  <a href="/Movies/Details/1">Details</a> |
  <a href="/Movies/Delete/1">Delete</a>
</td>
```

<span data-ttu-id="d1773-120">Uma solicitação para a página com o modelo de rota “{id:int}” que **não** inclui o inteiro retornará um erro HTTP 404 (não encontrado).</span><span class="sxs-lookup"><span data-stu-id="d1773-120">A request to the page with the "{id:int}" route template that does **not** include the integer will return an HTTP 404 (not found) error.</span></span> <span data-ttu-id="d1773-121">Por exemplo, `http://localhost:5000/Movies/Details` retornará um erro 404.</span><span class="sxs-lookup"><span data-stu-id="d1773-121">For example, `http://localhost:5000/Movies/Details` will return a 404 error.</span></span> <span data-ttu-id="d1773-122">Para tornar a ID opcional, acrescente `?` à restrição de rota:</span><span class="sxs-lookup"><span data-stu-id="d1773-122">To make the ID optional, append `?` to the route constraint:</span></span>

 ```cshtml
@page "{id:int?}"
```

::: moniker range="= aspnetcore-2.0"

### <a name="update-concurrency-exception-handling"></a><span data-ttu-id="d1773-123">Atualizar o tratamento de exceção de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="d1773-123">Update concurrency exception handling</span></span>

<span data-ttu-id="d1773-124">Atualize o método `OnPostAsync` no arquivo *Pages/Movies/Edit.cshtml.cs*.</span><span class="sxs-lookup"><span data-stu-id="d1773-124">Update the `OnPostAsync` method in the *Pages/Movies/Edit.cshtml.cs* file.</span></span> <span data-ttu-id="d1773-125">O seguinte código realçado mostra as alterações:</span><span class="sxs-lookup"><span data-stu-id="d1773-125">The following highlighted code shows the changes:</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Edit.cshtml.cs?name=snippet1&highlight=16-23)]

<span data-ttu-id="d1773-126">O código anterior apenas detecta as exceções de simultaneidade quando o primeiro cliente simultâneo exclui o filme e o segundo cliente simultâneo posta alterações no filme.</span><span class="sxs-lookup"><span data-stu-id="d1773-126">The previous code only detects concurrency exceptions when the first concurrent client deletes the movie, and the second concurrent client posts changes to the movie.</span></span>

<span data-ttu-id="d1773-127">Para testar o bloco `catch`:</span><span class="sxs-lookup"><span data-stu-id="d1773-127">To test the `catch` block:</span></span>

* <span data-ttu-id="d1773-128">Definir um ponto de interrupção em `catch (DbUpdateConcurrencyException)`</span><span class="sxs-lookup"><span data-stu-id="d1773-128">Set a breakpoint on `catch (DbUpdateConcurrencyException)`</span></span>
* <span data-ttu-id="d1773-129">Edite um filme.</span><span class="sxs-lookup"><span data-stu-id="d1773-129">Edit a movie.</span></span>
* <span data-ttu-id="d1773-130">Em outra janela do navegador, selecione o link **Excluir** do mesmo filme e, em seguida, exclua o filme.</span><span class="sxs-lookup"><span data-stu-id="d1773-130">In another browser window, select the **Delete** link for the same movie, and then delete the movie.</span></span>
* <span data-ttu-id="d1773-131">Na janela do navegador anterior, poste as alterações no filme.</span><span class="sxs-lookup"><span data-stu-id="d1773-131">In the previous browser window, post changes to the movie.</span></span>

<span data-ttu-id="d1773-132">O código de produção geralmente detectará conflitos de simultaneidade quando dois ou mais clientes atualizarem um registro ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="d1773-132">Production code would generally detect concurrency conflicts when two or more clients concurrently updated a record.</span></span> <span data-ttu-id="d1773-133">Confira [Lidar com conflitos de simultaneidade](xref:data/ef-rp/concurrency) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d1773-133">See [Handle concurrency conflicts](xref:data/ef-rp/concurrency) for more information.</span></span>

### <a name="posting-and-binding-review"></a><span data-ttu-id="d1773-134">Análise de postagem e associação</span><span class="sxs-lookup"><span data-stu-id="d1773-134">Posting and binding review</span></span>

<span data-ttu-id="d1773-135">Examine o arquivo *Pages/Movies/Edit.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="d1773-135">Examine the *Pages/Movies/Edit.cshtml.cs* file:</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Edit21.cshtml.cs?name=snippet2)]

<span data-ttu-id="d1773-136">Quando uma solicitação HTTP GET é feita para a página Movies/Edit (por exemplo, `http://localhost:5000/Movies/Edit/2`):</span><span class="sxs-lookup"><span data-stu-id="d1773-136">When an HTTP GET request is made to the Movies/Edit page (for example, `http://localhost:5000/Movies/Edit/2`):</span></span>

* <span data-ttu-id="d1773-137">O método `OnGetAsync` busca o filme do banco de dados e retorna o método `Page`.</span><span class="sxs-lookup"><span data-stu-id="d1773-137">The `OnGetAsync` method fetches the movie from the database and returns the `Page` method.</span></span> 
* <span data-ttu-id="d1773-138">O método `Page` renderiza a página Razor *Pages/Movies/Edit.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="d1773-138">The `Page` method renders the *Pages/Movies/Edit.cshtml* Razor Page.</span></span> <span data-ttu-id="d1773-139">O arquivo *Pages/Movies/Edit.cshtml* contém a diretiva de modelo (`@model RazorPagesMovie.Pages.Movies.EditModel`), que disponibiliza o modelo de filme na página.</span><span class="sxs-lookup"><span data-stu-id="d1773-139">The *Pages/Movies/Edit.cshtml* file contains the model directive (`@model RazorPagesMovie.Pages.Movies.EditModel`), which makes the movie model available on the page.</span></span>
* <span data-ttu-id="d1773-140">O formulário Editar é exibido com os valores do filme.</span><span class="sxs-lookup"><span data-stu-id="d1773-140">The Edit form is displayed with the values from the movie.</span></span>

<span data-ttu-id="d1773-141">Quando a página Movies/Edit é postada:</span><span class="sxs-lookup"><span data-stu-id="d1773-141">When the Movies/Edit page is posted:</span></span>

* <span data-ttu-id="d1773-142">Os valores de formulário na página são associados à propriedade `Movie`.</span><span class="sxs-lookup"><span data-stu-id="d1773-142">The form values on the page are bound to the `Movie` property.</span></span> <span data-ttu-id="d1773-143">O atributo `[BindProperty]` habilita o [Model binding](xref:mvc/models/model-binding).</span><span class="sxs-lookup"><span data-stu-id="d1773-143">The `[BindProperty]` attribute enables [Model binding](xref:mvc/models/model-binding).</span></span>

  ```csharp
  [BindProperty]
  public Movie Movie { get; set; }
  ```

* <span data-ttu-id="d1773-144">Se houver erros no estado do modelo (por exemplo, `ReleaseDate` não pode ser convertida em uma data), o formulário será postado novamente com os valores enviados.</span><span class="sxs-lookup"><span data-stu-id="d1773-144">If there are errors in the model state (for example, `ReleaseDate` cannot be converted to a date), the form is posted again with the submitted values.</span></span>
* <span data-ttu-id="d1773-145">Se não houver erros do modelo, o filme será salvo.</span><span class="sxs-lookup"><span data-stu-id="d1773-145">If there are no model errors, the movie is saved.</span></span>

<span data-ttu-id="d1773-146">Os métodos HTTP GET nas páginas Índice, Criar e Excluir do Razor seguem um padrão semelhante.</span><span class="sxs-lookup"><span data-stu-id="d1773-146">The HTTP GET methods in the Index, Create, and Delete Razor pages follow a similar pattern.</span></span> <span data-ttu-id="d1773-147">O método `OnPostAsync` HTTP POST na página Criar do Razor segue um padrão semelhante ao método `OnPostAsync` na página Editar do Razor.</span><span class="sxs-lookup"><span data-stu-id="d1773-147">The HTTP POST `OnPostAsync` method in the Create Razor Page follows a similar pattern to the `OnPostAsync` method in the Edit Razor Page.</span></span>

<span data-ttu-id="d1773-148">A pesquisa é adicionada no próximo tutorial.</span><span class="sxs-lookup"><span data-stu-id="d1773-148">Search is added in the next tutorial.</span></span>