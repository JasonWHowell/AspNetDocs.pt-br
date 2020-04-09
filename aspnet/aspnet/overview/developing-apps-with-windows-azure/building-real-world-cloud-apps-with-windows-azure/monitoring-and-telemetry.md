---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: Monitoramento e Telemetria (Construindo aplicativos de nuvem do mundo real com o Azure) | Microsoft Docs
author: MikeWasson
description: The Building Real World Cloud Apps with Azure e-book é baseado em uma apresentação desenvolvida por Scott Guthrie. Explica 13 padrões e práticas que ele pode...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676030"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>Monitoramento e Telemetria (Construindo aplicativos de nuvem do mundo real com o Azure)

por [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Baixe Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) ou [Baixe e-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> The **Building Real World Cloud Apps with Azure** e-book é baseado em uma apresentação desenvolvida por Scott Guthrie. Ele explica 13 padrões e práticas que podem ajudá-lo a ser bem sucedido desenvolvendo aplicativos web para a nuvem. Para obter informações sobre o e-book, consulte [o primeiro capítulo](introduction.md).

Muitas pessoas dependem dos clientes para que saibam quando sua aplicação está baixa. Isso não é realmente uma prática recomendada em qualquer lugar, e especialmente não na nuvem. Não há garantia de notificação rápida, e quando você é notificado, muitas vezes você recebe dados mínimos ou enganosos sobre o que aconteceu. Com bons sistemas de telemetria e registro, você pode estar ciente do que está acontecendo com seu aplicativo, e quando algo dá errado, você descobre imediatamente e tem informações úteis para resolver problemas para trabalhar.

## <a name="buy-or-rent-a-telemetry-solution"></a>Comprar ou alugar uma solução de telemetria

> [!NOTE]
> Este artigo foi escrito antes [do Application Insights](/azure/application-insights/app-insights-overview) ser lançado. O Application Insights é a abordagem preferida para soluções de telemetria no Azure. Consulte [Configurar insights de aplicativos para seu site ASP.NET](/azure/application-insights/app-insights-asp-net) para obter mais informações.

Uma das coisas que é ótima sobre o ambiente de nuvem é que é realmente fácil comprar ou alugar o seu caminho para a vitória. A telemetria é um exemplo. Sem muito esforço, você pode obter um sistema de telemetria muito bom em funcionamento, muito econômico. Há um monte de grandes parceiros que se integram com o Azure, e alguns deles têm níveis gratuitos – para que você possa obter telemetria básica para nada. Aqui estão apenas alguns dos disponíveis atualmente no Azure:

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[O Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) também inclui recursos de monitoramento.

Vamos rapidamente passar pela configuração do New Relic para mostrar como pode ser fácil usar um sistema de telemetria.

No portal de gestão do Azure, inscreva-se para o serviço. Clique **em Novo**e clique em **Armazenar**. A caixa de diálogo **Escolher um complemento** é exibida. Role para baixo e clique em **Nova Relíquia**.

![Escolha um complemento](monitoring-and-telemetry/_static/image1.png)

Clique na seta direita e escolha o nível de serviço desejado. Para esta demonstração usaremos o nível livre.

![Personalizar complemento](monitoring-and-telemetry/_static/image2.png)

Clique na seta direita, confirme a "compra", e a New Relic agora aparece como um Complemento no portal.

![Revisar compra](monitoring-and-telemetry/_static/image3.png)

![Novo complemento da Relíquia no portal de gestão](monitoring-and-telemetry/_static/image4.png)

Clique **em Informações de Conexão**e copie a chave de licença.

![Informações de conexão](monitoring-and-telemetry/_static/image5.png)

Vá para a guia **Configurar** para o seu aplicativo web no portal, defina o **monitoramento de desempenho** para **add-on**e defina a lista de parada **de saque** para Escolher add-on para **Nova Relíquia**. Em seguida, clique **em Salvar**.

![Nova relíquia na guia Configurar](monitoring-and-telemetry/_static/image6.png)

No Visual Studio, instale o pacote New Relic NuGet em seu aplicativo.

![Análise do desenvolvedor na guia Configurar](monitoring-and-telemetry/_static/image7.png)

Implante o aplicativo no Azure e comece a usá-lo. Crie algumas tarefas de Corrigir It para fornecer alguma atividade para a New Relic monitorar.

Em seguida, volte para a página **Nova Relíquia** na guia **Add-ons** do portal e clique **em Gerenciar**. O portal envia você para o portal de gerenciamento new relic, usando o login único para autenticação para que você não precise inserir suas credenciais novamente. A página Visão Geral apresenta uma variedade de estatísticas de desempenho. (Clique na imagem para ver a página de visão geral em tamanho real.)

[![Nova guia de monitoramento de relíquias](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

Aqui estão apenas algumas das estatísticas que você pode ver:

- Tempo médio de resposta em diferentes horas do dia.

    ![Tempo de resposta](monitoring-and-telemetry/_static/image10.png)
- Taxas de throughput (em solicitações por minuto) em diferentes horas do dia.

    ![Produtividade](monitoring-and-telemetry/_static/image11.png)
- Tempo de CPU do servidor gasto lidando com diferentes solicitações HTTP.

    ![Tempos de transação web](monitoring-and-telemetry/_static/image12.png)
- Tempo de CPU gasto em diferentes partes do código do aplicativo:

    ![Trace detalhes](monitoring-and-telemetry/_static/image13.png)
- Estatísticas históricas de desempenho.

    ![Desempenho histórico](monitoring-and-telemetry/_static/image14.png)
- Chamadas para serviços externos, como o serviço Blob e estatísticas sobre o quão confiável e responsivo o serviço tem sido.

    ![Serviços externos](monitoring-and-telemetry/_static/image15.png)

    ![Serviços externos](monitoring-and-telemetry/_static/image16.png)

    ![Serviço externo](monitoring-and-telemetry/_static/image17.png)
- Informações sobre de onde no mundo ou de onde veio o tráfego de aplicativos web nos EUA.

    ![painel Geografia do app&#39;s selecionado](monitoring-and-telemetry/_static/image18.png)

Você também pode configurar relatórios e eventos. Por exemplo, você pode dizer que sempre que começar a ver erros, envie um e-mail para alertar a equipe de suporte para o problema.

![Relatórios](monitoring-and-telemetry/_static/image19.png)

New Relic é apenas um exemplo de um sistema de telemetria; você pode obter tudo isso de outros serviços também. A beleza da nuvem é que sem ter que escrever nenhum código, e para um custo mínimo ou sem despesas, de repente você pode obter muito mais informações sobre como seu aplicativo está sendo usado e o que seus clientes estão realmente experimentando.

<a id="log"></a>
## <a name="log-for-insight"></a>Log para obter informações

Um pacote de telemetria é um bom primeiro passo, mas você ainda tem que instrumentalizar seu próprio código. O serviço de telemetria diz quando há um problema e diz o que os clientes estão experimentando, mas pode não lhe dar muita visão sobre o que está acontecendo em seu código.

Você não quer ter que passar por um servidor de produção para ver o que seu aplicativo está fazendo. Isso pode ser prático quando você tem um servidor, mas e quando você tem escalado para centenas de servidores e você não sabe quais você precisa remotar? Seu registro deve fornecer informações suficientes que você nunca precisa remotamente em servidores de produção para analisar e depurar problemas. Você deve estar registrando informações suficientes para que você possa isolar problemas apenas através dos logs.

### <a name="log-in-production"></a>Efetuar login na produção

Muitas pessoas ligam o rastreamento na produção apenas quando há um problema e querem depurar. Isso pode introduzir um atraso substancial entre o tempo que você está ciente de um problema e o tempo que você recebe informações úteis para solucionar problemas sobre ele. E as informações que você recebe podem não ser úteis para erros intermitentes.

O que recomendamos no ambiente em nuvem onde o armazenamento é barato é que você sempre deixe o registro ligado na produção. Dessa forma, quando os erros acontecem, você já os tem registrados, e você tem dados históricos que podem ajudá-lo a analisar questões que se desenvolvem ao longo do tempo ou acontecem regularmente em momentos diferentes. Você pode automatizar um processo de purga para excluir logs antigos, mas você pode achar que é mais caro configurar tal processo do que manter os logs.

A despesa adicional de registro é trivial em comparação com a quantidade de tempo e dinheiro que você pode economizar tendo todas as informações que você precisa já disponíveis quando algo dá errado. Então, quando alguém diz que teve um erro aleatório por volta das 8:00 da noite passada, mas não se lembra do erro, você pode facilmente descobrir qual foi o problema.

Por menos de US$ 4 por mês, você pode manter 50 gigabytes de logs na mão, e o impacto no desempenho do registro é trivial, desde que você tenha uma coisa em mente -- a fim de evitar gargalos de desempenho, certifique-se de que sua biblioteca de registro seja assíncrona.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>Diferencie registros que informem de registros que requerem ação

Os logs são feitos para INFORMAR (eu quero que você saiba alguma coisa) ou ACT (eu quero que você faça alguma coisa). Tenha cuidado para escrever apenas registros ACT para problemas que realmente requerem uma pessoa ou um processo automatizado para agir. Muitos logs ACT criarão ruído, exigindo muito trabalho para peneirar tudo para encontrar problemas genuínos. E se seus logs act acionarem automaticamente alguma ação, como o envio de e-mails para a equipe de suporte, evite que milhares dessas ações sejam desencadeadas por um único problema.

No rastreamento .NET System.Diagnostics, os logs podem ser atribuídos ao nível de Erro, Aviso, Informação e Depuração/Verbose. Você pode diferenciar o ACT dos logs DO INFORM reservando o nível de erro para logs ACT e usando os níveis inferiores para logs DE INFORM.

![Níveis de log](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>Configure os níveis de registro em tempo de execução

Embora valha a pena ter o registro sempre ligado na produção, outra prática recomendada é implementar uma estrutura de registro que permite ajustar em tempo de execução o nível de detalhe que você está registrando, sem reimplantar ou reiniciar seu aplicativo. Por exemplo, quando você usa `System.Diagnostics` a instalação de rastreamento em você pode criar registros de erro, aviso, informação e depuração/verbose. Recomendamos que você sempre registre os registros de erros, avisos e informações na produção, e você poderá adicionar dinamicamente o registro de depuração/Verbose para solução de problemas caso a caso.

Os aplicativos da Web no Azure App `System.Diagnostics` Service têm suporte interno para escrever logs no sistema de arquivos, armazenamento de tabela ou armazenamento Blob. Você pode selecionar diferentes níveis de registro para cada destino de armazenamento e pode alterar o nível de registro em tempo real sem reiniciar seu aplicativo. O suporte ao armazenamento Blob facilita a execução de trabalhos de análise [do HDInsight](https://docs.microsoft.com/azure/hdinsight/) nos registros de aplicativos, porque o HDInsight sabe como trabalhar diretamente com o armazenamento Blob.

### <a name="log-exceptions"></a>registrar exceções em log

Não apenas coloque *exceção. ToString()* em seu código de registro. Isso deixa de fora informações contextuais. No caso de erros de SQL, ele deixa de fora o número de erro SQL. Para todas as exceções, inclua informações de contexto, a exceção em si e exceções internas para garantir que você está fornecendo tudo o que será necessário para a solução de problemas. Por exemplo, as informações de contexto podem incluir o nome do servidor, um identificador de transação e um nome de usuário (mas não a senha ou quaisquer segredos!).

Se você confiar em cada desenvolvedor para fazer a coisa certa com o registro de exceção, alguns deles não. Para garantir que ele seja feito da maneira certa todas as vezes, construa o tratamento de exceção direto na sua interface de logger: passe o objeto de exceção para a classe logger e registre os dados de exceção corretamente na classe logger.

### <a name="log-calls-to-services"></a>Log de chamadas para serviços

Recomendamos que você escreva um registro toda vez que seu aplicativo chamar para um serviço, seja para um banco de dados ou uma API REST ou qualquer serviço externo. Inclua em seus registros não apenas uma indicação de sucesso ou fracasso, mas quanto tempo cada solicitação levou. No ambiente de nuvem, muitas vezes você verá problemas relacionados a lentidão em vez de paralisações completas. Algo que normalmente leva 10 milissegundos pode de repente começar a demorar um segundo. Quando alguém lhe diz que seu aplicativo é lento, você quer ser capaz de olhar para new relic ou qualquer serviço de telemetria que você tem e validar sua experiência, e então você quer ser capaz de olhar são seus próprios logs para mergulhar nos detalhes de por que é lento.

### <a name="use-an-ilogger-interface"></a>Use uma interface ILogger

O que recomendamos fazer quando você cria um aplicativo de produção é criar uma interface *ILogger* simples e colocar alguns métodos nele. Isso facilita a alteração da implementação de registro mais tarde e não precisa passar por todo o seu código para fazê-lo. Poderíamos estar usando `System.Diagnostics.Trace` a classe em todo o aplicativo Fix It, mas em vez disso estamos usando-o sob as capas em uma classe de registro que implementa *o ILogger,* e fazemos chamadas do método *ILogger* em todo o aplicativo.

Dessa forma, se você quiser tornar seu registro [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) mais rico, você pode substituir por qualquer mecanismo de registro que você quiser. Por exemplo, à medida que seu aplicativo cresce, você pode decidir que deseja usar um pacote de registro mais abrangente, como [o NLog](http://nlog-project.org/) ou [o Enterprise Library Logging Application Block](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx). ([Log4Net](http://logging.apache.org/log4net/) é outra estrutura de registro popular, mas não faz registro assíncrono.)

Uma possível razão para usar uma estrutura como o NLog é facilitar a divisão da saída de registro em armazenamentos de dados separados de alto volume e alto valor. Isso ajuda você a armazenar eficientemente grandes volumes de dados INFORM que você não precisa executar consultas rápidas contra, mantendo acesso rápido aos dados act.

### <a name="semantic-logging"></a>Registro semântico

Para obter uma maneira relativamente nova de fazer o registro que pode produzir informações de diagnóstico mais úteis, consulte [Enterprise Library Semantic Logging Application Block (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). O SLAB usa [o etw](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) de rastreamento de eventos para Windows (ETW) e o suporte [eventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) no .NET 4.5 para permitir que você crie logs mais estruturados e querisso. Você define um método diferente para cada tipo de evento que você registra, o que permite personalizar as informações que você escreve. Por exemplo, para registrar um erro de `LogSQLDatabaseError` banco de dados SQL, você pode chamar um método. Para esse tipo de exceção, você sabe que uma peça-chave da informação é o número de erro, então você pode incluir um parâmetro de número de erro na assinatura do método e registrar o número de erro como um campo separado no registro de registro que você escreve. Como o número está em um campo separado, você pode obter relatórios com mais facilidade e confiabilidade com base em números de erro SQL do que poderia se estivesse apenas concatenando o número de erro em uma seqüência de mensagens.

## <a name="logging-in-the-fix-it-app"></a>Login no aplicativo Corrigir It

### <a name="the-ilogger-interface"></a>A interface ILogger

Aqui está a interface *ILogger* no aplicativo Fix It.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

Esses métodos permitem que você escreva registros nos mesmos quatro níveis suportados pelo *System.Diagnostics*. Os métodos TraceApi são para registrar chamadas de serviço saturados com informações sobre latência. Você também pode adicionar um conjunto de métodos para o nível Debug/Verbose.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>A implementação do Logger da interface ILogger

A implementação da interface é realmente simples. Basicamente, ele apenas chama para os métodos padrão *do System.Diagnostics.* O trecho a seguir mostra todos os três métodos de Informação e um de cada um dos outros.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>Chamando os métodos ILogger

Toda vez que o código no aplicativo Fix It pega uma exceção, ele chama um método *ILogger* para registrar os detalhes de exceção. E toda vez que ele faz uma chamada para o banco de dados, serviço Blob ou uma API REST, ele inicia um cronômetro antes da chamada, pára o cronômetro quando o serviço retorna e registra o tempo decorrido junto com informações sobre sucesso ou falha.

Observe que a mensagem de registro inclui o nome da classe e o nome do método. É uma boa prática garantir que as mensagens de registro identifiquem qual parte do código do aplicativo as escreveu.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

Então, agora, para cada vez que o aplicativo Fix It fez uma chamada para o Banco de Dados SQL, você pode ver a chamada, o método que o chamou, e exatamente quanto tempo levou.

![Consulta ao banco de dados SQL em logs](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

Se você for navegar pelos registros, verá que o tempo que as chamadas de banco de dados levam é variável. Essas informações podem ser úteis: como o aplicativo registra tudo isso, você pode analisar tendências históricas em como o serviço de banco de dados está se saindo ao longo do tempo. Por exemplo, um serviço pode ser rápido na maior parte do tempo, mas as solicitações podem falhar ou as respostas podem diminuir em certas horas do dia.

Você pode fazer a mesma coisa para o serviço Blob – para cada vez que o aplicativo carrega um novo arquivo, há um log, e você pode ver exatamente quanto tempo levou para carregar cada arquivo.

![Log de upload blob](monitoring-and-telemetry/_static/image23.png)

São apenas algumas linhas extras de código para escrever toda vez que você chama um serviço, e agora sempre que alguém diz que se depara com um problema, você sabe exatamente qual era o problema, se foi um erro, ou mesmo se estava apenas correndo devagar. Você pode identificar a fonte do problema sem ter que usar remotamente em um servidor ou ativar o registro depois que o erro acontecer e esperar recriá-lo.

## <a name="dependency-injection-in-the-fix-it-app"></a>Injeção de dependência no aplicativo Fix It

Você pode se perguntar como o construtor de repositório no exemplo mostrado acima obtém a implementação da interface do logger:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

Para conectar a interface à implementação, o aplicativo usa [injeção de dependência](http://en.wikipedia.org/wiki/Dependency_injection)(DI) com [AutoFac](http://autofac.org/). O DI permite que você use um objeto baseado em uma interface em muitos lugares ao longo do seu código e só precisa especificar em um só lugar a implementação que é usada quando a interface é instanciada. Isso facilita a alteração da implementação: por exemplo, você pode querer substituir o logger system.Diagnostics por um logger NLog. Ou para testes automatizados, você pode querer substituir uma versão simulada do logger.

O aplicativo Corrigir It usa DI em todos os repositórios e em todos os controladores. Os construtores das classes controladoras recebem uma interface *ITaskRepository* da mesma forma que o repositório obtém uma interface de logger:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

O aplicativo usa a biblioteca AutoFac DI para fornecer automaticamente *instâncias TaskRepository* e *Logger* para esses construtores.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

Esse código basicamente diz que em qualquer lugar que um construtor precise de uma interface *ILogger,* passe em uma instância da classe *Logger* e sempre que precisar de uma interface *IFixItTaskRepository,* passe em uma instância da classe *FixItTaskRepository.*

[AutoFac](http://autofac.org/) é uma das muitas estruturas de injeção de dependência que você pode usar. Outra popular é [a Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx), que é recomendada e suportada pela Microsoft Patterns and Practices.

## <a name="built-in-logging-support-in-azure"></a>Suporte de registro incorporado no Azure

O Azure suporta os seguintes tipos de [registro para aplicativos web no Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio):

- Sistema.Diagnósticos rastreamento (você pode ligar e desligar e definir níveis na mosca sem reiniciar o site).
- Eventos do Windows.
- Logs IIS (HTTP/FREB).

O Azure suporta os seguintes tipos de [login em Serviços de Nuvem](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics):

- Sistema.Rastreamento diagnóstico.
- Contadores de desempenho.
- Eventos do Windows.
- Logs IIS (HTTP/FREB).
- Monitoramento de diretórios personalizados.

O aplicativo Fix It usa rastreamento System.Diagnostics. Tudo o que você precisa fazer para ativar o login do System.Diagnostics em um aplicativo web é virar um switch no portal ou chamar a API REST. No portal, clique na guia **Configuração** do seu site e role para baixo para ver a seção Diagnósticos de **Aplicativos.** Você pode ativar ou desativar o registro e selecionar o nível de registro desejado. Você pode fazer com que o Azure escreva os logs para o sistema de arquivos ou para uma conta de armazenamento.

![Diagnósticos de aplicativos e diagnósticos do site na guia Configurar](monitoring-and-telemetry/_static/image24.png)

Depois de habilitar o login no Azure, você poderá ver logs na janela Saída do Visual Studio à medida que eles são criados.

![Menu de logs de streaming](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![Menu de logs de streaming](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

Você também pode ter logs gravados em sua conta de armazenamento e visualizá-los com qualquer ferramenta que possa acessar o serviço azure Storage Table, como **server explorer** no Visual Studio ou [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/).

![Logs no Server Explorer](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>Resumo

É realmente simples implementar um sistema de telemetria fora da caixa, o registro de instrumentos em seu próprio código e configurar o login no Azure. E quando você tem problemas de produção, a combinação de um sistema de telemetria e registros personalizados irá ajudá-lo a resolver problemas rapidamente antes que eles se tornem grandes problemas para seus clientes.

No [próximo capítulo,](transient-fault-handling.md) veremos como lidar com erros transitórios para que eles não se tornem problemas de produção que você tem que investigar.

## <a name="resources"></a>Recursos

Para obter mais informações, consulte os recursos a seguir.

Documentação principalmente sobre telemetria:

- [Padrões e práticas da Microsoft - Orientação Azure](https://msdn.microsoft.com/library/dn568099.aspx). Consulte orientação de instrumentação e telemetria, orientação de medição de serviço, padrão de monitoramento de ponto final de saúde e padrão de reconfiguração em tempo de execução.
- [Penny Pinching in the Cloud: Habilitando o monitoramento de desempenho de novas relíquias em sites do Azure](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx).
- [Práticas recomendadas para o design de serviços de grande escala em serviços de nuvem do Azure.](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx) Papel branco de Mark Simms e Michael Thomassy. Consulte a seção Telemetria e Diagnóstico.
- [Desenvolvimento de próxima geração com insights de aplicativos.](https://msdn.microsoft.com/magazine/dn683794.aspx) Artigo da Revista MSDN.

Documentação principalmente sobre registro:

- [Bloco de aplicação de registro semântico (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). Neil Mackenzie apresenta o caso do registro semântico com a SLAB.
- [Criação de registros estruturados e significativos com registro semântico](https://channel9.msdn.com/Events/Build/2013/3-336). (Vídeo) Julian Dominguez apresenta o caso do registro semântico com a SLAB.
- [EF6 SQL Logging – Parte 1: Registro simples](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/). Arthur Vickers mostra como registrar consultas executadas pelo Entity Framework na EF 6.
- [Resiliência de conexão e interceptação de comando com o Framework entity em um ASP.NET aplicativo MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). Em quarto lugar em uma série tutorial de nove partes, mostra como usar o recurso de interceptação de comando SF 6 para registrar comandos SQL enviados ao banco de dados pelo Entity Framework.
- [Melhore o registro usando atributos c# 5.0 Deinformações do chamador](http://www.dotnetcurry.com/showarticle.aspx?ID=972). Como registrar facilmente o nome do método de chamada sem codificar duramente em literais ou usando reflexão para obtê-lo manualmente.

Documentação principalmente sobre solução de problemas:

- [Blog de depuração de solução &amp; de problemas do Azure](https://blogs.msdn.com/b/kwill/).
- [AzureTools – O utilitário de diagnóstico usado pela equipe de suporte ao desenvolvedor do Azure](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true). Introduz e fornece um link de download para uma ferramenta que pode ser usada em uma VM Azure para baixar e executar uma grande variedade de ferramentas de diagnóstico e monitoramento. Útil quando você precisa diagnosticar um problema em uma VM específica.
- [Solucionar problemas de um aplicativo web no Azure App Service usando o Visual Studio](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio). Um tutorial passo-a-passo para começar com o rastreamento do System.Diagnostics e depuração remota.

Vídeos:

- [FailSafe: Construindo serviços de nuvem escaláveis e resilientes.](https://channel9.msdn.com/Series/FailSafe) Série de nove partes de Ulrich Homann, Marc Mercuri e Mark Simms. Apresenta conceitos de alto nível e princípios arquitetônicos de forma muito acessível e interessante, com histórias extraídas da experiência da Microsoft Customer Advisory Team (CAT) com clientes reais. Os episódios 4 e 9 são sobre monitoramento e telemetria. O episódio 9 inclui uma visão geral dos serviços de monitoramento MetricsHub, AppDynamics, New Relic e PagerDuty.
- [Building Big: Lições aprendidas com os clientes do Azure - Parte II](https://channel9.msdn.com/Events/Build/2012/3-030). Mark Simms fala sobre projetar para o fracasso e instrumentar tudo. Semelhante à série Failsafe, mas entra em mais detalhes de como fazer.

Amostra de código:

- [Fundamentos do Serviço de Nuvem no Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Aplicativo de exemplo criado pela Equipe de Assessoria ao Cliente do Microsoft Azure. Demonstra tanto as práticas de telemetria quanto de registro, conforme explicado nos artigos a seguir. A amostra implementa o registro de aplicativos usando [o NLog](http://nlog-project.org/). Para obter documentação relacionada, consulte a [série de quatro artigos wiki da TechNet sobre telemetria e registro](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon).

> [!div class="step-by-step"]
> [Próximo](design-to-survive-failures.md)
> [anterior](transient-fault-handling.md)
