---
uid: whitepapers/side-by-side-with-10
title: ASP.NET a execução lado a lado de .NET Framework 1,0 e 1,1 | Microsoft Docs
author: rick-anderson
description: Este white paper descreve como instalar o .NET 1,0 e o .NET 1,1 em seu computador, permitindo que um aplicativo Web ASP.NET seja executado em qualquer uma das versões do fram...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632968"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="8b923-103">Execução lado a lado do ASP.NET no .NET Framework 1.0 e 1.1</span><span class="sxs-lookup"><span data-stu-id="8b923-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="8b923-104">Este white paper descreve como instalar o .NET 1,0 e o .NET 1,1 em seu computador, permitindo que um aplicativo Web ASP.NET seja executado em qualquer uma das versões do Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="8b923-105">Aplica-se a ASP.NET 1,0 e ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="8b923-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="8b923-106">No ASP.NET, os aplicativos são considerados em execução lado a lado quando são instalados no mesmo computador, mas usam versões diferentes do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="8b923-107">O tópico a seguir descreve como configurar aplicativos ASP.NET para execução lado a lado e fornece etapas detalhadas para:</span><span class="sxs-lookup"><span data-stu-id="8b923-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="8b923-108">Manter o mapeamento do aplicativo Web para .NET Framework versão 1,0 durante a instalação</span><span class="sxs-lookup"><span data-stu-id="8b923-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="8b923-109">Mapear um aplicativo Web para uma versão específica do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8b923-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="8b923-110">Localizar a versão do .NET Framework que um site está usando</span><span class="sxs-lookup"><span data-stu-id="8b923-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="8b923-111">Tradicionalmente, quando um componente ou aplicativo é atualizado em um computador, a versão mais antiga é removida e substituída pela versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="8b923-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="8b923-112">Se a nova versão não for compatível com a versão anterior, isso geralmente interromperá outros aplicativos que usam o componente ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b923-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="8b923-113">O .NET Framework fornece suporte para a execução lado a lado, o que permite que várias versões de um assembly ou aplicativo sejam instaladas no mesmo computador ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="8b923-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="8b923-114">Como várias versões podem ser instaladas simultaneamente, os aplicativos gerenciados podem selecionar qual versão usar sem afetar os aplicativos que usam uma versão diferente.</span><span class="sxs-lookup"><span data-stu-id="8b923-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="8b923-115">Por padrão, durante a instalação da versão 1,1 do .NET Framework, todos os aplicativos ASP.NET existentes são automaticamente reconfigurados para usar a versão mais recente do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="8b923-116">Se você não quiser que seus aplicativos ASP.NET sejam padronizados para .NET Framework 1,1, clique [aqui](#1) para saber como evitar isso durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="8b923-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="8b923-117">Se você atualizar seu servidor Web para .NET Framework 1,1 e desejar que um ou mais aplicativos Web sejam executados .NET Framework 1,0, você precisará atualizar o mapa de script do Serviços de Informações da Internet (IIS).</span><span class="sxs-lookup"><span data-stu-id="8b923-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="8b923-118">O mapeamento de script é o mecanismo para mapear a extensão de arquivo. aspx para um aplicativo Web específico para uma versão do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="8b923-119">Clique [aqui](#2) para saber como mapear um aplicativo Web para uma versão específica do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="8b923-120">Você pode usar o Gerenciador de informações da Internet ou a ferramenta de registro do ASP.NET IIS (ASPNET\_regiis. exe) para descobrir qual versão do .NET Framework está executando um aplicativo Web específico.</span><span class="sxs-lookup"><span data-stu-id="8b923-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="8b923-121">Clique [aqui](#3) para saber como localizar a versão do .NET Framework que um site da Web está usando.</span><span class="sxs-lookup"><span data-stu-id="8b923-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="8b923-122">Uma consideração de importação ao migrar para o .NET Framework 1,1 é que cada versão do .NET Framework usa seu próprio arquivo Machine. config.</span><span class="sxs-lookup"><span data-stu-id="8b923-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="8b923-123">Como resultado, se um administrador da Web tiver feito alterações no arquivo Machine. config, essas alterações deverão ser migradas para o arquivo Machine. config do .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="8b923-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="8b923-124">Manter o mapeamento do aplicativo Web para .NET Framework 1,0 durante a instalação</span><span class="sxs-lookup"><span data-stu-id="8b923-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="8b923-125">Por padrão, todos os aplicativos ASP.NET existentes são reconfigurados automaticamente durante a instalação para usar a versão mais recente do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="8b923-126">Usando a versão mais recente do .NET Framework, os aplicativos podem aproveitar ao máximo os aprimoramentos e os novos recursos incluídos na nova versão.</span><span class="sxs-lookup"><span data-stu-id="8b923-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="8b923-127">Ao mesmo tempo, o administrador da Web, que pode querer ter um controle granular sobre quais aplicativos são atualizados, pode impedir o remapeamento automático de todos os aplicativos ASP.NET existentes durante a instalação do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="8b923-128">Para evitar o remapeamento automático de todo o aplicativo ASP.NET para a versão mais recente do .NET Framework, o administrador da Web pode usar a opção de linha de comando/noaspupgrade com o programa de instalação do Dotnetfx. exe.</span><span class="sxs-lookup"><span data-stu-id="8b923-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="8b923-129">**Para evitar o remapeamento total do aplicativo ASP.NET para uma versão mais recente**</span><span class="sxs-lookup"><span data-stu-id="8b923-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="8b923-130">Vá para **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="8b923-130">Go to **Start**.</span></span>
2. <span data-ttu-id="8b923-131">Clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="8b923-131">Click on **run**.</span></span>
3. <span data-ttu-id="8b923-132">Digite **cmd**.</span><span class="sxs-lookup"><span data-stu-id="8b923-132">Type **cmd**.</span></span>
4. <span data-ttu-id="8b923-133">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b923-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="8b923-134">No prompt de comando, digite a seguinte linha para iniciar a instalação do .NET Framework: **Dotnetfx. exe/c: "instalar o/noaspupgrade?** .</span><span class="sxs-lookup"><span data-stu-id="8b923-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="8b923-135">Clique em **Sim** na instalação do Microsoft .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="8b923-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="8b923-136">Isso iniciará o processo de instalação do .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="8b923-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="8b923-137">Mapear um aplicativo Web para uma versão específica do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8b923-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="8b923-138">Cada versão do .NET Framework inclui uma versão da ferramenta de registro do IIS do ASP.NET (ASPNET\_regiis. exe).</span><span class="sxs-lookup"><span data-stu-id="8b923-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="8b923-139">Essa ferramenta permite que os administradores especifiquem que um aplicativo Web seja executado em uma versão específica do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="8b923-140">Isso é conhecido como mapeamento de um aplicativo Web para uma versão do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b923-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="8b923-141">Os administradores devem selecionar o ASPNET\_regiis. exe que corresponde à versão do .NET Framework que será associado ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8b923-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="8b923-142">Por exemplo, um administrador que deseja especificar que um site usa .NET Framework 1,1 deve usar o ASPNET\_regiis. exe que vem com .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="8b923-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="8b923-143">O ASPNET\_regiis. exe para a versão 1,0 está localizado em:</span><span class="sxs-lookup"><span data-stu-id="8b923-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="8b923-144">C:\WINDOWS\Microsoft.NET\Framework\\**v 1.0.3705**\ASPNET\_regiis</span><span class="sxs-lookup"><span data-stu-id="8b923-144">C:\WINDOWS\Microsoft.NET\Framework\\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="8b923-145">O ASPNET\_regiis. exe para a versão 1, 1 está localizado em:</span><span class="sxs-lookup"><span data-stu-id="8b923-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="8b923-146">C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\ASPNET\_regiis</span><span class="sxs-lookup"><span data-stu-id="8b923-146">C:\WINDOWS\Microsoft.NET\Framework\\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="8b923-147">O ASPNET\_regiis. exe fornece duas opções para o mapeamento de script de um aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="8b923-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="8b923-148">**-s** define o mapa de script no caminho e em seus diretórios filho.</span><span class="sxs-lookup"><span data-stu-id="8b923-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="8b923-149">**-SN** define o mapa de script somente no caminho.</span><span class="sxs-lookup"><span data-stu-id="8b923-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="8b923-150">O caminho define o caminho de metadados do IIS do aplicativo Web, que é definido na forma de W3SVC/ROOT/{WebSiteNumber}/{nome do aplicativo\_}.</span><span class="sxs-lookup"><span data-stu-id="8b923-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="8b923-151">Por exemplo, para um aplicativo Web chamado portal localizado no site da Web padrão, o caminho da metabase é W3SVC/1/ROOT/Portal.</span><span class="sxs-lookup"><span data-stu-id="8b923-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="8b923-152">Observação Você também pode usar uma ferramenta chamada editor de metabase para obter o caminho da metabase.</span><span class="sxs-lookup"><span data-stu-id="8b923-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="8b923-153">Você pode baixar essa ferramenta no site do Suporte da Microsoft em [https://support.microsoft.com/default.aspx?scid=kb; en-US; 232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span><span class="sxs-lookup"><span data-stu-id="8b923-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="8b923-154">Execute ASPNET\_Regiss. exe-s W3SVC/1/ROOT/portal para atualizar o mapa de script do IIS do portal e seu subaplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b923-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="8b923-155">Execute ASPNET\_regiry. exe-SN W3SVC/1/ROOT/portal para atualizar o mapa de script do IIS do portal, sem afetar os aplicativos nos subdiretórios do portal? s.</span><span class="sxs-lookup"><span data-stu-id="8b923-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="8b923-156">Localizar a versão de .NET Framework que um aplicativo Web está usando</span><span class="sxs-lookup"><span data-stu-id="8b923-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="8b923-157">Um administrador pode usar o Service Manager da Internet para descobrir qual versão do .NET Framework executa um site.</span><span class="sxs-lookup"><span data-stu-id="8b923-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="8b923-158">Versões diferentes do sistema operacional iniciam a Internet Service Manager de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="8b923-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="8b923-159">Para iniciar o Service Manager, siga as etapas listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="8b923-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="8b923-160">**Para iniciar o Internet Service Manager**</span><span class="sxs-lookup"><span data-stu-id="8b923-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="8b923-161">Vá para **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="8b923-161">Go to **Start**.</span></span>
2. <span data-ttu-id="8b923-162">Clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="8b923-162">Click on **run**.</span></span>
3. <span data-ttu-id="8b923-163">Digite **inetmgr**.</span><span class="sxs-lookup"><span data-stu-id="8b923-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="8b923-164">Na Service Manager da Internet, selecione o aplicativo Web cuja versão do .NET Framework você deseja saber.</span><span class="sxs-lookup"><span data-stu-id="8b923-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="8b923-165">Clique com o botão direito do mouse no aplicativo Web e clique em **Propriedades.**</span><span class="sxs-lookup"><span data-stu-id="8b923-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="8b923-166">Na janela de propriedades, selecione **configuração.**</span><span class="sxs-lookup"><span data-stu-id="8b923-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="8b923-167">Na tabela de mapeamento de aplicativos, selecione **. aspx**e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="8b923-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="8b923-168">Na caixa de texto **executável** , examine o diretório da versão rolando.</span><span class="sxs-lookup"><span data-stu-id="8b923-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="8b923-169">Se o diretório da versão for v. 1.1.4322, o aplicativo será mapeado para .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="8b923-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="8b923-170">Por outro lado, se o diretório da versão for v 1.0.3705, o aplicativo será mapeado para .NET Framework 1,0.</span><span class="sxs-lookup"><span data-stu-id="8b923-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
