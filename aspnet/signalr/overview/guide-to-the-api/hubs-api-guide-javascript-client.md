---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hubs API Guide - JavaScript Client | Microsoft Docs
author: bradygaster
description: Este documento fornece uma introdução ao uso da API hubs para signalR versão 2 em clientes JavaScript, como navegadores e aplicativos da Windows Store (WinJS) ...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676079"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="7b09a-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span><span class="sxs-lookup"><span data-stu-id="7b09a-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="7b09a-104">Este documento fornece uma introdução ao uso da API hubs para signalR versão 2 em clientes JavaScript, como navegadores e aplicativos da Windows Store (WinJS).</span><span class="sxs-lookup"><span data-stu-id="7b09a-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="7b09a-105">A API SignalR Hubs permite que você faça chamadas de procedimento remoto (RPCs) de um servidor para clientes conectados e de clientes para o servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="7b09a-106">No código do servidor, você define métodos que podem ser chamados pelos clientes e você chama métodos que são executados no cliente.</span><span class="sxs-lookup"><span data-stu-id="7b09a-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="7b09a-107">No código do cliente, você define métodos que podem ser chamados do servidor e você chama métodos que são executados no servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="7b09a-108">O SignalR cuida de todo o encanamento cliente-servidor para você.</span><span class="sxs-lookup"><span data-stu-id="7b09a-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="7b09a-109">SignalR também oferece uma API de nível inferior chamada Conexões Persistentes.</span><span class="sxs-lookup"><span data-stu-id="7b09a-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="7b09a-110">Para obter uma introdução ao SignalR, hubs e persistent connections, consulte [Introdução ao SignalR](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="7b09a-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="7b09a-111">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="7b09a-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="7b09a-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7b09a-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="7b09a-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="7b09a-113">.NET 4.5</span></span>
> - <span data-ttu-id="7b09a-114">SignalR versão 2</span><span class="sxs-lookup"><span data-stu-id="7b09a-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="7b09a-115">Versões anteriores deste tópico</span><span class="sxs-lookup"><span data-stu-id="7b09a-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="7b09a-116">Para obter informações sobre versões anteriores do SignalR, consulte [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="7b09a-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="7b09a-117">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="7b09a-117">Questions and comments</span></span>
>
> <span data-ttu-id="7b09a-118">Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="7b09a-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="7b09a-119">Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="7b09a-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="7b09a-120">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7b09a-120">Overview</span></span>

<span data-ttu-id="7b09a-121">Este documento contém as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="7b09a-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="7b09a-122">O proxy gerado e o que ele faz por você</span><span class="sxs-lookup"><span data-stu-id="7b09a-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="7b09a-123">Quando usar o proxy gerado</span><span class="sxs-lookup"><span data-stu-id="7b09a-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="7b09a-124">Configuração do cliente</span><span class="sxs-lookup"><span data-stu-id="7b09a-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="7b09a-125">Como referenciar o proxy gerado dinamicamente</span><span class="sxs-lookup"><span data-stu-id="7b09a-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="7b09a-126">Como criar um arquivo físico para o proxy gerado signalR</span><span class="sxs-lookup"><span data-stu-id="7b09a-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="7b09a-127">Como estabelecer uma conexão</span><span class="sxs-lookup"><span data-stu-id="7b09a-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="7b09a-128">$.connection.hub é o mesmo objeto que $.hubConnection() cria</span><span class="sxs-lookup"><span data-stu-id="7b09a-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="7b09a-129">Execução assíncrona do método de início</span><span class="sxs-lookup"><span data-stu-id="7b09a-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="7b09a-130">Como estabelecer uma conexão entre domínios</span><span class="sxs-lookup"><span data-stu-id="7b09a-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="7b09a-131">Como configurar a conexão</span><span class="sxs-lookup"><span data-stu-id="7b09a-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="7b09a-132">Como especificar parâmetros de seqüência de consultas</span><span class="sxs-lookup"><span data-stu-id="7b09a-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="7b09a-133">Como especificar o método de transporte</span><span class="sxs-lookup"><span data-stu-id="7b09a-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="7b09a-134">Como obter um proxy para uma classe Hub</span><span class="sxs-lookup"><span data-stu-id="7b09a-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="7b09a-135">Como definir métodos no cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="7b09a-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="7b09a-136">Como chamar métodos de servidor do cliente</span><span class="sxs-lookup"><span data-stu-id="7b09a-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="7b09a-137">Como lidar com eventos de vida de conexão</span><span class="sxs-lookup"><span data-stu-id="7b09a-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="7b09a-138">Como lidar com erros</span><span class="sxs-lookup"><span data-stu-id="7b09a-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="7b09a-139">Como habilitar o registro do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="7b09a-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="7b09a-140">Para obter a documentação sobre como programar os clientes do servidor ou .NET, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="7b09a-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="7b09a-141">SignalR Hubs Guia de API - Servidor</span><span class="sxs-lookup"><span data-stu-id="7b09a-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="7b09a-142">SignalR Hubs API Guide - .NET Client</span><span class="sxs-lookup"><span data-stu-id="7b09a-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="7b09a-143">O componente servidor SignalR 2 só está disponível no .NET 4.5 (embora haja um cliente .NET para SignalR 2 no .NET 4.0).</span><span class="sxs-lookup"><span data-stu-id="7b09a-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="7b09a-144">O proxy gerado e o que ele faz por você</span><span class="sxs-lookup"><span data-stu-id="7b09a-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="7b09a-145">Você pode programar um cliente JavaScript para se comunicar com um serviço SignalR com ou sem um proxy que o SignalR gera para você.</span><span class="sxs-lookup"><span data-stu-id="7b09a-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="7b09a-146">O que o proxy faz para você é simplificar a sintaxe do código que você usa para conectar, gravar métodos que o servidor chama e métodos de chamada no servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="7b09a-147">Quando você escreve código para chamar métodos de servidor, o proxy gerado permite que você use uma `serverMethod(arg1, arg2)` sintaxe que parece que você estava executando uma função local: você pode escrever em vez de `invoke('serverMethod', arg1, arg2)`.</span><span class="sxs-lookup"><span data-stu-id="7b09a-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="7b09a-148">A sintaxe proxy gerada também permite um erro imediato e inteligível do lado do cliente se você digitar mal o nome do método do servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="7b09a-149">E se você criar manualmente o arquivo que define os proxies, você também poderá obter suporte ao IntelliSense para escrever código que chama métodos de servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="7b09a-150">Por exemplo, suponha que você tenha a seguinte classe hub no servidor:</span><span class="sxs-lookup"><span data-stu-id="7b09a-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="7b09a-151">Os exemplos de código a seguir mostram como `NewContosoChatMessage` o código JavaScript se parece `addContosoChatMessageToPage` para invocar o método no servidor e receber invocações do método do servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="7b09a-152">**Com o proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="7b09a-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="7b09a-153">**Sem o proxy gerado**</span><span class="sxs-lookup"><span data-stu-id="7b09a-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="7b09a-154">Quando usar o proxy gerado</span><span class="sxs-lookup"><span data-stu-id="7b09a-154">When to use the generated proxy</span></span>

<span data-ttu-id="7b09a-155">Se você quiser registrar vários manipuladores de eventos para um método cliente que o servidor chama, você não poderá usar o proxy gerado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="7b09a-156">Caso contrário, você pode optar por usar o proxy gerado ou não com base na sua preferência de codificação.</span><span class="sxs-lookup"><span data-stu-id="7b09a-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="7b09a-157">Se você optar por não usá-lo, não precisa referenciar a URL `script` "signalr/hubs" em um elemento no código do cliente.</span><span class="sxs-lookup"><span data-stu-id="7b09a-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="7b09a-158">Configuração do cliente</span><span class="sxs-lookup"><span data-stu-id="7b09a-158">Client setup</span></span>

<span data-ttu-id="7b09a-159">Um cliente JavaScript requer referências ao jQuery e ao arquivo JavaScript do núcleo SignalR.</span><span class="sxs-lookup"><span data-stu-id="7b09a-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="7b09a-160">A versão jQuery deve ser 1.6.4 ou versões posteriores principais, como 1.7.2, 1.8.2 ou 1.9.1.</span><span class="sxs-lookup"><span data-stu-id="7b09a-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="7b09a-161">Se você decidir usar o proxy gerado, você também precisará de uma referência ao arquivo JavaScript proxy gerado pelo SignalR.</span><span class="sxs-lookup"><span data-stu-id="7b09a-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="7b09a-162">O exemplo a seguir mostra como as referências podem parecer em uma página HTML que usa o proxy gerado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="7b09a-163">Essas referências devem ser incluídas nesta ordem: jQuery primeiro, núcleo SignalR depois disso e proxies SignalR por último.</span><span class="sxs-lookup"><span data-stu-id="7b09a-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="7b09a-164">Como referenciar o proxy gerado dinamicamente</span><span class="sxs-lookup"><span data-stu-id="7b09a-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="7b09a-165">No exemplo anterior, a referência ao proxy gerado pelo SignalR é para código JavaScript gerado dinamicamente, não para um arquivo físico.</span><span class="sxs-lookup"><span data-stu-id="7b09a-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="7b09a-166">SignalR cria o código JavaScript para o proxy em tempo real e serve-o ao cliente em resposta à URL "/signalr/hubs".</span><span class="sxs-lookup"><span data-stu-id="7b09a-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="7b09a-167">Se você especificou uma URL base diferente para `MapSignalR` conexões SignalR no servidor em seu método, a URL para o arquivo proxy gerado dinamicamente é sua URL personalizada com "/hubs" anexados a ele.</span><span class="sxs-lookup"><span data-stu-id="7b09a-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="7b09a-168">Para clientes JavaScript do Windows 8 (Windows Store), use o arquivo proxy físico em vez do gerado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="7b09a-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="7b09a-169">Para obter mais informações, consulte [Como criar um arquivo físico para o proxy gerado pelo SignalR](#manualproxy) mais tarde neste tópico.</span><span class="sxs-lookup"><span data-stu-id="7b09a-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="7b09a-170">Em uma ASP.NET exibição de Navalha MVC 4 ou 5, use o tilde para consultar a raiz do aplicativo na referência do arquivo proxy:</span><span class="sxs-lookup"><span data-stu-id="7b09a-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="7b09a-171">Para obter mais informações sobre como usar o SignalR no MVC 5, consulte [Getting Started com SignalR e MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="7b09a-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="7b09a-172">Em uma ASP.NET exibição de `Url.Content` Navalha MVC 3, use para a referência do arquivo proxy:</span><span class="sxs-lookup"><span data-stu-id="7b09a-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="7b09a-173">Em um aplicativo ASP.NET `ResolveClientUrl` Formulários da Web, use para a referência do arquivo de seus proxies ou registre-o através do ScriptManager usando um caminho relativo raiz de aplicativo (começando com um tilde):</span><span class="sxs-lookup"><span data-stu-id="7b09a-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="7b09a-174">Como regra geral, use o mesmo método para especificar a URL "/signalr/hubs" que você usa para arquivos CSS ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7b09a-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="7b09a-175">Se você especificar uma URL sem usar um tilde, em alguns cenários seu aplicativo funcionará corretamente quando você testar no Visual Studio usando o IIS Express, mas falhará com um erro de 404 quando você implantar no IIS completo.</span><span class="sxs-lookup"><span data-stu-id="7b09a-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="7b09a-176">Para obter mais informações, consulte **Resolvendo referências a recursos de nível raiz** em servidores web no Visual Studio para ASP.NET Projetos [Web](https://msdn.microsoft.com/library/58wxa9w5.aspx) no site do MSDN.</span><span class="sxs-lookup"><span data-stu-id="7b09a-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="7b09a-177">Quando você executa um projeto web no Visual Studio 2017 no modo de depuração, e se você usar o Internet Explorer como seu navegador, você pode ver o arquivo proxy no **Solution Explorer** em **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="7b09a-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="7b09a-178">Para ver o conteúdo do arquivo, clique duas vezes **em hubs**.</span><span class="sxs-lookup"><span data-stu-id="7b09a-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="7b09a-179">Se você não estiver usando o Visual Studio 2012 ou 2013 e o Internet Explorer, ou se você não estiver no modo de depuração, você também pode obter o conteúdo do arquivo navegando para a URL "/signalR/hubs".</span><span class="sxs-lookup"><span data-stu-id="7b09a-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="7b09a-180">Por exemplo, se o `http://localhost:56699`seu site `http://localhost:56699/SignalR/hubs` estiver sendo executado em , vá para o seu navegador.</span><span class="sxs-lookup"><span data-stu-id="7b09a-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="7b09a-181">Como criar um arquivo físico para o proxy gerado signalR</span><span class="sxs-lookup"><span data-stu-id="7b09a-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="7b09a-182">Como uma alternativa ao proxy gerado dinamicamente, você pode criar um arquivo físico que tenha o código proxy e faça referência a esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="7b09a-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="7b09a-183">Você pode querer fazer isso para controlar o comportamento de cache ou agrupamento, ou para obter o IntelliSense quando você está codificando chamadas para métodos de servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="7b09a-184">Para criar um arquivo proxy, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7b09a-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="7b09a-185">Instale o pacote [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b09a-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="7b09a-186">Abra um prompt de comando e navegue até a pasta *de ferramentas* que contém o arquivo SignalR.exe.</span><span class="sxs-lookup"><span data-stu-id="7b09a-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="7b09a-187">A pasta de ferramentas está no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="7b09a-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="7b09a-188">Insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7b09a-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="7b09a-189">O caminho para o *seu .dll* é tipicamente a pasta *bin* na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="7b09a-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="7b09a-190">Este comando cria um arquivo chamado *server.js* na mesma pasta *que signalr.exe*.</span><span class="sxs-lookup"><span data-stu-id="7b09a-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="7b09a-191">Coloque o arquivo *server.js* em uma pasta apropriada em seu projeto, renomeie-o conforme apropriado para o seu aplicativo e adicione uma referência a ele no lugar da referência "signalr/hubs".</span><span class="sxs-lookup"><span data-stu-id="7b09a-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="7b09a-192">Como estabelecer uma conexão</span><span class="sxs-lookup"><span data-stu-id="7b09a-192">How to establish a connection</span></span>

<span data-ttu-id="7b09a-193">Antes de estabelecer uma conexão, você tem que criar um objeto de conexão, criar um proxy e registrar manipuladores de eventos para métodos que podem ser chamados do servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="7b09a-194">Quando os manipuladores de proxy e eventos estiverem `start` configurados, estabeleça a conexão chamando o método.</span><span class="sxs-lookup"><span data-stu-id="7b09a-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="7b09a-195">Se você estiver usando o proxy gerado, você não precisa criar o objeto de conexão em seu próprio código porque o código proxy gerado o faz para você.</span><span class="sxs-lookup"><span data-stu-id="7b09a-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="7b09a-196">**Estabeleça uma conexão (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="7b09a-197">**Estabeleça uma conexão (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="7b09a-198">O código de exemplo usa a URL padrão "/signalr" para se conectar ao serviço SignalR.</span><span class="sxs-lookup"><span data-stu-id="7b09a-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="7b09a-199">Para obter informações sobre como especificar uma URL base diferente, consulte [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="7b09a-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="7b09a-200">Por padrão, a localização do hub é o servidor atual; se você estiver se conectando a um servidor `start` diferente, especifique a URL antes de chamar o método, como mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b09a-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="7b09a-201">Normalmente você registra manipuladores `start` de eventos antes de chamar o método para estabelecer a conexão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="7b09a-202">Se você quiser registrar alguns manipuladores de eventos depois de estabelecer a conexão, você pode fazer isso, mas você deve registrar pelo menos um dos seus manipuladores de eventos antes de chamar o `start` método.</span><span class="sxs-lookup"><span data-stu-id="7b09a-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="7b09a-203">Uma razão para isso é que pode haver muitos Hubs em um `OnConnected` aplicativo, mas você não gostaria de acionar o evento em todos os Hubs se você só vai usar para um deles.</span><span class="sxs-lookup"><span data-stu-id="7b09a-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="7b09a-204">Quando a conexão é estabelecida, a presença de um método de cliente no `OnConnected` proxy de um Hub é o que diz ao SignalR para acionar o evento.</span><span class="sxs-lookup"><span data-stu-id="7b09a-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="7b09a-205">Se você não registrar nenhum manipulador de `start` eventos antes de chamar o método, você poderá invocar `OnConnected` métodos no Hub, mas o método do Hub não será chamado e nenhum método de cliente será invocado do servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="7b09a-206">$.connection.hub é o mesmo objeto que $.hubConnection() cria</span><span class="sxs-lookup"><span data-stu-id="7b09a-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="7b09a-207">Como você pode ver nos exemplos, quando você `$.connection.hub` usa o proxy gerado, refere-se ao objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="7b09a-208">Este é o mesmo objeto `$.hubConnection()` que você recebe chamando quando você não está usando o proxy gerado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="7b09a-209">O código proxy gerado cria a conexão para você executando a seguinte declaração:</span><span class="sxs-lookup"><span data-stu-id="7b09a-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Criando uma conexão no arquivo proxy gerado](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="7b09a-211">Quando você está usando o proxy gerado, `$.connection.hub` você pode fazer qualquer coisa com o que você pode fazer com um objeto de conexão quando você não está usando o proxy gerado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="7b09a-212">Execução assíncrona do método de início</span><span class="sxs-lookup"><span data-stu-id="7b09a-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="7b09a-213">O `start` método é executado de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="7b09a-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="7b09a-214">Ele retorna um [objeto jQuery Diferido,](http://api.jquery.com/category/deferred-object/)o que significa que você `pipe`pode `done`adicionar `fail`funções de retorno de chamada chamando métodos como , e .</span><span class="sxs-lookup"><span data-stu-id="7b09a-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="7b09a-215">Se você tiver um código que deseja executar depois que a conexão for estabelecida, como uma chamada para um método de servidor, coloque esse código em uma função de retorno de chamada ou chame-o de uma função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="7b09a-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="7b09a-216">O `.done` método de retorno de chamada é executado após a conexão ter `OnConnected` sido estabelecida e, após qualquer código que você tenha em seu método de manipulador de eventos, no servidor termina a execução.</span><span class="sxs-lookup"><span data-stu-id="7b09a-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="7b09a-217">Se você colocar a declaração "Agora conectado" do exemplo `start` anterior como a `.done` próxima linha `console.log` de código após a chamada do método (não em um retorno de chamada), a linha será executada antes que a conexão seja estabelecida, como mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b09a-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Maneira errada de escrever código que é executado após a conexão é estabelecida](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="7b09a-219">Como estabelecer uma conexão entre domínios</span><span class="sxs-lookup"><span data-stu-id="7b09a-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="7b09a-220">Normalmente, se o navegador `http://contoso.com`carregar uma página de , a `http://contoso.com/signalr`conexão SignalR está no mesmo domínio, em .</span><span class="sxs-lookup"><span data-stu-id="7b09a-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="7b09a-221">Se a `http://contoso.com` página de `http://fabrikam.com/signalr`fazer uma conexão com , que é uma conexão de domínio cruzado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="7b09a-222">Por razões de segurança, as conexões entre domínios são desativadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="7b09a-223">No SignalR 1.x, as solicitações de domínio cruzado eram controladas por um único sinalizador EnableCrossDomain.</span><span class="sxs-lookup"><span data-stu-id="7b09a-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="7b09a-224">Esta bandeira controlava tanto as solicitações JSONP quanto CORS.</span><span class="sxs-lookup"><span data-stu-id="7b09a-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="7b09a-225">Para maior flexibilidade, todo o suporte ao CORS foi removido do componente do servidor do SignalR (os clientes JavaScript ainda usam o CORS normalmente se for detectado que o navegador o suporta), e novos middleware oWIN foram disponibilizados para suportar esses cenários.</span><span class="sxs-lookup"><span data-stu-id="7b09a-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="7b09a-226">Se o JSONP for necessário no cliente (para suportar solicitações de domínio cruzado em `EnableJSONP` navegadores `HubConfiguration` mais `true`antigos), ele precisará ser ativado explicitamente definindo no objeto para , como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7b09a-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="7b09a-227">O JSONP é desativado por padrão, pois é menos seguro que o CORS.</span><span class="sxs-lookup"><span data-stu-id="7b09a-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="7b09a-228">**Adicionando microsoft.Owin.Cors ao seu projeto:** Para instalar esta biblioteca, execute o seguinte comando no Console do Gerenciador de Pacotes:</span><span class="sxs-lookup"><span data-stu-id="7b09a-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="7b09a-229">Este comando adicionará a versão 2.1.0 do pacote ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="7b09a-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="7b09a-230">Chamando UseCors</span><span class="sxs-lookup"><span data-stu-id="7b09a-230">Calling UseCors</span></span>

 <span data-ttu-id="7b09a-231">O trecho de código a seguir demonstra como implementar conexões entre domínios no SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="7b09a-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="7b09a-232">**Implementação de solicitações de domínio cruzado no SignalR 2**</span><span class="sxs-lookup"><span data-stu-id="7b09a-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="7b09a-233">O código a seguir demonstra como ativar CORS ou JSONP em um projeto SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="7b09a-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="7b09a-234">Esta amostra `Map` de `RunSignalR` código `MapSignalR`usa e, em vez de, de modo que o middleware CORS é executado apenas `MapSignalR`para as solicitações SignalR que requerem suporte ao CORS (em vez de todo o tráfego no caminho especificado em .) O mapa também pode ser usado para qualquer outro middleware que precise ser executado para um prefixo de URL específico, em vez de para toda a aplicação.</span><span class="sxs-lookup"><span data-stu-id="7b09a-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="7b09a-235">Não se `jQuery.support.cors` defina como verdadeiro em seu código.</span><span class="sxs-lookup"><span data-stu-id="7b09a-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![Não defina jQuery.support.cors como verdadeiro](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="7b09a-237">SignalR lida com o uso do CORS.</span><span class="sxs-lookup"><span data-stu-id="7b09a-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="7b09a-238">A `jQuery.support.cors` configuração para true desativa o JSONP porque faz com que o SignalR assuma que o navegador suporta cors.</span><span class="sxs-lookup"><span data-stu-id="7b09a-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="7b09a-239">Quando você está se conectando a uma URL de host local, o Internet Explorer 10 não considerará uma conexão entre domínios, então o aplicativo funcionará localmente com o IE 10, mesmo que você não tenha ativado conexões de domínio cruzado no servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="7b09a-240">Para obter informações sobre o uso de conexões entre domínios com o Internet Explorer 9, consulte [este segmento StackOverflow](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span><span class="sxs-lookup"><span data-stu-id="7b09a-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="7b09a-241">Para obter informações sobre o uso de conexões entre domínios com o Chrome, consulte [este segmento StackOverflow](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span><span class="sxs-lookup"><span data-stu-id="7b09a-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="7b09a-242">O código de exemplo usa a URL padrão "/signalr" para se conectar ao serviço SignalR.</span><span class="sxs-lookup"><span data-stu-id="7b09a-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="7b09a-243">Para obter informações sobre como especificar uma URL base diferente, consulte [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="7b09a-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="7b09a-244">Como configurar a conexão</span><span class="sxs-lookup"><span data-stu-id="7b09a-244">How to configure the connection</span></span>

<span data-ttu-id="7b09a-245">Antes de estabelecer uma conexão, você pode especificar parâmetros de seqüência de consulta ou especificar o método de transporte.</span><span class="sxs-lookup"><span data-stu-id="7b09a-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="7b09a-246">Como especificar parâmetros de seqüência de consultas</span><span class="sxs-lookup"><span data-stu-id="7b09a-246">How to specify query string parameters</span></span>

<span data-ttu-id="7b09a-247">Se você quiser enviar dados para o servidor quando o cliente se conectar, você pode adicionar parâmetros de seqüência de consulta ao objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="7b09a-248">Os exemplos a seguir mostram como definir um parâmetro de seqüência de consultas no código do cliente.</span><span class="sxs-lookup"><span data-stu-id="7b09a-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="7b09a-249">**Defina um valor de seqüência de consulta antes de chamar o método iniciar (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="7b09a-250">**Defina um valor de seqüência de consulta antes de chamar o método iniciar (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="7b09a-251">O exemplo a seguir mostra como ler um parâmetro de seqüência de consultas no código do servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="7b09a-252">Como especificar o método de transporte</span><span class="sxs-lookup"><span data-stu-id="7b09a-252">How to specify the transport method</span></span>

<span data-ttu-id="7b09a-253">Como parte do processo de conexão, um cliente SignalR normalmente negocia com o servidor para determinar o melhor transporte que é suportado tanto pelo servidor quanto pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="7b09a-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="7b09a-254">Se você já sabe qual transporte deseja usar, você pode contornar esse processo `start` de negociação especificando o método de transporte quando você chamar o método.</span><span class="sxs-lookup"><span data-stu-id="7b09a-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="7b09a-255">**Código do cliente que especifica o método de transporte (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="7b09a-256">**Código do cliente que especifica o método de transporte (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="7b09a-257">Como alternativa, você pode especificar vários métodos de transporte na ordem em que deseja que o SignalR os experimente:</span><span class="sxs-lookup"><span data-stu-id="7b09a-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="7b09a-258">**Código do cliente que especifica um esquema de retorno de transporte personalizado (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="7b09a-259">**Código do cliente que especifica um esquema de retorno de transporte personalizado (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="7b09a-260">Você pode usar os seguintes valores para especificar o método de transporte:</span><span class="sxs-lookup"><span data-stu-id="7b09a-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="7b09a-261">"WebSockets"</span><span class="sxs-lookup"><span data-stu-id="7b09a-261">"webSockets"</span></span>
- <span data-ttu-id="7b09a-262">"ForeverFrame"</span><span class="sxs-lookup"><span data-stu-id="7b09a-262">"foreverFrame"</span></span>
- <span data-ttu-id="7b09a-263">"ServerSentEvents"</span><span class="sxs-lookup"><span data-stu-id="7b09a-263">"serverSentEvents"</span></span>
- <span data-ttu-id="7b09a-264">"LongPolling"</span><span class="sxs-lookup"><span data-stu-id="7b09a-264">"longPolling"</span></span>

<span data-ttu-id="7b09a-265">Os exemplos a seguir mostram como descobrir qual método de transporte está sendo usado por uma conexão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="7b09a-266">**Código do cliente que exibe o método de transporte usado por uma conexão (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="7b09a-267">**Código do cliente que exibe o método de transporte usado por uma conexão (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="7b09a-268">Para obter informações sobre como verificar o método de transporte no código do servidor, consulte [ASP.NET SignalR Hubs API Guide - Server - Como obter informações sobre o cliente a partir da propriedade Context](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="7b09a-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="7b09a-269">Para obter mais informações sobre transportes e recuos, consulte [Introdução ao SignalR - Transportes e Recuos](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="7b09a-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="7b09a-270">Como obter um proxy para uma classe Hub</span><span class="sxs-lookup"><span data-stu-id="7b09a-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="7b09a-271">Cada objeto de conexão que você cria encapsula informações sobre uma conexão a um serviço SignalR que contém uma ou mais classes do Hub.</span><span class="sxs-lookup"><span data-stu-id="7b09a-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="7b09a-272">Para se comunicar com uma classe Hub, você usa um objeto proxy que você mesmo cria (se você não estiver usando o proxy gerado) ou que é gerado para você.</span><span class="sxs-lookup"><span data-stu-id="7b09a-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="7b09a-273">No cliente, o nome do proxy é uma versão com maiúsculas e camelos do nome da classe Hub.</span><span class="sxs-lookup"><span data-stu-id="7b09a-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="7b09a-274">SignalR faz automaticamente essa alteração para que o código JavaScript possa estar em conformidade com as convenções JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7b09a-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="7b09a-275">**Classe hub no servidor**</span><span class="sxs-lookup"><span data-stu-id="7b09a-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="7b09a-276">**Obtenha uma referência ao proxy do cliente gerado para o Hub**</span><span class="sxs-lookup"><span data-stu-id="7b09a-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="7b09a-277">**Criar proxy de cliente para a classe Hub (sem proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="7b09a-278">Se você decorar sua classe `HubName` Hub com um atributo, use o nome exato sem alterar o caso.</span><span class="sxs-lookup"><span data-stu-id="7b09a-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="7b09a-279">**Classe hub no servidor com atributo HubName**</span><span class="sxs-lookup"><span data-stu-id="7b09a-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="7b09a-280">**Obtenha uma referência ao proxy do cliente gerado para o Hub**</span><span class="sxs-lookup"><span data-stu-id="7b09a-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="7b09a-281">**Criar proxy de cliente para a classe Hub (sem proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="7b09a-282">Como definir métodos no cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="7b09a-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="7b09a-283">Para definir um método que o servidor pode chamar de um Hub, `client` adicione um manipulador de `on` eventos ao proxy do Hub usando a propriedade do proxy gerado ou chame o método se você não estiver usando o proxy gerado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="7b09a-284">Os parâmetros podem ser objetos complexos.</span><span class="sxs-lookup"><span data-stu-id="7b09a-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="7b09a-285">Adicione o manipulador de `start` eventos antes de chamar o método para estabelecer a conexão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="7b09a-286">(Se você quiser adicionar manipuladores `start` de eventos após chamar o método, consulte a nota em [Como estabelecer uma conexão](#establishconnection) anteriormente neste documento e use a sintaxe mostrada para definir um método sem usar o proxy gerado.)</span><span class="sxs-lookup"><span data-stu-id="7b09a-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="7b09a-287">A correspondência do nome do método é insensível ao caso.</span><span class="sxs-lookup"><span data-stu-id="7b09a-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="7b09a-288">Por `Clients.All.addContosoChatMessageToPage` exemplo, no servidor `AddContosoChatMessageToPage` `addContosoChatMessageToPage`executará `addcontosochatmessagetopage` , ou no cliente.</span><span class="sxs-lookup"><span data-stu-id="7b09a-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="7b09a-289">**Definir método no cliente (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="7b09a-290">**Forma alternativa de definir o método no cliente (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="7b09a-291">**Defina o método no cliente (sem o proxy gerado ou ao adicionar após chamar o método de início)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="7b09a-292">**Código do servidor que chama o método do cliente**</span><span class="sxs-lookup"><span data-stu-id="7b09a-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="7b09a-293">Os exemplos a seguir incluem um objeto complexo como parâmetro de método.</span><span class="sxs-lookup"><span data-stu-id="7b09a-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="7b09a-294">**Defina o método no cliente que leva um objeto complexo (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="7b09a-295">**Defina o método no cliente que leva um objeto complexo (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="7b09a-296">**Código do servidor que define o objeto complexo**</span><span class="sxs-lookup"><span data-stu-id="7b09a-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="7b09a-297">**Código do servidor que chama o método do cliente usando um objeto complexo**</span><span class="sxs-lookup"><span data-stu-id="7b09a-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="7b09a-298">Como chamar métodos de servidor do cliente</span><span class="sxs-lookup"><span data-stu-id="7b09a-298">How to call server methods from the client</span></span>

<span data-ttu-id="7b09a-299">Para chamar um método de servidor `server` do cliente, use `invoke` a propriedade do proxy gerado ou o método no proxy do Hub se você não estiver usando o proxy gerado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="7b09a-300">O valor de retorno ou parâmetros podem ser objetos complexos.</span><span class="sxs-lookup"><span data-stu-id="7b09a-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="7b09a-301">Passe em uma versão camelo do nome do método no Hub.</span><span class="sxs-lookup"><span data-stu-id="7b09a-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="7b09a-302">SignalR faz automaticamente essa alteração para que o código JavaScript possa estar em conformidade com as convenções JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7b09a-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="7b09a-303">Os exemplos a seguir mostram como chamar um método de servidor que não tem um valor de retorno e como chamar um método de servidor que tenha um valor de retorno.</span><span class="sxs-lookup"><span data-stu-id="7b09a-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="7b09a-304">**Método do servidor sem atributo HubMethodName**</span><span class="sxs-lookup"><span data-stu-id="7b09a-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="7b09a-305">**Código do servidor que define o objeto complexo passado em um parâmetro**</span><span class="sxs-lookup"><span data-stu-id="7b09a-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="7b09a-306">**Código do cliente que invoca o método do servidor (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="7b09a-307">**Código do cliente que invoca o método do servidor (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="7b09a-308">Se você decorou o `HubMethodName` método Hub com um atributo, use esse nome sem alterar o caso.</span><span class="sxs-lookup"><span data-stu-id="7b09a-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="7b09a-309">**Método do servidor** com um atributo HubMethodName</span><span class="sxs-lookup"><span data-stu-id="7b09a-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="7b09a-310">**Código do cliente que invoca o método do servidor (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="7b09a-311">**Código do cliente que invoca o método do servidor (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="7b09a-312">Os exemplos anteriores mostram como chamar um método de servidor que não tem valor de retorno.</span><span class="sxs-lookup"><span data-stu-id="7b09a-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="7b09a-313">Os exemplos a seguir mostram como chamar um método de servidor que tenha um valor de retorno.</span><span class="sxs-lookup"><span data-stu-id="7b09a-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="7b09a-314">**Código do servidor para um método que tem um valor de retorno**</span><span class="sxs-lookup"><span data-stu-id="7b09a-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="7b09a-315">**A classe stock usada para o** valor de retorno</span><span class="sxs-lookup"><span data-stu-id="7b09a-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="7b09a-316">**Código do cliente que invoca o método do servidor (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="7b09a-317">**Código do cliente que invoca o método do servidor (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="7b09a-318">Como lidar com eventos de vida de conexão</span><span class="sxs-lookup"><span data-stu-id="7b09a-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="7b09a-319">O SignalR fornece os seguintes eventos de vida útil da conexão que você pode lidar:</span><span class="sxs-lookup"><span data-stu-id="7b09a-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="7b09a-320">`starting`: Levantada antes de qualquer dado ser enviado pela conexão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="7b09a-321">`received`: Levantada quando qualquer dado é recebido na conexão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="7b09a-322">Fornece os dados recebidos.</span><span class="sxs-lookup"><span data-stu-id="7b09a-322">Provides the received data.</span></span>
- <span data-ttu-id="7b09a-323">`connectionSlow`: Elevado quando o cliente detecta uma conexão lenta ou freqüentemente caindo.</span><span class="sxs-lookup"><span data-stu-id="7b09a-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="7b09a-324">`reconnecting`: Elevado quando o transporte subjacente começa a se reconectar.</span><span class="sxs-lookup"><span data-stu-id="7b09a-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="7b09a-325">`reconnected`: Elevado quando o transporte subjacente for reconectado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="7b09a-326">`stateChanged`: Elevado quando o estado de conexão muda.</span><span class="sxs-lookup"><span data-stu-id="7b09a-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="7b09a-327">Fornece o estado antigo e o novo estado (Conexão, Conexão, Reconexão ou Desconectado).</span><span class="sxs-lookup"><span data-stu-id="7b09a-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="7b09a-328">`disconnected`: Elevado quando a conexão se desconecta.</span><span class="sxs-lookup"><span data-stu-id="7b09a-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="7b09a-329">Por exemplo, se você quiser exibir mensagens de aviso quando houver problemas `connectionSlow` de conexão que possam causar atrasos visíveis, manuseie o evento.</span><span class="sxs-lookup"><span data-stu-id="7b09a-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="7b09a-330">**Lidar com a conexãoEvento lento (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="7b09a-331">**Lidar com a conexãoEvento lento (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="7b09a-332">Para obter mais informações, consulte [Compreensão e manipulação de eventos vitalícios de conexão no SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="7b09a-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="7b09a-333">Como lidar com erros</span><span class="sxs-lookup"><span data-stu-id="7b09a-333">How to handle errors</span></span>

<span data-ttu-id="7b09a-334">O cliente SignalR JavaScript fornece um `error` evento para o o que você pode adicionar um manipulador.</span><span class="sxs-lookup"><span data-stu-id="7b09a-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="7b09a-335">Você também pode usar o método fail para adicionar um manipulador para erros resultantes de uma invocação do método do servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="7b09a-336">Se você não habilitar explicitamente mensagens de erro detalhadas no servidor, o objeto de exceção que o SignalR retorna após um erro contém informações mínimas sobre o erro.</span><span class="sxs-lookup"><span data-stu-id="7b09a-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="7b09a-337">Por exemplo, se `newContosoChatMessage` uma chamada falhar, a mensagem`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`de erro no objeto de erro contém " " Enviar mensagens de erro detalhadas aos clientes em produção não é recomendado por razões de segurança, mas se você quiser ativar mensagens de erro detalhadas para fins de solução de problemas, use o código a seguir no servidor.</span><span class="sxs-lookup"><span data-stu-id="7b09a-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="7b09a-338">O exemplo a seguir mostra como adicionar um manipulador para o evento de erro.</span><span class="sxs-lookup"><span data-stu-id="7b09a-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="7b09a-339">**Adicione um manipulador de erros (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="7b09a-340">**Adicione um manipulador de erros (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="7b09a-341">O exemplo a seguir mostra como lidar com um erro de uma invocação do método.</span><span class="sxs-lookup"><span data-stu-id="7b09a-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="7b09a-342">**Manuseie um erro de uma invocação de método (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="7b09a-343">**Manuseie um erro de uma invocação de método (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="7b09a-344">Se uma invocação de `error` método falhar, o evento também `error` será levantado, `.fail` de modo que seu código no manipulador de métodos e no método de retorno de chamada seria executado.</span><span class="sxs-lookup"><span data-stu-id="7b09a-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="7b09a-345">Como habilitar o registro do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="7b09a-345">How to enable client-side logging</span></span>

<span data-ttu-id="7b09a-346">Para habilitar o registro do lado `logging` do cliente em uma `start` conexão, defina a propriedade no objeto de conexão antes de chamar o método para estabelecer a conexão.</span><span class="sxs-lookup"><span data-stu-id="7b09a-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="7b09a-347">**Habilitar o registro (com o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="7b09a-348">**Habilitar o registro (sem o proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="7b09a-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="7b09a-349">Para ver os logs, abra as ferramentas de desenvolvedor do seu navegador e vá para a guia Console. Para obter um tutorial que mostre instruções passo a passo e capturas de tela que mostram como fazer isso, consulte [Server Broadcast com ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span><span class="sxs-lookup"><span data-stu-id="7b09a-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
