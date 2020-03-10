---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: Usando Inspetor de Página no MVC ASP.NET | Microsoft Docs
author: rick-anderson
description: Inspetor de Página no Visual Studio 2012 é uma ferramenta de desenvolvimento para a Web com um navegador integrado. Selecione qualquer elemento no navegador integrado e Inspetor de Página i...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538013"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="5f808-104">Usando o Inspetor de Página no ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="5f808-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="5f808-105">por Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="5f808-105">by Tim Ammann</span></span>

> <span data-ttu-id="5f808-106">Inspetor de Página no Visual Studio 2012 é uma ferramenta de desenvolvimento para a Web com um navegador integrado.</span><span class="sxs-lookup"><span data-stu-id="5f808-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="5f808-107">Selecione qualquer elemento no navegador integrado e Inspetor de Página realça instantaneamente a origem e o CSS do elemento.</span><span class="sxs-lookup"><span data-stu-id="5f808-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="5f808-108">Você pode procurar qualquer modo de exibição MVC, localizar rapidamente as fontes de marcação renderizada e usar as ferramentas de navegador diretamente no ambiente do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f808-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="5f808-109">Assista ao vídeo</span><span class="sxs-lookup"><span data-stu-id="5f808-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="5f808-110">Este tutorial mostra como habilitar Modo de Inspeção e, em seguida, localizar e editar rapidamente a marcação e o CSS em seu projeto Web.</span><span class="sxs-lookup"><span data-stu-id="5f808-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="5f808-111">O tutorial usa um projeto MVC, mas você também pode usar Inspetor de Página para [Web Forms](https://go.microsoft.com/?linkid=9802001) e outros aplicativos ASP.net.</span><span class="sxs-lookup"><span data-stu-id="5f808-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="5f808-112">O tutorial tem as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="5f808-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="5f808-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5f808-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="5f808-114">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5f808-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="5f808-115">Usar Inspetor de Página para navegar até um modo de exibição</span><span class="sxs-lookup"><span data-stu-id="5f808-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="5f808-116">Habilitar Modo de Inspeção</span><span class="sxs-lookup"><span data-stu-id="5f808-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="5f808-117">Usar Inspetor de Página para fazer alterações na marcação</span><span class="sxs-lookup"><span data-stu-id="5f808-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="5f808-118">Modo de Inspeção e a janela HTML</span><span class="sxs-lookup"><span data-stu-id="5f808-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - [<span data-ttu-id="5f808-119">Visualizar alterações de CSS na janela estilos</span><span class="sxs-lookup"><span data-stu-id="5f808-119">Preview CSS Changes in the Styles window</span></span>](#_7_previewing_css)
> - [<span data-ttu-id="5f808-120">Sincronização automática de CSS</span><span class="sxs-lookup"><span data-stu-id="5f808-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="5f808-121">Usando o seletor de cores CSS</span><span class="sxs-lookup"><span data-stu-id="5f808-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="5f808-122">Mapeando elementos de página dinâmica para JavaScript</span><span class="sxs-lookup"><span data-stu-id="5f808-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="5f808-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5f808-123">Prerequisites</span></span>

- <span data-ttu-id="5f808-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) ou [Visual Studio Express 2012 para Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="5f808-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="5f808-125">Para obter a versão mais recente do Inspetor de Página, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) para instalar o SDK do Windows Azure para .NET 2,0.</span><span class="sxs-lookup"><span data-stu-id="5f808-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="5f808-126">Inspetor de Página é agrupado com Microsoft Web Developer Tools.</span><span class="sxs-lookup"><span data-stu-id="5f808-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="5f808-127">A versão mais recente é 1,3.</span><span class="sxs-lookup"><span data-stu-id="5f808-127">The latest version is 1.3.</span></span> <span data-ttu-id="5f808-128">Para verificar qual versão você tem, execute o Visual Studio e selecione **sobre Microsoft Visual Studio** no menu **ajuda** .</span><span class="sxs-lookup"><span data-stu-id="5f808-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="5f808-129">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5f808-129">Create a Web Application</span></span>

<span data-ttu-id="5f808-130">Primeiro, crie um aplicativo Web com o qual você usará Inspetor de Página.</span><span class="sxs-lookup"><span data-stu-id="5f808-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="5f808-131">No Visual Studio, escolha **arquivo** &gt; **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="5f808-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="5f808-132">À esquerda, expanda **Visual C#** , selecione **Web**e, em seguida, selecione **ASP.net MVC4 aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="5f808-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![Novo aplicativo MVC ASP.NET](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="5f808-134">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f808-134">Click **OK**.</span></span>

<span data-ttu-id="5f808-135">Na caixa de diálogo **novo projeto do ASP.NET MVC 4** , selecione **aplicativo de Internet**.</span><span class="sxs-lookup"><span data-stu-id="5f808-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="5f808-136">Deixe o **Razor** como o mecanismo de exibição padrão.</span><span class="sxs-lookup"><span data-stu-id="5f808-136">Leave **Razor** as the default view engine.</span></span>

![Novo projeto MVC do ASP.NET – aplicativo de Internet](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="5f808-138">O aplicativo é aberto no modo de exibição de **código-fonte** .</span><span class="sxs-lookup"><span data-stu-id="5f808-138">The application opens in **Source** view.</span></span>

![Novo aplicativo MVC ASP.NET na exibição de origem](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="5f808-140">Agora que você tem um aplicativo com o qual trabalhar, você pode usar Inspetor de Página para examiná-lo e modificá-lo.</span><span class="sxs-lookup"><span data-stu-id="5f808-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="5f808-141">Usar Inspetor de Página para navegar até um modo de exibição</span><span class="sxs-lookup"><span data-stu-id="5f808-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="5f808-142">No Visual Studio 2012, você pode clicar com o botão direito do mouse em qualquer exibição em seu projeto, selecionar **Exibir no Inspetor de página**e Inspetor de página irá descobrir a rota e exibir a página.</span><span class="sxs-lookup"><span data-stu-id="5f808-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="5f808-143">Em **Gerenciador de soluções**, expanda a pasta **exibições** e a pasta **base** .</span><span class="sxs-lookup"><span data-stu-id="5f808-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="5f808-144">Clique com o botão direito do mouse no arquivo index. cshtml e escolha **Exibir no Inspetor de página**.</span><span class="sxs-lookup"><span data-stu-id="5f808-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![Exibir index. cshtml no Inspetor de Página](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="5f808-146">Por padrão, Inspetor de Página é encaixada como uma janela no lado esquerdo do ambiente do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f808-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="5f808-147">Se preferir, você pode encaixá-lo em outro lugar ou desencaixar a janela.</span><span class="sxs-lookup"><span data-stu-id="5f808-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="5f808-148">Consulte [como: organizar e encaixar janelas](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f808-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="5f808-149">O painel superior da janela de Inspetor de Página mostra a página atual em uma janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="5f808-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="5f808-150">O painel inferior mostra a página na marcação HTML, juntamente com algumas guias que permitem inspecionar diferentes aspectos da página.</span><span class="sxs-lookup"><span data-stu-id="5f808-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="5f808-151">O painel inferior é semelhante ao [ferramentas para desenvolvedores F12](https://msdn.microsoft.com/ie/aa740478) no Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5f808-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![Aplicativo ASP.NET MVC no Inspetor de Página](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="5f808-153">Neste tutorial, você usará as guias **HTML** e **estilos** para navegar rapidamente e fazer alterações no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5f808-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="5f808-154">Modo de EnableInspection</span><span class="sxs-lookup"><span data-stu-id="5f808-154">EnableInspection Mode</span></span>

<span data-ttu-id="5f808-155">Para colocar Inspetor de Página em Modo de Inspeção, clique no botão **inspecionar** .</span><span class="sxs-lookup"><span data-stu-id="5f808-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="5f808-156">Em Modo de Inspeção, quando você mantém o ponteiro do mouse sobre qualquer parte da página renderizada, a marcação de origem ou o código correspondente é realçado.</span><span class="sxs-lookup"><span data-stu-id="5f808-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![Alternar Modo de Inspeção](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="5f808-158">Agora, mova o mouse sobre diferentes partes da página dentro Inspetor de Página.</span><span class="sxs-lookup"><span data-stu-id="5f808-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="5f808-159">Como você faz, o ponteiro do mouse muda para um sinal de adição grande e o elemento abaixo é realçado:</span><span class="sxs-lookup"><span data-stu-id="5f808-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Passando o mouse sobre div. Content-Wrapper](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="5f808-161">À medida que você move o ponteiro do mouse, o Visual Studio realça o sintaxe Razor correspondente no arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="5f808-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="5f808-162">Se o elemento HTML vier de outro arquivo de origem, o Visual Studio abrirá automaticamente o arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f808-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="5f808-163">No Inspetor de Página, a guia **HTML** mostra o HTML que foi gerado a partir do sintaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="5f808-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="5f808-164">À medida que você move o ponteiro do mouse, os elementos HTML são realçados.</span><span class="sxs-lookup"><span data-stu-id="5f808-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="5f808-165">A guia **estilos** mostra as regras de CSS para o elemento.</span><span class="sxs-lookup"><span data-stu-id="5f808-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="5f808-166">Usar Inspetor de Página para fazer alterações na marcação</span><span class="sxs-lookup"><span data-stu-id="5f808-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="5f808-167">Inspetor de Página permite encontrar marcação cujo local pode não ser óbvio.</span><span class="sxs-lookup"><span data-stu-id="5f808-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="5f808-168">Em seguida, você pode modificar a marcação e ver as alterações resultantes.</span><span class="sxs-lookup"><span data-stu-id="5f808-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="5f808-169">Para ver isso, clique em **inspecionar** e role até a parte inferior da página na janela Inspetor de página.</span><span class="sxs-lookup"><span data-stu-id="5f808-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="5f808-170">Quando você move o ponteiro do mouse para a área de rodapé, Inspetor de Página abre o arquivo \_layout. cshtml e realça a seção da página de layout que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="5f808-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="5f808-171">Como você pode ver, o rodapé é definido no arquivo de layout e não na exibição em si.</span><span class="sxs-lookup"><span data-stu-id="5f808-171">As you can see, the footer are is defined in the layout file, and not the view itself.</span></span>

![Rodapé](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="5f808-173">Agora, mova o ponteiro do mouse sobre a linha com <a id="a"> </a>o aviso de direitos autorais.</span><span class="sxs-lookup"><span data-stu-id="5f808-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="5f808-174">Na página \_layout. cshtml, a linha correspondente é realçada.</span><span class="sxs-lookup"><span data-stu-id="5f808-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![Linha de copyright de rodapé realçada](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="5f808-176">Adicione texto ao final da linha no arquivo layout. cshtml do \_.</span><span class="sxs-lookup"><span data-stu-id="5f808-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="5f808-177">&lt;p&gt;&amp;cópia; @DateTime.Now.Year-meu aplicativo MVC ASP.NET Rocks!&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="5f808-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="5f808-178">Agora, pressione Ctrl + Alt + Enter ou clique na barra de atualização para ver os resultados na janela do navegador Inspetor de Página.</span><span class="sxs-lookup"><span data-stu-id="5f808-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![Meu aplicativo ASP.NET Rocks!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="5f808-180">Talvez você tenha pensado no rodapé definido em index. cshtml, mas ele se tornou no \_layout. cshtml e Inspetor de Página encontrá-lo para você.</span><span class="sxs-lookup"><span data-stu-id="5f808-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="5f808-181">Modo de Inspeção e a janela HTML</span><span class="sxs-lookup"><span data-stu-id="5f808-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="5f808-182">Em seguida, você terá uma visão rápida da janela HTML e de como ela mapeia os elementos para você.</span><span class="sxs-lookup"><span data-stu-id="5f808-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="5f808-183">Clique em **inspecionar** para colocar Inspetor de Página em modo de inspeção.</span><span class="sxs-lookup"><span data-stu-id="5f808-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="5f808-184">Clique na parte superior da página que diz "seu logotipo aqui".</span><span class="sxs-lookup"><span data-stu-id="5f808-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="5f808-185">Você está examinando um elemento específico em mais detalhes, portanto, a exibição na janela do navegador não é mais alterada à medida que você move o ponteiro do mouse.</span><span class="sxs-lookup"><span data-stu-id="5f808-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="5f808-186">Agora, mova o ponteiro do mouse para a janela **HTML** .</span><span class="sxs-lookup"><span data-stu-id="5f808-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="5f808-187">À medida que você move o ponteiro do mouse, Inspetor de Página descreve o elemento dentro da janela **HTML** e realça o elemento correspondente na janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="5f808-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![Janela HTML](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="5f808-189">Como antes, Inspetor de Página abre o arquivo \_layout. cshtml para você em uma guia temporária. Clique na guia temporário do \_layout. cshtml e a marcação correspondente será realçada na seção&gt; do cabeçalho de &lt;para você:</span><span class="sxs-lookup"><span data-stu-id="5f808-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![Marcação realçada](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="5f808-191">Visualizar alterações de CSS na janela estilos</span><span class="sxs-lookup"><span data-stu-id="5f808-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="5f808-192">Em seguida, você usará a janela **estilos** de Inspetor de página para visualizar as alterações no CSS.</span><span class="sxs-lookup"><span data-stu-id="5f808-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="5f808-193">Clique em **inspecionar** para colocar Inspetor de Página em modo de inspeção.</span><span class="sxs-lookup"><span data-stu-id="5f808-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="5f808-194">Na janela do navegador Inspetor de Página, mova o ponteiro do mouse sobre a seção "Home Page" até que o rótulo **div. Content-wrapper** seja exibido.</span><span class="sxs-lookup"><span data-stu-id="5f808-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Passando o mouse sobre div. Content-Wrapper](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="5f808-196">Clique na seção div. Content-wrapper uma vez e mova o ponteiro do mouse para a janela **estilos** .</span><span class="sxs-lookup"><span data-stu-id="5f808-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="5f808-197">A janela **estilos** mostra todas as regras de CSS para este elemento.</span><span class="sxs-lookup"><span data-stu-id="5f808-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="5f808-198">Role para baixo até localizar o seletor de classe. em destaque. Content-wrapper.</span><span class="sxs-lookup"><span data-stu-id="5f808-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="5f808-199">Agora desmarque a caixa de seleção da propriedade Background-Color.</span><span class="sxs-lookup"><span data-stu-id="5f808-199">Now clear the checkbox for the background-color property.</span></span>

![Limpar cor da fundo](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="5f808-201">Observe como as visualizações de alteração são instantaneamente na janela Inspetor de Página navegador.</span><span class="sxs-lookup"><span data-stu-id="5f808-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="5f808-202">Marque a caixa de seleção novamente, clique duas vezes no valor da propriedade e altere-o para vermelho.</span><span class="sxs-lookup"><span data-stu-id="5f808-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="5f808-203">A alteração mostra imediatamente:</span><span class="sxs-lookup"><span data-stu-id="5f808-203">The change shows immediately:</span></span>

![Cor de fundo vermelha](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="5f808-205">A janela **estilos** facilita o teste e a visualização das alterações de CSS antes de você confirmar as alterações na própria folha de estilos.</span><span class="sxs-lookup"><span data-stu-id="5f808-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="5f808-206">Sincronização automática de CSS</span><span class="sxs-lookup"><span data-stu-id="5f808-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="5f808-207">Este recurso requer a versão 1,3 de Inspetor de Página.</span><span class="sxs-lookup"><span data-stu-id="5f808-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="5f808-208">O recurso de sincronização automática de CSS permite que você edite um arquivo CSS diretamente e veja as alterações imediatamente no navegador Inspetor de Página.</span><span class="sxs-lookup"><span data-stu-id="5f808-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="5f808-209">Clique em **inspecionar** para colocar Inspetor de Página em modo de inspeção.</span><span class="sxs-lookup"><span data-stu-id="5f808-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="5f808-210">No navegador Inspetor de Página, mova o ponteiro do mouse sobre a seção "Home Page" até que o rótulo **div. Content-wrapper** seja exibido.</span><span class="sxs-lookup"><span data-stu-id="5f808-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="5f808-211">Clique em uma vez para selecionar este elemento.</span><span class="sxs-lookup"><span data-stu-id="5f808-211">Click once to select this element.</span></span>

<span data-ttu-id="5f808-212">A janela **estilos** mostra todas as regras de CSS para este elemento.</span><span class="sxs-lookup"><span data-stu-id="5f808-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="5f808-213">Role para baixo até localizar o seletor de classe. em destaque. Content-wrapper.</span><span class="sxs-lookup"><span data-stu-id="5f808-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="5f808-214">Clique em ". em destaque. Content-wrapper".</span><span class="sxs-lookup"><span data-stu-id="5f808-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="5f808-215">Inspetor de Página abre o arquivo CSS que define esse estilo (site. css) e realça o estilo CSS correspondente.</span><span class="sxs-lookup"><span data-stu-id="5f808-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="5f808-216">Agora, altere o valor de `background-color` para "vermelho".</span><span class="sxs-lookup"><span data-stu-id="5f808-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="5f808-217">A alteração aparece imediatamente no navegador Inspetor de Página.</span><span class="sxs-lookup"><span data-stu-id="5f808-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="5f808-218">Usando o seletor de cores CSS</span><span class="sxs-lookup"><span data-stu-id="5f808-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="5f808-219">O editor de CSS no Visual Studio 2012 tem um seletor de cores que torna mais fácil escolher e inserir cores.</span><span class="sxs-lookup"><span data-stu-id="5f808-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="5f808-220">O seletor de cores inclui uma paleta padrão de cores, dá suporte a nomes de cores padrão, códigos de hash, cores RGB, RGBA, HSL e HSLA e mantém uma lista das cores que você usou mais recentemente no documento.</span><span class="sxs-lookup"><span data-stu-id="5f808-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="5f808-221">Na seção anterior, você alterou o valor da propriedade `background-color`.</span><span class="sxs-lookup"><span data-stu-id="5f808-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="5f808-222">Para invocar o seletor de cores, coloque o ponto de inserção após o nome da propriedade e digite **#** ou **RGB (** .</span><span class="sxs-lookup"><span data-stu-id="5f808-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![A barra do seletor de cores CSS](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="5f808-224">Clique em uma cor para selecioná-la ou pressione a tecla seta para baixo e use as teclas de seta para a esquerda e para a direita para percorrer as cores.</span><span class="sxs-lookup"><span data-stu-id="5f808-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="5f808-225">Quando você visita uma cor, o valor hexadecimal correspondente é visualizado:</span><span class="sxs-lookup"><span data-stu-id="5f808-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![plano de fundo-valor da propriedade de cor visualizado](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="5f808-227">Se a barra de cores não tiver a cor exata desejada, você poderá usar o pop-down seletor de cores.</span><span class="sxs-lookup"><span data-stu-id="5f808-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="5f808-228">Para abri-lo, clique na divisa dupla na extremidade direita da barra de cores ou pressione a seta para baixo uma ou duas vezes no teclado.</span><span class="sxs-lookup"><span data-stu-id="5f808-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![Pop-down seletor de cores CSS](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="5f808-230">Clique em uma cor na barra vertical à direita.</span><span class="sxs-lookup"><span data-stu-id="5f808-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="5f808-231">Isso mostra um gradiente para essa cor na janela principal.</span><span class="sxs-lookup"><span data-stu-id="5f808-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="5f808-232">Escolha uma cor diretamente na barra vertical pressionando ENTER ou clique em qualquer ponto na janela principal para escolher com maior precisão.</span><span class="sxs-lookup"><span data-stu-id="5f808-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="5f808-233">Se houver uma cor na tela do computador que você deseja usar (ela não precisa estar dentro da interface do usuário do Visual Studio), você poderá capturar seu valor usando a ferramenta de conta-gotas no canto inferior direito.</span><span class="sxs-lookup"><span data-stu-id="5f808-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="5f808-234">Você também pode alterar a opacidade de uma cor movendo o controle deslizante na parte inferior do seletor de cores.</span><span class="sxs-lookup"><span data-stu-id="5f808-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="5f808-235">Isso altera os valores de cor para os valores RGBA, pois o formato RGBA pode representar a opacidade.</span><span class="sxs-lookup"><span data-stu-id="5f808-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="5f808-236">Depois de escolher uma cor, pressione Enter e, em seguida, digite um ponto e vírgula para concluir a entrada de cor de fundo no arquivo *site. css* .</span><span class="sxs-lookup"><span data-stu-id="5f808-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="5f808-237">A barra de atualização de Inspetor de Página</span><span class="sxs-lookup"><span data-stu-id="5f808-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="5f808-238">Inspetor de Página detecta imediatamente a alteração no arquivo *site. css* e exibe um alerta em uma barra de atualização.</span><span class="sxs-lookup"><span data-stu-id="5f808-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![Barra de atualização](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="5f808-240">Para salvar todos os arquivos e atualizar o navegador Inspetor de Página, pressione Ctrl + Alt + Enter ou clique na barra de atualização.</span><span class="sxs-lookup"><span data-stu-id="5f808-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="5f808-241">A alteração na cor de realce aparece no navegador.</span><span class="sxs-lookup"><span data-stu-id="5f808-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="5f808-242">Mapeando elementos de página dinâmica para JavaScript</span><span class="sxs-lookup"><span data-stu-id="5f808-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="5f808-243">Em aplicativos Web modernos, os elementos na página geralmente são gerados dinamicamente com JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5f808-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="5f808-244">Isso significa que não há marcação estática (HTML ou Razor) que corresponda a esses elementos de página.</span><span class="sxs-lookup"><span data-stu-id="5f808-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="5f808-245">Com a versão 1,3, agora Inspetor de Página pode mapear itens que foram adicionados dinamicamente à página de volta para o código JavaScript correspondente.</span><span class="sxs-lookup"><span data-stu-id="5f808-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="5f808-246">Para demonstrar esse recurso, usaremos o [modelo Spa (aplicativo de página única)](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span><span class="sxs-lookup"><span data-stu-id="5f808-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5f808-247">O modelo SPA requer a atualização [ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650) .</span><span class="sxs-lookup"><span data-stu-id="5f808-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="5f808-248">No Visual Studio, escolha **arquivo** &gt; **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="5f808-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="5f808-249">À esquerda, expanda **Visual C#** , selecione **Web**e, em seguida, selecione **ASP.net MVC4 aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="5f808-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="5f808-250">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f808-250">Click **OK**.</span></span>

<span data-ttu-id="5f808-251">Na caixa de diálogo **novo projeto ASP.NET MVC 4** , selecione **aplicativo de página única**.</span><span class="sxs-lookup"><span data-stu-id="5f808-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="5f808-252">Em Gerenciador de Soluções, expanda a pasta **exibições** e a pasta **base** .</span><span class="sxs-lookup"><span data-stu-id="5f808-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="5f808-253">Clique com o botão direito do mouse no arquivo index. cshtml e escolha **Exibir no Inspetor de página**.</span><span class="sxs-lookup"><span data-stu-id="5f808-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="5f808-254">A primeira coisa que é exibida no navegador de Inspetor de Página é uma página de logon.</span><span class="sxs-lookup"><span data-stu-id="5f808-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="5f808-255">Clique em "inscrever-se" e crie um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="5f808-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="5f808-256">Depois de se inscrever, o aplicativo o conecta e cria uma lista de tarefas pendentes com alguns itens de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5f808-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="5f808-257">Clique em **inspecionar** para colocar Inspetor de Página em modo de inspeção.</span><span class="sxs-lookup"><span data-stu-id="5f808-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="5f808-258">No navegador Inspetor de Página, clique em um dos itens de tarefas.</span><span class="sxs-lookup"><span data-stu-id="5f808-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="5f808-259">Observe que, em vez de ser realçado em azul, o elemento é realçado em laranja, com "JS" ao lado do nome do elemento.</span><span class="sxs-lookup"><span data-stu-id="5f808-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="5f808-260">Isso indica que o elemento foi criado dinamicamente por meio de script.</span><span class="sxs-lookup"><span data-stu-id="5f808-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="5f808-261">Além disso, um sublinhado laranja aparece na guia **pilha de chamadas** . Isso indica que o painel **pilha de chamadas** tem mais informações sobre o elemento.</span><span class="sxs-lookup"><span data-stu-id="5f808-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="5f808-262">Clique na guia **pilha de chamadas** . O painel **pilha de chamadas** mostra a pilha de chamadas para a chamada JavaScript que criou o elemento.</span><span class="sxs-lookup"><span data-stu-id="5f808-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="5f808-263">Chamadas para bibliotecas externas, como jQuery, são recolhidas, para que você possa ver facilmente as chamadas para o script do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5f808-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="5f808-264">Para ver a pilha completa, incluindo chamadas para bibliotecas externas, você pode expandir os nós rotulados como "bibliotecas externas":</span><span class="sxs-lookup"><span data-stu-id="5f808-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="5f808-265">Se você clicar em um item na pilha de chamadas, o Visual Studio abrirá o arquivo de código e destacará o script correspondente.</span><span class="sxs-lookup"><span data-stu-id="5f808-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="5f808-266">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="5f808-266">See Also</span></span>

<span data-ttu-id="5f808-267">[Introdução ao ASP.NET MVC 4 com o Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (site do ASP.net)</span><span class="sxs-lookup"><span data-stu-id="5f808-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="5f808-268">[Introdução ao inspetor de página](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (vídeo do Channel 9)</span><span class="sxs-lookup"><span data-stu-id="5f808-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="5f808-269">[Inspetor de página mensagens de erro](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="5f808-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
