---
uid: webhooks/diagnostics/logging
title: ASP.NET login do WebHooks | Microsoft Docs
author: rick-anderson
description: Como fazer o login ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675351"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET login do WebHooks

O Microsoft ASP.NET O WebHooks usa o registro como forma de relatar problemas e problemas. Os registros padrão são gravados usando [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) onde eles podem ser manged usando [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) como qualquer outro fluxo de log.

Ao implantar seu Aplicativo Web como um aplicativo Web Do Azure, os logs são automaticamente captados e podem ser gerenciados juntamente com qualquer outro [registro do System.Diagnostics.Trace.](https://msdn.microsoft.com/library/system.diagnostics.trace) Para obter [detalhes, consulte Ativar o registro de diagnósticos para aplicativos web no Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

Além disso, os logs podem ser obtidos diretamente de dentro do Visual Studio, conforme descrito em [Troubleshoot a web app in Azure App Service usando o Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="redirecting-logs"></a>Redirecionando logs

Em vez de escrever logs no [System.Diagnostics.Trace,](https://msdn.microsoft.com/library/system.diagnostics.trace)é possível fornecer uma implementação de registro alternativo que pode fazer log diretamente em um gerenciador de log, como [Log4Net](http://logging.apache.org/log4net/) e [NLog](http://nlog-project.org/). Basta fornecer uma implementação do [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) e registrá-lo com um mecanismo de injeção de dependência de sua escolha e ele será captado pela Microsoft ASP.NET WebHooks. Consulte [Dependency Injection em ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) para obter detalhes.
