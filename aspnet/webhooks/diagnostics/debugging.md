---
uid: webhooks/diagnostics/debugging
title: ASP.NET webhooks depuração | Microsoft Docs
author: rick-anderson
description: Como depurar ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675378"
---
# <a name="aspnet-webhooks-debugging"></a>ASP.NET depuração de WebHooks

## <a name="debugging-in-azure"></a>Depuração no Azure

Para depurar seu Aplicativo web durante a execução no Azure, consulte o tutorial [Solução de problemas de um aplicativo web no Azure App Service usando o Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="debugging-with-source-and-symbols"></a>Depuração com Origem e Símbolos

Além de depurar seu próprio código, é possível depurar diretamente no Microsoft ASP.NET WebHooks e, de fato, em todos os .NET. Isso funciona independentemente de você depurar localmente ou remotamente. Primeiro, configure o Visual Studio para encontrar a origem e os símbolos indo para **Depurar** e, em seguida, **Opções e Configurações**. Defina as opções assim:

![Opções e Configurações](_static/SourceSymbols.png)

Em seguida, adicione um link ao [symbolsource.org](http://symbolsource.org) para baixar a origem e os símbolos. Vá para a guia **Símbolos** do menu acima e adicione o seguinte como um local de símbolo:

```
http://srv.symbolsource.org/pdb/Public
```

Além disso, certifique-se de que o diretório de cache tenha um nome curto; caso contrário, os nomes dos arquivos podem ficar muito longos, o que fará com que os símbolos não sejam carregados. Um caminho de amostra é:

```
C:\SymCache
```

As configurações devem ser semelhantes a esta:

![Exemplo de localização do arquivo do símbolo de opções](_static/SymSource.png)
