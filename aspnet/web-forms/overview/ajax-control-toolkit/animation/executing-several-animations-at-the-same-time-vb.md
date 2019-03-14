---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: Executando várias animações ao mesmo tempo (VB) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. Ele permite para executar severa...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: 20baa40c34dd8c8907b940764987441bc7a91da9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041373"
---
<a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="0a596-104">Executando várias animações ao mesmo tempo (VB)</span><span class="sxs-lookup"><span data-stu-id="0a596-104">Executing Several Animations at The Same Time (VB)</span></span>
====================
<span data-ttu-id="0a596-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0a596-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0a596-106">[Baixar o código](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0a596-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="0a596-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="0a596-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0a596-108">Ele permite para executar várias animações de forma paralela.</span><span class="sxs-lookup"><span data-stu-id="0a596-108">It allows to run several animations in a parallel fashion.</span></span>


## <a name="overview"></a><span data-ttu-id="0a596-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0a596-109">Overview</span></span>

<span data-ttu-id="0a596-110">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="0a596-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0a596-111">Ele permite para executar várias animações de forma paralela.</span><span class="sxs-lookup"><span data-stu-id="0a596-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="0a596-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="0a596-112">Steps</span></span>

<span data-ttu-id="0a596-113">Em primeiro lugar, inclua o `ScriptManager` na página; em seguida, a biblioteca do AJAX ASP.NET é carregada, tornando possível usar o Kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="0a596-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="0a596-114">A animação será aplicada a um painel de texto que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="0a596-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="0a596-115">Na classe CSS associado para o painel, definir uma cor de fundo interessante e também definir uma largura fixa para o painel:</span><span class="sxs-lookup"><span data-stu-id="0a596-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="0a596-116">Em seguida, adicione a `AnimationExtender` para a página, fornecendo uma `ID`, o `TargetControlID` atributo e o obrigatoriamente `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="0a596-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="0a596-117">Dentro de `<Animations>` nó, use `<OnLoad>` para as animações são executadas uma vez que a página foi totalmente carregada.</span><span class="sxs-lookup"><span data-stu-id="0a596-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="0a596-118">Em geral, `<OnLoad>` aceita apenas uma animação.</span><span class="sxs-lookup"><span data-stu-id="0a596-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="0a596-119">A estrutura de animação permite unir várias animações em um, utilizando o `<Parallel>` elemento.</span><span class="sxs-lookup"><span data-stu-id="0a596-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="0a596-120">Todas as animações em `<Parallel>` são executadas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="0a596-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="0a596-121">Aqui está a uma marcação possíveis para o `AnimationExtender` controle, o desaparecimento e redimensionar o painel ao mesmo tempo:</span><span class="sxs-lookup"><span data-stu-id="0a596-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="0a596-122">E realmente: quando você executa esse script, o painel é exibido e, em seguida, redimensiona (mais do que threefolding sua largura e halfing sua altura) e fade out ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="0a596-122">And indeed: when you run this script, the panel is displayed, then resizes (more than threefolding its width and halfing its height) and fades out at the same time.</span></span>


<span data-ttu-id="0a596-123">[![O painel é desaparecimento e redimensionamento (incluindo seu conteúdo, graças ao mecanismo de renderização do navegador)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0a596-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span></span>

<span data-ttu-id="0a596-124">O painel é desaparecimento e redimensionamento (incluindo seu conteúdo, graças ao mecanismo de renderização do navegador) ([clique para exibir a imagem em tamanho normal](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0a596-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0a596-125">[Anterior](adding-animation-to-a-control-vb.md)
> [Próximo](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0a596-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>