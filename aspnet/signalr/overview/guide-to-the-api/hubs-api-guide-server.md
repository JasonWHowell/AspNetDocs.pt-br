---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR Hubs API Guide - Server (C#) | Microsoft Docs
author: bradygaster
description: Este documento fornece uma introdução à programação do lado do servidor da aPI do ASP.NET SignalR Hubs para SignalR versão 2, com amostras de código demonstrando...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676184"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="e8951-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span><span class="sxs-lookup"><span data-stu-id="e8951-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="e8951-104">por [Patrick Fletcher](https://github.com/pfletcher), Tom [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e8951-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="e8951-105">Este documento fornece uma introdução à programação do lado do servidor da aPI ASP.NET SignalR Hubs para SignalR versão 2, com amostras de código demonstrando opções comuns.</span><span class="sxs-lookup"><span data-stu-id="e8951-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="e8951-106">A API SignalR Hubs permite que você faça chamadas de procedimento remoto (RPCs) de um servidor para clientes conectados e de clientes para o servidor.</span><span class="sxs-lookup"><span data-stu-id="e8951-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="e8951-107">No código do servidor, você define métodos que podem ser chamados pelos clientes e você chama métodos que são executados no cliente.</span><span class="sxs-lookup"><span data-stu-id="e8951-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="e8951-108">No código do cliente, você define métodos que podem ser chamados do servidor e você chama métodos que são executados no servidor.</span><span class="sxs-lookup"><span data-stu-id="e8951-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="e8951-109">O SignalR cuida de todo o encanamento cliente-servidor para você.</span><span class="sxs-lookup"><span data-stu-id="e8951-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="e8951-110">SignalR também oferece uma API de nível inferior chamada Conexões Persistentes.</span><span class="sxs-lookup"><span data-stu-id="e8951-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="e8951-111">Para obter uma introdução ao SignalR, hubs e persistent connections, consulte [Introdução ao SignalR 2](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="e8951-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="e8951-112">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="e8951-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="e8951-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e8951-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="e8951-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="e8951-114">.NET 4.5</span></span>
> - <span data-ttu-id="e8951-115">SignalR versão 2</span><span class="sxs-lookup"><span data-stu-id="e8951-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="e8951-116">Versões tópicos</span><span class="sxs-lookup"><span data-stu-id="e8951-116">Topic versions</span></span>
> 
> <span data-ttu-id="e8951-117">Para obter informações sobre versões anteriores do SignalR, consulte [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="e8951-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="e8951-118">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="e8951-118">Questions and comments</span></span>
> 
> <span data-ttu-id="e8951-119">Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="e8951-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="e8951-120">Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="e8951-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="e8951-121">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e8951-121">Overview</span></span>

<span data-ttu-id="e8951-122">Este documento contém as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="e8951-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="e8951-123">Como registrar middleware SignalR</span><span class="sxs-lookup"><span data-stu-id="e8951-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="e8951-124">A URL /signalr</span><span class="sxs-lookup"><span data-stu-id="e8951-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="e8951-125">Configuração de opções SignalR</span><span class="sxs-lookup"><span data-stu-id="e8951-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="e8951-126">Como criar e usar classes hub</span><span class="sxs-lookup"><span data-stu-id="e8951-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="e8951-127">Vida útil do objeto hub</span><span class="sxs-lookup"><span data-stu-id="e8951-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="e8951-128">Cartucho de camelo de nomes de Hub em clientes JavaScript</span><span class="sxs-lookup"><span data-stu-id="e8951-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="e8951-129">Vários hubs</span><span class="sxs-lookup"><span data-stu-id="e8951-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="e8951-130">Hubs fortemente digitados</span><span class="sxs-lookup"><span data-stu-id="e8951-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="e8951-131">Como definir métodos na classe Hub que os clientes podem chamar</span><span class="sxs-lookup"><span data-stu-id="e8951-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="e8951-132">Invólucro de camelo de nomes de métodos em clientes JavaScript</span><span class="sxs-lookup"><span data-stu-id="e8951-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="e8951-133">Quando executar assíncronamente</span><span class="sxs-lookup"><span data-stu-id="e8951-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="e8951-134">Definindo sobrecargas</span><span class="sxs-lookup"><span data-stu-id="e8951-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="e8951-135">Relatando o progresso das invocações do método hub</span><span class="sxs-lookup"><span data-stu-id="e8951-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="e8951-136">Como chamar os métodos do cliente da classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="e8951-137">Selecionando quais clientes receberão o RPC</span><span class="sxs-lookup"><span data-stu-id="e8951-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="e8951-138">Nenhuma validação de tempo de compilação para nomes de métodos</span><span class="sxs-lookup"><span data-stu-id="e8951-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="e8951-139">Correspondência de nome do método insensível a casos</span><span class="sxs-lookup"><span data-stu-id="e8951-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="e8951-140">Execução assíncrona</span><span class="sxs-lookup"><span data-stu-id="e8951-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="e8951-141">Como gerenciar a adesão ao grupo da classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="e8951-142">Execução assíncrona dos métodos Adicionar e Remover</span><span class="sxs-lookup"><span data-stu-id="e8951-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="e8951-143">Persistência de membros do grupo</span><span class="sxs-lookup"><span data-stu-id="e8951-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="e8951-144">Grupos de usuários únicos</span><span class="sxs-lookup"><span data-stu-id="e8951-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="e8951-145">Como lidar com eventos de conexão vitalícia na classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="e8951-146">Quando onConnected, OnDisconnected e OnReconnected são chamados</span><span class="sxs-lookup"><span data-stu-id="e8951-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="e8951-147">Estado de chamada não povoado</span><span class="sxs-lookup"><span data-stu-id="e8951-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="e8951-148">Como obter informações sobre o cliente a partir da propriedade Context</span><span class="sxs-lookup"><span data-stu-id="e8951-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="e8951-149">Como passar o estado entre clientes e a classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="e8951-150">Como lidar com erros na classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="e8951-151">Como chamar métodos de clientes e gerenciar grupos de fora da classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="e8951-152">Chamando métodos de cliente</span><span class="sxs-lookup"><span data-stu-id="e8951-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="e8951-153">Gestão de membros do grupo</span><span class="sxs-lookup"><span data-stu-id="e8951-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="e8951-154">Como habilitar o rastreamento</span><span class="sxs-lookup"><span data-stu-id="e8951-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="e8951-155">Como personalizar o pipeline do Hubs</span><span class="sxs-lookup"><span data-stu-id="e8951-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="e8951-156">Para obter a documentação sobre como programar os clientes, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="e8951-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="e8951-157">SignalR Hubs API Guide - JavaScript Client</span><span class="sxs-lookup"><span data-stu-id="e8951-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="e8951-158">SignalR Hubs API Guide - .NET Client</span><span class="sxs-lookup"><span data-stu-id="e8951-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="e8951-159">Os componentes do servidor para SignalR 2 estão disponíveis apenas no .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="e8951-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="e8951-160">Os servidores em execução .NET 4.0 devem usar SignalR v1.x.</span><span class="sxs-lookup"><span data-stu-id="e8951-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="e8951-161">Como registrar middleware SignalR</span><span class="sxs-lookup"><span data-stu-id="e8951-161">How to register SignalR middleware</span></span>

<span data-ttu-id="e8951-162">Para definir a rota que os clientes usarão para se conectar ao seu Hub, ligue para o `MapSignalR` método quando o aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="e8951-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="e8951-163">`MapSignalR`é um método `OwinExtensions` de [extensão](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) para a classe.</span><span class="sxs-lookup"><span data-stu-id="e8951-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="e8951-164">O exemplo a seguir mostra como definir a rota SignalR Hubs usando uma classe de inicialização OWIN.</span><span class="sxs-lookup"><span data-stu-id="e8951-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="e8951-165">Se você estiver adicionando a funcionalidade SignalR a um aplicativo MVC ASP.NET, certifique-se de que a rota SignalR seja adicionada antes das outras rotas.</span><span class="sxs-lookup"><span data-stu-id="e8951-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="e8951-166">Para obter mais informações, consulte [Tutorial: Getting Started with SignalR 2 e MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="e8951-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="e8951-167">A URL /signalr</span><span class="sxs-lookup"><span data-stu-id="e8951-167">The /signalr URL</span></span>

<span data-ttu-id="e8951-168">Por padrão, a URL de rota que os clientes usarão para se conectar ao seu Hub é "/signalr".</span><span class="sxs-lookup"><span data-stu-id="e8951-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="e8951-169">(Não confunda essa URL com a URL "/signalr/hubs", que é para o arquivo JavaScript gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e8951-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="e8951-170">Para obter mais informações sobre o proxy gerado, consulte [SignalR Hubs API Guide - JavaScript Client - O proxy gerado e o que ele faz por você](hubs-api-guide-javascript-client.md#genproxy).)</span><span class="sxs-lookup"><span data-stu-id="e8951-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="e8951-171">Pode haver circunstâncias extraordinárias que tornam esta URL base não utilizável para SignalR; por exemplo, você tem uma pasta em seu projeto chamada *signalr* e você não quer alterar o nome.</span><span class="sxs-lookup"><span data-stu-id="e8951-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="e8951-172">Nesse caso, você pode alterar a URL base, como mostrado nos exemplos a seguir (substitua "/signalr" no código de exemplo pela URL desejada).</span><span class="sxs-lookup"><span data-stu-id="e8951-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="e8951-173">**Código do servidor que especifica a URL**</span><span class="sxs-lookup"><span data-stu-id="e8951-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="e8951-174">**Código cliente JavaScript que especifica a URL (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="e8951-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="e8951-175">**Código cliente JavaScript que especifica a URL (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="e8951-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="e8951-176">**.NET código de cliente que especifica a URL**</span><span class="sxs-lookup"><span data-stu-id="e8951-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="e8951-177">Configuração de opções de signalr</span><span class="sxs-lookup"><span data-stu-id="e8951-177">Configuring SignalR Options</span></span>

<span data-ttu-id="e8951-178">As sobrecargas `MapSignalR` do método permitem que você especifique uma URL personalizada, um resolver dependência personalizado e as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="e8951-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="e8951-179">Habilite chamadas de domínio cruzado usando CORS ou JSONP de clientes do navegador.</span><span class="sxs-lookup"><span data-stu-id="e8951-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="e8951-180">Normalmente, se o navegador `http://contoso.com`carregar uma página de , a `http://contoso.com/signalr`conexão SignalR está no mesmo domínio, em .</span><span class="sxs-lookup"><span data-stu-id="e8951-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="e8951-181">Se a `http://contoso.com` página de `http://fabrikam.com/signalr`fazer uma conexão com , que é uma conexão de domínio cruzado.</span><span class="sxs-lookup"><span data-stu-id="e8951-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="e8951-182">Por razões de segurança, as conexões entre domínios são desativadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="e8951-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="e8951-183">Para obter mais informações, consulte [ASP.NET SignalR Hubs API Guide - JavaScript Client - Como estabelecer uma conexão entre domínios](hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="e8951-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="e8951-184">Habilite mensagens de erro detalhadas.</span><span class="sxs-lookup"><span data-stu-id="e8951-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="e8951-185">Quando ocorrem erros, o comportamento padrão do SignalR é enviar aos clientes uma mensagem de notificação sem detalhes sobre o que aconteceu.</span><span class="sxs-lookup"><span data-stu-id="e8951-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="e8951-186">O envio de informações detalhadas de erro aos clientes não é recomendado na produção, pois usuários mal-intencionados podem ser capazes de usar as informações em ataques contra seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8951-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="e8951-187">Para solução de problemas, você pode usar essa opção para ativar temporariamente mais relatórios informativos de erros.</span><span class="sxs-lookup"><span data-stu-id="e8951-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="e8951-188">Desativar arquivos proxy JavaScript gerados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e8951-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="e8951-189">Por padrão, um arquivo JavaScript com proxies para suas classes hub é gerado em resposta à URL "/signalr/hubs".</span><span class="sxs-lookup"><span data-stu-id="e8951-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="e8951-190">Se você não quiser usar os proxies JavaScript, ou se você quiser gerar este arquivo manualmente e consultar um arquivo físico em seus clientes, você pode usar essa opção para desativar a geração de proxy.</span><span class="sxs-lookup"><span data-stu-id="e8951-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="e8951-191">Para obter mais informações, consulte [SignalR Hubs API Guide - JavaScript Client - Como criar um arquivo físico para o proxy gerado signalR](hubs-api-guide-javascript-client.md#manualproxy).</span><span class="sxs-lookup"><span data-stu-id="e8951-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="e8951-192">O exemplo a seguir mostra como especificar a URL de `MapSignalR` conexão SignalR e essas opções em uma chamada para o método.</span><span class="sxs-lookup"><span data-stu-id="e8951-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="e8951-193">Para especificar uma URL personalizada, substitua "/signalr" no exemplo pela URL que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e8951-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="e8951-194">Como criar e usar classes hub</span><span class="sxs-lookup"><span data-stu-id="e8951-194">How to create and use Hub classes</span></span>

<span data-ttu-id="e8951-195">Para criar um Hub, crie uma classe derivada do [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="e8951-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="e8951-196">O exemplo a seguir mostra uma classe Hub simples para um aplicativo de bate-papo.</span><span class="sxs-lookup"><span data-stu-id="e8951-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="e8951-197">Neste exemplo, um cliente conectado `NewContosoChatMessage` pode chamar o método e, quando isso acontece, os dados recebidos são transmitidos para todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="e8951-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="e8951-198">Vida útil do objeto hub</span><span class="sxs-lookup"><span data-stu-id="e8951-198">Hub object lifetime</span></span>

<span data-ttu-id="e8951-199">Você não instancia a classe Hub ou chama seus métodos a partir de seu próprio código no servidor; tudo o que é feito para você pelo gasoduto SignalR Hubs.</span><span class="sxs-lookup"><span data-stu-id="e8951-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="e8951-200">O SignalR cria uma nova instância da sua classe Hub cada vez que precisa lidar com uma operação do Hub, como quando um cliente conecta, desconecta ou faz uma chamada de método para o servidor.</span><span class="sxs-lookup"><span data-stu-id="e8951-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="e8951-201">Como as instâncias da classe Hub são transitórias, você não pode usá-las para manter o estado de uma chamada de método para outra.</span><span class="sxs-lookup"><span data-stu-id="e8951-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="e8951-202">Cada vez que o servidor recebe uma chamada de método de um cliente, uma nova instância da classe Hub processa a mensagem.</span><span class="sxs-lookup"><span data-stu-id="e8951-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="e8951-203">Para manter o estado através de múltiplas conexões e chamadas de método, use algum outro método, como um `Hub`banco de dados, ou uma variável estática na classe Hub, ou uma classe diferente que não deriva de .</span><span class="sxs-lookup"><span data-stu-id="e8951-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="e8951-204">Se você persistir dados na memória, usando um método como uma variável estática na classe Hub, os dados serão perdidos quando o domínio do aplicativo for reciclado.</span><span class="sxs-lookup"><span data-stu-id="e8951-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="e8951-205">Se você quiser enviar mensagens para clientes a partir de seu próprio código que é executado fora da classe Hub, você não pode fazê-lo instanciando uma instância de classe Hub, mas você pode fazê-lo recebendo uma referência ao objeto de contexto SignalR para sua classe Hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="e8951-206">Para obter mais informações, consulte [Como chamar os métodos do cliente e gerenciar grupos de fora da classe Hub](#callfromoutsidehub) mais tarde neste tópico.</span><span class="sxs-lookup"><span data-stu-id="e8951-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="e8951-207">Cartucho de camelo de nomes de Hub em clientes JavaScript</span><span class="sxs-lookup"><span data-stu-id="e8951-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="e8951-208">Por padrão, os clientes JavaScript referem-se a Hubs usando uma versão com maiúsculas e camelos do nome da classe.</span><span class="sxs-lookup"><span data-stu-id="e8951-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="e8951-209">SignalR faz automaticamente essa alteração para que o código JavaScript possa estar em conformidade com as convenções JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e8951-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="e8951-210">O exemplo anterior seria `contosoChatHub` referido como em código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e8951-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="e8951-211">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="e8951-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="e8951-212">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="e8951-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="e8951-213">Se você quiser especificar um nome diferente `HubName` para os clientes usarem, adicione o atributo.</span><span class="sxs-lookup"><span data-stu-id="e8951-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="e8951-214">Quando você `HubName` usa um atributo, não há alteração de nome para caso de camelo em clientes JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e8951-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="e8951-215">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="e8951-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="e8951-216">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="e8951-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="e8951-217">Vários hubs</span><span class="sxs-lookup"><span data-stu-id="e8951-217">Multiple Hubs</span></span>

<span data-ttu-id="e8951-218">Você pode definir várias classes do Hub em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8951-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="e8951-219">Quando você faz isso, a conexão é compartilhada, mas os grupos são separados:</span><span class="sxs-lookup"><span data-stu-id="e8951-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="e8951-220">Todos os clientes usarão a mesma URL para estabelecer uma conexão SignalR com seu serviço ("/signalr" ou sua URL personalizada se você especificou uma), e essa conexão é usada para todos os Hubs definidos pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="e8951-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="e8951-221">Não há diferença de desempenho para vários Hubs em comparação com a definição de todas as funcionalidades do Hub em uma única classe.</span><span class="sxs-lookup"><span data-stu-id="e8951-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="e8951-222">Todos os Hubs obtêm as mesmas informações de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="e8951-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="e8951-223">Uma vez que todos os Hubs compartilham a mesma conexão, a única informação de solicitação HTTP que o servidor recebe é o que vem na solicitação HTTP original que estabelece a conexão SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8951-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="e8951-224">Se você usar a solicitação de conexão para passar informações do cliente para o servidor especificando uma seqüência de consultas, você não poderá fornecer diferentes strings de consulta para diferentes Hubs.</span><span class="sxs-lookup"><span data-stu-id="e8951-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="e8951-225">Todos os Hubs receberão as mesmas informações.</span><span class="sxs-lookup"><span data-stu-id="e8951-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="e8951-226">O arquivo de proxies JavaScript gerado conterá proxies para todos os Hubs em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="e8951-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="e8951-227">Para obter informações sobre os proxies JavaScript, consulte [SignalR Hubs API Guide - JavaScript Client - O proxy gerado e o que ele faz por você](hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="e8951-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="e8951-228">Os grupos são definidos dentro dos Hubs.</span><span class="sxs-lookup"><span data-stu-id="e8951-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="e8951-229">No SignalR você pode definir grupos nomeados para transmitir para subconjuntos de clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="e8951-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="e8951-230">Os grupos são mantidos separadamente para cada Hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="e8951-231">Por exemplo, um grupo chamado "Administradores" incluiria `ContosoChatHub` um conjunto de clientes para sua classe, `StockTickerHub` e o mesmo nome de grupo se referiria a um conjunto diferente de clientes para sua classe.</span><span class="sxs-lookup"><span data-stu-id="e8951-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="e8951-232">Hubs fortemente digitados</span><span class="sxs-lookup"><span data-stu-id="e8951-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="e8951-233">Para definir uma interface para seus métodos de hub que seu cliente pode referenciar (e habilitar o Intellisense em seus métodos de `Hub<T>` hub), obtenha seu hub (introduzido no SignalR 2.1) em vez de `Hub`:</span><span class="sxs-lookup"><span data-stu-id="e8951-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="e8951-234">Como definir métodos na classe Hub que os clientes podem chamar</span><span class="sxs-lookup"><span data-stu-id="e8951-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="e8951-235">Para expor um método no Hub que você deseja ser callable do cliente, declare um método público, como mostrado nos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e8951-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="e8951-236">Você pode especificar um tipo de retorno e parâmetros, incluindo tipos e matrizes complexos, como faria em qualquer método C#.</span><span class="sxs-lookup"><span data-stu-id="e8951-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="e8951-237">Todos os dados que você recebe em parâmetros ou retornam ao chamador são comunicados entre o cliente e o servidor usando JSON, e o SignalR lida com a vinculação de objetos complexos e conjuntos de objetos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e8951-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="e8951-238">Invólucro de camelo de nomes de métodos em clientes JavaScript</span><span class="sxs-lookup"><span data-stu-id="e8951-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="e8951-239">Por padrão, os clientes JavaScript referem-se aos métodos do Hub usando uma versão com maiúsculas e camelos do nome do método.</span><span class="sxs-lookup"><span data-stu-id="e8951-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="e8951-240">SignalR faz automaticamente essa alteração para que o código JavaScript possa estar em conformidade com as convenções JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e8951-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="e8951-241">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="e8951-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="e8951-242">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="e8951-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="e8951-243">Se você quiser especificar um nome diferente `HubMethodName` para os clientes usarem, adicione o atributo.</span><span class="sxs-lookup"><span data-stu-id="e8951-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="e8951-244">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="e8951-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="e8951-245">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="e8951-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="e8951-246">Quando executar assíncronamente</span><span class="sxs-lookup"><span data-stu-id="e8951-246">When to execute asynchronously</span></span>

<span data-ttu-id="e8951-247">Se o método for de longa duração ou tiver que fazer um trabalho que envolva espera, como uma procuração de [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) banco de `void` dados ou uma chamada de serviço web, faça o método Hub assíncrono retornando um objeto Task (em lugar de retorno) ou [Task&lt;T&gt; ](https://msdn.microsoft.com/library/dd321424.aspx) (no lugar do tipo de `T` retorno).</span><span class="sxs-lookup"><span data-stu-id="e8951-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="e8951-248">Quando você `Task` retorna um objeto do método, `Task` o SignalR espera que o preenchimento seja concluído e, em seguida, ele envia o resultado desembrulhado de volta para o cliente, de modo que não há diferença em como você codifica o método de chamada no cliente.</span><span class="sxs-lookup"><span data-stu-id="e8951-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="e8951-249">Tornar um método Hub assíncrono evita bloquear a conexão quando ele usa o transporte WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e8951-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="e8951-250">Quando um método do Hub é executado de forma sincronizada e o transporte é WebSocket, as invocações subseqüentes de métodos no Hub do mesmo cliente são bloqueadas até que o método Hub seja concluído.</span><span class="sxs-lookup"><span data-stu-id="e8951-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="e8951-251">O exemplo a seguir mostra o mesmo método codificado para ser executado de forma sincronizada ou assíncrona, seguido pelo código cliente JavaScript que funciona para chamar qualquer versão.</span><span class="sxs-lookup"><span data-stu-id="e8951-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="e8951-252">**Síncrono**</span><span class="sxs-lookup"><span data-stu-id="e8951-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="e8951-253">**Assíncrono**</span><span class="sxs-lookup"><span data-stu-id="e8951-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="e8951-254">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="e8951-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="e8951-255">Para obter mais informações sobre como usar métodos assíncronos em ASP.NET 4.5, consulte [Usando Métodos Assíncronos em ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="e8951-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="e8951-256">Definindo sobrecargas</span><span class="sxs-lookup"><span data-stu-id="e8951-256">Defining Overloads</span></span>

<span data-ttu-id="e8951-257">Se você quiser definir sobrecargas para um método, o número de parâmetros em cada sobrecarga deve ser diferente.</span><span class="sxs-lookup"><span data-stu-id="e8951-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="e8951-258">Se você diferenciar uma sobrecarga apenas especificando diferentes tipos de parâmetros, sua classe Hub irá compilar, mas o serviço SignalR abrirá uma exceção no tempo de execução quando os clientes tentarem chamar uma das sobrecargas.</span><span class="sxs-lookup"><span data-stu-id="e8951-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="e8951-259">Relatando o progresso das invocações do método hub</span><span class="sxs-lookup"><span data-stu-id="e8951-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="e8951-260">O SignalR 2.1 adiciona suporte ao [padrão de relatórios de progresso](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduzido no .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="e8951-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="e8951-261">Para implementar relatórios `IProgress<T>` de progresso, defina um parâmetro para o método do hub que seu cliente pode acessar:</span><span class="sxs-lookup"><span data-stu-id="e8951-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="e8951-262">Ao escrever um método de servidor de longa duração, é importante usar um padrão de programação assíncrono como OSync/ Aguarde em vez de bloquear o segmento do hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="e8951-263">Como chamar os métodos do cliente da classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="e8951-264">Para chamar os métodos do `Clients` cliente do servidor, use a propriedade em um método em sua classe Hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="e8951-265">O exemplo a seguir `addNewMessageToPage` mostra o código do servidor que chama todos os clientes conectados e o código do cliente que define o método em um cliente JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e8951-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="e8951-266">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="e8951-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="e8951-267">Invocar um método de cliente é uma operação `Task`assíncrona e retorna um .</span><span class="sxs-lookup"><span data-stu-id="e8951-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="e8951-268">Use: `await`</span><span class="sxs-lookup"><span data-stu-id="e8951-268">Use `await`:</span></span>

* <span data-ttu-id="e8951-269">Para garantir que a mensagem seja enviada sem erro.</span><span class="sxs-lookup"><span data-stu-id="e8951-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="e8951-270">Para habilitar erros de captura e manuseio em um bloco de captura de tentativa.</span><span class="sxs-lookup"><span data-stu-id="e8951-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="e8951-271">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="e8951-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="e8951-272">Você não pode obter um valor de retorno de um método de cliente; sintaxe `int x = Clients.All.add(1,1)` como não funciona.</span><span class="sxs-lookup"><span data-stu-id="e8951-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="e8951-273">Você pode especificar tipos e matrizes complexos para os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e8951-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="e8951-274">O exemplo a seguir passa um tipo complexo para o cliente em um parâmetro de método.</span><span class="sxs-lookup"><span data-stu-id="e8951-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="e8951-275">**Código do servidor que chama um método cliente usando um objeto complexo**</span><span class="sxs-lookup"><span data-stu-id="e8951-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="e8951-276">**Código do servidor que define o objeto complexo**</span><span class="sxs-lookup"><span data-stu-id="e8951-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="e8951-277">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="e8951-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="e8951-278">Selecionando quais clientes receberão o RPC</span><span class="sxs-lookup"><span data-stu-id="e8951-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="e8951-279">A propriedade Clientes retorna um objeto [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) que fornece várias opções para especificar quais clientes receberão o RPC:</span><span class="sxs-lookup"><span data-stu-id="e8951-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="e8951-280">Todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="e8951-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="e8951-281">Só o cliente de chamada.</span><span class="sxs-lookup"><span data-stu-id="e8951-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="e8951-282">Todos os clientes, exceto o cliente de chamada.</span><span class="sxs-lookup"><span data-stu-id="e8951-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="e8951-283">Um cliente específico identificado pelo ID de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="e8951-284">Este exemplo `addContosoChatMessageToPage` chama o cliente de chamada `Clients.Caller`e tem o mesmo efeito que usar .</span><span class="sxs-lookup"><span data-stu-id="e8951-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="e8951-285">Todos os clientes conectados, exceto os clientes especificados, identificados por identificação de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="e8951-286">Todos os clientes conectados em um grupo especificado.</span><span class="sxs-lookup"><span data-stu-id="e8951-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="e8951-287">Todos os clientes conectados em um grupo especificado, exceto os clientes especificados, identificados por identificação de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="e8951-288">Todos os clientes conectados em um grupo especificado, exceto o cliente de chamada.</span><span class="sxs-lookup"><span data-stu-id="e8951-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="e8951-289">Um usuário específico, identificado por userId.</span><span class="sxs-lookup"><span data-stu-id="e8951-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="e8951-290">Por padrão, `IPrincipal.Identity.Name`isso é , mas isso pode ser alterado [registrando uma implementação do IUserIdProvider com o host global](mapping-users-to-connections.md#IUserIdProvider).</span><span class="sxs-lookup"><span data-stu-id="e8951-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="e8951-291">Todos os clientes e grupos em uma lista de IDs de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="e8951-292">Uma lista de grupos.</span><span class="sxs-lookup"><span data-stu-id="e8951-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="e8951-293">Um usuário pelo nome.</span><span class="sxs-lookup"><span data-stu-id="e8951-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="e8951-294">Uma lista de nomes de usuário (introduzida no SignalR 2.1).</span><span class="sxs-lookup"><span data-stu-id="e8951-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="e8951-295">Nenhuma validação de tempo de compilação para nomes de métodos</span><span class="sxs-lookup"><span data-stu-id="e8951-295">No compile-time validation for method names</span></span>

<span data-ttu-id="e8951-296">O nome do método que você especifica é interpretado como um objeto dinâmico, o que significa que não há validação intelliSense ou tempo de compilação para ele.</span><span class="sxs-lookup"><span data-stu-id="e8951-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="e8951-297">A expressão é avaliada no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e8951-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="e8951-298">Quando a chamada do método é executada, o SignalR envia o nome do método e os valores do parâmetro para o cliente, e se o cliente tiver um método que corresponda ao nome, esse método é chamado e os valores do parâmetro são passados para ele.</span><span class="sxs-lookup"><span data-stu-id="e8951-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="e8951-299">Se nenhum método de correspondência for encontrado no cliente, nenhum erro será levantado.</span><span class="sxs-lookup"><span data-stu-id="e8951-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="e8951-300">Para obter informações sobre o formato dos dados que o SignalR transmite ao cliente nos bastidores quando você chama um método cliente, consulte [Introdução ao SignalR](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="e8951-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="e8951-301">Correspondência de nome do método insensível a casos</span><span class="sxs-lookup"><span data-stu-id="e8951-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="e8951-302">A correspondência do nome do método é insensível ao caso.</span><span class="sxs-lookup"><span data-stu-id="e8951-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="e8951-303">Por `Clients.All.addContosoChatMessageToPage` exemplo, no servidor `AddContosoChatMessageToPage` `addcontosochatmessagetopage`executará `addContosoChatMessageToPage` , ou no cliente.</span><span class="sxs-lookup"><span data-stu-id="e8951-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="e8951-304">Execução assíncrona</span><span class="sxs-lookup"><span data-stu-id="e8951-304">Asynchronous execution</span></span>

<span data-ttu-id="e8951-305">O método que você chama executa assíncronamente.</span><span class="sxs-lookup"><span data-stu-id="e8951-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="e8951-306">Qualquer código que venha após uma chamada de método para um cliente será executado imediatamente sem esperar que o SignalR termine de transmitir dados aos clientes, a menos que você especifique que as linhas de código subseqüentes devem aguardar a conclusão do método.</span><span class="sxs-lookup"><span data-stu-id="e8951-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="e8951-307">O exemplo de código a seguir mostra como executar dois métodos cliente sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="e8951-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="e8951-308">**Usando aguardar (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="e8951-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="e8951-309">Se você `await` usar para esperar até que um método cliente termine antes que a próxima linha de código seja executada, isso não significa que os clientes realmente receberão a mensagem antes que a próxima linha de código seja executada.</span><span class="sxs-lookup"><span data-stu-id="e8951-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="e8951-310">"Conclusão" de uma chamada de método do cliente significa apenas que o SignalR fez tudo o que era necessário para enviar a mensagem.</span><span class="sxs-lookup"><span data-stu-id="e8951-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="e8951-311">Se você precisa verificar se os clientes receberam a mensagem, você mesmo tem que programar esse mecanismo.</span><span class="sxs-lookup"><span data-stu-id="e8951-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="e8951-312">Por exemplo, você `MessageReceived` pode codificar um método `addContosoChatMessageToPage` no Hub, e `MessageReceived` no método no cliente você pode ligar depois de fazer o trabalho que você precisa fazer no cliente.</span><span class="sxs-lookup"><span data-stu-id="e8951-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="e8951-313">No `MessageReceived` Hub você pode fazer qualquer trabalho que dependa da recepção e processamento real do método de chamada.</span><span class="sxs-lookup"><span data-stu-id="e8951-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="e8951-314">Como usar uma variável de string como nome do método</span><span class="sxs-lookup"><span data-stu-id="e8951-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="e8951-315">Se você quiser invocar um método cliente usando uma variável `Clients.All` de `Clients.Others` `Clients.Caller`string como nome `IClientProxy` do método, cast (ou , etc.) para e, em seguida, chamar [Invocação (métodoNome, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="e8951-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="e8951-316">Como gerenciar a adesão ao grupo da classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="e8951-317">Os grupos no SignalR fornecem um método para transmitir mensagens para subconjuntos especificados de clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="e8951-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="e8951-318">Um grupo pode ter qualquer número de clientes, e um cliente pode ser membro de qualquer número de grupos.</span><span class="sxs-lookup"><span data-stu-id="e8951-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="e8951-319">Para gerenciar a associação de grupos, use os `Groups` métodos [Adicionar](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) e [Remover](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) fornecidos pela propriedade da classe Hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="e8951-320">O exemplo a `Groups.Add` `Groups.Remove` seguir mostra os métodos usados nos métodos do Hub que são chamados pelo código do cliente, seguidos pelo código cliente JavaScript que os chama.</span><span class="sxs-lookup"><span data-stu-id="e8951-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="e8951-321">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="e8951-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="e8951-322">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="e8951-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="e8951-323">Você não precisa criar grupos explicitamente.</span><span class="sxs-lookup"><span data-stu-id="e8951-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="e8951-324">Na verdade, um grupo é criado automaticamente na primeira vez `Groups.Add`que você especifica seu nome em uma chamada para , e ele é excluído quando você remove a última conexão de adesão a ele.</span><span class="sxs-lookup"><span data-stu-id="e8951-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="e8951-325">Não há API para obter uma lista de membros de grupo ou uma lista de grupos.</span><span class="sxs-lookup"><span data-stu-id="e8951-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="e8951-326">O SignalR envia mensagens para clientes e grupos com base em um [modelo pub/sub,](http://en.wikipedia.org/wiki/Publish/subscribe)e o servidor não mantém listas de grupos ou membros de grupos.</span><span class="sxs-lookup"><span data-stu-id="e8951-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="e8951-327">Isso ajuda a maximizar a escalabilidade, porque sempre que você adiciona um nó a uma fazenda web, qualquer estado que o SignalR mantém tem que ser propagado para o novo nó.</span><span class="sxs-lookup"><span data-stu-id="e8951-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="e8951-328">Execução assíncrona dos métodos Adicionar e Remover</span><span class="sxs-lookup"><span data-stu-id="e8951-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="e8951-329">Os `Groups.Add` `Groups.Remove` métodos e métodos são executados assíncronamente.</span><span class="sxs-lookup"><span data-stu-id="e8951-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="e8951-330">Se você quiser adicionar um cliente a um grupo e enviar imediatamente uma mensagem ao `Groups.Add` cliente usando o grupo, você tem que ter certeza de que o método termina primeiro.</span><span class="sxs-lookup"><span data-stu-id="e8951-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="e8951-331">O exemplo de código a seguir mostra como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="e8951-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="e8951-332">**Adicionando um cliente a um grupo e, em seguida, mensagens que o cliente**</span><span class="sxs-lookup"><span data-stu-id="e8951-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="e8951-333">Persistência de membros do grupo</span><span class="sxs-lookup"><span data-stu-id="e8951-333">Group membership persistence</span></span>

<span data-ttu-id="e8951-334">O SignalR rastreia conexões, não usuários, então se você quiser que um usuário esteja no mesmo `Groups.Add` grupo toda vez que o usuário estabelecer uma conexão, você tem que ligar toda vez que o usuário estabelecer uma nova conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="e8951-335">Depois de uma perda temporária de conectividade, às vezes o SignalR pode restaurar a conexão automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e8951-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="e8951-336">Nesse caso, o SignalR está restaurando a mesma conexão, não estabelecendo uma nova conexão, e assim a adesão ao grupo do cliente é automaticamente restaurada.</span><span class="sxs-lookup"><span data-stu-id="e8951-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="e8951-337">Isso é possível mesmo quando a interrupção temporária é resultado de uma reinicialização ou falha do servidor, porque o estado de conexão para cada cliente, incluindo membros do grupo, é acionado para o cliente.</span><span class="sxs-lookup"><span data-stu-id="e8951-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="e8951-338">Se um servidor for para baixo e for substituído por um novo servidor antes do tempo de conexão acabar, um cliente poderá se reconectar automaticamente ao novo servidor e reinscrever-se em grupos dos dois membros.</span><span class="sxs-lookup"><span data-stu-id="e8951-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="e8951-339">Quando uma conexão não pode ser restaurada automaticamente após uma perda de conectividade, ou quando a conexão é desligada, ou quando o cliente se desconecta (por exemplo, quando um navegador navega para uma nova página), as associações do grupo são perdidas.</span><span class="sxs-lookup"><span data-stu-id="e8951-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="e8951-340">A próxima vez que o usuário se conectar será uma nova conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="e8951-341">Para manter as associações em grupo quando o mesmo usuário estabelecer uma nova conexão, seu aplicativo tem que rastrear as associações entre usuários e grupos e restaurar membros de grupo cada vez que um usuário estabelece uma nova conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="e8951-342">Para obter mais informações sobre conexões e reconexões, consulte [Como lidar com eventos de conexão vitalícia na classe Hub](#connectionlifetime) mais tarde neste tópico.</span><span class="sxs-lookup"><span data-stu-id="e8951-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="e8951-343">Grupos de usuários únicos</span><span class="sxs-lookup"><span data-stu-id="e8951-343">Single-user groups</span></span>

<span data-ttu-id="e8951-344">Os aplicativos que usam signalR normalmente têm que acompanhar as associações entre usuários e conexões para saber qual usuário enviou uma mensagem e quais usuários devem receber uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="e8951-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="e8951-345">Grupos são usados em um dos dois padrões comumente usados para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="e8951-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="e8951-346">Grupos de usuários únicos.</span><span class="sxs-lookup"><span data-stu-id="e8951-346">Single-user groups.</span></span>

    <span data-ttu-id="e8951-347">Você pode especificar o nome de usuário como nome do grupo e adicionar o ID de conexão atual ao grupo toda vez que o usuário se conectar ou se reconectar.</span><span class="sxs-lookup"><span data-stu-id="e8951-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="e8951-348">Para enviar mensagens ao usuário você envia para o grupo.</span><span class="sxs-lookup"><span data-stu-id="e8951-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="e8951-349">Uma desvantagem desse método é que o grupo não fornece uma maneira de descobrir se o usuário está online ou offline.</span><span class="sxs-lookup"><span data-stu-id="e8951-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="e8951-350">Rastreie associações entre nomes de usuários e IDs de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="e8951-351">Você pode armazenar uma associação entre cada nome de usuário e um ou mais IDs de conexão em um dicionário ou banco de dados, e atualizar os dados armazenados cada vez que o usuário se conecta ou desconecta.</span><span class="sxs-lookup"><span data-stu-id="e8951-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="e8951-352">Para enviar mensagens ao usuário, você especifica os IDs de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="e8951-353">Uma desvantagem deste método é que ele requer mais memória.</span><span class="sxs-lookup"><span data-stu-id="e8951-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="e8951-354">Como lidar com eventos de conexão vitalícia na classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="e8951-355">As razões típicas para lidar com eventos de vida de conexão são para acompanhar se um usuário está conectado ou não, e para acompanhar a associação entre nomes de usuários e IDs de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="e8951-356">Para executar seu próprio código quando os `OnConnected`clientes se conectarem ou desconectarem, anular os `OnDisconnected`métodos virtuais e `OnReconnected` virtuais da classe Hub, como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e8951-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="e8951-357">Quando onConnected, OnDisconnected e OnReconnected são chamados</span><span class="sxs-lookup"><span data-stu-id="e8951-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="e8951-358">Cada vez que um navegador navega para uma nova página, uma nova conexão deve `OnConnected` ser estabelecida, o que significa que o SignalR executará o `OnDisconnected` método seguido pelo método.</span><span class="sxs-lookup"><span data-stu-id="e8951-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="e8951-359">SignalR sempre cria um novo ID de conexão quando uma nova conexão é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e8951-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="e8951-360">O `OnReconnected` método é chamado quando há uma interrupção temporária na conectividade da a que o SignalR pode recuperar automaticamente, como quando um cabo é temporariamente desconectado e reconectado antes que o tempo de conexão seja desligado. O `OnDisconnected` método é chamado quando o cliente é desconectado e o SignalR não pode se reconectar automaticamente, como quando um navegador navega para uma nova página.</span><span class="sxs-lookup"><span data-stu-id="e8951-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="e8951-361">Portanto, uma possível seqüência de `OnConnected`eventos `OnReconnected` `OnDisconnected`para um determinado cliente é, ; `OnConnected`ou, `OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="e8951-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="e8951-362">Você não verá a `OnConnected` `OnDisconnected`seqüência, `OnReconnected` para uma determinada conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="e8951-363">O `OnDisconnected` método não é chamado em alguns cenários, como quando um servidor cai ou o Domínio do Aplicativo é reciclado.</span><span class="sxs-lookup"><span data-stu-id="e8951-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="e8951-364">Quando outro servidor entra em linha ou o Domínio do Aplicativo completa sua reciclagem, alguns clientes podem ser capazes de se reconectar e disparar o `OnReconnected` evento.</span><span class="sxs-lookup"><span data-stu-id="e8951-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="e8951-365">Para obter mais informações, consulte [Compreensão e manipulação de eventos vitalícios de conexão no SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="e8951-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="e8951-366">Estado de chamada não povoado</span><span class="sxs-lookup"><span data-stu-id="e8951-366">Caller state not populated</span></span>

<span data-ttu-id="e8951-367">Os métodos de manipulador de eventos de vida de conexão são `state` chamados do servidor, o que `Caller` significa que qualquer estado que você colocar o objeto no cliente não será preenchido na propriedade no servidor.</span><span class="sxs-lookup"><span data-stu-id="e8951-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="e8951-368">Para obter `state` informações sobre `Caller` o objeto e a propriedade, consulte [Como passar o estado entre os clientes e a classe Hub](#passstate) mais tarde neste tópico.</span><span class="sxs-lookup"><span data-stu-id="e8951-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="e8951-369">Como obter informações sobre o cliente a partir da propriedade Context</span><span class="sxs-lookup"><span data-stu-id="e8951-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="e8951-370">Para obter informações sobre o `Context` cliente, use a propriedade da classe Hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="e8951-371">A `Context` propriedade retorna um objeto [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) que fornece acesso às seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="e8951-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="e8951-372">A ID de conexão do cliente de chamada.</span><span class="sxs-lookup"><span data-stu-id="e8951-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="e8951-373">O ID de conexão é um GUID atribuído pelo SignalR (você não pode especificar o valor em seu próprio código).</span><span class="sxs-lookup"><span data-stu-id="e8951-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="e8951-374">Há um ID de conexão para cada conexão, e o mesmo ID de conexão é usado por todos os Hubs se você tiver vários Hubs em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8951-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="e8951-375">Dados de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="e8951-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="e8951-376">Você também pode obter `Context.Headers`cabeçalhos HTTP de .</span><span class="sxs-lookup"><span data-stu-id="e8951-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="e8951-377">A razão para múltiplas referências à `Context.Headers` mesma coisa é `Context.Request` que foi criada `Context.Headers` primeiro, a propriedade foi adicionada mais tarde, e foi mantida para compatibilidade retrógrada.</span><span class="sxs-lookup"><span data-stu-id="e8951-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="e8951-378">Consultar dados de seqüência.</span><span class="sxs-lookup"><span data-stu-id="e8951-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="e8951-379">Você também pode obter dados `Context.QueryString`de seqüência de consulta de .</span><span class="sxs-lookup"><span data-stu-id="e8951-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="e8951-380">A seqüência de consulta que você recebe nesta propriedade é a que foi usada com a solicitação HTTP que estabeleceu a conexão SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8951-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="e8951-381">Você pode adicionar parâmetros de seqüência de consulta no cliente configurando a conexão, que é uma maneira conveniente de passar dados sobre o cliente do cliente para o servidor.</span><span class="sxs-lookup"><span data-stu-id="e8951-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="e8951-382">O exemplo a seguir mostra uma maneira de adicionar uma seqüência de consultas em um cliente JavaScript quando você usa o proxy gerado.</span><span class="sxs-lookup"><span data-stu-id="e8951-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="e8951-383">Para obter mais informações sobre como definir parâmetros de seqüência de consultas, consulte as guias de API para os clientes [JavaScript](hubs-api-guide-javascript-client.md) e [.NET.](hubs-api-guide-net-client.md)</span><span class="sxs-lookup"><span data-stu-id="e8951-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="e8951-384">Você pode encontrar o método de transporte usado para a conexão nos dados da seqüência de consultas, juntamente com alguns outros valores usados internamente pelo SignalR:</span><span class="sxs-lookup"><span data-stu-id="e8951-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="e8951-385">O valor `transportMethod` será "webSockets", "serverSentEvents", "foreverFrame" ou "longPolling".</span><span class="sxs-lookup"><span data-stu-id="e8951-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="e8951-386">Observe que se você verificar `OnConnected` esse valor no método de manipulador de eventos, em alguns cenários você pode inicialmente obter um valor de transporte que não é o método final de transporte negociado para a conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="e8951-387">Nesse caso, o método abrirá uma exceção e será chamado novamente mais tarde quando o método final de transporte for estabelecido.</span><span class="sxs-lookup"><span data-stu-id="e8951-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="e8951-388">Cookies.</span><span class="sxs-lookup"><span data-stu-id="e8951-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="e8951-389">Você também pode `Context.RequestCookies`obter cookies de .</span><span class="sxs-lookup"><span data-stu-id="e8951-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="e8951-390">Informação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e8951-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="e8951-391">O objeto HttpContext para a solicitação :</span><span class="sxs-lookup"><span data-stu-id="e8951-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="e8951-392">Use este método `HttpContext.Current` em vez `HttpContext` de obter o objeto para a conexão SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8951-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="e8951-393">Como passar o estado entre clientes e a classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="e8951-394">O proxy do `state` cliente fornece um objeto no qual você pode armazenar dados que deseja ser transmitidos ao servidor com cada chamada de método.</span><span class="sxs-lookup"><span data-stu-id="e8951-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="e8951-395">No servidor você pode acessar `Clients.Caller` esses dados na propriedade nos métodos do Hub que são chamados pelos clientes.</span><span class="sxs-lookup"><span data-stu-id="e8951-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="e8951-396">A `Clients.Caller` propriedade não está povoada para `OnConnected`os `OnDisconnected`métodos de manipulador de eventos de vida de conexão, e `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="e8951-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="e8951-397">Criar ou atualizar `state` dados no `Clients.Caller` objeto e a propriedade funciona em ambas as direções.</span><span class="sxs-lookup"><span data-stu-id="e8951-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="e8951-398">Você pode atualizar valores no servidor e eles são repassados para o cliente.</span><span class="sxs-lookup"><span data-stu-id="e8951-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="e8951-399">O exemplo a seguir mostra o código cliente JavaScript que armazena estado para transmissão para o servidor a cada chamada de método.</span><span class="sxs-lookup"><span data-stu-id="e8951-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="e8951-400">O exemplo a seguir mostra o código equivalente em um cliente .NET.</span><span class="sxs-lookup"><span data-stu-id="e8951-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="e8951-401">Na sua classe Hub, você pode `Clients.Caller` acessar esses dados na propriedade.</span><span class="sxs-lookup"><span data-stu-id="e8951-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="e8951-402">O exemplo a seguir mostra o código que recupera o estado referido no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="e8951-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="e8951-403">Este mecanismo para o estado persistente não se destina a grandes `state` `Clients.Caller` quantidades de dados, uma vez que tudo o que você coloca na propriedade ou é rodada-tripped com cada invocação do método.</span><span class="sxs-lookup"><span data-stu-id="e8951-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="e8951-404">É útil para itens menores, como nomes de usuários ou contadores.</span><span class="sxs-lookup"><span data-stu-id="e8951-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="e8951-405">Em VB.NET ou em um hub fortemente digitado, o objeto `Clients.Caller`de estado do chamador não pode ser acessado através de ; em vez `Clients.CallerState` disso, use (introduzido no SignalR 2.1):</span><span class="sxs-lookup"><span data-stu-id="e8951-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="e8951-406">**Usando CallerState em C #**</span><span class="sxs-lookup"><span data-stu-id="e8951-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="e8951-407">**Usando callerstate no Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="e8951-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="e8951-408">Como lidar com erros na classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="e8951-409">Para lidar com erros que ocorrem nos métodos da classe Hub, primeiro certifique-se de "observar" `await`quaisquer exceções de operações assíncronas (como invocar métodos do cliente) usando .</span><span class="sxs-lookup"><span data-stu-id="e8951-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="e8951-410">Em seguida, use um ou mais dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="e8951-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="e8951-411">Enrole o código do método em blocos de captura e registre o objeto de exceção.</span><span class="sxs-lookup"><span data-stu-id="e8951-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="e8951-412">Para fins de depuração, você pode enviar a exceção ao cliente, mas por razões de segurança o envio de informações detalhadas aos clientes em produção não é recomendado.</span><span class="sxs-lookup"><span data-stu-id="e8951-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="e8951-413">Crie um módulo de pipeline hubs que lida com o método [OnIncomingError.](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="e8951-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="e8951-414">O exemplo a seguir mostra um módulo de pipeline que registra erros, seguido de código em Startup.cs que injeta o módulo no pipeline do Hubs.</span><span class="sxs-lookup"><span data-stu-id="e8951-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="e8951-415">Use `HubException` a classe (introduzida no SignalR 2).</span><span class="sxs-lookup"><span data-stu-id="e8951-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="e8951-416">Este erro pode ser jogado de qualquer invocação do hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="e8951-417">O `HubError` construtor recebe uma mensagem de string e um objeto para armazenar dados extras de erro.</span><span class="sxs-lookup"><span data-stu-id="e8951-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="e8951-418">O SignalR serializará automaticamente a exceção e enviará ao cliente, onde será usado para rejeitar ou falhar a invocação do método hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="e8951-419">As amostras de código a `HubException` seguir demonstram como jogar um durante uma invocação do Hub e como lidar com a exceção em clientes JavaScript e .NET.</span><span class="sxs-lookup"><span data-stu-id="e8951-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="e8951-420">**Código do servidor demonstrando a classe HubException**</span><span class="sxs-lookup"><span data-stu-id="e8951-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="e8951-421">**Código do cliente JavaScript demonstrando resposta a jogar um HubException em um hub**</span><span class="sxs-lookup"><span data-stu-id="e8951-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="e8951-422">**Código de cliente .NET demonstrando resposta a jogar um HubException em um hub**</span><span class="sxs-lookup"><span data-stu-id="e8951-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="e8951-423">Para obter mais informações sobre os módulos de pipeline do Hub, consulte [Como personalizar o pipeline do Hubs](#hubpipeline) mais tarde neste tópico.</span><span class="sxs-lookup"><span data-stu-id="e8951-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="e8951-424">Como habilitar o rastreamento</span><span class="sxs-lookup"><span data-stu-id="e8951-424">How to enable tracing</span></span>

<span data-ttu-id="e8951-425">Para habilitar o rastreamento do lado do servidor, adicione um elemento system.diagnostics ao seu arquivo Web.config, como mostrado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="e8951-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="e8951-426">Quando você executa o aplicativo no Visual Studio, você pode visualizar os logs na janela **Saída.**</span><span class="sxs-lookup"><span data-stu-id="e8951-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="e8951-427">Como chamar métodos de clientes e gerenciar grupos de fora da classe Hub</span><span class="sxs-lookup"><span data-stu-id="e8951-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="e8951-428">Para chamar métodos de cliente de uma classe diferente da sua classe Hub, obtenha uma referência ao objeto de contexto SignalR para o Hub e use-o para chamar métodos no cliente ou gerenciar grupos.</span><span class="sxs-lookup"><span data-stu-id="e8951-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="e8951-429">A classe `StockTicker` de amostra a seguir obtém o objeto de contexto, armazena-o em uma instância da classe, `updateStockPrice` armazena a instância de classe `StockTickerHub`em uma propriedade estática e usa o contexto da instância de classe singleton para chamar o método em clientes conectados a um Hub chamado .</span><span class="sxs-lookup"><span data-stu-id="e8951-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="e8951-430">Se você precisar usar o contexto várias vezes em um objeto de longa duração, obtenha a referência uma vez e salve-a em vez de obtê-lo novamente cada vez.</span><span class="sxs-lookup"><span data-stu-id="e8951-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="e8951-431">Obter o contexto uma vez garante que o SignalR envie mensagens aos clientes na mesma seqüência em que seus métodos do Hub fazem invocações de métodos clientes.</span><span class="sxs-lookup"><span data-stu-id="e8951-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="e8951-432">Para obter um tutorial que mostre como usar o contexto SignalR para um Hub, consulte [Server Broadcast com ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="e8951-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="e8951-433">Chamando métodos de cliente</span><span class="sxs-lookup"><span data-stu-id="e8951-433">Calling client methods</span></span>

<span data-ttu-id="e8951-434">Você pode especificar quais clientes receberão o RPC, mas você tem menos opções do que quando você liga de uma classe Hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="e8951-435">A razão para isso é que o contexto não está associado a uma determinada chamada de um cliente, `Clients.Others`portanto, quaisquer métodos que exijam conhecimento do ID de conexão atual, como , ou `Clients.Caller`, ou `Clients.OthersInGroup`, não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e8951-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="e8951-436">As seguintes opções estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="e8951-436">The following options are available:</span></span>

- <span data-ttu-id="e8951-437">Todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="e8951-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="e8951-438">Um cliente específico identificado pelo ID de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="e8951-439">Todos os clientes conectados, exceto os clientes especificados, identificados por identificação de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="e8951-440">Todos os clientes conectados em um grupo especificado.</span><span class="sxs-lookup"><span data-stu-id="e8951-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="e8951-441">Todos os clientes conectados em um grupo especificado, exceto clientes especificados, identificados por id de conexão.</span><span class="sxs-lookup"><span data-stu-id="e8951-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="e8951-442">Se você estiver ligando para a sua classe não-Hub a partir de métodos em `Clients.Client` `Clients.AllExcept`sua `Clients.Group` classe `Clients.Caller`Hub, você pode passar no ID de conexão atual e usá-lo com , ou para simular , `Clients.Others`ou `Clients.OthersInGroup`.</span><span class="sxs-lookup"><span data-stu-id="e8951-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="e8951-443">No exemplo a `MoveShapeHub` seguir, a classe passa `Broadcaster` o ID `Broadcaster` de `Clients.Others`conexão para a classe para que a classe possa simular .</span><span class="sxs-lookup"><span data-stu-id="e8951-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="e8951-444">Gestão de membros do grupo</span><span class="sxs-lookup"><span data-stu-id="e8951-444">Managing group membership</span></span>

<span data-ttu-id="e8951-445">Para gerenciar grupos, você tem as mesmas opções que você tem em uma classe Hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="e8951-446">Adicione um cliente a um grupo</span><span class="sxs-lookup"><span data-stu-id="e8951-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="e8951-447">Remova um cliente de um grupo</span><span class="sxs-lookup"><span data-stu-id="e8951-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="e8951-448">Como personalizar o pipeline do Hubs</span><span class="sxs-lookup"><span data-stu-id="e8951-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="e8951-449">SignalR permite que você injete seu próprio código no pipeline do Hub.</span><span class="sxs-lookup"><span data-stu-id="e8951-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="e8951-450">O exemplo a seguir mostra um módulo de pipeline hub personalizado que registra cada chamada de método recebida do cliente e chamada de método de saída invocada no cliente:</span><span class="sxs-lookup"><span data-stu-id="e8951-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="e8951-451">O código a seguir no *arquivo Startup.cs* registra o módulo a ser executado no pipeline do Hub:</span><span class="sxs-lookup"><span data-stu-id="e8951-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="e8951-452">Existem muitos métodos diferentes que você pode substituir.</span><span class="sxs-lookup"><span data-stu-id="e8951-452">There are many different methods that you can override.</span></span> <span data-ttu-id="e8951-453">Para obter uma lista completa, consulte [Métodos hubPipelineModule](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="e8951-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
