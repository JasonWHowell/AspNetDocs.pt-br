---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Herança de tipo complexo em OData v4 com ASP.NET API web | Microsoft Docs
author: rick-anderson
description: De acordo com a especificação OData v4, um tipo complexo pode herdar de outro tipo complexo. (Um tipo complexo é um tipo estruturado sem uma chave.) API da Web...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543594"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>Herança de tipo complexo em OData v4 com ASP.NET API web

pela [Microsoft](https://github.com/microsoft)

> De acordo com a [especificação](http://www.odata.org/documentation/odata-version-4-0/)OData v4, um tipo complexo pode herdar de outro tipo complexo. (Um tipo *complexo* é um tipo estruturado sem uma chave.) O Web API OData 5.3 suporta herança de tipo complexo.
> 
> Este tópico mostra como construir um modelo de dados de entidade (EDM) com tipos complexos de herança. Para obter o código-fonte completo, consulte [Amostra de Herança do Tipo Complexo OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Versões de software usadas no tutorial
> 
> 
> - Web API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>Hierarquia de Modelos

Para ilustrar a herança de tipo complexa, usaremos a seguinte hierarquia de classe.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`é um tipo complexo abstrato. `Rectangle`, `Triangle`e `Circle` são tipos complexos `Shape` `RoundRectangle` derivados `Rectangle`e derivados de . `Window`é um tipo de `Shape` entidade e contém uma instância.

Aqui estão as classes CLR que definem esses tipos.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>Construa o modelo EDM

Para criar o EDM, você pode usar **o ODataConventionModelBuilder**, que infere as relações de herança dos tipos CLR.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

Você também pode construir o EDM explicitamente, usando **ODataModelBuilder**. Isso requer mais código, mas dá-lhe mais controle sobre o EDM.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

Esses dois exemplos criam o mesmo esquema EDM.

## <a name="metadata-document"></a>Documento de metadados

Aqui está o documento de metadados OData, mostrando herança de tipo complexa.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

A partir do documento de metadados, você pode ver que:

- O `Shape` tipo complexo é abstrato.
- O `Rectangle` `Triangle`tipo `Circle` , e complexo `Shape`tem o tipo de base .
- O `RoundRectangle` tipo tem `Rectangle`o tipo base .

## <a name="casting-complex-types"></a>Tipos complexos de fundição

O casting de tipos complexos agora é suportado. Por exemplo, a consulta a `Shape` seguir `Rectangle`lança a a a .

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

Aqui está a carga de resposta:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
