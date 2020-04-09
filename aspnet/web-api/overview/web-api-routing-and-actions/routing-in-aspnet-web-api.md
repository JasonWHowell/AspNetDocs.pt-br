---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Roteamento em ASP.NET API web | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676128"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="625fa-102">Roteamento no ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="625fa-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="625fa-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="625fa-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="625fa-104">Este artigo descreve como ASP.NET API da Web encaminha solicitações HTTP aos controladores.</span><span class="sxs-lookup"><span data-stu-id="625fa-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="625fa-105">Se você está familiarizado com ASP.NET MVC, o roteamento da API da Web é muito semelhante ao roteamento mvc.</span><span class="sxs-lookup"><span data-stu-id="625fa-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="625fa-106">A principal diferença é que a API da Web usa o verbo HTTP, não o caminho URI, para selecionar a ação.</span><span class="sxs-lookup"><span data-stu-id="625fa-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="625fa-107">Você também pode usar roteamento no estilo MVC na API da Web.</span><span class="sxs-lookup"><span data-stu-id="625fa-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="625fa-108">Este artigo não assume qualquer conhecimento de ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="625fa-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="625fa-109">Tabelas de roteamento</span><span class="sxs-lookup"><span data-stu-id="625fa-109">Routing Tables</span></span>

<span data-ttu-id="625fa-110">Em ASP.NET API da Web, um *controlador* é uma classe que lida com solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="625fa-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="625fa-111">Os métodos públicos do controlador são chamados *métodos* de ação ou simplesmente *ações.*</span><span class="sxs-lookup"><span data-stu-id="625fa-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="625fa-112">Quando a estrutura da API da Web recebe uma solicitação, ela encaminha a solicitação para uma ação.</span><span class="sxs-lookup"><span data-stu-id="625fa-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="625fa-113">Para determinar qual ação invocar, a estrutura usa uma *tabela de roteamento*.</span><span class="sxs-lookup"><span data-stu-id="625fa-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="625fa-114">O modelo de projeto do Visual Studio para API web cria uma rota padrão:</span><span class="sxs-lookup"><span data-stu-id="625fa-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="625fa-115">Essa rota é definida no *arquivo WebApiConfig.cs,* que é colocado no diretório *\_App Start:*</span><span class="sxs-lookup"><span data-stu-id="625fa-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="625fa-116">Para obter mais `WebApiConfig` informações sobre a classe, consulte [Configuração ASP.NET API da Web](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="625fa-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="625fa-117">Se você auto-hospedar a API da Web, você `HttpSelfHostConfiguration` deve definir a tabela de roteamento diretamente no objeto.</span><span class="sxs-lookup"><span data-stu-id="625fa-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="625fa-118">Para obter mais informações, consulte [Auto-host de uma API da Web](../older-versions/self-host-a-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="625fa-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="625fa-119">Cada entrada na tabela de roteamento contém um *modelo de rota*.</span><span class="sxs-lookup"><span data-stu-id="625fa-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="625fa-120">O modelo de rota padrão &quot;para API da Web é&quot;api/{controller}/{id} .</span><span class="sxs-lookup"><span data-stu-id="625fa-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="625fa-121">Neste modelo, &quot;a&quot; api é um segmento de caminho literal, e {controller} e {id} são variáveis de espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="625fa-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="625fa-122">Quando a estrutura da API da Web recebe uma solicitação HTTP, ela tenta igualar o URI com um dos modelos de rota na tabela de roteamento.</span><span class="sxs-lookup"><span data-stu-id="625fa-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="625fa-123">Se nenhuma rota corresponder, o cliente recebe um erro de 404.</span><span class="sxs-lookup"><span data-stu-id="625fa-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="625fa-124">Por exemplo, as SEGUINTES URIs correspondem à rota padrão:</span><span class="sxs-lookup"><span data-stu-id="625fa-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="625fa-125">/api/contatos</span><span class="sxs-lookup"><span data-stu-id="625fa-125">/api/contacts</span></span>
- <span data-ttu-id="625fa-126">/api/contatos/1</span><span class="sxs-lookup"><span data-stu-id="625fa-126">/api/contacts/1</span></span>
- <span data-ttu-id="625fa-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="625fa-127">/api/products/gizmo1</span></span>

<span data-ttu-id="625fa-128">No entanto, o SEGUINTE URI não &quot;corresponde,&quot; pois não possui o segmento de API:</span><span class="sxs-lookup"><span data-stu-id="625fa-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="625fa-129">/contatos/1</span><span class="sxs-lookup"><span data-stu-id="625fa-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="625fa-130">A razão para o uso de "api" na rota é evitar colisões com ASP.NET roteamento MVC.</span><span class="sxs-lookup"><span data-stu-id="625fa-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="625fa-131">Dessa forma, você &quot;pode&quot; ter /contatos ir &quot;para um controlador&quot; MVC, e /api/contatos ir para um controlador de API da Web.</span><span class="sxs-lookup"><span data-stu-id="625fa-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="625fa-132">Claro, se você não gosta desta convenção, você pode alterar a tabela de rotas padrão.</span><span class="sxs-lookup"><span data-stu-id="625fa-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="625fa-133">Uma vez que uma rota correspondente é encontrada, a API da Web seleciona o controlador e a ação:</span><span class="sxs-lookup"><span data-stu-id="625fa-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="625fa-134">Para encontrar o controlador, &quot;a&quot; API da Web adiciona o Controller ao valor da variável *{controller}.*</span><span class="sxs-lookup"><span data-stu-id="625fa-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="625fa-135">Para encontrar a ação, a API da Web olha para o verbo HTTP e, em seguida, procura uma ação cujo nome começa com esse nome http verbo.</span><span class="sxs-lookup"><span data-stu-id="625fa-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="625fa-136">Por exemplo, com uma solicitação GET, a API &quot;&quot;da Web &quot;procura&quot; &quot;uma ação&quot;prefixada com Get , como GetContact ou GetAllContacts .</span><span class="sxs-lookup"><span data-stu-id="625fa-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="625fa-137">Esta convenção se aplica apenas aos verbos GET, POST, PUT, DELETE, HEAD, OPTIONS e PATCH.</span><span class="sxs-lookup"><span data-stu-id="625fa-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="625fa-138">Você pode habilitar outros verbos HTTP usando atributos em seu controlador.</span><span class="sxs-lookup"><span data-stu-id="625fa-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="625fa-139">Veremos um exemplo disso mais tarde.</span><span class="sxs-lookup"><span data-stu-id="625fa-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="625fa-140">Outras variáveis de espaço reservado no modelo de rota, como *{id},* são mapeadas para parâmetros de ação.</span><span class="sxs-lookup"><span data-stu-id="625fa-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="625fa-141">Vamos examinar um exemplo.</span><span class="sxs-lookup"><span data-stu-id="625fa-141">Let's look at an example.</span></span> <span data-ttu-id="625fa-142">Suponha que você defina o seguinte controlador:</span><span class="sxs-lookup"><span data-stu-id="625fa-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="625fa-143">Aqui estão algumas possíveis solicitações HTTP, juntamente com a ação que é invocada para cada um:</span><span class="sxs-lookup"><span data-stu-id="625fa-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="625fa-144">Verbo HTTP</span><span class="sxs-lookup"><span data-stu-id="625fa-144">HTTP Verb</span></span> | <span data-ttu-id="625fa-145">Caminho URI</span><span class="sxs-lookup"><span data-stu-id="625fa-145">URI Path</span></span> | <span data-ttu-id="625fa-146">Ação</span><span class="sxs-lookup"><span data-stu-id="625fa-146">Action</span></span> | <span data-ttu-id="625fa-147">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="625fa-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="625fa-148">GET</span><span class="sxs-lookup"><span data-stu-id="625fa-148">GET</span></span> | <span data-ttu-id="625fa-149">api/produtos</span><span class="sxs-lookup"><span data-stu-id="625fa-149">api/products</span></span> | <span data-ttu-id="625fa-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="625fa-150">GetAllProducts</span></span> | <span data-ttu-id="625fa-151">*(nenhum)*</span><span class="sxs-lookup"><span data-stu-id="625fa-151">*(none)*</span></span> |
| <span data-ttu-id="625fa-152">GET</span><span class="sxs-lookup"><span data-stu-id="625fa-152">GET</span></span> | <span data-ttu-id="625fa-153">api/produtos/4</span><span class="sxs-lookup"><span data-stu-id="625fa-153">api/products/4</span></span> | <span data-ttu-id="625fa-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="625fa-154">GetProductById</span></span> | <span data-ttu-id="625fa-155">4</span><span class="sxs-lookup"><span data-stu-id="625fa-155">4</span></span> |
| <span data-ttu-id="625fa-156">Delete (excluir)</span><span class="sxs-lookup"><span data-stu-id="625fa-156">DELETE</span></span> | <span data-ttu-id="625fa-157">api/produtos/4</span><span class="sxs-lookup"><span data-stu-id="625fa-157">api/products/4</span></span> | <span data-ttu-id="625fa-158">Excluirproduto</span><span class="sxs-lookup"><span data-stu-id="625fa-158">DeleteProduct</span></span> | <span data-ttu-id="625fa-159">4</span><span class="sxs-lookup"><span data-stu-id="625fa-159">4</span></span> |
| <span data-ttu-id="625fa-160">POST</span><span class="sxs-lookup"><span data-stu-id="625fa-160">POST</span></span> | <span data-ttu-id="625fa-161">api/produtos</span><span class="sxs-lookup"><span data-stu-id="625fa-161">api/products</span></span> | <span data-ttu-id="625fa-162">*(sem correspondência)*</span><span class="sxs-lookup"><span data-stu-id="625fa-162">*(no match)*</span></span> |  |

<span data-ttu-id="625fa-163">Observe que o segmento *{id}* do URI, se presente, é mapeado para o parâmetro *id* da ação.</span><span class="sxs-lookup"><span data-stu-id="625fa-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="625fa-164">Neste exemplo, o controlador define dois métodos GET, um com um parâmetro *de id* e outro sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="625fa-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="625fa-165">Além disso, observe que a solicitação POST falhará, pois o controlador não define um &quot;Post... &quot; método.</span><span class="sxs-lookup"><span data-stu-id="625fa-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="625fa-166">Variações de roteamento</span><span class="sxs-lookup"><span data-stu-id="625fa-166">Routing Variations</span></span>

<span data-ttu-id="625fa-167">A seção anterior descreveu o mecanismo básico de roteamento para ASP.NET API da Web.</span><span class="sxs-lookup"><span data-stu-id="625fa-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="625fa-168">Esta seção descreve algumas variações.</span><span class="sxs-lookup"><span data-stu-id="625fa-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="625fa-169">Verbos HTTP</span><span class="sxs-lookup"><span data-stu-id="625fa-169">HTTP verbs</span></span>

<span data-ttu-id="625fa-170">Em vez de usar a convenção de nomeação para verbos HTTP, você pode especificar explicitamente o verbo HTTP para uma ação decorando o método de ação com um dos seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="625fa-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="625fa-171">No exemplo a `FindProduct` seguir, o método é mapeado para obter solicitações:</span><span class="sxs-lookup"><span data-stu-id="625fa-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="625fa-172">Para permitir vários verbos HTTP para uma ação, ou para permitir verbos HTTP que não sejam `[AcceptVerbs]` GET, PUT, POST, DELETE, HEAD, OPTIONS e PATCH, use o atributo, que leva uma lista de verbos HTTP.</span><span class="sxs-lookup"><span data-stu-id="625fa-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="625fa-173">Roteamento por Nome de Ação</span><span class="sxs-lookup"><span data-stu-id="625fa-173">Routing by Action Name</span></span>

<span data-ttu-id="625fa-174">Com o modelo de roteamento padrão, a API da Web usa o verbo HTTP para selecionar a ação.</span><span class="sxs-lookup"><span data-stu-id="625fa-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="625fa-175">No entanto, você também pode criar uma rota onde o nome de ação está incluído no URI:</span><span class="sxs-lookup"><span data-stu-id="625fa-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="625fa-176">Neste modelo de rota, o parâmetro *{action}* nomeia o método de ação no controlador.</span><span class="sxs-lookup"><span data-stu-id="625fa-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="625fa-177">Com este estilo de roteamento, use atributos para especificar os verbos HTTP permitidos.</span><span class="sxs-lookup"><span data-stu-id="625fa-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="625fa-178">Por exemplo, suponha que seu controlador tenha o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="625fa-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="625fa-179">Neste caso, uma solicitação GET para "api/products/details/1" seria mapeada para o `Details` método.</span><span class="sxs-lookup"><span data-stu-id="625fa-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="625fa-180">Este estilo de roteamento é semelhante ao ASP.NET MVC, e pode ser apropriado para uma API no estilo RPC.</span><span class="sxs-lookup"><span data-stu-id="625fa-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="625fa-181">Você pode substituir o nome `[ActionName]` de ação usando o atributo.</span><span class="sxs-lookup"><span data-stu-id="625fa-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="625fa-182">No exemplo a seguir, existem &quot;duas ações que mapeiam para api/products/miniatura/*id*. Um suporta GET e o outro suporta POST:</span><span class="sxs-lookup"><span data-stu-id="625fa-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="625fa-183">Não-Ações</span><span class="sxs-lookup"><span data-stu-id="625fa-183">Non-Actions</span></span>

<span data-ttu-id="625fa-184">Para evitar que um método seja invocado `[NonAction]` como ação, use o atributo.</span><span class="sxs-lookup"><span data-stu-id="625fa-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="625fa-185">Isso sinaliza para a estrutura que o método não é uma ação, mesmo que de outra forma corresponda às regras de roteamento.</span><span class="sxs-lookup"><span data-stu-id="625fa-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="625fa-186">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="625fa-186">Further Reading</span></span>

<span data-ttu-id="625fa-187">Este tópico forneceu uma visão de alto nível do roteamento.</span><span class="sxs-lookup"><span data-stu-id="625fa-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="625fa-188">Para obter mais detalhes, consulte [Roteamento e Seleção de Ação](routing-and-action-selection.md), que descreve exatamente como a estrutura corresponde a um URI a uma rota, seleciona um controlador e, em seguida, seleciona a ação para invocar.</span><span class="sxs-lookup"><span data-stu-id="625fa-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
