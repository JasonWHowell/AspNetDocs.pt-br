---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: Exibindo uma Tabela de Dados de Banco de Dados (C#) | Microsoft Docs
author: rick-anderson
description: Neste tutorial, eu demonstrei dois métodos de exibição de um conjunto de registros de banco de dados. Eu mostro dois métodos de formatação de um conjunto de registros de banco de dados em um HTML ta...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3fca8ac9e9b4e549ca76ffa282cc03aa4cc50e88
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542021"
---
# <a name="displaying-a-table-of-database-data-c"></a>Exibir uma tabela de dados de banco de dados (C#)

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> Neste tutorial, eu demonstrei dois métodos de exibição de um conjunto de registros de banco de dados. Eu mostro dois métodos de formatação de um conjunto de registros de banco de dados em uma tabela HTML. Primeiro, eu mostro como você pode formatar os registros do banco de dados diretamente dentro de uma exibição. Em seguida, eu demonstrei como você pode tirar proveito das parciais ao formatação de registros de banco de dados.

O objetivo deste tutorial é explicar como você pode exibir uma tabela HTML de dados de banco de dados em um aplicativo mvc ASP.NET. Primeiro, você aprende a usar as ferramentas de andaimes incluídas no Visual Studio para gerar uma visualização que exibe um conjunto de registros automaticamente. Em seguida, você aprende a usar uma parcial como modelo ao formatação de registros de banco de dados.

## <a name="create-the-model-classes"></a>Criar as classes modelo

Vamos exibir o conjunto de registros da tabela de banco de dados Filmes. A tabela de banco de dados Filmes contém as seguintes colunas:

<a id="0.3_table01"></a>

| **Nome da coluna** | **Tipo de dados** | **Permitir Nulos** |
| --- | --- | --- |
| ID | Int | Falso |
| Title | Nvarchar(200) | Falso |
| Diretor | NVarchar(50) | Falso |
| Data lançada | Datetime | Falso |

Para representar a tabela Filmes em nosso ASP.NET aplicativo MVC, precisamos criar uma classe modelo. Neste tutorial, usamos o Microsoft Entity Framework para criar nossas classes de modelos.

> [!NOTE] 
> 
> Neste tutorial, usamos o Microsoft Entity Framework. No entanto, é importante entender que você pode usar uma variedade de tecnologias diferentes para interagir com um banco de dados de um aplicativo mvc ASP.NET, incluindo LINQ para SQL, NHibernate ou ADO.NET.

Siga estas etapas para iniciar o Assistente do Modelo de Dados da Entidade:

1. Clique com o botão direito do mouse na pasta Modelos na janela Solution Explorer e selecione a opção **menu Adicionar, Novo Item**.
2. Selecione a categoria **Dados** e selecione o modelo **ADO.NET Modelo de Dados de Entidade.**
3. Dê ao seu modelo de dados o nome *MoviesDBModel.edmx* e clique no botão **Adicionar.**

Depois de clicar no botão Adicionar, o Assistente do Modelo de Dados da Entidade aparecerá (consulte Figura 1). Siga estas etapas para completar o assistente:

1. Na etapa **Escolher conteúdo de modelo,** selecione a opção **Gerar do banco de dados.**
2. Na etapa **Escolha sua conexão de dados,** use a conexão de dados *MoviesDB.mdf* e o nome *MoviesDBEntities* para as configurações de conexão. Clique no botão **Avançar**.
3. Na etapa **Escolher objetos do banco de dados,** expanda o nó Tabelas, selecione a tabela Filmes. Digite o namespace *Models* e clique no botão **Concluir.**

[![Criando aulas de LINQ para SQL](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)

**Figura 01**: Criação de classes LINQ para SQL[(Clique para exibir imagem em tamanho real)](displaying-a-table-of-database-data-cs/_static/image2.png)

Depois de concluir o Assistente do Modelo de Dados da Entidade, o Designer de Modelo de Dados de Entidade será aberto. O Designer deve exibir a entidade Filmes (ver Figura 2).

[![O Designer de Modelos de Dados da Entidade](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)

**Figura 02**: O Designer do Modelo de Dados da Entidade[(Clique para ver a imagem em tamanho real)](displaying-a-table-of-database-data-cs/_static/image4.png)

Precisamos fazer uma mudança antes de continuarmos. O Entity Data Wizard gera uma classe modelo chamada *Filmes* que representa a tabela de banco de dados Filmes. Como usaremos a classe Filmes para representar um determinado filme, precisamos modificar o nome da classe para ser *Filme* em vez de *Filmes* (singular em vez de plural).

Clique duas vezes no nome da classe na superfície do designer e mude o nome da classe de Filmes para Filme. Depois de fazer essa alteração, clique no botão **Salvar** (o ícone do disquete) para gerar a classe Movie.

## <a name="create-the-movies-controller"></a>Criar o controlador de filmes

Agora que temos uma maneira de representar nossos registros de banco de dados, podemos criar um controlador que retorna a coleção de filmes. Na janela Visual Studio Solution Explorer, clique com o botão direito do mouse na pasta Controladores e selecione a opção de menu **Adicionar, Controlador** (ver Figura 3).

[![O menu do controlador de adicionação](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)

**Figura 03**: O menu Adicionar controlador[(Clique para ver a imagem em tamanho real)](displaying-a-table-of-database-data-cs/_static/image6.png)

Quando a caixa de diálogo **Adicionar controlador** for exibida, digite o nome do controlador MovieController (consulte Figura 4). Clique no botão **Adicionar** para adicionar o novo controlador.

[![A caixa de diálogo Adicionar controlador](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)

**Figura 04**: A caixa de diálogo Adicionar controlador[(Clique para exibir a imagem em tamanho real)](displaying-a-table-of-database-data-cs/_static/image8.png)

Precisamos modificar a ação Index() exposta pelo controlador Movie para que ele retorne o conjunto de registros de banco de dados. Modifique o controlador para que ele se pareça com o controlador na Listagem 1.

**Listagem 1 – Controladores\MovieController.cs**

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

Na Lista 1, a classe MoviesDBEntities é usada para representar o banco de dados MoviesDB. Para usar esta classe, você precisa importar o espaço de nome MvcApplication1.Models como este:

usando MvcApplication1.Models;

As *entidades de expressão. MovieSet.ToList()* retorna o conjunto de todos os filmes da tabela de banco de dados Filmes.

## <a name="create-the-view"></a>Criar a exibição

A maneira mais fácil de exibir um conjunto de registros de banco de dados em uma tabela HTML é aproveitar os andaimes fornecidos pelo Visual Studio.

Construa seu aplicativo selecionando a opção de menu **Build, Build Solution**. Você deve construir seu aplicativo antes de abrir a caixa de diálogo **Adicionar exibição** ou suas classes de dados não aparecerão na caixa de diálogo.

Clique com o botão direito do mouse na ação Índice() e selecione a opção de menu **Adicionar exibição** (ver Figura 5).

[![Adicionando uma visualização](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)

**Figura 05**: Adicionando uma exibição[(Clique para exibir imagem em tamanho real)](displaying-a-table-of-database-data-cs/_static/image10.png)

Na **caixa de** diálogo Adicionar exibição, marque a caixa de seleção rotulada **Criar uma exibição fortemente digitada**. Selecione a classe Movie como a **classe de dados de exibição**. Selecione *Lista* como o conteúdo da **exibição** (ver Figura 6). A seleção dessas opções gerará uma exibição fortemente digitada que exibe uma lista de filmes.

[![A caixa de diálogo Adicionar exibição](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)

**Figura 06**: A caixa de diálogo Adicionar exibição[(Clique para exibir a imagem em tamanho real)](displaying-a-table-of-database-data-cs/_static/image12.png)

Depois de clicar no botão **Adicionar,** a exibição na Listagem 2 é gerada automaticamente. Esta exibição contém o código necessário para iterar através da coleção de filmes e exibir cada uma das propriedades de um filme.

**Listagem 2 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

Você pode executar o aplicativo selecionando a opção de menu **Debug, Start Debugging** (ou apertando a tecla F5). A execução do aplicativo inicia o Internet Explorer. Se você navegar até a URL /Movie, então você verá a página na Figura 7.

[![Uma tabela de filmes](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)

**Figura 07**: Uma tabela de filmes[(Clique para ver imagem em tamanho real)](displaying-a-table-of-database-data-cs/_static/image14.png)

Se você não gosta de nada sobre o aparecimento da grade de registros de banco de dados na Figura 7, então você pode simplesmente modificar a exibição Índice. Por exemplo, você pode alterar o cabeçalho *DateReleased* para *Date Released* modificando a exibição Índice.

## <a name="create-a-template-with-a-partial"></a>Crie um modelo com um parcial

Quando uma vista fica muito complicada, é uma boa ideia começar a dividir a vista em parciais. O uso de parciais torna seus pontos de vista mais fáceis de entender e manter. Criaremos uma parcial que podemos usar como modelo para formatar cada um dos registros do banco de dados de filmes.

Siga estas etapas para criar a parcial:

1. Clique com o botão direito do mouse na pasta Views\Movie e selecione a opção de menu **Adicionar exibição**.
2. Verifique a caixa de seleção rotulada *Criar uma exibição parcial (.ascx)*.
3. Nomeie o Modelo de *Filme parcial*.
4. Verifique a caixa de seleção rotulada **Criar uma exibição fortemente digitada**.
5. Selecione Filme como a *classe de dados de exibição*.
6. Selecione Esvaziar como o conteúdo da *exibição*.
7. Clique no botão **Adicionar** para adicionar a parcial ao seu projeto.

Depois de concluir essas etapas, modifique a parcial MovieTemplate para parecer a Lista 3.

**Listagem 3 – Views\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

A parcial na Lista 3 contém um modelo para uma única linha de registros.

A exibição Índice modificado na Listagem 4 usa a parcial MovieTemplate.

**Listagem 4 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

A exibição na Lista 4 contém um loop forecada que itera em todos os filmes. Para cada filme, a parcial MovieTemplate é usada para formatar o filme. O MovieTemplate é renderizado chamando o método de ajuda RenderPartial().

A exibição Índice modificado torna a mesma tabela HTML de registros de banco de dados. No entanto, a visão foi muito simplificada.

O método RenderPartial() é diferente da maioria dos outros métodos auxiliares porque não retorna uma string. Portanto, você deve chamar o método &lt;RenderPartial() usando % Html.RenderPartial(); %&gt; em &lt;vez de %= Html.RenderPartial(); %&gt;.

## <a name="summary"></a>Resumo

O objetivo deste tutorial foi explicar como você pode exibir um conjunto de registros de banco de dados em uma tabela HTML. Primeiro, você aprendeu como retornar um conjunto de registros de banco de dados de uma ação do controlador, aproveitando o Microsoft Entity Framework. Em seguida, você aprendeu a usar andaimes do Visual Studio para gerar uma visão que exibe uma coleção de itens automaticamente. Finalmente, você aprendeu a simplificar a visão aproveitando uma parcial. Você aprendeu a usar uma parcial como modelo para que você possa formatar cada registro de banco de dados.

> [!div class="step-by-step"]
> [Próximo](creating-model-classes-with-linq-to-sql-cs.md)
> [anterior](performing-simple-validation-cs.md)
