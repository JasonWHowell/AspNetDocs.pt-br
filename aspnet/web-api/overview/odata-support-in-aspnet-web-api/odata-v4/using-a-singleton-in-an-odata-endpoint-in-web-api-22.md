---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Criar um singleton no OData v4 usando a API Web 2,2 | Microsoft Docs
author: rick-anderson
description: Este tópico mostra como definir um singleton em um ponto de extremidade OData na API Web 2,2.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622083"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>Criar um singleton no OData v4 usando a API Web 2,2

por Zoe Luo

> Tradicionalmente, uma entidade só poderia ser acessada se fosse encapsulada dentro de um conjunto de entidades. Mas o OData v4 fornece duas opções adicionais, singleton e confinamento, que são compatíveis com o WebAPI 2,2.

Este artigo mostra como definir um singleton em um ponto de extremidade OData na API Web 2,2. Para obter informações sobre o que é um singleton e como você pode se beneficiar com o uso dele, consulte [usando um singleton para definir sua entidade especial](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx). Para criar um ponto de extremidade do OData v4 na API Web, consulte [criar um ponto de extremidade do OData v4 usando ASP.NET Web API 2,2](create-an-odata-v4-endpoint.md). 

Criaremos um singleton em seu projeto de API Web usando o seguinte modelo de dados:

![Modelo de dados](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

Um singleton chamado `Umbrella` será definido com base no tipo `Company`e um conjunto de entidades chamado `Employees` será definido com base no tipo `Employee`.

A solução usada neste tutorial pode ser baixada do [codeplex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).

## <a name="define-the-data-model"></a>Definir o modelo de dados

1. Defina os tipos CLR.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. Gere o modelo EDM com base nos tipos CLR.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    Aqui, `builder.Singleton<Company>("Umbrella")` diz ao construtor de modelos para criar um singleton nomeado `Umbrella` no modelo EDM.

    Os metadados gerados serão semelhantes ao seguinte:

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    Dos metadados, podemos ver que a propriedade de navegação `Company` no conjunto de entidades de `Employees` está associada à `Umbrella`singleton. A associação é feita automaticamente pelo `ODataConventionModelBuilder`, já que somente `Umbrella` tem o tipo de `Company`. Se houver qualquer ambiguidade no modelo, você poderá usar `HasSingletonBinding` para associar explicitamente uma propriedade de navegação a um singleton; `HasSingletonBinding` tem o mesmo efeito que usar o atributo `Singleton` na definição de tipo CLR:

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>Definir o controlador singleton

Assim como o controlador de EntitySet, o controlador singleton é herdado de `ODataController`e o nome do controlador singleton deve ser `[singletonName]Controller`.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

Para lidar com diferentes tipos de solicitações, é necessário que as ações sejam predefinidas no controlador. O **Roteamento de atributos** é habilitado por padrão no WebApi 2,2. Por exemplo, para definir uma ação para lidar com a consulta `Revenue` de `Company` usando o roteamento de atributos, use o seguinte:

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

Se você não estiver disposto a definir atributos para cada ação, basta definir suas ações seguindo as [convenções de roteamento OData](../odata-routing-conventions.md). Como uma chave não é necessária para consultar um singleton, as ações definidas no controlador singleton são ligeiramente diferentes das ações definidas no controlador de EntitySet.

Para referência, as assinaturas de método para cada definição de ação no controlador singleton estão listadas abaixo.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

Basicamente, isso é tudo o que você precisa fazer no lado do serviço. O [projeto de exemplo](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contém todo o código para a solução e o cliente OData que mostra como usar o singleton. O cliente é criado seguindo as etapas em [criar um aplicativo cliente do OData v4](create-an-odata-v4-client-app.md).

. 

*Agradecemos ao Leo Hu pelo conteúdo original deste artigo.*
