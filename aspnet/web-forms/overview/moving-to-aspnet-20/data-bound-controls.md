---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: Controles de limite de dados | Microsoft Docs
author: rick-anderson
description: A maioria dos aplicativos ASP.NET dependem de algum grau de apresentação de dados de uma fonte de dados back-end. Os controles vinculados a dados têm sido uma parte fundamental da interação com...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: 941e2ed15b3da28991e7b06cbab570eb1b5b8899
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543074"
---
# <a name="data-bound-controls"></a>Controles de dados associados

pela [Microsoft](https://github.com/microsoft)

> A maioria dos aplicativos ASP.NET dependem de algum grau de apresentação de dados de uma fonte de dados back-end. Os controles vinculados a dados têm sido uma parte fundamental da interação com dados em aplicativos web dinâmicos. ASP.NET 2.0 introduz algumas melhorias substanciais nos controles vinculados a dados, incluindo uma nova classe BaseDataBoundControl e sintaxe declarativa.

A maioria dos aplicativos ASP.NET dependem de algum grau de apresentação de dados de uma fonte de dados back-end. Os controles vinculados a dados têm sido uma parte fundamental da interação com dados em aplicativos web dinâmicos. ASP.NET 2.0 introduz algumas melhorias substanciais nos controles vinculados a dados, incluindo uma nova classe BaseDataBoundControl e sintaxe declarativa.

O BaseDataBoundControl atua como a classe base da classe DataBoundControl e da classe HierarchicalDataBoundControl. Neste módulo, discutiremos as seguintes classes derivadas do DataBoundControl:

- AdRotator
- Controles de lista
- GridView
- Formview
- Detailsview

Também discutiremos as seguintes classes que derivam da classe HierarchicalDataBoundControl:

- TreeView
- Menu
- Sitemappath

## <a name="databoundcontrol-class"></a>Classe de controle de databound

A classe DataBoundControl é uma classe abstrata (marcada como MustInherit em VB) usada para interagir com dados tabulares ou estilo de lista. Os controles a seguir são alguns dos controles que derivam do DataBoundControl.

## <a name="adrotator"></a>AdRotator

O controle do AdRotator permite que você exiba um banner gráfico em uma página da Web vinculada a uma URL específica. O gráfico exibido é girado usando propriedades para o controle. A freqüência de um anúncio específico exibido em uma página pode ser configurada usando a propriedade Impressões e os **anúncios** podem ser filtrados usando a filtragem de palavras-chave.

Os controles do AdRotator usam um arquivo XML ou uma tabela em um banco de dados para obter dados. Os atributos a seguir são usados em arquivos XML para configurar o controle do AdRotator.

### <a name="imageurl"></a>ImageUrl
A URL de uma imagem a ser exibida para o anúncio.

### <a name="navigateurl"></a>Navigateurl
A URL para a a que o usuário deve ser levado quando o anúncio é clicado. Isso deve ser codificado por URL.

### <a name="alternatetext"></a>AlternateText
O texto alternativo que é exibido em uma dica de ferramenta e lido pelos leitores de tela. Também é exibido quando a imagem especificada por ImageUrl não está disponível.

### <a name="keyword"></a>Palavra-chave
Define uma palavra-chave que pode ser usada ao usar a filtragem de palavras-chave. Se especificado, somente os anúncios com uma palavra-chave correspondente ao filtro de palavras-chave serão exibidos.

### <a name="impressions"></a>Impressões
Um número de ponderação que determina com que frequência um anúncio em particular é provável que apareça. É relativo à impressão de outros anúncios no mesmo arquivo. O valor máximo das impressões coletivas para todos os anúncios em um arquivo XML é de 2.048.000.000 1.

### <a name="height"></a>Altura
A altura do anúncio em pixels.

### <a name="width"></a>Largura
A largura do anúncio em pixels.

> [!NOTE]
> Os atributos Altura e Largura sobrepõem a altura e a largura do próprio controle do AdRotator.

Um arquivo XML típico pode parecer o seguinte:

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

No exemplo acima, o anúncio de Contoso é duas vezes mais provável de aparecer do anúncio do ASP.NET site por causa do valor para o atributo Impressões.

Para exibir anúncios do arquivo XML acima, adicione um controle do AdRotator a uma página e defina a propriedade **AdvertisementFile** para apontar para o arquivo XML como mostrado abaixo:

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

Se você optar por usar uma tabela de banco de dados como fonte de dados para o controle do AdRotator, primeiro você precisará configurar um banco de dados usando o seguinte esquema:

| **Nome da coluna** | **Tipo de dados** | **Descrição** |
| --- | --- | --- |
| ID | INT | Chave primária. Esta coluna pode ter qualquer nome. |
| ImageUrl | nvarchar *(comprimento)* | A URL relativa ou absoluta da imagem a ser exibida para o anúncio. |
| Navigateurl | nvarchar *(comprimento)* | A URL de destino do anúncio. Se você não fornecer um valor, o anúncio não é um hiperlink. |
| AlternateText | nvarchar *(comprimento)* | O texto exibido se a imagem não puder ser encontrada. Em alguns navegadores, o texto é exibido como uma Dica de Ferramenta. O texto alternativo também é usado para acessibilidade para que os usuários que não podem ver o gráfico possam ouvir sua descrição lida em voz alta. |
| Palavra-chave | nvarchar *(comprimento)* | Uma categoria para o anúncio no qual a página pode filtrar. |
| Impressões | int(4) | Um número que indica a probabilidade de quantas vezes o anúncio é exibido. Quanto maior o número, mais freqüentemente o anúncio será exibido. O total de todos os valores de impressões no arquivo XML não pode exceder 2.048.000.000 - 1. |
| Largura | int(4) | A largura da imagem em pixels. |
| Altura | int(4) | A altura da imagem em pixels. |

Nos casos em que você já tem um banco de dados com um esquema diferente, você pode usar as propriedades **AlternateTextField,** **ImageUrlField**e **NavigateUrlField** para mapear os atributos do AdRotator ao seu banco de dados existente. Para exibir os dados do banco de dados no controle do AdRotator, adicione um controle de origem de dados à página, configure a seqüência de conexões para o controle de origem de dados para apontar para o seu banco de dados e defina a propriedade **DataSourceID** do controle do AdRotator para o ID do controle de origem de dados. Nos casos em que você tiver a necessidade de configurar os anúncios do AdRotator de forma programática, use o evento AdCreated. O evento AdCreated tem dois parâmetros; um objeto e o outro uma instância de AdCreatedEventArgs. O AdCreatedEventArgs é uma referência ao anúncio que está sendo criado.

O seguinte trecho de código define o ImageUrl, NavigateUrl e AlternateText para um anúncio de forma programática:

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>Controles de lista

Os controles de lista incluem a ListBox, DropDownList, CheckBoxList, RadioButtonList e BulletedList. Cada um desses controles pode ser vinculado a uma fonte de dados. Eles usam um campo na fonte de dados como o texto de exibição e podem usar opcionalmente um segundo campo como o valor de um item. Os itens também podem ser adicionados estáticamente no tempo de projeto, e você pode misturar itens estáticos e itens dinâmicos adicionados a partir de uma fonte de dados.

Para vincular os dados a um controle de lista, adicione um controle de origem de dados à página. Especifique um comando SELECT para o controle de origem de dados e, em seguida, defina a propriedade DataSourceID do controle de lista para o ID do controle de origem de dados. Use as propriedades **DataTextField** e **DataValueField** para definir o texto de exibição e o valor para o controle. Além disso, você pode usar a propriedade **DataTextFormatString** para controlar a aparência do texto de exibição da seguinte forma:

| **Expressão** | **Descrição** |
| --- | --- |
| Preço:{0:C} | Para dados numéricos/decimais. Exibe o "Preço" literal seguido de números no formato de moeda. O formato da moeda depende da configuração de cultura especificada no atributo cultura na diretiva **Página** ou no arquivo Web.config. |
| {0:D4} | Para dados inteiros. Não pode ser usado com números decimais. Os inteiros são exibidos em um campo acolchoado zero, com quatro caracteres de largura. |
| {0:N2}% | Para dados numéricos. Exibe o número com precisão de 2 casas decimais seguido do "%" literal. |
| {0:000.0} | Para dados numéricos/decimais. Os números são arredondados para um lugar decimal. Os números com menos de três dígitos zero são preenchidos com zeros. |
| {0:D} | Para dados de data/hora. Exibe formato de longa data ("Quinta-feira, 06 de agosto de 1996"). O formato de data depende da configuração da cultura da página ou do arquivo Web.config. |
| {0:d} | Para dados de data/hora. Exibe formato de data curta ("31/12/99"). |
| {0:yy-MM-dd} | Para dados de data/hora. Exposições datam em formato nuérico do mês-dia (96-08-06) |

## <a name="gridview"></a>GridView

O controle GridView permite a exibição e edição de dados tabulares usando uma abordagem declarativa e é o sucessor do controle DataGrid. Os recursos a seguir estão disponíveis no controle GridView.

- Vinculação aos controles de origem de dados, como O SqlDataSource.
- Recursos de classificação incorporados.
- Recursos de atualização e exclusão incorporados.
- Recursos de paginação incorporados.
- Recursos de seleção de linha incorporados.
- Acesso programático ao modelo de objeto GridView para definir dinamicamente propriedades, lidar com eventos e assim por diante.
- Vários campos-chave.
- Vários campos de dados para as colunas de hiperlink.
- Aparência personalizável através de temas e estilos.

**Campos de coluna**

Cada coluna no controle GridView é representada por um objeto DataControlField. Por padrão, a propriedade AutoGenerateColumns é definida como **true,** o que cria um objeto AutoGeneratedField para cada campo na fonte de dados. Cada campo é então renderizado como uma coluna no controle GridView na ordem em que cada campo aparece na fonte de dados. Você também pode controlar manualmente quais campos de coluna aparecem no controle **GridView** definindo a propriedade **AutoGenerateColumns** como **falsa** e, em seguida, definindo sua própria coleção de campos de coluna. Diferentes tipos de campo de colunas determinam o comportamento das colunas no controle.

A tabela a seguir lista os diferentes tipos de campo de coluna que podem ser usados.

| **Tipo de campo de coluna** | **Descrição** |
| --- | --- |
| BoundField | Exibe o valor de um campo em uma fonte de dados. Este é o tipo de coluna padrão do controle GridView. |
| ButtonField | Exibe um botão de comando para cada item no controle GridView. Isso permite criar uma coluna de controles de botão personalizados, como o botão Adicionar ou remover. |
| CheckBoxField | Exibe uma caixa de seleção para cada item no controle GridView. Este tipo de campo de coluna é comumente usado para exibir campos com um valor booleano. |
| CommandField | Exibe botões de comando predefinidos para executar operações de seleção, edição ou exclusão. |
| HyperLinkField | Exibe o valor de um campo em uma fonte de dados como um hiperlink. Este tipo de campo de coluna permite vincular um segundo campo à URL do hiperlink. |
| ImageField | Exibe uma imagem para cada item no controle GridView. |
| Templatefield | Exibe conteúdo definido pelo usuário para cada item no controle GridView de acordo com um modelo especificado. Este tipo de campo de coluna permite criar um campo de coluna personalizado. |

Para definir uma coleção de campo de coluna declarativamente, adicione primeiro as tags de abertura e fechamento ** &lt;de colunas&gt; ** entre as tags de abertura e fechamento do controle GridView. Em seguida, liste os campos de coluna que você deseja incluir entre as ** &lt;tags Colunas&gt; ** de abertura e fechamento. As colunas especificadas são adicionadas à coleção Colunas na ordem listada. A coleção **Colunas** armazena todos os campos de coluna no controle e permite gerenciar programáticamente os campos de coluna no controle GridView.

Campos de coluna explicitamente declarados podem ser exibidos em combinação com campos de coluna gerados automaticamente. Quando ambos são usados, os campos de coluna explicitamente declarados são renderizados primeiro, seguidos pelos campos de coluna gerados automaticamente.

## <a name="binding-to-data"></a>Vinculação a Dados

O controle do GridView pode ser vinculado a um controle de origem de dados (como **SqlDataSource,** **ObjectDataSource**e assim por diante), bem como qualquer fonte de dados que implemente a interface System.Collections.IEnumerable (como System.Data.DataView, System.Collections.ArrayList ou System.Collections.Hashtable). Use um dos seguintes métodos para vincular o controle GridView ao tipo de origem de dados apropriado:

- Para vincular a um controle de origem de dados, defina a propriedade DataSourceID do controle GridView ao valor de ID do controle de origem de dados. O controle gridview se liga automaticamente ao controle de origem de dados especificado e pode aproveitar os recursos do controle de origem de dados para executar a funcionalidade de classificação, atualização, exclusão e paginação. Este é o método preferido para vincular aos dados.
- Para vincular a uma fonte de dados que implementa a interface System.Collections.IEnumerable, programate a propriedade DataSource do controle GridView à fonte de dados e, em seguida, chame o método DataBind. Ao usar esse método, o controle GridView não fornece funcionalidade de classificação, atualização, exclusão e paginação incorporada. Você precisa fornecer essa funcionalidade você mesmo.

## <a name="data-operations"></a>Operações de dados

O controle GridView fornece muitos recursos incorporados que permitem ao usuário classificar, atualizar, excluir, selecionar e página através de itens no controle. Quando o controle do GridView está vinculado a um controle de origem de dados, o controle gridview pode tirar proveito dos recursos do controle de origem de dados e fornecer funcionalidade automática de classificação, atualização e exclusão automática.

> [!NOTE]
> O controle GridView pode fornecer suporte para classificação, atualização e exclusão com outros tipos de fontes de dados; no entanto, você precisará fornecer um manipulador de eventos apropriado com a implementação dessas operações.

A classificação permite que o usuário classifique os itens no controle gridview em relação a uma coluna específica clicando no cabeçalho da coluna. Para habilitar a classificação, defina a propriedade AllowSorting como **true**.

As funcionalidades automáticas de atualização, exclusão e seleção são ativadas quando um botão em um campo de coluna **ButtonField** ou **TemplateField,** com um nome de comando de "Editar", "Excluir" e "Selecionar", respectivamente, é clicado. O controle GridView pode adicionar automaticamente um campo de coluna **CommandField** com um botão Editar, excluir ou Selecionar se a propriedade AutoGenerateEditButton, AutoGenerateDeleteButton ou AutoGenerateSelectButton estiver definida **como true,** respectivamente.

> [!NOTE]
> A inserção de registros na fonte de dados não é suportada diretamente pelo controle GridView. No entanto, é possível inserir registros usando o controle GridView em conjunto com o controle DetailsView ou FormView.

Em vez de exibir todos os registros na fonte de dados ao mesmo tempo, o controle GridView pode quebrar automaticamente os registros em páginas. Para habilitar a paginação, defina a propriedade AllowPaging **como verdadeira**.

## <a name="customizing-the-user-interface"></a>Personalizando a interface do usuário

Você pode personalizar a aparência do controle GridView definindo as propriedades de estilo para as diferentes partes do controle. A tabela a seguir lista as diferentes propriedades de estilo.

| **Propriedade de estilo** | **Descrição** |
| --- | --- |
| Alternatingrowstyle | As configurações de estilo para as linhas de dados alternadas no controle GridView. Quando esta propriedade é definida, as linhas de dados são exibidas alternando entre as configurações RowStyle e **alternandoRowStyle.** |
| Editrowstyle | As configurações de estilo para a linha que está sendo editada no controle GridView. |
| Emptydatarowstyle | As configurações de estilo para a linha de dados vazia exibida no controle GridView quando a fonte de dados não contém registros. |
| Footerstyle | As configurações de estilo para a linha de rodapé do controle GridView. |
| Headerstyle | As configurações de estilo para a linha de cabeçalho do controle GridView. |
| Pagerstyle | As configurações de estilo para a linha de pager do controle GridView. |
| Rowstyle | As configurações de estilo para as linhas de dados no controle GridView. Quando a propriedade **AlternatingRowStyle** também é definida, as linhas de dados são exibidas alternando entre as configurações **RowStyle** e **alternandoRowStyle.** |
| Selectedrowstyle | As configurações de estilo para a linha selecionada no controle GridView. |

Você também pode mostrar ou esconder diferentes partes do controle. A tabela a seguir lista as propriedades que controlam quais partes são mostradas ou ocultas.

| **Propriedade** | **Descrição** |
| --- | --- |
| Showfooter | Mostra ou esconde a seção rodapé do controle GridView. |
| Showheader | Mostra ou esconde a seção de cabeçalho do controle GridView. |

### <a name="events"></a>Eventos

O controle GridView fornece vários eventos contra os que você pode programar. Isso permite que você execute uma rotina personalizada sempre que um evento ocorra. A tabela a seguir lista os eventos suportados pelo controle GridView.

| **Evento** | **Descrição** |
| --- | --- |
| Pageindexchanged | Ocorre quando um dos botões do pager é clicado, mas depois que o controle GridView lida com a operação de paginação. Este evento é comumente usado quando você precisa executar uma tarefa depois que o usuário navega para uma página diferente no controle. |
| Pageindexchanging | Ocorre quando um dos botões do pager é clicado, mas antes que o controle GridView manuseie a operação de paginação. Este evento é frequentemente usado para cancelar a operação de paginação. |
| Rowcancelingedit | Ocorre quando o botão Cancelar de uma linha é clicado, mas antes que o controle gridview saia do modo de edição. Este evento é frequentemente usado para parar a operação de cancelamento. |
| Rowcommand | Ocorre quando um botão é clicado no controle GridView. Este evento é frequentemente usado para executar uma tarefa quando um botão é clicado no controle. |
| Rowcreated | Ocorre quando uma nova linha é criada no controle GridView. Este evento é frequentemente usado para modificar o conteúdo de uma linha quando a linha é criada. |
| Rowdatabound | Ocorre quando uma linha de dados é vinculada a dados no controle GridView. Este evento é frequentemente usado para modificar o conteúdo de uma linha quando a linha está vinculada a dados. |
| Rowdeleted | Ocorre quando o botão Excluir de uma linha é clicado, mas depois que o controle GridView exclui o registro da fonte de dados. Este evento é frequentemente usado para verificar os resultados da operação de exclusão. |
| Rowdeleting | Ocorre quando o botão Excluir de uma linha é clicado, mas antes que o controle GridView exclua o registro da fonte de dados. Este evento é frequentemente usado para cancelar a operação de exclusão. |
| Rowediting | Ocorre quando o botão Editar de uma linha é clicado, mas antes que o controle GridView entre no modo de edição. Este evento é frequentemente usado para cancelar a operação de edição. |
| Rowupdated | Ocorre quando o botão Atualização de uma linha é clicado, mas depois que o controle GridView atualiza a linha. Este evento é frequentemente usado para verificar os resultados da operação de atualização. |
| Rowupdating | Ocorre quando o botão Atualização de uma linha é clicado, mas antes que o controle GridView atualize a linha. Este evento é frequentemente usado para cancelar a operação de atualização. |
| SelectedIndexChanged | Ocorre quando o botão Select de uma linha é clicado, mas depois que o controle GridView lida com a operação selecionada. Este evento é frequentemente usado para executar uma tarefa depois que uma linha é selecionada no controle. |
| Selectedindexchanging | Ocorre quando o botão Select de uma linha é clicado, mas antes que o controle GridView manuseie a operação selecionada. Este evento é frequentemente usado para cancelar a operação de seleção. |
| Classificado | Ocorre quando o hiperlink para classificar uma coluna é clicado, mas depois que o controle gridview lida com a operação de classificação. Este evento é comumente usado para executar uma tarefa depois que o usuário clica em um hiperlink para classificar uma coluna. |
| Classificação | Ocorre quando o hiperlink para classificar uma coluna é clicado, mas antes que o controle GridView manuseie a operação de classificação. Este evento é frequentemente usado para cancelar a operação de classificação ou para executar uma rotina de classificação personalizada. |

## <a name="formview"></a>Formview

O controle FormView é usado para exibir um único registro de uma fonte de dados. É semelhante ao controle DetailsView, exceto que exibe modelos definidos pelo usuário em vez de campos de linha. Criar seus próprios modelos lhe dá maior flexibilidade no controle de como os dados são exibidos. O controle FormView suporta os seguintes recursos:

- Vinculação aos controles de origem de dados, como SqlDataSource e ObjectDataSource.
- Recursos de inserção incorporados.
- Recursos de atualização e exclusão incorporados.
- Recursos de paginação incorporados.
- Acesso programático ao modelo de objeto FormView para definir dinamicamente propriedades, lidar com eventos e assim por diante.
- Aparência personalizável através de modelos, temas e estilos definidos pelo usuário.

## <a name="templates"></a>Modelos

Para que o controle FormView exiba conteúdo, você precisa criar modelos para as diferentes partes do controle. A maioria dos modelos são opcionais; no entanto, você deve criar um modelo para o modo em que o controle está configurado. Por exemplo, um controle FormView que suporta a inserção de registros deve ter um modelo de item de inserção definido. A tabela a seguir lista os diferentes modelos que você pode criar.

| **Tipo do modelo** | **Descrição** |
| --- | --- |
| Edititemtemplate | Define o conteúdo da linha de dados quando o controle FormView está no modo de edição. Este modelo geralmente contém controles de entrada e botões de comando com os quais o usuário pode editar um registro existente. |
| Emptydatatemplate | Define o conteúdo da linha de dados vazia exibida quando o controle FormView está vinculado a uma fonte de dados que não contém nenhum registro. Este modelo geralmente contém conteúdo para alertar o usuário de que a fonte de dados não contém nenhum registro. |
| Footertemplate | Define o conteúdo para a linha de rodapé. Este modelo geralmente contém qualquer conteúdo adicional que você gostaria de exibir na linha de rodapé. Como alternativa, você pode simplesmente especificar texto para exibir na linha de rodapé definindo a propriedade FooterText. |
| Headertemplate | Define o conteúdo da linha de cabeçalho. Este modelo geralmente contém qualquer conteúdo adicional que você gostaria de exibir na linha de cabeçalho. Como alternativa, você pode simplesmente especificar texto para exibir na linha de cabeçalho definindo a propriedade HeaderText. |
| ItemTemplate | Define o conteúdo da linha de dados quando o controle FormView estiver no modo somente leitura. Este modelo geralmente contém conteúdo para exibir os valores de um registro existente. |
| Insertitemtemplate | Define o conteúdo da linha de dados quando o controle FormView está no modo de inserção. Este modelo geralmente contém controles de entrada e botões de comando com os quais o usuário pode adicionar um novo registro. |
| Pagertemplate | Define o conteúdo da linha de pager exibida quando o recurso de paginação está ativado (quando a propriedade AllowPaging é definida como **true**). Este modelo geralmente contém controles com os quais o usuário pode navegar para outro registro. |

Os controles de entrada no modelo de item de edição e no modelo de itens de inserção podem ser vinculados aos campos de uma fonte de dados usando uma expressão de vinculação bidirecional. Isso permite que o controle FormView extraia automaticamente os valores do controle de entrada para uma operação de atualização ou inserção. Expressões de vinculação bidirecionais também permitem que controles de entrada em um modelo de item de edição exibam automaticamente os valores de campo originais.

### <a name="binding-to-data"></a>Vinculação a Dados

O controle do FormView pode ser vinculado a um controle de origem de dados (como **SqlDataSource,** AccessDataSource, **ObjectDataSource** e assim por diante), ou a qualquer fonte de dados que implemente a interface System.Collections.IEnumerable (como System.Data.DataView, System.Collections.ArrayList e System.Collections.Hashtable). Use um dos seguintes métodos para vincular o controle FormView ao tipo de origem de dados apropriado:

- Para vincular a um controle de origem de dados, defina a propriedade DataSourceID do controle FormView ao valor de ID do controle de origem de dados. O controle do FormView se liga automaticamente ao controle de origem de dados especificado e pode aproveitar os recursos do controle de origem de dados para executar a funcionalidade de inserção, atualização, exclusão e paginação. Este é o método preferido para vincular aos dados.
- Para vincular a uma fonte de dados que implementa a interface **System.Collections.IEnumerable,** programate a propriedade DataSource do controle FormView à fonte de dados e, em seguida, chame o método DataBind. Ao usar este método, o controle FormView não fornece funcionalidade de inserção, atualização, exclusão e paginação incorporada. Você precisa fornecer essa funcionalidade usando o evento apropriado.

## <a name="data-operations"></a>Operações de dados

O controle FormView fornece muitos recursos incorporados que permitem ao usuário atualizar, excluir, inserir e página através de itens no controle. Quando o controle do FormView está vinculado a um controle de origem de dados, o controle formView pode tirar proveito dos recursos do controle de origem de dados e fornecer funcionalidade de atualização, exclusão, inserção e paginação automática. O controle FormView pode fornecer suporte para operações de atualização, exclusão, inserção e paginação com outros tipos de fontes de dados; no entanto, você deve fornecer um manipulador de eventos apropriado com a implementação dessas operações.

Como o controle FormView usa modelos, ele não fornece uma maneira de gerar automaticamente botões de comando para executar a atualização, exclusão ou inserção de operações. Você deve incluir manualmente esses botões de comando no modelo apropriado. O controle FormView reconhece certos botões que têm suas propriedades **CommandName** definidas para valores específicos. A tabela a seguir lista os botões de comando que o controle FormView reconhece.

| **Botão** | **Valor do nome do comando** | **Descrição** |
| --- | --- | --- |
| Cancelar | "Cancelar" | Usado na atualização ou inserção de operações para cancelar a operação e descartar os valores inseridos pelo usuário. O controle FormView retorna ao modo especificado pela propriedade DefaultMode. |
| Excluir | "Excluir" | Usado na exclusão de operações para excluir o registro exibido da fonte de dados. Levanta os eventos ItemDeleting e ItemDeleted. |
| Editar | "Editar" | Usado na atualização de operações para colocar o controle FormView no modo de edição. O conteúdo especificado na propriedade **EditItemTemplate** é exibido para a linha de dados. |
| Inserir | "Inserir" | Usado na inserção de operações para tentar inserir um novo registro na fonte de dados usando os valores fornecidos pelo usuário. Eleva os eventos Inseridas e itens inseridas no item. |
| Novo | "Novo" | Usado na inserção de operações para colocar o controle FormView no modo de inserção. O conteúdo especificado na propriedade **InsertItemTemplate** é exibido para a linha de dados. |
| Página | "Página" | Usado em operações de paginação para representar um botão na linha pager que executa a paginação. Para especificar a operação de paginação, defina a propriedade **CommandArgument** do botão como "Next", "Prev", "First", "Last" ou o índice da página para a qual navegar. Aumenta os eventos PageIndexChanging e PageIndexChanged. |
| Atualizar | "Atualização" | Usado na atualização de operações para tentar atualizar o registro exibido na fonte de dados com os valores fornecidos pelo usuário. Levanta os eventos ItemAtualização e ItemAtualizado. |

Ao contrário do botão Excluir (que exclui o registro exibido imediatamente), quando o botão Editar ou Novo é clicado, o controle FormView entra no modo de edição ou inserção, respectivamente. No modo de edição, o conteúdo contido na propriedade **EditItemTemplate** é exibido para o item de dados atual. Normalmente, o modelo de item de edição é definido de tal forma que o botão Editar é substituído por um botão Atualizar e cancelar. Controles de entrada apropriados para o tipo de dados do campo (como uma TextBox ou um controle CheckBox) também são geralmente exibidos com o valor de um campo para o usuário modificar. Clicar no botão Atualizar atualiza o registro na fonte de dados, enquanto o botão Cancelar abandona quaisquer alterações.

Da mesma forma, o conteúdo contido na propriedade **InsertItemTemplate** é exibido para o item de dados quando o controle está no modo de inserção. O modelo de item de inserção é normalmente definido de tal forma que o botão Novo é substituído por um botão Inserir e um botão Cancelar, e os controles de entrada vazios são exibidos para que o usuário insira os valores para o novo registro. Clicar no botão Inserir insere o registro na fonte de dados, enquanto o botão Cancelar abandona quaisquer alterações.

O controle FormView fornece um recurso de paginação, que permite que o usuário navegue para outros registros na fonte de dados. Quando ativada, uma linha de pager é exibida no controle FormView que contém os controles de navegação da página. Para habilitar a paginação, defina a propriedade **AllowPaging** **como verdadeira**. Você pode personalizar a linha pager definindo as propriedades dos objetos contidos no PagerStyle e na propriedade PagerSettings. Em vez de usar a ui da linha de página incorporada, você pode criar sua própria ui usando a propriedade **PagerTemplate.**

## <a name="customizing-the-user-interface"></a>Personalizando a interface do usuário

Você pode personalizar a aparência do controle FormView definindo as propriedades de estilo para as diferentes partes do controle. A tabela a seguir lista as diferentes propriedades de estilo.

| **Propriedade de estilo** | **Descrição** |
| --- | --- |
| Editrowstyle | As configurações de estilo para a linha de dados quando o controle FormView está no modo de edição. |
| Emptydatarowstyle | As configurações de estilo para a linha de dados vazia exibida no controle FormView quando a fonte de dados não contém registros. |
| Footerstyle | As configurações de estilo para a linha de rodapé do controle FormView. |
| Headerstyle | As configurações de estilo para a linha de cabeçalho do controle FormView. |
| Insertrowstyle | As configurações de estilo para a linha de dados quando o controle FormView está no modo de inserção. |
| Pagerstyle | As configurações de estilo para a linha pager exibidano controle FormView quando o recurso de paginação está ativado. |
| Rowstyle | As configurações de estilo para a linha de dados quando o controle FormView estiver no modo somente leitura. |

## <a name="events"></a>Eventos

O controle FormView fornece vários eventos contra os que você pode programar. Isso permite que você execute uma rotina personalizada sempre que um evento ocorra. A tabela a seguir lista os eventos suportados pelo controle FormView.

| **Evento** | **Descrição** |
| --- | --- |
| Itemcommand | Ocorre quando um botão dentro de um controle FormView é clicado. Este evento é frequentemente usado para executar uma tarefa quando um botão é clicado no controle. |
| Itemcreated | Ocorre depois que todos os objetos FormViewRow são criados no controle FormView. Este evento é frequentemente usado para modificar os valores de um registro antes de ser exibido. |
| Itemdeleted | Ocorre quando um botão Excluir (um botão com sua propriedade **CommandName** definido como "Excluir") é clicado, mas depois que o controle FormView exclui o registro da fonte de dados. Este evento é frequentemente usado para verificar os resultados da operação de exclusão. |
| Itemdeleting | Ocorre quando um botão Excluir é clicado, mas antes que o controle FormView exclua o registro da fonte de dados. Este evento é frequentemente usado para cancelar a operação de exclusão. |
| Iteminserted | Ocorre quando um botão Inserir (um botão com sua propriedade **CommandName** definido como "Insert") é clicado, mas após o controle FormView insere o registro. Este evento é frequentemente usado para verificar os resultados da operação de inserção. |
| Iteminserting | Ocorre quando um botão Inserir é clicado, mas antes que o controle FormView insira o registro. Este evento é frequentemente usado para cancelar a operação de inserção. |
| Itemupdated | Ocorre quando um botão Atualizar (um botão com sua propriedade **CommandName** definido como "Atualização") é clicado, mas após o controle FormView atualiza a linha. Este evento é frequentemente usado para verificar os resultados da operação de atualização. |
| Itemupdating | Ocorre quando um botão Atualizar é clicado, mas antes que o controle FormView atualize o registro. Este evento é frequentemente usado para cancelar a operação de atualização. |
| Modechanged | Ocorre após os modos de alteração do controle FormView (para editar, inserir ou modo somente leitura). Este evento é frequentemente usado para executar uma tarefa quando o controle FormView muda os modos. |
| Modechanging | Ocorre antes que o modo de alteração do controle FormView (para editar, inserir ou modo somente leitura). Este evento é frequentemente usado para cancelar uma alteração de modo. |
| Pageindexchanged | Ocorre quando um dos botões do pager é clicado, mas depois que o controle FormView lida com a operação de paginação. Este evento é comumente usado quando você precisa executar uma tarefa depois que o usuário navega para um registro diferente no controle. |
| Pageindexchanging | Ocorre quando um dos botões do pager é clicado, mas antes que o controle FormView manuseie a operação de paginação. Este evento é frequentemente usado para cancelar a operação de paginação. |

## <a name="detailsview"></a>Detailsview

O controle DetailsView é usado para exibir um único registro de uma fonte de dados em uma tabela, onde cada campo do registro é exibido em uma linha da tabela. Ele pode ser usado em combinação com um controle GridView para cenários de detalhes mestres. O controle DetailsView suporta os seguintes recursos:

- Vinculação aos controles de origem de dados, como O SqlDataSource.
- Recursos de inserção incorporados.
- Recursos de atualização e exclusão incorporados.
- Recursos de paginação incorporados.
- Acesso programático ao modelo de objeto DetailsVer para definir dinamicamente propriedades, lidar com eventos e assim por diante.
- Aparência personalizável através de temas e estilos.

## <a name="row-fields"></a>Campos de linha

Cada linha de dados no controle DetailsView é criada declarando um controle de campo. Diferentes tipos de campo de linha determinam o comportamento das linhas no controle. Os controles de campo derivam do DataControlField. A tabela a seguir lista os diferentes tipos de campo de linha que podem ser usados.

| **Tipo de campo de coluna** | **Descrição** |
| --- | --- |
| BoundField | Exibe o valor de um campo em uma fonte de dados como texto. |
| ButtonField | Exibe um botão de comando no controle DetailsView. Isso permite que você exiba uma linha com um controle de botão personalizado, como um botão Adicionar ou remover. |
| CheckBoxField | Exibe uma caixa de seleção no controle DetailsView. Este tipo de campo de linha é comumente usado para exibir campos com um valor booleano. |
| CommandField | Exibe botões de comando incorporados para executar operações de edição, inserção ou exclusão no controle DetailsView. |
| HyperLinkField | Exibe o valor de um campo em uma fonte de dados como um hiperlink. Este tipo de campo de linha permite vincular um segundo campo à URL do hiperlink. |
| ImageField | Exibe uma imagem no controle DetailsView. |
| Templatefield | Exibe conteúdo definido pelo usuário para uma linha no controle DetailsView de acordo com um modelo especificado. Este tipo de campo de linha permite que você crie um campo de linha personalizado. |

Por padrão, a propriedade AutoGenerateRows é definida como **true,** que gera automaticamente um objeto de campo de linha vinculado para cada campo de um tipo vinculável na fonte de dados. Os tipos vinculáveis válidos são String, DateTime, Decimal, Guid e o conjunto de tipos primitivos. Cada campo é então exibido em uma linha como texto, na ordem em que cada campo aparece na fonte de dados.

A geração automática das linhas fornece uma maneira rápida e fácil de exibir todos os campos do registro. No entanto, para fazer uso dos recursos avançados do controle DetailsView, você deve declarar explicitamente os campos de linha para incluir no controle DetailsView. Para declarar os campos de linha, primeiro defina a propriedade **AutoGenerateRows** como **falsa**. Em seguida, adicione ** &lt;&gt; ** marcas de abertura e fechamento de Campos entre as tags de abertura e fechamento do controle DetailsView. Por fim, liste os campos de linha que você deseja incluir entre as tags De abertura e fechamento ** &lt;de Campos.&gt; ** Os campos de linha especificados são adicionados à coleção Campos na ordem listada. A coleção **Campos** permite gerenciar programáticamente os campos de linha no controle DetailsView.

> [!NOTE]
> Os campos de linha gerados automaticamente não são adicionados à coleção Campos.

## <a name="binding-to-data"></a>Vinculação a Dados

O controle DetailsView pode ser vinculado a um controle de origem de dados, como **SqlDataSource** ou AccessDataSource, ou a qualquer fonte de dados que implemente a interface System.Collections.IEnumerable, como System.Data.DataView, System.Collections.ArrayList e System.Collections.Hashtable.

Use um dos seguintes métodos para vincular o controle DetailsView ao tipo de origem de dados apropriado:

- Para vincular a um controle de origem de dados, defina a propriedade DataSourceID do controle DetailsView ao valor de ID do controle de origem de dados. O controle DetailsView se liga automaticamente ao controle de origem de dados especificado. Este é o método preferido para vincular aos dados.
- Para vincular a uma fonte de dados que implementa a interface **System.Collections.IEnumerable,** defina programaticamente a propriedade DataSource do controle DetailsView à fonte de dados e, em seguida, chame o método DataBind.

## <a name="security"></a>Segurança

Este controle pode ser usado para exibir a entrada do usuário, o que pode incluir script cliente malicioso. Verifique qualquer informação enviada de um cliente para script executável, declarações SQL ou outro código antes de exibi-la em seu aplicativo. ASP.NET fornece um recurso de validação de solicitação de entrada para bloquear script e HTML na entrada do usuário.

## <a name="data-operations"></a>Operações de dados

O controle DetailsView fornece recursos incorporados que permitem ao usuário atualizar, excluir, inserir e página através de itens no controle. Quando o controle DetailsView está vinculado a um controle de origem de dados, o controle DetailsView pode tirar proveito dos recursos do controle de origem de dados e fornecer funcionalidade de atualização, exclusão, inserção e paginação automática.

O controle DetailsView pode fornecer suporte para operações de atualização, exclusão, inserção e paginação com outros tipos de fontes de dados; no entanto, você deve fornecer a implementação para essas operações em um manipulador de eventos apropriado.

O controle DetailsView pode adicionar automaticamente um campo de linha **CommandField** com um botão Editar, excluir ou Novo, definindo as propriedades AutoGenerateEditButton, AutoGenerateDeleteButton ou AutoGenerateInsertButton para **true,** respectivamente. Ao contrário do botão Excluir (que exclui o registro selecionado imediatamente), quando o botão Editar ou Novo é clicado, o controle DetailsView entra no modo de edição ou inserção, respectivamente. No modo de edição, o botão Editar é substituído por um botão Atualizar e cancelar. Os controles de entrada apropriados para o tipo de dados do campo (como uma TextBox ou um controle CheckBox) são exibidos com o valor de um campo para o usuário modificar. Clicar no botão Atualizar atualiza o registro na fonte de dados, enquanto o botão Cancelar abandona quaisquer alterações. Da mesma forma, no modo de inserção, o botão Novo é substituído por um botão Inserir e um cancelamento, e os controles de entrada vazios são exibidos para que o usuário insira os valores para o novo registro.

O controle DetailsView fornece um recurso de paginação, que permite que o usuário navegue para outros registros na fonte de dados. Quando ativado, os controles de navegação de página são exibidos em uma linha de pager. Para habilitar a paginação, defina a propriedade AllowPaging **como verdadeira**. A linha pager pode ser personalizada usando as propriedades PagerStyle e PagerSettings.

## <a name="customizing-the-user-interface"></a>Personalizando a interface do usuário

Você pode personalizar a aparência do controle DetailsView definindo as propriedades de estilo para as diferentes partes do controle. A tabela a seguir lista as diferentes propriedades de estilo.

| **Propriedade de estilo** | **Descrição** |
| --- | --- |
| Alternatingrowstyle | As configurações de estilo para as linhas de dados alternadas no controle DetailsView. Quando esta propriedade é definida, as linhas de dados são exibidas alternando entre as configurações RowStyle e **alternandoRowStyle.** |
| Commandrowstyle | As configurações de estilo para a linha que contém os botões de comando incorporados no controle DetailsView. |
| Editrowstyle | As configurações de estilo para as linhas de dados quando o controle DetailsView está no modo de edição. |
| Emptydatarowstyle | As configurações de estilo para a linha de dados vazia exibida no controle DetailsView quando a fonte de dados não contém registros. |
| Footerstyle | As configurações de estilo para a linha de rodapé do controle DetailsView. |
| Headerstyle | As configurações de estilo para a linha de cabeçalho do controle DetailsView. |
| Insertrowstyle | As configurações de estilo para as linhas de dados quando o controle DetailsView está no modo de inserção. |
| Pagerstyle | As configurações de estilo para a linha de pager do controle DetailsView. |
| Rowstyle | As configurações de estilo para as linhas de dados no controle DetailsView. Quando a propriedade **AlternatingRowStyle** também é definida, as linhas de dados são exibidas alternando entre as configurações **RowStyle** e **alternandoRowStyle.** |
| Fieldheaderstyle | As configurações de estilo para a coluna de cabeçalho do controle DetailsView. |

## <a name="events"></a>Eventos

O controle DetailsView fornece vários eventos contra os que você pode programar. Isso permite que você execute uma rotina personalizada sempre que um evento ocorra. A tabela a seguir lista os eventos suportados pelo controle DetailsView. O controle DetailsView também herda esses eventos de suas classes base: DataBinding, DataBound, Disposed, Init, Load, PreRender e Render.

| **Evento** | **Descrição** |
| --- | --- |
| Itemcommand | Ocorre quando um botão é clicado no controle DetailsView. |
| Itemcreated | Ocorre depois que todos os objetos DetailsViewRow são criados no controle DetailsView. Este evento é frequentemente usado para modificar os valores de um registro antes de ser exibido. |
| Itemdeleted | Ocorre quando um botão Excluir é clicado, mas após o controle DetailsView exclui o registro da fonte de dados. Este evento é frequentemente usado para verificar os resultados da operação de exclusão. |
| Itemdeleting | Ocorre quando um botão Excluir é clicado, mas antes que o controle DetailsView exclua o registro da fonte de dados. Este evento é frequentemente usado para cancelar a operação de exclusão. |
| Iteminserted | Ocorre quando um botão Inserir é clicado, mas após o controle DetailsView insere o registro. Este evento é frequentemente usado para verificar os resultados da operação de inserção. |
| Iteminserting | Ocorre quando um botão Inserir é clicado, mas antes que o controle DetailsView insira o registro. Este evento é frequentemente usado para cancelar a operação de inserção. |
| Itemupdated | Ocorre quando um botão Atualizar é clicado, mas após o controle DetailsView atualiza a linha. Este evento é frequentemente usado para verificar os resultados da operação de atualização. |
| Itemupdating | Ocorre quando um botão Atualizar é clicado, mas antes que o controle DetailsView atualize o registro. Este evento é frequentemente usado para cancelar a operação de atualização. |
| Modechanged | Ocorre após os modos DetailsExibir alterações de controle (editar, inserir ou modo somente leitura). Este evento é frequentemente usado para executar uma tarefa quando o controle DetailsView altera os modos. |
| Modechanging | Ocorre antes do modo DetailsExibir alterações de controle (editar, inserir ou modo somente leitura). Este evento é frequentemente usado para cancelar uma alteração de modo. |
| Pageindexchanged | Ocorre quando um dos botões do pager é clicado, mas após o controle DetailsView lida com a operação de paginação. Este evento é comumente usado quando você precisa executar uma tarefa depois que o usuário navega para um registro diferente no controle. |
| Pageindexchanging | Ocorre quando um dos botões do pager é clicado, mas antes que o controle DetailsView manuseie a operação de paginação. Este evento é frequentemente usado para cancelar a operação de paginação. |

## <a name="the-menu-control"></a>O Controle de Menu

O controle de menu em ASP.NET 2.0 foi projetado para ser um sistema de navegação completo. Ele pode ser vinculado facilmente a fontes de dados hierárquicas, como o SiteMapDataSource.

Uma estrutura de controles de menu pode ser definida declarativamente ou dinamicamente e consiste em um único nó raiz e qualquer número de sub-nós. O código a seguir define declarativamente um menu para o controle menu.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

No exemplo acima, o nó Home.aspx é o nó raiz. Todos os outros nós estão aninhados dentro do nó raiz em vários níveis.

Existem dois tipos de menus que o controle do Menu pode renderizar; menus estáticos e menus dinâmicos. Os menus estáticos consistem em itens de menu que são sempre visíveis. Os menus dinâmicos consistem em itens de menu que só são visíveis quando o usuário paira sobre eles com o mouse. Os clientes podem muitas vezes confundir menus estáticos com menus definidos declarativamente e menus dinâmicos com menus que são datados vinculados em tempo de execução. De fato, menus dinâmicos e estáticos não estão relacionados ao método populacional. Os termos *estáticos* e *dinâmicos* referem-se apenas a saber se o menu é ou não exibido estáticamente por padrão ou exibido somente quando o usuário toma alguma ação.

A propriedade **StaticDisplayLevels** é usada para configurar quantos níveis do menu são estáticos e, portanto, exibidos por padrão. No exemplo acima, definir a propriedade **StaticDisplayLevels** para um valor de 2 faria com que o menu exibisse estáticamente o nó Home, o nó Música e o nó Filmes. Todos os outros nós seriam exibidos dinamicamente quando o usuário pairasse sobre o nó pai.

A propriedade **MaximumDynamicDisplayLevels** configura o número máximo de níveis dinâmicos que o menu é capaz de exibir. Quaisquer menus dinâmicos em um nível superior ao valor especificado pela propriedade **MaximumDynamicDisplayLevels** são descartados.

> [!NOTE]
> É quase certo que você pode encontrar situações em que os menus não parecem renderizar devido à propriedade MaximumDynamicDisplayLevels. Nesses casos, certifique-se de que a propriedade esteja configurada o suficiente para permitir a exibição dos menus dos clientes.

## <a name="data-binding-the-menu-control"></a>Vinculação de dados ao controle do menu

O controle de menu pode ser vinculado a qualquer fonte de dados hierárquica, como o SiteMapDataSource ou o XMLDataSource. O SiteMapDataSource é o método mais usado para vincular dados a um controle de menu porque ele se alimenta do arquivo Web.sitemap e seu esquema fornece uma API conhecida para o controle do Menu. A listagem abaixo mostra um arquivo web.sitemap simples.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

Observe que há apenas um elemento root siteMapNode, neste caso, o elemento Home. Vários atributos podem ser configurados para cada siteMapNode. Os atributos mais utilizados são:

- **url** Especifica a URL a ser exibida quando um usuário clica no item do menu. Se este atributo não estiver presente, o nó simplesmente postará de volta quando clicado.
- **título** Especifica o texto exibido no item do menu.
- **descrição** Usado como documentação para o nó. Também é exibido como uma dica de ferramenta quando o mouse é pairado sobre o nó.
- **siteMapFile** Permite mapas de site aninhados. Este atributo deve apontar para um arquivo de ASP.NET sitemap bem formado.
- **papéis** Permite que a aparência de um nó seja controlada por ASP.NET corte de segurança.

Observe que, embora esses atributos sejam todos opcionais, o comportamento do menu pode não ser o esperado se eles não forem especificados. Por exemplo, se *o* atributo url for especificado, mas o atributo de *descrição* não for, o nó não será visível e não haverá como navegar até a URL especificada.

## <a name="controlling-a-menus-operation"></a>Controlando uma operação de menus

Existem várias propriedades que afetam o funcionamento de um ASP.NET controle de menu; a propriedade **Orientação,** a propriedade **DisappearAfter,** a propriedade **StaticItemFormatString** e a propriedade **StaticPopoutImageUrl** são apenas algumas delas.

- A **Orientação** pode ser definida como *horizontal* ou *vertical* e controla se os itens do menu estático são colocados horizontalmente em uma linha ou verticalmente e empilhados uns sobre os outros. Esta propriedade não afeta menus dinâmicos.
- A propriedade **DisappearAfter** configura quanto tempo um menu dinâmico deve permanecer visível depois que o mouse for removido dele. O valor é especificado em milissegundos e é padrão para 500. Definir esta propriedade como um valor de -1 fará com que o menu nunca desapareça automaticamente. Nesse caso, o menu só desaparecerá quando o usuário clicar fora do menu.
- A propriedade **StaticItemFormatString** facilita a manutenção de verbiage consistente no sistema de menus. Ao especificar esta *{0}* propriedade, deve ser inserido no lugar da descrição que aparece na fonte de dados. Por exemplo, para que o item do menu do exercício 1 diga Visite {0} nossa página de produtos, etc., você especificaria Visitar nossa página para o StaticItemFormatString. Em tempo de execução, {0} ASP.NET substituirá qualquer ocorrência com a descrição correta para o item do menu.
- A propriedade **StaticPopoutImageUrl** especifica a imagem usada para indicar que um nó de menu específico tem nó de filho que pode ser acessado pairando sobre ele. Os menus dinâmicos continuarão a usar a imagem padrão.

## <a name="templated-menu-controls"></a>Controles de menu modelados

O controle de menu é um controle modelado e permite dois Modelos de Itens diferentes; o StaticItemTemplate e o DynamicItemTemplate. Usando esses modelos, você pode facilmente adicionar controles de servidor ou controles de usuário aos seus menus.

Para editar os modelos no Visual Studio .NET, clique no botão Smart Tag no menu e escolha Editar modelos. Em seguida, você pode escolher entre editar o StaticItemTemplate ou o DynamicItemTemplate.

Quaisquer controles adicionados ao StaticItemTemplate aparecerão no menu estático quando a página for carregada. Quaisquer controles adicionados ao DynamicItemTemplate aparecerão em todos os menus pop-up.

## <a name="menu-events"></a>Eventos do Menu

O controle do Menu tem dois eventos que são exclusivos dele; o **MenuItemClicked** e o evento **MenuItemDatabound.**

O evento MenuItemClicked é levantado quando um item do menu é clicado. O evento MenuItemDatabound é levantado quando um item do menu é vinculado a dados. O **MenuEventArgs** que é passado para o manipulador de eventos fornece acesso ao item do menu através da propriedade Item.

## <a name="controlling-a-menus-appearance"></a>Controlando a aparência de menus

Você também pode afetar a aparência de um controle de menu usando um ou mais dos muitos estilos disponíveis para formatar menus. Entre eles estão **StaticMenuStyle,** **DynamicMenuStyle,** **DynamicMenuItemStyle,** **DynamicSelectedStyle**e **DynamicHoverStyle**. Essas propriedades são configuradas usando uma seqüência padrão de estilo HTML. Por exemplo, o seguinte afetará o estilo para menus dinâmicos.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> Se você estiver usando qualquer um dos estilos Hover, você precisará adicionar &lt;um elemento de cabeça&gt; na página com o elemento *runat* definido para *servidor*.

Os controles de menu também suportam o uso de temas ASP.NET 2.0.

## <a name="the-treeview-control"></a>O controle treeview

O controle TreeView exibe dados em uma estrutura semelhante a uma árvore. Assim como no controle de Menu, ele pode ser facilmente vinculado a qualquer fonte de dados hierárquico, como o SiteMapDataSource.

A primeira pergunta que os clientes provavelmente farão sobre o controle treeview em ASP.NET 2.0 é se ele está ou não relacionado ao TreeView IE WebControl que estava disponível para ASP.NET 1.x. Não, não é. O controle ASP.NET 2.0 TreeView foi gravado do zero e oferece uma melhoria significativa em relação ao IE TreeView WebControl que estava disponível anteriormente.

Não entrarei em detalhes sobre como vincular um controle TreeView a um mapa do site, pois ele é realizado exatamente da mesma maneira que o controle do Menu. No entanto, o controle TreeView tem algumas diferenças distintas na maneira como ele opera.

Por padrão, um controle TreeView aparece totalmente expandido. Para alterar o nível de expansão na carga inicial, modifique a propriedade **ExpandDepth** do controle. Isso é particularmente importante nos casos em que o TreeView é vinculado a dados ao expandir determinados nódulos.

## <a name="databinding-the-treeview-control"></a>Vinculando os dados do controle treeview

Ao contrário do controle de menu, o TreeView se presta bem ao manuseio de grandes quantidades de dados. Portanto, além da vinculação de dados a um SiteMapDataSource ou XMLDataSource, o TreeView é frequentemente vinculado a um DataSet ou a outros dados relacionais. Nos casos em que o controle TreeView está vinculado a grandes quantidades de dados, é melhor vincular-se apenas a dados que são realmente visíveis no controle. Em seguida, os dados se vinculam a dados adicionais à medida que os nós do TreeView são expandidos.

Nestes casos, a propriedade **PopulateOnDemand** do TreeView deve ser definida como *true*. Em seguida, você precisará fornecer uma implementação para o método **TreeNodePopulate.**

## <a name="data-binding-without-postback"></a>Vinculação de dados sem pós-volta

Observe que quando você expande um nó no exemplo anterior pela primeira vez, a página é posta de volta e atualiza. Isso não é um problema neste exemplo, mas você pode imaginar que ele pode estar em um ambiente de produção com uma grande quantidade de dados. Um cenário melhor seria aquele em que o TreeView ainda preencheria dinamicamente seus nós, mas sem um post de volta ao servidor.

Ao definir as **propriedades PopulateNodeclient** e as propriedades **PopulateOnDemand** como true, o controle ASP.NET TreeView preencherá dinaticamente os nós sem um post back. Quando o nó pai é expandido, uma solicitação XMLHttp é feita do cliente e o evento OnTreeNodePopulate é acionado. O servidor responde com uma ilha de dados XML que é usada para vincular os nós de criança.

ASP.NET cria dinamicamente o código do cliente que implementa essa funcionalidade. As &lt;&gt; tags de script que contêm o script são geradas apontando para um arquivo AXD. Por exemplo, a listagem abaixo mostra os links de script para o código de script que gera a solicitação XMLHttp.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

Se você navegar pelo arquivo AXD acima no seu navegador e abri-lo, você verá o código que implementa a solicitação XMLHttp. Este método impede que os clientes modifiquem o arquivo de script.

## <a name="controlling-the-operation-of-the-treeview-control"></a>Controlando a operação do controle treeview

O controle TreeView tem várias propriedades que afetam o funcionamento do controle. As propriedades mais óbvias são as **ShowCheckBoxes,** **ShowExpandCollapse**e **ShowLines**.

A propriedade **ShowCheckBoxes** afeta se os nós exibem ou não uma caixa de seleção quando renderizados. Os valores válidos para esta propriedade são **Nenhum,** **Raiz,** **Pai,** **Folha**e **Todos**. Isso afeta o controle treeview da seguinte forma:

| **Valor da propriedade** | **Efeito** |
| --- | --- |
| Nenhum | As caixas de seleção não são exibidas em nenhum nó. Essa é a configuração padrão. |
| Root | Uma caixa de seleção só é exibida no nó raiz. |
| Pai | Uma caixa de seleção só é exibida nesses nódulos que têm nódulos infantis. Esses nódulos infantis podem ser nódulos dos pais ou nódulos de folhas. |
| Folha | Uma caixa de seleção é exibida apenas naqueles nódulos que não têm nó infantil. |
| Todos | Uma caixa de seleção é exibida em todos os nós. |

Quando as caixas de seleção estiverem sendo usadas, a propriedade **CheckNodes** devolverá uma coleção de nós do TreeView que são verificados após o postback.

A propriedade **ShowExpandCollapse** controla o aparecimento da imagem expande/colapso ao lado de nós raiz e pai. Se esta propriedade for definida como **falsa,** os nós treeview serão renderizados como hiperlinks e serão expandidos/colapsados clicando no link.

A propriedade **ShowLines** controla se as linhas são exibidas ou não conectando nós-pai a nós de filho. Quando **falso** (o padrão), nenhuma linha é exibida. Quando **verdadeiro,** o controle TreeView usará imagens de linhas na pasta especificada pela propriedade **LineImagesFolder.**

Para personalizar a aparência das linhas TreeView, o Visual Studio .NET 2005 inclui uma ferramenta de Line Designer. Você pode acessar esta ferramenta usando o botão Smart Tag no controle TreeView como abaixo.

![](data-bound-controls/_static/image1.jpg)

**Figura 1**

Ao selecionar a opção **Personalizar imagens de linha,** a ferramenta 'Designer de linhas' será lançada permitindo que você configure a aparência das linhas TreeView.

## <a name="treeview-events"></a>Eventos TreeView

O controle TreeView tem os seguintes eventos exclusivos:

- SelectedNodeChanged Ocorre quando um nó é selecionado com base na propriedade **SelectAction.**
- TreeNodeCheckChanged Ocorre quando um estado de caixa de seleção de nós é alterado.
- TreeNodeExpanded Ocorre quando um nó é expandido com base na propriedade **SelectAction.**
- TreeNodeCollapsed ocorre quando um nó é colapsado.
- TreeNodeDataBound Ocorre quando um nó está vinculado a dados.
- TreeNodePopulate Ocorre quando um nó é preenchido.

A propriedade **SelectAction** permite configurar qual evento é acionado quando um nó é selecionado. A propriedade SelectAction fornece as seguintes ações:

- TreeNodeSelectAction.Expand Raises TreeNodeExpanded when the node is selected.
- TreeNodeSelectAction.None Não levanta nenhum evento quando o nó é selecionado.
- TreeNodeSelectAction.Select Levanta o evento SelectedNodeChanged quando o nó é selecionado.
- TreeNodeSelectAction.SelectExpand Eleva o evento SelectedNodeChanged e o evento TreeNodeExpanded quando o nó é selecionado.

## <a name="controlling-appearance-with-styles"></a>Controlando a aparência com estilos

O controle TreeView fornece muitas propriedades para controlar a aparência do controle com estilos. As propriedades a seguir estão disponíveis.

| **Nome da propriedade** | **Controles** |
| --- | --- |
| Hovernodestyle | Controla o estilo dos nódulos quando o mouse é pairado sobre eles. |
| Leafnodestyle | Controla o estilo dos nódulos de folha. |
| Nodestyle | Controla o estilo para todos os nós. Estilos específicos de nó (como LeafNodeStyle) sobrepõem este estilo. |
| Parentnodestyle | Controla o estilo para todos os nós pais. |
| Rootnodestyle | Controla o estilo para o nó raiz. |
| Selectednodestyle | Controla o estilo para o nó selecionado. |

Cada uma dessas propriedades é somente leitura. No entanto, cada um deles retornará um objeto **TreeNodeStyle,** e as propriedades desse objeto podem ser modificadas usando o formato *de subpropriedade de propriedade.* Por exemplo, para definir a propriedade **ForeColor** do **SelectedNodeStyle,** você usaria a seguinte sintaxe:

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

Observe que a tag acima não está fechada. Isso porque ao usar a sintaxe declarativa mostrada aqui, você incluiria os nós treeviews no código HTML também.

As propriedades de estilo também podem ser especificadas em código usando o formato *property.subproperty.* Por exemplo, para definir a propriedade **ForeColor** do **RootNodeStyle** em código, você usaria a seguinte sintaxe:

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> Para obter uma lista abrangente das diferentes propriedades de estilo, consulte a documentação do MSDN no objeto TreeNodeStyle.

## <a name="the-sitemappath-control"></a>O controle sitemappath

O controle SiteMapPath fornece um controle de navegação de migalhas de pão para desenvolvedores ASP.NET. Como os outros controles de navegação, ele pode ser facilmente vinculado a dados hierárquicos, como o SiteMapDataSource ou xmlDataSource.

Um controle siteMapPath é composto por objetos SiteMapNodeItem. Existem três tipos de nós; o nó Raiz, os nós pai e o nó Corrente. O nó raiz é o nó no topo da estrutura hierárquica. O nó atual representa a página atual. Todos os outros nós são nós-mãe.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>Controlando a operação do Controle siteMapPath

As propriedades que controlam a operação do controle siteMapPath são as seguintes:

| **Propriedade** | **Descrição da Propriedade** |
| --- | --- |
| Níveis dos paisexibidos | Controla quantos nós-pais são exibidos. O padrão é -1, que não impõe nenhuma restrição ao número de nós-pai exibidos. |
| Pathdirection | Controla a direção do SiteMapPath. Os valores válidos são RootToCurrent (default) e CurrentToRoot. |
| Pathseparator | Uma string que controla o caractere que separa os números em um controle siteMapPath. O valor padrão é :. |
| Rendercurrentnodeaslink | Um valor booleano que controla se o nó atual é ou não renderizado como um link. O padrão é False. |
| Skiplinktext | Auxilia com acessibilidade quando a página é visualizada pelos leitores de tela. Esta propriedade permite que os leitores de tela pulem o controle siteMapPath. Para desativar esse recurso, defina a propriedade como String.Empty. |

## <a name="templated-sitemappath-controls"></a>Controles siteMapPath modelados

O SiteMapControl é um controle de modelos e, como tal, você pode definir diferentes modelos para usar na exibição do controle. Para editar modelos em um controle siteMapPath, clique no botão Smart Tag no controle e escolha Editar modelos no menu. Isso exibe o menu SiteMapTasks como mostrado abaixo, onde você pode escolher entre os diferentes modelos disponíveis.

![](data-bound-controls/_static/image2.jpg)

**Figura 2**

O **modelo NodeTemplate** refere-se a qualquer nó no SiteMapPath. Se o nó for um nó raiz ou o nó atual e um **RootNodeTemplate** ou **CurrentNodeTemplate** estiver configurado, o NodeTemplate será substituído.

## <a name="sitemappath-events"></a>Eventos siteMapPath

O controle SiteMapPath tem dois eventos que não são derivados da classe Controle; o evento **ItemCreated** e o evento **ItemDataBound.** O evento ItemCreated é levantado quando um item siteMapPath é criado. O ItemDataBound é levantado quando o método DataBind é chamado durante a vinculação de dados de um nó SiteMapPath. Um objeto **SiteMapNodeemEventArgs** fornece acesso ao SiteMapNodeItem específico através da propriedade Item.

## <a name="controlling-appearance-with-styles"></a>Controlando a aparência com estilos

Os seguintes estilos estão disponíveis para formatação de um controle SiteMapPath.

| **Nome da propriedade** | **Controles** |
| --- | --- |
| Currentnodestyle | Controla o estilo do texto para o nó atual. |
| Rootnodestyle | Controla o estilo do texto para o nó raiz. |
| Nodestyle | Controla o estilo do texto para todos os nós assumindo que um CurrentNodeStyle ou RootNodeStyle não se aplica. |

A propriedade NodeStyle é substituída pelo CurrentNodeStyle ou pelo RootNodeStyle. Cada uma dessas propriedades é somente leitura e retorna um objeto **Estilo.** Para afetar o aparecimento de um nó usando uma dessas propriedades, você precisará definir as propriedades do objeto Estilo que é devolvido. Por exemplo, o código abaixo altera a propriedade forecolor do nó atual.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

A propriedade também pode ser aplicada de forma programática da seguinte forma:

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> Se um modelo for aplicado, o estilo não será aplicado.

## <a name="lab-1-configuring-an-aspnet-menu-control"></a>Laboratório 1: Configuração de um controle de menu ASP.NET

1. Crie um novo site.
2. Adicione um arquivo mapa do site selecionando Arquivo, Novo, Arquivo e escolhendo Mapa do Site na lista de modelos de arquivos.
3. Abra o mapa do site (Web.sitemap por padrão) e modifique-o para que ele se pareça com a listagem abaixo. As páginas às quais você está vinculando no arquivo do mapa do site realmente não existem, mas isso não será um problema para este exercício.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. Abra o formulário web padrão na exibição Design.
5. Na seção Navegação da Caixa de ferramentas, adicione um novo controle de menu à página.
6. Na seção Dados da Caixa de Ferramentas, adicione um novo SiteMapDataSource. O SiteMapDataSource usará automaticamente o arquivo Web.sitemap em seu site. (O arquivo Web.sitemap *deve* estar na pasta raiz do site.)
7. Clique no controle menu e clique no botão Marcação inteligente para exibir a caixa de diálogo 'Tarefas do menu'.
8. Na parada Escolher a fonte de dados, selecione SiteMapDataSource1.
9. Clique no link AutoFormat e escolha um formato para o Menu.
10. No painel Propriedades, defina a propriedade **StaticDisplayLevels** como 2. O controle do menu deve agora exibir o nó Casa, Produtos e Serviços no Designer.
11. Navegue pela página no seu navegador para usar o menu. (Como as páginas adicionadas ao mapa do site não existem de fato, você verá um erro ao tentar navegar até elas.)

Experimente alterar as propriedades StaticDisplayLevels e MaximumDynamicDisplayLevels e veja como elas afetam a forma como o menu é renderizado.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>Laboratório 2: Vinculando dinamicamente um controle treeview

Este exercício pressupõe que você tenha o SQL Server em execução local e que o banco de dados Northwind esteja presente na instância do SQL Server. Se essas condições não forem atendidas, altere a seqüência de conexão na amostra. Observe que você também pode precisar especificar a autenticação do SQL Server em vez de uma conexão confiável.

1. Crie um novo site.
2. Alterne para exibição Código para Default.aspx e substitua todo o código pelo código listado abaixo. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. Salve a página como treeview.aspx.
4. Navegue pela página.
5. Quando a página for exibida pela primeira vez, visualize a fonte da página no seu navegador. Note que apenas os nódulos visíveis foram enviados ao cliente.
6. Clique no sinal de mais ao lado de qualquer nó.
7. Ver fonte na página novamente. Observe que os nós recém-exibidos estão agora presentes.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>Laboratório 3: Detalhes Visualização e edição de dados usando uma visão de rede e detalhesVer

1. Crie um novo site.
2. Adicione uma nova web.config ao site da Web.
3. Adicione uma seqüência de conexões ao arquivo Web.config, conforme mostrado abaixo: 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > Você pode precisar alterar a seqüência de conexões com base no seu ambiente.
4. Salvar e fechar o arquivo web.config.
5. Abra Default.aspx e adicione um novo controle SqlDataSource.
6. Alterar o ID do controle SqlDataSource para **Produtos**.
7. No menu **SqlDataSource Tasks,** clique **em Configurar origem de dados**.
8. Selecione **Northwind** na parada de conexão e clique em Avançar.
9. Selecione **produtos** na lista de **seleção Nome** e verifique as caixas de seleção **ProductID,** **ProductName,** **UnitPrice**e **UnitsInStock,** conforme mostrado abaixo. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. Clique em **Próximo**.
11. Clique em **Concluir**.
12. Mude para exibição origem e examine o código gerado. Observe o **SelectCommand,** **DeleteCommand,** **InsertCommand**e **UpdateCommand** que foram adicionados ao controle SqlDataSource. Observe também os parâmetros que foram adicionados.
13. Mude para exibição Design e adicione um novo controle GridView à página.
14. Selecione **Produtos** na gota **De saque da fonte de dados** escolhida.
15. Verifique **Ativar a paginação** e **habilitar a seleção** conforme mostrado abaixo. 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. Clique no link **Editar colunas** e **certifique-se de** que os campos de geração automática sejam verificados.
17. Clique em **OK**.
18. Com o controle GridView selecionado, clique no botão ao lado da propriedade **DataKeyNames** no painel Propriedades.
19. Selecione **ProductID** na lista de **&gt;** campos de dados **disponíveis** e clique no botão para adicioná-lo.
20. Clique em OK.
21. Adicione um novo controle SqlDataSource à página.
22. Alterar o ID do controle SqlDataSource para **Detalhes**.
23. No menu SqlDataSource Tasks, escolha **Configurar origem de dados**.
24. Escolha **Northwind** no dropdown e clique **em Next**.
25. Selecione <strong>Produtos</strong> na lista de <strong> \<itens de entrada <strong>nome</strong> e verifique a caixa de seleção>* forte na caixa de lista <strong>Colunas.</strong>
26. Clique no botão **WHERE.**
27. Selecione **ProductID** **na** coluna de isento.
28. Selecione **=** na estada operadora.
29. Selecione **Controle** **na** gota de origem.
30. Selecione **GridView1** na ida de **controle.**
31. Clique no botão **Adicionar** para adicionar a cláusula WHERE.
32. Clique em **OK**.
33. Clique no botão **Avançado** e verifique a caixa de seleção **Gerar inserir, ATUALIZAR e excluir declarações.**
34. Clique em **OK**.
35. Clique **em "Avançar"** e clique **em Terminar**.
36. Adicionar um controle DetailsExibir à página.
37. Na gota **de código** de dados escolhida, escolha **Detalhes**.
38. Verifique a **caixa de seleção Ativar edição** como mostrado abaixo. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. Salve a página e navegue em Default.aspx.
40. Clique no link **Selecionar** ao lado de diferentes registros para ver a atualização DetailsView automaticamente.
41. Clique no link **Editar** no controle DetailsView.
42. Faça uma alteração no registro e clique **em Atualizar**.
