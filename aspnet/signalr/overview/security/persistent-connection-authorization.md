---
uid: signalr/overview/security/persistent-connection-authorization
title: Autenticação e autorização para conexões persistentes do Signalr | Microsoft Docs
author: bradygaster
description: Este tópico descreve como impor a autorização em uma conexão persistente. Para obter informações gerais sobre como integrar a segurança em um aplicativo Signalr,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578872"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="2f132-104">Autenticação e autorização para conexões persistentes do SignalR</span><span class="sxs-lookup"><span data-stu-id="2f132-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="2f132-105">por [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2f132-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="2f132-106">Este tópico descreve como impor a autorização em uma conexão persistente.</span><span class="sxs-lookup"><span data-stu-id="2f132-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="2f132-107">Para obter informações gerais sobre como integrar a segurança em um aplicativo Signalr, consulte [introdução à segurança](introduction-to-security.md).</span><span class="sxs-lookup"><span data-stu-id="2f132-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="2f132-108">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="2f132-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="2f132-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2f132-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2f132-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2f132-110">.NET 4.5</span></span>
> - <span data-ttu-id="2f132-111">Sinalização versão 2</span><span class="sxs-lookup"><span data-stu-id="2f132-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="2f132-112">Versões anteriores deste tópico</span><span class="sxs-lookup"><span data-stu-id="2f132-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="2f132-113">Para obter informações sobre versões anteriores do Signalr, confira [versões mais antigas do signalr](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="2f132-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2f132-114">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="2f132-114">Questions and comments</span></span>
>
> <span data-ttu-id="2f132-115">Deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="2f132-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2f132-116">Se você tiver dúvidas que não estão diretamente relacionadas ao tutorial, poderá lançá-las no fórum do [signalr ASP.net](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [stackoverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="2f132-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="2f132-117">Impor autorização</span><span class="sxs-lookup"><span data-stu-id="2f132-117">Enforce authorization</span></span>

<span data-ttu-id="2f132-118">Para impor regras de autorização ao usar um [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , você deve substituir o método `AuthorizeRequest`.</span><span class="sxs-lookup"><span data-stu-id="2f132-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="2f132-119">Você não pode usar o atributo `Authorize` com conexões persistentes.</span><span class="sxs-lookup"><span data-stu-id="2f132-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="2f132-120">O método `AuthorizeRequest` é chamado pela estrutura do Signalr antes de cada solicitação para verificar se o usuário está autorizado a executar a ação solicitada.</span><span class="sxs-lookup"><span data-stu-id="2f132-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="2f132-121">O método `AuthorizeRequest` não é chamado a partir do cliente; em vez disso, você autentica o usuário por meio do mecanismo de autenticação padrão do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2f132-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="2f132-122">O exemplo a seguir mostra como limitar solicitações a usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="2f132-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="2f132-123">Você pode adicionar qualquer lógica de autorização personalizada no método AuthorizeRequest; como, verificando se um usuário pertence a uma função específica.</span><span class="sxs-lookup"><span data-stu-id="2f132-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
