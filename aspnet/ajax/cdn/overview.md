---
uid: ajax/cdn/overview
title: Rede de distribuição de conteúdo do Microsoft Ajax | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 65eee9bc477fc8adf10e8d819b93375ffbb72d7b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044503"
---
<a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="b914e-102">Rede de Distribuição de Conteúdo do Microsoft Ajax</span><span class="sxs-lookup"><span data-stu-id="b914e-102">Microsoft Ajax Content Delivery Network</span></span>
====================
> [!WARNING]
> <span data-ttu-id="b914e-103">Aplicativos de produção não devem usar uma dependência nos ativos da CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="b914e-104">Aplicativos devem testar para o ativo CDN referenciado e usar um ativo de fallback quando o CDN não está disponível.</span><span class="sxs-lookup"><span data-stu-id="b914e-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span> 
>
> <span data-ttu-id="b914e-105">CDN do Microsoft Ajax não tem SLA além de usar uma CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="b914e-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="b914e-106">Use [esse problema de GitHub](https://github.com/aspnet/Docs/issues/5832) para relatar problemas com a CDN do Microsoft Ajax.</span><span class="sxs-lookup"><span data-stu-id="b914e-106">Use [this GitHub issue](https://github.com/aspnet/Docs/issues/5832) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="b914e-107">Sumário</span><span class="sxs-lookup"><span data-stu-id="b914e-107">Table of Contents</span></span>

<span data-ttu-id="b914e-108">**[AJAX.microsoft.com renomeado para ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="b914e-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="b914e-109">**[Suporte do Visual Studio .vsdoc](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="b914e-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="b914e-110">**[Usando o ASP.NET Ajax da CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="b914e-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="b914e-111">**[Usando o jQuery da CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="b914e-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="b914e-112">**[Usando o jQuery UI da CDN](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="b914e-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="b914e-113">**[Arquivos de terceiros na CDN](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="b914e-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="b914e-114">Versões do jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="b914e-115">Versões de migrar do jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="b914e-116">Versões de interface do usuário na CDN do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="b914e-117">Versões de validação na CDN do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="b914e-118">jQuery Mobile de versões no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="b914e-119">Versões de modelos na CDN do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="b914e-120">Ciclo de lançamentos na CDN do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="b914e-121">jQuery DataTables versões na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="b914e-122">Versões do Modernizr na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="b914e-123">Versões de JSHint na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="b914e-124">Versões do Knockout na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="b914e-125">Globalizar versões na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="b914e-126">Responder a versões na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="b914e-127">Versões de bootstrap na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="b914e-128">Versões de bootstrap TouchCarousel na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="b914e-129">Versões de hammer.js na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="b914e-130">Web Forms do ASP.NET e Ajax versões na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="b914e-131">Versões do ASP.NET MVC no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="b914e-132">Versões do ASP.NET SignalR no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="b914e-133">A Microsoft Ajax Content Delivery Network (CDN) hospeda bibliotecas JavaScript populares de terceiros, como o jQuery e permite que você os adicione facilmente para seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="b914e-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="b914e-134">Por exemplo, você pode começar a usar jQuery, que é hospedado deste CDN simplesmente adicionando um &lt;script&gt; marca para a página que aponta para ajax.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="b914e-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="b914e-135">Ao aproveitar a CDN, você pode melhorar significativamente o desempenho de seus aplicativos Ajax.</span><span class="sxs-lookup"><span data-stu-id="b914e-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="b914e-136">O conteúdo da CDN é armazenados em cache em servidores localizados em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="b914e-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="b914e-137">Além disso, a CDN permite que os navegadores para reutilizar arquivos JavaScript de terceiros em cache para sites da web que estão localizados em domínios diferentes.</span><span class="sxs-lookup"><span data-stu-id="b914e-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="b914e-138">A CDN dá suporte a SSL (HTTPS), caso seja necessário atender a uma página da web usando o protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="b914e-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="b914e-139">A CDN hospeda as seguintes bibliotecas de script de terceiros que foram carregadas e, em seguida, são licenciadas para você, pelos proprietários dessas bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="b914e-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="b914e-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="b914e-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="b914e-141">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="b914e-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="b914e-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="b914e-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="b914e-143">jQuery Validation (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="b914e-143">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="b914e-144">jQuery ciclo (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="b914e-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="b914e-145">jQuery DataTables (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="b914e-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="b914e-146">CDN do Microsoft Ajax também inclui as seguintes bibliotecas que foram carregadas pela Microsoft:</span><span class="sxs-lookup"><span data-stu-id="b914e-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="b914e-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="b914e-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="b914e-148">Arquivos de JavaScript do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b914e-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="b914e-149">Arquivos ASP.NET SignalR JavaScript</span><span class="sxs-lookup"><span data-stu-id="b914e-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="b914e-150">Microsoft não reivindica a propriedade de todas as bibliotecas de terceiros hospedados nesta CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="b914e-151">Os proprietários dos direitos autorais das bibliotecas são licenciamento destas bibliotecas para você.</span><span class="sxs-lookup"><span data-stu-id="b914e-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="b914e-152">Quaisquer direitos que talvez você precise baixar para usar essas bibliotecas, são concedidos unicamente e exclusivamente pelos respectivos proprietários dos direitos autorais.</span><span class="sxs-lookup"><span data-stu-id="b914e-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="b914e-153">Como esses não são bibliotecas da Microsoft, a Microsoft fornece sem garantias ou licenças de direitos de propriedade intelectual (incluindo sem direitos de patentes implícitos) para as bibliotecas de terceiros hospedadas deste CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="b914e-154">Se você quiser enviar sua biblioteca de JavaScript e sua biblioteca é uma das principais bibliotecas JavaScript (conforme listado em http://trends.builtwith.com) ou extensões/plug-ins para essas bibliotecas que são (a) populares; ou (b) útil para uso no ASP.NET, em seguida, entre em contato com AjaxCDNSubmission@Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="b914e-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="b914e-155">AJAX.microsoft.com renomeado para ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="b914e-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="b914e-156">A CDN usado para usar o nome de domínio microsoft.com e foi alterada para usar o nome de domínio aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="b914e-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="b914e-157">Essa alteração foi feita para aumentar o desempenho porque quando um navegador referenciado no domínio microsoft.com enviaria os cookies desse domínio pela rede com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="b914e-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="b914e-158">Renomeando com um nome de domínio que não seja o microsoft.com desempenho pode ser aumentado em tanto para 25%.</span><span class="sxs-lookup"><span data-stu-id="b914e-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="b914e-159">Observe ajax.microsoft.com continuarão a funcionar, mas ajax.aspnetcdn.com é recomendado.</span><span class="sxs-lookup"><span data-stu-id="b914e-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="b914e-160">Formato antigo: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="b914e-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="b914e-161">Novo formato: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="b914e-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="b914e-162">Suporte do Visual Studio .vsdoc</span><span class="sxs-lookup"><span data-stu-id="b914e-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="b914e-163">Para usar os arquivos de .vsdoc corretamente com o Visual Studio 2008, você precisará certificar-se de que você tenha o VS 2008 SP1 e o hotfix para arquivos vsdoc instalados.</span><span class="sxs-lookup"><span data-stu-id="b914e-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="b914e-164">Você pode obtê-los aqui:</span><span class="sxs-lookup"><span data-stu-id="b914e-164">You can get these from here:</span></span>

- [<span data-ttu-id="b914e-165">Baixe o Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="b914e-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Baixe o Visual Studio 2008 SP1")
- [<span data-ttu-id="b914e-166">Baixar o hotfix .vsdoc para Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="b914e-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "baixar o hotfix .vsdoc para Visual Studio 2008 SP1")

<span data-ttu-id="b914e-167">Visual Studio 2010 dá suporte a arquivos de .vsdoc sem quaisquer patches adicionais.</span><span class="sxs-lookup"><span data-stu-id="b914e-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="b914e-168">Usando o ASP.NET Ajax da CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="b914e-169">Ao usar o ASP.NET 4, você pode redirecionar todas as solicitações para os scripts de estrutura do ASP.NET para o CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="b914e-170">Recuperar os scripts da CDN, em vez de seu servidor web local pode melhorar consideravelmente o desempenho de sites públicos do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b914e-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="b914e-171">Use a propriedade ScriptManager EnableCDN para redirecionar todas as solicitações de script do ASP.NET framework para CDN do Microsoft Ajax:</span><span class="sxs-lookup"><span data-stu-id="b914e-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="b914e-172">Usando o jQuery da CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="b914e-173">Você pode usar scripts de jQuery hospedados em CDN em seu aplicativo Web, adicionando o seguinte elemento de script para uma página:</span><span class="sxs-lookup"><span data-stu-id="b914e-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="b914e-174">A CDN também inclui a versão reduzida do script jQuery, que pode ser obtido usando o seguinte elemento:</span><span class="sxs-lookup"><span data-stu-id="b914e-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="b914e-175">Para permitir que sua página de fallback para carregar jQuery de um caminho local em seu próprio site, se a CDN estiver disponível, adicione o seguinte elemento imediatamente após o elemento que referencia o CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="b914e-176">A página de exemplo a seguir usa a versão CDN da biblioteca jQuery (com fallback para uma cópia local) para exibir o conteúdo de um elemento div, quando um botão é clicado.</span><span class="sxs-lookup"><span data-stu-id="b914e-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="b914e-177">Você pode saber mais sobre o jQuery e baixar uma cópia local do jQuery, visitando a [jQuery](http://jquery.com/) site da Web.</span><span class="sxs-lookup"><span data-stu-id="b914e-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="b914e-178">Usando o jQuery UI da CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="b914e-179">A CDN também hospeda a biblioteca de interface do usuário do jQuery.</span><span class="sxs-lookup"><span data-stu-id="b914e-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="b914e-180">A biblioteca de interface do usuário do jQuery inclui um conjunto avançado de widgets e efeitos que você pode usar em seus aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b914e-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="b914e-181">Por exemplo, a página a seguir ilustra como você pode usar o jQuery UI Datepicker no contexto de um aplicativo ASP.NET Web Forms para exibir um calendário pop-up:</span><span class="sxs-lookup"><span data-stu-id="b914e-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="b914e-182">Quando você move o foco para a caixa de texto usando o teclado, será exibido um calendário:</span><span class="sxs-lookup"><span data-stu-id="b914e-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Calendário pop-up criado com o Datepicker](overview/_static/image1.png)

<span data-ttu-id="b914e-184">Observe que você deve incluir três arquivos da CDN no código acima:</span><span class="sxs-lookup"><span data-stu-id="b914e-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="b914e-185">A biblioteca jQuery &mdash; a biblioteca de interface do usuário do jQuery depende da biblioteca jQuery.</span><span class="sxs-lookup"><span data-stu-id="b914e-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="b914e-186">Você deve adicionar a biblioteca jQuery para sua página antes de adicionar a biblioteca de interface do usuário do jQuery.</span><span class="sxs-lookup"><span data-stu-id="b914e-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="b914e-187">A biblioteca de interface do usuário do jQuery &mdash; a biblioteca de interface do usuário do jQuery contém todos os efeitos de interface do usuário do jQuery e widgets, como o widget Datepicker usado na página acima.</span><span class="sxs-lookup"><span data-stu-id="b914e-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="b914e-188">Um tema de interface do usuário do jQuery &mdash; o jQuery UI dá suporte a diferentes temas.</span><span class="sxs-lookup"><span data-stu-id="b914e-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="b914e-189">A página acima inclui um link para um arquivo CSS para importar o tema de Redmond.</span><span class="sxs-lookup"><span data-stu-id="b914e-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="b914e-190">Todos os temas de interface do usuário do jQuery padrão são hospedados na CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="b914e-191">[Visite essa página](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 na CDN do Microsoft Ajax") exibam miniaturas para cada tema.</span><span class="sxs-lookup"><span data-stu-id="b914e-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="b914e-192">Para saber mais sobre a biblioteca de interface do usuário do jQuery, visite oficial [site de interface do usuário do jQuery](http://jQueryUI.com "site do jQuery UI").</span><span class="sxs-lookup"><span data-stu-id="b914e-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="b914e-193">Arquivos de terceiros na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="b914e-194">A CDN hospeda algumas das bibliotecas de JavaScript de terceiros mais populares.</span><span class="sxs-lookup"><span data-stu-id="b914e-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="b914e-195">Microsoft não reivindica a propriedade de todas as bibliotecas de terceiros hospedados nesta CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="b914e-196">Os proprietários dos direitos autorais das bibliotecas são licenciamento destas bibliotecas para você.</span><span class="sxs-lookup"><span data-stu-id="b914e-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="b914e-197">Quaisquer direitos que talvez você precise baixar para usar essas bibliotecas, são concedidos unicamente e exclusivamente pelos respectivos proprietários dos direitos autorais.</span><span class="sxs-lookup"><span data-stu-id="b914e-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="b914e-198">Como esses não são bibliotecas da Microsoft, a Microsoft fornece sem garantias ou licenças de direitos de propriedade intelectual (incluindo sem direitos de patentes implícitos) para as bibliotecas de terceiros hospedadas deste CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="b914e-199">Versões do jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="b914e-200">As seguintes versões do jQuery são hospedadas na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-331"></a><span data-ttu-id="b914e-201">versão do jQuery 3.3.1</span><span class="sxs-lookup"><span data-stu-id="b914e-201">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="b914e-202">versão do jQuery 3.2.1</span><span class="sxs-lookup"><span data-stu-id="b914e-202">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="b914e-203">versão do jQuery 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b914e-203">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="b914e-204">versão do jQuery 3.1.1</span><span class="sxs-lookup"><span data-stu-id="b914e-204">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="b914e-205">jQuery versão 3.1.0</span><span class="sxs-lookup"><span data-stu-id="b914e-205">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="b914e-206">jQuery versão 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b914e-206">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="b914e-207">versão do jQuery 2.2.4</span><span class="sxs-lookup"><span data-stu-id="b914e-207">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="b914e-208">jQuery versão 2.2.3</span><span class="sxs-lookup"><span data-stu-id="b914e-208">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="b914e-209">jQuery versão 2.2.2</span><span class="sxs-lookup"><span data-stu-id="b914e-209">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="b914e-210">jQuery versão 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b914e-210">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="b914e-211">versão 2.2.0 do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-211">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="b914e-212">versão do jQuery 2.1.4</span><span class="sxs-lookup"><span data-stu-id="b914e-212">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="b914e-213">jQuery versão 2.1.3</span><span class="sxs-lookup"><span data-stu-id="b914e-213">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="b914e-214">versão do jQuery 2.1.2</span><span class="sxs-lookup"><span data-stu-id="b914e-214">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="b914e-215">versão do jQuery 2.1.1</span><span class="sxs-lookup"><span data-stu-id="b914e-215">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="b914e-216">versão 2.1.0 do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-216">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="b914e-217">jQuery versão 2.0.3</span><span class="sxs-lookup"><span data-stu-id="b914e-217">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="b914e-218">versão do jQuery 2.0.2</span><span class="sxs-lookup"><span data-stu-id="b914e-218">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="b914e-219">jQuery versão 2.0.1</span><span class="sxs-lookup"><span data-stu-id="b914e-219">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="b914e-220">jQuery versão 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b914e-220">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="b914e-221">versão do jQuery 1.12.4</span><span class="sxs-lookup"><span data-stu-id="b914e-221">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="b914e-222">versão do jQuery 1.12.3</span><span class="sxs-lookup"><span data-stu-id="b914e-222">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="b914e-223">versão do jQuery 1.12.2</span><span class="sxs-lookup"><span data-stu-id="b914e-223">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="b914e-224">versão do jQuery 1.12.1</span><span class="sxs-lookup"><span data-stu-id="b914e-224">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="b914e-225">versão do jQuery 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b914e-225">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="b914e-226">versão do jQuery 1.11.3</span><span class="sxs-lookup"><span data-stu-id="b914e-226">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="b914e-227">versão do jQuery 1.11.2</span><span class="sxs-lookup"><span data-stu-id="b914e-227">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="b914e-228">versão do jQuery 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b914e-228">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="b914e-229">versão do jQuery 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b914e-229">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="b914e-230">versão do jQuery 1.10.2</span><span class="sxs-lookup"><span data-stu-id="b914e-230">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="b914e-231">versão do jQuery 1.10.1</span><span class="sxs-lookup"><span data-stu-id="b914e-231">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="b914e-232">versão do jQuery 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b914e-232">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="b914e-233">versão do jQuery 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b914e-233">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="b914e-234">jQuery versão 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b914e-234">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="b914e-235">versão do jQuery 1.8.3</span><span class="sxs-lookup"><span data-stu-id="b914e-235">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="b914e-236">versão do jQuery 1.8.2</span><span class="sxs-lookup"><span data-stu-id="b914e-236">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="b914e-237">jQuery versão 1.8.1</span><span class="sxs-lookup"><span data-stu-id="b914e-237">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="b914e-238">jQuery versão 1.8.0</span><span class="sxs-lookup"><span data-stu-id="b914e-238">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="b914e-239">versão do jQuery 1.7.2</span><span class="sxs-lookup"><span data-stu-id="b914e-239">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="b914e-240">versão 1.7.1 do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-240">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="b914e-241">versão do jQuery 1.7</span><span class="sxs-lookup"><span data-stu-id="b914e-241">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="b914e-242">versão do jQuery 1.6.4</span><span class="sxs-lookup"><span data-stu-id="b914e-242">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="b914e-243">versão do jQuery 1.6.3</span><span class="sxs-lookup"><span data-stu-id="b914e-243">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="b914e-244">versão do jQuery 1.6.2</span><span class="sxs-lookup"><span data-stu-id="b914e-244">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="b914e-245">jQuery versão 1.6.1</span><span class="sxs-lookup"><span data-stu-id="b914e-245">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="b914e-246">versão do jQuery 1.6</span><span class="sxs-lookup"><span data-stu-id="b914e-246">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="b914e-247">versão do jQuery 1.5.2</span><span class="sxs-lookup"><span data-stu-id="b914e-247">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="b914e-248">versão do jQuery 1.5.1</span><span class="sxs-lookup"><span data-stu-id="b914e-248">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="b914e-249">versão do jQuery 1.5</span><span class="sxs-lookup"><span data-stu-id="b914e-249">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="b914e-250">versão do jQuery 1.4.4</span><span class="sxs-lookup"><span data-stu-id="b914e-250">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="b914e-251">versão do jQuery 1.4.3</span><span class="sxs-lookup"><span data-stu-id="b914e-251">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="b914e-252">versão do jQuery 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b914e-252">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="b914e-253">versão 1.4.1 do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-253">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="b914e-254">jQuery versão 1.4</span><span class="sxs-lookup"><span data-stu-id="b914e-254">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="b914e-255">jQuery versão 1.3.2</span><span class="sxs-lookup"><span data-stu-id="b914e-255">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="b914e-256">Versões de migrar do jQuery no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-256">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="b914e-257">As seguintes versões do jQuery as migrações são hospedadas na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-257">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="b914e-258">jQuery versão 3.0.0 as migrações</span><span class="sxs-lookup"><span data-stu-id="b914e-258">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="b914e-259">jQuery versão 1.2.1 as migrações</span><span class="sxs-lookup"><span data-stu-id="b914e-259">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="b914e-260">Migrar a versão 1.2.0 do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-260">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="b914e-261">jQuery versão 1.1.1 as migrações</span><span class="sxs-lookup"><span data-stu-id="b914e-261">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="b914e-262">Migrar a versão 1.1.0 do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-262">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="b914e-263">Migrar a versão 1.0.0 do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-263">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="b914e-264">Versões de interface do usuário na CDN do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-264">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="b914e-265">As seguintes versões da biblioteca de interface do usuário do jQuery são hospedadas em deste CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-265">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="b914e-266">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b914e-266">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b914e-267">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="b914e-267">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-268">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b914e-268">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-269">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="b914e-269">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-270">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="b914e-270">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-271">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="b914e-271">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-272">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b914e-272">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-273">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b914e-273">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-274">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="b914e-274">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-275">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="b914e-275">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-276">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="b914e-276">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "jQuery UI 1.10.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-277">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="b914e-277">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-278">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b914e-278">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-279">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="b914e-279">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-280">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b914e-280">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-281">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b914e-281">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-282">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="b914e-282">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-283">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="b914e-283">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-284">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="b914e-284">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-285">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="b914e-285">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-286">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="b914e-286">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-287">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="b914e-287">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-288">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="b914e-288">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-289">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="b914e-289">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-290">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="b914e-290">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-291">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="b914e-291">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-292">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="b914e-292">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-293">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="b914e-293">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-294">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="b914e-294">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-295">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="b914e-295">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-296">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="b914e-296">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-297">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="b914e-297">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-298">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="b914e-298">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-299">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="b914e-299">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-300">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="b914e-300">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-301">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="b914e-301">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="b914e-302">Versões de validação na CDN do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-302">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="b914e-303">As seguintes versões da biblioteca de validação do jQuery são hospedadas em deste CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-303">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="b914e-304">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b914e-304">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b914e-305">jQuery Validate 1.19.0</span><span class="sxs-lookup"><span data-stu-id="b914e-305">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "1.19.0 de validação do jQuery")
- [<span data-ttu-id="b914e-306">jQuery Validate 1.17.0</span><span class="sxs-lookup"><span data-stu-id="b914e-306">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "1.17.0 de validação do jQuery")
- [<span data-ttu-id="b914e-307">jQuery Validate 1.16.0</span><span class="sxs-lookup"><span data-stu-id="b914e-307">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "validação do jQuery 1.16.0")
- [<span data-ttu-id="b914e-308">jQuery Validate 1.15.1</span><span class="sxs-lookup"><span data-stu-id="b914e-308">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "validação do jQuery 1.15.1")
- [<span data-ttu-id="b914e-309">jQuery Validate 1.15.0</span><span class="sxs-lookup"><span data-stu-id="b914e-309">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "validação do jQuery 1.15.0")
- [<span data-ttu-id="b914e-310">jQuery Validate 1.14.0</span><span class="sxs-lookup"><span data-stu-id="b914e-310">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "validação do jQuery 1.14.0")
- [<span data-ttu-id="b914e-311">jQuery Validate 1.13.1</span><span class="sxs-lookup"><span data-stu-id="b914e-311">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "validação do jQuery 1.13.1")
- [<span data-ttu-id="b914e-312">jQuery Validate 1.13.0</span><span class="sxs-lookup"><span data-stu-id="b914e-312">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "validação do jQuery 1.13.0")
- [<span data-ttu-id="b914e-313">jQuery Validate 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b914e-313">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "validação do jQuery 1.12.0")
- [<span data-ttu-id="b914e-314">jQuery Validate 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b914e-314">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "validação do jQuery 1.11.1")
- [<span data-ttu-id="b914e-315">jQuery Validate 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b914e-315">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "validação do jQuery 1.11.0")
- [<span data-ttu-id="b914e-316">jQuery Validate 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b914e-316">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "validação do jQuery 1.10.0")
- [<span data-ttu-id="b914e-317">jQuery Validate 1.9</span><span class="sxs-lookup"><span data-stu-id="b914e-317">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jQuery. Validate versão 1.9")
- [<span data-ttu-id="b914e-318">jQuery Validate 1.8.1</span><span class="sxs-lookup"><span data-stu-id="b914e-318">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jQuery. Validate versão 1.8.1")
- [<span data-ttu-id="b914e-319">jQuery Validate 1.8</span><span class="sxs-lookup"><span data-stu-id="b914e-319">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jQuery. Validate versão 1.8")
- [<span data-ttu-id="b914e-320">jQuery Validate 1.7</span><span class="sxs-lookup"><span data-stu-id="b914e-320">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jQuery. Validate versão 1.7")
- [<span data-ttu-id="b914e-321">Validar jQuery 1.6</span><span class="sxs-lookup"><span data-stu-id="b914e-321">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "validar jQuery 1.6")
- [<span data-ttu-id="b914e-322">Validar jQuery 1.5.5</span><span class="sxs-lookup"><span data-stu-id="b914e-322">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "validar jQuery 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="b914e-323">jQuery Mobile de versões no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-323">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="b914e-324">As seguintes versões da biblioteca jQuery Mobile são hospedadas nesta CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-324">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="b914e-325">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b914e-325">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b914e-326">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="b914e-326">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-327">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b914e-327">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-328">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="b914e-328">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-329">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="b914e-329">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-330">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="b914e-330">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-331">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="b914e-331">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-332">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="b914e-332">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-333">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="b914e-333">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-334">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="b914e-334">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-335">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b914e-335">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-336">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b914e-336">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-337">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="b914e-337">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-338">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b914e-338">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-339">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="b914e-339">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-340">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="b914e-340">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "jQuery Mobile 1.0 RC2 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-341">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="b914e-341">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "jQuery Mobile 1.0 RC1 na CDN do Microsoft Ajax")
- [<span data-ttu-id="b914e-342">versão beta do jQuery Mobile 1.0 3</span><span class="sxs-lookup"><span data-stu-id="b914e-342">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "jQuery Mobile 1.0 Beta 3 na CDN do Microsoft Ajax")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="b914e-343">Versões de modelos na CDN do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-343">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="b914e-344">As seguintes versões do plug-in do jQuery Templates são hospedadas nesta CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-344">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="b914e-345">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b914e-345">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b914e-346">Modelos jQuery Beta 1</span><span class="sxs-lookup"><span data-stu-id="b914e-346">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "modelos jQuery Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="b914e-347">Ciclo de lançamentos na CDN do jQuery</span><span class="sxs-lookup"><span data-stu-id="b914e-347">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="b914e-348">As seguintes versões do plug-in do jQuery Cycle são hospedadas nesta CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-348">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="b914e-349">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b914e-349">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b914e-350">jQuery ciclo 2.99</span><span class="sxs-lookup"><span data-stu-id="b914e-350">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery 2.99 ciclo")
- [<span data-ttu-id="b914e-351">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="b914e-351">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="b914e-352">jQuery ciclo 2,88</span><span class="sxs-lookup"><span data-stu-id="b914e-352">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery 2,88 ciclo")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="b914e-353">jQuery DataTables versões na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-353">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="b914e-354">As seguintes versões do plug-in jQuery DataTables são hospedadas em deste CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-354">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="b914e-355">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b914e-355">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b914e-356">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="b914e-356">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="b914e-357">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="b914e-357">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="b914e-358">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="b914e-358">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="b914e-359">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="b914e-359">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="b914e-360">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="b914e-360">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="b914e-361">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b914e-361">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="b914e-362">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b914e-362">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="b914e-363">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="b914e-363">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="b914e-364">Versões do Modernizr na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-364">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="b914e-365">As seguintes versões do [Modernizr](http://www.modernizr.com "Modernizr") são hospedados na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-365">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="b914e-366">Versões de JSHint na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-366">JSHint Releases on the CDN</span></span>

<span data-ttu-id="b914e-367">As seguintes versões do [JSHint](http://www.jshint.com "JSHint") são hospedados na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-367">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="b914e-368">Versões do Knockout na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-368">Knockout Releases on the CDN</span></span>

<span data-ttu-id="b914e-369">As seguintes versões do [Knockout](http://www.knockoutjs.com "Knockout") são hospedados na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-369">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

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

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="b914e-370">Globalizar versões na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-370">Globalize Releases on the CDN</span></span>

<span data-ttu-id="b914e-371">As seguintes versões do [Globalize](https://github.com/jquery/globalize "Globalize") são hospedados na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-371">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="b914e-372">Globalizar versão 1.0.0</span><span class="sxs-lookup"><span data-stu-id="b914e-372">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="b914e-373">Globalizar versão 0.1.1</span><span class="sxs-lookup"><span data-stu-id="b914e-373">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="b914e-374">todas as culturas</span><span class="sxs-lookup"><span data-stu-id="b914e-374">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="b914e-375">Substitua "{-código de cultura}" com o código de cultura desejada, por exemplo, a Microsoft globalize.culture.en GB.js== arquivos na CDN do = = essas bibliotecas foram carregadas pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b914e-375">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="b914e-376">Responder a versões na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-376">Respond Releases on the CDN</span></span>

<span data-ttu-id="b914e-377">As seguintes versões do [ https://github.com/scottjehl/Respond ] (https://github.com/scottjehl/Respond " https://github.com/scottjehl/Respond ") responder são hospedados na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-377">The following releases of [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") Respond are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="b914e-378">Responder a versão 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b914e-378">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="b914e-379">Responder a versão 1.4.1</span><span class="sxs-lookup"><span data-stu-id="b914e-379">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="b914e-380">Responder a versão 1.4.0</span><span class="sxs-lookup"><span data-stu-id="b914e-380">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="b914e-381">Responder a versão 1.3.0</span><span class="sxs-lookup"><span data-stu-id="b914e-381">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="b914e-382">Responder a versão 1.2.0</span><span class="sxs-lookup"><span data-stu-id="b914e-382">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="b914e-383">Versões de bootstrap na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-383">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="b914e-384">As seguintes versões do [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") hospedados na CDN do bootstrap:</span><span class="sxs-lookup"><span data-stu-id="b914e-384">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-421"></a><span data-ttu-id="b914e-385">Inicializar versão 4.2.1</span><span class="sxs-lookup"><span data-stu-id="b914e-385">Bootstrap version 4.2.1</span></span>

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

#### <a name="bootstrap-version-411"></a><span data-ttu-id="b914e-386">Versão bootstrap 4.1.1</span><span class="sxs-lookup"><span data-stu-id="b914e-386">Bootstrap version 4.1.1</span></span>

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

#### <a name="bootstrap-version-400"></a><span data-ttu-id="b914e-387">Inicializar versão 4.0.0</span><span class="sxs-lookup"><span data-stu-id="b914e-387">Bootstrap version 4.0.0</span></span>

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

#### <a name="bootstrap-version-340"></a><span data-ttu-id="b914e-388">Inicializar versão 3.4.0</span><span class="sxs-lookup"><span data-stu-id="b914e-388">Bootstrap version 3.4.0</span></span>

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

#### <a name="bootstrap-version-337"></a><span data-ttu-id="b914e-389">Versão bootstrap 3.3.7</span><span class="sxs-lookup"><span data-stu-id="b914e-389">Bootstrap version 3.3.7</span></span>

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

#### <a name="bootstrap-version-336"></a><span data-ttu-id="b914e-390">Versão bootstrap 3.3.6</span><span class="sxs-lookup"><span data-stu-id="b914e-390">Bootstrap version 3.3.6</span></span>

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

#### <a name="bootstrap-version-335"></a><span data-ttu-id="b914e-391">Versão bootstrap 3.3.5</span><span class="sxs-lookup"><span data-stu-id="b914e-391">Bootstrap version 3.3.5</span></span>

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

#### <a name="bootstrap-version-334"></a><span data-ttu-id="b914e-392">Versão bootstrap 3.3.4</span><span class="sxs-lookup"><span data-stu-id="b914e-392">Bootstrap version 3.3.4</span></span>

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

#### <a name="bootstrap-version-332"></a><span data-ttu-id="b914e-393">Versão bootstrap 3.3.2</span><span class="sxs-lookup"><span data-stu-id="b914e-393">Bootstrap version 3.3.2</span></span>

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

#### <a name="bootstrap-version-331"></a><span data-ttu-id="b914e-394">Versão bootstrap 3.3.1</span><span class="sxs-lookup"><span data-stu-id="b914e-394">Bootstrap version 3.3.1</span></span>

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

#### <a name="bootstrap-version-330"></a><span data-ttu-id="b914e-395">Inicializar a versão 3.3.0</span><span class="sxs-lookup"><span data-stu-id="b914e-395">Bootstrap version 3.3.0</span></span>

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

#### <a name="bootstrap-version-320"></a><span data-ttu-id="b914e-396">Versão bootstrap 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b914e-396">Bootstrap version 3.2.0</span></span>

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

#### <a name="bootstrap-version-311"></a><span data-ttu-id="b914e-397">Versão bootstrap 3.1.1</span><span class="sxs-lookup"><span data-stu-id="b914e-397">Bootstrap version 3.1.1</span></span>

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

#### <a name="bootstrap-version-310"></a><span data-ttu-id="b914e-398">Inicializar versão 3.1.0</span><span class="sxs-lookup"><span data-stu-id="b914e-398">Bootstrap version 3.1.0</span></span>

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

#### <a name="bootstrap-version-303"></a><span data-ttu-id="b914e-399">Versão bootstrap 3.0.3</span><span class="sxs-lookup"><span data-stu-id="b914e-399">Bootstrap version 3.0.3</span></span>

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

#### <a name="bootstrap-version-302"></a><span data-ttu-id="b914e-400">Versão bootstrap 3.0.2</span><span class="sxs-lookup"><span data-stu-id="b914e-400">Bootstrap version 3.0.2</span></span>

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

#### <a name="bootstrap-version-301"></a><span data-ttu-id="b914e-401">Inicializar versão 3.0.1</span><span class="sxs-lookup"><span data-stu-id="b914e-401">Bootstrap version 3.0.1</span></span>

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

#### <a name="bootstrap-version-300"></a><span data-ttu-id="b914e-402">Inicializar versão 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b914e-402">Bootstrap version 3.0.0</span></span>

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

#### <a name="bootstrap-version-232"></a><span data-ttu-id="b914e-403">Versão 2.3.2 do Bootstrap</span><span class="sxs-lookup"><span data-stu-id="b914e-403">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="b914e-404">Inicializar versão 2.3.1</span><span class="sxs-lookup"><span data-stu-id="b914e-404">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="b914e-405">Versões de bootstrap TouchCarousel na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-405">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="b914e-406">As seguintes versões do [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") versões de Bootstrap TouchCarousel são hospedados na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-406">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="b914e-407">Bootstrap TouchCarousel versão 0.8.0</span><span class="sxs-lookup"><span data-stu-id="b914e-407">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="b914e-408">Versões de hammer.js na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-408">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="b914e-409">As seguintes versões do [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js versões são hospedados na CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-409">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="b914e-410">Hammer.js versão 2.0.4</span><span class="sxs-lookup"><span data-stu-id="b914e-410">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="b914e-411">Web Forms do ASP.NET e Ajax versões na CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-411">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="b914e-412">As seguintes versões da biblioteca do Ajax ASP.NET são hospedadas na CDN.</span><span class="sxs-lookup"><span data-stu-id="b914e-412">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="b914e-413">Clique em cada link para ver a lista real de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b914e-413">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b914e-414">Versão do ASP.NET Web Forms e Ajax 4.5.2</span><span class="sxs-lookup"><span data-stu-id="b914e-414">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "Web Forms do ASP.NET e Ajax 4.5.2")
- [<span data-ttu-id="b914e-415">Versão do ASP.NET Web Forms e Ajax 4</span><span class="sxs-lookup"><span data-stu-id="b914e-415">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "Web Forms do ASP.NET e Ajax 4")
- [<span data-ttu-id="b914e-416">Versão 3.5 do ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="b914e-416">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="b914e-417">Versões do ASP.NET MVC no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-417">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="b914e-418">Os seguintes arquivos JavaScript do ASP.NET MVC são hospedados em deste CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-418">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="b914e-419">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="b914e-419">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="b914e-420">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="b914e-420">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="b914e-421">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="b914e-421">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="b914e-422">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="b914e-422">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="b914e-423">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="b914e-423">ASP.NET MVC 3.0</span></span>

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

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="b914e-424">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="b914e-424">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="b914e-425">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="b914e-425">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="b914e-426">Versões do ASP.NET SignalR no CDN</span><span class="sxs-lookup"><span data-stu-id="b914e-426">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="b914e-427">Os seguintes arquivos ASP.NET SignalR JavaScript são hospedados em deste CDN:</span><span class="sxs-lookup"><span data-stu-id="b914e-427">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="b914e-428">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="b914e-428">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="b914e-429">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b914e-429">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="b914e-430">SignalR do ASP.NET 2.2.0</span><span class="sxs-lookup"><span data-stu-id="b914e-430">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="b914e-431">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="b914e-431">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="b914e-432">SignalR do ASP.NET 2.0.3</span><span class="sxs-lookup"><span data-stu-id="b914e-432">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="b914e-433">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="b914e-433">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="b914e-434">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="b914e-434">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="b914e-435">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b914e-435">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="b914e-436">SignalR do ASP.NET 1.1.3</span><span class="sxs-lookup"><span data-stu-id="b914e-436">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="b914e-437">1.1.2 do ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="b914e-437">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="b914e-438">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b914e-438">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="b914e-439">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b914e-439">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="b914e-440">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b914e-440">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="b914e-441">Para obter informações sobre os termos de uso para o CDN, consulte [Ajax CDN termos de uso do Microsoft](https://www.asp.net/terms-of-use "Ajax CDN termos de uso do Microsoft").</span><span class="sxs-lookup"><span data-stu-id="b914e-441">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>