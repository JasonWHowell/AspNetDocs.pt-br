---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: Adicionando conteúdo dinâmico a uma página em cache (VB) | Microsoft Docs
author: rick-anderson
description: Aprenda a misturar conteúdo dinâmico e armazenado em cache na mesma página. A substituição pós-cache permite que você exiba conteúdo dinâmico, como anúncios de banner o...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ed022fc560becbd21722b94f2428cf7b32f2635
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542255"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a>Adicionar conteúdo dinâmico a uma página em cache (VB)

pela [Microsoft](https://github.com/microsoft)

> Aprenda a misturar conteúdo dinâmico e armazenado em cache na mesma página. A substituição pós-cache permite que você exiba conteúdo dinâmico, como anúncios de banner ou itens de notícias, dentro de uma página que tenha sido armazenada em cache.

Aproveitando o cache de saída, você pode melhorar drasticamente o desempenho de um ASP.NET aplicativo MVC. Em vez de regenerar uma página toda vez que a página é solicitada, a página pode ser gerada uma vez e armazenada em cache na memória para vários usuários.

Mas há um problema. E se você precisar exibir conteúdo dinâmico na página? Por exemplo, imagine que você deseja exibir um banner na página. Você não quer que o anúncio do banner seja armazenado em cache para que cada usuário veja o mesmo anúncio. Você não faria dinheiro assim!

Felizmente, há uma solução fácil. Você pode tirar proveito de um recurso da estrutura de ASP.NET chamada *substituição pós-cache*. A substituição pós-cache permite substituir o conteúdo dinâmico em uma página que foi armazenada em cache na memória.

Normalmente, quando você faz cache &lt;de&gt; uma página usando o atributo OutputCache, a página é armazenada em cache tanto no servidor quanto no cliente (o navegador da Web). Quando você usa a substituição pós-cache, uma página é armazenada em cache apenas no servidor.

#### <a name="using-post-cache-substitution"></a>Usando a substituição pós-cache

O uso da substituição pós-cache requer duas etapas. Primeiro, você precisa definir um método que retorne uma string que represente o conteúdo dinâmico que você deseja exibir na página armazenada em cache. Em seguida, você chama o método HttpResponse.WriteReplacement() para injetar o conteúdo dinâmico na página.

Imagine, por exemplo, que você deseja exibir aleatoriamente diferentes itens de notícias em uma página armazenada em cache. A classe na Listagem 1 expõe um único método, chamado RenderNews(), que retorna aleatoriamente um item de notícias de uma lista de três itens de notícias.

**Listagem 1 – Modelos\News.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

Para aproveitar a substituição pós-cache, você chama o método HttpResponse.WriteReplacement(). O método WriteReplacement() configura o código para substituir uma região da página armazenada em cache por conteúdo dinâmico. O método WriteReplacement() é usado para exibir o item de notícias aleatórias na exibição na Lista 2.

**Listagem 2 – Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

O método RenderNews é passado para o método WriteReplacement(). Observe que o método RenderNews não é chamado. Em vez disso, uma referência ao método é passada para WriteSubstitution() com a ajuda do operador AddressOf.

A exibição Índice está armazenada em cache. A exibição é devolvida pelo controlador na Listagem 3. Observe que a ação Index() &lt;é&gt; decorada com um atributo OutputCache que faz com que a exibição Index seja armazenada em cache por 60 segundos.

**Listagem 3 – Controladores\HomeController.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

Mesmo que a exibição Índice esteja armazenada em cache, diferentes notícias aleatórias são exibidas quando você solicita a página Índice. Ao solicitar a página Index, o tempo exibido pela página não muda por 60 segundos (ver Figura 1). O fato de que o tempo não muda prova que a página está armazenada em cache. No entanto, o conteúdo injetado pelo método WriteSubstitution() – o item de notícias aleatórias – muda a cada solicitação .

**Figura 1 – Injetar notícias dinâmicas em uma página em cache**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Usando a substituição pós-cache em métodos auxiliares

Uma maneira mais fácil de aproveitar a substituição pós-cache é encapsular a chamada para o método WriteReplacement() dentro de um método de ajuda personalizado. Esta abordagem é ilustrada pelo método auxiliar na Listagem 4.

**Listagem 4 – Helpers\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

A lista 4 contém um módulo Visual Basic que expõe dois métodos: RenderBanner() e RenderBannerInternal(). O método RenderBanner() representa o método de ajuda real. Este método estende a classe padrão ASP.NET Classe HtmlHelper mVC para que você possa chamar Html.RenderBanner() em uma exibição como qualquer outro método auxiliar.

O método RenderBanner() chama o método HttpResponse.WriteReplacement() que passa o método RenderBannerInternal() para o método WriteReplacement().

O método RenderBannerInternal() é um método privado. Este método não será exposto como um método auxiliar. O método RenderBannerInternal() retorna aleatoriamente uma imagem de anúncio de banner de uma lista de três imagens de anúncio de banner.

A exibição de índice modificado na Listagem 5 ilustra como você pode usar o método de ajuda RenderBanner(). Observe que &lt;uma diretiva&gt; adicional %@ Import % está incluída na parte superior da exibição para importar o namespace MvcApplication1.Helpers. Se você negligenciar a importação desse namespace, então o método RenderBanner não aparecerá como um método na propriedade Html.

**Listagem 5 – Views\Home\Index.aspx (com o método RenderBanner()**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

Quando você solicita a página renderizada pela exibição na Lista 5, um anúncio de banner diferente é exibido a cada solicitação (ver Figura 2). A página é armazenada em cache, mas o anúncio do banner é injetado dinamicamente pelo método de ajuda renderBanner().

**Figura 2 – A exibição do Índice exibindo um anúncio de banner aleatório**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>Resumo

Este tutorial explicou como você pode atualizar dinamicamente o conteúdo em uma página armazenada em cache. Você aprendeu a usar o método HttpResponse.WriteReplacement() para permitir que conteúdo dinâmico seja injetado em uma página em cache. Você também aprendeu como encapsular a chamada para o método WriteReplacement() dentro de um método de ajuda HTML.

Aproveite o cache sempre que possível – pode ter um impacto dramático no desempenho de suas aplicações web. Como explicado neste tutorial, você pode aproveitar o cache mesmo quando precisar exibir conteúdo dinâmico em suas páginas.

> [!div class="step-by-step"]
> [Próximo](improving-performance-with-output-caching-vb.md)
> [anterior](creating-a-controller-vb.md)
