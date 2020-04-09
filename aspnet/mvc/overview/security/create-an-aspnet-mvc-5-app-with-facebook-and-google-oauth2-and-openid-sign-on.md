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
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Criar um aplicativo do ASP.NET MVC 5 com logon OAuth2 no Facebook, Twitter, LinkedIn e Google (C#)

por [Rick Anderson](https://twitter.com/RickAndMSFT)

> Este tutorial mostra como construir um aplicativo web mvc 5 ASP.NET que permite que os usuários façam login usando [o OAuth 2.0](http://oauth.net/2/) com credenciais de um provedor de autenticação externa, como Facebook, Twitter, LinkedIn, Microsoft ou Google. Para simplificar, este tutorial se concentra em trabalhar com credenciais do Facebook e do Google.
> 
> Habilitar essas credenciais em seus sites oferece uma vantagem significativa porque milhões de usuários já têm contas com esses provedores externos. Esses usuários podem estar mais inclinados a se inscrever no seu site se não tiverem que criar e lembrar de um novo conjunto de credenciais.
> 
> Veja também [ASP.NET aplicativo MVC 5 com SMS e autenticação de dois fatores por e-mail.](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)
> 
> O tutorial também mostra como adicionar dados de perfil para o usuário e como usar a API de associação para adicionar funções. Este tutorial foi escrito por [Rick Anderson](https://blogs.msdn.com/rickAndy) [@RickAndMSFT](https://twitter.com/RickAndMSFT) ( Por favor, siga-me no Twitter: ).

<a id="start"></a>
## <a name="getting-started"></a>Introdução

Comece instalando e executando [o Visual Studio Express 2013 para Web](https://go.microsoft.com/fwlink/?LinkId=299058) ou Visual Studio [2013](https://go.microsoft.com/fwlink/?LinkId=306566). Instale o Visual Studio [2013 Atualização 3](https://go.microsoft.com/fwlink/?LinkId=390521) ou superior. Para obter ajuda com dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, e muito mais, consulte este [projeto de amostra](https://github.com/matthewdunsdon/oauthforaspnet).

> [!NOTE]
> Você deve instalar o Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) ou superior para usar o Google OAuth 2 e depurar localmente sem avisos SSL.

Clique em **Novo projeto** a partir da página **Iniciar,** ou você pode usar o menu e selecionar **Arquivo**e, em seguida, **Novo Projeto**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>Criando seu primeiro aplicativo

Clique em **Novo projeto,** depois selecione **Visual C#** à esquerda e, em seguida, **na Web** e selecione ASP.NET **Aplicativo web**. Nomeie seu projeto "MvcAuth" e clique em **OK**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

Na caixa de diálogo **Projeto Novo ASP.NET,** clique em **MVC**. Se a autenticação não for **Contas de Usuário Individuais,** clique no botão **Autenticação de alteração** e selecione Contas de Usuário **Individuais**. Ao verificar **host na nuvem,** o aplicativo será muito fácil de hospedar no Azure.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

Se você selecionou **Host na nuvem,** complete a caixa de diálogo configurar.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>Use o NuGet para atualizar para o mais recente middleware OWIN

Use o gerenciador de pacotes NuGet para atualizar o [middleware OWIN](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md). Selecione **Atualizações** no menu à esquerda. Você pode clicar no botão **Atualizar tudo** ou pode procurar apenas pacotes OWIN (mostrados na próxima imagem):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

Na imagem abaixo, apenas pacotes OWIN são mostrados:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

A partir do PMC Package Manager `Update-Package` Console (Package Manager Console), você pode inserir o comando, que atualizará todos os pacotes.

Pressione **F5** ou **Ctrl+F5** para executar o aplicativo. Na imagem abaixo, o número da porta é 1234. Quando você executar o aplicativo, você verá um número de porta diferente.

Dependendo do tamanho da janela do seu navegador, talvez seja necessário clicar no ícone de navegação para ver os links **Home**, **About**, **Contact,** **Register** e **Log in.**

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>Configuração do SSL no Projeto

Para se conectar a provedores de autenticação como Google e Facebook, você precisará configurar o IIS-Express para usar o SSL. É importante continuar usando SSL após login e não voltar para HTTP, seu cookie de login é tão secreto quanto seu nome de usuário e senha, e sem usar SSL você está enviando-o em texto claro através do fio. Além disso, você já tomou o tempo para realizar o aperto de mão e proteger o canal (que é a maior parte do que torna https mais lento do que HTTP) antes que o pipeline MVC seja executado, então redirecionar de volta para HTTP depois que você estiver logado não tornará a solicitação atual ou solicitações futuras muito mais rápido.

1. No **Solution Explorer,** clique no projeto **MvcAuth.**
2. Aperte a tecla F4 para mostrar as propriedades do projeto. Alternativamente, no menu **Exibir,** você pode selecionar **Janela propriedades**.
3. Alterar **SSL Ativado** para True.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. Copie a URL SSL `https://localhost:44300/` (que será a menos que você tenha criado outros projetos SSL).
5. No **Solution Explorer,** clique com o botão direito do mouse no projeto **MvcAuth** e selecione **Propriedades**.
6. Selecione a guia **Web** e cole a URL SSL na caixa Url do **projeto.** Salvar o arquivo (Ctl+S). Você precisará desta URL para configurar aplicativos de autenticação do Facebook e do Google.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. Adicione o atributo `Home` [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) ao controlador para exigir que todas as solicitações devem usar HTTPS. Uma abordagem mais segura é adicionar o filtro [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) ao aplicativo. Consulte a &quot;seção Proteja o Aplicativo com&quot; SSL e o Atributo Autorize no meu tutorial [Crie um aplicativo MVC ASP.NET com auth e SQL DB e implante no Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Uma parte do controlador Home é mostrada abaixo.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Pressione CTRL+F5 para executar o aplicativo. Se você instalou o certificado no passado, você pode pular o resto desta seção e pular para [Criar um aplicativo do Google para OAuth 2 e conectar o aplicativo ao projeto,](#goog)caso contrário, siga as instruções para confiar no certificado auto-assinado que o IIS Express gerou.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. Leia a caixa de diálogo **Aviso de segurança** e clique em **Sim** se quiser instalar o certificado representando o host local.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. O IE mostra a *Home page* e não há nenhum aviso de SSL.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. O Google Chrome também aceita o certificado e mostrará conteúdo HTTPS sem aviso prévio. O Firefox usa sua própria loja de certificados, por isso exibirá um aviso. Para o nosso aplicativo você pode clicar com segurança **em I Understand the Risks**.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>Criando um aplicativo do Google para OAuth 2 e conectando o aplicativo ao projeto

> [!WARNING]
> Para obter as instruções atuais do Google OAuth, [consulte Configurando a autenticação do Google no ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).

1. Navegue até o [Console Para Desenvolvedores do Google](https://console.developers.google.com/).
2. Se você não tiver criado um projeto antes, selecione **Credenciais** na guia esquerda e selecione **Criar**.
3. Na guia esquerda, clique em **Credenciais**.
4. Clique **em Criar credenciais** **e, em seguida, OAuth client ID**. 

    1. Na caixa de diálogo **Criar ID do cliente,** mantenha o **aplicativo Web** padrão para o tipo de aplicativo.
    2. Defina as origens **JavaScript autorizadas** para a`https://localhost:44300/` URL SSL que você usou acima (a menos que você tenha criado outros projetos SSL)
    3. Defina o **URI de redirecionamento autorizado** para:  
         `https://localhost:44300/signin-google`
5. Clique no item do menu da tela OAuth Consent e, em seguida, defina seu endereço de e-mail e nome do produto. Quando tiver concluído o formulário clique **em Salvar**.
6. Clique no item do menu Biblioteca, pesquise **a API do Google+,** clique nele e pressione Ativar.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   A imagem abaixo mostra as APIs habilitadas.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. No Google APIs API Manager, visite a guia **Credenciais** para obter o **ID do cliente**. Baixe para salvar um arquivo JSON com segredos de aplicativo. Copie e cole o **ClientId** e `UseGoogleAuthentication` **clientSecret** no método encontrado no arquivo *Startup.Auth.cs* na pasta *App_Start.* Os valores **ClientId** e **ClientSecret** mostrados abaixo são amostras e não funcionam.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > Segurança - Nunca armazene dados confidenciais em seu código-fonte. A conta e as credenciais são adicionadas ao código acima para manter a amostra simples. Consulte [as práticas recomendadas para implantar senhas e outros dados confidenciais para ASP.NET e Serviço de Aplicativos Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
8. Pressione **CTRL+F5** para construir e executar o aplicativo. Clique no link **Logon** .  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. Em **Use outro serviço para fazer login,** clique em **Google**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > Se você perder qualquer uma das etapas acima, você receberá um erro HTTP 401. Verifique novamente seus passos acima. Se você perder uma configuração necessária (por **exemplo, nome do produto),** adicione o item ausente e salve; pode levar alguns minutos para a autenticação funcionar.
10. Você será redirecionado para o site do Google onde você digitará suas credenciais.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. Após inserir suas credenciais, aparecerá uma solicitação para que você dê permissões para o aplicativo Web que acabou de criar: 
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. Clique **em Aceitar**. Agora você será redirecionado de volta para a página **Registrar** do aplicativo MvcAuth, onde você pode registrar sua conta do Google. Você tem a opção de alterar o nome de registro de email local utilizado para sua conta do Gmail, mas normalmente você deverá preferir manter o alias de email padrão (ou seja, aquele utilizado por você para a autenticação). Clique em **Registrar**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Criando o aplicativo no Facebook e conectando o aplicativo ao projeto

> [!WARNING]
> Para obter as instruções atuais de autenticação do Facebook OAuth2, consulte [Configuração da autenticação do Facebook](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>Examine os dados de adesão

No menu **Exibir,** clique em **Server Explorer**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

Expandir **a Conexão Padrão (MvcAuth),** expandir **tabelas,** clicar com o botão direito do mouse **AspNetUsers** e clicar **em Mostrar dados da tabela**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers dados da tabela](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>Adicionando dados de perfil à classe de usuário

Nesta seção você adicionará data de nascimento e cidade natal aos dados do usuário durante o registro, conforme mostrado na imagem a seguir.

![reg com cidade natal e Bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

Abra o arquivo *Models\IdentityModels.cs* e adicione a data de nascimento e as propriedades da cidade natal:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

Abra o arquivo *Models\AccountViewModels.cs* e a data `ExternalLoginConfirmationViewModel`de nascimento definida e as propriedades da cidade natal em .

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

Abra o arquivo *Controllers\AccountController.cs* e adicione código para `ExternalLoginConfirmation` data de nascimento e cidade natal no método de ação, conforme mostrado:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

Adicione data de nascimento e cidade natal ao arquivo *Views\Account\ExternalLoginConfirmation.cshtml:*

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

Exclua o banco de dados de membros para que você possa novamente registrar sua conta do Facebook com seu aplicativo e verificar se você pode adicionar a nova data de nascimento e as informações do perfil da cidade natal.

No **Solution Explorer**, clique no ícone Mostrar todos os **arquivos** e clique com o botão direito do mouse Em *\_Adicionar dados\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* e clique em **Excluir**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

No menu **Ferramentas,** clique em **NuGet Package Manger**e clique **em Package Manager Console** (PMC). Digite os seguintes comandos no PMC.

1. Ativar migrações
2. Adiciona-Migração Init
3. Banco de dados de atualização

Execute o aplicativo e use o FaceBook e o Google para fazer login e registrar alguns usuários.

## <a name="examine-the-membership-data"></a>Examine os dados de adesão

No menu **Exibir,** clique em **Server Explorer**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

Clique com o botão direito **do mouse AspNetUsers** e clique **em Mostrar dados da tabela**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

Os `HomeTown` `BirthDate` campos e campos são mostrados abaixo.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>Fazer login fora do seu aplicativo e fazer login com outra conta

Se você fizer login no seu aplicativo com o Facebook, e depois fizer login e tentar fazer login novamente com uma conta diferente do Facebook (usando o mesmo navegador), você estará imediatamente logado na conta anterior do Facebook que você usou. Para usar outra conta, você precisa navegar para o Facebook e sair no Facebook. A mesma regra se aplica a qualquer outro provedor de autenticação de terceiros. Alternativamente, você pode fazer login com outra conta usando um navegador diferente.

## <a name="next-steps"></a>Próximas etapas

Consulte [Introduzindo os provedores de segurança Yahoo e LinkedIn OAuth para OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) por Jerrie Pelser para as instruções do Yahoo e LinkedIn. Consulte os botões de login social pretty da Jerrie para ASP.NET MVC 5 para habilitar botões de login social.

Siga meu tutorial [Crie um aplicativo ASP.NET MVC com auth e SQL DB e implante no Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), que continua este tutorial e mostra o seguinte:

1. Como implantar seu aplicativo no Azure.
2. Como garantir o aplicativo com funções.
3. Como proteger seu aplicativo com os filtros [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) e [Authorize.](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)
4. Como usar a API de adesão para adicionar usuários e funções.

Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar. Você também pode solicitar novos tópicos no [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code). Você pode até mesmo pedir e votar em novos recursos a serem adicionados ao ASP.NET. Por exemplo, você pode votar em uma ferramenta para [criar e gerenciar usuários e funções.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

Para uma boa explicação de como ASP.NET serviços de autenticação externa funcionam, consulte os [Serviços de Autenticação Externa](https://asp.net/web-api/overview/security/external-authentication-services)de Robert McMurray. O artigo de Robert também entra em detalhes na habilitação da autenticação da Microsoft e do Twitter. O excelente [tutorial EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) de Tom Dykstra mostra como trabalhar com o Framework de entidades.
