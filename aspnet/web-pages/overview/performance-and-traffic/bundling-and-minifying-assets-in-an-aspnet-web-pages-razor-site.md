---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: Agrupamento e Minificação de Ativos em um site de páginas da Web ASP.NET (Razor) | Microsoft Docs
author: rick-anderson
description: Agrupamento e minificação são maneiras de tornar seu site mais rápido. O agrupamento permite combinar vários arquivos JavaScript (.js) ou várias folhas de estilo em cascata (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 2a877c1e1a06ea2357f96b37ec4ae72f9f9c9ff3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81539903"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="3de05-104">Agrupamento e minificação de ativos em um site de Páginas da Web do ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="3de05-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="3de05-105">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3de05-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3de05-106">Agrupamento e minificação são maneiras de tornar seu site mais rápido.</span><span class="sxs-lookup"><span data-stu-id="3de05-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="3de05-107">O agrupamento permite combinar vários arquivos JavaScript *(.js)* ou vários arquivos de folha de estilo em cascata *(.css)* para que eles possam ser baixados como uma unidade, em vez de um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="3de05-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="3de05-108">A minificação espreme o espaço em branco e realiza outros tipos de compressão para tornar os arquivos baixados o menor possível.</span><span class="sxs-lookup"><span data-stu-id="3de05-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="3de05-109">A versão RC de ASP.NET Páginas da Web 2 não suporta agrupamento e minificação porque o pacote que contém os elementos necessários ainda não está disponível no Microsoft WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="3de05-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="3de05-110">Pedimos desculpas por esta inconveniência.</span><span class="sxs-lookup"><span data-stu-id="3de05-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="3de05-111">Espera-se que o pacote esteja disponível na versão final de ASP.NET Páginas da Web 2 e WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="3de05-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
