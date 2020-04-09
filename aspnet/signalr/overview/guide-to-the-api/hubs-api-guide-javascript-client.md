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
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR Hubs API Guide - JavaScript Client

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este documento fornece uma introdução ao uso da API hubs para signalR versão 2 em clientes JavaScript, como navegadores e aplicativos da Windows Store (WinJS).
>
> A API SignalR Hubs permite que você faça chamadas de procedimento remoto (RPCs) de um servidor para clientes conectados e de clientes para o servidor. No código do servidor, você define métodos que podem ser chamados pelos clientes e você chama métodos que são executados no cliente. No código do cliente, você define métodos que podem ser chamados do servidor e você chama métodos que são executados no servidor. O SignalR cuida de todo o encanamento cliente-servidor para você.
>
> SignalR também oferece uma API de nível inferior chamada Conexões Persistentes. Para obter uma introdução ao SignalR, hubs e persistent connections, consulte [Introdução ao SignalR](../getting-started/introduction-to-signalr.md).
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

- [O proxy gerado e o que ele faz por você](#genproxy)

    - [Quando usar o proxy gerado](#cantusegenproxy)
- [Configuração do cliente](#clientsetup)

    - [Como referenciar o proxy gerado dinamicamente](#dynamicproxy)
    - [Como criar um arquivo físico para o proxy gerado signalR](#manualproxy)
- [Como estabelecer uma conexão](#establishconnection)

    - [$.connection.hub é o mesmo objeto que $.hubConnection() cria](#connequivalence)
    - [Execução assíncrona do método de início](#asyncstart)
- [Como estabelecer uma conexão entre domínios](#crossdomain)
- [Como configurar a conexão](#configureconnection)

    - [Como especificar parâmetros de seqüência de consultas](#querystring)
    - [Como especificar o método de transporte](#transport)
- [Como obter um proxy para uma classe Hub](#getproxy)
- [Como definir métodos no cliente que o servidor pode chamar](#callclient)
- [Como chamar métodos de servidor do cliente](#callserver)
- [Como lidar com eventos de vida de conexão](#connectionlifetime)
- [Como lidar com erros](#handleerrors)
- [Como habilitar o registro do lado do cliente](#logging)

Para obter a documentação sobre como programar os clientes do servidor ou .NET, consulte os seguintes recursos:

- [SignalR Hubs Guia de API - Servidor](hubs-api-guide-server.md)
- [SignalR Hubs API Guide - .NET Client](hubs-api-guide-net-client.md)

O componente servidor SignalR 2 só está disponível no .NET 4.5 (embora haja um cliente .NET para SignalR 2 no .NET 4.0).

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>O proxy gerado e o que ele faz por você

Você pode programar um cliente JavaScript para se comunicar com um serviço SignalR com ou sem um proxy que o SignalR gera para você. O que o proxy faz para você é simplificar a sintaxe do código que você usa para conectar, gravar métodos que o servidor chama e métodos de chamada no servidor.

Quando você escreve código para chamar métodos de servidor, o proxy gerado permite que você use uma `serverMethod(arg1, arg2)` sintaxe que parece que você estava executando uma função local: você pode escrever em vez de `invoke('serverMethod', arg1, arg2)`. A sintaxe proxy gerada também permite um erro imediato e inteligível do lado do cliente se você digitar mal o nome do método do servidor. E se você criar manualmente o arquivo que define os proxies, você também poderá obter suporte ao IntelliSense para escrever código que chama métodos de servidor.

Por exemplo, suponha que você tenha a seguinte classe hub no servidor:

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

Os exemplos de código a seguir mostram como `NewContosoChatMessage` o código JavaScript se parece `addContosoChatMessageToPage` para invocar o método no servidor e receber invocações do método do servidor.

**Com o proxy gerado**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**Sem o proxy gerado**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>Quando usar o proxy gerado

Se você quiser registrar vários manipuladores de eventos para um método cliente que o servidor chama, você não poderá usar o proxy gerado. Caso contrário, você pode optar por usar o proxy gerado ou não com base na sua preferência de codificação. Se você optar por não usá-lo, não precisa referenciar a URL `script` "signalr/hubs" em um elemento no código do cliente.

<a id="clientsetup"></a>

## <a name="client-setup"></a>Configuração do cliente

Um cliente JavaScript requer referências ao jQuery e ao arquivo JavaScript do núcleo SignalR. A versão jQuery deve ser 1.6.4 ou versões posteriores principais, como 1.7.2, 1.8.2 ou 1.9.1. Se você decidir usar o proxy gerado, você também precisará de uma referência ao arquivo JavaScript proxy gerado pelo SignalR. O exemplo a seguir mostra como as referências podem parecer em uma página HTML que usa o proxy gerado.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

Essas referências devem ser incluídas nesta ordem: jQuery primeiro, núcleo SignalR depois disso e proxies SignalR por último.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>Como referenciar o proxy gerado dinamicamente

No exemplo anterior, a referência ao proxy gerado pelo SignalR é para código JavaScript gerado dinamicamente, não para um arquivo físico. SignalR cria o código JavaScript para o proxy em tempo real e serve-o ao cliente em resposta à URL "/signalr/hubs". Se você especificou uma URL base diferente para `MapSignalR` conexões SignalR no servidor em seu método, a URL para o arquivo proxy gerado dinamicamente é sua URL personalizada com "/hubs" anexados a ele.

> [!NOTE]
> Para clientes JavaScript do Windows 8 (Windows Store), use o arquivo proxy físico em vez do gerado dinamicamente. Para obter mais informações, consulte [Como criar um arquivo físico para o proxy gerado pelo SignalR](#manualproxy) mais tarde neste tópico.

Em uma ASP.NET exibição de Navalha MVC 4 ou 5, use o tilde para consultar a raiz do aplicativo na referência do arquivo proxy:

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

Para obter mais informações sobre como usar o SignalR no MVC 5, consulte [Getting Started com SignalR e MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).

Em uma ASP.NET exibição de `Url.Content` Navalha MVC 3, use para a referência do arquivo proxy:

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

Em um aplicativo ASP.NET `ResolveClientUrl` Formulários da Web, use para a referência do arquivo de seus proxies ou registre-o através do ScriptManager usando um caminho relativo raiz de aplicativo (começando com um tilde):

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

Como regra geral, use o mesmo método para especificar a URL "/signalr/hubs" que você usa para arquivos CSS ou JavaScript. Se você especificar uma URL sem usar um tilde, em alguns cenários seu aplicativo funcionará corretamente quando você testar no Visual Studio usando o IIS Express, mas falhará com um erro de 404 quando você implantar no IIS completo. Para obter mais informações, consulte **Resolvendo referências a recursos de nível raiz** em servidores web no Visual Studio para ASP.NET Projetos [Web](https://msdn.microsoft.com/library/58wxa9w5.aspx) no site do MSDN.

Quando você executa um projeto web no Visual Studio 2017 no modo de depuração, e se você usar o Internet Explorer como seu navegador, você pode ver o arquivo proxy no **Solution Explorer** em **Scripts**.

Para ver o conteúdo do arquivo, clique duas vezes **em hubs**. Se você não estiver usando o Visual Studio 2012 ou 2013 e o Internet Explorer, ou se você não estiver no modo de depuração, você também pode obter o conteúdo do arquivo navegando para a URL "/signalR/hubs". Por exemplo, se o `http://localhost:56699`seu site `http://localhost:56699/SignalR/hubs` estiver sendo executado em , vá para o seu navegador.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>Como criar um arquivo físico para o proxy gerado signalR

Como uma alternativa ao proxy gerado dinamicamente, você pode criar um arquivo físico que tenha o código proxy e faça referência a esse arquivo. Você pode querer fazer isso para controlar o comportamento de cache ou agrupamento, ou para obter o IntelliSense quando você está codificando chamadas para métodos de servidor.

Para criar um arquivo proxy, execute as seguintes etapas:

1. Instale o pacote [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet.
2. Abra um prompt de comando e navegue até a pasta *de ferramentas* que contém o arquivo SignalR.exe. A pasta de ferramentas está no seguinte local:

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. Insira o seguinte comando:

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    O caminho para o *seu .dll* é tipicamente a pasta *bin* na pasta do projeto.

    Este comando cria um arquivo chamado *server.js* na mesma pasta *que signalr.exe*.
4. Coloque o arquivo *server.js* em uma pasta apropriada em seu projeto, renomeie-o conforme apropriado para o seu aplicativo e adicione uma referência a ele no lugar da referência "signalr/hubs".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Como estabelecer uma conexão

Antes de estabelecer uma conexão, você tem que criar um objeto de conexão, criar um proxy e registrar manipuladores de eventos para métodos que podem ser chamados do servidor. Quando os manipuladores de proxy e eventos estiverem `start` configurados, estabeleça a conexão chamando o método.

Se você estiver usando o proxy gerado, você não precisa criar o objeto de conexão em seu próprio código porque o código proxy gerado o faz para você.

<a id="nogenconnection"></a>

**Estabeleça uma conexão (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**Estabeleça uma conexão (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

O código de exemplo usa a URL padrão "/signalr" para se conectar ao serviço SignalR. Para obter informações sobre como especificar uma URL base diferente, consulte [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).

Por padrão, a localização do hub é o servidor atual; se você estiver se conectando a um servidor `start` diferente, especifique a URL antes de chamar o método, como mostrado no exemplo a seguir:

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> Normalmente você registra manipuladores `start` de eventos antes de chamar o método para estabelecer a conexão. Se você quiser registrar alguns manipuladores de eventos depois de estabelecer a conexão, você pode fazer isso, mas você deve registrar pelo menos um dos seus manipuladores de eventos antes de chamar o `start` método. Uma razão para isso é que pode haver muitos Hubs em um `OnConnected` aplicativo, mas você não gostaria de acionar o evento em todos os Hubs se você só vai usar para um deles. Quando a conexão é estabelecida, a presença de um método de cliente no `OnConnected` proxy de um Hub é o que diz ao SignalR para acionar o evento. Se você não registrar nenhum manipulador de `start` eventos antes de chamar o método, você poderá invocar `OnConnected` métodos no Hub, mas o método do Hub não será chamado e nenhum método de cliente será invocado do servidor.

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$.connection.hub é o mesmo objeto que $.hubConnection() cria

Como você pode ver nos exemplos, quando você `$.connection.hub` usa o proxy gerado, refere-se ao objeto de conexão. Este é o mesmo objeto `$.hubConnection()` que você recebe chamando quando você não está usando o proxy gerado. O código proxy gerado cria a conexão para você executando a seguinte declaração:

![Criando uma conexão no arquivo proxy gerado](hubs-api-guide-javascript-client/_static/image3.png)

Quando você está usando o proxy gerado, `$.connection.hub` você pode fazer qualquer coisa com o que você pode fazer com um objeto de conexão quando você não está usando o proxy gerado.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>Execução assíncrona do método de início

O `start` método é executado de forma assíncrona. Ele retorna um [objeto jQuery Diferido,](http://api.jquery.com/category/deferred-object/)o que significa que você `pipe`pode `done`adicionar `fail`funções de retorno de chamada chamando métodos como , e . Se você tiver um código que deseja executar depois que a conexão for estabelecida, como uma chamada para um método de servidor, coloque esse código em uma função de retorno de chamada ou chame-o de uma função de retorno de chamada. O `.done` método de retorno de chamada é executado após a conexão ter `OnConnected` sido estabelecida e, após qualquer código que você tenha em seu método de manipulador de eventos, no servidor termina a execução.

Se você colocar a declaração "Agora conectado" do exemplo `start` anterior como a `.done` próxima linha `console.log` de código após a chamada do método (não em um retorno de chamada), a linha será executada antes que a conexão seja estabelecida, como mostrado no exemplo a seguir:

![Maneira errada de escrever código que é executado após a conexão é estabelecida](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>Como estabelecer uma conexão entre domínios

Normalmente, se o navegador `http://contoso.com`carregar uma página de , a `http://contoso.com/signalr`conexão SignalR está no mesmo domínio, em . Se a `http://contoso.com` página de `http://fabrikam.com/signalr`fazer uma conexão com , que é uma conexão de domínio cruzado. Por razões de segurança, as conexões entre domínios são desativadas por padrão.

No SignalR 1.x, as solicitações de domínio cruzado eram controladas por um único sinalizador EnableCrossDomain. Esta bandeira controlava tanto as solicitações JSONP quanto CORS. Para maior flexibilidade, todo o suporte ao CORS foi removido do componente do servidor do SignalR (os clientes JavaScript ainda usam o CORS normalmente se for detectado que o navegador o suporta), e novos middleware oWIN foram disponibilizados para suportar esses cenários.

Se o JSONP for necessário no cliente (para suportar solicitações de domínio cruzado em `EnableJSONP` navegadores `HubConfiguration` mais `true`antigos), ele precisará ser ativado explicitamente definindo no objeto para , como mostrado abaixo. O JSONP é desativado por padrão, pois é menos seguro que o CORS.

**Adicionando microsoft.Owin.Cors ao seu projeto:** Para instalar esta biblioteca, execute o seguinte comando no Console do Gerenciador de Pacotes:

`Install-Package Microsoft.Owin.Cors`

Este comando adicionará a versão 2.1.0 do pacote ao seu projeto.

### <a name="calling-usecors"></a>Chamando UseCors

 O trecho de código a seguir demonstra como implementar conexões entre domínios no SignalR 2.

**Implementação de solicitações de domínio cruzado no SignalR 2**

O código a seguir demonstra como ativar CORS ou JSONP em um projeto SignalR 2. Esta amostra `Map` de `RunSignalR` código `MapSignalR`usa e, em vez de, de modo que o middleware CORS é executado apenas `MapSignalR`para as solicitações SignalR que requerem suporte ao CORS (em vez de todo o tráfego no caminho especificado em .) O mapa também pode ser usado para qualquer outro middleware que precise ser executado para um prefixo de URL específico, em vez de para toda a aplicação.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - Não se `jQuery.support.cors` defina como verdadeiro em seu código.
>
>     ![Não defina jQuery.support.cors como verdadeiro](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR lida com o uso do CORS. A `jQuery.support.cors` configuração para true desativa o JSONP porque faz com que o SignalR assuma que o navegador suporta cors.
> - Quando você está se conectando a uma URL de host local, o Internet Explorer 10 não considerará uma conexão entre domínios, então o aplicativo funcionará localmente com o IE 10, mesmo que você não tenha ativado conexões de domínio cruzado no servidor.
> - Para obter informações sobre o uso de conexões entre domínios com o Internet Explorer 9, consulte [este segmento StackOverflow](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).
> - Para obter informações sobre o uso de conexões entre domínios com o Chrome, consulte [este segmento StackOverflow](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).
> - O código de exemplo usa a URL padrão "/signalr" para se conectar ao serviço SignalR. Para obter informações sobre como especificar uma URL base diferente, consulte [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Como configurar a conexão

Antes de estabelecer uma conexão, você pode especificar parâmetros de seqüência de consulta ou especificar o método de transporte.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Como especificar parâmetros de seqüência de consultas

Se você quiser enviar dados para o servidor quando o cliente se conectar, você pode adicionar parâmetros de seqüência de consulta ao objeto de conexão. Os exemplos a seguir mostram como definir um parâmetro de seqüência de consultas no código do cliente.

**Defina um valor de seqüência de consulta antes de chamar o método iniciar (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**Defina um valor de seqüência de consulta antes de chamar o método iniciar (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

O exemplo a seguir mostra como ler um parâmetro de seqüência de consultas no código do servidor.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Como especificar o método de transporte

Como parte do processo de conexão, um cliente SignalR normalmente negocia com o servidor para determinar o melhor transporte que é suportado tanto pelo servidor quanto pelo cliente. Se você já sabe qual transporte deseja usar, você pode contornar esse processo `start` de negociação especificando o método de transporte quando você chamar o método.

**Código do cliente que especifica o método de transporte (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**Código do cliente que especifica o método de transporte (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

Como alternativa, você pode especificar vários métodos de transporte na ordem em que deseja que o SignalR os experimente:

**Código do cliente que especifica um esquema de retorno de transporte personalizado (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**Código do cliente que especifica um esquema de retorno de transporte personalizado (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

Você pode usar os seguintes valores para especificar o método de transporte:

- "WebSockets"
- "ForeverFrame"
- "ServerSentEvents"
- "LongPolling"

Os exemplos a seguir mostram como descobrir qual método de transporte está sendo usado por uma conexão.

**Código do cliente que exibe o método de transporte usado por uma conexão (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**Código do cliente que exibe o método de transporte usado por uma conexão (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

Para obter informações sobre como verificar o método de transporte no código do servidor, consulte [ASP.NET SignalR Hubs API Guide - Server - Como obter informações sobre o cliente a partir da propriedade Context](hubs-api-guide-server.md#contextproperty). Para obter mais informações sobre transportes e recuos, consulte [Introdução ao SignalR - Transportes e Recuos](../getting-started/introduction-to-signalr.md#transports).

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>Como obter um proxy para uma classe Hub

Cada objeto de conexão que você cria encapsula informações sobre uma conexão a um serviço SignalR que contém uma ou mais classes do Hub. Para se comunicar com uma classe Hub, você usa um objeto proxy que você mesmo cria (se você não estiver usando o proxy gerado) ou que é gerado para você.

No cliente, o nome do proxy é uma versão com maiúsculas e camelos do nome da classe Hub. SignalR faz automaticamente essa alteração para que o código JavaScript possa estar em conformidade com as convenções JavaScript.

**Classe hub no servidor**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**Obtenha uma referência ao proxy do cliente gerado para o Hub**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**Criar proxy de cliente para a classe Hub (sem proxy gerado)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

Se você decorar sua classe `HubName` Hub com um atributo, use o nome exato sem alterar o caso.

**Classe hub no servidor com atributo HubName**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**Obtenha uma referência ao proxy do cliente gerado para o Hub**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**Criar proxy de cliente para a classe Hub (sem proxy gerado)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Como definir métodos no cliente que o servidor pode chamar

Para definir um método que o servidor pode chamar de um Hub, `client` adicione um manipulador de `on` eventos ao proxy do Hub usando a propriedade do proxy gerado ou chame o método se você não estiver usando o proxy gerado. Os parâmetros podem ser objetos complexos.

Adicione o manipulador de `start` eventos antes de chamar o método para estabelecer a conexão. (Se você quiser adicionar manipuladores `start` de eventos após chamar o método, consulte a nota em [Como estabelecer uma conexão](#establishconnection) anteriormente neste documento e use a sintaxe mostrada para definir um método sem usar o proxy gerado.)

A correspondência do nome do método é insensível ao caso. Por `Clients.All.addContosoChatMessageToPage` exemplo, no servidor `AddContosoChatMessageToPage` `addContosoChatMessageToPage`executará `addcontosochatmessagetopage` , ou no cliente.

**Definir método no cliente (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**Forma alternativa de definir o método no cliente (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**Defina o método no cliente (sem o proxy gerado ou ao adicionar após chamar o método de início)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**Código do servidor que chama o método do cliente**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

Os exemplos a seguir incluem um objeto complexo como parâmetro de método.

**Defina o método no cliente que leva um objeto complexo (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**Defina o método no cliente que leva um objeto complexo (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**Código do servidor que define o objeto complexo**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**Código do servidor que chama o método do cliente usando um objeto complexo**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Como chamar métodos de servidor do cliente

Para chamar um método de servidor `server` do cliente, use `invoke` a propriedade do proxy gerado ou o método no proxy do Hub se você não estiver usando o proxy gerado. O valor de retorno ou parâmetros podem ser objetos complexos.

Passe em uma versão camelo do nome do método no Hub. SignalR faz automaticamente essa alteração para que o código JavaScript possa estar em conformidade com as convenções JavaScript.

Os exemplos a seguir mostram como chamar um método de servidor que não tem um valor de retorno e como chamar um método de servidor que tenha um valor de retorno.

**Método do servidor sem atributo HubMethodName**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**Código do servidor que define o objeto complexo passado em um parâmetro**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**Código do cliente que invoca o método do servidor (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**Código do cliente que invoca o método do servidor (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

Se você decorou o `HubMethodName` método Hub com um atributo, use esse nome sem alterar o caso.

**Método do servidor** com um atributo HubMethodName

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**Código do cliente que invoca o método do servidor (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**Código do cliente que invoca o método do servidor (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

Os exemplos anteriores mostram como chamar um método de servidor que não tem valor de retorno. Os exemplos a seguir mostram como chamar um método de servidor que tenha um valor de retorno.

**Código do servidor para um método que tem um valor de retorno**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

**A classe stock usada para o** valor de retorno

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**Código do cliente que invoca o método do servidor (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**Código do cliente que invoca o método do servidor (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Como lidar com eventos de vida de conexão

O SignalR fornece os seguintes eventos de vida útil da conexão que você pode lidar:

- `starting`: Levantada antes de qualquer dado ser enviado pela conexão.
- `received`: Levantada quando qualquer dado é recebido na conexão. Fornece os dados recebidos.
- `connectionSlow`: Elevado quando o cliente detecta uma conexão lenta ou freqüentemente caindo.
- `reconnecting`: Elevado quando o transporte subjacente começa a se reconectar.
- `reconnected`: Elevado quando o transporte subjacente for reconectado.
- `stateChanged`: Elevado quando o estado de conexão muda. Fornece o estado antigo e o novo estado (Conexão, Conexão, Reconexão ou Desconectado).
- `disconnected`: Elevado quando a conexão se desconecta.

Por exemplo, se você quiser exibir mensagens de aviso quando houver problemas `connectionSlow` de conexão que possam causar atrasos visíveis, manuseie o evento.

**Lidar com a conexãoEvento lento (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**Lidar com a conexãoEvento lento (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

Para obter mais informações, consulte [Compreensão e manipulação de eventos vitalícios de conexão no SignalR](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Como lidar com erros

O cliente SignalR JavaScript fornece um `error` evento para o o que você pode adicionar um manipulador. Você também pode usar o método fail para adicionar um manipulador para erros resultantes de uma invocação do método do servidor.

Se você não habilitar explicitamente mensagens de erro detalhadas no servidor, o objeto de exceção que o SignalR retorna após um erro contém informações mínimas sobre o erro. Por exemplo, se `newContosoChatMessage` uma chamada falhar, a mensagem`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`de erro no objeto de erro contém " " Enviar mensagens de erro detalhadas aos clientes em produção não é recomendado por razões de segurança, mas se você quiser ativar mensagens de erro detalhadas para fins de solução de problemas, use o código a seguir no servidor.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

O exemplo a seguir mostra como adicionar um manipulador para o evento de erro.

**Adicione um manipulador de erros (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**Adicione um manipulador de erros (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

O exemplo a seguir mostra como lidar com um erro de uma invocação do método.

**Manuseie um erro de uma invocação de método (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**Manuseie um erro de uma invocação de método (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

Se uma invocação de `error` método falhar, o evento também `error` será levantado, `.fail` de modo que seu código no manipulador de métodos e no método de retorno de chamada seria executado.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>Como habilitar o registro do lado do cliente

Para habilitar o registro do lado `logging` do cliente em uma `start` conexão, defina a propriedade no objeto de conexão antes de chamar o método para estabelecer a conexão.

**Habilitar o registro (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**Habilitar o registro (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

Para ver os logs, abra as ferramentas de desenvolvedor do seu navegador e vá para a guia Console. Para obter um tutorial que mostre instruções passo a passo e capturas de tela que mostram como fazer isso, consulte [Server Broadcast com ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).
