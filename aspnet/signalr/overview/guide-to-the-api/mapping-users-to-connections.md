---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: Mapeando usuários de SignalR para conexões | Microsoft Docs
author: bradygaster
description: Este tópico mostra como reter informações sobre os usuários e suas conexões. Patrick Fletcher ajudou a escrever este tópico. Versões de software usadas neste tópico...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676156"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="32022-105">Mapeamento de usuários do SignalR para conexões</span><span class="sxs-lookup"><span data-stu-id="32022-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="32022-106"> por [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="32022-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="32022-107">Este tópico mostra como reter informações sobre os usuários e suas conexões.</span><span class="sxs-lookup"><span data-stu-id="32022-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="32022-108">Patrick Fletcher ajudou a escrever este tópico.</span><span class="sxs-lookup"><span data-stu-id="32022-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="32022-109">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="32022-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="32022-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="32022-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="32022-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="32022-111">.NET 4.5</span></span>
> - <span data-ttu-id="32022-112">SignalR versão 2</span><span class="sxs-lookup"><span data-stu-id="32022-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="32022-113">Versões anteriores deste tópico</span><span class="sxs-lookup"><span data-stu-id="32022-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="32022-114">Para obter informações sobre versões anteriores do SignalR, consulte [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="32022-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="32022-115">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="32022-115">Questions and comments</span></span>
>
> <span data-ttu-id="32022-116">Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="32022-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="32022-117">Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="32022-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="32022-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="32022-118">Introduction</span></span>

<span data-ttu-id="32022-119">Cada cliente conectado a um hub passa um id de conexão único. Você pode recuperar esse `Context.ConnectionId` valor na propriedade do contexto do hub.</span><span class="sxs-lookup"><span data-stu-id="32022-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="32022-120">Se o seu aplicativo precisar mapear um usuário para o id de conexão e persistir esse mapeamento, você pode usar um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="32022-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="32022-121">O provedor de id do usuário (Signalr 2)</span><span class="sxs-lookup"><span data-stu-id="32022-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="32022-122">[Armazenamento na memória,](#inmemory)como um dicionário</span><span class="sxs-lookup"><span data-stu-id="32022-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="32022-123">Grupo SignalR para cada usuário</span><span class="sxs-lookup"><span data-stu-id="32022-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="32022-124">[Armazenamento externo permanente,](#database)como uma tabela de banco de dados ou armazenamento de tabela azure</span><span class="sxs-lookup"><span data-stu-id="32022-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="32022-125">Cada uma dessas implementações é mostrada neste tópico.</span><span class="sxs-lookup"><span data-stu-id="32022-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="32022-126">Você usa `OnConnected` `OnDisconnected`os `OnReconnected` métodos e `Hub` métodos da classe para rastrear o status da conexão do usuário.</span><span class="sxs-lookup"><span data-stu-id="32022-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="32022-127">A melhor abordagem para sua aplicação depende de:</span><span class="sxs-lookup"><span data-stu-id="32022-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="32022-128">O número de servidores web que hospedam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32022-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="32022-129">Se você precisa obter uma lista dos usuários conectados no momento.</span><span class="sxs-lookup"><span data-stu-id="32022-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="32022-130">Se você precisa persistir as informações de grupo e do usuário quando o aplicativo ou servidor é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="32022-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="32022-131">Se a latência de chamar um servidor externo é um problema.</span><span class="sxs-lookup"><span data-stu-id="32022-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="32022-132">A tabela a seguir mostra qual abordagem funciona para essas considerações.</span><span class="sxs-lookup"><span data-stu-id="32022-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="32022-133">Mais de um servidor</span><span class="sxs-lookup"><span data-stu-id="32022-133">More than one server</span></span> | <span data-ttu-id="32022-134">Obtenha lista de usuários conectados no momento</span><span class="sxs-lookup"><span data-stu-id="32022-134">Get list of currently connected users</span></span> | <span data-ttu-id="32022-135">Persistir informações após reinicializações</span><span class="sxs-lookup"><span data-stu-id="32022-135">Persist information after restarts</span></span> | <span data-ttu-id="32022-136">Desempenho ideal</span><span class="sxs-lookup"><span data-stu-id="32022-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="32022-137">Provedor de usuário</span><span class="sxs-lookup"><span data-stu-id="32022-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="32022-138">Na memória</span><span class="sxs-lookup"><span data-stu-id="32022-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="32022-139">Grupos de usuários únicos</span><span class="sxs-lookup"><span data-stu-id="32022-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="32022-140">Permanente, externo</span><span class="sxs-lookup"><span data-stu-id="32022-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="32022-141">Provedor IUserID</span><span class="sxs-lookup"><span data-stu-id="32022-141">IUserID provider</span></span>

<span data-ttu-id="32022-142">Esse recurso permite que os usuários especifiquem o que o IId é baseado em uma IRequest através de uma nova interface IUserIdProvider.</span><span class="sxs-lookup"><span data-stu-id="32022-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="32022-143">**O Provedor iUserId**</span><span class="sxs-lookup"><span data-stu-id="32022-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="32022-144">Por padrão, haverá uma implementação que `IPrincipal.Identity.Name` usa o do usuário como nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="32022-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="32022-145">Para alterar isso, registre `IUserIdProvider` sua implementação com o host global quando a sua aplicação começar:</span><span class="sxs-lookup"><span data-stu-id="32022-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="32022-146">A partir de um hub, você poderá enviar mensagens para esses usuários através da seguinte API:</span><span class="sxs-lookup"><span data-stu-id="32022-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="32022-147">**Enviando uma mensagem para um usuário específico**</span><span class="sxs-lookup"><span data-stu-id="32022-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="32022-148">Armazenamento na memória</span><span class="sxs-lookup"><span data-stu-id="32022-148">In-memory storage</span></span>

<span data-ttu-id="32022-149">Os exemplos a seguir mostram como reter a conexão e as informações do usuário em um dicionário armazenado na memória.</span><span class="sxs-lookup"><span data-stu-id="32022-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="32022-150">O dicionário `HashSet` usa um para armazenar o id de conexão. A qualquer momento, um usuário pode ter mais de uma conexão com o aplicativo SignalR.</span><span class="sxs-lookup"><span data-stu-id="32022-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="32022-151">Por exemplo, um usuário que esteja conectado através de vários dispositivos ou mais de uma guia do navegador teria mais de um id de conexão.</span><span class="sxs-lookup"><span data-stu-id="32022-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="32022-152">Se o aplicativo for desligado, todas as informações serão perdidas, mas serão repovoadas à medida que os usuários restabelecerem suas conexões.</span><span class="sxs-lookup"><span data-stu-id="32022-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="32022-153">O armazenamento na memória não funciona se o ambiente incluir mais de um servidor web porque cada servidor teria uma coleção separada de conexões.</span><span class="sxs-lookup"><span data-stu-id="32022-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="32022-154">O primeiro exemplo mostra uma classe que gerencia o mapeamento dos usuários para conexões.</span><span class="sxs-lookup"><span data-stu-id="32022-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="32022-155">A chave para o HashSet será o nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="32022-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="32022-156">O próximo exemplo mostra como usar a classe de mapeamento de conexão a partir de um hub.</span><span class="sxs-lookup"><span data-stu-id="32022-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="32022-157">A instância da classe é armazenada `_connections`em um nome variável .</span><span class="sxs-lookup"><span data-stu-id="32022-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="32022-158">Grupos de usuários únicos</span><span class="sxs-lookup"><span data-stu-id="32022-158">Single-user groups</span></span>

<span data-ttu-id="32022-159">Você pode criar um grupo para cada usuário e, em seguida, enviar uma mensagem para esse grupo quando você quiser alcançar apenas esse usuário.</span><span class="sxs-lookup"><span data-stu-id="32022-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="32022-160">O nome de cada grupo é o nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="32022-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="32022-161">Se um usuário tiver mais de uma conexão, cada id de conexão será adicionado ao grupo do usuário.</span><span class="sxs-lookup"><span data-stu-id="32022-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="32022-162">Você não deve remover manualmente o usuário do grupo quando o usuário se desconectar.</span><span class="sxs-lookup"><span data-stu-id="32022-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="32022-163">Esta ação é realizada automaticamente pela estrutura SignalR.</span><span class="sxs-lookup"><span data-stu-id="32022-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="32022-164">O exemplo a seguir mostra como implementar grupos de usuários únicos.</span><span class="sxs-lookup"><span data-stu-id="32022-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="32022-165">Armazenamento externo permanente</span><span class="sxs-lookup"><span data-stu-id="32022-165">Permanent, external storage</span></span>

<span data-ttu-id="32022-166">Este tópico mostra como usar um banco de dados ou o armazenamento de tabela do Azure para armazenar informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="32022-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="32022-167">Essa abordagem funciona quando você tem vários servidores web porque cada servidor web pode interagir com o mesmo repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="32022-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="32022-168">Se os servidores da Web pararem de `OnDisconnected` funcionar ou o aplicativo for reiniciado, o método não será chamado.</span><span class="sxs-lookup"><span data-stu-id="32022-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="32022-169">Portanto, é possível que seu repositório de dados tenha registros de ids de conexão que não são mais válidos.</span><span class="sxs-lookup"><span data-stu-id="32022-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="32022-170">Para limpar esses registros órfãos, você pode querer invalidar qualquer conexão que foi criada fora de um prazo que seja relevante para sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="32022-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="32022-171">Os exemplos nesta seção incluem um valor para rastreamento quando a conexão foi criada, mas não mostram como limpar registros antigos porque você pode querer fazer isso como processo de fundo.</span><span class="sxs-lookup"><span data-stu-id="32022-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="32022-172">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="32022-172">Database</span></span>

<span data-ttu-id="32022-173">Os exemplos a seguir mostram como reter conexão e informações do usuário em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="32022-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="32022-174">Você pode usar qualquer tecnologia de acesso a dados; no entanto, o exemplo abaixo mostra como definir modelos usando o Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="32022-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="32022-175">Esses modelos de entidade correspondem a tabelas e campos de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="32022-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="32022-176">Sua estrutura de dados pode variar consideravelmente dependendo dos requisitos de sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="32022-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="32022-177">O primeiro exemplo mostra como definir uma entidade de usuário que pode ser associada a muitas entidades de conexão.</span><span class="sxs-lookup"><span data-stu-id="32022-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="32022-178">Em seguida, a partir do hub, você pode rastrear o estado de cada conexão com o código mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="32022-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="32022-179">Armazenamento de tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="32022-179">Azure table storage</span></span>

<span data-ttu-id="32022-180">O exemplo a seguir de armazenamento de tabela do Azure é semelhante ao exemplo do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="32022-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="32022-181">Ele não inclui todas as informações que você precisaria para começar com o Azure Table Storage Service.</span><span class="sxs-lookup"><span data-stu-id="32022-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="32022-182">Para obter informações, [consulte Como usar o armazenamento de tabela do .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="32022-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="32022-183">O exemplo a seguir mostra uma entidade de tabela para armazenar informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="32022-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="32022-184">Ele divide os dados pelo nome do usuário e identifica cada entidade pelo id de conexão, para que o usuário possa ter várias conexões a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="32022-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="32022-185">No hub, você rastreia o status da conexão de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="32022-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
