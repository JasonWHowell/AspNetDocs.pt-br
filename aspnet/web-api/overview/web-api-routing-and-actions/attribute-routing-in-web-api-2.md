---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Roteamento de atributos na API 2 da Web ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675379"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>Roteamento de atributos na API 2 da Web ASP.NET

por [Mike Wasson](https://github.com/MikeWasson)

*Roteamento* é como a API da Web corresponde a um URI a uma ação. A API 2 da Web suporta um novo tipo de roteamento, chamado *roteamento de atributos*. Como o nome indica, o roteamento de atributos usa atributos para definir rotas. O roteamento de atributos oferece mais controle sobre as URIs em sua API web. Por exemplo, você pode facilmente criar URIs que descrevem hierarquias de recursos.

O estilo anterior de roteamento, chamado de roteamento baseado em convenções, ainda é totalmente suportado. Na verdade, você pode combinar ambas as técnicas no mesmo projeto.

Este tópico mostra como ativar o roteamento de atributos e descreve as várias opções para roteamento de atributos. Para obter um tutorial de ponta a ponta que usa roteamento de atributos, consulte [Criar uma API REST com roteamento de atributos na API 2](create-a-rest-api-with-attribute-routing.md)da Web .

## <a name="prerequisites"></a>Pré-requisitos

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Edição Comunitária, Profissional ou Empresarial

Alternativamente, use o NuGet Package Manager para instalar os pacotes necessários. No menu **Ferramentas** no Visual Studio, selecione **NuGet Package Manager**e selecione Console do **Gerenciador de Pacotes**. Digite o seguinte comando na janela Console do Gerenciador de pacotes:

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>Por que roteamento de atributos?

O primeiro lançamento da API web usou roteamento *baseado em convenções.* Nesse tipo de roteamento, você define um ou mais modelos de rota, que são basicamente strings parametrizadas. Quando o framework recebe uma solicitação, ela corresponde ao URI com o modelo de rota. Para obter mais informações sobre o roteamento baseado em convenções, consulte [Roteamento em ASP.NET API da Web](routing-in-aspnet-web-api.md).

Uma vantagem do roteamento baseado em convenções é que os modelos são definidos em um único lugar, e as regras de roteamento são aplicadas consistentemente em todos os controladores. Infelizmente, o roteamento baseado em convenções torna difícil suportar certos padrões uri que são comuns em APIs RESTful. Por exemplo, os recursos geralmente contêm recursos infantis: os clientes têm pedidos, filmes têm atores, livros têm autores e assim por diante. É natural criar URIs que reflitam essas relações:

`/customers/1/orders`

Esse tipo de URI é difícil de criar usando roteamento baseado em convenções. Embora possa ser feito, os resultados não são bem dimensionados se você tiver muitos controladores ou tipos de recursos.

Com roteamento de atributos, é trivial definir uma rota para este URI. Basta adicionar um atributo à ação do controlador:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

Aqui estão alguns outros padrões que atribuem roteamento facilita.

**Controle de versão de API**

Neste exemplo, "/api/v1/products" seriam encaminhados para um controlador diferente de "/api/v2/produtos".

`/api/v1/products`
`/api/v2/products`

**Segmentos uri sobrecarregados**

Neste exemplo, "1" é um número de pedido, mas "pendente" mapas para uma coleção.

`/orders/1`
`/orders/pending`

**Múltiplos tipos de parâmetros**

Neste exemplo, "1" é um número de pedido, mas "2013/06/16" especifica uma data.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>Ativando o roteamento de atributos

Para habilitar o roteamento de atributos, chame **MapHttpAttributeRoutes** durante a configuração. Este método de extensão é definido na classe **System.Web.HttpConfigurationExtensions.**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

O roteamento de atributos pode ser combinado com o roteamento [baseado em convenções.](routing-in-aspnet-web-api.md) Para definir rotas baseadas em convenções, chame o método **MapHttpRoute.**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Para obter mais informações sobre a configuração da API da Web, consulte [Configuração ASP.NET API 2](../advanced/configuring-aspnet-web-api.md)da Web .

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>Nota: Migrando da API web 1

Antes da API 2 da Web, os modelos de projeto da API da Web geraram código assim:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

Se o roteamento de atributos estiver ativado, este código lançará uma exceção. Se você atualizar um projeto de API da Web existente para usar roteamento de atributos, certifique-se de atualizar esse código de configuração para o seguinte:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> Para obter mais informações, consulte [Configurando a API da Web com ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>Adicionando atributos de rota

Aqui está um exemplo de uma rota definida usando um atributo:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

Os &quot;clientes de string/{customerId}/orders&quot; é o modelo URI para a rota. A API da Web tenta combinar o URI de solicitação com o modelo. Neste exemplo, "clientes" e "pedidos" são segmentos literais, e "{customerId}" é um parâmetro variável. As seguintes URIs corresponderiam a este modelo:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

Você pode restringir a correspondência usando [restrições, descritas](#constraints)mais tarde neste tópico.

Observe que &quot;o parâmetro&quot; {customerId} no modelo de rota corresponde ao nome do parâmetro *id* do cliente no método. Quando a API da Web invoca a ação do controlador, ela tenta vincular os parâmetros de rota. Por exemplo, se `http://example.com/customers/1/orders`o URI estiver, a API da Web tentará vincular o valor "1" ao parâmetro *id do cliente* na ação.

Um modelo URI pode ter vários parâmetros:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

Quaisquer métodos de controlador que não tenham um atributo de rota usam roteamento baseado em convenção. Dessa forma, você pode combinar ambos os tipos de roteamento no mesmo projeto.

## <a name="http-methods"></a>Métodos HTTP

A API da Web também seleciona ações com base no método HTTP da solicitação (GET, POST, etc). Por padrão, a API da Web procura uma correspondência insensível a casos com o início do nome do método do controlador. Por exemplo, um `PutCustomers` método de controlador chamado corresponde a uma solicitação HTTP PUT.

Você pode substituir esta convenção decorando o método com os seguintes atributos:

- **[HttpDelete]**
- **[HttpGet]**
- **[Httphead]**
- **[Opções http]**
- **[HttpPatch]**
- **[HttpPost]**
- **[HttpPut]**

O exemplo a seguir mapeia o método CreateBook para solicitações HTTP POST.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

Para todos os outros métodos HTTP, incluindo métodos não padronizados, use o atributo **AcceptVerbs,** que leva uma lista de métodos HTTP.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>Prefixos de rota

Muitas vezes, as rotas em um controlador começam com o mesmo prefixo. Por exemplo:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

Você pode definir um prefixo comum para um controlador inteiro usando o atributo **[RoutePrefix]:**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

Use um tilde (~) no atributo do método para substituir o prefixo de rota:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

O prefixo de rota pode incluir parâmetros:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>Restrições de rota

As restrições de rota permitem restringir a forma como os parâmetros no modelo de rota são compatíveis. A sintaxe &quot;geral é {parâmetro:restrição}&quot;. Por exemplo:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

Aqui, a primeira rota só &quot;será&quot; selecionada se o segmento de id do URI for um inteiro. Caso contrário, a segunda rota será escolhida.

A tabela a seguir lista as restrições suportadas.

| Constraint | Descrição | Exemplo |
| --- | --- | --- |
| alpha | Corresponde aos caracteres do alfabeto latino maiúsculo ou minúsculo (a-z, A-Z) | {x:alfa} |
| bool | Combina com um valor booleano. | {x:bool} |
| DATETIME | Corresponde a um valor **de Hora de Data.** | {x:hora de data} |
| decimal | Corresponde a um valor decimal. | {x:decimal} |
| double | Corresponde a um valor de 64 bits de ponto flutuante. | {x:double} |
| FLOAT | Corresponde a um valor de ponto flutuante de 32 bits. | {x:float} |
| guid | Corresponde a um valor GUID. | {x:guid} |
| INT | Corresponde a um valor inteiro de 32 bits. | {x:int} |
| comprimento | Corresponde a uma seqüência com o comprimento especificado ou dentro de um intervalo especificado de comprimentos. | {x:comprimento(6)} {x:comprimento(1,20)} |
| long | Corresponde a um valor inteiro de 64 bits. | {x:long} |
| max | Corresponde a um inteiro com um valor máximo. | {x:max(10)} |
| Maxlength | Combina uma corda com um comprimento máximo. | {x:comprimento máximo(10)} |
| Min | Corresponde a um inteiro com um valor mínimo. | {x:min(10)} |
| Minlength | Combina uma corda com um comprimento mínimo. | {x:minlength(10)} |
| range | Corresponde a um inteiro dentro de uma faixa de valores. | {x:intervalo(10,50)} |
| regex | Corresponde a uma expressão regular. | {x:regex(^\d{3}-\d{3}-\d{4}$)} |

Observe que algumas das restrições, &quot;&quot;como min, tomam argumentos entre parênteses. Você pode aplicar múltiplas restrições a um parâmetro, separado por um cólon.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>Restrições de rota personalizadas

Você pode criar restrições de rota personalizadas implementando a interface **IHttpRouteConstraint.** Por exemplo, a seguinte restrição restringe um parâmetro a um valor inteiro não zero.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

O código a seguir mostra como registrar a restrição:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

Agora você pode aplicar a restrição em suas rotas:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

Você também pode substituir toda a classe **DefaultInlineConstraintResolver** implementando a interface **IInlineResolverResolver.** Isso substituirá todas as restrições incorporadas, a menos que sua implementação do **IInlineConstraintResolver** as adicione especificamente.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>Parâmetros e valores padrão opcionais do URI

Você pode tornar um parâmetro URI opcional adicionando um ponto de interrogação ao parâmetro de rota. Se um parâmetro de rota for opcional, você deve definir um valor padrão para o parâmetro do método.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

Neste exemplo, `/api/books/locale/1033` `/api/books/locale` e retorne o mesmo recurso.

Alternativamente, você pode especificar um valor padrão dentro do modelo de rota, da seguinte forma:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

Isso é quase o mesmo que o exemplo anterior, mas há uma pequena diferença de comportamento quando o valor padrão é aplicado.

- No primeiro exemplo ("{lcid:int?}"), o valor padrão de 1033 é atribuído diretamente ao parâmetro do método, de modo que o parâmetro terá esse valor exato.
- No segundo exemplo ("{lcid:int=1033}"), o valor padrão de "1033" passa pelo processo de vinculação do modelo. O aglutinante modelo padrão converterá "1033" para o valor numérico 1033. No entanto, você pode conectar um fichário de modelo personalizado, que pode fazer algo diferente.

(Na maioria dos casos, a menos que você tenha aglutinantes de modelo personalizados em seu pipeline, as duas formas serão equivalentes.)

<a id="route-names"></a>
## <a name="route-names"></a>Nomes de rotas

Na Web API, cada rota tem um nome. Os nomes de rota são úteis para gerar links, para que você possa incluir um link em uma resposta HTTP.

Para especificar o nome da rota, defina a propriedade **Nome** no atributo. O exemplo a seguir mostra como definir o nome da rota e também como usar o nome da rota ao gerar um link.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>Ordem de Rota

Quando a estrutura tenta combinar um URI com uma rota, ele avalia as rotas em uma ordem específica. Para especificar a ordem, defina a propriedade **Order** no atributo route. Valores mais baixos são avaliados primeiro. O valor padrão do pedido é zero.

Veja como o pedido total é determinado:

1. Compare a propriedade **Order** do atributo route.
2. Veja cada segmento URI no modelo de rota. Para cada segmento, a ordem é a seguinte:

    1. Segmentos literais.
    2. Parâmetros de rota com restrições.
    3. Parâmetros de rota sem restrições.
    4. Segmentos de parâmetros curinga com restrições.
    5. Segmentos de parâmetros curinga sem restrições.
3. No caso de um empate, as rotas são ordenadas por uma comparação de stringordinal insensível[(OrdinalIgnoreCase)](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)do modelo de rota.

Veja um exemplo. Suponha que você defina o seguinte controlador:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

Essas rotas são ordenadas da seguinte forma.

1. ordens/detalhes
2. ordens/{id}
3. pedidos/{nome do cliente}
4. ordens/{\*data}
5. ordens/pendências

Observe que "detalhes" é um segmento literal e aparece antes de "{id}", mas "pendente" aparece por último porque a propriedade **Order** é 1. (Este exemplo pressupõe que não há clientes chamados "detalhes" ou "pendentes". Em geral, tente evitar rotas ambíguas. Neste exemplo, um modelo `GetByCustomer` de rota melhor para é "customers/{customerName}" )
