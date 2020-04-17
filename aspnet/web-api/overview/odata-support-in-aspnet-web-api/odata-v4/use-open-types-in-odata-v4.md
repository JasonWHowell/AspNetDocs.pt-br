---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Tipos abertos em OData v4 com ASP.NET API web | Microsoft Docs
author: rick-anderson
description: No OData v4, um tipo aberto é um tipo estruturado que contém propriedades dinâmicas, além de quaisquer propriedades que são declaradas na definição do tipo. Abrir...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543724"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Abrir tipos em OData v4 com ASP.NET API web

pela [Microsoft](https://github.com/microsoft)

> No OData v4, um *tipo aberto* é um tipo estruturado que contém propriedades dinâmicas, além de quaisquer propriedades que são declaradas na definição do tipo. Os tipos abertos permitem adicionar flexibilidade aos seus modelos de dados. Este tutorial mostra como usar tipos abertos em ASP.NET OData da API da Web.
> 
> Este tutorial pressupõe que você já sabe como criar um ponto final de OData em ASP.NET API da Web. Se não, comece lendo [Crie um OData v4 Endpoint](create-an-odata-v4-endpoint.md) primeiro.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Versões de software usadas no tutorial
> 
> 
> - Web API OData 5.3
> - OData v4

Primeiro, algumas terminologias oData:

- Tipo de entidade: Um tipo estruturado com uma chave.
- Tipo complexo: Um tipo estruturado sem chave.
- Tipo aberto: Um tipo com propriedades dinâmicas. Tanto os tipos de entidades quanto os tipos complexos podem ser abertos.

O valor de uma propriedade dinâmica pode ser um tipo primitivo, tipo complexo ou tipo de enumeração; ou uma coleção de qualquer um desses tipos. Para obter mais informações sobre tipos abertos, consulte a [especificação OData v4](http://www.odata.org/documentation/odata-version-4-0/).

## <a name="install-the-web-odata-libraries"></a>Instale as Bibliotecas Web OData

Use o NuGet Package Manager para instalar as bibliotecas De Dados da API da Web mais recentes. Da janela Console do Gerenciador de Pacotes:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>Definir os tipos de CLR

Comece definindo os modelos EDM como tipos CLR.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Quando o Modelo de Dados de Entidade (EDM) é criado,

- `Category`é um tipo de enumeração.
- `Address`é um tipo complexo. (Ele não tem uma chave, por isso não é um tipo de entidade.)
- `Customer`é um tipo de entidade. (Tem uma chave.)
- `Press`é um tipo complexo aberto.
- `Book`é um tipo de entidade aberta.

Para criar um tipo aberto, o tipo CLR deve ter uma propriedade do tipo `IDictionary<string, object>`, que detém as propriedades dinâmicas.

## <a name="build-the-edm-model"></a>Construa o modelo EDM

Se você usar **o ODataConventionModelBuilder** `Press` para `Book` criar o EDM, e for automaticamente `IDictionary<string, object>` adicionado como tipos abertos, com base na presença de uma propriedade.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Você também pode construir o EDM explicitamente, usando **ODataModelBuilder**.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>Adicionar um controlador de dados odata

Em seguida, adicione um controlador OData. Para este tutorial, usaremos um controlador simplificado que apenas suporta solicitações GET e POST, e usa uma lista na memória para armazenar entidades.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

Observe que `Book` a primeira instância não tem propriedades dinâmicas. A `Book` segunda instância tem as seguintes propriedades dinâmicas:

- "Publicado": Tipo primitivo
- "Autores": Coleção de tipos primitivos
- "Outras Categorias": Coleção de tipos de enumeração.

Além disso, `Press` a `Book` propriedade dessa instância tem as seguintes propriedades dinâmicas:

- "Blog": Tipo primitivo
- "Endereço": Tipo complexo

## <a name="query-the-metadata"></a>Consultar os Metadados

Para obter o documento de metadados oData, envie uma solicitação GET para `~/$metadata`. O corpo de resposta deve ser semelhante a isso:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

A partir do documento de metadados, você pode ver que:

- Para `Book` os `Press` e tipos, `OpenType` o valor do atributo é verdadeiro. Os `Customer` `Address` tipos não têm esse atributo.
- O `Book` tipo de entidade tem três propriedades declaradas: ISBN, Title e Press. Os metadados OData não `Book.Properties` incluem a propriedade da classe CLR.
- Da mesma `Press` forma, o tipo complexo tem apenas duas propriedades declaradas: Nome e Categoria. Os metadados não `Press.DynamicProperties` incluem a propriedade da classe CLR.

## <a name="query-an-entity"></a>Consultar uma Entidade

Para obter o livro com isbn igual a "978-0-7356-7942-9", envie uma solicitação GET para `~/Books('978-0-7356-7942-9')`. O corpo de resposta deve ser semelhante ao seguinte. (Recuado para torná-lo mais legível.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Observe que as propriedades dinâmicas estão incluídas em linha com as propriedades declaradas.

## <a name="post-an-entity"></a>POSTAR uma Entidade

Para adicionar uma entidade do Livro, envie uma solicitação POST para `~/Books`. O cliente pode definir propriedades dinâmicas na carga útil da solicitação.

Aqui está um pedido de exemplo. Observe as propriedades "Preço" e "Publicado".

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Se você definir um ponto de ruptura no método controlador, poderá `Properties` ver que a API da Web adicionou essas propriedades ao dicionário.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Recursos adicionais

[Amostra de tipo aberto de odata](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
