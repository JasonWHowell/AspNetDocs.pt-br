---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: Passando dados para exibir páginas-mestre (C#) | Microsoft Docs
author: rick-anderson
description: O objetivo deste tutorial é explicar como você pode passar dados de um controlador para uma página-mestre de exibição. Examinamos duas estratégias para passar dados para uma visão m...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a934f93d89e6530becc114fe455c8b3ab2968de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542476"
---
# <a name="passing-data-to-view-master-pages-c"></a>Transmitir dados para Exibir páginas mestras (C#)

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> O objetivo deste tutorial é explicar como você pode passar dados de um controlador para uma página-mestre de exibição. Examinamos duas estratégias para passar dados para uma página-mestre de exibição. Primeiro, discutimos uma solução fácil que resulta em uma aplicação difícil de manter. Em seguida, examinamos uma solução muito melhor que requer um pouco mais de trabalho inicial, mas resulta em uma aplicação muito mais sustentável.

## <a name="passing-data-to-view-master-pages"></a>Passando dados para exibir páginas-mestre

O objetivo deste tutorial é explicar como você pode passar dados de um controlador para uma página-mestre de exibição. Examinamos duas estratégias para passar dados para uma página-mestre de exibição. Primeiro, discutimos uma solução fácil que resulta em uma aplicação difícil de manter. Em seguida, examinamos uma solução muito melhor que requer um pouco mais de trabalho inicial, mas resulta em uma aplicação muito mais sustentável.

### <a name="the-problem"></a>O problema

Imagine que você está construindo um aplicativo de banco de dados de filmes e deseja exibir a lista de categorias de filmes em cada página em seu aplicativo (ver Figura 1). Imagine, além disso, que a lista de categorias de filmes seja armazenada em uma tabela de banco de dados. Nesse caso, faria sentido recuperar as categorias do banco de dados e renderizar a lista de categorias de filmes dentro de uma página-mestre de exibição.

[![Exibindo categorias de filmes em uma página mestre de exibição](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)

**Figura 01**: Exibindo categorias de filme em uma página-mestre de exibição[(Clique para exibir imagem em tamanho real)](passing-data-to-view-master-pages-cs/_static/image3.png)

Eis o problema. Como você recupera a lista de categorias de filmes na página principal? É tentador chamar métodos de suas classes modelo diretamente na página principal. Em outras palavras, é tentador incluir o código para recuperar os dados do banco de dados em sua página-mestre. No entanto, ignorar seus controladores MVC para acessar o banco de dados violaria a separação limpa de preocupações que é um dos principais benefícios da construção de um aplicativo MVC.

Em um aplicativo MVC, você deseja que toda a interação entre suas visualizações MVC e seu modelo MVC seja tratada por seus controladores MVC. Essa separação de preocupações resulta em uma aplicação mais sustentável, adaptável e testável.

Em um aplicativo MVC, todos os dados passados para uma exibição – incluindo uma página-mestre de exibição – devem ser passados para uma exibição por uma ação do controlador. Além disso, os dados devem ser passados aproveitando os dados de exibição. No restante deste tutorial, examino dois métodos de passar dados de visualização para uma página-mestre de exibição.

### <a name="the-simple-solution"></a>A Solução Simples

Vamos começar com a solução mais simples para passar dados de exibição de um controlador para uma página-mestre de exibição. A solução mais simples é passar os dados de exibição para a página-mestre em cada ação do controlador.

Considere o controlador na Lista 1. Expõe duas ações `Index()` nomeadas e `Details()`. O `Index()` método de ação retorna todos os filmes na tabela de banco de dados Filmes. O `Details()` método de ação retorna todos os filmes em uma categoria de filme em particular.

**Listagem 1 –`Controllers\HomeController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

Observe que tanto as ações Index() quanto as Detalhes() adicionam dois itens para visualizar dados. A ação Index() adiciona duas chaves: categorias e filmes. A chave de categorias representa a lista de categorias de filme exibidas pela página-mestre de exibição. A tecla filmes representa a lista de filmes exibidos pela página 'Índice'.

A ação Detalhes() também adiciona duas chaves nomeadas categorias e filmes. A chave de categorias, mais uma vez, representa a lista de categorias de filmes exibidas pela página-mestre de exibição. A tecla filmes representa a lista de filmes em uma determinada categoria exibida pela página Detalhes (ver Figura 2).

[![A exibição de detalhes](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)

**Figura 02**: A exibição detalhes[(Clique para ver a imagem em tamanho real)](passing-data-to-view-master-pages-cs/_static/image6.png)

A exibição do Índice está contida na Lista 2. Ele simplesmente itera através da lista de filmes representados pelo item de filmes em dados de exibição.

**Listagem 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

A página-mestre de exibição está contida na Lista 3. A página-mestre de visualização itera e renderiza todas as categorias de filme representadas pelo item de categorias a partir de dados de exibição.

**Lista 3 –`Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

Todos os dados são passados para a exibição e para a página-mestre de exibição através de dados de exibição. Essa é a maneira correta de passar dados para a página mestra.

Então, o que há de errado com essa solução? O problema é que essa solução viola o princípio DRY (Não repita a si mesmo). Cada ação do controlador deve adicionar a mesma lista de categorias de filmes para exibir dados. Ter código duplicado em seu aplicativo torna seu aplicativo muito mais difícil de manter, adaptar e modificar.

### <a name="the-good-solution"></a>A Boa Solução

Nesta seção, examinamos uma solução alternativa e melhor para passar dados de uma ação controladora para uma página-mestre de exibição. Em vez de adicionar as categorias de filme para a página mestre em cada ação do controlador, adicionamos as categorias de filme aos dados de exibição apenas uma vez. Todos os dados de exibição usados pela página-mestre de exibição são adicionados em um controlador de aplicativo.

A classe ApplicationController está contida na Lista 4.

**Lista 4 –`Controllers\ApplicationController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

Existem três coisas que você deve notar sobre o controlador de aplicativos na Listagem 4. Primeiro, observe que a classe herda da classe base System.Web.Mvc.Controller. O controlador de aplicativos é uma classe controladora.

Em segundo lugar, observe que a classe controladora de aplicativo é uma classe abstrata. Uma aula abstrata é uma classe que deve ser implementada por uma classe concreta. Como o controlador de aplicativo é uma classe abstrata, você não pode invocar nenhum método definido diretamente na classe. Se você tentar invocar diretamente a classe aplicativo, você receberá uma mensagem de erro Recurso Não Pode Ser Encontrado.

Em terceiro lugar, observe que o controlador de aplicativo contém um construtor que adiciona a lista de categorias de filme para visualizar dados. Cada classe de controlador que herda do controlador de aplicativo chama automaticamente o construtor do controlador de aplicativo. Sempre que você chamar qualquer ação em qualquer controlador que herda do controlador de aplicativos, as categorias de filme são incluídas nos dados de exibição automaticamente.

O controlador Filmes na Lista 5 herda do controlador de aplicativos.

**Lista 5 –`Controllers\MoviesController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

O controlador Filmes, assim como o controlador Home discutido na seção `Index()` `Details()`anterior, expõe dois métodos de ação nomeados e . Observe que a lista de categorias de filme exibidas pela página-mestre `Index()` `Details()` de exibição não é adicionada para exibir dados no método ou no método. Como o controlador De filmes herda do controlador de aplicativos, a lista de categorias de filme é adicionada para visualizar dados automaticamente.

Observe que essa solução para adicionar dados de exibição para uma página-mestre de exibição não viola o princípio DRY (Não repita a si mesmo). O código para adicionar a lista de categorias de filmes para visualizar dados está contido em apenas um local: o construtor para o controlador de aplicativos.

### <a name="summary"></a>Resumo

Neste tutorial, discutimos duas abordagens para passar dados de visualização de um controlador para uma página-mestre de exibição. Primeiro, examinamos uma abordagem simples, mas difícil de manter. Na primeira seção, discutimos como você pode adicionar dados de exibição para uma página-mestre de exibição em cada ação do controlador em seu aplicativo. Concluímos que essa foi uma abordagem ruim porque viola o princípio DRY (Não repita a si mesmo).

Em seguida, examinamos uma estratégia muito melhor para adicionar dados necessários por uma página-mestre de exibição para visualizar dados. Em vez de adicionar os dados de exibição em cada ação do controlador, adicionamos os dados de exibição apenas uma vez dentro de um controlador de aplicativo. Dessa forma, você pode evitar código duplicado ao passar dados para uma página-mestre de exibição em um aplicativo mVC ASP.NET.

> [!div class="step-by-step"]
> [Próximo](creating-page-layouts-with-view-master-pages-cs.md)
> [anterior](asp-net-mvc-views-overview-vb.md)
