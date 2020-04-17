---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Entendendo o processo de execução ASP.NET de MVC | Microsoft Docs
author: rick-anderson
description: Saiba como o framework ASP.NET MVC processa uma solicitação de navegador passo a passo.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541020"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>Noções básicas sobre o processo de execução do ASP.NET MVC

pela [Microsoft](https://github.com/microsoft)

> Saiba como o framework ASP.NET MVC processa uma solicitação de navegador passo a passo.

As solicitações para um aplicativo web baseado em MVC ASP.NET passam primeiro pelo objeto **UrlRoutingModule,** que é um módulo HTTP. Este módulo analisa a solicitação e executa a seleção de rotas. O objeto **UrlRoutingModule** seleciona o primeiro objeto de rota que corresponde à solicitação atual. (Um objeto de rota é uma classe que implementa **routeBase**e é tipicamente uma instância da classe **Route.)** Se nenhuma rota corresponder, o objeto **UrlRoutingModule** não faz nada e permite que a solicitação volte ao processamento regular de solicitações de solicitação de ASP.NET ou IIS.

A partir do objeto **Route** selecionado, o objeto **UrlRoutingModule** obtém o objeto **IRouteHandler** associado ao objeto **Route.** Normalmente, em um aplicativo MVC, esta será uma instância do **MvcRouteHandler**. A instância **IRouteHandler** cria um objeto **IHttpHandler** e passa-o pelo objeto **IHttpContext.** Por padrão, a instância **IHttpHandler** para MVC é o objeto **MvcHandler.** Em seguida, o objeto **MvcHandler** seleciona o controlador que irá lidar com a solicitação.

> [!NOTE]
> Quando um aplicativo Web ASP.NET MVC é executado no IIS 7.0, nenhuma extensão de nome de arquivo é necessária para projetos De MVC. No entanto, no IIS 6.0, o manipulador requer que você mapeie a extensão do nome do arquivo .mvc para o ASP.NET ISAPI DLL.

O módulo e o manipulador são os pontos de entrada para a estrutura mVC ASP.NET. Eles realizam as seguintes ações:

- Selecione o controlador apropriado em um aplicativo Web MVC.
- Obtenha uma instância específica do controlador.
- Ligue para o método **Execute** do controlador.

As seguintes listas das etapas de execução de um projeto Web MVC:

- Receba a primeira solicitação para a aplicação 

    - No arquivo Global.asax, os objetos **Route** são adicionados ao objeto **RouteTable.**
- Executar roteamento 

    - O módulo **UrlRoutingModule** usa o primeiro objeto **Route** correspondente na coleção **RouteTable** para criar o objeto **RouteData,** que ele usa para criar um objeto **RequestContext** (**IHttpContext).**
- Criar manipulador de solicitações MVC 

    - O objeto **MvcRouteHandler** cria uma instância da classe **MvcHandler** e passa-a a instância **RequestContext.**
- Criar controlador 

    - O objeto **MvcHandler** usa a instância **RequestContext** para identificar o objeto **IControllerFactory** (tipicamente uma instância da classe **DefaultControllerFactory)** para criar a instância do controlador com.
- Executar controlador - A instância **MvcHandler** chama o método **executar** do controlador. |
- Invocar ação 

    - A maioria dos controladores herda da classe base **do controlador.** Para os controladores que o fazem, o objeto **ControllerActionInvoker** associado ao controlador determina qual método de ação da classe controladora chamar e, em seguida, chama esse método.
- Resultado de execução 

    - Um método de ação típico pode receber a entrada do usuário, preparar os dados de resposta apropriados e, em seguida, executar o resultado retornando um tipo de resultado. Os tipos de resultados incorporados que podem ser executados incluem os seguintes: **ViewResult** (que renderiza uma exibição e é o tipo de resultado mais usado), **RedirectToRouteResult,** **RedirectResult,** **ContentResult,** **JsonResult**e **EmptyResult**.
