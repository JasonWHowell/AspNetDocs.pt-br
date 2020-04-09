---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Tutorial: Transmissão do servidor com SignalR 2 | Microsoft Docs'
author: tdykstra
description: Este tutorial mostra como criar um aplicativo web que usa ASP.NET SignalR 2 para fornecer funcionalidade de transmissão de servidor.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676093"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>Tutorial: Transmissão do servidor com SignalR 2

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Este tutorial mostra como criar um aplicativo web que usa ASP.NET SignalR 2 para fornecer funcionalidade de transmissão de servidor. A transmissão do servidor significa que o servidor inicia as comunicações enviadas aos clientes.

O aplicativo que você criará neste tutorial simula um ticker de estoque, um cenário típico para a funcionalidade de transmissão de servidor. Periodicamente, o servidor atualiza aleatoriamente os preços das ações e transmite as atualizações para todos os clientes conectados. No navegador, os números e **Change** símbolos **%** na Alteração e colunas mudam dinamicamente em resposta às notificações do servidor. Se você abrir navegadores adicionais para a mesma URL, todos eles mostrarão os mesmos dados e as mesmas alterações nos dados simultaneamente.

![Criar web](tutorial-server-broadcast-with-signalr/_static/image1.png)

Neste tutorial, você:

> [!div class="checklist"]
> * Criar o projeto
> * Configurar o código de servidor
> * Examine o código do servidor
> * Configure o código do cliente
> * Examine o código do cliente
> * Testar o aplicativo
> * Habilitar o registro em log

> [!IMPORTANT]
> Se você não quiser trabalhar as etapas de construção do aplicativo, você pode instalar o pacote SignalR.Sample em um novo projeto Vazio ASP.NET Web Application. Se você instalar o pacote NuGet sem executar as etapas neste tutorial, você deve seguir as instruções no arquivo *readme.txt.* Para executar o pacote, você precisa adicionar uma `ConfigureSignalR` classe de inicialização OWIN que chama o método no pacote instalado. Você receberá um erro se não adicionar a classe de inicialização OWIN. Consulte a seção Instalar a amostra [StockTicker](#install-the-stockticker-sample) deste artigo.

## <a name="prerequisites"></a>Pré-requisitos

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) com a carga de trabalho **ASP.NET e desenvolvimento para a Web**.

## <a name="create-the-project"></a>Criar o projeto

Esta seção mostra como usar o Visual Studio 2017 para criar um aplicativo web vazio ASP.NET.

1. No Visual Studio, crie um aplicativo web ASP.NET.

    ![Criar web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. Na **nova ASP.NET web Application - SignalR.StockTicker,** deixe **Empty** selecionado e selecione **OK**.

## <a name="set-up-the-server-code"></a>Configurar o código de servidor

Nesta seção, você configura o código que é executado no servidor.

### <a name="create-the-stock-class"></a>Criar a classe Stock

Você começa criando a classe de modelo *Stock* que você usará para armazenar e transmitir informações sobre um estoque.

1. No **Solution Explorer,** clique com o botão direito do mouse no projeto e **selecione Adicionar** > **classe**.

1. Nomeie o *estoque da* classe e adicione-o ao projeto.

1. Substitua o código no arquivo *Stock.cs* por este código:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    As duas propriedades que você definirá `Symbol` quando criar estoques são (por exemplo, MSFT para Microsoft) e `Price`. As outras propriedades dependem de `Price`como e quando você definir . A primeira vez `Price`que você definir `DayOpen`, o valor é propagado para . Depois disso, quando `Price`você define , `Change` `PercentChange` o aplicativo calcula `Price` os `DayOpen`valores e propriedades com base na diferença entre e .

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>Crie as classes StockTickerHub e StockTicker

Você usará a API signalR Hub para lidar com a interação servidor-cliente. Uma `StockTickerHub` classe derivada da `Hub` classe SignalR lidará com conexões recebidas e chamadas de método dos clientes. Você também precisa manter dados `Timer` de estoque e executar um objeto. O `Timer` objeto acionará periodicamente atualizações de preços independentes das conexões do cliente. Você não pode colocar essas `Hub` funções em uma classe, porque hubs são transitórios. O aplicativo `Hub` cria uma instância de classe para cada tarefa no hub, como conexões e chamadas do cliente para o servidor. Assim, o mecanismo que mantém os dados de ações, atualiza os preços e transmite as atualizações de preços tem que ser executado em uma classe separada. Você vai nomear `StockTicker`a classe.

![Transmissão de StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

Você só quer que `StockTicker` uma instância da classe seja executada no servidor, então `StockTickerHub` você precisará `StockTicker` configurar uma referência de cada instância para a instância singleton. A `StockTicker` classe tem que transmitir para os clientes porque tem `StockTicker` os dados `Hub` de estoque e aciona atualizações, mas não é uma classe. A `StockTicker` classe tem que obter uma referência ao objeto de contexto de conexão SignalR Hub. Em seguida, ele pode usar o objeto de contexto de conexão SignalR para transmitir aos clientes.

#### <a name="create-stocktickerhubcs"></a>Criar StockTickerHub.cs

1. No **Solution Explorer,** clique com o botão direito do mouse no projeto e **selecione Adicionar** > **novo item**.

1. Em **Adicionar novo item - SignalR.StockTicker,** **selecione** > **Imagem Visual C#** > **Sinalizar da Web** > **instalada** e selecione **SignalR Hub Class (v2)**.

1. Nomeie a classe *StockTickerHub* e adicione-a ao projeto.

    Esta etapa cria o arquivo de classe *StockTickerHub.cs.* Simultaneamente, ele adiciona um conjunto de arquivos de script e referências de montagem que suportasignalR para o projeto.

1. Substitua o código no arquivo *StockTickerHub.cs* por este código:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. Salve o arquivo.

O aplicativo usa a classe [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) para definir métodos que os clientes podem chamar no servidor. Você está definindo `GetAllStocks()`um método: . Quando um cliente se conecta inicialmente ao servidor, ele chamará esse método para obter uma lista de todas as ações com seus preços atuais. O método pode ser executado `IEnumerable<Stock>` sincronicamente e retornar porque está retornando dados da memória.

Se o método tivesse que obter os dados fazendo algo que envolvesse espera, como `Task<IEnumerable<Stock>>` uma pesquisa de banco de dados ou uma chamada de serviço web, você especificaria como o valor de retorno para permitir o processamento assíncrono. Para obter mais informações, consulte [ASP.NET Guia de API signalR Hubs - Server - Quando executar assíncronamente](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).

O `HubName` atributo especifica como o aplicativo fará referência ao Código Hub em JavaScript no cliente. O nome padrão no cliente se você não usar esse atributo, é uma versão camelCase do nome da classe, que neste caso seria `stockTickerHub`.

Como você verá mais tarde `StockTicker` quando criar a classe, o aplicativo cria `Instance` uma instância singleton dessa classe em sua propriedade estática. Essa instância `StockTicker` de singleton está na memória, não importa quantos clientes conectem ou desconectem. Esse exemplo é `GetAllStocks()` o que o método usa para retornar as informações atuais de estoque.

#### <a name="create-stocktickercs"></a>Criar StockTicker.cs

1. No **Solution Explorer,** clique com o botão direito do mouse no projeto e **selecione Adicionar** > **classe**.

1. Nomeie a classe *StockTicker* e adicione-a ao projeto.

1. Substitua o código no arquivo *StockTicker.cs* por este código:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

Uma vez que todos os segmentos estarão executando a mesma instância do código StockTicker, a classe StockTicker tem que ser segura de rosca.

### <a name="examine-the-server-code"></a>Examine o código do servidor

Se você examinar o código do servidor, ele ajudará você a entender como o aplicativo funciona.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>Armazenamento da instância singleton em um campo estático

O código inicializa `_instance` o campo estático que apoia a `Instance` propriedade com uma instância da classe. Como o construtor é privado, é a única instância da classe que o aplicativo pode criar. O aplicativo usa [inicialização Lazy](/dotnet/framework/performance/lazy-initialization) para o `_instance` campo. Não é por razões de desempenho. É para ter certeza de que a criação de instâncias é segura de rosca.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

Cada vez que um cliente se conecta ao servidor, uma nova instância da classe StockTickerHub `StockTicker.Instance` em execução em um `StockTickerHub` segmento separado obtém a instância de singleton do StockTicker da propriedade estática, como você viu anteriormente na classe.

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Armazenamento de dados de ações em um Dicionário Simultâneo

A construtora inicia a `_stocks` coleta com alguns `GetAllStocks` dados de estoque amostral, e devolve os estoques. Como você viu anteriormente, essa coleção `StockTickerHub.GetAllStocks`de ações é devolvida `Hub` por , que é um método de servidor na classe que os clientes podem chamar.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

A coleção de ações é definida como um tipo [de Dicionário Simultâneo](https://msdn.microsoft.com/library/dd287191.aspx) para a segurança do segmento. Como alternativa, você pode usar um objeto [dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) e bloquear explicitamente o dicionário quando você fizer alterações nele.

Para este aplicativo de exemplo, é OK armazenar dados de aplicativos na memória `StockTicker` e perder os dados quando o aplicativo se desfaz da ocorrência. Em um aplicativo real, você trabalharia com um armazenamento de dados back-end como um banco de dados.

#### <a name="periodically-updating-stock-prices"></a>Atualização periódica dos preços das ações

O construtor inicia `Timer` um objeto que periodicamente chama métodos que atualizam os preços das ações aleatoriamente.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`chamadas `UpdateStockPrices`, que passa em nulo no parâmetro estadual. Antes de atualizar os preços, `_updateStockPricesLock` o aplicativo bloqueia o objeto. O código verifica se outro segmento já está `TryUpdateStockPrice` atualizando os preços e, em seguida, ele chama cada ação da lista. O `TryUpdateStockPrice` método decide se altera o preço das ações e quanto o altera. Se o preço das ações `BroadcastStockPrice` mudar, o aplicativo liga para transmitir a variação do preço das ações para todos os clientes conectados.

A `_updatingStockPrices` bandeira designada [volátil](https://msdn.microsoft.com/library/x13ttww7.aspx) para ter certeza de que é segura para rosca.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

Em uma aplicação `TryUpdateStockPrice` real, o método chamaria um serviço web para procurar o preço. Neste código, o aplicativo usa um gerador de números aleatórios para fazer alterações aleatoriamente.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>Obtendo o contexto SignalR para que a classe StockTicker possa transmitir aos clientes

Como as mudanças de `StockTicker` preço se originam aqui no `updateStockPrice` objeto, é o objeto que precisa chamar um método em todos os clientes conectados. Em `Hub` uma aula, você tem uma API `StockTicker` para chamar métodos `Hub` de cliente, mas não `Hub` deriva da classe e não tem uma referência a nenhum objeto. Para transmitir para clientes conectados, a `StockTicker` classe tem `StockTickerHub` que obter a instância de contexto SignalR para a classe e usá-la para chamar métodos aos clientes.

O código recebe uma referência ao contexto SignalR quando cria a instância de classe singleton, passa `Clients` essa referência ao construtor e o construtor o coloca na propriedade.

Existem duas razões pelas quais você quer obter o contexto apenas uma vez: obter o contexto é uma tarefa cara, e obtê-lo uma vez garante que o aplicativo preserve a ordem pretendida de mensagens enviadas aos clientes.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

Obter `Clients` a propriedade do contexto e `StockTickerClient` colocá-lo na propriedade permite que você escreva código para `Hub` chamar métodos de cliente que se parece com o mesmo que seria em uma classe. Por exemplo, para transmitir a `Clients.All.updateStockPrice(stock)`todos os clientes que você pode escrever .

O `updateStockPrice` método que você `BroadcastStockPrice` está chamando ainda não existe. Você adicionará mais tarde quando escrever código que é executado no cliente. Você pode `updateStockPrice` se `Clients.All` referir aqui porque é dinâmico, o que significa que o aplicativo avaliará a expressão em tempo de execução. Quando essa chamada de método for executada, o SignalR enviará o nome do método e `updateStockPrice`o valor do parâmetro para o cliente, e se o cliente tiver um método chamado, o aplicativo chamará esse método e passará o valor do parâmetro para ele.

`Clients.All`significa enviar para todos os clientes. O SignalR oferece outras opções para especificar para quais clientes ou grupos de clientes enviar. Para obter mais informações, consulte [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>Registre a rota SignalR

O servidor precisa saber qual URL interceptar e direcionar para signalR. Para fazer isso, adicione uma classe de inicialização OWIN:

1. No **Solution Explorer,** clique com o botão direito do mouse no projeto e **selecione Adicionar** > **novo item**.

1. Em **Adicionar novo item - SignalR.StockTicker** selecione**Visual C#** > Web **instalado** > e,**em** seguida, selecione **OWIN Startup Class**.

1. Nomeie a classe *Inicialização* e selecione **OK**.

1. Substitua o código padrão no arquivo *Startup.cs* por este código:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

Você já terminou de configurar o código do servidor. Na próxima seção, você vai configurar o cliente.

## <a name="set-up-the-client-code"></a>Configure o código do cliente

Nesta seção, você configura o código que é executado no cliente.

### <a name="create-the-html-page-and-javascript-file"></a>Crie a página HTML e o arquivo JavaScript

A página HTML exibirá os dados e o arquivo JavaScript organizará os dados.

#### <a name="create-stocktickerhtml"></a>Criar StockTicker.html

Primeiro, você adicionará o cliente HTML.

1. No **Solution Explorer,** clique com o botão direito do mouse no projeto e selecione **Adicionar** > **página HTML**.

1. Nomeie o *arquivo StockTicker* e selecione **OK**.

1. Substitua o código padrão no arquivo *StockTicker.html* por este código:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    O HTML cria uma tabela com cinco colunas, uma linha de cabeçalho e uma linha de dados com uma única célula que abrange todas as cinco colunas. A linha de dados mostra "carregamento..." momentaneamente quando o aplicativo começa. O código JavaScript removerá essa linha e adicionará em suas linhas de lugar com dados de estoque recuperados do servidor.

    As tags de script especificam:

    * O arquivo de script jQuery.

    * O arquivo de script do núcleo SignalR.

    * O arquivo de script SignalR proxies.

    * Um arquivo de script stockticker que você criará mais tarde.

    O aplicativo gera dinamicamente o arquivo de script signalR proxies. Ele especifica a URL "/signalr/hubs" e define métodos proxy para os métodos `StockTickerHub.GetAllStocks`na classe Hub, neste caso, para . Se preferir, você pode gerar este arquivo JavaScript manualmente usando [utilitários SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/). Não se esqueça de desativar a `MapHubs` criação de arquivos dinâmicos na chamada do método.

1. No **Solution Explorer,** expanda **scripts**.

    Bibliotecas de scripts para jQuery e SignalR são visíveis no projeto.

    > [!IMPORTANT]
    > O gerenciador de pacotes instalará uma versão posterior dos scripts SignalR.

1. Atualize as referências de script no bloco de código para corresponder às versões dos arquivos de script no projeto.

1. No **Solution Explorer,** clique com o botão direito do *mouse stockTicker.html*e selecione **Definir como Página inicial**.

#### <a name="create-stocktickerjs"></a>Criar StockTicker.js

Agora crie o arquivo JavaScript.

1. No **Solution Explorer,** clique com o botão direito do mouse no projeto e selecione **Adicionar** > **arquivo JavaScript**.

1. Nomeie o *arquivo StockTicker* e selecione **OK**.

1. Adicione este código ao arquivo *StockTicker.js:*

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>Examine o código do cliente

Se você examinar o código do cliente, ele ajudará você a aprender como o código do cliente interage com o código do servidor para fazer o aplicativo funcionar.

#### <a name="starting-the-connection"></a>Iniciando a conexão

`$.connection`refere-se aos proxies SignalR. O código recebe uma referência `StockTickerHub` ao proxy para `ticker` a classe e coloca-o na variável. O nome do proxy é o `HubName` nome que foi definido pelo atributo:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

Depois de definir todas as variáveis e funções, a última linha de código no arquivo `start` inicializa a conexão SignalR ligando para a função SignalR. A `start` função é executada de forma assíncrona e retorna um [objeto jQuery Diferido](http://api.jquery.com/category/deferred-object/). Você pode chamar a função feita para especificar a função a ser chamada quando o aplicativo terminar a ação assíncrona.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>Obtendo todas as ações

A `init` função `getAllStocks` chama a função no servidor e usa as informações que o servidor retorna para atualizar a tabela de estoque. Observe que, por padrão, você tem que usar camelCasing no cliente, mesmo que o nome do método esteja pascal-cased no servidor. A regra do cameloCasing só se aplica a métodos, não a objetos. Por exemplo, você `stock.Symbol` `stock.Price`se `stock.symbol` refere `stock.price`e, não ou .

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

No `init` método, o aplicativo cria HTML para uma linha de tabela `formatStock` para cada `stock` objeto de estoque `supplant` recebido do servidor, `rowTemplate` chamando `stock` para formatar propriedades do objeto e, em seguida, chamando para substituir os espaços reservados na variável com os valores de propriedade do objeto. O HTML resultante é então anexado à tabela de estoque.

> [!NOTE]
> Você `init` chama passando-o `callback` como uma função que é `start` executada após o término da função assíncrona. Se você `init` chamou como uma declaração JavaScript separada após a chamada, `start`a função falharia porque seria executada imediatamente sem esperar que a função inicial terminasse de estabelecer a conexão. Nesse caso, `init` a função tentaria `getAllStocks` ligar para a função antes que o aplicativo estabelecesse uma conexão com o servidor.

#### <a name="getting-updated-stock-prices"></a>Obtendo preços atualizados das ações

Quando o servidor muda o preço de `updateStockPrice` uma ação, ele chama os clientes conectados. O aplicativo adiciona a função à `stockTicker` propriedade do cliente do proxy para torná-la disponível para chamadas do servidor.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

A `updateStockPrice` função formata um objeto de estoque recebido do servidor `init` em uma linha de tabela da mesma forma que na função. Em vez de anexar a linha à mesa, ele encontra a linha atual do estoque na tabela e substitui essa linha pela nova.

## <a name="test-the-application"></a>Testar o aplicativo

Você pode testar o aplicativo para ter certeza de que está funcionando. Você verá todas as janelas do navegador exibirem a tabela de estoque ao vivo com os preços das ações flutuando.

1. Na barra de ferramentas, ative a **Depuração de Script** e selecione o botão de reprodução para executar o aplicativo no modo Debug.

    ![Captura de tela do usuário ligando o modo de depuração e selecionando a reprodução.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    Uma janela do navegador será aberta exibindo a **Tabela de Estoque ao Vivo**. A tabela de estoque mostra inicialmente o "carregamento..." linha, então, depois de um curto período de tempo, o aplicativo mostra os dados iniciais de ações, e então os preços das ações começam a mudar.

1. Copie a URL do navegador, abra dois outros navegadores e cole as URLs nas barras de endereço.

    A exibição inicial de estoque é a mesma do primeiro navegador e as alterações acontecem simultaneamente.

1. Feche todos os navegadores, abra um novo navegador e vá para a mesma URL.

    O objeto singleton StockTicker continuou a ser executado no servidor. A **Tabela de Ações ao Vivo** mostra que as ações continuaram a mudar. Você não vê a tabela inicial sem números de mudança.

1. Feche o navegador.

## <a name="enable-logging"></a>Habilitar o registro em log

SignalR tem uma função de registro incorporada que você pode habilitar no cliente para ajudar na solução de problemas. Nesta seção, você habilita o registro e vê exemplos que mostram como os logs lhe dizem qual dos seguintes métodos de transporte o SignalR está usando:

* [WebSockets](http://en.wikipedia.org/wiki/WebSocket), suportado pelo IIS 8 e navegadores atuais.

* [Eventos enviados por servidor,](http://en.wikipedia.org/wiki/Server-sent_events)suportados por navegadores diferentes do Internet Explorer.

* [Quadro para sempre](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), suportado pelo Internet Explorer.

* [Ajax longa votação](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), apoiado por todos os navegadores.

Para qualquer conexão, o SignalR escolhe o melhor método de transporte que tanto o servidor quanto o suporte ao cliente.

1. Abrir *StockTicker.js*.

1. Adicione esta linha de código destacada para permitir o registro imediatamente antes do código que inicializa a conexão no final do arquivo:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. Pressione **F5** para executar o projeto.

1. Abra a janela de ferramentas de desenvolvedor do seu navegador e selecione o Console para ver os logs. Você pode ter que atualizar a página para ver os registros do SignalR negociando o método de transporte para uma nova conexão.

    * Se você estiver executando o Internet Explorer 10 no Windows 8 (IIS 8), o método de transporte é **WebSockets**.

    * Se você estiver executando o Internet Explorer 10 no Windows 7 (IIS 7.5), o método de transporte é **iframe**.

    * Se você estiver executando o Firefox 19 no Windows 8 (IIS 8), o método de transporte é **WebSockets**.

        > [!TIP]
        > No Firefox, instale o complemento do Firebug para obter uma janela console.

    * Se você estiver executando o Firefox 19 no Windows 7 (IIS 7.5), o método de transporte é um evento **enviado pelo servidor.**

## <a name="install-the-stockticker-sample"></a>Instale a amostra stockticker

O [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) instala o aplicativo StockTicker. O pacote NuGet inclui mais recursos do que a versão simplificada que você criou do zero. Nesta seção do tutorial, você instala o pacote NuGet e revisa os novos recursos e o código que os implementa.

> [!IMPORTANT]
> Se você instalar o pacote sem executar as etapas anteriores deste tutorial, você deve adicionar uma classe de inicialização OWIN ao seu projeto. Este arquivo readme.txt para o pacote NuGet explica esta etapa.

### <a name="install-the-signalrsample-nuget-package"></a>Instale o pacote SignalR.Sample NuGet

1. No **Gerenciador de Soluções**, clique com o botão direito no projeto e escolha **Gerenciar Pacotes NuGet**.

1. No **gerenciador de pacotes NuGet: SignalR.StockTicker,** selecione **Procurar**.

1. Na **origem do pacote,** selecione **nuget.org**.

1. Digite *SignalR.Sample* na caixa de pesquisa e selecione **Microsoft.AspNet.SignalR.Sample** > **Install**.

1. No **Solution Explorer,** expanda a pasta *SignalR.Sample.*

    A instalação do pacote SignalR.Sample criou a pasta e seu conteúdo.

1. Na pasta *SignalR.Sample,* clique com o botão direito do mouse *StockTicker.html*e selecione **Definir como página inicial**.

    > [!NOTE]
    > A instalação do pacote SignalR.Sample NuGet pode alterar a versão do jQuery que você tem na pasta *Scripts.* O novo arquivo *StockTicker.html* que o pacote instala na pasta *SignalR.Sample* estará em sincronia com a versão jQuery que o pacote instala, mas se você quiser executar seu arquivo *StockTicker.html* original novamente, você pode ter que atualizar a referência jQuery na tag script primeiro.

### <a name="run-the-application"></a>Executar o aplicativo

 A tabela que você viu no primeiro app tinha recursos úteis. O aplicativo completo de ticker de estoque mostra novos recursos: uma janela de rolagem horizontal que mostra os dados de estoque e as ações que mudam de cor à medida que sobem e caem.

1. Pressione **F5** para executar o aplicativo.

     Quando você executa o aplicativo pela primeira vez, o "mercado" é "fechado" e você vê uma tabela estática e uma janela de ticker que não está rolando.

1. Selecione **Mercado Aberto**.

    ![Captura de tela do ticker ao vivo.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * A caixa **Live Stock Ticker** começa a rolar horizontalmente, e o servidor começa a transmitir periodicamente as alterações de preço das ações em uma base aleatória.

    * Cada vez que o preço das ações muda, o aplicativo atualiza tanto a **Tabela de Ações Ao Vivo** quanto o **Ticker de Ações Ao Vivo**.

    * Quando a variação de preço de uma ação é positiva, o aplicativo mostra as ações com um fundo verde.

    * Quando a mudança é negativa, o aplicativo mostra o estoque com um fundo vermelho.

1. Selecione **Mercado Próximo**.

    * As atualizações da tabela param.

    * O ticker pára de rolar.

1. Selecione **Restaurar**.

    * Todos os dados de estoque são redefinidos.

    * O aplicativo restaura o estado inicial antes do início das mudanças de preço.

1. Copie a URL do navegador, abra dois outros navegadores e cole as URLs nas barras de endereço.

1. Você vê os mesmos dados atualizados dinamicamente ao mesmo tempo em cada navegador.

1. Quando você seleciona qualquer um dos controles, todos os navegadores respondem da mesma maneira ao mesmo tempo.

### <a name="live-stock-ticker-display"></a>Exibição live stock ticker

A exibição **Live Stock Ticker** é `<div>` uma lista não ordenada em um elemento formatado em uma única linha pelos estilos CSS. O aplicativo inicializa e atualiza o ticker da mesma forma que a `<li>` tabela: substituindo `<li>` os espaços `<ul>` reservados em uma seqüência de modelos e adicionando dinamicamente os elementos ao elemento. O aplicativo inclui rolagem usando a `animate` função jQuery para variar a margem-esquerda da lista não ordenada dentro do `<div>`.

#### <a name="signalrsample-stocktickerhtml"></a>SignalR.Sample StockTicker.html

O código HTML do ticker de ações:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR.Sample StockTicker.css

O código CSS do ticker de ações:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR.Sample SignalR.StockTicker.js

O código jQuery que o faz rolar:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Métodos adicionais no servidor que o cliente pode chamar

Para adicionar flexibilidade ao aplicativo, existem métodos adicionais que o aplicativo pode chamar.

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR.Sample StockTickerHub.cs

A `StockTickerHub` classe define quatro métodos adicionais que o cliente pode chamar:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

O aplicativo `OpenMarket` `CloseMarket`chama `Reset` , e em resposta aos botões no topo da página. Eles demonstram o padrão de um cliente desencadeando uma mudança de estado imediatamente propagada para todos os clientes. Cada um desses métodos chama `StockTicker` um método na classe que causa a mudança do estado de mercado e, em seguida, transmite o novo estado.

#### <a name="signalrsample-stocktickercs"></a>SignalR.Sample StockTicker.cs

Na `StockTicker` classe, o aplicativo mantém o `MarketState` estado do `MarketState` mercado com um imóvel que devolve um valor enum:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

Cada um dos métodos que alteram o estado de `StockTicker` mercado o faz dentro de um bloco de bloqueio porque a classe tem que ser segura de rosca:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

Para ter certeza de que esse `_marketState` código é `MarketState` seguro para `volatile`segmentos, o campo que faz parte da propriedade designada:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

Os `BroadcastMarketStateChange` `BroadcastMarketReset` métodos e métodos são semelhantes ao método BroadcastStockPrice que você já viu, exceto que eles chamam de métodos diferentes definidos no cliente:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>Funções adicionais no cliente que o servidor pode chamar

A `updateStockPrice` função agora lida com a tabela e o `jQuery.Color` visor do ticker, e usa para piscar as cores vermelha e verde.

Novas funções no *SignalR.StockTicker.js* ativam e desativam os botões com base no estado de mercado. Eles também param ou iniciam a rolagem horizontal **do Ticker de estoque vivo.** Como muitas funções estão `ticker.client`sendo adicionadas, o aplicativo usa a [função jQuery extend](http://api.jquery.com/jQuery.extend/) para adicioná-las.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Configuração adicional do cliente após estabelecer a conexão

Depois que o cliente estabelece a conexão, ele tem algum trabalho adicional a fazer:

* Descubra se o mercado está aberto ou `marketOpened` `marketClosed` fechado para ligar para o evento apropriado ou para funcionar.

* Anexar as chamadas do método do servidor aos botões.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

Os métodos do servidor não são conectados aos botões até que o aplicativo estabeleça a conexão. É para que o código não possa chamar os métodos do servidor antes que eles estejam disponíveis.

## <a name="additional-resources"></a>Recursos adicionais

Neste tutorial você aprendeu como programar um aplicativo SignalR que transmite mensagens do servidor para todos os clientes conectados. Agora você pode transmitir mensagens de forma periódica e em resposta a notificações de qualquer cliente. Você pode usar o conceito de instância de singleton multi-threaded para manter o estado do servidor em cenários de jogos online multi-jogadores. Por exemplo, consulte [o jogo ShootR baseado no SignalR](https://github.com/NTaylorMullen/ShootR).

Para tutoriais que mostram cenários de comunicação ponto a ponto, consulte [Getting Started com SignalR](introduction-to-signalr.md) e [Atualização em Tempo Real com SignalR](tutorial-high-frequency-realtime-with-signalr.md).

Para obter mais informações sobre signalR, consulte os seguintes recursos:

* [ASP.NET SignalR](../../index.md)
* [Projeto Sinalizador](http://signalr.net/)
* [SignalR GitHub e Amostras](https://github.com/SignalR/SignalR)
* [Wiki do sinalizador](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você:

> [!div class="checklist"]
> * Criou o projeto
> * Configurar o código de servidor
> * Examinou o código do servidor
> * Configure o código do cliente
> * Examinou o código do cliente
> * Testado o aplicativo
> * Registro ativado

Avance para o próximo artigo para saber como criar um aplicativo web em tempo real que usa ASP.NET SignalR 2.
> [!div class="nextstepaction"]
> [Crie um aplicativo web em tempo real com o SignalR](real-time-web-applications-with-signalr.md)
