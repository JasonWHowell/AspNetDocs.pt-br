---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Entendendo o processo de execução ASP.NET de MVC | Microsoft Docs
author: rick-anderson
description: Saiba como o framework ASP.NET MVC processa uma solicitação de navegador passo a passo.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541020"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="5865c-103">Noções básicas sobre o processo de execução do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="5865c-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="5865c-104">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5865c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5865c-105">Saiba como o framework ASP.NET MVC processa uma solicitação de navegador passo a passo.</span><span class="sxs-lookup"><span data-stu-id="5865c-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="5865c-106">As solicitações para um aplicativo web baseado em MVC ASP.NET passam primeiro pelo objeto **UrlRoutingModule,** que é um módulo HTTP.</span><span class="sxs-lookup"><span data-stu-id="5865c-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="5865c-107">Este módulo analisa a solicitação e executa a seleção de rotas.</span><span class="sxs-lookup"><span data-stu-id="5865c-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="5865c-108">O objeto **UrlRoutingModule** seleciona o primeiro objeto de rota que corresponde à solicitação atual.</span><span class="sxs-lookup"><span data-stu-id="5865c-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="5865c-109">(Um objeto de rota é uma classe que implementa **routeBase**e é tipicamente uma instância da classe **Route.)** Se nenhuma rota corresponder, o objeto **UrlRoutingModule** não faz nada e permite que a solicitação volte ao processamento regular de solicitações de solicitação de ASP.NET ou IIS.</span><span class="sxs-lookup"><span data-stu-id="5865c-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="5865c-110">A partir do objeto **Route** selecionado, o objeto **UrlRoutingModule** obtém o objeto **IRouteHandler** associado ao objeto **Route.**</span><span class="sxs-lookup"><span data-stu-id="5865c-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="5865c-111">Normalmente, em um aplicativo MVC, esta será uma instância do **MvcRouteHandler**.</span><span class="sxs-lookup"><span data-stu-id="5865c-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="5865c-112">A instância **IRouteHandler** cria um objeto **IHttpHandler** e passa-o pelo objeto **IHttpContext.**</span><span class="sxs-lookup"><span data-stu-id="5865c-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="5865c-113">Por padrão, a instância **IHttpHandler** para MVC é o objeto **MvcHandler.**</span><span class="sxs-lookup"><span data-stu-id="5865c-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="5865c-114">Em seguida, o objeto **MvcHandler** seleciona o controlador que irá lidar com a solicitação.</span><span class="sxs-lookup"><span data-stu-id="5865c-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="5865c-115">Quando um aplicativo Web ASP.NET MVC é executado no IIS 7.0, nenhuma extensão de nome de arquivo é necessária para projetos De MVC.</span><span class="sxs-lookup"><span data-stu-id="5865c-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="5865c-116">No entanto, no IIS 6.0, o manipulador requer que você mapeie a extensão do nome do arquivo .mvc para o ASP.NET ISAPI DLL.</span><span class="sxs-lookup"><span data-stu-id="5865c-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="5865c-117">O módulo e o manipulador são os pontos de entrada para a estrutura mVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5865c-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="5865c-118">Eles realizam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="5865c-118">They perform the following actions:</span></span>

- <span data-ttu-id="5865c-119">Selecione o controlador apropriado em um aplicativo Web MVC.</span><span class="sxs-lookup"><span data-stu-id="5865c-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="5865c-120">Obtenha uma instância específica do controlador.</span><span class="sxs-lookup"><span data-stu-id="5865c-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="5865c-121">Ligue para o método **Execute** do controlador.</span><span class="sxs-lookup"><span data-stu-id="5865c-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="5865c-122">As seguintes listas das etapas de execução de um projeto Web MVC:</span><span class="sxs-lookup"><span data-stu-id="5865c-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="5865c-123">Receba a primeira solicitação para a aplicação</span><span class="sxs-lookup"><span data-stu-id="5865c-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="5865c-124">No arquivo Global.asax, os objetos **Route** são adicionados ao objeto **RouteTable.**</span><span class="sxs-lookup"><span data-stu-id="5865c-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="5865c-125">Executar roteamento</span><span class="sxs-lookup"><span data-stu-id="5865c-125">Perform routing</span></span> 

    - <span data-ttu-id="5865c-126">O módulo **UrlRoutingModule** usa o primeiro objeto **Route** correspondente na coleção **RouteTable** para criar o objeto **RouteData,** que ele usa para criar um objeto **RequestContext** (**IHttpContext).**</span><span class="sxs-lookup"><span data-stu-id="5865c-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="5865c-127">Criar manipulador de solicitações MVC</span><span class="sxs-lookup"><span data-stu-id="5865c-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="5865c-128">O objeto **MvcRouteHandler** cria uma instância da classe **MvcHandler** e passa-a a instância **RequestContext.**</span><span class="sxs-lookup"><span data-stu-id="5865c-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="5865c-129">Criar controlador</span><span class="sxs-lookup"><span data-stu-id="5865c-129">Create controller</span></span> 

    - <span data-ttu-id="5865c-130">O objeto **MvcHandler** usa a instância **RequestContext** para identificar o objeto **IControllerFactory** (tipicamente uma instância da classe **DefaultControllerFactory)** para criar a instância do controlador com.</span><span class="sxs-lookup"><span data-stu-id="5865c-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="5865c-131">Executar controlador - A instância **MvcHandler** chama o método **executar** do controlador.</span><span class="sxs-lookup"><span data-stu-id="5865c-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="5865c-132">Invocar ação</span><span class="sxs-lookup"><span data-stu-id="5865c-132">Invoke action</span></span> 

    - <span data-ttu-id="5865c-133">A maioria dos controladores herda da classe base **do controlador.**</span><span class="sxs-lookup"><span data-stu-id="5865c-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="5865c-134">Para os controladores que o fazem, o objeto **ControllerActionInvoker** associado ao controlador determina qual método de ação da classe controladora chamar e, em seguida, chama esse método.</span><span class="sxs-lookup"><span data-stu-id="5865c-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="5865c-135">Resultado de execução</span><span class="sxs-lookup"><span data-stu-id="5865c-135">Execute result</span></span> 

    - <span data-ttu-id="5865c-136">Um método de ação típico pode receber a entrada do usuário, preparar os dados de resposta apropriados e, em seguida, executar o resultado retornando um tipo de resultado.</span><span class="sxs-lookup"><span data-stu-id="5865c-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="5865c-137">Os tipos de resultados incorporados que podem ser executados incluem os seguintes: **ViewResult** (que renderiza uma exibição e é o tipo de resultado mais usado), **RedirectToRouteResult,** **RedirectResult,** **ContentResult,** **JsonResult**e **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="5865c-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
