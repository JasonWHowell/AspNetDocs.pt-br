---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: Usando postback automático com CascadingDropDown (C#) | Microsoft Docs
author: wenz
description: O controle CascadingDropDown no AJAX Control Toolkit estende um controle DropDownList para que as alterações em uma DropDownList carreguem valores associados em anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574518"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a><span data-ttu-id="6a18c-103">Uso de postback automático com CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="6a18c-103">Using Auto-Postback with CascadingDropDown (C#)</span></span>

<span data-ttu-id="6a18c-104">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6a18c-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6a18c-105">[Baixar código](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) ou [baixar PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6a18c-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span></span>

> <span data-ttu-id="6a18c-106">O controle CascadingDropDown no AJAX Control Toolkit estende um controle DropDownList para que as alterações em uma DropDownList carreguem valores associados em outra DropDownList.</span><span class="sxs-lookup"><span data-stu-id="6a18c-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="6a18c-107">No entanto, ao usar o controle CascadingDropDown, o ASP. O recurso AutoPostBack do controle DropDownList da NET não funciona, pois o carregamento de dados de forma assíncrona na lista gera um postback (desnecessário) em si.</span><span class="sxs-lookup"><span data-stu-id="6a18c-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="6a18c-108">Com algum código JavaScript, esse efeito pode ser evitado.</span><span class="sxs-lookup"><span data-stu-id="6a18c-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="6a18c-109">{1&gt;Visão Geral&lt;1}</span><span class="sxs-lookup"><span data-stu-id="6a18c-109">Overview</span></span>

<span data-ttu-id="6a18c-110">O controle CascadingDropDown no AJAX Control Toolkit estende um controle DropDownList para que as alterações em uma DropDownList carreguem valores associados em outra DropDownList.</span><span class="sxs-lookup"><span data-stu-id="6a18c-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="6a18c-111">(Por exemplo, uma lista fornece uma lista de Estados dos EUA e a próxima lista é então preenchida com cidades principais nesse estado.) No entanto, ao usar o controle CascadingDropDown, o ASP. O recurso AutoPostBack do controle DropDownList da NET não funciona, pois o carregamento de dados de forma assíncrona na lista gera um postback (desnecessário) em si.</span><span class="sxs-lookup"><span data-stu-id="6a18c-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="6a18c-112">Com algum código JavaScript, esse efeito pode ser evitado.</span><span class="sxs-lookup"><span data-stu-id="6a18c-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="6a18c-113">Etapas</span><span class="sxs-lookup"><span data-stu-id="6a18c-113">Steps</span></span>

<span data-ttu-id="6a18c-114">Para ativar a funcionalidade do ASP.NET AJAX e do kit de ferramentas de controle, o controle de `ScriptManager` deve ser colocado em qualquer lugar na página (mas dentro do elemento &lt;`form`&gt;):</span><span class="sxs-lookup"><span data-stu-id="6a18c-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="6a18c-115">Em seguida, um controle DropDownList é necessário:</span><span class="sxs-lookup"><span data-stu-id="6a18c-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="6a18c-116">Para essa lista, um extensor CascadingDropDown é adicionado, fornecendo a URL do serviço Web e informações do método:</span><span class="sxs-lookup"><span data-stu-id="6a18c-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="6a18c-117">Em seguida, o extensor CascadingDropDown chama assincronamente um serviço Web com a seguinte assinatura de método:</span><span class="sxs-lookup"><span data-stu-id="6a18c-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="6a18c-118">O método retorna uma matriz do tipo valor CascadingDropDown.</span><span class="sxs-lookup"><span data-stu-id="6a18c-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="6a18c-119">O construtor do tipo espera primeiro a legenda da entrada da lista e, em seguida, o valor (HTML `value` atributo).</span><span class="sxs-lookup"><span data-stu-id="6a18c-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="6a18c-120">Carregar a página no navegador preencherá a lista suspensa com três fornecedores, a segunda sendo selecionada.</span><span class="sxs-lookup"><span data-stu-id="6a18c-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="6a18c-121">Além disso, ASP.NET define o `__doPostBack()` método JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6a18c-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="6a18c-122">Depois que a página for carregada, essa chamada JavaScript será adicionada à lista suspensa, mas somente se houver elementos nela.</span><span class="sxs-lookup"><span data-stu-id="6a18c-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="6a18c-123">Se não houver nenhum elemento na lista, o kit de ferramentas de controle está carregando-os no momento, portanto, o código JavaScript usa um tempo limite e tenta novamente em um meio segundo.</span><span class="sxs-lookup"><span data-stu-id="6a18c-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

<span data-ttu-id="6a18c-124">Dessa forma, um postback só é executado quando há elementos na lista e o usuário seleciona uma entrada.</span><span class="sxs-lookup"><span data-stu-id="6a18c-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="6a18c-125">[![selecionar um elemento de lista causa um postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6a18c-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="6a18c-126">A seleção de um elemento de lista causa um postback ([clique para exibir a imagem em tamanho normal](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6a18c-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6a18c-127">[Anterior](presetting-list-entries-with-cascadingdropdown-cs.md)
> [Próximo](filling-a-list-using-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6a18c-127">[Previous](presetting-list-entries-with-cascadingdropdown-cs.md)
[Next](filling-a-list-using-cascadingdropdown-vb.md)</span></span>
