---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: Associação de dados a um acordeão (C#) | Microsoft Docs
author: wenz
description: O controle de acordeão no AJAX Control Toolkit fornece vários painéis e permite que o usuário exiba um deles de cada vez. Os painéis geralmente são declarados com w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c28cc958a1de9844627ae16175a5aed153993a8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614551"
---
# <a name="databinding-to-an-accordion-c"></a><span data-ttu-id="6b3c7-104">Associação de Dados com um Accordion (C#)</span><span class="sxs-lookup"><span data-stu-id="6b3c7-104">Databinding to an Accordion (C#)</span></span>

<span data-ttu-id="6b3c7-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6b3c7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6b3c7-106">[Baixar código](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) ou [baixar PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6b3c7-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span></span>

> <span data-ttu-id="6b3c7-107">O controle de acordeão no AJAX Control Toolkit fornece vários painéis e permite que o usuário exiba um deles de cada vez.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="6b3c7-108">Os painéis geralmente são declarados dentro da própria página, mas a associação a uma fonte de dados oferece mais flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="6b3c7-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6b3c7-109">Overview</span></span>

<span data-ttu-id="6b3c7-110">O controle de acordeão no AJAX Control Toolkit fornece vários painéis e permite que o usuário exiba um deles de cada vez.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="6b3c7-111">Os painéis geralmente são declarados dentro da própria página, mas a associação a uma fonte de dados oferece mais flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="6b3c7-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="6b3c7-112">Steps</span></span>

<span data-ttu-id="6b3c7-113">Em primeiro lugar, uma fonte de dados é necessária.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-113">First of all, a data source is required.</span></span> <span data-ttu-id="6b3c7-114">Este exemplo usa o banco de dados AdventureWorks e o Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="6b3c7-115">O banco de dados é uma parte opcional de uma instalação do Visual Studio (incluindo a edição Express) e também está disponível como um download separado em [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="6b3c7-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="6b3c7-116">O banco de dados AdventureWorks faz parte dos exemplos SQL Server 2005 e bancos de dados de exemplo (download em [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="6b3c7-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="6b3c7-117">A maneira mais fácil de definir o banco de dados é usar o Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) e anexar o arquivo de banco de dados `AdventureWorks.mdf`.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="6b3c7-118">Para este exemplo, presumimos que a instância do SQL Server 2005 Express Edition é chamada `SQLEXPRESS` e reside no mesmo computador que o servidor Web; Essa também é a configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="6b3c7-119">Se a configuração for diferente, você precisará adaptar as informações de conexão do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="6b3c7-120">Para ativar a funcionalidade do ASP.NET AJAX e do kit de ferramentas de controle, o controle de `ScriptManager` deve ser colocado em qualquer lugar na página (mas dentro do elemento `<form>`):</span><span class="sxs-lookup"><span data-stu-id="6b3c7-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

<span data-ttu-id="6b3c7-121">Em seguida, adicione uma fonte de dados à página.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-121">Then, add a data source to the page.</span></span> <span data-ttu-id="6b3c7-122">Para usar uma quantidade limitada de dados, selecionamos apenas as cinco primeiras entradas na tabela de fornecedores do banco de dados AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="6b3c7-123">Se você estiver usando o assistente do Visual Studio para criar a fonte de dados, lembre-se de que um bug na versão atual não prefixará o nome da tabela (`Vendor`) com `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="6b3c7-124">A marcação a seguir mostra a sintaxe correta:</span><span class="sxs-lookup"><span data-stu-id="6b3c7-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

<span data-ttu-id="6b3c7-125">Lembre-se do nome (ID) da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="6b3c7-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="6b3c7-126">Essa identificação deve ser usada na propriedade `DataSourceID` do controle do acordeão:</span><span class="sxs-lookup"><span data-stu-id="6b3c7-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

<span data-ttu-id="6b3c7-127">Dentro do controle de acordeão, você pode fornecer modelos para várias partes do controle, incluindo o cabeçalho (`<HeaderTemplate>`) e o conteúdo (`<ContentTemplate>`).</span><span class="sxs-lookup"><span data-stu-id="6b3c7-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="6b3c7-128">Dentro desses elementos, basta gerar os dados da fonte de dados, usando o método `DataBinder.Eval()`:</span><span class="sxs-lookup"><span data-stu-id="6b3c7-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

<span data-ttu-id="6b3c7-129">Quando a página é carregada, a fonte de dados deve estar associada ao acordeão com este código do lado do servidor:</span><span class="sxs-lookup"><span data-stu-id="6b3c7-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

<span data-ttu-id="6b3c7-130">Para concluir este exemplo, você precisa definir as duas classes CSS que são referenciadas no controle de acordeão (em suas propriedades `HeaderCssClass` e `ContentCssClass`).</span><span class="sxs-lookup"><span data-stu-id="6b3c7-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="6b3c7-131">Coloque a seguinte marcação na seção `<head>` da página:</span><span class="sxs-lookup"><span data-stu-id="6b3c7-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]

<span data-ttu-id="6b3c7-132">[![os dados no acordeão são fornecidos diretamente da fonte de dados](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6b3c7-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span></span>

<span data-ttu-id="6b3c7-133">Os dados no acordeão são fornecidos diretamente da fonte de dados ([clique para exibir a imagem em tamanho normal](databinding-to-an-accordion-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6b3c7-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6b3c7-134">Próximo</span><span class="sxs-lookup"><span data-stu-id="6b3c7-134">Next</span></span>](dynamically-adding-an-accordion-pane-cs.md)
