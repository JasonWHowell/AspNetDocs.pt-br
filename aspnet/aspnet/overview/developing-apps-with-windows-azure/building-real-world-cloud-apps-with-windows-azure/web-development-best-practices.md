---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Práticas recomendadas de desenvolvimento web (construindo aplicativos de nuvem do mundo real com o Azure) | Microsoft Docs
author: MikeWasson
description: The Building Real World Cloud Apps with Azure e-book é baseado em uma apresentação desenvolvida por Scott Guthrie. Explica 13 padrões e práticas que ele pode...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675995"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Práticas recomendadas de desenvolvimento web (construindo aplicativos de nuvem do mundo real com o Azure)

por [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Baixe Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) ou [Baixe e-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> The **Building Real World Cloud Apps with Azure** e-book é baseado em uma apresentação desenvolvida por Scott Guthrie. Ele explica 13 padrões e práticas que podem ajudá-lo a ser bem sucedido desenvolvendo aplicativos web para a nuvem. Para obter informações sobre o e-book, consulte [o primeiro capítulo](introduction.md).

Os três primeiros padrões foram sobre a criação de um processo de desenvolvimento ágil; o resto é sobre arquitetura e código. Esta é uma coleção de práticas recomendadas de desenvolvimento web:

- [Servidores web apátridas](#stateless) atrás de um balanceador de carga inteligente.
- [Evite o estado de sessão](#sessionstate) (ou se você não puder evitá-lo, use cache distribuído em vez de um banco de dados).
- [Use um CDN](#cdn) para fazer cache de tela ativos de arquivo estáticos (imagens, scripts).
- Use o [suporte assíncrono do .NET 4.5](#async) para evitar o bloqueio de chamadas.

Essas práticas são válidas para todo o desenvolvimento da Web, não apenas para aplicativos em nuvem, mas são especialmente importantes para aplicativos em nuvem. Eles trabalham juntos para ajudá-lo a fazer o melhor uso do dimensionamento altamente flexível oferecido pelo ambiente da nuvem. Se você não seguir essas práticas, você terá limitações ao tentar dimensionar sua aplicação.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>Nível web apátrida atrás de um balanceador de carga inteligente

*O nível da Web apátrida* significa que você não armazena nenhum dado de aplicativo na memória do servidor web ou no sistema de arquivos. Manter seu nível web stateless permite que você forneça uma melhor experiência ao cliente e economize dinheiro:

- Se o nível da Web for apátrida e ficar atrás de um balanceador de carga, você poderá responder rapidamente às alterações no tráfego de aplicativos adicionando ou removendo dinamicamente servidores. No ambiente em nuvem, onde você só paga por recursos do servidor enquanto você realmente usá-los, essa capacidade de responder a mudanças na demanda pode se traduzir em enormes economias.
- Um nível web apátrida é arquitetônicamente muito mais simples para dimensionar o aplicativo. Isso também permite que você responda às necessidades de dimensionamento mais rapidamente, e gaste menos dinheiro em desenvolvimento e testes no processo.
- Os servidores em nuvem, como servidores locais, precisam ser corrigidos e reinicializados ocasionalmente; e se o nível da Web for apátrida, redirecionar o tráfego quando um servidor for desligado temporariamente não causará erros ou comportamentos inesperados.

A maioria dos aplicativos do mundo real precisa armazenar estado para uma sessão web; o ponto principal aqui é não armazená-lo no servidor web. Você pode armazenar o estado de outras maneiras, como no cliente em cookies ou fora do processo do lado do servidor em ASP.NET estado de sessão usando um provedor de cache. Você pode armazenar arquivos no [armazenamento Windows Azure Blob](unstructured-blob-storage.md) em vez do sistema de arquivos local.

Como exemplo de como é fácil escalar um aplicativo em Sites do Windows Azure se o seu nível da Web estiver sem estado, consulte a guia **Escala** para um Site do Windows Azure no portal de gerenciamento:

![Guia Escala](web-development-best-practices/_static/image1.png)

Se você quiser adicionar servidores web, você pode apenas arrastar o controle deslizante de contagem de instâncias para a direita. Defina-o como 5 e clique **em Salvar,** e em segundos você tem 5 servidores web no Windows Azure lidando com o tráfego do seu site.

![Cinco instâncias](web-development-best-practices/_static/image2.png)

Você pode facilmente definir a contagem de instâncias para 3 ou voltar para 1. Quando você volta, você começa a economizar dinheiro imediatamente porque o Windows Azure cobra a cada minuto, não por hora.

Você também pode dizer ao Windows Azure para aumentar ou diminuir automaticamente o número de servidores web com base no uso da CPU. No exemplo a seguir, quando o uso da CPU for abaixo de 60%, o número de servidores web diminuirá para um mínimo de 2, e se o uso da CPU for superior a 80%, o número de servidores web será aumentado até um máximo de 4.

![Escala por uso de CPU](web-development-best-practices/_static/image3.png)

Ou se você sabe que seu site só estará ocupado durante o horário de trabalho? Você pode dizer ao Windows Azure para executar vários servidores durante o dia e diminuir para um único servidor noites, noites e fins de semana. A série a seguir de capturas de tela mostra como configurar o site para executar um servidor em horas de folga e 4 servidores durante o horário de trabalho das 8:00 às 17:00.

![Escala por cronograma](web-development-best-practices/_static/image4.png)

![Definir horários](web-development-best-practices/_static/image5.png)

![Programação diurna](web-development-best-practices/_static/image6.png)

![Programação da semana](web-development-best-practices/_static/image7.png)

![Programação do fim de semana](web-development-best-practices/_static/image8.png)

E, claro, tudo isso pode ser feito em scripts, bem como no portal.

A capacidade do seu aplicativo de dimensionar é quase ilimitada no Windows Azure, desde que você evite impedimentos para adicionar ou remover dinamicamente VMs do servidor, mantendo o nível web apátrida.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>Evite o estado da sessão

Geralmente, não é prático em uma aplicativo em nuvem real evitar o armazenamento de alguma forma de estado para uma sessão de usuário, mas algumas abordagens afetam o desempenho e a escalabilidade mais do que outras. Se você precisar armazenar o estado, a melhor solução será manter o estado em uma quantidade pequena e armazená-lo em cookies. Se isso não for viável, a próxima melhor solução é usar ASP.NET estado de sessão com um provedor para [cache distribuído e na memória](distributed-caching.md#sessionstate). A pior solução de um ponto de vista de escalabilidade e desempenho é usar um provedor de estado de sessão com backup em um banco de dados.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>Use um CDN para armazenar ativos de arquivos estáticos

CDN é um acrônimo para Content Delivery Network. Você fornece ativos de arquivos estáticos, como imagens e arquivos de script para um provedor de CDN, e o provedor armazena esses arquivos em data centers em todo o mundo para que, onde quer que as pessoas acessem seu aplicativo, eles obtenham resposta relativamente rápida e baixa latência para os ativos armazenados em cache. Isso acelera o tempo total de carga do site e reduz a carga em seus servidores web. CDNs são especialmente importantes se você estiver alcançando um público que é amplamente distribuído geograficamente.

O Windows Azure tem um CDN, e você pode usar outros CDNs em um aplicativo que é executado no Windows Azure ou em qualquer ambiente de hospedagem web.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>Use o suporte assíncrono do .NET 4.5 para evitar o bloqueio de chamadas

.NET 4.5 aprimorou as linguagens de programação C# e VB, a fim de tornar muito mais simples lidar com tarefas assíncronamente. O benefício da programação assíncrona não é apenas para situações de processamento paralelo, como quando você deseja iniciar várias chamadas de serviço web simultaneamente. Ele também permite que seu servidor web funcione de forma mais eficiente e confiável em condições de alta carga. Um servidor web só tem um número limitado de threads disponíveis e em condições de alta carga quando todos os segmentos estão em uso, as solicitações recebidas têm que esperar até que os segmentos sejam liberados. Se o código do aplicativo não lidar com tarefas como consultas de banco de dados e chamadas de serviço web de forma assíncrona, muitos segmentos serão desnecessariamente amarrados enquanto o servidor aguarda uma resposta de I/O. Isso limita a quantidade de tráfego que o servidor pode suportar em condições de alta carga. Com programação assíncrona, os threads que aguardam um serviço web ou banco de dados para retornar dados são liberados para atender novas solicitações até que os dados sejam recebidos. Em um servidor web ocupado, centenas ou milhares de solicitações podem ser processadas prontamente, o que de outra forma estaria esperando que os threads fossem liberados.

Como você viu anteriormente, é tão fácil diminuir o número de servidores web que lidam com seu site quanto para aumentá-los. Portanto, se um servidor pode obter maior throughput, você não precisa de tantos deles e você pode diminuir seus custos porque você precisa de menos servidores para um determinado volume de tráfego do que você faria de outra forma.

O suporte para o modelo de programação assíncrona .NET 4.5 está incluído no ASP.NET 4.5 para Formulários Web, MVC e API web; na Entity Framework 6 e na API de armazenamento do [Windows Azure](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx).

### <a name="async-support-in-aspnet-45"></a>Suporte assíncrono em ASP.NET 4.5

Em ASP.NET 4.5, o suporte à programação assíncrona foi adicionado não apenas ao idioma, mas também aos frameworks MVC, Web Forms e Web API. Por exemplo, um método de ação controlador mvc ASP.NET recebe dados de uma solicitação da Web e passa os dados para uma exibição que, em seguida, cria o HTML a ser enviado para o navegador. Frequentemente, o método de ação precisa obter dados de um banco de dados ou serviço web para exibi-los em uma página da Web ou para salvar dados inseridos em uma página da Web. Nesses cenários é fácil tornar o método de ação assíncrono: em vez de retornar um objeto *ActionResult,* você retorna *&lt;Task ActionResult&gt; * e marca o método com a palavra-chave *assíncrona.* Dentro do método, quando uma linha de código inicia uma operação que envolve tempo de espera, você marca com a palavra-chave aguarde.

Aqui está um método de ação simples que chama um método de repositório para uma consulta de banco de dados:

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

E aqui está o mesmo método que lida com a chamada de banco de dados assíncronamente:

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

Sob as capas, o compilador gera o código assíncrono apropriado. Quando o aplicativo faz `FindTaskByIdAsync`a chamada `FindTask` para , ASP.NET faz a solicitação e, em seguida, desfaz o segmento do trabalhador e torna-o disponível para processar outra solicitação. Quando `FindTask` a solicitação é feita, um segmento é reiniciado para continuar processando o código que vem após essa chamada. Durante o intervalo `FindTask` entre quando a solicitação é iniciada e quando os dados são retornados, você tem um segmento disponível para fazer um trabalho útil que, de outra forma, seria amarrado à espera da resposta.

Há algumas despesas gerais para código assíncrono, mas em condições de baixa carga, essa sobrecarga é insignificante, enquanto em condições de alta carga você é capaz de processar solicitações que de outra forma seriam mantidas esperando por threads disponíveis.

Foi possível fazer esse tipo de programação assíncrona desde ASP.NET 1.1, mas era difícil de escrever, propenso a erros e difícil de depurar. Agora que simplificamos a codificação para ele em ASP.NET 4.5, não há razão para não fazê-lo mais.

### <a name="async-support-in-entity-framework-6"></a>Suporte a sincronismo no Quadro de Entidades 6

Como parte do suporte assíncrono em 4.5, enviamos suporte async para chamadas de serviço web, soquetes e I/O do sistema de arquivos, mas o padrão mais comum para aplicativos web é atingir um banco de dados, e nossas bibliotecas de dados não suportavam a sincronia. Agora, o Entity Framework 6 adiciona suporte asincronia para acesso ao banco de dados.

No Framework 6, todos os métodos que fazem com que uma consulta ou comando seja enviado ao banco de dados têm versões assíncronas. O exemplo aqui mostra a versão assincronia do método *Find.*

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

E esse suporte assíncrono funciona não apenas para inserções, exclusões, atualizações e achados simples, ele também funciona com consultas LINQ:

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

Há uma `Async` versão do `ToList` método porque neste código esse é o método que faz com que uma consulta seja enviada para o banco de dados. Os `Where` `OrderByDescending` métodos configuram apenas a consulta, enquanto o `ToListAsync` método executa `result` a consulta e armazena a resposta na variável.

## <a name="summary"></a>Resumo

Você pode implementar as melhores práticas de desenvolvimento web descritas aqui em qualquer estrutura de programação web e em qualquer ambiente em nuvem, mas temos ferramentas em ASP.NET e Windows Azure para facilitar. Se você seguir esses padrões, você pode facilmente dimensionar seu nível da Web e minimizar suas despesas porque cada servidor será capaz de lidar com mais tráfego.

O [próximo capítulo](single-sign-on.md) analisa como a nuvem permite cenários de login único.

## <a name="resources"></a>Recursos

Para obter mais informações, consulte os seguintes recursos.

Servidores web apátridas:

- [Padrões e práticas da Microsoft - Orientação de autodimensionamento](https://msdn.microsoft.com/library/dn589774.aspx).
- [Desabilitando a afinidade de instância saquear nos sites do Windows Azure](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/). Post de blog de Erez Benari, explica afinidade de sessão em Sites do Windows Azure.

Cdn:

- [FailSafe: Construindo serviços de nuvem escaláveis e resilientes.](https://channel9.msdn.com/Series/FailSafe) Série de vídeo de nove partes de Ulrich Homann, Marc Mercuri e Mark Simms. Veja a discussão da CDN no episódio 3 a partir das 1:34:00.
- [Padrões e práticas da Microsoft padrão de hospedagem de conteúdo estático](https://msdn.microsoft.com/library/dn589776.aspx)
- [Resenhas de CDN](http://www.cdnreviews.com/). Visão geral de muitos CDNs.

Programação assíncrona:

- [Usando métodos assíncronos em ASP.NET MVC 4](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md). Tutorial de Rick Anderson.
- [Programação Assíncrona com Assincronismo e Espera (C# e Visual Básico)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx). MSDN white paper que explica a lógica para a programação assíncrona, como funciona em ASP.NET 4.5 e como escrever código para implementá-lo.
- [Consulta e salvamento do Framework da entidade](https://msdn.microsoft.com/data/jj819165)
- [Como criar aplicativos ASP.NET Web usando o Async](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7). Apresentação em vídeo por Rowan Miller. Inclui uma demonstração gráfica de como a programação assíncrona pode facilitar aumentos dramáticos no throughput do servidor web em condições de alta carga.
- [FailSafe: Construindo serviços de nuvem escaláveis e resilientes.](https://channel9.msdn.com/Series/FailSafe) Série de vídeo de nove partes de Ulrich Homann, Marc Mercuri e Mark Simms. Para discussões sobre o impacto da programação assíncrona sobre escalabilidade, consulte o episódio 4 e o episódio 8.
- [A magia de usar Métodos Assíncronos em ASP.NET 4.5 mais um hascha importante](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). Post de blog de Scott Hanselman, principalmente sobre o uso de assincronismo em ASP.NET aplicativos web forms.

Para obter práticas recomendadas adicionais de desenvolvimento web, consulte os seguintes recursos:

- [O aplicativo de amostra gemido - Práticas recomendadas](the-fix-it-sample-application.md#bestpractices). O apêndice deste e-book lista uma série de práticas recomendadas que foram implementadas no aplicativo Fix It.
- [Lista de verificação de desenvolvedores web](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [Próximo](continuous-integration-and-continuous-delivery.md)
> [anterior](single-sign-on.md)
