---
uid: webhooks/receiving/dependencies
title: ASP.NET dependências do receptor WebHooks | Microsoft Docs
author: rick-anderson
description: Dependências do receptor e injeção de dependência em ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675209"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET dependências do receptor WebHooks

O ASP.NET WebHooks da Microsoft é projetado com injeção de dependência em mente. A maioria das dependências do sistema pode ser substituída por implementações alternativas usando um motor de injeção de dependência.

Consulte [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) para obter uma lista de dependências do receptor. Se nenhuma dependência tiver sido registrada, uma implementação padrão será usada. Consulte [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) para obter uma lista de implementações padrão.
