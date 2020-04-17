---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: Criando classes de modelo com LINQ para SQL (VB) | Microsoft Docs
author: rick-anderson
description: O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo mvc ASP.NET. Neste tutorial, você aprende a construir o modelo c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 1a6133227eedc8934af7bf872532ca667b97d0f8
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542697"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a>Criação de classes de modelo com o LINQ to SQL (VB)

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo mvc ASP.NET. Neste tutorial, você aprende a construir classes de modelo saem e executam acesso ao banco de dados aproveitando o Microsoft LINQ para o SQL.

O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo mvc ASP.NET. Neste tutorial, você aprende a construir classes de modelo saem e executam acesso ao banco de dados aproveitando o Microsoft LINQ para o SQL.

Neste tutorial, construímos um aplicativo básico de banco de dados movie. Começamos criando o aplicativo de banco de dados Movie da maneira mais rápida e fácil possível. Realizamos todo o nosso acesso de dados diretamente de nossas ações de controlador.

Em seguida, você aprende a usar o padrão repositório. Usar o padrão repositório requer um pouco mais de trabalho. No entanto, a vantagem de adotar esse padrão é que ele permite construir aplicativos que sejam adaptáveis à mudança e possam ser facilmente testados.

## <a name="what-is-a-model-class"></a>O que é uma classe modelo?

Um modelo MVC contém toda a lógica de aplicação que não está contida em uma exibição MVC ou controlador MVC. Em particular, um modelo MVC contém toda a lógica de acesso a dados e negócios de aplicativos.

Você pode usar uma variedade de tecnologias diferentes para implementar sua lógica de acesso a dados. Por exemplo, você pode construir suas classes de acesso a dados usando as classes Microsoft Entity Framework, NHibernate, Subsonic ou ADO.NET.

Neste tutorial, uso LINQ para SQL para consultar e atualizar o banco de dados. Linq para SQL fornece um método muito fácil de interagir com um banco de dados Microsoft SQL Server. No entanto, é importante entender que o ASP.NET quadro MVC não está vinculado ao LINQ ao SQL de forma alguma. ASP.NET MVC é compatível com qualquer tecnologia de acesso a dados.

## <a name="create-a-movie-database"></a>Criar um banco de dados de filmes

Neste tutorial - a fim de ilustrar como você pode construir classes de modelo - construímos um aplicativo de banco de dados de filme simples. O primeiro passo é criar um novo banco de dados. Clique com o\_botão direito do mouse na pasta Dados do aplicativo na janela Do Explorador de soluções e selecione a opção de menu **Adicionar, Novo Item**. Selecione o modelo de banco de dados do servidor SQL, dê-lhe o nome MoviesDB.mdf e clique no botão **Adicionar** (consulte Figura 1).

[![Adicionando um novo banco de dados do SQL Server](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**Figura 01**: Adicionando um novo banco de dados do servidor SQL[(Clique para exibir imagem em tamanho real)](creating-model-classes-with-linq-to-sql-vb/_static/image3.png)

Depois de criar o novo banco de dados, você pode abrir o banco\_de dados clicando duas vezes no arquivo MoviesDB.mdf na pasta Dados do aplicativo. Clicar duas vezes no arquivo MoviesDB.mdf abre a janela Server Explorer (ver Figura 2).

|   | A janela Server Explorer é chamada de janela Database Explorer ao usar o Visual Web Developer. |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

[![Usando a janela Server Explorer](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**Figura 02**: Usando a janela Server Explorer[(Clique para ver a imagem em tamanho real)](creating-model-classes-with-linq-to-sql-vb/_static/image6.png)

Precisamos adicionar uma tabela ao nosso banco de dados que represente nossos filmes. Clique com o botão direito do mouse na pasta Tabelas e selecione a opção de menu **Adicionar nova tabela**. A seleção desta opção de menu abre o Table Designer (ver Figura 3).

[![Usando a janela Server Explorer](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**Figura 03**: O Designer de Tabela[(Clique para ver a imagem em tamanho real](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))

Precisamos adicionar as seguintes colunas à nossa tabela de banco de dados:

| **Nome da coluna** | **Tipo de dados** | **Permitir Nulos** |
| --- | --- | --- |
| ID | Int | Falso |
| Title | Nvarchar(200) | Falso |
| Diretor | Nvarchar(50) | Falso |

Você precisa fazer duas coisas especiais para a coluna de id. Primeiro, você precisa marcar a coluna Id como uma coluna de tecla principal selecionando a coluna no Table Designer e clicando no ícone de uma tecla. LINQ para SQL exige que você especifique suas colunas principais de tecla ao executar inserções ou atualizações no banco de dados.

Em seguida, você precisa marcar a coluna Identificar como uma coluna Identidade, atribuindo o valor Sim à propriedade **Is Identity** (ver Figura 3). Uma coluna Identidade é uma coluna que é atribuída a um novo número automaticamente sempre que você adiciona uma nova linha de dados a uma tabela.

Depois de fazer essas alterações, salve a tabela com o nome tblMovie. Você pode salvar a tabela clicando no botão Salvar.

## <a name="create-linq-to-sql-classes"></a>Crie LINQ para classes SQL

Nosso modelo MVC conterá classes LINQ para SQL que representam a tabela de banco de dados tblMovie. A maneira mais fácil de criar essas classes LINQ para SQL é clicar com o botão direito do mouse na pasta Modelos, selecionar **Adicionar, Novo Item,** selecionar o modelo LINQ para SQL Classes, dar às classes o nome Movie.dbml e clicar no botão **Adicionar** (ver Figura 4).

[![Criando aulas de LINQ para SQL](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**Figura 04**: Criação de classes LINQ para SQL[(Clique para exibir imagem em tamanho real)](creating-model-classes-with-linq-to-sql-vb/_static/image12.png)

Imediatamente após criar o Movie LINQ para SQL Classes, o Designer Relacional de Objeto saem. Você pode arrastar tabelas de banco de dados da janela Server Explorer para o Object Relational Designer para criar LINQ para SQL Classes que representam tabelas de banco de dados específicas. Precisamos adicionar a tabela de banco de dados tblMovie no Object Relational Designer (ver Figura 4).

[![Usando o Designer Relacional de Objeto](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**Figura 05**: Usando o Designer Relacional de Objetos[(Clique para ver a imagem em tamanho real)](creating-model-classes-with-linq-to-sql-vb/_static/image15.png)

Por padrão, o Object Relational Designer cria uma classe com o mesmo nome da tabela de banco de dados que você arrasta para o Designer. No entanto, não queremos chamar nossa classe de tblMovie. Portanto, clique no nome da classe no Designer e mude o nome da classe para Movie.

Por fim, clique no botão **Salvar** (a imagem do disquete) para salvar o LINQ nas Classes SQL. Caso contrário, as classes LINQ para SQL não serão geradas pelo Object Relational Designer.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Usando LINQ para SQL em uma ação controladora

Agora que temos nossas classes LINQ para SQL, podemos usar essas classes para recuperar dados do banco de dados. Nesta seção, você aprende a usar o LINQ para as classes SQL diretamente dentro de uma ação controladora. Exibiremos a lista de filmes da tabela de banco de dados tblMovies em uma exibição de MVC.

Primeiro, precisamos modificar a classe HomeController. Esta classe pode ser encontrada na pasta Controladores do seu aplicativo. Modifique a classe para que pareça a classe na Lista 1.

**Listagem 1 –`Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

A ação Index() na Listagem 1 usa uma classe LINQ para SQL DataContext (o MovieDataContext) para representar o banco de dados MoviesDB. A classe MoveDataContext foi gerada pelo Visual Studio Object Relational Designer.

Uma consulta LINQ é realizada no DataContext para recuperar todos os filmes da tabela de banco de dados tblMovies. A lista de filmes é atribuída a uma variável local chamada filmes. Finalmente, a lista de filmes é passada para a exibição de dados.

Para mostrar os filmes, precisamos modificar a exibição indexada. Você pode encontrar a exibição Índice na pasta Views\Home\. Atualize a exibição Índice para que pareça com a exibição na Listagem 2.

**Listagem 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

Observe que a exibição &lt;de Índice modificado&gt; inclui uma diretiva %@ import namespace % na parte superior da exibição. Esta diretiva importa o namespace MvcApplication1. Precisamos desse namespace para trabalhar com as classes modelo – em particular, a classe Movie – na visão.

A exibição na Lista 2 contém um loop Para Cada que itera todos os itens representados pela propriedade ViewData.Model. O valor da propriedade Título é exibido para cada filme.

Observe que o valor da propriedade ViewData.Model é lançado para um IEnumerable. Isso é necessário para fazer um loop através do conteúdo do ViewData.Model. Outra opção aqui é criar uma visão fortemente digitada. Quando você cria uma exibição fortemente digitada, você lança a propriedade ViewData.Model para um determinado tipo na classe de código atrás de uma exibição.

Se você executar o aplicativo depois de modificar a classe HomeController e a exibição Índice, você receberá uma página em branco. Você terá uma página em branco porque não há registros de filmes na tabela de banco de dados tblMovies.

Para adicionar registros à tabela de banco de dados tblMovies, clique com o botão direito do mouse na tabela de banco de dados tblMovies na janela Server Explorer (janela do Database Explorer no Visual Web Developer) e selecione a opção de menu **Mostrar Dados da Tabela**. Você pode inserir registros de filme usando a grade que aparece (ver Figura 5).

[![Inserindo filmes](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**Figura 06**: Inserir filmes[(Clique para ver imagem em tamanho real)](creating-model-classes-with-linq-to-sql-vb/_static/image18.png)

Depois de adicionar alguns registros de banco de dados à tabela tblMovies e executar o aplicativo, você verá a página na Figura 7. Todos os registros do banco de dados de filmes são exibidos em uma lista de balas.

[![Exibindo filmes com a exibição Index](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**Figura 07**: Exibindo filmes com a exibição Index[(Clique para exibir imagem em tamanho real)](creating-model-classes-with-linq-to-sql-vb/_static/image21.png)

## <a name="using-the-repository-pattern"></a>Usando o padrão de repositório

Na seção anterior, usamos linq para classes SQL diretamente dentro de uma ação controladora. Usamos a classe MovieDataContext diretamente da ação do controlador Index(). Não há nada de errado em fazer isso no caso de uma aplicação simples. No entanto, trabalhar diretamente com LINQ para SQL em uma classe de controlador cria problemas quando você precisa construir uma aplicação mais complexa.

O uso do LINQ para SQL dentro de uma classe controladora dificulta a mudança das tecnologias de acesso a dados no futuro. Por exemplo, você pode decidir mudar de usar o Microsoft LINQ para o SQL para usar o Microsoft Entity Framework como sua tecnologia de acesso a dados. Nesse caso, você precisaria reescrever cada controlador que acessar o banco de dados dentro do seu aplicativo.

O uso de LINQ para SQL dentro de uma classe de controladores também dificulta a construção de testes unitários para sua aplicação. Normalmente, você não quer interagir com um banco de dados ao realizar testes unitários. Você deseja usar seus testes unitários para testar sua lógica de aplicativo e não seu servidor de banco de dados.

Para construir um aplicativo MVC que seja mais adaptável às mudanças futuras e que possa ser mais facilmente testado, você deve considerar o uso do padrão repositório. Quando você usa o padrão repositório, você cria uma classe de repositório separada que contém toda a lógica de acesso ao banco de dados.

Quando você cria a classe de repositório, você cria uma interface que representa todos os métodos usados pela classe de repositório. Dentro de seus controladores, você escreve seu código contra a interface em vez do repositório. Dessa forma, você pode implementar o repositório usando diferentes tecnologias de acesso a dados no futuro.

A interface na Listagem 3 é chamada IMovieRepository e representa um único método chamado ListAll().

**Lista 3 –`Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

A classe de repositório na Listagem 4 implementa a interface IMovieRepository. Observe que ele contém um método chamado ListAll() que corresponde ao método exigido pela interface IMovieRepository.

**Lista 4 –`Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

Finalmente, a classe MoviesController na Lista 5 usa o padrão Repositório. Ele não usa mais LINQ para classes SQL diretamente.

**Lista 5 –`Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

Observe que a classe MoviesController na Listagem 5 tem dois construtores. O primeiro construtor, o construtor sem parâmetros, é chamado quando sua aplicação está em execução. Este construtor cria uma instância da classe MovieRepository e passa-a para o segundo construtor.

O segundo construtor tem um único parâmetro: um parâmetro IMovieRepository. Este construtor simplesmente atribui o valor do parâmetro a um \_campo de nível de classe chamado repositório.

A classe MoviesController está se aproveitando de um padrão de design de software chamado padrão de injeção de dependência. Em particular, está usando algo chamado Injeção de Dependência de Construtores. Você pode ler mais sobre este padrão lendo o seguinte artigo de Martin Fowler:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

Observe que todo o código da classe MoviesController (com exceção do primeiro construtor) interage com a interface IMovieRepository em vez da classe MovieRepository real. O código interage com uma interface abstrata em vez de uma implementação concreta da interface.

Se você quiser modificar a tecnologia de acesso a dados usada pelo aplicativo, então você pode simplesmente implementar a interface IMovieRepository com uma classe que usa a tecnologia alternativa de acesso ao banco de dados. Por exemplo, você pode criar uma classe EntityFrameworkMovieRepository ou uma classe SubSonicMovieRepository. Como a classe controladora está programada contra a interface, você pode passar uma nova implementação do IMovieRepository para a classe controladora e a classe continuaria a funcionar.

Além disso, se você quiser testar a classe MoviesController, então você pode passar uma falsa classe de repositório de filmes para o MoviesController. Você pode implementar a classe IMovieRepository com uma classe que realmente não acessa o banco de dados, mas contém todos os métodos necessários da interface IMovieRepository. Dessa forma, você pode testar a classe MoviesController sem realmente acessar um banco de dados real.

## <a name="summary"></a>Resumo

O objetivo deste tutorial foi demonstrar como você pode criar classes de modeloS MVC aproveitando o Microsoft LINQ para o SQL. Examinamos duas estratégias para exibir dados de banco de dados em um aplicativo ASP.NET MVC. Primeiro, criamos aulas de LINQ para SQL e usamos as classes diretamente dentro de uma ação controladora. O uso de classes LINQ para SQL dentro de um controlador permite que você exiba dados de banco de dados de forma rápida e fácil em um aplicativo MVC.

Em seguida, exploramos um caminho um pouco mais difícil, mas definitivamente mais virtuoso para exibir dados de banco de dados. Aproveitamos o padrão do Repositório e colocamos toda a nossa lógica de acesso ao banco de dados em uma classe de repositório separada. Em nosso controlador, escrevemos todo o nosso código contra uma interface em vez de uma classe de concreto. A vantagem do padrão repositório é que ele nos permite alterar facilmente as tecnologias de acesso ao banco de dados no futuro e nos permite testar facilmente nossas classes de controladores.

> [!div class="step-by-step"]
> [Próximo](creating-model-classes-with-the-entity-framework-vb.md)
> [anterior](displaying-a-table-of-database-data-vb.md)
