---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: Recolhendo e expandindo um painel do JavaScript (VB) | Microsoft Docs
author: wenz
description: O controle CollapsiblePanel no kit de ferramentas de controle do ASP.NET AJAX estende um painel e fornece a capacidade de recolher seu conteúdo e expandi-lo...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535843"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a><span data-ttu-id="fecef-103">Recolher e expandir um painel de JavaScript (VB)</span><span class="sxs-lookup"><span data-stu-id="fecef-103">Collapsing and Expanding a Panel from JavaScript (VB)</span></span>

<span data-ttu-id="fecef-104">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fecef-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fecef-105">[Baixar código](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) ou [baixar PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fecef-105">[Download Code](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span></span>

> <span data-ttu-id="fecef-106">O controle CollapsiblePanel no kit de ferramentas de controle do ASP.NET AJAX estende um painel e fornece a capacidade de recolher seu conteúdo e expandi-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="fecef-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="fecef-107">Essas duas ações também podem ser disparadas a partir do código JavaScript personalizado.</span><span class="sxs-lookup"><span data-stu-id="fecef-107">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="fecef-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fecef-108">Overview</span></span>

<span data-ttu-id="fecef-109">O controle CollapsiblePanel no kit de ferramentas de controle do ASP.NET AJAX estende um painel e fornece a capacidade de recolher seu conteúdo e expandi-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="fecef-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="fecef-110">Essas duas ações também podem ser disparadas a partir do código JavaScript personalizado.</span><span class="sxs-lookup"><span data-stu-id="fecef-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="fecef-111">Etapas</span><span class="sxs-lookup"><span data-stu-id="fecef-111">Steps</span></span>

<span data-ttu-id="fecef-112">Em primeiro lugar, crie uma nova página ASP.NET e inclua o `ScriptManager` dentro do elemento um `<form>`.</span><span class="sxs-lookup"><span data-stu-id="fecef-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="fecef-113">Isso carrega a biblioteca do ASP.NET AJAX que é exigida pelo kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="fecef-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="fecef-114">Em seguida, crie um painel com texto para que o efeito recolher/expandir possa ser visto:</span><span class="sxs-lookup"><span data-stu-id="fecef-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="fecef-115">Como você pode ver, o painel faz referência a uma classe CSS que é mostrada aqui (e basicamente define uma cor de plano de fundo e a largura do painel):</span><span class="sxs-lookup"><span data-stu-id="fecef-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

<span data-ttu-id="fecef-116">O controle `CollapsiblePanelExtender` requer o atributo `TargetControlID` para que o kit de ferramentas saiba qual painel deve ser recolhido ou expandido após a solicitação:</span><span class="sxs-lookup"><span data-stu-id="fecef-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

<span data-ttu-id="fecef-117">Infelizmente, o extensor atualmente não expõe uma API específica para recolher ou expandir o painel, mas alguns métodos não documentados farão isso.</span><span class="sxs-lookup"><span data-stu-id="fecef-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="fecef-118">Em primeiro lugar, adicione três botões HTML à página, o que irá disparar o JavaScript do lado do cliente para recolher ou expandir o conteúdo do painel:</span><span class="sxs-lookup"><span data-stu-id="fecef-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="fecef-119">No código JavaScript do lado do cliente (iniciado com `<script type="text/javascript">`), o método `$find()` precisa ser usado para acessar o `CollapsiblePanelExtender`.</span><span class="sxs-lookup"><span data-stu-id="fecef-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="fecef-120">`$find("cpe")` retornará uma referência a ele.</span><span class="sxs-lookup"><span data-stu-id="fecef-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="fecef-121">A partir daí, métodos específicos resolverão a tarefa em questão.</span><span class="sxs-lookup"><span data-stu-id="fecef-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="fecef-122">O método para abrir (expandir) o painel é chamado de `_doOpen()`; o código a seguir implementa a função `doOpen()` chamada quando o primeiro botão é clicado:</span><span class="sxs-lookup"><span data-stu-id="fecef-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

<span data-ttu-id="fecef-123">Para fechar ou recolher o painel, o método `_doClose()` precisa ser executado.</span><span class="sxs-lookup"><span data-stu-id="fecef-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="fecef-124">Assim, quando o usuário clica no segundo botão, o seguinte código JavaScript é chamado:</span><span class="sxs-lookup"><span data-stu-id="fecef-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

<span data-ttu-id="fecef-125">O terceiro botão alterna o estado do painel: de recolhido para expandido, e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="fecef-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="fecef-126">O `CollapsiblePanelExtender` expõe o método `toggle()` que faz exatamente isso: reverte o estado do painel.</span><span class="sxs-lookup"><span data-stu-id="fecef-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="fecef-127">No entanto, há também outra abordagem (que é usada internamente pelo método `toggle()`): o método `get_Collapsed()` da `CollapsiblePanelExtender()` nos informa se o painel está recolhido ou não.</span><span class="sxs-lookup"><span data-stu-id="fecef-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="fecef-128">Dependendo do valor de retorno dessa função, o painel será expandido (método`_doOpen()`) ou o método recolhido (`_doClose()`):</span><span class="sxs-lookup"><span data-stu-id="fecef-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

<span data-ttu-id="fecef-129">[![o terceiro botão altera o estado do painel: de recolhido para expandido e para trás](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fecef-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="fecef-130">O terceiro botão altera o estado do painel: de recolhido para expandido e de volta ([clique para exibir a imagem em tamanho normal](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fecef-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fecef-131">Anterior</span><span class="sxs-lookup"><span data-stu-id="fecef-131">Previous</span></span>](collapsing-and-expanding-a-panel-from-javascript-cs.md)
