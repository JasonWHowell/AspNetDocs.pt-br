---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: Adicionando animação a um controle (C#) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. Este tutorial mostra como...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: dd63157fe616c5f6874b7cca11f4ede15018df04
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614446"
---
# <a name="adding-animation-to-a-control-c"></a><span data-ttu-id="cf32b-104">Adição de animação a um controle (C#)</span><span class="sxs-lookup"><span data-stu-id="cf32b-104">Adding Animation to a Control (C#)</span></span>

<span data-ttu-id="cf32b-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cf32b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cf32b-106">[Baixar código](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) ou [baixar PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="cf32b-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="cf32b-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="cf32b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cf32b-108">Este tutorial mostra como configurar essa animação.</span><span class="sxs-lookup"><span data-stu-id="cf32b-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="cf32b-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cf32b-109">Overview</span></span>

<span data-ttu-id="cf32b-110">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="cf32b-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cf32b-111">Este tutorial mostra como configurar essa animação.</span><span class="sxs-lookup"><span data-stu-id="cf32b-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="cf32b-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="cf32b-112">Steps</span></span>

<span data-ttu-id="cf32b-113">A primeira etapa é normalmente para incluir o `ScriptManager` na página para que a biblioteca ASP.NET AJAX seja carregada e o kit de ferramentas de controle possa ser usado:</span><span class="sxs-lookup"><span data-stu-id="cf32b-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="cf32b-114">A animação neste cenário será aplicada a um painel de texto semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="cf32b-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="cf32b-115">A classe CSS associada para o painel define uma cor de plano de fundo e uma largura:</span><span class="sxs-lookup"><span data-stu-id="cf32b-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="cf32b-116">Em seguida, precisamos do `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="cf32b-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="cf32b-117">Depois de fornecer um `ID` e o `runat="server"`usual, o atributo `TargetControlID` deve ser definido como o controle para animar em nosso caso, o painel:</span><span class="sxs-lookup"><span data-stu-id="cf32b-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="cf32b-118">A animação inteira é aplicada declarativamente, usando uma sintaxe XML, infelizmente, atualmente, não tem suporte total do IntelliSense do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf32b-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="cf32b-119">O nó raiz está `<Animations>;` dentro desse nó, vários eventos são permitidos, que determinam quando as animações levam (m) lugar:</span><span class="sxs-lookup"><span data-stu-id="cf32b-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="cf32b-120">`OnClick` (clique do mouse)</span><span class="sxs-lookup"><span data-stu-id="cf32b-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="cf32b-121">`OnHoverOut` (quando o mouse sai de um controle)</span><span class="sxs-lookup"><span data-stu-id="cf32b-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="cf32b-122">`OnHoverOver` (quando o mouse passa sobre um controle, parando a animação de `OnHoverOut`)</span><span class="sxs-lookup"><span data-stu-id="cf32b-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="cf32b-123">`OnLoad` (quando a página tiver sido carregada)</span><span class="sxs-lookup"><span data-stu-id="cf32b-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="cf32b-124">`OnMouseOut` (quando o mouse sai de um controle)</span><span class="sxs-lookup"><span data-stu-id="cf32b-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="cf32b-125">`OnMouseOver` (quando o mouse passa sobre um controle, não parando a animação de `OnMouseOut`)</span><span class="sxs-lookup"><span data-stu-id="cf32b-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="cf32b-126">A estrutura vem com um conjunto de animações, cada uma representada por seu próprio elemento XML.</span><span class="sxs-lookup"><span data-stu-id="cf32b-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="cf32b-127">Aqui está uma seleção:</span><span class="sxs-lookup"><span data-stu-id="cf32b-127">Here is a selection:</span></span>

- <span data-ttu-id="cf32b-128">`<Color>` (alterando uma cor)</span><span class="sxs-lookup"><span data-stu-id="cf32b-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="cf32b-129">`<FadeIn>` (esmaecimento)</span><span class="sxs-lookup"><span data-stu-id="cf32b-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="cf32b-130">`<FadeOut>` (esmaecimento)</span><span class="sxs-lookup"><span data-stu-id="cf32b-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="cf32b-131">`<Property>` (alterando a propriedade de um controle)</span><span class="sxs-lookup"><span data-stu-id="cf32b-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="cf32b-132">`<Pulse>` (Pulsating)</span><span class="sxs-lookup"><span data-stu-id="cf32b-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="cf32b-133">`<Resize>` (alterando o tamanho)</span><span class="sxs-lookup"><span data-stu-id="cf32b-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="cf32b-134">`<Scale>` (alterando o tamanho proporcionalmente)</span><span class="sxs-lookup"><span data-stu-id="cf32b-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="cf32b-135">Neste exemplo, o painel deve desaparecer. A animação deve levar de 10 a 1,5 segundos (`Duration` atributo), exibindo 24 quadros (etapas de animação) por segundo (atributo`Fps`).</span><span class="sxs-lookup"><span data-stu-id="cf32b-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="cf32b-136">Aqui está a marcação completa para o controle de `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="cf32b-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="cf32b-137">Quando você executa esse script, o painel é exibido e desaparece em um e meio segundo.</span><span class="sxs-lookup"><span data-stu-id="cf32b-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="cf32b-138">[![o painel está esmaecido](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cf32b-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="cf32b-139">O painel está esmaecido ([clique para exibir a imagem em tamanho normal](adding-animation-to-a-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cf32b-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="cf32b-140">Próximo</span><span class="sxs-lookup"><span data-stu-id="cf32b-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
