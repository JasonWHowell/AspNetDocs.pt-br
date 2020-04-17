---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Criar um Novo Projeto ASP.NET MVC | Microsoft Docs
author: rick-anderson
description: O passo 1 mostra como colocar a estrutura básica do aplicativo NerdDinner no lugar.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541475"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="d1ca6-103">Criar um novo projeto do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="d1ca6-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="d1ca6-104">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d1ca6-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d1ca6-105">Baixar PDF</span><span class="sxs-lookup"><span data-stu-id="d1ca6-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="d1ca6-106">Este é o passo 1 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="d1ca6-107">O passo 1 mostra como colocar a estrutura básica do aplicativo NerdDinner no lugar.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="d1ca6-108">Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="d1ca6-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="d1ca6-109">NerdDinner Passo 1:&gt;Arquivo- Novo Projeto</span><span class="sxs-lookup"><span data-stu-id="d1ca6-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="d1ca6-110">Começaremos nosso aplicativo NerdDinner selecionando o item do menu **File-&gt;New Project** dentro do Visual Studio 2008 ou do Visual Web Developer 2008 Express gratuito.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="d1ca6-111">Isso trará à tona o diálogo "Novo Projeto".</span><span class="sxs-lookup"><span data-stu-id="d1ca6-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="d1ca6-112">Para criar um novo aplicativo mvc ASP.NET, selecionaremos o nó "Web" no lado esquerdo da caixa de diálogo e, em seguida, escolheremos o modelo de projeto "ASP.NET MVC Web Application" à direita:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="d1ca6-113">*Importante: Certifique-se de que você baixou e instalou ASP.NET MVC - caso contrário, ele não aparecerá na caixa de diálogo Do Novo Projeto. Você pode usar o V2 do [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) se ainda não o tiver instalado&gt;(ASP.NET MVC está disponível na seção "Plataforma web- Frameworks e Runtimes").*</span><span class="sxs-lookup"><span data-stu-id="d1ca6-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="d1ca6-114">Vamos nomear o novo projeto que vamos criar "NerdDinner" e, em seguida, clique no botão "ok" para criá-lo.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="d1ca6-115">Quando clicarmos em "ok" o Visual Studio trará uma caixa de diálogo adicional que nos leva a criar opcionalmente um projeto de teste de unidade para o novo aplicativo também.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="d1ca6-116">Este projeto de teste unitário nos permite criar testes automatizados que verifiquem a funcionalidade e o comportamento do nosso aplicativo (algo que abordaremos como fazer mais tarde neste tutorial).</span><span class="sxs-lookup"><span data-stu-id="d1ca6-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="d1ca6-117">A lista suspensa "Test framework" na caixa de diálogo acima está preenchida com todos os modelos de projeto de teste de unidade ASP.NET mVC disponíveis instalados na máquina.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="d1ca6-118">As versões podem ser baixadas para NUnit, MBUnit e XUnit.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="d1ca6-119">A estrutura de teste da unidade visual incorporada também é suportada.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="d1ca6-120">*Nota: O Visual Studio Unit Test Framework só está disponível com versões profissionais e superiores do Visual Studio 2008. Se você estiver usando vs 2008 Standard Edition ou Visual Web Developer 2008 Express, você precisará baixar e instalar as extensões NUnit, MBUnit ou XUnit para ASP.NET MVC para que esta caixa de diálogo seja mostrada. A caixa de diálogo não será exibida se não houver nenhuma estrutura de teste instalada.*</span><span class="sxs-lookup"><span data-stu-id="d1ca6-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="d1ca6-121">Usaremos o nome padrão "NerdDinner.Tests" para o projeto de teste que criamos e usaremos a opção de framework "Visual Studio Unit Test".</span><span class="sxs-lookup"><span data-stu-id="d1ca6-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="d1ca6-122">Quando clicarmos no botão "ok" o Visual Studio criará uma solução para nós com dois projetos nele - um para nossa aplicação web e outro para nossos testes unitários:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="d1ca6-123">Examinando a estrutura do diretório NerdDinner</span><span class="sxs-lookup"><span data-stu-id="d1ca6-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="d1ca6-124">Quando você cria um novo aplicativo mvc ASP.NET com o Visual Studio, ele adiciona automaticamente uma série de arquivos e diretórios ao projeto:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="d1ca6-125">ASP.NET projetos de MVC por padrão têm seis diretórios de nível superior:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="d1ca6-126">**Diretório**</span><span class="sxs-lookup"><span data-stu-id="d1ca6-126">**Directory**</span></span> | <span data-ttu-id="d1ca6-127">**Finalidade**</span><span class="sxs-lookup"><span data-stu-id="d1ca6-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="d1ca6-128">**/Controladores**</span><span class="sxs-lookup"><span data-stu-id="d1ca6-128">**/Controllers**</span></span> | <span data-ttu-id="d1ca6-129">Onde você coloca classes de controlador que lidam com solicitações de URL</span><span class="sxs-lookup"><span data-stu-id="d1ca6-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="d1ca6-130">**/Modelos**</span><span class="sxs-lookup"><span data-stu-id="d1ca6-130">**/Models**</span></span> | <span data-ttu-id="d1ca6-131">Onde você coloca classes que representam e manipulam dados</span><span class="sxs-lookup"><span data-stu-id="d1ca6-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="d1ca6-132">**/Visualizações**</span><span class="sxs-lookup"><span data-stu-id="d1ca6-132">**/Views**</span></span> | <span data-ttu-id="d1ca6-133">Onde você coloca arquivos de modelo de UI que são responsáveis pela renderização de saída</span><span class="sxs-lookup"><span data-stu-id="d1ca6-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="d1ca6-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="d1ca6-134">**/Scripts**</span></span> | <span data-ttu-id="d1ca6-135">Onde você coloca arquivos e scripts da biblioteca JavaScript (.js)</span><span class="sxs-lookup"><span data-stu-id="d1ca6-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="d1ca6-136">**/Conteúdo**</span><span class="sxs-lookup"><span data-stu-id="d1ca6-136">**/Content**</span></span> | <span data-ttu-id="d1ca6-137">Onde você coloca CSS e arquivos de imagem, e outros conteúdos não dinâmicos/não-JavaScript</span><span class="sxs-lookup"><span data-stu-id="d1ca6-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="d1ca6-138">**/Dados\_do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="d1ca6-138">**/App\_Data**</span></span> | <span data-ttu-id="d1ca6-139">Onde você armazena arquivos de dados que deseja ler/gravar.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="d1ca6-140">ASP.NET MVC não requer essa estrutura.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="d1ca6-141">Na verdade, os desenvolvedores que trabalham em grandes aplicativos normalmente particionam o aplicativo em vários projetos para torná-lo mais gerenciável (por exemplo: classes de modelos de dados geralmente vão em um projeto de biblioteca de classes separado do aplicativo web).</span><span class="sxs-lookup"><span data-stu-id="d1ca6-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="d1ca6-142">A estrutura padrão do projeto, no entanto, fornece uma agradável convenção de diretório padrão que podemos usar para manter nossas preocupações de aplicativos limpas.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="d1ca6-143">Quando expandimos o diretório /Controladores, descobriremos que o Visual Studio adicionou duas classes de controlador – HomeController e AccountController – por padrão ao projeto:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="d1ca6-144">Quando expandimos o diretório /Views, encontraremos três subdiretórios – /Home, /Account e /Shared – bem como vários arquivos de modelo dentro deles também foram adicionados ao projeto por padrão:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="d1ca6-145">Quando expandimos os diretórios /Conteúdo e /Scripts, encontraremos um arquivo Site.css que é usado para estilizar todos os HTML no site, bem como bibliotecas JavaScript que podem habilitar ASP.NET suporte a AJAX e jQuery dentro do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="d1ca6-146">Quando expandimos o projeto NerdDinner.Tests, encontraremos duas classes que contêm testes unitários para nossas classes de controlador:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="d1ca6-147">Esses arquivos padrão adicionados pelo Visual Studio nos fornecem uma estrutura básica para um aplicativo de trabalho - completa com página inicial, sobre página, páginas de login/logout/registro da conta e uma página de erro não manipulada (tudo conectado e funcionando fora da caixa).</span><span class="sxs-lookup"><span data-stu-id="d1ca6-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="d1ca6-148">Executando o aplicativo NerdDinner</span><span class="sxs-lookup"><span data-stu-id="d1ca6-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="d1ca6-149">Podemos executar o projeto escolhendo os itens do **menu Debug-Start&gt;** ou **&gt;Debug- Start sem depuração** de itens do menu:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="d1ca6-150">Isso iniciará o servidor web integrado ASP.NET que vem com o Visual Studio e executará nosso aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="d1ca6-151">Abaixo está a página inicial do nosso novo projeto (URL: "/") quando ele é executado:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="d1ca6-152">Clicar na guia "Sobre" exibe uma página sobre (URL: "/Home/About"):</span><span class="sxs-lookup"><span data-stu-id="d1ca6-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="d1ca6-153">Clicar no link "Fazer logon" no canto superior direito nos leva a uma página de login (URL: "/Account/LogOn")</span><span class="sxs-lookup"><span data-stu-id="d1ca6-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="d1ca6-154">Se não tivermos uma conta de login, podemos clicar no link de registro (URL: "/Account/Register") para criar um:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="d1ca6-155">O código para implementar a funcionalidade de home, about e logout/register foi adicionado por padrão quando criamos nosso novo projeto.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="d1ca6-156">Vamos usá-lo como ponto de partida da nossa aplicação.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="d1ca6-157">Testando o aplicativo NerdDinner</span><span class="sxs-lookup"><span data-stu-id="d1ca6-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="d1ca6-158">Se estivermos usando a Edição Profissional ou a versão superior do Visual Studio 2008, podemos usar o suporte de teste de unidade incorporada do IDE dentro do Visual Studio para testar o projeto:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="d1ca6-159">A escolha de uma das opções acima abrirá o painel "Resultados de Teste" dentro do IDE e nos fornecerá status de aprovação/falha nos testes de 27 unidades incluídos em nosso novo projeto que abrangem a funcionalidade incorporada:</span><span class="sxs-lookup"><span data-stu-id="d1ca6-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="d1ca6-160">Mais tarde, neste tutorial, falaremos mais sobre testes automatizados e adicionaremos testes adicionais de unidade que cobrem a funcionalidade do aplicativo que implementamos.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="d1ca6-161">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="d1ca6-161">Next Step</span></span>

<span data-ttu-id="d1ca6-162">Agora temos uma estrutura básica de aplicação.</span><span class="sxs-lookup"><span data-stu-id="d1ca6-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="d1ca6-163">Vamos agora criar um banco de [dados para armazenar nossos dados de aplicativos.](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="d1ca6-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d1ca6-164">[Próximo](introducing-the-nerddinner-tutorial.md)
> [anterior](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="d1ca6-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
