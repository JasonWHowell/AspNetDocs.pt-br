---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
title: Paginar com eficiência por meio de grandes quantidades de dados (VB) | Microsoft Docs
author: rick-anderson
description: A opção de paginação padrão de um controle de apresentação de dados é inadequada ao trabalhar com grandes quantidades de dados, como sua recuperação de controle de fonte de dados subjacente...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 3e20e64a-8808-4b49-88d6-014e2629d56f
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
msc.type: authoredcontent
ms.openlocfilehash: d1c49e076e1c78e584f91fe2357a98da321f4260
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045098"
---
# <a name="efficiently-paging-through-large-amounts-of-data-vb"></a>Paginação de grandes quantidades de dados com eficiência (VB)

por [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Baixar o aplicativo de exemplo](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_VB.exe) ou [baixar PDF](efficiently-paging-through-large-amounts-of-data-vb/_static/datatutorial25vb1.pdf)

> A opção de paginação padrão de um controle de apresentação de dados é inadequada ao trabalhar com grandes quantidades de dados, pois seu controle de fonte de dados subjacente recupera todos os registros, mesmo que apenas um subconjunto de dados seja exibido. Em tais circunstâncias, devemos reativar a paginação personalizada.

## <a name="introduction"></a>Introdução

Como discutimos no tutorial anterior, a paginação pode ser implementada de uma das duas maneiras:

- A **paginação padrão** pode ser implementada simplesmente marcando a opção habilitar paginação na marca inteligente s do controle da Web de dados; no entanto, sempre que exibir uma página de dados, o ObjectDataSource recupera *todos* os registros, embora apenas um subconjunto deles seja exibido na página
- A **paginação personalizada** melhora o desempenho da paginação padrão, recuperando somente os registros do banco de dados que precisam ser exibidos para a página específica do dado solicitado pelo usuário; no entanto, a paginação personalizada envolve um pouco mais de esforço para implementar que a paginação padrão

Devido à facilidade de implementação, basta marcar uma caixa de seleção e pronto! a paginação padrão é uma opção atraente. Sua abordagem ingênua na recuperação de todos os registros, no entanto, o torna uma opção insatisfatória ao paginar por quantidades de dados suficientemente grandes ou para sites com muitos usuários simultâneos. Em tais circunstâncias, devemos reativar a paginação personalizada para fornecer um sistema responsivo.

O desafio da paginação personalizada é a capacidade de escrever uma consulta que retorna o conjunto preciso de registros necessários para uma determinada página de dados. Felizmente, Microsoft SQL Server 2005 fornece uma nova palavra-chave para classificar resultados, que nos permite escrever uma consulta que pode recuperar com eficiência o subconjunto apropriado de registros. Neste tutorial, veremos como usar essa nova palavra-chave SQL Server 2005 para implementar a paginação personalizada em um controle GridView. Embora a interface do usuário para paginação personalizada seja idêntica à de paginação padrão, a depuração de uma página para a próxima usando a paginação personalizada pode ser várias ordens de magnitude mais rápido que a paginação padrão.

> [!NOTE]
> O lucro de desempenho exato exibido por paginação personalizada depende do número total de registros sendo paginados e da carga que está sendo colocada no servidor de banco de dados. No final deste tutorial, veremos algumas métricas aproximadas que demonstram os benefícios no desempenho obtido por meio de paginação personalizada.

## <a name="step-1-understanding-the-custom-paging-process"></a>Etapa 1: Noções básicas sobre o processo de paginação personalizada

Ao paginar por meio de dados, os registros precisos exibidos em uma página dependem da página de dados que estão sendo solicitadas e do número de registros exibidos por página. Por exemplo, imagine que queríamos paginar os produtos 81, exibindo 10 produtos por página. Ao exibir a primeira página, nós d desejamos produtos de 1 a 10; ao exibir a segunda página, temos interesse nos produtos 11 a 20 e assim por diante.

Há três variáveis que ditam quais registros precisam ser recuperados e como a interface de paginação deve ser renderizada:

- **Iniciar índice de linha** o índice da primeira linha na página de dados a ser exibida; Esse índice pode ser calculado multiplicando-se o índice da página pelos registros a serem exibidos por página e adicionando um. Por exemplo, ao paginar por meio de registros 10 por vez, para a primeira página (cujo índice de página é 0), o índice de linha inicial é 0 \* 10 + 1, ou 1; para a segunda página (cujo índice de página é 1), o índice de linha inicial é 1 \* 10 + 1 ou 11.
- **Máximo de linhas** o número máximo de registros a serem exibidos por página. Essa variável é conhecida como máximo de linhas desde a última página pode haver menos registros retornados do que o tamanho da página. Por exemplo, ao paginar por meio de 81 produtos 10 registros por página, a nona e a última página terão apenas um registro. Nenhuma página, no entanto, mostrará mais registros do que o valor máximo de linhas.
- **Contagem** de registros total o número total de registros que estão sendo paginados. Embora essa variável não seja necessária para determinar quais registros recuperar para uma determinada página, ele dita a interface de paginação. Por exemplo, se houver 81 produtos sendo paginados, a interface de paginação saberá exibir nove números de página na interface do usuário de paginação.

Com a paginação padrão, o índice de linha inicial é calculado como o produto do índice de página e o tamanho da página, mais um, enquanto o máximo de linhas é simplesmente o tamanho da página. Uma vez que a paginação padrão recupera todos os registros do banco de dados durante a renderização de qualquer página, o índice de cada linha é conhecido, tornando a mudança para a linha de índice de linha inicial uma tarefa trivial. Além disso, a contagem total de registros está prontamente disponível, pois s simplesmente o número de registros na DataTable (ou qualquer objeto que esteja sendo usado para manter os resultados do banco de dados).

Dadas as variáveis de índice de linha inicial e máximo de linhas, uma implementação de paginação personalizada deve retornar apenas o subconjunto preciso de registros começando no índice de linha inicial e até o número máximo de linhas de registros depois disso. A paginação personalizada fornece dois desafios:

- Devemos ser capazes de associar com eficiência um índice de linha a cada linha em todos os dados que são paginados por meio de forma que possamos começar a retornar registros no índice de linha inicial especificado
- Precisamos fornecer o número total de registros sendo paginados

Nas próximas duas etapas, examinaremos o script SQL necessário para responder a esses dois desafios. Além do script SQL, também precisaremos implementar métodos na DAL e na BLL.

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>Etapa 2: retornando o número total de registros sendo paginados por

Antes de examinarmos como recuperar o subconjunto preciso de registros para a página que está sendo exibida, vamos primeiro examinar como retornar o número total de registros sendo paginados. Essas informações são necessárias para configurar corretamente a interface do usuário de paginação. O número total de registros retornados por uma consulta SQL específica pode ser obtido usando a [ `COUNT` função de agregação](https://msdn.microsoft.com/library/ms175997.aspx). Por exemplo, para determinar o número total de registros na `Products` tabela, podemos usar a seguinte consulta:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample1.sql)]

Vamos adicionar um método à nossa DAL que retorna essas informações. Em particular, criaremos um método DAL chamado `TotalNumberOfProducts()` que executa a `SELECT` instrução mostrada acima.

Comece abrindo o `Northwind.xsd` arquivo dataset tipado na `App_Code/DAL` pasta. Em seguida, clique com o botão direito do mouse em `ProductsTableAdapter` no designer e escolha Adicionar consulta. Como vimos nos tutoriais anteriores, isso nos permitirá adicionar um novo método à DAL que, quando invocada, executará uma instrução SQL específica ou um procedimento armazenado. Assim como acontece com nossos métodos do TableAdapter nos tutoriais anteriores, para esta opção usar uma instrução SQL ad hoc.

![Usar uma instrução SQL ad hoc](efficiently-paging-through-large-amounts-of-data-vb/_static/image1.png)

**Figura 1**: usar uma instrução SQL ad hoc

Na próxima tela, podemos especificar o tipo de consulta a ser criado. Como essa consulta retornará um único valor escalar, o número total de registros na `Products` tabela escolha o `SELECT` que retorna uma opção de valor individual.

![Configurar a consulta para usar uma instrução SELECT que retorna um único valor](efficiently-paging-through-large-amounts-of-data-vb/_static/image2.png)

**Figura 2**: configurar a consulta para usar uma instrução SELECT que retorna um único valor

Depois de indicar o tipo de consulta a ser usado, devemos especificar a consulta.

![Usar a consulta Selecionar contagem (*) de produtos](efficiently-paging-through-large-amounts-of-data-vb/_static/image3.png)

**Figura 3**: usar a consulta Selecionar contagem ( \* ) de produtos

Por fim, especifique o nome para o método. Como mencionado anteriormente, vamos usar `TotalNumberOfProducts` .

![Nomeie o método DAL TotalNumberOfProducts](efficiently-paging-through-large-amounts-of-data-vb/_static/image4.png)

**Figura 4**: nomear o método Dal TotalNumberOfProducts

Depois de clicar em concluir, o assistente adicionará o `TotalNumberOfProducts` método à Dal. Os métodos de retorno escalares na DAL retornam tipos anuláveis, caso o resultado da consulta SQL seja `NULL` . Nossa `COUNT` consulta, no entanto, sempre retornará um `NULL` valor diferente; independentemente do método Dal retornar um inteiro anulável.

Além do método DAL, também precisamos de um método na BLL. Abra o `ProductsBLL` arquivo de classe e adicione um `TotalNumberOfProducts` método que simplesmente chame para o método da Dal s `TotalNumberOfProducts` :

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample2.vb)]

O método s DAL `TotalNumberOfProducts` retorna um inteiro anulável; no entanto, criamos o `ProductsBLL` método Class s `TotalNumberOfProducts` para que ele retorne um número inteiro padrão. Portanto, precisamos que o método da `ProductsBLL` classe s `TotalNumberOfProducts` retorne a parte do valor do inteiro anulável retornado pelo método da Dal s `TotalNumberOfProducts` . A chamada para `GetValueOrDefault()` retorna o valor do inteiro anulável, se existir; se o inteiro anulável for `null` , no entanto, ele retornará o valor inteiro padrão, 0.

## <a name="step-3-returning-the-precise-subset-of-records"></a>Etapa 3: retornando o subconjunto preciso de registros

Nossa próxima tarefa é criar métodos na DAL e na BLL que aceitem as variáveis de índice de linha inicial e máximo de linhas discutidas anteriormente e retornam os registros apropriados. Antes de fazermos isso, vamos examinar primeiro o script SQL necessário. O desafio voltado para nós é que devemos ser capazes de atribuir com eficiência um índice a cada linha em que os resultados inteiros fossem paginados para que possamos retornar apenas os registros que começam no índice de linha inicial (e até o número máximo de registros de registros).

Isso não é um desafio se já houver uma coluna na tabela de banco de dados que serve como um índice de linha. À primeira vista, podemos imaginar que o `Products` campo s da tabela `ProductID` seria suficiente, pois o primeiro produto tem `ProductID` de 1, a segunda 2 e assim por diante. No entanto, a exclusão de um produto deixa uma lacuna na sequência, anulando essa abordagem.

Há duas técnicas gerais usadas para associar com eficiência um índice de linha com os dados a serem paginados, habilitando assim o subconjunto preciso de registros a serem recuperados:

- **Usando SQL Server 2005 s `ROW_NUMBER()` Palavra-chave** New para SQL Server 2005, a `ROW_NUMBER()` palavra-chave associa uma classificação a cada registro retornado com base em alguma ordenação. Essa classificação pode ser usada como um índice de linha para cada linha.
- **Usando uma variável de tabela `SET ROWCOUNT` e** A [ `SET ROWCOUNT` instrução](https://msdn.microsoft.com/library/ms188774.aspx) SQL Server s pode ser usada para especificar quantos registros totais uma consulta deve processar antes de terminar; [variáveis de tabela](http://www.sqlteam.com/item.asp?ItemID=9454) são variáveis T-SQL locais que podem conter dados tabulares, semelhante a [tabelas temporárias](http://www.sqlteam.com/item.asp?ItemID=2029). Essa abordagem funciona igualmente bem com Microsoft SQL Server 2005 e SQL Server 2000 (enquanto a `ROW_NUMBER()` abordagem só funciona com SQL Server 2005).  
  
  A ideia aqui é criar uma variável de tabela que tenha uma `IDENTITY` coluna e colunas para as chaves primárias da tabela cujos dados estão sendo paginados. Em seguida, o conteúdo da tabela cujos dados estão sendo paginados é despejado na variável de tabela, associando assim um índice de linha sequencial (por meio da `IDENTITY` coluna) para cada registro na tabela. Depois que a variável de tabela tiver sido populada, uma `SELECT` instrução na variável de tabela, unida à tabela subjacente, poderá ser executada para extrair os registros específicos. A `SET ROWCOUNT` instrução é usada para limitar de forma inteligente o número de registros que precisam ser despejados na variável de tabela.  
  
  Essa abordagem de eficiência é baseada no número de página que está sendo solicitado, uma vez que o valor `SET ROWCOUNT` é atribuído ao valor de índice de linha inicial mais o máximo de linhas. Ao paginar por meio de páginas de menor número, como as primeiras páginas de dados, essa abordagem é muito eficiente. No entanto, ele exibe o desempenho padrão como paginação ao recuperar uma página próxima ao final.

Este tutorial implementa a paginação personalizada usando a `ROW_NUMBER()` palavra-chave. Para obter mais informações sobre como usar a variável e a técnica de tabela `SET ROWCOUNT` , consulte [um método mais eficiente para paginar por meio de grandes conjuntos de resultados](http://www.4guysfromrolla.com/webtech/042606-1.shtml).

A `ROW_NUMBER()` palavra-chave associada a uma classificação com cada registro retornado em uma ordem específica usando a seguinte sintaxe:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample3.sql)]

`ROW_NUMBER()` Retorna um valor numérico que especifica a classificação de cada registro com relação à ordenação indicada. Por exemplo, para ver a classificação de cada produto, ordenada do mais caro para o menos, poderíamos usar a seguinte consulta:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample4.sql)]

A Figura 5 mostra esses resultados da consulta quando executados por meio da janela de consulta no Visual Studio. Observe que os produtos são ordenados por preço, juntamente com uma classificação de preço para cada linha.

![A classificação de preço está incluída para cada registro retornado](efficiently-paging-through-large-amounts-of-data-vb/_static/image5.png)

**Figura 5**: a classificação de preço é incluída para cada registro retornado

> [!NOTE]
> `ROW_NUMBER()` é apenas uma das muitas funções de classificação novas disponíveis no SQL Server 2005. Para obter uma discussão mais completa sobre `ROW_NUMBER()` o, juntamente com outras funções de classificação, leia [retornando resultados classificados com Microsoft SQL Server 2005](http://www.4guysfromrolla.com/webtech/010406-1.shtml).

Ao ordenar os resultados pela `ORDER BY` coluna especificada na `OVER` cláusula ( `UnitPrice` , no exemplo acima), SQL Server deve classificar os resultados. Essa é uma operação rápida se houver um índice clusterizado sobre as colunas em que os resultados estão sendo ordenados ou se houver um índice de cobertura, mas pode ser mais dispendioso do contrário. Para ajudar a melhorar o desempenho de consultas grandes o suficiente, considere adicionar um índice não clusterizado à coluna pela qual os resultados são ordenados. Consulte [classificando funções e desempenho no SQL Server 2005](http://www.sql-server-performance.com/ak_ranking_functions.asp) para obter uma visão mais detalhada das considerações sobre desempenho.

As informações de classificação retornadas pelo `ROW_NUMBER()` não podem ser usadas diretamente na `WHERE` cláusula. No entanto, uma tabela derivada pode ser usada para retornar o `ROW_NUMBER()` resultado, que pode aparecer na `WHERE` cláusula. Por exemplo, a consulta a seguir usa uma tabela derivada para retornar as colunas NomeDoProduto e UnitPrice, juntamente com o `ROW_NUMBER()` resultado, e, em seguida, usa uma `WHERE` cláusula para retornar apenas os produtos cuja classificação de preço esteja entre 11 e 20:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample5.sql)]

Ampliando esse conceito um pouco mais, podemos utilizar essa abordagem para recuperar uma página específica de dados de acordo com o índice de linha de início desejado e os valores máximos de linhas:

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample6.html)]

> [!NOTE]
> Como veremos mais adiante neste tutorial, o *`StartRowIndex`* fornecido pelo ObjectDataSource é indexado a partir de zero, enquanto o `ROW_NUMBER()` valor retornado pelo SQL Server 2005 é indexado a partir de 1. Portanto, a `WHERE` cláusula retorna os registros onde `PriceRank` é estritamente maior que *`StartRowIndex`* e menor ou igual a *`StartRowIndex`*  +  *`MaximumRows`* .

Agora que vimos como `ROW_NUMBER()` o pode ser usado para recuperar uma determinada página de dados de acordo com os valores de índice de linha inicial e máximo de linhas, agora precisamos implementar essa lógica como métodos na Dal e na BLL.

Ao criar essa consulta, devemos decidir a ordenação pela qual os resultados serão classificados; Vamos classificar os produtos por seu nome em ordem alfabética. Isso significa que, com a implementação de paginação personalizada neste tutorial, não será possível criar um relatório paginado personalizado do que também possa ser classificado. No entanto, no próximo tutorial, veremos como essa funcionalidade pode ser fornecida.

Na seção anterior, criamos o método DAL como uma instrução SQL ad hoc. Infelizmente, o analisador T-SQL no Visual Studio usado pelo assistente TableAdapter não gosta da `OVER` sintaxe usada pela `ROW_NUMBER()` função. Portanto, devemos criar esse método DAL como um procedimento armazenado. Selecione o Gerenciador de Servidores no menu Exibir (ou pressione CTRL + ALT + S) e expanda o `NORTHWND.MDF` nó. Para adicionar um novo procedimento armazenado, clique com o botão direito do mouse no nó procedimentos armazenados e escolha Adicionar um novo procedimento armazenado (consulte a Figura 6).

![Adicionar um novo procedimento armazenado para paginação por meio dos produtos](efficiently-paging-through-large-amounts-of-data-vb/_static/image6.png)

**Figura 6**: adicionar um novo procedimento armazenado para paginação por meio dos produtos

Esse procedimento armazenado deve aceitar dois parâmetros de entrada de inteiro – `@startRowIndex` e `@maximumRows` usar a `ROW_NUMBER()` função ordenada pelo `ProductName` campo, retornando apenas as linhas maiores que o especificado `@startRowIndex` e menor ou igual a `@startRowIndex`  +  `@maximumRow` s. Insira o script a seguir no novo procedimento armazenado e, em seguida, clique no ícone salvar para adicionar o procedimento armazenado ao banco de dados.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample7.sql)]

Depois de criar o procedimento armazenado, Reserve um tempo para testá-lo. Clique com o botão direito do mouse no `GetProductsPaged` nome do procedimento armazenado na Gerenciador de servidores e escolha a opção Executar. O Visual Studio solicitará os parâmetros de entrada e os `@startRowIndex` `@maximumRow` s (consulte a Figura 7). Tente valores diferentes e examine os resultados.

![Insira um valor para os @startRowIndex @maximumRows parâmetros e](efficiently-paging-through-large-amounts-of-data-vb/_static/image7.png)

<strong>Figura 7</strong>: inserir um valor para os @startRowIndex @maximumRows parâmetros e

Depois de escolher esses valores de parâmetros de entrada, a janela de saída mostrará os resultados. A Figura 8 mostra os resultados ao passar 10 para os `@startRowIndex` parâmetros e `@maximumRows` .

[![Os registros que apareceriam na segunda página de dados são retornados](efficiently-paging-through-large-amounts-of-data-vb/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image8.png)

**Figura 8**: os registros que apareceriam na segunda página de dados são retornados ([clique para exibir a imagem em tamanho normal](efficiently-paging-through-large-amounts-of-data-vb/_static/image10.png))

Com esse procedimento armazenado criado, estamos prontos para criar o `ProductsTableAdapter` método. Abra o `Northwind.xsd` dataset tipado, clique com o botão direito do mouse no `ProductsTableAdapter` e escolha a opção Adicionar consulta. Em vez de criar a consulta usando uma instrução SQL ad hoc, crie-a usando um procedimento armazenado existente.

![Criar o método DAL usando um procedimento armazenado existente](efficiently-paging-through-large-amounts-of-data-vb/_static/image11.png)

**Figura 9**: criar o método Dal usando um procedimento armazenado existente

Em seguida, é solicitado que você selecione o procedimento armazenado a ser invocado. Selecione o `GetProductsPaged` procedimento armazenado na lista suspensa.

![Escolha o procedimento armazenado GetProductsPaged na lista suspensa](efficiently-paging-through-large-amounts-of-data-vb/_static/image12.png)

**Figura 10**: escolha o procedimento armazenado GetProductsPaged na lista suspensa

A próxima tela perguntará que tipo de dados é retornado pelo procedimento armazenado: dados tabulares, um único valor ou nenhum valor. Como o `GetProductsPaged` procedimento armazenado pode retornar vários registros, indique que ele retorna dados tabulares.

![Indicar que o procedimento armazenado retorna dados tabulares](efficiently-paging-through-large-amounts-of-data-vb/_static/image13.png)

**Figura 11**: indicar que o procedimento armazenado retorna dados tabulares

Por fim, indique os nomes dos métodos que você deseja criar. Assim como nos tutoriais anteriores, vá em frente e crie métodos usando o Fill a DataTable e retorne uma DataTable. Nomeie o primeiro método `FillPaged` e o segundo `GetProductsPaged` .

![Nomeie os métodos FillPaged e GetProductsPaged](efficiently-paging-through-large-amounts-of-data-vb/_static/image14.png)

**Figura 12**: nomear os métodos FillPaged e GetProductsPaged

Além de criar um método DAL para retornar uma página específica de produtos, também precisamos fornecer essa funcionalidade na BLL. Como o método DAL, o método GetProductsPaged de BLL deve aceitar duas entradas de inteiro para especificar o índice de linha inicial e o máximo de linhas, e deve retornar apenas os registros que se enquadram no intervalo especificado. Crie um método de BLL na classe ProductsBLL que meramente chama o método da DAL s GetProductsPaged, desta forma:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample8.vb)]

Você pode usar qualquer nome para os parâmetros de entrada do método de BLL, mas, como veremos em breve, optando por usar `startRowIndex` e `maximumRows` nos pouparei de um pouco de trabalho ao configurar um ObjectDataSource para usar esse método.

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>Etapa 4: Configurando o ObjectDataSource para usar a paginação personalizada

Com os métodos BLL e DAL para acessar um subconjunto específico de registros concluídos, estamos prontos para criar um controle GridView que páginas por meio de seus registros subjacentes usando a paginação personalizada. Comece abrindo a `EfficientPaging.aspx` página na `PagingAndSorting` pasta, adicione um GridView à página e configure-o para usar um novo controle ObjectDataSource. Nos nossos tutoriais anteriores, frequentemente tivemos o ObjectDataSource configurado para usar o `ProductsBLL` método Class s `GetProducts` . Desta vez, no entanto, desejamos usar o `GetProductsPaged` método, uma vez que o `GetProducts` método retorna *todos* os produtos no banco de dados, enquanto `GetProductsPaged` retorna apenas um subconjunto específico de registros.

![Configurar o ObjectDataSource para usar o método GetProductsPaged da classe ProductsBLL](efficiently-paging-through-large-amounts-of-data-vb/_static/image15.png)

**Figura 13**: configurar o ObjectDataSource para usar o método GetProductsPaged da classe ProductsBLL

Como recriamos um GridView somente leitura, Reserve um momento para definir a lista suspensa método nas guias inserir, atualizar e excluir para (nenhum).

Em seguida, o assistente ObjectDataSource solicitará as fontes dos valores de `GetProductsPaged` método s `startRowIndex` e de `maximumRows` parâmetros de entrada. Esses parâmetros de entrada serão realmente definidos pelo GridView automaticamente, portanto, basta deixar a fonte definida como nenhum e clicar em concluir.

![Deixar as origens do parâmetro de entrada como nenhuma](efficiently-paging-through-large-amounts-of-data-vb/_static/image16.png)

**Figura 14**: deixar as origens do parâmetro de entrada como nenhuma

Depois de concluir o assistente ObjectDataSource, o GridView conterá um BoundField ou CheckBoxField para cada um dos campos de dados do produto. Sinta-se à vontade para personalizar a aparência do GridView como você pode ver. Eu optei por exibir apenas o `ProductName` , `CategoryName` , `SupplierName` , `QuantityPerUnit` e `UnitPrice` boundfields. Além disso, configure o GridView para dar suporte à paginação marcando a caixa de seleção habilitar paginação em sua marca inteligente. Após essas alterações, a marcação declarativa de GridView e ObjectDataSource deve ser semelhante ao seguinte:

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample9.aspx)]

Se você visitar a página por meio de um navegador, no entanto, o GridView não será encontrado.

![O GridView não é exibido](efficiently-paging-through-large-amounts-of-data-vb/_static/image17.png)

**Figura 15**: o GridView não é exibido

O GridView está ausente porque o ObjectDataSource está usando 0 como os valores para ambos os parâmetros de `GetProductsPaged` `startRowIndex` `maximumRows` entrada e. Portanto, a consulta SQL resultante está retornando nenhum registro e, portanto, o GridView não é exibido.

Para corrigir isso, precisamos configurar o ObjectDataSource para usar a paginação personalizada. Isso pode ser feito nas seguintes etapas:

1. **Defina a Propriedade ObjectDataSource s `EnablePaging` como `true` ** this indica para o ObjectDataSource que ele deve passar para os `SelectMethod` dois parâmetros adicionais: um para especificar o índice de linha inicial ( [`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx) ) e outro para especificar o número máximo de linhas ( [`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx) ).
2. **Defina as propriedades ObjectDataSource `StartRowIndexParameterName` e, `MaximumRowsParameterName` adequadamente** , as `StartRowIndexParameterName` `MaximumRowsParameterName` Propriedades e indicam os nomes dos parâmetros de entrada passados para o `SelectMethod` para fins de paginação personalizada. Por padrão, esses nomes de parâmetro são `startIndexRow` e `maximumRows` , que é o motivo pelo qual, ao criar o `GetProductsPaged` método na BLL, usei esses valores para os parâmetros de entrada. Se você optar por usar nomes de parâmetro diferentes para o método da BLL s `GetProductsPaged` , como `startIndex` e `maxRows` , por exemplo, precisaria definir o ObjectDataSource s `StartRowIndexParameterName` e `MaximumRowsParameterName` as propriedades de acordo (como startIndex para `StartRowIndexParameterName` e maxRows para `MaximumRowsParameterName` ).
3. **Defina a [ `SelectCountMethod` Propriedade](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx) ObjectDataSource s como o nome do método que retorna o número total de registros sendo paginados por meio de ( `TotalNumberOfProducts` )** Lembre-se de que o `ProductsBLL` método Class s `TotalNumberOfProducts` retorna o número total de registros sendo paginados por meio do uso de um método Dal que executa uma `SELECT COUNT(*) FROM Products` consulta. Essas informações são necessárias para o ObjectDataSource a fim de processar corretamente a interface de paginação.
4. **Remover os `startRowIndex` `maximumRows` `<asp:Parameter>` elementos e da marcação declaradora de ObjectDataSource s** ao configurar o ObjectDataSource por meio do assistente, o Visual Studio adicionou automaticamente dois `<asp:Parameter>` elementos para os `GetProductsPaged` parâmetros de entrada do método. Ao definir `EnablePaging` como `true` , esses parâmetros serão passados automaticamente; se eles também aparecerem na sintaxe declarativa, o ObjectDataSource tentará passar *quatro* parâmetros para o `GetProductsPaged` método e dois parâmetros para o `TotalNumberOfProducts` método. Se você esquecer de remover esses `<asp:Parameter>` elementos, ao visitar a página por meio de um navegador, receberá uma mensagem de erro como: *ObjectDataSource ' ObjectDataSource1 ' não pôde encontrar um método não genérico ' TotalNumberOfProducts ' que tenha parâmetros: StartRowIndex, MaximumRows*.

Depois de fazer essas alterações, a sintaxe declarada de ObjectDataSource s deve ser semelhante ao seguinte:

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample10.aspx)]

Observe que as `EnablePaging` Propriedades e foram `SelectCountMethod` definidas e que os `<asp:Parameter>` elementos foram removidos. A Figura 16 mostra uma captura de tela da janela Propriedades após essas alterações terem sido feitas.

![Para usar a paginação personalizada, configure o controle ObjectDataSource](efficiently-paging-through-large-amounts-of-data-vb/_static/image18.png)

**Figura 16**: para usar a paginação personalizada, configure o controle ObjectDataSource

Depois de fazer essas alterações, visite esta página por meio de um navegador. Você deve ver 10 produtos listados, ordenados alfabeticamente. Reserve um momento para percorrer os dados uma página por vez. Embora não haja nenhuma diferença visual da perspectiva do usuário final entre a paginação padrão e a paginação personalizada, a paginação personalizada é mais eficiente para páginas por meio de grandes quantidades de dados, uma vez que recupera apenas os registros que precisam ser exibidos para uma determinada página.

[![Os dados, ordenados pelo nome do produto, são paginados usando a paging personalizado](efficiently-paging-through-large-amounts-of-data-vb/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image19.png)

**Figura 17**: os dados, ordenados pelo nome do produto, são paginados usando a paging personalizado ([clique para exibir a imagem em tamanho normal](efficiently-paging-through-large-amounts-of-data-vb/_static/image21.png))

> [!NOTE]
> Com a paginação personalizada, o valor de contagem de páginas retornado pelo ObjectDataSource `SelectCountMethod` é armazenado no estado de exibição do GridView. Outras variáveis GridView, a coleção,,, `PageIndex` `EditIndex` `SelectedIndex` `DataKeys` e assim por diante, são armazenadas no *estado de controle*, que é persistido independentemente do valor da `EnableViewState` Propriedade GridView. Como o `PageCount` valor é mantido entre postbacks usando o estado de exibição, ao usar uma interface de paginação que inclui um link para levá-lo até a última página, é imperativo que o estado de exibição do GridView seja habilitado. (Se a sua interface de paginação não incluir um link direto para a última página, você poderá desabilitar o estado de exibição.)

Clicar no link da última página causa um postback e instrui o GridView a atualizar sua `PageIndex` propriedade. Se o link da última página for clicado, o GridView atribuirá sua `PageIndex` Propriedade a um valor menor que sua `PageCount` propriedade. Com o estado de exibição desabilitado, o `PageCount` valor é perdido em postagens e o `PageIndex` valor inteiro máximo é atribuído ao seu. Em seguida, o GridView tenta determinar o índice de linha inicial multiplicando as `PageSize` `PageCount` Propriedades e. Isso resulta em um `OverflowException` desde que o produto exceda o tamanho máximo de inteiro permitido.

## <a name="implement-custom-paging-and-sorting"></a>Implementar paginação e classificação personalizadas

Nossa implementação de paginação personalizada atual requer que a ordem pela qual os dados são paginados seja especificada estaticamente ao criar o `GetProductsPaged` procedimento armazenado. No entanto, você pode ter observado que a marca inteligente GridView s contém uma caixa de seleção Habilitar classificação, além da opção habilitar paginação. Infelizmente, adicionar suporte à classificação ao GridView com nossa implementação de paginação personalizada atual classificará apenas os registros na página de dados exibida atualmente. Por exemplo, se você configurar o GridView para também oferecer suporte à paginação e, em seguida, ao exibir a primeira página de dados, classificar por nome do produto em ordem decrescente, ele inverterá a ordem dos produtos na página 1. Como mostra a Figura 18, mostra Carnarvon, tigres como o primeiro produto ao classificar em ordem alfabética inversa, que ignora os 71 outros produtos que vêm após Carnarvon, tigres, alfabeticamente; somente os registros na primeira página são considerados na classificação.

[![Somente os dados mostrados na página atual são classificados](efficiently-paging-through-large-amounts-of-data-vb/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image22.png)

**Figura 18**: somente os dados mostrados na página atual são classificados ([clique para exibir a imagem em tamanho normal](efficiently-paging-through-large-amounts-of-data-vb/_static/image24.png))

A classificação só se aplica à página de dados atual porque a classificação está ocorrendo depois que os dados são recuperados do método da BLL s `GetProductsPaged` , e esse método retorna apenas os registros para a página específica. Para implementar a classificação corretamente, precisamos passar a expressão de classificação para o `GetProductsPaged` método para que os dados possam ser classificados adequadamente antes de retornar a página de dados específica. Veremos como fazer isso em nosso próximo tutorial.

## <a name="implementing-custom-paging-and-deleting"></a>Implementando paginação personalizada e excluindo

Se você estiver habilitando a funcionalidade de exclusão em um GridView cujos dados são paginados usando técnicas de paging personalizadas, descobrirá que, ao excluir o último registro da última página, o GridView desaparecerá em vez de reduzir adequadamente os s GridView `PageIndex` . Para reproduzir esse bug, habilite a exclusão para o tutorial que acabamos de criar. Vá para a última página (página 9), em que você verá um único produto, já que estamos paginando por meio de 81 produtos, 10 produtos por vez. Excluir este produto.

Ao excluir o último produto, o GridView *deve* ir automaticamente para a oitava página, e essa funcionalidade é exibida com paginação padrão. Com a paginação personalizada, no entanto, depois de excluir o último produto na última página, o GridView simplesmente desaparece da tela completamente. O motivo preciso *pelo qual* isso acontece é um pouco além do escopo deste tutorial; consulte [excluindo o último registro na última página de um GridView com paginação personalizada](http://scottonwriting.net/sowblog/posts/7326.aspx) para obter detalhes de baixo nível sobre a origem desse problema. Em resumo, isso ocorre devido à seguinte sequência de etapas executadas pelo GridView quando o botão excluir é clicado:

1. Excluir o registro
2. Obter os registros apropriados a serem exibidos para o especificado `PageIndex` e `PageSize`
3. Verifique se o `PageIndex` não excede o número de páginas de dados na fonte de dados; se tiver, decrementará automaticamente a Propriedade GridView s `PageIndex`
4. Associar a página de dados apropriada ao GridView usando os registros obtidos na etapa 2

O problema se origina do fato de que, na etapa 2, o que `PageIndex` é usado ao captar os registros a serem exibidos ainda é a `PageIndex` da última página cujo registro único acabou de ser excluído. Portanto, na etapa 2, *nenhum* registro é retornado, já que a última página de dados não contém mais nenhum registro. Em seguida, na etapa 3, o GridView percebe que sua `PageIndex` propriedade é maior do que o número total de páginas na fonte de dados (desde que tenhamos excluído o último registro na última página) e, portanto, decrementa sua `PageIndex` propriedade. Na etapa 4, o GridView tenta se associar aos dados recuperados na etapa 2; no entanto, na etapa 2, nenhum registro foi retornado, portanto, resultando em um GridView vazio. Com a paginação padrão, esse problema não está na superfície, pois na etapa 2 *todos os* registros são recuperados da fonte de dados.

Para corrigir isso, temos duas opções. A primeira é criar um manipulador de eventos para o manipulador de `RowDeleted` eventos GridView que determina quantos registros foram exibidos na página que acabou de ser excluída. Se houvesse apenas um registro, o registro acabou de ser excluído deve ter sido o último e precisamos decrementar os s GridView `PageIndex` . É claro que só queremos atualizar o `PageIndex` se a operação de exclusão foi realmente bem-sucedida, o que pode ser determinado garantindo que a `e.Exception` propriedade seja `null` .

Essa abordagem funciona porque atualiza o `PageIndex` após a etapa 1, mas antes da etapa 2. Portanto, na etapa 2, o conjunto apropriado de registros é retornado. Para fazer isso, use um código semelhante ao seguinte:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample11.vb)]

Uma alternativa alternativa é criar um manipulador de eventos para o evento ObjectDataSource s `RowDeleted` e definir a `AffectedRows` propriedade com um valor de 1. Depois de excluir o registro na etapa 1 (mas antes de recuperar os dados novamente na etapa 2), o GridView atualizará sua `PageIndex` propriedade se uma ou mais linhas tiverem sido afetadas pela operação. No entanto, a `AffectedRows` propriedade não é definida pelo ObjectDataSource e, portanto, essa etapa é omitida. Uma maneira de executar essa etapa é definir manualmente a `AffectedRows` propriedade se a operação de exclusão for concluída com êxito. Isso pode ser feito usando um código semelhante ao seguinte:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample12.vb)]

O código para ambos os manipuladores de eventos pode ser encontrado na classe code-behind do `EfficientPaging.aspx` exemplo.

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>Comparando o desempenho da paginação padrão e personalizada

Como a paginação personalizada recupera apenas os registros necessários, enquanto a paginação padrão retorna *todos* os registros de cada página que está sendo exibida, ela limpa se a paginação personalizada é mais eficiente do que a paginação padrão. Mas o quanto mais eficiente é a paginação personalizada? Que tipo de ganhos de desempenho pode ser visto movendo-se da paginação padrão para a paginação personalizada?

Infelizmente, não há nenhum tamanho que atenda a todas as respostas aqui. O lucro de desempenho depende de uma série de fatores, quanto mais proeminente dois são o número de registros sendo paginados e a carga colocada no servidor de banco de dados e nos canais de comunicação entre o servidor Web e o servidor de banco de dados. Para tabelas pequenas com apenas algumas dúzias de registros, a diferença de desempenho pode ser insignificante. No entanto, para tabelas grandes, com milhares a centenas de milhares de linhas, a diferença de desempenho é de acento agudo.

Um artigo de minha, [paginação personalizada no ASP.NET 2,0 com SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx), contém alguns testes de desempenho que executei para exibir as diferenças no desempenho entre essas duas técnicas de paginação ao paginar por meio de uma tabela de banco de dados com registros 50.000. Nesses testes, examinei o tempo para executar a consulta no nível de SQL Server (usando o [SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)) e na página ASP.NET usando os [recursos de rastreamento de ASP.net](https://msdn.microsoft.com/library/y13fw6we.aspx). Tenha em mente que esses testes foram executados na minha caixa de desenvolvimento com um único usuário ativo e, portanto, não são científicos e não imitam padrões de carga de site típicos. Independentemente disso, os resultados ilustram as diferenças relativas no tempo de execução para a paginação padrão e personalizada ao trabalhar com quantidades de dados suficientemente grandes.

|  | **Duração média (s)** | **Reads** |
| --- | --- | --- |
| **Paginação padrão do SQL Profiler** | 1,411 | 383 |
| **Paginação personalizada do SQL Profiler** | 0, 2 | 29 |
| **Rastreamento de ASP.NET de paginação padrão** | 2,379 | *N/A* |
| **Rastreamento de ASP.NET de paginação personalizada** | 0, 29 | *N/A* |

Como você pode ver, a recuperação de uma página específica de dados exigiu 354 menos leituras em média e é concluída em uma fração do tempo. Na página ASP.NET, a página personalizada foi capaz de renderizar perto<sup>de 1/100,</sup> do tempo necessário ao usar a paginação padrão. Consulte [meu artigo](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) para obter mais informações sobre esses resultados juntamente com o código e um banco de dados que você pode baixar para reproduzir esses testes em seu próprio ambiente.

## <a name="summary"></a>Resumo

A paginação padrão é um fácil para implementar apenas marque a caixa de seleção habilitar paginação na marca inteligente s de controle da Web de dados, mas essa simplicidade é o custo do desempenho. Com a paginação padrão, quando um usuário solicita qualquer página de dados, *todos os* registros são retornados, embora apenas uma pequena fração deles possa ser mostrada. Para combater essa sobrecarga de desempenho, o ObjectDataSource oferece uma paginação personalizada de opção de paginação alternativa.

Embora a paginação personalizada Aprimore os problemas de desempenho de paginação padrão, recuperando apenas os registros que precisam ser exibidos, mais envolvida para implementar a paginação personalizada. Primeiro, uma consulta deve ser escrita de forma correta (e eficiente) acessa o subconjunto específico de registros solicitados. Isso pode ser feito de várias maneiras; o que examinamos neste tutorial é usar SQL Server nova função de 2005 s `ROW_NUMBER()` para classificar os resultados e, em seguida, retornar apenas os resultados cuja classificação esteja dentro de um intervalo especificado. Além disso, precisamos adicionar um meio para determinar o número total de registros sendo paginados. Depois de criar esses métodos DAL e BLL, também precisamos configurar o ObjectDataSource para que ele possa determinar quantos registros totais estão sendo paginados e pode passar corretamente os valores de índice de linha inicial e máximo de linhas para a BLL.

Embora a implementação de paginação personalizada exija várias etapas e não seja tão simples quanto a paginação padrão, a paginação personalizada é uma necessidade durante a paginação por quantidades de dados suficientemente grandes. À medida que os resultados são examinados, a paginação personalizada pode lançar segundos fora do tempo de renderização da página ASP.NET e pode clarear a carga no servidor de banco de dados por uma ou mais ordens de magnitude.

Boa programação!

## <a name="about-the-author"></a>Sobre o autor

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor de sete livros sobre ASP/ASP. net e fundador da [4guysfromrolla.com](http://www.4guysfromrolla.com), tem trabalhado com tecnologias Web da Microsoft desde 1998. Scott trabalha como consultor, instrutor e escritor independentes. Seu livro mais recente é que a [*Sams ensina a ASP.NET 2,0 em 24 horas*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ele pode ser acessado em [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) ou por meio de seu blog, que pode ser encontrado em [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

> [!div class="step-by-step"]
> [Anterior](paging-and-sorting-report-data-vb.md) 
>  [Avançar](sorting-custom-paged-data-vb.md)
