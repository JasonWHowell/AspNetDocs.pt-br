---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: Expansão do SignalR com o SQL Server (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386550"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a><span data-ttu-id="566a0-102">Expansão do SignalR com o SQL Server (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="566a0-102">SignalR Scaleout with SQL Server (SignalR 1.x)</span></span>

<span data-ttu-id="566a0-103">por [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="566a0-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="566a0-104">Neste tutorial, você usará o SQL Server para distribuir mensagens através de um aplicativo de SignalR é implantado em duas instâncias separadas do IIS.</span><span class="sxs-lookup"><span data-stu-id="566a0-104">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="566a0-105">Você também pode executar este tutorial em um computador de teste único, mas para obter o efeito completo, você precisará implantar o aplicativo do SignalR em dois ou mais servidores.</span><span class="sxs-lookup"><span data-stu-id="566a0-105">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="566a0-106">Você também deve instalar o SQL Server em um dos servidores, ou em um servidor dedicado separado.</span><span class="sxs-lookup"><span data-stu-id="566a0-106">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="566a0-107">Outra opção é executar o tutorial usando as máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="566a0-107">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="566a0-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="566a0-108">Prerequisites</span></span>

<span data-ttu-id="566a0-109">Microsoft SQL Server 2005 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="566a0-109">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="566a0-110">Backplane dá suporte a edições de área de trabalho e o servidor do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="566a0-110">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="566a0-111">Ele não oferece suporte a banco de dados do Azure ou SQL Server Compact Edition.</span><span class="sxs-lookup"><span data-stu-id="566a0-111">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="566a0-112">(Se seu aplicativo estiver hospedado no Azure, considere o backplane do barramento de serviço em vez disso.)</span><span class="sxs-lookup"><span data-stu-id="566a0-112">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="566a0-113">Visão geral</span><span class="sxs-lookup"><span data-stu-id="566a0-113">Overview</span></span>

<span data-ttu-id="566a0-114">Antes de passarmos para o tutorial detalhado, aqui está uma visão rápida do que você deve fazer.</span><span class="sxs-lookup"><span data-stu-id="566a0-114">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="566a0-115">Crie um novo banco de dados vazio.</span><span class="sxs-lookup"><span data-stu-id="566a0-115">Create a new empty database.</span></span> <span data-ttu-id="566a0-116">Backplane criará as tabelas necessárias neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="566a0-116">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="566a0-117">Adicione esses pacotes do NuGet ao seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="566a0-117">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="566a0-118">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="566a0-118">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="566a0-119">Microsoft.AspNet.SignalR.SqlServer</span><span class="sxs-lookup"><span data-stu-id="566a0-119">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="566a0-120">Crie um aplicativo do SignalR.</span><span class="sxs-lookup"><span data-stu-id="566a0-120">Create a SignalR application.</span></span>
4. <span data-ttu-id="566a0-121">Adicione o seguinte código ao global. asax para configurar o backplane:</span><span class="sxs-lookup"><span data-stu-id="566a0-121">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a><span data-ttu-id="566a0-122">Configurar o banco de dados</span><span class="sxs-lookup"><span data-stu-id="566a0-122">Configure the Database</span></span>

<span data-ttu-id="566a0-123">Decida se o aplicativo usará a autenticação do Windows ou autenticação do SQL Server para acessar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="566a0-123">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="566a0-124">Independentemente disso, certifique-se de que o usuário de banco de dados tem permissões para fazer logon, criar esquemas e criar tabelas.</span><span class="sxs-lookup"><span data-stu-id="566a0-124">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="566a0-125">Crie um novo banco de dados para o backplane usar.</span><span class="sxs-lookup"><span data-stu-id="566a0-125">Create a new database for the backplane to use.</span></span> <span data-ttu-id="566a0-126">Você pode atribuir qualquer nome para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="566a0-126">You can give the database any name.</span></span> <span data-ttu-id="566a0-127">Você não precisa criar todas as tabelas no banco de dados; backplane criará as tabelas necessárias.</span><span class="sxs-lookup"><span data-stu-id="566a0-127">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="566a0-128">Habilite o Service Broker</span><span class="sxs-lookup"><span data-stu-id="566a0-128">Enable Service Broker</span></span>

<span data-ttu-id="566a0-129">É recomendável habilitar o Service Broker para o banco de dados do backplane.</span><span class="sxs-lookup"><span data-stu-id="566a0-129">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="566a0-130">O Service Broker fornece suporte nativo para mensagens e enfileiramento no SQL Server, que permite que o backplane receber atualizações com mais eficiência.</span><span class="sxs-lookup"><span data-stu-id="566a0-130">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="566a0-131">(No entanto, o backplane também funciona sem o Service Broker.)</span><span class="sxs-lookup"><span data-stu-id="566a0-131">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="566a0-132">Para verificar se o Service Broker está habilitado, consulte o **está\_broker\_habilitada** coluna no **sys. Databases** exibição do catálogo.</span><span class="sxs-lookup"><span data-stu-id="566a0-132">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="566a0-133">Para habilitar o Service Broker, use a seguinte consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="566a0-133">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="566a0-134">Se essa consulta é exibido um deadlock, certifique-se não há nenhum aplicativo conectado ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="566a0-134">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="566a0-135">Se você tiver habilitado o rastreamento, os rastreamentos também mostrará se o Service Broker está habilitado.</span><span class="sxs-lookup"><span data-stu-id="566a0-135">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="566a0-136">Criar um aplicativo de SignalR</span><span class="sxs-lookup"><span data-stu-id="566a0-136">Create a SignalR Application</span></span>

<span data-ttu-id="566a0-137">Crie um aplicativo do SignalR, seguindo um destes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="566a0-137">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="566a0-138">Introdução ao SignalR</span><span class="sxs-lookup"><span data-stu-id="566a0-138">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="566a0-139">Introdução ao SignalR e MVC 4</span><span class="sxs-lookup"><span data-stu-id="566a0-139">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="566a0-140">Em seguida, modificaremos o aplicativo de bate-papo para dar suporte à expansão com o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="566a0-140">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="566a0-141">Primeiro, adicione o pacote do SignalR.SqlServer NuGet ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="566a0-141">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="566a0-142">No Visual Studio, do **ferramentas** menu, selecione **Gerenciador de pacotes NuGet**, em seguida, selecione **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="566a0-142">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="566a0-143">Na janela do Console do Gerenciador de pacotes, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="566a0-143">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="566a0-144">Em seguida, abra o arquivo global asax.</span><span class="sxs-lookup"><span data-stu-id="566a0-144">Next, open the Global.asax file.</span></span> <span data-ttu-id="566a0-145">Adicione o seguinte código para o **Application\_iniciar** método:</span><span class="sxs-lookup"><span data-stu-id="566a0-145">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="566a0-146">Implantar e executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="566a0-146">Deploy and Run the Application</span></span>

<span data-ttu-id="566a0-147">Prepare suas instâncias do Windows Server para implantar o aplicativo do SignalR.</span><span class="sxs-lookup"><span data-stu-id="566a0-147">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="566a0-148">Adicione a função do IIS.</span><span class="sxs-lookup"><span data-stu-id="566a0-148">Add the IIS role.</span></span> <span data-ttu-id="566a0-149">Inclua recursos de "Desenvolvimento de aplicativos", incluindo o protocolo WebSocket.</span><span class="sxs-lookup"><span data-stu-id="566a0-149">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="566a0-150">Também incluem o serviço de gerenciamento (listados em "Ferramentas de gerenciamento").</span><span class="sxs-lookup"><span data-stu-id="566a0-150">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="566a0-151">**Install Web implantação 3.0.**</span><span class="sxs-lookup"><span data-stu-id="566a0-151">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="566a0-152">Quando você executar o Gerenciador do IIS, ele solicitará que você instale o Microsoft Web Platform, ou pode [baixar o instalador](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="566a0-152">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="566a0-153">No instalador da plataforma, procure implantação da Web e instale o Web Deploy 3.0</span><span class="sxs-lookup"><span data-stu-id="566a0-153">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="566a0-154">Verifique se o serviço de gerenciamento da Web está em execução.</span><span class="sxs-lookup"><span data-stu-id="566a0-154">Check that the Web Management Service is running.</span></span> <span data-ttu-id="566a0-155">Caso contrário, inicie o serviço.</span><span class="sxs-lookup"><span data-stu-id="566a0-155">If not, start the service.</span></span> <span data-ttu-id="566a0-156">(Se você não vir o serviço de gerenciamento da Web na lista de serviços do Windows, certifique-se de que você instalou o serviço de gerenciamento quando você adicionou a função do IIS.)</span><span class="sxs-lookup"><span data-stu-id="566a0-156">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="566a0-157">Por fim, abra a porta 8172 para TCP.</span><span class="sxs-lookup"><span data-stu-id="566a0-157">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="566a0-158">Essa é a porta que usa a ferramenta de implantação da Web.</span><span class="sxs-lookup"><span data-stu-id="566a0-158">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="566a0-159">Agora você está pronto para implantar o projeto do Visual Studio em seu computador de desenvolvimento para o servidor.</span><span class="sxs-lookup"><span data-stu-id="566a0-159">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="566a0-160">No Gerenciador de soluções, clique com botão direito a solução e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="566a0-160">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="566a0-161">Para obter mais documentação sobre a implantação da web, consulte [mapa de conteúdo de implantação da Web para Visual Studio e o ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="566a0-161">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="566a0-162">Se você implantar o aplicativo em dois servidores, você pode abrir cada instância em uma janela separada do navegador e ver que cada um receba mensagens do SignalR de outra.</span><span class="sxs-lookup"><span data-stu-id="566a0-162">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="566a0-163">(É claro que, em um ambiente de produção, os dois servidores estaria atrás de um balanceador de carga.)</span><span class="sxs-lookup"><span data-stu-id="566a0-163">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="566a0-164">Depois de executar o aplicativo, você pode ver que o SignalR cria automaticamente tabelas no banco de dados:</span><span class="sxs-lookup"><span data-stu-id="566a0-164">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="566a0-165">O SignalR gerencia as tabelas.</span><span class="sxs-lookup"><span data-stu-id="566a0-165">SignalR manages the tables.</span></span> <span data-ttu-id="566a0-166">Desde que o aplicativo for implantado, não excluir linhas, modifique a tabela e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="566a0-166">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
