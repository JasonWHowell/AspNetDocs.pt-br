---
uid: signalr/overview/older-versions/troubleshooting
title: Solução de problemas do SignalR (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: Este artigo descreve problemas comuns com o desenvolvimento de aplicativos SignalR.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543087"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="114ce-103">Solução de problemas do SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="114ce-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="114ce-104">por [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="114ce-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="114ce-105">Este documento descreve problemas comuns de solução de problemas com o SignalR.</span><span class="sxs-lookup"><span data-stu-id="114ce-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="114ce-106">Este documento contém as seguintes seções.</span><span class="sxs-lookup"><span data-stu-id="114ce-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="114ce-107">Os métodos de chamada entre o cliente e o servidor falham silenciosamente</span><span class="sxs-lookup"><span data-stu-id="114ce-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="114ce-108">Outros problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="114ce-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="114ce-109">Erros de compilação e lado do servidor</span><span class="sxs-lookup"><span data-stu-id="114ce-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="114ce-110">Problemas do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="114ce-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="114ce-111">Problemas de Serviços de Informação na Internet</span><span class="sxs-lookup"><span data-stu-id="114ce-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="114ce-112">Problemas do Azure</span><span class="sxs-lookup"><span data-stu-id="114ce-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="114ce-113">Os métodos de chamada entre o cliente e o servidor falham silenciosamente</span><span class="sxs-lookup"><span data-stu-id="114ce-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="114ce-114">Esta seção descreve possíveis causas para que uma chamada de método entre cliente e servidor falhe sem uma mensagem de erro significativa.</span><span class="sxs-lookup"><span data-stu-id="114ce-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="114ce-115">Em um aplicativo SignalR, o servidor não tem informações sobre os métodos que o cliente implementa; quando o servidor invoca um método cliente, o nome do método e os dados do parâmetro são enviados ao cliente, e o método é executado somente se existir no formato que o servidor especificou.</span><span class="sxs-lookup"><span data-stu-id="114ce-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="114ce-116">Se nenhum método de correspondência for encontrado no cliente, nada acontecerá e nenhuma mensagem de erro será levantada no servidor.</span><span class="sxs-lookup"><span data-stu-id="114ce-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="114ce-117">Para investigar melhor os métodos do cliente que não estão sendo chamados, você pode ativar o registro antes de ligar para o método de início no hub para ver quais chamadas estão vindo do servidor.</span><span class="sxs-lookup"><span data-stu-id="114ce-117">To further investigate client methods not getting called, you can turn on logging before calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="114ce-118">Para habilitar o login em um aplicativo JavaScript, consulte [Como ativar o registro do lado do cliente (versão do cliente JavaScript)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="114ce-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="114ce-119">Para habilitar o login em um aplicativo cliente .NET, consulte [Como habilitar o registro do lado do cliente (versão do cliente.NET)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="114ce-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="114ce-120">Método mal escrito, assinatura de método incorreta ou nome do hub incorreto</span><span class="sxs-lookup"><span data-stu-id="114ce-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="114ce-121">Se o nome ou assinatura de um método chamado não corresponder exatamente a um método apropriado no cliente, a chamada falhará.</span><span class="sxs-lookup"><span data-stu-id="114ce-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="114ce-122">Verifique se o nome do método chamado pelo servidor corresponde ao nome do método no cliente.</span><span class="sxs-lookup"><span data-stu-id="114ce-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="114ce-123">Além disso, o SignalR cria o proxy do hub usando métodos com maiúsculas e minúsculas, como é apropriado no JavaScript, de modo que um método chamado `SendMessage` no servidor seria chamado `sendMessage` no proxy do cliente.</span><span class="sxs-lookup"><span data-stu-id="114ce-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="114ce-124">Se você `HubName` usar o atributo no código do lado do servidor, verifique se o nome usado corresponde ao nome usado para criar o hub no cliente.</span><span class="sxs-lookup"><span data-stu-id="114ce-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="114ce-125">Se você não `HubName` usar o atributo, verifique se o nome do hub em um cliente JavaScript é camel-cased, como chatHub em vez de ChatHub.</span><span class="sxs-lookup"><span data-stu-id="114ce-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="114ce-126">Nome do método duplicado no cliente</span><span class="sxs-lookup"><span data-stu-id="114ce-126">Duplicate method name on client</span></span>

<span data-ttu-id="114ce-127">Verifique se você não tem um método duplicado no cliente que difere apenas por caso.</span><span class="sxs-lookup"><span data-stu-id="114ce-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="114ce-128">Se o seu aplicativo `sendMessage`cliente tiver um método chamado, `SendMessage` verifique se também não há um método chamado.</span><span class="sxs-lookup"><span data-stu-id="114ce-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="114ce-129">Faltando analisador JSON no cliente</span><span class="sxs-lookup"><span data-stu-id="114ce-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="114ce-130">SignalR requer que um analisador JSON esteja presente para serializar chamadas entre o servidor e o cliente.</span><span class="sxs-lookup"><span data-stu-id="114ce-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="114ce-131">Se o seu cliente não tiver um analisador JSON integrado (como o Internet Explorer 7), você precisará incluir um em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="114ce-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="114ce-132">Você pode baixar o analisador JSON [aqui](http://nuget.org/packages/json2).</span><span class="sxs-lookup"><span data-stu-id="114ce-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="114ce-133">Mixing Hub e PersistentConnection sintaxe</span><span class="sxs-lookup"><span data-stu-id="114ce-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="114ce-134">O SignalR usa dois modelos de comunicação: Hubs e PersistentConnections.</span><span class="sxs-lookup"><span data-stu-id="114ce-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="114ce-135">A sintaxe para chamar esses dois modelos de comunicação é diferente no código do cliente.</span><span class="sxs-lookup"><span data-stu-id="114ce-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="114ce-136">Se você adicionou um hub no código do servidor, verifique se todo o código do seu cliente usa a sintaxe do hub adequada.</span><span class="sxs-lookup"><span data-stu-id="114ce-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="114ce-137">**Código cliente JavaScript que cria uma Conexão Persistente em um cliente JavaScript**</span><span class="sxs-lookup"><span data-stu-id="114ce-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="114ce-138">**Código cliente JavaScript que cria um Proxy hub em um cliente Javascript**</span><span class="sxs-lookup"><span data-stu-id="114ce-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="114ce-139">**C# código do servidor que mapeia uma rota para uma Conexão Persistente**</span><span class="sxs-lookup"><span data-stu-id="114ce-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="114ce-140">**C# código de servidor que mapeia uma rota para um Hub ou para vários hubs se você tiver vários aplicativos**</span><span class="sxs-lookup"><span data-stu-id="114ce-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="114ce-141">A conexão foi iniciada antes da assinatura ser adicionada</span><span class="sxs-lookup"><span data-stu-id="114ce-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="114ce-142">Se a conexão do Hub for iniciada antes que os métodos que podem ser chamados do servidor sejam adicionados ao proxy, as mensagens não serão recebidas.</span><span class="sxs-lookup"><span data-stu-id="114ce-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="114ce-143">O seguinte código JavaScript não iniciará o hub corretamente:</span><span class="sxs-lookup"><span data-stu-id="114ce-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="114ce-144">**Código cliente JavaScript incorreto que não permitirá que mensagens do Hubs sejam recebidas**</span><span class="sxs-lookup"><span data-stu-id="114ce-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="114ce-145">Em vez disso, adicione as assinaturas do método antes de chamar Iniciar:</span><span class="sxs-lookup"><span data-stu-id="114ce-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="114ce-146">**Código cliente JavaScript que adiciona corretamente assinaturas a um hub**</span><span class="sxs-lookup"><span data-stu-id="114ce-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="114ce-147">Nome do método ausente no proxy do hub</span><span class="sxs-lookup"><span data-stu-id="114ce-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="114ce-148">Verifique se o método definido no servidor está subscrito no cliente.</span><span class="sxs-lookup"><span data-stu-id="114ce-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="114ce-149">Mesmo que o servidor defina o método, ele ainda deve ser adicionado ao proxy do cliente.</span><span class="sxs-lookup"><span data-stu-id="114ce-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="114ce-150">Os métodos podem ser adicionados ao proxy do cliente das `client` seguintes maneiras (Observe que o método é adicionado ao membro do hub, não diretamente ao hub):</span><span class="sxs-lookup"><span data-stu-id="114ce-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="114ce-151">**Código cliente JavaScript que adiciona métodos a um proxy de hub**</span><span class="sxs-lookup"><span data-stu-id="114ce-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="114ce-152">Métodos de hub ou hub não declarados como Públicos</span><span class="sxs-lookup"><span data-stu-id="114ce-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="114ce-153">Para ser visível no cliente, a implementação do `public`hub e os métodos devem ser declarados como .</span><span class="sxs-lookup"><span data-stu-id="114ce-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="114ce-154">Acessando o hub a partir de um aplicativo diferente</span><span class="sxs-lookup"><span data-stu-id="114ce-154">Accessing hub from a different application</span></span>

<span data-ttu-id="114ce-155">Os SignalR Hubs só podem ser acessados através de aplicativos que implementam clientes SignalR.</span><span class="sxs-lookup"><span data-stu-id="114ce-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="114ce-156">O SignalR não pode interoperar com outras bibliotecas de comunicação (como serviços web SOAP ou WCF.) Se não houver um cliente SignalR disponível para sua plataforma de destino, você não poderá acessar o ponto final do servidor diretamente.</span><span class="sxs-lookup"><span data-stu-id="114ce-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="114ce-157">Serialização manual de dados</span><span class="sxs-lookup"><span data-stu-id="114ce-157">Manually serializing data</span></span>

<span data-ttu-id="114ce-158">O SignalR usará automaticamente o JSON para serializar os parâmetros do seu método, não há necessidade de fazê-lo você mesmo.</span><span class="sxs-lookup"><span data-stu-id="114ce-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="114ce-159">Método do Hub remoto não executado no cliente na função OnDisconnected</span><span class="sxs-lookup"><span data-stu-id="114ce-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="114ce-160">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="114ce-160">This behavior is by design.</span></span> <span data-ttu-id="114ce-161">Quando `OnDisconnected` é chamado, o hub `Disconnected` já entrou no estado, o que não permite que outros métodos de hub sejam chamados.</span><span class="sxs-lookup"><span data-stu-id="114ce-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="114ce-162">**C# código do servidor que executa corretamente o código no evento OnDisconnected**</span><span class="sxs-lookup"><span data-stu-id="114ce-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="114ce-163">Limite de conexão atingido</span><span class="sxs-lookup"><span data-stu-id="114ce-163">Connection limit reached</span></span>

<span data-ttu-id="114ce-164">Ao usar a versão completa do IIS em um sistema operacional cliente como o Windows 7, um limite de 10 conexões é imposto.</span><span class="sxs-lookup"><span data-stu-id="114ce-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="114ce-165">Ao usar um sistema operacional cliente, use o IIS Express para evitar esse limite.</span><span class="sxs-lookup"><span data-stu-id="114ce-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="114ce-166">A conexão entre domínios não é configurada corretamente</span><span class="sxs-lookup"><span data-stu-id="114ce-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="114ce-167">Se uma conexão entre domínios (uma conexão para a qual a URL SignalR não está no mesmo domínio da página de hospedagem) não for configurada corretamente, a conexão pode falhar sem uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="114ce-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="114ce-168">Para obter informações sobre como ativar a comunicação entre [domínios, consulte Como estabelecer uma conexão entre domínios](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="114ce-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="114ce-169">Conexão usando NTLM (Active Directory) que não funciona no cliente .NET</span><span class="sxs-lookup"><span data-stu-id="114ce-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="114ce-170">Uma conexão em um aplicativo cliente .NET que usa segurança de domínio pode falhar se a conexão não estiver configurada corretamente.</span><span class="sxs-lookup"><span data-stu-id="114ce-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="114ce-171">Para usar signalR em um ambiente de domínio, defina a propriedade de conexão necessária da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="114ce-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="114ce-172">**C# código cliente que implementa credenciais de conexão**</span><span class="sxs-lookup"><span data-stu-id="114ce-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="114ce-173">Outros problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="114ce-173">Other connection issues</span></span>

<span data-ttu-id="114ce-174">Esta seção descreve as causas e soluções para sintomas específicos ou mensagens de erro que ocorrem durante uma conexão.</span><span class="sxs-lookup"><span data-stu-id="114ce-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="114ce-175">Erro "Iniciar deve ser chamado antes que os dados possam ser enviados"</span><span class="sxs-lookup"><span data-stu-id="114ce-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="114ce-176">Esse erro é comumente visto se o código faz referência a objetos SignalR antes de a conexão ser iniciada.</span><span class="sxs-lookup"><span data-stu-id="114ce-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="114ce-177">O fio para manipuladores e assim que chamará métodos definidos no servidor deve ser adicionado após a conexão ser concluída.</span><span class="sxs-lookup"><span data-stu-id="114ce-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="114ce-178">Observe que a `Start` chamada é assíncrona, portanto, o código após a chamada pode ser executado antes de ser concluída.</span><span class="sxs-lookup"><span data-stu-id="114ce-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="114ce-179">A melhor maneira de adicionar manipuladores depois que uma conexão é iniciada completamente é colocá-los em uma função de retorno de chamada que é passada como um parâmetro para o método de inicialização:</span><span class="sxs-lookup"><span data-stu-id="114ce-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="114ce-180">**JavaScript código cliente que adiciona corretamente manipuladores de eventos que referenciam objetos SignalR**</span><span class="sxs-lookup"><span data-stu-id="114ce-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="114ce-181">Esse erro também será visto se uma conexão parar enquanto os objetos SignalR ainda estiverem sendo referenciados.</span><span class="sxs-lookup"><span data-stu-id="114ce-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="114ce-182">Erro "301 movido permanentemente" ou "302 movido temporariamente"</span><span class="sxs-lookup"><span data-stu-id="114ce-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="114ce-183">Esse erro pode ser visto se o projeto contiver uma pasta chamada SignalR, que interferirá com o proxy criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="114ce-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="114ce-184">Para evitar esse erro, não `SignalR` use uma pasta chamada em seu aplicativo ou desligue a geração automática de proxy.</span><span class="sxs-lookup"><span data-stu-id="114ce-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="114ce-185">Consulte [o Proxy gerado e o que ele faz para obter](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="114ce-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="114ce-186">Erro "403 Proibido" no cliente .NET ou Silverlight</span><span class="sxs-lookup"><span data-stu-id="114ce-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="114ce-187">Esse erro pode ocorrer em ambientes entre domínios onde a comunicação entre domínios não está adequadamente ativada.</span><span class="sxs-lookup"><span data-stu-id="114ce-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="114ce-188">Para obter informações sobre como ativar a comunicação entre [domínios, consulte Como estabelecer uma conexão entre domínios](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="114ce-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="114ce-189">Para estabelecer uma conexão entre domínios em um cliente Silverlight, consulte [conexões de domínio cruzado de clientes Silverlight](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span><span class="sxs-lookup"><span data-stu-id="114ce-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="114ce-190">Erro "404 Não Encontrado"</span><span class="sxs-lookup"><span data-stu-id="114ce-190">"404 Not Found" error</span></span>

<span data-ttu-id="114ce-191">Há várias causas para este problema.</span><span class="sxs-lookup"><span data-stu-id="114ce-191">There are several causes for this issue.</span></span> <span data-ttu-id="114ce-192">Verifique tudo o que puder:</span><span class="sxs-lookup"><span data-stu-id="114ce-192">Verify all of the following:</span></span>

- <span data-ttu-id="114ce-193">**Referência de endereço proxy do hub não formatado corretamente:** Esse erro é comumente visto se a referência ao endereço proxy do hub gerado não for formatado corretamente.</span><span class="sxs-lookup"><span data-stu-id="114ce-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="114ce-194">Verifique se a referência ao endereço do hub é feita corretamente.</span><span class="sxs-lookup"><span data-stu-id="114ce-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="114ce-195">Veja [como fazer referência ao proxy gerado dinamicamente](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="114ce-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="114ce-196">**Adicionando rotas ao aplicativo antes de adicionar a rota do hub:** Se o aplicativo usar outras rotas, verifique se `MapHubs`a primeira rota adicionada é a chamada para .</span><span class="sxs-lookup"><span data-stu-id="114ce-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="114ce-197">"Erro do servidor interno 500"</span><span class="sxs-lookup"><span data-stu-id="114ce-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="114ce-198">Este é um erro muito genérico que poderia ter uma grande variedade de causas.</span><span class="sxs-lookup"><span data-stu-id="114ce-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="114ce-199">Os detalhes do erro devem aparecer no registro de eventos do servidor ou podem ser encontrados através da depuração do servidor.</span><span class="sxs-lookup"><span data-stu-id="114ce-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="114ce-200">Informações de erro mais detalhadas podem ser obtidas ligando erros detalhados no servidor.</span><span class="sxs-lookup"><span data-stu-id="114ce-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="114ce-201">Para obter mais informações, consulte [Como lidar com erros na classe Hub](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span><span class="sxs-lookup"><span data-stu-id="114ce-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="114ce-202">Erro &lt;"TypeError:&gt; hubType is indefined"</span><span class="sxs-lookup"><span data-stu-id="114ce-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="114ce-203">Este erro resultará se `MapHubs` a chamada não for feita corretamente.</span><span class="sxs-lookup"><span data-stu-id="114ce-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="114ce-204">Veja [Como registrar a rota SignalR e configurar as opções SignalR](../guide-to-the-api/hubs-api-guide-server.md#route) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="114ce-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="114ce-205">JsonSerializationException não foi tratada pelo código do usuário</span><span class="sxs-lookup"><span data-stu-id="114ce-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="114ce-206">Verifique se os parâmetros enviados aos seus métodos não incluem tipos não serializáveis (como alças de arquivo ou conexões de banco de dados).</span><span class="sxs-lookup"><span data-stu-id="114ce-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="114ce-207">Se você precisar usar membros em um objeto do lado do servidor que você não deseja ser enviado ao `JSONIgnore` cliente (seja por segurança ou por razões de serialização), use o atributo.</span><span class="sxs-lookup"><span data-stu-id="114ce-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="114ce-208">Erro de "erro de protocolo: transporte desconhecido"</span><span class="sxs-lookup"><span data-stu-id="114ce-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="114ce-209">Esse erro pode ocorrer se o cliente não suportar os transportes que o SignalR usa.</span><span class="sxs-lookup"><span data-stu-id="114ce-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="114ce-210">Consulte [Transportes e Recuos](../getting-started/introduction-to-signalr.md#transports) para obter informações sobre quais navegadores podem ser usados com o SignalR.</span><span class="sxs-lookup"><span data-stu-id="114ce-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="114ce-211">"A geração de proxy javaScript Hub foi desativada."</span><span class="sxs-lookup"><span data-stu-id="114ce-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="114ce-212">Esse erro ocorrerá `DisableJavaScriptProxies` se for definido, incluindo também uma `signalr/hubs`referência ao proxy gerado dinamicamente em .</span><span class="sxs-lookup"><span data-stu-id="114ce-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="114ce-213">Para obter mais informações sobre a criação manual do proxy, consulte [O proxy gerado e o que ele faz por você](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="114ce-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="114ce-214">"O ID de conexão está no formato incorreto" ou "A identidade do usuário não pode ser alterada durante um erro de signalr ativo"</span><span class="sxs-lookup"><span data-stu-id="114ce-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="114ce-215">Esse erro pode ser visto se a autenticação estiver sendo usada e o cliente estiver conectado antes que a conexão seja interrompida.</span><span class="sxs-lookup"><span data-stu-id="114ce-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="114ce-216">A solução é parar a conexão SignalR antes de fazer logon do cliente.</span><span class="sxs-lookup"><span data-stu-id="114ce-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="114ce-217">"Erro não capturado: SignalR: jQuery não encontrado.</span><span class="sxs-lookup"><span data-stu-id="114ce-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="114ce-218">Certifique-se de que jQuery é referenciado antes do erro do arquivo SignalR.js</span><span class="sxs-lookup"><span data-stu-id="114ce-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="114ce-219">O cliente SignalR JavaScript requer que jQuery seja executado.</span><span class="sxs-lookup"><span data-stu-id="114ce-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="114ce-220">Verifique se sua referência ao jQuery está correta, se o caminho utilizado é válido e que a referência a jQuery é anterior à referência ao SignalR.</span><span class="sxs-lookup"><span data-stu-id="114ce-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="114ce-221">Erro de "Erro de tipo&lt;&gt;não capturado: não é possível ler propriedade ' propriedade ' de erro indefinido"</span><span class="sxs-lookup"><span data-stu-id="114ce-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="114ce-222">Este erro resulta de não ter jQuery ou os hubs proxy referenciados corretamente.</span><span class="sxs-lookup"><span data-stu-id="114ce-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="114ce-223">Verifique se sua referência ao jQuery e ao proxy hubs está correta, se o caminho usado é válido e que a referência ao jQuery é anterior à referência ao proxy hubs.</span><span class="sxs-lookup"><span data-stu-id="114ce-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="114ce-224">A referência padrão ao proxy de hubs deve ser pareada com a seguinte:</span><span class="sxs-lookup"><span data-stu-id="114ce-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="114ce-225">**Código do lado do cliente HTML que faz referência correta ao proxy hubs**</span><span class="sxs-lookup"><span data-stu-id="114ce-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="114ce-226">"RuntimeBinderException não foi manipulado pelo código do usuário"</span><span class="sxs-lookup"><span data-stu-id="114ce-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="114ce-227">Este erro pode ocorrer quando `Hub.On` a sobrecarga incorreta é usada.</span><span class="sxs-lookup"><span data-stu-id="114ce-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="114ce-228">Se o método tiver um valor de retorno, o tipo de retorno deve ser especificado como um parâmetro de tipo genérico:</span><span class="sxs-lookup"><span data-stu-id="114ce-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="114ce-229">**Método definido no cliente (sem proxy gerado)**</span><span class="sxs-lookup"><span data-stu-id="114ce-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="114ce-230">O ID de conexão é inconsistente ou quebras de conexão entre cargas de página</span><span class="sxs-lookup"><span data-stu-id="114ce-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="114ce-231">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="114ce-231">This behavior is by design.</span></span> <span data-ttu-id="114ce-232">Uma vez que o objeto do hub está hospedado no objeto da página, o hub é destruído quando a página é atualizada.</span><span class="sxs-lookup"><span data-stu-id="114ce-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="114ce-233">Um aplicativo de várias páginas precisa manter a associação entre usuários e IDs de conexão para que eles sejam consistentes entre as cargas de página.</span><span class="sxs-lookup"><span data-stu-id="114ce-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="114ce-234">Os IDs de conexão podem ser `ConcurrentDictionary` armazenados no servidor em um objeto ou em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="114ce-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="114ce-235">Erro "Valor não pode ser nulo"</span><span class="sxs-lookup"><span data-stu-id="114ce-235">"Value cannot be null" error</span></span>

<span data-ttu-id="114ce-236">Os métodos do lado do servidor com parâmetros opcionais não são suportados no momento; se o parâmetro opcional for omitido, o método falhará.</span><span class="sxs-lookup"><span data-stu-id="114ce-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="114ce-237">Para obter mais informações, consulte [Parâmetros Opcionais](https://github.com/SignalR/SignalR/issues/324).</span><span class="sxs-lookup"><span data-stu-id="114ce-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="114ce-238">"Firefox não pode estabelecer uma conexão com o servidor no &lt;endereço"&gt;erro no Firebug</span><span class="sxs-lookup"><span data-stu-id="114ce-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="114ce-239">Esta mensagem de erro pode ser vista no Firebug se a negociação do transporte WebSocket falhar e outro transporte for usado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="114ce-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="114ce-240">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="114ce-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="114ce-241">"O certificado remoto é inválido de acordo com o procedimento de validação" erro no aplicativo cliente .NET</span><span class="sxs-lookup"><span data-stu-id="114ce-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="114ce-242">Se o seu servidor precisar de certificados de cliente personalizados, então você pode adicionar um certificado x509 à conexão antes que a solicitação seja feita.</span><span class="sxs-lookup"><span data-stu-id="114ce-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="114ce-243">Adicione o certificado à `Connection.AddClientCertificate`conexão usando .</span><span class="sxs-lookup"><span data-stu-id="114ce-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="114ce-244">A conexão cai após os tempos de autenticação fora</span><span class="sxs-lookup"><span data-stu-id="114ce-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="114ce-245">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="114ce-245">This behavior is by design.</span></span> <span data-ttu-id="114ce-246">As credenciais de autenticação não podem ser modificadas enquanto uma conexão estiver ativa; para atualizar credenciais, a conexão deve ser interrompida e reiniciada.</span><span class="sxs-lookup"><span data-stu-id="114ce-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="114ce-247">OnConnected é chamado duas vezes ao usar jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="114ce-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="114ce-248">A função de `initializePage` jQuery Mobile força os scripts em cada página a serem reexecutados, criando assim uma segunda conexão.</span><span class="sxs-lookup"><span data-stu-id="114ce-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="114ce-249">As soluções para este problema incluem:</span><span class="sxs-lookup"><span data-stu-id="114ce-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="114ce-250">Inclua a referência ao jQuery Mobile antes do arquivo JavaScript.</span><span class="sxs-lookup"><span data-stu-id="114ce-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="114ce-251">Desativar a `initializePage` função `$.mobile.autoInitializePage = false`configurando .</span><span class="sxs-lookup"><span data-stu-id="114ce-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="114ce-252">Aguarde que a página termine de inicializar antes de iniciar a conexão.</span><span class="sxs-lookup"><span data-stu-id="114ce-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="114ce-253">As mensagens estão atrasadas em aplicativos Silverlight usando eventos enviados pelo servidor</span><span class="sxs-lookup"><span data-stu-id="114ce-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="114ce-254">As mensagens são atrasadas ao usar eventos enviados pelo servidor no Silverlight.</span><span class="sxs-lookup"><span data-stu-id="114ce-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="114ce-255">Para forçar uma votação longa a ser usada, use o seguinte ao iniciar a conexão:</span><span class="sxs-lookup"><span data-stu-id="114ce-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="114ce-256">"Permissão negada" usando o protocolo Forever Frame</span><span class="sxs-lookup"><span data-stu-id="114ce-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="114ce-257">Esta é uma questão conhecida, descrita [aqui.](https://github.com/SignalR/SignalR/issues/1963)</span><span class="sxs-lookup"><span data-stu-id="114ce-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="114ce-258">Esse sintoma pode ser visto usando a mais recente biblioteca JQuery; a solução é fazer o downgrade do aplicativo para o JQuery 1.8.2.</span><span class="sxs-lookup"><span data-stu-id="114ce-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="114ce-259">Erros de compilação e lado do servidor</span><span class="sxs-lookup"><span data-stu-id="114ce-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="114ce-260">A seção a seguir contém possíveis soluções para erros de tempo de execução do compilador e do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="114ce-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="114ce-261">A referência à instância do Hub é nula</span><span class="sxs-lookup"><span data-stu-id="114ce-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="114ce-262">Uma vez que uma instância de hub é criada para cada conexão, você não pode criar uma instância de um hub em seu código você mesmo.</span><span class="sxs-lookup"><span data-stu-id="114ce-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="114ce-263">Para chamar métodos em um hub de fora do próprio hub, consulte [Como chamar os métodos do cliente e gerenciar grupos de fora da classe Hub](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) para obter uma referência ao contexto do hub.</span><span class="sxs-lookup"><span data-stu-id="114ce-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="114ce-264">HTTPContext.Current.Session é nulo</span><span class="sxs-lookup"><span data-stu-id="114ce-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="114ce-265">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="114ce-265">This behavior is by design.</span></span> <span data-ttu-id="114ce-266">O SignalR não suporta o estado de sessão ASP.NET, uma vez que permitir o estado da sessão quebraria as mensagens duplex.</span><span class="sxs-lookup"><span data-stu-id="114ce-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="114ce-267">Nenhum método adequado para substituir</span><span class="sxs-lookup"><span data-stu-id="114ce-267">No suitable method to override</span></span>

<span data-ttu-id="114ce-268">Você pode ver esse erro se estiver usando código de documentação ou blogs antigos.</span><span class="sxs-lookup"><span data-stu-id="114ce-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="114ce-269">Verifique se você não está fazendo referência a nomes de métodos `OnConnectedAsync`que foram alterados ou preteridos (como ).</span><span class="sxs-lookup"><span data-stu-id="114ce-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="114ce-270">HostContextExtensions.WebSocketServerUrl é nulo</span><span class="sxs-lookup"><span data-stu-id="114ce-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="114ce-271">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="114ce-271">This behavior is by design.</span></span> <span data-ttu-id="114ce-272">Este membro é preterido e não deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="114ce-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="114ce-273">"Um erro de "signalr.hubs" já está na coleção de rotas</span><span class="sxs-lookup"><span data-stu-id="114ce-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="114ce-274">Este erro será `MapHubs` visto se for chamado duas vezes pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="114ce-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="114ce-275">Alguns exemplos `MapHubs` de aplicativos chamam diretamente no arquivo global do aplicativo; outros fazem a chamada em uma aula de invólucro.</span><span class="sxs-lookup"><span data-stu-id="114ce-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="114ce-276">Certifique-se de que sua aplicação não faça as duas coisas.</span><span class="sxs-lookup"><span data-stu-id="114ce-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="114ce-277">Problemas do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="114ce-277">Visual Studio issues</span></span>

<span data-ttu-id="114ce-278">Esta seção descreve problemas encontrados no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114ce-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="114ce-279">O nó script documents não aparece no Solution Explorer</span><span class="sxs-lookup"><span data-stu-id="114ce-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="114ce-280">Alguns de nossos tutoriais direcionam você para o nó "Script Documents" no Solution Explorer durante a depuração.</span><span class="sxs-lookup"><span data-stu-id="114ce-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="114ce-281">Este nó é produzido pelo depurador JavaScript e só aparecerá durante a depuração de clientes do navegador no Internet Explorer; o nó não aparecerá se o Chrome ou o Firefox forem usados.</span><span class="sxs-lookup"><span data-stu-id="114ce-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="114ce-282">O depurador JavaScript também não será executado se outro depurador de cliente estiver sendo executado, como o depurador Silverlight.</span><span class="sxs-lookup"><span data-stu-id="114ce-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="114ce-283">SignalR não funciona no Visual Studio 2008 ou anterior</span><span class="sxs-lookup"><span data-stu-id="114ce-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="114ce-284">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="114ce-284">This behavior is by design.</span></span> <span data-ttu-id="114ce-285">SignalR requer .NET Framework 4 ou posterior; isso requer que os aplicativos SignalR sejam desenvolvidos no Visual Studio 2010 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="114ce-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="114ce-286">Questões do IIS</span><span class="sxs-lookup"><span data-stu-id="114ce-286">IIS issues</span></span>

<span data-ttu-id="114ce-287">Esta seção contém problemas com os Serviços de Informação da Internet.</span><span class="sxs-lookup"><span data-stu-id="114ce-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="114ce-288">Site falha após chamada do MapHubs</span><span class="sxs-lookup"><span data-stu-id="114ce-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="114ce-289">Este problema foi corrigido na versão mais recente do SignalR.</span><span class="sxs-lookup"><span data-stu-id="114ce-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="114ce-290">Verifique se você está usando a versão mais recente lançada do SignalR atualizando sua instalação usando nuGet.</span><span class="sxs-lookup"><span data-stu-id="114ce-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="114ce-291">Problemas do Azure</span><span class="sxs-lookup"><span data-stu-id="114ce-291">Azure issues</span></span>

<span data-ttu-id="114ce-292">Esta seção contém problemas com o Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="114ce-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="114ce-293">As mensagens não são recebidas através do backplane do Azure depois de alterar nomes de tópicos</span><span class="sxs-lookup"><span data-stu-id="114ce-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="114ce-294">Os tópicos usados pelo backplane do Azure não se destinam a ser configuráveis pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="114ce-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
