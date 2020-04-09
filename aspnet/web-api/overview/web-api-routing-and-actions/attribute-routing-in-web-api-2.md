---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Roteamento de atributos na API 2 da Web ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675379"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="811f0-102">Roteamento de atributos na API 2 da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="811f0-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="811f0-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="811f0-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="811f0-104">*Roteamento* é como a API da Web corresponde a um URI a uma ação.</span><span class="sxs-lookup"><span data-stu-id="811f0-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="811f0-105">A API 2 da Web suporta um novo tipo de roteamento, chamado *roteamento de atributos*.</span><span class="sxs-lookup"><span data-stu-id="811f0-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="811f0-106">Como o nome indica, o roteamento de atributos usa atributos para definir rotas.</span><span class="sxs-lookup"><span data-stu-id="811f0-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="811f0-107">O roteamento de atributos oferece mais controle sobre as URIs em sua API web.</span><span class="sxs-lookup"><span data-stu-id="811f0-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="811f0-108">Por exemplo, você pode facilmente criar URIs que descrevem hierarquias de recursos.</span><span class="sxs-lookup"><span data-stu-id="811f0-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="811f0-109">O estilo anterior de roteamento, chamado de roteamento baseado em convenções, ainda é totalmente suportado.</span><span class="sxs-lookup"><span data-stu-id="811f0-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="811f0-110">Na verdade, você pode combinar ambas as técnicas no mesmo projeto.</span><span class="sxs-lookup"><span data-stu-id="811f0-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="811f0-111">Este tópico mostra como ativar o roteamento de atributos e descreve as várias opções para roteamento de atributos.</span><span class="sxs-lookup"><span data-stu-id="811f0-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="811f0-112">Para obter um tutorial de ponta a ponta que usa roteamento de atributos, consulte [Criar uma API REST com roteamento de atributos na API 2](create-a-rest-api-with-attribute-routing.md)da Web .</span><span class="sxs-lookup"><span data-stu-id="811f0-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="811f0-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="811f0-113">Prerequisites</span></span>

<span data-ttu-id="811f0-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Edição Comunitária, Profissional ou Empresarial</span><span class="sxs-lookup"><span data-stu-id="811f0-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="811f0-115">Alternativamente, use o NuGet Package Manager para instalar os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="811f0-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="811f0-116">No menu **Ferramentas** no Visual Studio, selecione **NuGet Package Manager**e selecione Console do **Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="811f0-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="811f0-117">Digite o seguinte comando na janela Console do Gerenciador de pacotes:</span><span class="sxs-lookup"><span data-stu-id="811f0-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="811f0-118">Por que roteamento de atributos?</span><span class="sxs-lookup"><span data-stu-id="811f0-118">Why Attribute Routing?</span></span>

<span data-ttu-id="811f0-119">O primeiro lançamento da API web usou roteamento *baseado em convenções.*</span><span class="sxs-lookup"><span data-stu-id="811f0-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="811f0-120">Nesse tipo de roteamento, você define um ou mais modelos de rota, que são basicamente strings parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="811f0-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="811f0-121">Quando o framework recebe uma solicitação, ela corresponde ao URI com o modelo de rota.</span><span class="sxs-lookup"><span data-stu-id="811f0-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="811f0-122">Para obter mais informações sobre o roteamento baseado em convenções, consulte [Roteamento em ASP.NET API da Web](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="811f0-122">For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="811f0-123">Uma vantagem do roteamento baseado em convenções é que os modelos são definidos em um único lugar, e as regras de roteamento são aplicadas consistentemente em todos os controladores.</span><span class="sxs-lookup"><span data-stu-id="811f0-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="811f0-124">Infelizmente, o roteamento baseado em convenções torna difícil suportar certos padrões uri que são comuns em APIs RESTful.</span><span class="sxs-lookup"><span data-stu-id="811f0-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="811f0-125">Por exemplo, os recursos geralmente contêm recursos infantis: os clientes têm pedidos, filmes têm atores, livros têm autores e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="811f0-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="811f0-126">É natural criar URIs que reflitam essas relações:</span><span class="sxs-lookup"><span data-stu-id="811f0-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="811f0-127">Esse tipo de URI é difícil de criar usando roteamento baseado em convenções.</span><span class="sxs-lookup"><span data-stu-id="811f0-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="811f0-128">Embora possa ser feito, os resultados não são bem dimensionados se você tiver muitos controladores ou tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="811f0-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="811f0-129">Com roteamento de atributos, é trivial definir uma rota para este URI.</span><span class="sxs-lookup"><span data-stu-id="811f0-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="811f0-130">Basta adicionar um atributo à ação do controlador:</span><span class="sxs-lookup"><span data-stu-id="811f0-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="811f0-131">Aqui estão alguns outros padrões que atribuem roteamento facilita.</span><span class="sxs-lookup"><span data-stu-id="811f0-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="811f0-132">**Controle de versão de API**</span><span class="sxs-lookup"><span data-stu-id="811f0-132">**API versioning**</span></span>

<span data-ttu-id="811f0-133">Neste exemplo, "/api/v1/products" seriam encaminhados para um controlador diferente de "/api/v2/produtos".</span><span class="sxs-lookup"><span data-stu-id="811f0-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="811f0-134">**Segmentos uri sobrecarregados**</span><span class="sxs-lookup"><span data-stu-id="811f0-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="811f0-135">Neste exemplo, "1" é um número de pedido, mas "pendente" mapas para uma coleção.</span><span class="sxs-lookup"><span data-stu-id="811f0-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="811f0-136">**Múltiplos tipos de parâmetros**</span><span class="sxs-lookup"><span data-stu-id="811f0-136">**Multiple parameter types**</span></span>

<span data-ttu-id="811f0-137">Neste exemplo, "1" é um número de pedido, mas "2013/06/16" especifica uma data.</span><span class="sxs-lookup"><span data-stu-id="811f0-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="811f0-138">Ativando o roteamento de atributos</span><span class="sxs-lookup"><span data-stu-id="811f0-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="811f0-139">Para habilitar o roteamento de atributos, chame **MapHttpAttributeRoutes** durante a configuração.</span><span class="sxs-lookup"><span data-stu-id="811f0-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="811f0-140">Este método de extensão é definido na classe **System.Web.HttpConfigurationExtensions.**</span><span class="sxs-lookup"><span data-stu-id="811f0-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="811f0-141">O roteamento de atributos pode ser combinado com o roteamento [baseado em convenções.](routing-in-aspnet-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="811f0-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="811f0-142">Para definir rotas baseadas em convenções, chame o método **MapHttpRoute.**</span><span class="sxs-lookup"><span data-stu-id="811f0-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="811f0-143">Para obter mais informações sobre a configuração da API da Web, consulte [Configuração ASP.NET API 2](../advanced/configuring-aspnet-web-api.md)da Web .</span><span class="sxs-lookup"><span data-stu-id="811f0-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="811f0-144">Nota: Migrando da API web 1</span><span class="sxs-lookup"><span data-stu-id="811f0-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="811f0-145">Antes da API 2 da Web, os modelos de projeto da API da Web geraram código assim:</span><span class="sxs-lookup"><span data-stu-id="811f0-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="811f0-146">Se o roteamento de atributos estiver ativado, este código lançará uma exceção.</span><span class="sxs-lookup"><span data-stu-id="811f0-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="811f0-147">Se você atualizar um projeto de API da Web existente para usar roteamento de atributos, certifique-se de atualizar esse código de configuração para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="811f0-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="811f0-148">Para obter mais informações, consulte [Configurando a API da Web com ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span><span class="sxs-lookup"><span data-stu-id="811f0-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="811f0-149">Adicionando atributos de rota</span><span class="sxs-lookup"><span data-stu-id="811f0-149">Adding Route Attributes</span></span>

<span data-ttu-id="811f0-150">Aqui está um exemplo de uma rota definida usando um atributo:</span><span class="sxs-lookup"><span data-stu-id="811f0-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="811f0-151">Os &quot;clientes de string/{customerId}/orders&quot; é o modelo URI para a rota.</span><span class="sxs-lookup"><span data-stu-id="811f0-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="811f0-152">A API da Web tenta combinar o URI de solicitação com o modelo.</span><span class="sxs-lookup"><span data-stu-id="811f0-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="811f0-153">Neste exemplo, "clientes" e "pedidos" são segmentos literais, e "{customerId}" é um parâmetro variável.</span><span class="sxs-lookup"><span data-stu-id="811f0-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="811f0-154">As seguintes URIs corresponderiam a este modelo:</span><span class="sxs-lookup"><span data-stu-id="811f0-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="811f0-155">Você pode restringir a correspondência usando [restrições, descritas](#constraints)mais tarde neste tópico.</span><span class="sxs-lookup"><span data-stu-id="811f0-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="811f0-156">Observe que &quot;o parâmetro&quot; {customerId} no modelo de rota corresponde ao nome do parâmetro *id* do cliente no método.</span><span class="sxs-lookup"><span data-stu-id="811f0-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="811f0-157">Quando a API da Web invoca a ação do controlador, ela tenta vincular os parâmetros de rota.</span><span class="sxs-lookup"><span data-stu-id="811f0-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="811f0-158">Por exemplo, se `http://example.com/customers/1/orders`o URI estiver, a API da Web tentará vincular o valor "1" ao parâmetro *id do cliente* na ação.</span><span class="sxs-lookup"><span data-stu-id="811f0-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="811f0-159">Um modelo URI pode ter vários parâmetros:</span><span class="sxs-lookup"><span data-stu-id="811f0-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="811f0-160">Quaisquer métodos de controlador que não tenham um atributo de rota usam roteamento baseado em convenção.</span><span class="sxs-lookup"><span data-stu-id="811f0-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="811f0-161">Dessa forma, você pode combinar ambos os tipos de roteamento no mesmo projeto.</span><span class="sxs-lookup"><span data-stu-id="811f0-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="811f0-162">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="811f0-162">HTTP Methods</span></span>

<span data-ttu-id="811f0-163">A API da Web também seleciona ações com base no método HTTP da solicitação (GET, POST, etc).</span><span class="sxs-lookup"><span data-stu-id="811f0-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="811f0-164">Por padrão, a API da Web procura uma correspondência insensível a casos com o início do nome do método do controlador.</span><span class="sxs-lookup"><span data-stu-id="811f0-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="811f0-165">Por exemplo, um `PutCustomers` método de controlador chamado corresponde a uma solicitação HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="811f0-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="811f0-166">Você pode substituir esta convenção decorando o método com os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="811f0-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="811f0-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="811f0-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="811f0-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="811f0-168">**[HttpGet]**</span></span>
- <span data-ttu-id="811f0-169">**[Httphead]**</span><span class="sxs-lookup"><span data-stu-id="811f0-169">**[HttpHead]**</span></span>
- <span data-ttu-id="811f0-170">**[Opções http]**</span><span class="sxs-lookup"><span data-stu-id="811f0-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="811f0-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="811f0-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="811f0-172">**[HttpPost]**</span><span class="sxs-lookup"><span data-stu-id="811f0-172">**[HttpPost]**</span></span>
- <span data-ttu-id="811f0-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="811f0-173">**[HttpPut]**</span></span>

<span data-ttu-id="811f0-174">O exemplo a seguir mapeia o método CreateBook para solicitações HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="811f0-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="811f0-175">Para todos os outros métodos HTTP, incluindo métodos não padronizados, use o atributo **AcceptVerbs,** que leva uma lista de métodos HTTP.</span><span class="sxs-lookup"><span data-stu-id="811f0-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="811f0-176">Prefixos de rota</span><span class="sxs-lookup"><span data-stu-id="811f0-176">Route Prefixes</span></span>

<span data-ttu-id="811f0-177">Muitas vezes, as rotas em um controlador começam com o mesmo prefixo.</span><span class="sxs-lookup"><span data-stu-id="811f0-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="811f0-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="811f0-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="811f0-179">Você pode definir um prefixo comum para um controlador inteiro usando o atributo **[RoutePrefix]:**</span><span class="sxs-lookup"><span data-stu-id="811f0-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="811f0-180">Use um tilde (~) no atributo do método para substituir o prefixo de rota:</span><span class="sxs-lookup"><span data-stu-id="811f0-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="811f0-181">O prefixo de rota pode incluir parâmetros:</span><span class="sxs-lookup"><span data-stu-id="811f0-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="811f0-182">Restrições de rota</span><span class="sxs-lookup"><span data-stu-id="811f0-182">Route Constraints</span></span>

<span data-ttu-id="811f0-183">As restrições de rota permitem restringir a forma como os parâmetros no modelo de rota são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="811f0-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="811f0-184">A sintaxe &quot;geral é {parâmetro:restrição}&quot;.</span><span class="sxs-lookup"><span data-stu-id="811f0-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="811f0-185">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="811f0-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="811f0-186">Aqui, a primeira rota só &quot;será&quot; selecionada se o segmento de id do URI for um inteiro.</span><span class="sxs-lookup"><span data-stu-id="811f0-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="811f0-187">Caso contrário, a segunda rota será escolhida.</span><span class="sxs-lookup"><span data-stu-id="811f0-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="811f0-188">A tabela a seguir lista as restrições suportadas.</span><span class="sxs-lookup"><span data-stu-id="811f0-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="811f0-189">Constraint</span><span class="sxs-lookup"><span data-stu-id="811f0-189">Constraint</span></span> | <span data-ttu-id="811f0-190">Descrição</span><span class="sxs-lookup"><span data-stu-id="811f0-190">Description</span></span> | <span data-ttu-id="811f0-191">Exemplo</span><span class="sxs-lookup"><span data-stu-id="811f0-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="811f0-192">alpha</span><span class="sxs-lookup"><span data-stu-id="811f0-192">alpha</span></span> | <span data-ttu-id="811f0-193">Corresponde aos caracteres do alfabeto latino maiúsculo ou minúsculo (a-z, A-Z)</span><span class="sxs-lookup"><span data-stu-id="811f0-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="811f0-194">{x:alfa}</span><span class="sxs-lookup"><span data-stu-id="811f0-194">{x:alpha}</span></span> |
| <span data-ttu-id="811f0-195">bool</span><span class="sxs-lookup"><span data-stu-id="811f0-195">bool</span></span> | <span data-ttu-id="811f0-196">Combina com um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="811f0-196">Matches a Boolean value.</span></span> | <span data-ttu-id="811f0-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="811f0-197">{x:bool}</span></span> |
| <span data-ttu-id="811f0-198">DATETIME</span><span class="sxs-lookup"><span data-stu-id="811f0-198">datetime</span></span> | <span data-ttu-id="811f0-199">Corresponde a um valor **de Hora de Data.**</span><span class="sxs-lookup"><span data-stu-id="811f0-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="811f0-200">{x:hora de data}</span><span class="sxs-lookup"><span data-stu-id="811f0-200">{x:datetime}</span></span> |
| <span data-ttu-id="811f0-201">decimal</span><span class="sxs-lookup"><span data-stu-id="811f0-201">decimal</span></span> | <span data-ttu-id="811f0-202">Corresponde a um valor decimal.</span><span class="sxs-lookup"><span data-stu-id="811f0-202">Matches a decimal value.</span></span> | <span data-ttu-id="811f0-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="811f0-203">{x:decimal}</span></span> |
| <span data-ttu-id="811f0-204">double</span><span class="sxs-lookup"><span data-stu-id="811f0-204">double</span></span> | <span data-ttu-id="811f0-205">Corresponde a um valor de 64 bits de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="811f0-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="811f0-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="811f0-206">{x:double}</span></span> |
| <span data-ttu-id="811f0-207">FLOAT</span><span class="sxs-lookup"><span data-stu-id="811f0-207">float</span></span> | <span data-ttu-id="811f0-208">Corresponde a um valor de ponto flutuante de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="811f0-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="811f0-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="811f0-209">{x:float}</span></span> |
| <span data-ttu-id="811f0-210">guid</span><span class="sxs-lookup"><span data-stu-id="811f0-210">guid</span></span> | <span data-ttu-id="811f0-211">Corresponde a um valor GUID.</span><span class="sxs-lookup"><span data-stu-id="811f0-211">Matches a GUID value.</span></span> | <span data-ttu-id="811f0-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="811f0-212">{x:guid}</span></span> |
| <span data-ttu-id="811f0-213">INT</span><span class="sxs-lookup"><span data-stu-id="811f0-213">int</span></span> | <span data-ttu-id="811f0-214">Corresponde a um valor inteiro de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="811f0-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="811f0-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="811f0-215">{x:int}</span></span> |
| <span data-ttu-id="811f0-216">comprimento</span><span class="sxs-lookup"><span data-stu-id="811f0-216">length</span></span> | <span data-ttu-id="811f0-217">Corresponde a uma seqüência com o comprimento especificado ou dentro de um intervalo especificado de comprimentos.</span><span class="sxs-lookup"><span data-stu-id="811f0-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="811f0-218">{x:comprimento(6)} {x:comprimento(1,20)}</span><span class="sxs-lookup"><span data-stu-id="811f0-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="811f0-219">long</span><span class="sxs-lookup"><span data-stu-id="811f0-219">long</span></span> | <span data-ttu-id="811f0-220">Corresponde a um valor inteiro de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="811f0-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="811f0-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="811f0-221">{x:long}</span></span> |
| <span data-ttu-id="811f0-222">max</span><span class="sxs-lookup"><span data-stu-id="811f0-222">max</span></span> | <span data-ttu-id="811f0-223">Corresponde a um inteiro com um valor máximo.</span><span class="sxs-lookup"><span data-stu-id="811f0-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="811f0-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="811f0-224">{x:max(10)}</span></span> |
| <span data-ttu-id="811f0-225">Maxlength</span><span class="sxs-lookup"><span data-stu-id="811f0-225">maxlength</span></span> | <span data-ttu-id="811f0-226">Combina uma corda com um comprimento máximo.</span><span class="sxs-lookup"><span data-stu-id="811f0-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="811f0-227">{x:comprimento máximo(10)}</span><span class="sxs-lookup"><span data-stu-id="811f0-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="811f0-228">Min</span><span class="sxs-lookup"><span data-stu-id="811f0-228">min</span></span> | <span data-ttu-id="811f0-229">Corresponde a um inteiro com um valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="811f0-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="811f0-230">{x:min(10)}</span><span class="sxs-lookup"><span data-stu-id="811f0-230">{x:min(10)}</span></span> |
| <span data-ttu-id="811f0-231">Minlength</span><span class="sxs-lookup"><span data-stu-id="811f0-231">minlength</span></span> | <span data-ttu-id="811f0-232">Combina uma corda com um comprimento mínimo.</span><span class="sxs-lookup"><span data-stu-id="811f0-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="811f0-233">{x:minlength(10)}</span><span class="sxs-lookup"><span data-stu-id="811f0-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="811f0-234">range</span><span class="sxs-lookup"><span data-stu-id="811f0-234">range</span></span> | <span data-ttu-id="811f0-235">Corresponde a um inteiro dentro de uma faixa de valores.</span><span class="sxs-lookup"><span data-stu-id="811f0-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="811f0-236">{x:intervalo(10,50)}</span><span class="sxs-lookup"><span data-stu-id="811f0-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="811f0-237">regex</span><span class="sxs-lookup"><span data-stu-id="811f0-237">regex</span></span> | <span data-ttu-id="811f0-238">Corresponde a uma expressão regular.</span><span class="sxs-lookup"><span data-stu-id="811f0-238">Matches a regular expression.</span></span> | <span data-ttu-id="811f0-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="811f0-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="811f0-240">Observe que algumas das restrições, &quot;&quot;como min, tomam argumentos entre parênteses.</span><span class="sxs-lookup"><span data-stu-id="811f0-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="811f0-241">Você pode aplicar múltiplas restrições a um parâmetro, separado por um cólon.</span><span class="sxs-lookup"><span data-stu-id="811f0-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="811f0-242">Restrições de rota personalizadas</span><span class="sxs-lookup"><span data-stu-id="811f0-242">Custom Route Constraints</span></span>

<span data-ttu-id="811f0-243">Você pode criar restrições de rota personalizadas implementando a interface **IHttpRouteConstraint.**</span><span class="sxs-lookup"><span data-stu-id="811f0-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="811f0-244">Por exemplo, a seguinte restrição restringe um parâmetro a um valor inteiro não zero.</span><span class="sxs-lookup"><span data-stu-id="811f0-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="811f0-245">O código a seguir mostra como registrar a restrição:</span><span class="sxs-lookup"><span data-stu-id="811f0-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="811f0-246">Agora você pode aplicar a restrição em suas rotas:</span><span class="sxs-lookup"><span data-stu-id="811f0-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="811f0-247">Você também pode substituir toda a classe **DefaultInlineConstraintResolver** implementando a interface **IInlineResolverResolver.**</span><span class="sxs-lookup"><span data-stu-id="811f0-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="811f0-248">Isso substituirá todas as restrições incorporadas, a menos que sua implementação do **IInlineConstraintResolver** as adicione especificamente.</span><span class="sxs-lookup"><span data-stu-id="811f0-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="811f0-249">Parâmetros e valores padrão opcionais do URI</span><span class="sxs-lookup"><span data-stu-id="811f0-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="811f0-250">Você pode tornar um parâmetro URI opcional adicionando um ponto de interrogação ao parâmetro de rota.</span><span class="sxs-lookup"><span data-stu-id="811f0-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="811f0-251">Se um parâmetro de rota for opcional, você deve definir um valor padrão para o parâmetro do método.</span><span class="sxs-lookup"><span data-stu-id="811f0-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="811f0-252">Neste exemplo, `/api/books/locale/1033` `/api/books/locale` e retorne o mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="811f0-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="811f0-253">Alternativamente, você pode especificar um valor padrão dentro do modelo de rota, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="811f0-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="811f0-254">Isso é quase o mesmo que o exemplo anterior, mas há uma pequena diferença de comportamento quando o valor padrão é aplicado.</span><span class="sxs-lookup"><span data-stu-id="811f0-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="811f0-255">No primeiro exemplo ("{lcid:int?}"), o valor padrão de 1033 é atribuído diretamente ao parâmetro do método, de modo que o parâmetro terá esse valor exato.</span><span class="sxs-lookup"><span data-stu-id="811f0-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="811f0-256">No segundo exemplo ("{lcid:int=1033}"), o valor padrão de "1033" passa pelo processo de vinculação do modelo.</span><span class="sxs-lookup"><span data-stu-id="811f0-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="811f0-257">O aglutinante modelo padrão converterá "1033" para o valor numérico 1033.</span><span class="sxs-lookup"><span data-stu-id="811f0-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="811f0-258">No entanto, você pode conectar um fichário de modelo personalizado, que pode fazer algo diferente.</span><span class="sxs-lookup"><span data-stu-id="811f0-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="811f0-259">(Na maioria dos casos, a menos que você tenha aglutinantes de modelo personalizados em seu pipeline, as duas formas serão equivalentes.)</span><span class="sxs-lookup"><span data-stu-id="811f0-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="811f0-260">Nomes de rotas</span><span class="sxs-lookup"><span data-stu-id="811f0-260">Route Names</span></span>

<span data-ttu-id="811f0-261">Na Web API, cada rota tem um nome.</span><span class="sxs-lookup"><span data-stu-id="811f0-261">In Web API, every route has a name.</span></span> <span data-ttu-id="811f0-262">Os nomes de rota são úteis para gerar links, para que você possa incluir um link em uma resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="811f0-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="811f0-263">Para especificar o nome da rota, defina a propriedade **Nome** no atributo.</span><span class="sxs-lookup"><span data-stu-id="811f0-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="811f0-264">O exemplo a seguir mostra como definir o nome da rota e também como usar o nome da rota ao gerar um link.</span><span class="sxs-lookup"><span data-stu-id="811f0-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="811f0-265">Ordem de Rota</span><span class="sxs-lookup"><span data-stu-id="811f0-265">Route Order</span></span>

<span data-ttu-id="811f0-266">Quando a estrutura tenta combinar um URI com uma rota, ele avalia as rotas em uma ordem específica.</span><span class="sxs-lookup"><span data-stu-id="811f0-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="811f0-267">Para especificar a ordem, defina a propriedade **Order** no atributo route.</span><span class="sxs-lookup"><span data-stu-id="811f0-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="811f0-268">Valores mais baixos são avaliados primeiro.</span><span class="sxs-lookup"><span data-stu-id="811f0-268">Lower values are evaluated first.</span></span> <span data-ttu-id="811f0-269">O valor padrão do pedido é zero.</span><span class="sxs-lookup"><span data-stu-id="811f0-269">The default order value is zero.</span></span>

<span data-ttu-id="811f0-270">Veja como o pedido total é determinado:</span><span class="sxs-lookup"><span data-stu-id="811f0-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="811f0-271">Compare a propriedade **Order** do atributo route.</span><span class="sxs-lookup"><span data-stu-id="811f0-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="811f0-272">Veja cada segmento URI no modelo de rota.</span><span class="sxs-lookup"><span data-stu-id="811f0-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="811f0-273">Para cada segmento, a ordem é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="811f0-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="811f0-274">Segmentos literais.</span><span class="sxs-lookup"><span data-stu-id="811f0-274">Literal segments.</span></span>
    2. <span data-ttu-id="811f0-275">Parâmetros de rota com restrições.</span><span class="sxs-lookup"><span data-stu-id="811f0-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="811f0-276">Parâmetros de rota sem restrições.</span><span class="sxs-lookup"><span data-stu-id="811f0-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="811f0-277">Segmentos de parâmetros curinga com restrições.</span><span class="sxs-lookup"><span data-stu-id="811f0-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="811f0-278">Segmentos de parâmetros curinga sem restrições.</span><span class="sxs-lookup"><span data-stu-id="811f0-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="811f0-279">No caso de um empate, as rotas são ordenadas por uma comparação de stringordinal insensível[(OrdinalIgnoreCase)](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)do modelo de rota.</span><span class="sxs-lookup"><span data-stu-id="811f0-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="811f0-280">Veja um exemplo.</span><span class="sxs-lookup"><span data-stu-id="811f0-280">Here is an example.</span></span> <span data-ttu-id="811f0-281">Suponha que você defina o seguinte controlador:</span><span class="sxs-lookup"><span data-stu-id="811f0-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="811f0-282">Essas rotas são ordenadas da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="811f0-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="811f0-283">ordens/detalhes</span><span class="sxs-lookup"><span data-stu-id="811f0-283">orders/details</span></span>
2. <span data-ttu-id="811f0-284">ordens/{id}</span><span class="sxs-lookup"><span data-stu-id="811f0-284">orders/{id}</span></span>
3. <span data-ttu-id="811f0-285">pedidos/{nome do cliente}</span><span class="sxs-lookup"><span data-stu-id="811f0-285">orders/{customerName}</span></span>
4. <span data-ttu-id="811f0-286">ordens/{\*data}</span><span class="sxs-lookup"><span data-stu-id="811f0-286">orders/{\*date}</span></span>
5. <span data-ttu-id="811f0-287">ordens/pendências</span><span class="sxs-lookup"><span data-stu-id="811f0-287">orders/pending</span></span>

<span data-ttu-id="811f0-288">Observe que "detalhes" é um segmento literal e aparece antes de "{id}", mas "pendente" aparece por último porque a propriedade **Order** é 1.</span><span class="sxs-lookup"><span data-stu-id="811f0-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="811f0-289">(Este exemplo pressupõe que não há clientes chamados "detalhes" ou "pendentes".</span><span class="sxs-lookup"><span data-stu-id="811f0-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="811f0-290">Em geral, tente evitar rotas ambíguas.</span><span class="sxs-lookup"><span data-stu-id="811f0-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="811f0-291">Neste exemplo, um modelo `GetByCustomer` de rota melhor para é "customers/{customerName}" )</span><span class="sxs-lookup"><span data-stu-id="811f0-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
