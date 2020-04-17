---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: Caching | Microsoft Docs
author: rick-anderson
description: A compreensão do cache é importante para uma aplicação de ASP.NET com bom desempenho. ASP.NET 1.x ofereceu três opções diferentes para cache; cache de saída,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: a199a9c0352dfb054e8d4e5e67652db9bd38851c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542931"
---
# <a name="caching"></a>Cache

pela [Microsoft](https://github.com/microsoft)

> A compreensão do cache é importante para uma aplicação de ASP.NET com bom desempenho. ASP.NET 1.x ofereceu três opções diferentes para cache; cache de saída, cache de fragmentos e a API de cache.

A compreensão do cache é importante para uma aplicação de ASP.NET com bom desempenho. ASP.NET 1.x ofereceu três opções diferentes para cache; cache de saída, cache de fragmentos e a API de cache. ASP.NET 2.0 oferece todos esses três métodos, mas adiciona alguns recursos adicionais significativos. Existem várias novas dependências de cache e os desenvolvedores agora têm a opção de criar dependências personalizadas de cache também. A configuração do cache também foi melhorada significativamente em ASP.NET 2.0.

## <a name="new-features"></a>Novos recursos

## <a name="cache-profiles"></a>Perfis de cache

Os perfis de cache permitem que os desenvolvedores definam configurações específicas de cache que podem ser aplicadas a páginas individuais. Por exemplo, se você tiver algumas páginas que devem ser expiradas do cache após 12 horas, você pode facilmente criar um perfil de cache que pode ser aplicado a essas páginas. Para adicionar um novo perfil &lt;de cache, use a seção saídaSCacheSettings&gt; no arquivo de configuração. Por exemplo, abaixo está a configuração de um perfil de cache chamado *twoday* que configura uma duração de cache de 12 horas.

[!code-xml[Main](caching/samples/sample1.xml)]

Para aplicar este perfil de cache a uma página específica, use o atributo CacheProfile da diretiva @ OutputCache, conforme mostrado abaixo:

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>Dependências de cache personalizadas

ASP.NET desenvolvedores 1.x clamaram por dependências personalizadas de cache. Em ASP.NET 1.x, a classe CacheDependency foi selada, o que impediu que os desenvolvedores dessem suas próprias classes. Em ASP.NET 2.0, essa limitação é removida e os desenvolvedores são livres para desenvolver suas próprias dependências de cache personalizados. A classe CacheDependency permite a criação de uma dependência de cache personalizada com base em arquivos, diretórios ou chaves de cache.

Por exemplo, o código abaixo cria uma nova dependência de cache personalizado com base em um arquivo chamado stuff.xml localizado na raiz do aplicativo web:

[!code-csharp[Main](caching/samples/sample3.cs)]

Neste cenário, quando o arquivo stuff.xml muda, o item armazenado em cache é invalidado.

Também é possível criar uma dependência de cache personalizada usando chaves de cache. Usando este método, a remoção da chave de cache invalidará os dados armazenados em cache. O exemplo a seguir ilustra isso:

[!code-csharp[Main](caching/samples/sample4.cs)]

Para invalidar o item que foi inserido acima, basta remover o item que foi inserido no cache para atuar como a chave de cache.

[!code-csharp[Main](caching/samples/sample5.cs)]

Observe que a chave do item que atua como chave de cache deve ser a mesma que o valor adicionado à matriz de chaves de cache.

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>Dependências de cache SQL baseadas em pesquisas (também chamadas de dependências baseadas em tabela)

O SQL Server 7 e 2000 usa o modelo baseado em votação para dependências de cache SQL. O modelo baseado em pesquisa usa um gatilho em uma tabela de banco de dados que é acionado quando os dados na tabela mudam. Esse gatilho atualiza um campo **changeId** na tabela de notificação que ASP.NET verifica periodicamente. Se o campo **changeId** tiver sido atualizado, ASP.NET sabe que os dados foram alterados e invalida os dados armazenados em cache.

> [!NOTE]
> O SQL Server 2005 também pode usar o modelo baseado em votação, mas como o modelo baseado em pesquisa não é o modelo mais eficiente, é aconselhável usar um modelo baseado em consulta (discutido posteriormente) com o SQL Server 2005.

Para que uma dependência de cache SQL use o modelo baseado em pesquisa para funcionar corretamente, as tabelas devem ter notificações ativadas. Isso pode ser feito programáticamente usando a classe SqlCacheDependencyAdmin ou usando o utilitário aspnet\_regsql.exe.

A linha de comando a seguir registra a tabela Produtos no banco de dados Northwind localizado em uma instância do SQL Server chamada *dbase* for SQL cache dependency.

[!code-console[Main](caching/samples/sample6.cmd)]

A seguir está uma explicação dos switches de linha de comando usados no comando acima:

| **Interruptor de linha de comando** | **Finalidade** |
| --- | --- |
| -S *server* | Especifica o nome do servidor. |
| -ed | Especifica que o banco de dados deve ser habilitado para dependência de cache SQL. |
| -d *\_nome do banco de dados* | Especifica o nome do banco de dados que deve ser ativado para dependência de cache SQL. |
| -E | Especifica que o\_aspnet regsql deve usar a autenticação do Windows ao se conectar ao banco de dados. |
| -et | Especifica que estamos habilitando uma tabela de banco de dados para dependência de cache SQL. |
| -t *\_nome da tabela* | Especifica o nome da tabela de banco de dados para ativar a dependência de cache SQL. |

> [!NOTE]
> Há outros switches disponíveis para\_aspnet regsql.exe. Para uma lista completa,\_execute aspnet regsql.exe -? de uma linha de comando.

Quando este comando é executado, as seguintes alterações são feitas no banco de dados do SQL Server:

- Uma **tabela\_AspNet SqlCacheTablesForChangeNotification** é adicionada. Esta tabela contém uma linha para cada tabela no banco de dados para a qual uma dependência de cache SQL foi ativada.
- Os seguintes procedimentos armazenados são criados dentro do banco de dados:

| AspNet\_SqlCachePollingDeprocedimentoarmazenado | Consulta a tabela\_AspNet SqlCacheTablesForChangeNotification e retorna todas as tabelas habilitadas para dependência de cache SQL e o valor do changeId para cada tabela. Este proc armazenado é usado para pesquisas para determinar se os dados foram alterados. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTables | Retorna todas as tabelas habilitadas para dependência de cache SQL consultando a tabela AspNet\_SqlCacheTablesForChangeNotification e retorna todas as tabelas habilitadas para dependência de cache SQL. |
| AspNet\_SqlCacheRegisterTableProcedimento armazenado | Registra uma tabela para dependência de cache SQL adicionando a entrada necessária na tabela de notificação e adiciona o gatilho. |
| AspNet\_SqlCacheUnRegisterTableProcedimento armazenado | Desregistra uma tabela para dependência de cache SQL removendo a entrada na tabela de notificação e remove o gatilho. |
| AspNet\_SqlCacheUpdateChangeIdProcedimento armazenado | Atualiza a tabela de notificação incrementando o changeId para a tabela alterada. ASP.NET usa esse valor para determinar se os dados foram alterados. Como indicado abaixo, este proc armazenado é executado pelo gatilho criado quando a tabela está ativada. |

- Um gatilho do SQL Server chamado ** _\_aspNet_\_\_\_SqlCacheNotification Trigger** é criado para a tabela. Este gatilho executa o\_AspNet SqlCacheUpdateChangeIdStoredProcedure quando um INSERT, UPDATE ou DELETE é executado na tabela.
- Uma função do SQL Server chamada **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** é adicionada ao banco de dados.

A função **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server tem permissões EXEC para o AspNet\_SqlCachePollingStoredProcedure. Para que o modelo de votação funcione corretamente, você\_deve\_adicionar sua conta de processo à função aspnet ChangeNotification ReceiveNotificationsOnlyAccess. A ferramenta\_aspnet regsql.exe não fará isso por você.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>Configurando dependências de cache SQL baseadas em pesquisa

Existem várias etapas necessárias para configurar dependências de cache SQL baseadas em pesquisa. O primeiro passo é habilitar o banco de dados e a tabela como discutido acima. Uma vez que essa etapa esteja concluída, o resto da configuração é a seguinte:

- Configuração do arquivo de configuração ASP.NET.
- Configurando o SqlCacheDependency

### <a name="configuring-the-aspnet-configuration-file"></a>Configuração do arquivo de configuração ASP.NET

Além de adicionar uma seqüência de conexões como discutido &lt;em&gt; um &lt;módulo anterior, você&gt; também deve configurar um elemento de cache com um elemento sqlCacheDependency, conforme mostrado abaixo:

[!code-xml[Main](caching/samples/sample7.xml)]

Essa configuração permite uma dependência de cache SQL no banco de dados de *pubs.* Observe que o atributo &lt;pollTime no&gt; elemento sqlCacheDependency é padrão para 60000 milissegundos ou 1 minuto. (Este valor não pode ser inferior a 500 milissegundos.) Neste exemplo, &lt;o&gt; elemento add adiciona um novo banco de dados e substitui o pollTime, definindo-o para 900000mils.

#### <a name="configuring-the-sqlcachedependency"></a>Configurando o SqlCacheDependency

O próximo passo é configurar o SqlCacheDependency. A maneira mais fácil de conseguir isso é especificar o valor para o atributo SqlDependency na diretiva @ Outcache da seguinte forma:

[!code-aspx[Main](caching/samples/sample8.aspx)]

Na diretiva acima @ OutputCache, uma dependência de cache SQL é configurada para a tabela *de autores* no banco de dados *de pubs.* Várias dependências podem ser configuradas separando-as com um ponto e vírgula assim:

[!code-aspx[Main](caching/samples/sample9.aspx)]

Outro método de configuração do SqlCacheDependency é fazê-lo programáticamente. O código a seguir cria uma nova dependência de cache SQL na tabela de *autores* no banco de dados dos *pubs.*

[!code-csharp[Main](caching/samples/sample10.cs)]

Um dos benefícios de definir programáticamente a dependência do cache SQL é que você pode lidar com quaisquer exceções que possam ocorrer. Por exemplo, se você tentar definir uma dependência de cache SQL para um banco de dados que não tenha sido habilitado para notificação, uma exceção **DatabaseNotEnabledForNotificationException** será lançada. Nesse caso, você pode tentar ativar o banco de dados para notificações ligando para o método **SqlCacheDependencyAdmin.EnableNotifications** e passando-o para o nome do banco de dados.

Da mesma forma, se você tentar definir uma dependência de cache SQL para uma tabela que não tenha sido ativada para notificação, uma **TableNotEnabledForNotificationException** será lançada. Em seguida, você pode chamar o método **SqlCacheDependencyAdmin.EnableTableForNotifications** passando-lhe o nome do banco de dados e o nome da tabela.

A amostra de código a seguir ilustra como configurar corretamente o tratamento de exceção ao configurar uma dependência de cache SQL.

[!code-csharp[Main](caching/samples/sample11.cs)]

Mais informações:[https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>Dependências de cache SQL baseadas em consulta (somente sql server 2005)

Ao usar o SQL Server 2005 para dependência de cache SQL, o modelo baseado em pesquisa não é necessário. Quando usado com o SQL Server 2005, as dependências de cache SQL se comunicam diretamente através de conexões SQL à instância do SQL Server (nenhuma configuração adicional é necessária) usando notificações de consulta do SQL Server 2005.

A maneira mais simples de habilitar a notificação baseada em consulta é fazê-lo de forma declarativa, definindo o atributo **SqlCacheDependency** do objeto de origem de dados para **O Comandode Notificação** e definindo o atributo **EnableCaching** como **verdadeiro**. Usando este método, nenhum código é necessário. Se o resultado de um comando executado contra a fonte de dados for alterado, ele invalidará os dados do cache.

O exemplo a seguir configura um controle de origem de dados para dependência de cache SQL:

[!code-aspx[Main](caching/samples/sample12.aspx)]

Neste caso, se a consulta especificada no **SelectCommand** retornar um resultado diferente do que fez originalmente, os resultados armazenados em cache serão invalidados.

Você também pode especificar que todas as suas fontes de dados estão habilitadas para dependências de cache SQL definindo o atributo **SqlDependency** da diretiva **@ OutputCache** para **CommandNotification**. O exemplo abaixo ilustra isso.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> Para obter mais informações sobre notificações de consulta no SQL Server 2005, consulte os Livros do Servidor SQL Online.

Outro método de configuração de uma dependência de cache SQL baseada em consulta é fazê-lo de forma programática usando a classe SqlCacheDependency. A amostra de código a seguir ilustra como isso é realizado.

[!code-csharp[Main](caching/samples/sample14.cs)]

Mais informações:[https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>Substituição pós-cache

Cachear uma página pode aumentar drasticamente o desempenho de um aplicativo da Web. No entanto, em alguns casos, você precisa que a maior parte da página seja armazenada em cache e alguns fragmentos dentro da página sejam dinâmicos. Por exemplo, se você criar uma página de notícias totalmente estática por períodos de tempo definidos, você pode definir a página inteira como armazenada em cache. Se você quiser incluir um banner de anúncio rotativo que mudou em cada solicitação de página, então a parte da página que contém o anúncio precisa ser dinâmica. Para permitir que você faça cache de uma página, mas substitua algum conteúdo dinamicamente, você pode usar ASP.NET substituição pós-cache. Com a substituição pós-cache, a página inteira é armazenada em cache com peças específicas marcadas como isentas de cache. No exemplo dos banners de anúncios, o controle Do AdRotator permite que você aproveite a substituição pós-cache para que os anúncios criados dinamicamente para cada usuário e para cada atualização de página.

Existem três maneiras de implementar a substituição pós-cache:

- Declarativamente, usando o controle de substituição.
- Programáticamente, utilizando a API de controle de substituição.
- Implicitamente, usando o controle do AdRotator.

### <a name="substitution-control"></a>Controle de Substituição

O controle de substituição ASP.NET especifica uma seção de uma página armazenada em cache que é criada dinamicamente em vez de armazenada em cache. Você coloca um controle de substituição no local na página onde deseja que o conteúdo dinâmico apareça. No tempo de execução, o controle De substituição chama um método que você especifica com a propriedade MethodName. O método deve retornar uma seqüência, que então substitui o conteúdo do controle de substituição. O método deve ser um método estático no controle de Página ou UserControl que contém. O uso do controle de substituição faz com que a capacidade de cache do lado do cliente seja alterada para a capacidade de cache do servidor, de modo que a página não seja armazenada em cache no cliente. Isso garante que as solicitações futuras para a página chamem o método novamente para gerar conteúdo dinâmico.

### <a name="substitution-api"></a>API de substituição

Para criar conteúdo dinâmico para uma página em cache programática, você pode chamar o método [WriteReplacement](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) em seu código de página, passando-o o nome de um método como parâmetro. O método que lida com a criação do conteúdo dinâmico pega um único parâmetro [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) e retorna uma string. A seqüência de retorno é o conteúdo que será substituído no local dado. Uma vantagem de chamar o método WriteReplacement em vez de usar o controle de substituição declarativamente é que você pode chamar um método de qualquer objeto arbitrário em vez de chamar um método estático da Página ou do objeto UserControl.

Chamar o método WriteReplacement faz com que a capacidade de cache do lado do cliente seja alterada para a capacidade de cache do servidor, de modo que a página não seja armazenada em cache no cliente. Isso garante que as solicitações futuras para a página chamem o método novamente para gerar conteúdo dinâmico.

### <a name="adrotator-control"></a>Controle do AdRotator

O controle do servidor AdRotator implementa o suporte para substituição pós-cache internamente. Se você colocar um controle do AdRotator em sua página, ele renderizará anúncios exclusivos em cada solicitação, independentemente de a página principal estar armazenada em cache. Como resultado, uma página que inclui um controle do AdRotator é apenas um servidor armazenado em cache.

## <a name="controlcachepolicy-class"></a>Classe ControlCachePolicy

A classe ControlCachePolicy permite o controle programático do cache de fragmentos usando controles do usuário. ASP.NET incorpora controles de usuário em uma instância [BasePartialCachingControl.](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) A classe BasePartialCachingControl representa um controle de usuário que tem o cache de saída ativado.

Quando você acessa a propriedade [BasePartialCachingControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) de um controle [PartialCachingControl,](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) você sempre receberá um objeto ControlCachePolicy válido. No entanto, se você acessar a propriedade [UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) de um controle [UserControl,](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) você receberá um objeto ControlCachePolicy válido somente se o controle do usuário já estiver embrulhado por um controle BasePartialCachingControl. Se ele não estiver embrulhado, o objeto ControlCachePolicy retornado pela propriedade lançará exceções quando você tentar manipulá-lo porque ele não tem um BasePartialCachingControl associado. Para determinar se uma instância userControl suporta cache sem gerar exceções, inspecione a propriedade [SupportsCaching.](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)

O uso da classe ControlCachePolicy é uma das várias maneiras pelas quais você pode ativar o cache de saída. A lista a seguir descreve métodos que você pode usar para ativar o cache de saída:

- Use a diretiva [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) para ativar o cache de saída em cenários declarativos.
- Use o atributo [PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) para habilitar o cache para um controle de usuário em um arquivo de código atrás.
- Use a classe ControlCachePolicy para especificar configurações de cache em cenários programáticos nos quais você está trabalhando com instâncias do BasePartialCachingControl que foram habilitadas para cache usando um dos métodos anteriores e carregadas dinamicamente usando o método [System.Web.UI.TemplateControl.LoadControl.](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)

Uma instância ControlCachePolicy pode ser manipulada com sucesso apenas entre os estágios Init e PreRender do ciclo de vida de controle. Se você modificar um objeto ControlCachePolicy após a fase PreRender, ASP.NET lançaruma exceção porque quaisquer alterações feitas após a renderização do controle não podem realmente afetar as configurações de cache (um controle é armazenado em cache durante a fase Renderização). Finalmente, uma instância de controle do usuário (e, portanto, seu objeto ControlCachePolicy) só está disponível para manipulação programática quando ela é realmente renderizada.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>Alterações na configuração &lt;de&gt; cache - O elemento de cache

Existem várias alterações na configuração de cache em ASP.NET 2.0. O &lt;elemento&gt; cache é novo em ASP.NET 2.0 e permite que você faça alterações de configuração de cache no arquivo de configuração. Os seguintes atributos estão disponíveis.

| **Elemento** | **Descrição** |
| --- | --- |
| **Cache** | Elemento opcional. Define configurações globais de cache de aplicativos. |
| **Outputcache** | Elemento opcional. Especifica as configurações de cache de saída em todo o aplicativo. |
| **Outputcachesettings** | Elemento opcional. Especifica configurações de cache de saída que podem ser aplicadas às páginas do aplicativo. |
| **Sqlcachedependency** | Elemento opcional. Configura as dependências de cache do SQL para um aplicativo ASP.NET. |

### <a name="the-ltcachegt-element"></a>O &lt;&gt; elemento cache

Os seguintes atributos &lt;&gt; estão disponíveis no elemento cache:

| **Atributo** | **Descrição** |
| --- | --- |
| **Disablememorycollection** | Atributo **Boolean** opcional. Obtém ou define um valor indicando se a coleção de memória de cache que ocorre quando a máquina está sob pressão de memória está desativada. |
| **desativarExpiração** | Atributo **Boolean** opcional. Obtém ou define um valor indicando se o vencimento do cache está desativado. Quando desativados, os itens armazenados em cache não expiram e a limpeza em segundo plano de itens de cache expirados não ocorre. |
| **Privatebyteslimit** | Atributo **Opcional Int64.** Obtém ou define um valor indicando o tamanho máximo dos bytes privados de um aplicativo antes que o cache comece a liberar itens expirados e tentar recuperar a memória. Esse limite inclui tanto a memória usada pelo cache quanto a sobrecarga de memória normal do aplicativo em execução. Uma configuração de zero indica que ASP.NET usará sua própria heurística para determinar quando começar a recuperar a memória. |
| **Percentagephysicalmemoryusedlimit** | Atributo **Int32** opcional. Obtém ou define um valor indicando a porcentagem máxima da memória física de uma máquina que pode ser consumida por um aplicativo antes que o cache comece a liberar itens expirados e tentando recuperar a memória Este uso de memória inclui tanto a memória usada pelo cache quanto o uso normal da memória do aplicativo em execução. Uma configuração de zero indica que ASP.NET usará sua própria heurística para determinar quando começar a recuperar a memória. |
| **privateBytesPollTime** | Atributo **TimeSpan** opcional. Obtém ou define um valor que indique o intervalo de tempo entre a pesquisa para o uso da memória de bytes privados do aplicativo. |

### <a name="the-ltoutputcachegt-element"></a>O &lt;elemento&gt; outputCache

Os atributos a &lt;seguir&gt; estão disponíveis para o elemento outputCache.

|       <strong>Atributo</strong>        |                                                                                                                                                                                                                                                       <strong>Descrição</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>habilitarOutputCache</strong>    |                                                                                                                                                          Atributo <strong>Boolean</strong> opcional. Ativa/desativa o cache de saída da página. Se desativado, nenhuma página será armazenada em cache independentemente das configurações programáticas ou declarativas. O valor padrão é <strong>verdadeiro</strong>.                                                                                                                                                           |
|  <strong>habilitarFragmentCache</strong>   |                                                Atributo <strong>Boolean</strong> opcional. Ativa/desativa o cache de fragmentos do aplicativo. Se desativado, nenhuma página será armazenada em cache independentemente da diretiva [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) ou do perfil de cache usado. Inclui um cabeçalho de controle de cache indicando que servidores proxy upstream, bem como clientes de navegador, não devem tentar fazer cache de saída de página. O valor padrão é <strong>falso</strong>.                                                 |
| <strong>Sendcachecontrolheader</strong> |                                                                                                                                                      Atributo <strong>Boolean</strong> opcional. Obtém ou define um valor indicando se o <strong>cache-control:private</strong> header é enviado pelo módulo de cache de saída por padrão. O valor padrão é <strong>falso</strong>.                                                                                                                                                      |
|      <strong>Omitvarystar</strong>      | Atributo <strong>Boolean</strong> opcional. Habilita/desativa o<strong>envio \<de um cabeçalho Http " Vary: /strong><em>" na resposta. Com a configuração padrão de falso, um</em>cabeçalho " *Variar: \*" é enviado para páginas em cache de <strong>saída. Quando o cabeçalho Vary é enviado, ele permite que diferentes versões sejam armazenadas em cache com base no que é especificado no cabeçalho Vary. Por exemplo, <em>Vary:Os agentes de usuário</em> armazenarão diferentes versões de uma página com base no agente de usuário que emite a solicitação. O valor padrão é **falso</strong>. |

### <a name="the-ltoutputcachesettingsgt-element"></a>O &lt;elemento outputCacheSettings&gt;

O &lt;elemento outputCacheSettings&gt; permite a criação de perfis de cache como descrito anteriormente. O único elemento &lt;filho para&gt; o elemento &lt;outputCacheSettings é o elemento outputCacheProfiles&gt; para configurar perfis de cache.

### <a name="the-ltsqlcachedependencygt-element"></a>O &lt;elemento sqlCacheDependency&gt;

Os atributos a &lt;seguir estão disponíveis&gt; para o elemento sqlCacheDependency.

| **Atributo** | **Descrição** |
| --- | --- |
| **Habilitado** | Atributo **booleano necessário.** Indica se as mudanças estão sendo ou não pesquisadas. |
| **Polltime** | Atributo **Int32** opcional. Define a freqüência com que o SqlCacheDependency pesquisa a tabela de banco de dados para alterações. Esse valor corresponde ao número de milissegundos entre as pesquisas sucessivas. Não pode ser definido para menos de 500 milissegundos. O valor padrão é de 1 minuto. |

### <a name="more-information"></a>Mais informações

Existem algumas informações adicionais que você deve estar ciente sobre a configuração do cache.

- Se o limite de bytes privados do processo do trabalhador não for definido, o cache usará um dos seguintes limites: 

    - x86 2GB: 800MB ou 60% da MEMÓRIA RAM física, o que for menor
    - x86 3GB: 1800MB ou 60% da MEMÓRIA RAM física, o que for menor
    - x64: 1 terabyte ou 60% da RAM física, o que for menor
- Se o limite de bytes &lt;privados do processo&gt; do trabalhador e o cache privateBytesLimit/forem definidos, o cache usará o mínimo dos dois.
- Assim como em 1.x, derrubamos entradas de cache e chamamos GC. Coletar por duas razões: 

    - Estamos muito perto do limite de bytes privados
    - A memória disponível é próxima ou inferior a 10%
- Você pode efetivamente desativar o trim e o &lt;cache para condições&gt; de memória baixas disponíveis definindo porcentagem de cachePhysicalMemoryUseLimit/ para 100.
- Ao contrário do 1.x, o 2.0 suspenderá o corte e coletará chamadas se o último GC. A coleta não reduziu os bytes privados ou o tamanho dos montes gerenciados em mais de 1% do limite de memória (cache).

## <a name="lab1-custom-cache-dependencies"></a>Lab1: Dependências de cache personalizado

1. Crie um novo site.
2. Adicione um novo arquivo XML chamado cache.xml e salve-o na raiz do aplicativo web.
3. Adicione o seguinte código\_ao método 'Carga de página' no código-atrás de default.aspx: 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. Adicione o seguinte ao topo do default.aspx na exibição de origem: 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Navegue por Default.aspx. O que diz o tempo?
6. Atualize o navegador. O que diz o tempo?
7. Abra cache.xml e adicione o seguinte código: 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. Salvar cache.xml.
9. Atualize seu navegador. O que diz o tempo?
10. Explique por que o tempo atualizado em vez de exibir os valores armazenados anteriormente:

## <a name="lab-2-using-polling-based-cache-dependencies"></a>Laboratório 2: Usando dependências de cache baseadas em pesquisas

Este laboratório usa o projeto que você criou no módulo anterior que permite a edição de dados no banco de dados Northwind através de um controle GridView e DetailsView.

1. Abra o projeto no Visual Studio 2005.
2. Execute o utilitário\_aspnet regsql contra o banco de dados Northwind para habilitar o banco de dados e a tabela Produtos. Use o seguinte comando de um prompt de comando do Visual Studio: 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Adicione o seguinte ao seu arquivo Web.config: 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. Adicione um novo webform chamado showdata.aspx.
5. Adicione a seguinte diretiva @ outputcache à página showdata.aspx: 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. Adicione o seguinte código\_à carga de página de showdata.aspx: 

    [!code-html[Main](caching/samples/sample21.html)]
7. Adicione um novo controle SqlDataSource para mostrardata.aspx e configure-o para usar a conexão de banco de dados Northwind. Clique em Avançar.
8. Selecione as caixas de seleção ProductName e ProductID e clique em Next.
9. Clique em Concluir.
10. Adicione um novo GridView à página showdata.aspx.
11. Escolha SqlDataSource1 na estada.
12. Salvar e navegar showdata.aspx. Anote o tempo exibido.
