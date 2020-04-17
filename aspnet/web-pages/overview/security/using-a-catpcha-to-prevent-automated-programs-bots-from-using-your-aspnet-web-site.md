---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Usando um site CAPTCHA para impedir que bots usem seu ASP.NET Web Razor) site | Microsoft Docs
author: rick-anderson
description: Este artigo explica como usar o ReCaptcha (uma medida de segurança) para impedir que programas automatizados (bots) realizem tarefas em uma ASP.NET Páginas da Web (Razor) nós...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543750"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="38068-103">Usando um site CAPTCHA para impedir que bots usem o seu ASP.NET Web Razor)</span><span class="sxs-lookup"><span data-stu-id="38068-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="38068-104">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="38068-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="38068-105">Este artigo explica como usar o ReCaptcha (uma medida de segurança) para impedir que programas automatizados (bots) realizem tarefas em um site de páginas da Web ASP.NET (Razor).</span><span class="sxs-lookup"><span data-stu-id="38068-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="38068-106">**O que você aprenderá:**</span><span class="sxs-lookup"><span data-stu-id="38068-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="38068-107">Como adicionar um teste CAPTCHA ao seu site.</span><span class="sxs-lookup"><span data-stu-id="38068-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="38068-108">Estas são as ASP.NET características introduzidas no artigo:</span><span class="sxs-lookup"><span data-stu-id="38068-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="38068-109">O `ReCaptcha` ajudante.</span><span class="sxs-lookup"><span data-stu-id="38068-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="38068-110">As informações deste artigo se aplicam a ASP.NET Páginas da Web 1.0 e páginas da Web 2.</span><span class="sxs-lookup"><span data-stu-id="38068-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="38068-111">Sobre a CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="38068-111">About CAPTCHAs</span></span>

<span data-ttu-id="38068-112">Sempre que você permite que as pessoas se registrem em seu site, ou mesmo apenas digite um nome e URL (como para um comentário de blog), você pode obter uma enxurrada de nomes falsos.</span><span class="sxs-lookup"><span data-stu-id="38068-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="38068-113">Estes são muitas vezes deixados por programas automatizados (bots) que tentam deixar URLs em todos os sites que podem encontrar.</span><span class="sxs-lookup"><span data-stu-id="38068-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="38068-114">(Uma motivação comum é colocar os URLs de produtos à venda.)</span><span class="sxs-lookup"><span data-stu-id="38068-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="38068-115">Você pode ajudar a garantir que um usuário seja uma pessoa real e não um programa de computador usando um *CAPTCHA* para validar os usuários quando eles se registram ou digitam seu nome e site.</span><span class="sxs-lookup"><span data-stu-id="38068-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="38068-116">CAPTCHA significa teste de Turing público completamente automatizado para diferenciar computadores e humanos.</span><span class="sxs-lookup"><span data-stu-id="38068-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="38068-117">Um CAPTCHA é um teste *de resposta a desafios* no qual o usuário é solicitado a fazer algo que é fácil para uma pessoa fazer, mas difícil para um programa automatizado fazer.</span><span class="sxs-lookup"><span data-stu-id="38068-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="38068-118">O tipo mais comum de CAPTCHA é aquele em que você vê algumas letras distorcidas e é solicitado a digitá-las.</span><span class="sxs-lookup"><span data-stu-id="38068-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="38068-119">(A distorção deve dificultar a decifração das letras pelos bots.)</span><span class="sxs-lookup"><span data-stu-id="38068-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="38068-120">Adicionando um teste de ReCaptcha</span><span class="sxs-lookup"><span data-stu-id="38068-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="38068-121">Em ASP.NET páginas, você `ReCaptcha` pode usar o ajudante para renderizar um teste[http://recaptcha.net](http://recaptcha.net)CAPTCHA baseado no serviço ReCaptcha ( ).</span><span class="sxs-lookup"><span data-stu-id="38068-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="38068-122">O `ReCaptcha` ajudante exibe uma imagem de duas palavras distorcidas que os usuários têm que inserir corretamente antes que a página seja validada.</span><span class="sxs-lookup"><span data-stu-id="38068-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="38068-123">A resposta do usuário é validada pelo serviço ReCaptcha.Net.</span><span class="sxs-lookup"><span data-stu-id="38068-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="38068-124">Cadastre-se[http://recaptcha.net](http://recaptcha.net)no seu site em ReCaptcha.Net ( ).</span><span class="sxs-lookup"><span data-stu-id="38068-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="38068-125">Quando você concluir o registro, você terá uma chave pública e uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="38068-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="38068-126">Adicione a biblioteca ASP.NET de ajudantes da Web ao seu site, conforme descrito na [instalação de ajudantes em um site de páginas da ASP.NET,](https://go.microsoft.com/fwlink/?LinkId=252372)se você ainda não tiver.</span><span class="sxs-lookup"><span data-stu-id="38068-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="38068-127">Se você ainda não tiver um \* \_arquivo AppStart.cshtml,\* na pasta raiz de um site crie um arquivo chamado \* \_AppStart.cshtml\*.</span><span class="sxs-lookup"><span data-stu-id="38068-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="38068-128">Adicione as `Recaptcha` seguintes configurações de ajuda no \* \_arquivo AppStart.cshtml:\*</span><span class="sxs-lookup"><span data-stu-id="38068-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="38068-129">Defina `PublicKey` `PrivateKey` as propriedades usando suas próprias chaves públicas e privadas.</span><span class="sxs-lookup"><span data-stu-id="38068-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="38068-130">Salve o arquivo \* \_AppStart.cshtml\* e feche-o.</span><span class="sxs-lookup"><span data-stu-id="38068-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="38068-131">Na pasta raiz de um site, crie uma nova página chamada *Recaptcha.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="38068-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="38068-132">Substitua o conteúdo existente pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="38068-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="38068-133">Execute a página *Recaptcha.cshtml* em um navegador.</span><span class="sxs-lookup"><span data-stu-id="38068-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="38068-134">Se `PrivateKey` o valor for válido, a página exibirá o controle ReCaptcha e um botão.</span><span class="sxs-lookup"><span data-stu-id="38068-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="38068-135">Se você não tivesse definido as teclas globalmente no \* \_AppStart.html,\* a página exibiria um erro.</span><span class="sxs-lookup"><span data-stu-id="38068-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="38068-136">Digite as palavras para o teste.</span><span class="sxs-lookup"><span data-stu-id="38068-136">Enter the words for the test.</span></span> <span data-ttu-id="38068-137">Se você passar no teste ReCaptcha, verá uma mensagem nesse sentido.</span><span class="sxs-lookup"><span data-stu-id="38068-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="38068-138">Caso contrário, você verá uma mensagem de erro e o controle ReCaptcha será reexibido.</span><span class="sxs-lookup"><span data-stu-id="38068-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="38068-139">Se o computador estiver em um domínio que usa servidor `defaultproxy` proxy, talvez seja necessário configurar o elemento do arquivo *Web.config.*</span><span class="sxs-lookup"><span data-stu-id="38068-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="38068-140">O exemplo a seguir mostra um `defaultproxy` arquivo *Web.config* com o elemento configurado para permitir que o serviço ReCaptcha funcione.</span><span class="sxs-lookup"><span data-stu-id="38068-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="38068-141">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="38068-141">Additional Resources</span></span>

- [<span data-ttu-id="38068-142">Personalizando o comportamento em todo o site para sites de páginas da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="38068-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="38068-143">Site do ReCaptcha</span><span class="sxs-lookup"><span data-stu-id="38068-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
