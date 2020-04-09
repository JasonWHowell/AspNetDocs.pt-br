---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Roteamento em ASP.NET API web | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676128"
---
# <a name="routing-in-aspnet-web-api"></a>Roteamento no ASP.NET Web API

por [Mike Wasson](https://github.com/MikeWasson)

Este artigo descreve como ASP.NET API da Web encaminha solicitações HTTP aos controladores.

> [!NOTE]
> Se você está familiarizado com ASP.NET MVC, o roteamento da API da Web é muito semelhante ao roteamento mvc. A principal diferença é que a API da Web usa o verbo HTTP, não o caminho URI, para selecionar a ação. Você também pode usar roteamento no estilo MVC na API da Web. Este artigo não assume qualquer conhecimento de ASP.NET MVC.

## <a name="routing-tables"></a>Tabelas de roteamento

Em ASP.NET API da Web, um *controlador* é uma classe que lida com solicitações HTTP. Os métodos públicos do controlador são chamados *métodos* de ação ou simplesmente *ações.* Quando a estrutura da API da Web recebe uma solicitação, ela encaminha a solicitação para uma ação.

Para determinar qual ação invocar, a estrutura usa uma *tabela de roteamento*. O modelo de projeto do Visual Studio para API web cria uma rota padrão:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

Essa rota é definida no *arquivo WebApiConfig.cs,* que é colocado no diretório *\_App Start:*

![](routing-in-aspnet-web-api/_static/image1.png)

Para obter mais `WebApiConfig` informações sobre a classe, consulte [Configuração ASP.NET API da Web](../advanced/configuring-aspnet-web-api.md).

Se você auto-hospedar a API da Web, você `HttpSelfHostConfiguration` deve definir a tabela de roteamento diretamente no objeto. Para obter mais informações, consulte [Auto-host de uma API da Web](../older-versions/self-host-a-web-api.md).

Cada entrada na tabela de roteamento contém um *modelo de rota*. O modelo de rota padrão &quot;para API da Web é&quot;api/{controller}/{id} . Neste modelo, &quot;a&quot; api é um segmento de caminho literal, e {controller} e {id} são variáveis de espaço reservado.

Quando a estrutura da API da Web recebe uma solicitação HTTP, ela tenta igualar o URI com um dos modelos de rota na tabela de roteamento. Se nenhuma rota corresponder, o cliente recebe um erro de 404. Por exemplo, as SEGUINTES URIs correspondem à rota padrão:

- /api/contatos
- /api/contatos/1
- /api/products/gizmo1

No entanto, o SEGUINTE URI não &quot;corresponde,&quot; pois não possui o segmento de API:

- /contatos/1

> [!NOTE]
> A razão para o uso de "api" na rota é evitar colisões com ASP.NET roteamento MVC. Dessa forma, você &quot;pode&quot; ter /contatos ir &quot;para um controlador&quot; MVC, e /api/contatos ir para um controlador de API da Web. Claro, se você não gosta desta convenção, você pode alterar a tabela de rotas padrão.

Uma vez que uma rota correspondente é encontrada, a API da Web seleciona o controlador e a ação:

- Para encontrar o controlador, &quot;a&quot; API da Web adiciona o Controller ao valor da variável *{controller}.*
- Para encontrar a ação, a API da Web olha para o verbo HTTP e, em seguida, procura uma ação cujo nome começa com esse nome http verbo. Por exemplo, com uma solicitação GET, a API &quot;&quot;da Web &quot;procura&quot; &quot;uma ação&quot;prefixada com Get , como GetContact ou GetAllContacts . Esta convenção se aplica apenas aos verbos GET, POST, PUT, DELETE, HEAD, OPTIONS e PATCH. Você pode habilitar outros verbos HTTP usando atributos em seu controlador. Veremos um exemplo disso mais tarde.
- Outras variáveis de espaço reservado no modelo de rota, como *{id},* são mapeadas para parâmetros de ação.

Vamos examinar um exemplo. Suponha que você defina o seguinte controlador:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

Aqui estão algumas possíveis solicitações HTTP, juntamente com a ação que é invocada para cada um:

| Verbo HTTP | Caminho URI | Ação | Parâmetro |
| --- | --- | --- | --- |
| GET | api/produtos | GetAllProducts | *(nenhum)* |
| GET | api/produtos/4 | GetProductById | 4 |
| Delete (excluir) | api/produtos/4 | Excluirproduto | 4 |
| POST | api/produtos | *(sem correspondência)* |  |

Observe que o segmento *{id}* do URI, se presente, é mapeado para o parâmetro *id* da ação. Neste exemplo, o controlador define dois métodos GET, um com um parâmetro *de id* e outro sem parâmetros.

Além disso, observe que a solicitação POST falhará, pois o controlador não define um &quot;Post... &quot; método.

## <a name="routing-variations"></a>Variações de roteamento

A seção anterior descreveu o mecanismo básico de roteamento para ASP.NET API da Web. Esta seção descreve algumas variações.

### <a name="http-verbs"></a>Verbos HTTP

Em vez de usar a convenção de nomeação para verbos HTTP, você pode especificar explicitamente o verbo HTTP para uma ação decorando o método de ação com um dos seguintes atributos:

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

No exemplo a `FindProduct` seguir, o método é mapeado para obter solicitações:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

Para permitir vários verbos HTTP para uma ação, ou para permitir verbos HTTP que não sejam `[AcceptVerbs]` GET, PUT, POST, DELETE, HEAD, OPTIONS e PATCH, use o atributo, que leva uma lista de verbos HTTP.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>Roteamento por Nome de Ação

Com o modelo de roteamento padrão, a API da Web usa o verbo HTTP para selecionar a ação. No entanto, você também pode criar uma rota onde o nome de ação está incluído no URI:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

Neste modelo de rota, o parâmetro *{action}* nomeia o método de ação no controlador. Com este estilo de roteamento, use atributos para especificar os verbos HTTP permitidos. Por exemplo, suponha que seu controlador tenha o seguinte método:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

Neste caso, uma solicitação GET para "api/products/details/1" seria mapeada para o `Details` método. Este estilo de roteamento é semelhante ao ASP.NET MVC, e pode ser apropriado para uma API no estilo RPC.

Você pode substituir o nome `[ActionName]` de ação usando o atributo. No exemplo a seguir, existem &quot;duas ações que mapeiam para api/products/miniatura/*id*. Um suporta GET e o outro suporta POST:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>Não-Ações

Para evitar que um método seja invocado `[NonAction]` como ação, use o atributo. Isso sinaliza para a estrutura que o método não é uma ação, mesmo que de outra forma corresponda às regras de roteamento.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>Leitura adicional

Este tópico forneceu uma visão de alto nível do roteamento. Para obter mais detalhes, consulte [Roteamento e Seleção de Ação](routing-and-action-selection.md), que descreve exatamente como a estrutura corresponde a um URI a uma rota, seleciona um controlador e, em seguida, seleciona a ação para invocar.
