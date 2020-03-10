---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Chamando a API Web de um aplicativo Windows Phone 8C#()-ASP.NET 4. x
author: rmcmurray
description: 'Tutorial com código: Crie um aplicativo ASP.NET Web API no ASP.NET 4. x que fornece um catálogo de livros para um aplicativo Windows Phone 8.'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614733"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="53c0d-103">Chamar a API Web em um aplicativo do Windows Phone 8 (C#)</span><span class="sxs-lookup"><span data-stu-id="53c0d-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>

<span data-ttu-id="53c0d-104">por [Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="53c0d-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="53c0d-105">Neste tutorial, você aprenderá a criar um cenário completo de ponta a ponta que consiste em um aplicativo ASP.NET Web API que fornece um catálogo de livros para um aplicativo Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="53c0d-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="53c0d-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="53c0d-106">Overview</span></span>

<span data-ttu-id="53c0d-107">Os serviços RESTful, como ASP.NET Web API simplificam a criação de aplicativos baseados em HTTP para desenvolvedores, abstraindo a arquitetura para aplicativos do lado do servidor e do cliente.</span><span class="sxs-lookup"><span data-stu-id="53c0d-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="53c0d-108">Em vez de criar um protocolo baseado em soquete proprietário para comunicação, os desenvolvedores de API da Web simplesmente precisam publicar os métodos HTTP necessários para seu aplicativo, (por exemplo: GET, POST, PUT, DELETE) e os desenvolvedores de aplicativos cliente só precisam consumir os métodos HTTP que são necessários para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53c0d-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="53c0d-109">Neste tutorial de ponta a ponta, você aprenderá a usar a API Web para criar os seguintes projetos:</span><span class="sxs-lookup"><span data-stu-id="53c0d-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="53c0d-110">Na [primeira parte deste tutorial](#STEP1), você criará um aplicativo ASP.NET Web API que dá suporte a todas as operações CRUD (criar, ler, atualizar e excluir) para gerenciar um catálogo de livros.</span><span class="sxs-lookup"><span data-stu-id="53c0d-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="53c0d-111">Este aplicativo usará o [arquivo XML de exemplo (Books. xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) do MSDN.</span><span class="sxs-lookup"><span data-stu-id="53c0d-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="53c0d-112">Na [segunda parte deste tutorial](#STEP2), você criará um aplicativo interativo Windows Phone 8 que recupera os dados do seu aplicativo de API Web.</span><span class="sxs-lookup"><span data-stu-id="53c0d-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="53c0d-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="53c0d-113">Prerequisites</span></span>

- <span data-ttu-id="53c0d-114">Visual Studio 2013 com o SDK do Windows Phone 8 instalado</span><span class="sxs-lookup"><span data-stu-id="53c0d-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="53c0d-115">Windows 8 ou posterior em um sistema de 64 bits com o Hyper-V instalado</span><span class="sxs-lookup"><span data-stu-id="53c0d-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="53c0d-116">Para obter uma lista de requisitos adicionais, consulte a seção *requisitos do sistema* na página de download do [Windows Phone SDK 8,0](https://www.microsoft.com/download/details.aspx?id=35471) .</span><span class="sxs-lookup"><span data-stu-id="53c0d-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="53c0d-117">Se você pretende testar a conectividade entre os projetos da API Web e do Windows Phone 8 no sistema local, será necessário seguir as instruções no artigo *[conectando o emulador Windows Phone 8 ao aplicativo da API Web em um computador local](https://go.microsoft.com/fwlink/?LinkId=324014)* para configurar seu ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="53c0d-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="53c0d-118">Etapa 1: criando o projeto de livrar-API Web</span><span class="sxs-lookup"><span data-stu-id="53c0d-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="53c0d-119">A primeira etapa deste tutorial de ponta a ponta é criar um projeto de API Web que dê suporte a todas as operações CRUD; Observe que você adicionará o projeto de aplicativo Windows Phone a essa solução na [etapa 2](#STEP2) deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="53c0d-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="53c0d-120">Abra **Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="53c0d-121">Clique em **arquivo**, em **novo**e em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="53c0d-122">Quando a caixa de diálogo **novo projeto** for exibida, expanda **instalado**, depois **modelos**, **Visual C#** e, em seguida, **Web**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="53c0d-123">Clique na imagem para expandir</span><span class="sxs-lookup"><span data-stu-id="53c0d-123">Click image to expand</span></span>                                                                |

4. <span data-ttu-id="53c0d-124">Realce **aplicativo Web ASP.net**, digite **bookstore** para o nome do projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="53c0d-125">Quando a caixa de diálogo **novo projeto ASP.net** for exibida, selecione o modelo **API Web** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="53c0d-126">Clique na imagem para expandir</span><span class="sxs-lookup"><span data-stu-id="53c0d-126">Click image to expand</span></span>                                                                |

6. <span data-ttu-id="53c0d-127">Quando o projeto de API Web for aberto, remova o controlador de exemplo do projeto:</span><span class="sxs-lookup"><span data-stu-id="53c0d-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="53c0d-128">Expanda a pasta **controladores** no Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="53c0d-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="53c0d-129">Clique com o botão direito do mouse no arquivo **ValuesController.cs** e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="53c0d-130">Clique em **OK** quando for solicitado a confirmar a exclusão.</span><span class="sxs-lookup"><span data-stu-id="53c0d-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="53c0d-131">Adicionar um arquivo de dados XML ao projeto da API Web; Esse arquivo contém o conteúdo do catálogo da livraria:</span><span class="sxs-lookup"><span data-stu-id="53c0d-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="53c0d-132">Clique com o botão direito do mouse na pasta **\_dados do aplicativo** no Gerenciador de soluções, clique em **Adicionar**e em **novo item**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="53c0d-133">Quando a caixa de diálogo **Adicionar novo item** for exibida, realce o modelo de **arquivo XML** .</span><span class="sxs-lookup"><span data-stu-id="53c0d-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="53c0d-134">Nomeie o arquivo **Books. xml**e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="53c0d-135">Quando o arquivo **Books. xml** for aberto, substitua o código no arquivo pelo XML do arquivo **Books. xml** de exemplo no MSDN:</span><span class="sxs-lookup"><span data-stu-id="53c0d-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="53c0d-136">Salve e feche o arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="53c0d-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="53c0d-137">Adicione o modelo de livrarte ao projeto de API Web; Esse modelo contém a lógica CRUD (criar, ler, atualizar e excluir) para o aplicativo de livraria:</span><span class="sxs-lookup"><span data-stu-id="53c0d-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="53c0d-138">Clique com o botão direito do mouse na pasta **modelos** no Gerenciador de soluções, clique em **Adicionar**e em **classe**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="53c0d-139">Quando a caixa de diálogo **Adicionar novo item** for exibida, nomeie o arquivo de classe **BookDetails.cs**e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="53c0d-140">Quando o arquivo **BookDetails.cs** for aberto, substitua o código no arquivo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="53c0d-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="53c0d-141">Salve e feche o arquivo **BookDetails.cs** .</span><span class="sxs-lookup"><span data-stu-id="53c0d-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="53c0d-142">Adicione o controlador da livraria ao projeto da API Web:</span><span class="sxs-lookup"><span data-stu-id="53c0d-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="53c0d-143">Clique com o botão direito do mouse na pasta **controladores** no Gerenciador de soluções, clique em **Adicionar**e em **controlador**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="53c0d-144">Quando a caixa de diálogo **Adicionar Scaffold** for exibida, realce **controlador da API Web 2 – vazio**e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="53c0d-145">Quando a caixa de diálogo **Adicionar controlador** for exibida, nomeie o controlador **BooksController**e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="53c0d-146">Quando o arquivo **BooksController.cs** for aberto, substitua o código no arquivo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="53c0d-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="53c0d-147">Salve e feche o arquivo **BooksController.cs** .</span><span class="sxs-lookup"><span data-stu-id="53c0d-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="53c0d-148">Crie o aplicativo de API Web para verificar se há erros.</span><span class="sxs-lookup"><span data-stu-id="53c0d-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="53c0d-149">Etapa 2: adicionando o projeto de catálogo da livraria do Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="53c0d-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="53c0d-150">A próxima etapa desse cenário de ponta a ponta é criar o aplicativo de catálogo para o Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="53c0d-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="53c0d-151">Este aplicativo usará o *Windows Phone modelo de aplicativo vinculado* para a interface do usuário padrão e usará o aplicativo de API Web que você criou na [etapa 1](#STEP1) deste tutorial como a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="53c0d-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="53c0d-152">Clique com o botão direito do mouse na solução de **livraria** no Gerenciador de soluções, clique em **Adicionar**e em **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="53c0d-153">Quando a caixa de diálogo **novo projeto** for exibida, expanda **instalado**, **Visual C#** e, em seguida, **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="53c0d-154">Realce **Windows Phone aplicativo vinculado**, insira **BookCatalog** para o nome e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="53c0d-155">Adicione o pacote NuGet Json.NET ao projeto **BookCatalog** :</span><span class="sxs-lookup"><span data-stu-id="53c0d-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="53c0d-156">Clique com o botão direito do mouse em **referências** para o projeto **BookCatalog** no Gerenciador de soluções e clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="53c0d-157">Quando a caixa de diálogo **gerenciar pacotes NuGet** for exibida, expanda a seção **online** e realce **NuGet.org**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="53c0d-158">Insira **JSON.net** no campo de pesquisa e clique no ícone de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="53c0d-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="53c0d-159">Realce **JSON.net** nos resultados da pesquisa e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="53c0d-160">Quando a instalação for concluída, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="53c0d-161">Adicione o modelo **BookDetails** ao projeto **BookCatalog** ; contém um modelo genérico da classe bookstore:</span><span class="sxs-lookup"><span data-stu-id="53c0d-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="53c0d-162">Clique com o botão direito do mouse no projeto **BookCatalog** no Gerenciador de soluções, clique em **Adicionar**e clique em **nova pasta**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="53c0d-163">Nomeie os novos **modelos**de pasta.</span><span class="sxs-lookup"><span data-stu-id="53c0d-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="53c0d-164">Clique com o botão direito do mouse na pasta **modelos** no Gerenciador de soluções, clique em **Adicionar**e em **classe**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="53c0d-165">Quando a caixa de diálogo **Adicionar novo item** for exibida, nomeie o arquivo de classe **BookDetails.cs**e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53c0d-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="53c0d-166">Quando o arquivo **BookDetails.cs** for aberto, substitua o código no arquivo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="53c0d-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="53c0d-167">Salve e feche o arquivo **BookDetails.cs** .</span><span class="sxs-lookup"><span data-stu-id="53c0d-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="53c0d-168">Atualize a classe **MainViewModel.cs** para incluir a funcionalidade para se comunicar com o aplicativo de API Web da livraria:</span><span class="sxs-lookup"><span data-stu-id="53c0d-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="53c0d-169">Expanda a pasta **ViewModels** no Gerenciador de soluções e clique duas vezes no arquivo **MainViewModel.cs** .</span><span class="sxs-lookup"><span data-stu-id="53c0d-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="53c0d-170">Quando o arquivo **MainViewModel.cs** for aberto, substitua o código no arquivo pelo seguinte; Observe que você precisará atualizar o valor da constante `apiUrl` com a URL real de sua API Web:</span><span class="sxs-lookup"><span data-stu-id="53c0d-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="53c0d-171">Salve e feche o arquivo **MainViewModel.cs** .</span><span class="sxs-lookup"><span data-stu-id="53c0d-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="53c0d-172">Atualize o arquivo **MainPage. XAML** para personalizar o nome do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="53c0d-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="53c0d-173">Clique duas vezes no arquivo **MainPage. XAML** no Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="53c0d-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="53c0d-174">Quando o arquivo **MainPage. XAML** for aberto, localize as seguintes linhas de código:</span><span class="sxs-lookup"><span data-stu-id="53c0d-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="53c0d-175">Substitua essas linhas pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="53c0d-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="53c0d-176">Salve e feche o arquivo **MainPage. XAML** .</span><span class="sxs-lookup"><span data-stu-id="53c0d-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="53c0d-177">Atualize o arquivo **DetailsPage. XAML** para personalizar os itens exibidos:</span><span class="sxs-lookup"><span data-stu-id="53c0d-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="53c0d-178">Clique duas vezes no arquivo **DetailsPage. XAML** no Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="53c0d-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="53c0d-179">Quando o arquivo **DetailsPage. XAML** for aberto, localize as seguintes linhas de código:</span><span class="sxs-lookup"><span data-stu-id="53c0d-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="53c0d-180">Substitua essas linhas pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="53c0d-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="53c0d-181">Salve e feche o arquivo **DetailsPage. XAML** .</span><span class="sxs-lookup"><span data-stu-id="53c0d-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="53c0d-182">Compile o aplicativo Windows Phone para verificar se há erros.</span><span class="sxs-lookup"><span data-stu-id="53c0d-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="53c0d-183">Etapa 3: testando a solução de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="53c0d-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="53c0d-184">Conforme mencionado na seção *pré-requisitos* deste tutorial, quando você estiver testando a conectividade entre os projetos da API Web e do Windows Phone 8 no sistema local, será necessário seguir as instruções no artigo *[conectando o emulador do Windows Phone 8 ao aplicativo da API Web em um computador local](https://go.microsoft.com/fwlink/?LinkId=324014)* para configurar o ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="53c0d-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="53c0d-185">Depois de configurar o ambiente de teste, você precisará definir o aplicativo Windows Phone como o projeto de inicialização.</span><span class="sxs-lookup"><span data-stu-id="53c0d-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="53c0d-186">Para fazer isso, realce o aplicativo **BookCatalog** no Gerenciador de soluções e, em seguida, clique em **definir como projeto de inicialização**:</span><span class="sxs-lookup"><span data-stu-id="53c0d-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="53c0d-187">Clique na imagem para expandir</span><span class="sxs-lookup"><span data-stu-id="53c0d-187">Click image to expand</span></span> |

<span data-ttu-id="53c0d-188">Quando você pressionar F5, o Visual Studio iniciará o emulador Windows Phone, que exibirá um &quot;aguardará&quot; mensagem enquanto os dados do aplicativo são recuperados da API Web:</span><span class="sxs-lookup"><span data-stu-id="53c0d-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="53c0d-189">Clique na imagem para expandir</span><span class="sxs-lookup"><span data-stu-id="53c0d-189">Click image to expand</span></span> |

<span data-ttu-id="53c0d-190">Se tudo for bem-sucedido, você verá o catálogo exibido:</span><span class="sxs-lookup"><span data-stu-id="53c0d-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="53c0d-191">Clique na imagem para expandir</span><span class="sxs-lookup"><span data-stu-id="53c0d-191">Click image to expand</span></span> |

<span data-ttu-id="53c0d-192">Se você tocar em qualquer título de livro, o aplicativo exibirá a descrição do livro:</span><span class="sxs-lookup"><span data-stu-id="53c0d-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="53c0d-193">Clique na imagem para expandir</span><span class="sxs-lookup"><span data-stu-id="53c0d-193">Click image to expand</span></span> |

<span data-ttu-id="53c0d-194">Se o aplicativo não puder se comunicar com sua API Web, uma mensagem de erro será exibida:</span><span class="sxs-lookup"><span data-stu-id="53c0d-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="53c0d-195">Clique na imagem para expandir</span><span class="sxs-lookup"><span data-stu-id="53c0d-195">Click image to expand</span></span> |

<span data-ttu-id="53c0d-196">Se você tocar na mensagem de erro, todos os detalhes adicionais sobre o erro serão exibidos:</span><span class="sxs-lookup"><span data-stu-id="53c0d-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="53c0d-197">Clique na imagem para expandir</span><span class="sxs-lookup"><span data-stu-id="53c0d-197">Click image to expand</span></span>                                                                 |
