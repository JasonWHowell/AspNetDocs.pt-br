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
# <a name="aspnet-webhooks-overview"></a>visão geral do WebHooks ASP.NET

WebHooks é um padrão HTTP leve que fornece um modelo simples de pub/sub para conectar APIs web e serviços SaaS. Quando um evento acontece em um serviço, uma notificação é enviada na forma de uma solicitação HTTP POST para assinantes cadastrados. A solicitação POST contém informações sobre o evento, o que torna possível que o receptor atue em conformidade.

Devido à sua simplicidade, os WebHooks já estão expostos por um grande número de serviços, incluindo [Dropbox,](http://dropbox.com/) [GitHub,](https://www.github.com/) [Bitbucket,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [PayPal,](http://www.paypal.com/) [Slack,](http://www.slack.com) [Stripe,](http://www.stripe.com) [Trello](http://www.trello.com/)e muitos mais. Por exemplo, um WebHook pode indicar que um arquivo foi alterado no [Dropbox,](http://dropbox.com/)ou uma alteração de código foi cometida no GitHub, ou um pagamento foi iniciado no [PayPal,](http://www.paypal.com/)ou um cartão foi criado no [Trello](http://www.trello.com/). As possibilidades são infinitas!

O Microsoft ASP.NET WebHooks facilita o envio e o recebimento de WebHooks como parte do seu aplicativo ASP.NET:

* No lado receptor, ele fornece um modelo comum para receber e processar WebHooks de qualquer número de provedores webhook. Ele sai da caixa com suporte para [Dropbox,](http://dropbox.com/) [GitHub,](https://www.github.com/) [Bitbucket,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [PayPal,](http://www.paypal.com/) [Pusher,](http://www.pusher.com) [Salesforce,](http://www.salesforce.com) [Slack,](http://www.slack.com) [Stripe,](http://www.stripe.com) [Trello,](http://www.trello.com/)[WordPress](http://www.wordpress.com) e [Zendesk,](https://www.zendesk.com/) mas é fácil adicionar suporte para mais.

* No lado de envio, ele fornece suporte para gerenciar e armazenar assinaturas, bem como para o envio de notificações de eventos para o conjunto certo de assinantes. Isso permite que você defina seu próprio conjunto de eventos que os assinantes podem assinar e notificá-los quando as coisas acontecerem.

As duas partes podem ser usadas juntas ou separadas, dependendo do seu cenário. Se você só precisa receber WebHooks de outros serviços, então você pode usar apenas a parte receptora; se você só quer expor WebHooks para outros consumirem, então você pode fazer exatamente isso.

O código tem como alvo ASP.NET Web API 2 e ASP.NET MVC 5 e está disponível como [OSS no GitHub](https://github.com/aspnet/WebHooks).

## <a name="webhooks-overview"></a>Visão geral do WebHooks

WebHooks é um padrão que significa que ele varia de serviço para serviço, mas a ideia básica é a mesma. Você pode pensar no WebHooks como um modelo simples de pub/sub onde um usuário pode se inscrever em eventos acontecendo em outros lugares. As notificações do evento são propagadas como solicitações HTTP POST contendo informações sobre o evento em si.

Normalmente, a solicitação HTTP POST contém um objeto JSON ou dados de formulário HTML determinados pelo remetente WebHook, incluindo informações sobre o evento que fazem com que o WebHook seja acionado. Por exemplo, um órgão de solicitação do WebHook POST do [GitHub](https://www.github.com/) se parece com isso como resultado de um novo problema sendo aberto em um repositório específico:

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

Para garantir que o WebHook seja de fato do remetente pretendido, a solicitação POST é segurada de alguma forma e, em seguida, verificada pelo receptor. Por exemplo, [o GitHub WebHooks](https://developer.github.com/webhooks/) inclui um *cabeçalho HTTP x-hub-signature* com um hash do corpo de solicitação que é verificado pela implementação do receptor para que você não tenha que se preocupar com isso.

O fluxo do WebHook geralmente é algo assim:

* O remetente WebHook expõe eventos aos que um cliente pode se inscrever. Os eventos descrevem alterações observáveis no sistema, por exemplo, que um novo item de dados foi inserido, que um processo foi concluído ou outra coisa.

* O receptor WebHook assina registrando um WebHook que consiste em quatro coisas:

     1. Um URI para onde a notificação do evento deve ser postada na forma de uma solicitação HTTP POST;

     2. Um conjunto de filtros descrevendo os eventos específicos para os quais o WebHook deve ser acionado;

     3. Uma chave secreta que é usada para assinar a solicitação HTTP POST;

     4. Dados adicionais que devem ser incluídos na solicitação HTTP POST. Isso pode, por exemplo, ser campos de cabeçalho HTTP adicionais ou propriedades incluídas no órgão de solicitação HTTP POST.

* Uma vez que um evento acontece, os registros correspondentes do WebHook são encontrados e as solicitações HTTP POST são enviadas. Normalmente, a geração das solicitações HTTP POST são repetidas várias vezes se por algum motivo o destinatário não estiver respondendo ou a solicitação HTTP POST resultar em uma resposta de erro.

## <a name="webhooks-processing-pipeline"></a>Pipeline de processamento webhooks

O pipeline de processamento do Microsoft ASP.NET WebHooks para WebHooks de entrada é assim:

![ASP.NET pipeline de processamento webhooks](_static/WebHookReceivers.png)

Os dois conceitos-chave aqui são *Receptores* e *Manipuladores:*

* *Os receptores* são responsáveis por lidar com o sabor particular do WebHook de um determinado remetente e por aplicar verificações de segurança para garantir que a solicitação do WebHook seja realmente do remetente pretendido.

* *Os manipuladores* são tipicamente onde o código do usuário é executado processando o WebHook em particular.

Nos nós a seguir, esses conceitos são descritos em mais detalhes.
