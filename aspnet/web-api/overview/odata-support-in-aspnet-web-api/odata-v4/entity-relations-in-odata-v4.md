---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: Relações de entidade no OData v4 usando o ASP.NET Web API 2,2 | Microsoft Docs
author: MikeWasson
description: 'A maioria dos conjuntos de dados define as relações entre as entidades: os clientes têm pedidos; os livros têm autores; os produtos têm fornecedores. Usando o OData, os clientes podem navegar...'
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598689"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="a6070-104">Relações de entidade no OData v4 usando o ASP.NET Web API 2,2</span><span class="sxs-lookup"><span data-stu-id="a6070-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="a6070-105">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a6070-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="a6070-106">A maioria dos conjuntos de dados define as relações entre as entidades: os clientes têm pedidos; os livros têm autores; os produtos têm fornecedores.</span><span class="sxs-lookup"><span data-stu-id="a6070-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="a6070-107">Usando o OData, os clientes podem navegar pelas relações de entidade.</span><span class="sxs-lookup"><span data-stu-id="a6070-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="a6070-108">Dado um produto, você pode encontrar o fornecedor.</span><span class="sxs-lookup"><span data-stu-id="a6070-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="a6070-109">Você também pode criar ou remover relações.</span><span class="sxs-lookup"><span data-stu-id="a6070-109">You can also create or remove relationships.</span></span> <span data-ttu-id="a6070-110">Por exemplo, você pode definir o fornecedor de um produto.</span><span class="sxs-lookup"><span data-stu-id="a6070-110">For example, you can set the supplier for a product.</span></span>
>
> <span data-ttu-id="a6070-111">Este tutorial mostra como dar suporte a essas operações no OData v4 usando ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="a6070-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="a6070-112">O tutorial se baseia no tutorial [criar um ponto de extremidade do OData v4 usando o ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a6070-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a6070-113">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="a6070-113">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="a6070-114">API Web 2,1</span><span class="sxs-lookup"><span data-stu-id="a6070-114">Web API 2.1</span></span>
> - <span data-ttu-id="a6070-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="a6070-115">OData v4</span></span>
> - <span data-ttu-id="a6070-116">Visual Studio 2013 (Baixe o Visual Studio 2017 [aqui](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="a6070-116">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="a6070-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="a6070-117">Entity Framework 6</span></span>
> - <span data-ttu-id="a6070-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="a6070-118">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="a6070-119">Versões do tutorial</span><span class="sxs-lookup"><span data-stu-id="a6070-119">Tutorial versions</span></span>
>
> <span data-ttu-id="a6070-120">Para o OData versão 3, consulte [relações de entidade de suporte no OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span><span class="sxs-lookup"><span data-stu-id="a6070-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="a6070-121">Adicionar uma entidade de fornecedor</span><span class="sxs-lookup"><span data-stu-id="a6070-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="a6070-122">O tutorial se baseia no tutorial [criar um ponto de extremidade do OData v4 usando o ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a6070-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="a6070-123">Primeiro, precisamos de uma entidade relacionada.</span><span class="sxs-lookup"><span data-stu-id="a6070-123">First, we need a related entity.</span></span> <span data-ttu-id="a6070-124">Adicione uma classe chamada `Supplier` na pasta modelos.</span><span class="sxs-lookup"><span data-stu-id="a6070-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="a6070-125">Adicione uma propriedade de navegação à classe `Product`:</span><span class="sxs-lookup"><span data-stu-id="a6070-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="a6070-126">Adicione um novo **DbSet** à classe `ProductsContext`, para que Entity Framework inclua a tabela Supplier no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a6070-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="a6070-127">No WebApiConfig.cs, adicione um &quot;fornecedores&quot; entidade definida ao modelo de dados de entidade:</span><span class="sxs-lookup"><span data-stu-id="a6070-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="a6070-128">Adicionar um controlador de fornecedores</span><span class="sxs-lookup"><span data-stu-id="a6070-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="a6070-129">Adicione uma classe de `SuppliersController` à pasta controladores.</span><span class="sxs-lookup"><span data-stu-id="a6070-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="a6070-130">Não mostrarei como adicionar operações CRUD para esse controlador.</span><span class="sxs-lookup"><span data-stu-id="a6070-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="a6070-131">As etapas são as mesmas para o controlador de produtos (consulte [criar um ponto de extremidade do OData v4](create-an-odata-v4-endpoint.md)).</span><span class="sxs-lookup"><span data-stu-id="a6070-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="a6070-132">Obtendo entidades relacionadas</span><span class="sxs-lookup"><span data-stu-id="a6070-132">Getting Related Entities</span></span>

<span data-ttu-id="a6070-133">Para obter o fornecedor de um produto, o cliente envia uma solicitação GET:</span><span class="sxs-lookup"><span data-stu-id="a6070-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="a6070-134">Para dar suporte a essa solicitação, adicione o seguinte método à classe `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="a6070-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="a6070-135">Esse método usa uma Convenção de nomenclatura padrão</span><span class="sxs-lookup"><span data-stu-id="a6070-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="a6070-136">Nome do método: GetX, em que X é a propriedade de navegação.</span><span class="sxs-lookup"><span data-stu-id="a6070-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="a6070-137">Nome do parâmetro: *chave*</span><span class="sxs-lookup"><span data-stu-id="a6070-137">Parameter name: *key*</span></span>

<span data-ttu-id="a6070-138">Se você seguir essa Convenção de nomenclatura, a API da Web mapeará automaticamente a solicitação HTTP para o método do controlador.</span><span class="sxs-lookup"><span data-stu-id="a6070-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="a6070-139">Exemplo de solicitação HTTP:</span><span class="sxs-lookup"><span data-stu-id="a6070-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="a6070-140">Resposta HTTP de exemplo:</span><span class="sxs-lookup"><span data-stu-id="a6070-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="a6070-141">Obtendo uma coleção relacionada</span><span class="sxs-lookup"><span data-stu-id="a6070-141">Getting a related collection</span></span>

<span data-ttu-id="a6070-142">No exemplo anterior, um produto tem um fornecedor.</span><span class="sxs-lookup"><span data-stu-id="a6070-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="a6070-143">Uma propriedade de navegação também pode retornar uma coleção.</span><span class="sxs-lookup"><span data-stu-id="a6070-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="a6070-144">O código a seguir obtém os produtos para um fornecedor:</span><span class="sxs-lookup"><span data-stu-id="a6070-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="a6070-145">Nesse caso, o método retorna um **IQueryable** em vez de um **SingleResult&lt;t&gt;**</span><span class="sxs-lookup"><span data-stu-id="a6070-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="a6070-146">Exemplo de solicitação HTTP:</span><span class="sxs-lookup"><span data-stu-id="a6070-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="a6070-147">Resposta HTTP de exemplo:</span><span class="sxs-lookup"><span data-stu-id="a6070-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="a6070-148">Criando uma relação entre entidades</span><span class="sxs-lookup"><span data-stu-id="a6070-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="a6070-149">O OData dá suporte à criação ou remoção de relações entre duas entidades existentes.</span><span class="sxs-lookup"><span data-stu-id="a6070-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="a6070-150">Na terminologia do OData v4, a relação é uma&quot;de referência de &quot;.</span><span class="sxs-lookup"><span data-stu-id="a6070-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="a6070-151">(No OData v3, a relação foi chamada de *link*.</span><span class="sxs-lookup"><span data-stu-id="a6070-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="a6070-152">As diferenças de protocolo não são importantes para este tutorial.)</span><span class="sxs-lookup"><span data-stu-id="a6070-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="a6070-153">Uma referência tem seu próprio URI, com o formulário `/Entity/NavigationProperty/$ref`.</span><span class="sxs-lookup"><span data-stu-id="a6070-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="a6070-154">Por exemplo, aqui está o URI para endereçar a referência entre um produto e seu fornecedor:</span><span class="sxs-lookup"><span data-stu-id="a6070-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="a6070-155">Para adicionar uma relação, o cliente envia uma solicitação POST ou PUT para esse endereço.</span><span class="sxs-lookup"><span data-stu-id="a6070-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="a6070-156">PUT se a propriedade de navegação for uma única entidade, como `Product.Supplier`.</span><span class="sxs-lookup"><span data-stu-id="a6070-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="a6070-157">POST se a propriedade de navegação for uma coleção, como `Supplier.Products`.</span><span class="sxs-lookup"><span data-stu-id="a6070-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="a6070-158">O corpo da solicitação contém o URI da outra entidade na relação.</span><span class="sxs-lookup"><span data-stu-id="a6070-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="a6070-159">Aqui está um exemplo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="a6070-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="a6070-160">Neste exemplo, o cliente envia uma solicitação PUT para `/Products(6)/Supplier/$ref`, que é o URI de $ref para o `Supplier` do produto com ID = 6.</span><span class="sxs-lookup"><span data-stu-id="a6070-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="a6070-161">Se a solicitação for realizada com sucesso, o servidor enviará uma resposta 204 (sem conteúdo):</span><span class="sxs-lookup"><span data-stu-id="a6070-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="a6070-162">Aqui está o método de controlador para adicionar uma relação a um `Product`:</span><span class="sxs-lookup"><span data-stu-id="a6070-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="a6070-163">O parâmetro *NavigationProperty* especifica a relação a ser definida.</span><span class="sxs-lookup"><span data-stu-id="a6070-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="a6070-164">(Se houver mais de uma propriedade de navegação na entidade, você poderá adicionar mais instruções `case`.)</span><span class="sxs-lookup"><span data-stu-id="a6070-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="a6070-165">O parâmetro de *link* contém o URI do fornecedor.</span><span class="sxs-lookup"><span data-stu-id="a6070-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="a6070-166">A API da Web analisa automaticamente o corpo da solicitação para obter o valor desse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a6070-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="a6070-167">Para pesquisar o fornecedor, precisamos da ID (ou da chave), que faz parte do parâmetro de *link* .</span><span class="sxs-lookup"><span data-stu-id="a6070-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="a6070-168">Para fazer isso, use o seguinte método auxiliar:</span><span class="sxs-lookup"><span data-stu-id="a6070-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="a6070-169">Basicamente, esse método usa a biblioteca OData para dividir o caminho do URI em segmentos, localizar o segmento que contém a chave e converter a chave no tipo correto.</span><span class="sxs-lookup"><span data-stu-id="a6070-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="a6070-170">Excluindo uma relação entre entidades</span><span class="sxs-lookup"><span data-stu-id="a6070-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="a6070-171">Para excluir uma relação, o cliente envia uma solicitação HTTP DELETE para o URI de $ref:</span><span class="sxs-lookup"><span data-stu-id="a6070-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="a6070-172">Aqui está o método de controlador para excluir a relação entre um produto e um fornecedor:</span><span class="sxs-lookup"><span data-stu-id="a6070-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="a6070-173">Nesse caso, `Product.Supplier` é a &quot;1&quot; fim de uma relação de um para muitos, para que você possa remover a relação apenas definindo `Product.Supplier` para `null`.</span><span class="sxs-lookup"><span data-stu-id="a6070-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="a6070-174">Na &quot;muitos&quot; fim de uma relação, o cliente deve especificar qual entidade relacionada será removida.</span><span class="sxs-lookup"><span data-stu-id="a6070-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="a6070-175">Para fazer isso, o cliente envia o URI da entidade relacionada na cadeia de caracteres de consulta da solicitação.</span><span class="sxs-lookup"><span data-stu-id="a6070-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="a6070-176">Por exemplo, para remover "produto 1" do "fornecedor 1":</span><span class="sxs-lookup"><span data-stu-id="a6070-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="a6070-177">Para dar suporte a isso na API Web, precisamos incluir um parâmetro extra no método `DeleteRef`.</span><span class="sxs-lookup"><span data-stu-id="a6070-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="a6070-178">Aqui está o método de controlador para remover um produto da relação de `Supplier.Products`.</span><span class="sxs-lookup"><span data-stu-id="a6070-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="a6070-179">O parâmetro de *chave* é a chave para o fornecedor e o parâmetro *relatedKey* é a chave do produto a ser removido da relação de `Products`.</span><span class="sxs-lookup"><span data-stu-id="a6070-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="a6070-180">Observe que a API da Web obtém automaticamente a chave da cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="a6070-180">Note that Web API automatically gets the key from the query string.</span></span>
