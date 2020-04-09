---
uid: signalr/overview/getting-started/introduction-to-signalr
title: Introdução ao SignalR | Microsoft Docs
author: bradygaster
description: Este artigo descreve o que é signalR, e algumas das soluções que ele foi projetado para criar.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676345"
---
# <a name="introduction-to-signalr"></a>Introdução ao SignalR

por [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este artigo descreve o que é signalR, e algumas das soluções que ele foi projetado para criar. 
> 
> ## <a name="questions-and-comments"></a>Perguntas e comentários
> 
> Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página. Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).

## <a name="what-is-signalr"></a>O que é SignalR?

ASP.NET SignalR é uma biblioteca para desenvolvedores ASP.NET que simplifica o processo de adicionar funcionalidade web em tempo real aos aplicativos. A funcionalidade da Web em tempo real é a capacidade de ter o conteúdo push de código do servidor para clientes conectados instantaneamente à medida que ele se torna disponível, em vez de fazer com que o servidor espere que um cliente solicite novos dados.

O SignalR pode ser usado para adicionar qualquer tipo de funcionalidade web "em tempo real" ao seu aplicativo ASP.NET. Embora o chat seja frequentemente usado como exemplo, você pode fazer muito mais. Sempre que um usuário atualiza uma página da Web para ver novos dados, ou a página implementa [uma longa pesquisa](http://en.wikipedia.org/wiki/Push_technology#Long_polling) para recuperar novos dados, ele é um candidato para usar o SignalR. Exemplos incluem dashboards e aplicativos de monitoramento, aplicativos colaborativos (como edição simultânea de documentos), atualizações de progresso no trabalho e formulários em tempo real.

O SignalR também permite novos tipos de aplicativos web que requerem atualizações de alta frequência do servidor, por exemplo, jogos em tempo real.

O SignalR fornece uma API simples para criar chamadas de procedimento remoto (RPC) de servidor para cliente que chamam funções JavaScript em navegadores clientes (e outras plataformas cliente) a partir do código .NET do lado do servidor. O SignalR também inclui API para gerenciamento de conexão (por exemplo, eventos de conexão e desconexão) e conexões de agrupamento.

![Métodos de invocação com SignalR](introduction-to-signalr/_static/image1.png)

O SignalR lida com o gerenciamento de conexões automaticamente e permite transmitir mensagens a todos os clientes conectados ao mesmo tempo, como uma sala de chat. Você também pode enviar mensagens para clientes específicos. A conexão entre o cliente e o servidor é persistente, diferente de uma conexão HTTP clássica, que é restabelecida para cada comunicação.

O SignalR suporta a funcionalidade "server push", na qual o código do servidor pode chamar para o código do cliente no navegador usando O RPC (Remote Procedure Calls, chamadas de procedimento remoto), em vez do modelo de solicitação-resposta comum na web hoje.

Os aplicativos SignalR podem ser dimensionados para milhares de clientes usando provedores de escala incorporados e de terceiros.

Os provedores incorporados incluem:
* [Barramento de Serviço](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

Os provedores de terceiros incluem:
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

SignalR é de código aberto, acessível através do [GitHub](https://github.com/signalr).

## <a name="signalr-and-websocket"></a>SignalR e WebSocket

SignalR usa o novo transporte WebSocket quando disponível e volta para transportes mais antigos, quando necessário. Embora você certamente possa escrever seu aplicativo usando o WebSocket diretamente, usar o SignalR significa que muitas das funcionalidades extras que você precisaria implementar já estão feitas para você. O mais importante é que isso significa que você pode codificar seu aplicativo para tirar proveito do WebSocket sem ter que se preocupar em criar um caminho de código separado para clientes mais velhos. O SignalR também protege você de ter que se preocupar com atualizações para o WebSocket, uma vez que o SignalR é atualizado para suportar alterações no transporte subjacente, fornecendo ao seu aplicativo uma interface consistente em versões do WebSocket.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>Transportes e recuos

SignalR é uma abstração sobre alguns dos transportes que são necessários para fazer o trabalho em tempo real entre cliente e servidor. Uma conexão SignalR começa como HTTP e, em seguida, é promovida a uma conexão WebSocket se estiver disponível. O WebSocket é o transporte ideal para o SignalR, uma vez que faz o uso mais eficiente da memória do servidor, tem a menor latência e possui os recursos mais subjacentes (como comunicação duplex completa entre cliente e servidor), mas também tem os requisitos mais rigorosos: o WebSocket exige que o servidor esteja usando o Windows Server 2012 ou o Windows 8, e o .NET Framework 4.5. Se esses requisitos não forem atendidos, o SignalR tentará usar outros transportes para fazer suas conexões.

### <a name="html-5-transports"></a>Transportes HTML 5

Esses transportes dependem do suporte para [HTML 5](http://en.wikipedia.org/wiki/HTML5). Se o navegador cliente não suportar o padrão HTML 5, transportes mais antigos serão usados.

- **WebSocket** (se o servidor e o navegador indicarem que podem suportar websocket). O WebSocket é o único transporte que estabelece uma conexão verdadeira e bidirecional entre cliente e servidor. No entanto, o WebSocket também tem os requisitos mais rigorosos; ele é totalmente suportado apenas nas versões mais recentes do Microsoft Internet Explorer, Google Chrome e Mozilla Firefox, e só tem uma implementação parcial em outros navegadores, como Opera e Safari.
- **Server Sent Events**, também conhecido como EventSource (se o navegador suporta Eventos Enviados pelo Servidor, que é basicamente todos os navegadores, exceto o Internet Explorer.)

### <a name="comet-transports"></a>Transportes de cometas

Os seguintes transportes são baseados no modelo de aplicativo web [do Comet,](http://en.wikipedia.org/wiki/Comet_(programming)) no qual um navegador ou outro cliente mantém uma solicitação HTTP de longa data, que o servidor pode usar para empurrar dados para o cliente sem que o cliente os solicite especificamente.

- **Forever Frame** (somente para Internet Explorer). O Forever Frame cria um IFrame oculto que faz uma solicitação a um ponto final no servidor que não é concluído. Em seguida, o servidor envia continuamente o script para o cliente que é executado imediatamente, fornecendo uma conexão em tempo real unidirecional de servidor para cliente. A conexão de cliente para servidor usa uma conexão separada do servidor para a conexão do cliente e, como uma solicitação HTTP padrão, uma nova conexão é criada para cada pedaço de dados que precisa ser enviado.
- **Ajax votação longa**. A votação longa não cria uma conexão persistente, mas, em vez disso, pesquisa o servidor com uma solicitação que permanece aberta até que o servidor responda, momento em que a conexão fecha, e uma nova conexão é solicitada imediatamente. Isso pode introduzir alguma latência enquanto a conexão é reconfigurada.

Para obter mais informações sobre quais transportes são suportados sob as quais configurações, consulte [Plataformas suportadas](supported-platforms.md).

### <a name="transport-selection-process"></a>Processo seletivo de transporte

A lista a seguir mostra os passos que o SignalR usa para decidir qual transporte usar.

1. Se o navegador for o Internet Explorer 8 ou anterior, a Pesquisa Longa será usada.
2. Se o JSONP estiver configurado `jsonp` (ou seja, o parâmetro será definido para `true` quando a conexão for iniciada), a Votação Longa será usada.
3. Se uma conexão entre domínios estiver sendo feita (isto é, se o ponto final signalR não estiver no mesmo domínio da página de hospedagem), o WebSocket será usado se os seguintes critérios forem atendidos:

   - O cliente suporta CORS (Cross-Origin Resource Sharing). Para obter detalhes sobre quais clientes suportam o CORS, consulte [o CORS em caniuse.com](http://www.caniuse.com/CORS).
   - O cliente suporta WebSocket
   - O servidor suporta WebSocket

     Se algum desses critérios não for atendido, a Votação Longa será usada. Para obter mais informações sobre conexões entre domínios, consulte [Como estabelecer uma conexão entre domínios](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).
4. Se o JSONP não estiver configurado e a conexão não for de domínio cruzado, o WebSocket será usado se o cliente e o servidor o suportarem.
5. Se o cliente ou o servidor não suportarem o WebSocket, o Server Sent Events será usado se ele estiver disponível.
6. Se os Eventos enviados pelo servidor não estiverm disponíveis, o Forever Frame será tentado.
7. Se o Forever Frame falhar, a Votação Longa será usada.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>Monitoramento de transportes

Você pode determinar o transporte que seu aplicativo está usando, permitindo o login em seu hub e abrindo a janela do console no seu navegador.

Para habilitar o registro de eventos do seu hub em um navegador, adicione o seguinte comando ao aplicativo do cliente:

`$.connection.hub.logging = true;`

- No Internet Explorer, abra as ferramentas do desenvolvedor pressionando F12 e clique na guia Console.

    ![Console no Microsoft Internet Explorer](introduction-to-signalr/_static/image2.png)
- No Chrome, abra o console pressionando Ctrl+Shift+J.

    ![Console no Google Chrome](introduction-to-signalr/_static/image3.png)

Com o console aberto e o registro ativado, você poderá ver qual transporte está sendo usado pelo SignalR.

![Console no Internet Explorer mostrando transporte de WebSocket](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>Especificando um transporte

Negociar um transporte leva um certo tempo e recursos de cliente/servidor. Se os recursos do cliente forem conhecidos, então um transporte pode ser especificado quando a conexão com o cliente for iniciada. O seguinte trecho de código demonstra a inicialização de uma conexão usando o transporte Ajax Long Polling, como seria usado se soubesse-se que o cliente não suportava nenhum outro protocolo:

`connection.start({ transport: 'longPolling' });`

Você pode especificar uma ordem de recuo se quiser que um cliente tente transportes específicos em ordem. O seguinte trecho de código demonstra a tentativa de WebSocket, e falhando nisso, indo diretamente para pesquisa longa.

`connection.start({ transport: ['webSockets','longPolling'] });`

As constantes de string para especificar transportes são definidas da seguinte forma:

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>Conexões e Hubs

A API SignalR contém dois modelos de comunicação entre clientes e servidores: Conexões Persistentes e Hubs.

Uma conexão representa um ponto final simples para o envio de mensagens de destinatário único, agrupadas ou transmitidas. A API de conexão persistente (representada no código .NET pela classe PersistentConnection) dá ao desenvolvedor acesso direto ao protocolo de comunicação de baixo nível que o SignalR expõe. O uso do modelo de comunicação Conexões será familiar para desenvolvedores que usaram APIs baseadas em conexão, como a Windows Communication Foundation.

Um Hub é um pipeline mais de alto nível construído sobre a API de conexão que permite que seu cliente e servidor chamem métodos uns dos outros diretamente. O SignalR lida com o despacho através dos limites da máquina como se fosse mágico, permitindo que os clientes chamem métodos no servidor tão facilmente quanto os métodos locais, e vice-versa. O uso do modelo de comunicação Hubs será familiar para desenvolvedores que usaram APIs de invocação remota, como .NET Remoting. O uso de um Hub também permite que você passe parâmetros fortemente digitados para métodos, permitindo a vinculação do modelo.

### <a name="architecture-diagram"></a>Diagrama de arquitetura

O diagrama a seguir mostra a relação entre Hubs, Conexões Persistentes e as tecnologias subjacentes usadas para transportes.

![Diagrama de arquitetura SignalR mostrando APIs, transportes e clientes](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>Como os Hubs funcionam

Quando o código do lado do servidor chama um método no cliente, um pacote é enviado através do transporte ativo que contém o nome e os parâmetros do método a ser chamado (quando um objeto é enviado como parâmetro de método, ele é serializado usando JSON). Em seguida, o cliente corresponde o nome do método aos métodos definidos no código do lado do cliente. Se houver uma correspondência, o método do cliente será executado usando os dados de parâmetros desserializados.

A chamada do método pode ser monitorada usando ferramentas como [o Fiddler.](http://fiddler2.com/) A imagem a seguir mostra uma chamada de método enviada de um servidor SignalR para um cliente do navegador da Web no painel Logs do Fiddler. A chamada do método está `MoveShapeHub`sendo enviada de um hub `updateShape`chamado , e o método que está sendo invocado é chamado .

![Exibição do registro do Violinista mostrando o tráfego signalR](introduction-to-signalr/_static/image6.png)

Neste exemplo, o nome do `H` hub é identificado com o parâmetro; o nome do método `M` é identificado com o parâmetro, e os `A` dados enviados ao método são identificados com o parâmetro. O aplicativo que gerou essa mensagem é criado no tutorial [de alta frequência em tempo real.](tutorial-high-frequency-realtime-with-signalr.md)

### <a name="choosing-a-communication-model"></a>Escolhendo um modelo de comunicação

A maioria dos aplicativos deve usar a API hubs. A API conexões pode ser usada nas seguintes circunstâncias:

- O formato da mensagem real enviada precisa ser especificado.
- O desenvolvedor prefere trabalhar com um modelo de mensagens e despachos em vez de um modelo de invocação remota.
- Um aplicativo existente que usa um modelo de mensagens está sendo portado para usar o SignalR.
