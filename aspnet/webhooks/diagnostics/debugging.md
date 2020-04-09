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
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="d8d05-103">ASP.NET depuração de WebHooks</span><span class="sxs-lookup"><span data-stu-id="d8d05-103">ASP.NET WebHooks debugging</span></span>

## <a name="debugging-in-azure"></a><span data-ttu-id="d8d05-104">Depuração no Azure</span><span class="sxs-lookup"><span data-stu-id="d8d05-104">Debugging in Azure</span></span>

<span data-ttu-id="d8d05-105">Para depurar seu Aplicativo web durante a execução no Azure, consulte o tutorial [Solução de problemas de um aplicativo web no Azure App Service usando o Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span><span class="sxs-lookup"><span data-stu-id="d8d05-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="d8d05-106">Depuração com Origem e Símbolos</span><span class="sxs-lookup"><span data-stu-id="d8d05-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="d8d05-107">Além de depurar seu próprio código, é possível depurar diretamente no Microsoft ASP.NET WebHooks e, de fato, em todos os .NET.</span><span class="sxs-lookup"><span data-stu-id="d8d05-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="d8d05-108">Isso funciona independentemente de você depurar localmente ou remotamente.</span><span class="sxs-lookup"><span data-stu-id="d8d05-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="d8d05-109">Primeiro, configure o Visual Studio para encontrar a origem e os símbolos indo para **Depurar** e, em seguida, **Opções e Configurações**.</span><span class="sxs-lookup"><span data-stu-id="d8d05-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="d8d05-110">Defina as opções assim:</span><span class="sxs-lookup"><span data-stu-id="d8d05-110">Set the options like this:</span></span>

![Opções e Configurações](_static/SourceSymbols.png)

<span data-ttu-id="d8d05-112">Em seguida, adicione um link ao [symbolsource.org](http://symbolsource.org) para baixar a origem e os símbolos.</span><span class="sxs-lookup"><span data-stu-id="d8d05-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="d8d05-113">Vá para a guia **Símbolos** do menu acima e adicione o seguinte como um local de símbolo:</span><span class="sxs-lookup"><span data-stu-id="d8d05-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="d8d05-114">Além disso, certifique-se de que o diretório de cache tenha um nome curto; caso contrário, os nomes dos arquivos podem ficar muito longos, o que fará com que os símbolos não sejam carregados.</span><span class="sxs-lookup"><span data-stu-id="d8d05-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="d8d05-115">Um caminho de amostra é:</span><span class="sxs-lookup"><span data-stu-id="d8d05-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="d8d05-116">As configurações devem ser semelhantes a esta:</span><span class="sxs-lookup"><span data-stu-id="d8d05-116">The settings should look similar to this:</span></span>

![Exemplo de localização do arquivo do símbolo de opções](_static/SymSource.png)
