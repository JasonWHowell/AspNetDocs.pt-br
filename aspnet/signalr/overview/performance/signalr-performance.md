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
# <a name="signalr-performance"></a>Desempenho do SignalR

por [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este tópico descreve como projetar, medir e melhorar o desempenho em um aplicativo SignalR.
>
> ## <a name="software-versions-used-in-this-topic"></a>Versões de software usadas neste tópico
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

Para uma apresentação recente sobre desempenho e dimensionamento signalR, consulte [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).

Este tópico contém as seguintes seções:

- [Considerações sobre o design](#design)
- [Ajuste do servidor SignalR para desempenho](#tuning)
- [Solucionando problemas de desempenho](#troubleshooting)
- [Usando contadores de desempenho SignalR](#perfcounters)
- [Usando outros contadores de desempenho](#othercounters)
- [Outros recursos](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>Considerações sobre o design

Esta seção descreve padrões que podem ser implementados durante o projeto de um aplicativo SignalR, para garantir que o desempenho não esteja sendo prejudicado gerando tráfego de rede desnecessário.

### <a name="throttling-message-frequency"></a>Freqüência de mensagem de estrangulamento

Mesmo em um aplicativo que envia mensagens em alta frequência (como um aplicativo de jogos em tempo real), a maioria dos aplicativos não precisa enviar mais do que algumas mensagens por segundo. Para reduzir a quantidade de tráfego que cada cliente gera, um loop de mensagem pode ser implementado que faz filas e envia mensagens não com mais freqüência do que uma taxa fixa (ou seja, até um certo número de mensagens serão enviadas a cada segundo, se houver mensagens nesse intervalo de tempo a serem enviadas). Para obter um aplicativo de exemplo que estrangule as mensagens a uma determinada taxa (tanto do cliente quanto do servidor), consulte [Tempo Real de Alta Frequência com SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).

### <a name="reducing-message-size"></a>Reduzindo o tamanho da mensagem

Você pode reduzir o tamanho de uma mensagem SignalR reduzindo o tamanho de seus objetos serializados. No código do servidor, se você estiver enviando um objeto que contém propriedades que não precisam `JsonIgnore` ser transmitidas, evite que essas propriedades sejam serializadas usando o atributo. Os nomes das propriedades também são armazenados na mensagem; os nomes das propriedades podem `JsonProperty` ser encurtados usando o atributo. A amostra de código a seguir demonstra como excluir uma propriedade de ser enviada ao cliente e como encurtar os nomes da propriedade:

**Código do servidor .NET que demonstra o atributo JsonIgnore para excluir dados de serem enviados ao cliente e o atributo JsonProperty para reduzir o tamanho da mensagem**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

Para manter a legibilidade/manutenção no código do cliente, os nomes de propriedade abreviados podem ser remapeados para nomes amigáveis ao homem após o recebimento da mensagem. A amostra de código a seguir demonstra uma maneira possível de remapear nomes encurtados `reMap` para nomes mais longos, definindo um contrato de mensagem (mapeamento) e usando a função para aplicar o contrato à classe de mensagem otimizada:

**Código JavaScript do lado do cliente que remapeia nomes de propriedades encurtados para nomes leíveis por humanos**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

Os nomes podem ser encurtados em mensagens do cliente para o servidor também, usando o mesmo método.

Reduzir a pegada de memória (ou seja, a quantidade de memória usada para a mensagem) do objeto de mensagem também pode melhorar o desempenho. Por exemplo, se a `int` gama completa de `short` `byte` um não for necessária, um ou pode ser usado em vez disso.

Uma vez que as mensagens são armazenadas no barramento de mensagens na memória do servidor, a redução do tamanho das mensagens também pode resolver problemas de memória do servidor.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>Ajuste do servidor SignalR para desempenho

As seguintes configurações podem ser usadas para ajustar seu servidor para obter melhor desempenho em um aplicativo SignalR. Para obter informações gerais sobre como melhorar o desempenho em um aplicativo ASP.NET, consulte [Melhorar o desempenho ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).

**Configurações de configuração SignalR**

- **DefaultMessageBufferSize**: Por padrão, o SignalR retém 1000 mensagens na memória por hub por conexão. Se grandes mensagens estiverem sendo usadas, isso pode criar problemas de memória que podem ser aliviados pela redução desse valor. Essa configuração pode `Application_Start` ser definida no manipulador de `Configuration` eventos em um aplicativo ASP.NET ou no método de uma classe de inicialização OWIN em um aplicativo auto-hospedado. A amostra a seguir demonstra como reduzir esse valor para reduzir a pegada de memória do seu aplicativo, a fim de reduzir a quantidade de memória do servidor usada:

    **Código do servidor .NET em Startup.cs para diminuir o tamanho padrão do buffer de mensagens**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**Configurações de configuração do IIS**

- **Solicitações simultâneas máximas por aplicativo**: O aumento do número de solicitações simultâneas de IIS aumentará os recursos do servidor disponíveis para atender às solicitações. O valor padrão é 5000; para aumentar essa configuração, execute os seguintes comandos em um prompt de comando elevado:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **Queue de pool de aplicativos**: Este é o número máximo de solicitações que http.sys filas para o pool de aplicativos. Quando a fila está cheia, novas solicitações recebem uma resposta 503 "Service Indisponível". O valor padrão é 1000.

    Reduzir o comprimento da fila para o processo do trabalhador no pool de aplicativos que hospeda seu aplicativo conservará recursos de memória. Para obter mais informações, consulte [Gerenciar, ajustar e configurar pools de aplicativos](https://technet.microsoft.com/library/cc745955.aspx).

**configurações de configuração ASP.NET**

Esta seção inclui configurações que podem `aspnet.config` ser definidas no arquivo. Este arquivo é encontrado em um dos dois locais, dependendo da plataforma:

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

ASP.NET configurações que podem melhorar o desempenho do SignalR incluem as seguintes:

- **Máximo de solicitações simultâneas por CPU**: O aumento dessa configuração pode aliviar gargalos de desempenho. Para aumentar essa configuração, adicione `aspnet.config` a seguinte configuração ao arquivo:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **Limite de fila de solicitação**: Quando o `maxConcurrentRequestsPerCPU` número total de conexões exceder a configuração, ASP.NET iniciarão o estrangulamento de solicitações usando uma fila. Para aumentar o tamanho da fila, `requestQueueLimit` você pode aumentar a configuração. Para fazer isso, adicione a `processModel` seguinte configuração ao nó em (em `config/machine.config` vez de `aspnet.config`):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>Solucionando problemas de desempenho

Esta seção descreve maneiras de encontrar gargalos de desempenho em sua aplicação.

### <a name="verifying-that-websocket-is-being-used"></a>Verificando se o WebSocket está sendo usado

Embora o SignalR possa usar uma variedade de transportes para comunicação entre cliente e servidor, o WebSocket oferece uma vantagem de desempenho significativa, e deve ser usado se o cliente e o servidor o suportarem. Para determinar se seu cliente e servidor atendem aos requisitos do WebSocket, consulte [Transportes e Recus](../getting-started/introduction-to-signalr.md#transports). Para determinar qual transporte está sendo usado em seu aplicativo, você pode usar as ferramentas do desenvolvedor do navegador e examinar os logs para ver qual transporte está sendo usado para a conexão. Para obter informações sobre o uso das ferramentas de desenvolvimento do navegador no Internet Explorer e no Chrome, consulte [Transportes e Recuos](../getting-started/introduction-to-signalr.md#transports).

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>Usando contadores de desempenho SignalR

Esta seção descreve como ativar e usar contadores de `Microsoft.AspNet.SignalR.Utils` desempenho SignalR, encontrados no pacote.

### <a name="installing-signalrexe"></a>Instalando signalr.exe

Contadores de desempenho podem ser adicionados ao servidor usando um utilitário chamado SignalR.exe. Para instalar este utilitário, siga estas etapas:

1. No Visual Studio, selecione **Ferramentas** > **NuGet Package Manager** > **Gerencie pacotes NuGet para solução**
2. Procure **signalr.utils**e selecione Instalar.

    ![](signalr-performance/_static/image1.png)
3. Aceite o contrato de licença para instalar o pacote.
4. SignalR.exe será instalado `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`para .

### <a name="installing-performance-counters-with-signalrexe"></a>Instalando contadores de desempenho com SignalR.exe

Para instalar contadores de desempenho SignalR, execute SignalR.exe em um prompt de comando elevado com o seguinte parâmetro:

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

Para remover os contadores de desempenho signalR, execute SignalR.exe em um prompt de comando elevado com o seguinte parâmetro:

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>Contadores de desempenho signalR

O pacote de utilitários instala os seguintes contadores de desempenho. Os contadores "Total" medem o número de eventos desde a última reinicialização do pool de aplicativos ou do servidor.

**Métricas de conexão**

As seguintes métricas medem os eventos de vida de conexão que ocorrem. Para obter mais informações, consulte [Compreensão e manipulação de eventos vitalícios de conexão](../guide-to-the-api/handling-connection-lifetime-events.md).

- **Conexões conectadas**
- **Conexões reconectadas**
- **Conexões desconectadas**
- **Corrente de conexões**

**Métricas de mensagens**

As seguintes métricas medem o tráfego de mensagens gerado pelo SignalR.

- **Mensagens de conexão recebidas total**
- **Mensagens de conexão enviadas total**
- **Mensagens de conexão recebidas/seg**
- **Mensagens de conexão enviadas/sec**

**Métricas do barramento de mensagens**

As seguintes métricas medem o tráfego através do barramento de mensagens do SignalR interno, a fila na qual todas as mensagens SignalR de entrada e saída são colocadas. Uma mensagem é **publicada** quando é enviada ou transmitida. Um **Assinante** neste contexto é uma assinatura no ônibus de mensagens; isso deve igualar o número de clientes mais o próprio servidor. Um **Trabalhador Alocado** é um componente que envia dados para conexões ativas; um **Trabalhador Ocupado** é aquele que está enviando ativamente uma mensagem.

- **Mensagens de ônibus recebidas total**
- **Menção menção mensagens mensagens recebidas/seg**
- **Mensagens de ônibus de mensagens publicadas total**
- **Mensagens de ônibus publicadas/seg**
- **Assinantes de ônibus de mensagem atuais**
- **Assinantes de ônibus de mensagem Total**
- **Assinantes de ônibus de mensagem/Sec**
- **Trabalhadores alocados no ônibus de mensagem**
- **Trabalhadores ocupados de ônibus de mensagem**
- **Tópicos de barra de mensagens atuais**

**Métricas de erro**

As seguintes métricas medem erros gerados pelo tráfego de mensagens SignalR. **Erros de resolução do hub** ocorrem quando um método de hub ou hub não pode ser resolvido. **Erros de invocação do Hub** são exceções lançadas ao invocar um método de hub. **Erros de transporte** são erros de conexão lançados durante uma solicitação ou resposta HTTP.

- **Erros: Todo total**
- **Erros: All/Sec**
- **Erros: Centro de Resolução Total**
- **Erros: Resolução do Hub/Seg**
- **Erros: Total de Invocação do Hub**
- **Erros: Invocação do Hub/Sec**
- **Erros: Total de transporte**
- **Erros: Transporte/Seg**

<a id="scaleout_metrics"></a>

**Métricas de scaleout**

As seguintes métricas medem o tráfego e os erros gerados pelo provedor de scaleout. Um **Fluxo** neste contexto é uma unidade de escala usada pelo provedor de scaleout; esta é uma tabela se o SQL Server for usado, um Tópico se o Service Bus for usado e uma Assinatura se Redis for usado. Cada fluxo garante operações ordenadas de leitura e gravação; um único fluxo é um gargalo de escala potencial, de modo que o número de fluxos pode ser aumentado para ajudar a reduzir esse gargalo. Se vários fluxos forem usados, o SignalR distribuirá automaticamente (fragmentos) mensagens através desses fluxos de forma a garantir que as mensagens enviadas de qualquer conexão estejam em ordem.

A configuração [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) controla o comprimento da fila de envio de escala mantida pelo SignalR. Configurá-lo para um valor maior que 0 colocará todas as mensagens em uma fila de envio para serem enviadas uma de cada vez para o backplane de mensagens configurada. Se o tamanho da fila estiver acima do comprimento configurado, as chamadas subseqüentes a serem enviadas falharão imediatamente com uma [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) até que o número de mensagens na fila seja menor do que a configuração novamente. A fila é desativada por padrão porque os backplanes implementados geralmente têm sua própria fila ou controle de fluxo no local. No caso do SQL Server, o pool de conexões limita efetivamente o número de envios acontecendo a qualquer momento.

Por padrão, apenas um fluxo é usado para SQL Server e Redis, cinco fluxos são usados para Barra de Serviço e a fila está desativada, mas essas configurações podem ser alteradas através da configuração no SQL Server and Service Bus:

**.NET Server Code para configurar a contagem de tabelas e o comprimento da fila para o backplane do SQL Server**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**.NET Server Code para configurar a contagem de tópicos e o comprimento da fila para o backplane do Service Bus**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

Um **fluxo de buffer** é aquele que entrou em um estado defeituoso; quando o fluxo estiver no estado defeituoso, todas as mensagens enviadas para o backplane falharão imediatamente até que o fluxo não esteja mais falhando. O **Comprimento da Fila de Envio** é o número de mensagens que foram postadas, mas ainda não enviadas.

- **Mensagens de menção de escala recebidas/seg**
- **Fluxos de scaleout total**
- **Fluxos scaleout abertos**
- **Buffering de fluxos de scaleout**
- **Total de erros de scaleout**
- **Erros de escala/sec**
- **Comprimento da fila de envio de scaleout**

Para obter mais informações sobre o que esses contadores estão medindo, consulte [SignalR Scaleout com a Azure Service Bus](scaleout-with-windows-azure-service-bus.md).

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>Usando outros contadores de desempenho

Os seguintes contadores de desempenho também podem ser úteis para monitorar o desempenho do seu aplicativo.

**Memória**

- .NET CLR\\Memory # bytes em todos os Heaps (para w3wp)

**ASP.NET**

- ASP.NET\Solicitações atuais
- ASP.NET\Fila
- ASP.NET\Rejeitado

**Cpu**

- Informações do processador\Tempo do processador

**TCP/IP**

- TCPv6/Conexões Estabelecidas
- TCPv4/Conexões Estabelecidas

**Serviço web**

- Serviço web\conexões atuais
- Serviço web\Conexões máximas

**Threading**

- .NET CLR Locks\\and Threads # dos tópicos lógicos atuais
- .NET CLR Locks\\and Threads # dos threads físicos atuais

<a id="otherresources"></a>

## <a name="other-resources"></a>Outros recursos

Para obter mais informações sobre ASP.NET monitoramento e ajuste de desempenho, consulte os seguintes tópicos:

- [Visão geral do desempenho do ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [ASP.NET o uso do thread no IIS 7.5, IIS 7.0 e IIS 6.0](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;aplicativoElemento&gt; pool (Configurações da Web)](https://msdn.microsoft.com/library/dd560842.aspx)
