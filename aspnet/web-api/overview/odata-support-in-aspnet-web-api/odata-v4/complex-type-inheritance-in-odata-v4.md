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
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="92cdd-104">Herança de tipo complexo em OData v4 com ASP.NET API web</span><span class="sxs-lookup"><span data-stu-id="92cdd-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="92cdd-105">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="92cdd-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="92cdd-106">De acordo com a [especificação](http://www.odata.org/documentation/odata-version-4-0/)OData v4, um tipo complexo pode herdar de outro tipo complexo.</span><span class="sxs-lookup"><span data-stu-id="92cdd-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="92cdd-107">(Um tipo *complexo* é um tipo estruturado sem uma chave.) O Web API OData 5.3 suporta herança de tipo complexo.</span><span class="sxs-lookup"><span data-stu-id="92cdd-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="92cdd-108">Este tópico mostra como construir um modelo de dados de entidade (EDM) com tipos complexos de herança.</span><span class="sxs-lookup"><span data-stu-id="92cdd-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="92cdd-109">Para obter o código-fonte completo, consulte [Amostra de Herança do Tipo Complexo OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="92cdd-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="92cdd-110">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="92cdd-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="92cdd-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="92cdd-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="92cdd-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="92cdd-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="92cdd-113">Hierarquia de Modelos</span><span class="sxs-lookup"><span data-stu-id="92cdd-113">Model Hierarchy</span></span>

<span data-ttu-id="92cdd-114">Para ilustrar a herança de tipo complexa, usaremos a seguinte hierarquia de classe.</span><span class="sxs-lookup"><span data-stu-id="92cdd-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="92cdd-115">`Shape`é um tipo complexo abstrato.</span><span class="sxs-lookup"><span data-stu-id="92cdd-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="92cdd-116">`Rectangle`, `Triangle`e `Circle` são tipos complexos `Shape` `RoundRectangle` derivados `Rectangle`e derivados de .</span><span class="sxs-lookup"><span data-stu-id="92cdd-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="92cdd-117">`Window`é um tipo de `Shape` entidade e contém uma instância.</span><span class="sxs-lookup"><span data-stu-id="92cdd-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="92cdd-118">Aqui estão as classes CLR que definem esses tipos.</span><span class="sxs-lookup"><span data-stu-id="92cdd-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="92cdd-119">Construa o modelo EDM</span><span class="sxs-lookup"><span data-stu-id="92cdd-119">Build the EDM Model</span></span>

<span data-ttu-id="92cdd-120">Para criar o EDM, você pode usar **o ODataConventionModelBuilder**, que infere as relações de herança dos tipos CLR.</span><span class="sxs-lookup"><span data-stu-id="92cdd-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="92cdd-121">Você também pode construir o EDM explicitamente, usando **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="92cdd-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="92cdd-122">Isso requer mais código, mas dá-lhe mais controle sobre o EDM.</span><span class="sxs-lookup"><span data-stu-id="92cdd-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="92cdd-123">Esses dois exemplos criam o mesmo esquema EDM.</span><span class="sxs-lookup"><span data-stu-id="92cdd-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="92cdd-124">Documento de metadados</span><span class="sxs-lookup"><span data-stu-id="92cdd-124">Metadata Document</span></span>

<span data-ttu-id="92cdd-125">Aqui está o documento de metadados OData, mostrando herança de tipo complexa.</span><span class="sxs-lookup"><span data-stu-id="92cdd-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="92cdd-126">A partir do documento de metadados, você pode ver que:</span><span class="sxs-lookup"><span data-stu-id="92cdd-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="92cdd-127">O `Shape` tipo complexo é abstrato.</span><span class="sxs-lookup"><span data-stu-id="92cdd-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="92cdd-128">O `Rectangle` `Triangle`tipo `Circle` , e complexo `Shape`tem o tipo de base .</span><span class="sxs-lookup"><span data-stu-id="92cdd-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="92cdd-129">O `RoundRectangle` tipo tem `Rectangle`o tipo base .</span><span class="sxs-lookup"><span data-stu-id="92cdd-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="92cdd-130">Tipos complexos de fundição</span><span class="sxs-lookup"><span data-stu-id="92cdd-130">Casting Complex Types</span></span>

<span data-ttu-id="92cdd-131">O casting de tipos complexos agora é suportado.</span><span class="sxs-lookup"><span data-stu-id="92cdd-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="92cdd-132">Por exemplo, a consulta a `Shape` seguir `Rectangle`lança a a a .</span><span class="sxs-lookup"><span data-stu-id="92cdd-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="92cdd-133">Aqui está a carga de resposta:</span><span class="sxs-lookup"><span data-stu-id="92cdd-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
