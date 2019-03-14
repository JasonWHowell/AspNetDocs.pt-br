---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: Tratamento de Postbacks de um controle pop-up sem um UpdatePanel (VB) | Microsoft Docs
author: wenz
description: O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado. Quando ocorre um postback em su...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 6dcb2b09279ec6400465f79fadc2a1b6c72f8f07
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064553"
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="a6cee-104">Tratamento de postbacks de um controle pop-up sem um UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="a6cee-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>
====================
<span data-ttu-id="a6cee-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a6cee-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a6cee-106">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a6cee-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="a6cee-107">O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado.</span><span class="sxs-lookup"><span data-stu-id="a6cee-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="a6cee-108">Quando ocorre um postback em tal um painel e há vários painéis na página é difícil determinar qual painel foi clicado.</span><span class="sxs-lookup"><span data-stu-id="a6cee-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="a6cee-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a6cee-109">Overview</span></span>

<span data-ttu-id="a6cee-110">O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado.</span><span class="sxs-lookup"><span data-stu-id="a6cee-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="a6cee-111">Quando ocorre um postback em tal um painel e há vários painéis na página é difícil determinar qual painel foi clicado.</span><span class="sxs-lookup"><span data-stu-id="a6cee-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="a6cee-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="a6cee-112">Steps</span></span>

<span data-ttu-id="a6cee-113">Ao usar um `PopupControl` com um postback, mas sem a necessidade de um `UpdatePanel` na página, o Kit de ferramentas de controle não oferece uma maneira de determinar qual elemento cliente disparou o pop-up que por sua vez causou o postback.</span><span class="sxs-lookup"><span data-stu-id="a6cee-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="a6cee-114">No entanto, um pequeno truque fornece uma solução alternativa para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="a6cee-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="a6cee-115">Em primeiro lugar, aqui está a configuração básica: duas caixas de texto que disparam o mesmo pop-up, um calendário.</span><span class="sxs-lookup"><span data-stu-id="a6cee-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="a6cee-116">Dois `PopupControlExtenders` reúnem as caixas de texto e o pop-up.</span><span class="sxs-lookup"><span data-stu-id="a6cee-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="a6cee-117">A ideia básica é adicionar um campo de formulário oculto na &lt; `form` &gt; elemento que contém a caixa de texto que iniciou o pop-up:</span><span class="sxs-lookup"><span data-stu-id="a6cee-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="a6cee-118">Quando a página é carregada, o código JavaScript adiciona um manipulador de eventos para ambas as caixas de texto: Sempre que o usuário clica em uma caixa de texto, seu nome é escrito no campo de formulário oculto:</span><span class="sxs-lookup"><span data-stu-id="a6cee-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="a6cee-119">No código do lado do servidor, o valor do campo oculto deve ser lido.</span><span class="sxs-lookup"><span data-stu-id="a6cee-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="a6cee-120">Como os campos de formulário ocultos são triviais para manipular, uma abordagem de lista de permissões para validar o valor oculto é necessária.</span><span class="sxs-lookup"><span data-stu-id="a6cee-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="a6cee-121">Depois que a caixa de texto correto foi identificada, a data do calendário é gravada nele.</span><span class="sxs-lookup"><span data-stu-id="a6cee-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]


<span data-ttu-id="a6cee-122">[![O calendário é exibido quando o usuário clica na caixa de texto](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a6cee-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="a6cee-123">O calendário é exibido quando o usuário clica na caixa de texto ([clique para exibir a imagem em tamanho normal](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a6cee-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>


<span data-ttu-id="a6cee-124">[![Clicar em uma data coloca na caixa de texto](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="a6cee-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="a6cee-125">Clicar em uma data coloca na caixa de texto ([clique para exibir a imagem em tamanho normal](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="a6cee-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a6cee-126">Anterior</span><span class="sxs-lookup"><span data-stu-id="a6cee-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)