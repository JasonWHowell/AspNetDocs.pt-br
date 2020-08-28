---
uid: mvc/overview/getting-started/introduction/adding-search
title: Pesquisar | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: be4e4d13e574b0fcb77d2d0fb8c6f58041b1ece2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044820"
---
# <a name="search"></a>Search

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="adding-a-search-method-and-search-view"></a>Adicionando um método de pesquisa e uma exibição de pesquisa

Nesta seção, você adicionará a funcionalidade de pesquisa ao `Index` método de ação que permite pesquisar filmes por gênero ou por nome.

## <a name="prerequisites"></a>Pré-requisitos

Para corresponder às capturas de tela desta seção, você precisa executar o aplicativo (F5) e adicionar os filmes a seguir ao banco de dados.

| Título | Data de lançamento | Gênero | Preço |
| ----- | ------------ | ----- | ----- |
| Ghostbusters | 6/8/1984 | Comédia | 6,99 |
| Ghostbusters II | 6/16/1989 | Comédia | 6,99 |
| Planeta da Apes | 3/27/1986 | Ação | 5,99 |

## <a name="updating-the-index-form"></a>Atualizando o formulário de índice

Comece atualizando o `Index` método de ação para a `MoviesController` classe existente. O código é o seguinte:

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

A primeira linha do `Index` método cria a seguinte consulta [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) para selecionar os filmes:

[!code-csharp[Main](adding-search/samples/sample2.cs)]

A consulta é definida neste ponto, mas ainda não foi executada no banco de dados.

Se o `searchString` parâmetro contiver uma cadeia de caracteres, a consulta de filmes será modificada para filtrar o valor da cadeia de caracteres de pesquisa, usando o seguinte código:

[!code-csharp[Main](adding-search/samples/sample3.cs)]

O código `s => s.Title` acima é uma [Expressão Lambda](https://msdn.microsoft.com/library/bb397687.aspx). As Lambdas são usadas em consultas [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) baseadas em método como argumentos para métodos de operador de consulta padrão, como o método [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) usado no código acima. Consultas LINQ não são executadas quando são definidas ou quando são modificadas chamando um método como `Where` ou `OrderBy` . Em vez disso, a execução da consulta é adiada, o que significa que a avaliação de uma expressão é adiada até que seu valor percebido seja realmente iterado ou o [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) método seja chamado. No `Search` exemplo, a consulta é executada na exibição *index. cshtml* . Para obter mais informações sobre a execução de consulta adiada, consulte [Execução da consulta](https://msdn.microsoft.com/library/bb738633.aspx).

> [!NOTE]
> O método [Contains](https://msdn.microsoft.com/library/bb155125.aspx) é executado no banco de dados, não no código c# acima. No banco de dados, [contém](https://msdn.microsoft.com/library/bb155125.aspx) mapas para [SQL como](https://msdn.microsoft.com/library/ms179859.aspx), que não diferencia maiúsculas de minúsculas.

Agora você pode atualizar a `Index` exibição que exibirá o formulário para o usuário.

Execute o aplicativo e navegue até */Movies/index*. Acrescente uma cadeia de consulta, como `?searchString=ghost`, à URL. Os filmes filtrados são exibidos.

![SearchQryStr](adding-search/_static/image1.png)

Se você alterar a assinatura do `Index` método para ter um parâmetro chamado `id` , o `id` parâmetro corresponderá ao `{id}` espaço reservado para as rotas padrão definidas no arquivo * \_ Start\RouteConfig.cs do aplicativo* .

[!code-json[Main](adding-search/samples/sample4.txt)]

O `Index` método original tem esta aparência::

[!code-csharp[Main](adding-search/samples/sample5.cs)]

O `Index` método modificado seria semelhante ao seguinte:

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

Agora você pode passar o título de pesquisa como dados de rota (um segmento de URL), em vez de como um valor de cadeia de consulta.

![](adding-search/_static/image2.png)

No entanto, você não pode esperar que os usuários modifiquem a URL sempre que desejarem pesquisar um filme. Portanto, agora você adicionará uma interface do usuário para ajudá-los a filtrar os filmes. Se você alterou a assinatura do `Index` método para testar como passar o parâmetro de ID de associação de rota, altere-o de volta para que o `Index` método aceite um parâmetro de cadeia de caracteres chamado `searchString` :

[!code-csharp[Main](adding-search/samples/sample7.cs)]

Abra o arquivo *Views\Movies\Index.cshtml* e, logo após `@Html.ActionLink("Create New", "Create")` , adicione a marcação de formulário realçada abaixo:

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

O `Html.BeginForm` auxiliar cria uma marca de abertura `<form>` . O `Html.BeginForm` auxiliar faz com que o formulário seja Postado para si mesmo quando o usuário envia o formulário clicando no botão de **filtro** .

Visual Studio 2013 tem uma boa melhoria ao exibir e editar arquivos de exibição. Quando você executa o aplicativo com um arquivo de exibição aberto, Visual Studio 2013 invoca o método de ação do controlador correto para exibir a exibição.

![](adding-search/_static/image3.png)

Com a exibição de índice aberta no Visual Studio (conforme mostrado na imagem acima), toque em CTR F5 ou F5 para executar o aplicativo e, em seguida, tente pesquisar um filme.

![](adding-search/_static/image4.png)

Não há `HttpPost` sobrecarga do `Index` método. Você não precisa dele, porque o método não está alterando o estado do aplicativo, apenas filtrando os dados.

Você poderá adicionar o método `HttpPost Index` a seguir. Nesse caso, o chamador de ação corresponderia ao `HttpPost Index` método e o `HttpPost Index` método seria executado conforme mostrado na imagem abaixo.

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

No entanto, mesmo se você adicionar esta versão `HttpPost` do método `Index`, haverá uma limitação na forma de como isso tudo foi implementado. Imagine que você deseja adicionar uma pesquisa específica como Favoritos ou enviar um link para seus amigos para que eles possam clicar para ver a mesma lista filtrada de filmes. Observe que a URL para a solicitação HTTP POST é igual à URL da solicitação GET (localhost: xxxxx/Movies/index) – não há informações de pesquisa na própria URL. No momento, as informações de cadeia de caracteres de pesquisa são enviadas ao servidor como um valor de campo de formulário. Isso significa que você não pode capturar essas informações de pesquisa para indicar ou enviar para amigos em uma URL.

A solução é usar uma sobrecarga de `BeginForm` que especifica que a solicitação POST deve adicionar as informações de pesquisa à URL e que ela deve ser roteada para a `HttpGet` versão do `Index` método. Substitua o `BeginForm` método sem parâmetros existente pela seguinte marcação:

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

Agora, quando você envia uma pesquisa, a URL contém uma cadeia de caracteres de consulta de pesquisa. A pesquisa também irá para o método de ação `HttpGet Index`, mesmo se você tiver um método `HttpPost Index`.

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>Adicionando pesquisa por gênero

Se você adicionou a `HttpPost` versão do `Index` método, exclua-a agora.

Em seguida, você adicionará um recurso para permitir que os usuários pesquisem filmes por gênero. Substitua o método `Index` pelo seguinte código:

[!code-csharp[Main](adding-search/samples/sample11.cs)]

Essa versão do `Index` método usa um parâmetro adicional, ou seja, `movieGenre` As primeiras linhas de código criam um `List` objeto para conter gêneros de filme do banco de dados.

O código a seguir é uma consulta LINQ que recupera todos os gêneros do banco de dados.

[!code-csharp[Main](adding-search/samples/sample12.cs)]

O código usa o `AddRange` método da coleção genérica `List` para adicionar todos os gêneros distintos à lista. (Sem o `Distinct` modificador, os gêneros duplicados seriam adicionados; por exemplo, comédia seria adicionado duas vezes em nosso exemplo). Em seguida, o código armazena a lista de gêneros no `ViewBag.MovieGenre` objeto. Armazenar dados de categoria (como gêneros de filme) como um objeto [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) em um `ViewBag` , acessando os dados da categoria em uma caixa de listagem suspensa é uma abordagem típica para aplicativos MVC.

O código a seguir mostra como verificar o `movieGenre` parâmetro. Se não estiver vazio, o código restringirá ainda mais a consulta de filmes para limitar os filmes selecionados ao gênero especificado.

[!code-csharp[Main](adding-search/samples/sample13.cs)]

Como mencionado anteriormente, a consulta não é executada no banco de dados até que a lista de filmes seja iterada (o que acontece na exibição, após o `Index` retorno do método de ação).

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>Adicionando marcação à exibição de índice para dar suporte à pesquisa por gênero

Adicione um `Html.DropDownList` auxiliar ao arquivo *Views\Movies\Index.cshtml* , logo antes do `TextBox` auxiliar. A marcação concluída é mostrada abaixo:

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

No seguinte código:

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

O parâmetro "MovieGenre" fornece a chave para o `DropDownList` auxiliar localizar um `IEnumerable<SelectListItem>` no `ViewBag` . O `ViewBag` foi populado no método de ação:

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

O parâmetro "All" fornece um rótulo de opção. Se você inspecionar essa escolha em seu navegador, verá que seu atributo "value" está vazio. Como nosso controlador apenas filtra `if` a cadeia de caracteres não está `null` ou vazia, o envio de um valor vazio para `movieGenre` mostra todos os gêneros.

Você também pode definir uma opção para ser selecionada por padrão. Se você quisesse "comédia" como a opção padrão, altere o código no controlador da seguinte forma:

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

Execute o aplicativo e navegue até */Movies/index*. Experimente uma pesquisa por gênero, por nome de filme e por ambos os critérios.

![](adding-search/_static/image8.png)

Nesta seção, você criou um método de ação de pesquisa e uma exibição que permitem que os usuários pesquisem por título e gênero do filme. Na próxima seção, você examinará como adicionar uma propriedade ao `Movie` modelo e como adicionar um inicializador que criará automaticamente um banco de dados de teste.

> [!div class="step-by-step"]
> [Anterior](examining-the-edit-methods-and-edit-view.md) 
>  [Avançar](adding-a-new-field.md)
