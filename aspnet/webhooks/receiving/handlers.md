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
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="6f349-103">ASP.NET manipuladores WebHooks</span><span class="sxs-lookup"><span data-stu-id="6f349-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="6f349-104">Uma vez que as solicitações do WebHooks foram validadas por um receptor WebHook, ela está pronta para ser processada pelo código do usuário.</span><span class="sxs-lookup"><span data-stu-id="6f349-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="6f349-105">É aqui que *os manipuladores* entram.</span><span class="sxs-lookup"><span data-stu-id="6f349-105">This is where *handlers* come in.</span></span> <span data-ttu-id="6f349-106">Os manipuladores derivam da interface [IWebHookHandler,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) mas normalmente usa a classe [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) em vez de derivar diretamente da interface.</span><span class="sxs-lookup"><span data-stu-id="6f349-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="6f349-107">Uma solicitação do WebHook pode ser processada por um ou mais manipuladores.</span><span class="sxs-lookup"><span data-stu-id="6f349-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="6f349-108">Os manipuladores são chamados em ordem com base em suas respectivas propriedades *de Ordem* indo do mais baixo para o mais alto onde a Ordem é um inteiro simples (sugerido ser entre 1 e 100):</span><span class="sxs-lookup"><span data-stu-id="6f349-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![Diagrama de propriedade da ordem do manipulador webhook](_static/Handlers.png)

<span data-ttu-id="6f349-110">Um manipulador pode definir opcionalmente a propriedade *Response* no WebHookHandlerContext, o que levará o processamento a parar e a resposta a ser enviada de volta como a resposta HTTP ao WebHook.</span><span class="sxs-lookup"><span data-stu-id="6f349-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="6f349-111">No caso acima, o Manipulador C não será chamado porque tem uma ordem maior do que B e B define a resposta.</span><span class="sxs-lookup"><span data-stu-id="6f349-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="6f349-112">Definir a resposta é normalmente apenas relevante para WebHooks onde a resposta pode levar as informações de volta para a API de origem.</span><span class="sxs-lookup"><span data-stu-id="6f349-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="6f349-113">Este é, por exemplo, o caso do Slack WebHooks, onde a resposta é postada de volta ao canal de onde o WebHook veio.</span><span class="sxs-lookup"><span data-stu-id="6f349-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="6f349-114">Os manipuladores podem definir a propriedade Receiver se quiserem receber WebHooks desse receptor em particular.</span><span class="sxs-lookup"><span data-stu-id="6f349-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="6f349-115">Se eles não definirem o receptor eles são chamados para todos eles.</span><span class="sxs-lookup"><span data-stu-id="6f349-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="6f349-116">Outro uso comum de uma resposta é usar uma resposta *410 Gone* para indicar que o WebHook não está mais ativo e nenhuma solicitação adicional deve ser enviada.</span><span class="sxs-lookup"><span data-stu-id="6f349-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="6f349-117">Por padrão, um manipulador será chamado por todos os receptores WebHook.</span><span class="sxs-lookup"><span data-stu-id="6f349-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="6f349-118">No entanto, se a propriedade *Receiver* estiver definida como nome de um manipulador, esse manipulador só receberá solicitações do WebHook desse receptor.</span><span class="sxs-lookup"><span data-stu-id="6f349-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="6f349-119">Processando um WebHook</span><span class="sxs-lookup"><span data-stu-id="6f349-119">Processing a WebHook</span></span>

<span data-ttu-id="6f349-120">Quando um manipulador é chamado, ele recebe um [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) contendo informações sobre a solicitação do WebHook.</span><span class="sxs-lookup"><span data-stu-id="6f349-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="6f349-121">Os dados, normalmente o corpo de solicitação HTTP, estão disponíveis na propriedade *Data.*</span><span class="sxs-lookup"><span data-stu-id="6f349-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="6f349-122">O tipo de dados é tipicamente dados de formulário JSON ou HTML, mas é possível lançar para um tipo mais específico, se desejado.</span><span class="sxs-lookup"><span data-stu-id="6f349-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="6f349-123">Por exemplo, os WebHooks personalizados gerados por ASP.NET WebHooks podem ser lançados para o tipo [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6f349-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

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

  ## <a name="queued-processing"></a><span data-ttu-id="6f349-124">Processamento em fila</span><span class="sxs-lookup"><span data-stu-id="6f349-124">Queued Processing</span></span>

<span data-ttu-id="6f349-125">A maioria dos remetentes do WebHook reenviará um WebHook se uma resposta não for gerada dentro de alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="6f349-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="6f349-126">Isso significa que o seu manipulador deve concluir o processamento dentro desse prazo para que ele não seja chamado novamente.</span><span class="sxs-lookup"><span data-stu-id="6f349-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="6f349-127">Se o processamento demorar mais ou for melhor tratado separadamente, o [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) pode ser usado para enviar a solicitação do WebHook para uma fila, por exemplo, [fila de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f349-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="6f349-128">Um esboço de uma implementação [do WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) é fornecido aqui:</span><span class="sxs-lookup"><span data-stu-id="6f349-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

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
