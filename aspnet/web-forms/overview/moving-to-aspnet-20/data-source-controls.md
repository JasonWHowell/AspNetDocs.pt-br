---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: Controles de Fonte de Dados | Microsoft Docs
author: rick-anderson
description: O controle datagrid em ASP.NET 1.x marcou uma grande melhoria no acesso a dados em aplicativos da Web. No entanto, não foi tão fácil de usar como poderia ter sido...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540214"
---
# <a name="data-source-controls"></a>Controles de fonte de dados

pela [Microsoft](https://github.com/microsoft)

> O controle datagrid em ASP.NET 1.x marcou uma grande melhoria no acesso a dados em aplicativos da Web. No entanto, não foi tão fácil de usar como poderia ter sido. Ele ainda exigiu uma quantidade considerável de código para obter funcionalidade muito útil a partir dele. Esse é o modelo em todos os esforços de acesso a dados em 1.x.

O controle datagrid em ASP.NET 1.x marcou uma grande melhoria no acesso a dados em aplicativos da Web. No entanto, não foi tão fácil de usar como poderia ter sido. Ele ainda exigiu uma quantidade considerável de código para obter funcionalidade muito útil a partir dele. Esse é o modelo em todos os esforços de acesso a dados em 1.x.

ASP.NET 2.0 aborda isso com, em parte, controles de origem de dados. Os controles de origem de dados em ASP.NET 2.0 fornecem aos desenvolvedores um modelo declarativo para recuperar dados, exibir dados e editar dados. O objetivo dos controles de origem de dados é fornecer uma representação consistente de dados para controles vinculados a dados, independentemente da fonte desses dados. No centro dos controles de origem de dados em ASP.NET 2.0 está a classe abstrata DataSourceControl. A classe DataSourceControl fornece uma implementação base da interface IDataSource e da interface IListSource, a última das quais permite atribuir o controle de origem de dados como o DataSource de um controle vinculado a dados (através da nova propriedade DataSourceId discutida posteriormente) e expor os dados nele como uma lista. Cada lista de dados de um controle de origem de dados é exposta como um objeto DataSourceView. O acesso às instâncias do DataSourceView é fornecido pela interface IDataSource. Por exemplo, o método GetViewNames retorna uma ICollection que permite enumerar o DataSourceViews associado a um determinado controle de origem de dados, e o método GetView permite que você acesse uma instância específica do DataSourceView por nome.

Os controles de origem de dados não têm interface de usuário. Eles são implementados como controles de servidor para que possam suportar a sintaxe declarativa e para que tenham acesso ao estado de página, se desejar. Os controles de origem de dados não fornecem nenhuma marcação HTML ao cliente.

> [!NOTE]
> Como você verá mais tarde, também há benefícios de cache obtidos usando controles de fonte de dados.

## <a name="storing-connection-strings"></a>Armazenamento de strings de conexão

Antes de começarmos a ver como configurar os controles de origem de dados, devemos cobrir um novo recurso em ASP.NET 2.0 sobre as strings de conexão. ASP.NET 2.0 introduz uma nova seção no arquivo de configuração que permite armazenar facilmente strings de conexão que podem ser lidas dinamicamente em tempo de execução. A &lt;seção&gt; conexõesStrings facilita a armazenamento de strings de conexão.

O trecho abaixo adiciona uma nova seqüência de conexão.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> Assim como &lt;na&gt; seção Configurações, a &lt;seção conexõesStrings&gt; aparece fora da seção &lt;system.web&gt; no arquivo de configuração.

Para usar essa seqüência de conexões, você pode usar a seguinte sintaxe ao definir o atributo ConnectionString de um controle de servidor.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

A &lt;seção&gt; conexõesStrings também pode ser criptografada para que informações confidenciais não sejam expostas. Essa habilidade será coberta em um módulo posterior.

## <a name="caching-data-sources"></a>Fontes de dados de cache

Cada DataSourceControl fornece quatro propriedades para configurar o cache; HabilitarCaching, CacheDuration, CacheExpirationPolicy e CacheKeyDependency.

## <a name="enablecaching"></a>Enablecaching

EnableCaching é uma propriedade booleana que determina se o cache está ou não habilitado para o controle de origem de dados.

## <a name="cacheduration-property"></a>Propriedade cacheduration

A propriedade CacheDuration define o número de segundos em que o cache permanece válido. Definir esta propriedade como **0** faz com que o cache permaneça válido até ser explicitamente invalidado.

## <a name="cacheexpirationpolicy-property"></a>Propriedade CacheExpirationPolicy

A propriedade CacheExpirationPolicy pode ser definida como **Absoluta** ou **Deslizante**. Configurá-lo como Absoluto significa que o tempo máximo que os dados serão armazenados em cache é o número de segundos especificado pela propriedade CacheDuration. Ao defini-lo como Deslizando, o tempo de expiração é redefinido quando cada operação é realizada.

## <a name="cachekeydependency-property"></a>Propriedade CacheKeyDependency

Se um valor de seqüência for especificado para a propriedade CacheKeyDependency, ASP.NET configurará uma nova dependência de cache com base nessa seqüência. Isso permite que você invalide explicitamente o cache simplesmente alterando ou removendo o CacheKeyDependency.

**Importante**: Se a personificação estiver ativada e o acesso à fonte de dados e/ou conteúdo dos dados for baseado na identidade do cliente, é recomendável que o cache seja desativado definindo EnableCaching to False. Se o cache estiver ativado neste cenário e um usuário diferente do usuário que originalmente solicitou os dados emitir uma solicitação, a autorização para a fonte de dados não será aplicada. Os dados serão simplesmente servidos a partir do cache.

## <a name="the-sqldatasource-control"></a>O controle SqlDataSource

O controle SqlDataSource permite que um desenvolvedor acesse dados armazenados em qualquer banco de dados relacional que suporte ADO.NET. Ele pode usar o provedor System.Data.SqlClient para acessar um banco de dados Do SQL Server, o provedor System.Data.OleDb, o provedor System.Data.Odbc ou o provedor System.Data.OracleClient para acessar o Oracle. Portanto, o SqlDataSource certamente não é usado apenas para acessar dados em um banco de dados SQL Server.

Para usar o SqlDataSource, basta fornecer um valor para a propriedade ConnectionString e especificar um comando SQL ou procedimento armazenado. O controle SqlDataSource cuida de trabalhar com a arquitetura ADO.NET subjacente. Ele abre a conexão, consulta a fonte de dados ou executa o procedimento armazenado, retorna os dados e, em seguida, fecha a conexão para você.

> [!NOTE]
> Como a classe DataSourceControl fecha automaticamente a conexão para você, ela deve reduzir o número de chamadas de clientes geradas pelo vazamento de conexões de banco de dados.

O trecho de código abaixo liga um controle DropDownList a um controle SqlDataSource usando a seqüência de conexões armazenada no arquivo de configuração como mostrado acima.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

Como ilustrado acima, a propriedade DataSourceMode do SqlDataSource especifica o modo para a fonte de dados. No exemplo acima, o DataSourceMode é definido como DataReader. Nesse caso, o SqlDataSource retornará um objeto IDataReader usando um cursor somente para frente e somente leitura. O tipo especificado de objeto que é devolvido é controlado pelo provedor que é usado. Neste caso, estou usando o provedor System.Data.SqlClient conforme &lt;especificado&gt; na seção conexõesStrings do arquivo Web.config. Portanto, o objeto que for devolvido será do tipo SqlDataReader. Ao especificar um valor DataSourceMode do DataSet, os dados podem ser armazenados em um DataSet no servidor. Este modo permite adicionar recursos como classificação, paginação, etc. Se eu estivesse vinculando os dados do SqlDataSource a um controle gridview, eu teria escolhido o modo DataSet. No entanto, no caso de uma Lista dropdown, o modo DataReader é a escolha correta.

> [!NOTE]
> Ao registrar um SqlDataSource ou um AccessDataSource, a propriedade DataSourceMode deve ser definida como DataSet. Uma exceção ocorrerá se você habilitar o cache com um DataSourceMode do DataReader.

## <a name="sqldatasource-properties"></a>SqlDataSourcePropriedades

A seguir estão algumas das propriedades do controle SqlDataSource.

### <a name="cancelselectonnullparameter"></a>Cancelselectonnullparameter

Um valor booleano que especifica se um comando selecionado é cancelado se um dos parâmetros for nulo. True por padrão.

### <a name="conflictdetection"></a>Conflictdetection

Em uma situação em que vários usuários podem estar atualizando uma fonte de dados ao mesmo tempo, a propriedade ConflictDetection determina o comportamento do controle SqlDataSource. Esta propriedade avalia um dos valores da enumeração ConflictOptions. Esses valores são **CompareAllValues** e **OverwriteChanges**. Se definido como SobregravaçãoAltera,a última pessoa a gravar dados na fonte de dados substitui quaisquer alterações anteriores. No entanto, se a propriedade ConflictDetection estiver definida como CompareAllValues, os parâmetros serão criados para as colunas retornadas pelo SelectCommand e os parâmetros também serão criados para manter os valores originais em cada uma dessas colunas, permitindo que o SqlDataSource determine se os valores foram alterados ou não desde que o SelectCommand foi executado.

### <a name="deletecommand"></a>Deletecommand

Define ou recebe a seqüência SQL usada ao excluir linhas do banco de dados. Isso pode ser uma consulta SQL ou um nome de procedimento armazenado.

### <a name="deletecommandtype"></a>Deletecommandtype

Define ou obtém o tipo de comando excluir, seja uma consulta SQL (Texto) ou um procedimento armazenado (StoredProcedure).

### <a name="deleteparameters"></a>Deleteparameters

Retorna os parâmetros usados pelo Comando de Exclusão do objeto SqlDataSourceView associado ao controle SqlDataSource.

### <a name="oldvaluesparameterformatstring"></a>Oldvaluesparameterformatstring

Essa propriedade é usada para especificar o formato dos parâmetros de valor originais nos casos em que a propriedade ConflictDetection está definida como CompareAllValues. O padrão {0} é o que significa que os parâmetros de valor originais tomarão o mesmo nome do parâmetro original. Em outras palavras, se o nome de campo for @EmployeeIDEmployeeID, o parâmetro de valor original seria .

### <a name="selectcommand"></a>SelectCommand

Define ou recebe a seqüência SQL que é usada para recuperar dados do banco de dados. Isso pode ser uma consulta SQL ou um nome de procedimento armazenado.

### <a name="selectcommandtype"></a>Selectcommandtype

Define ou obtém o tipo de comando select, uma consulta SQL (Texto) ou um procedimento armazenado (StoredProcedure).

### <a name="selectparameters"></a>Selectparameters

Retorna os parâmetros usados pelo SelectCommand do objeto SqlDataSourceView associado ao controle SqlDataSource.

### <a name="sortparametername"></a>Sortparametername

Obtém ou define o nome de um parâmetro de procedimento armazenado que é usado ao classificar dados recuperados pelo controle de origem de dados. Válido somente quando SelectCommandType estiver definido como StoredProcedure.

### <a name="sqlcachedependency"></a>Sqlcachedependency

Uma seqüência delimitada de ponto e vírgula especificando os bancos de dados e tabelas usados em uma dependência de cache do SQL Server. (As dependências de cache SQL serão discutidas em um módulo posterior.)

### <a name="updatecommand"></a>Updatecommand

Define ou recebe a seqüência SQL que é usada ao atualizar dados no banco de dados. Isso pode ser uma consulta SQL ou um nome de procedimento armazenado.

### <a name="updatecommandtype"></a>Updatecommandtype

Define ou recebe o tipo de comando de atualização, seja uma consulta SQL (Texto) ou um procedimento armazenado (StoredProcedure).

### <a name="updateparameters"></a>Updateparameters

Retorna os parâmetros usados pelo UpdateCommand do objeto SqlDataSourceView associado ao controle SqlDataSource.

## <a name="the-accessdatasource-control"></a>O controle AccessDataSource

O controle AccessDataSource deriva da classe SqlDataSource e é usado para vincular dados a um banco de dados do Microsoft Access. A propriedade ConnectionString para o controle AccessDataSource é uma propriedade somente leitura. Em vez de usar a propriedade ConnectionString, a propriedade DataFile é usada para apontar para o Banco de Dados de Acesso, conforme mostrado abaixo.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

O AccessDataSource sempre definirá o Nome do Provedor do SqlDataSource base para System.Data.OleDb e se conectará ao banco de dados usando o provedor Microsoft.Jet.OLEDB.4.0 OLE DB. Não é possível usar o controle AccessDataSource para se conectar a um banco de dados access protegido por senha. Se você tiver que se conectar a um banco de dados protegido por senha, você deve usar o controle SqlDataSource.

> [!NOTE]
> Os bancos de dados de acesso armazenados no site da Web devem ser colocados no diretório Dados do Aplicativo.\_ ASP.NET não permite que os arquivos neste diretório sejam navegados. Você precisará conceder permissões de leitura e gravação\_da conta do processo ao diretório de dados do aplicativo ao usar bancos de dados access.

## <a name="the-xmldatasource-control"></a>O controle XmlDataSource

O XmlDataSource é usado para vincular dados XML a controles vinculados a dados. Você pode vincular a um arquivo XML usando a propriedade DataFile ou pode vincular-se a uma seqüência XML usando a propriedade Data. O XmlDataSource expõe os atributos XML como campos vinculáveis. Nos casos em que você precisa vincular a valores que não estão representados como atributos, você precisará usar uma transformação XSL. Você também pode usar expressões XPath para filtrar dados XML.

Considere o seguinte arquivo XML:

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

Observe que o XmlDataSource usa uma propriedade XPath do *People/Person* para filtrar apenas os &lt;nós Pessoa.&gt; O DropDownList então vincula-se ao atributo LastName usando a propriedade DataTextField.

Embora o controle XmlDataSource seja usado principalmente para vincular dados a dados somente de leitura XML, é possível editar o arquivo de dados XML. Observe que, nesses casos, a inserção automática, a atualização e a exclusão de informações no arquivo XML não acontecem automaticamente como acontece com outros controles de origem de dados. Em vez disso, você terá que escrever código para editar manualmente os dados usando os seguintes métodos do controle XmlDataSource.

### <a name="getxmldocument"></a>Getxmldocument

Recupera um objeto XmlDocument contendo o código XML recuperado pelo XmlDataSource.

### <a name="save"></a>Salvar

Salva o XmlDocument na memória de volta à fonte de dados.

É importante perceber que o método Salvar só funcionará quando as seguintes duas condições forem atendidas:

1. O XmlDataSource está usando a propriedade DataFile para vincular a um arquivo XML em vez da propriedade Data para vincular a dados XML na memória.
2. Nenhuma transformação é especificada através da propriedade Transformar ou TransformarArquivo.

Observe também que o método Salvar pode produzir resultados inesperados quando chamado por vários usuários simultaneamente.

## <a name="the-objectdatasource-control"></a>O controle ObjectDataSourceSource

Os controles de origem de dados que cobrimos até agora são excelentes opções para aplicativos de dois níveis onde o controle de origem de dados se comunica diretamente com o armazenamento de dados. No entanto, muitos aplicativos do mundo real são aplicativos de vários níveis onde um controle de origem de dados pode precisar se comunicar com um objeto de negócios que, por sua vez, se comunica com a camada de dados. Nessas situações, o ObjectDataSource preenche bem a conta. O ObjectDataSource funciona em conjunto com um objeto de origem. O controle ObjectDataSource criará uma instância do objeto de origem, chamará o método especificado e eliminará a instância do objeto no âmbito de uma única solicitação, se o objeto tiver métodos de ocorrência em vez de métodos estáticos (Compartilhadono No Visual Basic). Portanto, seu objeto deve ser apátrida. Ou seja, seu objeto deve adquirir e liberar todos os recursos necessários dentro do período de uma única solicitação. Você pode controlar como o objeto de origem é criado manipulando o evento ObjectCreating do controle ObjectDataSource. Você pode criar uma instância do objeto de origem e, em seguida, definir a propriedade ObjectInstance da classe ObjectDataSourceEventArgs para essa instância. O controle ObjectDataSource usará a instância criada no evento ObjectCreating em vez de criar uma instância por conta própria.

Se o objeto de origem de um controle ObjectDataSource expor métodos estáticos públicos (Compartilhados no Visual Basic) que podem ser chamados para recuperar e modificar dados, um controle ObjectDataSource chamará esses métodos diretamente. Se um controle ObjectDataSource deve criar uma instância do objeto de origem para fazer chamadas de método, o objeto deve incluir um construtor público que não tem parâmetros. O controle ObjectDataSource chamará este construtor quando ele criar uma nova instância do objeto de origem.

Se o objeto de origem não contiver um construtor público sem parâmetros, você poderá criar uma instância do objeto de origem que será usado pelo controle ObjectDataSource no evento ObjectCreating.

## <a name="specifying-object-methods"></a>Especificando métodos de objeto

O objeto de origem de um controle ObjectDataSource pode conter qualquer número de métodos usados para selecionar, inserir, atualizar ou excluir dados. Esses métodos são chamados pelo controle ObjectDataSource com base no nome do método, conforme identificado usando a propriedade SelectMethod, InsertMethod, UpdateMethod ou DeleteMethod do controle ObjectDataSource. O objeto de origem também pode incluir um método SelectCount opcional, que é identificado pelo controle ObjectDataSource usando a propriedade SelectCountMethod, que retorna a contagem do número total de objetos na fonte de dados. O controle ObjectDataSource chamará o método SelectCount depois que um método Select for chamado para recuperar o número total de registros na fonte de dados para uso ao pagirá.

## <a name="lab-using-data-source-controls"></a>Laboratório usando controles de fonte de dados

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>Exercício 1 - Exibir dados com o Controle SqlDataSource

O exercício a seguir usa o controle SqlDataSource para se conectar ao banco de dados Northwind. Ele assume que você tem acesso ao banco de dados Northwind em uma instância do SQL Server 2000.

1. Criar um site do ASP.NET.
2. Adicione um novo arquivo web.config.

    1. Clique com o botão direito do mouse sobre o projeto no Solution Explorer e clique em Adicionar novo item.
    2. Escolha o Arquivo de Configuração da Web na lista de modelos e clique em Adicionar.
3. Editar &lt;a seção conexõesStrings&gt; da seguinte forma: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. Alterne para exibição de código e adicione um &lt;atributo ConnectionString e&gt; um atributo SelectCommand ao controle asp:SqlDataSource da seguinte forma: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. Na exibição do Design, adicione um novo controle GridView.
6. Na parada Escolher a fonte de dados no menu 'Tarefas de rede', escolha SqlDataSource1'.
7. Clique com o botão direito do mouse em Default.aspx e escolha Exibir no Navegador no menu. Clique em Sim quando solicitado para salvar.
8. O GridView exibe os dados da tabela Produtos.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>Exercício 2 - Edição de dados com o Controle SqlDataSource

O exercício a seguir demonstra como vincular os dados a um controle DropDownList usando a sintaxe declarativa e permite editar os dados apresentados no controle DropDownList.

1. Na exibição Design, exclua o controle GridView do Default.aspx. 

    **Importante**: Deixe o controle SqlDataSource na página.
2. Adicione um controle DropDownList ao Default.aspx.
3. Mude para exibição Origem.
4. Adicione um atributo DataSourceId, DataTextField e &lt;DataValueField ao&gt; controle asp:DropDownList da seguinte forma: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Salve Default.aspx e visualize-o no navegador. Observe que o DropDownList contém todos os produtos do banco de dados Northwind.
6. Feche o navegador.
7. Na exibição De origem do Default.aspx, adicione um novo controle TextBox abaixo do controle DropDownList. Altere a propriedade ID da TextBox para txtProductName.
8. Sob o controle TextBox, adicione um novo controle button. Altere a propriedade ID do Botão para btnUpdate e a propriedade Text para **Update Product Name**.
9. Na exibição de origem do Default.aspx, adicione uma propriedade UpdateCommand e dois novos UpdateParameters à tag SqlDataSource da seguinte forma: 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > Observe que há dois parâmetros de atualização (ProductName e ProductID) adicionados neste código. Esses parâmetros são mapeados para a propriedade Text da txtProductName TextBox e da propriedade SelectedValue da ddlProducts DropDownList.
10. Mude para exibição design e clique duas vezes no controle Button para adicionar um manipulador de eventos.
11. Adicione o seguinte código ao\_código btnUpdate Clique: 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Clique com o botão direito do mouse em Default.aspx e escolha visualizá-lo no navegador. Clique em Sim quando solicitado para salvar todas as alterações.
13. ASP.NET classes parciais 2.0 permitem a compilação em tempo de execução. Não é necessário construir um aplicativo para ver as alterações de código entrarem em vigor.
14. Selecione um produto na Lista de Gotas.
15. Digite um novo nome para o produto selecionado na TextBox e, em seguida, clique no botão Atualizar.
16. O nome do produto é atualizado no banco de dados.

## <a name="exercise-3-using-the-objectdatasource-control"></a>Exercício 3 Usando o controle ObjectDataSource

Este exercício demonstrará como usar o controle ObjectDataSource e um objeto de origem para interagir com o banco de dados Northwind.

1. Clique com o botão direito do mouse sobre o projeto no Solution Explorer e clique em Adicionar novo item.
2. Selecione Formulário da Web na lista de modelos. Altere o nome para object.aspx e clique em Adicionar.
3. Clique com o botão direito do mouse sobre o projeto no Solution Explorer e clique em Adicionar novo item.
4. Selecione Classe na lista de modelos. Altere o nome da classe para NorthwindData.cs e clique em Adicionar.
5. Clique em Sim quando solicitado para\_adicionar a classe à pasta Código do aplicativo.
6. Adicione o seguinte código ao arquivo NorthwindData.cs: 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. Adicione o seguinte código à exibição Origem do object.aspx: 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. Salve todos os arquivos e navegue pelo object.aspx.
9. Interaja com a interface visualizando detalhes, editando funcionários, adicionando funcionários e excluindo funcionários.
