---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: Animando um controle UpdatePanel (VB) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. Para o conteúdo de um...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d66dda923940a328c0757049c9d8bfa3b2d2b9fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607101"
---
# <a name="animating-an-updatepanel-control-vb"></a><span data-ttu-id="2eb4b-104">Animar um controle UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="2eb4b-104">Animating an UpdatePanel Control (VB)</span></span>

<span data-ttu-id="2eb4b-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2eb4b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2eb4b-106">[Baixar código](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) ou [baixar PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2eb4b-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span></span>

> <span data-ttu-id="2eb4b-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="2eb4b-108">Para o conteúdo de um UpdatePanel, existe um extensor especial que depende muito da estrutura de animação: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="2eb4b-109">Este tutorial mostra como configurar essa animação para um UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="2eb4b-110">{1&gt;Visão Geral&lt;1}</span><span class="sxs-lookup"><span data-stu-id="2eb4b-110">Overview</span></span>

<span data-ttu-id="2eb4b-111">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="2eb4b-112">Para o conteúdo de um `UpdatePanel`, existe um extensor especial que depende muito da estrutura de animação: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="2eb4b-113">Este tutorial mostra como configurar essa animação para um `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="2eb4b-114">Etapas</span><span class="sxs-lookup"><span data-stu-id="2eb4b-114">Steps</span></span>

<span data-ttu-id="2eb4b-115">A primeira etapa é normalmente para incluir o `ScriptManager` na página para que a biblioteca ASP.NET AJAX seja carregada e o kit de ferramentas de controle possa ser usado:</span><span class="sxs-lookup"><span data-stu-id="2eb4b-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

<span data-ttu-id="2eb4b-116">A animação neste cenário será aplicada a um ASP.NET `Wizard` controle da Web que reside em um `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="2eb4b-117">Três etapas (arbitrárias) fornecem opções suficientes para disparar postbacks:</span><span class="sxs-lookup"><span data-stu-id="2eb4b-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

<span data-ttu-id="2eb4b-118">A marcação necessária para o controle de `UpdatePanelAnimationExtender` é bem semelhante à marcação usada para o `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="2eb4b-119">No atributo `TargetControlID`, fornecemos a `ID` do `UpdatePanel` para animar; dentro do controle `UpdatePanelAnimationExtender`, o elemento `<Animations>` mantém a marcação XML para as animações.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="2eb4b-120">No entanto, há uma diferença: a quantidade de eventos e manipuladores de eventos é limitada em comparação com `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="2eb4b-121">Por `UpdatePanels`, somente duas delas existem:</span><span class="sxs-lookup"><span data-stu-id="2eb4b-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="2eb4b-122">`<OnUpdated>` quando o UpdatePanel foi atualizado</span><span class="sxs-lookup"><span data-stu-id="2eb4b-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="2eb4b-123">`<OnUpdating>` quando o UpdatePanel inicia a atualização</span><span class="sxs-lookup"><span data-stu-id="2eb4b-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="2eb4b-124">Nesse cenário, o novo conteúdo do `UpdatePanel` (após o postback) deve desaparecer.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="2eb4b-125">Essa é a marcação necessária para isso:</span><span class="sxs-lookup"><span data-stu-id="2eb4b-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

<span data-ttu-id="2eb4b-126">Agora, sempre que um postback ocorrer no UpdatePanel, o novo conteúdo do painel esmaecerá sem problemas.</span><span class="sxs-lookup"><span data-stu-id="2eb4b-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="2eb4b-127">[![a próxima etapa do assistente está esmaecida](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2eb4b-127">[![The next wizard step is fading in](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="2eb4b-128">A próxima etapa do assistente está esmaecida ([clique para exibir a imagem em tamanho normal](animating-an-updatepanel-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2eb4b-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2eb4b-129">[Anterior](changing-an-animation-using-client-side-code-vb.md)
> [Próximo](dynamically-controlling-updatepanel-animations-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2eb4b-129">[Previous](changing-an-animation-using-client-side-code-vb.md)
[Next](dynamically-controlling-updatepanel-animations-vb.md)</span></span>
