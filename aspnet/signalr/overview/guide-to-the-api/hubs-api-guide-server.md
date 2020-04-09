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
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET SignalR Hubs API Guide - Server (C#)

por [Patrick Fletcher](https://github.com/pfletcher), Tom [Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este documento fornece uma introdução à programação do lado do servidor da aPI ASP.NET SignalR Hubs para SignalR versão 2, com amostras de código demonstrando opções comuns.
> 
> A API SignalR Hubs permite que você faça chamadas de procedimento remoto (RPCs) de um servidor para clientes conectados e de clientes para o servidor. No código do servidor, você define métodos que podem ser chamados pelos clientes e você chama métodos que são executados no cliente. No código do cliente, você define métodos que podem ser chamados do servidor e você chama métodos que são executados no servidor. O SignalR cuida de todo o encanamento cliente-servidor para você.
> 
> SignalR também oferece uma API de nível inferior chamada Conexões Persistentes. Para obter uma introdução ao SignalR, hubs e persistent connections, consulte [Introdução ao SignalR 2](../getting-started/introduction-to-signalr.md).
> 
> ## <a name="software-versions-used-in-this-topic"></a>Versões de software usadas neste tópico
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR versão 2
>   
> 
> 
> ## <a name="topic-versions"></a>Versões tópicos
> 
> Para obter informações sobre versões anteriores do SignalR, consulte [SignalR Older Versions](../older-versions/index.md).
> 
> ## <a name="questions-and-comments"></a>Perguntas e comentários
> 
> Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página. Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Visão geral

Este documento contém as seguintes seções:

- [Como registrar middleware SignalR](#route)

    - [A URL /signalr](#signalrurl)
    - [Configuração de opções SignalR](#options)
- [Como criar e usar classes hub](#hubclass)

    - [Vida útil do objeto hub](#transience)
    - [Cartucho de camelo de nomes de Hub em clientes JavaScript](#hubnames)
    - [Vários hubs](#multiplehubs)
    - [Hubs fortemente digitados](#stronglytypedhubs)
- [Como definir métodos na classe Hub que os clientes podem chamar](#hubmethods)

    - [Invólucro de camelo de nomes de métodos em clientes JavaScript](#methodnames)
    - [Quando executar assíncronamente](#asyncmethods)
    - [Definindo sobrecargas](#overloads)
    - [Relatando o progresso das invocações do método hub](#progress)
- [Como chamar os métodos do cliente da classe Hub](#callfromhub)

    - [Selecionando quais clientes receberão o RPC](#selectingclients)
    - [Nenhuma validação de tempo de compilação para nomes de métodos](#dynamicmethodnames)
    - [Correspondência de nome do método insensível a casos](#caseinsensitive)
    - [Execução assíncrona](#asyncclient)
- [Como gerenciar a adesão ao grupo da classe Hub](#groupsfromhub)

    - [Execução assíncrona dos métodos Adicionar e Remover](#asyncgroupmethods)
    - [Persistência de membros do grupo](#grouppersistence)
    - [Grupos de usuários únicos](#singleusergroups)
- [Como lidar com eventos de conexão vitalícia na classe Hub](#connectionlifetime)

    - [Quando onConnected, OnDisconnected e OnReconnected são chamados](#onreconnected)
    - [Estado de chamada não povoado](#nocallerstate)
- [Como obter informações sobre o cliente a partir da propriedade Context](#contextproperty)
- [Como passar o estado entre clientes e a classe Hub](#passstate)
- [Como lidar com erros na classe Hub](#handleErrors)
- [Como chamar métodos de clientes e gerenciar grupos de fora da classe Hub](#callfromoutsidehub)

    - [Chamando métodos de cliente](#callingclientsoutsidehub)
    - [Gestão de membros do grupo](#managinggroupsoutsidehub)
- [Como habilitar o rastreamento](#tracing)
- [Como personalizar o pipeline do Hubs](#hubpipeline)

Para obter a documentação sobre como programar os clientes, consulte os seguintes recursos:

- [SignalR Hubs API Guide - JavaScript Client](hubs-api-guide-javascript-client.md)
- [SignalR Hubs API Guide - .NET Client](hubs-api-guide-net-client.md)

Os componentes do servidor para SignalR 2 estão disponíveis apenas no .NET 4.5. Os servidores em execução .NET 4.0 devem usar SignalR v1.x.

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>Como registrar middleware SignalR

Para definir a rota que os clientes usarão para se conectar ao seu Hub, ligue para o `MapSignalR` método quando o aplicativo for iniciado. `MapSignalR`é um método `OwinExtensions` de [extensão](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) para a classe. O exemplo a seguir mostra como definir a rota SignalR Hubs usando uma classe de inicialização OWIN.

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

Se você estiver adicionando a funcionalidade SignalR a um aplicativo MVC ASP.NET, certifique-se de que a rota SignalR seja adicionada antes das outras rotas. Para obter mais informações, consulte [Tutorial: Getting Started with SignalR 2 e MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>A URL /signalr

Por padrão, a URL de rota que os clientes usarão para se conectar ao seu Hub é "/signalr". (Não confunda essa URL com a URL "/signalr/hubs", que é para o arquivo JavaScript gerado automaticamente. Para obter mais informações sobre o proxy gerado, consulte [SignalR Hubs API Guide - JavaScript Client - O proxy gerado e o que ele faz por você](hubs-api-guide-javascript-client.md#genproxy).)

Pode haver circunstâncias extraordinárias que tornam esta URL base não utilizável para SignalR; por exemplo, você tem uma pasta em seu projeto chamada *signalr* e você não quer alterar o nome. Nesse caso, você pode alterar a URL base, como mostrado nos exemplos a seguir (substitua "/signalr" no código de exemplo pela URL desejada).

**Código do servidor que especifica a URL**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**Código cliente JavaScript que especifica a URL (com o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**Código cliente JavaScript que especifica a URL (sem o proxy gerado)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**.NET código de cliente que especifica a URL**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>Configuração de opções de signalr

As sobrecargas `MapSignalR` do método permitem que você especifique uma URL personalizada, um resolver dependência personalizado e as seguintes opções:

- Habilite chamadas de domínio cruzado usando CORS ou JSONP de clientes do navegador.

    Normalmente, se o navegador `http://contoso.com`carregar uma página de , a `http://contoso.com/signalr`conexão SignalR está no mesmo domínio, em . Se a `http://contoso.com` página de `http://fabrikam.com/signalr`fazer uma conexão com , que é uma conexão de domínio cruzado. Por razões de segurança, as conexões entre domínios são desativadas por padrão. Para obter mais informações, consulte [ASP.NET SignalR Hubs API Guide - JavaScript Client - Como estabelecer uma conexão entre domínios](hubs-api-guide-javascript-client.md#crossdomain).
- Habilite mensagens de erro detalhadas.

    Quando ocorrem erros, o comportamento padrão do SignalR é enviar aos clientes uma mensagem de notificação sem detalhes sobre o que aconteceu. O envio de informações detalhadas de erro aos clientes não é recomendado na produção, pois usuários mal-intencionados podem ser capazes de usar as informações em ataques contra seu aplicativo. Para solução de problemas, você pode usar essa opção para ativar temporariamente mais relatórios informativos de erros.
- Desativar arquivos proxy JavaScript gerados automaticamente.

    Por padrão, um arquivo JavaScript com proxies para suas classes hub é gerado em resposta à URL "/signalr/hubs". Se você não quiser usar os proxies JavaScript, ou se você quiser gerar este arquivo manualmente e consultar um arquivo físico em seus clientes, você pode usar essa opção para desativar a geração de proxy. Para obter mais informações, consulte [SignalR Hubs API Guide - JavaScript Client - Como criar um arquivo físico para o proxy gerado signalR](hubs-api-guide-javascript-client.md#manualproxy).

O exemplo a seguir mostra como especificar a URL de `MapSignalR` conexão SignalR e essas opções em uma chamada para o método. Para especificar uma URL personalizada, substitua "/signalr" no exemplo pela URL que você deseja usar.

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>Como criar e usar classes hub

Para criar um Hub, crie uma classe derivada do [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx). O exemplo a seguir mostra uma classe Hub simples para um aplicativo de bate-papo.

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

Neste exemplo, um cliente conectado `NewContosoChatMessage` pode chamar o método e, quando isso acontece, os dados recebidos são transmitidos para todos os clientes conectados.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>Vida útil do objeto hub

Você não instancia a classe Hub ou chama seus métodos a partir de seu próprio código no servidor; tudo o que é feito para você pelo gasoduto SignalR Hubs. O SignalR cria uma nova instância da sua classe Hub cada vez que precisa lidar com uma operação do Hub, como quando um cliente conecta, desconecta ou faz uma chamada de método para o servidor.

Como as instâncias da classe Hub são transitórias, você não pode usá-las para manter o estado de uma chamada de método para outra. Cada vez que o servidor recebe uma chamada de método de um cliente, uma nova instância da classe Hub processa a mensagem. Para manter o estado através de múltiplas conexões e chamadas de método, use algum outro método, como um `Hub`banco de dados, ou uma variável estática na classe Hub, ou uma classe diferente que não deriva de . Se você persistir dados na memória, usando um método como uma variável estática na classe Hub, os dados serão perdidos quando o domínio do aplicativo for reciclado.

Se você quiser enviar mensagens para clientes a partir de seu próprio código que é executado fora da classe Hub, você não pode fazê-lo instanciando uma instância de classe Hub, mas você pode fazê-lo recebendo uma referência ao objeto de contexto SignalR para sua classe Hub. Para obter mais informações, consulte [Como chamar os métodos do cliente e gerenciar grupos de fora da classe Hub](#callfromoutsidehub) mais tarde neste tópico.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>Cartucho de camelo de nomes de Hub em clientes JavaScript

Por padrão, os clientes JavaScript referem-se a Hubs usando uma versão com maiúsculas e camelos do nome da classe. SignalR faz automaticamente essa alteração para que o código JavaScript possa estar em conformidade com as convenções JavaScript. O exemplo anterior seria `contosoChatHub` referido como em código JavaScript.

**Servidor**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**Cliente JavaScript usando proxy gerado**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

Se você quiser especificar um nome diferente `HubName` para os clientes usarem, adicione o atributo. Quando você `HubName` usa um atributo, não há alteração de nome para caso de camelo em clientes JavaScript.

**Servidor**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**Cliente JavaScript usando proxy gerado**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>Vários hubs

Você pode definir várias classes do Hub em um aplicativo. Quando você faz isso, a conexão é compartilhada, mas os grupos são separados:

- Todos os clientes usarão a mesma URL para estabelecer uma conexão SignalR com seu serviço ("/signalr" ou sua URL personalizada se você especificou uma), e essa conexão é usada para todos os Hubs definidos pelo serviço.

    Não há diferença de desempenho para vários Hubs em comparação com a definição de todas as funcionalidades do Hub em uma única classe.
- Todos os Hubs obtêm as mesmas informações de solicitação HTTP.

    Uma vez que todos os Hubs compartilham a mesma conexão, a única informação de solicitação HTTP que o servidor recebe é o que vem na solicitação HTTP original que estabelece a conexão SignalR. Se você usar a solicitação de conexão para passar informações do cliente para o servidor especificando uma seqüência de consultas, você não poderá fornecer diferentes strings de consulta para diferentes Hubs. Todos os Hubs receberão as mesmas informações.
- O arquivo de proxies JavaScript gerado conterá proxies para todos os Hubs em um arquivo.

    Para obter informações sobre os proxies JavaScript, consulte [SignalR Hubs API Guide - JavaScript Client - O proxy gerado e o que ele faz por você](hubs-api-guide-javascript-client.md#genproxy).
- Os grupos são definidos dentro dos Hubs.

    No SignalR você pode definir grupos nomeados para transmitir para subconjuntos de clientes conectados. Os grupos são mantidos separadamente para cada Hub. Por exemplo, um grupo chamado "Administradores" incluiria `ContosoChatHub` um conjunto de clientes para sua classe, `StockTickerHub` e o mesmo nome de grupo se referiria a um conjunto diferente de clientes para sua classe.

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>Hubs fortemente digitados

Para definir uma interface para seus métodos de hub que seu cliente pode referenciar (e habilitar o Intellisense em seus métodos de `Hub<T>` hub), obtenha seu hub (introduzido no SignalR 2.1) em vez de `Hub`:

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>Como definir métodos na classe Hub que os clientes podem chamar

Para expor um método no Hub que você deseja ser callable do cliente, declare um método público, como mostrado nos exemplos a seguir.

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

Você pode especificar um tipo de retorno e parâmetros, incluindo tipos e matrizes complexos, como faria em qualquer método C#. Todos os dados que você recebe em parâmetros ou retornam ao chamador são comunicados entre o cliente e o servidor usando JSON, e o SignalR lida com a vinculação de objetos complexos e conjuntos de objetos automaticamente.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>Invólucro de camelo de nomes de métodos em clientes JavaScript

Por padrão, os clientes JavaScript referem-se aos métodos do Hub usando uma versão com maiúsculas e camelos do nome do método. SignalR faz automaticamente essa alteração para que o código JavaScript possa estar em conformidade com as convenções JavaScript.

**Servidor**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**Cliente JavaScript usando proxy gerado**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

Se você quiser especificar um nome diferente `HubMethodName` para os clientes usarem, adicione o atributo.

**Servidor**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**Cliente JavaScript usando proxy gerado**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>Quando executar assíncronamente

Se o método for de longa duração ou tiver que fazer um trabalho que envolva espera, como uma procuração de [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) banco de `void` dados ou uma chamada de serviço web, faça o método Hub assíncrono retornando um objeto Task (em lugar de retorno) ou [Task&lt;T&gt; ](https://msdn.microsoft.com/library/dd321424.aspx) (no lugar do tipo de `T` retorno). Quando você `Task` retorna um objeto do método, `Task` o SignalR espera que o preenchimento seja concluído e, em seguida, ele envia o resultado desembrulhado de volta para o cliente, de modo que não há diferença em como você codifica o método de chamada no cliente.

Tornar um método Hub assíncrono evita bloquear a conexão quando ele usa o transporte WebSocket. Quando um método do Hub é executado de forma sincronizada e o transporte é WebSocket, as invocações subseqüentes de métodos no Hub do mesmo cliente são bloqueadas até que o método Hub seja concluído.

O exemplo a seguir mostra o mesmo método codificado para ser executado de forma sincronizada ou assíncrona, seguido pelo código cliente JavaScript que funciona para chamar qualquer versão.

**Síncrono**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**Assíncrono**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**Cliente JavaScript usando proxy gerado**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

Para obter mais informações sobre como usar métodos assíncronos em ASP.NET 4.5, consulte [Usando Métodos Assíncronos em ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).

<a id="overloads"></a>

### <a name="defining-overloads"></a>Definindo sobrecargas

Se você quiser definir sobrecargas para um método, o número de parâmetros em cada sobrecarga deve ser diferente. Se você diferenciar uma sobrecarga apenas especificando diferentes tipos de parâmetros, sua classe Hub irá compilar, mas o serviço SignalR abrirá uma exceção no tempo de execução quando os clientes tentarem chamar uma das sobrecargas.

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>Relatando o progresso das invocações do método hub

O SignalR 2.1 adiciona suporte ao [padrão de relatórios de progresso](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduzido no .NET 4.5. Para implementar relatórios `IProgress<T>` de progresso, defina um parâmetro para o método do hub que seu cliente pode acessar:

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

Ao escrever um método de servidor de longa duração, é importante usar um padrão de programação assíncrono como OSync/ Aguarde em vez de bloquear o segmento do hub.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>Como chamar os métodos do cliente da classe Hub

Para chamar os métodos do `Clients` cliente do servidor, use a propriedade em um método em sua classe Hub. O exemplo a seguir `addNewMessageToPage` mostra o código do servidor que chama todos os clientes conectados e o código do cliente que define o método em um cliente JavaScript.

**Servidor**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

Invocar um método de cliente é uma operação `Task`assíncrona e retorna um . Use: `await`

* Para garantir que a mensagem seja enviada sem erro. 
* Para habilitar erros de captura e manuseio em um bloco de captura de tentativa.

**Cliente JavaScript usando proxy gerado**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

Você não pode obter um valor de retorno de um método de cliente; sintaxe `int x = Clients.All.add(1,1)` como não funciona.

Você pode especificar tipos e matrizes complexos para os parâmetros. O exemplo a seguir passa um tipo complexo para o cliente em um parâmetro de método.

**Código do servidor que chama um método cliente usando um objeto complexo**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**Código do servidor que define o objeto complexo**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**Cliente JavaScript usando proxy gerado**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>Selecionando quais clientes receberão o RPC

A propriedade Clientes retorna um objeto [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) que fornece várias opções para especificar quais clientes receberão o RPC:

- Todos os clientes conectados.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- Só o cliente de chamada.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- Todos os clientes, exceto o cliente de chamada.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- Um cliente específico identificado pelo ID de conexão.

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    Este exemplo `addContosoChatMessageToPage` chama o cliente de chamada `Clients.Caller`e tem o mesmo efeito que usar .
- Todos os clientes conectados, exceto os clientes especificados, identificados por identificação de conexão.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- Todos os clientes conectados em um grupo especificado.

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- Todos os clientes conectados em um grupo especificado, exceto os clientes especificados, identificados por identificação de conexão.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- Todos os clientes conectados em um grupo especificado, exceto o cliente de chamada.

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- Um usuário específico, identificado por userId.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    Por padrão, `IPrincipal.Identity.Name`isso é , mas isso pode ser alterado [registrando uma implementação do IUserIdProvider com o host global](mapping-users-to-connections.md#IUserIdProvider).
- Todos os clientes e grupos em uma lista de IDs de conexão.

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- Uma lista de grupos.

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- Um usuário pelo nome.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- Uma lista de nomes de usuário (introduzida no SignalR 2.1).

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>Nenhuma validação de tempo de compilação para nomes de métodos

O nome do método que você especifica é interpretado como um objeto dinâmico, o que significa que não há validação intelliSense ou tempo de compilação para ele. A expressão é avaliada no tempo de execução. Quando a chamada do método é executada, o SignalR envia o nome do método e os valores do parâmetro para o cliente, e se o cliente tiver um método que corresponda ao nome, esse método é chamado e os valores do parâmetro são passados para ele. Se nenhum método de correspondência for encontrado no cliente, nenhum erro será levantado. Para obter informações sobre o formato dos dados que o SignalR transmite ao cliente nos bastidores quando você chama um método cliente, consulte [Introdução ao SignalR](../getting-started/introduction-to-signalr.md).

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>Correspondência de nome do método insensível a casos

A correspondência do nome do método é insensível ao caso. Por `Clients.All.addContosoChatMessageToPage` exemplo, no servidor `AddContosoChatMessageToPage` `addcontosochatmessagetopage`executará `addContosoChatMessageToPage` , ou no cliente.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>Execução assíncrona

O método que você chama executa assíncronamente. Qualquer código que venha após uma chamada de método para um cliente será executado imediatamente sem esperar que o SignalR termine de transmitir dados aos clientes, a menos que você especifique que as linhas de código subseqüentes devem aguardar a conclusão do método. O exemplo de código a seguir mostra como executar dois métodos cliente sequencialmente.

**Usando aguardar (.NET 4.5)**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

Se você `await` usar para esperar até que um método cliente termine antes que a próxima linha de código seja executada, isso não significa que os clientes realmente receberão a mensagem antes que a próxima linha de código seja executada. "Conclusão" de uma chamada de método do cliente significa apenas que o SignalR fez tudo o que era necessário para enviar a mensagem. Se você precisa verificar se os clientes receberam a mensagem, você mesmo tem que programar esse mecanismo. Por exemplo, você `MessageReceived` pode codificar um método `addContosoChatMessageToPage` no Hub, e `MessageReceived` no método no cliente você pode ligar depois de fazer o trabalho que você precisa fazer no cliente. No `MessageReceived` Hub você pode fazer qualquer trabalho que dependa da recepção e processamento real do método de chamada.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>Como usar uma variável de string como nome do método

Se você quiser invocar um método cliente usando uma variável `Clients.All` de `Clients.Others` `Clients.Caller`string como nome `IClientProxy` do método, cast (ou , etc.) para e, em seguida, chamar [Invocação (métodoNome, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>Como gerenciar a adesão ao grupo da classe Hub

Os grupos no SignalR fornecem um método para transmitir mensagens para subconjuntos especificados de clientes conectados. Um grupo pode ter qualquer número de clientes, e um cliente pode ser membro de qualquer número de grupos.

Para gerenciar a associação de grupos, use os `Groups` métodos [Adicionar](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) e [Remover](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) fornecidos pela propriedade da classe Hub. O exemplo a `Groups.Add` `Groups.Remove` seguir mostra os métodos usados nos métodos do Hub que são chamados pelo código do cliente, seguidos pelo código cliente JavaScript que os chama.

**Servidor**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**Cliente JavaScript usando proxy gerado**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

Você não precisa criar grupos explicitamente. Na verdade, um grupo é criado automaticamente na primeira vez `Groups.Add`que você especifica seu nome em uma chamada para , e ele é excluído quando você remove a última conexão de adesão a ele.

Não há API para obter uma lista de membros de grupo ou uma lista de grupos. O SignalR envia mensagens para clientes e grupos com base em um [modelo pub/sub,](http://en.wikipedia.org/wiki/Publish/subscribe)e o servidor não mantém listas de grupos ou membros de grupos. Isso ajuda a maximizar a escalabilidade, porque sempre que você adiciona um nó a uma fazenda web, qualquer estado que o SignalR mantém tem que ser propagado para o novo nó.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Execução assíncrona dos métodos Adicionar e Remover

Os `Groups.Add` `Groups.Remove` métodos e métodos são executados assíncronamente. Se você quiser adicionar um cliente a um grupo e enviar imediatamente uma mensagem ao `Groups.Add` cliente usando o grupo, você tem que ter certeza de que o método termina primeiro. O exemplo de código a seguir mostra como fazer isso.

**Adicionando um cliente a um grupo e, em seguida, mensagens que o cliente**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>Persistência de membros do grupo

O SignalR rastreia conexões, não usuários, então se você quiser que um usuário esteja no mesmo `Groups.Add` grupo toda vez que o usuário estabelecer uma conexão, você tem que ligar toda vez que o usuário estabelecer uma nova conexão.

Depois de uma perda temporária de conectividade, às vezes o SignalR pode restaurar a conexão automaticamente. Nesse caso, o SignalR está restaurando a mesma conexão, não estabelecendo uma nova conexão, e assim a adesão ao grupo do cliente é automaticamente restaurada. Isso é possível mesmo quando a interrupção temporária é resultado de uma reinicialização ou falha do servidor, porque o estado de conexão para cada cliente, incluindo membros do grupo, é acionado para o cliente. Se um servidor for para baixo e for substituído por um novo servidor antes do tempo de conexão acabar, um cliente poderá se reconectar automaticamente ao novo servidor e reinscrever-se em grupos dos dois membros.

Quando uma conexão não pode ser restaurada automaticamente após uma perda de conectividade, ou quando a conexão é desligada, ou quando o cliente se desconecta (por exemplo, quando um navegador navega para uma nova página), as associações do grupo são perdidas. A próxima vez que o usuário se conectar será uma nova conexão. Para manter as associações em grupo quando o mesmo usuário estabelecer uma nova conexão, seu aplicativo tem que rastrear as associações entre usuários e grupos e restaurar membros de grupo cada vez que um usuário estabelece uma nova conexão.

Para obter mais informações sobre conexões e reconexões, consulte [Como lidar com eventos de conexão vitalícia na classe Hub](#connectionlifetime) mais tarde neste tópico.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>Grupos de usuários únicos

Os aplicativos que usam signalR normalmente têm que acompanhar as associações entre usuários e conexões para saber qual usuário enviou uma mensagem e quais usuários devem receber uma mensagem. Grupos são usados em um dos dois padrões comumente usados para fazer isso.

- Grupos de usuários únicos.

    Você pode especificar o nome de usuário como nome do grupo e adicionar o ID de conexão atual ao grupo toda vez que o usuário se conectar ou se reconectar. Para enviar mensagens ao usuário você envia para o grupo. Uma desvantagem desse método é que o grupo não fornece uma maneira de descobrir se o usuário está online ou offline.
- Rastreie associações entre nomes de usuários e IDs de conexão.

    Você pode armazenar uma associação entre cada nome de usuário e um ou mais IDs de conexão em um dicionário ou banco de dados, e atualizar os dados armazenados cada vez que o usuário se conecta ou desconecta. Para enviar mensagens ao usuário, você especifica os IDs de conexão. Uma desvantagem deste método é que ele requer mais memória.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>Como lidar com eventos de conexão vitalícia na classe Hub

As razões típicas para lidar com eventos de vida de conexão são para acompanhar se um usuário está conectado ou não, e para acompanhar a associação entre nomes de usuários e IDs de conexão. Para executar seu próprio código quando os `OnConnected`clientes se conectarem ou desconectarem, anular os `OnDisconnected`métodos virtuais e `OnReconnected` virtuais da classe Hub, como mostrado no exemplo a seguir.

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>Quando onConnected, OnDisconnected e OnReconnected são chamados

Cada vez que um navegador navega para uma nova página, uma nova conexão deve `OnConnected` ser estabelecida, o que significa que o SignalR executará o `OnDisconnected` método seguido pelo método. SignalR sempre cria um novo ID de conexão quando uma nova conexão é estabelecida.

O `OnReconnected` método é chamado quando há uma interrupção temporária na conectividade da a que o SignalR pode recuperar automaticamente, como quando um cabo é temporariamente desconectado e reconectado antes que o tempo de conexão seja desligado. O `OnDisconnected` método é chamado quando o cliente é desconectado e o SignalR não pode se reconectar automaticamente, como quando um navegador navega para uma nova página. Portanto, uma possível seqüência de `OnConnected`eventos `OnReconnected` `OnDisconnected`para um determinado cliente é, ; `OnConnected`ou, `OnDisconnected`. Você não verá a `OnConnected` `OnDisconnected`seqüência, `OnReconnected` para uma determinada conexão.

O `OnDisconnected` método não é chamado em alguns cenários, como quando um servidor cai ou o Domínio do Aplicativo é reciclado. Quando outro servidor entra em linha ou o Domínio do Aplicativo completa sua reciclagem, alguns clientes podem ser capazes de se reconectar e disparar o `OnReconnected` evento.

Para obter mais informações, consulte [Compreensão e manipulação de eventos vitalícios de conexão no SignalR](handling-connection-lifetime-events.md).

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>Estado de chamada não povoado

Os métodos de manipulador de eventos de vida de conexão são `state` chamados do servidor, o que `Caller` significa que qualquer estado que você colocar o objeto no cliente não será preenchido na propriedade no servidor. Para obter `state` informações sobre `Caller` o objeto e a propriedade, consulte [Como passar o estado entre os clientes e a classe Hub](#passstate) mais tarde neste tópico.

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>Como obter informações sobre o cliente a partir da propriedade Context

Para obter informações sobre o `Context` cliente, use a propriedade da classe Hub. A `Context` propriedade retorna um objeto [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) que fornece acesso às seguintes informações:

- A ID de conexão do cliente de chamada.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    O ID de conexão é um GUID atribuído pelo SignalR (você não pode especificar o valor em seu próprio código). Há um ID de conexão para cada conexão, e o mesmo ID de conexão é usado por todos os Hubs se você tiver vários Hubs em seu aplicativo.
- Dados de cabeçalho HTTP.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    Você também pode obter `Context.Headers`cabeçalhos HTTP de . A razão para múltiplas referências à `Context.Headers` mesma coisa é `Context.Request` que foi criada `Context.Headers` primeiro, a propriedade foi adicionada mais tarde, e foi mantida para compatibilidade retrógrada.
- Consultar dados de seqüência.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    Você também pode obter dados `Context.QueryString`de seqüência de consulta de .

    A seqüência de consulta que você recebe nesta propriedade é a que foi usada com a solicitação HTTP que estabeleceu a conexão SignalR. Você pode adicionar parâmetros de seqüência de consulta no cliente configurando a conexão, que é uma maneira conveniente de passar dados sobre o cliente do cliente para o servidor. O exemplo a seguir mostra uma maneira de adicionar uma seqüência de consultas em um cliente JavaScript quando você usa o proxy gerado.

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    Para obter mais informações sobre como definir parâmetros de seqüência de consultas, consulte as guias de API para os clientes [JavaScript](hubs-api-guide-javascript-client.md) e [.NET.](hubs-api-guide-net-client.md)

    Você pode encontrar o método de transporte usado para a conexão nos dados da seqüência de consultas, juntamente com alguns outros valores usados internamente pelo SignalR:

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    O valor `transportMethod` será "webSockets", "serverSentEvents", "foreverFrame" ou "longPolling". Observe que se você verificar `OnConnected` esse valor no método de manipulador de eventos, em alguns cenários você pode inicialmente obter um valor de transporte que não é o método final de transporte negociado para a conexão. Nesse caso, o método abrirá uma exceção e será chamado novamente mais tarde quando o método final de transporte for estabelecido.
- Cookies.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    Você também pode `Context.RequestCookies`obter cookies de .
- Informação do usuário.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- O objeto HttpContext para a solicitação :

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    Use este método `HttpContext.Current` em vez `HttpContext` de obter o objeto para a conexão SignalR.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>Como passar o estado entre clientes e a classe Hub

O proxy do `state` cliente fornece um objeto no qual você pode armazenar dados que deseja ser transmitidos ao servidor com cada chamada de método. No servidor você pode acessar `Clients.Caller` esses dados na propriedade nos métodos do Hub que são chamados pelos clientes. A `Clients.Caller` propriedade não está povoada para `OnConnected`os `OnDisconnected`métodos de manipulador de eventos de vida de conexão, e `OnReconnected`.

Criar ou atualizar `state` dados no `Clients.Caller` objeto e a propriedade funciona em ambas as direções. Você pode atualizar valores no servidor e eles são repassados para o cliente.

O exemplo a seguir mostra o código cliente JavaScript que armazena estado para transmissão para o servidor a cada chamada de método.

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

O exemplo a seguir mostra o código equivalente em um cliente .NET.

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

Na sua classe Hub, você pode `Clients.Caller` acessar esses dados na propriedade. O exemplo a seguir mostra o código que recupera o estado referido no exemplo anterior.

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> Este mecanismo para o estado persistente não se destina a grandes `state` `Clients.Caller` quantidades de dados, uma vez que tudo o que você coloca na propriedade ou é rodada-tripped com cada invocação do método. É útil para itens menores, como nomes de usuários ou contadores.

Em VB.NET ou em um hub fortemente digitado, o objeto `Clients.Caller`de estado do chamador não pode ser acessado através de ; em vez `Clients.CallerState` disso, use (introduzido no SignalR 2.1):

**Usando CallerState em C #**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**Usando callerstate no Visual Basic**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>Como lidar com erros na classe Hub

Para lidar com erros que ocorrem nos métodos da classe Hub, primeiro certifique-se de "observar" `await`quaisquer exceções de operações assíncronas (como invocar métodos do cliente) usando . Em seguida, use um ou mais dos seguintes métodos:

- Enrole o código do método em blocos de captura e registre o objeto de exceção. Para fins de depuração, você pode enviar a exceção ao cliente, mas por razões de segurança o envio de informações detalhadas aos clientes em produção não é recomendado.
- Crie um módulo de pipeline hubs que lida com o método [OnIncomingError.](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) O exemplo a seguir mostra um módulo de pipeline que registra erros, seguido de código em Startup.cs que injeta o módulo no pipeline do Hubs.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- Use `HubException` a classe (introduzida no SignalR 2). Este erro pode ser jogado de qualquer invocação do hub. O `HubError` construtor recebe uma mensagem de string e um objeto para armazenar dados extras de erro. O SignalR serializará automaticamente a exceção e enviará ao cliente, onde será usado para rejeitar ou falhar a invocação do método hub.

    As amostras de código a `HubException` seguir demonstram como jogar um durante uma invocação do Hub e como lidar com a exceção em clientes JavaScript e .NET.

    **Código do servidor demonstrando a classe HubException**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **Código do cliente JavaScript demonstrando resposta a jogar um HubException em um hub**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **Código de cliente .NET demonstrando resposta a jogar um HubException em um hub**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

Para obter mais informações sobre os módulos de pipeline do Hub, consulte [Como personalizar o pipeline do Hubs](#hubpipeline) mais tarde neste tópico.

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>Como habilitar o rastreamento

Para habilitar o rastreamento do lado do servidor, adicione um elemento system.diagnostics ao seu arquivo Web.config, como mostrado neste exemplo:

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

Quando você executa o aplicativo no Visual Studio, você pode visualizar os logs na janela **Saída.**

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>Como chamar métodos de clientes e gerenciar grupos de fora da classe Hub

Para chamar métodos de cliente de uma classe diferente da sua classe Hub, obtenha uma referência ao objeto de contexto SignalR para o Hub e use-o para chamar métodos no cliente ou gerenciar grupos.

A classe `StockTicker` de amostra a seguir obtém o objeto de contexto, armazena-o em uma instância da classe, `updateStockPrice` armazena a instância de classe `StockTickerHub`em uma propriedade estática e usa o contexto da instância de classe singleton para chamar o método em clientes conectados a um Hub chamado .

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

Se você precisar usar o contexto várias vezes em um objeto de longa duração, obtenha a referência uma vez e salve-a em vez de obtê-lo novamente cada vez. Obter o contexto uma vez garante que o SignalR envie mensagens aos clientes na mesma seqüência em que seus métodos do Hub fazem invocações de métodos clientes. Para obter um tutorial que mostre como usar o contexto SignalR para um Hub, consulte [Server Broadcast com ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>Chamando métodos de cliente

Você pode especificar quais clientes receberão o RPC, mas você tem menos opções do que quando você liga de uma classe Hub. A razão para isso é que o contexto não está associado a uma determinada chamada de um cliente, `Clients.Others`portanto, quaisquer métodos que exijam conhecimento do ID de conexão atual, como , ou `Clients.Caller`, ou `Clients.OthersInGroup`, não estão disponíveis. As seguintes opções estão disponíveis:

- Todos os clientes conectados.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- Um cliente específico identificado pelo ID de conexão.

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- Todos os clientes conectados, exceto os clientes especificados, identificados por identificação de conexão.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- Todos os clientes conectados em um grupo especificado.

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- Todos os clientes conectados em um grupo especificado, exceto clientes especificados, identificados por id de conexão.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

Se você estiver ligando para a sua classe não-Hub a partir de métodos em `Clients.Client` `Clients.AllExcept`sua `Clients.Group` classe `Clients.Caller`Hub, você pode passar no ID de conexão atual e usá-lo com , ou para simular , `Clients.Others`ou `Clients.OthersInGroup`. No exemplo a `MoveShapeHub` seguir, a classe passa `Broadcaster` o ID `Broadcaster` de `Clients.Others`conexão para a classe para que a classe possa simular .

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>Gestão de membros do grupo

Para gerenciar grupos, você tem as mesmas opções que você tem em uma classe Hub.

- Adicione um cliente a um grupo

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- Remova um cliente de um grupo

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>Como personalizar o pipeline do Hubs

SignalR permite que você injete seu próprio código no pipeline do Hub. O exemplo a seguir mostra um módulo de pipeline hub personalizado que registra cada chamada de método recebida do cliente e chamada de método de saída invocada no cliente:

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

O código a seguir no *arquivo Startup.cs* registra o módulo a ser executado no pipeline do Hub:

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

Existem muitos métodos diferentes que você pode substituir. Para obter uma lista completa, consulte [Métodos hubPipelineModule](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).
