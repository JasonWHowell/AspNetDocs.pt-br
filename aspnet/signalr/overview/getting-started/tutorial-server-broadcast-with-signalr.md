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
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="eb114-103">Tutorial: Transmissão do servidor com SignalR 2</span><span class="sxs-lookup"><span data-stu-id="eb114-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="eb114-104">Este tutorial mostra como criar um aplicativo web que usa ASP.NET SignalR 2 para fornecer funcionalidade de transmissão de servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="eb114-105">A transmissão do servidor significa que o servidor inicia as comunicações enviadas aos clientes.</span><span class="sxs-lookup"><span data-stu-id="eb114-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="eb114-106">O aplicativo que você criará neste tutorial simula um ticker de estoque, um cenário típico para a funcionalidade de transmissão de servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="eb114-107">Periodicamente, o servidor atualiza aleatoriamente os preços das ações e transmite as atualizações para todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="eb114-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="eb114-108">No navegador, os números e **Change** símbolos **%** na Alteração e colunas mudam dinamicamente em resposta às notificações do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="eb114-109">Se você abrir navegadores adicionais para a mesma URL, todos eles mostrarão os mesmos dados e as mesmas alterações nos dados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="eb114-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Criar web](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="eb114-111">Neste tutorial, você:</span><span class="sxs-lookup"><span data-stu-id="eb114-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb114-112">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="eb114-112">Create the project</span></span>
> * <span data-ttu-id="eb114-113">Configurar o código de servidor</span><span class="sxs-lookup"><span data-stu-id="eb114-113">Set up the server code</span></span>
> * <span data-ttu-id="eb114-114">Examine o código do servidor</span><span class="sxs-lookup"><span data-stu-id="eb114-114">Examine the server code</span></span>
> * <span data-ttu-id="eb114-115">Configure o código do cliente</span><span class="sxs-lookup"><span data-stu-id="eb114-115">Set up the client code</span></span>
> * <span data-ttu-id="eb114-116">Examine o código do cliente</span><span class="sxs-lookup"><span data-stu-id="eb114-116">Examine the client code</span></span>
> * <span data-ttu-id="eb114-117">Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="eb114-117">Test the application</span></span>
> * <span data-ttu-id="eb114-118">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="eb114-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eb114-119">Se você não quiser trabalhar as etapas de construção do aplicativo, você pode instalar o pacote SignalR.Sample em um novo projeto Vazio ASP.NET Web Application.</span><span class="sxs-lookup"><span data-stu-id="eb114-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="eb114-120">Se você instalar o pacote NuGet sem executar as etapas neste tutorial, você deve seguir as instruções no arquivo *readme.txt.*</span><span class="sxs-lookup"><span data-stu-id="eb114-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="eb114-121">Para executar o pacote, você precisa adicionar uma `ConfigureSignalR` classe de inicialização OWIN que chama o método no pacote instalado.</span><span class="sxs-lookup"><span data-stu-id="eb114-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="eb114-122">Você receberá um erro se não adicionar a classe de inicialização OWIN.</span><span class="sxs-lookup"><span data-stu-id="eb114-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="eb114-123">Consulte a seção Instalar a amostra [StockTicker](#install-the-stockticker-sample) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="eb114-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb114-124">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eb114-124">Prerequisites</span></span>

* <span data-ttu-id="eb114-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) com a carga de trabalho **ASP.NET e desenvolvimento para a Web**.</span><span class="sxs-lookup"><span data-stu-id="eb114-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="eb114-126">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="eb114-126">Create the project</span></span>

<span data-ttu-id="eb114-127">Esta seção mostra como usar o Visual Studio 2017 para criar um aplicativo web vazio ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="eb114-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="eb114-128">No Visual Studio, crie um aplicativo web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="eb114-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Criar web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="eb114-130">Na **nova ASP.NET web Application - SignalR.StockTicker,** deixe **Empty** selecionado e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb114-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="eb114-131">Configurar o código de servidor</span><span class="sxs-lookup"><span data-stu-id="eb114-131">Set up the server code</span></span>

<span data-ttu-id="eb114-132">Nesta seção, você configura o código que é executado no servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="eb114-133">Criar a classe Stock</span><span class="sxs-lookup"><span data-stu-id="eb114-133">Create the Stock class</span></span>

<span data-ttu-id="eb114-134">Você começa criando a classe de modelo *Stock* que você usará para armazenar e transmitir informações sobre um estoque.</span><span class="sxs-lookup"><span data-stu-id="eb114-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="eb114-135">No **Solution Explorer,** clique com o botão direito do mouse no projeto e **selecione Adicionar** > **classe**.</span><span class="sxs-lookup"><span data-stu-id="eb114-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="eb114-136">Nomeie o *estoque da* classe e adicione-o ao projeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="eb114-137">Substitua o código no arquivo *Stock.cs* por este código:</span><span class="sxs-lookup"><span data-stu-id="eb114-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="eb114-138">As duas propriedades que você definirá `Symbol` quando criar estoques são (por exemplo, MSFT para Microsoft) e `Price`.</span><span class="sxs-lookup"><span data-stu-id="eb114-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="eb114-139">As outras propriedades dependem de `Price`como e quando você definir .</span><span class="sxs-lookup"><span data-stu-id="eb114-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="eb114-140">A primeira vez `Price`que você definir `DayOpen`, o valor é propagado para .</span><span class="sxs-lookup"><span data-stu-id="eb114-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="eb114-141">Depois disso, quando `Price`você define , `Change` `PercentChange` o aplicativo calcula `Price` os `DayOpen`valores e propriedades com base na diferença entre e .</span><span class="sxs-lookup"><span data-stu-id="eb114-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="eb114-142">Crie as classes StockTickerHub e StockTicker</span><span class="sxs-lookup"><span data-stu-id="eb114-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="eb114-143">Você usará a API signalR Hub para lidar com a interação servidor-cliente.</span><span class="sxs-lookup"><span data-stu-id="eb114-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="eb114-144">Uma `StockTickerHub` classe derivada da `Hub` classe SignalR lidará com conexões recebidas e chamadas de método dos clientes.</span><span class="sxs-lookup"><span data-stu-id="eb114-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="eb114-145">Você também precisa manter dados `Timer` de estoque e executar um objeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="eb114-146">O `Timer` objeto acionará periodicamente atualizações de preços independentes das conexões do cliente.</span><span class="sxs-lookup"><span data-stu-id="eb114-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="eb114-147">Você não pode colocar essas `Hub` funções em uma classe, porque hubs são transitórios.</span><span class="sxs-lookup"><span data-stu-id="eb114-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="eb114-148">O aplicativo `Hub` cria uma instância de classe para cada tarefa no hub, como conexões e chamadas do cliente para o servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="eb114-149">Assim, o mecanismo que mantém os dados de ações, atualiza os preços e transmite as atualizações de preços tem que ser executado em uma classe separada.</span><span class="sxs-lookup"><span data-stu-id="eb114-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="eb114-150">Você vai nomear `StockTicker`a classe.</span><span class="sxs-lookup"><span data-stu-id="eb114-150">You'll name the class `StockTicker`.</span></span>

![Transmissão de StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="eb114-152">Você só quer que `StockTicker` uma instância da classe seja executada no servidor, então `StockTickerHub` você precisará `StockTicker` configurar uma referência de cada instância para a instância singleton.</span><span class="sxs-lookup"><span data-stu-id="eb114-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="eb114-153">A `StockTicker` classe tem que transmitir para os clientes porque tem `StockTicker` os dados `Hub` de estoque e aciona atualizações, mas não é uma classe.</span><span class="sxs-lookup"><span data-stu-id="eb114-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="eb114-154">A `StockTicker` classe tem que obter uma referência ao objeto de contexto de conexão SignalR Hub.</span><span class="sxs-lookup"><span data-stu-id="eb114-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="eb114-155">Em seguida, ele pode usar o objeto de contexto de conexão SignalR para transmitir aos clientes.</span><span class="sxs-lookup"><span data-stu-id="eb114-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="eb114-156">Criar StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="eb114-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="eb114-157">No **Solution Explorer,** clique com o botão direito do mouse no projeto e **selecione Adicionar** > **novo item**.</span><span class="sxs-lookup"><span data-stu-id="eb114-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="eb114-158">Em **Adicionar novo item - SignalR.StockTicker,** **selecione** > **Imagem Visual C#** > **Sinalizar da Web** > **instalada** e selecione **SignalR Hub Class (v2)**.</span><span class="sxs-lookup"><span data-stu-id="eb114-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="eb114-159">Nomeie a classe *StockTickerHub* e adicione-a ao projeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="eb114-160">Esta etapa cria o arquivo de classe *StockTickerHub.cs.*</span><span class="sxs-lookup"><span data-stu-id="eb114-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="eb114-161">Simultaneamente, ele adiciona um conjunto de arquivos de script e referências de montagem que suportasignalR para o projeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="eb114-162">Substitua o código no arquivo *StockTickerHub.cs* por este código:</span><span class="sxs-lookup"><span data-stu-id="eb114-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="eb114-163">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="eb114-163">Save the file.</span></span>

<span data-ttu-id="eb114-164">O aplicativo usa a classe [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) para definir métodos que os clientes podem chamar no servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="eb114-165">Você está definindo `GetAllStocks()`um método: .</span><span class="sxs-lookup"><span data-stu-id="eb114-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="eb114-166">Quando um cliente se conecta inicialmente ao servidor, ele chamará esse método para obter uma lista de todas as ações com seus preços atuais.</span><span class="sxs-lookup"><span data-stu-id="eb114-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="eb114-167">O método pode ser executado `IEnumerable<Stock>` sincronicamente e retornar porque está retornando dados da memória.</span><span class="sxs-lookup"><span data-stu-id="eb114-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="eb114-168">Se o método tivesse que obter os dados fazendo algo que envolvesse espera, como `Task<IEnumerable<Stock>>` uma pesquisa de banco de dados ou uma chamada de serviço web, você especificaria como o valor de retorno para permitir o processamento assíncrono.</span><span class="sxs-lookup"><span data-stu-id="eb114-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="eb114-169">Para obter mais informações, consulte [ASP.NET Guia de API signalR Hubs - Server - Quando executar assíncronamente](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span><span class="sxs-lookup"><span data-stu-id="eb114-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="eb114-170">O `HubName` atributo especifica como o aplicativo fará referência ao Código Hub em JavaScript no cliente.</span><span class="sxs-lookup"><span data-stu-id="eb114-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="eb114-171">O nome padrão no cliente se você não usar esse atributo, é uma versão camelCase do nome da classe, que neste caso seria `stockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="eb114-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="eb114-172">Como você verá mais tarde `StockTicker` quando criar a classe, o aplicativo cria `Instance` uma instância singleton dessa classe em sua propriedade estática.</span><span class="sxs-lookup"><span data-stu-id="eb114-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="eb114-173">Essa instância `StockTicker` de singleton está na memória, não importa quantos clientes conectem ou desconectem.</span><span class="sxs-lookup"><span data-stu-id="eb114-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="eb114-174">Esse exemplo é `GetAllStocks()` o que o método usa para retornar as informações atuais de estoque.</span><span class="sxs-lookup"><span data-stu-id="eb114-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="eb114-175">Criar StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="eb114-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="eb114-176">No **Solution Explorer,** clique com o botão direito do mouse no projeto e **selecione Adicionar** > **classe**.</span><span class="sxs-lookup"><span data-stu-id="eb114-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="eb114-177">Nomeie a classe *StockTicker* e adicione-a ao projeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="eb114-178">Substitua o código no arquivo *StockTicker.cs* por este código:</span><span class="sxs-lookup"><span data-stu-id="eb114-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="eb114-179">Uma vez que todos os segmentos estarão executando a mesma instância do código StockTicker, a classe StockTicker tem que ser segura de rosca.</span><span class="sxs-lookup"><span data-stu-id="eb114-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="eb114-180">Examine o código do servidor</span><span class="sxs-lookup"><span data-stu-id="eb114-180">Examine the server code</span></span>

<span data-ttu-id="eb114-181">Se você examinar o código do servidor, ele ajudará você a entender como o aplicativo funciona.</span><span class="sxs-lookup"><span data-stu-id="eb114-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="eb114-182">Armazenamento da instância singleton em um campo estático</span><span class="sxs-lookup"><span data-stu-id="eb114-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="eb114-183">O código inicializa `_instance` o campo estático que apoia a `Instance` propriedade com uma instância da classe.</span><span class="sxs-lookup"><span data-stu-id="eb114-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="eb114-184">Como o construtor é privado, é a única instância da classe que o aplicativo pode criar.</span><span class="sxs-lookup"><span data-stu-id="eb114-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="eb114-185">O aplicativo usa [inicialização Lazy](/dotnet/framework/performance/lazy-initialization) para o `_instance` campo.</span><span class="sxs-lookup"><span data-stu-id="eb114-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="eb114-186">Não é por razões de desempenho.</span><span class="sxs-lookup"><span data-stu-id="eb114-186">It's not for performance reasons.</span></span> <span data-ttu-id="eb114-187">É para ter certeza de que a criação de instâncias é segura de rosca.</span><span class="sxs-lookup"><span data-stu-id="eb114-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="eb114-188">Cada vez que um cliente se conecta ao servidor, uma nova instância da classe StockTickerHub `StockTicker.Instance` em execução em um `StockTickerHub` segmento separado obtém a instância de singleton do StockTicker da propriedade estática, como você viu anteriormente na classe.</span><span class="sxs-lookup"><span data-stu-id="eb114-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="eb114-189">Armazenamento de dados de ações em um Dicionário Simultâneo</span><span class="sxs-lookup"><span data-stu-id="eb114-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="eb114-190">A construtora inicia a `_stocks` coleta com alguns `GetAllStocks` dados de estoque amostral, e devolve os estoques.</span><span class="sxs-lookup"><span data-stu-id="eb114-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="eb114-191">Como você viu anteriormente, essa coleção `StockTickerHub.GetAllStocks`de ações é devolvida `Hub` por , que é um método de servidor na classe que os clientes podem chamar.</span><span class="sxs-lookup"><span data-stu-id="eb114-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="eb114-192">A coleção de ações é definida como um tipo [de Dicionário Simultâneo](https://msdn.microsoft.com/library/dd287191.aspx) para a segurança do segmento.</span><span class="sxs-lookup"><span data-stu-id="eb114-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="eb114-193">Como alternativa, você pode usar um objeto [dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) e bloquear explicitamente o dicionário quando você fizer alterações nele.</span><span class="sxs-lookup"><span data-stu-id="eb114-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="eb114-194">Para este aplicativo de exemplo, é OK armazenar dados de aplicativos na memória `StockTicker` e perder os dados quando o aplicativo se desfaz da ocorrência.</span><span class="sxs-lookup"><span data-stu-id="eb114-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="eb114-195">Em um aplicativo real, você trabalharia com um armazenamento de dados back-end como um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="eb114-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="eb114-196">Atualização periódica dos preços das ações</span><span class="sxs-lookup"><span data-stu-id="eb114-196">Periodically updating stock prices</span></span>

<span data-ttu-id="eb114-197">O construtor inicia `Timer` um objeto que periodicamente chama métodos que atualizam os preços das ações aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="eb114-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="eb114-198">`Timer`chamadas `UpdateStockPrices`, que passa em nulo no parâmetro estadual.</span><span class="sxs-lookup"><span data-stu-id="eb114-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="eb114-199">Antes de atualizar os preços, `_updateStockPricesLock` o aplicativo bloqueia o objeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="eb114-200">O código verifica se outro segmento já está `TryUpdateStockPrice` atualizando os preços e, em seguida, ele chama cada ação da lista.</span><span class="sxs-lookup"><span data-stu-id="eb114-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="eb114-201">O `TryUpdateStockPrice` método decide se altera o preço das ações e quanto o altera.</span><span class="sxs-lookup"><span data-stu-id="eb114-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="eb114-202">Se o preço das ações `BroadcastStockPrice` mudar, o aplicativo liga para transmitir a variação do preço das ações para todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="eb114-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="eb114-203">A `_updatingStockPrices` bandeira designada [volátil](https://msdn.microsoft.com/library/x13ttww7.aspx) para ter certeza de que é segura para rosca.</span><span class="sxs-lookup"><span data-stu-id="eb114-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="eb114-204">Em uma aplicação `TryUpdateStockPrice` real, o método chamaria um serviço web para procurar o preço.</span><span class="sxs-lookup"><span data-stu-id="eb114-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="eb114-205">Neste código, o aplicativo usa um gerador de números aleatórios para fazer alterações aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="eb114-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="eb114-206">Obtendo o contexto SignalR para que a classe StockTicker possa transmitir aos clientes</span><span class="sxs-lookup"><span data-stu-id="eb114-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="eb114-207">Como as mudanças de `StockTicker` preço se originam aqui no `updateStockPrice` objeto, é o objeto que precisa chamar um método em todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="eb114-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="eb114-208">Em `Hub` uma aula, você tem uma API `StockTicker` para chamar métodos `Hub` de cliente, mas não `Hub` deriva da classe e não tem uma referência a nenhum objeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="eb114-209">Para transmitir para clientes conectados, a `StockTicker` classe tem `StockTickerHub` que obter a instância de contexto SignalR para a classe e usá-la para chamar métodos aos clientes.</span><span class="sxs-lookup"><span data-stu-id="eb114-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="eb114-210">O código recebe uma referência ao contexto SignalR quando cria a instância de classe singleton, passa `Clients` essa referência ao construtor e o construtor o coloca na propriedade.</span><span class="sxs-lookup"><span data-stu-id="eb114-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="eb114-211">Existem duas razões pelas quais você quer obter o contexto apenas uma vez: obter o contexto é uma tarefa cara, e obtê-lo uma vez garante que o aplicativo preserve a ordem pretendida de mensagens enviadas aos clientes.</span><span class="sxs-lookup"><span data-stu-id="eb114-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="eb114-212">Obter `Clients` a propriedade do contexto e `StockTickerClient` colocá-lo na propriedade permite que você escreva código para `Hub` chamar métodos de cliente que se parece com o mesmo que seria em uma classe.</span><span class="sxs-lookup"><span data-stu-id="eb114-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="eb114-213">Por exemplo, para transmitir a `Clients.All.updateStockPrice(stock)`todos os clientes que você pode escrever .</span><span class="sxs-lookup"><span data-stu-id="eb114-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="eb114-214">O `updateStockPrice` método que você `BroadcastStockPrice` está chamando ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="eb114-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="eb114-215">Você adicionará mais tarde quando escrever código que é executado no cliente.</span><span class="sxs-lookup"><span data-stu-id="eb114-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="eb114-216">Você pode `updateStockPrice` se `Clients.All` referir aqui porque é dinâmico, o que significa que o aplicativo avaliará a expressão em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="eb114-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="eb114-217">Quando essa chamada de método for executada, o SignalR enviará o nome do método e `updateStockPrice`o valor do parâmetro para o cliente, e se o cliente tiver um método chamado, o aplicativo chamará esse método e passará o valor do parâmetro para ele.</span><span class="sxs-lookup"><span data-stu-id="eb114-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="eb114-218">`Clients.All`significa enviar para todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="eb114-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="eb114-219">O SignalR oferece outras opções para especificar para quais clientes ou grupos de clientes enviar.</span><span class="sxs-lookup"><span data-stu-id="eb114-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="eb114-220">Para obter mais informações, consulte [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="eb114-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="eb114-221">Registre a rota SignalR</span><span class="sxs-lookup"><span data-stu-id="eb114-221">Register the SignalR route</span></span>

<span data-ttu-id="eb114-222">O servidor precisa saber qual URL interceptar e direcionar para signalR.</span><span class="sxs-lookup"><span data-stu-id="eb114-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="eb114-223">Para fazer isso, adicione uma classe de inicialização OWIN:</span><span class="sxs-lookup"><span data-stu-id="eb114-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="eb114-224">No **Solution Explorer,** clique com o botão direito do mouse no projeto e **selecione Adicionar** > **novo item**.</span><span class="sxs-lookup"><span data-stu-id="eb114-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="eb114-225">Em **Adicionar novo item - SignalR.StockTicker** selecione**Visual C#** > Web **instalado** > e,**em** seguida, selecione **OWIN Startup Class**.</span><span class="sxs-lookup"><span data-stu-id="eb114-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="eb114-226">Nomeie a classe *Inicialização* e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb114-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="eb114-227">Substitua o código padrão no arquivo *Startup.cs* por este código:</span><span class="sxs-lookup"><span data-stu-id="eb114-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="eb114-228">Você já terminou de configurar o código do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="eb114-229">Na próxima seção, você vai configurar o cliente.</span><span class="sxs-lookup"><span data-stu-id="eb114-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="eb114-230">Configure o código do cliente</span><span class="sxs-lookup"><span data-stu-id="eb114-230">Set up the client code</span></span>

<span data-ttu-id="eb114-231">Nesta seção, você configura o código que é executado no cliente.</span><span class="sxs-lookup"><span data-stu-id="eb114-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="eb114-232">Crie a página HTML e o arquivo JavaScript</span><span class="sxs-lookup"><span data-stu-id="eb114-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="eb114-233">A página HTML exibirá os dados e o arquivo JavaScript organizará os dados.</span><span class="sxs-lookup"><span data-stu-id="eb114-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="eb114-234">Criar StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="eb114-234">Create StockTicker.html</span></span>

<span data-ttu-id="eb114-235">Primeiro, você adicionará o cliente HTML.</span><span class="sxs-lookup"><span data-stu-id="eb114-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="eb114-236">No **Solution Explorer,** clique com o botão direito do mouse no projeto e selecione **Adicionar** > **página HTML**.</span><span class="sxs-lookup"><span data-stu-id="eb114-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="eb114-237">Nomeie o *arquivo StockTicker* e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb114-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="eb114-238">Substitua o código padrão no arquivo *StockTicker.html* por este código:</span><span class="sxs-lookup"><span data-stu-id="eb114-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="eb114-239">O HTML cria uma tabela com cinco colunas, uma linha de cabeçalho e uma linha de dados com uma única célula que abrange todas as cinco colunas.</span><span class="sxs-lookup"><span data-stu-id="eb114-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="eb114-240">A linha de dados mostra "carregamento..." momentaneamente quando o aplicativo começa.</span><span class="sxs-lookup"><span data-stu-id="eb114-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="eb114-241">O código JavaScript removerá essa linha e adicionará em suas linhas de lugar com dados de estoque recuperados do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="eb114-242">As tags de script especificam:</span><span class="sxs-lookup"><span data-stu-id="eb114-242">The script tags specify:</span></span>

    * <span data-ttu-id="eb114-243">O arquivo de script jQuery.</span><span class="sxs-lookup"><span data-stu-id="eb114-243">The jQuery script file.</span></span>

    * <span data-ttu-id="eb114-244">O arquivo de script do núcleo SignalR.</span><span class="sxs-lookup"><span data-stu-id="eb114-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="eb114-245">O arquivo de script SignalR proxies.</span><span class="sxs-lookup"><span data-stu-id="eb114-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="eb114-246">Um arquivo de script stockticker que você criará mais tarde.</span><span class="sxs-lookup"><span data-stu-id="eb114-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="eb114-247">O aplicativo gera dinamicamente o arquivo de script signalR proxies.</span><span class="sxs-lookup"><span data-stu-id="eb114-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="eb114-248">Ele especifica a URL "/signalr/hubs" e define métodos proxy para os métodos `StockTickerHub.GetAllStocks`na classe Hub, neste caso, para .</span><span class="sxs-lookup"><span data-stu-id="eb114-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="eb114-249">Se preferir, você pode gerar este arquivo JavaScript manualmente usando [utilitários SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span><span class="sxs-lookup"><span data-stu-id="eb114-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="eb114-250">Não se esqueça de desativar a `MapHubs` criação de arquivos dinâmicos na chamada do método.</span><span class="sxs-lookup"><span data-stu-id="eb114-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="eb114-251">No **Solution Explorer,** expanda **scripts**.</span><span class="sxs-lookup"><span data-stu-id="eb114-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="eb114-252">Bibliotecas de scripts para jQuery e SignalR são visíveis no projeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="eb114-253">O gerenciador de pacotes instalará uma versão posterior dos scripts SignalR.</span><span class="sxs-lookup"><span data-stu-id="eb114-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="eb114-254">Atualize as referências de script no bloco de código para corresponder às versões dos arquivos de script no projeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="eb114-255">No **Solution Explorer,** clique com o botão direito do *mouse stockTicker.html*e selecione **Definir como Página inicial**.</span><span class="sxs-lookup"><span data-stu-id="eb114-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="eb114-256">Criar StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="eb114-256">Create StockTicker.js</span></span>

<span data-ttu-id="eb114-257">Agora crie o arquivo JavaScript.</span><span class="sxs-lookup"><span data-stu-id="eb114-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="eb114-258">No **Solution Explorer,** clique com o botão direito do mouse no projeto e selecione **Adicionar** > **arquivo JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="eb114-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="eb114-259">Nomeie o *arquivo StockTicker* e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb114-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="eb114-260">Adicione este código ao arquivo *StockTicker.js:*</span><span class="sxs-lookup"><span data-stu-id="eb114-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="eb114-261">Examine o código do cliente</span><span class="sxs-lookup"><span data-stu-id="eb114-261">Examine the client code</span></span>

<span data-ttu-id="eb114-262">Se você examinar o código do cliente, ele ajudará você a aprender como o código do cliente interage com o código do servidor para fazer o aplicativo funcionar.</span><span class="sxs-lookup"><span data-stu-id="eb114-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="eb114-263">Iniciando a conexão</span><span class="sxs-lookup"><span data-stu-id="eb114-263">Starting the connection</span></span>

<span data-ttu-id="eb114-264">`$.connection`refere-se aos proxies SignalR.</span><span class="sxs-lookup"><span data-stu-id="eb114-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="eb114-265">O código recebe uma referência `StockTickerHub` ao proxy para `ticker` a classe e coloca-o na variável.</span><span class="sxs-lookup"><span data-stu-id="eb114-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="eb114-266">O nome do proxy é o `HubName` nome que foi definido pelo atributo:</span><span class="sxs-lookup"><span data-stu-id="eb114-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="eb114-267">Depois de definir todas as variáveis e funções, a última linha de código no arquivo `start` inicializa a conexão SignalR ligando para a função SignalR.</span><span class="sxs-lookup"><span data-stu-id="eb114-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="eb114-268">A `start` função é executada de forma assíncrona e retorna um [objeto jQuery Diferido](http://api.jquery.com/category/deferred-object/).</span><span class="sxs-lookup"><span data-stu-id="eb114-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="eb114-269">Você pode chamar a função feita para especificar a função a ser chamada quando o aplicativo terminar a ação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="eb114-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="eb114-270">Obtendo todas as ações</span><span class="sxs-lookup"><span data-stu-id="eb114-270">Getting all the stocks</span></span>

<span data-ttu-id="eb114-271">A `init` função `getAllStocks` chama a função no servidor e usa as informações que o servidor retorna para atualizar a tabela de estoque.</span><span class="sxs-lookup"><span data-stu-id="eb114-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="eb114-272">Observe que, por padrão, você tem que usar camelCasing no cliente, mesmo que o nome do método esteja pascal-cased no servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="eb114-273">A regra do cameloCasing só se aplica a métodos, não a objetos.</span><span class="sxs-lookup"><span data-stu-id="eb114-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="eb114-274">Por exemplo, você `stock.Symbol` `stock.Price`se `stock.symbol` refere `stock.price`e, não ou .</span><span class="sxs-lookup"><span data-stu-id="eb114-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="eb114-275">No `init` método, o aplicativo cria HTML para uma linha de tabela `formatStock` para cada `stock` objeto de estoque `supplant` recebido do servidor, `rowTemplate` chamando `stock` para formatar propriedades do objeto e, em seguida, chamando para substituir os espaços reservados na variável com os valores de propriedade do objeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="eb114-276">O HTML resultante é então anexado à tabela de estoque.</span><span class="sxs-lookup"><span data-stu-id="eb114-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="eb114-277">Você `init` chama passando-o `callback` como uma função que é `start` executada após o término da função assíncrona.</span><span class="sxs-lookup"><span data-stu-id="eb114-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="eb114-278">Se você `init` chamou como uma declaração JavaScript separada após a chamada, `start`a função falharia porque seria executada imediatamente sem esperar que a função inicial terminasse de estabelecer a conexão.</span><span class="sxs-lookup"><span data-stu-id="eb114-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="eb114-279">Nesse caso, `init` a função tentaria `getAllStocks` ligar para a função antes que o aplicativo estabelecesse uma conexão com o servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="eb114-280">Obtendo preços atualizados das ações</span><span class="sxs-lookup"><span data-stu-id="eb114-280">Getting updated stock prices</span></span>

<span data-ttu-id="eb114-281">Quando o servidor muda o preço de `updateStockPrice` uma ação, ele chama os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="eb114-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="eb114-282">O aplicativo adiciona a função à `stockTicker` propriedade do cliente do proxy para torná-la disponível para chamadas do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="eb114-283">A `updateStockPrice` função formata um objeto de estoque recebido do servidor `init` em uma linha de tabela da mesma forma que na função.</span><span class="sxs-lookup"><span data-stu-id="eb114-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="eb114-284">Em vez de anexar a linha à mesa, ele encontra a linha atual do estoque na tabela e substitui essa linha pela nova.</span><span class="sxs-lookup"><span data-stu-id="eb114-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="eb114-285">Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="eb114-285">Test the application</span></span>

<span data-ttu-id="eb114-286">Você pode testar o aplicativo para ter certeza de que está funcionando.</span><span class="sxs-lookup"><span data-stu-id="eb114-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="eb114-287">Você verá todas as janelas do navegador exibirem a tabela de estoque ao vivo com os preços das ações flutuando.</span><span class="sxs-lookup"><span data-stu-id="eb114-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="eb114-288">Na barra de ferramentas, ative a **Depuração de Script** e selecione o botão de reprodução para executar o aplicativo no modo Debug.</span><span class="sxs-lookup"><span data-stu-id="eb114-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![Captura de tela do usuário ligando o modo de depuração e selecionando a reprodução.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="eb114-290">Uma janela do navegador será aberta exibindo a **Tabela de Estoque ao Vivo**.</span><span class="sxs-lookup"><span data-stu-id="eb114-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="eb114-291">A tabela de estoque mostra inicialmente o "carregamento..." linha, então, depois de um curto período de tempo, o aplicativo mostra os dados iniciais de ações, e então os preços das ações começam a mudar.</span><span class="sxs-lookup"><span data-stu-id="eb114-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="eb114-292">Copie a URL do navegador, abra dois outros navegadores e cole as URLs nas barras de endereço.</span><span class="sxs-lookup"><span data-stu-id="eb114-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="eb114-293">A exibição inicial de estoque é a mesma do primeiro navegador e as alterações acontecem simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="eb114-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="eb114-294">Feche todos os navegadores, abra um novo navegador e vá para a mesma URL.</span><span class="sxs-lookup"><span data-stu-id="eb114-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="eb114-295">O objeto singleton StockTicker continuou a ser executado no servidor.</span><span class="sxs-lookup"><span data-stu-id="eb114-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="eb114-296">A **Tabela de Ações ao Vivo** mostra que as ações continuaram a mudar.</span><span class="sxs-lookup"><span data-stu-id="eb114-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="eb114-297">Você não vê a tabela inicial sem números de mudança.</span><span class="sxs-lookup"><span data-stu-id="eb114-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="eb114-298">Feche o navegador.</span><span class="sxs-lookup"><span data-stu-id="eb114-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="eb114-299">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="eb114-299">Enable logging</span></span>

<span data-ttu-id="eb114-300">SignalR tem uma função de registro incorporada que você pode habilitar no cliente para ajudar na solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="eb114-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="eb114-301">Nesta seção, você habilita o registro e vê exemplos que mostram como os logs lhe dizem qual dos seguintes métodos de transporte o SignalR está usando:</span><span class="sxs-lookup"><span data-stu-id="eb114-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="eb114-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), suportado pelo IIS 8 e navegadores atuais.</span><span class="sxs-lookup"><span data-stu-id="eb114-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="eb114-303">[Eventos enviados por servidor,](http://en.wikipedia.org/wiki/Server-sent_events)suportados por navegadores diferentes do Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="eb114-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="eb114-304">[Quadro para sempre](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), suportado pelo Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="eb114-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="eb114-305">[Ajax longa votação](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), apoiado por todos os navegadores.</span><span class="sxs-lookup"><span data-stu-id="eb114-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="eb114-306">Para qualquer conexão, o SignalR escolhe o melhor método de transporte que tanto o servidor quanto o suporte ao cliente.</span><span class="sxs-lookup"><span data-stu-id="eb114-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="eb114-307">Abrir *StockTicker.js*.</span><span class="sxs-lookup"><span data-stu-id="eb114-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="eb114-308">Adicione esta linha de código destacada para permitir o registro imediatamente antes do código que inicializa a conexão no final do arquivo:</span><span class="sxs-lookup"><span data-stu-id="eb114-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="eb114-309">Pressione **F5** para executar o projeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="eb114-310">Abra a janela de ferramentas de desenvolvedor do seu navegador e selecione o Console para ver os logs.</span><span class="sxs-lookup"><span data-stu-id="eb114-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="eb114-311">Você pode ter que atualizar a página para ver os registros do SignalR negociando o método de transporte para uma nova conexão.</span><span class="sxs-lookup"><span data-stu-id="eb114-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="eb114-312">Se você estiver executando o Internet Explorer 10 no Windows 8 (IIS 8), o método de transporte é **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="eb114-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="eb114-313">Se você estiver executando o Internet Explorer 10 no Windows 7 (IIS 7.5), o método de transporte é **iframe**.</span><span class="sxs-lookup"><span data-stu-id="eb114-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="eb114-314">Se você estiver executando o Firefox 19 no Windows 8 (IIS 8), o método de transporte é **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="eb114-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="eb114-315">No Firefox, instale o complemento do Firebug para obter uma janela console.</span><span class="sxs-lookup"><span data-stu-id="eb114-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="eb114-316">Se você estiver executando o Firefox 19 no Windows 7 (IIS 7.5), o método de transporte é um evento **enviado pelo servidor.**</span><span class="sxs-lookup"><span data-stu-id="eb114-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="eb114-317">Instale a amostra stockticker</span><span class="sxs-lookup"><span data-stu-id="eb114-317">Install the StockTicker sample</span></span>

<span data-ttu-id="eb114-318">O [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) instala o aplicativo StockTicker.</span><span class="sxs-lookup"><span data-stu-id="eb114-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="eb114-319">O pacote NuGet inclui mais recursos do que a versão simplificada que você criou do zero.</span><span class="sxs-lookup"><span data-stu-id="eb114-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="eb114-320">Nesta seção do tutorial, você instala o pacote NuGet e revisa os novos recursos e o código que os implementa.</span><span class="sxs-lookup"><span data-stu-id="eb114-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eb114-321">Se você instalar o pacote sem executar as etapas anteriores deste tutorial, você deve adicionar uma classe de inicialização OWIN ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="eb114-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="eb114-322">Este arquivo readme.txt para o pacote NuGet explica esta etapa.</span><span class="sxs-lookup"><span data-stu-id="eb114-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="eb114-323">Instale o pacote SignalR.Sample NuGet</span><span class="sxs-lookup"><span data-stu-id="eb114-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="eb114-324">No **Gerenciador de Soluções**, clique com o botão direito no projeto e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="eb114-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="eb114-325">No **gerenciador de pacotes NuGet: SignalR.StockTicker,** selecione **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="eb114-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="eb114-326">Na **origem do pacote,** selecione **nuget.org**.</span><span class="sxs-lookup"><span data-stu-id="eb114-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="eb114-327">Digite *SignalR.Sample* na caixa de pesquisa e selecione **Microsoft.AspNet.SignalR.Sample** > **Install**.</span><span class="sxs-lookup"><span data-stu-id="eb114-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="eb114-328">No **Solution Explorer,** expanda a pasta *SignalR.Sample.*</span><span class="sxs-lookup"><span data-stu-id="eb114-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="eb114-329">A instalação do pacote SignalR.Sample criou a pasta e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="eb114-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="eb114-330">Na pasta *SignalR.Sample,* clique com o botão direito do mouse *StockTicker.html*e selecione **Definir como página inicial**.</span><span class="sxs-lookup"><span data-stu-id="eb114-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb114-331">A instalação do pacote SignalR.Sample NuGet pode alterar a versão do jQuery que você tem na pasta *Scripts.*</span><span class="sxs-lookup"><span data-stu-id="eb114-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="eb114-332">O novo arquivo *StockTicker.html* que o pacote instala na pasta *SignalR.Sample* estará em sincronia com a versão jQuery que o pacote instala, mas se você quiser executar seu arquivo *StockTicker.html* original novamente, você pode ter que atualizar a referência jQuery na tag script primeiro.</span><span class="sxs-lookup"><span data-stu-id="eb114-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="eb114-333">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="eb114-333">Run the application</span></span>

 <span data-ttu-id="eb114-334">A tabela que você viu no primeiro app tinha recursos úteis.</span><span class="sxs-lookup"><span data-stu-id="eb114-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="eb114-335">O aplicativo completo de ticker de estoque mostra novos recursos: uma janela de rolagem horizontal que mostra os dados de estoque e as ações que mudam de cor à medida que sobem e caem.</span><span class="sxs-lookup"><span data-stu-id="eb114-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="eb114-336">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eb114-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="eb114-337">Quando você executa o aplicativo pela primeira vez, o "mercado" é "fechado" e você vê uma tabela estática e uma janela de ticker que não está rolando.</span><span class="sxs-lookup"><span data-stu-id="eb114-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="eb114-338">Selecione **Mercado Aberto**.</span><span class="sxs-lookup"><span data-stu-id="eb114-338">Select **Open Market**.</span></span>

    ![Captura de tela do ticker ao vivo.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="eb114-340">A caixa **Live Stock Ticker** começa a rolar horizontalmente, e o servidor começa a transmitir periodicamente as alterações de preço das ações em uma base aleatória.</span><span class="sxs-lookup"><span data-stu-id="eb114-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="eb114-341">Cada vez que o preço das ações muda, o aplicativo atualiza tanto a **Tabela de Ações Ao Vivo** quanto o **Ticker de Ações Ao Vivo**.</span><span class="sxs-lookup"><span data-stu-id="eb114-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="eb114-342">Quando a variação de preço de uma ação é positiva, o aplicativo mostra as ações com um fundo verde.</span><span class="sxs-lookup"><span data-stu-id="eb114-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="eb114-343">Quando a mudança é negativa, o aplicativo mostra o estoque com um fundo vermelho.</span><span class="sxs-lookup"><span data-stu-id="eb114-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="eb114-344">Selecione **Mercado Próximo**.</span><span class="sxs-lookup"><span data-stu-id="eb114-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="eb114-345">As atualizações da tabela param.</span><span class="sxs-lookup"><span data-stu-id="eb114-345">The table updates stop.</span></span>

    * <span data-ttu-id="eb114-346">O ticker pára de rolar.</span><span class="sxs-lookup"><span data-stu-id="eb114-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="eb114-347">Selecione **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="eb114-347">Select **Reset**.</span></span>

    * <span data-ttu-id="eb114-348">Todos os dados de estoque são redefinidos.</span><span class="sxs-lookup"><span data-stu-id="eb114-348">All stock data is reset.</span></span>

    * <span data-ttu-id="eb114-349">O aplicativo restaura o estado inicial antes do início das mudanças de preço.</span><span class="sxs-lookup"><span data-stu-id="eb114-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="eb114-350">Copie a URL do navegador, abra dois outros navegadores e cole as URLs nas barras de endereço.</span><span class="sxs-lookup"><span data-stu-id="eb114-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="eb114-351">Você vê os mesmos dados atualizados dinamicamente ao mesmo tempo em cada navegador.</span><span class="sxs-lookup"><span data-stu-id="eb114-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="eb114-352">Quando você seleciona qualquer um dos controles, todos os navegadores respondem da mesma maneira ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="eb114-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="eb114-353">Exibição live stock ticker</span><span class="sxs-lookup"><span data-stu-id="eb114-353">Live Stock Ticker display</span></span>

<span data-ttu-id="eb114-354">A exibição **Live Stock Ticker** é `<div>` uma lista não ordenada em um elemento formatado em uma única linha pelos estilos CSS.</span><span class="sxs-lookup"><span data-stu-id="eb114-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="eb114-355">O aplicativo inicializa e atualiza o ticker da mesma forma que a `<li>` tabela: substituindo `<li>` os espaços `<ul>` reservados em uma seqüência de modelos e adicionando dinamicamente os elementos ao elemento.</span><span class="sxs-lookup"><span data-stu-id="eb114-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="eb114-356">O aplicativo inclui rolagem usando a `animate` função jQuery para variar a margem-esquerda da lista não ordenada dentro do `<div>`.</span><span class="sxs-lookup"><span data-stu-id="eb114-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="eb114-357">SignalR.Sample StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="eb114-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="eb114-358">O código HTML do ticker de ações:</span><span class="sxs-lookup"><span data-stu-id="eb114-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="eb114-359">SignalR.Sample StockTicker.css</span><span class="sxs-lookup"><span data-stu-id="eb114-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="eb114-360">O código CSS do ticker de ações:</span><span class="sxs-lookup"><span data-stu-id="eb114-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="eb114-361">SignalR.Sample SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="eb114-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="eb114-362">O código jQuery que o faz rolar:</span><span class="sxs-lookup"><span data-stu-id="eb114-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="eb114-363">Métodos adicionais no servidor que o cliente pode chamar</span><span class="sxs-lookup"><span data-stu-id="eb114-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="eb114-364">Para adicionar flexibilidade ao aplicativo, existem métodos adicionais que o aplicativo pode chamar.</span><span class="sxs-lookup"><span data-stu-id="eb114-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="eb114-365">SignalR.Sample StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="eb114-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="eb114-366">A `StockTickerHub` classe define quatro métodos adicionais que o cliente pode chamar:</span><span class="sxs-lookup"><span data-stu-id="eb114-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="eb114-367">O aplicativo `OpenMarket` `CloseMarket`chama `Reset` , e em resposta aos botões no topo da página.</span><span class="sxs-lookup"><span data-stu-id="eb114-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="eb114-368">Eles demonstram o padrão de um cliente desencadeando uma mudança de estado imediatamente propagada para todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="eb114-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="eb114-369">Cada um desses métodos chama `StockTicker` um método na classe que causa a mudança do estado de mercado e, em seguida, transmite o novo estado.</span><span class="sxs-lookup"><span data-stu-id="eb114-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="eb114-370">SignalR.Sample StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="eb114-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="eb114-371">Na `StockTicker` classe, o aplicativo mantém o `MarketState` estado do `MarketState` mercado com um imóvel que devolve um valor enum:</span><span class="sxs-lookup"><span data-stu-id="eb114-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="eb114-372">Cada um dos métodos que alteram o estado de `StockTicker` mercado o faz dentro de um bloco de bloqueio porque a classe tem que ser segura de rosca:</span><span class="sxs-lookup"><span data-stu-id="eb114-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="eb114-373">Para ter certeza de que esse `_marketState` código é `MarketState` seguro para `volatile`segmentos, o campo que faz parte da propriedade designada:</span><span class="sxs-lookup"><span data-stu-id="eb114-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="eb114-374">Os `BroadcastMarketStateChange` `BroadcastMarketReset` métodos e métodos são semelhantes ao método BroadcastStockPrice que você já viu, exceto que eles chamam de métodos diferentes definidos no cliente:</span><span class="sxs-lookup"><span data-stu-id="eb114-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="eb114-375">Funções adicionais no cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="eb114-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="eb114-376">A `updateStockPrice` função agora lida com a tabela e o `jQuery.Color` visor do ticker, e usa para piscar as cores vermelha e verde.</span><span class="sxs-lookup"><span data-stu-id="eb114-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="eb114-377">Novas funções no *SignalR.StockTicker.js* ativam e desativam os botões com base no estado de mercado.</span><span class="sxs-lookup"><span data-stu-id="eb114-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="eb114-378">Eles também param ou iniciam a rolagem horizontal **do Ticker de estoque vivo.**</span><span class="sxs-lookup"><span data-stu-id="eb114-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="eb114-379">Como muitas funções estão `ticker.client`sendo adicionadas, o aplicativo usa a [função jQuery extend](http://api.jquery.com/jQuery.extend/) para adicioná-las.</span><span class="sxs-lookup"><span data-stu-id="eb114-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="eb114-380">Configuração adicional do cliente após estabelecer a conexão</span><span class="sxs-lookup"><span data-stu-id="eb114-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="eb114-381">Depois que o cliente estabelece a conexão, ele tem algum trabalho adicional a fazer:</span><span class="sxs-lookup"><span data-stu-id="eb114-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="eb114-382">Descubra se o mercado está aberto ou `marketOpened` `marketClosed` fechado para ligar para o evento apropriado ou para funcionar.</span><span class="sxs-lookup"><span data-stu-id="eb114-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="eb114-383">Anexar as chamadas do método do servidor aos botões.</span><span class="sxs-lookup"><span data-stu-id="eb114-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="eb114-384">Os métodos do servidor não são conectados aos botões até que o aplicativo estabeleça a conexão.</span><span class="sxs-lookup"><span data-stu-id="eb114-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="eb114-385">É para que o código não possa chamar os métodos do servidor antes que eles estejam disponíveis.</span><span class="sxs-lookup"><span data-stu-id="eb114-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb114-386">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="eb114-386">Additional resources</span></span>

<span data-ttu-id="eb114-387">Neste tutorial você aprendeu como programar um aplicativo SignalR que transmite mensagens do servidor para todos os clientes conectados.</span><span class="sxs-lookup"><span data-stu-id="eb114-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="eb114-388">Agora você pode transmitir mensagens de forma periódica e em resposta a notificações de qualquer cliente.</span><span class="sxs-lookup"><span data-stu-id="eb114-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="eb114-389">Você pode usar o conceito de instância de singleton multi-threaded para manter o estado do servidor em cenários de jogos online multi-jogadores.</span><span class="sxs-lookup"><span data-stu-id="eb114-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="eb114-390">Por exemplo, consulte [o jogo ShootR baseado no SignalR](https://github.com/NTaylorMullen/ShootR).</span><span class="sxs-lookup"><span data-stu-id="eb114-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="eb114-391">Para tutoriais que mostram cenários de comunicação ponto a ponto, consulte [Getting Started com SignalR](introduction-to-signalr.md) e [Atualização em Tempo Real com SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="eb114-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="eb114-392">Para obter mais informações sobre signalR, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="eb114-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="eb114-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="eb114-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="eb114-394">Projeto Sinalizador</span><span class="sxs-lookup"><span data-stu-id="eb114-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="eb114-395">SignalR GitHub e Amostras</span><span class="sxs-lookup"><span data-stu-id="eb114-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="eb114-396">Wiki do sinalizador</span><span class="sxs-lookup"><span data-stu-id="eb114-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="eb114-397">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eb114-397">Next steps</span></span>

<span data-ttu-id="eb114-398">Neste tutorial, você:</span><span class="sxs-lookup"><span data-stu-id="eb114-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb114-399">Criou o projeto</span><span class="sxs-lookup"><span data-stu-id="eb114-399">Created the project</span></span>
> * <span data-ttu-id="eb114-400">Configurar o código de servidor</span><span class="sxs-lookup"><span data-stu-id="eb114-400">Set up the server code</span></span>
> * <span data-ttu-id="eb114-401">Examinou o código do servidor</span><span class="sxs-lookup"><span data-stu-id="eb114-401">Examined the server code</span></span>
> * <span data-ttu-id="eb114-402">Configure o código do cliente</span><span class="sxs-lookup"><span data-stu-id="eb114-402">Set up the client code</span></span>
> * <span data-ttu-id="eb114-403">Examinou o código do cliente</span><span class="sxs-lookup"><span data-stu-id="eb114-403">Examined the client code</span></span>
> * <span data-ttu-id="eb114-404">Testado o aplicativo</span><span class="sxs-lookup"><span data-stu-id="eb114-404">Tested the application</span></span>
> * <span data-ttu-id="eb114-405">Registro ativado</span><span class="sxs-lookup"><span data-stu-id="eb114-405">Enabled logging</span></span>

<span data-ttu-id="eb114-406">Avance para o próximo artigo para saber como criar um aplicativo web em tempo real que usa ASP.NET SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="eb114-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="eb114-407">Crie um aplicativo web em tempo real com o SignalR</span><span class="sxs-lookup"><span data-stu-id="eb114-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
