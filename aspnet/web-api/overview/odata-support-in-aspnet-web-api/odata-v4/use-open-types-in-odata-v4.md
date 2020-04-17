---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Tipos abertos em OData v4 com ASP.NET API web | Microsoft Docs
author: rick-anderson
description: No OData v4, um tipo aberto é um tipo estruturado que contém propriedades dinâmicas, além de quaisquer propriedades que são declaradas na definição do tipo. Abrir...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543724"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="27aca-104">Abrir tipos em OData v4 com ASP.NET API web</span><span class="sxs-lookup"><span data-stu-id="27aca-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="27aca-105">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="27aca-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="27aca-106">No OData v4, um *tipo aberto* é um tipo estruturado que contém propriedades dinâmicas, além de quaisquer propriedades que são declaradas na definição do tipo.</span><span class="sxs-lookup"><span data-stu-id="27aca-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="27aca-107">Os tipos abertos permitem adicionar flexibilidade aos seus modelos de dados.</span><span class="sxs-lookup"><span data-stu-id="27aca-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="27aca-108">Este tutorial mostra como usar tipos abertos em ASP.NET OData da API da Web.</span><span class="sxs-lookup"><span data-stu-id="27aca-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="27aca-109">Este tutorial pressupõe que você já sabe como criar um ponto final de OData em ASP.NET API da Web.</span><span class="sxs-lookup"><span data-stu-id="27aca-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="27aca-110">Se não, comece lendo [Crie um OData v4 Endpoint](create-an-odata-v4-endpoint.md) primeiro.</span><span class="sxs-lookup"><span data-stu-id="27aca-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="27aca-111">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="27aca-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="27aca-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="27aca-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="27aca-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="27aca-113">OData v4</span></span>

<span data-ttu-id="27aca-114">Primeiro, algumas terminologias oData:</span><span class="sxs-lookup"><span data-stu-id="27aca-114">First, some OData terminology:</span></span>

- <span data-ttu-id="27aca-115">Tipo de entidade: Um tipo estruturado com uma chave.</span><span class="sxs-lookup"><span data-stu-id="27aca-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="27aca-116">Tipo complexo: Um tipo estruturado sem chave.</span><span class="sxs-lookup"><span data-stu-id="27aca-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="27aca-117">Tipo aberto: Um tipo com propriedades dinâmicas.</span><span class="sxs-lookup"><span data-stu-id="27aca-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="27aca-118">Tanto os tipos de entidades quanto os tipos complexos podem ser abertos.</span><span class="sxs-lookup"><span data-stu-id="27aca-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="27aca-119">O valor de uma propriedade dinâmica pode ser um tipo primitivo, tipo complexo ou tipo de enumeração; ou uma coleção de qualquer um desses tipos.</span><span class="sxs-lookup"><span data-stu-id="27aca-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="27aca-120">Para obter mais informações sobre tipos abertos, consulte a [especificação OData v4](http://www.odata.org/documentation/odata-version-4-0/).</span><span class="sxs-lookup"><span data-stu-id="27aca-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="27aca-121">Instale as Bibliotecas Web OData</span><span class="sxs-lookup"><span data-stu-id="27aca-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="27aca-122">Use o NuGet Package Manager para instalar as bibliotecas De Dados da API da Web mais recentes.</span><span class="sxs-lookup"><span data-stu-id="27aca-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="27aca-123">Da janela Console do Gerenciador de Pacotes:</span><span class="sxs-lookup"><span data-stu-id="27aca-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="27aca-124">Definir os tipos de CLR</span><span class="sxs-lookup"><span data-stu-id="27aca-124">Define the CLR Types</span></span>

<span data-ttu-id="27aca-125">Comece definindo os modelos EDM como tipos CLR.</span><span class="sxs-lookup"><span data-stu-id="27aca-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="27aca-126">Quando o Modelo de Dados de Entidade (EDM) é criado,</span><span class="sxs-lookup"><span data-stu-id="27aca-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="27aca-127">`Category`é um tipo de enumeração.</span><span class="sxs-lookup"><span data-stu-id="27aca-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="27aca-128">`Address`é um tipo complexo.</span><span class="sxs-lookup"><span data-stu-id="27aca-128">`Address` is a complex type.</span></span> <span data-ttu-id="27aca-129">(Ele não tem uma chave, por isso não é um tipo de entidade.)</span><span class="sxs-lookup"><span data-stu-id="27aca-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="27aca-130">`Customer`é um tipo de entidade.</span><span class="sxs-lookup"><span data-stu-id="27aca-130">`Customer` is an entity type.</span></span> <span data-ttu-id="27aca-131">(Tem uma chave.)</span><span class="sxs-lookup"><span data-stu-id="27aca-131">(It has a key.)</span></span>
- <span data-ttu-id="27aca-132">`Press`é um tipo complexo aberto.</span><span class="sxs-lookup"><span data-stu-id="27aca-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="27aca-133">`Book`é um tipo de entidade aberta.</span><span class="sxs-lookup"><span data-stu-id="27aca-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="27aca-134">Para criar um tipo aberto, o tipo CLR deve ter uma propriedade do tipo `IDictionary<string, object>`, que detém as propriedades dinâmicas.</span><span class="sxs-lookup"><span data-stu-id="27aca-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="27aca-135">Construa o modelo EDM</span><span class="sxs-lookup"><span data-stu-id="27aca-135">Build the EDM Model</span></span>

<span data-ttu-id="27aca-136">Se você usar **o ODataConventionModelBuilder** `Press` para `Book` criar o EDM, e for automaticamente `IDictionary<string, object>` adicionado como tipos abertos, com base na presença de uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="27aca-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="27aca-137">Você também pode construir o EDM explicitamente, usando **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="27aca-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="27aca-138">Adicionar um controlador de dados odata</span><span class="sxs-lookup"><span data-stu-id="27aca-138">Add an OData Controller</span></span>

<span data-ttu-id="27aca-139">Em seguida, adicione um controlador OData.</span><span class="sxs-lookup"><span data-stu-id="27aca-139">Next, add an OData controller.</span></span> <span data-ttu-id="27aca-140">Para este tutorial, usaremos um controlador simplificado que apenas suporta solicitações GET e POST, e usa uma lista na memória para armazenar entidades.</span><span class="sxs-lookup"><span data-stu-id="27aca-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="27aca-141">Observe que `Book` a primeira instância não tem propriedades dinâmicas.</span><span class="sxs-lookup"><span data-stu-id="27aca-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="27aca-142">A `Book` segunda instância tem as seguintes propriedades dinâmicas:</span><span class="sxs-lookup"><span data-stu-id="27aca-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="27aca-143">"Publicado": Tipo primitivo</span><span class="sxs-lookup"><span data-stu-id="27aca-143">"Published": Primitive type</span></span>
- <span data-ttu-id="27aca-144">"Autores": Coleção de tipos primitivos</span><span class="sxs-lookup"><span data-stu-id="27aca-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="27aca-145">"Outras Categorias": Coleção de tipos de enumeração.</span><span class="sxs-lookup"><span data-stu-id="27aca-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="27aca-146">Além disso, `Press` a `Book` propriedade dessa instância tem as seguintes propriedades dinâmicas:</span><span class="sxs-lookup"><span data-stu-id="27aca-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="27aca-147">"Blog": Tipo primitivo</span><span class="sxs-lookup"><span data-stu-id="27aca-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="27aca-148">"Endereço": Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="27aca-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="27aca-149">Consultar os Metadados</span><span class="sxs-lookup"><span data-stu-id="27aca-149">Query the Metadata</span></span>

<span data-ttu-id="27aca-150">Para obter o documento de metadados oData, envie uma solicitação GET para `~/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="27aca-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="27aca-151">O corpo de resposta deve ser semelhante a isso:</span><span class="sxs-lookup"><span data-stu-id="27aca-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="27aca-152">A partir do documento de metadados, você pode ver que:</span><span class="sxs-lookup"><span data-stu-id="27aca-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="27aca-153">Para `Book` os `Press` e tipos, `OpenType` o valor do atributo é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="27aca-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="27aca-154">Os `Customer` `Address` tipos não têm esse atributo.</span><span class="sxs-lookup"><span data-stu-id="27aca-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="27aca-155">O `Book` tipo de entidade tem três propriedades declaradas: ISBN, Title e Press.</span><span class="sxs-lookup"><span data-stu-id="27aca-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="27aca-156">Os metadados OData não `Book.Properties` incluem a propriedade da classe CLR.</span><span class="sxs-lookup"><span data-stu-id="27aca-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="27aca-157">Da mesma `Press` forma, o tipo complexo tem apenas duas propriedades declaradas: Nome e Categoria.</span><span class="sxs-lookup"><span data-stu-id="27aca-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="27aca-158">Os metadados não `Press.DynamicProperties` incluem a propriedade da classe CLR.</span><span class="sxs-lookup"><span data-stu-id="27aca-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="27aca-159">Consultar uma Entidade</span><span class="sxs-lookup"><span data-stu-id="27aca-159">Query an Entity</span></span>

<span data-ttu-id="27aca-160">Para obter o livro com isbn igual a "978-0-7356-7942-9", envie uma solicitação GET para `~/Books('978-0-7356-7942-9')`.</span><span class="sxs-lookup"><span data-stu-id="27aca-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="27aca-161">O corpo de resposta deve ser semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="27aca-161">The response body should look similar to the following.</span></span> <span data-ttu-id="27aca-162">(Recuado para torná-lo mais legível.)</span><span class="sxs-lookup"><span data-stu-id="27aca-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="27aca-163">Observe que as propriedades dinâmicas estão incluídas em linha com as propriedades declaradas.</span><span class="sxs-lookup"><span data-stu-id="27aca-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="27aca-164">POSTAR uma Entidade</span><span class="sxs-lookup"><span data-stu-id="27aca-164">POST an Entity</span></span>

<span data-ttu-id="27aca-165">Para adicionar uma entidade do Livro, envie uma solicitação POST para `~/Books`.</span><span class="sxs-lookup"><span data-stu-id="27aca-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="27aca-166">O cliente pode definir propriedades dinâmicas na carga útil da solicitação.</span><span class="sxs-lookup"><span data-stu-id="27aca-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="27aca-167">Aqui está um pedido de exemplo.</span><span class="sxs-lookup"><span data-stu-id="27aca-167">Here is an example request.</span></span> <span data-ttu-id="27aca-168">Observe as propriedades "Preço" e "Publicado".</span><span class="sxs-lookup"><span data-stu-id="27aca-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="27aca-169">Se você definir um ponto de ruptura no método controlador, poderá `Properties` ver que a API da Web adicionou essas propriedades ao dicionário.</span><span class="sxs-lookup"><span data-stu-id="27aca-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="27aca-170">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="27aca-170">Additional Resources</span></span>

[<span data-ttu-id="27aca-171">Amostra de tipo aberto de odata</span><span class="sxs-lookup"><span data-stu-id="27aca-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
