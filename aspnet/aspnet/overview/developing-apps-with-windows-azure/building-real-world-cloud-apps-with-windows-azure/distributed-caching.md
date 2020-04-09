---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: Cache distribuído (construindo aplicativos de nuvem do mundo real com o Azure) | Microsoft Docs
author: MikeWasson
description: The Building Real World Cloud Apps with Azure e-book é baseado em uma apresentação desenvolvida por Scott Guthrie. Explica 13 padrões e práticas que ele pode...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676016"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>Cache distribuído (construindo aplicativos de nuvem do mundo real com o Azure)

por [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Baixe Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) ou [Baixe e-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> The **Building Real World Cloud Apps with Azure** e-book é baseado em uma apresentação desenvolvida por Scott Guthrie. Ele explica 13 padrões e práticas que podem ajudá-lo a ser bem sucedido desenvolvendo aplicativos web para a nuvem. Para obter informações sobre o e-book, consulte [o primeiro capítulo](introduction.md).

O capítulo anterior analisou o manuseio de falhas transitórias e mencionou o cache como uma estratégia de disjuntor. Este capítulo dá mais informações sobre o cache, incluindo quando usá-lo, padrões comuns para usá-lo e como implementá-lo no Azure.

## <a name="what-is-distributed-caching"></a>O que é cache distribuído

Um cache fornece acesso de alta taxa de transferência e baixa latência aos dados de aplicativos comumente acessados, armazenando os dados na memória. Para um aplicativo em nuvem, o tipo mais útil de cache é o cache distribuído, o que significa que os dados não são armazenados na memória do servidor web individual, mas em outros recursos da nuvem, e os dados armazenados em cache são disponibilizados para todos os servidores web de um aplicativo (ou outros VMs em nuvem que são usados pelo aplicativo).

![diagrama mostrando vários servidores web acessando os mesmos servidores de cache](distributed-caching/_static/image1.png)

Quando o aplicativo é dimensionado adicionando ou removendo servidores, ou quando os servidores são substituídos devido a atualizações ou falhas, os dados armazenados em cache permanecem acessíveis a todos os servidores que executam o aplicativo.

Ao evitar o acesso de dados de alta latência de um armazenamento de dados persistente, o cache pode melhorar drasticamente a capacidade de resposta do aplicativo. Por exemplo, recuperar dados do cache é muito mais rápido do que recuperá-los de um banco de dados relacional.

Um benefício lateral do cache é a redução do tráfego para o armazenamento de dados persistente, o que pode resultar em custos menores quando há taxas de saída de dados para o armazenamento de dados persistente.

## <a name="when-to-use-distributed-caching"></a>Quando usar cache distribuído

O cache funciona melhor para cargas de trabalho de aplicativos que fazem mais leitura do que a escrita de dados, e quando o modelo de dados suporta a organização de chave/valor que você usa para armazenar e recuperar dados em cache. Também é mais útil quando os usuários de aplicativos compartilham muitos dados comuns; por exemplo, o cache não forneceria tantos benefícios se cada usuário normalmente recuperasse dados exclusivos desse usuário. Um exemplo em que o cache pode ser muito benéfico é um catálogo de produtos, porque os dados não mudam com freqüência, e todos os clientes estão olhando para os mesmos dados.

O benefício do cache torna-se cada vez mais mensurável quanto mais uma escala de aplicativo, à medida que os limites de rendimento e atrasos de latência do armazenamento de dados persistente se tornam mais um limite para o desempenho geral do aplicativo. No entanto, você pode implementar cache por outras razões além do desempenho também. Para dados que não precisem estar perfeitamente atualizados quando mostrados ao usuário, o acesso ao cache pode servir como um disjuntor para quando o armazenamento de dados persistente estiver sem resposta ou indisponível.

## <a name="popular-cache-population-strategies"></a>Estratégias populares de população de cache

Para poder recuperar dados do cache, você tem que armazená-los lá primeiro. Existem várias estratégias para obter dados que você precisa em um cache:

- À vista sobre demanda / cache

    O aplicativo tenta recuperar dados do cache, e quando o cache não tem os dados (uma "falha"), o aplicativo armazena os dados no cache para que eles estejam disponíveis na próxima vez. Da próxima vez que o aplicativo tentar obter os mesmos dados, ele encontra o que está procurando no cache (um "hit"). Para evitar a busca de dados armazenados em cache que foram alterados no banco de dados, você invalida o cache ao fazer alterações no armazenamento de dados.
- Push de dados de fundo

    Serviços de fundo empurram dados para o cache em um horário regular, e o aplicativo sempre puxa do cache. Essa abordagem funciona muito bem com fontes de dados de alta latência que não exigem que você sempre retorne os dados mais recentes.
- Disjuntor

    O aplicativo normalmente se comunica diretamente com o armazenamento de dados persistente, mas quando o armazenamento de dados persistente tem problemas de disponibilidade, o aplicativo recupera dados do cache. Os dados podem ter sido colocados em cache usando o cache de lado ou a estratégia de pressão de dados em segundo plano. Trata-se de uma estratégia de manipulação de falhas em vez de uma estratégia de melhoria de desempenho.

Para manter os dados na corrente de cache, você pode excluir entradas de cache relacionadas quando seu aplicativo cria, atualiza ou exclui dados. Se estiver tudo bem para o seu aplicativo às vezes obter dados ligeiramente desatualizados, você pode contar com um tempo de expiração configurável para definir um limite de quão antigos os dados de cache podem ser.

Você pode configurar expiração absoluta (quantidade de tempo desde que o item de cache foi criado) ou expiração deslizante (quantidade de tempo desde a última vez que um item de cache foi acessado). A expiração absoluta é usada quando você está dependendo do mecanismo de expiração do cache para evitar que os dados fiquem muito obsoletos. No aplicativo Fix It, expulsaremos manualmente itens de cache velhos e usaremos o vencimento deslizante para manter os dados mais atuais em cache. Independentemente da política de expiração escolhida, o cache despejará automaticamente os itens mais antigos (Menos Recentemente Usados ou LRU) quando o limite de memória do cache for atingido.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>Código de cache de exemplo para o aplicativo Fix It

No código de exemplo a seguir, verificamos o cache primeiro ao recuperar uma tarefa Corrigir It. Se a tarefa for encontrada no cache, nós a devolvemos; se não for encontrado, o pegamos no banco de dados e armazenamos no cache. As mudanças que você faria para `FindTaskByIdAsync` adicionar cache ao método são destacadas.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Quando você atualiza ou exclui uma tarefa Corrigir It, você tem que invalidar (remover) a tarefa armazenada em cache. Caso contrário, futuras tentativas de ler essa tarefa continuarão a obter os dados antigos do cache.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

Estas são amostras para ilustrar o código de cache simples; o cache não foi implementado no projeto Fix It para download.

## <a name="azure-caching-services"></a>Serviços de cache azure

O Azure oferece os seguintes serviços de cache: [Cache Azure Redis](https://msdn.microsoft.com/library/dn690523.aspx) e [Cache Gerenciado do Azure](https://msdn.microsoft.com/library/dn386094.aspx). O cache Do Azure Redis é baseado no popular [cache redis de código aberto](http://redis.io/) e é a primeira escolha para a maioria dos cenários de cache.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>ASP.NET estado de sessão usando um provedor de cache

Como mencionado no [capítulo de melhores práticas de desenvolvimento web,](web-development-best-practices.md)uma prática recomendada é evitar o uso do estado de sessão. Se o aplicativo exigir estado de sessão, a próxima prática recomendada é evitar o provedor de memória padrão, porque isso não ativa a saída de escala (várias instâncias do servidor web). O ASP.NET provedor de estado de sessão do SQL Server permite que um site executado em vários servidores da Web use o estado de sessão, mas incorre em um alto custo de latência em comparação com um provedor de memória. A melhor solução se você tiver que usar o estado de sessão é usar um provedor de cache, como o [Provedor de Estado de Sessão para Cache Azure](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx).

## <a name="summary"></a>Resumo

Você viu como o aplicativo Fix It pode implementar cache para melhorar o tempo de resposta e a escalabilidade, e para permitir que o aplicativo continue respondendo às operações de leitura quando o banco de dados não estiver disponível. No [próximo capítulo,](queue-centric-work-pattern.md) mostraremos como melhorar ainda mais a escalabilidade e fazer com que o aplicativo continue respondendo às operações de gravação.

## <a name="resources"></a>Recursos

Para obter mais informações sobre cache, consulte os seguintes recursos.

Documentação

- [Cache Azure](https://msdn.microsoft.com/library/gg278356.aspx). Documentação oficial do MSDN sobre cache no Azure.
- [Padrões e práticas da Microsoft - Orientação Azure](https://msdn.microsoft.com/library/dn568099.aspx). Consulte a orientação de cache e o padrão Cache-Aside.
- [Failsafe: Orientação para arquiteturas de nuvem resilientes.](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx) Papel branco de Marc Mercuri, Ulrich Homann e Andrew Townhill. Veja a seção sobre Cache.
- [Práticas recomendadas para o design de serviços de grande escala em serviços de nuvem do Azure.](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx) W. Papel branco de Mark Simms e Michael Thomassy. Veja a seção sobre cache distribuído.
- [Cache distribuído no caminho para a escalabilidade](https://msdn.microsoft.com/magazine/dd942840.aspx). Um artigo mais antigo (2009) da Revista MSDN, mas uma introdução claramente escrita ao cache distribuído em geral; entra em mais profundidade do que as seções de cache dos white papers FailSafe e Best Practices.

vídeos

- [FailSafe: Construindo serviços de nuvem escaláveis e resilientes.](https://channel9.msdn.com/Series/FailSafe) Série de nove partes de Ulrich Homann, Marc Mercuri e Mark Simms. Apresenta uma visão de 400 níveis de como arquitetar aplicativos em nuvem. Esta série se concentra na teoria e nas razões; para mais detalhes, veja a série Building Big de Mark Simms. Veja a discussão do cache no episódio 3 a partir de 1:24:14.
- [Building Big: Lições aprendidas com os clientes do Azure - Parte I](https://channel9.msdn.com/Events/Build/2012/3-029). Simon Davies discute o cache distribuído a partir das 46:00. Semelhante à série Failsafe, mas entra em mais detalhes de como fazer. A apresentação foi dada em 31 de outubro de 2012, portanto não cobre o serviço de cache de Web Apps no Azure App Service que foi introduzido em 2013.

Exemplo de código

- [Fundamentos do Serviço de Nuvem no Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Aplicativo de amostra que implementa cache distribuído. Veja o post do blog [cloud service fundamentals – Caching Basics](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx).

> [!div class="step-by-step"]
> [Próximo](transient-fault-handling.md)
> [anterior](queue-centric-work-pattern.md)
