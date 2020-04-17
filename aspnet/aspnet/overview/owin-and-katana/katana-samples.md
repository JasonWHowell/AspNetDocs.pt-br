---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana Amostras | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540435"
---
# <a name="katana-samples"></a><span data-ttu-id="a5c8a-102">Exemplos do Katana</span><span class="sxs-lookup"><span data-stu-id="a5c8a-102">Katana Samples</span></span>

<span data-ttu-id="a5c8a-103">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a5c8a-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="a5c8a-104">Exemplos do Katana</span><span class="sxs-lookup"><span data-stu-id="a5c8a-104">Katana Samples</span></span>

<span data-ttu-id="a5c8a-105">**ASP.NET rotas código** | fonte[de amostra](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="a5c8a-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="a5c8a-106">Em alguns aplicativos, você vai querer conectar componentes OWIN na tabela de rota Asp.Net lado a lado com componentes não OWIN.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="a5c8a-107">Esta amostra mostra como usar os métodos de extensão RouteCollection MapOwinPath e MapOwinRoute fornecidos pelo Microsoft.Owin.Host.SystemWeb.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="a5c8a-108">**Código** | [fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines) da amostra de ramificações de pipelines</span><span class="sxs-lookup"><span data-stu-id="a5c8a-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="a5c8a-109">Os pipelines de processamento de solicitação OWIN não precisam ser lineares, eles podem ser ramificados para processar solicitações de diferentes maneiras.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="a5c8a-110">Esta amostra mostra como construir um pipeline de ramificação com base em caminhos de solicitação ou outros dados de solicitação, como cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="a5c8a-111">Esses componentes estão disponíveis no pacote nuget microsoft.Owin.Mapping.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="a5c8a-112">**Custom Server Sample** | [Código-fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) de amostra de servidor personalizado </span><span class="sxs-lookup"><span data-stu-id="a5c8a-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="a5c8a-113">Mostra como usar um servidor OWIN personalizado ao hospedar o OWIN por auto-hospedagem.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="a5c8a-114">**Embedded Sample** | [Código-fonte de](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded) amostra incorporado</span><span class="sxs-lookup"><span data-stu-id="a5c8a-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="a5c8a-115">Alguns servidores OWIN podem ser executados&quot;dentro do&quot;seu próprio processo (auto-hospedado).</span><span class="sxs-lookup"><span data-stu-id="a5c8a-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="a5c8a-116">Esta amostra mostra como iniciar um aplicativo OWIN usando as ferramentas fornecidas pelo pacote nuget microsoft.Owin.Hosting.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="a5c8a-117">**HelloWorld Sample** | [Código fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld) da amostra helloworld</span><span class="sxs-lookup"><span data-stu-id="a5c8a-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="a5c8a-118">OWIN é uma abstração de API de servidor HTTP que permite a portabilidade do aplicativo em vários servidores.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="a5c8a-119">Esta amostra demonstra como escrever um aplicativo Hello World usando **alguns invólucros simples** em torno da abstração OWIN crua e executá-lo em um servidor web como ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="a5c8a-120">**Olá Mundo Código** | [Fonte da](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin) amostra Raw OWIN</span><span class="sxs-lookup"><span data-stu-id="a5c8a-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="a5c8a-121">Esta amostra demonstra como escrever um aplicativo Hello World usando a abstração **OWIN crua** e executá-la em um servidor web como Asp.Net.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="a5c8a-122">**SignalR Sample** | [Código fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR) da amostra do sinalizador</span><span class="sxs-lookup"><span data-stu-id="a5c8a-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="a5c8a-123">Mostra como auto-hospedar signalR usando OWIN / Katana.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="a5c8a-124">Para obter mais informações sobre o SignalR auto-hospedagem, consulte [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="a5c8a-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="a5c8a-125">**Código** | fonte da amostra de arquivos estáticos[Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="a5c8a-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="a5c8a-126">Mostra como suportar solicitações HTTP para arquivos estáticos usando OWIN / Katana.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="a5c8a-127">**Web API** | [Código-fonte da](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) API da Web </span><span class="sxs-lookup"><span data-stu-id="a5c8a-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="a5c8a-128">Esta amostra mostra como hospedar OWIN no IIS e adicionar API web ao pipeline OWIN.</span><span class="sxs-lookup"><span data-stu-id="a5c8a-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="a5c8a-129">**Web Socket Sample** | [Código-fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) da amostra do soquete web </span><span class="sxs-lookup"><span data-stu-id="a5c8a-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="a5c8a-130">Mostra como suportar soquetes da Web no OWIN usando a classe [System.Net.WebSockets.WebSockets.WebSocket.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="a5c8a-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
