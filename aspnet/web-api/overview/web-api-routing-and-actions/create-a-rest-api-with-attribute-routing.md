---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: Criar uma API REST com roteamento de atributos no ASP.NET Web API 2 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188751"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>Criar uma API REST com roteamento de atributos no ASP.NET Web API 2

por [Mike Wasson](https://github.com/MikeWasson)

A API da Web 2 dá suporte a um novo tipo de roteamento, chamado *Roteamento de atributos*. Para obter uma visão geral do roteamento de atributos, consulte [Roteamento de atributos na API Web 2](attribute-routing-in-web-api-2.md). Neste tutorial, você usará o roteamento de atributos para criar uma API REST para uma coleção de livros. A API dará suporte às seguintes ações:

| Ação | URI de exemplo |
| --- | --- |
| Obtenha uma lista de todos os livros. | /api/books |
| Obter um livro por ID. | /api/books/1 |
| Obtenha os detalhes de um livro. | /api/books/1/details |
| Obter uma lista de livros por gênero. | /api/books/fantasy |
| Obter uma lista de livros por data de publicação. | /API/Books/Date/2013-02-16/API/Books/Date/2013/02/16 (formulário alternativo) |
| Obtenha uma lista de livros por um autor específico. | /api/authors/1/books |

Todos os métodos são somente leitura (solicitações HTTP GET).

Para a camada de dados, usaremos Entity Framework. Os registros de livros terão os seguintes campos:

- ID
- Título
- Gênero
- Data da publicação
- Preço
- Descrição
- AuthorId (chave estrangeira para uma tabela de autores)

No entanto, para a maioria das solicitações, a API retornará um subconjunto desses dados (título, autor e gênero). Para obter o registro completo, o cliente solicita `/api/books/{id}/details` .

## <a name="prerequisites"></a>Pré-requisitos

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional ou Enterprise Edition.

## <a name="create-the-visual-studio-project"></a>Criar o projeto do Visual Studio

Comece executando o Visual Studio. No menu **arquivo** , selecione **novo** e **projeto**.

Expanda **Installed**a  >  categoria**Visual C#** instalada. Em **Visual C#**, selecione **Web**. Na lista de modelos de projeto, selecione **ASP.NET aplicativo Web (.NET Framework)**. Nomeie o projeto &quot; BooksAPI &quot; .

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

Na caixa de diálogo **novo aplicativo Web ASP.net** , selecione o modelo **vazio** . Em "adicionar pastas e referências principais para", marque a caixa de seleção **API da Web** . Clique em **OK**.

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

Isso cria um projeto de esqueleto configurado para a funcionalidade da API Web.

### <a name="domain-models"></a>Modelos de domínio

Em seguida, adicione classes para modelos de domínio. No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Modelos. Selecione **Adicionar**e selecione **classe**. Nome da classe `Author`.

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

Substitua o código em Author.cs pelo seguinte:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

Agora, adicione outra classe chamada `Book` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>Adicionar um controlador de API Web

Nesta etapa, adicionaremos um controlador de API da Web que usa Entity Framework como a camada de dados.

Pressione CTRL+SHIFT+B para criar o projeto. Entity Framework usa a reflexão para descobrir as propriedades dos modelos, portanto, ele requer um assembly compilado para criar o esquema de banco de dados.

No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Controladores. Selecione **Adicionar**e, em seguida, selecione **controlador**.

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

Na caixa de diálogo **Adicionar Scaffold** , selecione **controlador da API Web 2 com ações, usando Entity Framework**.

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

Na caixa de diálogo **Adicionar controlador** , para **nome do controlador**, insira &quot; BooksController &quot; . Marque a &quot; caixa de seleção Usar ações do controlador assíncrono &quot; . Para **classe de modelo**, selecione &quot; livro &quot; . (Se você não vir a `Book` classe listada no menu suspenso, certifique-se de que você criou o projeto.) Em seguida, clique no botão "+".

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

Clique em **Adicionar** na caixa de diálogo **novo contexto de dados** .

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

Clique em **Adicionar** na caixa de diálogo **Adicionar controlador** . O scaffolding adiciona uma classe chamada `BooksController` que define o controlador da API. Ele também adiciona uma classe chamada `BooksAPIContext` na pasta modelos, que define o contexto de dados para Entity Framework.

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>Propagar o banco de dados

No menu ferramentas, selecione **Gerenciador de pacotes NuGet**e, em seguida, selecione **console do Gerenciador de pacotes**.

Na janela Console do Gerenciador de Pacotes, digite o seguinte comando:

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

Esse comando cria uma pasta migrações e adiciona um novo arquivo de código chamado Configuration.cs. Abra esse arquivo e adicione o código a seguir ao `Configuration.Seed` método.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

Na janela do console do Gerenciador de pacotes, digite os comandos a seguir.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

Esses comandos criam um banco de dados local e invocam o método semente para preencher o banco de dados.

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>Adicionar classes DTO

Se você executar o aplicativo agora e enviar uma solicitação GET para/API/Books/1, a resposta será semelhante à seguinte. (Adicionei o recuo para facilitar a leitura.)

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

Em vez disso, quero que essa solicitação retorne um subconjunto dos campos. Além disso, quero que ele retorne o nome do autor, em vez da ID do autor. Para fazer isso, modificaremos os métodos do controlador para retornar um DTO ( *objeto de transferência de dados* ) em vez do modelo do EF. Um DTO é um objeto projetado apenas para transportar dados.

Em Gerenciador de soluções, clique com o botão direito do mouse no projeto e selecione **Adicionar**  |  **nova pasta**. Nomeie a pasta &quot; DTOs &quot; . Adicione uma classe chamada `BookDto` à pasta DTOs, com a seguinte definição:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

Adicione outra classe chamada `BookDetailDto`.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

Em seguida, atualize a `BooksController` classe para retornar `BookDto` instâncias. Usaremos o método [consultável. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) para projetar `Book` instâncias para `BookDto` instâncias. Este é o código atualizado para a classe Controller.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> Excluí os `PutBook` métodos, `PostBook` e `DeleteBook` , porque eles não são necessários para este tutorial.

Agora, se você executar o aplicativo e solicitar/API/Books/1, o corpo da resposta deverá ser assim:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>Adicionar atributos de rota

Em seguida, converteremos o controlador para usar o roteamento de atributos. Primeiro, adicione um atributo **RoutePrefix** ao controlador. Esse atributo define os segmentos de URI iniciais para todos os métodos neste controlador.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

Em seguida, adicione atributos **[Route]** às ações do controlador, da seguinte maneira:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

O modelo de rota para cada método de controlador é o prefixo mais a cadeia de caracteres especificada no atributo de **rota** . Para o `GetBook` método, o modelo de rota inclui a cadeia de caracteres com parâmetros &quot; {ID: int} &quot; , que corresponde se o segmento URI contém um valor inteiro.

| Método | Modelo de rota | URI de exemplo |
| --- | --- | --- |
| `GetBooks` | "API/livros" | `http://localhost/api/books` |
| `GetBook` | "API/Books/{ID: int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>Obter detalhes do livro

Para obter detalhes do livro, o cliente enviará uma solicitação GET para `/api/books/{id}/details` , onde *{ID}* é a ID do livro.

Adicione o método a seguir à classe `BooksController`.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

Se você solicitar `/api/books/1/details` , a resposta terá esta aparência:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>Obter livros por gênero

Para obter uma lista de livros em um gênero específico, o cliente enviará uma solicitação GET para `/api/books/genre` , onde *gênero* é o nome do gênero. (Por exemplo, `/api/books/fantasy`.)

Adicione o método a seguir a `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

Aqui, estamos definindo uma rota que contém um parâmetro {gênero} no modelo de URI. Observe que a API da Web é capaz de distinguir esses dois URIs e roteá-los para métodos diferentes:

`/api/books/1`

`/api/books/fantasy`

Isso ocorre porque o `GetBook` método inclui uma restrição que o segmento "ID" deve ser um valor inteiro:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

Se você solicitar/API/Books/Fantasy, a resposta terá esta aparência:

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>Obter livros por autor

Para obter uma lista de livros de um determinado autor, o cliente enviará uma solicitação GET para `/api/authors/id/books` , onde *ID* é a ID do autor.

Adicione o método a seguir a `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

Este exemplo é interessante porque os &quot; livros &quot; são tratados como um recurso filho de &quot; autores &quot; . Esse padrão é bastante comum em APIs RESTful.

O til (~) no modelo de rota substitui o prefixo de rota no atributo **RoutePrefix** .

## <a name="get-books-by-publication-date"></a>Obter livros por data de publicação

Para obter uma lista de livros por data de publicação, o cliente enviará uma solicitação GET para `/api/books/date/yyyy-mm-dd` , onde *aaaa-mm-dd* é a data.

Aqui está uma maneira de fazer isso:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

O `{pubdate:datetime}` parâmetro é restrito para corresponder a um valor **DateTime** . Isso funciona, mas, na verdade, é mais permissivo do que gostaríamos. Por exemplo, esses URIs também corresponderão à rota:

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

Não há nada de errado ao permitir esses URIs. No entanto, você pode restringir a rota para um formato específico adicionando uma restrição de expressão regular ao modelo de rota:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

Agora, somente as datas no formato &quot; aaaa-mm-dd &quot; corresponderão. Observe que não usamos o Regex para validar que obtemos uma data real. Isso é tratado quando a API Web tenta converter o segmento URI em uma instância **DateTime** . Uma data inválida, como ' 2012-47-99 ', não será convertida e o cliente receberá um erro 404.

Você também pode dar suporte a um separador de barra ( `/api/books/date/yyyy/mm/dd` ) adicionando outro atributo **[Route]** com um Regex diferente.

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

Há um detalhe sutil, mas importante, aqui. O segundo modelo de rota tem um caractere curinga ( \* ) no início do parâmetro {pubDate}:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

Isso informa ao mecanismo de roteamento que {pubDate} deve corresponder ao restante do URI. Por padrão, um parâmetro de modelo corresponde a um único segmento de URI. Nesse caso, queremos que {pubDate} abranja vários segmentos URI:

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>Código do controlador

Aqui está o código completo para a classe BooksController.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>Resumo

O roteamento de atributos oferece mais controle e maior flexibilidade ao criar URIs para sua API.
