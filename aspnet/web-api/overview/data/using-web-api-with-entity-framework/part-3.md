---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Usar migrações do Code First para propagar o banco de dados | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59421661"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a>Usar migrações do Code First para propagar o banco de dados

por [Mike Wasson](https://github.com/MikeWasson)

[Baixe o projeto concluído](https://github.com/MikeWasson/BookService)

Nesta seção, você usará [migrações do Code First](https://msdn.microsoft.com/data/jj591621) no EF para propagar o banco de dados com dados de teste.

Dos **ferramentas** menu, selecione **Gerenciador de pacotes NuGet**, em seguida, selecione **Package Manager Console**. Na janela do Console do Gerenciador de pacotes, digite o seguinte comando:

[!code-console[Main](part-3/samples/sample1.cmd)]

Este comando adiciona uma pasta chamada migrações ao seu projeto, além de um arquivo de código chamado Configuration.cs na pasta Migrations.

![](part-3/_static/image1.png)

Abra o arquivo Configuration.cs. Adicione o seguinte **usando** instrução.

[!code-csharp[Main](part-3/samples/sample2.cs)]

Em seguida, adicione o seguinte código para o **Configuration.Seed** método:

[!code-csharp[Main](part-3/samples/sample3.cs)]

Na janela do Console do Gerenciador de pacotes, digite os seguintes comandos:

[!code-console[Main](part-3/samples/sample4.cmd)]

O primeiro comando gera o código que cria o banco de dados e o segundo comando executa esse código. O banco de dados é criado localmente, usando [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>Explorar a API (opcional)

Pressione F5 para executar o aplicativo no modo de depuração. Visual Studio inicia o IIS Express e executa seu aplicativo web. Em seguida, o Visual Studio inicia um navegador e abre a home page do aplicativo.

Quando o Visual Studio executa um projeto da web, ele atribui um número de porta. Na imagem abaixo, o número da porta é 50524. Quando você executa o aplicativo, você verá um número de porta diferente.

![](part-3/_static/image3.png)

A home page é implementada usando o ASP.NET MVC. Na parte superior da página, há um link que diz "API". Este link leva você para uma página de ajuda gerada automaticamente para a API da web. (Para saber como esta página de Ajuda é gerada e como você pode adicionar sua própria documentação para a página, consulte [criando páginas de ajuda para API Web ASP.NET](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) Você pode clicar no menu Ajuda links da página para ver detalhes sobre a API, incluindo o formato de solicitação e resposta.

![](part-3/_static/image4.png)

A API permite que as operações CRUD no banco de dados. O exemplo a seguir resume a API.

| Autores |  |
| --- | -- |
| GET api/authors | Obter todos os autores. |
| GET api/authors/{id} | Obter um autor por ID. |
| POST /api/authors | Crie um novo autor. |
| PUT /api/authors/{id} | Atualize um autor existente. |
| DELETE /api/authors/{id} | Exclua um autor. |

| Livros |  |
| --- | -- |
| GET /api/books | Obter todos os livros. |
| GET /api/books/{id} | Obtenha um livro por ID. |
| POST /api/books | Crie um novo catálogo. |
| PUT /api/books/{id} | Atualize um livro existente. |
| DELETE /api/books/{id} | Exclua um livro. |

## <a name="view-the-database-optional"></a>Exibir o banco de dados (opcional)

Quando você executou o comando Update-Database, o EF criou o banco de dados e chamado a `Seed` método. Quando você executa o aplicativo localmente, o EF usa [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx). Você pode exibir o banco de dados no Visual Studio. Dos **modo de exibição** menu, selecione **Pesquisador de objetos do SQL Server**.

![](part-3/_static/image5.png)

No **conectar ao servidor** caixa de diálogo, no **nome do servidor** caixa de edição, digite "\v11.0 (localdb)". Deixe o **autenticação** opção como "Autenticação do Windows". Clique em **Conectar**.

![](part-3/_static/image6.png)

Visual Studio se conecta ao LocalDB e mostra os bancos de dados existentes na janela do Pesquisador de objetos do SQL Server. Você pode expandir os nós para ver as tabelas que criou o EF.

![](part-3/_static/image7.png)

Para exibir os dados, uma tabela com o botão direito e selecione **exibir dados**.

![](part-3/_static/image8.png)

Captura de tela a seguir mostra os resultados da tabela livros. Observe que o EF preenchido com os dados de propagação do banco de dados e a tabela contém a chave estrangeira à tabela autores.

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [Anterior](part-2.md)
> [Próximo](part-4.md)
