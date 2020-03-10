---
uid: signalr/overview/security/hub-authorization
title: Autenticação e autorização para hubs do Signalr | Microsoft Docs
author: bradygaster
description: Este tópico descreve como restringir quais usuários ou funções podem acessar métodos de Hub. Versões de software usadas neste tópico Visual Studio 2013 o Signaler do .NET 4,5 ve...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578914"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="00260-104">Autenticação e autorização para hubs do SignalR</span><span class="sxs-lookup"><span data-stu-id="00260-104">Authentication and Authorization for SignalR Hubs</span></span>

<span data-ttu-id="00260-105">por [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="00260-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="00260-106">Este tópico descreve como restringir quais usuários ou funções podem acessar métodos de Hub.</span><span class="sxs-lookup"><span data-stu-id="00260-106">This topic describes how to restrict which users or roles can access hub methods.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="00260-107">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="00260-107">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="00260-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="00260-108">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="00260-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="00260-109">.NET 4.5</span></span>
> - <span data-ttu-id="00260-110">Sinalização versão 2</span><span class="sxs-lookup"><span data-stu-id="00260-110">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="00260-111">Versões anteriores deste tópico</span><span class="sxs-lookup"><span data-stu-id="00260-111">Previous versions of this topic</span></span>
>
> <span data-ttu-id="00260-112">Para obter informações sobre versões anteriores do Signalr, confira [versões mais antigas do signalr](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="00260-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="00260-113">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="00260-113">Questions and comments</span></span>
>
> <span data-ttu-id="00260-114">Deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="00260-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="00260-115">Se você tiver dúvidas que não estão diretamente relacionadas ao tutorial, poderá lançá-las no fórum do [signalr ASP.net](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [stackoverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="00260-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="00260-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="00260-116">Overview</span></span>

<span data-ttu-id="00260-117">Este tópico contém as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="00260-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="00260-118">Autorizar atributo</span><span class="sxs-lookup"><span data-stu-id="00260-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="00260-119">Exigir autenticação para todos os hubs</span><span class="sxs-lookup"><span data-stu-id="00260-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="00260-120">Autorização personalizada</span><span class="sxs-lookup"><span data-stu-id="00260-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="00260-121">Passar informações de autenticação para clientes</span><span class="sxs-lookup"><span data-stu-id="00260-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="00260-122">Opções de autenticação para clientes .NET</span><span class="sxs-lookup"><span data-stu-id="00260-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="00260-123">Cookie com autenticação de formulários</span><span class="sxs-lookup"><span data-stu-id="00260-123">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="00260-124">Autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="00260-124">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="00260-125">Cabeçalho de conexão</span><span class="sxs-lookup"><span data-stu-id="00260-125">Connection header</span></span>](#header)
    - [<span data-ttu-id="00260-126">Certificado</span><span class="sxs-lookup"><span data-stu-id="00260-126">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="00260-127">Autorizar atributo</span><span class="sxs-lookup"><span data-stu-id="00260-127">Authorize attribute</span></span>

<span data-ttu-id="00260-128">O signalr fornece o atributo [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) para especificar quais usuários ou funções têm acesso a um Hub ou método.</span><span class="sxs-lookup"><span data-stu-id="00260-128">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="00260-129">Esse atributo está localizado no namespace `Microsoft.AspNet.SignalR`.</span><span class="sxs-lookup"><span data-stu-id="00260-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="00260-130">Você aplica o atributo `Authorize` a um Hub ou métodos específicos em um Hub.</span><span class="sxs-lookup"><span data-stu-id="00260-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="00260-131">Quando você aplica o atributo `Authorize` a uma classe de Hub, o requisito de autorização especificado é aplicado a todos os métodos no Hub.</span><span class="sxs-lookup"><span data-stu-id="00260-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="00260-132">Este tópico fornece exemplos dos diferentes tipos de requisitos de autorização que você pode aplicar.</span><span class="sxs-lookup"><span data-stu-id="00260-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="00260-133">Sem o atributo `Authorize`, um cliente conectado pode acessar qualquer método público no Hub.</span><span class="sxs-lookup"><span data-stu-id="00260-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="00260-134">Se você tiver definido uma função denominada "admin" em seu aplicativo Web, poderá especificar que somente os usuários nessa função possam acessar um hub com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="00260-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="00260-135">Ou você pode especificar que um hub contém um método que está disponível para todos os usuários e um segundo método que só está disponível para usuários autenticados, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="00260-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="00260-136">Os exemplos a seguir abordam diferentes cenários de autorização:</span><span class="sxs-lookup"><span data-stu-id="00260-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="00260-137">`[Authorize]` – somente usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="00260-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="00260-138">`[Authorize(Roles = "Admin,Manager")]` – somente usuários autenticados nas funções especificadas</span><span class="sxs-lookup"><span data-stu-id="00260-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="00260-139">`[Authorize(Users = "user1,user2")]` – somente usuários autenticados com os nomes de usuário especificados</span><span class="sxs-lookup"><span data-stu-id="00260-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="00260-140">`[Authorize(RequireOutgoing=false)]` – somente usuários autenticados podem invocar o Hub, mas as chamadas do servidor de volta para os clientes não são limitadas pela autorização, como, quando apenas determinados usuários podem enviar uma mensagem, mas todas as outras pessoas podem receber a mensagem.</span><span class="sxs-lookup"><span data-stu-id="00260-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="00260-141">A propriedade RequireOutgoing só pode ser aplicada a todo o Hub, não a métodos de indivíduos dentro do Hub.</span><span class="sxs-lookup"><span data-stu-id="00260-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="00260-142">Quando RequireOutgoing não está definido como false, somente os usuários que atendem ao requisito de autorização são chamados do servidor.</span><span class="sxs-lookup"><span data-stu-id="00260-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="00260-143">Exigir autenticação para todos os hubs</span><span class="sxs-lookup"><span data-stu-id="00260-143">Require authentication for all hubs</span></span>

<span data-ttu-id="00260-144">Você pode exigir autenticação para todos os hubs e métodos de Hub em seu aplicativo chamando o método [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) quando o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="00260-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="00260-145">Você pode usar esse método quando tiver vários hubs e desejar impor um requisito de autenticação para todos eles.</span><span class="sxs-lookup"><span data-stu-id="00260-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="00260-146">Com esse método, você não pode especificar os requisitos para função, usuário ou autorização de saída.</span><span class="sxs-lookup"><span data-stu-id="00260-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="00260-147">Você só pode especificar que o acesso aos métodos de Hub seja restrito a usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="00260-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="00260-148">No entanto, você ainda pode aplicar o atributo autorizar a hubs ou métodos para especificar requisitos adicionais.</span><span class="sxs-lookup"><span data-stu-id="00260-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="00260-149">Qualquer requisito especificado em um atributo é adicionado ao requisito básico de autenticação.</span><span class="sxs-lookup"><span data-stu-id="00260-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="00260-150">O exemplo a seguir mostra um arquivo de inicialização que restringe todos os métodos de Hub para usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="00260-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="00260-151">Se você chamar o método `RequireAuthentication()` depois que uma solicitação de Signalr for processada, o Signalr gerará uma exceção de `InvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="00260-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="00260-152">O signalr gera essa exceção porque você não pode adicionar um módulo ao HubPipeline depois que o pipeline é invocado.</span><span class="sxs-lookup"><span data-stu-id="00260-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="00260-153">O exemplo anterior mostra a chamada do método `RequireAuthentication` no método `Configuration` que é executado uma vez antes da manipulação da primeira solicitação.</span><span class="sxs-lookup"><span data-stu-id="00260-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="00260-154">Autorização personalizada</span><span class="sxs-lookup"><span data-stu-id="00260-154">Customized authorization</span></span>

<span data-ttu-id="00260-155">Se você precisar personalizar como a autorização é determinada, você pode criar uma classe que deriva de `AuthorizeAttribute` e substituir o método [Userautoted](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="00260-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="00260-156">Para cada solicitação, o Signalr invoca esse método para determinar se o usuário está autorizado a concluir a solicitação.</span><span class="sxs-lookup"><span data-stu-id="00260-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="00260-157">No método substituído, você fornece a lógica necessária para seu cenário de autorização.</span><span class="sxs-lookup"><span data-stu-id="00260-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="00260-158">O exemplo a seguir mostra como impor a autorização por meio de identidade baseada em declarações.</span><span class="sxs-lookup"><span data-stu-id="00260-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="00260-159">Passar informações de autenticação para clientes</span><span class="sxs-lookup"><span data-stu-id="00260-159">Pass authentication information to clients</span></span>

<span data-ttu-id="00260-160">Talvez seja necessário usar as informações de autenticação no código que é executado no cliente.</span><span class="sxs-lookup"><span data-stu-id="00260-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="00260-161">Você passa as informações necessárias ao chamar os métodos no cliente.</span><span class="sxs-lookup"><span data-stu-id="00260-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="00260-162">Por exemplo, um método de aplicativo de chat pode passar como um parâmetro o nome de usuário da pessoa que está postando uma mensagem, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="00260-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="00260-163">Ou, você pode criar um objeto para representar as informações de autenticação e passar esse objeto como um parâmetro, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="00260-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="00260-164">Você nunca deve passar a ID de conexão de um cliente para outros clientes, uma vez que um usuário mal-intencionado pode usá-lo para imitar uma solicitação desse cliente.</span><span class="sxs-lookup"><span data-stu-id="00260-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="00260-165">Opções de autenticação para clientes .NET</span><span class="sxs-lookup"><span data-stu-id="00260-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="00260-166">Quando você tem um cliente .NET, como um aplicativo de console, que interage com um hub limitado a usuários autenticados, você pode passar as credenciais de autenticação em um cookie, no cabeçalho de conexão ou em um certificado.</span><span class="sxs-lookup"><span data-stu-id="00260-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="00260-167">Os exemplos nesta seção mostram como usar esses métodos diferentes para autenticar um usuário.</span><span class="sxs-lookup"><span data-stu-id="00260-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="00260-168">Eles não são aplicativos de Signaler totalmente funcionais.</span><span class="sxs-lookup"><span data-stu-id="00260-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="00260-169">Para obter mais informações sobre clientes .NET com o Signalr, consulte [Guia de API de hubs-cliente .net](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="00260-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="00260-170">Cookie</span><span class="sxs-lookup"><span data-stu-id="00260-170">Cookie</span></span>

<span data-ttu-id="00260-171">Quando o cliente .NET interage com um Hub que usa a autenticação de formulários ASP.NET, você precisará definir manualmente o cookie de autenticação na conexão.</span><span class="sxs-lookup"><span data-stu-id="00260-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="00260-172">Você adiciona o cookie à propriedade `CookieContainer` no objeto [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="00260-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="00260-173">O exemplo a seguir mostra um aplicativo de console que recupera um cookie de autenticação de uma página da Web e adiciona esse cookie à conexão.</span><span class="sxs-lookup"><span data-stu-id="00260-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="00260-174">O aplicativo de console posta as credenciais para <strong>www.contoso.com/RemoteLogin</strong> que podem se referir a uma página vazia que contém o seguinte arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="00260-174">The console app posts the credentials to <strong>www.contoso.com/RemoteLogin</strong> which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="00260-175">Autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="00260-175">Windows authentication</span></span>

<span data-ttu-id="00260-176">Ao usar a autenticação do Windows, você pode passar as credenciais do usuário atual usando a propriedade [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) .</span><span class="sxs-lookup"><span data-stu-id="00260-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="00260-177">Você define as credenciais para a conexão com o valor de DefaultCredentials.</span><span class="sxs-lookup"><span data-stu-id="00260-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="00260-178">Cabeçalho de conexão</span><span class="sxs-lookup"><span data-stu-id="00260-178">Connection header</span></span>

<span data-ttu-id="00260-179">Se seu aplicativo não estiver usando cookies, você poderá passar informações do usuário no cabeçalho de conexão.</span><span class="sxs-lookup"><span data-stu-id="00260-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="00260-180">Por exemplo, você pode passar um token no cabeçalho de conexão.</span><span class="sxs-lookup"><span data-stu-id="00260-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="00260-181">Em seguida, no Hub, você verificaria o token do usuário.</span><span class="sxs-lookup"><span data-stu-id="00260-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="00260-182">Certificado</span><span class="sxs-lookup"><span data-stu-id="00260-182">Certificate</span></span>

<span data-ttu-id="00260-183">Você pode passar um certificado de cliente para verificar o usuário.</span><span class="sxs-lookup"><span data-stu-id="00260-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="00260-184">Você adiciona o certificado ao criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="00260-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="00260-185">O exemplo a seguir mostra apenas como adicionar um certificado de cliente à conexão; Ele não mostra o aplicativo de console completo.</span><span class="sxs-lookup"><span data-stu-id="00260-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="00260-186">Ele usa a classe [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) , que fornece várias maneiras diferentes de criar o certificado.</span><span class="sxs-lookup"><span data-stu-id="00260-186">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
