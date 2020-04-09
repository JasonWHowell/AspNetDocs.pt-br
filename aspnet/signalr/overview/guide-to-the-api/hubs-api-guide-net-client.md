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
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET SignalR Hubs API Guide - .NET Client (C#)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este documento fornece uma introdução ao uso da API hubs para clientes SignalR versão 2 em clientes .NET, como Windows Store (WinRT), WPF, Silverlight e aplicativos de console.
>
> A API SignalR Hubs permite que você faça chamadas de procedimento remoto (RPCs) de um servidor para clientes conectados e de clientes para o servidor. No código do servidor, você define métodos que podem ser chamados pelos clientes e você chama métodos que são executados no cliente. No código do cliente, você define métodos que podem ser chamados do servidor e você chama métodos que são executados no servidor. O SignalR cuida de todo o encanamento cliente-servidor para você.
>
> SignalR também oferece uma API de nível inferior chamada Conexões Persistentes. Para uma introdução ao SignalR, Hubs e Persistent Connections, ou para um tutorial que mostra como construir um aplicativo SignalR completo, consulte [SignalR - Getting Started](../getting-started/index.md).
>
> ## <a name="software-versions-used-in-this-topic"></a>Versões de software usadas neste tópico
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR versão 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Versões anteriores deste tópico
>
> Para obter informações sobre versões anteriores do SignalR, consulte [SignalR Older Versions](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Perguntas e comentários
>
> Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página. Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Visão geral

Este documento contém as seguintes seções:

- [Configuração do cliente](#clientsetup)
- [Como estabelecer uma conexão](#establishconnection)

    - [Conexões entre domínios de clientes Silverlight](#slcrossdomain)
- [Como configurar a conexão](#configureconnection)

    - [Como definir o número máximo de conexões simultâneas em clientes WPF](#maxconnections)
    - [Como especificar parâmetros de seqüência de consultas](#querystring)
    - [Como especificar o método de transporte](#transport)
    - [Como especificar cabeçalhos HTTP](#httpheaders)
    - [Como especificar certificados de cliente](#clientcertificate)
- [Como criar o proxy do Hub](#proxy)
- [Como definir métodos no cliente que o servidor pode chamar](#callclient)

    - [Métodos sem parâmetros](#clientmethodswithoutparms)
    - [Métodos com parâmetros, especificando tipos de parâmetros](#clientmethodswithparmtypes)
    - [Métodos com parâmetros, especificando objetos dinâmicos para os parâmetros](#clientmethodswithdynamparms)
    - [Como remover um manipulador](#removehandler)
- [Como chamar métodos de servidor do cliente](#callserver)
- [Como lidar com eventos de vida de conexão](#connectionlifetime)
- [Como lidar com erros](#handleerrors)
- [Como habilitar o registro do lado do cliente](#logging)
- [Amostras de código de aplicativo WPF, Silverlight e console para métodos de cliente que o servidor pode chamar](#wpfsl)

Para obter uma amostra de projetos de clientes .NET, consulte os seguintes recursos:

- [gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) em GitHub.com (WinRT, Silverlight, exemplos de aplicativos de console).
- [DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (exemplo WPF).
- [SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (exemplo do aplicativo console).

Para obter a documentação sobre como programar os clientes servidor ou JavaScript, consulte os seguintes recursos:

- [SignalR Hubs Guia de API - Servidor](hubs-api-guide-server.md)
- [SignalR Hubs API Guide - JavaScript Client](hubs-api-guide-javascript-client.md)

Os links para tópicos de referência da API são para a versão .NET 4.5 da API. Se você estiver usando .NET 4, consulte [a versão .NET 4 dos tópicos da API](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="clientsetup"></a>

## <a name="client-setup"></a>Configuração do cliente

Instale o pacote [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet (não o pacote [Microsoft.AspNet.SignalR).](http://nuget.org/packages/microsoft.aspnet.signalr) Este pacote suporta clientes WinRT, Silverlight, WPF, console e Windows Phone, tanto para clientes .NET 4 quanto .NET 4.5.

Se a versão do SignalR que você tem no cliente for diferente da versão que você tem no servidor, o SignalR muitas vezes é capaz de se adaptar à diferença. Por exemplo, um servidor executando o SignalR versão 2 suportará clientes que tenham 1.1.x instalado, bem como clientes que tenham a versão 2 instalada. Se a diferença entre a versão no servidor e a versão no cliente for muito grande, ou `InvalidOperationException` se o cliente for mais recente que o servidor, o SignalR abre uma exceção quando o cliente tenta estabelecer uma conexão. A mensagem`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`de erro é " ".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Como estabelecer uma conexão

Antes de estabelecer uma conexão, `HubConnection` você tem que criar um objeto e criar um proxy. Para estabelecer a conexão, chame o `Start` método no `HubConnection` objeto.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> Para clientes JavaScript, você tem que registrar `Start` pelo menos um manipulador de eventos antes de chamar o método para estabelecer a conexão. Isso não é necessário para clientes .NET. Para clientes JavaScript, o código proxy gerado cria automaticamente proxies para todos os Hubs existentes no servidor, e registrar um manipulador é como você indica quais Hubs seu cliente pretende usar. Mas para um cliente .NET você cria proxies hub manualmente, então o SignalR assume que você estará usando qualquer Hub para o que você criar um proxy.

O código de exemplo usa a URL padrão "/signalr" para se conectar ao serviço SignalR. Para obter informações sobre como especificar uma URL base diferente, consulte [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).

O `Start` método é executado de forma assíncrona. Para garantir que as linhas de código subseqüentes não executem até que a conexão seja estabelecida, use `await` em um método assíncrono de ASP.NET 4,5 ou `.Wait()` em um método síncrono. Não use `.Wait()` em um cliente WinRT.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Conexões entre domínios de clientes Silverlight

Para obter informações sobre como habilitar conexões entre domínios de clientes Silverlight, consulte [Tornando um serviço disponível através dos limites do domínio](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Como configurar a conexão

Antes de estabelecer uma conexão, você pode especificar qualquer uma das seguintes opções:

- Limite de conexões simultâneas.
- Parâmetros da seqüência de consultas.
- O método de transporte.
- Cabeçalhos HTTP.
- Certificados de cliente.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>Como definir o número máximo de conexões simultâneas em clientes WPF

Em clientes WPF, você pode ter que aumentar o número máximo de conexões simultâneas do seu valor padrão de 2. O valor recomendado é 10.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

Para obter mais informações, consulte [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Como especificar parâmetros de seqüência de consultas

Se você quiser enviar dados para o servidor quando o cliente se conectar, você pode adicionar parâmetros de seqüência de consulta ao objeto de conexão. O exemplo a seguir mostra como definir um parâmetro de seqüência de consultas no código do cliente.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

O exemplo a seguir mostra como ler um parâmetro de seqüência de consultas no código do servidor.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Como especificar o método de transporte

Como parte do processo de conexão, um cliente SignalR normalmente negocia com o servidor para determinar o melhor transporte que é suportado tanto pelo servidor quanto pelo cliente. Se você já sabe qual transporte deseja usar, você pode contornar esse processo de negociação. Para especificar o método de transporte, passe em um objeto de transporte para o método Iniciar. O exemplo a seguir mostra como especificar o método de transporte no código do cliente.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

O espaço de nome [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) inclui as seguintes classes que você pode usar para especificar o transporte.

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Disponível apenas quando o servidor e o cliente usam .NET 4.5.)
- [AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (escolhe automaticamente o melhor transporte que é suportado pelo cliente e pelo servidor. Este é o transporte padrão. Passar isso para `Start` o método tem o mesmo efeito de não passar em nada.)

O transporte ForeverFrame não está incluído nesta lista porque é usado apenas por navegadores.

Para obter informações sobre como verificar o método de transporte no código do servidor, consulte [ASP.NET SignalR Hubs API Guide - Server - Como obter informações sobre o cliente a partir da propriedade Context](hubs-api-guide-server.md#contextproperty). Para obter mais informações sobre transportes e recuos, consulte [Introdução ao SignalR - Transportes e Recuos](../getting-started/introduction-to-signalr.md#transports).

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>Como especificar cabeçalhos HTTP

Para definir cabeçalhos `Headers` HTTP, use a propriedade no objeto de conexão. O exemplo a seguir mostra como adicionar um cabeçalho HTTP.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>Como especificar certificados de cliente

Para adicionar certificados de `AddClientCertificate` cliente, use o método no objeto de conexão.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>Como criar o proxy do Hub

Para definir métodos no cliente que um Hub pode ligar do servidor e invocar métodos em um Hub `CreateHubProxy` no servidor, crie um proxy para o Hub, chamando o objeto de conexão. A seqüência `CreateHubProxy` de seqüência para a qual você passa `HubName` é o nome da sua classe Hub ou o nome especificado pelo atributo se um foi usado no servidor. A correspondência de nome não diferencia maiúsculas de minúsculas.

**Classe hub no servidor**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**Crie proxy de cliente para a classe Hub**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

Se você decorar sua classe `HubName` Hub com um atributo, use esse nome.

**Classe hub no servidor**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**Crie proxy de cliente para a classe Hub**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

Se você `HubConnection.CreateHubProxy` ligar várias `hubName`vezes com o `IHubProxy` mesmo, você terá o mesmo objeto armazenado em cache.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Como definir métodos no cliente que o servidor pode chamar

Para definir um método que o servidor pode `On` chamar, use o método do proxy para registrar um manipulador de eventos.

A correspondência do nome do método é insensível ao caso. Por `Clients.All.UpdateStockPrice` exemplo, no servidor `updateStockPrice` `updatestockprice`executará `UpdateStockPrice` , ou no cliente.

Diferentes plataformas cliente têm requisitos diferentes para como você escreve código de método para atualizar a ui. Os exemplos mostrados são para clientes WinRT (Windows Store .NET). Exemplos de aplicativos WPF, Silverlight e console são fornecidos em [uma seção separada mais tarde neste tópico](#wpfsl).

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>Métodos sem parâmetros

Se o método que você está manipulando não tiver parâmetros, use a sobrecarga não genérica do `On` método:

**Método cliente de chamada de código de servidor sem parâmetros**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**Código do Cliente WinRT para método chamado de servidor sem[parâmetros (veja exemplos WPF e Silverlight mais tarde neste tópico)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Métodos com parâmetros, especificando os tipos de parâmetros

Se o método que você está manipulando tiver parâmetros, especifique os tipos dos parâmetros como os tipos genéricos do `On` método. Existem sobrecargas genéricas do `On` método para permitir que você especifique até 8 parâmetros (4 no Windows Phone 7). No exemplo a seguir, um parâmetro `UpdateStockPrice` é enviado para o método.

**Método de chamada de código do servidor com um parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**A classe Stock usada para o parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**Código do Cliente WinRT para um método chamado de servidor com um parâmetro[(veja exemplos WPF e Silverlight mais tarde neste tópico)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Métodos com parâmetros, especificando objetos dinâmicos para os parâmetros

Como alternativa à especificação de parâmetros como tipos genéricos do `On` método, você pode especificar parâmetros como objetos dinâmicos:

**Método de chamada de código do servidor com um parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**A classe Stock usada para o parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**Código cliente WinRT para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro[(veja exemplos WPF e Silverlight mais tarde neste tópico](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>Como remover um manipulador

Para remover um manipulador, chame seu `Dispose` método.

**Código do cliente para um método chamado de servidor**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**Código do cliente para remover o manipulador**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Como chamar métodos de servidor do cliente

Para chamar um método no `Invoke` servidor, use o método no proxy do Hub.

Se o método do servidor não tiver valor de `Invoke` retorno, use a sobrecarga não genérica do método.

**Código do servidor para um método que não tem valor de retorno**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**Código do cliente chamando um método que não tem valor de retorno**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

Se o método do servidor tiver um valor de retorno, especifique o tipo de retorno como o tipo genérico do `Invoke` método.

**Código do servidor para um método que tem um valor de retorno e leva um parâmetro de tipo complexo**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**A classe stock usada para o parâmetro e o valor de retorno**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**Código do cliente chamando um método que tem um valor de retorno e leva um parâmetro de tipo complexo, em um método de sincronização de ASP.NET 4.5**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**Código do cliente chamando um método que tem um valor de retorno e leva um parâmetro de tipo complexo, em um método síncrono**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

O `Invoke` método executa assíncronamente e retorna um `Task` objeto. Se você não `await` especificar ou `.Wait()`, a próxima linha de código será executada antes que o método que você invoca tenha terminado de executar.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Como lidar com eventos de vida de conexão

O SignalR fornece os seguintes eventos de vida útil da conexão que você pode lidar:

- `Received`: Levantada quando qualquer dado é recebido na conexão. Fornece os dados recebidos.
- `ConnectionSlow`: Elevado quando o cliente detecta uma conexão lenta ou freqüentemente caindo.
- `Reconnecting`: Elevado quando o transporte subjacente começa a se reconectar.
- `Reconnected`: Elevado quando o transporte subjacente for reconectado.
- `StateChanged`: Elevado quando o estado de conexão muda. Fornece o estado antigo e o novo estado. Para obter informações sobre valores de estado de conexão, consulte [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).
- `Closed`: Elevado quando a conexão se desconecta.

Por exemplo, se você quiser exibir mensagens de aviso para erros que não são fatais, mas `ConnectionSlow` causam problemas de conexão intermitente, como lentidão ou queda frequente da conexão, manuseie o evento.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

Para obter mais informações, consulte [Compreensão e manipulação de eventos vitalícios de conexão no SignalR](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Como lidar com erros

Se você não habilitar explicitamente mensagens de erro detalhadas no servidor, o objeto de exceção que o SignalR retorna após um erro contém informações mínimas sobre o erro. Por exemplo, se `newContosoChatMessage` uma chamada falhar, a mensagem`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`de erro no objeto de erro contém " " Enviar mensagens de erro detalhadas aos clientes em produção não é recomendado por razões de segurança, mas se você quiser ativar mensagens de erro detalhadas para fins de solução de problemas, use o código a seguir no servidor.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

Para lidar com erros que o SignalR `Error` levanta, você pode adicionar um manipulador para o evento no objeto de conexão.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

Para lidar com erros de invocações de método, enrole o código em um bloco de tentativa de captura.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>Como habilitar o registro do lado do cliente

Para habilitar o registro `TraceLevel` do `TraceWriter` lado do cliente, defina as propriedades e as propriedades no objeto de conexão.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>Amostras de código de aplicativo WPF, Silverlight e console para métodos de cliente que o servidor pode chamar

As amostras de código mostradas anteriormente para definir os métodos do cliente que o servidor pode chamar aplicam-se aos clientes WinRT. As amostras a seguir mostram o código equivalente para clientes wpf, silverlight e aplicativos de console.

### <a name="methods-without-parameters"></a>Métodos sem parâmetros

**Código cliente WPF para método chamado de servidor sem parâmetros**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Código cliente silverlight para método chamado de servidor sem parâmetros**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**Código cliente do aplicativo de console para método chamado de servidor sem parâmetros**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Métodos com parâmetros, especificando os tipos de parâmetros

**Código do cliente WPF para um método chamado de servidor com um parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Código cliente silverlight para um método chamado de servidor com um parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**Código cliente do aplicativo de console para um método chamado de servidor com um parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Métodos com parâmetros, especificando objetos dinâmicos para os parâmetros

**Código cliente WPF para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Código cliente silverlight para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**Console código cliente do aplicativo para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
