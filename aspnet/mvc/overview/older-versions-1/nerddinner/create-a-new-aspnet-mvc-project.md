---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Criar um novo projeto MVC do ASP.NET | Microsoft Docs
author: microsoft
description: A etapa 1 mostra como colocar a estrutura do aplicativo NerdDinner básica em vigor.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580930"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="e583d-103">Criar um novo projeto do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e583d-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="e583d-104">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e583d-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e583d-105">Baixar PDF</span><span class="sxs-lookup"><span data-stu-id="e583d-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="e583d-106">Esta é a etapa 1 de um [tutorial de aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) gratuito que percorre como criar um aplicativo Web pequeno, mas completo usando o ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="e583d-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="e583d-107">A etapa 1 mostra como colocar a estrutura do aplicativo NerdDinner básica em vigor.</span><span class="sxs-lookup"><span data-stu-id="e583d-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="e583d-108">Se você estiver usando o ASP.NET MVC 3, recomendamos seguir as [introdução com](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) os tutoriais da [loja de música](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 ou MVC.</span><span class="sxs-lookup"><span data-stu-id="e583d-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="e583d-109">NerdDinner etapa 1: arquivo-&gt;novo projeto</span><span class="sxs-lookup"><span data-stu-id="e583d-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="e583d-110">Vamos começar nosso aplicativo NerdDinner selecionando o item de menu **arquivo-&gt;novo projeto** no visual Studio 2008 ou o Visual Web developer 2008 Express gratuito.</span><span class="sxs-lookup"><span data-stu-id="e583d-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="e583d-111">Isso abrirá a caixa de diálogo "novo projeto".</span><span class="sxs-lookup"><span data-stu-id="e583d-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="e583d-112">Para criar um novo aplicativo MVC do ASP.NET, selecionaremos o nó "Web" no lado esquerdo da caixa de diálogo e, em seguida, escolheremos o modelo de projeto "aplicativo Web do ASP.NET MVC" à direita:</span><span class="sxs-lookup"><span data-stu-id="e583d-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="e583d-113">*Importante: Verifique se você baixou e instalou o ASP.NET MVC-caso contrário, ele não aparecerá na caixa de diálogo novo projeto. Você pode usar a v2 do [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) se ainda não o tiver instalado (o ASP.NET MVC está disponível na seção "plataforma Web-&gt;estruturas e tempos de execução").*</span><span class="sxs-lookup"><span data-stu-id="e583d-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="e583d-114">Vamos nomear o novo projeto de que vamos criar "NerdDinner" e clicar no botão "OK" para criá-lo.</span><span class="sxs-lookup"><span data-stu-id="e583d-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="e583d-115">Quando clicamos em "OK", o Visual Studio abrirá uma caixa de diálogo adicional que nos solicitará também criar um projeto de teste de unidade para o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e583d-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="e583d-116">Este projeto de teste de unidade nos permite criar testes automatizados que verificam a funcionalidade e o comportamento do nosso aplicativo (algo que abordaremos como fazer mais tarde neste tutorial).</span><span class="sxs-lookup"><span data-stu-id="e583d-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="e583d-117">O menu suspenso "estrutura de teste" na caixa de diálogo acima é populado com todos os modelos de projeto de teste de unidade MVC ASP.NET disponíveis instalados no computador.</span><span class="sxs-lookup"><span data-stu-id="e583d-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="e583d-118">As versões podem ser baixadas para NUnit, MBUnit e XUnit.</span><span class="sxs-lookup"><span data-stu-id="e583d-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="e583d-119">Também há suporte para a estrutura de teste de unidade do Visual Studio interna.</span><span class="sxs-lookup"><span data-stu-id="e583d-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="e583d-120">*Observação: a estrutura de teste de unidade do Visual Studio só está disponível com o Visual Studio 2008 Professional e versões posteriores. Se estiver usando o VS 2008 Standard Edition ou o Visual Web Developer 2008 Express, você precisará baixar e instalar as extensões NUnit, MBUnit ou XUnit para o ASP.NET MVC para que essa caixa de diálogo seja mostrada. A caixa de diálogo não será exibida se não houver nenhuma estrutura de teste instalada.*</span><span class="sxs-lookup"><span data-stu-id="e583d-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="e583d-121">Usaremos o nome padrão "NerdDinner. Tests" para o projeto de teste que criamos e usamos a opção de estrutura "teste de unidade do Visual Studio".</span><span class="sxs-lookup"><span data-stu-id="e583d-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="e583d-122">Quando clicamos no botão "OK", o Visual Studio criará uma solução para nós com dois projetos em ti, um para nosso aplicativo Web e outro para nossos testes de unidade:</span><span class="sxs-lookup"><span data-stu-id="e583d-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="e583d-123">Examinando a estrutura do diretório NerdDinner</span><span class="sxs-lookup"><span data-stu-id="e583d-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="e583d-124">Quando você cria um novo aplicativo MVC ASP.NET com o Visual Studio, ele adiciona automaticamente vários arquivos e diretórios ao projeto:</span><span class="sxs-lookup"><span data-stu-id="e583d-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="e583d-125">Por padrão, os projetos do ASP.NET MVC têm seis diretórios de nível superior:</span><span class="sxs-lookup"><span data-stu-id="e583d-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="e583d-126">**Diretório**</span><span class="sxs-lookup"><span data-stu-id="e583d-126">**Directory**</span></span> | <span data-ttu-id="e583d-127">**Finalidade**</span><span class="sxs-lookup"><span data-stu-id="e583d-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="e583d-128">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="e583d-128">**/Controllers**</span></span> | <span data-ttu-id="e583d-129">Onde você coloca classes de controlador que manipulam solicitações de URL</span><span class="sxs-lookup"><span data-stu-id="e583d-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="e583d-130">**/Models**</span><span class="sxs-lookup"><span data-stu-id="e583d-130">**/Models**</span></span> | <span data-ttu-id="e583d-131">Onde você coloca classes que representam e manipulam dados</span><span class="sxs-lookup"><span data-stu-id="e583d-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="e583d-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="e583d-132">**/Views**</span></span> | <span data-ttu-id="e583d-133">Onde você coloca os arquivos de modelo da interface do usuário que são responsáveis por processar a saída</span><span class="sxs-lookup"><span data-stu-id="e583d-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="e583d-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="e583d-134">**/Scripts**</span></span> | <span data-ttu-id="e583d-135">Onde você coloca os arquivos e scripts da biblioteca JavaScript (. js)</span><span class="sxs-lookup"><span data-stu-id="e583d-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="e583d-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="e583d-136">**/Content**</span></span> | <span data-ttu-id="e583d-137">Onde você coloca arquivos de CSS e de imagem e outros conteúdos não dinâmicos/não-JavaScript</span><span class="sxs-lookup"><span data-stu-id="e583d-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="e583d-138">**/App dados de\_**</span><span class="sxs-lookup"><span data-stu-id="e583d-138">**/App\_Data**</span></span> | <span data-ttu-id="e583d-139">Onde você armazena os arquivos de dados que deseja ler/gravar.</span><span class="sxs-lookup"><span data-stu-id="e583d-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="e583d-140">O ASP.NET MVC não requer essa estrutura.</span><span class="sxs-lookup"><span data-stu-id="e583d-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="e583d-141">Na verdade, os desenvolvedores que trabalham em aplicativos grandes normalmente particionam o aplicativo em vários projetos para torná-lo mais gerenciável (por exemplo: classes de modelo de dados geralmente vão em um projeto de biblioteca de classes separado do aplicativo Web).</span><span class="sxs-lookup"><span data-stu-id="e583d-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="e583d-142">A estrutura de projeto padrão, no entanto, fornece uma boa Convenção de diretório padrão que podemos usar para manter as preocupações de nosso aplicativo limpas.</span><span class="sxs-lookup"><span data-stu-id="e583d-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="e583d-143">Quando expandirmos o diretório/Controllers, descobriremos que o Visual Studio adicionou duas classes Controller – HomeController e AccountController – por padrão ao projeto:</span><span class="sxs-lookup"><span data-stu-id="e583d-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="e583d-144">Quando expandirmos o diretório/views, localizaremos três subdiretórios –/Home,/Account e/Shared – assim como vários arquivos de modelo dentro deles também foram adicionados ao projeto por padrão:</span><span class="sxs-lookup"><span data-stu-id="e583d-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="e583d-145">Quando expandirmos os diretórios/Content e/scripts, encontrarei um arquivo site. CSS que é usado para estilizar todo o HTML no site, bem como bibliotecas JavaScript que podem habilitar o suporte a AJAX e jQuery no aplicativo:</span><span class="sxs-lookup"><span data-stu-id="e583d-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="e583d-146">Quando expandirmos o projeto NerdDinner. Tests, localizaremos duas classes que contêm testes de unidade para nossas classes de controlador:</span><span class="sxs-lookup"><span data-stu-id="e583d-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="e583d-147">Esses arquivos padrão adicionados pelo Visual Studio nos fornecem uma estrutura básica para um aplicativo funcional-completo com home page, páginas sobre página, logon de conta/logout/registro e uma página de erro não tratada (tudo conectado e pronto para uso).</span><span class="sxs-lookup"><span data-stu-id="e583d-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="e583d-148">Executando o aplicativo NerdDinner</span><span class="sxs-lookup"><span data-stu-id="e583d-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="e583d-149">Podemos executar o projeto escolhendo **debug-&gt;iniciar depuração** ou **debug-&gt;iniciar sem Depurar itens de** menu:</span><span class="sxs-lookup"><span data-stu-id="e583d-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="e583d-150">Isso iniciará o servidor Web ASP.NET interno que vem com o Visual Studio e executará nosso aplicativo:</span><span class="sxs-lookup"><span data-stu-id="e583d-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="e583d-151">Abaixo está o home page para nosso novo projeto (URL: "/") quando ele é executado:</span><span class="sxs-lookup"><span data-stu-id="e583d-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="e583d-152">Clicar na guia "sobre" exibe uma página About (URL: "/Home/About"):</span><span class="sxs-lookup"><span data-stu-id="e583d-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="e583d-153">Clicar no link "logon" no canto superior direito nos leva a uma página de logon (URL: "/Account/LogOn")</span><span class="sxs-lookup"><span data-stu-id="e583d-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="e583d-154">Se não tivermos uma conta de logon, poderemos clicar no link de registro (URL: "/Account/Register") para criar uma:</span><span class="sxs-lookup"><span data-stu-id="e583d-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="e583d-155">O código para implementar a funcionalidade de início, sobre e logout/registro acima foi adicionado por padrão quando criamos nosso novo projeto.</span><span class="sxs-lookup"><span data-stu-id="e583d-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="e583d-156">Vamos usá-lo como o ponto de partida de nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e583d-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="e583d-157">Testando o aplicativo NerdDinner</span><span class="sxs-lookup"><span data-stu-id="e583d-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="e583d-158">Se estivermos usando a Professional Edition ou uma versão superior do Visual Studio 2008, podemos usar o suporte de IDE de teste de unidade interno no Visual Studio para testar o projeto:</span><span class="sxs-lookup"><span data-stu-id="e583d-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="e583d-159">A escolha de uma das opções acima abrirá o painel "Resultados de Teste" no IDE e nos fornecerá o status de aprovação/reprovação nos testes de unidade 27 incluídos em nosso novo projeto que abrange a funcionalidade interna:</span><span class="sxs-lookup"><span data-stu-id="e583d-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="e583d-160">Mais adiante neste tutorial, falaremos mais sobre os testes automatizados e adicionaremos outros testes de unidade que abrangem a funcionalidade do aplicativo que implementamos.</span><span class="sxs-lookup"><span data-stu-id="e583d-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="e583d-161">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="e583d-161">Next Step</span></span>

<span data-ttu-id="e583d-162">Agora temos uma estrutura de aplicativo básica em vigor.</span><span class="sxs-lookup"><span data-stu-id="e583d-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="e583d-163">Agora, vamos [criar um banco de dados para armazenar os aplicativos de aplicativo](create-a-database.md).</span><span class="sxs-lookup"><span data-stu-id="e583d-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e583d-164">[Anterior](introducing-the-nerddinner-tutorial.md)
> [Próximo](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="e583d-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
