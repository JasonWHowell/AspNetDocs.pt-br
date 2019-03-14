---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: Criando páginas de ajuda para API Web ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 04/01/2013
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: c081064a32151a71fc4f3ea407e0c48a1539432a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042523"
---
<a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="11dc7-102">Criando páginas de ajuda para API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="11dc7-102">Creating Help Pages for ASP.NET Web API</span></span>
====================
<span data-ttu-id="11dc7-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="11dc7-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="11dc7-104">Quando você cria uma API da web, muitas vezes é útil criar uma página de Ajuda, para que outros desenvolvedores saibam como chamar sua API.</span><span class="sxs-lookup"><span data-stu-id="11dc7-104">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="11dc7-105">Você pode criar toda a documentação manualmente, mas é melhor usado para gerar automaticamente tanto quanto possível.</span><span class="sxs-lookup"><span data-stu-id="11dc7-105">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span>

<span data-ttu-id="11dc7-106">Para facilitar essa tarefa, a API Web do ASP.NET fornece uma biblioteca em tempo de execução para a geração automática de páginas de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="11dc7-106">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="11dc7-107">Criando páginas de Ajuda da API</span><span class="sxs-lookup"><span data-stu-id="11dc7-107">Creating API Help Pages</span></span>

<span data-ttu-id="11dc7-108">Instale [ASP.NET e Web Tools 2012.2 atualização](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="11dc7-108">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="11dc7-109">Essa atualização integra-se a páginas de ajuda para o modelo de projeto de API da Web.</span><span class="sxs-lookup"><span data-stu-id="11dc7-109">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="11dc7-110">Em seguida, crie um novo projeto ASP.NET MVC 4 e selecione o modelo de projeto de API da Web.</span><span class="sxs-lookup"><span data-stu-id="11dc7-110">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="11dc7-111">O modelo de projeto cria um controlador de API de exemplo chamado `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="11dc7-111">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="11dc7-112">O modelo também cria as páginas de Ajuda da API.</span><span class="sxs-lookup"><span data-stu-id="11dc7-112">The template also creates the API help pages.</span></span> <span data-ttu-id="11dc7-113">Todos os arquivos de código para a página de ajuda são colocados na pasta áreas do projeto.</span><span class="sxs-lookup"><span data-stu-id="11dc7-113">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="11dc7-114">Quando você executa o aplicativo, a página inicial contém um link para a página de Ajuda da API.</span><span class="sxs-lookup"><span data-stu-id="11dc7-114">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="11dc7-115">Na home page, o caminho relativo é /Help.</span><span class="sxs-lookup"><span data-stu-id="11dc7-115">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="11dc7-116">Este link leva você para uma página de resumo da API.</span><span class="sxs-lookup"><span data-stu-id="11dc7-116">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="11dc7-117">A exibição do MVC para essa página é definida em Areas/HelpPage/Views/Help/Index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="11dc7-117">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="11dc7-118">Você pode editar esta página para modificar o layout, introdução, título, estilos e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="11dc7-118">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="11dc7-119">A parte principal da página é uma tabela de APIs, agrupadas pelo controlador.</span><span class="sxs-lookup"><span data-stu-id="11dc7-119">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="11dc7-120">As entradas da tabela são geradas dinamicamente, usando o **IApiExplorer** interface.</span><span class="sxs-lookup"><span data-stu-id="11dc7-120">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="11dc7-121">(Falarei mais sobre essa interface posteriormente.) Se você adicionar um novo controlador de API, a tabela é automaticamente atualizada em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="11dc7-121">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="11dc7-122">A coluna de "API" lista o método HTTP e o URI relativo.</span><span class="sxs-lookup"><span data-stu-id="11dc7-122">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="11dc7-123">A coluna "Descrição" contém a documentação para cada API.</span><span class="sxs-lookup"><span data-stu-id="11dc7-123">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="11dc7-124">Inicialmente, a documentação é apenas o texto de espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="11dc7-124">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="11dc7-125">Na próxima seção, mostrarei como adicionar a documentação de comentários XML.</span><span class="sxs-lookup"><span data-stu-id="11dc7-125">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="11dc7-126">Cada API tem um link para uma página com informações mais detalhadas, incluindo os corpos de solicitação e resposta de exemplo.</span><span class="sxs-lookup"><span data-stu-id="11dc7-126">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="11dc7-127">Adicionar páginas de ajuda para um projeto existente</span><span class="sxs-lookup"><span data-stu-id="11dc7-127">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="11dc7-128">Você pode adicionar páginas de ajuda para um projeto de API da Web existente usando o Gerenciador de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="11dc7-128">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="11dc7-129">Essa opção é útil que começar a partir de um modelo de projeto diferente que o modelo de "API Web".</span><span class="sxs-lookup"><span data-stu-id="11dc7-129">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="11dc7-130">Dos **ferramentas** menu, selecione **Gerenciador de pacotes NuGet**e, em seguida, selecione **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="11dc7-130">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="11dc7-131">No [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) janela, digite um dos seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="11dc7-131">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="11dc7-132">Para um **c#** aplicativo: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="11dc7-132">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="11dc7-133">Para um **Visual Basic** aplicativo: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="11dc7-133">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="11dc7-134">Há dois pacotes, um para c# e outro para o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="11dc7-134">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="11dc7-135">Certifique-se de usar aquele que corresponde ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="11dc7-135">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="11dc7-136">Esse comando instala os assemblies necessários e adiciona as exibições do MVC para as páginas de Ajuda (localizadas na pasta áreas/HelpPage).</span><span class="sxs-lookup"><span data-stu-id="11dc7-136">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="11dc7-137">Você precisará adicionar manualmente um link para a página de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="11dc7-137">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="11dc7-138">O URI é /Help.</span><span class="sxs-lookup"><span data-stu-id="11dc7-138">The URI is /Help.</span></span> <span data-ttu-id="11dc7-139">Para criar um link em um modo de exibição do razor, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="11dc7-139">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="11dc7-140">Além disso, certifique-se registrar áreas.</span><span class="sxs-lookup"><span data-stu-id="11dc7-140">Also, make sure to register areas.</span></span> <span data-ttu-id="11dc7-141">No arquivo global. asax, adicione o seguinte código para o **Application\_iniciar** método, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="11dc7-141">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="11dc7-142">Adicionando documentação da API</span><span class="sxs-lookup"><span data-stu-id="11dc7-142">Adding API Documentation</span></span>

<span data-ttu-id="11dc7-143">Por padrão, a Ajuda páginas têm cadeias de caracteres de espaço reservado para a documentação.</span><span class="sxs-lookup"><span data-stu-id="11dc7-143">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="11dc7-144">Você pode usar [comentários da documentação XML](https://msdn.microsoft.com/library/b2s063f7.aspx) para criar a documentação.</span><span class="sxs-lookup"><span data-stu-id="11dc7-144">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="11dc7-145">Para habilitar esse recurso, abra o arquivo HelpPage/aplicativo/áreas\_Start/HelpPageConfig.cs e remova a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="11dc7-145">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="11dc7-146">Agora habilite a documentação XML.</span><span class="sxs-lookup"><span data-stu-id="11dc7-146">Now enable XML documentation.</span></span> <span data-ttu-id="11dc7-147">No Gerenciador de soluções, clique com botão direito no projeto e selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="11dc7-147">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="11dc7-148">Selecione o **Build** página.</span><span class="sxs-lookup"><span data-stu-id="11dc7-148">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="11dc7-149">Sob **saída**, verifique **arquivo de documentação XML**.</span><span class="sxs-lookup"><span data-stu-id="11dc7-149">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="11dc7-150">Na caixa de edição, digite "aplicativo\_Data/XmlDocument.xml".</span><span class="sxs-lookup"><span data-stu-id="11dc7-150">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="11dc7-151">Em seguida, abra o código para o `ValuesController` controlador da API, que é definido no /Controllers/ValuesControler.cs.</span><span class="sxs-lookup"><span data-stu-id="11dc7-151">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesControler.cs.</span></span> <span data-ttu-id="11dc7-152">Adicione alguns comentários de documentação para os métodos do controlador.</span><span class="sxs-lookup"><span data-stu-id="11dc7-152">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="11dc7-153">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="11dc7-153">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="11dc7-154">Dica: Se você posiciona o cursor na linha acima do método e digite as três barras "/", o Visual Studio insere automaticamente os elementos XML.</span><span class="sxs-lookup"><span data-stu-id="11dc7-154">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="11dc7-155">Em seguida, você pode preencher os espaços em branco.</span><span class="sxs-lookup"><span data-stu-id="11dc7-155">Then you can fill in the blanks.</span></span>


<span data-ttu-id="11dc7-156">Agora, criar e executar o aplicativo novamente e navegue até as páginas de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="11dc7-156">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="11dc7-157">As cadeias de caracteres de documentação devem aparecer na tabela de API.</span><span class="sxs-lookup"><span data-stu-id="11dc7-157">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="11dc7-158">A página de Ajuda lê as cadeias de caracteres do arquivo XML em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="11dc7-158">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="11dc7-159">(Quando você implanta o aplicativo, verifique se implantar o arquivo XML.)</span><span class="sxs-lookup"><span data-stu-id="11dc7-159">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="11dc7-160">Nos bastidores</span><span class="sxs-lookup"><span data-stu-id="11dc7-160">Under the Hood</span></span>

<span data-ttu-id="11dc7-161">As páginas de ajuda são criadas sobre o **ApiExplorer** classe, que é parte da estrutura da API Web.</span><span class="sxs-lookup"><span data-stu-id="11dc7-161">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="11dc7-162">O **ApiExplorer** classe fornece matéria-prima para a criação de uma página de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="11dc7-162">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="11dc7-163">Para cada API **ApiExplorer** contém uma **ApiDescription** que descreve a API.</span><span class="sxs-lookup"><span data-stu-id="11dc7-163">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="11dc7-164">Para essa finalidade, "API" é definida como a combinação de URI relativo e o método HTTP.</span><span class="sxs-lookup"><span data-stu-id="11dc7-164">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="11dc7-165">Por exemplo, aqui estão algumas APIs distintas:</span><span class="sxs-lookup"><span data-stu-id="11dc7-165">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="11dc7-166">OBTER /api/Products</span><span class="sxs-lookup"><span data-stu-id="11dc7-166">GET /api/Products</span></span>
- <span data-ttu-id="11dc7-167">OBTER/API/produtos / {id}</span><span class="sxs-lookup"><span data-stu-id="11dc7-167">GET /api/Products/{id}</span></span>
- <span data-ttu-id="11dc7-168">POSTAR/api/produtos</span><span class="sxs-lookup"><span data-stu-id="11dc7-168">POST /api/Products</span></span>

<span data-ttu-id="11dc7-169">Se uma ação do controlador dá suporte a vários métodos HTTP, o **ApiExplorer** trata cada método como uma API distinta.</span><span class="sxs-lookup"><span data-stu-id="11dc7-169">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="11dc7-170">Para ocultar uma API do **ApiExplorer**, adicione o **ApiExplorerSettings** atributo para a ação e o conjunto *IgnoreApi* como true.</span><span class="sxs-lookup"><span data-stu-id="11dc7-170">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="11dc7-171">Você também pode adicionar esse atributo para o controlador, para excluir o controlador inteiro.</span><span class="sxs-lookup"><span data-stu-id="11dc7-171">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="11dc7-172">A classe ApiExplorer obtém cadeias de caracteres de documentação do **IDocumentationProvider** interface.</span><span class="sxs-lookup"><span data-stu-id="11dc7-172">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="11dc7-173">Como você viu anteriormente, a biblioteca de páginas de Ajuda fornece um **IDocumentationProvider** que obtém a documentação de cadeias de caracteres de documentação XML.</span><span class="sxs-lookup"><span data-stu-id="11dc7-173">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="11dc7-174">O código está localizado em /Areas/HelpPage/XmlDocumentationProvider.cs.</span><span class="sxs-lookup"><span data-stu-id="11dc7-174">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="11dc7-175">Você pode obter documentação de outra origem, escrevendo seus próprios **IDocumentationProvider**.</span><span class="sxs-lookup"><span data-stu-id="11dc7-175">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="11dc7-176">Para fazer a conexão, chame o **SetDocumentationProvider** definido no método de extensão, **HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="11dc7-176">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="11dc7-177">**ApiExplorer** chama automaticamente o **IDocumentationProvider** a interface para obter cadeias de caracteres de documentação para cada API.</span><span class="sxs-lookup"><span data-stu-id="11dc7-177">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="11dc7-178">Ele armazena na **documentação** propriedade da **ApiDescription** e **ApiParameterDescription** objetos.</span><span class="sxs-lookup"><span data-stu-id="11dc7-178">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11dc7-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11dc7-179">Next Steps</span></span>

<span data-ttu-id="11dc7-180">Você não fica limitado às páginas de ajuda mostradas aqui.</span><span class="sxs-lookup"><span data-stu-id="11dc7-180">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="11dc7-181">Na verdade, **ApiExplorer** não está limitado a criar páginas de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="11dc7-181">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="11dc7-182">Yao Huang Lin escreveu que postagens no blog alguns ótimo para ajudá-lo a pensar fora da caixa:</span><span class="sxs-lookup"><span data-stu-id="11dc7-182">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="11dc7-183">Adicionando um cliente de teste simples para a página de Ajuda do ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="11dc7-183">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="11dc7-184">Tornando a página de Ajuda do ASP.NET Web API trabalhar em serviços de hospedagem interna</span><span class="sxs-lookup"><span data-stu-id="11dc7-184">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="11dc7-185">Geração de tempo de design da Ajuda page (ou cliente) para API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="11dc7-185">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="11dc7-186">Personalizações avançadas da página de ajuda</span><span class="sxs-lookup"><span data-stu-id="11dc7-186">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)