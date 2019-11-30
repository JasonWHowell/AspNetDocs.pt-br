---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: Introdução com o ASP.NET 4,7 Web Forms e o Visual Studio 2017 | Microsoft Docs
author: Erikre
description: Esta série de tutoriais passo a passo ensinará as noções básicas da criação de um aplicativo ASP.NET Web Forms usando o ASP.NET 4,7 e o Microsoft Visual Studio
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615462"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="91947-103">Introdução com o ASP.NET 4,5 Web Forms e o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="91947-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>

<span data-ttu-id="91947-104">[Baixar o projeto de exemplo WingtipC#Toys ()](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) ou [baixar o livro eletrônico (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="91947-104">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="91947-105">Esta série de tutoriais mostra como criar um aplicativo ASP.NET Web Forms com o ASP.NET 4,5 e o Microsoft Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="91947-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="91947-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="91947-106">Introduction</span></span>

<span data-ttu-id="91947-107">Esta série de tutoriais orienta você pela criação de um aplicativo ASP.NET Web Forms usando o Visual Studio 2017 e o ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="91947-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="91947-108">Você criará um aplicativo chamado **Wingtip Toys** – um site de vitrine simplificado vendendo itens online.</span><span class="sxs-lookup"><span data-stu-id="91947-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="91947-109">Durante a série, novos recursos do ASP.NET 4,5 são realçados.</span><span class="sxs-lookup"><span data-stu-id="91947-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="91947-110">Público-alvo</span><span class="sxs-lookup"><span data-stu-id="91947-110">Target audience</span></span>

<span data-ttu-id="91947-111">Os desenvolvedores novos no ASP.NET Web Forms são o público-alvo desta série de tutoriais.</span><span class="sxs-lookup"><span data-stu-id="91947-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="91947-112">Você deve ter algum conhecimento nas seguintes áreas:</span><span class="sxs-lookup"><span data-stu-id="91947-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="91947-113">Programação orientada a objeto (OOP) e linguagens</span><span class="sxs-lookup"><span data-stu-id="91947-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="91947-114">Desenvolvimento para a Web (HTML, CSS, JavaScript)</span><span class="sxs-lookup"><span data-stu-id="91947-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="91947-115">Bancos de dados relacionais</span><span class="sxs-lookup"><span data-stu-id="91947-115">Relational databases</span></span>
- <span data-ttu-id="91947-116">Arquitetura de N camadas</span><span class="sxs-lookup"><span data-stu-id="91947-116">N-tier architecture</span></span>

<span data-ttu-id="91947-117">Para examinar essas áreas, considere estudar o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="91947-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="91947-118">Introdução com VisualC#</span><span class="sxs-lookup"><span data-stu-id="91947-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="91947-119">[Desenvolvimento](https://msdn.microsoft.com/beginner/bb308760.aspx)para a Web, [HTML, CSS, JavaScript, SQL, PHP, jQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="91947-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="91947-120">Banco de dados relacional</span><span class="sxs-lookup"><span data-stu-id="91947-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="91947-121">Arquitetura de várias camadas</span><span class="sxs-lookup"><span data-stu-id="91947-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="91947-122">Recursos do aplicativo</span><span class="sxs-lookup"><span data-stu-id="91947-122">Application features</span></span>

<span data-ttu-id="91947-123">Os recursos de formulário da Web do ASP.NET apresentados nesta série incluem:</span><span class="sxs-lookup"><span data-stu-id="91947-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="91947-124">O projeto de aplicativo Web (não o projeto de site da Web)</span><span class="sxs-lookup"><span data-stu-id="91947-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="91947-125">Web Forms</span><span class="sxs-lookup"><span data-stu-id="91947-125">Web Forms</span></span>
- <span data-ttu-id="91947-126">Páginas mestras, configuração</span><span class="sxs-lookup"><span data-stu-id="91947-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="91947-127">Inicialização</span><span class="sxs-lookup"><span data-stu-id="91947-127">Bootstrap</span></span>
- <span data-ttu-id="91947-128">Entity Framework Code First, LocalDB</span><span class="sxs-lookup"><span data-stu-id="91947-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="91947-129">Validação de solicitação</span><span class="sxs-lookup"><span data-stu-id="91947-129">Request Validation</span></span>
- <span data-ttu-id="91947-130">Controles de dados fortemente tipados</span><span class="sxs-lookup"><span data-stu-id="91947-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="91947-131">Model binding</span><span class="sxs-lookup"><span data-stu-id="91947-131">Model Binding</span></span>
- <span data-ttu-id="91947-132">Anotações de dados</span><span class="sxs-lookup"><span data-stu-id="91947-132">Data Annotations</span></span>
- <span data-ttu-id="91947-133">Provedores de valor</span><span class="sxs-lookup"><span data-stu-id="91947-133">Value Providers</span></span>
- <span data-ttu-id="91947-134">SSL e OAuth</span><span class="sxs-lookup"><span data-stu-id="91947-134">SSL and OAuth</span></span>
- <span data-ttu-id="91947-135">ASP.NET Identity, configuração e autorização</span><span class="sxs-lookup"><span data-stu-id="91947-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="91947-136">Validação não invasiva</span><span class="sxs-lookup"><span data-stu-id="91947-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="91947-137">Roteamento</span><span class="sxs-lookup"><span data-stu-id="91947-137">Routing</span></span>
- <span data-ttu-id="91947-138">Tratamento de erro do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="91947-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="91947-139">Cenários e tarefas de aplicativos</span><span class="sxs-lookup"><span data-stu-id="91947-139">Application scenarios and tasks</span></span>

<span data-ttu-id="91947-140">As tarefas da série de tutoriais incluem:</span><span class="sxs-lookup"><span data-stu-id="91947-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="91947-141">Criando, revisando e executando um novo projeto</span><span class="sxs-lookup"><span data-stu-id="91947-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="91947-142">Criando uma estrutura de banco de dados</span><span class="sxs-lookup"><span data-stu-id="91947-142">Creating a database structure</span></span>
- <span data-ttu-id="91947-143">Inicializando e propagando um banco de dados</span><span class="sxs-lookup"><span data-stu-id="91947-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="91947-144">Personalizando a interface do usuário com estilos, elementos gráficos e uma página mestra</span><span class="sxs-lookup"><span data-stu-id="91947-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="91947-145">Adicionando páginas e navegação</span><span class="sxs-lookup"><span data-stu-id="91947-145">Adding pages and navigation</span></span>
- <span data-ttu-id="91947-146">Exibindo detalhes do menu e dados do produto</span><span class="sxs-lookup"><span data-stu-id="91947-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="91947-147">Criando um carrinho de compras</span><span class="sxs-lookup"><span data-stu-id="91947-147">Creating a shopping cart</span></span>
- <span data-ttu-id="91947-148">Adicionando suporte a SSL e OAuth</span><span class="sxs-lookup"><span data-stu-id="91947-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="91947-149">Adicionando um método de pagamento</span><span class="sxs-lookup"><span data-stu-id="91947-149">Adding a payment method</span></span>
- <span data-ttu-id="91947-150">Incluindo uma função de administrador e um usuário para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="91947-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="91947-151">Restringindo o acesso a páginas e pastas específicas</span><span class="sxs-lookup"><span data-stu-id="91947-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="91947-152">Carregando um arquivo para o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="91947-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="91947-153">Implementando validação de entrada</span><span class="sxs-lookup"><span data-stu-id="91947-153">Implementing input validation</span></span>
- <span data-ttu-id="91947-154">Registrando rotas para o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="91947-154">Registering routes for the web application</span></span>
- <span data-ttu-id="91947-155">Implementando o tratamento de erros e o log de erros</span><span class="sxs-lookup"><span data-stu-id="91947-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="91947-156">{1&gt;Visão Geral&lt;1}</span><span class="sxs-lookup"><span data-stu-id="91947-156">Overview</span></span>

<span data-ttu-id="91947-157">Esta série de tutoriais destina-se a alguém familiarizado com conceitos de programação, mas novidade no ASP.NET Web Forms.</span><span class="sxs-lookup"><span data-stu-id="91947-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="91947-158">Se você já estiver familiarizado com o ASP.NET Web Forms, esta série ainda poderá ajudá-lo a aprender sobre os novos recursos do ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="91947-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="91947-159">Para leitores que não conhecem os conceitos de programação e Web Forms ASP.NET, consulte os tutoriais de Web Forms adicionais fornecidos na seção [introdução](../../../index.md) no site do ASP.net.</span><span class="sxs-lookup"><span data-stu-id="91947-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="91947-160">O ASP.NET 4,5 fornecido nesta série de tutoriais inclui os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="91947-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="91947-161">Uma interface do usuário simples para a criação de projetos que oferece [suporte para muitas estruturas ASP.net](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC e API da Web).</span><span class="sxs-lookup"><span data-stu-id="91947-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="91947-162">[Inicialização](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), layout, temas e estrutura de design responsivo.</span><span class="sxs-lookup"><span data-stu-id="91947-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="91947-163">[ASP.net Identity](../../../../identity/index.md), um novo sistema de associação ASP.NET que funciona da mesma em todas as estruturas do ASP.net e funciona com software de hospedagem na Web diferente do IIS.</span><span class="sxs-lookup"><span data-stu-id="91947-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="91947-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="91947-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="91947-165">Uma atualização do Entity Framework permitindo que você:</span><span class="sxs-lookup"><span data-stu-id="91947-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="91947-166">Recuperar e manipular dados como objetos fortemente tipados</span><span class="sxs-lookup"><span data-stu-id="91947-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="91947-167">Acessar dados de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="91947-167">Access data asynchronously</span></span>
  - <span data-ttu-id="91947-168">Tratar falhas de conexão transitórias</span><span class="sxs-lookup"><span data-stu-id="91947-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="91947-169">Instruções SQL de log</span><span class="sxs-lookup"><span data-stu-id="91947-169">Log SQL statements</span></span>

<span data-ttu-id="91947-170">Para obter uma lista completa de recursos do ASP.NET 4,5, consulte [ASP.net and Web Tools para ver Visual Studio 2013 notas de versão](../../../../visual-studio/overview/2013/release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="91947-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="91947-171">O aplicativo de exemplo Wingtip Toys</span><span class="sxs-lookup"><span data-stu-id="91947-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="91947-172">As capturas de tela a seguir são do aplicativo ASP.NET Web Forms que você cria nesta série de tutoriais.</span><span class="sxs-lookup"><span data-stu-id="91947-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="91947-173">Quando você executa o aplicativo no Visual Studio, a seguinte página inicial da Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="91947-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![Wingtip Toys – página padrão](introduction-and-overview/_static/image1.png)

<span data-ttu-id="91947-175">Você pode registrar-se como um novo usuário ou entrar como um usuário existente.</span><span class="sxs-lookup"><span data-stu-id="91947-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="91947-176">A navegação superior tem links para categorias de produtos e seus produtos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="91947-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="91947-177">Se você selecionar **produtos**, todos os produtos disponíveis serão exibidos.</span><span class="sxs-lookup"><span data-stu-id="91947-177">If you select **Products**, all available products are displayed.</span></span> 

![Wingtip Toys-produtos](introduction-and-overview/_static/image2.png)

<span data-ttu-id="91947-179">Se você selecionar um produto específico, os detalhes do produto serão exibidos.</span><span class="sxs-lookup"><span data-stu-id="91947-179">If you select a specific product, product details are displayed.</span></span>

![Wingtip Toys-detalhes do produto](introduction-and-overview/_static/image3.png)

<span data-ttu-id="91947-181">Como usuário, você pode registrar e entrar com Web Forms funcionalidade padrão do modelo.</span><span class="sxs-lookup"><span data-stu-id="91947-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="91947-182">Este tutorial também explica como entrar usando uma conta do Gmail existente.</span><span class="sxs-lookup"><span data-stu-id="91947-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="91947-183">Além disso, você pode entrar como administrador para adicionar e remover produtos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="91947-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys-entrar](introduction-and-overview/_static/image4.png)

<span data-ttu-id="91947-185">Depois de entrar como um usuário, você pode adicionar produtos ao carrinho de compras e fazer checkout com o PayPal.</span><span class="sxs-lookup"><span data-stu-id="91947-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="91947-186">O aplicativo de exemplo foi projetado para funcionar na área restrita do desenvolvedor do PayPal.</span><span class="sxs-lookup"><span data-stu-id="91947-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="91947-187">Não ocorre nenhuma transação real do Money.</span><span class="sxs-lookup"><span data-stu-id="91947-187">No actual money transaction takes place.</span></span>

![Wingtip Toys – carrinho de compras](introduction-and-overview/_static/image5.png)

<span data-ttu-id="91947-189">O PayPal confirma suas informações de conta, de pedido e de pagamento.</span><span class="sxs-lookup"><span data-stu-id="91947-189">PayPal confirms your account, order, and payment information.</span></span>

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="91947-191">Depois de retornar do PayPal, você pode revisar e concluir seu pedido.</span><span class="sxs-lookup"><span data-stu-id="91947-191">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys – revisão do pedido](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="91947-193">{1&gt;{2&gt;Pré-requisitos&lt;2}&lt;1}</span><span class="sxs-lookup"><span data-stu-id="91947-193">Prerequisites</span></span>

<span data-ttu-id="91947-194">Antes de começar, verifique se o seguinte software está instalado no computador:</span><span class="sxs-lookup"><span data-stu-id="91947-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="91947-195">[Microsoft Visual Studio 2017 ou Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="91947-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="91947-196">O .NET Framework é instalado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="91947-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="91947-197">Esta série de tutoriais usa o Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="91947-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="91947-198">Você pode usar ou Microsoft Visual Studio 2017 para concluir esta série de tutoriais.</span><span class="sxs-lookup"><span data-stu-id="91947-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="91947-199">Observe o seguinte sobre o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="91947-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="91947-200">Microsoft Visual Studio 2017 e Microsoft Visual Studio Community 2017 são chamados de *Visual Studio* durante esta série de tutoriais.</span><span class="sxs-lookup"><span data-stu-id="91947-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="91947-201">O Visual Studio 2017 é instalado ao lado de todas as versões mais antigas já instaladas.</span><span class="sxs-lookup"><span data-stu-id="91947-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="91947-202">Os sites criados em versões anteriores podem ser abertos no Visual Studio 2017 e continuam a ser abertos em versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="91947-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="91947-203">Na primeira vez que você iniciou o Visual Studio, supõe-se que você selecionou as configurações de *desenvolvimento da Web* .</span><span class="sxs-lookup"><span data-stu-id="91947-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="91947-204">Para obter mais informações, consulte [como: selecionar configurações de ambiente de desenvolvimento da Web](https://msdn.microsoft.com/library/ff521558.aspx).</span><span class="sxs-lookup"><span data-stu-id="91947-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="91947-205">Depois de instalar os pré-requisitos, você estará pronto para começar a criar o projeto Web apresentado nesta série de tutoriais.</span><span class="sxs-lookup"><span data-stu-id="91947-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="91947-206">Baixar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="91947-206">Download the sample application</span></span>

 <span data-ttu-id="91947-207">Você pode baixar o aplicativo de exemplo completo a qualquer momento no site de exemplos do MSDN:</span><span class="sxs-lookup"><span data-stu-id="91947-207">You can download the completed sample application at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="91947-208">[Introdução com ASP.NET 4,5 Web Forms e Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="91947-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="91947-209">Este download tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="91947-209">This download has the following items:</span></span>

- <span data-ttu-id="91947-210">O aplicativo de exemplo na pasta *WingtipToys*</span><span class="sxs-lookup"><span data-stu-id="91947-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="91947-211">Os recursos usados para criar o aplicativo de exemplo na pasta *WingtipToys-assets* na pasta *WingtipToys*</span><span class="sxs-lookup"><span data-stu-id="91947-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="91947-212">O download é um arquivo *. zip* .</span><span class="sxs-lookup"><span data-stu-id="91947-212">The download is a *.zip* file.</span></span> <span data-ttu-id="91947-213">Para ver o projeto concluído que essa série de tutoriais cria, localize e selecione *C#* a pasta no arquivo. zip.</span><span class="sxs-lookup"><span data-stu-id="91947-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="91947-214">Salve a C# pasta na pasta que você usa para trabalhar com projetos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91947-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="91947-215">Por padrão, a pasta Projects do Visual Studio 2017 é:</span><span class="sxs-lookup"><span data-stu-id="91947-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="91947-216"><strong>C:\Users&#92;</strong>  <strong><em>&lt;nome de usuário&gt;</em></strong> <strong>\source\repos</strong></span><span class="sxs-lookup"><span data-stu-id="91947-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="91947-217">Renomeie a ***C#*** pasta para ***WingtipToys***.</span><span class="sxs-lookup"><span data-stu-id="91947-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="91947-218">Se você já tiver uma pasta chamada *WingtipToys* na pasta Projects, renomeie temporariamente essa pasta existente antes de *C#* renomear a pasta como *WingtipToys*.</span><span class="sxs-lookup"><span data-stu-id="91947-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="91947-219">Para executar o projeto concluído, abra a pasta *WingtipToys* e clique duas vezes no arquivo *WingtipToys. sln* .</span><span class="sxs-lookup"><span data-stu-id="91947-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="91947-220">O Visual Studio 2017 abre o projeto.</span><span class="sxs-lookup"><span data-stu-id="91947-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="91947-221">Em seguida, clique com o botão direito do mouse no arquivo *Default. aspx* em **Gerenciador de soluções** e selecione **Exibir no navegador**.</span><span class="sxs-lookup"><span data-stu-id="91947-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="91947-222">Faça um teste de Web Forms de ASP.NET para examinar o conteúdo</span><span class="sxs-lookup"><span data-stu-id="91947-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="91947-223">Depois de concluir a série de tutoriais, faça um teste para testar seu conhecimento e reforçar os principais conceitos.</span><span class="sxs-lookup"><span data-stu-id="91947-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="91947-224">Cada pergunta fornece uma explicação e links para diretrizes adicionais.</span><span class="sxs-lookup"><span data-stu-id="91947-224">Each question provides an explanation and links to additional guidance.</span></span>

* [<span data-ttu-id="91947-225">Teste de Web Forms de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="91947-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="91947-226">Suporte e comentários do tutorial</span><span class="sxs-lookup"><span data-stu-id="91947-226">Tutorial support and comments</span></span>

<span data-ttu-id="91947-227">Para dúvidas e comentários, use a seção Q e a incluída no [introdução com o ASP.NET 4,5 Web Forms e](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) a página de exemplo Visual Studio 2013C#da Wingtip Toys ().</span><span class="sxs-lookup"><span data-stu-id="91947-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="91947-228">Comentários sobre esta série de tutoriais são bem-vindos.</span><span class="sxs-lookup"><span data-stu-id="91947-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="91947-229">Quando essa série de tutoriais é atualizada, cada esforço é feito para considerar correções ou sugestões de melhorias.</span><span class="sxs-lookup"><span data-stu-id="91947-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="91947-230">Se ocorrer um erro, as mensagens de erro correspondentes poderão ser confusas, sem uma boa explicação sobre como corrigi-lo.</span><span class="sxs-lookup"><span data-stu-id="91947-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="91947-231">Para obter ajuda, você pode verificar os [fóruns do ASP.net](https://forums.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="91947-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="91947-232">Outra boa fonte é a Q e uma seção na [introdução com ASP.NET 4,5 Web Forms e](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) a página de exemplo Visual Studio 2013 daC#Wingtip Toys ().</span><span class="sxs-lookup"><span data-stu-id="91947-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="91947-233">Avançar</span><span class="sxs-lookup"><span data-stu-id="91947-233">Next</span></span>](create-the-project.md)
