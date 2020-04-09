---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR Hubs API Guide - .NET Client (C#) | Microsoft Docs
author: bradygaster
description: Este documento fornece uma introdução ao uso da API hubs para clientes SignalR versão 2 em clientes .NET, como Windows Store (WinRT), WPF, Silverlight e contras...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676331"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="84260-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span><span class="sxs-lookup"><span data-stu-id="84260-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="84260-104">Este documento fornece uma introdução ao uso da API hubs para clientes SignalR versão 2 em clientes .NET, como Windows Store (WinRT), WPF, Silverlight e aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="84260-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="84260-105">A API SignalR Hubs permite que você faça chamadas de procedimento remoto (RPCs) de um servidor para clientes conectados e de clientes para o servidor.</span><span class="sxs-lookup"><span data-stu-id="84260-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="84260-106">No código do servidor, você define métodos que podem ser chamados pelos clientes e você chama métodos que são executados no cliente.</span><span class="sxs-lookup"><span data-stu-id="84260-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="84260-107">No código do cliente, você define métodos que podem ser chamados do servidor e você chama métodos que são executados no servidor.</span><span class="sxs-lookup"><span data-stu-id="84260-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="84260-108">O SignalR cuida de todo o encanamento cliente-servidor para você.</span><span class="sxs-lookup"><span data-stu-id="84260-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="84260-109">SignalR também oferece uma API de nível inferior chamada Conexões Persistentes.</span><span class="sxs-lookup"><span data-stu-id="84260-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="84260-110">Para uma introdução ao SignalR, Hubs e Persistent Connections, ou para um tutorial que mostra como construir um aplicativo SignalR completo, consulte [SignalR - Getting Started](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="84260-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="84260-111">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="84260-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="84260-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="84260-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="84260-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="84260-113">.NET 4.5</span></span>
> - <span data-ttu-id="84260-114">SignalR versão 2</span><span class="sxs-lookup"><span data-stu-id="84260-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="84260-115">Versões anteriores deste tópico</span><span class="sxs-lookup"><span data-stu-id="84260-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="84260-116">Para obter informações sobre versões anteriores do SignalR, consulte [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="84260-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="84260-117">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="84260-117">Questions and comments</span></span>
>
> <span data-ttu-id="84260-118">Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="84260-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="84260-119">Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="84260-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="84260-120">Visão geral</span><span class="sxs-lookup"><span data-stu-id="84260-120">Overview</span></span>

<span data-ttu-id="84260-121">Este documento contém as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="84260-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="84260-122">Configuração do cliente</span><span class="sxs-lookup"><span data-stu-id="84260-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="84260-123">Como estabelecer uma conexão</span><span class="sxs-lookup"><span data-stu-id="84260-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="84260-124">Conexões entre domínios de clientes Silverlight</span><span class="sxs-lookup"><span data-stu-id="84260-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="84260-125">Como configurar a conexão</span><span class="sxs-lookup"><span data-stu-id="84260-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="84260-126">Como definir o número máximo de conexões simultâneas em clientes WPF</span><span class="sxs-lookup"><span data-stu-id="84260-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="84260-127">Como especificar parâmetros de seqüência de consultas</span><span class="sxs-lookup"><span data-stu-id="84260-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="84260-128">Como especificar o método de transporte</span><span class="sxs-lookup"><span data-stu-id="84260-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="84260-129">Como especificar cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="84260-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="84260-130">Como especificar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="84260-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="84260-131">Como criar o proxy do Hub</span><span class="sxs-lookup"><span data-stu-id="84260-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="84260-132">Como definir métodos no cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="84260-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="84260-133">Métodos sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="84260-134">Métodos com parâmetros, especificando tipos de parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="84260-135">Métodos com parâmetros, especificando objetos dinâmicos para os parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="84260-136">Como remover um manipulador</span><span class="sxs-lookup"><span data-stu-id="84260-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="84260-137">Como chamar métodos de servidor do cliente</span><span class="sxs-lookup"><span data-stu-id="84260-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="84260-138">Como lidar com eventos de vida de conexão</span><span class="sxs-lookup"><span data-stu-id="84260-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="84260-139">Como lidar com erros</span><span class="sxs-lookup"><span data-stu-id="84260-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="84260-140">Como habilitar o registro do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="84260-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="84260-141">Amostras de código de aplicativo WPF, Silverlight e console para métodos de cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="84260-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="84260-142">Para obter uma amostra de projetos de clientes .NET, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="84260-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="84260-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) em GitHub.com (WinRT, Silverlight, exemplos de aplicativos de console).</span><span class="sxs-lookup"><span data-stu-id="84260-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="84260-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (exemplo WPF).</span><span class="sxs-lookup"><span data-stu-id="84260-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="84260-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (exemplo do aplicativo console).</span><span class="sxs-lookup"><span data-stu-id="84260-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="84260-146">Para obter a documentação sobre como programar os clientes servidor ou JavaScript, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="84260-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="84260-147">SignalR Hubs Guia de API - Servidor</span><span class="sxs-lookup"><span data-stu-id="84260-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="84260-148">SignalR Hubs API Guide - JavaScript Client</span><span class="sxs-lookup"><span data-stu-id="84260-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="84260-149">Os links para tópicos de referência da API são para a versão .NET 4.5 da API.</span><span class="sxs-lookup"><span data-stu-id="84260-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="84260-150">Se você estiver usando .NET 4, consulte [a versão .NET 4 dos tópicos da API](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="84260-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="84260-151">Configuração do cliente</span><span class="sxs-lookup"><span data-stu-id="84260-151">Client setup</span></span>

<span data-ttu-id="84260-152">Instale o pacote [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet (não o pacote [Microsoft.AspNet.SignalR).](http://nuget.org/packages/microsoft.aspnet.signalr)</span><span class="sxs-lookup"><span data-stu-id="84260-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="84260-153">Este pacote suporta clientes WinRT, Silverlight, WPF, console e Windows Phone, tanto para clientes .NET 4 quanto .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="84260-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="84260-154">Se a versão do SignalR que você tem no cliente for diferente da versão que você tem no servidor, o SignalR muitas vezes é capaz de se adaptar à diferença.</span><span class="sxs-lookup"><span data-stu-id="84260-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="84260-155">Por exemplo, um servidor executando o SignalR versão 2 suportará clientes que tenham 1.1.x instalado, bem como clientes que tenham a versão 2 instalada.</span><span class="sxs-lookup"><span data-stu-id="84260-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="84260-156">Se a diferença entre a versão no servidor e a versão no cliente for muito grande, ou `InvalidOperationException` se o cliente for mais recente que o servidor, o SignalR abre uma exceção quando o cliente tenta estabelecer uma conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="84260-157">A mensagem`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`de erro é " ".</span><span class="sxs-lookup"><span data-stu-id="84260-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="84260-158">Como estabelecer uma conexão</span><span class="sxs-lookup"><span data-stu-id="84260-158">How to establish a connection</span></span>

<span data-ttu-id="84260-159">Antes de estabelecer uma conexão, `HubConnection` você tem que criar um objeto e criar um proxy.</span><span class="sxs-lookup"><span data-stu-id="84260-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="84260-160">Para estabelecer a conexão, chame o `Start` método no `HubConnection` objeto.</span><span class="sxs-lookup"><span data-stu-id="84260-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="84260-161">Para clientes JavaScript, você tem que registrar `Start` pelo menos um manipulador de eventos antes de chamar o método para estabelecer a conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="84260-162">Isso não é necessário para clientes .NET.</span><span class="sxs-lookup"><span data-stu-id="84260-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="84260-163">Para clientes JavaScript, o código proxy gerado cria automaticamente proxies para todos os Hubs existentes no servidor, e registrar um manipulador é como você indica quais Hubs seu cliente pretende usar.</span><span class="sxs-lookup"><span data-stu-id="84260-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="84260-164">Mas para um cliente .NET você cria proxies hub manualmente, então o SignalR assume que você estará usando qualquer Hub para o que você criar um proxy.</span><span class="sxs-lookup"><span data-stu-id="84260-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="84260-165">O código de exemplo usa a URL padrão "/signalr" para se conectar ao serviço SignalR.</span><span class="sxs-lookup"><span data-stu-id="84260-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="84260-166">Para obter informações sobre como especificar uma URL base diferente, consulte [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="84260-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="84260-167">O `Start` método é executado de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="84260-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="84260-168">Para garantir que as linhas de código subseqüentes não executem até que a conexão seja estabelecida, use `await` em um método assíncrono de ASP.NET 4,5 ou `.Wait()` em um método síncrono.</span><span class="sxs-lookup"><span data-stu-id="84260-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="84260-169">Não use `.Wait()` em um cliente WinRT.</span><span class="sxs-lookup"><span data-stu-id="84260-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="84260-170">Conexões entre domínios de clientes Silverlight</span><span class="sxs-lookup"><span data-stu-id="84260-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="84260-171">Para obter informações sobre como habilitar conexões entre domínios de clientes Silverlight, consulte [Tornando um serviço disponível através dos limites do domínio](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="84260-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="84260-172">Como configurar a conexão</span><span class="sxs-lookup"><span data-stu-id="84260-172">How to configure the connection</span></span>

<span data-ttu-id="84260-173">Antes de estabelecer uma conexão, você pode especificar qualquer uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="84260-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="84260-174">Limite de conexões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="84260-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="84260-175">Parâmetros da seqüência de consultas.</span><span class="sxs-lookup"><span data-stu-id="84260-175">Query string parameters.</span></span>
- <span data-ttu-id="84260-176">O método de transporte.</span><span class="sxs-lookup"><span data-stu-id="84260-176">The transport method.</span></span>
- <span data-ttu-id="84260-177">Cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="84260-177">HTTP headers.</span></span>
- <span data-ttu-id="84260-178">Certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="84260-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="84260-179">Como definir o número máximo de conexões simultâneas em clientes WPF</span><span class="sxs-lookup"><span data-stu-id="84260-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="84260-180">Em clientes WPF, você pode ter que aumentar o número máximo de conexões simultâneas do seu valor padrão de 2.</span><span class="sxs-lookup"><span data-stu-id="84260-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="84260-181">O valor recomendado é 10.</span><span class="sxs-lookup"><span data-stu-id="84260-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="84260-182">Para obter mais informações, consulte [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="84260-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="84260-183">Como especificar parâmetros de seqüência de consultas</span><span class="sxs-lookup"><span data-stu-id="84260-183">How to specify query string parameters</span></span>

<span data-ttu-id="84260-184">Se você quiser enviar dados para o servidor quando o cliente se conectar, você pode adicionar parâmetros de seqüência de consulta ao objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="84260-185">O exemplo a seguir mostra como definir um parâmetro de seqüência de consultas no código do cliente.</span><span class="sxs-lookup"><span data-stu-id="84260-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="84260-186">O exemplo a seguir mostra como ler um parâmetro de seqüência de consultas no código do servidor.</span><span class="sxs-lookup"><span data-stu-id="84260-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="84260-187">Como especificar o método de transporte</span><span class="sxs-lookup"><span data-stu-id="84260-187">How to specify the transport method</span></span>

<span data-ttu-id="84260-188">Como parte do processo de conexão, um cliente SignalR normalmente negocia com o servidor para determinar o melhor transporte que é suportado tanto pelo servidor quanto pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="84260-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="84260-189">Se você já sabe qual transporte deseja usar, você pode contornar esse processo de negociação.</span><span class="sxs-lookup"><span data-stu-id="84260-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="84260-190">Para especificar o método de transporte, passe em um objeto de transporte para o método Iniciar.</span><span class="sxs-lookup"><span data-stu-id="84260-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="84260-191">O exemplo a seguir mostra como especificar o método de transporte no código do cliente.</span><span class="sxs-lookup"><span data-stu-id="84260-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="84260-192">O espaço de nome [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) inclui as seguintes classes que você pode usar para especificar o transporte.</span><span class="sxs-lookup"><span data-stu-id="84260-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="84260-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="84260-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="84260-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="84260-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="84260-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Disponível apenas quando o servidor e o cliente usam .NET 4.5.)</span><span class="sxs-lookup"><span data-stu-id="84260-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="84260-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (escolhe automaticamente o melhor transporte que é suportado pelo cliente e pelo servidor.</span><span class="sxs-lookup"><span data-stu-id="84260-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="84260-197">Este é o transporte padrão.</span><span class="sxs-lookup"><span data-stu-id="84260-197">This is the default transport.</span></span> <span data-ttu-id="84260-198">Passar isso para `Start` o método tem o mesmo efeito de não passar em nada.)</span><span class="sxs-lookup"><span data-stu-id="84260-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="84260-199">O transporte ForeverFrame não está incluído nesta lista porque é usado apenas por navegadores.</span><span class="sxs-lookup"><span data-stu-id="84260-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="84260-200">Para obter informações sobre como verificar o método de transporte no código do servidor, consulte [ASP.NET SignalR Hubs API Guide - Server - Como obter informações sobre o cliente a partir da propriedade Context](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="84260-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="84260-201">Para obter mais informações sobre transportes e recuos, consulte [Introdução ao SignalR - Transportes e Recuos](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="84260-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="84260-202">Como especificar cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="84260-202">How to specify HTTP headers</span></span>

<span data-ttu-id="84260-203">Para definir cabeçalhos `Headers` HTTP, use a propriedade no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="84260-204">O exemplo a seguir mostra como adicionar um cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="84260-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="84260-205">Como especificar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="84260-205">How to specify client certificates</span></span>

<span data-ttu-id="84260-206">Para adicionar certificados de `AddClientCertificate` cliente, use o método no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="84260-207">Como criar o proxy do Hub</span><span class="sxs-lookup"><span data-stu-id="84260-207">How to create the Hub proxy</span></span>

<span data-ttu-id="84260-208">Para definir métodos no cliente que um Hub pode ligar do servidor e invocar métodos em um Hub `CreateHubProxy` no servidor, crie um proxy para o Hub, chamando o objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="84260-209">A seqüência `CreateHubProxy` de seqüência para a qual você passa `HubName` é o nome da sua classe Hub ou o nome especificado pelo atributo se um foi usado no servidor.</span><span class="sxs-lookup"><span data-stu-id="84260-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="84260-210">A correspondência de nome não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="84260-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="84260-211">**Classe hub no servidor**</span><span class="sxs-lookup"><span data-stu-id="84260-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="84260-212">**Crie proxy de cliente para a classe Hub**</span><span class="sxs-lookup"><span data-stu-id="84260-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="84260-213">Se você decorar sua classe `HubName` Hub com um atributo, use esse nome.</span><span class="sxs-lookup"><span data-stu-id="84260-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="84260-214">**Classe hub no servidor**</span><span class="sxs-lookup"><span data-stu-id="84260-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="84260-215">**Crie proxy de cliente para a classe Hub**</span><span class="sxs-lookup"><span data-stu-id="84260-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="84260-216">Se você `HubConnection.CreateHubProxy` ligar várias `hubName`vezes com o `IHubProxy` mesmo, você terá o mesmo objeto armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="84260-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="84260-217">Como definir métodos no cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="84260-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="84260-218">Para definir um método que o servidor pode `On` chamar, use o método do proxy para registrar um manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="84260-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="84260-219">A correspondência do nome do método é insensível ao caso.</span><span class="sxs-lookup"><span data-stu-id="84260-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="84260-220">Por `Clients.All.UpdateStockPrice` exemplo, no servidor `updateStockPrice` `updatestockprice`executará `UpdateStockPrice` , ou no cliente.</span><span class="sxs-lookup"><span data-stu-id="84260-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="84260-221">Diferentes plataformas cliente têm requisitos diferentes para como você escreve código de método para atualizar a ui.</span><span class="sxs-lookup"><span data-stu-id="84260-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="84260-222">Os exemplos mostrados são para clientes WinRT (Windows Store .NET).</span><span class="sxs-lookup"><span data-stu-id="84260-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="84260-223">Exemplos de aplicativos WPF, Silverlight e console são fornecidos em [uma seção separada mais tarde neste tópico](#wpfsl).</span><span class="sxs-lookup"><span data-stu-id="84260-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="84260-224">Métodos sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-224">Methods without parameters</span></span>

<span data-ttu-id="84260-225">Se o método que você está manipulando não tiver parâmetros, use a sobrecarga não genérica do `On` método:</span><span class="sxs-lookup"><span data-stu-id="84260-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="84260-226">**Método cliente de chamada de código de servidor sem parâmetros**</span><span class="sxs-lookup"><span data-stu-id="84260-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="84260-227">**Código do Cliente WinRT para método chamado de servidor sem[parâmetros (veja exemplos WPF e Silverlight mais tarde neste tópico)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="84260-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="84260-228">Métodos com parâmetros, especificando os tipos de parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="84260-229">Se o método que você está manipulando tiver parâmetros, especifique os tipos dos parâmetros como os tipos genéricos do `On` método.</span><span class="sxs-lookup"><span data-stu-id="84260-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="84260-230">Existem sobrecargas genéricas do `On` método para permitir que você especifique até 8 parâmetros (4 no Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="84260-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="84260-231">No exemplo a seguir, um parâmetro `UpdateStockPrice` é enviado para o método.</span><span class="sxs-lookup"><span data-stu-id="84260-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="84260-232">**Método de chamada de código do servidor com um parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="84260-233">**A classe Stock usada para o parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="84260-234">**Código do Cliente WinRT para um método chamado de servidor com um parâmetro[(veja exemplos WPF e Silverlight mais tarde neste tópico)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="84260-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="84260-235">Métodos com parâmetros, especificando objetos dinâmicos para os parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="84260-236">Como alternativa à especificação de parâmetros como tipos genéricos do `On` método, você pode especificar parâmetros como objetos dinâmicos:</span><span class="sxs-lookup"><span data-stu-id="84260-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="84260-237">**Método de chamada de código do servidor com um parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="84260-238">**A classe Stock usada para o parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="84260-239">**Código cliente WinRT para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro[(veja exemplos WPF e Silverlight mais tarde neste tópico](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="84260-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="84260-240">Como remover um manipulador</span><span class="sxs-lookup"><span data-stu-id="84260-240">How to remove a handler</span></span>

<span data-ttu-id="84260-241">Para remover um manipulador, chame seu `Dispose` método.</span><span class="sxs-lookup"><span data-stu-id="84260-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="84260-242">**Código do cliente para um método chamado de servidor**</span><span class="sxs-lookup"><span data-stu-id="84260-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="84260-243">**Código do cliente para remover o manipulador**</span><span class="sxs-lookup"><span data-stu-id="84260-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="84260-244">Como chamar métodos de servidor do cliente</span><span class="sxs-lookup"><span data-stu-id="84260-244">How to call server methods from the client</span></span>

<span data-ttu-id="84260-245">Para chamar um método no `Invoke` servidor, use o método no proxy do Hub.</span><span class="sxs-lookup"><span data-stu-id="84260-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="84260-246">Se o método do servidor não tiver valor de `Invoke` retorno, use a sobrecarga não genérica do método.</span><span class="sxs-lookup"><span data-stu-id="84260-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="84260-247">**Código do servidor para um método que não tem valor de retorno**</span><span class="sxs-lookup"><span data-stu-id="84260-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="84260-248">**Código do cliente chamando um método que não tem valor de retorno**</span><span class="sxs-lookup"><span data-stu-id="84260-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="84260-249">Se o método do servidor tiver um valor de retorno, especifique o tipo de retorno como o tipo genérico do `Invoke` método.</span><span class="sxs-lookup"><span data-stu-id="84260-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="84260-250">**Código do servidor para um método que tem um valor de retorno e leva um parâmetro de tipo complexo**</span><span class="sxs-lookup"><span data-stu-id="84260-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="84260-251">**A classe stock usada para o parâmetro e o valor de retorno**</span><span class="sxs-lookup"><span data-stu-id="84260-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="84260-252">**Código do cliente chamando um método que tem um valor de retorno e leva um parâmetro de tipo complexo, em um método de sincronização de ASP.NET 4.5**</span><span class="sxs-lookup"><span data-stu-id="84260-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="84260-253">**Código do cliente chamando um método que tem um valor de retorno e leva um parâmetro de tipo complexo, em um método síncrono**</span><span class="sxs-lookup"><span data-stu-id="84260-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="84260-254">O `Invoke` método executa assíncronamente e retorna um `Task` objeto.</span><span class="sxs-lookup"><span data-stu-id="84260-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="84260-255">Se você não `await` especificar ou `.Wait()`, a próxima linha de código será executada antes que o método que você invoca tenha terminado de executar.</span><span class="sxs-lookup"><span data-stu-id="84260-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="84260-256">Como lidar com eventos de vida de conexão</span><span class="sxs-lookup"><span data-stu-id="84260-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="84260-257">O SignalR fornece os seguintes eventos de vida útil da conexão que você pode lidar:</span><span class="sxs-lookup"><span data-stu-id="84260-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="84260-258">`Received`: Levantada quando qualquer dado é recebido na conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="84260-259">Fornece os dados recebidos.</span><span class="sxs-lookup"><span data-stu-id="84260-259">Provides the received data.</span></span>
- <span data-ttu-id="84260-260">`ConnectionSlow`: Elevado quando o cliente detecta uma conexão lenta ou freqüentemente caindo.</span><span class="sxs-lookup"><span data-stu-id="84260-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="84260-261">`Reconnecting`: Elevado quando o transporte subjacente começa a se reconectar.</span><span class="sxs-lookup"><span data-stu-id="84260-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="84260-262">`Reconnected`: Elevado quando o transporte subjacente for reconectado.</span><span class="sxs-lookup"><span data-stu-id="84260-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="84260-263">`StateChanged`: Elevado quando o estado de conexão muda.</span><span class="sxs-lookup"><span data-stu-id="84260-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="84260-264">Fornece o estado antigo e o novo estado.</span><span class="sxs-lookup"><span data-stu-id="84260-264">Provides the old state and the new state.</span></span> <span data-ttu-id="84260-265">Para obter informações sobre valores de estado de conexão, consulte [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="84260-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="84260-266">`Closed`: Elevado quando a conexão se desconecta.</span><span class="sxs-lookup"><span data-stu-id="84260-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="84260-267">Por exemplo, se você quiser exibir mensagens de aviso para erros que não são fatais, mas `ConnectionSlow` causam problemas de conexão intermitente, como lentidão ou queda frequente da conexão, manuseie o evento.</span><span class="sxs-lookup"><span data-stu-id="84260-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="84260-268">Para obter mais informações, consulte [Compreensão e manipulação de eventos vitalícios de conexão no SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="84260-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="84260-269">Como lidar com erros</span><span class="sxs-lookup"><span data-stu-id="84260-269">How to handle errors</span></span>

<span data-ttu-id="84260-270">Se você não habilitar explicitamente mensagens de erro detalhadas no servidor, o objeto de exceção que o SignalR retorna após um erro contém informações mínimas sobre o erro.</span><span class="sxs-lookup"><span data-stu-id="84260-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="84260-271">Por exemplo, se `newContosoChatMessage` uma chamada falhar, a mensagem`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`de erro no objeto de erro contém " " Enviar mensagens de erro detalhadas aos clientes em produção não é recomendado por razões de segurança, mas se você quiser ativar mensagens de erro detalhadas para fins de solução de problemas, use o código a seguir no servidor.</span><span class="sxs-lookup"><span data-stu-id="84260-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="84260-272">Para lidar com erros que o SignalR `Error` levanta, você pode adicionar um manipulador para o evento no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="84260-273">Para lidar com erros de invocações de método, enrole o código em um bloco de tentativa de captura.</span><span class="sxs-lookup"><span data-stu-id="84260-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="84260-274">Como habilitar o registro do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="84260-274">How to enable client-side logging</span></span>

<span data-ttu-id="84260-275">Para habilitar o registro `TraceLevel` do `TraceWriter` lado do cliente, defina as propriedades e as propriedades no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="84260-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="84260-276">Amostras de código de aplicativo WPF, Silverlight e console para métodos de cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="84260-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="84260-277">As amostras de código mostradas anteriormente para definir os métodos do cliente que o servidor pode chamar aplicam-se aos clientes WinRT.</span><span class="sxs-lookup"><span data-stu-id="84260-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="84260-278">As amostras a seguir mostram o código equivalente para clientes wpf, silverlight e aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="84260-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="84260-279">Métodos sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-279">Methods without parameters</span></span>

<span data-ttu-id="84260-280">**Código cliente WPF para método chamado de servidor sem parâmetros**</span><span class="sxs-lookup"><span data-stu-id="84260-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="84260-281">**Código cliente silverlight para método chamado de servidor sem parâmetros**</span><span class="sxs-lookup"><span data-stu-id="84260-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="84260-282">**Código cliente do aplicativo de console para método chamado de servidor sem parâmetros**</span><span class="sxs-lookup"><span data-stu-id="84260-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="84260-283">Métodos com parâmetros, especificando os tipos de parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="84260-284">**Código do cliente WPF para um método chamado de servidor com um parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="84260-285">**Código cliente silverlight para um método chamado de servidor com um parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="84260-286">**Código cliente do aplicativo de console para um método chamado de servidor com um parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="84260-287">Métodos com parâmetros, especificando objetos dinâmicos para os parâmetros</span><span class="sxs-lookup"><span data-stu-id="84260-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="84260-288">**Código cliente WPF para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="84260-289">**Código cliente silverlight para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="84260-290">**Console código cliente do aplicativo para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84260-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
