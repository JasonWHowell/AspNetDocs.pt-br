---
uid: webhooks/source
title: ASP.NET código-fonte do WebHooks e pacotes NuGet | Microsoft Docs
author: rick-anderson
description: Links para código-fonte ASP.NET WebHooks e pacotes NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675316"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET pacotes de código-fonte webhooks e nuget

O Microsoft ASP.NET WebHooks faz parte da família de módulos microsoft ASP.NET e está hospedado como um [Projeto de Código Aberto no GitHub](https://github.com/aspnet/WebHooks). Isso significa que aceitamos contribuições, mas, por favor, analise as [Diretrizes de Contribuição](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) antes de apresentar um pedido de retirada.

Esta documentação on-line que você está lendo agora também está hospedada como [Open Source no GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) e também aceita contribuições.

## <a name="nuget-packages"></a>Pacotes NuGet

Os [pacotes NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) são divididos em três partes:

* [Comum](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Um pacote comum que é compartilhado entre remetentes e receptores.

* [Remetente](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Um conjunto de pacotes que suportam o envio de seus próprios WebHooks para outros. A funcionalidade para o envio de WebHooks é descrita com mais detalhes no [Envio de WebHooks](sending/senders.md).

* [Receptores](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Um conjunto de pacotes que suportam o recebimento de WebHooks de outros. A funcionalidade para receber WebHooks é descrita com mais detalhes no [Receiving WebHooks](receiving/index.md).
