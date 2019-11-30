---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: Desabilitando ações durante a animação (VB) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. Ele também dá suporte a ação...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606828"
---
# <a name="disabling-actions-during-animation-vb"></a><span data-ttu-id="84851-104">Desabilitar ações durante a animação (VB)</span><span class="sxs-lookup"><span data-stu-id="84851-104">Disabling Actions during Animation (VB)</span></span>

<span data-ttu-id="84851-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="84851-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="84851-106">[Baixar código](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) ou [baixar PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="84851-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span></span>

> <span data-ttu-id="84851-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="84851-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="84851-108">Ele também dá suporte a ações, como cliques do mouse.</span><span class="sxs-lookup"><span data-stu-id="84851-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="84851-109">No entanto, quando um clique do mouse inicia uma animação, é desejável desabilitar cliques do mouse durante a animação.</span><span class="sxs-lookup"><span data-stu-id="84851-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="84851-110">{1&gt;Visão Geral&lt;1}</span><span class="sxs-lookup"><span data-stu-id="84851-110">Overview</span></span>

<span data-ttu-id="84851-111">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="84851-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="84851-112">Ele também dá suporte a ações, como cliques do mouse.</span><span class="sxs-lookup"><span data-stu-id="84851-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="84851-113">No entanto, quando um clique do mouse inicia uma animação, é desejável desabilitar cliques do mouse durante a animação.</span><span class="sxs-lookup"><span data-stu-id="84851-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="84851-114">Etapas</span><span class="sxs-lookup"><span data-stu-id="84851-114">Steps</span></span>

<span data-ttu-id="84851-115">Em primeiro lugar, inclua o `ScriptManager` na página; em seguida, a biblioteca do ASP.NET AJAX é carregada, possibilitando o uso do kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="84851-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

<span data-ttu-id="84851-116">A animação será aplicada a um botão HTML como este:</span><span class="sxs-lookup"><span data-stu-id="84851-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

<span data-ttu-id="84851-117">Observe que um controle HTML é usado em vez de um controle da Web, já que não queremos que o botão crie um postback; Ele deve simplesmente iniciar a animação do lado do cliente para nós.</span><span class="sxs-lookup"><span data-stu-id="84851-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="84851-118">Em seguida, adicione o `AnimationExtender` à página, fornecendo um `ID`, o atributo `TargetControlID` e a `runat="server"`obrigatório:</span><span class="sxs-lookup"><span data-stu-id="84851-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

<span data-ttu-id="84851-119">Dentro do nó `<Animations>`, `<OnClick>` é o elemento certo para manipular o clique do mouse.</span><span class="sxs-lookup"><span data-stu-id="84851-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="84851-120">No entanto, o botão também poderia ser clicado durante a animação.</span><span class="sxs-lookup"><span data-stu-id="84851-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="84851-121">O elemento `<EnableAction>` pode cuidar disso.</span><span class="sxs-lookup"><span data-stu-id="84851-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="84851-122">A configuração `Enabled="false"` desabilita o botão como parte da animação.</span><span class="sxs-lookup"><span data-stu-id="84851-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="84851-123">Como estamos usando várias animações individuais (desativando o botão e as animações reais), o elemento `<Parallel>` é necessário para unir as animações individuais em uma.</span><span class="sxs-lookup"><span data-stu-id="84851-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="84851-124">Aqui está a marcação completa para `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="84851-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

<span data-ttu-id="84851-125">Também seria possível reabilitar o botão após a animação, usando o seguinte elemento XML no final da lista:</span><span class="sxs-lookup"><span data-stu-id="84851-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

<span data-ttu-id="84851-126">No entanto, no cenário fornecido, isso seria inútil, pois o botão desaparece e não fica visível no final da animação.</span><span class="sxs-lookup"><span data-stu-id="84851-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="84851-127">[![o botão é desabilitado assim que a animação é executada](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="84851-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span></span>

<span data-ttu-id="84851-128">O botão é desabilitado assim que a animação é executada ([clique para exibir a imagem em tamanho normal](disabling-actions-during-animation-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="84851-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="84851-129">[Anterior](animating-in-response-to-user-interaction-vb.md)
> [Próximo](triggering-an-animation-in-another-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="84851-129">[Previous](animating-in-response-to-user-interaction-vb.md)
[Next](triggering-an-animation-in-another-control-vb.md)</span></span>
