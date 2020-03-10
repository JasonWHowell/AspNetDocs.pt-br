---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Criando um ponto de extremidade OData v3 com a API Web 2 | Microsoft Docs
author: MikeWasson
description: O Protocolo Open Data (OData) é um protocolo de acesso a dados para a Web. O OData fornece uma maneira uniforme de estruturar dados, consultar os dados e manipular os dados...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556409"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="5a09c-104">Criando um ponto de extremidade OData v3 com a API Web 2</span><span class="sxs-lookup"><span data-stu-id="5a09c-104">Creating an OData v3 Endpoint with Web API 2</span></span>

<span data-ttu-id="5a09c-105">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5a09c-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5a09c-106">Baixar projeto concluído</span><span class="sxs-lookup"><span data-stu-id="5a09c-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="5a09c-107">O [protocolo Open Data](http://www.odata.org/) (OData) é um protocolo de acesso a dados para a Web.</span><span class="sxs-lookup"><span data-stu-id="5a09c-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="5a09c-108">O OData fornece uma maneira uniforme de estruturar dados, consultar os dados e manipular o conjunto de dados por meio de operações CRUD (criar, ler, atualizar e excluir).</span><span class="sxs-lookup"><span data-stu-id="5a09c-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="5a09c-109">O OData dá suporte aos formatos AtomPub (XML) e JSON.</span><span class="sxs-lookup"><span data-stu-id="5a09c-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="5a09c-110">O OData também define uma maneira de expor metadados sobre os dados.</span><span class="sxs-lookup"><span data-stu-id="5a09c-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="5a09c-111">Os clientes podem usar os metadados para descobrir as informações de tipo e as relações para o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="5a09c-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="5a09c-112">ASP.NET Web API facilita a criação de um ponto de extremidade OData para um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="5a09c-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="5a09c-113">Você pode controlar exatamente a quais operações OData o ponto de extremidade dá suporte.</span><span class="sxs-lookup"><span data-stu-id="5a09c-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="5a09c-114">Você pode hospedar vários pontos de extremidade OData, juntamente com pontos de extremidade não-OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="5a09c-115">Você tem controle total sobre o modelo de dados, a lógica de negócios de back-end e a camada de dados.</span><span class="sxs-lookup"><span data-stu-id="5a09c-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5a09c-116">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="5a09c-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="5a09c-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5a09c-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="5a09c-118">API Web 2</span><span class="sxs-lookup"><span data-stu-id="5a09c-118">Web API 2</span></span>
> - <span data-ttu-id="5a09c-119">Versão 3 do OData</span><span class="sxs-lookup"><span data-stu-id="5a09c-119">OData Version 3</span></span>
> - <span data-ttu-id="5a09c-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="5a09c-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="5a09c-121">Proxy de depuração da Web do Fiddler (opcional)</span><span class="sxs-lookup"><span data-stu-id="5a09c-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="5a09c-122">O suporte a API Web OData foi adicionado na [atualização do ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="5a09c-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="5a09c-123">No entanto, este tutorial usa scaffolding que foi adicionado no Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="5a09c-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>

<span data-ttu-id="5a09c-124">Neste tutorial, você criará um ponto de extremidade OData simples que os clientes podem consultar.</span><span class="sxs-lookup"><span data-stu-id="5a09c-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="5a09c-125">Você também criará um C# cliente para o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="5a09c-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="5a09c-126">Depois de concluir este tutorial, o próximo conjunto de tutoriais mostra como adicionar mais funcionalidade, incluindo relações de entidade, ações e $expand/$select.</span><span class="sxs-lookup"><span data-stu-id="5a09c-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="5a09c-127">Criar o projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a09c-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="5a09c-128">Adicionar um modelo de entidade</span><span class="sxs-lookup"><span data-stu-id="5a09c-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="5a09c-129">Adicionar um controlador OData</span><span class="sxs-lookup"><span data-stu-id="5a09c-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="5a09c-130">Adicionar o EDM e a rota</span><span class="sxs-lookup"><span data-stu-id="5a09c-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="5a09c-131">Propagar o banco de dados (opcional)</span><span class="sxs-lookup"><span data-stu-id="5a09c-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="5a09c-132">Explorando o ponto de extremidade OData</span><span class="sxs-lookup"><span data-stu-id="5a09c-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="5a09c-133">Formatos de serialização OData</span><span class="sxs-lookup"><span data-stu-id="5a09c-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="5a09c-134">Criar o projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a09c-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="5a09c-135">Neste tutorial, você criará um ponto de extremidade OData que dá suporte a operações CRUD básicas.</span><span class="sxs-lookup"><span data-stu-id="5a09c-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="5a09c-136">O ponto de extremidade vai expor um único recurso, uma lista de produtos.</span><span class="sxs-lookup"><span data-stu-id="5a09c-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="5a09c-137">Os tutoriais posteriores adicionarão mais recursos.</span><span class="sxs-lookup"><span data-stu-id="5a09c-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="5a09c-138">Inicie o Visual Studio e selecione **novo projeto** na página inicial.</span><span class="sxs-lookup"><span data-stu-id="5a09c-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="5a09c-139">Ou, no menu **arquivo** , selecione **novo** e **projeto**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="5a09c-140">No painel **modelos** , selecione **modelos instalados** e expanda o nó C# Visual.</span><span class="sxs-lookup"><span data-stu-id="5a09c-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="5a09c-141">Em **Visual C#** , selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="5a09c-142">Selecione **o modelo de aplicativo Web ASP.net** .</span><span class="sxs-lookup"><span data-stu-id="5a09c-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="5a09c-143">Na caixa de diálogo **novo projeto ASP.net** , selecione o modelo **vazio** .</span><span class="sxs-lookup"><span data-stu-id="5a09c-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="5a09c-144">Em &quot;adicionar pastas e referências principais para...&quot;, verifique a **API Web**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="5a09c-145">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="5a09c-146">Adicionar um modelo de entidade</span><span class="sxs-lookup"><span data-stu-id="5a09c-146">Add an Entity Model</span></span>

<span data-ttu-id="5a09c-147">Um *modelo* é um objeto que representa os dados no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a09c-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="5a09c-148">Para este tutorial, precisamos de um modelo que represente um produto.</span><span class="sxs-lookup"><span data-stu-id="5a09c-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="5a09c-149">O modelo corresponde ao nosso tipo de entidade OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="5a09c-150">No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Modelos.</span><span class="sxs-lookup"><span data-stu-id="5a09c-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="5a09c-151">No menu de contexto, selecione **Adicionar** e, em seguida, selecione **Classe**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="5a09c-152">Na caixa de diálogo **Adicionar novo** item, nomeie a classe &quot;produto&quot;.</span><span class="sxs-lookup"><span data-stu-id="5a09c-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="5a09c-153">Por convenção, as classes de modelo são colocadas na pasta modelos.</span><span class="sxs-lookup"><span data-stu-id="5a09c-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="5a09c-154">Você não precisa seguir essa convenção em seus próprios projetos, mas vamos usá-la para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5a09c-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>

<span data-ttu-id="5a09c-155">No arquivo Product.cs, adicione a seguinte definição de classe:</span><span class="sxs-lookup"><span data-stu-id="5a09c-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="5a09c-156">A propriedade ID será a chave de entidade.</span><span class="sxs-lookup"><span data-stu-id="5a09c-156">The ID property will be the entity key.</span></span> <span data-ttu-id="5a09c-157">Os clientes podem consultar produtos por ID.</span><span class="sxs-lookup"><span data-stu-id="5a09c-157">Clients can query products by ID.</span></span> <span data-ttu-id="5a09c-158">Esse campo também seria a chave primária no banco de dados back-end.</span><span class="sxs-lookup"><span data-stu-id="5a09c-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="5a09c-159">Compile o projeto agora.</span><span class="sxs-lookup"><span data-stu-id="5a09c-159">Build the project now.</span></span> <span data-ttu-id="5a09c-160">Na próxima etapa, usaremos algumas scaffolding do Visual Studio que usam a reflexão para localizar o tipo de produto.</span><span class="sxs-lookup"><span data-stu-id="5a09c-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="5a09c-161">Adicionar um controlador OData</span><span class="sxs-lookup"><span data-stu-id="5a09c-161">Add an OData Controller</span></span>

<span data-ttu-id="5a09c-162">Um *controlador* é uma classe que MANIPULA solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a09c-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="5a09c-163">Você define um controlador separado para cada conjunto de entidades no serviço OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="5a09c-164">Neste tutorial, criaremos um único controlador.</span><span class="sxs-lookup"><span data-stu-id="5a09c-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="5a09c-165">Em Gerenciador de Soluções, clique com o botão direito do mouse na pasta controladores.</span><span class="sxs-lookup"><span data-stu-id="5a09c-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="5a09c-166">Selecione **Adicionar** e, em seguida, selecione **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="5a09c-167">Na caixa de diálogo **Adicionar Scaffold** , selecione &quot;controlador ODATA da API Web 2 com ações, usando Entity Framework&quot;.</span><span class="sxs-lookup"><span data-stu-id="5a09c-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="5a09c-168">Na caixa de diálogo **Adicionar controlador** , nomeie o controlador "ProductsController".</span><span class="sxs-lookup"><span data-stu-id="5a09c-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="5a09c-169">Marque a caixa de seleção &quot;usar ações do controlador assíncrono&quot;.</span><span class="sxs-lookup"><span data-stu-id="5a09c-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="5a09c-170">Na lista suspensa **modelo** , selecione a classe produto.</span><span class="sxs-lookup"><span data-stu-id="5a09c-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="5a09c-171">Clique no botão **novo contexto de dados...** .</span><span class="sxs-lookup"><span data-stu-id="5a09c-171">Click the **New data context...** button.</span></span> <span data-ttu-id="5a09c-172">Deixe o nome padrão para o tipo de contexto de dados e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="5a09c-173">Clique em Adicionar na caixa de diálogo Adicionar controlador para adicionar o controlador.</span><span class="sxs-lookup"><span data-stu-id="5a09c-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="5a09c-174">Observação: se você receber uma mensagem de erro dizendo &quot;ocorreu um erro ao obter o tipo...&quot;, certifique-se de ter criado o projeto do Visual Studio depois de adicionar a classe Product.</span><span class="sxs-lookup"><span data-stu-id="5a09c-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="5a09c-175">O scaffolding usa a reflexão para encontrar a classe.</span><span class="sxs-lookup"><span data-stu-id="5a09c-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="5a09c-176">O scaffolding adiciona dois arquivos de código ao projeto:</span><span class="sxs-lookup"><span data-stu-id="5a09c-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="5a09c-177">Products.cs define o controlador da API Web que implementa o ponto de extremidade OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="5a09c-178">O ProductServiceContext.cs fornece métodos para consultar o banco de dados subjacente, usando Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="5a09c-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="5a09c-179">Adicionar o EDM e a rota</span><span class="sxs-lookup"><span data-stu-id="5a09c-179">Add the EDM and Route</span></span>

<span data-ttu-id="5a09c-180">Em Gerenciador de Soluções, expanda a pasta\_iniciar o aplicativo e abra o arquivo chamado WebApiConfig.cs.</span><span class="sxs-lookup"><span data-stu-id="5a09c-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="5a09c-181">Essa classe contém o código de configuração para a API da Web.</span><span class="sxs-lookup"><span data-stu-id="5a09c-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="5a09c-182">Substitua este código pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="5a09c-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="5a09c-183">Esse código faz duas coisas:</span><span class="sxs-lookup"><span data-stu-id="5a09c-183">This code does two things:</span></span>

- <span data-ttu-id="5a09c-184">Cria um Modelo de Dados de Entidade (EDM) para o ponto de extremidade OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="5a09c-185">Adiciona uma rota para o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="5a09c-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="5a09c-186">Um EDM é um modelo abstrato dos dados.</span><span class="sxs-lookup"><span data-stu-id="5a09c-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="5a09c-187">O EDM é usado para criar o documento de metadados e definir os URIs para o serviço.</span><span class="sxs-lookup"><span data-stu-id="5a09c-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="5a09c-188">O **ODataConventionModelBuilder** cria um EDM usando um conjunto de convenções de nomenclatura padrão EDM.</span><span class="sxs-lookup"><span data-stu-id="5a09c-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="5a09c-189">Essa abordagem requer o mínimo de código.</span><span class="sxs-lookup"><span data-stu-id="5a09c-189">This approach requires the least code.</span></span> <span data-ttu-id="5a09c-190">Se você quiser mais controle sobre o EDM, poderá usar a classe **ODataModelBuilder** para criar o EDM adicionando Propriedades, chaves e propriedades de navegação explicitamente.</span><span class="sxs-lookup"><span data-stu-id="5a09c-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="5a09c-191">O método **EntitySet** adiciona um conjunto de entidades ao EDM:</span><span class="sxs-lookup"><span data-stu-id="5a09c-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="5a09c-192">A cadeia de caracteres "Products" define o nome do conjunto de entidades.</span><span class="sxs-lookup"><span data-stu-id="5a09c-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="5a09c-193">O nome do controlador deve corresponder ao nome do conjunto de entidades.</span><span class="sxs-lookup"><span data-stu-id="5a09c-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="5a09c-194">Neste tutorial, o conjunto de entidades é chamado de "produtos" e o controlador é nomeado `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="5a09c-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="5a09c-195">Se você tiver nomeado o conjunto de entidades "ProductSet", você nomearia o controlador `ProductSetController`.</span><span class="sxs-lookup"><span data-stu-id="5a09c-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="5a09c-196">Observe que um ponto de extremidade pode ter vários conjuntos de entidades.</span><span class="sxs-lookup"><span data-stu-id="5a09c-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="5a09c-197">Chame **EntitySet&lt;t&gt;** para cada conjunto de entidades e, em seguida, defina um controlador correspondente.</span><span class="sxs-lookup"><span data-stu-id="5a09c-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="5a09c-198">O método **MapODataRoute** adiciona uma rota para o ponto de extremidade OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="5a09c-199">O primeiro parâmetro é um nome amigável para a rota.</span><span class="sxs-lookup"><span data-stu-id="5a09c-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="5a09c-200">Os clientes do seu serviço não veem esse nome.</span><span class="sxs-lookup"><span data-stu-id="5a09c-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="5a09c-201">O segundo parâmetro é o prefixo de URI para o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="5a09c-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="5a09c-202">Dado esse código, o URI para o conjunto de entidades Products é http://<em>hostname</em>/OData/Products.</span><span class="sxs-lookup"><span data-stu-id="5a09c-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="5a09c-203">Seu aplicativo pode ter mais de um ponto de extremidade OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="5a09c-204">Para cada ponto de extremidade, chame <strong>MapODataRoute</strong> e forneça um nome de rota exclusivo e um prefixo URI exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5a09c-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="5a09c-205">Propagar o banco de dados (opcional)</span><span class="sxs-lookup"><span data-stu-id="5a09c-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="5a09c-206">Nesta etapa, você usará Entity Framework para propagar o banco de dados com algum dado de teste.</span><span class="sxs-lookup"><span data-stu-id="5a09c-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="5a09c-207">Esta etapa é opcional, mas permite testar seu ponto de extremidade OData imediatamente.</span><span class="sxs-lookup"><span data-stu-id="5a09c-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="5a09c-208">No menu **ferramentas** , selecione **Gerenciador de pacotes NuGet**e, em seguida, selecione **console do Gerenciador de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="5a09c-209">Na janela Console do Gerenciador de Pacotes, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5a09c-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="5a09c-210">Isso adiciona uma pasta chamada migrações e um arquivo de código chamado Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="5a09c-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="5a09c-211">Abra esse arquivo e adicione o código a seguir ao método `Configuration.Seed`.</span><span class="sxs-lookup"><span data-stu-id="5a09c-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="5a09c-212">Na janela do console do Gerenciador de pacotes, digite os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5a09c-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="5a09c-213">Esses comandos geram código que cria o banco de dados e, em seguida, executa esse código.</span><span class="sxs-lookup"><span data-stu-id="5a09c-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="5a09c-214">Explorando o ponto de extremidade OData</span><span class="sxs-lookup"><span data-stu-id="5a09c-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="5a09c-215">Nesta seção, usaremos o [proxy de depuração da Web do Fiddler](http://www.fiddler2.com) para enviar solicitações ao ponto de extremidade e examinar as mensagens de resposta.</span><span class="sxs-lookup"><span data-stu-id="5a09c-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="5a09c-216">Isso ajudará você a entender os recursos de um ponto de extremidade OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="5a09c-217">No Visual Studio, pressione F5 para iniciar a depuração.</span><span class="sxs-lookup"><span data-stu-id="5a09c-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="5a09c-218">Por padrão, o Visual Studio abre o navegador para `http://localhost:*port*`, em que *porta* é o número da porta configurado nas configurações do projeto.</span><span class="sxs-lookup"><span data-stu-id="5a09c-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="5a09c-219">Você pode alterar o número da porta nas configurações do projeto.</span><span class="sxs-lookup"><span data-stu-id="5a09c-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="5a09c-220">Em Gerenciador de Soluções, clique com o botão direito do mouse no projeto e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="5a09c-221">Na janela Propriedades, selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="5a09c-222">Insira o número da porta na **URL do projeto**.</span><span class="sxs-lookup"><span data-stu-id="5a09c-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="5a09c-223">Documento de serviço</span><span class="sxs-lookup"><span data-stu-id="5a09c-223">Service Document</span></span>

<span data-ttu-id="5a09c-224">O *documento de serviço* contém uma lista dos conjuntos de entidades para o ponto de extremidade OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="5a09c-225">Para obter o documento de serviço, envie uma solicitação GET para o URI raiz do serviço.</span><span class="sxs-lookup"><span data-stu-id="5a09c-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="5a09c-226">Usando o Fiddler, insira o seguinte URI na guia **compositor** : `http://localhost:port/odata/`, em que *Port* é o número da porta.</span><span class="sxs-lookup"><span data-stu-id="5a09c-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="5a09c-227">Clique no botão **Executar** .</span><span class="sxs-lookup"><span data-stu-id="5a09c-227">Click the **Execute** button.</span></span> <span data-ttu-id="5a09c-228">O Fiddler envia uma solicitação HTTP GET para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a09c-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="5a09c-229">Você deve ver a resposta na lista de sessões da Web.</span><span class="sxs-lookup"><span data-stu-id="5a09c-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="5a09c-230">Se tudo estiver funcionando, o código de status será 200.</span><span class="sxs-lookup"><span data-stu-id="5a09c-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="5a09c-231">Clique duas vezes na resposta na lista sessões da Web para ver os detalhes da mensagem de resposta na guia inspetores.</span><span class="sxs-lookup"><span data-stu-id="5a09c-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="5a09c-232">A mensagem de resposta HTTP bruta deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="5a09c-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="5a09c-233">Por padrão, a API da Web retorna o documento de serviço no formato AtomPub.</span><span class="sxs-lookup"><span data-stu-id="5a09c-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="5a09c-234">Para solicitar o JSON, adicione o seguinte cabeçalho à solicitação HTTP:</span><span class="sxs-lookup"><span data-stu-id="5a09c-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="5a09c-235">Agora, a resposta HTTP contém uma carga JSON:</span><span class="sxs-lookup"><span data-stu-id="5a09c-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="5a09c-236">Documento de metadados de serviço</span><span class="sxs-lookup"><span data-stu-id="5a09c-236">Service Metadata Document</span></span>

<span data-ttu-id="5a09c-237">O *documento de metadados de serviço* descreve o modelo de dados do serviço, usando uma linguagem XML chamada de CSDL (linguagem de definição de esquema conceitual).</span><span class="sxs-lookup"><span data-stu-id="5a09c-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="5a09c-238">O documento de metadados mostra a estrutura dos dados no serviço e pode ser usado para gerar o código do cliente.</span><span class="sxs-lookup"><span data-stu-id="5a09c-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="5a09c-239">Para obter o documento de metadados, envie uma solicitação GET para `http://localhost:port/odata/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="5a09c-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="5a09c-240">Aqui estão os metadados para o ponto de extremidade mostrado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5a09c-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="5a09c-241">Conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="5a09c-241">Entity Set</span></span>

<span data-ttu-id="5a09c-242">Para obter o conjunto de entidades de produtos, envie uma solicitação GET para `http://localhost:port/odata/Products`.</span><span class="sxs-lookup"><span data-stu-id="5a09c-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="5a09c-243">Entidade</span><span class="sxs-lookup"><span data-stu-id="5a09c-243">Entity</span></span>

<span data-ttu-id="5a09c-244">Para obter um produto individual, envie uma solicitação GET para `http://localhost:port/odata/Products(1)`, onde "1" é a ID do produto.</span><span class="sxs-lookup"><span data-stu-id="5a09c-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="5a09c-245">Formatos de serialização OData</span><span class="sxs-lookup"><span data-stu-id="5a09c-245">OData Serialization Formats</span></span>

<span data-ttu-id="5a09c-246">O OData dá suporte a vários formatos de serialização:</span><span class="sxs-lookup"><span data-stu-id="5a09c-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="5a09c-247">Pub (XML) Atom</span><span class="sxs-lookup"><span data-stu-id="5a09c-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="5a09c-248">JSON "Light" (introduzido no OData v3)</span><span class="sxs-lookup"><span data-stu-id="5a09c-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="5a09c-249">JSON "detalhado" (OData v2)</span><span class="sxs-lookup"><span data-stu-id="5a09c-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="5a09c-250">Por padrão, a API Web usa o formato "Light" de AtomPubJSON.</span><span class="sxs-lookup"><span data-stu-id="5a09c-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="5a09c-251">Para obter o formato AtomPub, defina o cabeçalho Accept como "Application/Atom + XML".</span><span class="sxs-lookup"><span data-stu-id="5a09c-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="5a09c-252">Aqui está um exemplo de corpo de resposta:</span><span class="sxs-lookup"><span data-stu-id="5a09c-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="5a09c-253">Você pode ver uma desvantagem óbvia do formato Atom: é muito mais detalhado do que a luz JSON.</span><span class="sxs-lookup"><span data-stu-id="5a09c-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="5a09c-254">No entanto, se você tiver um cliente que entenda AtomPub, o cliente poderá preferir esse formato em JSON.</span><span class="sxs-lookup"><span data-stu-id="5a09c-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="5a09c-255">Esta é a versão clara do JSON da mesma entidade:</span><span class="sxs-lookup"><span data-stu-id="5a09c-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="5a09c-256">O formato JSON Light foi introduzido na versão 3 do protocolo OData.</span><span class="sxs-lookup"><span data-stu-id="5a09c-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="5a09c-257">Para compatibilidade com versões anteriores, um cliente pode solicitar o formato JSON "detalhado" mais antigo.</span><span class="sxs-lookup"><span data-stu-id="5a09c-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="5a09c-258">Para solicitar o JSON detalhado, defina o cabeçalho Accept como `application/json;odata=verbose`.</span><span class="sxs-lookup"><span data-stu-id="5a09c-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="5a09c-259">Esta é a versão detalhada:</span><span class="sxs-lookup"><span data-stu-id="5a09c-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="5a09c-260">Esse formato transmite mais metadados no corpo da resposta, o que pode adicionar uma sobrecarga considerável em uma sessão inteira.</span><span class="sxs-lookup"><span data-stu-id="5a09c-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="5a09c-261">Além disso, ele adiciona um nível de indireção encapsulando o objeto em uma propriedade chamada "d".</span><span class="sxs-lookup"><span data-stu-id="5a09c-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a09c-262">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a09c-262">Next Steps</span></span>

- [<span data-ttu-id="5a09c-263">Adicionar relações de entidade</span><span class="sxs-lookup"><span data-stu-id="5a09c-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="5a09c-264">Adicionar ações OData</span><span class="sxs-lookup"><span data-stu-id="5a09c-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="5a09c-265">Chamar o serviço OData de um cliente .NET</span><span class="sxs-lookup"><span data-stu-id="5a09c-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
