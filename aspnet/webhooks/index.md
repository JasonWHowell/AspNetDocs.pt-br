---
uid: webhooks/index
title: visão geral do ASP.NET WebHooks | Microsoft Docs
author: rick-anderson
description: Uma introdução ao ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675438"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="dce60-103">visão geral do WebHooks ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dce60-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="dce60-104">WebHooks é um padrão HTTP leve que fornece um modelo simples de pub/sub para conectar APIs web e serviços SaaS.</span><span class="sxs-lookup"><span data-stu-id="dce60-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="dce60-105">Quando um evento acontece em um serviço, uma notificação é enviada na forma de uma solicitação HTTP POST para assinantes cadastrados.</span><span class="sxs-lookup"><span data-stu-id="dce60-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="dce60-106">A solicitação POST contém informações sobre o evento, o que torna possível que o receptor atue em conformidade.</span><span class="sxs-lookup"><span data-stu-id="dce60-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="dce60-107">Devido à sua simplicidade, os WebHooks já estão expostos por um grande número de serviços, incluindo [Dropbox,](http://dropbox.com/) [GitHub,](https://www.github.com/) [Bitbucket,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [PayPal,](http://www.paypal.com/) [Slack,](http://www.slack.com) [Stripe,](http://www.stripe.com) [Trello](http://www.trello.com/)e muitos mais.</span><span class="sxs-lookup"><span data-stu-id="dce60-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="dce60-108">Por exemplo, um WebHook pode indicar que um arquivo foi alterado no [Dropbox,](http://dropbox.com/)ou uma alteração de código foi cometida no GitHub, ou um pagamento foi iniciado no [PayPal,](http://www.paypal.com/)ou um cartão foi criado no [Trello](http://www.trello.com/).</span><span class="sxs-lookup"><span data-stu-id="dce60-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="dce60-109">As possibilidades são infinitas!</span><span class="sxs-lookup"><span data-stu-id="dce60-109">The possibilities are endless!</span></span>

<span data-ttu-id="dce60-110">O Microsoft ASP.NET WebHooks facilita o envio e o recebimento de WebHooks como parte do seu aplicativo ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="dce60-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="dce60-111">No lado receptor, ele fornece um modelo comum para receber e processar WebHooks de qualquer número de provedores webhook.</span><span class="sxs-lookup"><span data-stu-id="dce60-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="dce60-112">Ele sai da caixa com suporte para [Dropbox,](http://dropbox.com/) [GitHub,](https://www.github.com/) [Bitbucket,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [PayPal,](http://www.paypal.com/) [Pusher,](http://www.pusher.com) [Salesforce,](http://www.salesforce.com) [Slack,](http://www.slack.com) [Stripe,](http://www.stripe.com) [Trello,](http://www.trello.com/)[WordPress](http://www.wordpress.com) e [Zendesk,](https://www.zendesk.com/) mas é fácil adicionar suporte para mais.</span><span class="sxs-lookup"><span data-stu-id="dce60-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="dce60-113">No lado de envio, ele fornece suporte para gerenciar e armazenar assinaturas, bem como para o envio de notificações de eventos para o conjunto certo de assinantes.</span><span class="sxs-lookup"><span data-stu-id="dce60-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="dce60-114">Isso permite que você defina seu próprio conjunto de eventos que os assinantes podem assinar e notificá-los quando as coisas acontecerem.</span><span class="sxs-lookup"><span data-stu-id="dce60-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="dce60-115">As duas partes podem ser usadas juntas ou separadas, dependendo do seu cenário.</span><span class="sxs-lookup"><span data-stu-id="dce60-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="dce60-116">Se você só precisa receber WebHooks de outros serviços, então você pode usar apenas a parte receptora; se você só quer expor WebHooks para outros consumirem, então você pode fazer exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="dce60-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="dce60-117">O código tem como alvo ASP.NET Web API 2 e ASP.NET MVC 5 e está disponível como [OSS no GitHub](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="dce60-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="dce60-118">Visão geral do WebHooks</span><span class="sxs-lookup"><span data-stu-id="dce60-118">WebHooks Overview</span></span>

<span data-ttu-id="dce60-119">WebHooks é um padrão que significa que ele varia de serviço para serviço, mas a ideia básica é a mesma.</span><span class="sxs-lookup"><span data-stu-id="dce60-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="dce60-120">Você pode pensar no WebHooks como um modelo simples de pub/sub onde um usuário pode se inscrever em eventos acontecendo em outros lugares.</span><span class="sxs-lookup"><span data-stu-id="dce60-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="dce60-121">As notificações do evento são propagadas como solicitações HTTP POST contendo informações sobre o evento em si.</span><span class="sxs-lookup"><span data-stu-id="dce60-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="dce60-122">Normalmente, a solicitação HTTP POST contém um objeto JSON ou dados de formulário HTML determinados pelo remetente WebHook, incluindo informações sobre o evento que fazem com que o WebHook seja acionado.</span><span class="sxs-lookup"><span data-stu-id="dce60-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="dce60-123">Por exemplo, um órgão de solicitação do WebHook POST do [GitHub](https://www.github.com/) se parece com isso como resultado de um novo problema sendo aberto em um repositório específico:</span><span class="sxs-lookup"><span data-stu-id="dce60-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="dce60-124">Para garantir que o WebHook seja de fato do remetente pretendido, a solicitação POST é segurada de alguma forma e, em seguida, verificada pelo receptor.</span><span class="sxs-lookup"><span data-stu-id="dce60-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="dce60-125">Por exemplo, [o GitHub WebHooks](https://developer.github.com/webhooks/) inclui um *cabeçalho HTTP x-hub-signature* com um hash do corpo de solicitação que é verificado pela implementação do receptor para que você não tenha que se preocupar com isso.</span><span class="sxs-lookup"><span data-stu-id="dce60-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="dce60-126">O fluxo do WebHook geralmente é algo assim:</span><span class="sxs-lookup"><span data-stu-id="dce60-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="dce60-127">O remetente WebHook expõe eventos aos que um cliente pode se inscrever.</span><span class="sxs-lookup"><span data-stu-id="dce60-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="dce60-128">Os eventos descrevem alterações observáveis no sistema, por exemplo, que um novo item de dados foi inserido, que um processo foi concluído ou outra coisa.</span><span class="sxs-lookup"><span data-stu-id="dce60-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="dce60-129">O receptor WebHook assina registrando um WebHook que consiste em quatro coisas:</span><span class="sxs-lookup"><span data-stu-id="dce60-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="dce60-130">Um URI para onde a notificação do evento deve ser postada na forma de uma solicitação HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="dce60-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="dce60-131">Um conjunto de filtros descrevendo os eventos específicos para os quais o WebHook deve ser acionado;</span><span class="sxs-lookup"><span data-stu-id="dce60-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="dce60-132">Uma chave secreta que é usada para assinar a solicitação HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="dce60-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="dce60-133">Dados adicionais que devem ser incluídos na solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="dce60-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="dce60-134">Isso pode, por exemplo, ser campos de cabeçalho HTTP adicionais ou propriedades incluídas no órgão de solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="dce60-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="dce60-135">Uma vez que um evento acontece, os registros correspondentes do WebHook são encontrados e as solicitações HTTP POST são enviadas.</span><span class="sxs-lookup"><span data-stu-id="dce60-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="dce60-136">Normalmente, a geração das solicitações HTTP POST são repetidas várias vezes se por algum motivo o destinatário não estiver respondendo ou a solicitação HTTP POST resultar em uma resposta de erro.</span><span class="sxs-lookup"><span data-stu-id="dce60-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="dce60-137">Pipeline de processamento webhooks</span><span class="sxs-lookup"><span data-stu-id="dce60-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="dce60-138">O pipeline de processamento do Microsoft ASP.NET WebHooks para WebHooks de entrada é assim:</span><span class="sxs-lookup"><span data-stu-id="dce60-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET pipeline de processamento webhooks](_static/WebHookReceivers.png)

<span data-ttu-id="dce60-140">Os dois conceitos-chave aqui são *Receptores* e *Manipuladores:*</span><span class="sxs-lookup"><span data-stu-id="dce60-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="dce60-141">*Os receptores* são responsáveis por lidar com o sabor particular do WebHook de um determinado remetente e por aplicar verificações de segurança para garantir que a solicitação do WebHook seja realmente do remetente pretendido.</span><span class="sxs-lookup"><span data-stu-id="dce60-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="dce60-142">*Os manipuladores* são tipicamente onde o código do usuário é executado processando o WebHook em particular.</span><span class="sxs-lookup"><span data-stu-id="dce60-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="dce60-143">Nos nós a seguir, esses conceitos são descritos em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="dce60-143">In the following nodes these concepts are described in more details.</span></span>
