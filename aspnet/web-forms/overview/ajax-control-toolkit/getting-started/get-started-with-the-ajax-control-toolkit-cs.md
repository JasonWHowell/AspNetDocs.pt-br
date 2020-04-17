---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Comece com o AJAX Control Toolkit (C#) | Microsoft Docs
author: rick-anderson
description: Aprenda tudo o que você precisa saber para começar a usar o AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: b5954019ec3312f06f38012e4d3f9b1f71573f76
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543581"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="13138-103">Introdução ao AJAX Control Toolkit (C#)</span><span class="sxs-lookup"><span data-stu-id="13138-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="13138-104">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="13138-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="13138-105">Aprenda tudo o que você precisa saber para começar a usar o AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="13138-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="13138-106">O AJAX Control Toolkit contém mais de 30 controles gratuitos que você pode usar em seus aplicativos de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="13138-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="13138-107">Neste tutorial, você aprende a baixar o AJAX Control Toolkit e adicionar os controles do kit de ferramentas à sua caixa de ferramentas Visual Studio/Visual Web Developer Express.</span><span class="sxs-lookup"><span data-stu-id="13138-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="13138-108">Baixando o AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="13138-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="13138-109">O [AJAX Control Toolkit](http://devexpress.com/act) é um projeto de código aberto desenvolvido pelos membros da comunidade ASP.NET e da equipe ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="13138-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 

<span data-ttu-id="13138-110">[![Baixando o AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="13138-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="13138-111">**Figura 01**: Baixar o AJAX Control Toolkit[(Clique para ver imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="13138-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>

<span data-ttu-id="13138-112">Depois de baixar o arquivo, você precisa desbloquear o arquivo.</span><span class="sxs-lookup"><span data-stu-id="13138-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="13138-113">Clique com o botão direito do mouse no arquivo, selecione Propriedades e clique no botão **Desbloquear** (consulte Figura 2).</span><span class="sxs-lookup"><span data-stu-id="13138-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="13138-114">[![Desbloqueando o arquivo ZIP do AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="13138-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="13138-115">**Figura 02**: Desbloquear o arquivo ZIP do AJAX Control Toolkit[(Clique para exibir a imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="13138-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>

<span data-ttu-id="13138-116">Depois de desbloquear o arquivo, você pode descompactar o arquivo: Clique com o botão direito do mouse no arquivo e selecione a opção **Extrato Todos** o menu.</span><span class="sxs-lookup"><span data-stu-id="13138-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="13138-117">Agora, estamos prontos para adicionar o kit de ferramentas à caixa de ferramentas visual studio/visual web developer.</span><span class="sxs-lookup"><span data-stu-id="13138-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="13138-118">Adicionando o Kit de Ferramentas de Controle AJAX à caixa de ferramentas</span><span class="sxs-lookup"><span data-stu-id="13138-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="13138-119">A maneira mais fácil de usar o AJAX Control Toolkit é adicionar o kit de ferramentas à sua caixa de ferramentas Visual Studio/Visual Web Developer (ver Figura 3).</span><span class="sxs-lookup"><span data-stu-id="13138-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="13138-120">Dessa forma, você pode simplesmente arrastar um controle de kit de ferramentas para uma página quando quiser usá-lo.</span><span class="sxs-lookup"><span data-stu-id="13138-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="13138-121">[![AJAX Control Toolkit aparece na caixa de ferramentas](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="13138-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="13138-122">**Figura 03**: AJAX Control Toolkit aparece na caixa de ferramentas[(Clique para exibir imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="13138-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>

<span data-ttu-id="13138-123">Primeiro, você precisa adicionar uma guia AJAX Control Toolkit à caixa de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="13138-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="13138-124">Siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="13138-124">Follow these steps.</span></span>

1. <span data-ttu-id="13138-125">Crie um novo site ASP.NET selecionando a opção menu Arquivo, Novo Site.</span><span class="sxs-lookup"><span data-stu-id="13138-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="13138-126">Clique duas vezes no Default.aspx na janela Solution Explorer para abrir o arquivo no editor.</span><span class="sxs-lookup"><span data-stu-id="13138-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="13138-127">Clique com o botão direito do mouse na caixa de ferramentas abaixo da Guia Geral e selecione a opção de menu **Adicionar guia** (ver Figura 4).</span><span class="sxs-lookup"><span data-stu-id="13138-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="13138-128">Digite uma nova guia chamada AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="13138-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="13138-129">[![Adicionando uma nova guia](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="13138-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="13138-130">**Figura 04**: Adicionando uma nova guia[(Clique para exibir imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="13138-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>

<span data-ttu-id="13138-131">Em seguida, você precisa adicionar os controles ajax control toolkit à nova guia. Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="13138-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="13138-132">Clique com o botão direito do mouse abaixo da guia AJAX Control Toolkit e selecione a opção menu **Escolha itens (veja Figura 5)**.</span><span class="sxs-lookup"><span data-stu-id="13138-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="13138-133">Navegue até o local onde você descompactou o AJAX Control Toolkit e selecione o conjunto AjaxControlToolkit.dll.</span><span class="sxs-lookup"><span data-stu-id="13138-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="13138-134">[![Escolha itens para adicionar à caixa de ferramentas](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="13138-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="13138-135">**Figura 05**: Escolha itens para adicionar à caixa de ferramentas[(Clique para exibir imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="13138-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>

<span data-ttu-id="13138-136">Depois de concluir essas etapas, todos os controles do kit de ferramentas aparecerão em sua caixa de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="13138-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="13138-137">Atualizando para uma nova versão do Kit de ferramentas</span><span class="sxs-lookup"><span data-stu-id="13138-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="13138-138">Se você estava usando uma versão mais antiga do Toolkit e agora precisa passar para uma versão posterior aqui estão as etapas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="13138-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="13138-139">Binários - Exclua a versão antiga do conjunto AjaxControlToolkit.dll da pasta Bin do seu site.</span><span class="sxs-lookup"><span data-stu-id="13138-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="13138-140">Itens da caixa de ferramentas - Exclua a guia AJAX Control Toolkit e siga os passos acima para recriar a guia com a nova versão do conjunto AjaxControlToolkit.dll.</span><span class="sxs-lookup"><span data-stu-id="13138-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="13138-141">Avançar</span><span class="sxs-lookup"><span data-stu-id="13138-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
