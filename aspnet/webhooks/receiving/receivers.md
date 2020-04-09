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
# <a name="aspnet-webhooks-receivers"></a>ASP.NET receptores WebHooks

Receber WebHooks depende de quem é o remetente. Às vezes, há etapas adicionais registrando um WebHook verificando se o assinante está realmente ouvindo. Alguns WebHooks fornecem um modelo push-to-pull onde a solicitação HTTP POST contém apenas uma referência às informações do evento que serão então recuperadas independentemente. Muitas vezes o modelo de segurança varia bastante.

O objetivo da Microsoft ASP.NET WebHooks é tornar mais simples e consistente conectar sua API sem gastar muito tempo pensando em como lidar com qualquer variante específica de WebHooks.

Um receptor WebHook é responsável por aceitar e verificar WebHooks de um remetente específico. Um receptor WebHook pode suportar qualquer número de WebHooks, cada um com sua própria configuração. Por exemplo, o receptor GitHub WebHook pode aceitar WebHooks de qualquer número de repositórios do GitHub.

## <a name="webhook-receiver-uris"></a>URIs receptor de webhook

Ao instalar o Microsoft ASP.NET WebHooks, você recebe um controlador WebHook geral que aceita solicitações do WebHook a partir de um número aberto de serviços. Quando uma solicitação chega, ele escolhe o receptor apropriado que você instalou para manusear um remetente WebHook específico.

O URI deste controlador é o WebHook URI que você registra no serviço e é do formulário:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

Por razões de segurança, muitos receptores WebHook exigem que o URI seja um URI *https* e, em alguns casos, ele também deve conter um parâmetro de consulta adicional que é usado para impor que apenas a parte pretendida pode enviar WebHooks para o URI acima.

O `<receiver>` componente é o nome do `github` `slack`receptor, por exemplo, ou .

O *{id}* é um identificador opcional que pode ser usado para identificar uma configuração específica do receptor WebHook. Isso pode ser usado para registrar N WebHooks com um receptor específico. Por exemplo, os três URIs a seguir podem ser usados para registrar-se para três WebHooks independentes:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>Instalando um receptor WebHook

Para receber webhooks usando WebHooks ASP.NET Microsoft, primeiro você instala o pacote Nuget para o provedor webhook ou provedores de quem deseja receber WebHooks. Os pacotes Nuget são chamados [Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) onde a última parte indica o serviço suportado. Por exemplo

[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) fornece suporte para receber WebHooks do GitHub e [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) fornece suporte para receber WebHooks gerados por ASP.NET WebHooks.

Fora da caixa você pode encontrar suporte para Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello e WordPress, mas é possível suportar qualquer número de outros provedores.

## <a name="configuring-a-webhook-receiver"></a>Configurando um receptor WebHook

Os receptores WebHook são configurados através do inteface [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) e implementações específicas dessa interface podem ser registradas usando qualquer modelo de injeção de dependência. A implementação padrão usa configurações de aplicativos que podem ser definidas no arquivo Web.config ou, se usar aplicativos web do Azure, podem ser definidas através do [Portal Azure](https://portal.azure.com/).

![Configurações do Aplicativo do Azure](_static/AzureAppSettings.png)

O formato para teclas de configuração de aplicativo é o seguinte:

```
MS_WebHookReceiverSecret_<receiver>
```

O valor é uma lista de valores separados por comuma que correspondem aos valores *{id}* para os quais os WebHooks foram registrados, por exemplo:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>Inicializando um receptor WebHook

Os receptores WebHook são inicializados registrando-os, normalmente na classe estática *WebApiConfig,* por exemplo:

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
