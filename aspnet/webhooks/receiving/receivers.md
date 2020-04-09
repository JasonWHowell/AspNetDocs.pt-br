---
uid: webhooks/receiving/receivers
title: ASP.NET receptores WebHooks | Microsoft Docs
author: rick-anderson
description: ASP.NET receptores WebHooks
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675164"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="b5d96-103">ASP.NET receptores WebHooks</span><span class="sxs-lookup"><span data-stu-id="b5d96-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="b5d96-104">Receber WebHooks depende de quem é o remetente.</span><span class="sxs-lookup"><span data-stu-id="b5d96-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="b5d96-105">Às vezes, há etapas adicionais registrando um WebHook verificando se o assinante está realmente ouvindo.</span><span class="sxs-lookup"><span data-stu-id="b5d96-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="b5d96-106">Alguns WebHooks fornecem um modelo push-to-pull onde a solicitação HTTP POST contém apenas uma referência às informações do evento que serão então recuperadas independentemente.</span><span class="sxs-lookup"><span data-stu-id="b5d96-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="b5d96-107">Muitas vezes o modelo de segurança varia bastante.</span><span class="sxs-lookup"><span data-stu-id="b5d96-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="b5d96-108">O objetivo da Microsoft ASP.NET WebHooks é tornar mais simples e consistente conectar sua API sem gastar muito tempo pensando em como lidar com qualquer variante específica de WebHooks.</span><span class="sxs-lookup"><span data-stu-id="b5d96-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="b5d96-109">Um receptor WebHook é responsável por aceitar e verificar WebHooks de um remetente específico.</span><span class="sxs-lookup"><span data-stu-id="b5d96-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="b5d96-110">Um receptor WebHook pode suportar qualquer número de WebHooks, cada um com sua própria configuração.</span><span class="sxs-lookup"><span data-stu-id="b5d96-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="b5d96-111">Por exemplo, o receptor GitHub WebHook pode aceitar WebHooks de qualquer número de repositórios do GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5d96-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="b5d96-112">URIs receptor de webhook</span><span class="sxs-lookup"><span data-stu-id="b5d96-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="b5d96-113">Ao instalar o Microsoft ASP.NET WebHooks, você recebe um controlador WebHook geral que aceita solicitações do WebHook a partir de um número aberto de serviços.</span><span class="sxs-lookup"><span data-stu-id="b5d96-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="b5d96-114">Quando uma solicitação chega, ele escolhe o receptor apropriado que você instalou para manusear um remetente WebHook específico.</span><span class="sxs-lookup"><span data-stu-id="b5d96-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="b5d96-115">O URI deste controlador é o WebHook URI que você registra no serviço e é do formulário:</span><span class="sxs-lookup"><span data-stu-id="b5d96-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="b5d96-116">Por razões de segurança, muitos receptores WebHook exigem que o URI seja um URI *https* e, em alguns casos, ele também deve conter um parâmetro de consulta adicional que é usado para impor que apenas a parte pretendida pode enviar WebHooks para o URI acima.</span><span class="sxs-lookup"><span data-stu-id="b5d96-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="b5d96-117">O `<receiver>` componente é o nome do `github` `slack`receptor, por exemplo, ou .</span><span class="sxs-lookup"><span data-stu-id="b5d96-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="b5d96-118">O *{id}* é um identificador opcional que pode ser usado para identificar uma configuração específica do receptor WebHook.</span><span class="sxs-lookup"><span data-stu-id="b5d96-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="b5d96-119">Isso pode ser usado para registrar N WebHooks com um receptor específico.</span><span class="sxs-lookup"><span data-stu-id="b5d96-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="b5d96-120">Por exemplo, os três URIs a seguir podem ser usados para registrar-se para três WebHooks independentes:</span><span class="sxs-lookup"><span data-stu-id="b5d96-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="b5d96-121">Instalando um receptor WebHook</span><span class="sxs-lookup"><span data-stu-id="b5d96-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="b5d96-122">Para receber webhooks usando WebHooks ASP.NET Microsoft, primeiro você instala o pacote Nuget para o provedor webhook ou provedores de quem deseja receber WebHooks.</span><span class="sxs-lookup"><span data-stu-id="b5d96-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="b5d96-123">Os pacotes Nuget são chamados [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) onde a última parte indica o serviço suportado.</span><span class="sxs-lookup"><span data-stu-id="b5d96-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="b5d96-124">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="b5d96-124">For example</span></span>

<span data-ttu-id="b5d96-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) fornece suporte para receber WebHooks do GitHub e [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) fornece suporte para receber WebHooks gerados por ASP.NET WebHooks.</span><span class="sxs-lookup"><span data-stu-id="b5d96-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="b5d96-126">Fora da caixa você pode encontrar suporte para Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello e WordPress, mas é possível suportar qualquer número de outros provedores.</span><span class="sxs-lookup"><span data-stu-id="b5d96-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="b5d96-127">Configurando um receptor WebHook</span><span class="sxs-lookup"><span data-stu-id="b5d96-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="b5d96-128">Os receptores WebHook são configurados através do inteface [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) e implementações específicas dessa interface podem ser registradas usando qualquer modelo de injeção de dependência.</span><span class="sxs-lookup"><span data-stu-id="b5d96-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="b5d96-129">A implementação padrão usa configurações de aplicativos que podem ser definidas no arquivo Web.config ou, se usar aplicativos web do Azure, podem ser definidas através do [Portal Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b5d96-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Configurações do Aplicativo do Azure](_static/AzureAppSettings.png)

<span data-ttu-id="b5d96-131">O formato para teclas de configuração de aplicativo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b5d96-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="b5d96-132">O valor é uma lista de valores separados por comuma que correspondem aos valores *{id}* para os quais os WebHooks foram registrados, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b5d96-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="b5d96-133">Inicializando um receptor WebHook</span><span class="sxs-lookup"><span data-stu-id="b5d96-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="b5d96-134">Os receptores WebHook são inicializados registrando-os, normalmente na classe estática *WebApiConfig,* por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b5d96-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
