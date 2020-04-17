---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programação ASP.NET Páginas da Web (Razor) Usando o Visual Studio | Microsoft Docs
author: Rick-Anderson
description: Este apêndice explica como você pode usar o Visual Studio 2010 ou o Visual Web Developer 2010 Express para programar ASP.NET Páginas da Web com a sintaxe Razor.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542892"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="d56c3-103">Programação ASP.NET Páginas da Web (Razor) usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d56c3-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="d56c3-104"> por [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d56c3-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d56c3-105">Este artigo explica como você pode usar o Visual Studio ou visual Web Developer Express para programar ASP.NET sites da Web Pages (Razor).</span><span class="sxs-lookup"><span data-stu-id="d56c3-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="d56c3-106">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="d56c3-106">What you'll learn</span></span>
>
> - <span data-ttu-id="d56c3-107">O que você precisa instalar (se alguma coisa) para trabalhar com ASP.NET Páginas da Web em sua versão do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d56c3-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="d56c3-108">Como adicionar suporte para ASP.NET Páginas da Web ao Visual Web Developer 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="d56c3-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="d56c3-109">Como usar recursos no Visual Studio para trabalhar com páginas ASP.NET Razor, incluindo o IntelliSense e o depurador.</span><span class="sxs-lookup"><span data-stu-id="d56c3-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d56c3-110">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="d56c3-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="d56c3-111">páginas da Web ASP.NET (Navalha) 3</span><span class="sxs-lookup"><span data-stu-id="d56c3-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="d56c3-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d56c3-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="d56c3-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="d56c3-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="d56c3-114">Este tutorial também funciona com ASP.NET Páginas web 2, Visual Studio 2012, Visual Studio 2010 e WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="d56c3-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="d56c3-115">Você pode programar páginas da Web ASP.NET com sintaxe de Navalha usando WebMatrix ou muitos outros editores de código.</span><span class="sxs-lookup"><span data-stu-id="d56c3-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="d56c3-116">Você também pode usar o Microsoft Visual Studio, que é um ambiente de desenvolvimento integrado (IDE) completo que fornece um poderoso conjunto de ferramentas para criar muitos tipos de aplicativos (não apenas sites).</span><span class="sxs-lookup"><span data-stu-id="d56c3-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="d56c3-117">Para trabalhar com páginas ASP.NET Razor, você pode usar [o Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="d56c3-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="d56c3-118">Dois recursos particularmente úteis que o Visual Studio fornece para programação com ASP.NET páginas da Web Razor são:</span><span class="sxs-lookup"><span data-stu-id="d56c3-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="d56c3-119">*IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="d56c3-119">*IntelliSense*.</span></span> <span data-ttu-id="d56c3-120">O recurso IntelliSense incorporado ao Visual Studio é mais abrangente do que o IntelliSense no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="d56c3-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="d56c3-121">*Depurador.*</span><span class="sxs-lookup"><span data-stu-id="d56c3-121">*Debugger*.</span></span> <span data-ttu-id="d56c3-122">O depurador permite que você solucionem seu código interrompendo um programa enquanto ele está em execução, examinando variáveis e passando pela linha de código por linha.</span><span class="sxs-lookup"><span data-stu-id="d56c3-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="d56c3-123">Usando o Visual Studio com diferentes versões de páginas da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d56c3-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="d56c3-124">Para desenvolver ASP.NET aplicativos web no Visual Studio 2017, instale a carga de trabalho **de ASP.NET e desenvolvimento web.**</span><span class="sxs-lookup"><span data-stu-id="d56c3-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="d56c3-125">Visual Studio 2012 e Visual Studio 2013 incluem suporte para páginas da Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d56c3-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="d56c3-126">(Os pacotes necessários para suportar ASP.NET Páginas da Web são instalados quando você instala o Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="d56c3-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="d56c3-127">O Visual Studio 2010 não inclui suporte por padrão para páginas da Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d56c3-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="d56c3-128">Para usar ASP.NET Páginas da Web com o Visual Studio 2010, você deve instalar o pacote mvc ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d56c3-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="d56c3-129">Para obter ASP.NET Páginas da Web 2, você instala ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="d56c3-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="d56c3-130">A tabela a seguir resume o suporte para ASP.NET Páginas da Web em diferentes versões do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d56c3-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="d56c3-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="d56c3-131">Visual Studio 2010</span></span> | <span data-ttu-id="d56c3-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d56c3-132">Visual Studio 2012</span></span> | <span data-ttu-id="d56c3-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d56c3-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d56c3-134">**Páginas da Web do ASP.NET 2**</span><span class="sxs-lookup"><span data-stu-id="d56c3-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="d56c3-135">Instalar ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="d56c3-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="d56c3-136">(Incluído)</span><span class="sxs-lookup"><span data-stu-id="d56c3-136">(Included)</span></span> | <span data-ttu-id="d56c3-137">(Incluído)</span><span class="sxs-lookup"><span data-stu-id="d56c3-137">(Included)</span></span> |
| <span data-ttu-id="d56c3-138">**Páginas da Web do ASP.NET 3**</span><span class="sxs-lookup"><span data-stu-id="d56c3-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="d56c3-139">Atualização para ASP.NET Páginas da Web 3 através do NuGet</span><span class="sxs-lookup"><span data-stu-id="d56c3-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="d56c3-140">(Incluído)</span><span class="sxs-lookup"><span data-stu-id="d56c3-140">(Included)</span></span> |

<span data-ttu-id="d56c3-141">Para trabalhar com o Visual Studio 2010, consulte [Instalando suporte para páginas da Web ASP.NET no Visual Studio 2010](#vs2010support).</span><span class="sxs-lookup"><span data-stu-id="d56c3-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="d56c3-142">Lançando o Visual Studio da WebMatrix</span><span class="sxs-lookup"><span data-stu-id="d56c3-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="d56c3-143">Se você começou um projeto no WebMatrix e deseja mudar para o Visual Studio, o WebMatrix fornece um botão para abrir facilmente o projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d56c3-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="d56c3-144">Você deve ter o Visual Studio instalado no seu computador para que este botão seja ativado.</span><span class="sxs-lookup"><span data-stu-id="d56c3-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="d56c3-145">A imagem a seguir mostra o botão no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="d56c3-145">The following image shows the button in WebMatrix.</span></span>

![lançar Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="d56c3-147">Quando você clica no botão, o projeto é aberto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d56c3-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="d56c3-148">Você pode alternar para frente e para trás entre webmatrix e visual studio sem quaisquer problemas.</span><span class="sxs-lookup"><span data-stu-id="d56c3-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="d56c3-149">Você será notificado se algum arquivo tiver sido alterado no outro ambiente e precisar ser recarregado para obter as últimas alterações.</span><span class="sxs-lookup"><span data-stu-id="d56c3-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="d56c3-150">Criando ASP.NET Razor Site no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d56c3-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="d56c3-151">Para criar um site ASP.NET Razor no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d56c3-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="d56c3-152">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d56c3-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="d56c3-153">No menu **Arquivo,** clique **em Novo site**.</span><span class="sxs-lookup"><span data-stu-id="d56c3-153">In the **File** menu, click **New Web Site**.</span></span>

    ![criar um novo site](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="d56c3-155">Na caixa de diálogo **Novo Site,** selecione o idioma a ser usado (Visual C# ou Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="d56c3-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="d56c3-156">Selecione o modelo **ASP.NET Site (Razor).**</span><span class="sxs-lookup"><span data-stu-id="d56c3-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![local de navalha](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="d56c3-158">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d56c3-158">Click **OK**.</span></span>

<span data-ttu-id="d56c3-159">Seu novo projeto existe e está preenchido com algumas páginas da Web padrão para ajudá-lo a começar.</span><span class="sxs-lookup"><span data-stu-id="d56c3-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="d56c3-160">Usando IntelliSense</span><span class="sxs-lookup"><span data-stu-id="d56c3-160">Using IntelliSense</span></span>

<span data-ttu-id="d56c3-161">Agora que você criou um site, você pode ver como o IntelliSense funciona no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d56c3-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="d56c3-162">No site que você acabou de criar, abra a página *Default.cshtml.*</span><span class="sxs-lookup"><span data-stu-id="d56c3-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="d56c3-163">Após `<h3>` as tags na `@ServerInfo.` página, digite (incluindo o dot).</span><span class="sxs-lookup"><span data-stu-id="d56c3-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="d56c3-164">Observe como o IntelliSense exibe `ServerInfo` os métodos disponíveis para o ajudante em uma lista de baixa.</span><span class="sxs-lookup"><span data-stu-id="d56c3-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="d56c3-166">Selecione `GetHtml` o método na lista e, em seguida, pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="d56c3-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="d56c3-167">O IntelliSense preenche automaticamente o método.</span><span class="sxs-lookup"><span data-stu-id="d56c3-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="d56c3-168">(Como em qualquer método em C#, você deve adicionar `()` caracteres após o método.) O código completo `GetHtml` para o método parece o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="d56c3-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="d56c3-169">Pressione Ctrl+F5 para executar a página.</span><span class="sxs-lookup"><span data-stu-id="d56c3-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="d56c3-170">É assim que a página se parece quando exibida em um navegador:</span><span class="sxs-lookup"><span data-stu-id="d56c3-170">This is what the page looks like when displayed in a browser:</span></span>

    ![página padrão no navegador](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="d56c3-172">Feche o navegador.</span><span class="sxs-lookup"><span data-stu-id="d56c3-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="d56c3-173">Usando o Depurador</span><span class="sxs-lookup"><span data-stu-id="d56c3-173">Using the Debugger</span></span>

1. <span data-ttu-id="d56c3-174">Na parte superior da página *Default.cshtml,* após `Page.Title`a linha que começa com , adicione a seguinte linha de código:</span><span class="sxs-lookup"><span data-stu-id="d56c3-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="d56c3-175">Na margem cinza do editor à esquerda do código, clique ao lado desta nova linha para adicionar um *ponto de ruptura*.</span><span class="sxs-lookup"><span data-stu-id="d56c3-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="d56c3-176">Um ponto de ruptura é um marcador que diz ao depurador para parar de executar o programa nesse ponto para que você possa ver o que está acontecendo.</span><span class="sxs-lookup"><span data-stu-id="d56c3-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![definir ponto de interrupção](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="d56c3-178">Remova a chamada `ServerInfo.GetHtml` para o método e `@myTime` adicione uma chamada à variável em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="d56c3-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="d56c3-179">Esta chamada exibe o valor de tempo atual que é devolvido pela nova linha de código.</span><span class="sxs-lookup"><span data-stu-id="d56c3-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="d56c3-180">Pressione F5 para executar a página no depurador.</span><span class="sxs-lookup"><span data-stu-id="d56c3-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="d56c3-181">A página pára no ponto de partida que você definiu.</span><span class="sxs-lookup"><span data-stu-id="d56c3-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="d56c3-182">A imagem a seguir mostra como a página se parece no editor com o ponto de partida (em amarelo).</span><span class="sxs-lookup"><span data-stu-id="d56c3-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![ponto de ruptura depuração](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="d56c3-184">Na barra de ferramentas Debug, clique no botão **Passo a passo** (ou pressione F11) para executar a próxima linha de código.</span><span class="sxs-lookup"><span data-stu-id="d56c3-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="d56c3-185">Cada vez que você clica neste botão, você avança a execução para a próxima linha de código.</span><span class="sxs-lookup"><span data-stu-id="d56c3-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Passo no botão](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="d56c3-187">Examine o valor `myTime` da variável segurando o ponteiro do mouse sobre ele ou inspecionando os valores **exibidos** nas janelas Locals e **Call Stack.**</span><span class="sxs-lookup"><span data-stu-id="d56c3-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="d56c3-188">Visual Studio exibe o valor da variável.</span><span class="sxs-lookup"><span data-stu-id="d56c3-188">Visual Studio display the value of the variable.</span></span>

    ![mostrar valor do tempo](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="d56c3-190">Quando terminar de examinar a variável e passar pelo código, pressione F5 para continuar executando a página sem parar em cada linha.</span><span class="sxs-lookup"><span data-stu-id="d56c3-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="d56c3-191">Quando você terminar de passar por todo o código, o navegador exibe a página.</span><span class="sxs-lookup"><span data-stu-id="d56c3-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="d56c3-192">Para saber mais sobre o depurador e sobre como depurar código no Visual Studio, consulte [Passo a Passo: Depurando Páginas da Web no Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d56c3-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="d56c3-193">Usando razor em ASP.NET projetos de MVC com Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d56c3-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="d56c3-194">A sintaxe Razor também é usada extensivamente em ASP.NET projetos de MVC.</span><span class="sxs-lookup"><span data-stu-id="d56c3-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="d56c3-195">O MVC é uma maneira poderosa e baseada em padrões de construir sites dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="d56c3-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="d56c3-196">Se o seu site de páginas da ASP.NET se tornar difícil de manter, você pode querer considerar convertê-lo em um aplicativo mvc ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d56c3-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="d56c3-197">Para um exemplo de criação de um aplicativo MVC, consulte [Getting Started com ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d56c3-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="d56c3-198">Instalando suporte para páginas da Web ASP.NET no Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="d56c3-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="d56c3-199">Esta seção mostra como instalar o Visual Web Developer Express 2010 e o ASP.NET Web Pages Tools para o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d56c3-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="d56c3-200">Se você ainda não tiver o Instalador de Plataforma web, baixe-o na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="d56c3-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="d56c3-201">Execute o Instalador de Plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="d56c3-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="d56c3-202">Clique na guia **Produtos.**</span><span class="sxs-lookup"><span data-stu-id="d56c3-202">Click the **Products** tab.</span></span>

    ![Guia Produtos WebPI](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="d56c3-204">Procure **por ASP.NET MVC 4** (para ASP.NET Páginas da Web 2) e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d56c3-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="d56c3-205">Esses produtos incluem ferramentas do Visual Studio para construir sites ASP.NET Razor.</span><span class="sxs-lookup"><span data-stu-id="d56c3-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![Opções de instalação do WebPi](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="d56c3-207">Clique **em Instalar** para concluir a instalação.</span><span class="sxs-lookup"><span data-stu-id="d56c3-207">Click **Install** to complete the installation.</span></span>
