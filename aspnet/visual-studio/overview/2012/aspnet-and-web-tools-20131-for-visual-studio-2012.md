---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Release Notes for ASP.NET and Web Tools 2013.1 para Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: Este documento descreve o lançamento de ASP.NET e Web Tools 2013.1 para o Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543568"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="56273-103">Notas de versão do ASP.NET and Web Tools 2013.1 para Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="56273-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="56273-104">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="56273-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="56273-105">Este documento descreve o lançamento de ASP.NET e Web Tools 2013.1 para o Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="56273-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="56273-106">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="56273-106">Contents</span></span>

- [<span data-ttu-id="56273-107">Notas de instalação</span><span class="sxs-lookup"><span data-stu-id="56273-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="56273-108">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="56273-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="56273-109">Novos recursos em ASP.NET e Web Tools 2013.1 para Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="56273-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="56273-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="56273-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="56273-111">Modelos</span><span class="sxs-lookup"><span data-stu-id="56273-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="56273-112">ASP.NET modelo MVC 5</span><span class="sxs-lookup"><span data-stu-id="56273-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="56273-113">ASP.NET modelo de API 2 da Web</span><span class="sxs-lookup"><span data-stu-id="56273-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="56273-114">Modelos de itens</span><span class="sxs-lookup"><span data-stu-id="56273-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="56273-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="56273-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="56273-116">andaimes de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="56273-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="56273-117">Editor de Navalha</span><span class="sxs-lookup"><span data-stu-id="56273-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="56273-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="56273-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="56273-119">Problemas conhecidos e mudanças de quebra</span><span class="sxs-lookup"><span data-stu-id="56273-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="56273-120">andaimes de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="56273-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="56273-121">Andaimes mvc e Web API - HTTP 404, erro não encontrado</span><span class="sxs-lookup"><span data-stu-id="56273-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="56273-122">Visual Studio Express 2012 para Web pára de funcionar depois de adicionar um item andaime</span><span class="sxs-lookup"><span data-stu-id="56273-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="56273-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="56273-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="56273-124">Visualizar arquivo cshtml com Browse With ou F5 causa um erro no servidor</span><span class="sxs-lookup"><span data-stu-id="56273-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="56273-125">Url Rewrite e Tilde(~)</span><span class="sxs-lookup"><span data-stu-id="56273-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="56273-126">Modelos</span><span class="sxs-lookup"><span data-stu-id="56273-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="56273-127">Notas de instalação</span><span class="sxs-lookup"><span data-stu-id="56273-127">Installation Notes</span></span>

<span data-ttu-id="56273-128">[Instalar](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET e Web Tools 2013.1 para Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="56273-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="56273-129">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="56273-129">Software Requirements</span></span>

<span data-ttu-id="56273-130">Você deve ter o Visual Studio 2012 ou o Visual Studio Express 2012 para web.</span><span class="sxs-lookup"><span data-stu-id="56273-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="56273-131">Novos recursos em ASP.NET e Web Tools 2013.1 para Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="56273-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="56273-132">Inicialização</span><span class="sxs-lookup"><span data-stu-id="56273-132">Bootstrap</span></span>

<span data-ttu-id="56273-133">Quando você andaime controladores e visualizações MVC 5, a marcação para as visualizações usa [Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="56273-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="56273-134">Modelos</span><span class="sxs-lookup"><span data-stu-id="56273-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="56273-135">ASP.NET modelo MVC 5</span><span class="sxs-lookup"><span data-stu-id="56273-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="56273-136">Adicionamos um novo modelo MVC 5.</span><span class="sxs-lookup"><span data-stu-id="56273-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="56273-137">Ele faz referência aos pacotes MVC 5 NuGet mais recentes, e você pode usar andaimes para adicionar controladores e visualizações.</span><span class="sxs-lookup"><span data-stu-id="56273-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="56273-138">ASP.NET modelo de API 2 da Web</span><span class="sxs-lookup"><span data-stu-id="56273-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="56273-139">Adicionamos um novo modelo de API 2 da Web.</span><span class="sxs-lookup"><span data-stu-id="56273-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="56273-140">Ele faz referência aos pacotes NuGet da Web API 2, e você pode usar andaimes para adicionar controladores e visualizações.</span><span class="sxs-lookup"><span data-stu-id="56273-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="56273-141">Modelos de item</span><span class="sxs-lookup"><span data-stu-id="56273-141">Item Templates</span></span>

<span data-ttu-id="56273-142">Adicionamos novos modelos de itens para visualizações MVC 5, Páginas da Web (Razor 3) e controladores de API 2 da Web.</span><span class="sxs-lookup"><span data-stu-id="56273-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="56273-143">Eles instalam os pacotes NuGet relacionados ao projeto enquanto adicionam novos itens.</span><span class="sxs-lookup"><span data-stu-id="56273-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="56273-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="56273-144">Entity Framework 6</span></span>

<span data-ttu-id="56273-145">Quando você andaime um controlador De MVC ou Web API usando Entity Framework, usamos o Framework 6.</span><span class="sxs-lookup"><span data-stu-id="56273-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="56273-146">Para obter mais informações sobre o Entity Framework, consulte o [Histórico de Versões do Quadro de Entidades](https://msdn.com/data/jj574253).</span><span class="sxs-lookup"><span data-stu-id="56273-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="56273-147">Você também pode baixar e instalar o Entity Framework 6 Tools for Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="56273-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="56273-148">Consulte o [Quadro de Entidades Get](https://msdn.com/data/ee712906#tooling).</span><span class="sxs-lookup"><span data-stu-id="56273-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="56273-149">andaimes de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="56273-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="56273-150">ASP.NET Andaimes é uma estrutura de geração de código para aplicações ASP.NET Web.</span><span class="sxs-lookup"><span data-stu-id="56273-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="56273-151">Facilita a adição de código de caldeira ao seu projeto que interage com um modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="56273-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="56273-152">Nas versões anteriores do Visual Studio, os andaimes eram limitados a projetos ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="56273-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="56273-153">Com esta atualização, agora você pode usar andaimes para qualquer projeto ASP.NET, incluindo Formulários da Web.</span><span class="sxs-lookup"><span data-stu-id="56273-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="56273-154">Esta atualização não suporta a geração de páginas para um projeto de Formulários da Web, mas você ainda pode usar andaimes com Formulários web adicionando dependências De MVC ao projeto.</span><span class="sxs-lookup"><span data-stu-id="56273-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="56273-155">O suporte para gerar páginas para Formulários da Web será adicionado em uma atualização futura.</span><span class="sxs-lookup"><span data-stu-id="56273-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="56273-156">Ao usar andaimes, garantimos que todas as dependências necessárias sejam instaladas no projeto.</span><span class="sxs-lookup"><span data-stu-id="56273-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="56273-157">Por exemplo, se você começar com um projeto ASP.NET Web Forms e usar andaimes para adicionar um Controlador de API da Web, os pacotes e referências NuGet necessários serão adicionados ao seu projeto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="56273-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="56273-158">Para adicionar andaimes MVC a um projeto Formulários da Web, adicione um **novo item de andaimes** e selecione **dependências MVC 5** na janela de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56273-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="56273-159">Existem duas opções para andaimes MVC; Mínimo e completo.</span><span class="sxs-lookup"><span data-stu-id="56273-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="56273-160">Se você selecionar Mínimo, apenas os pacotes e referências do NuGet para ASP.NET MVC serão adicionados ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="56273-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="56273-161">Se você selecionar a opção Completa, as dependências mínimas serão adicionadas, bem como os arquivos de conteúdo necessários para um projeto MVC.</span><span class="sxs-lookup"><span data-stu-id="56273-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="56273-162">O suporte para controladores assync de andaimes usa os novos recursos de assync do Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="56273-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="56273-163">Para obter mais informações e tutoriais, consulte ASP.NET Visão [Geral do Andaime](../2013/aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56273-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="56273-164">Esses tutoriais mostram andaimes com o Visual Studio 2013, mas também são aplicáveis ao ASP.NET e Web Tools 2013.1 para o Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="56273-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="56273-165">Editor de Navalha</span><span class="sxs-lookup"><span data-stu-id="56273-165">Razor Editor</span></span>

<span data-ttu-id="56273-166">Com esta atualização, o Visual Studio 2012 agora suporta ferramentas/edição do Razor 3.</span><span class="sxs-lookup"><span data-stu-id="56273-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="56273-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="56273-167">NuGet 2.7</span></span>

<span data-ttu-id="56273-168">O NuGet 2.7 inclui um rico conjunto de novos recursos que são descritos em detalhes no [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="56273-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="56273-169">Esta versão do NuGet remove a necessidade de os usuários permitirem explicitamente que o NuGet restaure pacotes perdidos.</span><span class="sxs-lookup"><span data-stu-id="56273-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="56273-170">Ao instalar o NuGet 2.7, os usuários concordam implicitamente em restaurar automaticamente os pacotes perdidos.</span><span class="sxs-lookup"><span data-stu-id="56273-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="56273-171">Os usuários podem explicitamente desativar a restauração do pacote através das configurações do NuGet no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="56273-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="56273-172">Essa mudança simplifica como funciona a restauração do pacote.</span><span class="sxs-lookup"><span data-stu-id="56273-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="56273-173">Problemas conhecidos e mudanças de quebra</span><span class="sxs-lookup"><span data-stu-id="56273-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="56273-174">andaimes de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="56273-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="56273-175">Andaimes mvc e Web API - HTTP 404, erro não encontrado</span><span class="sxs-lookup"><span data-stu-id="56273-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="56273-176">Se você encontrar um erro ao adicionar um item andaime a um projeto, é possível que seu projeto seja deixado em um estado inconsistente.</span><span class="sxs-lookup"><span data-stu-id="56273-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="56273-177">Algumas das mudanças feitas serão feitas em andaimes, mas outras alterações, como os pacotes NuGet instalados, não serão revertidas.</span><span class="sxs-lookup"><span data-stu-id="56273-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="56273-178">Se as alterações de configuração de roteamento forem revertidas, os usuários receberão um erro HTTP 404 ao navegar em itens de andaime.</span><span class="sxs-lookup"><span data-stu-id="56273-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="56273-179">Para corrigir esse erro para MVC, adicione um novo item andaime e selecione Dependências MVC 5 (mínima ou completa).</span><span class="sxs-lookup"><span data-stu-id="56273-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="56273-180">Este processo adicionará todas as alterações necessárias ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="56273-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="56273-181">Para corrigir esse erro para API da Web:</span><span class="sxs-lookup"><span data-stu-id="56273-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="56273-182">Adicione a seguinte classe WebApiConfig ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="56273-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="56273-183">Configure o WebApiConfig.Registre-se no método Iniciar de aplicativos\_em Global.asax da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="56273-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="56273-184">Visual Studio Express 2012 para Web pára de funcionar depois de adicionar um item andaime</span><span class="sxs-lookup"><span data-stu-id="56273-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="56273-185">Se o Visual Studio Express 2012 para web parar de funcionar depois de adicionar item andaime com o Entity Framework (como o Controlador API 2 da Web com ações, usando o Entity Framework), é possível que o Visual Studio Express não tenha conseguido carregar a imagem nativa de um conjunto dependente do System.Web.Extensions.</span><span class="sxs-lookup"><span data-stu-id="56273-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="56273-186">Para corrigir esse problema, configure o Visual Studio Express para trabalhar com a imagem MSIL do System.Web.Extensions:</span><span class="sxs-lookup"><span data-stu-id="56273-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="56273-187">Abrir o prompt de comando no modo Administrador.</span><span class="sxs-lookup"><span data-stu-id="56273-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="56273-188">Vá para %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE ou %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (para Windows de 64 bits).</span><span class="sxs-lookup"><span data-stu-id="56273-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="56273-189">Abra o VWDExpress.exe.config em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="56273-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="56273-190">Adicione a seguinte &lt;linha&gt;/&lt;sob&gt; o elemento de tempo de execução de configuração:</span><span class="sxs-lookup"><span data-stu-id="56273-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="56273-191">Reiniciar visual studio express 2012 para Web.</span><span class="sxs-lookup"><span data-stu-id="56273-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="56273-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="56273-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="56273-193">Visualizar arquivo cshtml com Browse With ou F5 causa um erro no servidor</span><span class="sxs-lookup"><span data-stu-id="56273-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="56273-194">Quando você cria um projeto MVC 5 no Visual Studio 2012 (ou abre no Visual Studio 2012 um projeto MVC 5 que foi criado no Visual Studio 2013) e tenta visualizar um arquivo cshtml usando Browse With ou F5, você receberá um erro que afirma - **Erro do servidor no aplicativo '/'**.</span><span class="sxs-lookup"><span data-stu-id="56273-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="56273-195">O servidor tenta navegar para`http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="56273-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="56273-196">Para resolver esse problema, altere a configuração **Iniciar ação** em seu projeto para **Página Específica**.</span><span class="sxs-lookup"><span data-stu-id="56273-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="56273-197">Você não precisa fornecer um valor para a página.</span><span class="sxs-lookup"><span data-stu-id="56273-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="56273-198">Depois de fazer essa alteração, a seleção de`http://localhost:XXXX`F5 navega até a raiz de sua aplicação ( ).</span><span class="sxs-lookup"><span data-stu-id="56273-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="56273-199">Esse comportamento não é o mesmo que o comportamento dos projetos MVC 5 no Visual Studio 2013, onde a configuração **Página Atual** lança a página aberta.</span><span class="sxs-lookup"><span data-stu-id="56273-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="56273-200">Url Rewrite e Tilde(~)</span><span class="sxs-lookup"><span data-stu-id="56273-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="56273-201">Depois de atualizar para ASP.NET Razor 3 ou ASP.NET MVC 5, a notação tilde(~) pode não funcionar corretamente se você estiver usando regravações de URL.</span><span class="sxs-lookup"><span data-stu-id="56273-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="56273-202">A reescrita de URL afeta a notação de tilde(~)&gt;em &lt;elementos HTML como &lt;A/&gt;, &lt;SCRIPT/ , LINK/&gt;, e, como resultado, o tilde não é mais mapeado para o diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="56273-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="56273-203">Por exemplo, se você reescrever pedidos de **asp.net/content** para **asp.net**, o atributo href em &lt;A href="~/content/"/&gt; resolve **/content/content/** em vez de **/**.</span><span class="sxs-lookup"><span data-stu-id="56273-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="56273-204">Para suprimir essa alteração, você pode definir o contexto **IIS\_WasUrlRewritten** como falso em cada página da Web ou no **\_Aplicativo BeginRequest** em Global.asax.</span><span class="sxs-lookup"><span data-stu-id="56273-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="56273-205">Modelos</span><span class="sxs-lookup"><span data-stu-id="56273-205">Templates</span></span>

<span data-ttu-id="56273-206">Quando você cria ASP.NET projetos de MVC com o Visual Studio 2012 no Windows 8.1 ou No Windows Server 2012 R2, o Visual Studio exibe uma mensagem de erro que afirma "Configurando a Web [url] para falha ASP.NET 4.5".</span><span class="sxs-lookup"><span data-stu-id="56273-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![erro de configuração](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="56273-208">Você vê esse erro porque o Visual Studio 2012 não habilita o recurso ASP.NET 4.5 quando ele é instalado nessas versões do Windows.</span><span class="sxs-lookup"><span data-stu-id="56273-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="56273-209">Para habilitar ASP.NET 4.5, execute as etapas descritas nos [recursos do Turn Windows ativado ou desdiário](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span><span class="sxs-lookup"><span data-stu-id="56273-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![ativar ou desativar os recursos do Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="56273-211">Alternativamente, você pode habilitar ASP.NET 4.5 através da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="56273-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="56273-212">Abrir o prompt de comando no modo Administrador.</span><span class="sxs-lookup"><span data-stu-id="56273-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="56273-213">Execute o seguinte comando para habilitar ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="56273-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
