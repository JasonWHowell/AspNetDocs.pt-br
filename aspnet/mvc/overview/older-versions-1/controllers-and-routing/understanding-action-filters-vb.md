---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: Entendendo filtros de ação (VB) | Microsoft Docs
author: rick-anderson
description: O objetivo deste tutorial é explicar filtros de ação. Um filtro de ação é um atributo que você pode aplicar a uma ação do controlador -- ou a um controlador inteiro...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 70ab564bc1217f67874090d2ae6899d9bcd743a1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542099"
---
# <a name="understanding-action-filters-vb"></a>Noções básicas sobre filtros de ação (VB)

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> O objetivo deste tutorial é explicar filtros de ação. Um filtro de ação é um atributo que você pode aplicar a uma ação do controlador - ou a um controlador inteiro - que modifica a maneira como a ação é executada.

## <a name="understanding-action-filters"></a>Entendendo filtros de ação

O objetivo deste tutorial é explicar filtros de ação. Um filtro de ação é um atributo que você pode aplicar a uma ação do controlador - ou a um controlador inteiro - que modifica a maneira como a ação é executada. A ASP.NET estrutura MVC inclui vários filtros de ação:

- OutputCache – Este filtro de ação armazena a saída de uma ação do controlador por um período de tempo especificado.
- HandleError – Este filtro de ação lida com erros levantados quando uma ação do controlador é executada.
- Autorizar – Este filtro de ação permite restringir o acesso a um determinado usuário ou função.

Você também pode criar seus próprios filtros de ação personalizados. Por exemplo, você pode querer criar um filtro de ação personalizado para implementar um sistema de autenticação personalizado. Ou, você pode querer criar um filtro de ação que modifique os dados de exibição retornados por uma ação controladora.

Neste tutorial, você aprende a construir um filtro de ação do zero. Criamos um filtro de ação Log que registra diferentes etapas do processamento de uma ação na janela Saída do Visual Studio.

### <a name="using-an-action-filter"></a>Usando um filtro de ação

Um filtro de ação é um atributo. Você pode aplicar a maioria dos filtros de ação a uma ação individual do controlador ou a um controlador inteiro.

Por exemplo, o controlador de dados na `Index()` Listagem 1 expõe uma ação nomeada que retorna o tempo atual. Esta ação é decorada `OutputCache` com o filtro de ação. Este filtro faz com que o valor devolvido pela ação seja armazenado em cache por 10 segundos.

**Listagem 1 –`Controllers\DataController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

Se você invocar `Index()` repetidamente a ação inserindo a URL /Data/Index na barra de endereços do seu navegador e apertando o botão Atualizar várias vezes, então você verá o mesmo tempo por 10 segundos. A saída `Index()` da ação é armazenada em cache por 10 segundos (ver Figura 1).

[![Tempo armazenado em cache](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)

**Figura 01**: Tempo armazenado em cache[(Clique para ver a imagem em tamanho real](understanding-action-filters-vb/_static/image3.png))

Na Lista 1, um filtro `OutputCache` de ação único – `Index()` o filtro de ação – é aplicado ao método. Se você precisar, você pode aplicar vários filtros de ação à mesma ação. Por exemplo, você pode querer `OutputCache` `HandleError` aplicar os filtros e os filtros de ação à mesma ação.

Na Lista 1, o `OutputCache` filtro de `Index()` ação é aplicado à ação. Você também pode aplicar `DataController` esse atributo à própria classe. Nesse caso, o resultado devolvido por qualquer ação exposta pelo controlador seria armazenado em cache por 10 segundos.

### <a name="the-different-types-of-filters"></a>Os diferentes tipos de filtros

A estrutura mvc ASP.NET suporta quatro tipos diferentes de filtros:

1. Filtros de autorização `IAuthorizationFilter` – Implementa o atributo.
2. Filtros de ação `IActionFilter` – Implementa o atributo.
3. Filtros de resultado `IResultFilter` – Implementa o atributo.
4. Filtros de exceção `IExceptionFilter` – Implementa o atributo.

Os filtros são executados na ordem listada acima. Por exemplo, os filtros de autorização são sempre executados antes que filtros de ação e filtros de exceção sejam sempre executados após qualquer outro tipo de filtro.

Os filtros de autorização são usados para implementar autenticação e autorização para ações do controlador. Por exemplo, o filtro Autorizar é um exemplo de filtro Autorização.

Os filtros de ação contêm lógica sacada antes e depois de ser executada uma ação do controlador. Você pode usar um filtro de ação, por exemplo, para modificar os dados de exibição que uma ação do controlador retorna.

Os filtros de resultado contêm a lógica executada antes e depois de um resultado de exibição ser executado. Por exemplo, você pode querer modificar um resultado de exibição antes que a exibição seja renderizada no navegador.

Filtros de exceção são o último tipo de filtro a ser executado. Você pode usar um filtro de exceção para lidar com erros levantados pelas ações do controlador ou pelos resultados de ação do controlador. Você também pode usar filtros de exceção para registrar erros.

Cada tipo diferente de filtro é executado em uma ordem específica. Se você quiser controlar a ordem na qual filtros do mesmo tipo são executados, então você pode definir a propriedade Order de um filtro.

A classe base para todos `System.Web.Mvc.FilterAttribute` os filtros de ação é a classe. Se você quiser implementar um tipo específico de filtro, então você precisa criar uma classe que herda da classe filtro base e implementa uma ou mais das interfaces IAuthorizationFilter, IActionFilter, IResultFilter ou ExceptionFilter.

### <a name="the-base-actionfilterattribute-class"></a>A classe de atributo de filtro de ação base

Para facilitar a implementação de um filtro de ação personalizado, a `ActionFilterAttribute` estrutura ASP.NET MVC inclui uma classe base. Esta classe implementa `IActionFilter` `IResultFilter` tanto as interfaces `Filter` quanto as herdadas da classe.

A terminologia aqui não é totalmente consistente. Tecnicamente, uma classe que herda da classe ActionFilterAttribute é um filtro de ação e um filtro de resultado. No entanto, no sentido solto, a palavra filtro de ação é usada para se referir a qualquer tipo de filtro na estrutura mvc ASP.NET.

A classe base ActionFilterAttribute tem os seguintes métodos que você pode substituir:

- OnActionExecuting – Este método é chamado antes de uma ação do controlador ser executada.
- OnActionExecuted – Este método é chamado após a execução de uma ação do controlador.
- OnResultExecuting – Este método é chamado antes de um resultado de ação do controlador ser executado.
- OnResultExecuted – Este método é chamado após a execução de um resultado de ação do controlador.

Na próxima seção, veremos como você pode implementar cada um desses métodos diferentes.

### <a name="creating-a-log-action-filter"></a>Criando um filtro de ação de log

Para ilustrar como você pode construir um filtro de ação personalizado, criaremos um filtro de ação personalizado que registra as etapas de processamento de uma ação controladora na janela Saída do Visual Studio. Nosso `LogActionFilter` está contido na Lista 2.

**Listagem 2 –`ActionFilters\LogActionFilter.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

Na `OnActionExecuting()`Lista 2, `OnActionExecuted()` `OnResultExecuting()`todos `OnResultExecuted()` os métodos `Log()` e métodos chamam o método. O nome do método e os dados `Log()` de rota atuais são passados para o método. O `Log()` método grava uma mensagem na janela Saída do Estúdio Visual (ver Figura 2).

[![Escrevendo para a janela de saída do Visual Studio](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)

**Figura 02**: Escrever na janela Saída do Estúdio Visual[(Clique para ver a imagem em tamanho real)](understanding-action-filters-vb/_static/image6.png)

O controlador Home na Lista 3 ilustra como você pode aplicar o filtro de ação Log a toda uma classe de controlador. Sempre que qualquer uma das ações expostas pelo controlador `Index()` Home `About()` for invocada – seja o método ou o método – as etapas de processamento da ação são registradas na janela Saída do Visual Studio.

**Lista 3 –`Controllers\HomeController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a>Resumo

Neste tutorial, você foi introduzido a ASP.NET filtros de ação MVC. Você aprendeu sobre os quatro tipos diferentes de filtros: filtros de autorização, filtros de ação, filtros de resultado e filtros de exceção. Você também aprendeu `ActionFilterAttribute` sobre a classe base.

Finalmente, você aprendeu como implementar um simples filtro de ação. Criamos um filtro de ação Log que registra as etapas de processamento de uma ação do controlador na janela Saída do Visual Studio.

> [!div class="step-by-step"]
> [Próximo](asp-net-mvc-routing-overview-vb.md)
> [anterior](improving-performance-with-output-caching-vb.md)
