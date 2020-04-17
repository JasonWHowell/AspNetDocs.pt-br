---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Criando uma Ação (C#) | Microsoft Docs
author: rick-anderson
description: Aprenda a adicionar uma nova ação a um controlador MVC ASP.NET. Conheça os requisitos para que um método seja uma ação.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c1edfbab41afa58c7cb2c0d306995e9fe491c90
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542268"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="1e21e-104">Criar uma ação (C#)</span><span class="sxs-lookup"><span data-stu-id="1e21e-104">Creating an Action (C#)</span></span>

<span data-ttu-id="1e21e-105">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1e21e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1e21e-106">Aprenda a adicionar uma nova ação a um controlador MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1e21e-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="1e21e-107">Conheça os requisitos para que um método seja uma ação.</span><span class="sxs-lookup"><span data-stu-id="1e21e-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="1e21e-108">O objetivo deste tutorial é explicar como você pode criar uma nova ação de controlador.</span><span class="sxs-lookup"><span data-stu-id="1e21e-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="1e21e-109">Você aprende sobre os requisitos de um método de ação.</span><span class="sxs-lookup"><span data-stu-id="1e21e-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="1e21e-110">Você também aprende como evitar que um método seja exposto como uma ação.</span><span class="sxs-lookup"><span data-stu-id="1e21e-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="1e21e-111">Adicionando uma ação a um controlador</span><span class="sxs-lookup"><span data-stu-id="1e21e-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="1e21e-112">Você adiciona uma nova ação a um controlador adicionando um novo método ao controlador.</span><span class="sxs-lookup"><span data-stu-id="1e21e-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="1e21e-113">Por exemplo, o controlador na Listagem 1 contém uma ação chamada Index() e uma ação chamada SayHello().</span><span class="sxs-lookup"><span data-stu-id="1e21e-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="1e21e-114">Ambos os métodos são expostos como ações.</span><span class="sxs-lookup"><span data-stu-id="1e21e-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="1e21e-115">**Listagem 1 - Controladores\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="1e21e-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="1e21e-116">Para ser exposto ao universo como uma ação, um método deve atender a certos requisitos:</span><span class="sxs-lookup"><span data-stu-id="1e21e-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="1e21e-117">O método deve ser público.</span><span class="sxs-lookup"><span data-stu-id="1e21e-117">The method must be public.</span></span>
- <span data-ttu-id="1e21e-118">O método não pode ser um método estático.</span><span class="sxs-lookup"><span data-stu-id="1e21e-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="1e21e-119">O método não pode ser um método de extensão.</span><span class="sxs-lookup"><span data-stu-id="1e21e-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="1e21e-120">O método não pode ser um construtor, getter ou setter.</span><span class="sxs-lookup"><span data-stu-id="1e21e-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="1e21e-121">O método não pode ter tipos genéricos abertos.</span><span class="sxs-lookup"><span data-stu-id="1e21e-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="1e21e-122">O método não é um método da classe base do controlador.</span><span class="sxs-lookup"><span data-stu-id="1e21e-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="1e21e-123">O método não pode conter parâmetros **de ref** ou **out.**</span><span class="sxs-lookup"><span data-stu-id="1e21e-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="1e21e-124">Observe que não há restrições sobre o tipo de retorno de uma ação do controlador.</span><span class="sxs-lookup"><span data-stu-id="1e21e-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="1e21e-125">Uma ação do controlador pode retornar uma seqüência, uma Hora de Data, uma instância da classe Random ou anular.</span><span class="sxs-lookup"><span data-stu-id="1e21e-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="1e21e-126">A ASP.NET estrutura MVC converterá qualquer tipo de retorno que não seja um resultado de ação em uma seqüência e renderizará a seqüência para o navegador.</span><span class="sxs-lookup"><span data-stu-id="1e21e-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="1e21e-127">Quando você adiciona qualquer método que não viole esses requisitos a um controlador, o método é exposto como uma ação do controlador.</span><span class="sxs-lookup"><span data-stu-id="1e21e-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="1e21e-128">Tenha cuidado aqui.</span><span class="sxs-lookup"><span data-stu-id="1e21e-128">Be careful here.</span></span> <span data-ttu-id="1e21e-129">Uma ação do controlador pode ser invocada por qualquer pessoa conectada à Internet.</span><span class="sxs-lookup"><span data-stu-id="1e21e-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="1e21e-130">Não crie, por exemplo, uma ação de controlador DeleteMySite().</span><span class="sxs-lookup"><span data-stu-id="1e21e-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="1e21e-131">Impedindo que um método público seja invocado</span><span class="sxs-lookup"><span data-stu-id="1e21e-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="1e21e-132">Se você precisa criar um método público em uma classe controladora e não quiser expor o método como uma ação do controlador, então você pode impedir que o método seja invocado usando o atributo [NonAction].</span><span class="sxs-lookup"><span data-stu-id="1e21e-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="1e21e-133">Por exemplo, o controlador na Listagem 2 contém um método público chamado CompanySecrets() que é decorado com o atributo [NonAction].</span><span class="sxs-lookup"><span data-stu-id="1e21e-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="1e21e-134">**Listagem 2 - Controladores\WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="1e21e-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="1e21e-135">Se você tentar invocar a ação do controlador CompanySecrets() digitando /Work/CompanySecrets na barra de endereços do seu navegador, então você receberá a mensagem de erro na Figura 1.</span><span class="sxs-lookup"><span data-stu-id="1e21e-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="1e21e-136">[![Invocando um método de não ação](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1e21e-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="1e21e-137">**Figura 01**: Invocar um método de não ação[(Clique para exibir imagem em tamanho real)](creating-an-action-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="1e21e-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1e21e-138">[Próximo](creating-a-controller-cs.md)
> [anterior](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1e21e-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
