---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Modos de exibição dinâmicos versus Exibições com rigidez de tipos | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702940"
---
# <a name="dynamic-v-strongly-typed-views"></a>Modos de exibição dinâmicos versus Exibições fortemente tipadas

por [Rick Anderson](https://twitter.com/RickAndMSFT)

Há três maneiras de passar informações de um controlador para uma exibição no ASP.NET MVC 3:

1. Como um objeto de modelo fortemente tipado.
2. Como um tipo dinâmico (usando @model dinâmico)
3. Usando ViewBag

Escrevi um aplicativo de blog mais simples MVC 3 para comparar e contrastar exibições dinâmicas e com rigidez de tipos. O controlador começa com uma lista simples de Blogs:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

Clique com o botão direito do mouse no método IndexNotStonglyTyped () e adicione uma exibição do Razor.

[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

Verifique se a caixa de **exibição criar um tipo forte** não está marcada. A exibição resultante não contém muito:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

Como estamos usando uma exibição dinâmica e não com rigidez de tipos, o IntelliSense não nos ajuda. O código completo é mostrado abaixo:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

Agora, adicionaremos uma exibição com rigidez de tipos. Adicione o seguinte código ao controlador:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

Observe que é exatamente a mesma exibição de retorno (topBlogs); Chame como a exibição não fortemente tipada. Clique com o botão direito do mouse dentro de *StonglyTypedIndex ()* e selecione **Adicionar exibição**. Desta vez, selecione a classe de modelo de **blog** e selecione **lista** como o modelo Scaffold.

[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

Dentro do novo modelo de exibição, obtemos suporte ao IntelliSense.

[![7002. IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)
