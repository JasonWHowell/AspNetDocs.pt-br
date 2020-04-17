---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana Amostras | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540435"
---
# <a name="katana-samples"></a>Exemplos do Katana

pela [Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Exemplos do Katana

**ASP.NET rotas código** | fonte[de amostra](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
Em alguns aplicativos, você vai querer conectar componentes OWIN na tabela de rota Asp.Net lado a lado com componentes não OWIN. Esta amostra mostra como usar os métodos de extensão RouteCollection MapOwinPath e MapOwinRoute fornecidos pelo Microsoft.Owin.Host.SystemWeb.

**Código** | [fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines) da amostra de ramificações de pipelines  
Os pipelines de processamento de solicitação OWIN não precisam ser lineares, eles podem ser ramificados para processar solicitações de diferentes maneiras. Esta amostra mostra como construir um pipeline de ramificação com base em caminhos de solicitação ou outros dados de solicitação, como cabeçalhos. Esses componentes estão disponíveis no pacote nuget microsoft.Owin.Mapping.

**Custom Server Sample** | [Código-fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) de amostra de servidor personalizado   
Mostra como usar um servidor OWIN personalizado ao hospedar o OWIN por auto-hospedagem.

**Embedded Sample** | [Código-fonte de](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded) amostra incorporado  
Alguns servidores OWIN podem ser executados&quot;dentro do&quot;seu próprio processo (auto-hospedado). Esta amostra mostra como iniciar um aplicativo OWIN usando as ferramentas fornecidas pelo pacote nuget microsoft.Owin.Hosting.

**HelloWorld Sample** | [Código fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld) da amostra helloworld  
OWIN é uma abstração de API de servidor HTTP que permite a portabilidade do aplicativo em vários servidores. Esta amostra demonstra como escrever um aplicativo Hello World usando **alguns invólucros simples** em torno da abstração OWIN crua e executá-lo em um servidor web como ASP.NET.

**Olá Mundo Código** | [Fonte da](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin) amostra Raw OWIN  
Esta amostra demonstra como escrever um aplicativo Hello World usando a abstração **OWIN crua** e executá-la em um servidor web como Asp.Net.

**SignalR Sample** | [Código fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR) da amostra do sinalizador  
Mostra como auto-hospedar signalR usando OWIN / Katana. Para obter mais informações sobre o SignalR auto-hospedagem, consulte [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

**Código** | fonte da amostra de arquivos estáticos[Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
Mostra como suportar solicitações HTTP para arquivos estáticos usando OWIN / Katana.

**Web API** | [Código-fonte da](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) API da Web   
Esta amostra mostra como hospedar OWIN no IIS e adicionar API web ao pipeline OWIN.

**Web Socket Sample** | [Código-fonte](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) da amostra do soquete web   
Mostra como suportar soquetes da Web no OWIN usando a classe [System.Net.WebSockets.WebSockets.WebSocket.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)
