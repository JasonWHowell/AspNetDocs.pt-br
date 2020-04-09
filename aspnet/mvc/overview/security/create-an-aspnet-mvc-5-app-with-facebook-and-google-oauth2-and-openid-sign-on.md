---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Criar aplicativo MVC 5 com Facebook, Twitter, LinkedIn e Google OAuth2 Sign-on (C#) | Microsoft Docs
author: Rick-Anderson
description: Este tutorial mostra como construir um aplicativo web ASP.NET MVC 5 que permite que os usuários façam login usando o OAuth 2.0 com credenciais de um authenti externo...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676317"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="159f3-103">Criar um aplicativo do ASP.NET MVC 5 com logon OAuth2 no Facebook, Twitter, LinkedIn e Google (C#)</span><span class="sxs-lookup"><span data-stu-id="159f3-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="159f3-104">por [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="159f3-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="159f3-105">Este tutorial mostra como construir um aplicativo web mvc 5 ASP.NET que permite que os usuários façam login usando [o OAuth 2.0](http://oauth.net/2/) com credenciais de um provedor de autenticação externa, como Facebook, Twitter, LinkedIn, Microsoft ou Google.</span><span class="sxs-lookup"><span data-stu-id="159f3-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="159f3-106">Para simplificar, este tutorial se concentra em trabalhar com credenciais do Facebook e do Google.</span><span class="sxs-lookup"><span data-stu-id="159f3-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="159f3-107">Habilitar essas credenciais em seus sites oferece uma vantagem significativa porque milhões de usuários já têm contas com esses provedores externos.</span><span class="sxs-lookup"><span data-stu-id="159f3-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="159f3-108">Esses usuários podem estar mais inclinados a se inscrever no seu site se não tiverem que criar e lembrar de um novo conjunto de credenciais.</span><span class="sxs-lookup"><span data-stu-id="159f3-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="159f3-109">Veja também [ASP.NET aplicativo MVC 5 com SMS e autenticação de dois fatores por e-mail.](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="159f3-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="159f3-110">O tutorial também mostra como adicionar dados de perfil para o usuário e como usar a API de associação para adicionar funções.</span><span class="sxs-lookup"><span data-stu-id="159f3-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="159f3-111">Este tutorial foi escrito por [Rick Anderson](https://blogs.msdn.com/rickAndy) [@RickAndMSFT](https://twitter.com/RickAndMSFT) ( Por favor, siga-me no Twitter: ).</span><span class="sxs-lookup"><span data-stu-id="159f3-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="159f3-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="159f3-112">Getting Started</span></span>

<span data-ttu-id="159f3-113">Comece instalando e executando [o Visual Studio Express 2013 para Web](https://go.microsoft.com/fwlink/?LinkId=299058) ou Visual Studio [2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="159f3-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="159f3-114">Instale o Visual Studio [2013 Atualização 3](https://go.microsoft.com/fwlink/?LinkId=390521) ou superior.</span><span class="sxs-lookup"><span data-stu-id="159f3-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="159f3-115">Para obter ajuda com dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, e muito mais, consulte este [projeto de amostra](https://github.com/matthewdunsdon/oauthforaspnet).</span><span class="sxs-lookup"><span data-stu-id="159f3-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="159f3-116">Você deve instalar o Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) ou superior para usar o Google OAuth 2 e depurar localmente sem avisos SSL.</span><span class="sxs-lookup"><span data-stu-id="159f3-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="159f3-117">Clique em **Novo projeto** a partir da página **Iniciar,** ou você pode usar o menu e selecionar **Arquivo**e, em seguida, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="159f3-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="159f3-118">Criando seu primeiro aplicativo</span><span class="sxs-lookup"><span data-stu-id="159f3-118">Creating Your First Application</span></span>

<span data-ttu-id="159f3-119">Clique em **Novo projeto,** depois selecione **Visual C#** à esquerda e, em seguida, **na Web** e selecione ASP.NET **Aplicativo web**.</span><span class="sxs-lookup"><span data-stu-id="159f3-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="159f3-120">Nomeie seu projeto "MvcAuth" e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="159f3-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="159f3-121">Na caixa de diálogo **Projeto Novo ASP.NET,** clique em **MVC**.</span><span class="sxs-lookup"><span data-stu-id="159f3-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="159f3-122">Se a autenticação não for **Contas de Usuário Individuais,** clique no botão **Autenticação de alteração** e selecione Contas de Usuário **Individuais**.</span><span class="sxs-lookup"><span data-stu-id="159f3-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="159f3-123">Ao verificar **host na nuvem,** o aplicativo será muito fácil de hospedar no Azure.</span><span class="sxs-lookup"><span data-stu-id="159f3-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="159f3-124">Se você selecionou **Host na nuvem,** complete a caixa de diálogo configurar.</span><span class="sxs-lookup"><span data-stu-id="159f3-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="159f3-125">Use o NuGet para atualizar para o mais recente middleware OWIN</span><span class="sxs-lookup"><span data-stu-id="159f3-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="159f3-126">Use o gerenciador de pacotes NuGet para atualizar o [middleware OWIN](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span><span class="sxs-lookup"><span data-stu-id="159f3-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="159f3-127">Selecione **Atualizações** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="159f3-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="159f3-128">Você pode clicar no botão **Atualizar tudo** ou pode procurar apenas pacotes OWIN (mostrados na próxima imagem):</span><span class="sxs-lookup"><span data-stu-id="159f3-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="159f3-129">Na imagem abaixo, apenas pacotes OWIN são mostrados:</span><span class="sxs-lookup"><span data-stu-id="159f3-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="159f3-130">A partir do PMC Package Manager `Update-Package` Console (Package Manager Console), você pode inserir o comando, que atualizará todos os pacotes.</span><span class="sxs-lookup"><span data-stu-id="159f3-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="159f3-131">Pressione **F5** ou **Ctrl+F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="159f3-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="159f3-132">Na imagem abaixo, o número da porta é 1234.</span><span class="sxs-lookup"><span data-stu-id="159f3-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="159f3-133">Quando você executar o aplicativo, você verá um número de porta diferente.</span><span class="sxs-lookup"><span data-stu-id="159f3-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="159f3-134">Dependendo do tamanho da janela do seu navegador, talvez seja necessário clicar no ícone de navegação para ver os links **Home**, **About**, **Contact,** **Register** e **Log in.**</span><span class="sxs-lookup"><span data-stu-id="159f3-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="159f3-135">Configuração do SSL no Projeto</span><span class="sxs-lookup"><span data-stu-id="159f3-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="159f3-136">Para se conectar a provedores de autenticação como Google e Facebook, você precisará configurar o IIS-Express para usar o SSL.</span><span class="sxs-lookup"><span data-stu-id="159f3-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="159f3-137">É importante continuar usando SSL após login e não voltar para HTTP, seu cookie de login é tão secreto quanto seu nome de usuário e senha, e sem usar SSL você está enviando-o em texto claro através do fio.</span><span class="sxs-lookup"><span data-stu-id="159f3-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="159f3-138">Além disso, você já tomou o tempo para realizar o aperto de mão e proteger o canal (que é a maior parte do que torna https mais lento do que HTTP) antes que o pipeline MVC seja executado, então redirecionar de volta para HTTP depois que você estiver logado não tornará a solicitação atual ou solicitações futuras muito mais rápido.</span><span class="sxs-lookup"><span data-stu-id="159f3-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="159f3-139">No **Solution Explorer,** clique no projeto **MvcAuth.**</span><span class="sxs-lookup"><span data-stu-id="159f3-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="159f3-140">Aperte a tecla F4 para mostrar as propriedades do projeto.</span><span class="sxs-lookup"><span data-stu-id="159f3-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="159f3-141">Alternativamente, no menu **Exibir,** você pode selecionar **Janela propriedades**.</span><span class="sxs-lookup"><span data-stu-id="159f3-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="159f3-142">Alterar **SSL Ativado** para True.</span><span class="sxs-lookup"><span data-stu-id="159f3-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="159f3-143">Copie a URL SSL `https://localhost:44300/` (que será a menos que você tenha criado outros projetos SSL).</span><span class="sxs-lookup"><span data-stu-id="159f3-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="159f3-144">No **Solution Explorer,** clique com o botão direito do mouse no projeto **MvcAuth** e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="159f3-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="159f3-145">Selecione a guia **Web** e cole a URL SSL na caixa Url do **projeto.**</span><span class="sxs-lookup"><span data-stu-id="159f3-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="159f3-146">Salvar o arquivo (Ctl+S).</span><span class="sxs-lookup"><span data-stu-id="159f3-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="159f3-147">Você precisará desta URL para configurar aplicativos de autenticação do Facebook e do Google.</span><span class="sxs-lookup"><span data-stu-id="159f3-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="159f3-148">Adicione o atributo `Home` [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) ao controlador para exigir que todas as solicitações devem usar HTTPS.</span><span class="sxs-lookup"><span data-stu-id="159f3-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="159f3-149">Uma abordagem mais segura é adicionar o filtro [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="159f3-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="159f3-150">Consulte a &quot;seção Proteja o Aplicativo com&quot; SSL e o Atributo Autorize no meu tutorial [Crie um aplicativo MVC ASP.NET com auth e SQL DB e implante no Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="159f3-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="159f3-151">Uma parte do controlador Home é mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="159f3-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="159f3-152">Pressione CTRL+F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="159f3-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="159f3-153">Se você instalou o certificado no passado, você pode pular o resto desta seção e pular para [Criar um aplicativo do Google para OAuth 2 e conectar o aplicativo ao projeto,](#goog)caso contrário, siga as instruções para confiar no certificado auto-assinado que o IIS Express gerou.</span><span class="sxs-lookup"><span data-stu-id="159f3-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="159f3-154">Leia a caixa de diálogo **Aviso de segurança** e clique em **Sim** se quiser instalar o certificado representando o host local.</span><span class="sxs-lookup"><span data-stu-id="159f3-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="159f3-155">O IE mostra a *Home page* e não há nenhum aviso de SSL.</span><span class="sxs-lookup"><span data-stu-id="159f3-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="159f3-156">O Google Chrome também aceita o certificado e mostrará conteúdo HTTPS sem aviso prévio.</span><span class="sxs-lookup"><span data-stu-id="159f3-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="159f3-157">O Firefox usa sua própria loja de certificados, por isso exibirá um aviso.</span><span class="sxs-lookup"><span data-stu-id="159f3-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="159f3-158">Para o nosso aplicativo você pode clicar com segurança **em I Understand the Risks**.</span><span class="sxs-lookup"><span data-stu-id="159f3-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="159f3-159">Criando um aplicativo do Google para OAuth 2 e conectando o aplicativo ao projeto</span><span class="sxs-lookup"><span data-stu-id="159f3-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="159f3-160">Para obter as instruções atuais do Google OAuth, [consulte Configurando a autenticação do Google no ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="159f3-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="159f3-161">Navegue até o [Console Para Desenvolvedores do Google](https://console.developers.google.com/).</span><span class="sxs-lookup"><span data-stu-id="159f3-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="159f3-162">Se você não tiver criado um projeto antes, selecione **Credenciais** na guia esquerda e selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="159f3-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="159f3-163">Na guia esquerda, clique em **Credenciais**.</span><span class="sxs-lookup"><span data-stu-id="159f3-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="159f3-164">Clique **em Criar credenciais** **e, em seguida, OAuth client ID**.</span><span class="sxs-lookup"><span data-stu-id="159f3-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="159f3-165">Na caixa de diálogo **Criar ID do cliente,** mantenha o **aplicativo Web** padrão para o tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="159f3-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="159f3-166">Defina as origens **JavaScript autorizadas** para a`https://localhost:44300/` URL SSL que você usou acima (a menos que você tenha criado outros projetos SSL)</span><span class="sxs-lookup"><span data-stu-id="159f3-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="159f3-167">Defina o **URI de redirecionamento autorizado** para:</span><span class="sxs-lookup"><span data-stu-id="159f3-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="159f3-168">Clique no item do menu da tela OAuth Consent e, em seguida, defina seu endereço de e-mail e nome do produto.</span><span class="sxs-lookup"><span data-stu-id="159f3-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="159f3-169">Quando tiver concluído o formulário clique **em Salvar**.</span><span class="sxs-lookup"><span data-stu-id="159f3-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="159f3-170">Clique no item do menu Biblioteca, pesquise **a API do Google+,** clique nele e pressione Ativar.</span><span class="sxs-lookup"><span data-stu-id="159f3-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="159f3-171">A imagem abaixo mostra as APIs habilitadas.</span><span class="sxs-lookup"><span data-stu-id="159f3-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="159f3-172">No Google APIs API Manager, visite a guia **Credenciais** para obter o **ID do cliente**.</span><span class="sxs-lookup"><span data-stu-id="159f3-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="159f3-173">Baixe para salvar um arquivo JSON com segredos de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="159f3-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="159f3-174">Copie e cole o **ClientId** e `UseGoogleAuthentication` **clientSecret** no método encontrado no arquivo *Startup.Auth.cs* na pasta *App_Start.*</span><span class="sxs-lookup"><span data-stu-id="159f3-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="159f3-175">Os valores **ClientId** e **ClientSecret** mostrados abaixo são amostras e não funcionam.</span><span class="sxs-lookup"><span data-stu-id="159f3-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="159f3-176">Segurança - Nunca armazene dados confidenciais em seu código-fonte.</span><span class="sxs-lookup"><span data-stu-id="159f3-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="159f3-177">A conta e as credenciais são adicionadas ao código acima para manter a amostra simples.</span><span class="sxs-lookup"><span data-stu-id="159f3-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="159f3-178">Consulte [as práticas recomendadas para implantar senhas e outros dados confidenciais para ASP.NET e Serviço de Aplicativos Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="159f3-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="159f3-179">Pressione **CTRL+F5** para construir e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="159f3-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="159f3-180">Clique no link **Logon** .</span><span class="sxs-lookup"><span data-stu-id="159f3-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="159f3-181">Em **Use outro serviço para fazer login,** clique em **Google**.</span><span class="sxs-lookup"><span data-stu-id="159f3-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="159f3-182">Se você perder qualquer uma das etapas acima, você receberá um erro HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="159f3-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="159f3-183">Verifique novamente seus passos acima.</span><span class="sxs-lookup"><span data-stu-id="159f3-183">Recheck your steps above.</span></span> <span data-ttu-id="159f3-184">Se você perder uma configuração necessária (por **exemplo, nome do produto),** adicione o item ausente e salve; pode levar alguns minutos para a autenticação funcionar.</span><span class="sxs-lookup"><span data-stu-id="159f3-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="159f3-185">Você será redirecionado para o site do Google onde você digitará suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="159f3-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="159f3-186">Após inserir suas credenciais, aparecerá uma solicitação para que você dê permissões para o aplicativo Web que acabou de criar: </span><span class="sxs-lookup"><span data-stu-id="159f3-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="159f3-187">Clique **em Aceitar**.</span><span class="sxs-lookup"><span data-stu-id="159f3-187">Click **Accept**.</span></span> <span data-ttu-id="159f3-188">Agora você será redirecionado de volta para a página **Registrar** do aplicativo MvcAuth, onde você pode registrar sua conta do Google.</span><span class="sxs-lookup"><span data-stu-id="159f3-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="159f3-189">Você tem a opção de alterar o nome de registro de email local utilizado para sua conta do Gmail, mas normalmente você deverá preferir manter o alias de email padrão (ou seja, aquele utilizado por você para a autenticação).</span><span class="sxs-lookup"><span data-stu-id="159f3-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="159f3-190">Clique em **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="159f3-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="159f3-191">Criando o aplicativo no Facebook e conectando o aplicativo ao projeto</span><span class="sxs-lookup"><span data-stu-id="159f3-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="159f3-192">Para obter as instruções atuais de autenticação do Facebook OAuth2, consulte [Configuração da autenticação do Facebook](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="159f3-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="159f3-193">Examine os dados de adesão</span><span class="sxs-lookup"><span data-stu-id="159f3-193">Examine the Membership Data</span></span>

<span data-ttu-id="159f3-194">No menu **Exibir,** clique em **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="159f3-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="159f3-195">Expandir **a Conexão Padrão (MvcAuth),** expandir **tabelas,** clicar com o botão direito do mouse **AspNetUsers** e clicar **em Mostrar dados da tabela**.</span><span class="sxs-lookup"><span data-stu-id="159f3-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers dados da tabela](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="159f3-197">Adicionando dados de perfil à classe de usuário</span><span class="sxs-lookup"><span data-stu-id="159f3-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="159f3-198">Nesta seção você adicionará data de nascimento e cidade natal aos dados do usuário durante o registro, conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="159f3-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![reg com cidade natal e Bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="159f3-200">Abra o arquivo *Models\IdentityModels.cs* e adicione a data de nascimento e as propriedades da cidade natal:</span><span class="sxs-lookup"><span data-stu-id="159f3-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="159f3-201">Abra o arquivo *Models\AccountViewModels.cs* e a data `ExternalLoginConfirmationViewModel`de nascimento definida e as propriedades da cidade natal em .</span><span class="sxs-lookup"><span data-stu-id="159f3-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="159f3-202">Abra o arquivo *Controllers\AccountController.cs* e adicione código para `ExternalLoginConfirmation` data de nascimento e cidade natal no método de ação, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="159f3-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="159f3-203">Adicione data de nascimento e cidade natal ao arquivo *Views\Account\ExternalLoginConfirmation.cshtml:*</span><span class="sxs-lookup"><span data-stu-id="159f3-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="159f3-204">Exclua o banco de dados de membros para que você possa novamente registrar sua conta do Facebook com seu aplicativo e verificar se você pode adicionar a nova data de nascimento e as informações do perfil da cidade natal.</span><span class="sxs-lookup"><span data-stu-id="159f3-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="159f3-205">No **Solution Explorer**, clique no ícone Mostrar todos os **arquivos** e clique com o botão direito do mouse Em *\_Adicionar dados\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="159f3-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="159f3-206">No menu **Ferramentas,** clique em **NuGet Package Manger**e clique **em Package Manager Console** (PMC).</span><span class="sxs-lookup"><span data-stu-id="159f3-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="159f3-207">Digite os seguintes comandos no PMC.</span><span class="sxs-lookup"><span data-stu-id="159f3-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="159f3-208">Ativar migrações</span><span class="sxs-lookup"><span data-stu-id="159f3-208">Enable-Migrations</span></span>
2. <span data-ttu-id="159f3-209">Adiciona-Migração Init</span><span class="sxs-lookup"><span data-stu-id="159f3-209">Add-Migration Init</span></span>
3. <span data-ttu-id="159f3-210">Banco de dados de atualização</span><span class="sxs-lookup"><span data-stu-id="159f3-210">Update-Database</span></span>

<span data-ttu-id="159f3-211">Execute o aplicativo e use o FaceBook e o Google para fazer login e registrar alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="159f3-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="159f3-212">Examine os dados de adesão</span><span class="sxs-lookup"><span data-stu-id="159f3-212">Examine the Membership Data</span></span>

<span data-ttu-id="159f3-213">No menu **Exibir,** clique em **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="159f3-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="159f3-214">Clique com o botão direito **do mouse AspNetUsers** e clique **em Mostrar dados da tabela**.</span><span class="sxs-lookup"><span data-stu-id="159f3-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="159f3-215">Os `HomeTown` `BirthDate` campos e campos são mostrados abaixo.</span><span class="sxs-lookup"><span data-stu-id="159f3-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="159f3-216">Fazer login fora do seu aplicativo e fazer login com outra conta</span><span class="sxs-lookup"><span data-stu-id="159f3-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="159f3-217">Se você fizer login no seu aplicativo com o Facebook, e depois fizer login e tentar fazer login novamente com uma conta diferente do Facebook (usando o mesmo navegador), você estará imediatamente logado na conta anterior do Facebook que você usou.</span><span class="sxs-lookup"><span data-stu-id="159f3-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="159f3-218">Para usar outra conta, você precisa navegar para o Facebook e sair no Facebook.</span><span class="sxs-lookup"><span data-stu-id="159f3-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="159f3-219">A mesma regra se aplica a qualquer outro provedor de autenticação de terceiros.</span><span class="sxs-lookup"><span data-stu-id="159f3-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="159f3-220">Alternativamente, você pode fazer login com outra conta usando um navegador diferente.</span><span class="sxs-lookup"><span data-stu-id="159f3-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="159f3-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="159f3-221">Next Steps</span></span>

<span data-ttu-id="159f3-222">Consulte [Introduzindo os provedores de segurança Yahoo e LinkedIn OAuth para OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) por Jerrie Pelser para as instruções do Yahoo e LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="159f3-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="159f3-223">Consulte os botões de login social pretty da Jerrie para ASP.NET MVC 5 para habilitar botões de login social.</span><span class="sxs-lookup"><span data-stu-id="159f3-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="159f3-224">Siga meu tutorial [Crie um aplicativo ASP.NET MVC com auth e SQL DB e implante no Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), que continua este tutorial e mostra o seguinte:</span><span class="sxs-lookup"><span data-stu-id="159f3-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="159f3-225">Como implantar seu aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="159f3-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="159f3-226">Como garantir o aplicativo com funções.</span><span class="sxs-lookup"><span data-stu-id="159f3-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="159f3-227">Como proteger seu aplicativo com os filtros [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) e [Authorize.](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="159f3-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="159f3-228">Como usar a API de adesão para adicionar usuários e funções.</span><span class="sxs-lookup"><span data-stu-id="159f3-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="159f3-229">Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar.</span><span class="sxs-lookup"><span data-stu-id="159f3-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="159f3-230">Você também pode solicitar novos tópicos no [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span><span class="sxs-lookup"><span data-stu-id="159f3-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="159f3-231">Você pode até mesmo pedir e votar em novos recursos a serem adicionados ao ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="159f3-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="159f3-232">Por exemplo, você pode votar em uma ferramenta para [criar e gerenciar usuários e funções.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="159f3-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="159f3-233">Para uma boa explicação de como ASP.NET serviços de autenticação externa funcionam, consulte os [Serviços de Autenticação Externa](https://asp.net/web-api/overview/security/external-authentication-services)de Robert McMurray.</span><span class="sxs-lookup"><span data-stu-id="159f3-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="159f3-234">O artigo de Robert também entra em detalhes na habilitação da autenticação da Microsoft e do Twitter.</span><span class="sxs-lookup"><span data-stu-id="159f3-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="159f3-235">O excelente [tutorial EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) de Tom Dykstra mostra como trabalhar com o Framework de entidades.</span><span class="sxs-lookup"><span data-stu-id="159f3-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
