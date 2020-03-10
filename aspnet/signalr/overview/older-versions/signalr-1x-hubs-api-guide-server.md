---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: Guia da API de hubs do Signalr ASP.NET – servidor (Signalr 1. x) | Microsoft Docs
author: bradygaster
description: Este documento fornece uma introdução à programação do lado do servidor da API de hubs do Signalr ASP.NET para o Signalr versão 1,1, com exemplos de código que demonstram...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579635"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a><span data-ttu-id="5983a-103">Guia da API de hubs do Signalr ASP.NET – servidor (Signalr 1. x)</span><span class="sxs-lookup"><span data-stu-id="5983a-103">ASP.NET SignalR Hubs API Guide - Server (SignalR 1.x)</span></span>

<span data-ttu-id="5983a-104">por [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5983a-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5983a-105">Este documento fornece uma introdução à programação do lado do servidor da API de hubs do Signalr ASP.NET para o Signalr versão 1,1, com exemplos de código que demonstram opções comuns.</span><span class="sxs-lookup"><span data-stu-id="5983a-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 1.1, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="5983a-106">A API de hubs de Signalr permite que você faça RPCs (chamadas de procedimento remoto) de um servidor para clientes conectados e de clientes para o servidor.</span><span class="sxs-lookup"><span data-stu-id="5983a-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="5983a-107">No código do servidor, você define métodos que podem ser chamados por clientes e chama métodos que são executados no cliente.</span><span class="sxs-lookup"><span data-stu-id="5983a-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="5983a-108">No código do cliente, você define métodos que podem ser chamados do servidor e chama métodos que são executados no servidor.</span><span class="sxs-lookup"><span data-stu-id="5983a-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="5983a-109">O signalr cuida de todo o direcionamento de cliente para servidor para você.</span><span class="sxs-lookup"><span data-stu-id="5983a-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="5983a-110">O signalr também oferece uma API de nível inferior chamada conexões persistentes.</span><span class="sxs-lookup"><span data-stu-id="5983a-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="5983a-111">Para obter uma introdução ao Signalr, hubs e conexões persistentes, ou para um tutorial que mostra como criar um aplicativo Signalr completo, consulte [signalr-introdução](index.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="5983a-112">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5983a-112">Overview</span></span>

<span data-ttu-id="5983a-113">Este documento contém as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="5983a-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="5983a-114">Como registrar a rota do Signalr e configurar as opções do Signalr</span><span class="sxs-lookup"><span data-stu-id="5983a-114">How to register the SignalR route and configure SignalR options</span></span>](#route)

    - [<span data-ttu-id="5983a-115">A URL do/signalr</span><span class="sxs-lookup"><span data-stu-id="5983a-115">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="5983a-116">Configurando opções do Signalr</span><span class="sxs-lookup"><span data-stu-id="5983a-116">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="5983a-117">Como criar e usar classes de Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-117">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="5983a-118">Tempo de vida do objeto Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-118">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="5983a-119">Camel-compartimento de nomes de Hub em clientes JavaScript</span><span class="sxs-lookup"><span data-stu-id="5983a-119">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="5983a-120">Vários hubs</span><span class="sxs-lookup"><span data-stu-id="5983a-120">Multiple Hubs</span></span>](#multiplehubs)
- [<span data-ttu-id="5983a-121">Como definir métodos na classe Hub que os clientes podem chamar</span><span class="sxs-lookup"><span data-stu-id="5983a-121">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="5983a-122">Camel-capitalização de nomes de método em clientes JavaScript</span><span class="sxs-lookup"><span data-stu-id="5983a-122">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="5983a-123">Quando executar de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="5983a-123">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="5983a-124">Definindo sobrecargas</span><span class="sxs-lookup"><span data-stu-id="5983a-124">Defining overloads</span></span>](#overloads)
- [<span data-ttu-id="5983a-125">Como chamar métodos de cliente da classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-125">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="5983a-126">Selecionando quais clientes receberão o RPC</span><span class="sxs-lookup"><span data-stu-id="5983a-126">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="5983a-127">Nenhuma validação de tempo de compilação para nomes de método</span><span class="sxs-lookup"><span data-stu-id="5983a-127">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="5983a-128">Correspondência de nome de método que não diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="5983a-128">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="5983a-129">Execução assíncrona</span><span class="sxs-lookup"><span data-stu-id="5983a-129">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="5983a-130">Como gerenciar a associação de grupo da classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-130">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="5983a-131">Execução assíncrona de métodos Add e remove</span><span class="sxs-lookup"><span data-stu-id="5983a-131">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="5983a-132">Persistência de associação de grupo</span><span class="sxs-lookup"><span data-stu-id="5983a-132">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="5983a-133">Grupos de usuário único</span><span class="sxs-lookup"><span data-stu-id="5983a-133">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="5983a-134">Como tratar eventos de tempo de vida da conexão na classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-134">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="5983a-135">Quando onconnected, OnDisconnect e OnReconnected são chamados</span><span class="sxs-lookup"><span data-stu-id="5983a-135">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="5983a-136">Estado do chamador não preenchido</span><span class="sxs-lookup"><span data-stu-id="5983a-136">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="5983a-137">Como obter informações sobre o cliente a partir da propriedade Context</span><span class="sxs-lookup"><span data-stu-id="5983a-137">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="5983a-138">Como passar o estado entre clientes e a classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-138">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="5983a-139">Como tratar erros na classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-139">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="5983a-140">Como chamar métodos de cliente e gerenciar grupos de fora da classe de Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-140">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="5983a-141">Chamando métodos de cliente</span><span class="sxs-lookup"><span data-stu-id="5983a-141">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="5983a-142">Gerenciando a associação de grupo</span><span class="sxs-lookup"><span data-stu-id="5983a-142">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="5983a-143">Como habilitar o rastreamento</span><span class="sxs-lookup"><span data-stu-id="5983a-143">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="5983a-144">Como personalizar o pipeline de hubs</span><span class="sxs-lookup"><span data-stu-id="5983a-144">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="5983a-145">Para obter a documentação sobre como programar clientes do, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="5983a-145">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="5983a-146">Guia de API de hubs de signalr-cliente JavaScript</span><span class="sxs-lookup"><span data-stu-id="5983a-146">SignalR Hubs API Guide - JavaScript Client</span></span>](index.md)
- [<span data-ttu-id="5983a-147">Guia da API de hubs do signalr-cliente .NET</span><span class="sxs-lookup"><span data-stu-id="5983a-147">SignalR Hubs API Guide - .NET Client</span></span>](index.md)

<span data-ttu-id="5983a-148">Links para os tópicos de referência de API são para a versão 4,5 do .NET da API.</span><span class="sxs-lookup"><span data-stu-id="5983a-148">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="5983a-149">Se você estiver usando o .NET 4, consulte [a versão .NET 4 dos tópicos da API](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="5983a-149">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a><span data-ttu-id="5983a-150">Como registrar a rota do Signalr e configurar as opções do Signalr</span><span class="sxs-lookup"><span data-stu-id="5983a-150">How to register the SignalR route and configure SignalR options</span></span>

<span data-ttu-id="5983a-151">Para definir a rota que os clientes usarão para se conectar ao seu hub, chame o método [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) quando o aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="5983a-151">To define the route that clients will use to connect to your Hub, call the [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="5983a-152">`MapHubs` é um [método de extensão](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) para a classe `System.Web.Routing.RouteCollection`.</span><span class="sxs-lookup"><span data-stu-id="5983a-152">`MapHubs` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `System.Web.Routing.RouteCollection` class.</span></span> <span data-ttu-id="5983a-153">O exemplo a seguir mostra como definir a rota de hubs do Signalr no arquivo *global. asax* .</span><span class="sxs-lookup"><span data-stu-id="5983a-153">The following example shows how to define the SignalR Hubs route in the *Global.asax* file.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

<span data-ttu-id="5983a-154">Se você estiver adicionando a funcionalidade do Signalr a um aplicativo MVC ASP.NET, certifique-se de que a rota do Signalr seja adicionada antes das outras rotas.</span><span class="sxs-lookup"><span data-stu-id="5983a-154">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="5983a-155">Para obter mais informações, consulte [tutorial: introdução com signalr e MVC 4](index.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-155">For more information, see [Tutorial: Getting Started with SignalR and MVC 4](index.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="5983a-156">A URL do/signalr</span><span class="sxs-lookup"><span data-stu-id="5983a-156">The /signalr URL</span></span>

<span data-ttu-id="5983a-157">Por padrão, a URL de rota que os clientes usarão para se conectar ao seu hub é "/signalr".</span><span class="sxs-lookup"><span data-stu-id="5983a-157">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="5983a-158">(Não confunda essa URL com a URL "/signalr/hubs", que é para o arquivo JavaScript gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5983a-158">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="5983a-159">Para obter mais informações sobre o proxy gerado, consulte [Guia de API de hubs de signalr-cliente JavaScript-o proxy gerado e o que ele faz por você](index.md).)</span><span class="sxs-lookup"><span data-stu-id="5983a-159">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).)</span></span>

<span data-ttu-id="5983a-160">Pode haver circunstâncias extraordinárias que tornam essa URL base inutilizável para o Signalr; por exemplo, você tem uma pasta em seu projeto denominada *signalr* e não deseja alterar o nome.</span><span class="sxs-lookup"><span data-stu-id="5983a-160">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="5983a-161">Nesse caso, você pode alterar a URL base, conforme mostrado nos exemplos a seguir (substitua "/signalr" no código de exemplo pela URL desejada).</span><span class="sxs-lookup"><span data-stu-id="5983a-161">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="5983a-162">**Código do servidor que especifica a URL**</span><span class="sxs-lookup"><span data-stu-id="5983a-162">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

<span data-ttu-id="5983a-163">**Código de cliente JavaScript que especifica a URL (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="5983a-163">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="5983a-164">**Código de cliente JavaScript que especifica a URL (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="5983a-164">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

<span data-ttu-id="5983a-165">**Código de cliente .NET que especifica a URL**</span><span class="sxs-lookup"><span data-stu-id="5983a-165">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="5983a-166">Configurando opções do Signalr</span><span class="sxs-lookup"><span data-stu-id="5983a-166">Configuring SignalR Options</span></span>

<span data-ttu-id="5983a-167">Sobrecargas do método `MapHubs` permitem que você especifique uma URL personalizada, um resolvedor de dependência personalizado e as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="5983a-167">Overloads of the `MapHubs` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="5983a-168">Habilitar chamadas entre domínios de clientes de navegador.</span><span class="sxs-lookup"><span data-stu-id="5983a-168">Enable cross-domain calls from browser clients.</span></span>

    <span data-ttu-id="5983a-169">Normalmente, se o navegador carregar uma página de `http://contoso.com`, a conexão do Signalr estará no mesmo domínio, em `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="5983a-169">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="5983a-170">Se a página de `http://contoso.com` fizer uma conexão com `http://fabrikam.com/signalr`, essa será uma conexão entre domínios.</span><span class="sxs-lookup"><span data-stu-id="5983a-170">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="5983a-171">Por motivos de segurança, as conexões entre domínios são desabilitadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="5983a-171">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="5983a-172">Para obter mais informações, consulte [Guia de API de hubs do ASP.net signalr-cliente JavaScript-como estabelecer uma conexão entre domínios](index.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-172">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](index.md).</span></span>
- <span data-ttu-id="5983a-173">Habilitar mensagens de erro detalhadas.</span><span class="sxs-lookup"><span data-stu-id="5983a-173">Enable detailed error messages.</span></span>

    <span data-ttu-id="5983a-174">Quando ocorrem erros, o comportamento padrão do Signalr é enviar para os clientes uma mensagem de notificação sem detalhes sobre o que aconteceu.</span><span class="sxs-lookup"><span data-stu-id="5983a-174">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="5983a-175">Não é recomendável enviar informações de erro detalhadas para clientes em produção, pois usuários mal-intencionados podem usar as informações em ataques contra seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5983a-175">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="5983a-176">Para solucionar problemas, você pode usar essa opção para habilitar temporariamente relatórios de erros mais informativos.</span><span class="sxs-lookup"><span data-stu-id="5983a-176">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="5983a-177">Desabilitar arquivos de proxy JavaScript gerados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5983a-177">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="5983a-178">Por padrão, um arquivo JavaScript com proxies para suas classes de Hub é gerado em resposta à URL "/signalr/hubs".</span><span class="sxs-lookup"><span data-stu-id="5983a-178">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="5983a-179">Se você não quiser usar os proxies JavaScript ou se quiser gerar esse arquivo manualmente e se referir a um arquivo físico em seus clientes, poderá usar essa opção para desabilitar a geração de proxy.</span><span class="sxs-lookup"><span data-stu-id="5983a-179">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="5983a-180">Para obter mais informações, consulte [Guia de API de hubs de signalr-cliente JavaScript-como criar um arquivo físico para o proxy gerado pelo signalr](index.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-180">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](index.md).</span></span>

<span data-ttu-id="5983a-181">O exemplo a seguir mostra como especificar a URL de conexão do Signalr e essas opções em uma chamada para o método `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="5983a-181">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapHubs` method.</span></span> <span data-ttu-id="5983a-182">Para especificar uma URL personalizada, substitua "/signalr" no exemplo pela URL que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="5983a-182">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="5983a-183">Como criar e usar classes de Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-183">How to create and use Hub classes</span></span>

<span data-ttu-id="5983a-184">Para criar um Hub, crie uma classe que derive de [Microsoft. AspNet. signalr. Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="5983a-184">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="5983a-185">O exemplo a seguir mostra uma classe de Hub simples para um aplicativo de chat.</span><span class="sxs-lookup"><span data-stu-id="5983a-185">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

<span data-ttu-id="5983a-186">Neste exemplo, um cliente conectado pode chamar o método `NewContosoChatMessage` e, quando ele faz, os dados recebidos são transmitidos para todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="5983a-186">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="5983a-187">Tempo de vida do objeto Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-187">Hub object lifetime</span></span>

<span data-ttu-id="5983a-188">Você não instancia a classe Hub nem chama seus métodos de seu próprio código no servidor; tudo isso é feito para você pelo pipeline de hubs do Signalr.</span><span class="sxs-lookup"><span data-stu-id="5983a-188">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="5983a-189">O signalr cria uma nova instância da classe Hub cada vez que precisa manipular uma operação de Hub, como quando um cliente se conecta, desconecta ou faz uma chamada de método para o servidor.</span><span class="sxs-lookup"><span data-stu-id="5983a-189">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="5983a-190">Como as instâncias da classe Hub são transitórias, você não pode usá-las para manter o estado de uma chamada de método para a próxima.</span><span class="sxs-lookup"><span data-stu-id="5983a-190">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="5983a-191">Cada vez que o servidor recebe uma chamada de método de um cliente, uma nova instância da sua classe de Hub processa a mensagem.</span><span class="sxs-lookup"><span data-stu-id="5983a-191">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="5983a-192">Para manter o estado por meio de várias conexões e chamadas de método, use outro método, como um banco de dados, ou uma variável estática na classe Hub, ou uma classe diferente que não derive de `Hub`.</span><span class="sxs-lookup"><span data-stu-id="5983a-192">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="5983a-193">Se você persistir dados na memória, usando um método como uma variável estática na classe Hub, os dados serão perdidos quando o domínio do aplicativo for reciclado.</span><span class="sxs-lookup"><span data-stu-id="5983a-193">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="5983a-194">Se você quiser enviar mensagens para clientes de seu próprio código que é executado fora da classe Hub, não é possível fazer isso instanciando uma instância de classe de Hub, mas você pode fazer isso obtendo uma referência ao objeto de contexto Signalr para a classe Hub.</span><span class="sxs-lookup"><span data-stu-id="5983a-194">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="5983a-195">Para obter mais informações, consulte [como chamar métodos de cliente e gerenciar grupos de fora da classe de Hub](#callfromoutsidehub) mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="5983a-195">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="5983a-196">Camel-compartimento de nomes de Hub em clientes JavaScript</span><span class="sxs-lookup"><span data-stu-id="5983a-196">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="5983a-197">Por padrão, os clientes JavaScript se referem a hubs usando uma versão do nome de classe do camel case.</span><span class="sxs-lookup"><span data-stu-id="5983a-197">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="5983a-198">O signalr faz essa alteração automaticamente para que o código JavaScript possa estar em conformidade com as convenções de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5983a-198">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="5983a-199">O exemplo anterior seria conhecido como `contosoChatHub` no código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5983a-199">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="5983a-200">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="5983a-200">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

<span data-ttu-id="5983a-201">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="5983a-201">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

<span data-ttu-id="5983a-202">Se você quiser especificar um nome diferente para os clientes usarem, adicione o atributo `HubName`.</span><span class="sxs-lookup"><span data-stu-id="5983a-202">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="5983a-203">Quando você usa um atributo `HubName`, não há nenhuma alteração de nome para o camel case em clientes JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5983a-203">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="5983a-204">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="5983a-204">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

<span data-ttu-id="5983a-205">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="5983a-205">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="5983a-206">Vários hubs</span><span class="sxs-lookup"><span data-stu-id="5983a-206">Multiple Hubs</span></span>

<span data-ttu-id="5983a-207">Você pode definir várias classes de Hub em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5983a-207">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="5983a-208">Quando você faz isso, a conexão é compartilhada, mas os grupos são separados:</span><span class="sxs-lookup"><span data-stu-id="5983a-208">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="5983a-209">Todos os clientes usarão a mesma URL para estabelecer uma conexão de Signalr com seu serviço ("/signalr" ou sua URL personalizada se você tiver especificado um) e essa conexão será usada para todos os hubs definidos pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="5983a-209">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="5983a-210">Não há nenhuma diferença de desempenho para vários hubs em comparação com a definição de toda a funcionalidade de Hub em uma única classe.</span><span class="sxs-lookup"><span data-stu-id="5983a-210">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="5983a-211">Todos os hubs obtêm as mesmas informações de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="5983a-211">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="5983a-212">Como todos os hubs compartilham a mesma conexão, as únicas informações de solicitação HTTP que o servidor Obtém são o que vem na solicitação HTTP original que estabelece a conexão do Signalr.</span><span class="sxs-lookup"><span data-stu-id="5983a-212">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="5983a-213">Se você usar a solicitação de conexão para passar informações do cliente para o servidor, especificando uma cadeia de caracteres de consulta, não poderá fornecer cadeias de consulta diferentes para diferentes hubs.</span><span class="sxs-lookup"><span data-stu-id="5983a-213">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="5983a-214">Todos os hubs receberão as mesmas informações.</span><span class="sxs-lookup"><span data-stu-id="5983a-214">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="5983a-215">O arquivo de proxies JavaScript gerado conterá proxies para todos os hubs em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="5983a-215">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="5983a-216">Para obter informações sobre proxies JavaScript, consulte [Guia de API de hubs de signalr-cliente JavaScript-o proxy gerado e o que ele faz para você](index.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-216">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).</span></span>
- <span data-ttu-id="5983a-217">Os grupos são definidos dentro de hubs.</span><span class="sxs-lookup"><span data-stu-id="5983a-217">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="5983a-218">No Signalr, você pode definir grupos nomeados para difundir para subconjuntos de clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="5983a-218">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="5983a-219">Os grupos são mantidos separadamente para cada Hub.</span><span class="sxs-lookup"><span data-stu-id="5983a-219">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="5983a-220">Por exemplo, um grupo chamado "administradores" incluiria um conjunto de clientes para sua classe de `ContosoChatHub`, e o mesmo nome de grupo se referiria a um conjunto diferente de clientes para sua classe `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="5983a-220">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="5983a-221">Como definir métodos na classe Hub que os clientes podem chamar</span><span class="sxs-lookup"><span data-stu-id="5983a-221">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="5983a-222">Para expor um método no Hub que você deseja que possa ser chamado pelo cliente, declare um método público, conforme mostrado nos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="5983a-222">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="5983a-223">Você pode especificar um tipo de retorno e parâmetros, incluindo tipos complexos e matrizes, como faria em C# qualquer método.</span><span class="sxs-lookup"><span data-stu-id="5983a-223">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="5983a-224">Todos os dados que você recebe em parâmetros ou retornam ao chamador são comunicados entre o cliente e o servidor usando JSON, e o Signalr manipula a associação de objetos complexos e matrizes de objetos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5983a-224">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="5983a-225">Camel-capitalização de nomes de método em clientes JavaScript</span><span class="sxs-lookup"><span data-stu-id="5983a-225">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="5983a-226">Por padrão, os clientes JavaScript referem-se a métodos de Hub usando uma versão do nome do método com camel case.</span><span class="sxs-lookup"><span data-stu-id="5983a-226">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="5983a-227">O signalr faz essa alteração automaticamente para que o código JavaScript possa estar em conformidade com as convenções de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5983a-227">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="5983a-228">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="5983a-228">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="5983a-229">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="5983a-229">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="5983a-230">Se você quiser especificar um nome diferente para os clientes usarem, adicione o atributo `HubMethodName`.</span><span class="sxs-lookup"><span data-stu-id="5983a-230">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="5983a-231">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="5983a-231">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="5983a-232">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="5983a-232">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="5983a-233">Quando executar de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="5983a-233">When to execute asynchronously</span></span>

<span data-ttu-id="5983a-234">Se o método for de execução demorada ou precisar de trabalho que envolvesse espera, como uma pesquisa de banco de dados ou uma chamada de serviço Web, torne o método de Hub assíncrono retornando uma [tarefa](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (no lugar de `void` retorno) ou a [tarefa&lt;objeto t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) (em vez de `T` tipo de retorno).</span><span class="sxs-lookup"><span data-stu-id="5983a-234">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="5983a-235">Quando você retorna um objeto `Task` do método, o Signalr aguarda a conclusão da `Task` e, em seguida, envia o resultado desencapsulado para o cliente, de modo que não há diferença em como você codifica a chamada do método no cliente.</span><span class="sxs-lookup"><span data-stu-id="5983a-235">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="5983a-236">Tornar um método de Hub assíncrono evita o bloqueio da conexão quando ele usa o transporte WebSocket.</span><span class="sxs-lookup"><span data-stu-id="5983a-236">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="5983a-237">Quando um método de Hub é executado de forma síncrona e o transporte é WebSocket, as invocações subsequentes de métodos no Hub do mesmo cliente são bloqueadas até que o método de Hub seja concluído.</span><span class="sxs-lookup"><span data-stu-id="5983a-237">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="5983a-238">O exemplo a seguir mostra o mesmo método codificado para ser executado de forma síncrona ou assíncrona, seguido pelo código de cliente JavaScript que funciona para chamar qualquer versão.</span><span class="sxs-lookup"><span data-stu-id="5983a-238">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="5983a-239">**Replicação**</span><span class="sxs-lookup"><span data-stu-id="5983a-239">**Synchronous**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="5983a-240">**Assíncrona-ASP.NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="5983a-240">**Asynchronous - ASP.NET 4.5**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="5983a-241">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="5983a-241">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="5983a-242">Para obter mais informações sobre como usar métodos assíncronos no ASP.NET 4,5, consulte [usando métodos assíncronos no ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-242">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="5983a-243">Definindo sobrecargas</span><span class="sxs-lookup"><span data-stu-id="5983a-243">Defining Overloads</span></span>

<span data-ttu-id="5983a-244">Se você quiser definir sobrecargas para um método, o número de parâmetros em cada sobrecarga deverá ser diferente.</span><span class="sxs-lookup"><span data-stu-id="5983a-244">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="5983a-245">Se você diferenciar uma sobrecarga apenas especificando tipos de parâmetros diferentes, a classe de Hub será compilada, mas o serviço Signalr gerará uma exceção em tempo de execução quando os clientes tentarem chamar uma das sobrecargas.</span><span class="sxs-lookup"><span data-stu-id="5983a-245">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="5983a-246">Como chamar métodos de cliente da classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-246">How to call client methods from the Hub class</span></span>

<span data-ttu-id="5983a-247">Para chamar métodos de cliente do servidor, use a propriedade `Clients` em um método em sua classe de Hub.</span><span class="sxs-lookup"><span data-stu-id="5983a-247">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="5983a-248">O exemplo a seguir mostra o código do servidor que chama `addNewMessageToPage` em todos os clientes conectados e o código do cliente que define o método em um cliente JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5983a-248">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="5983a-249">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="5983a-249">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

<span data-ttu-id="5983a-250">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="5983a-250">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

<span data-ttu-id="5983a-251">Não é possível obter um valor de retorno de um método de cliente; a sintaxe como `int x = Clients.All.add(1,1)` não funciona.</span><span class="sxs-lookup"><span data-stu-id="5983a-251">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="5983a-252">Você pode especificar tipos e matrizes complexos para os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5983a-252">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="5983a-253">O exemplo a seguir passa um tipo complexo para o cliente em um parâmetro de método.</span><span class="sxs-lookup"><span data-stu-id="5983a-253">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="5983a-254">**Código de servidor que chama um método de cliente usando um objeto complexo**</span><span class="sxs-lookup"><span data-stu-id="5983a-254">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

<span data-ttu-id="5983a-255">**Código de servidor que define o objeto complexo**</span><span class="sxs-lookup"><span data-stu-id="5983a-255">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

<span data-ttu-id="5983a-256">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="5983a-256">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="5983a-257">Selecionando quais clientes receberão o RPC</span><span class="sxs-lookup"><span data-stu-id="5983a-257">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="5983a-258">A propriedade clients retorna um objeto [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) que fornece várias opções para especificar quais clientes receberão o RPC:</span><span class="sxs-lookup"><span data-stu-id="5983a-258">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="5983a-259">Todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="5983a-259">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- <span data-ttu-id="5983a-260">Somente o cliente de chamada.</span><span class="sxs-lookup"><span data-stu-id="5983a-260">Only the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="5983a-261">Todos os clientes, exceto o cliente de chamada.</span><span class="sxs-lookup"><span data-stu-id="5983a-261">All clients except the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="5983a-262">Um cliente específico identificado pela ID de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-262">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    <span data-ttu-id="5983a-263">Este exemplo chama `addContosoChatMessageToPage` no cliente de chamada e tem o mesmo efeito que usar `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="5983a-263">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="5983a-264">Todos os clientes conectados, exceto os clientes especificados, identificados pela ID de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-264">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- <span data-ttu-id="5983a-265">Todos os clientes conectados em um grupo especificado.</span><span class="sxs-lookup"><span data-stu-id="5983a-265">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- <span data-ttu-id="5983a-266">Todos os clientes conectados em um grupo especificado, exceto os clientes especificados, identificados pela ID de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-266">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- <span data-ttu-id="5983a-267">Todos os clientes conectados em um grupo especificado, exceto o cliente de chamada.</span><span class="sxs-lookup"><span data-stu-id="5983a-267">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="5983a-268">Nenhuma validação de tempo de compilação para nomes de método</span><span class="sxs-lookup"><span data-stu-id="5983a-268">No compile-time validation for method names</span></span>

<span data-ttu-id="5983a-269">O nome do método que você especifica é interpretado como um objeto dinâmico, o que significa que não há nenhuma validação de tempo de compilação ou IntelliSense para ele.</span><span class="sxs-lookup"><span data-stu-id="5983a-269">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="5983a-270">A expressão é avaliada em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5983a-270">The expression is evaluated at run time.</span></span> <span data-ttu-id="5983a-271">Quando a chamada de método é executada, o Signalr envia o nome do método e os valores de parâmetro para o cliente e, se o cliente tiver um método que corresponda ao nome, esse método será chamado e os valores de parâmetro serão passados para ele.</span><span class="sxs-lookup"><span data-stu-id="5983a-271">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="5983a-272">Se nenhum método correspondente for encontrado no cliente, nenhum erro será gerado.</span><span class="sxs-lookup"><span data-stu-id="5983a-272">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="5983a-273">Para obter informações sobre o formato dos dados que o sinalizador transmite para o cliente em segundo plano quando você chama um método de cliente, consulte [introdução ao signalr](index.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-273">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](index.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="5983a-274">Correspondência de nome de método que não diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="5983a-274">Case-insensitive method name matching</span></span>

<span data-ttu-id="5983a-275">A correspondência de nome de método não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5983a-275">Method name matching is case-insensitive.</span></span> <span data-ttu-id="5983a-276">Por exemplo, `Clients.All.addContosoChatMessageToPage` no servidor será executado `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`ou `addContosoChatMessageToPage` no cliente.</span><span class="sxs-lookup"><span data-stu-id="5983a-276">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="5983a-277">Execução assíncrona</span><span class="sxs-lookup"><span data-stu-id="5983a-277">Asynchronous execution</span></span>

<span data-ttu-id="5983a-278">O método que você chama é executado de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="5983a-278">The method that you call executes asynchronously.</span></span> <span data-ttu-id="5983a-279">Qualquer código que venha após uma chamada de método para um cliente será executado imediatamente sem esperar que o Signalr termine de transmitir dados para os clientes, a menos que você especifique que as linhas subsequentes de código devem aguardar a conclusão do método.</span><span class="sxs-lookup"><span data-stu-id="5983a-279">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="5983a-280">Os exemplos de código a seguir mostram como executar dois métodos de cliente sequencialmente, um usando código que funciona no .NET 4,5 e um usando código que funciona no .NET 4.</span><span class="sxs-lookup"><span data-stu-id="5983a-280">The following code examples show how to execute two client methods sequentially, one using code that works in .NET 4.5, and one using code that works in .NET 4.</span></span>

<span data-ttu-id="5983a-281">**Exemplo do .NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="5983a-281">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

<span data-ttu-id="5983a-282">**Exemplo do .NET 4**</span><span class="sxs-lookup"><span data-stu-id="5983a-282">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

<span data-ttu-id="5983a-283">Se você usar `await` ou `ContinueWith` para aguardar até que um método de cliente seja concluído antes que a próxima linha de código seja executada, isso não significa que os clientes receberão a mensagem antes que a próxima linha de código seja executada.</span><span class="sxs-lookup"><span data-stu-id="5983a-283">If you use `await` or `ContinueWith` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="5983a-284">"Conclusão" de uma chamada de método de cliente significa apenas que o Signalr fez tudo o que é necessário para enviar a mensagem.</span><span class="sxs-lookup"><span data-stu-id="5983a-284">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="5983a-285">Se você precisar de verificação de que os clientes receberam a mensagem, precisará programar esse mecanismo por conta própria.</span><span class="sxs-lookup"><span data-stu-id="5983a-285">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="5983a-286">Por exemplo, você pode codificar um método `MessageReceived` no Hub e, no método `addContosoChatMessageToPage` no cliente, você poderia chamar `MessageReceived` depois de fazer qualquer trabalho que precisar fazer no cliente.</span><span class="sxs-lookup"><span data-stu-id="5983a-286">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="5983a-287">Em `MessageReceived` no Hub, você pode fazer todo o trabalho depende da recepção real do cliente e do processamento da chamada do método original.</span><span class="sxs-lookup"><span data-stu-id="5983a-287">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="5983a-288">Como usar uma variável de cadeia de caracteres como o nome do método</span><span class="sxs-lookup"><span data-stu-id="5983a-288">How to use a string variable as the method name</span></span>

<span data-ttu-id="5983a-289">Se você quiser invocar um método de cliente usando uma variável de cadeia de caracteres como o nome do método, `Clients.All` de conversão (ou `Clients.Others`, `Clients.Caller`, etc.) para `IClientProxy` e, em seguida, chamar [Invoke (MethodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="5983a-289">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="5983a-290">Como gerenciar a associação de grupo da classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-290">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="5983a-291">Os grupos no Signalr fornecem um método para transmitir mensagens para os subconjuntos especificados de clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="5983a-291">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="5983a-292">Um grupo pode ter qualquer número de clientes, e um cliente pode ser um membro de qualquer número de grupos.</span><span class="sxs-lookup"><span data-stu-id="5983a-292">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="5983a-293">Para gerenciar a associação de grupo, use os métodos [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) e [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) fornecidos pela propriedade `Groups` da classe Hub.</span><span class="sxs-lookup"><span data-stu-id="5983a-293">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="5983a-294">O exemplo a seguir mostra os métodos `Groups.Add` e `Groups.Remove` usados em métodos de Hub que são chamados pelo código do cliente, seguidos pelo código de cliente JavaScript que os chama.</span><span class="sxs-lookup"><span data-stu-id="5983a-294">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="5983a-295">**Servidor**</span><span class="sxs-lookup"><span data-stu-id="5983a-295">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

<span data-ttu-id="5983a-296">**Cliente JavaScript usando proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="5983a-296">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

<span data-ttu-id="5983a-297">Você não precisa criar grupos explicitamente.</span><span class="sxs-lookup"><span data-stu-id="5983a-297">You don't have to explicitly create groups.</span></span> <span data-ttu-id="5983a-298">Na verdade, um grupo é criado automaticamente na primeira vez que você especifica seu nome em uma chamada para `Groups.Add`e é excluído quando você remove a última conexão da associação.</span><span class="sxs-lookup"><span data-stu-id="5983a-298">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="5983a-299">Não há API para obter uma lista de associação de grupo ou uma lista de grupos.</span><span class="sxs-lookup"><span data-stu-id="5983a-299">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="5983a-300">O signalr envia mensagens para clientes e grupos com base em um [modelo pub/sub](http://en.wikipedia.org/wiki/Publish/subscribe)e o servidor não mantém listas de grupos ou associações de grupo.</span><span class="sxs-lookup"><span data-stu-id="5983a-300">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="5983a-301">Isso ajuda a maximizar a escalabilidade, porque sempre que você adiciona um nó a um web farm, qualquer Estado que o Signalr mantém deve ser propagado para o novo nó.</span><span class="sxs-lookup"><span data-stu-id="5983a-301">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="5983a-302">Execução assíncrona de métodos Add e remove</span><span class="sxs-lookup"><span data-stu-id="5983a-302">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="5983a-303">Os métodos `Groups.Add` e `Groups.Remove` são executados de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="5983a-303">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="5983a-304">Se você quiser adicionar um cliente a um grupo e enviar imediatamente uma mensagem para o cliente usando o grupo, será necessário certificar-se de que o método de `Groups.Add` seja concluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="5983a-304">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="5983a-305">Os exemplos de código a seguir mostram como fazer isso, um usando código que funciona no .NET 4,5 e outro usando código que funciona no .NET 4</span><span class="sxs-lookup"><span data-stu-id="5983a-305">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4</span></span>

<span data-ttu-id="5983a-306">**Exemplo do .NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="5983a-306">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="5983a-307">**Exemplo do .NET 4**</span><span class="sxs-lookup"><span data-stu-id="5983a-307">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="5983a-308">Persistência de associação de grupo</span><span class="sxs-lookup"><span data-stu-id="5983a-308">Group membership persistence</span></span>

<span data-ttu-id="5983a-309">O signalr rastreia conexões, e não os usuários, portanto, se você quiser que um usuário esteja no mesmo grupo sempre que o usuário estabelecer uma conexão, você precisará chamar `Groups.Add` toda vez que o usuário estabelecer uma nova conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-309">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="5983a-310">Após uma perda temporária de conectividade, às vezes o Signalr pode restaurar a conexão automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5983a-310">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="5983a-311">Nesse caso, o Signalr está restaurando a mesma conexão, não estabelecendo uma nova conexão e, portanto, a associação de grupo do cliente é restaurada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5983a-311">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="5983a-312">Isso é possível mesmo quando a interrupção temporária é o resultado de uma reinicialização ou falha do servidor, pois o estado da conexão para cada cliente, incluindo associações de grupo, é feito de forma redonda para o cliente.</span><span class="sxs-lookup"><span data-stu-id="5983a-312">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="5983a-313">Se um servidor ficar inativo e for substituído por um novo servidor antes que a conexão expire, um cliente poderá se reconectar automaticamente ao novo servidor e inscrever-se novamente em grupos dos quais ele é membro.</span><span class="sxs-lookup"><span data-stu-id="5983a-313">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="5983a-314">Quando uma conexão não pode ser restaurada automaticamente após uma perda de conectividade, ou quando a conexão atinge o tempo limite ou quando o cliente se desconecta (por exemplo, quando um navegador navega para uma nova página), as associações de grupo são perdidas.</span><span class="sxs-lookup"><span data-stu-id="5983a-314">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="5983a-315">Na próxima vez que o usuário se conectar, será uma nova conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-315">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="5983a-316">Para manter as associações de grupo quando o mesmo usuário estabelece uma nova conexão, seu aplicativo precisa rastrear as associações entre usuários e grupos e restaurar as associações de grupo cada vez que um usuário estabelece uma nova conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-316">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="5983a-317">Para obter mais informações sobre conexões e reconexões, consulte [como lidar com eventos de tempo de vida de conexão na classe Hub](#connectionlifetime) mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="5983a-317">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="5983a-318">Grupos de usuário único</span><span class="sxs-lookup"><span data-stu-id="5983a-318">Single-user groups</span></span>

<span data-ttu-id="5983a-319">Os aplicativos que usam o Signalr normalmente precisam manter o controle das associações entre usuários e conexões para saber qual usuário enviou uma mensagem e quais usuários devem receber uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="5983a-319">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="5983a-320">Os grupos são usados em um dos dois padrões comumente usados para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="5983a-320">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="5983a-321">Grupos de usuário único.</span><span class="sxs-lookup"><span data-stu-id="5983a-321">Single-user groups.</span></span>

    <span data-ttu-id="5983a-322">Você pode especificar o nome de usuário como o nome do grupo e adicionar a ID de conexão atual ao grupo toda vez que o usuário se conectar ou reconectar.</span><span class="sxs-lookup"><span data-stu-id="5983a-322">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="5983a-323">Para enviar mensagens ao usuário que você envia para o grupo.</span><span class="sxs-lookup"><span data-stu-id="5983a-323">To send messages to the user you send to the group.</span></span> <span data-ttu-id="5983a-324">Uma desvantagem desse método é que o grupo não fornece uma maneira de descobrir se o usuário está online ou offline.</span><span class="sxs-lookup"><span data-stu-id="5983a-324">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="5983a-325">Rastreie associações entre nomes de usuário e IDs de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-325">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="5983a-326">Você pode armazenar uma associação entre cada nome de usuário e uma ou mais identificações de conexão em um dicionário ou banco de dados, e atualizar as informações armazenadas cada vez que o usuário se conectar ou se desconectar.</span><span class="sxs-lookup"><span data-stu-id="5983a-326">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="5983a-327">Para enviar mensagens ao usuário, você especifica as IDs de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-327">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="5983a-328">Uma desvantagem desse método é que ela ocupa mais memória.</span><span class="sxs-lookup"><span data-stu-id="5983a-328">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="5983a-329">Como tratar eventos de tempo de vida da conexão na classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-329">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="5983a-330">Os motivos típicos para lidar com eventos de tempo de vida de conexão são controlar se um usuário está conectado ou não, e controlar a associação entre nomes de usuário e IDs de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-330">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="5983a-331">Para executar seu próprio código quando os clientes se conectam ou desconectam, substitua os métodos virtuais `OnConnected`, `OnDisconnected`e `OnReconnected` da classe Hub, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5983a-331">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="5983a-332">Quando onconnected, OnDisconnect e OnReconnected são chamados</span><span class="sxs-lookup"><span data-stu-id="5983a-332">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="5983a-333">Cada vez que um navegador navega para uma nova página, uma nova conexão precisa ser estabelecida, o que significa que o Signalr executará o método `OnDisconnected` seguido pelo método `OnConnected`.</span><span class="sxs-lookup"><span data-stu-id="5983a-333">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="5983a-334">O signalr sempre cria uma nova ID de conexão quando uma nova conexão é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5983a-334">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="5983a-335">O método `OnReconnected` é chamado quando houve uma interrupção temporária na conectividade com a qual o Signalr pode se recuperar automaticamente, como quando um cabo é temporariamente desconectado e reconectado antes que a conexão expire. O método `OnDisconnected` é chamado quando o cliente é desconectado e o Signalr não pode se reconectar automaticamente, como quando um navegador navega para uma nova página.</span><span class="sxs-lookup"><span data-stu-id="5983a-335">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="5983a-336">Portanto, uma possível sequência de eventos para um determinado cliente é `OnConnected`, `OnReconnected`, `OnDisconnected`; ou `OnConnected`, `OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="5983a-336">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="5983a-337">Você não verá a sequência `OnConnected`, `OnDisconnected`, `OnReconnected` para uma determinada conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-337">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="5983a-338">O método `OnDisconnected` não é chamado em alguns cenários, como quando um servidor fica inoperante ou o domínio do aplicativo é reciclado.</span><span class="sxs-lookup"><span data-stu-id="5983a-338">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="5983a-339">Quando outro servidor entra na linha ou o domínio do aplicativo conclui sua reciclagem, alguns clientes podem ser capazes de se reconectar e acionar o evento de `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="5983a-339">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="5983a-340">Para obter mais informações, consulte [noções básicas e manipulação de eventos de tempo de vida de conexão no signalr](index.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-340">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="5983a-341">Estado do chamador não preenchido</span><span class="sxs-lookup"><span data-stu-id="5983a-341">Caller state not populated</span></span>

<span data-ttu-id="5983a-342">Os métodos do manipulador de eventos de tempo de vida da conexão são chamados do servidor, o que significa que qualquer estado colocado no objeto `state` no cliente não será preenchido na propriedade `Caller` no servidor.</span><span class="sxs-lookup"><span data-stu-id="5983a-342">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="5983a-343">Para obter informações sobre o objeto `state` e a propriedade `Caller`, consulte [como passar o estado entre clientes e a classe Hub](#passstate) mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="5983a-343">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="5983a-344">Como obter informações sobre o cliente a partir da propriedade Context</span><span class="sxs-lookup"><span data-stu-id="5983a-344">How to get information about the client from the Context property</span></span>

<span data-ttu-id="5983a-345">Para obter informações sobre o cliente, use a propriedade `Context` da classe Hub.</span><span class="sxs-lookup"><span data-stu-id="5983a-345">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="5983a-346">A propriedade `Context` retorna um objeto [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) que fornece acesso às seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="5983a-346">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="5983a-347">A ID de conexão do cliente de chamada.</span><span class="sxs-lookup"><span data-stu-id="5983a-347">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    <span data-ttu-id="5983a-348">A ID de conexão é um GUID atribuído pelo Signalr (você não pode especificar o valor em seu próprio código).</span><span class="sxs-lookup"><span data-stu-id="5983a-348">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="5983a-349">Há uma ID de conexão para cada conexão e a mesma ID de conexão é usada por todos os hubs se você tiver vários hubs em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5983a-349">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="5983a-350">Dados de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="5983a-350">HTTP header data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    <span data-ttu-id="5983a-351">Você também pode obter cabeçalhos HTTP de `Context.Headers`.</span><span class="sxs-lookup"><span data-stu-id="5983a-351">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="5983a-352">O motivo para várias referências para a mesma coisa é que `Context.Headers` foi criado primeiro, a propriedade `Context.Request` foi adicionada mais tarde e `Context.Headers` foi retida para compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="5983a-352">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="5983a-353">Dados de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="5983a-353">Query string data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    <span data-ttu-id="5983a-354">Você também pode obter dados de cadeia de caracteres de consulta de `Context.QueryString`.</span><span class="sxs-lookup"><span data-stu-id="5983a-354">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="5983a-355">A cadeia de caracteres de consulta que você obtém nessa propriedade é aquela que foi usada com a solicitação HTTP que estabeleceu a conexão do Signalr.</span><span class="sxs-lookup"><span data-stu-id="5983a-355">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="5983a-356">Você pode adicionar parâmetros de cadeia de caracteres de consulta no cliente Configurando a conexão, que é uma maneira conveniente de passar dados sobre o cliente do cliente para o servidor.</span><span class="sxs-lookup"><span data-stu-id="5983a-356">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="5983a-357">O exemplo a seguir mostra uma maneira de adicionar uma cadeia de caracteres de consulta em um cliente JavaScript quando você usa o proxy gerado.</span><span class="sxs-lookup"><span data-stu-id="5983a-357">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    <span data-ttu-id="5983a-358">Para obter mais informações sobre como definir parâmetros de cadeia de caracteres de consulta, consulte os guias de API para os clientes [JavaScript](index.md) e [.net](index.md) .</span><span class="sxs-lookup"><span data-stu-id="5983a-358">For more information about setting query string parameters, see the API guides for the [JavaScript](index.md) and [.NET](index.md) clients.</span></span>

    <span data-ttu-id="5983a-359">Você pode encontrar o método de transporte usado para a conexão nos dados da cadeia de caracteres de consulta, juntamente com alguns outros valores usados internamente pelo Signalr:</span><span class="sxs-lookup"><span data-stu-id="5983a-359">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    <span data-ttu-id="5983a-360">O valor de `transportMethod` será "WebSockets", "serverSentEvents", "foreverFrame" ou "longPolling".</span><span class="sxs-lookup"><span data-stu-id="5983a-360">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="5983a-361">Observe que, se você marcar esse valor no método do manipulador de eventos `OnConnected`, em alguns cenários você poderá obter inicialmente um valor de transporte que não seja o método de transporte negociado final para a conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-361">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="5983a-362">Nesse caso, o método lançará uma exceção e será chamado novamente mais tarde quando o método de transporte final for estabelecido.</span><span class="sxs-lookup"><span data-stu-id="5983a-362">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="5983a-363">Arar.</span><span class="sxs-lookup"><span data-stu-id="5983a-363">Cookies.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="5983a-364">Você também pode obter cookies de `Context.RequestCookies`.</span><span class="sxs-lookup"><span data-stu-id="5983a-364">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="5983a-365">Informação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5983a-365">User information.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- <span data-ttu-id="5983a-366">O objeto HttpContext para a solicitação:</span><span class="sxs-lookup"><span data-stu-id="5983a-366">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    <span data-ttu-id="5983a-367">Use esse método em vez de obter `HttpContext.Current` para obter o objeto `HttpContext` para a conexão do Signalr.</span><span class="sxs-lookup"><span data-stu-id="5983a-367">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="5983a-368">Como passar o estado entre clientes e a classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-368">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="5983a-369">O proxy do cliente fornece um objeto `state` no qual você pode armazenar os dados que deseja transmitir para o servidor com cada chamada de método.</span><span class="sxs-lookup"><span data-stu-id="5983a-369">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="5983a-370">No servidor, você pode acessar esses dados na propriedade `Clients.Caller` em métodos de Hub que são chamados por clientes.</span><span class="sxs-lookup"><span data-stu-id="5983a-370">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="5983a-371">A propriedade `Clients.Caller` não é preenchida para os métodos do manipulador de eventos de tempo de vida da conexão `OnConnected`, `OnDisconnected`e `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="5983a-371">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="5983a-372">Criar ou atualizar dados no objeto `state` e a propriedade `Clients.Caller` funciona em ambas as direções.</span><span class="sxs-lookup"><span data-stu-id="5983a-372">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="5983a-373">Você pode atualizar valores no servidor e eles são passados de volta para o cliente.</span><span class="sxs-lookup"><span data-stu-id="5983a-373">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="5983a-374">O exemplo a seguir mostra o código de cliente JavaScript que armazena o estado de transmissão para o servidor com cada chamada de método.</span><span class="sxs-lookup"><span data-stu-id="5983a-374">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

<span data-ttu-id="5983a-375">O exemplo a seguir mostra o código equivalente em um cliente .NET.</span><span class="sxs-lookup"><span data-stu-id="5983a-375">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

<span data-ttu-id="5983a-376">Na sua classe de Hub, você pode acessar esses dados na propriedade `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="5983a-376">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="5983a-377">O exemplo a seguir mostra o código que recupera o estado referido no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="5983a-377">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="5983a-378">Esse mecanismo para o estado persistente não é destinado a grandes quantidades de dados, já que tudo que você coloca na propriedade `state` ou `Clients.Caller` é feito em ida e volta com cada invocação de método.</span><span class="sxs-lookup"><span data-stu-id="5983a-378">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="5983a-379">É útil para itens menores, como nomes de usuário ou contadores.</span><span class="sxs-lookup"><span data-stu-id="5983a-379">It's useful for smaller items such as user names or counters.</span></span>

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="5983a-380">Como tratar erros na classe Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-380">How to handle errors in the Hub class</span></span>

<span data-ttu-id="5983a-381">Para lidar com erros que ocorrem em seus métodos de classe de Hub, use um ou os dois métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5983a-381">To handle errors that occur in your Hub class methods, use one or both of the following methods:</span></span>

- <span data-ttu-id="5983a-382">Coloque o código do método em blocos try-catch e registre o objeto de exceção.</span><span class="sxs-lookup"><span data-stu-id="5983a-382">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="5983a-383">Para fins de depuração, você pode enviar a exceção para o cliente, mas por motivos de segurança não é recomendável enviar informações detalhadas aos clientes em produção.</span><span class="sxs-lookup"><span data-stu-id="5983a-383">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="5983a-384">Crie um módulo de pipeline de hubs que manipula o método [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="5983a-384">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="5983a-385">O exemplo a seguir mostra um módulo de pipeline que registra erros, seguido pelo código em global. asax que injeta o módulo no pipeline de hubs.</span><span class="sxs-lookup"><span data-stu-id="5983a-385">The following example shows a pipeline module that logs errors, followed by code in Global.asax that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

<span data-ttu-id="5983a-386">Para obter mais informações sobre módulos de pipeline de Hub, consulte [como personalizar o pipeline de hubs](#hubpipeline) mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="5983a-386">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="5983a-387">Como habilitar o rastreamento</span><span class="sxs-lookup"><span data-stu-id="5983a-387">How to enable tracing</span></span>

<span data-ttu-id="5983a-388">Para habilitar o rastreamento do lado do servidor, adicione um elemento System. Diagnostics ao seu arquivo Web. config, conforme mostrado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="5983a-388">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

<span data-ttu-id="5983a-389">Ao executar o aplicativo no Visual Studio, você pode exibir os logs na janela **saída** .</span><span class="sxs-lookup"><span data-stu-id="5983a-389">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="5983a-390">Como chamar métodos de cliente e gerenciar grupos de fora da classe de Hub</span><span class="sxs-lookup"><span data-stu-id="5983a-390">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="5983a-391">Para chamar métodos de cliente de uma classe diferente da classe de Hub, obtenha uma referência ao objeto de contexto do Signalr para o Hub e use-o para chamar métodos no cliente ou gerenciar grupos.</span><span class="sxs-lookup"><span data-stu-id="5983a-391">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="5983a-392">O exemplo a seguir `StockTicker` classe obtém o objeto de contexto, armazena-o em uma instância da classe, armazena a instância de classe em uma propriedade estática e usa o contexto da instância da classe singleton para chamar o método `updateStockPrice` em clientes que estão conectados a um Hub chamado `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="5983a-392">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

<span data-ttu-id="5983a-393">Se você precisar usar o contexto várias vezes em um objeto de vida útil longa, obtenha a referência uma vez e salve-a em vez de obtê-la novamente a cada vez.</span><span class="sxs-lookup"><span data-stu-id="5983a-393">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="5983a-394">Obter o contexto quando garante que o Signalr envie mensagens para clientes na mesma sequência em que os métodos de Hub fazem invocações de método de cliente.</span><span class="sxs-lookup"><span data-stu-id="5983a-394">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="5983a-395">Para obter um tutorial que mostra como usar o contexto do Signalr para um Hub, consulte [transmissão de servidor com o signalr ASP.net](index.md).</span><span class="sxs-lookup"><span data-stu-id="5983a-395">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](index.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="5983a-396">Chamando métodos de cliente</span><span class="sxs-lookup"><span data-stu-id="5983a-396">Calling client methods</span></span>

<span data-ttu-id="5983a-397">Você pode especificar quais clientes receberão o RPC, mas tem menos opções do que quando você chama de uma classe de Hub.</span><span class="sxs-lookup"><span data-stu-id="5983a-397">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="5983a-398">O motivo disso é que o contexto não está associado a uma chamada específica de um cliente, portanto, todos os métodos que exigem o conhecimento da ID de conexão atual, como `Clients.Others`ou `Clients.Caller`ou `Clients.OthersInGroup`, não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="5983a-398">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="5983a-399">As seguintes opções estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="5983a-399">The following options are available:</span></span>

- <span data-ttu-id="5983a-400">Todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="5983a-400">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- <span data-ttu-id="5983a-401">Um cliente específico identificado pela ID de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-401">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- <span data-ttu-id="5983a-402">Todos os clientes conectados, exceto os clientes especificados, identificados pela ID de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-402">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- <span data-ttu-id="5983a-403">Todos os clientes conectados em um grupo especificado.</span><span class="sxs-lookup"><span data-stu-id="5983a-403">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- <span data-ttu-id="5983a-404">Todos os clientes conectados em um grupo especificado, exceto os clientes especificados, identificados pela ID de conexão.</span><span class="sxs-lookup"><span data-stu-id="5983a-404">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

<span data-ttu-id="5983a-405">Se você estiver chamando a sua classe sem hub a partir de métodos em sua classe de Hub, poderá passar a ID de conexão atual e usá-la com `Clients.Client`, `Clients.AllExcept`ou `Clients.Group` para simular `Clients.Caller`, `Clients.Others`ou `Clients.OthersInGroup`.</span><span class="sxs-lookup"><span data-stu-id="5983a-405">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="5983a-406">No exemplo a seguir, a classe `MoveShapeHub` passa a ID de conexão para a classe `Broadcaster` para que a classe `Broadcaster` possa simular `Clients.Others`.</span><span class="sxs-lookup"><span data-stu-id="5983a-406">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="5983a-407">Gerenciando a associação de grupo</span><span class="sxs-lookup"><span data-stu-id="5983a-407">Managing group membership</span></span>

<span data-ttu-id="5983a-408">Para gerenciar grupos, você tem as mesmas opções que você faz em uma classe de Hub.</span><span class="sxs-lookup"><span data-stu-id="5983a-408">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="5983a-409">Adicionar um cliente a um grupo</span><span class="sxs-lookup"><span data-stu-id="5983a-409">Add a client to a group</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- <span data-ttu-id="5983a-410">Remover um cliente de um grupo</span><span class="sxs-lookup"><span data-stu-id="5983a-410">Remove a client from a group</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="5983a-411">Como personalizar o pipeline de hubs</span><span class="sxs-lookup"><span data-stu-id="5983a-411">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="5983a-412">O signalr permite injetar seu próprio código no pipeline do Hub.</span><span class="sxs-lookup"><span data-stu-id="5983a-412">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="5983a-413">O exemplo a seguir mostra um módulo de pipeline de Hub personalizado que registra cada chamada de método de entrada recebida do cliente e chamada de método de saída invocada no cliente:</span><span class="sxs-lookup"><span data-stu-id="5983a-413">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

<span data-ttu-id="5983a-414">O código a seguir no arquivo *global. asax* registra o módulo a ser executado no pipeline de Hub:</span><span class="sxs-lookup"><span data-stu-id="5983a-414">The following code in the *Global.asax* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

<span data-ttu-id="5983a-415">Há muitos métodos diferentes que podem ser substituídos.</span><span class="sxs-lookup"><span data-stu-id="5983a-415">There are many different methods that you can override.</span></span> <span data-ttu-id="5983a-416">Para obter uma lista completa, consulte [métodos HubPipelineModule](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="5983a-416">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
