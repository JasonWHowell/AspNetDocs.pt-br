---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: Criar uma API REST com roteamento de atributos no ASP.NET Web API 2 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188751"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="7afe2-102">Criar uma API REST com roteamento de atributos no ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="7afe2-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="7afe2-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7afe2-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7afe2-104">A API da Web 2 dá suporte a um novo tipo de roteamento, chamado *Roteamento de atributos*.</span><span class="sxs-lookup"><span data-stu-id="7afe2-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="7afe2-105">Para obter uma visão geral do roteamento de atributos, consulte [Roteamento de atributos na API Web 2](attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="7afe2-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="7afe2-106">Neste tutorial, você usará o roteamento de atributos para criar uma API REST para uma coleção de livros.</span><span class="sxs-lookup"><span data-stu-id="7afe2-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="7afe2-107">A API dará suporte às seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="7afe2-107">The API will support the following actions:</span></span>

| <span data-ttu-id="7afe2-108">Ação</span><span class="sxs-lookup"><span data-stu-id="7afe2-108">Action</span></span> | <span data-ttu-id="7afe2-109">URI de exemplo</span><span class="sxs-lookup"><span data-stu-id="7afe2-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="7afe2-110">Obtenha uma lista de todos os livros.</span><span class="sxs-lookup"><span data-stu-id="7afe2-110">Get a list of all books.</span></span> | <span data-ttu-id="7afe2-111">/api/books</span><span class="sxs-lookup"><span data-stu-id="7afe2-111">/api/books</span></span> |
| <span data-ttu-id="7afe2-112">Obter um livro por ID.</span><span class="sxs-lookup"><span data-stu-id="7afe2-112">Get a book by ID.</span></span> | <span data-ttu-id="7afe2-113">/api/books/1</span><span class="sxs-lookup"><span data-stu-id="7afe2-113">/api/books/1</span></span> |
| <span data-ttu-id="7afe2-114">Obtenha os detalhes de um livro.</span><span class="sxs-lookup"><span data-stu-id="7afe2-114">Get the details of a book.</span></span> | <span data-ttu-id="7afe2-115">/api/books/1/details</span><span class="sxs-lookup"><span data-stu-id="7afe2-115">/api/books/1/details</span></span> |
| <span data-ttu-id="7afe2-116">Obter uma lista de livros por gênero.</span><span class="sxs-lookup"><span data-stu-id="7afe2-116">Get a list of books by genre.</span></span> | <span data-ttu-id="7afe2-117">/api/books/fantasy</span><span class="sxs-lookup"><span data-stu-id="7afe2-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="7afe2-118">Obter uma lista de livros por data de publicação.</span><span class="sxs-lookup"><span data-stu-id="7afe2-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="7afe2-119">/API/Books/Date/2013-02-16/API/Books/Date/2013/02/16 (formulário alternativo)</span><span class="sxs-lookup"><span data-stu-id="7afe2-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="7afe2-120">Obtenha uma lista de livros por um autor específico.</span><span class="sxs-lookup"><span data-stu-id="7afe2-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="7afe2-121">/api/authors/1/books</span><span class="sxs-lookup"><span data-stu-id="7afe2-121">/api/authors/1/books</span></span> |

<span data-ttu-id="7afe2-122">Todos os métodos são somente leitura (solicitações HTTP GET).</span><span class="sxs-lookup"><span data-stu-id="7afe2-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="7afe2-123">Para a camada de dados, usaremos Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="7afe2-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="7afe2-124">Os registros de livros terão os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="7afe2-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="7afe2-125">ID</span><span class="sxs-lookup"><span data-stu-id="7afe2-125">ID</span></span>
- <span data-ttu-id="7afe2-126">Título</span><span class="sxs-lookup"><span data-stu-id="7afe2-126">Title</span></span>
- <span data-ttu-id="7afe2-127">Gênero</span><span class="sxs-lookup"><span data-stu-id="7afe2-127">Genre</span></span>
- <span data-ttu-id="7afe2-128">Data da publicação</span><span class="sxs-lookup"><span data-stu-id="7afe2-128">Publication date</span></span>
- <span data-ttu-id="7afe2-129">Preço</span><span class="sxs-lookup"><span data-stu-id="7afe2-129">Price</span></span>
- <span data-ttu-id="7afe2-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="7afe2-130">Description</span></span>
- <span data-ttu-id="7afe2-131">AuthorId (chave estrangeira para uma tabela de autores)</span><span class="sxs-lookup"><span data-stu-id="7afe2-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="7afe2-132">No entanto, para a maioria das solicitações, a API retornará um subconjunto desses dados (título, autor e gênero).</span><span class="sxs-lookup"><span data-stu-id="7afe2-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="7afe2-133">Para obter o registro completo, o cliente solicita `/api/books/{id}/details` .</span><span class="sxs-lookup"><span data-stu-id="7afe2-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7afe2-134">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7afe2-134">Prerequisites</span></span>

<span data-ttu-id="7afe2-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional ou Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="7afe2-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="7afe2-136">Criar o projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7afe2-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="7afe2-137">Comece executando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7afe2-137">Start by running Visual Studio.</span></span> <span data-ttu-id="7afe2-138">No menu **arquivo** , selecione **novo** e **projeto**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="7afe2-139">Expanda **Installed**a  >  categoria**Visual C#** instalada.</span><span class="sxs-lookup"><span data-stu-id="7afe2-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="7afe2-140">Em **Visual C#**, selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="7afe2-141">Na lista de modelos de projeto, selecione **ASP.NET aplicativo Web (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="7afe2-142">Nomeie o projeto &quot; BooksAPI &quot; .</span><span class="sxs-lookup"><span data-stu-id="7afe2-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="7afe2-143">Na caixa de diálogo **novo aplicativo Web ASP.net** , selecione o modelo **vazio** .</span><span class="sxs-lookup"><span data-stu-id="7afe2-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="7afe2-144">Em "adicionar pastas e referências principais para", marque a caixa de seleção **API da Web** .</span><span class="sxs-lookup"><span data-stu-id="7afe2-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="7afe2-145">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="7afe2-146">Isso cria um projeto de esqueleto configurado para a funcionalidade da API Web.</span><span class="sxs-lookup"><span data-stu-id="7afe2-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="7afe2-147">Modelos de domínio</span><span class="sxs-lookup"><span data-stu-id="7afe2-147">Domain Models</span></span>

<span data-ttu-id="7afe2-148">Em seguida, adicione classes para modelos de domínio.</span><span class="sxs-lookup"><span data-stu-id="7afe2-148">Next, add classes for domain models.</span></span> <span data-ttu-id="7afe2-149">No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Modelos.</span><span class="sxs-lookup"><span data-stu-id="7afe2-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="7afe2-150">Selecione **Adicionar**e selecione **classe**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="7afe2-151">Nome da classe `Author`.</span><span class="sxs-lookup"><span data-stu-id="7afe2-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="7afe2-152">Substitua o código em Author.cs pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="7afe2-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="7afe2-153">Agora, adicione outra classe chamada `Book` .</span><span class="sxs-lookup"><span data-stu-id="7afe2-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="7afe2-154">Adicionar um controlador de API Web</span><span class="sxs-lookup"><span data-stu-id="7afe2-154">Add a Web API Controller</span></span>

<span data-ttu-id="7afe2-155">Nesta etapa, adicionaremos um controlador de API da Web que usa Entity Framework como a camada de dados.</span><span class="sxs-lookup"><span data-stu-id="7afe2-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="7afe2-156">Pressione CTRL+SHIFT+B para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="7afe2-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="7afe2-157">Entity Framework usa a reflexão para descobrir as propriedades dos modelos, portanto, ele requer um assembly compilado para criar o esquema de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7afe2-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="7afe2-158">No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Controladores.</span><span class="sxs-lookup"><span data-stu-id="7afe2-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="7afe2-159">Selecione **Adicionar**e, em seguida, selecione **controlador**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="7afe2-160">Na caixa de diálogo **Adicionar Scaffold** , selecione **controlador da API Web 2 com ações, usando Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="7afe2-161">Na caixa de diálogo **Adicionar controlador** , para **nome do controlador**, insira &quot; BooksController &quot; .</span><span class="sxs-lookup"><span data-stu-id="7afe2-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="7afe2-162">Marque a &quot; caixa de seleção Usar ações do controlador assíncrono &quot; .</span><span class="sxs-lookup"><span data-stu-id="7afe2-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="7afe2-163">Para **classe de modelo**, selecione &quot; livro &quot; .</span><span class="sxs-lookup"><span data-stu-id="7afe2-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="7afe2-164">(Se você não vir a `Book` classe listada no menu suspenso, certifique-se de que você criou o projeto.) Em seguida, clique no botão "+".</span><span class="sxs-lookup"><span data-stu-id="7afe2-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="7afe2-165">Clique em **Adicionar** na caixa de diálogo **novo contexto de dados** .</span><span class="sxs-lookup"><span data-stu-id="7afe2-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="7afe2-166">Clique em **Adicionar** na caixa de diálogo **Adicionar controlador** .</span><span class="sxs-lookup"><span data-stu-id="7afe2-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="7afe2-167">O scaffolding adiciona uma classe chamada `BooksController` que define o controlador da API.</span><span class="sxs-lookup"><span data-stu-id="7afe2-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="7afe2-168">Ele também adiciona uma classe chamada `BooksAPIContext` na pasta modelos, que define o contexto de dados para Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="7afe2-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="7afe2-169">Propagar o banco de dados</span><span class="sxs-lookup"><span data-stu-id="7afe2-169">Seed the Database</span></span>

<span data-ttu-id="7afe2-170">No menu ferramentas, selecione **Gerenciador de pacotes NuGet**e, em seguida, selecione **console do Gerenciador de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="7afe2-171">Na janela Console do Gerenciador de Pacotes, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7afe2-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="7afe2-172">Esse comando cria uma pasta migrações e adiciona um novo arquivo de código chamado Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="7afe2-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="7afe2-173">Abra esse arquivo e adicione o código a seguir ao `Configuration.Seed` método.</span><span class="sxs-lookup"><span data-stu-id="7afe2-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="7afe2-174">Na janela do console do Gerenciador de pacotes, digite os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="7afe2-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="7afe2-175">Esses comandos criam um banco de dados local e invocam o método semente para preencher o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7afe2-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="7afe2-176">Adicionar classes DTO</span><span class="sxs-lookup"><span data-stu-id="7afe2-176">Add DTO Classes</span></span>

<span data-ttu-id="7afe2-177">Se você executar o aplicativo agora e enviar uma solicitação GET para/API/Books/1, a resposta será semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="7afe2-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="7afe2-178">(Adicionei o recuo para facilitar a leitura.)</span><span class="sxs-lookup"><span data-stu-id="7afe2-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="7afe2-179">Em vez disso, quero que essa solicitação retorne um subconjunto dos campos.</span><span class="sxs-lookup"><span data-stu-id="7afe2-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="7afe2-180">Além disso, quero que ele retorne o nome do autor, em vez da ID do autor.</span><span class="sxs-lookup"><span data-stu-id="7afe2-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="7afe2-181">Para fazer isso, modificaremos os métodos do controlador para retornar um DTO ( *objeto de transferência de dados* ) em vez do modelo do EF.</span><span class="sxs-lookup"><span data-stu-id="7afe2-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="7afe2-182">Um DTO é um objeto projetado apenas para transportar dados.</span><span class="sxs-lookup"><span data-stu-id="7afe2-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="7afe2-183">Em Gerenciador de soluções, clique com o botão direito do mouse no projeto e selecione **Adicionar**  |  **nova pasta**.</span><span class="sxs-lookup"><span data-stu-id="7afe2-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="7afe2-184">Nomeie a pasta &quot; DTOs &quot; .</span><span class="sxs-lookup"><span data-stu-id="7afe2-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="7afe2-185">Adicione uma classe chamada `BookDto` à pasta DTOs, com a seguinte definição:</span><span class="sxs-lookup"><span data-stu-id="7afe2-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="7afe2-186">Adicione outra classe chamada `BookDetailDto`.</span><span class="sxs-lookup"><span data-stu-id="7afe2-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="7afe2-187">Em seguida, atualize a `BooksController` classe para retornar `BookDto` instâncias.</span><span class="sxs-lookup"><span data-stu-id="7afe2-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="7afe2-188">Usaremos o método [consultável. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) para projetar `Book` instâncias para `BookDto` instâncias.</span><span class="sxs-lookup"><span data-stu-id="7afe2-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="7afe2-189">Este é o código atualizado para a classe Controller.</span><span class="sxs-lookup"><span data-stu-id="7afe2-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="7afe2-190">Excluí os `PutBook` métodos, `PostBook` e `DeleteBook` , porque eles não são necessários para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7afe2-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>

<span data-ttu-id="7afe2-191">Agora, se você executar o aplicativo e solicitar/API/Books/1, o corpo da resposta deverá ser assim:</span><span class="sxs-lookup"><span data-stu-id="7afe2-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="7afe2-192">Adicionar atributos de rota</span><span class="sxs-lookup"><span data-stu-id="7afe2-192">Add Route Attributes</span></span>

<span data-ttu-id="7afe2-193">Em seguida, converteremos o controlador para usar o roteamento de atributos.</span><span class="sxs-lookup"><span data-stu-id="7afe2-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="7afe2-194">Primeiro, adicione um atributo **RoutePrefix** ao controlador.</span><span class="sxs-lookup"><span data-stu-id="7afe2-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="7afe2-195">Esse atributo define os segmentos de URI iniciais para todos os métodos neste controlador.</span><span class="sxs-lookup"><span data-stu-id="7afe2-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="7afe2-196">Em seguida, adicione atributos **[Route]** às ações do controlador, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7afe2-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="7afe2-197">O modelo de rota para cada método de controlador é o prefixo mais a cadeia de caracteres especificada no atributo de **rota** .</span><span class="sxs-lookup"><span data-stu-id="7afe2-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="7afe2-198">Para o `GetBook` método, o modelo de rota inclui a cadeia de caracteres com parâmetros &quot; {ID: int} &quot; , que corresponde se o segmento URI contém um valor inteiro.</span><span class="sxs-lookup"><span data-stu-id="7afe2-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="7afe2-199">Método</span><span class="sxs-lookup"><span data-stu-id="7afe2-199">Method</span></span> | <span data-ttu-id="7afe2-200">Modelo de rota</span><span class="sxs-lookup"><span data-stu-id="7afe2-200">Route Template</span></span> | <span data-ttu-id="7afe2-201">URI de exemplo</span><span class="sxs-lookup"><span data-stu-id="7afe2-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="7afe2-202">"API/livros"</span><span class="sxs-lookup"><span data-stu-id="7afe2-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="7afe2-203">"API/Books/{ID: int}"</span><span class="sxs-lookup"><span data-stu-id="7afe2-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="7afe2-204">Obter detalhes do livro</span><span class="sxs-lookup"><span data-stu-id="7afe2-204">Get Book Details</span></span>

<span data-ttu-id="7afe2-205">Para obter detalhes do livro, o cliente enviará uma solicitação GET para `/api/books/{id}/details` , onde *{ID}* é a ID do livro.</span><span class="sxs-lookup"><span data-stu-id="7afe2-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="7afe2-206">Adicione o método a seguir à classe `BooksController`.</span><span class="sxs-lookup"><span data-stu-id="7afe2-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="7afe2-207">Se você solicitar `/api/books/1/details` , a resposta terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="7afe2-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="7afe2-208">Obter livros por gênero</span><span class="sxs-lookup"><span data-stu-id="7afe2-208">Get Books By Genre</span></span>

<span data-ttu-id="7afe2-209">Para obter uma lista de livros em um gênero específico, o cliente enviará uma solicitação GET para `/api/books/genre` , onde *gênero* é o nome do gênero.</span><span class="sxs-lookup"><span data-stu-id="7afe2-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="7afe2-210">(Por exemplo, `/api/books/fantasy`.)</span><span class="sxs-lookup"><span data-stu-id="7afe2-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="7afe2-211">Adicione o método a seguir a `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="7afe2-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="7afe2-212">Aqui, estamos definindo uma rota que contém um parâmetro {gênero} no modelo de URI.</span><span class="sxs-lookup"><span data-stu-id="7afe2-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="7afe2-213">Observe que a API da Web é capaz de distinguir esses dois URIs e roteá-los para métodos diferentes:</span><span class="sxs-lookup"><span data-stu-id="7afe2-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="7afe2-214">Isso ocorre porque o `GetBook` método inclui uma restrição que o segmento "ID" deve ser um valor inteiro:</span><span class="sxs-lookup"><span data-stu-id="7afe2-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="7afe2-215">Se você solicitar/API/Books/Fantasy, a resposta terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="7afe2-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="7afe2-216">Obter livros por autor</span><span class="sxs-lookup"><span data-stu-id="7afe2-216">Get Books By Author</span></span>

<span data-ttu-id="7afe2-217">Para obter uma lista de livros de um determinado autor, o cliente enviará uma solicitação GET para `/api/authors/id/books` , onde *ID* é a ID do autor.</span><span class="sxs-lookup"><span data-stu-id="7afe2-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="7afe2-218">Adicione o método a seguir a `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="7afe2-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="7afe2-219">Este exemplo é interessante porque os &quot; livros &quot; são tratados como um recurso filho de &quot; autores &quot; .</span><span class="sxs-lookup"><span data-stu-id="7afe2-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="7afe2-220">Esse padrão é bastante comum em APIs RESTful.</span><span class="sxs-lookup"><span data-stu-id="7afe2-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="7afe2-221">O til (~) no modelo de rota substitui o prefixo de rota no atributo **RoutePrefix** .</span><span class="sxs-lookup"><span data-stu-id="7afe2-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="7afe2-222">Obter livros por data de publicação</span><span class="sxs-lookup"><span data-stu-id="7afe2-222">Get Books By Publication Date</span></span>

<span data-ttu-id="7afe2-223">Para obter uma lista de livros por data de publicação, o cliente enviará uma solicitação GET para `/api/books/date/yyyy-mm-dd` , onde *aaaa-mm-dd* é a data.</span><span class="sxs-lookup"><span data-stu-id="7afe2-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="7afe2-224">Aqui está uma maneira de fazer isso:</span><span class="sxs-lookup"><span data-stu-id="7afe2-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="7afe2-225">O `{pubdate:datetime}` parâmetro é restrito para corresponder a um valor **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="7afe2-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="7afe2-226">Isso funciona, mas, na verdade, é mais permissivo do que gostaríamos.</span><span class="sxs-lookup"><span data-stu-id="7afe2-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="7afe2-227">Por exemplo, esses URIs também corresponderão à rota:</span><span class="sxs-lookup"><span data-stu-id="7afe2-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="7afe2-228">Não há nada de errado ao permitir esses URIs.</span><span class="sxs-lookup"><span data-stu-id="7afe2-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="7afe2-229">No entanto, você pode restringir a rota para um formato específico adicionando uma restrição de expressão regular ao modelo de rota:</span><span class="sxs-lookup"><span data-stu-id="7afe2-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="7afe2-230">Agora, somente as datas no formato &quot; aaaa-mm-dd &quot; corresponderão.</span><span class="sxs-lookup"><span data-stu-id="7afe2-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="7afe2-231">Observe que não usamos o Regex para validar que obtemos uma data real.</span><span class="sxs-lookup"><span data-stu-id="7afe2-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="7afe2-232">Isso é tratado quando a API Web tenta converter o segmento URI em uma instância **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="7afe2-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="7afe2-233">Uma data inválida, como ' 2012-47-99 ', não será convertida e o cliente receberá um erro 404.</span><span class="sxs-lookup"><span data-stu-id="7afe2-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="7afe2-234">Você também pode dar suporte a um separador de barra ( `/api/books/date/yyyy/mm/dd` ) adicionando outro atributo **[Route]** com um Regex diferente.</span><span class="sxs-lookup"><span data-stu-id="7afe2-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="7afe2-235">Há um detalhe sutil, mas importante, aqui.</span><span class="sxs-lookup"><span data-stu-id="7afe2-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="7afe2-236">O segundo modelo de rota tem um caractere curinga ( \* ) no início do parâmetro {pubDate}:</span><span class="sxs-lookup"><span data-stu-id="7afe2-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

<span data-ttu-id="7afe2-237">Isso informa ao mecanismo de roteamento que {pubDate} deve corresponder ao restante do URI.</span><span class="sxs-lookup"><span data-stu-id="7afe2-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="7afe2-238">Por padrão, um parâmetro de modelo corresponde a um único segmento de URI.</span><span class="sxs-lookup"><span data-stu-id="7afe2-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="7afe2-239">Nesse caso, queremos que {pubDate} abranja vários segmentos URI:</span><span class="sxs-lookup"><span data-stu-id="7afe2-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="7afe2-240">Código do controlador</span><span class="sxs-lookup"><span data-stu-id="7afe2-240">Controller Code</span></span>

<span data-ttu-id="7afe2-241">Aqui está o código completo para a classe BooksController.</span><span class="sxs-lookup"><span data-stu-id="7afe2-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="7afe2-242">Resumo</span><span class="sxs-lookup"><span data-stu-id="7afe2-242">Summary</span></span>

<span data-ttu-id="7afe2-243">O roteamento de atributos oferece mais controle e maior flexibilidade ao criar URIs para sua API.</span><span class="sxs-lookup"><span data-stu-id="7afe2-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>
