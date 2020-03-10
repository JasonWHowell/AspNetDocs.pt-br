---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: Criando uma restrição de rotaC#() | Microsoft Docs
author: StephenWalther
description: Neste tutorial, Stephen Walther demonstra como você pode controlar como o navegador solicita as rotas correspondentes criando restrições de rota com expressões regulares.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582008"
---
# <a name="creating-a-route-constraint-c"></a><span data-ttu-id="76a55-103">Criação de uma restrição de rota (C#)</span><span class="sxs-lookup"><span data-stu-id="76a55-103">Creating a Route Constraint (C#)</span></span>

<span data-ttu-id="76a55-104">por [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="76a55-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="76a55-105">Neste tutorial, Stephen Walther demonstra como você pode controlar como o navegador solicita as rotas correspondentes criando restrições de rota com expressões regulares.</span><span class="sxs-lookup"><span data-stu-id="76a55-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="76a55-106">Você usa restrições de rota para restringir as solicitações do navegador que correspondem a uma rota específica.</span><span class="sxs-lookup"><span data-stu-id="76a55-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="76a55-107">Você pode usar uma expressão regular para especificar uma restrição de rota.</span><span class="sxs-lookup"><span data-stu-id="76a55-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="76a55-108">Por exemplo, imagine que você definiu a rota na Listagem 1 em seu arquivo global. asax.</span><span class="sxs-lookup"><span data-stu-id="76a55-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="76a55-109">**Listagem 1-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="76a55-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="76a55-110">A listagem 1 contém uma rota chamada Product.</span><span class="sxs-lookup"><span data-stu-id="76a55-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="76a55-111">Você pode usar a rota do produto para mapear solicitações do navegador para o ProductController contido na Listagem 2.</span><span class="sxs-lookup"><span data-stu-id="76a55-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="76a55-112">**Listagem 2-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="76a55-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="76a55-113">Observe que a ação Details () exposta pelo controlador do produto aceita um único parâmetro chamado productId.</span><span class="sxs-lookup"><span data-stu-id="76a55-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="76a55-114">Esse parâmetro é um parâmetro inteiro.</span><span class="sxs-lookup"><span data-stu-id="76a55-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="76a55-115">A rota definida na Listagem 1 corresponderá a qualquer uma das seguintes URLs:</span><span class="sxs-lookup"><span data-stu-id="76a55-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="76a55-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="76a55-116">/Product/23</span></span>
- <span data-ttu-id="76a55-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="76a55-117">/Product/7</span></span>

<span data-ttu-id="76a55-118">Infelizmente, a rota também corresponderá às seguintes URLs:</span><span class="sxs-lookup"><span data-stu-id="76a55-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="76a55-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="76a55-119">/Product/blah</span></span>
- <span data-ttu-id="76a55-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="76a55-120">/Product/apple</span></span>

<span data-ttu-id="76a55-121">Como a ação Details () espera um parâmetro inteiro, fazer uma solicitação que contém algo diferente de um valor inteiro causará um erro.</span><span class="sxs-lookup"><span data-stu-id="76a55-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="76a55-122">Por exemplo, se você digitar a URL/Product/Apple em seu navegador, receberá a página de erro na Figura 1.</span><span class="sxs-lookup"><span data-stu-id="76a55-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="76a55-123">[![caixa de diálogo novo projeto](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="76a55-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="76a55-124">**Figura 01**: ver um detalhamento de página ([clique para exibir a imagem em tamanho normal](creating-a-route-constraint-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="76a55-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>

<span data-ttu-id="76a55-125">O que você realmente deseja fazer é corresponder apenas a URLs que contenham um número inteiro apropriado de productId.</span><span class="sxs-lookup"><span data-stu-id="76a55-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="76a55-126">Você pode usar uma restrição ao definir uma rota para restringir as URLs que correspondem à rota.</span><span class="sxs-lookup"><span data-stu-id="76a55-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="76a55-127">A rota de produto modificada na Listagem 3 contém uma restrição de expressão regular que só corresponde a inteiros.</span><span class="sxs-lookup"><span data-stu-id="76a55-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="76a55-128">**Listagem 3-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="76a55-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="76a55-129">A expressão regular \D + corresponde a um ou mais inteiros.</span><span class="sxs-lookup"><span data-stu-id="76a55-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="76a55-130">Essa restrição faz com que a rota do produto corresponda às seguintes URLs:</span><span class="sxs-lookup"><span data-stu-id="76a55-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="76a55-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="76a55-131">/Product/3</span></span>
- <span data-ttu-id="76a55-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="76a55-132">/Product/8999</span></span>

<span data-ttu-id="76a55-133">Mas não as seguintes URLs:</span><span class="sxs-lookup"><span data-stu-id="76a55-133">But not the following URLs:</span></span>

- <span data-ttu-id="76a55-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="76a55-134">/Product/apple</span></span>
- <span data-ttu-id="76a55-135">/Product</span><span class="sxs-lookup"><span data-stu-id="76a55-135">/Product</span></span>

- <span data-ttu-id="76a55-136">Essas solicitações de navegador serão tratadas por outra rota ou, se não houver rotas correspondentes, um erro *o recurso não pôde ser encontrado* será retornado.</span><span class="sxs-lookup"><span data-stu-id="76a55-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="76a55-137">[Anterior](creating-custom-routes-cs.md)
> [Próximo](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="76a55-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
