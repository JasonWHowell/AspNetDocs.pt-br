---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: Executando várias animações ao mesmo tempo (C#) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. Ele permite executar o servidor...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598115"
---
# <a name="executing-several-animations-at-the-same-time-c"></a><span data-ttu-id="ca169-104">Executando várias animações ao mesmo tempo (C#)</span><span class="sxs-lookup"><span data-stu-id="ca169-104">Executing Several Animations at The Same Time (C#)</span></span>

<span data-ttu-id="ca169-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ca169-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ca169-106">[Baixar código](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) ou [baixar PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ca169-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span></span>

> <span data-ttu-id="ca169-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="ca169-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ca169-108">Ele permite executar várias animações de maneira paralela.</span><span class="sxs-lookup"><span data-stu-id="ca169-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="ca169-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ca169-109">Overview</span></span>

<span data-ttu-id="ca169-110">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="ca169-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ca169-111">Ele permite executar várias animações de maneira paralela.</span><span class="sxs-lookup"><span data-stu-id="ca169-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="ca169-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="ca169-112">Steps</span></span>

<span data-ttu-id="ca169-113">Em primeiro lugar, inclua o `ScriptManager` na página; em seguida, a biblioteca do ASP.NET AJAX é carregada, possibilitando o uso do kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="ca169-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

<span data-ttu-id="ca169-114">A animação será aplicada a um painel de texto semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="ca169-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

<span data-ttu-id="ca169-115">Na classe CSS associada para o painel, defina uma cor de plano de fundo boa e também defina uma largura fixa para o painel:</span><span class="sxs-lookup"><span data-stu-id="ca169-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

<span data-ttu-id="ca169-116">Em seguida, adicione o `AnimationExtender` à página, fornecendo um `ID`, o atributo `TargetControlID` e a `runat="server"`obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ca169-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

<span data-ttu-id="ca169-117">Dentro do nó `<Animations>`, use `<OnLoad>` para executar as animações depois que a página tiver sido totalmente carregada.</span><span class="sxs-lookup"><span data-stu-id="ca169-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="ca169-118">Em geral, `<OnLoad>` aceita apenas uma animação.</span><span class="sxs-lookup"><span data-stu-id="ca169-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="ca169-119">A estrutura de animação permite unir várias animações em uma usando o elemento `<Parallel>`.</span><span class="sxs-lookup"><span data-stu-id="ca169-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="ca169-120">Todas as animações dentro de `<Parallel>` são executadas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="ca169-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="ca169-121">Veja uma possível marcação para o controle de `AnimationExtender`, desbotando e redimensionando o painel ao mesmo tempo:</span><span class="sxs-lookup"><span data-stu-id="ca169-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

<span data-ttu-id="ca169-122">E de fato: quando você executa esse script, o painel é exibido e, em seguida, redimensiona (mais do que percorrida sua largura e metade da altura) e esmaece ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="ca169-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="ca169-123">[![o painel está esmaecido e redimensionando (incluindo seu conteúdo, graças ao mecanismo de renderização do navegador)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ca169-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span></span>

<span data-ttu-id="ca169-124">O painel está esmaecido e redimensionando (incluindo seu conteúdo, graças ao mecanismo de renderização do navegador) ([clique para exibir a imagem em tamanho normal](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ca169-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ca169-125">[Anterior](adding-animation-to-a-control-cs.md)
> [Próximo](executing-several-animations-after-each-other-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ca169-125">[Previous](adding-animation-to-a-control-cs.md)
[Next](executing-several-animations-after-each-other-cs.md)</span></span>
