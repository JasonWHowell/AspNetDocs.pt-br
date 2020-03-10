---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Exibir detalhes do item | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557319"
---
# <a name="display-item-details"></a><span data-ttu-id="b7f52-102">Exibir detalhes do item</span><span class="sxs-lookup"><span data-stu-id="b7f52-102">Display Item Details</span></span>

<span data-ttu-id="b7f52-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b7f52-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b7f52-104">Baixar projeto concluído</span><span class="sxs-lookup"><span data-stu-id="b7f52-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="b7f52-105">Nesta seção, você adicionará a capacidade de exibir detalhes de cada livro.</span><span class="sxs-lookup"><span data-stu-id="b7f52-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="b7f52-106">No app. js, adicione ao seguinte código ao modelo de exibição:</span><span class="sxs-lookup"><span data-stu-id="b7f52-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="b7f52-107">Em views/home/index. cshtml, adicione um elemento de vinculação de dados ao link detalhes:</span><span class="sxs-lookup"><span data-stu-id="b7f52-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="b7f52-108">Isso associa o manipulador de cliques para o &lt;um elemento&gt; à função `getBookDetail` no modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="b7f52-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="b7f52-109">No mesmo arquivo, substitua a seguinte marcação:</span><span class="sxs-lookup"><span data-stu-id="b7f52-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="b7f52-110">por este:</span><span class="sxs-lookup"><span data-stu-id="b7f52-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="b7f52-111">Essa marcação cria uma tabela que está associada a dados para as propriedades do `detail` observável no modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="b7f52-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="b7f52-112">A sintaxe de &quot; "&lt;!--ko--&gt;permite incluir uma associação de Knockout fora de um elemento DOM.</span><span class="sxs-lookup"><span data-stu-id="b7f52-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="b7f52-113">Nesse caso, a associação de `if` faz com que esta seção de marcação seja exibida somente quando `details` não é nulo.</span><span class="sxs-lookup"><span data-stu-id="b7f52-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="b7f52-114">Agora, se você executar o aplicativo e clicar em uma das &quot;detalhes&quot; links, o aplicativo exibirá os detalhes do livro.</span><span class="sxs-lookup"><span data-stu-id="b7f52-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="b7f52-115">[Anterior](part-7.md)
> [Próximo](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="b7f52-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
