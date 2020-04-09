---
uid: webhooks/receiving/handlers
title: ASP.NET manipuladores WebHooks | Microsoft Docs
author: rick-anderson
description: Como lidar com solicitações em ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675214"
---
# <a name="aspnet-webhooks-handlers"></a>ASP.NET manipuladores WebHooks

Uma vez que as solicitações do WebHooks foram validadas por um receptor WebHook, ela está pronta para ser processada pelo código do usuário. É aqui que *os manipuladores* entram. Os manipuladores derivam da interface [IWebHookHandler,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) mas normalmente usa a classe [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) em vez de derivar diretamente da interface.

Uma solicitação do WebHook pode ser processada por um ou mais manipuladores. Os manipuladores são chamados em ordem com base em suas respectivas propriedades *de Ordem* indo do mais baixo para o mais alto onde a Ordem é um inteiro simples (sugerido ser entre 1 e 100):

![Diagrama de propriedade da ordem do manipulador webhook](_static/Handlers.png)

Um manipulador pode definir opcionalmente a propriedade *Response* no WebHookHandlerContext, o que levará o processamento a parar e a resposta a ser enviada de volta como a resposta HTTP ao WebHook. No caso acima, o Manipulador C não será chamado porque tem uma ordem maior do que B e B define a resposta.

Definir a resposta é normalmente apenas relevante para WebHooks onde a resposta pode levar as informações de volta para a API de origem. Este é, por exemplo, o caso do Slack WebHooks, onde a resposta é postada de volta ao canal de onde o WebHook veio. Os manipuladores podem definir a propriedade Receiver se quiserem receber WebHooks desse receptor em particular. Se eles não definirem o receptor eles são chamados para todos eles.

Outro uso comum de uma resposta é usar uma resposta *410 Gone* para indicar que o WebHook não está mais ativo e nenhuma solicitação adicional deve ser enviada.

Por padrão, um manipulador será chamado por todos os receptores WebHook. No entanto, se a propriedade *Receiver* estiver definida como nome de um manipulador, esse manipulador só receberá solicitações do WebHook desse receptor.

## <a name="processing-a-webhook"></a>Processando um WebHook

Quando um manipulador é chamado, ele recebe um [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) contendo informações sobre a solicitação do WebHook. Os dados, normalmente o corpo de solicitação HTTP, estão disponíveis na propriedade *Data.*

O tipo de dados é tipicamente dados de formulário JSON ou HTML, mas é possível lançar para um tipo mais específico, se desejado. Por exemplo, os WebHooks personalizados gerados por ASP.NET WebHooks podem ser lançados para o tipo [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) da seguinte forma:

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a>Processamento em fila

A maioria dos remetentes do WebHook reenviará um WebHook se uma resposta não for gerada dentro de alguns segundos. Isso significa que o seu manipulador deve concluir o processamento dentro desse prazo para que ele não seja chamado novamente.

Se o processamento demorar mais ou for melhor tratado separadamente, o [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) pode ser usado para enviar a solicitação do WebHook para uma fila, por exemplo, [fila de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179353.aspx).

Um esboço de uma implementação [do WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) é fornecido aqui:

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
