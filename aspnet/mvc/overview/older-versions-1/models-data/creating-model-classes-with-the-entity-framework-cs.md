---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: Criando classes de modelo com o Quadro de Entidades (C#) | Microsoft Docs
author: rick-anderson
description: Neste tutorial, você aprende a usar ASP.NET MVC com o Microsoft Entity Framework. Você aprende a usar o Assistente de Entidade para criar uma entidade ADO.NET Da...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 716d34167258b1005b25b1cd11bfaa6d80763320
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542658"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>Criação de classes de modelo com o Entity Framework (C#)

pela [Microsoft](https://github.com/microsoft)

> Neste tutorial, você aprende a usar ASP.NET MVC com o Microsoft Entity Framework. Você aprende a usar o Assistente de Entidade para criar um ADO.NET Modelo de Dados de Entidade. Ao longo deste tutorial, construímos um aplicativo web que ilustra como selecionar, inserir, atualizar e excluir dados de banco de dados usando o Framework de entidades.

O objetivo deste tutorial é explicar como você pode criar classes de acesso a dados usando o Microsoft Entity Framework ao criar um aplicativo mvc ASP.NET. Este tutorial não pressupõe nenhum conhecimento prévio do Microsoft Entity Framework. Ao final deste tutorial, você entenderá como usar o Framework de entidades para selecionar, inserir, atualizar e excluir registros de banco de dados.

O Microsoft Entity Framework é uma ferramenta De mapeamento relacional de objetos (O/RM) que permite gerar uma camada de acesso a dados a partir de um banco de dados automaticamente. O Quadro de Entidades permite evitar o trabalho tedioso de construir suas classes de acesso de dados manualmente.

Para ilustrar como você pode usar o Microsoft Entity Framework com ASP.NET MVC, vamos criar um aplicativo de exemplo simples. Criaremos um aplicativo de banco de dados de filmes que permite que você exiba e edite registros de banco de dados de filmes.

Este tutorial pressupõe que você tenha o Visual Studio 2008 ou visual Web Developer 2008 com o Service Pack 1. Você precisa do Service Pack 1 para usar o Quadro de Entidades. Você pode baixar o Visual Studio 2008 Service Pack 1 ou o Visual Web Developer com o Service Pack 1 a partir do seguinte endereço:

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> Não há conexão essencial entre ASP.NET MVC e o Microsoft Entity Framework. Existem várias alternativas para o Quadro de Entidades que você pode usar com ASP.NET MVC. Por exemplo, você pode construir suas classes mvc model usando outras ferramentas de O/RM, como Microsoft LINQ para SQL, NHibernate ou SubSonic.

## <a name="creating-the-movie-sample-database"></a>Criando o banco de dados de amostras de filmes

O aplicativo Movie Database usa uma tabela de banco de dados chamada Filmes que contém as seguintes colunas:

| Nome da coluna | Tipo de Dados | Permitir nulos? | É a chave primária? |
| --- | --- | --- | --- |
| ID | INT | Falso | True |
| Title | nvarchar(100) | Falso | Falso |
| Diretor | nvarchar(100) | Falso | Falso |

Você pode adicionar esta tabela a um projeto mVC ASP.NET seguindo estas etapas:

1. Clique com o\_botão direito do mouse na pasta Dados do aplicativo na janela Do Explorador de soluções e selecione a opção de menu **Adicionar, Novo Item.**
2. Na caixa de diálogo **Adicionar novo item,** selecione **SQL Server Database**, dê ao banco de dados o nome MoviesDB.mdf e clique no botão **Adicionar.**
3. Clique duas vezes no arquivo MoviesDB.mdf para abrir a janela Server Explorer/Database Explorer.
4. Expanda a conexão de banco de dados MoviesDB.mdf, clique com o botão direito do mouse na pasta Tabelas e selecione a opção de menu **Adicionar nova tabela**.
5. No Table Designer, adicione as colunas Id, Title e Director.
6. Clique no botão **Salvar** (ele tem o ícone do disquete) para salvar a nova tabela com o nome Filmes.

Depois de criar a tabela de banco de dados Filmes, você deve adicionar alguns dados de amostra à tabela. Clique com o botão direito do mouse na tabela Filmes e selecione a opção menu **Mostrar dados da tabela**. Você pode inserir dados falsos de filmes na grade que aparece.

## <a name="creating-the-adonet-entity-data-model"></a>Criando o modelo de dados da entidade ADO.NET

Para usar o Quadro de Entidades, você precisa criar um Modelo de Dados de Entidade. Você pode aproveitar o Visual Studio *Entity Data Model Wizard* para gerar um modelo de dados de entidade a partir de um banco de dados automaticamente.

Siga estas etapas:

1. Clique com o botão direito do mouse na pasta Modelos na janela Do Explorador de soluções e selecione a opção de menu **Adicionar, Novo Item**.
2. Na **caixa de diálogo Adicionar novo item,** selecione a categoria Dados (ver Figura 1).
3. Selecione o modelo **de ADO.NET Modelo de Dados da Entidade,** dê ao Modelo de Dados da Entidade o nome MoviesDBModel.edmx e clique no botão **Adicionar.** Clicar no botão **Adicionar** inicia o Assistente de Modelo de Dados.
4. Na etapa **Escolher conteúdo de modelo,** escolha a **opção Gerar em uma** opção de banco de dados e clique no botão **Seguinte** (consulte Figura 2).
5. Na etapa **Escolher sua conexão de dados,** selecione a conexão de banco de dados MoviesDB.mdf, digite as configurações de conexão de entidades chamada MoviesDBEntities e clique no botão **Seguinte** (consulte Figura 3).
6. Na etapa **Escolher objetos do banco de dados,** selecione a tabela de banco de dados De filme e clique no botão **Concluir** (consulte Figura 4).

Depois de concluir essas etapas, o ADO.NET Entity Data Model Designer (Entity Designer) é aberto.

**Figura 1 – Criação de um novo modelo de dados de entidades**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**Figura 2 – Escolha a etapa de conteúdo do modelo**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**Figura 3 – Escolha sua conexão de dados**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**Figura 4 – Escolha seus objetos de banco de dados**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>Modificando o modelo de dados da entidade ADO.NET

Depois de criar um Modelo de Dados de Entidade, você pode modificar o modelo aproveitando o Entity Designer (ver Figura 5). Você pode abrir o Entity Designer a qualquer momento clicando duas vezes no arquivo MoviesDBModel.edmx contido na pasta Models na janela Solution Explorer.

**Figura 5 – O designer de modelo suidiário de dados ADO.NET**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

Por exemplo, você pode usar o Entity Designer para alterar os nomes das classes que o Assistente de Dados do Modelo de Entidade gera. O Assistente criou uma nova classe de acesso a dados chamada Filmes. Em outras palavras, o Assistente deu à classe o mesmo nome da tabela de banco de dados. Como usaremos essa classe para representar uma instância de filme em particular, devemos renomear a classe de Filmes para Filme.

Se você quiser renomear uma classe de entidade, você pode clicar duas vezes no nome da classe no Entity Designer e inserir um novo nome (ver Figura 6). Alternativamente, você pode alterar o nome de uma entidade na janela Propriedades depois de selecionar uma entidade no Entity Designer.

**Figura 6 – Mudar o nome de uma entidade**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

Lembre-se de salvar seu Modelo de Dados de Entidade depois de fazer uma modificação clicando no botão Salvar (o ícone do disquete). Nos bastidores, o Entity Designer gera um conjunto de classes C#. Você pode visualizar essas classes abrindo o arquivo MoviesDBModel.Designer.cs da janela Solution Explorer.

Não modifique o código no arquivo Designer.cs, pois suas alterações serão substituídas na próxima vez que você usar o Entity Designer. Se você quiser estender a funcionalidade das classes de entidade definidas no arquivo Designer.cs, então você pode criar *classes parciais* em arquivos separados.

#### <a name="selecting-database-records-with-the-entity-framework"></a>Selecionando registros de banco de dados com o Framework da entidade

Vamos começar a construir nosso aplicativo de banco de dados de filmes criando uma página que exibe uma lista de registros de filmes. O controlador Home na Listagem 1 expõe uma ação chamada Index(). A ação Index() retorna todos os registros de filmes da tabela de banco de dados Movie aproveitando o Quadro de Entidades.

**Listagem 1 – Controladores\HomeController.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

Observe que o controlador na Listagem 1 inclui um construtor. O construtor inicia um campo de \_nível de classe chamado db. O \_campo db representa as entidades de banco de dados geradas pelo Microsoft Entity Framework. O \_campo db é uma instância da classe MoviesDBEntities que foi gerada pelo Entity Designer.

Para usar a classeMoviesDBEntities no controlador Home, você deve importar o namespace MovieEntityApp.Models *(MVCProjectName).* Modelos).

O \_campo db é usado dentro da ação Index() para recuperar os registros da tabela de banco de dados Filmes. A \_expressão db. MovieSet representa todos os registros da tabela de banco de dados Filmes. O método ToList() é usado para converter o conjunto de&lt;filmes&gt;em uma coleção genérica de objetos de filme (List Movie ).

Os registros do filme são recuperados com a ajuda de LINQ para Entidades. A ação Index() na Listagem 1 usa *sintaxe do método* LINQ para recuperar o conjunto de registros de banco de dados. Se preferir, você pode usar *a sintaxe de consulta* LINQ. As duas seguintes declarações fazem a mesma coisa:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

Use qualquer sintaxe LINQ – sintaxe de método ou sintaxe de consulta – que você achar mais intuitiva. Não há diferença de desempenho entre as duas abordagens – a única diferença é o estilo.

A exibição na Lista 2 é usada para exibir os registros do filme.

**Listagem 2 – Views\Home\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

A exibição na Lista 2 contém um loop **foreach** que itera através de cada registro de filme e exibe os valores das propriedades título e diretor do registro do filme. Observe que um link Editar e Excluir é exibido ao lado de cada registro. Além disso, um link Adicionar filme é exibido na parte inferior da exibição (ver Figura 7).

**Figura 7 – A visão do Índice**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

A exibição Índice é uma *exibição digitada*. A exibição Índice &lt;inclui uma&gt; diretiva %@ Page % com um atributo *Herdado* que lança a&lt;propriedade Model para uma coleção de lista genérica fortemente digitada de objetos de filme (Filme de lista).

## <a name="inserting-database-records-with-the-entity-framework"></a>Inserindo registros de banco de dados com o Framework da entidade

Você pode usar o Framework entity para facilitar a inserção de novos registros em uma tabela de banco de dados. A listagem 3 contém duas novas ações adicionadas à classe controlador a casa que você pode usar para inserir novos registros na tabela de banco de dados Movie.

**Listagem 3 – Controladores\HomeController.cs (Adicionar métodos)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

A primeira ação Add() simplesmente retorna uma exibição. A exibição contém um formulário para adicionar um novo registro de banco de dados de filmes (ver Figura 8). Quando você envia o formulário, a segunda ação Add() é invocada.

Observe que a segunda ação Add() é decorada com o atributo AcceptVerbs. Esta ação só pode ser invocada ao realizar uma operação HTTP POST. Em outras palavras, esta ação só pode ser invocada ao postar um formulário HTML.

A segunda ação Add() cria uma nova instância da classe Entity Framework Movie com a ajuda do método ASP.NET MVC TryUpdateModel(). O método TryUpdateModel() leva os campos no FormCollection passados para o método Add() e atribui os valores desses campos de formulário HTML à classe Movie.

Ao usar o Quadro de Entidades, você deve fornecer uma "lista branca" de propriedades ao usar os métodos TryUpdateModel ou UpdateModel para atualizar as propriedades de uma classe de entidade.

Em seguida, a ação Adicionar () realiza algumas validaçãos de formulário simples. A ação verifica se as propriedades Título e Diretor possuem valores. Se houver um erro de validação, uma mensagem de erro de validação será adicionada ao ModelState.

Se não houver erros de validação, um novo registro de filme será adicionado à tabela de banco de dados Filmes com a ajuda do Framework entity. O novo registro é adicionado ao banco de dados com as seguintes duas linhas de código:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

A primeira linha de código adiciona a nova entidade Movie ao conjunto de filmes que estão sendo rastreados pelo Entity Framework. A segunda linha de código salva quaisquer alterações que tenham sido feitas nos filmes que estão sendo rastreados de volta ao banco de dados subjacente.

**Figura 8 – A exibição adicionar**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>Atualizando registros de banco de dados com o Framework da entidade

Você pode seguir quase a mesma abordagem para editar um registro de banco de dados com o Framework entity como a abordagem que acabamos de seguir para inserir um novo registro de banco de dados. A lista 4 contém duas novas ações do controlador denominadas Edit(). A primeira ação Editar() retorna um formulário HTML para editar um registro de filme. A segunda ação Editar() tenta atualizar o banco de dados.

**Listagem 4 – Controladores\HomeController.cs (Métodos de edição)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

A segunda ação Edit() começa recuperando o registro de filme do banco de dados que corresponde ao Id do filme que está sendo editado. A seguinte declaração LINQ to Entities captura o primeiro registro de banco de dados que corresponde a um ID específico:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

Em seguida, o método TryUpdateModel() é usado para atribuir os valores dos campos de formulário HTML às propriedades da entidade de filme. Observe que uma lista branca é fornecida para especificar as propriedades exatas a serem atualizadas.

Em seguida, algumas validações simples são realizadas para verificar se as propriedades do Título do Filme e do Diretor têm valores. Se uma propriedade estiver perdendo um valor, então uma mensagem de erro de validação será adicionada ao ModelState e ao ModelState.IsValid retorna o valor falso.

Finalmente, se não houver erros de validação, a tabela de banco de dados De filmes subjacente saem atualizada sem alterações, chamando o método SaveChanges().

Ao editar registros de banco de dados, você precisa passar o Id do registro que está sendo editado para a ação do controlador que realiza a atualização do banco de dados. Caso contrário, a ação do controlador não saberá qual registro atualizar no banco de dados subjacente. A exibição Editar, contida na Lista 5, inclui um campo de formulário oculto que representa o Id do registro de banco de dados que está sendo editado.

**Listagem 5 – Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Excluindo registros de banco de dados com o Framework da entidade

A operação final do banco de dados, que precisamos abordar neste tutorial, é a exclusão de registros de banco de dados. Você pode usar a ação do controlador na Listagem 6 para excluir um registro de banco de dados específico.

**Lista 6 -- \Controllers\HomeController.cs (Exclua ação)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

A ação Excluir() primeiro recupera a entidade Movie que corresponde ao Id passado para a ação. Em seguida, o filme é excluído do banco de dados chamando o método DeleteObject() seguido pelo método SaveChanges(). Finalmente, o usuário é redirecionado de volta para a exibição Índice.

## <a name="summary"></a>Resumo

O objetivo deste tutorial foi demonstrar como você pode construir aplicativos web orientados por banco de dados aproveitando ASP.NET MVC e o Microsoft Entity Framework. Você aprendeu como criar um aplicativo que permite selecionar, inserir, atualizar e excluir registros de banco de dados.

Primeiro, discutimos como você pode usar o Assistente de Modelo de Dados de Entidade para gerar um Modelo de Dados de Entidade de dentro do Visual Studio. Em seguida, você aprende como usar o LINQ para entidades para recuperar um conjunto de registros de banco de dados de uma tabela de banco de dados. Finalmente, usamos o Framework de entidades para inserir, atualizar e excluir registros de banco de dados.

> [!div class="step-by-step"]
> [Avançar](creating-model-classes-with-linq-to-sql-cs.md)
