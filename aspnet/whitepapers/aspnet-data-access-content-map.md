---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET Acesso a Dados - Recursos Recomendados | Microsoft Docs
author: rick-anderson
description: Este tópico fornece links para recursos de documentação sobre como acessar dados em ASP.NET aplicativos web, principalmente usando o Framework entity e sql se...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676163"
---
# <a name="aspnet-data-access---recommended-resources"></a>Acesso a Dados do ASP.NET – Recursos recomendados

> Este tópico fornece links para recursos de documentação sobre como acessar dados em ASP.NET aplicativos web, principalmente usando o Entity Framework e o SQL Server.
> 
> Se você conhece um ótimo post de blog, [thread stackoverflow](http://stackoverflow.com) ou qualquer outro link que seja útil, [envie-nos um e-mail](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) com o link.
> 
> Última atualização em 3/04/2014

Este tópico contém as seguintes seções:

- [Começando com o acesso a dados em ASP.NET](#gettingstarted)
- [Usando o Quadro de Entidades](#ef)

    - [Usando o código-quadro da entidade primeiro](#cf)
    - [Usando as primeiras migrações do Código-Quadro da Entidade](#efcfmigrations)
    - [Usando o banco de dados framework da entidade primeiro ou o modelo primeiro (o designer da EF)](#efdbf)
    - [Carregar dados relacionados no Framework entity (carga preguiçosa, carregamento ansioso e carregamento explícito)](#efrelateddata)
    - [Otimização do desempenho do framework da entidade](#optimizingef)
    - [Manipulação de concorrência em um aplicativo de quadro de entidades](#efconcurrency)
    - [Livros sobre o Quadro de Entidades](#efbooks)
    - [Recursos adicionais do Framework da entidade](#otherefresources)
- [Vinculação de dados em aplicativos de formulários ASP.NET Web](#wfdatabinding)

    - [Usando a vinculação do modelo de formulários da Web](#wfmodelbinding)
    - [Usando controles de origem de dados de formulários da Web](#wfdsc)
    - [Usando controles vinculados a dados da Web e expressões de vinculação de dados](#wfdbc)
- [Trabalhando com bancos de dados sql server](#sqlserver)

    - [Trabalhando com bancos de dados SQL Server Express LocalDB](#sslocaldb)
    - [Trabalhando com bancos de dados expressos do SQL Server](#sse)
    - [Trabalhando com o Banco de Dados SQL do Windows Azure](#ssdb)
    - [Escolhendo entre sql server e banco de dados SQL do Windows Azure](#ssdbchoosing)
- [Trabalhando com sistemas de gerenciamento de banco de dados NoSQL](#nosql)
- [Usando consultas LINQ em aplicativos de ASP.NET](#linq)
- [Usando andaimes de dados dinâmicos](#dd)
- [Garantindo o acesso aos dados](#securing)
- [Otimização do desempenho do acesso a dados](#optimizingdataaccess)
- [Implantando um banco de dados](#deploying)
- [Acessando dados através de um Serviço Web](#webservice)
- [Recursos adicionais](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>Começando com o acesso a dados em ASP.NET

- [Opções de armazenamento de dados (construindo aplicativos de nuvem do mundo real com o Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). Capítulo de um e-book sobre desenvolvimento para a nuvem. Introduz bancos de dados NoSQL como uma alternativa que muitos desenvolvedores familiarizados com bancos de dados relacionais tendem a ignorar. Apresenta diretrizes sobre o que pensar ao escolher relacional ou NoSQL, ou escolher uma determinada plataforma.
- [ASP.NET Opções de Acesso a Dados](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). Introdução às opções de acesso a dados para bancos de dados relacionais para ASP.NET e orientações sobre como escolher plataformas e métodos de acesso adequados ao seu cenário.
- [Banco de dados relacional](http://en.wikipedia.org/wiki/Relational_database). Wikipédia). Se você não trabalhou com bancos de dados relacionais, consulte esta página para uma introdução à terminologia e conceitos de banco de dados relacionais. Para uma introdução ao SQL Server, em particular, consulte [Trabalhando com bancos de dados SQL Server](#sqlserver) mais tarde neste tópico.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Usando o Quadro de Entidades

- [Abordagens de desenvolvimento de estruturas de entidades](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Orientações sobre como escolher uma abordagem de desenvolvimento do Framework de entidades Primeiro, Modelo Primeiro ou Código Primeiro.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Usando o código-quadro da entidade primeiro

Os tutoriais a seguir oferecem aplicativos de amostra para download:

- [Começando com eF 6 usando MVC 5](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Abrange uma ampla gama de cenários do Entity Framework Code First, incluindo migrações e recursos do EF 6, como resiliência de conexão, interceptação de comando e assincronia. Esta é uma versão atualizada da [série EF 5 / MVC 4](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). A série anterior inclui um tutorial sobre o repositório e padrões de unidade de trabalho que não está incluído na nova série.
- [Introdução ao ASP.NET MVC 5](../mvc/overview/getting-started/introduction/getting-started.md). Abrange uma gama mais estreita de cenários do Entity Framework Code First, mas faz um trabalho mais abrangente de introdução de recursos de MVC.
- [Modelo binding e formulários web](https://go.microsoft.com/fwlink/?LinkId=286117). Usa o Código Primeiro em um aplicativo de Formulários da Web.
- [Começando com ASP.NET 4.5 Formulários web](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Uma introdução aos Formulários web com alguma cobertura do Code First. Usa vinculação de modelo.
- [MVC Music Store](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). Usa o Código Primeiro em um aplicativo de e-commerce MVC 3 que também implementa adesão e autorização. A versão MVC e o sistema de adesão ASP.NET (autenticação e autorização) utilizados aqui estão desatualizados; para obter mais informações atualizadas sobre [https://asp.net/identity](https://asp.net/identity)ASP.NET a de adesão, consulte .

Outros recursos:

- [Framework da entidade - Código primeiro para um banco de dados existente](https://msdn.microsoft.com/data/jj200620). Msdn. Vídeo e passo a passo que mostra como usar o Code First com um banco de dados existente.
- [Data Developer Center - Entity Framework](https://msdn.microsoft.com/data/ef). Msdn. Para obter um guia para a documentação do Quadro de Entidades que foi criado e mantido pela equipe do Quadro de Entidades, consulte o link ['Iniciar'.](https://msdn.microsoft.com/data/ee712907)

Consulte também [livros sobre o Quadro de Entidades](#efbooks) e Recursos [Estruturais adicionais de entidades](#otherefresources) mais tarde neste tópico.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Usando as primeiras migrações do Código-Quadro da Entidade

A maioria dos tutoriais do Code First listados acima cobrem migrações. Veja também os seguintes recursos.

- [Implantação da Web do ASP.NET usando o Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). Série de tutoriais de duas partes que mostra como usar as Migrações do Código primeiro para implantar um banco de dados.
- [Implante um aplicativo Secure ASP.NET MVC 5 com banco de dados de adesão, OAuth e SQL em um site do Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Microsoft Azure). Como usar migrações para implantar dados de adesão e aplicativos no Azure.
- [Visão geral da implantação da Web para o Visual Studio e ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment). Consulte a **configuração de implantação de banco de dados na** seção Visual Studio para obter uma explicação de como as Primeiras Migrações de Código são integradas aos recursos de implantação web do Visual Studio.
- [Data Developer Center - Code First Migrations](https://msdn.microsoft.com/data/jj591621) (MSDN). A documentação de Migrações da equipe do Quadro de Entidades.
- [Migrações Série screencast](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). Blog da EF). Três vídeos sobre tópicos avançados em Code First Migrations.
- [Código Primeiras migrações com sites de páginas da Web ASP.NET.](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites) Blog mikesdotnetting). Mostra como usar as migrações do Code First com um site de páginas da ASP.NET, colocando o contexto de dados em um projeto de biblioteca de classe visual studio.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Usando o banco de dados framework da entidade primeiro ou o modelo primeiro (o designer da EF)

- [Começando com o banco de dados Entity Framework 6 primeiro usando MVC 5](../mvc/overview/getting-started/database-first-development/setting-up-database.md). Execute um script no Server Explorer para criar um banco de dados e, em seguida, use o designer Entity Framework para criar o modelo de dados. Mostra como criar páginas web CRUD simples e para outras funções de manipulação de dados, você pode seguir um dos tutoriais do Code First, já que todos os fluxos de trabalho Da EF usam a mesma API do DbContext.

Os seguintes recursos são mais antigos. Eles são úteis se você quiser usar a versão 4.0 do Entity Framework e quiser usar um controle de origem de dados para vinculação de dados em um aplicativo Web Forms.

- [Começando com o Quadro de Entidades 4.0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). Mostra como usar o controle **EntityDataSource.**
- [Continuando com o Framework entity](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(mostra como usar o Controle **ObjectDataSource.** Inclui um tutorial sobre manipulação de simultâneos, um tutorial sobre o desempenho da EF e um tutorial sobre as novidades na EF 4.0.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Manipulação de dados relacionados no Entity Framework (Carga Preguiçosa, Carregamento Ansioso e Carregamento Explícito)

- [Leitura de dados relacionados com o Framework entity em um aplicativo mvc ASP.NET](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md). Código Primeiro, aplicação de amostra MVC. Os métodos mostrados aplicam-se também à vinculação do modelo Formulários da Web e ao fluxo de trabalho Database First.
- [Data Developer Center - Loading Related Entities](https://msdn.microsoft.com/data/jj574232) (MSDN). Documentação da equipe do Entity Framework sobre o carregamento de dados relacionados.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Otimização do desempenho do Framework de entidades

- [Cenários-quadro de entidades avançadas para uma aplicação ASP.NET](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md). Mostra como executar suas próprias instruções SQL ou chamar seus próprios procedimentos armazenados, como desativar a detecção de alterações e como desativar a validação ao salvar alterações.
- [Considerações de desempenho para o Quadro de Entidades 5](https://msdn.microsoft.com/data/hh949853) (MSDN).
- [Considerações de desempenho (Framework de entidades)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [Maximizando o desempenho com o Framework de entidades em um ASP.NET aplicativo web](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md). Aplica-se ao Quadro de Entidades 4.0.
- Veja também [Otimizando ASP.NET acesso a dados](#optimizingdataaccess) mais tarde neste tópico.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Manipulação de concorrência em um aplicativo de quadro de entidades

- [Manuseio de conmoeda com o Quadro de Entidades em um ASP.NET aplicativo MVC](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md). Código Primeiro, API DbContext, usando um aplicativo de amostra MVC.
- [Data Developer Center – Padrões de concorrência otimistas](https://msdn.microsoft.com/data/jj592904) (MSDN). A documentação de simultuo da equipe do Quadro de Entidades.
- [Manipulação de concorrência com o Framework entity framework em um ASP.NET aplicativo Web](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). Aplica-se ao Quadro de Entidades 4.0. Banco de dados Primeiro, ObjectContext API, usando um aplicativo de amostra Web Forms.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Livros sobre o Quadro de Entidades

- [Estrutura de Entidades de Programação: DbContext](http://shop.oreilly.com/product/0636920022237.do) por Julie Lerman e Rowan Miller.
- [Estrutura da Entidade de Programação: Código Primeiro](http://shop.oreilly.com/product/0636920022220.do) por Julie Lerman e Rowan Miller.

Ambos os livros estão atualizados com as técnicas recomendadas atuais. Eles fornecem uma introdução mais abrangente, mas fácil de seguir ao Quadro de Entidades do que qualquer coisa disponível na Internet. Outro livro, [Programming Entity Framework](http://shop.oreilly.com/product/9780596807252.do) de Julie Lerman, é maior e mais abrangente, mas é mais antigo e muitas das técnicas que ele cobre não são mais a maneira recomendada de usar o Quadro de Entidades. Veja também a lista de livros recomendados pela equipe do Entity Framework no [Data Developer Center - Livros](https://msdn.microsoft.com/data/aa937716) no site do MSDN.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>Outros Recursos-Quadro da Entidade

- [Blog da equipe entity Framework (ADO.NET).](https://blogs.msdn.com/b/adonet/) Um dos melhores recursos para as informações mais atuais e anúncios de novos aprimoramentos. Para outros blogs relacionados à EF, consulte o Blogroll em [Get Started with Entity Framework](https://msdn.microsoft.com/data/ee712907).
- [Revista MSDN.](https://msdn.microsoft.com/magazine/default.aspx) Consulte a coluna **Pontos de Dados,** que é freqüentemente sobre temas relacionados ao Quadro de Entidades.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>Vinculação de dados em aplicativos de formulários ASP.NET Web

- [ASP.NET Opções de acesso a](https://msdn.microsoft.com/library/jj822927.aspx) dados<a id="wfmodelbinding"></a>(MSDN) de formulários da Web .

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Usando a vinculação do modelo de formulários da Web

- [Modelo binding e formulários web](https://go.microsoft.com/fwlink/?LinkId=286117). Série tutorial usando ef code first.
- [Modelo de Formulários da Web Parte 1: Seleção de Dados](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (blog de Scott Guthrie). Nessas postagens mais antigas do blog, a propriedade atualmente chamada ItemType foi nomeada ModelType, mas caso contrário, as informações que eles contêm são válidas.
- [Modelo de Formulários da Web Parte 2: Filtragem de Dados](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (blog de Scott Guthrie).
- [Modelo de Formulários da Web Vinculante Parte 3: Atualização e Validação](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (blog de Scott Guthrie).
- [ASP.NET vinculação do modelo de formulários da Web 4.5](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md). (vídeo).
- [Modelo de vinculação Parte 1 - Seleção de Dados](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (vídeo).
- [Modelo de ligação Parte 2 - Filtragem](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (vídeo).
- [Começando com ASP.NET 4.5 Formulários da Web - Exibir itens e detalhes de dados](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Usando controles de origem de dados de formulários da Web

- [Controles de servidor web](https://msdn.microsoft.com/library/ms247258.aspx) de origem de dados (MSDN).
- [Anunciando o lançamento do provedor de dados dinâmicos e do controle EntityDataSource para entity framework 6](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) (blog Microsoft Web Development).

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Usando controles vinculados a dados da Web e expressões de vinculação de dados

- [Modelo binding e formulários web](https://go.microsoft.com/fwlink/?LinkId=286117). Série tutorial que usa EF Code First.
- [Começando com ASP.NET 4.5 Formulários da Web - Exibir itens e detalhes de dados](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).
- [Controles de dados fortemente digitados](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (blog de Scott Guthrie).
- [Controles de dados fortemente digitados](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (vídeo).
- [ASP.NET 4.5 Web Forms Strong Typed Data Controls](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (vídeo).
- [Controles de servidor web vinculados a dados](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN).
- [Visão geral das expressões de vinculação de dados](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). Esta página abrange apenas **Eval** e **Bind;** ele não foi atualizado para incluir **Item** e **BindItem**.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>Trabalhando com bancos de dados sql server

- [Recursos do banco de dados do servidor SQL](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). Para uma introdução geral a uma ampla variedade de tópicos do SQL Server, consulte as entradas sob este no TOC.
- [SQL Server Editions](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). Um resumo das edições disponíveis do SQL Server, com links para mais informações sobre cada um.)
- [Strings de conexão do servidor SQL para aplicativos web ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Usando o SQL Server Compact para ASP.NET Aplicações Web](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN).
- [Microsoft SQL Server: Amostras de produtos de banco de dados](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Aprove os bancos de dados AdventureWorks.
- [Instalação de bancos de dados de amostras](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Além dos métodos mostrados aqui, você também pode baixar um dos\_arquivos de sample .mdf para a pasta App Data de um projeto web, converter o banco de dados para LocalDB e criar uma seqüência de conexão LocalDB. Para obter informações sobre como fazer isso, consulte [Como: Atualizar para LocalDB](https://msdn.microsoft.com/library/hh873188.aspx).

Veja também as seções a seguir sobre como trabalhar com o SQL Server Express e o LocalDB, e escolher entre o SQL Server e o SQL Database.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>Trabalhando com bancos de dados SQL Server Express LocalDB

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). A introdução oficial do MSDN ao LocalDB.
- [Strings de conexão do servidor SQL para aplicativos web ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Como: Atualizar para LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN). Como migrar um arquivo .mdf de uma versão anterior do SQL Server Express para o LocalDB. Você também tem que passar por esse processo se você baixar um dos bancos de dados de [amostra do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=117483).
- [Apresentando o LocalDB, um sql express melhorado](https://go.microsoft.com/fwlink/?LinkId=234375) (blog SQL Server Express). Tem mais informações sobre por que o LocalDB foi criado do que está incluído no MSDN.
- [LocalDB: Onde está meu banco de dados?](https://go.microsoft.com/fwlink/?LinkId=234376) (Blog SQL Server Express). Informações sobre onde os arquivos de banco de dados LocalDB são criados.
- [Usando localDB com IIS completo, Parte 1: Perfil de Usuário](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (blog SQL Server Express). O LocalDB não foi projetado para trabalhar com o IIS. Esta série de posts no blog explica os problemas e algumas soluçãos.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>Trabalhando com bancos de dados expressos do SQL Server

- [Strings de conexão do servidor SQL para aplicativos web ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN). Se você usar a configuração de string attachDBFileName com o SQL Server Express, consulte especialmente a seção Ocorrência de Usuário desta página.
- [Como tomar posse do seu SQL Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (blog SQL Server Express). Um problema comum é não poder trabalhar com bancos de dados SQL Server Express porque você não é um administrador na instância do SQL Server Express. Por padrão, apenas a pessoa que instalou o SQL Server Express é um administrador. Este blog explica como se tornar um administrador do SQL Server Express se você é um administrador no computador.
- [Meu aplicativo web ASP.NET pode usar um banco de dados SQL Server Express em produção?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Trabalhando com o Banco de Dados SQL do Windows Azure

- [Implante um aplicativo MVC de ASP.NET seguro com banco de dados de adesão, OAuth e SQL em um site do Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (site do Microsoft Azure).
- [Bancos de dados SQL](https://docs.microsoft.com/azure/sql-database/) (site do Microsoft Azure). Começando tutoriais e guias de como fazer.
- [Banco de dados SQL do Windows Azure](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). O nó de nível superior da tabela de conteúdo para Banco de Dados SQL em MSDN.
- [Windows Azure SQL Database TechNet Wiki Articles Index](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (site da Microsoft TechNet).
- [Bloco de aplicação de manuseio de falhas transitórias](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). Uma estrutura que permite lidar com falhas transitórias de rede e erros de conexão que resultam do estrangulamento. Disponível em um pacote NuGet: [Enterprise Library 5.0 - Transiente Fault Handling Application Block](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling).
- [Começando com o SQL Database and Entity Framework](https://msdn.microsoft.com/data/jj556244) (MSDN).
- [Kit de treinamento do Windows Azure](https://www.microsoft.com/download/details.aspx?id=8396) (Microsoft Download Center). Inclui laboratórios práticos para banco de dados SQL.
- [Fórum comunitário do banco de dados Windows Azure SQL](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Movendo-se para o Windows Azure SQL Database](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN). Um capítulo de um cenário abrangente de ponta a ponta pela equipe de Padrões e Práticas da Microsoft. Cobre por que você pode querer migrar e como migrar do SQL Server para o SQL Database.
- [Migração de bancos de dados do SQL Server para o Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).
- [Assistente de migração de banco de dados SQL](http://sqlazuremw.codeplex.com/). Uma ferramenta de código aberto para migração de bancos de dados para e do Banco de Dados SQL.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>Escolhendo entre sql server e banco de dados SQL do Windows Azure

- [Compare o SQL Server com o Windows Azure SQL Database](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (site da Microsoft TechNet).
- [Migração de dados para o Banco de Dados SQL do Windows Azure: Ferramentas e Técnicas](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). Inclui seções que comparam o SQL Server com o SQL Database e fornecem orientações sobre quando migrar do SQL Server para o SQL Database.
- [Guia de entrega de banco de dados do Windows Azure SQL](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (site da Microsoft TechNet).
- [Limitações de recursos do SQL Server (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Armazenamento de mesa do Windows Azure e banco de dados SQL do Windows Azure - Comparado e Contrastado](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Para um aplicativo que você implanta no Windows Azure, o armazenamento da Tabela Windows Azure pode ser uma alternativa ao Banco de Dados SQL do Windows Azure. Este tópico ajuda você a decidir entre essas alternativas.
- [Banco de dados SQL do Windows Azure](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [Diretrizes e limitações (banco de dados SQL do Windows Azure)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>Trabalhando com sistemas de gerenciamento de banco de dados NoSQL

- [Windows Azure Data Services](https://www.windowsazure.com/develop/net/data/) (site do Microsoft Azure). Consulte o [guia de recursos do Serviço de Tabela](https://docs.microsoft.com/azure/) e a seção Big **Data** da página.
- [ASP.NET aplicativo multi-nível usando tabelas de armazenamento, filas e blobs](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (site do Microsoft Azure). Tutorial de ponta a ponta com aplicativo de amostra para download que usa tabelas NoSQL de armazenamento do Windows Azure.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>Usando consultas LINQ em aplicativos de ASP.NET

- [ASP.NET Opções de Acesso a Dados](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). Inclui uma introdução ao LINQ.
- [Vídeos de treinamento linq](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (blog de Joe Stagner).
- [ASP.NET thread do Fórum com links para recursos linq dinâmicos](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq).

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Usando andaimes de dados dinâmicos

- [Modelos dinâmicos de projetos de dados](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN). Orientação sobre quando usar projetos de Dados Dinâmicos.
- [ASP.NET Dados Dinâmicos](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>Garantindo o acesso aos dados

- [Proteção do acesso a dados em ASP.NET](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN).
- [Considerações de segurança (Framework entity)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- [Como: Conectar strings de conexão segura ao usar controles de origem de dados](https://msdn.microsoft.com/library/ms178372.aspx) (MSDN).

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>Otimização do desempenho do acesso a dados

- [visão geral do desempenho ASP.NET](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET Caching](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [Melhorando o desempenho ASP.NET](https://msdn.microsoft.com/library/ff647787) (MSDN). Há um aviso de "Conteúdo aposentado" no topo desta página, mas a maioria das informações ainda é relevante e não há nenhum recurso atualizado comparável.
- [Melhorando o desempenho do servidor SQL](https://msdn.microsoft.com/library/ff647793) (MSDN). Mesmo comentário do link anterior.

Veja também [o desempenho do Quadro de Entidades otimizando](#optimizingef) no início deste tópico.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>Implantando um banco de dados

- [ASP.NET Implantação da Web - Recursos Recomendados](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Acessando dados através de um Serviço Web

- [Acessando dados através de um Serviço Web](https://msdn.microsoft.com/library/ms178359.aspx#webservice) (MSDN). Orientação sobre quando usar API web versus WCF.
- [Começando com ASP.NET API web](../web-api/index.md).
- [Serviços de dados WCF](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>Recursos adicionais

- [ASP.NET faq de acesso a dados](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [tutoriais de formulários ASP.NET web - Dados](../web-forms/overview/data-access/index.md). A maioria desses tutoriais são relativamente antigos; certifique-se de ler [ASP.NET Opções de Acesso a Dados](https://msdn.microsoft.com/library/ms178359.aspx) e [Opções de Armazenamento de Dados (Construindo Aplicativos de Nuvem do Mundo Real com o Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) primeiro para que você não se esifique muito em um método de acesso a dados que não seja certo para o seu cenário.
- [ASP.NET mapa de conteúdo MVC](../mvc/overview/getting-started/recommended-resources-for-mvc.md).
- [tutoriais de páginas da ASP.NET - Dados](../web-pages/overview/data/index.md).
- [Acessando dados no Visual Studio](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN). Fornece uma lista de links semelhantes a este mapa de conteúdo, mas com foco no Visual Studio em vez de ASP.NET.
