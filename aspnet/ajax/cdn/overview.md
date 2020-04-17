---
uid: ajax/cdn/overview
title: Microsoft Ajax Content Delivery Network | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 8e7efa2f321976671be321c760e2b478fe6e9e99
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540201"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="02d86-102">Rede de Distribuição de Conteúdo do Microsoft Ajax</span><span class="sxs-lookup"><span data-stu-id="02d86-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="02d86-103">Os aplicativos de produção não devem depender muito dos ativos de CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="02d86-104">Os aplicativos devem testar o ativo CDN referenciado e usar um recurso de recuo quando o CDN não estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="02d86-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="02d86-105">O Microsoft Ajax CDN não tem SLA acima e além de usar um CDN azure.</span><span class="sxs-lookup"><span data-stu-id="02d86-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="02d86-106">Use [este problema do GitHub](https://github.com/dotnet/AspNetDocs/issues/116) para relatar problemas com o CDN do Microsoft Ajax.</span><span class="sxs-lookup"><span data-stu-id="02d86-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="02d86-107">Sumário</span><span class="sxs-lookup"><span data-stu-id="02d86-107">Table of Contents</span></span>

<span data-ttu-id="02d86-108">**[ajax.microsoft.com renomeado para ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="02d86-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="02d86-109">**[Suporte visual studio .vsdoc](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="02d86-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="02d86-110">**[Usando ASP.NET Ajax do CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="02d86-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="02d86-111">**[Usando jQuery do CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="02d86-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="02d86-112">**[Usando jQuery UI do CDN](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="02d86-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="02d86-113">**[Arquivos de terceiros no CDN](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="02d86-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="02d86-114">jQuery É lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="02d86-115">jQuery Migrate é lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="02d86-116">lançamentos de iLic jQuery ui no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="02d86-117">liberações de validação de jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="02d86-118">jQuery Mobile Lançamentos no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="02d86-119">lançamentos de modelos de jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="02d86-120">lançamentos do ciclo jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="02d86-121">jQuery DataTables É lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="02d86-122">Lançamentos modernizadores no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="02d86-123">Lançamentos jshint no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="02d86-124">Lançamentos de nocaute no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="02d86-125">Globalize lançamentos no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="02d86-126">Releases de resposta no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="02d86-127">Lançamentos bootstrap no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="02d86-128">Bootstrap TouchCarousel é lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="02d86-129">Lançamentos hammer.js no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="02d86-130">ASP.NET Web Forms e Ajax é lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="02d86-131">ASP.NET lançamentos de MVC no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="02d86-132">ASP.NET lançamentos do SignalR no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="02d86-133">O CDN (Microsoft Ajax Content Delivery Network, rede de entrega de conteúdo do Microsoft Ajax) hospeda bibliotecas JavaScript de terceiros populares, como o jQuery, e permite adicioná-las facilmente aos seus aplicativos da Web.</span><span class="sxs-lookup"><span data-stu-id="02d86-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="02d86-134">Por exemplo, você pode começar a usar o jQuery que &lt;está&gt; hospedado neste CDN simplesmente adicionando uma tag de script à sua página que aponta para ajax.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="02d86-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="02d86-135">Aproveitando o CDN, você pode melhorar significativamente o desempenho de suas aplicações Ajax.</span><span class="sxs-lookup"><span data-stu-id="02d86-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="02d86-136">O conteúdo do CDN é armazenado em cache em servidores localizados em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="02d86-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="02d86-137">Além disso, o CDN permite que os navegadores reutilizem arquivos JavaScript de terceiros armazenados em cache para sites da Web localizados em diferentes domínios.</span><span class="sxs-lookup"><span data-stu-id="02d86-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="02d86-138">O CDN suporta SSL (HTTPS) no caso de você precisar servir uma página da Web usando a Camada de Soquetes Seguros.</span><span class="sxs-lookup"><span data-stu-id="02d86-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="02d86-139">O CDN hospeda as seguintes bibliotecas de scripts de terceiros que foram carregadas e são licenciadas para você, pelos proprietários dessas bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="02d86-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="02d86-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="02d86-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="02d86-141">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="02d86-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="02d86-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="02d86-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="02d86-143">validação de jQuery (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="02d86-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="02d86-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="02d86-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="02d86-145">jQuery DataTables (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="02d86-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="02d86-146">O Microsoft Ajax CDN também inclui as seguintes bibliotecas que foram carregadas pela Microsoft:</span><span class="sxs-lookup"><span data-stu-id="02d86-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="02d86-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="02d86-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="02d86-148">arquivos JavaScript mvc ASP.NET</span><span class="sxs-lookup"><span data-stu-id="02d86-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="02d86-149">arquivos JavaScript do sinalizador de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="02d86-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="02d86-150">A Microsoft não reivindica a propriedade de quaisquer bibliotecas de terceiros hospedadas neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="02d86-151">Os proprietários de direitos autorais das bibliotecas estão licenciando essas bibliotecas para você.</span><span class="sxs-lookup"><span data-stu-id="02d86-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="02d86-152">Todos os direitos que você pode ter para baixar e usar tais bibliotecas são concedidos exclusivamente pelos respectivos proprietários de direitos autorais.</span><span class="sxs-lookup"><span data-stu-id="02d86-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="02d86-153">Como não são bibliotecas da Microsoft, a Microsoft não oferece garantias ou licenças de direitos de propriedade intelectual (incluindo nenhum direito de patente implícito) para as bibliotecas de terceiros hospedadas neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="02d86-154">Se você deseja enviar sua biblioteca JavaScript e sua biblioteca é uma http://trends.builtwith.com) das principais bibliotecas JavaScript (conforme listado em ou extensões/plugins para essas AjaxCDNSubmission@Microsoft.combibliotecas que são (a) populares; ou (b) úteis para uso em ASP.NET, então entre em contato .</span><span class="sxs-lookup"><span data-stu-id="02d86-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="02d86-155">ajax.microsoft.com renomeado para ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="02d86-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="02d86-156">O CDN costumava usar o nome de domínio microsoft.com e foi alterado para usar o nome de domínio aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="02d86-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="02d86-157">Essa alteração foi feita para aumentar o desempenho porque quando um navegador fazia referência ao domínio microsoft.com ele enviava quaisquer cookies desse domínio através do fio com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="02d86-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="02d86-158">Ao renomear para um nome de domínio diferente microsoft.com desempenho pode ser aumentado em até 25%.</span><span class="sxs-lookup"><span data-stu-id="02d86-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="02d86-159">Observe ajax.microsoft.com continuarão funcionando, mas ajax.aspnetcdn.com é recomendado.</span><span class="sxs-lookup"><span data-stu-id="02d86-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="02d86-160">Formato antigo:https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="02d86-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="02d86-161">Novo formato:https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="02d86-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="02d86-162">Suporte visual studio .vsdoc</span><span class="sxs-lookup"><span data-stu-id="02d86-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="02d86-163">Para usar os arquivos .vsdoc corretamente com o Visual Studio 2008, você precisa ter certeza de que você tem VS 2008 SP1 instalado e o hotfix para arquivos vsdoc instalados.</span><span class="sxs-lookup"><span data-stu-id="02d86-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="02d86-164">Você pode obtê-los a partir daqui:</span><span class="sxs-lookup"><span data-stu-id="02d86-164">You can get these from here:</span></span>

- [<span data-ttu-id="02d86-165">Baixar Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="02d86-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Baixar Visual Studio 2008 SP1")
- [<span data-ttu-id="02d86-166">Baixe .vsdoc hotfix para Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="02d86-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Baixe .vsdoc hotfix para Visual Studio 2008 SP1")

<span data-ttu-id="02d86-167">O Visual Studio 2010 suporta arquivos .vsdoc sem nenhum patches adicional.</span><span class="sxs-lookup"><span data-stu-id="02d86-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="02d86-168">Usando ASP.NET Ajax do CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="02d86-169">Ao usar ASP.NET 4, você pode redirecionar todas as solicitações de ASP.NET scripts de para o CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="02d86-170">Recuperar scripts do CDN em vez de seu servidor web local pode melhorar substancialmente o desempenho de sites de ASP.NET público.</span><span class="sxs-lookup"><span data-stu-id="02d86-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="02d86-171">Use a propriedade ScriptManager EnableCDN para redirecionar todas as solicitações de script de ASP.NET para o CDN do Microsoft Ajax:</span><span class="sxs-lookup"><span data-stu-id="02d86-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="02d86-172">Usando jQuery do CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="02d86-173">Você pode usar scripts jQuery hospedados no CDN em seu aplicativo web adicionando o seguinte elemento de script a uma página:</span><span class="sxs-lookup"><span data-stu-id="02d86-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="02d86-174">O CDN também inclui a versão minizada do script jQuery, que você pode obter usando o seguinte elemento:</span><span class="sxs-lookup"><span data-stu-id="02d86-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="02d86-175">Para permitir que sua página recue para carregar jQuery de um caminho local em seu próprio site se o CDN estiver indisponível, adicione o seguinte elemento imediatamente após o elemento referenciar o CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="02d86-176">A página de exemplo a seguir usa a versão CDN da biblioteca jQuery (com recuo para uma cópia local) para exibir o conteúdo de um elemento div quando um botão é clicado.</span><span class="sxs-lookup"><span data-stu-id="02d86-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="02d86-177">Você pode aprender mais sobre jQuery e baixar uma cópia local do jQuery visitando o site [jQuery.](http://jquery.com/)</span><span class="sxs-lookup"><span data-stu-id="02d86-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="02d86-178">Usando jQuery UI do CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="02d86-179">O CDN também hospeda a biblioteca jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="02d86-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="02d86-180">A biblioteca jQuery UI inclui um rico conjunto de widgets e efeitos que você pode usar em seus aplicativos de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="02d86-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="02d86-181">Por exemplo, a página a seguir ilustra como você pode usar o jQuery UI Datepicker no contexto de um aplicativo ASP.NET Formulários da Web para exibir um calendário pop-up:</span><span class="sxs-lookup"><span data-stu-id="02d86-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="02d86-182">Quando você move o foco para a TextBox usando o teclado, um calendário é exibido:</span><span class="sxs-lookup"><span data-stu-id="02d86-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Calendário pop-up criado com Datepicker](overview/_static/image1.png)

<span data-ttu-id="02d86-184">Observe que você deve incluir três arquivos do CDN no código acima:</span><span class="sxs-lookup"><span data-stu-id="02d86-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="02d86-185">A biblioteca &mdash; jQuery A biblioteca jQuery UI depende da biblioteca jQuery.</span><span class="sxs-lookup"><span data-stu-id="02d86-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="02d86-186">Você deve adicionar a biblioteca jQuery à sua página antes de adicionar a biblioteca jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="02d86-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="02d86-187">A biblioteca &mdash; jQuery UI A biblioteca jQuery UI contém todos os efeitos e widgets da i-UI jQuery, como o widget Datepicker usado na página acima.</span><span class="sxs-lookup"><span data-stu-id="02d86-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="02d86-188">Tema &mdash; jQuery UI A ui jQuery suporta diferentes temas.</span><span class="sxs-lookup"><span data-stu-id="02d86-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="02d86-189">A página acima inclui um link para um arquivo CSS para importar o tema Redmond.</span><span class="sxs-lookup"><span data-stu-id="02d86-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="02d86-190">Todos os temas padrão da UI jQuery estão hospedados no CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="02d86-191">[Visite esta página](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 na CDN do Microsoft Ajax") para ver miniaturas de cada tema.</span><span class="sxs-lookup"><span data-stu-id="02d86-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="02d86-192">Para saber mais sobre a biblioteca jQuery UI, visite o site oficial [da jQuery UI](http://jQueryUI.com "jQuery UI site").</span><span class="sxs-lookup"><span data-stu-id="02d86-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="02d86-193">Arquivos de terceiros no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="02d86-194">O CDN hospeda algumas das bibliotecas JavaScript de terceiros mais populares.</span><span class="sxs-lookup"><span data-stu-id="02d86-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="02d86-195">A Microsoft não reivindica a propriedade de quaisquer bibliotecas de terceiros hospedadas neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="02d86-196">Os proprietários de direitos autorais das bibliotecas estão licenciando essas bibliotecas para você.</span><span class="sxs-lookup"><span data-stu-id="02d86-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="02d86-197">Todos os direitos que você pode ter para baixar e usar tais bibliotecas são concedidos exclusivamente pelos respectivos proprietários de direitos autorais.</span><span class="sxs-lookup"><span data-stu-id="02d86-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="02d86-198">Como não são bibliotecas da Microsoft, a Microsoft não oferece garantias ou licenças de direitos de propriedade intelectual (incluindo nenhum direito de patente implícito) para as bibliotecas de terceiros hospedadas neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="02d86-199">jQuery É lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="02d86-200">Os seguintes lançamentos de jQuery estão hospedados no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-350"></a><span data-ttu-id="02d86-201">jQuery versão 3.5.0</span><span class="sxs-lookup"><span data-stu-id="02d86-201">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="02d86-202">jQuery versão 3.4.1</span><span class="sxs-lookup"><span data-stu-id="02d86-202">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="02d86-203">jQuery versão 3.4.0</span><span class="sxs-lookup"><span data-stu-id="02d86-203">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="02d86-204">jQuery versão 3.3.1</span><span class="sxs-lookup"><span data-stu-id="02d86-204">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="02d86-205">jQuery versão 3.2.1</span><span class="sxs-lookup"><span data-stu-id="02d86-205">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="02d86-206">jQuery versão 3.2.0</span><span class="sxs-lookup"><span data-stu-id="02d86-206">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="02d86-207">jQuery versão 3.1.1</span><span class="sxs-lookup"><span data-stu-id="02d86-207">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="02d86-208">jQuery versão 3.1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-208">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="02d86-209">jQuery versão 3.0.0</span><span class="sxs-lookup"><span data-stu-id="02d86-209">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="02d86-210">jQuery versão 2.2.4</span><span class="sxs-lookup"><span data-stu-id="02d86-210">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="02d86-211">jQuery versão 2.2.3</span><span class="sxs-lookup"><span data-stu-id="02d86-211">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="02d86-212">jQuery versão 2.2.2</span><span class="sxs-lookup"><span data-stu-id="02d86-212">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="02d86-213">jQuery versão 2.2.1</span><span class="sxs-lookup"><span data-stu-id="02d86-213">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="02d86-214">jQuery versão 2.2.0</span><span class="sxs-lookup"><span data-stu-id="02d86-214">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="02d86-215">jQuery versão 2.1.4</span><span class="sxs-lookup"><span data-stu-id="02d86-215">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="02d86-216">jQuery versão 2.1.3</span><span class="sxs-lookup"><span data-stu-id="02d86-216">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="02d86-217">jQuery versão 2.1.2</span><span class="sxs-lookup"><span data-stu-id="02d86-217">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="02d86-218">jQuery versão 2.1.1</span><span class="sxs-lookup"><span data-stu-id="02d86-218">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="02d86-219">jQuery versão 2.1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-219">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="02d86-220">jQuery versão 2.0.3</span><span class="sxs-lookup"><span data-stu-id="02d86-220">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="02d86-221">jQuery versão 2.0.2</span><span class="sxs-lookup"><span data-stu-id="02d86-221">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="02d86-222">jQuery versão 2.0.1</span><span class="sxs-lookup"><span data-stu-id="02d86-222">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="02d86-223">jQuery versão 2.0.0</span><span class="sxs-lookup"><span data-stu-id="02d86-223">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="02d86-224">jQuery versão 1.12.4</span><span class="sxs-lookup"><span data-stu-id="02d86-224">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="02d86-225">jQuery versão 1.12.3</span><span class="sxs-lookup"><span data-stu-id="02d86-225">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="02d86-226">jQuery versão 1.12.2</span><span class="sxs-lookup"><span data-stu-id="02d86-226">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="02d86-227">jQuery versão 1.12.1</span><span class="sxs-lookup"><span data-stu-id="02d86-227">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="02d86-228">jQuery versão 1.12.0</span><span class="sxs-lookup"><span data-stu-id="02d86-228">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="02d86-229">jQuery versão 1.11.3</span><span class="sxs-lookup"><span data-stu-id="02d86-229">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="02d86-230">jQuery versão 1.11.2</span><span class="sxs-lookup"><span data-stu-id="02d86-230">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="02d86-231">jQuery versão 1.11.1</span><span class="sxs-lookup"><span data-stu-id="02d86-231">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="02d86-232">jQuery versão 1.11.0</span><span class="sxs-lookup"><span data-stu-id="02d86-232">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="02d86-233">jQuery versão 1.10.2</span><span class="sxs-lookup"><span data-stu-id="02d86-233">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="02d86-234">jQuery versão 1.10.1</span><span class="sxs-lookup"><span data-stu-id="02d86-234">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="02d86-235">jQuery versão 1.10.0</span><span class="sxs-lookup"><span data-stu-id="02d86-235">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="02d86-236">jQuery versão 1.9.1</span><span class="sxs-lookup"><span data-stu-id="02d86-236">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="02d86-237">jQuery versão 1.9.0</span><span class="sxs-lookup"><span data-stu-id="02d86-237">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="02d86-238">jQuery versão 1.8.3</span><span class="sxs-lookup"><span data-stu-id="02d86-238">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="02d86-239">jQuery versão 1.8.2</span><span class="sxs-lookup"><span data-stu-id="02d86-239">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="02d86-240">jQuery versão 1.8.1</span><span class="sxs-lookup"><span data-stu-id="02d86-240">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="02d86-241">jQuery versão 1.8.0</span><span class="sxs-lookup"><span data-stu-id="02d86-241">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="02d86-242">jQuery versão 1.7.2</span><span class="sxs-lookup"><span data-stu-id="02d86-242">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="02d86-243">jQuery versão 1.7.1</span><span class="sxs-lookup"><span data-stu-id="02d86-243">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="02d86-244">jQuery versão 1.7</span><span class="sxs-lookup"><span data-stu-id="02d86-244">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="02d86-245">jQuery versão 1.6.4</span><span class="sxs-lookup"><span data-stu-id="02d86-245">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="02d86-246">jQuery versão 1.6.3</span><span class="sxs-lookup"><span data-stu-id="02d86-246">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="02d86-247">jQuery versão 1.6.2</span><span class="sxs-lookup"><span data-stu-id="02d86-247">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="02d86-248">jQuery versão 1.6.1</span><span class="sxs-lookup"><span data-stu-id="02d86-248">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="02d86-249">jQuery versão 1.6</span><span class="sxs-lookup"><span data-stu-id="02d86-249">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="02d86-250">jQuery versão 1.5.2</span><span class="sxs-lookup"><span data-stu-id="02d86-250">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="02d86-251">jQuery versão 1.5.1</span><span class="sxs-lookup"><span data-stu-id="02d86-251">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="02d86-252">jQuery versão 1.5</span><span class="sxs-lookup"><span data-stu-id="02d86-252">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="02d86-253">jQuery versão 1.4.4</span><span class="sxs-lookup"><span data-stu-id="02d86-253">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="02d86-254">jQuery versão 1.4.3</span><span class="sxs-lookup"><span data-stu-id="02d86-254">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="02d86-255">jQuery versão 1.4.2</span><span class="sxs-lookup"><span data-stu-id="02d86-255">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="02d86-256">jQuery versão 1.4.1</span><span class="sxs-lookup"><span data-stu-id="02d86-256">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="02d86-257">jQuery versão 1.4</span><span class="sxs-lookup"><span data-stu-id="02d86-257">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="02d86-258">jQuery versão 1.3.2</span><span class="sxs-lookup"><span data-stu-id="02d86-258">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="02d86-259">jQuery Migrate é lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-259">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="02d86-260">Os seguintes lançamentos do jQuery Migrate estão hospedados no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-260">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="02d86-261">jQuery Migrate versão 3.0.0</span><span class="sxs-lookup"><span data-stu-id="02d86-261">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="02d86-262">jQuery Migrate versão 1.2.1</span><span class="sxs-lookup"><span data-stu-id="02d86-262">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="02d86-263">jQuery Migrate versão 1.2.0</span><span class="sxs-lookup"><span data-stu-id="02d86-263">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="02d86-264">jQuery Migrate versão 1.1.1</span><span class="sxs-lookup"><span data-stu-id="02d86-264">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="02d86-265">jQuery Migrate versão 1.1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-265">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="02d86-266">jQuery Migrate versão 1.0.0</span><span class="sxs-lookup"><span data-stu-id="02d86-266">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="02d86-267">lançamentos de iLic jQuery ui no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-267">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="02d86-268">Os seguintes lançamentos da biblioteca jQuery UI estão hospedados neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-268">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="02d86-269">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="02d86-269">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="02d86-270">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="02d86-270">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-271">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="02d86-271">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-272">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="02d86-272">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-273">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="02d86-273">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-274">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="02d86-274">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-275">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="02d86-275">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-276">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="02d86-276">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-277">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="02d86-277">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-278">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="02d86-278">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-279">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="02d86-279">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "jQuery UI 1.10.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-280">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="02d86-280">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-281">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="02d86-281">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-282">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="02d86-282">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-283">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="02d86-283">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-284">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="02d86-284">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-285">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="02d86-285">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-286">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="02d86-286">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-287">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="02d86-287">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-288">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="02d86-288">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-289">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="02d86-289">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-290">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="02d86-290">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-291">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="02d86-291">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-292">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="02d86-292">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-293">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="02d86-293">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-294">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="02d86-294">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-295">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="02d86-295">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-296">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="02d86-296">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-297">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="02d86-297">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-298">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="02d86-298">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-299">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="02d86-299">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-300">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="02d86-300">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-301">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="02d86-301">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-302">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="02d86-302">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-303">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="02d86-303">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-304">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="02d86-304">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="02d86-305">liberações de validação de jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-305">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="02d86-306">As seguintes versões do [plugin jQuery Validation](https://jqueryvalidation.org/ "plugin de validação de jQuery") estão hospedadas neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-306">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="02d86-307">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="02d86-307">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="02d86-308">jQuery Validar 1.19.1</span><span class="sxs-lookup"><span data-stu-id="02d86-308">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "validação jQuery 1.19.1")
- [<span data-ttu-id="02d86-309">jQuery Validar 1.19.0</span><span class="sxs-lookup"><span data-stu-id="02d86-309">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "validação jQuery 1.19.0")
- [<span data-ttu-id="02d86-310">jQuery Validar 1.17.0</span><span class="sxs-lookup"><span data-stu-id="02d86-310">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "validação jQuery 1.17.0")
- [<span data-ttu-id="02d86-311">jQuery Validar 1.16.0</span><span class="sxs-lookup"><span data-stu-id="02d86-311">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "Validação do jQuery 1.16.0")
- [<span data-ttu-id="02d86-312">jQuery Validar 1.15.1</span><span class="sxs-lookup"><span data-stu-id="02d86-312">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "Validação do jQuery 1.15.1")
- [<span data-ttu-id="02d86-313">jQuery Validar 1.15.0</span><span class="sxs-lookup"><span data-stu-id="02d86-313">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "Validação do jQuery 1.15.0")
- [<span data-ttu-id="02d86-314">jQuery Validar 1.14.0</span><span class="sxs-lookup"><span data-stu-id="02d86-314">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "Validação do jQuery 1.14.0")
- [<span data-ttu-id="02d86-315">jQuery Validar 1.13.1</span><span class="sxs-lookup"><span data-stu-id="02d86-315">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "Validação do jQuery 1.13.1")
- [<span data-ttu-id="02d86-316">jQuery Validar 1.13.0</span><span class="sxs-lookup"><span data-stu-id="02d86-316">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "Validação do jQuery 1.13.0")
- [<span data-ttu-id="02d86-317">jQuery Validar 1.12.0</span><span class="sxs-lookup"><span data-stu-id="02d86-317">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "Validação do jQuery 1.12.0")
- [<span data-ttu-id="02d86-318">jQuery Validar 1.11.1</span><span class="sxs-lookup"><span data-stu-id="02d86-318">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "Validação do jQuery 1.11.1")
- [<span data-ttu-id="02d86-319">jQuery Validar 1.11.0</span><span class="sxs-lookup"><span data-stu-id="02d86-319">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "Validação do jQuery 1.11.0")
- [<span data-ttu-id="02d86-320">jQuery Validar 1.10.0</span><span class="sxs-lookup"><span data-stu-id="02d86-320">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "Validação do jQuery 1.10.0")
- [<span data-ttu-id="02d86-321">jQuery Validar 1.9</span><span class="sxs-lookup"><span data-stu-id="02d86-321">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate versão 1.9")
- [<span data-ttu-id="02d86-322">jQuery Validar 1.8.1</span><span class="sxs-lookup"><span data-stu-id="02d86-322">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate versão 1.8.1")
- [<span data-ttu-id="02d86-323">jQuery Validar 1.8</span><span class="sxs-lookup"><span data-stu-id="02d86-323">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate versão 1.8")
- [<span data-ttu-id="02d86-324">jQuery Validar 1.7</span><span class="sxs-lookup"><span data-stu-id="02d86-324">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate versão 1.7")
- [<span data-ttu-id="02d86-325">Validar jQuery 1.6</span><span class="sxs-lookup"><span data-stu-id="02d86-325">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "Validar jQuery 1.6")
- [<span data-ttu-id="02d86-326">Validar jQuery 1.5.5</span><span class="sxs-lookup"><span data-stu-id="02d86-326">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "Validar jQuery 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="02d86-327">jQuery Mobile Lançamentos no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-327">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="02d86-328">Os seguintes lançamentos da biblioteca jQuery Mobile estão hospedados neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-328">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="02d86-329">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="02d86-329">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="02d86-330">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="02d86-330">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-331">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="02d86-331">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-332">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="02d86-332">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-333">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="02d86-333">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-334">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="02d86-334">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-335">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="02d86-335">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-336">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="02d86-336">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-337">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="02d86-337">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-338">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="02d86-338">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-339">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="02d86-339">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-340">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-340">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-341">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="02d86-341">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-342">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="02d86-342">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-343">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-343">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-344">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="02d86-344">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "jQuery Mobile 1.0 RC2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-345">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="02d86-345">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "jQuery Mobile 1.0 RC1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="02d86-346">jQuery Mobile 1.0 beta 3</span><span class="sxs-lookup"><span data-stu-id="02d86-346">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "jQuery Mobile 1.0 Beta 3 na CDN do Microsoft Ajax")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="02d86-347">lançamentos de modelos de jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-347">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="02d86-348">As seguintes versões do plugin jQuery Templates estão hospedadas neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-348">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="02d86-349">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="02d86-349">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="02d86-350">Modelos jQuery Beta 1</span><span class="sxs-lookup"><span data-stu-id="02d86-350">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "Modelos jQuery Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="02d86-351">lançamentos do ciclo jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-351">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="02d86-352">As seguintes versões do plugin jQuery Cycle estão hospedadas neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-352">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="02d86-353">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="02d86-353">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="02d86-354">jQuery Ciclo 2.99</span><span class="sxs-lookup"><span data-stu-id="02d86-354">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="02d86-355">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="02d86-355">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="02d86-356">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="02d86-356">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="02d86-357">jQuery DataTables É lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-357">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="02d86-358">As seguintes versões do plugin jQuery DataTables estão hospedadas neste CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-358">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="02d86-359">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="02d86-359">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="02d86-360">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="02d86-360">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="02d86-361">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="02d86-361">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="02d86-362">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="02d86-362">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="02d86-363">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="02d86-363">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="02d86-364">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="02d86-364">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="02d86-365">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="02d86-365">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="02d86-366">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="02d86-366">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="02d86-367">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="02d86-367">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="02d86-368">Lançamentos modernizadores no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-368">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="02d86-369">As seguintes versões do [Modernizr](http://www.modernizr.com "Modernizador") estão hospedadas no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-369">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="02d86-370">Lançamentos jshint no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-370">JSHint Releases on the CDN</span></span>

<span data-ttu-id="02d86-371">As seguintes versões do [JSHint](http://www.jshint.com "JSHint") estão hospedadas no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-371">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="02d86-372">Lançamentos de nocaute no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-372">Knockout Releases on the CDN</span></span>

<span data-ttu-id="02d86-373">As seguintes versões de [Knockout](http://www.knockoutjs.com "Nocaute") estão hospedadas no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-373">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="02d86-374">Globalize lançamentos no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-374">Globalize Releases on the CDN</span></span>

<span data-ttu-id="02d86-375">Os seguintes lançamentos do [Globalize](https://github.com/jquery/globalize "Globalizar") estão hospedados no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-375">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="02d86-376">Globalize versão 1.0.0</span><span class="sxs-lookup"><span data-stu-id="02d86-376">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="02d86-377">Globalize versão 0.1.1</span><span class="sxs-lookup"><span data-stu-id="02d86-377">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="02d86-378">todas as culturas</span><span class="sxs-lookup"><span data-stu-id="02d86-378">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="02d86-379">Substitua "{culture-code}" pelo código de cultura desejado, por exemplo, globalize.culture.en-GB.js== Arquivos Microsoft no CDN ==Essas bibliotecas foram carregadas pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="02d86-379">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="02d86-380">Releases de resposta no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-380">Respond Releases on the CDN</span></span>

<span data-ttu-id="02d86-381">As seguintes versões do [Respond](https://github.com/scottjehl/Respond "Responder") estão hospedadas no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-381">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="02d86-382">Responda versão 1.4.2</span><span class="sxs-lookup"><span data-stu-id="02d86-382">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="02d86-383">Responda versão 1.4.1</span><span class="sxs-lookup"><span data-stu-id="02d86-383">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="02d86-384">Responda versão 1.4.0</span><span class="sxs-lookup"><span data-stu-id="02d86-384">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="02d86-385">Responda versão 1.3.0</span><span class="sxs-lookup"><span data-stu-id="02d86-385">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="02d86-386">Responda versão 1.2.0</span><span class="sxs-lookup"><span data-stu-id="02d86-386">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="02d86-387">Lançamentos bootstrap no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-387">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="02d86-388">Os seguintes lançamentos de [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap estão hospedados no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-388">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="02d86-389">Bootstrap versão 4.4.1</span><span class="sxs-lookup"><span data-stu-id="02d86-389">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="02d86-390">Bootstrap versão 4.3.1</span><span class="sxs-lookup"><span data-stu-id="02d86-390">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="02d86-391">Bootstrap versão 4.2.1</span><span class="sxs-lookup"><span data-stu-id="02d86-391">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="02d86-392">Bootstrap versão 4.1.1</span><span class="sxs-lookup"><span data-stu-id="02d86-392">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="02d86-393">Bootstrap versão 4.0.0</span><span class="sxs-lookup"><span data-stu-id="02d86-393">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="02d86-394">Bootstrap versão 3.4.1</span><span class="sxs-lookup"><span data-stu-id="02d86-394">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="02d86-395">Bootstrap versão 3.4.0</span><span class="sxs-lookup"><span data-stu-id="02d86-395">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="02d86-396">Bootstrap versão 3.3.7</span><span class="sxs-lookup"><span data-stu-id="02d86-396">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="02d86-397">Bootstrap versão 3.3.6</span><span class="sxs-lookup"><span data-stu-id="02d86-397">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="02d86-398">Bootstrap versão 3.3.5</span><span class="sxs-lookup"><span data-stu-id="02d86-398">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="02d86-399">Bootstrap versão 3.3.4</span><span class="sxs-lookup"><span data-stu-id="02d86-399">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="02d86-400">Bootstrap versão 3.3.2</span><span class="sxs-lookup"><span data-stu-id="02d86-400">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="02d86-401">Bootstrap versão 3.3.1</span><span class="sxs-lookup"><span data-stu-id="02d86-401">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="02d86-402">Bootstrap versão 3.3.0</span><span class="sxs-lookup"><span data-stu-id="02d86-402">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="02d86-403">Bootstrap versão 3.2.0</span><span class="sxs-lookup"><span data-stu-id="02d86-403">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="02d86-404">Bootstrap versão 3.1.1</span><span class="sxs-lookup"><span data-stu-id="02d86-404">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="02d86-405">Bootstrap versão 3.1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-405">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="02d86-406">Bootstrap versão 3.0.3</span><span class="sxs-lookup"><span data-stu-id="02d86-406">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="02d86-407">Bootstrap versão 3.0.2</span><span class="sxs-lookup"><span data-stu-id="02d86-407">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="02d86-408">Bootstrap versão 3.0.1</span><span class="sxs-lookup"><span data-stu-id="02d86-408">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="02d86-409">Bootstrap versão 3.0.0</span><span class="sxs-lookup"><span data-stu-id="02d86-409">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="02d86-410">Bootstrap versão 2.3.2</span><span class="sxs-lookup"><span data-stu-id="02d86-410">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="02d86-411">Bootstrap versão 2.3.1</span><span class="sxs-lookup"><span data-stu-id="02d86-411">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="02d86-412">Bootstrap TouchCarousel é lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-412">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="02d86-413">Os seguintes [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") lançamentos de Bootstrap TouchCarousel estão hospedados no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-413">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="02d86-414">Bootstrap TouchCarousel versão 0.8.0</span><span class="sxs-lookup"><span data-stu-id="02d86-414">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="02d86-415">Lançamentos hammer.js no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-415">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="02d86-416">As seguintes [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") versões de lançamentos hammer.js estão hospedadas no CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-416">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="02d86-417">Hammer.js versão 2.0.4</span><span class="sxs-lookup"><span data-stu-id="02d86-417">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="02d86-418">ASP.NET Web Forms e Ajax é lançado no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-418">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="02d86-419">Os seguintes lançamentos da ASP.NET Ajax Library estão hospedados no CDN.</span><span class="sxs-lookup"><span data-stu-id="02d86-419">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="02d86-420">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="02d86-420">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="02d86-421">ASP.NET Web Forms e Ajax versão 4.5.2</span><span class="sxs-lookup"><span data-stu-id="02d86-421">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "Web Forms do ASP.NET e Ajax 4.5.2")
- [<span data-ttu-id="02d86-422">ASP.NET Web Forms e Ajax versão 4</span><span class="sxs-lookup"><span data-stu-id="02d86-422">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms e Ajax 4")
- [<span data-ttu-id="02d86-423">ASP.NET Versão 3.5 do Ajax</span><span class="sxs-lookup"><span data-stu-id="02d86-423">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="02d86-424">ASP.NET lançamentos de MVC no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-424">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="02d86-425">Os seguintes arquivos JavaScript ASP.NET estão hospedados neste CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-425">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="02d86-426">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="02d86-426">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="02d86-427">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="02d86-427">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="02d86-428">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="02d86-428">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="02d86-429">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="02d86-429">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="02d86-430">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="02d86-430">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="02d86-431">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="02d86-431">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="02d86-432">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-432">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="02d86-433">ASP.NET lançamentos do SignalR no CDN</span><span class="sxs-lookup"><span data-stu-id="02d86-433">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="02d86-434">Os seguintes arquivos JavaScript ASP.NET estão hospedados neste CDN:</span><span class="sxs-lookup"><span data-stu-id="02d86-434">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="02d86-435">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="02d86-435">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="02d86-436">sinal de ASP.NET 2.2.1</span><span class="sxs-lookup"><span data-stu-id="02d86-436">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="02d86-437">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="02d86-437">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="02d86-438">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-438">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="02d86-439">sinal de ASP.NET 2.0.3</span><span class="sxs-lookup"><span data-stu-id="02d86-439">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="02d86-440">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="02d86-440">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="02d86-441">sinal de ASP.NET 2.0.1</span><span class="sxs-lookup"><span data-stu-id="02d86-441">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="02d86-442">sinal de ASP.NET 2.0.0</span><span class="sxs-lookup"><span data-stu-id="02d86-442">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="02d86-443">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="02d86-443">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="02d86-444">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="02d86-444">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="02d86-445">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="02d86-445">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="02d86-446">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="02d86-446">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="02d86-447">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="02d86-447">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="02d86-448">Para obter informações sobre os termos de uso do CDN, consulte os [Termos de Uso do Microsoft Ajax CDN](https://www.asp.net/terms-of-use "Termos de uso do Microsoft Ajax CDN").</span><span class="sxs-lookup"><span data-stu-id="02d86-448">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
