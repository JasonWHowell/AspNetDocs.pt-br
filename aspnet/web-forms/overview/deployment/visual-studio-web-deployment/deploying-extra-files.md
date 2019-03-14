---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'Implantação da Web do ASP.NET usando o Visual Studio: Implantando arquivos extras | Microsoft Docs'
author: tdykstra
description: Esta série de tutoriais mostra como implantar (publicar) um ASP.NET web de aplicativo para aplicativos de Web do serviço de aplicativo do Azure ou para um provedor de hospedagem de terceiros, usin...
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: 42b9089ba0662cf0912d2b637edec98f59c69927
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063463"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a><span data-ttu-id="d7552-103">Implantação da Web do ASP.NET usando o Visual Studio: Implantação de arquivos extras</span><span class="sxs-lookup"><span data-stu-id="d7552-103">ASP.NET Web Deployment using Visual Studio: Deploying Extra Files</span></span>
====================
<span data-ttu-id="d7552-104">por [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d7552-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d7552-105">Baixe o projeto inicial</span><span class="sxs-lookup"><span data-stu-id="d7552-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="d7552-106">Esta série de tutoriais mostra como implantar (publicar) um ASP.NET web application para aplicativos de Web do serviço de aplicativo do Azure ou para um provedor de hospedagem de terceiros, usando o Visual Studio 2012 ou Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="d7552-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="d7552-107">Para obter informações sobre a série, consulte [o primeiro tutorial na série](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7552-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="d7552-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d7552-108">Overview</span></span>

<span data-ttu-id="d7552-109">Este tutorial mostra como estender o Visual Studio web publicar pipeline para fazer uma tarefa adicional durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="d7552-109">This tutorial shows how to extend the Visual Studio web publish pipeline to do an additional task during deployment.</span></span> <span data-ttu-id="d7552-110">A tarefa é copiar os arquivos extras que não estão na pasta do projeto para o site de destino.</span><span class="sxs-lookup"><span data-stu-id="d7552-110">The task is to copy extra files that are not in the project folder to the destination web site.</span></span>

<span data-ttu-id="d7552-111">Para este tutorial, você copiará um arquivo extra: *robots*.</span><span class="sxs-lookup"><span data-stu-id="d7552-111">For this tutorial you'll copy one extra file: *robots.txt*.</span></span> <span data-ttu-id="d7552-112">Você deseja implantar esse arquivo para o preparo, mas não para produção.</span><span class="sxs-lookup"><span data-stu-id="d7552-112">You want to deploy this file to staging but not to production.</span></span> <span data-ttu-id="d7552-113">Na [a implantação para produção](deploying-to-production.md) tutorial, você adicionou esse arquivo ao projeto e configurou a produção publicar perfil para excluí-la.</span><span class="sxs-lookup"><span data-stu-id="d7552-113">In [the Deploying to Production](deploying-to-production.md) tutorial, you added this file to the project and configured the Production publish profile to exclude it.</span></span> <span data-ttu-id="d7552-114">Neste tutorial, você verá um método alternativo para lidar com essa situação, o que será útil para todos os arquivos que você deseja implantar, mas não deseja incluir no projeto.</span><span class="sxs-lookup"><span data-stu-id="d7552-114">In this tutorial you'll see an alternative method to handle this situation, one that will be useful for any files that you want to deploy but don't want to include in the project.</span></span>

## <a name="move-the-robotstxt-file"></a><span data-ttu-id="d7552-115">Mover o arquivo robots.</span><span class="sxs-lookup"><span data-stu-id="d7552-115">Move the robots.txt file</span></span>

<span data-ttu-id="d7552-116">Para se preparar para um método diferente de manipulação *robots*nesta seção do tutorial, você mover o arquivo para uma pasta que não está incluída no projeto e você excluir *robots* do preparo ambiente.</span><span class="sxs-lookup"><span data-stu-id="d7552-116">To prepare for a different method of handling *robots.txt*, in this section of the tutorial you move the file to a folder that is not included in the project, and you delete *robots.txt* from the staging environment.</span></span> <span data-ttu-id="d7552-117">É necessário excluir o arquivo de preparo para que você possa verificar se o novo método de implantação do arquivo para o ambiente está funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="d7552-117">It is necessary to delete the file from staging so that you can verify that your new method of deploying the file to that environment is working correctly.</span></span>

1. <span data-ttu-id="d7552-118">No **Gerenciador de soluções**, clique com botão direito do *robots* de arquivo e clique em **excluir do projeto**.</span><span class="sxs-lookup"><span data-stu-id="d7552-118">In **Solution Explorer**, right-click the *robots.txt* file and click **Exclude From Project**.</span></span>
2. <span data-ttu-id="d7552-119">Usando o Explorador de arquivos do Windows, crie uma nova pasta na pasta da solução e nomeie- *ExtraFiles*.</span><span class="sxs-lookup"><span data-stu-id="d7552-119">Using Windows File Explorer, create a new folder in the solution folder and name it *ExtraFiles*.</span></span>
3. <span data-ttu-id="d7552-120">Mover o *robots* arquivo o *ContosoUniversity* pasta do projeto para o *ExtraFiles* pasta.</span><span class="sxs-lookup"><span data-stu-id="d7552-120">Move the *robots.txt* file from the *ContosoUniversity* project folder to the *ExtraFiles* folder.</span></span>

    ![Pasta ExtraFiles](deploying-extra-files/_static/image1.png)
4. <span data-ttu-id="d7552-122">Usando a ferramenta FTP, exclua o *robots* arquivo a partir do site de preparo.</span><span class="sxs-lookup"><span data-stu-id="d7552-122">Using your FTP tool, delete the *robots.txt* file from the staging web site.</span></span>

    <span data-ttu-id="d7552-123">Como alternativa, você pode selecionar **remover arquivos adicionais no destino** sob **opções de publicação do arquivo** sobre o **configurações** guia do perfil de publicação de preparo, e publicar novamente para o preparo.</span><span class="sxs-lookup"><span data-stu-id="d7552-123">As an alternative, you can select **Remove additional files at destination** under **File Publish Options** on the **Settings** tab of the Staging publish profile, and republish to staging.</span></span>

## <a name="update-the-publish-profile-file"></a><span data-ttu-id="d7552-124">Atualizar o arquivo de perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="d7552-124">Update the publish profile file</span></span>

<span data-ttu-id="d7552-125">Você só precisa *robots* no preparo, portanto, o perfil de publicação única, você precisará atualizar para implantá-lo é de preparo.</span><span class="sxs-lookup"><span data-stu-id="d7552-125">You only need *robots.txt* in staging, so the only publish profile you need to update in order to deploy it is Staging.</span></span>

1. <span data-ttu-id="d7552-126">No Visual Studio, abra *Staging.pubxml*.</span><span class="sxs-lookup"><span data-stu-id="d7552-126">In Visual Studio, open *Staging.pubxml*.</span></span>
2. <span data-ttu-id="d7552-127">No final do arquivo, antes do fechamento `</Project>` marca, adicione a seguinte marcação:</span><span class="sxs-lookup"><span data-stu-id="d7552-127">At the end of the file, before the closing `</Project>` tag, add the following markup:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    <span data-ttu-id="d7552-128">Esse código cria uma nova *destino* que irá coletar arquivos adicionais a serem implantados.</span><span class="sxs-lookup"><span data-stu-id="d7552-128">This code creates a new *target* that will collect additional files to be deployed.</span></span> <span data-ttu-id="d7552-129">Um destino é composto de um ou mais tarefas MSBuild serão executadas com base nas condições especificadas.</span><span class="sxs-lookup"><span data-stu-id="d7552-129">A target is composed of one or more tasks that MSBuild will execute based on conditions you specify.</span></span>

    <span data-ttu-id="d7552-130">O `Include` atributo especifica que a pasta na qual localizar os arquivos *ExtraFiles*, localizado no mesmo nível que a pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="d7552-130">The `Include` attribute specifies that the folder in which to find the files is *ExtraFiles*, located at the same level as the project folder.</span></span> <span data-ttu-id="d7552-131">MSBuild coletará todos os arquivos dessa pasta e recursivamente de todas as subpastas (o asterisco duplo Especifica subpastas recursivas).</span><span class="sxs-lookup"><span data-stu-id="d7552-131">MSBuild will collect all files from that folder and recursively from any subfolders (the double asterisk specifies recursive subfolders).</span></span> <span data-ttu-id="d7552-132">Com esse código, você pode colocar vários arquivos e arquivos em subpastas dentro de *ExtraFiles* pasta e todos serão implantados.</span><span class="sxs-lookup"><span data-stu-id="d7552-132">With this code you could put multiple files, and files in subfolders inside the *ExtraFiles* folder, and all will be deployed.</span></span>

    <span data-ttu-id="d7552-133">O `DestinationRelativePath` elemento Especifica que os arquivos e pastas devem ser copiados para a pasta raiz do site da web de destino, na mesma estrutura de arquivo e pasta conforme forem encontradas em de *ExtraFiles* pasta.</span><span class="sxs-lookup"><span data-stu-id="d7552-133">The `DestinationRelativePath` element specifies that the folders and files should be copied to the root folder of the destination web site, in the same file and folder structure as they are found in the *ExtraFiles* folder.</span></span> <span data-ttu-id="d7552-134">Se você quiser copiar o *ExtraFiles* pasta propriamente dita, o `DestinationRelativePath` valor seria *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span><span class="sxs-lookup"><span data-stu-id="d7552-134">If you wanted to copy the *ExtraFiles* folder itself, the `DestinationRelativePath` value would be *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span></span>
3. <span data-ttu-id="d7552-135">No final do arquivo, antes do fechamento `</Project>` marca, adicione a seguinte marcação que especifica quando executar o novo destino.</span><span class="sxs-lookup"><span data-stu-id="d7552-135">At the end of the file, before the closing `</Project>` tag, add the following markup that specifies when to execute the new target.</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    <span data-ttu-id="d7552-136">Esse código faz com que o novo `CustomCollectFiles` destino seja executado sempre que o destino que copia arquivos para a pasta de destino é executado.</span><span class="sxs-lookup"><span data-stu-id="d7552-136">This code causes the new `CustomCollectFiles` target to be executed whenever the target that copies files to the destination folder is executed.</span></span> <span data-ttu-id="d7552-137">Há um destino separado para publicar em comparação com a criação do pacote de implantação e o novo destino é injetado em ambos os destinos, caso você pretenda implantar por meio de um pacote de implantação, em vez de publicação.</span><span class="sxs-lookup"><span data-stu-id="d7552-137">There is a separate target for publish versus deployment package creation, and the new target is injected in both targets in case you decide to deploy by using a deployment package instead of publishing.</span></span>

    <span data-ttu-id="d7552-138">O *. pubxml* arquivo agora se parece com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d7552-138">The *.pubxml* file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. <span data-ttu-id="d7552-139">Salve e feche o *Staging.pubxml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="d7552-139">Save and close the *Staging.pubxml* file.</span></span>

## <a name="publish-to-staging"></a><span data-ttu-id="d7552-140">Publicar para o preparo</span><span class="sxs-lookup"><span data-stu-id="d7552-140">Publish to staging</span></span>

<span data-ttu-id="d7552-141">Usando um clique a publicação ou a linha de comando, publicar o aplicativo usando o perfil de preparo.</span><span class="sxs-lookup"><span data-stu-id="d7552-141">Using one-click publish or the command line, publish the application by using the Staging profile.</span></span>

<span data-ttu-id="d7552-142">Se você usar um clique em Publicar, você pode verificar a **versão prévia** janela que *robots* serão copiados.</span><span class="sxs-lookup"><span data-stu-id="d7552-142">If you use one-click publish, you can verify in the **Preview** window that *robots.txt* will be copied.</span></span> <span data-ttu-id="d7552-143">Caso contrário, use sua ferramenta FTP para verificar se o *robots* arquivo está na pasta raiz do site da web após a implantação.</span><span class="sxs-lookup"><span data-stu-id="d7552-143">Otherwise, use your FTP tool to verify that the *robots.txt* file is in the root folder of the web site after deployment.</span></span>

## <a name="summary"></a><span data-ttu-id="d7552-144">Resumo</span><span class="sxs-lookup"><span data-stu-id="d7552-144">Summary</span></span>

<span data-ttu-id="d7552-145">Isso conclui esta série de tutoriais sobre como implantar um aplicativo da web ASP.NET em um provedor de hospedagem de terceiros.</span><span class="sxs-lookup"><span data-stu-id="d7552-145">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="d7552-146">Para obter mais informações sobre qualquer um dos tópicos abordados nesses tutoriais, consulte o [mapa de conteúdo de implantação do ASP.NET](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span><span class="sxs-lookup"><span data-stu-id="d7552-146">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span></span>

## <a name="more-information"></a><span data-ttu-id="d7552-147">Mais informações</span><span class="sxs-lookup"><span data-stu-id="d7552-147">More information</span></span>

<span data-ttu-id="d7552-148">Se você souber como trabalhar com arquivos do MSBuild, você pode automatizar muitas outras tarefas de implantação, escrevendo código em *. pubxml* arquivos (para tarefas específicas de perfil) ou o projeto *. wpp.targets* arquivo (para as tarefas se aplicam a todos os perfis).</span><span class="sxs-lookup"><span data-stu-id="d7552-148">If you know how to work with MSBuild files, you can automate many other deployment tasks by writing code in *.pubxml* files (for profile-specific tasks) or the project *.wpp.targets* file (for tasks that apply to all profiles).</span></span> <span data-ttu-id="d7552-149">Para obter mais informações sobre *. pubxml* e *. wpp.targets* arquivos, consulte [como: Editar configurações de implantação em Publicar arquivos de perfil (. pubxml) e o. arquivo wpp.targets em projetos do Visual Studio Web](https://msdn.microsoft.com/library/ff398069).</span><span class="sxs-lookup"><span data-stu-id="d7552-149">For more information about *.pubxml* and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069).</span></span> <span data-ttu-id="d7552-150">Para obter uma introdução básica para o código do MSBuild, consulte **a anatomia de um arquivo de projeto** em [série sobre implantação corporativa: Noções básicas sobre o arquivo de projeto](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="d7552-150">For a basic introduction to MSBuild code, see **The Anatomy of a Project File** in [Enterprise Deployment Series: Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="d7552-151">Para saber como trabalhar com arquivos do MSBuild para executar tarefas para seus próprios cenários, consulte este livro: [Dentro do mecanismo de compilação da Microsoft: Usando MSBuild e o Team Foundation Build](http://msbuildbook.com) Sayed Ibraham Hashimi e William Bartholomew.</span><span class="sxs-lookup"><span data-stu-id="d7552-151">To learn how to work with MSBuild files to perform tasks for your own scenarios, see this book: [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://msbuildbook.com) by Sayed Ibraham Hashimi and William Bartholomew.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="d7552-152">Confirmações</span><span class="sxs-lookup"><span data-stu-id="d7552-152">Acknowledgements</span></span>

<span data-ttu-id="d7552-153">Eu gostaria de agradecer a pessoas que fizeram contribuições significativas para o conteúdo desta série de tutoriais:</span><span class="sxs-lookup"><span data-stu-id="d7552-153">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="d7552-154">Alberto Poblacion, MVP &amp; MCT, Espanha</span><span class="sxs-lookup"><span data-stu-id="d7552-154">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="d7552-155">Jarod Ferguson, MVP de desenvolvimento de plataforma de dados, dos Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="d7552-155">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="d7552-156">Harsh Mittal, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d7552-156">Harsh Mittal, Microsoft</span></span>
- <span data-ttu-id="d7552-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="d7552-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- [<span data-ttu-id="d7552-158">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d7552-158">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="d7552-159">Mike Pope, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d7552-159">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="d7552-160">Mohit Srivastava, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d7552-160">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="d7552-161">Raffaele Rialdi, Italy</span><span class="sxs-lookup"><span data-stu-id="d7552-161">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="d7552-162">Rick Anderson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d7552-162">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="d7552-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="d7552-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="d7552-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="d7552-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="d7552-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="d7552-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="d7552-166">Srđan Božović, Serbia</span><span class="sxs-lookup"><span data-stu-id="d7552-166">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="d7552-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="d7552-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d7552-168">[Anterior](command-line-deployment.md)
> [Próximo](troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="d7552-168">[Previous](command-line-deployment.md)
[Next](troubleshooting.md)</span></span>