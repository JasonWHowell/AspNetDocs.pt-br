---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
title: Usando dependências do cache SQL (C#) | Microsoft Docs
author: rick-anderson
description: A estratégia de cache mais simples é permitir que os dados armazenados em cache expirem após um período de tempo especificado. Mas essa abordagem simples significa que os dados armazenados em cache maintai...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 0e91842c-7f10-4aed-8c23-4ee3e2774014
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
msc.type: authoredcontent
ms.openlocfilehash: 6a039cdfb1da294744b92648386468f69193ae6b
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045254"
---
# <a name="using-sql-cache-dependencies-c"></a>Uso de dependências de cache de SQL (C#)

por [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Baixar código](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_CS.zip) ou [baixar PDF](using-sql-cache-dependencies-cs/_static/datatutorial61cs1.pdf)

> A estratégia de cache mais simples é permitir que os dados armazenados em cache expirem após um período de tempo especificado. Mas essa abordagem simples significa que os dados armazenados em cache não mantêm nenhuma associação com sua fonte de dados subjacente, resultando em dados obsoletos que são mantidos muito longos ou dados atuais expirados em breve. Uma abordagem melhor é usar a classe SqlCacheDependency para que os dados permaneçam armazenados em cache até que seus dados subjacentes tenham sido modificados no SQL Database. Este tutorial mostra como.

## <a name="introduction"></a>Introdução

As técnicas de cache examinadas nos [dados de cache com os dados ObjectDataSource](caching-data-with-the-objectdatasource-cs.md) e [Caching nos tutoriais de arquitetura](caching-data-in-the-architecture-cs.md) usaram uma expiração baseada em tempo para remover os dados do cache após um período especificado. Essa abordagem é a maneira mais simples de balancear os ganhos de desempenho do cache contra a desatualização de dados. Ao selecionar uma expiração de tempo de *x* segundos, um desenvolvedor de página concedes a aproveitar os benefícios de desempenho do cache por apenas *x* segundos, mas pode ficar mais fácil que seus dados nunca sejam obsoletos por um máximo de *x* segundos. É claro que, para dados estáticos, *x* pode ser estendido para o tempo de vida do aplicativo Web, como foi examinado no tutorial [armazenando dados em cache no aplicativo de inicialização](caching-data-at-application-startup-cs.md) .

Ao armazenar em cache os dados do banco, uma expiração baseada em tempo é geralmente escolhida para sua facilidade de uso, mas frequentemente é uma solução inadequada. O ideal é que os dados do banco de dados permaneçam em cache até que os dados subjacentes tenham sido modificados no banco de dado; somente o cache seria removido. Essa abordagem maximiza os benefícios de desempenho do Caching e minimiza a duração dos dados obsoletos. No entanto, para aproveitar esses benefícios, deve haver algum sistema em vigor que saiba quando os dados subjacentes do banco foram modificados e remove os itens correspondentes do cache. Antes do ASP.NET 2,0, os desenvolvedores de páginas eram responsáveis por implementar esse sistema.

O ASP.NET 2,0 fornece uma [ `SqlCacheDependency` classe](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx) e a infraestrutura necessária para determinar quando uma alteração ocorreu no banco de dados para que os itens armazenados em cache correspondentes possam ser removidos. Há duas técnicas para determinar quando os dados subjacentes foram alterados: notificação e sondagem. Depois de discutir as diferenças entre notificação e sondagem, criaremos a infraestrutura necessária para dar suporte à sondagem e, em seguida, exploraremos como usar a `SqlCacheDependency` classe em cenários declarativos e programaticamente.

## <a name="understanding-notification-and-polling"></a>Entendendo a notificação e a sondagem

Há duas técnicas que podem ser usadas para determinar quando os dados em um banco de dado foram modificados: notificação e sondagem. Com a notificação, o banco de dados alertará automaticamente o tempo de execução ASP.NET quando os resultados de uma consulta específica tiverem sido alterados desde a última execução da consulta, em que ponto os itens armazenados em cache associados à consulta são removidos. Com a sondagem, o servidor de banco de dados mantém informações sobre quando tabelas específicas foram atualizadas pela última vez. O tempo de execução do ASP.NET sonda periodicamente o banco de dados para verificar quais tabelas foram alteradas desde que foram inseridas no cache. As tabelas cujos dados foram modificados têm seus itens de cache associados removidos.

A opção de notificação requer menos configuração do que a sondagem e é mais granular, pois controla as alterações no nível de consulta em vez de no nível de tabela. Infelizmente, as notificações só estão disponíveis nas edições completas do Microsoft SQL Server 2005 (ou seja, as edições não expressas). No entanto, a opção de sondagem pode ser usada para todas as versões do Microsoft SQL Server de 7,0 para 2005. Como esses tutoriais usam a edição Express do SQL Server 2005, nos concentraremos em configurar e usar a opção de sondagem. Consulte a seção leitura adicional no final deste tutorial para obter mais recursos sobre os recursos de notificação do SQL Server 2005 s.

Com a sondagem, o banco de dados deve ser configurado para incluir uma tabela chamada `AspNet_SqlCacheTablesForChangeNotification` que tenha três colunas- `tableName` , `notificationCreated` e `changeId` . Esta tabela contém uma linha para cada tabela que tem dados que podem precisar ser usados em uma dependência de cache do SQL no aplicativo Web. A `tableName` coluna especifica o nome da tabela enquanto `notificationCreated` indica a data e a hora em que a linha foi adicionada à tabela. A `changeId` coluna é do tipo `int` e tem um valor inicial de 0. Seu valor é incrementado com cada modificação na tabela.

Além da `AspNet_SqlCacheTablesForChangeNotification` tabela, o banco de dados também precisa incluir gatilhos em cada uma das tabelas que podem aparecer em uma dependência de cache do SQL. Esses gatilhos são executados sempre que uma linha é inserida, atualizada ou excluída e incrementa o valor de s da tabela `changeId` em `AspNet_SqlCacheTablesForChangeNotification` .

O tempo de execução do ASP.NET rastreia o atual `changeId` para uma tabela ao armazenar dados em cache usando um `SqlCacheDependency` objeto. O banco de dados é verificado periodicamente e todos os `SqlCacheDependency` objetos cujo `changeId` difere do valor no banco de dados são removidos, pois um `changeId` valor diferente indica que houve uma alteração na tabela desde que os dados foram armazenados em cache.

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>Etapa 1: explorando o `aspnet_regsql.exe` programa de linha de comando

Com a abordagem de sondagem, o banco de dados deve ser configurado para conter a infraestrutura descrita acima: uma tabela predefinida ( `AspNet_SqlCacheTablesForChangeNotification` ), alguns procedimentos armazenados e gatilhos em cada uma das tabelas que podem ser usadas em dependências de cache do SQL no aplicativo Web. Essas tabelas, procedimentos armazenados e gatilhos podem ser criados por meio do programa linha de comando `aspnet_regsql.exe` , localizado na `$WINDOWS$\Microsoft.NET\Framework\version` pasta. Para criar a `AspNet_SqlCacheTablesForChangeNotification` tabela e os procedimentos armazenados associados, execute o seguinte na linha de comando:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample1.cmd)]

> [!NOTE]
> Para executar esses comandos, o logon do banco de dados especificado deve estar nas [`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx) [`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx) funções e. Para examinar o T-SQL enviado ao banco de dados pelo `aspnet_regsql.exe` programa de linha de comando, consulte [esta entrada de blog](http://scottonwriting.net/sowblog/posts/10709.aspx).

Por exemplo, para adicionar a infraestrutura de sondagem a um banco de dados Microsoft SQL Server chamado `pubs` em um servidor de banco de dados chamado `ScottsServer` usando a autenticação do Windows, navegue até o diretório apropriado e, na linha de comando, digite:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample2.cmd)]

Depois que a infraestrutura no nível de banco de dados tiver sido adicionada, precisamos adicionar os gatilhos a essas tabelas que serão usadas em dependências de cache do SQL. Use o `aspnet_regsql.exe` programa de linha de comando novamente, mas especifique o nome da tabela usando a `-t` opção e, em vez de usar o `-ed` uso do comutador `-et` , desta forma:

[!code-html[Main](using-sql-cache-dependencies-cs/samples/sample3.html)]

Para adicionar os gatilhos às `authors` `titles` tabelas e no `pubs` banco de dados `ScottsServer` , use:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample4.cmd)]

Para este tutorial, adicione os gatilhos `Products` às `Categories` tabelas, e `Suppliers` . Veremos a sintaxe de linha de comando específica na etapa 3.

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>Etapa 2: fazendo referência a um banco de dados Microsoft SQL Server 2005 Express Edition em`App_Data`

O `aspnet_regsql.exe` programa de linha de comando requer o nome do banco de dados e do servidor para adicionar a infraestrutura de sondagem necessária. Mas qual é o nome do banco de dados e do servidor para um banco de dados Microsoft SQL Server 2005 Express que reside na `App_Data` pasta? Em vez de ter que descobrir quais são os nomes de banco de dados e servidor, eu me descobri que a abordagem mais simples é anexar o banco de `localhost\SQLExpress` dados à instância do Database e renomeá-los usando [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Se você tiver uma das versões completas do SQL Server 2005 instaladas em seu computador, provavelmente já terá SQL Server Management Studio instalado no computador. Se você tiver apenas a edição Express, poderá baixar o Microsoft SQL Server gratuito [Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796).

Comece fechando o Visual Studio. Em seguida, abra SQL Server Management Studio e opte por se conectar ao `localhost\SQLExpress` servidor usando a autenticação do Windows.

![Anexar ao servidor localhost\SQLExpress](using-sql-cache-dependencies-cs/_static/image1.gif)

**Figura 1**: anexar ao `localhost\SQLExpress` servidor

Depois de se conectar ao servidor, Management Studio mostrará o servidor e terá subpastas para os bancos de dados, segurança e assim por diante. Clique com o botão direito do mouse na pasta bancos de dados e escolha a opção anexar. Isso abrirá a caixa de diálogo anexar bancos de dados (consulte a Figura 2). Clique no botão Adicionar e selecione a `NORTHWND.MDF` pasta do banco de dados na pasta de seu aplicativo Web `App_Data` .

[![Anexe o NORTHWND. Banco de dados MDF da pasta App_Data](using-sql-cache-dependencies-cs/_static/image2.gif)](using-sql-cache-dependencies-cs/_static/image1.png)

**Figura 2**: anexar o `NORTHWND.MDF` banco de dados da `App_Data` pasta ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image2.png))

Isso adicionará o banco de dados à pasta databases. O nome do banco de dados pode ser o caminho completo para o arquivo de banco de dados ou o caminho completo foi colocado com um [GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier). Para evitar ter que digitar esse nome de banco de dados longo ao usar a \_ ferramenta de linha de comando aspnetregsql.exe, renomeie o banco de dados para um nome mais amigável clicando com o botão direito do mouse em banco de dados apenas anexado e escolhendo renomear. Eu me renomeei meu banco de dados como datatutorials.

![Renomear o banco de dados anexado para um nome mais amigável](using-sql-cache-dependencies-cs/_static/image3.gif)

**Figura 3**: renomear o banco de dados anexado para um nome mais amigável

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>Etapa 3: adicionar a infraestrutura de sondagem ao banco de dados Northwind

Agora que anexamos o `NORTHWND.MDF` banco de dados da `App_Data` pasta, estamos prontos para adicionar a infraestrutura de sondagem. Supondo que você tenha renomeado o banco de dados para datatutorials, execute os quatro comandos a seguir:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample5.cmd)]

Depois de executar esses quatro comandos, clique com o botão direito do mouse no nome do banco de dados em Management Studio, vá até o submenu tarefas e escolha desanexar. Em seguida, feche Management Studio e reabra o Visual Studio.

Depois que o Visual Studio for reaberto, aprofunde-se no banco de dados por meio do Gerenciador de Servidores. Observe a nova tabela ( `AspNet_SqlCacheTablesForChangeNotification` ), os novos procedimentos armazenados e os gatilhos nas `Products` tabelas, `Categories` e `Suppliers` .

![O banco de dados agora inclui a infraestrutura de sondagem necessária](using-sql-cache-dependencies-cs/_static/image4.gif)

**Figura 4**: o banco de dados agora inclui a infraestrutura de sondagem necessária

## <a name="step-4-configuring-the-polling-service"></a>Etapa 4: Configurando o serviço de sondagem

Depois de criar as tabelas, os gatilhos e os procedimentos armazenados necessários no banco de dados, a etapa final é configurar o serviço de sondagem, que é feito `Web.config` pelo especificando os bancos de dados a serem usados e a frequência de sondagem em milissegundos. A marcação a seguir sonda o banco de dados Northwind uma vez a cada segundo.

[!code-xml[Main](using-sql-cache-dependencies-cs/samples/sample6.xml)]

O `name` valor no `<add>` elemento (NorthwindDB) associa um nome legível por humanos a um banco de dados específico. Ao trabalhar com dependências de cache do SQL, precisaremos nos referir ao nome do banco de dados definido aqui, bem como à tabela na qual se baseiam o dado em cache. Veremos como usar a `SqlCacheDependency` classe para associar programaticamente dependências do cache SQL a dados armazenados em cache na etapa 6.

Depois que uma dependência de cache do SQL tiver sido estabelecida, o sistema de sondagem se conectará aos bancos de dados definidos nos `<databases>` elementos a cada `pollTime` milissegundos e executará o `AspNet_SqlCachePollingStoredProcedure` procedimento armazenado. Esse procedimento armazenado, que foi adicionado de volta na etapa 3 usando a `aspnet_regsql.exe` ferramenta de linha de comando, retorna os `tableName` `changeId` valores e para cada registro no `AspNet_SqlCacheTablesForChangeNotification` . As dependências do cache SQL desatualizadas são removidas do cache.

A `pollTime` Configuração apresenta uma compensação entre desempenho e desatualização de dados. Um `pollTime` valor pequeno aumenta o número de solicitações para o banco de dados, mas remove com mais rapidez o cache. Um `pollTime` valor maior reduz o número de solicitações de banco de dados, mas aumenta o atraso entre o momento em que o back-end é alterado e quando os itens de cache relacionados são removidos. Felizmente, a solicitação de banco de dados está executando um procedimento armazenado simples que retornam apenas algumas linhas de uma tabela simples e leve. Mas faça experiências com `pollTime` valores diferentes para encontrar um equilíbrio ideal entre o acesso ao banco de dados e a desatualização do seu aplicativo. O menor `pollTime` valor permitido é 500.

> [!NOTE]
> O exemplo acima fornece um único `pollTime` valor no `<sqlCacheDependency>` elemento, mas você pode opcionalmente especificar o `pollTime` valor no `<add>` elemento. Isso será útil se você tiver vários bancos de dados especificados e quiser personalizar a frequência de sondagem por banco de dados.

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>Etapa 5: trabalhando declarativamente com dependências de cache do SQL

Nas etapas 1 a 4, examinamos como configurar a infraestrutura de banco de dados necessária e configurar o sistema de sondagem. Com essa infraestrutura em vigor, agora podemos adicionar itens ao cache de dados com uma dependência de cache SQL associada usando técnicas programáticas ou declarativas. Nesta etapa, examinaremos como trabalhar de forma declarativa com as dependências de cache do SQL. Na etapa 6, veremos a abordagem programática.

Os [dados de cache com o tutorial ObjectDataSource](caching-data-with-the-objectdatasource-cs.md) exploraram os recursos de cache declarativos do ObjectDataSource. Ao simplesmente definir a `EnableCaching` propriedade como `true` e a `CacheDuration` propriedade como um intervalo de tempo, o ObjectDataSource armazenará em cache automaticamente os dados retornados de seu objeto subjacente para o intervalo especificado. O ObjectDataSource também pode usar uma ou mais dependências de cache do SQL.

Para demonstrar o uso de dependências do cache SQL declarativamente, abra a `SqlCacheDependencies.aspx` página na `Caching` pasta e arraste um GridView da caixa de ferramentas para o designer. Defina o GridView s `ID` como `ProductsDeclarative` e, de sua marca inteligente, escolha associá-lo a um novo ObjectDataSource chamado `ProductsDataSourceDeclarative` .

[![Criar um novo ObjectDataSource chamado ProductsDataSourceDeclarative](using-sql-cache-dependencies-cs/_static/image5.gif)](using-sql-cache-dependencies-cs/_static/image3.png)

**Figura 5**: criar um novo ObjectDataSource chamado `ProductsDataSourceDeclarative` ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image4.png))

Configure o ObjectDataSource para usar a `ProductsBLL` classe e defina a lista suspensa na guia selecionar como `GetProducts()` . Na guia atualizar, escolha a `UpdateProduct` sobrecarga com três parâmetros de entrada- `productName` , `unitPrice` e `productID` . Defina as listas suspensas como (nenhum) nas guias inserir e excluir.

[![Usar a sobrecarga UpdateProduct com três parâmetros de entrada](using-sql-cache-dependencies-cs/_static/image6.gif)](using-sql-cache-dependencies-cs/_static/image5.png)

**Figura 6**: usar a sobrecarga UpdateProduct com três parâmetros de entrada ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image6.png))

[![Defina a lista suspensa como (nenhum) para as guias inserir e excluir](using-sql-cache-dependencies-cs/_static/image7.gif)](using-sql-cache-dependencies-cs/_static/image7.png)

**Figura 7**: definir a lista suspensa como (nenhum) para as guias inserir e excluir ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image8.png))

Depois de concluir o assistente para configurar fonte de dados, o Visual Studio criará BoundFields e CheckBoxFields no GridView para cada um dos campos de dados. Remova todos os campos, mas, e `ProductName` `CategoryName` `UnitPrice` , e formate esses campos como você vê adequado. Na marca inteligente de GridView, marque as caixas de seleção habilitar paginação, Habilitar classificação e habilitar edição. O Visual Studio definirá a Propriedade ObjectDataSource s `OldValuesParameterFormatString` como `original_{0}` . Para que o recurso de edição GridView do funcione corretamente, remova essa propriedade totalmente da sintaxe declarativa ou defina-a de volta para seu valor padrão, `{0}` .

Por fim, adicione um controle rótulo da Web acima do GridView e defina sua `ID` propriedade como `ODSEvents` e sua `EnableViewState` propriedade como `false` . Depois de fazer essas alterações, a marcação declarativa de s de página deve ser semelhante à seguinte. Observe que eu fiz uma série de personalizações estética para os campos GridView que não são necessários para demonstrar a funcionalidade de dependência do cache do SQL.

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample7.aspx)]

Em seguida, crie um manipulador de eventos para o `Selecting` evento ObjectDataSource s e adicione o seguinte código:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample8.cs)]

Lembre-se de que o evento ObjectDataSource s `Selecting` é acionado somente ao recuperar dados de seu objeto subjacente. Se o ObjectDataSource acessar os dados de seu próprio cache, esse evento não será acionado.

Agora, visite esta página por meio de um navegador. Como já vimos implementar qualquer cache, sempre que você paginar, classificar ou editar a grade, a página deve exibir o texto, ' selecionando evento disparado, como mostra a Figura 8.

[![O evento ObjectDataSource s selecionando é acionado cada vez que GridView é paginado, editado ou classificado](using-sql-cache-dependencies-cs/_static/image8.gif)](using-sql-cache-dependencies-cs/_static/image9.png)

**Figura 8**: o evento ObjectDataSource s `Selecting` é acionado cada vez que GridView é paginado, editado ou classificado ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image10.png))

Como vimos no tutorial [dados de cache com o ObjectDataSource](caching-data-with-the-objectdatasource-cs.md) , definir a `EnableCaching` propriedade como `true` faz com que o ObjectDataSource armazene em cache seus dados para a duração especificada por sua `CacheDuration` propriedade. O ObjectDataSource também tem uma [ `SqlCacheDependency` Propriedade](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx), que adiciona uma ou mais dependências de cache do SQL aos dados armazenados em cache usando o padrão:

[!code-css[Main](using-sql-cache-dependencies-cs/samples/sample9.css)]

Em que *DatabaseName* é o nome do banco de dados, conforme especificado no `name` atributo do `<add>` elemento em `Web.config` , e *TableName* é o nome da tabela de banco de dados. Por exemplo, para criar um ObjectDataSource que armazena dados em cache indefinidamente com base em uma dependência de cache do SQL em relação à `Products` tabela Northwind, defina a Propriedade ObjectDataSource s `EnableCaching` como `true` e sua `SqlCacheDependency` propriedade como NorthwindDB: Products.

> [!NOTE]
> Você pode usar uma dependência de cache do SQL *e* uma expiração baseada em tempo definindo `EnableCaching` como `true` , `CacheDuration` para o intervalo de tempo e `SqlCacheDependency` para o banco de dados e os nomes de tabela. O ObjectDataSource removerá seus dados quando a expiração baseada em tempo for atingida ou quando o sistema de sondagem observar que os dados de banco de dado subjacentes foram alterados, o que acontecer primeiro.

O GridView no `SqlCacheDependencies.aspx` exibe dados de duas tabelas – `Products` e `Categories` (o campo produto s `CategoryName` é recuperado por meio de um `JOIN` ativado `Categories` ). Portanto, queremos especificar duas dependências de cache SQL: NorthwindDB: Products; NorthwindDB: categorias.

[![Configurar o ObjectDataSource para dar suporte ao cache usando dependências de cache do SQL em produtos e categorias](using-sql-cache-dependencies-cs/_static/image9.gif)](using-sql-cache-dependencies-cs/_static/image11.png)

**Figura 9**: configurar o ObjectDataSource para dar suporte ao cache usando dependências do cache SQL em `Products` e `Categories` ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image12.png))

Depois de configurar o ObjectDataSource para dar suporte ao Caching, visite a página novamente por meio de um navegador. Novamente, o texto ' selecionando o evento disparado deve aparecer na primeira página, mas deve desaparecer durante a paginação, classificação ou clique nos botões editar ou cancelar. Isso ocorre porque, depois que os dados são carregados no cache ObjectDataSource s, ele permanece lá até que as `Products` `Categories` tabelas ou sejam modificadas ou os dados sejam atualizados por meio de GridView.

Após a paginação pela grade e observando a falta da "selecionando texto acionado pelo evento, abra uma nova janela do navegador e navegue até o tutorial básico na seção editando, inserindo e excluindo ( `~/EditInsertDelete/Basics.aspx` ). Atualize o nome ou o preço de um produto. Em seguida, na primeira janela do navegador, exiba uma página de dados diferente, classifique a grade ou clique em um botão de edição de linha. Desta vez, o ' selecionando evento disparado deve reaparecer, pois os dados subjacentes do banco foram modificados (consulte a Figura 10). Se o texto não aparecer, aguarde alguns instantes e tente novamente. Lembre-se de que o serviço de sondagem está verificando alterações na `Products` tabela a cada `pollTime` milissegundos, portanto, há um atraso entre o momento em que os dados subjacentes são atualizados e quando os dados armazenados em cache são removidos.

[![A modificação da tabela produtos remove os dados do produto em cache](using-sql-cache-dependencies-cs/_static/image10.gif)](using-sql-cache-dependencies-cs/_static/image13.png)

**Figura 10**: a modificação da tabela produtos remove os dados do produto em cache ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image14.png))

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>Etapa 6: trabalhando programaticamente com a `SqlCacheDependency` classe

Os [dados de cache no tutorial de arquitetura](caching-data-in-the-architecture-cs.md) analisam os benefícios do uso de uma camada de cache separada na arquitetura em oposição ao acoplamento rígido do cache com o ObjectDataSource. Nesse tutorial, criamos uma `ProductsCL` classe para demonstrar programaticamente trabalhar com o cache de dados. Para utilizar as dependências de cache do SQL na camada de cache, use a `SqlCacheDependency` classe.

Com o sistema de sondagem, um `SqlCacheDependency` objeto deve ser associado a um par de banco de dados e tabela específico. O código a seguir, por exemplo, cria um `SqlCacheDependency` objeto com base na tabela s do banco de dados Northwind `Products` :

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample10.cs)]

Os dois parâmetros de entrada para o `SqlCacheDependency` Construtor s são os nomes de banco de dados e tabela, respectivamente. Assim como com a Propriedade ObjectDataSource s `SqlCacheDependency` , o nome do banco de dados usado é o mesmo que o valor especificado no `name` atributo do `<add>` elemento em `Web.config` . O nome da tabela é o nome real da tabela de banco de dados.

Para associar um a `SqlCacheDependency` um item adicionado ao cache de dados, use uma das `Insert` sobrecargas de método que aceita uma dependência. O código a seguir adiciona *valor* ao cache de dados por uma duração indefinida, mas o associa a uma `SqlCacheDependency` na `Products` tabela. Em suma, o *valor* permanecerá no cache até que seja removido devido a restrições de memória ou porque o sistema de sondagem detectou que a `Products` tabela foi alterada desde que foi armazenada em cache.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample11.cs)]

Atualmente, a classe s da camada de cache `ProductsCL` armazena em cache os dados da `Products` tabela usando uma expiração baseada em tempo de 60 segundos. Deixe que o s atualize essa classe para que ela use dependências de cache do SQL em vez disso. O `ProductsCL` método da classe s `AddCacheItem` , que é responsável por adicionar os dados ao cache, atualmente contém o seguinte código:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample12.cs)]

Atualize este código para usar um `SqlCacheDependency` objeto em vez da `MasterCacheKeyArray` dependência de cache:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample13.cs)]

Para testar essa funcionalidade, adicione um GridView à página abaixo do GridView existente `ProductsDeclarative` . Defina esse novo GridView s `ID` como `ProductsProgrammatic` e, por meio de sua marca inteligente, associe-o a um novo ObjectDataSource chamado `ProductsDataSourceProgrammatic` . Configure o ObjectDataSource para usar a `ProductsCL` classe, definindo as listas suspensas nas guias selecionar e atualizar para `GetProducts` e `UpdateProduct` , respectivamente.

[![Configurar o ObjectDataSource para usar a classe ProductsCL](using-sql-cache-dependencies-cs/_static/image11.gif)](using-sql-cache-dependencies-cs/_static/image15.png)

**Figura 11**: configurar o ObjectDataSource para usar a `ProductsCL` classe ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image16.png))

[![Selecione o método GetProducts na lista suspensa Selecionar Tab s](using-sql-cache-dependencies-cs/_static/image12.gif)](using-sql-cache-dependencies-cs/_static/image17.png)

**Figura 12**: selecione o `GetProducts` método na lista suspensa Selecionar Tab s ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image18.png))

[![Escolha o método UpdateProduct na lista suspensa da guia atualizar s](using-sql-cache-dependencies-cs/_static/image13.gif)](using-sql-cache-dependencies-cs/_static/image19.png)

**Figura 13**: escolha o método UpdateProduct na lista suspensa de atualizações na guia de atualização ([clique para exibir a imagem em tamanho normal](using-sql-cache-dependencies-cs/_static/image20.png))

Depois de concluir o assistente para configurar fonte de dados, o Visual Studio criará BoundFields e CheckBoxFields no GridView para cada um dos campos de dados. Assim como com o primeiro GridView adicionado a esta página, remova todos os campos, mas, `ProductName` `CategoryName` e `UnitPrice` e formate esses campos como desejar. Na marca inteligente de GridView, marque as caixas de seleção habilitar paginação, Habilitar classificação e habilitar edição. Assim como ocorre com o `ProductsDataSourceDeclarative` ObjectDataSource, o Visual Studio definirá a `ProductsDataSourceProgrammatic` Propriedade ObjectDataSource s `OldValuesParameterFormatString` como `original_{0}` . Para que o recurso de edição GridView do funcione corretamente, defina essa propriedade de volta para `{0}` (ou remova a atribuição de propriedade da sintaxe declarativa totalmente).

Depois de concluir essas tarefas, a marcação declarativa de GridView e ObjectDataSource resultante deve ser semelhante ao seguinte:

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample14.aspx)]

Para testar a dependência do cache do SQL na camada de cache, defina um ponto de interrupção no `ProductCL` método da classe s `AddCacheItem` e, em seguida, inicie a depuração. Quando você visita pela primeira vez `SqlCacheDependencies.aspx` , o ponto de interrupção deve ser atingido à medida que os dados são solicitados pelo primeiro e colocados no cache. Em seguida, mova para outra página no GridView ou classifique uma das colunas. Isso faz com que o GridView refaça seus dados, mas os dados devem ser encontrados no cache, já que a `Products` tabela de dados não foi modificada. Se os dados não forem encontrados repetidamente no cache, verifique se há memória suficiente disponível no computador e tente novamente.

Após a paginação por meio de algumas páginas do GridView, abra uma segunda janela do navegador e navegue até o tutorial básico na seção editando, inserindo e excluindo ( `~/EditInsertDelete/Basics.aspx` ). Atualize um registro da tabela produtos e, em seguida, na primeira janela do navegador, exiba uma nova página ou clique em um dos cabeçalhos de classificação.

Nesse cenário, você verá uma das duas coisas: ou o ponto de interrupção será atingido, indicando que os dados armazenados em cache foram removidos devido à alteração no banco de dados; ou, o ponto de interrupção não será atingido, o que significa que `SqlCacheDependencies.aspx` agora está mostrando dados obsoletos. Se o ponto de interrupção não for atingido, é provável que o serviço de sondagem ainda não tenha sido acionado desde que os dados foram alterados. Lembre-se de que o serviço de sondagem está verificando alterações na `Products` tabela a cada `pollTime` milissegundos, portanto, há um atraso entre o momento em que os dados subjacentes são atualizados e quando os dados armazenados em cache são removidos.

> [!NOTE]
> Esse atraso é mais provável de aparecer ao editar um dos produtos por meio do GridView no `SqlCacheDependencies.aspx` . Nos [dados de cache no tutorial de arquitetura](caching-data-in-the-architecture-cs.md) , adicionamos a `MasterCacheKeyArray` dependência de cache para garantir que os dados que estão sendo editados por meio do método de `ProductsCL` classe s `UpdateProduct` foram removidos do cache. No entanto, substituímos essa dependência de cache ao modificar o `AddCacheItem` método anteriormente nesta etapa e, portanto, a `ProductsCL` classe continuará a mostrar os dados armazenados em cache até que o sistema de sondagem anote a alteração na `Products` tabela. Veremos como reintroduzir a dependência de `MasterCacheKeyArray` cache na etapa 7.

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>Etapa 7: associando várias dependências a um item em cache

Lembre-se de que a `MasterCacheKeyArray` dependência de cache é usada para garantir que *todos os* dados relacionados ao produto sejam removidos do cache quando um único item associado a ele for atualizado. Por exemplo, o `GetProductsByCategoryID(categoryID)` método armazena em cache `ProductsDataTables` instâncias para cada valor de *CategoryID* exclusivo. Se um desses objetos for removido, a dependência de `MasterCacheKeyArray` cache garantirá que os outros também sejam removidos. Sem essa dependência de cache, quando os dados armazenados em cache são modificados, existe a possibilidade de que outros dados do produto em cache estejam desatualizados. Consequentemente, é importante que mantenhamos a `MasterCacheKeyArray` dependência de cache ao usar dependências do cache SQL. No entanto, o método s do cache de dados `Insert` permite apenas um único objeto de dependência.

Além disso, ao trabalhar com dependências de cache SQL, talvez seja necessário associar várias tabelas de banco de dados como dependências. Por exemplo, o `ProductsDataTable` cache na `ProductsCL` classe contém os nomes de categoria e de fornecedor para cada produto, mas o `AddCacheItem` método usa apenas uma dependência em `Products` . Nessa situação, se o usuário atualizar o nome de uma categoria ou fornecedor, os dados do produto em cache permanecerão no cache e ficarão desatualizados. Portanto, queremos tornar os dados do produto em cache dependentes não apenas da `Products` tabela, mas `Categories` também nas tabelas e `Suppliers` .

A [ `AggregateCacheDependency` classe](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx) fornece um meio para associar várias dependências a um item de cache. Comece criando uma `AggregateCacheDependency` instância. Em seguida, adicione o conjunto de dependências usando o `AggregateCacheDependency` `Add` método s. Ao inserir o item no cache de dados posteriormente, passe a `AggregateCacheDependency` instância. Quando *qualquer* uma das `AggregateCacheDependency` dependências de s da instância for alterada, o item armazenado em cache será removido.

A seguir, é mostrado o código atualizado para o `ProductsCL` método da classe s `AddCacheItem` . O método cria a `MasterCacheKeyArray` dependência de cache junto com `SqlCacheDependency` objetos para `Products` as `Categories` tabelas, e `Suppliers` . Todos eles são combinados em um `AggregateCacheDependency` objeto chamado `aggregateDependencies` , que é passado para o `Insert` método.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample15.cs)]

Teste esse novo código. Agora, as alterações `Products` nas `Categories` tabelas, ou fazem com que `Suppliers` os dados armazenados em cache sejam removidos. Além disso, o `ProductsCL` método da classe s `UpdateProduct` , que é chamado ao editar um produto por meio do GridView, remove a `MasterCacheKeyArray` dependência do cache, o que faz com que o cache `ProductsDataTable` seja removido e os dados sejam recuperados novamente na próxima solicitação.

> [!NOTE]
> As dependências do cache SQL também podem ser usadas com o [cache de saída](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx). Para ver uma demonstração dessa funcionalidade, consulte: [usando o cache de saída do ASP.NET com SQL Server](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx).

## <a name="summary"></a>Resumo

Ao armazenar em cache os dados do banco, os dados permanecerão idealmente no cache até que sejam modificados no banco de dado. Com o ASP.NET 2,0, as dependências de cache do SQL podem ser criadas e usadas em cenários declarativos e programáticos. Um dos desafios dessa abordagem é descobrir quando os dados foram modificados. As versões completas do Microsoft SQL Server 2005 fornecem recursos de notificação que podem alertar um aplicativo quando um resultado da consulta é alterado. Para a edição Express do SQL Server 2005 e versões mais antigas do SQL Server, um sistema de sondagem deve ser usado em vez disso. Felizmente, a configuração da infraestrutura de sondagem necessária é bem simples.

Boa programação!

## <a name="further-reading"></a>Leituras adicionais

Para obter mais informações sobre os tópicos discutidos neste tutorial, consulte os seguintes recursos:

- [Usando notificações de consulta no Microsoft SQL Server 2005](https://msdn.microsoft.com/library/ms175110.aspx)
- [Criando uma notificação de consulta](https://msdn.microsoft.com/library/ms188669.aspx)
- [Caching em ASP.NET com a `SqlCacheDependency` classe](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [Ferramenta de registro de SQL Server ASP.NET ( `aspnet_regsql.exe` )](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [Visão geral do `SqlCacheDependency`](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>Sobre o autor

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor de sete livros sobre ASP/ASP. net e fundador da [4guysfromrolla.com](http://www.4guysfromrolla.com), tem trabalhado com tecnologias Web da Microsoft desde 1998. Scott trabalha como consultor, instrutor e escritor independentes. Seu livro mais recente é que a [*Sams ensina a ASP.NET 2,0 em 24 horas*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ele pode ser acessado em [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) ou por meio de seu blog, que pode ser encontrado em [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Agradecimentos especiais a

Esta série de tutoriais foi revisada por muitos revisores úteis. Os revisores potenciais para este tutorial foram Marko Rangel, Teresa Murphy e Hilton Giesenow. Está interessado em revisar meus artigos futuros do MSDN? Nesse caso, me solte uma linha em [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Anterior](caching-data-at-application-startup-cs.md) 
>  [Avançar](caching-data-with-the-objectdatasource-vb.md)
