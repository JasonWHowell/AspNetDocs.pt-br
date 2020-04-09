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
# <a name="mapping-signalr-users-to-connections"></a>Mapeamento de usuários do SignalR para conexões

 por [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este tópico mostra como reter informações sobre os usuários e suas conexões.
>
> Patrick Fletcher ajudou a escrever este tópico.
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

## <a name="introduction"></a>Introdução

Cada cliente conectado a um hub passa um id de conexão único. Você pode recuperar esse `Context.ConnectionId` valor na propriedade do contexto do hub. Se o seu aplicativo precisar mapear um usuário para o id de conexão e persistir esse mapeamento, você pode usar um dos seguintes:

- [O provedor de id do usuário (Signalr 2)](#IUserIdProvider)
- [Armazenamento na memória,](#inmemory)como um dicionário
- [Grupo SignalR para cada usuário](#groups)
- [Armazenamento externo permanente,](#database)como uma tabela de banco de dados ou armazenamento de tabela azure

Cada uma dessas implementações é mostrada neste tópico. Você usa `OnConnected` `OnDisconnected`os `OnReconnected` métodos e `Hub` métodos da classe para rastrear o status da conexão do usuário.

A melhor abordagem para sua aplicação depende de:

- O número de servidores web que hospedam seu aplicativo.
- Se você precisa obter uma lista dos usuários conectados no momento.
- Se você precisa persistir as informações de grupo e do usuário quando o aplicativo ou servidor é reiniciado.
- Se a latência de chamar um servidor externo é um problema.

A tabela a seguir mostra qual abordagem funciona para essas considerações.

|  | Mais de um servidor | Obtenha lista de usuários conectados no momento | Persistir informações após reinicializações | Desempenho ideal |
| --- | --- | --- | --- | --- |
| Provedor de usuário | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| Na memória |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| Grupos de usuários únicos | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| Permanente, externo | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>Provedor IUserID

Esse recurso permite que os usuários especifiquem o que o IId é baseado em uma IRequest através de uma nova interface IUserIdProvider.

**O Provedor iUserId**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

Por padrão, haverá uma implementação que `IPrincipal.Identity.Name` usa o do usuário como nome de usuário. Para alterar isso, registre `IUserIdProvider` sua implementação com o host global quando a sua aplicação começar:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

A partir de um hub, você poderá enviar mensagens para esses usuários através da seguinte API:

**Enviando uma mensagem para um usuário específico**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>Armazenamento na memória

Os exemplos a seguir mostram como reter a conexão e as informações do usuário em um dicionário armazenado na memória. O dicionário `HashSet` usa um para armazenar o id de conexão. A qualquer momento, um usuário pode ter mais de uma conexão com o aplicativo SignalR. Por exemplo, um usuário que esteja conectado através de vários dispositivos ou mais de uma guia do navegador teria mais de um id de conexão.

Se o aplicativo for desligado, todas as informações serão perdidas, mas serão repovoadas à medida que os usuários restabelecerem suas conexões. O armazenamento na memória não funciona se o ambiente incluir mais de um servidor web porque cada servidor teria uma coleção separada de conexões.

O primeiro exemplo mostra uma classe que gerencia o mapeamento dos usuários para conexões. A chave para o HashSet será o nome do usuário.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

O próximo exemplo mostra como usar a classe de mapeamento de conexão a partir de um hub. A instância da classe é armazenada `_connections`em um nome variável .

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>Grupos de usuários únicos

Você pode criar um grupo para cada usuário e, em seguida, enviar uma mensagem para esse grupo quando você quiser alcançar apenas esse usuário. O nome de cada grupo é o nome do usuário. Se um usuário tiver mais de uma conexão, cada id de conexão será adicionado ao grupo do usuário.

Você não deve remover manualmente o usuário do grupo quando o usuário se desconectar. Esta ação é realizada automaticamente pela estrutura SignalR.

O exemplo a seguir mostra como implementar grupos de usuários únicos.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>Armazenamento externo permanente

Este tópico mostra como usar um banco de dados ou o armazenamento de tabela do Azure para armazenar informações de conexão. Essa abordagem funciona quando você tem vários servidores web porque cada servidor web pode interagir com o mesmo repositório de dados. Se os servidores da Web pararem de `OnDisconnected` funcionar ou o aplicativo for reiniciado, o método não será chamado. Portanto, é possível que seu repositório de dados tenha registros de ids de conexão que não são mais válidos. Para limpar esses registros órfãos, você pode querer invalidar qualquer conexão que foi criada fora de um prazo que seja relevante para sua aplicação. Os exemplos nesta seção incluem um valor para rastreamento quando a conexão foi criada, mas não mostram como limpar registros antigos porque você pode querer fazer isso como processo de fundo.

### <a name="database"></a>Banco de dados

Os exemplos a seguir mostram como reter conexão e informações do usuário em um banco de dados. Você pode usar qualquer tecnologia de acesso a dados; no entanto, o exemplo abaixo mostra como definir modelos usando o Entity Framework. Esses modelos de entidade correspondem a tabelas e campos de banco de dados. Sua estrutura de dados pode variar consideravelmente dependendo dos requisitos de sua aplicação.

O primeiro exemplo mostra como definir uma entidade de usuário que pode ser associada a muitas entidades de conexão.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

Em seguida, a partir do hub, você pode rastrear o estado de cada conexão com o código mostrado abaixo.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Armazenamento de tabelas do Azure

O exemplo a seguir de armazenamento de tabela do Azure é semelhante ao exemplo do banco de dados. Ele não inclui todas as informações que você precisaria para começar com o Azure Table Storage Service. Para obter informações, [consulte Como usar o armazenamento de tabela do .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).

O exemplo a seguir mostra uma entidade de tabela para armazenar informações de conexão. Ele divide os dados pelo nome do usuário e identifica cada entidade pelo id de conexão, para que o usuário possa ter várias conexões a qualquer momento.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

No hub, você rastreia o status da conexão de cada usuário.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
