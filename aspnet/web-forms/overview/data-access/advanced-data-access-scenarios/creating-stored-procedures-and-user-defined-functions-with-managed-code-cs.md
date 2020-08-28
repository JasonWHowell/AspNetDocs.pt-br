---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
title: Criando procedimentos armazenados e funções definidas pelo usuário com código gerenciado (C#) | Microsoft Docs
author: rick-anderson
description: O Microsoft SQL Server 2005 integra-se com o Common Language Runtime do .NET para permitir que os desenvolvedores criem objetos de banco de dados por meio de código gerenciado. Este tutorial...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 213eea41-1ab4-4371-8b24-1a1a66c515de
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
msc.type: authoredcontent
ms.openlocfilehash: c1882d019d9dfde2dc4f960cae65aa8268c97a51
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045293"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-c"></a>Criar procedimentos armazenados e funções definidas pelo usuário com código gerenciado (C#)

por [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Baixar código](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_CS.zip) ou [baixar PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/datatutorial75cs1.pdf)

> O Microsoft SQL Server 2005 integra-se com o Common Language Runtime do .NET para permitir que os desenvolvedores criem objetos de banco de dados por meio de código gerenciado. Este tutorial mostra como criar procedimentos armazenados gerenciados e funções gerenciadas definidas pelo usuário com seu código Visual Basic ou C#. Também vemos como essas edições do Visual Studio permitem que você depure esses objetos de banco de dados gerenciado.

## <a name="introduction"></a>Introdução

Bancos de dados como o Microsoft s SQL Server 2005 usam o [Transact-linguagem SQL (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) para inserção, modificação e recuperação. A maioria dos sistemas de banco de dados inclui construções para agrupar uma série de instruções SQL que podem ser executadas como uma única unidade reutilizável. Os procedimentos armazenados são um exemplo. Outra é UDFs ( *funções definidas pelo usuário*), uma construção que examinaremos mais detalhadamente na etapa 9.

Em seu núcleo, o SQL foi projetado para trabalhar com conjuntos de dados. As `SELECT` `UPDATE` instruções,, e `DELETE` inerentemente se aplicam a todos os registros na tabela correspondente e são limitadas apenas por suas `WHERE` cláusulas. Ainda há muitos recursos de linguagem projetados para trabalhar com um registro por vez e para manipular dados escalares. [ `CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553) permitem que um conjunto de registros seja executado em loop por um de cada vez. Funções de manipulação de cadeia de caracteres como `LEFT` , `CHARINDEX` e `PATINDEX` funcionam com dados escalares. O SQL também inclui instruções de fluxo `IF` de controle como e `WHILE` .

Antes do Microsoft SQL Server 2005, os procedimentos armazenados e UDFs só podiam ser definidos como uma coleção de instruções T-SQL. O SQL Server 2005, no entanto, foi projetado para fornecer integração com o [CLR (Common Language Runtime)](https://msdn.microsoft.com/netframework/aa497266.aspx), que é o tempo de execução usado por todos os assemblies do .net. Consequentemente, os procedimentos armazenados e UDFs em um banco de dados SQL Server 2005 podem ser criados usando código gerenciado. Ou seja, você pode criar um procedimento armazenado ou UDF como um método em uma classe C#. Isso permite que esses procedimentos armazenados e UDFs utilizem a funcionalidade no .NET Framework e de suas próprias classes personalizadas.

Neste tutorial, examinaremos como criar procedimentos armazenados gerenciados e funções definidas pelo usuário e como integrá-los ao nosso banco de dados Northwind. Vamos começar!

> [!NOTE]
> Os objetos de banco de dados gerenciado oferecem algumas vantagens em relação às suas contrapartes do SQL. A riqueza e a familiaridade da linguagem e a capacidade de reutilizar o código e a lógica existentes são as principais vantagens. Mas os objetos de banco de dados gerenciados provavelmente serão menos eficientes ao trabalhar com conjuntos de data que não envolvem muita lógica de procedimento. Para obter uma discussão mais completa sobre as vantagens de usar código gerenciado versus T-SQL, Confira as [vantagens de usar código gerenciado para criar objetos de banco de dados](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx).

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>Etapa 1: movendo o banco de dados Northwind para fora de`App_Data`

Todos os nossos tutoriais, até agora, usaram um arquivo de banco de dados Microsoft SQL Server 2005 Express Edition na `App_Data` pasta aplicativos Web. Colocar o banco de dados na `App_Data` distribuição simplificada e executar esses tutoriais como todos os arquivos estavam localizados em um diretório e não exigiu nenhuma etapa de configuração adicional para testar o tutorial.

No entanto, para este tutorial, vamos mover o banco de dados Northwind de `App_Data` e registrá-lo explicitamente com a instância de banco de dados SQL Server 2005 Express Edition. Embora possamos executar as etapas para este tutorial com o banco de dados na `App_Data` pasta, várias etapas são feitas de forma muito mais simples, registrando explicitamente o banco de dados com a instância de banco de dados SQL Server 2005 Express Edition.

O download para este tutorial tem os dois arquivos de banco de dados – `NORTHWND.MDF` e `NORTHWND_log.LDF` colocados em uma pasta chamada `DataFiles` . Se você estiver acompanhando sua própria implementação dos tutoriais, feche o Visual Studio e mova os `NORTHWND.MDF` arquivos e `NORTHWND_log.LDF` da pasta s do site `App_Data` para uma pasta fora do site. Depois que os arquivos de banco de dados tiverem sido movidos para outra pasta, precisamos registrar o banco de dados Northwind com a instância de banco de dados do SQL Server 2005 Express Edition. Isso pode ser feito em SQL Server Management Studio. Se você tiver uma edição não Express do SQL Server 2005 instalada em seu computador, provavelmente já terá Management Studio instalado. Se você só tiver SQL Server 2005 Express Edition em seu computador, Reserve um momento para baixar e instalar o [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796).

Inicialização do SQL Server Management Studio. Como mostra a Figura 1, Management Studio começa solicitando a qual servidor se conectar. Digite localhost\SQLExpress para o nome do servidor, escolha autenticação do Windows na lista suspensa autenticação e clique em conectar.

![Conectar-se à instância de banco de dados apropriada](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image1.png)

**Figura 1**: conectar-se à instância de banco de dados apropriada

Quando você estiver conectado, a janela pesquisador de objetos listará informações sobre a SQL Server 2005 Express Edition instância do banco de dados, incluindo seus bancos, informações de segurança, opções de gerenciamento e assim por diante.

Precisamos anexar o banco de dados Northwind na `DataFiles` pasta (ou onde você pode tê-lo movido) para a instância de banco de dados SQL Server 2005 Express Edition. Clique com o botão direito do mouse na pasta bancos de dados e escolha a opção anexar no menu de contexto. Isso abrirá a caixa de diálogo anexar bancos de dados. Clique no botão Adicionar, faça uma busca detalhada no `NORTHWND.MDF` arquivo apropriado e clique em OK. Neste ponto, sua tela deve ser semelhante à figura 2.

[![Conectar-se à instância de banco de dados apropriada](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image2.png)

**Figura 2**: conectar-se à instância de banco de dados apropriada ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image4.png))

> [!NOTE]
> Ao se conectar à instância de SQL Server 2005 Express Edition por meio do Management Studio a caixa de diálogo anexar bancos de dados não permite que você faça uma busca detalhada nos diretórios de perfil do usuário, como meus documentos. Portanto, certifique-se de colocar `NORTHWND.MDF` os `NORTHWND_log.LDF` arquivos e em um diretório de perfil que não seja de usuário.

Clique no botão OK para anexar o banco de dados. A caixa de diálogo anexar bancos de dados será fechada e o pesquisador de objetos agora deverá listar o banco de dados que acabou de ser anexado. É provável que o banco de dados Northwind tenha um nome como `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF` . Renomeie o banco de dados para Northwind clicando com o botão direito do mouse no banco de dados e escolhendo renomear.

![Renomear o banco de dados como Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image5.png)

**Figura 3**: renomear o banco de dados para Northwind

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>Etapa 2: criar uma nova solução e SQL Server projeto no Visual Studio

Para criar procedimentos armazenados gerenciados ou UDFs no SQL Server 2005, escreveremos o procedimento armazenado e a lógica UDF como código C# em uma classe. Depois que o código tiver sido gravado, precisaremos compilar essa classe em um assembly (um `.dll` arquivo), registrar o assembly com o SQL Server banco de dados e, em seguida, criar um procedimento armazenado ou um objeto UDF no banco de dados que aponta para o método correspondente no assembly. Essas etapas podem ser executadas manualmente. Podemos criar o código em qualquer editor de texto, compilá-lo na linha de comando usando o compilador C# ( [`csc.exe`](https://msdn.microsoft.com/library/ms379563(vs.80).aspx) ), registrá-lo com o banco de dados usando o [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) comando ou de Management Studio e adicionar o procedimento armazenado ou o objeto UDF por meio de meios semelhantes. Felizmente, as versões Professional e Team Systems do Visual Studio incluem um tipo de projeto SQL Server que automatiza essas tarefas. Neste tutorial, veremos como usar o tipo de projeto SQL Server para criar um procedimento armazenado gerenciado e UDF.

> [!NOTE]
> Se você estiver usando o Visual Web Developer ou a Standard Edition do Visual Studio, precisará usar a abordagem manual em vez disso. A etapa 13 fornece instruções detalhadas para executar essas etapas manualmente. Recomendo que você leia as etapas 2 a 12 antes de ler a etapa 13, já que essas etapas incluem importantes SQL Server instruções de configuração que devem ser aplicadas, independentemente de qual versão do Visual Studio você está usando.

Comece abrindo o Visual Studio. No menu arquivo, escolha novo projeto para exibir a caixa de diálogo novo projeto (consulte a Figura 4). Faça uma busca detalhada no tipo de projeto de banco de dados e, em seguida, nos modelos listados à direita, escolha criar um novo projeto de SQL Server. Optei por nomear este projeto `ManagedDatabaseConstructs` e o coloquei em uma solução chamada `Tutorial75` .

[![Criar um novo projeto de SQL Server](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image6.png)

**Figura 4**: criar um novo projeto de SQL Server ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image8.png))

Clique no botão OK na caixa de diálogo novo projeto para criar a solução e SQL Server projeto.

Um projeto SQL Server está vinculado a um banco de dados específico. Consequentemente, depois de criar o novo projeto SQL Server, imediatamente solicitamos que especifiquemos essas informações. A Figura 5 mostra a caixa de diálogo nova referência de banco de dados que foi preenchida para apontar para o banco de dados Northwind que registramos na instância de banco de dados SQL Server 2005 Express Edition de volta na etapa 1.

![Associar o projeto de SQL Server ao banco de dados Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image9.png)

**Figura 5**: associar o projeto de SQL Server ao banco de dados Northwind

Para depurar os procedimentos armazenados gerenciados e UDFs que criaremos dentro desse projeto, precisamos habilitar o suporte à depuração SQL/CLR para a conexão. Sempre que associar um projeto SQL Server com um novo banco de dados (como fizemos na Figura 5), o Visual Studio perguntará se desejamos habilitar a depuração SQL/CLR na conexão (veja a Figura 6). Clique em Sim.

![Habilitar depuração SQL/CLR](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image10.png)

**Figura 6**: habilitar a depuração SQL/CLR

Neste ponto, o novo projeto de SQL Server foi adicionado à solução. Ele contém uma pasta chamada `Test Scripts` com um arquivo chamado `Test.sql` , que é usado para depurar os objetos de banco de dados gerenciados criados no projeto. Veremos a depuração na etapa 12.

Agora, podemos adicionar novos procedimentos armazenados gerenciados e UDFs a esse projeto, mas antes de deixarmos que os s incluam primeiro nosso aplicativo Web existente na solução. No menu arquivo, selecione a opção Adicionar e escolha site existente. Navegue até a pasta do site apropriada e clique em OK. Como mostra a Figura 7, isso atualizará a solução para incluir dois projetos: o site e o `ManagedDatabaseConstructs` projeto SQL Server.

![O Gerenciador de Soluções agora inclui dois projetos](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image11.png)

**Figura 7**: a Gerenciador de soluções agora inclui dois projetos

O `NORTHWNDConnectionString` valor `Web.config` atualmente faz referência ao `NORTHWND.MDF` arquivo na `App_Data` pasta. Como removemos esse banco de dados de `App_Data` e o registramos explicitamente na instância do banco de dados SQL Server 2005 Express Edition, precisamos atualizar o valor de forma correspondente `NORTHWNDConnectionString` . Abra o `Web.config` arquivo no site e altere o `NORTHWNDConnectionString` valor para que a cadeia de conexão Leia: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True` . Após essa alteração, a `<connectionStrings>` seção em `Web.config` deve ser semelhante ao seguinte:

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample1.xml)]

> [!NOTE]
> Conforme discutido no [tutorial anterior](debugging-stored-procedures-cs.md), ao depurar um objeto de SQL Server de um aplicativo cliente, como um site do ASP.net, precisamos desabilitar o pool de conexões. A cadeia de conexão mostrada acima desabilita o pool de conexões ( `Pooling=false` ). Se você não planeja depurar os procedimentos armazenados gerenciados e UDFs do site do ASP.NET, habilite o pool de conexões.

## <a name="step-3-creating-a-managed-stored-procedure"></a>Etapa 3: Criando um procedimento armazenado gerenciado

Para adicionar um procedimento armazenado gerenciado ao banco de dados Northwind, primeiro precisamos criar o procedimento armazenado como um método no projeto SQL Server. No Gerenciador de Soluções, clique com o botão direito do mouse no `ManagedDatabaseConstructs` nome do projeto e escolha Adicionar um novo item. Isso exibirá a caixa de diálogo Adicionar novo item, que lista os tipos de objetos de banco de dados gerenciados que podem ser adicionados ao projeto. Como mostra a Figura 8, isso inclui procedimentos armazenados e funções definidas pelo usuário, entre outros.

Deixe que os s comecem adicionando um procedimento armazenado que simplesmente retorna todos os produtos que foram descontinuados. Nomeie o novo arquivo de procedimento armazenado `GetDiscontinuedProducts.cs` .

[![Adicione um novo procedimento armazenado chamado GetDiscontinuedProducts.cs](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image12.png)

**Figura 8**: adicionar um novo procedimento armazenado chamado `GetDiscontinuedProducts.cs` ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image14.png))

Isso criará um novo arquivo de classe C# com o seguinte conteúdo:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample2.cs)]

Observe que o procedimento armazenado é implementado como um `static` método dentro de um `partial` arquivo de classe chamado `StoredProcedures` . Além disso, o `GetDiscontinuedProducts` método é decorado com o `SqlProcedure attribute` , que marca o método como um procedimento armazenado.

O código a seguir cria um `SqlCommand` objeto e define seu `CommandText` como uma `SELECT` consulta que retorna todas as colunas da `Products` tabela para produtos cujo `Discontinued` campo é igual a 1. Em seguida, ele executa o comando e envia os resultados de volta para o aplicativo cliente. Adicione este código ao `GetDiscontinuedProducts` método.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample3.cs)]

Todos os objetos de banco de dados gerenciados têm acesso a um [ `SqlContext` objeto](https://msdn.microsoft.com/library/ms131108.aspx) que representa o contexto do chamador. O `SqlContext` fornece acesso a um [ `SqlPipe` objeto](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx) por meio de sua [ `Pipe` Propriedade](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx). Esse `SqlPipe` objeto é usado para ferry informações entre o banco de dados SQL Server e o aplicativo de chamada. Como o nome sugere, o [ `ExecuteAndSend` método](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) executa um `SqlCommand` objeto passado e envia os resultados de volta para o aplicativo cliente.

> [!NOTE]
> Os objetos de banco de dados gerenciados são mais adequados para procedimentos armazenados e UDFs que usam lógica de procedimento em vez da lógica baseada em conjunto. A lógica de procedimento envolve trabalhar com conjuntos de dados linha por linha ou trabalhar com dados escalares. O `GetDiscontinuedProducts` método que acabamos de criar, no entanto, não envolve nenhuma lógica de procedimento. Portanto, o ideal seria ser implementado como um procedimento armazenado T-SQL. Ele é implementado como um procedimento armazenado gerenciado para demonstrar as etapas necessárias para criar e implantar procedimentos armazenados gerenciados.

## <a name="step-4-deploying-the-managed-stored-procedure"></a>Etapa 4: Implantando o procedimento armazenado gerenciado

Com esse código concluído, estamos prontos para implantá-lo no banco de dados Northwind. Implantar um projeto de SQL Server compila o código em um assembly, registra o assembly com o banco de dados e cria os objetos correspondentes no banco de dados, vinculando-os aos métodos apropriados no assembly. O conjunto exato de tarefas executadas pela opção implantar é escrito mais precisamente na etapa 13. Clique com o botão direito do mouse no `ManagedDatabaseConstructs` nome do projeto na Gerenciador de soluções e escolha a opção implantar. No entanto, a implantação falha com o seguinte erro: sintaxe incorreta próxima a ' EXTERNAL '. Talvez seja necessário definir o nível de compatibilidade do banco de dados atual em um valor mais alto para habilitar este recurso. Consulte a ajuda para o procedimento armazenado `sp_dbcmptlevel` .

Essa mensagem de erro ocorre ao tentar registrar o assembly com o banco de dados Northwind. Para registrar um assembly com um banco de dados SQL Server 2005, o nível de compatibilidade do banco de dados deve ser definido como 90. Por padrão, novos bancos de dados SQL Server 2005 têm um nível de compatibilidade de 90. No entanto, os bancos de dados criados usando Microsoft SQL Server 2000 têm um nível de compatibilidade padrão de 80. Como o banco de dados Northwind era inicialmente um banco de dados Microsoft SQL Server 2000, seu nível de compatibilidade está atualmente definido como 80 e, portanto, precisa ser aumentado para 90 a fim de registrar objetos de banco de dados gerenciados.

Para atualizar o nível de compatibilidade do banco de dados, abra uma nova janela de consulta no Management Studio e digite:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample4.sql)]

Clique no ícone executar na barra de ferramentas para executar a consulta acima.

[![Atualizar o nível de compatibilidade do banco de dados Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image15.png)

**Figura 9**: atualizar o nível de compatibilidade do banco de dados Northwind ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image17.png))

Depois de atualizar o nível de compatibilidade, reimplante o projeto SQL Server. Desta vez, a implantação deve ser concluída sem erros.

Volte para SQL Server Management Studio, clique com o botão direito do mouse no banco de dados Northwind no Pesquisador de objetos e escolha Atualizar. Em seguida, faça uma busca detalhada na pasta de programação e expanda a pasta assemblies. Como mostra a Figura 10, o banco de dados Northwind agora inclui o assembly gerado pelo `ManagedDatabaseConstructs` projeto.

![O assembly ManagedDatabaseConstructs agora está registrado com o banco de dados Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image18.png)

**Figura 10**: o `ManagedDatabaseConstructs` assembly agora está registrado com o banco de dados Northwind

Expanda também a pasta procedimentos armazenados. Lá, você verá um procedimento armazenado chamado `GetDiscontinuedProducts` . Esse procedimento armazenado foi criado pelo processo de implantação e aponta para o `GetDiscontinuedProducts` método no `ManagedDatabaseConstructs` assembly. Quando o `GetDiscontinuedProducts` procedimento armazenado é executado, ele, por sua vez, executa o `GetDiscontinuedProducts` método. Como esse é um procedimento armazenado gerenciado, ele não pode ser editado por meio de Management Studio (portanto, o ícone de bloqueio ao lado do nome do procedimento armazenado).

![O procedimento armazenado GetDiscontinuedProducts está listado na pasta procedimentos armazenados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image19.png)

**Figura 11**: o `GetDiscontinuedProducts` procedimento armazenado está listado na pasta procedimentos armazenados

Ainda há mais um obstáculo que precisamos superar antes de chamarmos o procedimento armazenado gerenciado: o banco de dados está configurado para evitar a execução de código gerenciado. Verifique isso abrindo uma nova janela de consulta e executando o `GetDiscontinuedProducts` procedimento armazenado. Você receberá a seguinte mensagem de erro: a execução do código do usuário no .NET Framework está desabilitada. Habilite a opção de configuração ' CLR Enabled.

Para examinar as informações de configuração de s do banco de dados Northwind, insira e execute o comando `exec sp_configure` na janela de consulta. Isso mostra que a configuração CLR habilitado está definida atualmente como 0.

[![A configuração CLR Enabled está definida atualmente como 0](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image20.png)

**Figura 12**: a configuração CLR Enabled está definida atualmente como 0 ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image22.png))

Observe que cada definição de configuração na Figura 12 tem quatro valores listados com ela: os valores mínimo e máximo e os valores de configuração e de execução. Para atualizar o valor de configuração para a configuração CLR Enabled, execute o seguinte comando:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample5.sql)]

Se você executar novamente o, `exec sp_configure` verá que a instrução acima atualizou o valor de configuração de s de configurações do CLR habilitado para 1, mas que o valor de execução ainda está definido como 0. Para que essa alteração de configuração entre em vigor, precisamos executar o [ `RECONFIGURE` comando](https://msdn.microsoft.com/library/ms176069.aspx), que definirá o valor de execução para o valor de configuração atual. Basta inserir `RECONFIGURE` na janela de consulta e clicar no ícone executar na barra de ferramentas. Se você executar `exec sp_configure` agora, você deverá ver um valor de 1 para a configuração do CLR habilitado config e valores de execução.

Com a configuração habilitada para CLR concluída, estamos prontos para executar o `GetDiscontinuedProducts` procedimento armazenado gerenciado. Na janela de consulta, insira e execute o comando `exec` `GetDiscontinuedProducts` . Invocar o procedimento armazenado faz com que o código gerenciado correspondente no `GetDiscontinuedProducts` método seja executado. Esse código emite uma `SELECT` consulta para retornar todos os produtos que foram descontinuados e retorna esses dados para o aplicativo de chamada, que é SQL Server Management Studio nessa instância. Management Studio recebe esses resultados e os exibe na janela resultados.

[![O procedimento armazenado GetDiscontinuedProducts retorna todos os produtos descontinuados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image23.png)

**Figura 13**: o `GetDiscontinuedProducts` procedimento armazenado retorna todos os produtos descontinuados ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image25.png))

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>Etapa 5: Criando procedimentos armazenados gerenciados que aceitam parâmetros de entrada

Muitas das consultas e procedimentos armazenados que criamos em todos esses tutoriais usaram *parâmetros*. Por exemplo, no tutorial [criando novos procedimentos armazenados para o conjunto de dados do tipo s TableAdapters](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) , criamos um procedimento armazenado chamado `GetProductsByCategoryID` que aceitava um parâmetro de entrada chamado `@CategoryID` . Em seguida, o procedimento armazenado retornava todos os produtos cujo `CategoryID` campo correspondeu ao valor do `@CategoryID` parâmetro fornecido.

Para criar um procedimento armazenado gerenciado que aceita parâmetros de entrada, basta especificar esses parâmetros na definição do método. Para ilustrar isso, vamos adicionar outro procedimento armazenado gerenciado ao `ManagedDatabaseConstructs` projeto chamado `GetProductsWithPriceLessThan` . Esse procedimento armazenado gerenciado aceitará um parâmetro de entrada especificando um preço e retornará todos os produtos cujo `UnitPrice` campo é menor que o valor s do parâmetro.

Para adicionar um novo procedimento armazenado ao projeto, clique com o botão direito do mouse no `ManagedDatabaseConstructs` nome do projeto e escolha Adicionar um novo procedimento armazenado. Atribua um nome ao arquivo `GetProductsWithPriceLessThan.cs`. Como vimos na etapa 3, isso criará um novo arquivo de classe C# com um método chamado `GetProductsWithPriceLessThan` colocado dentro da `partial` classe `StoredProcedures` .

Atualize a `GetProductsWithPriceLessThan` definição do método de forma que aceite um [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) parâmetro de entrada chamado `price` e escreva o código a ser executado e retorne os resultados da consulta:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample6.cs)]

A `GetProductsWithPriceLessThan` definição e o código do método se assemelham à definição e ao código do `GetDiscontinuedProducts` método criado na etapa 3. As únicas diferenças são que o `GetProductsWithPriceLessThan` método aceita como parâmetro de entrada ( `price` ), a `SqlCommand` consulta s inclui um parâmetro ( `@MaxPrice` ), e um parâmetro é adicionado à `SqlCommand` coleção s `Parameters` e recebe o valor da `price` variável.

Depois de adicionar esse código, reimplante o projeto SQL Server. Em seguida, retorne para SQL Server Management Studio e atualize a pasta procedimentos armazenados. Você deverá ver uma nova entrada, `GetProductsWithPriceLessThan` . Em uma janela de consulta, insira e execute o comando `exec GetProductsWithPriceLessThan 25` , que listará todos os produtos com menos de $25, como mostra a Figura 14.

[![Os produtos em $25 são exibidos](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image26.png)

**Figura 14**: produtos em $25 são exibidos ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image28.png))

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>Etapa 6: chamando o procedimento armazenado gerenciado da camada de acesso a dados

Neste ponto, adicionamos os `GetDiscontinuedProducts` `GetProductsWithPriceLessThan` procedimentos armazenados gerenciados e para o `ManagedDatabaseConstructs` projeto e os registramos com o banco de dados Northwind SQL Server. Também invocamos esses procedimentos armazenados gerenciados de SQL Server Management Studio (consulte a Figura 13 e 14). No entanto, para que nosso aplicativo ASP.NET use esses procedimentos armazenados gerenciados, precisamos adicioná-los às camadas de acesso a dados e lógica de negócios na arquitetura. Nesta etapa, adicionaremos dois novos métodos ao `ProductsTableAdapter` no `NorthwindWithSprocs` dataset tipado, que foi inicialmente criado no tutorial [criando novos procedimentos armazenados para o DataSets s tipados](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) . Na etapa 7, adicionaremos métodos correspondentes à BLL.

Abra o `NorthwindWithSprocs` dataset tipado no Visual Studio e comece adicionando um novo método ao `ProductsTableAdapter` nome `GetDiscontinuedProducts` . Para adicionar um novo método a um TableAdapter, clique com o botão direito do mouse no nome do TableAdapter s no designer e escolha a opção Adicionar consulta no menu de contexto.

> [!NOTE]
> Como mudamos o banco de dados Northwind da `App_Data` pasta para a instância do banco de dados SQL Server 2005 Express Edition, é imperativo que a cadeia de conexão correspondente em Web.config ser atualizada para refletir essa alteração. Na etapa 2, discutimos a atualização do `NORTHWNDConnectionString` valor em `Web.config` . Se você esqueceu de fazer essa atualização, verá a mensagem de erro falha ao adicionar consulta. Não é possível localizar a conexão `NORTHWNDConnectionString` do objeto `Web.config` em uma caixa de diálogo ao tentar adicionar um novo método ao TableAdapter. Para resolver esse erro, clique em OK e, em seguida, vá para `Web.config` e atualize o `NORTHWNDConnectionString` valor conforme discutido na etapa 2. Em seguida, tente adicionar novamente o método ao TableAdapter. Desta vez, ele deve funcionar sem erros.

A adição de um novo método inicia o assistente de configuração de consulta do TableAdapter, que usamos muitas vezes nos tutoriais anteriores. A primeira etapa nos pede para especificar como o TableAdapter deve acessar o banco de dados: por meio de uma instrução SQL ad hoc ou por meio de um procedimento armazenado novo ou existente. Como já criamos e registramos o `GetDiscontinuedProducts` procedimento armazenado gerenciado com o banco de dados, escolha a opção usar procedimento armazenado existente e pressione Avançar.

[![Escolha a opção usar procedimento armazenado existente](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image29.png)

**Figura 15**: escolha a opção usar procedimento armazenado existente ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image31.png))

A próxima tela nos solicitará o procedimento armazenado que o método invocará. Escolha o `GetDiscontinuedProducts` procedimento armazenado gerenciado na lista suspensa e clique em Avançar.

[![Selecione o procedimento armazenado gerenciado GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image32.png)

**Figura 16**: selecione o `GetDiscontinuedProducts` procedimento armazenado gerenciado ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image34.png))

Em seguida, solicitamos que especifiquemos se o procedimento armazenado retorna linhas, um único valor ou nada. Como `GetDiscontinuedProducts` o retorna o conjunto de linhas de produtos descontinuadas, escolha a primeira opção (dados tabulares) e clique em Avançar.

[![Selecione a opção dados tabulares](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image35.png)

**Figura 17**: selecione a opção dados tabulares ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image37.png))

A tela final do assistente nos permite especificar os padrões de acesso a dados usados e os nomes dos métodos resultantes. Deixe ambas as caixas de seleção marcadas e nomeie os métodos `FillByDiscontinued` e `GetDiscontinuedProducts` . Clique em Concluir para concluir o assistente.

[![Nomeie os métodos FillByDiscontinued e GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image38.png)

**Figura 18**: nomear os métodos `FillByDiscontinued` e `GetDiscontinuedProducts` ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image40.png))

Repita essas etapas para criar métodos chamados `FillByPriceLessThan` e `GetProductsWithPriceLessThan` no `ProductsTableAdapter` para o `GetProductsWithPriceLessThan` procedimento armazenado gerenciado.

A Figura 19 mostra uma captura de tela do designer de DataSet depois de adicionar os métodos ao `ProductsTableAdapter` para os `GetDiscontinuedProducts` `GetProductsWithPriceLessThan` procedimentos armazenados gerenciados e.

[![O ProductsTableAdapter inclui os novos métodos adicionados nesta etapa](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image41.png)

**Figura 19**: a `ProductsTableAdapter` inclui os novos métodos adicionados nesta etapa ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image43.png))

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>Etapa 7: adicionando métodos correspondentes à camada de lógica de negócios

Agora que atualizamos a camada de acesso a dados para incluir métodos para chamar os procedimentos armazenados gerenciados adicionados nas etapas 4 e 5, precisamos adicionar métodos correspondentes à camada de lógica de negócios. Adicione os dois métodos a seguir à `ProductsBLLWithSprocs` classe:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample7.cs)]

Ambos os métodos simplesmente chamam o método DAL correspondente e retornam a `ProductsDataTable` instância. A `DataObjectMethodAttribute` marcação acima de cada método faz com que esses métodos sejam incluídos na lista suspensa na guia selecionar do assistente de configuração de fonte de dados ObjectDataSource s.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>Etapa 8: invocar os procedimentos armazenados gerenciados da camada de apresentação

Com a lógica de negócios e as camadas de acesso a dados aumentadas para incluir suporte para chamar os `GetDiscontinuedProducts` `GetProductsWithPriceLessThan` procedimentos armazenados gerenciados e, agora podemos exibir esses resultados de procedimentos armazenados por meio de uma página ASP.net.

Abra a `ManagedFunctionsAndSprocs.aspx` página na `AdvancedDAL` pasta e, na caixa de ferramentas, arraste um GridView para o designer. Defina a Propriedade GridView s `ID` como `DiscontinuedProducts` e, de sua marca inteligente, associe-a a uma nova ObjectDataSource chamada `DiscontinuedProductsDataSource` . Configure o ObjectDataSource para efetuar pull de seus dados do `ProductsBLLWithSprocs` método da classe s `GetDiscontinuedProducts` .

[![Configurar o ObjectDataSource para usar a classe ProductsBLLWithSprocs](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image44.png)

**Figura 20**: configurar o ObjectDataSource para usar a `ProductsBLLWithSprocs` classe ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image46.png))

[![Escolha o método GetDiscontinuedProducts na lista suspensa na guia selecionar](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image47.png)

**Figura 21**: escolha o `GetDiscontinuedProducts` método na lista suspensa na guia selecionar ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image49.png))

Como essa grade será usada para exibir apenas as informações do produto, defina as listas suspensas nas guias atualizar, inserir e excluir como (nenhum) e clique em concluir.

Após a conclusão do assistente, o Visual Studio adicionará automaticamente um BoundField ou CheckBoxField para cada campo de dados no `ProductsDataTable` . Reserve um tempo para remover todos esses campos, exceto para `ProductName` e `Discontinued` , no ponto em que a marcação declarativa de GridView e ObjectDataSource s deve ser semelhante ao seguinte:

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample8.aspx)]

Reserve um tempo para exibir esta página por meio de um navegador. Quando a página é visitada, o ObjectDataSource chama o `ProductsBLLWithSprocs` método Class s `GetDiscontinuedProducts` . Como vimos na etapa 7, esse método chama o método de classe s da DAL `ProductsDataTable` `GetDiscontinuedProducts` , que invoca o `GetDiscontinuedProducts` procedimento armazenado. Esse procedimento armazenado é um procedimento armazenado gerenciado e executa o código que criamos na etapa 3, retornando os produtos descontinuados.

Os resultados retornados pelo procedimento armazenado gerenciado são empacotados em uma `ProductsDataTable` pela Dal e, em seguida, retornados para a BLL, que, em seguida, retorna-os à camada de apresentação onde estão associados ao GridView e exibidos. Conforme esperado, a grade lista os produtos que foram descontinuados.

[![Os produtos descontinuados estão listados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image50.png)

**Figura 22**: os produtos descontinuados são listados ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image52.png))

Para uma prática adicional, adicione uma caixa de texto e outro GridView à página. Esse GridView exibe os produtos menores do que o valor inserido na caixa de texto chamando o `ProductsBLLWithSprocs` método Class s `GetProductsWithPriceLessThan` .

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>Etapa 9: Criando e chamando UDFs T-SQL

As funções definidas pelo usuário, ou UDFs, são objetos de banco de dados que imitam de forma semelhante a semântica das funções em linguagens de programação. Como uma função em C#, as UDFs podem incluir um número variável de parâmetros de entrada e retornar um valor de um tipo específico. Um UDF pode retornar dados escalares – uma cadeia de caracteres, um número inteiro e dados de tabela e assim por diante. Vamos dar uma olhada rápida em ambos os tipos de UDFs, começando com um UDF que retorna um tipo de dados escalar.

O UDF a seguir calcula o valor estimado do inventário para um produto específico. Ele faz isso levando três parâmetros de entrada: os `UnitPrice` valores, `UnitsInStock` e `Discontinued` para um produto específico e retorna um valor do tipo `money` . Ele computa o valor estimado do inventário multiplicando o `UnitPrice` pelo `UnitsInStock` . Para itens descontinuados, esse valor é dividido em metade.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample9.sql)]

Depois que esse UDF tiver sido adicionado ao banco de dados, ele poderá ser encontrado por meio de Management Studio expandindo a pasta de programação, as funções e as funções de valor escalar. Ele pode ser usado em uma `SELECT` consulta como esta:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample10.sql)]

Adicionei o `udf_ComputeInventoryValue` UDF ao banco de dados Northwind; A Figura 23 mostra a saída da `SELECT` consulta acima quando exibida por meio de Management Studio. Observe também que o UDF está listado na pasta funções Scalar-Value no Pesquisador de objetos.

[![Os valores de inventário de cada produto são listados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image53.png)

**Figura 23**: cada produto s valores de inventário é listado ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image55.png))

As UDFs também podem retornar dados tabulares. Por exemplo, podemos criar um UDF que retorne os produtos que pertencem a uma determinada categoria:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample11.sql)]

O `udf_GetProductsByCategoryID` UDF aceita um `@CategoryID` parâmetro de entrada e retorna os resultados da `SELECT` consulta especificada. Depois de criado, esse UDF pode ser referenciado na `FROM` cláusula (ou `JOIN` ) de uma `SELECT` consulta. O exemplo a seguir retorna os `ProductID` `ProductName` valores, e `CategoryID` para cada uma das bebidas.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample12.sql)]

Adicionei o `udf_GetProductsByCategoryID` UDF ao banco de dados Northwind; A figura 24 mostra a saída da `SELECT` consulta acima quando exibida por meio de Management Studio. UDFs que retornam dados tabulares podem ser encontrados na pasta de funções Table-Value do pesquisador de objetos.

[![ProductID, ProductName e CategoryID são listados para cada bebida](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image56.png)

**Figura 24**: as `ProductID` , `ProductName` e `CategoryID` são listadas para cada bebida ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image58.png))

> [!NOTE]
> Para obter mais informações sobre como criar e usar UDFs, confira [introdução às funções definidas pelo usuário](http://www.sqlteam.com/item.asp?ItemID=1955). Além disso, Confira as [vantagens e desvantagens das funções definidas pelo usuário](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1).

## <a name="step-10-creating-a-managed-udf"></a>Etapa 10: Criando um UDF gerenciado

Os `udf_ComputeInventoryValue` `udf_GetProductsByCategoryID` UDFs criados nos exemplos acima são objetos de banco de dados T-SQL. O SQL Server 2005 também dá suporte a UDFs gerenciadas, que podem ser adicionadas ao `ManagedDatabaseConstructs` projeto, assim como os procedimentos armazenados gerenciados das etapas 3 e 5. Para esta etapa, vamos implementar o `udf_ComputeInventoryValue` UDF no código gerenciado.

Para adicionar um UDF gerenciado ao `ManagedDatabaseConstructs` projeto, clique com o botão direito do mouse no nome do projeto em Gerenciador de soluções e escolha Adicionar um novo item. Selecione o modelo definido pelo usuário na caixa de diálogo Adicionar novo item e nomeie o novo arquivo UDF `udf_ComputeInventoryValue_Managed.cs` .

[![Adicionar um novo UDF gerenciado ao projeto ManagedDatabaseConstructs](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image59.png)

**Figura 25**: adicionar um novo UDF gerenciado ao `ManagedDatabaseConstructs` projeto ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image61.png))

O modelo de função definido pelo usuário cria uma `partial` classe chamada `UserDefinedFunctions` com um método cujo nome é igual ao nome do arquivo de classe ( `udf_ComputeInventoryValue_Managed` , nesta instância). Esse método é decorado usando o [ `SqlFunction` atributo](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx), que sinaliza o método como um UDF gerenciado.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample13.cs)]

`udf_ComputeInventoryValue`Atualmente, o método retorna um [ `SqlString` objeto](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) e não aceita nenhum parâmetro de entrada. Precisamos atualizar a definição do método para que ela aceite três parâmetros de entrada- `UnitPrice` , `UnitsInStock` , e `Discontinued` -e retorne um `SqlMoney` objeto. A lógica para calcular o valor de inventário é idêntica à do UDF do T-SQL `udf_ComputeInventoryValue` .

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample14.cs)]

Observe que os parâmetros de entrada do método UDF são de seus tipos SQL correspondentes: `SqlMoney` para o `UnitPrice` campo, [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) para `UnitsInStock` e [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) para `Discontinued` . Esses tipos de dados refletem os tipos definidos na `Products` tabela: a `UnitPrice` coluna é do tipo `money` , a `UnitsInStock` coluna do tipo `smallint` e a `Discontinued` coluna do tipo `bit` .

O código começa criando uma `SqlMoney` instância denominada `inventoryValue` que é atribuído um valor de 0. A `Products` tabela permite valores de banco de dados `NULL` nas `UnitsInPrice` `UnitsInStock` colunas e. Portanto, precisamos primeiro verificar se esses valores contêm `NULL` s, o que fazemos por meio da `SqlMoney` [ `IsNull` Propriedade](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)Object s. Se ambos `UnitPrice` e `UnitsInStock` não tiverem `NULL` valores, computaremos o `inventoryValue` para ser o produto dos dois. Em seguida, se `Discontinued` for true, o valor será dividido em metade.

> [!NOTE]
> O `SqlMoney` objeto só permite que duas `SqlMoney` instâncias sejam multiplicadas juntas. Ele não permite que uma `SqlMoney` instância seja multiplicada por um número de ponto flutuante literal. Portanto, para metade, `inventoryValue` multiplique-o por uma nova `SqlMoney` instância com o valor 0,5.

## <a name="step-11-deploying-the-managed-udf"></a>Etapa 11: Implantando o UDF gerenciado

Agora que o UDF gerenciado foi criado, estamos prontos para implantá-lo no banco de dados Northwind. Como vimos na etapa 4, os objetos gerenciados em um projeto SQL Server são implantados clicando com o botão direito do mouse no nome do projeto na Gerenciador de Soluções e escolhendo a opção implantar no menu de contexto.

Depois de implantar o projeto, retorne ao SQL Server Management Studio e atualize a pasta funções com valor escalar. Agora você deve ver duas entradas:

- `dbo.udf_ComputeInventoryValue` -o UDF do T-SQL criado na etapa 9 e
- `dbo.udf ComputeInventoryValue_Managed` -o UDF gerenciado criado na etapa 10 que acabou de ser implantado.

Para testar esse UDF gerenciado, execute a consulta a seguir no Management Studio:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample15.sql)]

Esse comando usa o `udf ComputeInventoryValue_Managed` UDF gerenciado em vez do UDF do T-SQL `udf_ComputeInventoryValue` , mas a saída é a mesma. Consulte novamente a Figura 23 para ver uma captura de tela da saída de UDF.

## <a name="step-12-debugging-the-managed-database-objects"></a>Etapa 12: Depurando os objetos de banco de dados gerenciados

No tutorial [depuração de procedimentos armazenados](debugging-stored-procedures-cs.md) , discutimos as três opções de depuração de SQL Server por meio do Visual Studio: depuração de banco de dados direta, depuração de aplicativo e depuração de um projeto SQL Server. Os objetos de banco de dados gerenciados não podem ser depurados por meio da depuração direta do banco de dados, mas podem ser depurados de um aplicativo cliente e diretamente do projeto SQL Server. No entanto, para que a depuração funcione, o banco de dados SQL Server 2005 deve permitir a depuração SQL/CLR. Lembre-se de que, quando criamos o projeto, o `ManagedDatabaseConstructs` Visual Studio nos perguntou se queríamos habilitar a depuração SQL/CLR (consulte a Figura 6 na etapa 2). Essa configuração pode ser modificada clicando com o botão direito do mouse no banco de dados na janela Gerenciador de Servidores.

![Verifique se o banco de dados permite depuração SQL/CLR](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image62.png)

**Figura 26**: verificar se o banco de dados permite a depuração SQL/CLR

Imagine que queríamos depurar o `GetProductsWithPriceLessThan` procedimento armazenado gerenciado. Começamos definindo um ponto de interrupção dentro do código do `GetProductsWithPriceLessThan` método.

[![Definir um ponto de interrupção no método GetProductsWithPriceLessThan](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image63.png)

**Figura 27**: definir um ponto de interrupção no `GetProductsWithPriceLessThan` método ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image65.png))

Vamos primeiro examinar a depuração dos objetos de banco de dados gerenciados do projeto SQL Server. Como nossa solução inclui dois projetos – o `ManagedDatabaseConstructs` projeto SQL Server junto com nosso site – para depurar do projeto SQL Server, precisamos instruir o Visual Studio a iniciar o projeto de `ManagedDatabaseConstructs` SQL Server quando iniciarmos a depuração. Clique com o botão direito do mouse `ManagedDatabaseConstructs` no projeto no Gerenciador de soluções e escolha a opção Definir como projeto de inicialização no menu de contexto.

Quando o `ManagedDatabaseConstructs` projeto é iniciado do depurador, ele executa as instruções SQL no `Test.sql` arquivo, que está localizado na `Test Scripts` pasta. Por exemplo, para testar o `GetProductsWithPriceLessThan` procedimento armazenado gerenciado, substitua o `Test.sql` conteúdo do arquivo existente pela instrução a seguir, que invoca o `GetProductsWithPriceLessThan` procedimento armazenado gerenciado passando o `@CategoryID` valor de 14,95:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample16.sql)]

Depois de inserir o script acima no `Test.sql` , inicie a depuração acessando o menu Depurar e escolhendo iniciar depuração ou pressionando F5 ou o ícone de execução verde na barra de ferramentas. Isso criará os projetos dentro da solução, implantará os objetos de banco de dados gerenciados no banco de dados Northwind e, em seguida, executará o `Test.sql` script. Nesse momento, o ponto de interrupção será atingido e poderemos percorrer o `GetProductsWithPriceLessThan` método, examinar os valores dos parâmetros de entrada e assim por diante.

[![O ponto de interrupção no método GetProductsWithPriceLessThan foi atingido](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image66.png)

**Figura 28**: o ponto de interrupção no `GetProductsWithPriceLessThan` método foi atingido ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image68.png))

Para que um objeto de banco de dados SQL seja depurado por meio de um aplicativo cliente, é imperativo que o banco de dados seja configurado para dar suporte à depuração de aplicativos. Clique com o botão direito do mouse no banco de dados em Gerenciador de Servidores e verifique se a opção de depuração do aplicativo está marcada. Além disso, precisamos configurar o aplicativo ASP.NET para integrar com o depurador do SQL e desabilitar o pool de conexões. Essas etapas foram discutidas detalhadamente na etapa 2 do tutorial [depuração de procedimentos armazenados](debugging-stored-procedures-cs.md) .

Depois de configurar o aplicativo e o banco de dados do ASP.NET, defina o site do ASP.NET como o projeto de inicialização e inicie a depuração. Se você visitar uma página que chama um dos objetos gerenciados que tem um ponto de interrupção, o aplicativo será interrompido e o controle será ativado para o depurador, no qual você pode percorrer o código, conforme mostrado na Figura 28.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>Etapa 13: Compilando e Implantando manualmente objetos de banco de dados gerenciados

SQL Server projetos facilitam a criação, a compilação e a implantação de objetos de banco de dados gerenciados. Infelizmente, os projetos SQL Server só estão disponíveis nas edições Professional e Team Systems do Visual Studio. Se você estiver usando o Visual Web Developer ou a Standard Edition do Visual Studio e quiser usar objetos de banco de dados gerenciado, será necessário criá-los e implantá-los manualmente. Isso envolve quatro etapas:

1. Criar um arquivo que contém o código-fonte do objeto de banco de dados gerenciado,
2. Compilar o objeto em um assembly,
3. Registre o assembly com o banco de dados SQL Server 2005 e
4. Crie um objeto de banco de dados no SQL Server que aponte para o método apropriado no assembly.

Para ilustrar essas tarefas, vamos criar um novo procedimento armazenado gerenciado que retorne os produtos cujo `UnitPrice` valor seja maior do que o especificado. Crie um novo arquivo no seu computador chamado `GetProductsWithPriceGreaterThan.cs` e insira o código a seguir no arquivo (você pode usar o Visual Studio, o bloco de notas ou qualquer editor de texto para fazer isso):

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample17.cs)]

Esse código é praticamente idêntico ao do `GetProductsWithPriceLessThan` método criado na etapa 5. As únicas diferenças são os nomes de método, a `WHERE` cláusula e o nome do parâmetro usado na consulta. De volta ao `GetProductsWithPriceLessThan` método, a `WHERE` cláusula Read: `WHERE UnitPrice < @MaxPrice` . Aqui, em `GetProductsWithPriceGreaterThan` , usamos: `WHERE UnitPrice > @MinPrice` .

Agora, precisamos compilar essa classe em um assembly. Na linha de comando, navegue até o diretório em que você salvou o `GetProductsWithPriceGreaterThan.cs` arquivo e use o compilador C# ( `csc.exe` ) para compilar o arquivo de classe em um assembly:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample18.cmd)]

Se a pasta que contém o `csc.exe` não estiver nos s do sistema `PATH` , você precisará fazer referência completa a seu caminho, da `%WINDOWS%\Microsoft.NET\Framework\version\` seguinte forma:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample19.cmd)]

[![Compilar GetProductsWithPriceGreaterThan.cs em um assembly](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image69.png)

**Figura 29**: Compilar `GetProductsWithPriceGreaterThan.cs` em um assembly ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image71.png))

O `/t` sinalizador especifica que o arquivo de classe C# deve ser compilado em uma dll (em vez de um executável). O `/out` sinalizador especifica o nome do assembly resultante.

> [!NOTE]
> Em vez de compilar o `GetProductsWithPriceGreaterThan.cs` arquivo de classe na linha de comando, você pode, alternativamente, usar o [Visual C# Express Edition](https://msdn.microsoft.com/vstudio/express/visualcsharp/) ou criar um projeto de biblioteca de classes separado no Visual Studio Standard Edition. S Ren Jacob Lauritsen forneceu um tipo de projeto do Visual C# Express Edition com código para o `GetProductsWithPriceGreaterThan` procedimento armazenado e os dois procedimentos armazenados gerenciados e o UDF criados nas etapas 3, 5 e 10. O projeto de s Ren inclui também os comandos T-SQL necessários para adicionar os objetos de banco de dados correspondentes.

Com o código compilado em um assembly, estamos prontos para registrar o assembly no banco de dados SQL Server 2005. Isso pode ser executado por meio do T-SQL, usando o comando `CREATE ASSEMBLY` ou por meio de SQL Server Management Studio. Deixe-nos concentrar-se no uso de Management Studio.

Em Management Studio, expanda a pasta programação no banco de dados Northwind. Uma de suas subpastas são assemblies. Para adicionar manualmente um novo assembly ao banco de dados, clique com o botão direito do mouse na pasta assemblies e escolha novo assembly no menu de contexto. Isso exibirá a caixa de diálogo novo assembly (consulte a figura 30). Clique no botão procurar, selecione o `ManuallyCreatedDBObjects.dll` assembly que acabamos de compilar e clique em OK para adicionar o assembly ao banco de dados. Você não deve ver o `ManuallyCreatedDBObjects.dll` assembly no Pesquisador de objetos.

[![Adicionar o assembly ManuallyCreatedDBObjects.dll ao banco de dados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image72.png)

**Figura 30**: Adicionar o `ManuallyCreatedDBObjects.dll` assembly ao banco de dados ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image74.png))

![O ManuallyCreatedDBObjects.dll está listado no Pesquisador de objetos](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image75.png)

**Figura 31**: o `ManuallyCreatedDBObjects.dll` é listado no Pesquisador de objetos

Embora tenhamos adicionado o assembly ao banco de dados Northwind, ainda temos que associar um procedimento armazenado ao `GetProductsWithPriceGreaterThan` método no assembly. Para fazer isso, abra uma nova janela de consulta e execute o seguinte script:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample20.sql)]

Isso cria um novo procedimento armazenado no banco de dados Northwind chamado `GetProductsWithPriceGreaterThan` e o associa com o método gerenciado `GetProductsWithPriceGreaterThan` (que está na classe `StoredProcedures` , que está no assembly `ManuallyCreatedDBObjects` ).

Depois de executar o script acima, atualize a pasta procedimentos armazenados no Pesquisador de objetos. Você deverá ver uma nova entrada de procedimento armazenado, `GetProductsWithPriceGreaterThan` que tem um ícone de bloqueio ao lado dele. Para testar esse procedimento armazenado, insira e execute o seguinte script na janela de consulta:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample21.sql)]

Como mostra a Figura 32, o comando acima exibe informações para esses produtos com um `UnitPrice` maior que $24.95.

[![O ManuallyCreatedDBObjects.dll está listado no Pesquisador de objetos](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image76.png)

**Figura 32**: o `ManuallyCreatedDBObjects.dll` está listado no Pesquisador de objetos ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image78.png))

## <a name="summary"></a>Resumo

O Microsoft SQL Server 2005 fornece integração com o CLR (Common Language Runtime), que permite a criação de objetos de banco de dados usando código gerenciado. Anteriormente, esses objetos de banco de dados só podiam ser criados usando o T-SQL, mas agora podemos criar esses objetos usando linguagens de programação .NET, como C#. Neste tutorial, criamos dois procedimentos armazenados gerenciados e uma função gerenciada definida pelo usuário.

O tipo de projeto SQL Server do Visual Studio s facilita a criação, a compilação e a implantação de objetos de banco de dados gerenciados. Além disso, ele oferece suporte à depuração avançada. No entanto, SQL Server tipos de projeto só estão disponíveis nas edições Professional e Team Systems do Visual Studio. Para aqueles que usam o Visual Web Developer ou a Standard Edition do Visual Studio, as etapas de criação, compilação e implantação devem ser executadas manualmente, como vimos na etapa 13.

Boa programação!

## <a name="further-reading"></a>Leituras adicionais

Para obter mais informações sobre os tópicos discutidos neste tutorial, consulte os seguintes recursos:

- [Vantagens e desvantagens de funções definidas pelo usuário](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [Criando objetos SQL Server 2005 no código gerenciado](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Criando gatilhos usando código gerenciado no SQL Server 2005](http://www.15seconds.com/issue/041006.htm)
- [Como: criar e executar um procedimento armazenado CLR SQL Server](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [Como: criar e executar um CLR SQL Server função definida pelo usuário](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [Como: editar o `Test.sql` script para executar objetos SQL](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [Introdução às funções definidas pelo usuário](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Código gerenciado e SQL Server 2005 (vídeo)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Referência de Transact-SQL](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [Walkthrough: Criando um procedimento armazenado no código gerenciado](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>Sobre o autor

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor de sete livros sobre ASP/ASP. net e fundador da [4guysfromrolla.com](http://www.4guysfromrolla.com), tem trabalhado com tecnologias Web da Microsoft desde 1998. Scott trabalha como consultor, instrutor e escritor independentes. Seu livro mais recente é que a [*Sams ensina a ASP.NET 2,0 em 24 horas*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ele pode ser acessado em [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) ou por meio de seu blog, que pode ser encontrado em [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Agradecimentos especiais a

Esta série de tutoriais foi revisada por muitos revisores úteis. O revisor de Lead para este tutorial foi S Ren Jacob Lauritsen. Além de examinar este artigo, S Ren também criou o projeto do Visual C# Express Edition incluído neste artigo S download para compilar manualmente os objetos de banco de dados gerenciados. Está interessado em revisar meus artigos futuros do MSDN? Nesse caso, me solte uma linha em [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Anterior](debugging-stored-procedures-cs.md) 
>  [Avançar](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
