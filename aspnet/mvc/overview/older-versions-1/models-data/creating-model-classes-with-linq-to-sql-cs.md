---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: Criando classes de modelo com LINQ para SQL (C#) | Microsoft Docs
author: rick-anderson
description: O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo mvc ASP.NET. Neste tutorial, você aprende a construir o modelo c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: eac6fec3a4cfd833b810378d946874a246d9a2c3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542723"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>Criação de classes de modelo com o LINQ to SQL (C#)

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo mvc ASP.NET. Neste tutorial, você aprende a construir classes de modelo saem e executam acesso ao banco de dados aproveitando o Microsoft LINQ para o SQL.

O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo mvc ASP.NET. Neste tutorial, você aprende a construir classes de modelo saem e realizar acesso ao banco de dados aproveitando o Microsoft LINQ para o SQL

Neste tutorial, construímos um aplicativo básico de banco de dados movie. Começamos criando o aplicativo de banco de dados Movie da maneira mais rápida e fácil possível. Realizamos todo o nosso acesso de dados diretamente de nossas ações de controlador.

Em seguida, você aprende a usar o padrão repositório. Usar o padrão repositório requer um pouco mais de trabalho. No entanto, a vantagem de adotar esse padrão é que ele permite construir aplicativos que sejam adaptáveis à mudança e possam ser facilmente testados.

## <a name="what-is-a-model-class"></a>O que é uma classe modelo?

Um modelo MVC contém toda a lógica de aplicação que não está contida em uma exibição MVC ou controlador MVC. Em particular, um modelo MVC contém toda a lógica de acesso a dados e negócios de aplicativos.

Você pode usar uma variedade de tecnologias diferentes para implementar sua lógica de acesso a dados. Por exemplo, você pode construir suas classes de acesso a dados usando as classes Microsoft Entity Framework, NHibernate, Subsonic ou ADO.NET.

Neste tutorial, uso LINQ para SQL para consultar e atualizar o banco de dados. Linq para SQL fornece um método muito fácil de interagir com um banco de dados Microsoft SQL Server. No entanto, é importante entender que o ASP.NET quadro MVC não está vinculado ao LINQ ao SQL de forma alguma. ASP.NET MVC é compatível com qualquer tecnologia de acesso a dados.

## <a name="create-a-movie-database"></a>Criar um banco de dados de filmes

Neste tutorial - a fim de ilustrar como você pode construir classes de modelo - construímos um aplicativo de banco de dados de filme simples. O primeiro passo é criar um novo banco de dados. Clique com o\_botão direito do mouse na pasta Dados do aplicativo na janela Do Explorador de soluções e selecione a opção de menu **Adicionar, Novo Item**. Selecione o modelo **de banco de dados do servidor SQL,** dê-lhe o nome MoviesDB.mdf e clique no botão **Adicionar** (consulte Figura 1).

[![Adicionando um novo banco de dados do SQL Server](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**Figura 01**: Adicionando um novo banco de dados do servidor SQL[(Clique para exibir imagem em tamanho real)](creating-model-classes-with-linq-to-sql-cs/_static/image3.png)

Depois de criar o novo banco de dados, você pode abrir o banco\_de dados clicando duas vezes no arquivo MoviesDB.mdf na pasta Dados do aplicativo. Clicar duas vezes no arquivo MoviesDB.mdf abre a janela Server Explorer (ver Figura 2).

A janela Server Explorer é chamada de janela Database Explorer ao usar o Visual Web Developer.

[![Usando a janela Server Explorer](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**Figura 02**: Usando a janela Server Explorer[(Clique para ver a imagem em tamanho real)](creating-model-classes-with-linq-to-sql-cs/_static/image6.png)

Precisamos adicionar uma tabela ao nosso banco de dados que represente nossos filmes. Clique com o botão direito do mouse na pasta Tabelas e selecione a opção de menu **Adicionar nova tabela**. A seleção desta opção de menu abre o Table Designer (ver Figura 3).

[![Usando a janela Server Explorer](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**Figura 03**: O Designer de Tabela[(Clique para ver a imagem em tamanho real](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))

Precisamos adicionar as seguintes colunas à nossa tabela de banco de dados:

| **Nome da coluna** | **Tipo de dados** | **Permitir Nulos** |
| --- | --- | --- |
| ID | Int | Falso |
| Title | Nvarchar(200) | Falso |
| Diretor | Nvarchar(50) | Falso |

Você precisa fazer duas coisas especiais para a coluna de id. Primeiro, você precisa marcar a coluna Id como uma coluna de tecla principal selecionando a coluna no Table Designer e clicando no ícone de uma tecla. LINQ para SQL exige que você especifique suas colunas principais de tecla ao executar inserções ou atualizações no banco de dados.

Em seguida, você precisa marcar a coluna Identificar como uma coluna Identidade, atribuindo o valor Sim à propriedade **Is Identity** (ver Figura 3). Uma coluna Identidade é uma coluna que é atribuída a um novo número automaticamente sempre que você adiciona uma nova linha de dados a uma tabela.

## <a name="create-linq-to-sql-classes"></a>Crie LINQ para classes SQL

Nosso modelo MVC conterá classes LINQ para SQL que representam a tabela de banco de dados tblMovie. A maneira mais fácil de criar essas classes LINQ para SQL é clicar com o botão direito do mouse na pasta Modelos, selecionar **Adicionar, Novo Item,** selecionar o modelo LINQ para SQL Classes, dar às classes o nome Movie.dbml e clicar no botão **Adicionar** (ver Figura 4).

[![Criando aulas de LINQ para SQL](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**Figura 04**: Criação de classes LINQ para SQL[(Clique para exibir imagem em tamanho real)](creating-model-classes-with-linq-to-sql-cs/_static/image12.png)

Imediatamente após criar o Movie LINQ para SQL Classes, o Designer Relacional de Objeto saem. Você pode arrastar tabelas de banco de dados da janela Server Explorer para o Object Relational Designer para criar LINQ para SQL Classes que representam tabelas de banco de dados específicas. Precisamos adicionar a tabela de banco de dados tblMovie no Object Relational Designer (ver Figura 5).

[![Usando o Designer Relacional de Objeto](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**Figura 05**: Usando o Designer Relacional de Objetos[(Clique para ver a imagem em tamanho real)](creating-model-classes-with-linq-to-sql-cs/_static/image15.png)

Por padrão, o Object Relational Designer cria uma classe com o mesmo nome da tabela de banco de dados que você arrasta para o Designer. No entanto, não queremos `tblMovie`chamar nossa classe. Portanto, clique no nome da classe no Designer e mude o nome da classe para Movie.

Por fim, clique no botão **Salvar** (a imagem do disquete) para salvar o LINQ nas Classes SQL. Caso contrário, as classes LINQ para SQL não serão geradas pelo Object Relational Designer.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Usando LINQ para SQL em uma ação controladora

Agora que temos nossas classes LINQ para SQL, podemos usar essas classes para recuperar dados do banco de dados. Nesta seção, você aprende a usar o LINQ para as classes SQL diretamente dentro de uma ação controladora. Exibiremos a lista de filmes da tabela de banco de dados tblMovies em uma exibição de MVC.

Primeiro, precisamos modificar a classe HomeController. Esta classe pode ser encontrada na pasta Controladores do seu aplicativo. Modifique a classe para que pareça a classe na Lista 1.

**Listagem 1 –`Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

A `Index()` ação na Listagem 1 usa uma classe LINQ `MovieDataContext`para SQL DataContext (a) para representar o `MoviesDB` banco de dados. A `MoveDataContext` aula foi gerada pelo Visual Studio Object Relational Designer.

Uma consulta LINQ é realizada no DataContext para recuperar `tblMovies` todos os filmes da tabela de banco de dados. A lista de filmes é atribuída `movies`a uma variável local chamada . Finalmente, a lista de filmes é passada para a exibição de dados.

Para mostrar os filmes, precisamos modificar a exibição indexada. Você pode encontrar a `Views\Home\` exibição Índice na pasta. Atualize a exibição Índice para que pareça com a exibição na Listagem 2.

**Listagem 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

Observe que a exibição `<%@ import namespace %>` de Índice modificado inclui uma diretiva na parte superior da exibição. Esta diretiva `MvcApplication1.Models namespace`importa o . Precisamos desse namespace para trabalhar `model` com as classes `Movie` – em particular, a classe – na visão.

A exibição na `foreach` Lista 2 contém um loop que itera `ViewData.Model` através de todos os itens representados pela propriedade. O valor `Title` da propriedade é `movie`exibido para cada um .

Observe que o `ViewData.Model` valor da propriedade `IEnumerable`é lançado para um . Isso é necessário para percorrer o `ViewData.Model`conteúdo de . Outra opção aqui é criar um `view`fortemente digitado . Quando você cria uma espécie `view`de tipo `ViewData.Model` forte, você lança a propriedade para um determinado tipo na classe de código atrás de uma exibição.

Se você executar o aplicativo `HomeController` depois de modificar a classe e a exibição Índice, você receberá uma página em branco. Você terá uma página em branco porque não `tblMovies` há registros de filmes na tabela de banco de dados.

Para adicionar registros à `tblMovies` tabela de banco `tblMovies` de dados, clique com o botão direito do mouse na tabela de banco de dados na janela Server Explorer (janela do Database Explorer no Visual Web Developer) e selecione a opção de menu Mostrar dados da tabela. Você pode `movie` inserir registros usando a grade que aparece (ver Figura 6).

[![Inserindo filmes](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**Figura 06**: Inserir filmes[(Clique para ver imagem em tamanho real)](creating-model-classes-with-linq-to-sql-cs/_static/image18.png)

Depois de adicionar alguns `tblMovies` registros de banco de dados à tabela e executar o aplicativo, você verá a página na Figura 7. Todos os registros do banco de dados de filmes são exibidos em uma lista de balas.

[![Exibindo filmes com a exibição Index](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**Figura 07**: Exibindo filmes com a exibição Index[(Clique para exibir imagem em tamanho real)](creating-model-classes-with-linq-to-sql-cs/_static/image21.png)

## <a name="using-the-repository-pattern"></a>Usando o padrão de repositório

Na seção anterior, usamos linq para classes SQL diretamente dentro de uma ação controladora. Usamos a `MovieDataContext` classe diretamente `Index()` da ação do controlador. Não há nada de errado em fazer isso no caso de uma aplicação simples. No entanto, trabalhar diretamente com LINQ para SQL em uma classe de controlador cria problemas quando você precisa construir uma aplicação mais complexa.

O uso do LINQ para SQL dentro de uma classe controladora dificulta a mudança das tecnologias de acesso a dados no futuro. Por exemplo, você pode decidir mudar de usar o Microsoft LINQ para o SQL para usar o Microsoft Entity Framework como sua tecnologia de acesso a dados. Nesse caso, você precisaria reescrever cada controlador que acessar o banco de dados dentro do seu aplicativo.

O uso de LINQ para SQL dentro de uma classe de controladores também dificulta a construção de testes unitários para sua aplicação. Normalmente, você não quer interagir com um banco de dados ao realizar testes unitários. Você deseja usar seus testes unitários para testar sua lógica de aplicativo e não seu servidor de banco de dados.

Para construir um aplicativo MVC que seja mais adaptável às mudanças futuras e que possa ser mais facilmente testado, você deve considerar o uso do padrão repositório. Quando você usa o padrão repositório, você cria uma classe de repositório separada que contém toda a lógica de acesso ao banco de dados.

Quando você cria a classe de repositório, você cria uma interface que representa todos os métodos usados pela classe de repositório. Dentro de seus controladores, você escreve seu código contra a interface em vez do repositório. Dessa forma, você pode implementar o repositório usando diferentes tecnologias de acesso a dados no futuro.

A interface na Listagem `IMovieRepository` 3 é nomeada e `ListAll()`representa um único método chamado .

**Lista 3 –`Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

A classe de repositório na `IMovieRepository` Listagem 4 implementa a interface. Observe que ele contém `ListAll()` um método nomeado que `IMovieRepository` corresponde ao método exigido pela interface.

**Lista 4 –`Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

Finalmente, `MoviesController` a classe na Lista 5 usa o padrão repositório. Ele não usa mais LINQ para classes SQL diretamente.

**Lista 5 –`Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

Observe que `MoviesController` a classe na Lista 5 tem dois construtores. O primeiro construtor, o construtor sem parâmetros, é chamado quando sua aplicação está em execução. Este construtor cria uma `MovieRepository` instância da classe e passa para o segundo construtor.

O segundo construtor tem um único `IMovieRepository` parâmetro: um parâmetro. Este construtor simplesmente atribui o valor do parâmetro a um `_repository`campo de nível de classe chamado .

A `MoviesController` classe está se aproveitando de um padrão de design de software chamado padrão de injeção de dependência. Em particular, está usando algo chamado Injeção de Dependência de Construtores. Você pode ler mais sobre este padrão lendo o seguinte artigo de Martin Fowler:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

Observe que todo o `MoviesController` código da classe (com exceção do primeiro `IMovieRepository` construtor) interage `MovieRepository` com a interface em vez da classe real. O código interage com uma interface abstrata em vez de uma implementação concreta da interface.

Se você quiser modificar a tecnologia de acesso a dados `IMovieRepository` usada pelo aplicativo, então você pode simplesmente implementar a interface com uma classe que usa a tecnologia alternativa de acesso ao banco de dados. Por exemplo, você `EntityFrameworkMovieRepository` pode criar `SubSonicMovieRepository` uma classe ou uma classe. Como a classe controladora é programada contra a interface, você pode passar uma nova implementação para a classe controladora `IMovieRepository` e a classe continuaria a funcionar.

Além disso, se você `MoviesController` quiser testar a classe, então você pode passar `HomeController`uma aula de repositório de filmes falsos para o . Você pode `IMovieRepository` implementar a classe com uma classe que realmente não acessa o banco de dados, mas contém todos os métodos necessários da `IMovieRepository` interface. Dessa forma, você pode `MoviesController` testar a classe sem realmente acessar um banco de dados real.

## <a name="summary"></a>Resumo

O objetivo deste tutorial foi demonstrar como você pode criar classes de modeloS MVC aproveitando o Microsoft LINQ para o SQL. Examinamos duas estratégias para exibir dados de banco de dados em um aplicativo ASP.NET MVC. Primeiro, criamos aulas de LINQ para SQL e usamos as classes diretamente dentro de uma ação controladora. O uso de classes LINQ para SQL dentro de um controlador permite que você exiba dados de banco de dados de forma rápida e fácil em um aplicativo MVC.

Em seguida, exploramos um caminho um pouco mais difícil, mas definitivamente mais virtuoso para exibir dados de banco de dados. Aproveitamos o padrão do Repositório e colocamos toda a nossa lógica de acesso ao banco de dados em uma classe de repositório separada. Em nosso controlador, escrevemos todo o nosso código contra uma interface em vez de uma classe de concreto. A vantagem do padrão repositório é que ele nos permite alterar facilmente as tecnologias de acesso ao banco de dados no futuro e nos permite testar facilmente nossas classes de controladores.

> [!div class="step-by-step"]
> [Próximo](creating-model-classes-with-the-entity-framework-cs.md)
> [anterior](displaying-a-table-of-database-data-cs.md)
