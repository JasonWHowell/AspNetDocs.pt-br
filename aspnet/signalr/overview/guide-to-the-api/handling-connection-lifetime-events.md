---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: Compreensão e manuseio de eventos vitalícios de conexão no SignalR | Microsoft Docs
author: bradygaster
description: Este artigo descreve como usar os eventos expostos pela API hubs.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676212"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>Noções básicas e tratamento de eventos de tempo de vida de conexão no SignalR

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este artigo fornece uma visão geral dos eventos de conexão SignalR, reconexão e desconexão que você pode lidar, e configurações de tempo e keepalive que você pode configurar.
>
> O artigo pressupõe que você já tenha algum conhecimento do SignalR e eventos de conexão vitalícia. Para obter uma introdução ao SignalR, consulte [Introdução ao SignalR](../getting-started/introduction-to-signalr.md). Para obter listas de eventos de vida útil da conexão, consulte os seguintes recursos:
>
> - [Como lidar com eventos de conexão vitalícia na classe Hub](hubs-api-guide-server.md#connectionlifetime)
> - [Como lidar com eventos de conexão vitalícia em clientes JavaScript](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [Como lidar com eventos de conexão vitalícia em clientes .NET](hubs-api-guide-net-client.md#connectionlifetime)
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

Este artigo inclui as seções a seguir:

- [Terminologia e cenários da vida de conexão](#terminology)

    - [Conexões SignalR, conexões de transporte e conexões físicas](#signalrvstransport)
    - [Cenários de desconexão de transporte](#transportdisconnect)
    - [Cenários de desconexão do cliente](#clientdisconnect)
    - [Cenários de desconexão do servidor](#serverdisconnect)
- [Tempo e configurações de keepalive](#timeoutkeepalive)

    - [Connectiontimeout](#connectiontimeout)
    - [Desconectartempo](#disconnecttimeout)
    - [Keepalive](#keepalive)
    - [Como alterar o tempo out e manter as configurações vivas](#changetimeout)
- [Como notificar o usuário sobre desconexões](#notifydisconnect)
- [Como reconectar continuamente](#continuousreconnect)
- [Como desconectar um cliente no código do servidor](#disconnectclientfromserver)
- [Detectando a razão de uma desconexão](#detectingreasonfordisconnection)

Os links para tópicos de referência da API são para a versão .NET 4.5 da API. Se você estiver usando .NET 4, consulte [a versão .NET 4 dos tópicos da API](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>Terminologia e cenários da vida de conexão

O `OnReconnected` manipulador de eventos em um `OnConnected` SignalR `OnDisconnected` Hub pode ser executado diretamente depois, mas não depois para um determinado cliente. A razão pela qual você pode ter uma reconexão sem uma desconexão é que existem várias maneiras pelas quais a palavra "conexão" é usada no SignalR.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>Conexões SignalR, conexões de transporte e conexões físicas

Este artigo diferenciará entre *conexões SignalR,* *conexões de transporte*e *conexões físicas:*

- **A conexão SignalR** refere-se a uma relação lógica entre um cliente e uma URL de servidor, mantida pela API SignalR e identificada exclusivamente por um ID de conexão. Os dados sobre essa relação são mantidos pela SignalR e são usados para estabelecer uma conexão de transporte. O relacionamento termina e o SignalR elimina os `Stop` dados quando o cliente chama o método ou um limite de tempo limite é atingido enquanto o SignalR está tentando restabelecer uma conexão de transporte perdida.
- **A conexão de transporte** refere-se a uma relação lógica entre um cliente e um servidor, mantida por uma das quatro APIs de transporte: WebSockets, eventos enviados por servidor, quadro para sempre ou votação longa. A SignalR usa a API de transporte para criar uma conexão de transporte, e a API de transporte depende da existência de uma conexão de rede física para criar a conexão de transporte. A conexão de transporte termina quando o SignalR o termina ou quando a API de transporte detecta que a conexão física está quebrada.
- **Conexão física** refere-se aos links de rede física - fios, sinais sem fio, roteadores, etc. - que facilitam a comunicação entre um computador cliente e um computador de servidor. A conexão física deve estar presente para estabelecer uma conexão de transporte, e uma conexão de transporte deve ser estabelecida para estabelecer uma conexão SignalR. No entanto, quebrar a conexão física nem sempre encerra imediatamente a conexão de transporte ou a conexão SignalR, como será explicado mais tarde neste tópico.

No diagrama a seguir, a conexão SignalR é representada pela aPI hubs e a camada API SignalR de Conexão Persistente, a conexão de transporte é representada pela camada Transportes e a conexão física é representada pelas linhas entre o servidor e os clientes.

![Diagrama de arquitetura SignalR](handling-connection-lifetime-events/_static/image1.png)

Quando você `Start` chama o método em um cliente SignalR, você está fornecendo o código cliente SignalR com todas as informações que precisa para estabelecer uma conexão física com um servidor. O código cliente SignalR usa essas informações para fazer uma solicitação HTTP e estabelecer uma conexão física que usa um dos quatro métodos de transporte. Se a conexão de transporte falhar ou o servidor falhar, a conexão SignalR não desaparecerá imediatamente porque o cliente ainda tem as informações de que precisa para restabelecer automaticamente uma nova conexão de transporte para a mesma URL signalR. Neste cenário, nenhuma intervenção do aplicativo do usuário está envolvida, e quando o código cliente SignalR estabelece uma nova conexão de transporte, ele não inicia uma nova conexão SignalR. A continuidade da conexão SignalR se reflete no fato de que o ID de conexão, que é criado quando você chama o `Start` método, não muda.

O `OnReconnected` manipulador de eventos no Hub é executado quando uma conexão de transporte é automaticamente restabelecida após ter sido perdida. O `OnDisconnected` manipulador de eventos é executado no final de uma conexão SignalR. Uma conexão SignalR pode terminar de todas as seguintes maneiras:

- Se o cliente `Stop` chamar o método, uma mensagem de parada será enviada para o servidor e o cliente e o servidor encerrarão imediatamente a conexão SignalR.
- Depois que a conectividade entre cliente e servidor é perdida, o cliente tenta se reconectar e o servidor espera que o cliente se reconecte. Se as tentativas de reconexão não forem bem sucedidas e o período de tempo de desconexão terminar, o cliente e o servidor encerrarão a conexão SignalR. O cliente pára de tentar se reconectar, e o servidor descarta sua representação da conexão SignalR.
- Se o cliente parar de funcionar `Stop` sem ter a chance de ligar para o método, o servidor aguarda a reconexão do cliente e, em seguida, termina a conexão SignalR após o período de tempo de desconexão.
- Se o servidor parar de funcionar, o cliente tentará reconectar (recriar a conexão de transporte) e, em seguida, termina a conexão SignalR após o período de tempo de desconexão.

Quando não há problemas de conexão, e o `Stop` aplicativo do usuário termina a conexão SignalR ligando para o método, a conexão SignalR e a conexão de transporte começam e terminam ao mesmo tempo. As seções a seguir descrevem com mais detalhes os outros cenários.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>Cenários de desconexão de transporte

As conexões físicas podem ser lentas ou podem haver interrupções na conectividade. Dependendo de fatores como a duração da interrupção, a conexão de transporte pode ser descartada. SignalR então tenta restabelecer a conexão de transporte. Às vezes, a API de conexão de transporte detecta a interrupção e descarta a conexão de transporte, e o SignalR descobre imediatamente que a conexão está perdida. Em outros cenários, nem a API de conexão de transporte nem a SignalR se conscientizam imediatamente de que a conectividade foi perdida. Para todos os transportes, exceto uma votação longa, o cliente SignalR usa uma função chamada *keepalive* para verificar a perda de conectividade que a API de transporte não consegue detectar. Para obter informações sobre conexões de votação longas, consulte [Timeout e mantenha as configurações vivas](#timeoutkeepalive) mais tarde neste tópico.

Quando uma conexão está inativa, periodicamente o servidor envia um pacote keepalive para o cliente. A partir da data em que este artigo está sendo escrito, a freqüência padrão é a cada 10 segundos. Ao ouvir esses pacotes, os clientes podem dizer se há um problema de conexão. Se um pacote keepalive não for recebido quando esperado, após um curto período de tempo o cliente assumir á supor que há problemas de conexão, como lentidão ou interrupções. Se o keepalive ainda não for recebido depois de mais tempo, o cliente assume que a conexão foi descartada, e começa a tentar se reconectar.

O diagrama a seguir ilustra os eventos do cliente e do servidor que são levantados em um cenário típico quando há problemas com a conexão física que não são imediatamente reconhecidos pela API de transporte. O diagrama aplica-se às seguintes circunstâncias:

- O transporte é WebSockets, quadro para sempre ou eventos enviados pelo servidor.
- Há diferentes períodos de interrupção na conexão de rede física.
- A API de transporte não se torna ciente das interrupções, então o SignalR conta com a funcionalidade keepalive para detectá-las.

![Desconexões de transporte](handling-connection-lifetime-events/_static/image2.png)

Se o cliente entrar no modo de reconexão, mas não conseguir estabelecer uma conexão de transporte dentro do limite de tempo limite de desconexão, o servidor encerrará a conexão SignalR. Quando isso acontece, o servidor executa o método do `OnDisconnected` Hub e faz fila uma mensagem de desconexão para enviar ao cliente caso o cliente consiga se conectar mais tarde. Se o cliente fizer a reconexão, ele `Stop` receberá o comando dedesconexão e chamará o método. Nesse cenário, `OnReconnected` não é executado quando o cliente `OnDisconnected` se reconecta e `Stop`não é executado quando o cliente liga . O diagrama a seguir ilustra este cenário.

![Interrupções no transporte - tempo de serviço](handling-connection-lifetime-events/_static/image3.png)

Os eventos vitalícios da conexão SignalR que podem ser levantados no cliente são os seguintes:

- `ConnectionSlow`evento do cliente.

    Criado quando uma proporção predefinida do período de tempo de tempo de keepalive passou desde que a última mensagem ou ping keepalive foi recebida. O período de aviso de tempo de tempo de manutenção padrão é 2/3 do tempo de tempo de manutenção vivo. O tempo de espera é de 20 segundos, então o aviso ocorre em cerca de 13 segundos.

    Por padrão, o servidor envia pings keepalive a cada 10 segundos, e o cliente verifica se há pings de keepalive a cada 2 segundos (um terço da diferença entre o valor de tempo de tempo vivo e o valor de aviso de tempo de tempo vivo).

    Se a API de transporte tomar conhecimento de uma desconexão, o SignalR poderá ser informado da desconexão antes que o período de aviso de tempo livre passe. Nesse caso, `ConnectionSlow` o evento não seria levantado, e o `Reconnecting` SignalR iria diretamente ao evento.
- `Reconnecting`evento do cliente.

    Levantada quando (a) a API de transporte detecta que a conexão está perdida, ou (b) o período de tempo de tempo de manter-se vivo passou desde que a última mensagem ou ping keepalive foi recebida. O código cliente SignalR começa a tentar se reconectar. Você pode lidar com este evento se quiser que seu aplicativo tome alguma ação quando uma conexão de transporte for perdida. O período de tempo padrão de manutenção é atualmente de 20 segundos.

    Se o código do cliente tentar chamar um método Hub enquanto o SignalR estiver no modo de reconexão, o SignalR tentará enviar o comando. Na maioria das vezes, tais tentativas falharão, mas em algumas circunstâncias elas podem ter sucesso. Para os eventos enviados pelo servidor, quadro para sempre e longos transportes de votação, o SignalR usa dois canais de comunicação, um que o cliente usa para enviar mensagens e outro que usa para receber mensagens. O canal usado para receber é o permanentemente aberto, e esse é o que é fechado quando a conexão física é interrompida. O canal usado para envio permanece disponível, portanto, se a conectividade física for restaurada, uma chamada de método de cliente para servidor pode ser bem sucedida antes que o canal de recebimento seja restabelecido. O valor de devolução não seria recebido até que o SignalR reabra o canal usado para receber.
- `Reconnected`evento do cliente.

    Levantada quando a conexão de transporte é restabelecida. O `OnReconnected` manipulador de eventos no Hub é executado.
- `Closed`evento cliente`disconnected` (evento em JavaScript).

    Levantado quando o período de tempo de desconexão expira enquanto o código cliente SignalR está tentando se reconectar depois de perder a conexão de transporte. O tempo de desconexão padrão é de 30 segundos. (Este evento também é levantado quando `Stop` a conexão termina porque o método é chamado.)

Interrupções de conexão de transporte que não são detectadas pela API de transporte e não atrasam a recepção de pings de keepalive do servidor por mais tempo do que o período de aviso de tempo de tempo de viagem pode não causar qualquer evento de conexão vitalícia a ser levantado.

Alguns ambientes de rede fecham deliberadamente conexões ociosas, e outra função dos pacotes keepalive é ajudar a evitar isso, informando a essas redes que uma conexão SignalR está em uso. Em casos extremos, a freqüência padrão de pings keepalive pode não ser suficiente para evitar conexões fechadas. Nesse caso, você pode configurar pings keepalive para serem enviados com mais freqüência. Para obter mais informações, consulte [Timeout e mantenha as configurações viva](#timeoutkeepalive) saem mais tarde neste tópico.

> [!NOTE]
>
> **Importante**: A sequência de eventos aqui descritos não é garantida. A SignalR faz todas as tentativas de aumentar os eventos de conexão ao longo da vida de forma previsível de acordo com este esquema, mas há muitas variações de eventos de rede e muitas maneiras pelas quais as estruturas de comunicação subjacentes, como as APIs de transporte, lidam com eles. Por exemplo, `Reconnected` o evento pode não ser levantado quando `OnConnected` o cliente se reconecta ou o manipulador no servidor pode ser executado quando a tentativa de estabelecer uma conexão não for bem sucedida. Este tópico descreve apenas os efeitos que normalmente seriam produzidos por certas circunstâncias típicas.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>Cenários de desconexão do cliente

Em um cliente do navegador, o código cliente SignalR que mantém uma conexão SignalR é executado no contexto JavaScript de uma página web. É por isso que a conexão SignalR tem que terminar quando você navega de uma página para outra, e é por isso que você tem várias conexões com vários IDs de conexão se você se conectar a partir de várias janelas ou guias do navegador. Quando o usuário fecha uma janela ou guia do navegador, ou navega para uma nova página ou atualiza a página, a conexão SignalR termina imediatamente porque o código cliente SignalR lida com esse evento do navegador para você e chama o `Stop` método. Nesses cenários, ou em qualquer plataforma `Stop` cliente quando `OnDisconnected` seu aplicativo chama o método, o `Closed` manipulador de eventos `disconnected` é executado imediatamente no servidor e o cliente levanta o evento (o evento é nomeado em JavaScript).

Se um aplicativo cliente ou o computador que ele está executando em falhas ou vai dormir (por exemplo, quando o usuário fecha o laptop), o servidor não é informado sobre o que aconteceu. Até onde o servidor sabe, a perda do cliente pode ser devido à interrupção da conectividade e o cliente pode estar tentando se reconectar. Portanto, nesses cenários, o servidor espera para dar ao `OnDisconnected` cliente a chance de se reconectar, e não executa até que o período de tempo de desconexão expire (cerca de 30 segundos por padrão). O diagrama a seguir ilustra este cenário.

![Falha no computador do cliente](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>Cenários de desconexão do servidor

Quando um servidor fica offline - ele reinicializa, falha, o domínio do aplicativo recicla, etc. - o resultado pode ser semelhante a uma conexão perdida, ou a API de transporte e signalR podem saber imediatamente que o servidor se foi, e signalR pode começar a tentar se reconectar sem elevar o `ConnectionSlow` evento. Se o cliente entrar no modo de reconexão e se o servidor recuperar ou reiniciar ou um novo servidor for colocado on-line antes que o período de tempo de desconexão expire, o cliente se reconectará ao servidor restaurado ou novo. Nesse caso, a conexão SignalR continua `Reconnected` no cliente e o evento é levantado. No primeiro servidor, `OnDisconnected` nunca é executado, e `OnReconnected` no novo `OnConnected` servidor, é executado, embora nunca tenha sido executado para aquele cliente naquele servidor antes. (O efeito é o mesmo se o cliente se reconectar ao mesmo servidor após uma reinicialização ou ciclo de domínio do aplicativo, porque quando o servidor reinicializa ele não tem memória de atividade de conexão anterior.) O diagrama a seguir pressupõe que a API de `ConnectionSlow` transporte se torne ciente da conexão perdida imediatamente, de modo que o evento não seja levantado.

![Falha e reconexão do servidor](handling-connection-lifetime-events/_static/image5.png)

Se um servidor não estiver disponível dentro do período de tempo de desconexão, a conexão SignalR será terminada. Neste cenário, `Closed` o`disconnected` evento ( em clientes JavaScript) `OnDisconnected` é levantado no cliente, mas nunca é chamado no servidor. O diagrama a seguir pressupõe que a API de transporte não se torne ciente da `ConnectionSlow` conexão perdida, por isso é detectada pela funcionalidade signalR keepalive e o evento é levantado.

![Falha e tempo de tempo do servidor](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Tempo e configurações de keepalive

O `ConnectionTimeout`padrão `DisconnectTimeout`e `KeepAlive` os valores são apropriados para a maioria dos cenários, mas podem ser alterados se o seu ambiente tiver necessidades especiais. Por exemplo, se o ambiente de rede fechar conexões que estão ociosas por 5 segundos, você pode ter que diminuir o valor de keepalive.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

Esta configuração representa a quantidade de tempo para deixar uma conexão de transporte aberta e esperar por uma resposta antes de fechá-la e abrir uma nova conexão. O valor padrão é de 110 segundos.

Essa configuração só se aplica quando a funcionalidade keepalive é desativada, o que normalmente se aplica apenas ao longo transporte de votação. O diagrama a seguir ilustra o efeito desta configuração em uma longa conexão de transporte de votação.

![Longa conexão de transporte de votação](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>Desconectartempo

Esta configuração representa a quantidade de tempo para esperar `Disconnected` depois que uma conexão de transporte é perdida antes de elevar o evento. O valor padrão é 30 segundos. Quando você `DisconnectTimeout` `KeepAlive` define, é automaticamente definido como `DisconnectTimeout` 1/3 do valor.

<a id="keepalive"></a>

### <a name="keepalive"></a>Keepalive

Esta configuração representa a quantidade de tempo para esperar antes de enviar um pacote keepalive sobre uma conexão ociosa. O valor padrão é 10 segundos. Este valor não deve ser superior `DisconnectTimeout` a 1/3 do valor.

Se você quiser `DisconnectTimeout` definir `KeepAlive`ambos `KeepAlive` `DisconnectTimeout`e , definir depois . Caso contrário, sua `KeepAlive` configuração `DisconnectTimeout` será `KeepAlive` substituída quando automaticamente definir como 1/3 do valor de tempo.

Se você quiser desativar a funcionalidade `KeepAlive` keepalive, defina como nulo. A funcionalidade keepalive é automaticamente desativada para o longo transporte de votação.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>Como alterar o tempo out e manter as configurações vivas

Para alterar os valores padrão dessas `Application_Start` configurações, defina-os no arquivo *Global.asax,* conforme mostrado no exemplo a seguir. Os valores mostrados no código amostral são os mesmos dos valores padrão.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>Como notificar o usuário sobre desconexões

Em alguns aplicativos, você pode querer exibir uma mensagem para o usuário quando houver problemas de conectividade. Você tem várias opções de como e quando fazer isso. As seguintes amostras de código são para um cliente JavaScript usando o proxy gerado.

- Manuseie o `connectionSlow` evento para exibir uma mensagem assim que o SignalR estiver ciente dos problemas de conexão, antes de entrar no modo de reconexão.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- Manuseie o `reconnecting` evento para exibir uma mensagem quando o SignalR estiver ciente de uma desconexão e estiver entrando no modo de reconexão.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- Manuseie o `disconnected` evento para exibir uma mensagem quando uma tentativa de reconexão tiver se esgotado. Neste cenário, a única maneira de restabelecer uma conexão com o servidor novamente `Start` é reiniciar a conexão SignalR chamando o método, que criará um novo ID de conexão. A amostra de código a seguir usa um sinalizador para garantir que você emita a notificação somente após `Stop` um tempo de reconexão, não após um fim normal à conexão SignalR causada pela chamada do método.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>Como reconectar continuamente

Em alguns aplicativos, você pode querer restabelecer automaticamente uma conexão depois que ela foi perdida e a tentativa de reconexão foi cronometrada. Para fazer isso, você `Start` pode `Closed` chamar o`disconnected` método do manipulador de eventos (manipulador de eventos em clientes JavaScript). Você pode querer esperar um período `Start` de tempo antes de ligar para evitar fazer isso com muita freqüência quando o servidor ou a conexão física não estiverem disponíveis. A seguinte amostra de código é para um cliente JavaScript usando o proxy gerado.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

Um problema potencial para estar ciente em clientes móveis é que tentativas de reconexão contínua quando o servidor ou conexão física não está disponível podem causar um dreno desnecessário da bateria.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>Como desconectar um cliente no código do servidor

A versão 2 do SignalR não possui uma API de servidor incorporada para desconectar clientes. Há [planos para adicionar essa funcionalidade no futuro.](https://github.com/SignalR/SignalR/issues/2101) Na versão atual do SignalR, a maneira mais simples de desconectar um cliente do servidor é implementar um método de desconexão no cliente e chamar esse método do servidor. A amostra de código a seguir mostra um método de desconexão para um cliente JavaScript usando o proxy gerado.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> Segurança - Nem este método para desconectar clientes nem a API incorporada proposta abordará o cenário de clientes hackeados `stopClient` que estão executando código malicioso, uma vez que os clientes poderiam se reconectar ou o código hackeado pode remover o método ou alterar o que ele faz. O local apropriado para implementar a proteção dos DOS (Stateful Denial-of-Service, negação de serviço) não está na estrutura ou na camada do servidor, mas sim na infra-estrutura front-end.

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>Detectando a razão de uma desconexão

O SignalR 2.1 adiciona `OnDisconnect` uma sobrecarga ao evento do servidor que indica se o cliente deliberadamente desligou em vez de cronometrar. O `StopCalled` parâmetro é verdadeiro se o cliente fechou explicitamente a conexão. No JavaScript, se um erro do servidor levou o cliente a `$.connection.hub.lastError`desconectar, as informações de erro serão passadas para o cliente como .

**Código do servidor `stopCalled` C#: parâmetro**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**Código cliente JavaScript: `lastError` acessando no `disconnect` evento.**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
