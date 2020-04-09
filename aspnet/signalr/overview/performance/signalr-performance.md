---
uid: signalr/overview/performance/signalr-performance
title: Desempenho do Sinalizador | Microsoft Docs
author: bradygaster
description: Desempenho do SignalR
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676086"
---
# <a name="signalr-performance"></a><span data-ttu-id="fa8ac-103">Desempenho do SignalR</span><span class="sxs-lookup"><span data-stu-id="fa8ac-103">SignalR Performance</span></span>

<span data-ttu-id="fa8ac-104">por [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="fa8ac-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="fa8ac-105">Este tópico descreve como projetar, medir e melhorar o desempenho em um aplicativo SignalR.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="fa8ac-106">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="fa8ac-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="fa8ac-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="fa8ac-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="fa8ac-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="fa8ac-108">.NET 4.5</span></span>
> - <span data-ttu-id="fa8ac-109">SignalR versão 2</span><span class="sxs-lookup"><span data-stu-id="fa8ac-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="fa8ac-110">Versões anteriores deste tópico</span><span class="sxs-lookup"><span data-stu-id="fa8ac-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="fa8ac-111">Para obter informações sobre versões anteriores do SignalR, consulte [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="fa8ac-112">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="fa8ac-112">Questions and comments</span></span>
>
> <span data-ttu-id="fa8ac-113">Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="fa8ac-114">Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="fa8ac-115">Para uma apresentação recente sobre desempenho e dimensionamento signalR, consulte [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="fa8ac-116">Este tópico contém as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="fa8ac-117">Considerações sobre o design</span><span class="sxs-lookup"><span data-stu-id="fa8ac-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="fa8ac-118">Ajuste do servidor SignalR para desempenho</span><span class="sxs-lookup"><span data-stu-id="fa8ac-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="fa8ac-119">Solucionando problemas de desempenho</span><span class="sxs-lookup"><span data-stu-id="fa8ac-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="fa8ac-120">Usando contadores de desempenho SignalR</span><span class="sxs-lookup"><span data-stu-id="fa8ac-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="fa8ac-121">Usando outros contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="fa8ac-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="fa8ac-122">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="fa8ac-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="fa8ac-123">Considerações sobre o design</span><span class="sxs-lookup"><span data-stu-id="fa8ac-123">Design considerations</span></span>

<span data-ttu-id="fa8ac-124">Esta seção descreve padrões que podem ser implementados durante o projeto de um aplicativo SignalR, para garantir que o desempenho não esteja sendo prejudicado gerando tráfego de rede desnecessário.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="fa8ac-125">Freqüência de mensagem de estrangulamento</span><span class="sxs-lookup"><span data-stu-id="fa8ac-125">Throttling message frequency</span></span>

<span data-ttu-id="fa8ac-126">Mesmo em um aplicativo que envia mensagens em alta frequência (como um aplicativo de jogos em tempo real), a maioria dos aplicativos não precisa enviar mais do que algumas mensagens por segundo.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="fa8ac-127">Para reduzir a quantidade de tráfego que cada cliente gera, um loop de mensagem pode ser implementado que faz filas e envia mensagens não com mais freqüência do que uma taxa fixa (ou seja, até um certo número de mensagens serão enviadas a cada segundo, se houver mensagens nesse intervalo de tempo a serem enviadas).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="fa8ac-128">Para obter um aplicativo de exemplo que estrangule as mensagens a uma determinada taxa (tanto do cliente quanto do servidor), consulte [Tempo Real de Alta Frequência com SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="fa8ac-129">Reduzindo o tamanho da mensagem</span><span class="sxs-lookup"><span data-stu-id="fa8ac-129">Reducing message size</span></span>

<span data-ttu-id="fa8ac-130">Você pode reduzir o tamanho de uma mensagem SignalR reduzindo o tamanho de seus objetos serializados.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="fa8ac-131">No código do servidor, se você estiver enviando um objeto que contém propriedades que não precisam `JsonIgnore` ser transmitidas, evite que essas propriedades sejam serializadas usando o atributo.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="fa8ac-132">Os nomes das propriedades também são armazenados na mensagem; os nomes das propriedades podem `JsonProperty` ser encurtados usando o atributo.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="fa8ac-133">A amostra de código a seguir demonstra como excluir uma propriedade de ser enviada ao cliente e como encurtar os nomes da propriedade:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="fa8ac-134">**Código do servidor .NET que demonstra o atributo JsonIgnore para excluir dados de serem enviados ao cliente e o atributo JsonProperty para reduzir o tamanho da mensagem**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="fa8ac-135">Para manter a legibilidade/manutenção no código do cliente, os nomes de propriedade abreviados podem ser remapeados para nomes amigáveis ao homem após o recebimento da mensagem.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="fa8ac-136">A amostra de código a seguir demonstra uma maneira possível de remapear nomes encurtados `reMap` para nomes mais longos, definindo um contrato de mensagem (mapeamento) e usando a função para aplicar o contrato à classe de mensagem otimizada:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="fa8ac-137">**Código JavaScript do lado do cliente que remapeia nomes de propriedades encurtados para nomes leíveis por humanos**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="fa8ac-138">Os nomes podem ser encurtados em mensagens do cliente para o servidor também, usando o mesmo método.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="fa8ac-139">Reduzir a pegada de memória (ou seja, a quantidade de memória usada para a mensagem) do objeto de mensagem também pode melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="fa8ac-140">Por exemplo, se a `int` gama completa de `short` `byte` um não for necessária, um ou pode ser usado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="fa8ac-141">Uma vez que as mensagens são armazenadas no barramento de mensagens na memória do servidor, a redução do tamanho das mensagens também pode resolver problemas de memória do servidor.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="fa8ac-142">Ajuste do servidor SignalR para desempenho</span><span class="sxs-lookup"><span data-stu-id="fa8ac-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="fa8ac-143">As seguintes configurações podem ser usadas para ajustar seu servidor para obter melhor desempenho em um aplicativo SignalR.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="fa8ac-144">Para obter informações gerais sobre como melhorar o desempenho em um aplicativo ASP.NET, consulte [Melhorar o desempenho ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="fa8ac-145">**Configurações de configuração SignalR**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="fa8ac-146">**DefaultMessageBufferSize**: Por padrão, o SignalR retém 1000 mensagens na memória por hub por conexão.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="fa8ac-147">Se grandes mensagens estiverem sendo usadas, isso pode criar problemas de memória que podem ser aliviados pela redução desse valor.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="fa8ac-148">Essa configuração pode `Application_Start` ser definida no manipulador de `Configuration` eventos em um aplicativo ASP.NET ou no método de uma classe de inicialização OWIN em um aplicativo auto-hospedado.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="fa8ac-149">A amostra a seguir demonstra como reduzir esse valor para reduzir a pegada de memória do seu aplicativo, a fim de reduzir a quantidade de memória do servidor usada:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="fa8ac-150">**Código do servidor .NET em Startup.cs para diminuir o tamanho padrão do buffer de mensagens**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="fa8ac-151">**Configurações de configuração do IIS**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="fa8ac-152">**Solicitações simultâneas máximas por aplicativo**: O aumento do número de solicitações simultâneas de IIS aumentará os recursos do servidor disponíveis para atender às solicitações.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="fa8ac-153">O valor padrão é 5000; para aumentar essa configuração, execute os seguintes comandos em um prompt de comando elevado:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="fa8ac-154">**Queue de pool de aplicativos**: Este é o número máximo de solicitações que http.sys filas para o pool de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="fa8ac-155">Quando a fila está cheia, novas solicitações recebem uma resposta 503 "Service Indisponível".</span><span class="sxs-lookup"><span data-stu-id="fa8ac-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="fa8ac-156">O valor padrão é 1000.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-156">The default value is 1000.</span></span>

    <span data-ttu-id="fa8ac-157">Reduzir o comprimento da fila para o processo do trabalhador no pool de aplicativos que hospeda seu aplicativo conservará recursos de memória.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="fa8ac-158">Para obter mais informações, consulte [Gerenciar, ajustar e configurar pools de aplicativos](https://technet.microsoft.com/library/cc745955.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="fa8ac-159">**configurações de configuração ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="fa8ac-160">Esta seção inclui configurações que podem `aspnet.config` ser definidas no arquivo.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="fa8ac-161">Este arquivo é encontrado em um dos dois locais, dependendo da plataforma:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="fa8ac-162">ASP.NET configurações que podem melhorar o desempenho do SignalR incluem as seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="fa8ac-163">**Máximo de solicitações simultâneas por CPU**: O aumento dessa configuração pode aliviar gargalos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="fa8ac-164">Para aumentar essa configuração, adicione `aspnet.config` a seguinte configuração ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="fa8ac-165">**Limite de fila de solicitação**: Quando o `maxConcurrentRequestsPerCPU` número total de conexões exceder a configuração, ASP.NET iniciarão o estrangulamento de solicitações usando uma fila.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="fa8ac-166">Para aumentar o tamanho da fila, `requestQueueLimit` você pode aumentar a configuração.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="fa8ac-167">Para fazer isso, adicione a `processModel` seguinte configuração ao nó em (em `config/machine.config` vez de `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="fa8ac-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="fa8ac-168">Solucionando problemas de desempenho</span><span class="sxs-lookup"><span data-stu-id="fa8ac-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="fa8ac-169">Esta seção descreve maneiras de encontrar gargalos de desempenho em sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="fa8ac-170">Verificando se o WebSocket está sendo usado</span><span class="sxs-lookup"><span data-stu-id="fa8ac-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="fa8ac-171">Embora o SignalR possa usar uma variedade de transportes para comunicação entre cliente e servidor, o WebSocket oferece uma vantagem de desempenho significativa, e deve ser usado se o cliente e o servidor o suportarem.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="fa8ac-172">Para determinar se seu cliente e servidor atendem aos requisitos do WebSocket, consulte [Transportes e Recus](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="fa8ac-173">Para determinar qual transporte está sendo usado em seu aplicativo, você pode usar as ferramentas do desenvolvedor do navegador e examinar os logs para ver qual transporte está sendo usado para a conexão.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="fa8ac-174">Para obter informações sobre o uso das ferramentas de desenvolvimento do navegador no Internet Explorer e no Chrome, consulte [Transportes e Recuos](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="fa8ac-175">Usando contadores de desempenho SignalR</span><span class="sxs-lookup"><span data-stu-id="fa8ac-175">Using SignalR performance counters</span></span>

<span data-ttu-id="fa8ac-176">Esta seção descreve como ativar e usar contadores de `Microsoft.AspNet.SignalR.Utils` desempenho SignalR, encontrados no pacote.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="fa8ac-177">Instalando signalr.exe</span><span class="sxs-lookup"><span data-stu-id="fa8ac-177">Installing signalr.exe</span></span>

<span data-ttu-id="fa8ac-178">Contadores de desempenho podem ser adicionados ao servidor usando um utilitário chamado SignalR.exe.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="fa8ac-179">Para instalar este utilitário, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="fa8ac-180">No Visual Studio, selecione **Ferramentas** > **NuGet Package Manager** > **Gerencie pacotes NuGet para solução**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="fa8ac-181">Procure **signalr.utils**e selecione Instalar.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="fa8ac-182">Aceite o contrato de licença para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="fa8ac-183">SignalR.exe será instalado `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`para .</span><span class="sxs-lookup"><span data-stu-id="fa8ac-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="fa8ac-184">Instalando contadores de desempenho com SignalR.exe</span><span class="sxs-lookup"><span data-stu-id="fa8ac-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="fa8ac-185">Para instalar contadores de desempenho SignalR, execute SignalR.exe em um prompt de comando elevado com o seguinte parâmetro:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="fa8ac-186">Para remover os contadores de desempenho signalR, execute SignalR.exe em um prompt de comando elevado com o seguinte parâmetro:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="fa8ac-187">Contadores de desempenho signalR</span><span class="sxs-lookup"><span data-stu-id="fa8ac-187">SignalR Performance counters</span></span>

<span data-ttu-id="fa8ac-188">O pacote de utilitários instala os seguintes contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="fa8ac-189">Os contadores "Total" medem o número de eventos desde a última reinicialização do pool de aplicativos ou do servidor.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="fa8ac-190">**Métricas de conexão**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-190">**Connection metrics**</span></span>

<span data-ttu-id="fa8ac-191">As seguintes métricas medem os eventos de vida de conexão que ocorrem.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="fa8ac-192">Para obter mais informações, consulte [Compreensão e manipulação de eventos vitalícios de conexão](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="fa8ac-193">**Conexões conectadas**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-193">**Connections Connected**</span></span>
- <span data-ttu-id="fa8ac-194">**Conexões reconectadas**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="fa8ac-195">**Conexões desconectadas**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="fa8ac-196">**Corrente de conexões**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-196">**Connections Current**</span></span>

<span data-ttu-id="fa8ac-197">**Métricas de mensagens**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-197">**Message metrics**</span></span>

<span data-ttu-id="fa8ac-198">As seguintes métricas medem o tráfego de mensagens gerado pelo SignalR.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="fa8ac-199">**Mensagens de conexão recebidas total**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="fa8ac-200">**Mensagens de conexão enviadas total**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="fa8ac-201">**Mensagens de conexão recebidas/seg**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="fa8ac-202">**Mensagens de conexão enviadas/sec**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="fa8ac-203">**Métricas do barramento de mensagens**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-203">**Message bus metrics**</span></span>

<span data-ttu-id="fa8ac-204">As seguintes métricas medem o tráfego através do barramento de mensagens do SignalR interno, a fila na qual todas as mensagens SignalR de entrada e saída são colocadas.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="fa8ac-205">Uma mensagem é **publicada** quando é enviada ou transmitida.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="fa8ac-206">Um **Assinante** neste contexto é uma assinatura no ônibus de mensagens; isso deve igualar o número de clientes mais o próprio servidor.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="fa8ac-207">Um **Trabalhador Alocado** é um componente que envia dados para conexões ativas; um **Trabalhador Ocupado** é aquele que está enviando ativamente uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="fa8ac-208">**Mensagens de ônibus recebidas total**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="fa8ac-209">**Menção menção mensagens mensagens recebidas/seg**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="fa8ac-210">**Mensagens de ônibus de mensagens publicadas total**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="fa8ac-211">**Mensagens de ônibus publicadas/seg**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="fa8ac-212">**Assinantes de ônibus de mensagem atuais**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="fa8ac-213">**Assinantes de ônibus de mensagem Total**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="fa8ac-214">**Assinantes de ônibus de mensagem/Sec**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="fa8ac-215">**Trabalhadores alocados no ônibus de mensagem**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="fa8ac-216">**Trabalhadores ocupados de ônibus de mensagem**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="fa8ac-217">**Tópicos de barra de mensagens atuais**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="fa8ac-218">**Métricas de erro**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-218">**Error metrics**</span></span>

<span data-ttu-id="fa8ac-219">As seguintes métricas medem erros gerados pelo tráfego de mensagens SignalR.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="fa8ac-220">**Erros de resolução do hub** ocorrem quando um método de hub ou hub não pode ser resolvido.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="fa8ac-221">**Erros de invocação do Hub** são exceções lançadas ao invocar um método de hub.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="fa8ac-222">**Erros de transporte** são erros de conexão lançados durante uma solicitação ou resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="fa8ac-223">**Erros: Todo total**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-223">**Errors: All Total**</span></span>
- <span data-ttu-id="fa8ac-224">**Erros: All/Sec**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="fa8ac-225">**Erros: Centro de Resolução Total**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="fa8ac-226">**Erros: Resolução do Hub/Seg**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="fa8ac-227">**Erros: Total de Invocação do Hub**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="fa8ac-228">**Erros: Invocação do Hub/Sec**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="fa8ac-229">**Erros: Total de transporte**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="fa8ac-230">**Erros: Transporte/Seg**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="fa8ac-231">**Métricas de scaleout**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-231">**Scaleout metrics**</span></span>

<span data-ttu-id="fa8ac-232">As seguintes métricas medem o tráfego e os erros gerados pelo provedor de scaleout.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="fa8ac-233">Um **Fluxo** neste contexto é uma unidade de escala usada pelo provedor de scaleout; esta é uma tabela se o SQL Server for usado, um Tópico se o Service Bus for usado e uma Assinatura se Redis for usado.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="fa8ac-234">Cada fluxo garante operações ordenadas de leitura e gravação; um único fluxo é um gargalo de escala potencial, de modo que o número de fluxos pode ser aumentado para ajudar a reduzir esse gargalo.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="fa8ac-235">Se vários fluxos forem usados, o SignalR distribuirá automaticamente (fragmentos) mensagens através desses fluxos de forma a garantir que as mensagens enviadas de qualquer conexão estejam em ordem.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="fa8ac-236">A configuração [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) controla o comprimento da fila de envio de escala mantida pelo SignalR.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="fa8ac-237">Configurá-lo para um valor maior que 0 colocará todas as mensagens em uma fila de envio para serem enviadas uma de cada vez para o backplane de mensagens configurada.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="fa8ac-238">Se o tamanho da fila estiver acima do comprimento configurado, as chamadas subseqüentes a serem enviadas falharão imediatamente com uma [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) até que o número de mensagens na fila seja menor do que a configuração novamente.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="fa8ac-239">A fila é desativada por padrão porque os backplanes implementados geralmente têm sua própria fila ou controle de fluxo no local.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="fa8ac-240">No caso do SQL Server, o pool de conexões limita efetivamente o número de envios acontecendo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="fa8ac-241">Por padrão, apenas um fluxo é usado para SQL Server e Redis, cinco fluxos são usados para Barra de Serviço e a fila está desativada, mas essas configurações podem ser alteradas através da configuração no SQL Server and Service Bus:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="fa8ac-242">**.NET Server Code para configurar a contagem de tabelas e o comprimento da fila para o backplane do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="fa8ac-243">**.NET Server Code para configurar a contagem de tópicos e o comprimento da fila para o backplane do Service Bus**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="fa8ac-244">Um **fluxo de buffer** é aquele que entrou em um estado defeituoso; quando o fluxo estiver no estado defeituoso, todas as mensagens enviadas para o backplane falharão imediatamente até que o fluxo não esteja mais falhando.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="fa8ac-245">O **Comprimento da Fila de Envio** é o número de mensagens que foram postadas, mas ainda não enviadas.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="fa8ac-246">**Mensagens de menção de escala recebidas/seg**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="fa8ac-247">**Fluxos de scaleout total**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="fa8ac-248">**Fluxos scaleout abertos**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="fa8ac-249">**Buffering de fluxos de scaleout**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="fa8ac-250">**Total de erros de scaleout**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="fa8ac-251">**Erros de escala/sec**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="fa8ac-252">**Comprimento da fila de envio de scaleout**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="fa8ac-253">Para obter mais informações sobre o que esses contadores estão medindo, consulte [SignalR Scaleout com a Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="fa8ac-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="fa8ac-254">Usando outros contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="fa8ac-254">Using other performance counters</span></span>

<span data-ttu-id="fa8ac-255">Os seguintes contadores de desempenho também podem ser úteis para monitorar o desempenho do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="fa8ac-256">**Memória**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-256">**Memory**</span></span>

- <span data-ttu-id="fa8ac-257">.NET CLR\\Memory # bytes em todos os Heaps (para w3wp)</span><span class="sxs-lookup"><span data-stu-id="fa8ac-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="fa8ac-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-258">**ASP.NET**</span></span>

- <span data-ttu-id="fa8ac-259">ASP.NET\Solicitações atuais</span><span class="sxs-lookup"><span data-stu-id="fa8ac-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="fa8ac-260">ASP.NET\Fila</span><span class="sxs-lookup"><span data-stu-id="fa8ac-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="fa8ac-261">ASP.NET\Rejeitado</span><span class="sxs-lookup"><span data-stu-id="fa8ac-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="fa8ac-262">**Cpu**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-262">**CPU**</span></span>

- <span data-ttu-id="fa8ac-263">Informações do processador\Tempo do processador</span><span class="sxs-lookup"><span data-stu-id="fa8ac-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="fa8ac-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-264">**TCP/IP**</span></span>

- <span data-ttu-id="fa8ac-265">TCPv6/Conexões Estabelecidas</span><span class="sxs-lookup"><span data-stu-id="fa8ac-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="fa8ac-266">TCPv4/Conexões Estabelecidas</span><span class="sxs-lookup"><span data-stu-id="fa8ac-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="fa8ac-267">**Serviço web**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-267">**Web Service**</span></span>

- <span data-ttu-id="fa8ac-268">Serviço web\conexões atuais</span><span class="sxs-lookup"><span data-stu-id="fa8ac-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="fa8ac-269">Serviço web\Conexões máximas</span><span class="sxs-lookup"><span data-stu-id="fa8ac-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="fa8ac-270">**Threading**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-270">**Threading**</span></span>

- <span data-ttu-id="fa8ac-271">.NET CLR Locks\\and Threads # dos tópicos lógicos atuais</span><span class="sxs-lookup"><span data-stu-id="fa8ac-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="fa8ac-272">.NET CLR Locks\\and Threads # dos threads físicos atuais</span><span class="sxs-lookup"><span data-stu-id="fa8ac-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="fa8ac-273">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="fa8ac-273">Other Resources</span></span>

<span data-ttu-id="fa8ac-274">Para obter mais informações sobre ASP.NET monitoramento e ajuste de desempenho, consulte os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="fa8ac-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="fa8ac-275">[Visão geral do desempenho do ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="fa8ac-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="fa8ac-276">ASP.NET o uso do thread no IIS 7.5, IIS 7.0 e IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="fa8ac-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="fa8ac-277">&lt;aplicativoElemento&gt; pool (Configurações da Web)</span><span class="sxs-lookup"><span data-stu-id="fa8ac-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
