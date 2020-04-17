---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Criando rotas personalizadas (C#) | Microsoft Docs
author: rick-anderson
description: Aprenda a adicionar rotas personalizadas a um aplicativo MVC ASP.NET. Neste tutorial, você aprende como modificar a tabela de rotas padrão no arquivo Global.asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542749"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="091a4-104">Criação de rotas personalizadas (C#)</span><span class="sxs-lookup"><span data-stu-id="091a4-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="091a4-105">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="091a4-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="091a4-106">Aprenda a adicionar rotas personalizadas a um aplicativo MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="091a4-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="091a4-107">Neste tutorial, você aprende como modificar a tabela de rotas padrão no arquivo Global.asax.</span><span class="sxs-lookup"><span data-stu-id="091a4-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="091a4-108">Neste tutorial, você aprende como adicionar uma rota personalizada a um aplicativo mvc ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="091a4-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="091a4-109">Você aprende como modificar a tabela de rota padrão no arquivo Global.asax com uma rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="091a4-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="091a4-110">Para muitos aplicativos simples de MVC ASP.NET, a tabela de rotas padrão funcionará muito bem.</span><span class="sxs-lookup"><span data-stu-id="091a4-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="091a4-111">No entanto, você pode descobrir que você tem necessidades de roteamento especializadas.</span><span class="sxs-lookup"><span data-stu-id="091a4-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="091a4-112">Nesse caso, você pode criar uma rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="091a4-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="091a4-113">Imagine, por exemplo, que você está construindo um aplicativo de blog.</span><span class="sxs-lookup"><span data-stu-id="091a4-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="091a4-114">Você pode querer lidar com pedidos de entrada que se parecem com isso:</span><span class="sxs-lookup"><span data-stu-id="091a4-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="091a4-115">/Arquivo/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="091a4-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="091a4-116">Quando um usuário insere essa solicitação, você deseja retornar a entrada do blog que corresponde à data de 25/12/2009.</span><span class="sxs-lookup"><span data-stu-id="091a4-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="091a4-117">Para lidar com esse tipo de solicitação, você precisa criar uma rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="091a4-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="091a4-118">O arquivo Global.asax na Listagem 1 contém uma nova rota personalizada, chamada Blog, que lida com solicitações que se parecem com /Archive/data*de entrada*.</span><span class="sxs-lookup"><span data-stu-id="091a4-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="091a4-119">**Listagem 1 - Global.asax (com rota personalizada)**</span><span class="sxs-lookup"><span data-stu-id="091a4-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="091a4-120">A ordem das rotas que você adiciona à tabela de rotas é importante.</span><span class="sxs-lookup"><span data-stu-id="091a4-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="091a4-121">Nossa nova rota personalizada do Blog é adicionada antes da rota Padrão existente.</span><span class="sxs-lookup"><span data-stu-id="091a4-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="091a4-122">Se você inverteu a ordem, então a rota Padrão sempre será chamada em vez da rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="091a4-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="091a4-123">A rota do Blog personalizado corresponde a qualquer solicitação que comece com /Archive/.</span><span class="sxs-lookup"><span data-stu-id="091a4-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="091a4-124">Então, corresponde a todas as seguintes URLs:</span><span class="sxs-lookup"><span data-stu-id="091a4-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="091a4-125">/Arquivo/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="091a4-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="091a4-126">/Arquivo/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="091a4-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="091a4-127">/Arquivo/maçã</span><span class="sxs-lookup"><span data-stu-id="091a4-127">/Archive/apple</span></span>

<span data-ttu-id="091a4-128">A rota personalizada mapeia a solicitação recebida para um controlador chamado Archive e invoca a ação Entrada().</span><span class="sxs-lookup"><span data-stu-id="091a4-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="091a4-129">Quando o método Entry() é chamado, a data de entrada é passada como um parâmetro chamado entryDate.</span><span class="sxs-lookup"><span data-stu-id="091a4-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="091a4-130">Você pode usar a rota personalizada do Blog com o controlador na Lista 2.</span><span class="sxs-lookup"><span data-stu-id="091a4-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="091a4-131">**Listagem 2 - ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="091a4-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="091a4-132">Observe que o método Entry() na Listagem 2 aceita um parâmetro do tipo DateTime.</span><span class="sxs-lookup"><span data-stu-id="091a4-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="091a4-133">A estrutura MVC é inteligente o suficiente para converter a data de entrada da URL em um valor DateTime automaticamente.</span><span class="sxs-lookup"><span data-stu-id="091a4-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="091a4-134">Se o parâmetro de data de entrada da URL não puder ser convertido em data-hora, um erro será levantado (consulte Figura 1).</span><span class="sxs-lookup"><span data-stu-id="091a4-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="091a4-135">**Figura 1 - Erro ao converter parâmetro**</span><span class="sxs-lookup"><span data-stu-id="091a4-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="091a4-136">[![A caixa de diálogo Novo Projeto](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="091a4-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="091a4-137">**Figura 01**: Erro ao converter parâmetro[(Clique para exibir imagem em tamanho real)](creating-custom-routes-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="091a4-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="091a4-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="091a4-138">Summary</span></span>

<span data-ttu-id="091a4-139">O objetivo deste tutorial foi demonstrar como você pode criar uma rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="091a4-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="091a4-140">Você aprendeu como adicionar uma rota personalizada à tabela de rotas no arquivo Global.asax que representa entradas de blog.</span><span class="sxs-lookup"><span data-stu-id="091a4-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="091a4-141">Discutimos como mapear solicitações de entradas de blog para um controlador chamado ArchiveController e uma ação controladora chamada Entry().</span><span class="sxs-lookup"><span data-stu-id="091a4-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="091a4-142">[Próximo](aspnet-mvc-controllers-overview-cs.md)
> [anterior](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="091a4-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
