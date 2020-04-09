---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: Serialização JSON e XML em ASP.NET API web - ASP.NET 4.x
author: MikeWasson
description: Descreve os assuntos de JSON e XML em ASP.NET API web para ASP.NET 4.x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676219"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>Serialização JSON e XML em ASP.NET API web

por [Mike Wasson](https://github.com/MikeWasson)

Este artigo descreve os assuntos formatters JSON e XML em ASP.NET API web.

Em ASP.NET API da Web, um *matéria-matéria do tipo mídia* é um objeto que pode:

- Leia objetos CLR de um corpo de mensagem HTTP
- Escreva objetos CLR em um corpo de mensagem HTTP

A API da Web fornece matérias foroforo tipo mídia tanto para JSON quanto para XML. A estrutura insere esses assuntos no pipeline por padrão. Os clientes podem solicitar JSON ou XML no cabeçalho Aceitar da solicitação HTTP.

## <a name="contents"></a>Conteúdo

- [JSON Media-Type Formatter](#json_media_type_formatter)

    - [Propriedades somente leitura](#json_readonly)
    - [Datas](#json_dates)
    - [Recuo](#json_indenting)
    - [Invólucro de Camelo](#json_camelcasing)
    - [Objetos anônimos e mal digitados](#json_anon)
- [XML Media-Type Formatter](#xml_media_type_formatter)

    - [Propriedades somente leitura](#xml_readonly)
    - [Datas](#xml_dates)
    - [Recuo](#xml_indenting)
    - [Configuração de serializadores XML por tipo](#xml_pertype)
- [Removendo o Formatter JSON ou XML](#removing_the_json_or_xml_formatter)
- [Manuseio de referências circulares de objetos](#handling_circular_object_references)
- [Testando serialização de objetos](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON Media-Type Formatter

A formatação JSON é fornecida pela classe **JsonMediaTypeFormatter.** Por padrão, **jsonMediaTypeFormatter** usa a biblioteca [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) para executar a serialização. Json.NET é um projeto de código aberto de terceiros.

Se preferir, você pode configurar a classe **JsonMediaTypeFormatter** para usar o **DataContractJsonSerializer** em vez de Json.NET. Para isso, defina a propriedade **UseDataContractJsonSerializer** como **verdadeira:**

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>Serialização JSON

Esta seção descreve alguns comportamentos específicos do formatter JSON, usando o serializador [de Json.NET](https://github.com/JamesNK/Newtonsoft.Json) padrão. Esta não se destina a ser uma documentação abrangente da biblioteca Json.NET; para obter mais informações, consulte a [documentação Json.NET](http://james.newtonking.com/projects/json/help/).

#### <a name="what-gets-serialized"></a>O que fica serializado?

Por padrão, todas as propriedades e campos públicos estão incluídos no JSON serializado. Para omitir uma propriedade ou campo, decore-a com o atributo **JsonIgnore.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

Se preferir &quot;uma abordagem opt-in,&quot; decore a classe com o atributo **DataContract.** Se esse atributo estiver presente, os membros serão ignorados a menos que tenham o **DataMember**. Você também pode usar **DataMember** para serializar membros privados.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Propriedades somente leitura

As propriedades somente leitura são serializadas por padrão.

<a id="json_dates"></a>
### <a name="dates"></a>Datas

Por padrão, Json.NET grava datas no formato [ISO 8601.](http://www.w3.org/TR/NOTE-datetime) As datas no UTC (Coordinated Universal Time) são escritas com um sufixo "Z". As datas em horário local incluem um deslocamento por fuso horário. Por exemplo:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

Por padrão, Json.NET preserva o fuso horário. Você pode anular isso definindo a propriedade DateTimeZoneHandling:

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

Se você preferir usar o formato`"\/Date(ticks)\/"`de data Microsoft [JSON](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) ( ) em vez da ISO 8601, defina a propriedade **DateFormatHandling** nas configurações do serializador:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>Recuo

Para gravar JSON recuado, defina a **configuração de formatação** como **Formatação.Recuada:**

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Invólucro de Camelo

Para escrever nomes de propriedade JSON com invólucro de camelo, sem alterar seu modelo de dados, defina o **CamelCasePropertyNamesContractResolver** no serializador:

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>Objetos anônimos e mal digitados

Um método de ação pode retornar um objeto anônimo e serializá-lo ao JSON. Por exemplo:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

O corpo da mensagem de resposta conterá o seguinte JSON:

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Se sua API web receber objetos JSON estruturados livremente dos clientes, você pode desserializar o corpo de solicitação para um tipo **Newtonsoft.Json.Linq.JObject.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

No entanto, geralmente é melhor usar objetos de dados fortemente digitados. Então você não precisa analisar os dados você mesmo, e você obter os benefícios da validação do modelo.

O serializador XML não suporta tipos anônimos ou **instâncias JObject.** Se você usar esses recursos para seus dados JSON, você deve remover o assunto XML do pipeline, conforme descrito mais tarde neste artigo.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML Media-Type Formatter

A formatação XML é fornecida pela classe **XmlMediaTypeFormatter.** Por padrão, **xmlMediaTypeFormatter** usa a classe **DataContractSerializer** para executar a serialização.

Se preferir, você pode configurar o **XmlMediaTypeFormatter** para usar o **XmlSerializer** em vez do **DataContractSerializer**. Para isso, defina a propriedade **UseXmlSerializer** como **verdadeira:**

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

A classe **XmlSerializer** suporta um conjunto mais estreito de tipos do que **dataContractSerializer,** mas dá mais controle sobre o XML resultante. Considere usar **XmlSerializer** se você precisar corresponder a um esquema XML existente.

### <a name="xml-serialization"></a>Serialização XML

Esta seção descreve alguns comportamentos específicos da matéria xml, usando o **DataContractSerializer**padrão .

Por padrão, o DataContractSerializer se comporta da seguinte forma:

- Todas as propriedades e campos de leitura/gravação públicas são serializados. Para omitir uma propriedade ou campo, decore-a com o atributo **IgnoreDataMember.**
- Membros privados e protegidos não são serializados.
- As propriedades somente leitura não são serializadas. (No entanto, o conteúdo de uma propriedade de coleção somente leitura é serializado.)
- Os nomes de classe e membros estão escritos no XML exatamente como aparecem na declaração de classe.
- Um namespace XML padrão é usado.

Se você precisar de mais controle sobre a serialização, você pode decorar a classe com o atributo **DataContract.** Quando este atributo está presente, a classe é serializada da seguinte forma:

- &quot;Opte&quot; na abordagem: Propriedades e campos não são serializados por padrão. Para serializar uma propriedade ou campo, decore-a com o atributo **DataMember.**
- Para serializar um membro privado ou protegido, decore-o com o atributo **DataMember.**
- As propriedades somente leitura não são serializadas.
- Para alterar a forma como o nome da classe aparece no XML, defina o parâmetro *Nome* no atributo **DataContract.**
- Para alterar a forma como um nome de membro aparece no XML, defina o parâmetro *Nome* no atributo **DataMember.**
- Para alterar o namespace xML, defina o parâmetro *Namespace* na classe **DataContract.**

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Propriedades somente leitura

As propriedades somente leitura não são serializadas. Se uma propriedade somente leitura tiver um campo privado de backup, você poderá marcar o campo privado com o atributo **DataMember.** Essa abordagem requer o atributo **DataContract** na classe.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>Datas

As datas são escritas no formato ISO 8601. Por exemplo, &quot;2012-05-23T20:21:37.9116538Z&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>Recuo

Para escrever XML recuado, defina a propriedade **Recuo** **como verdadeira:**

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>Configuração de serializadores XML por tipo

Você pode definir diferentes serializadores XML para diferentes tipos clr. Por exemplo, você pode ter um objeto de dados específico que requer **XmlSerializer** para compatibilidade retrógrada. Você pode usar **XmlSerializer** para este objeto e continuar a usar **DataContractSerializer** para outros tipos.

Para definir um serializador XML para um determinado tipo, chame **SetSerializer**.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

Você pode especificar um **XmlSerializer** ou qualquer objeto que deriva do **XmlObjectSerializer**.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>Removendo o Formatter JSON ou XML

Você pode remover o assunto JSON ou o assunto XML da lista de assuntos formatters, se você não quiser usá-los. As principais razões para fazer isso são:

- Para restringir as respostas da API da Web a um determinado tipo de mídia. Por exemplo, você pode decidir suportar apenas respostas JSON e remover o assunto XML.
- Para substituir o formatter padrão por um formatter personalizado. Por exemplo, você pode substituir o assunto JSON por sua própria implementação personalizada de um assunto de matéria-por-matéria JSON.

O código a seguir mostra como remover os assuntos padrão. Chame isso do método **\_Application Start,** definido em Global.asax.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>Manuseio de referências circulares de objetos

Por padrão, os assuntos de JSON e XML escrevem todos os objetos como valores. Se duas propriedades se referirem ao mesmo objeto ou se o mesmo objeto aparecer duas vezes em uma coleção, a matéria-chefe serializará o objeto duas vezes. Este é um problema particular se o gráfico de objetos contiver ciclos, porque o serializador lançará uma exceção quando detectar um loop no gráfico.

Considere os seguintes modelos de objeto e controlador.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

Invocar essa ação fará com que a matéria-metragem lance uma exceção, que se traduz em uma resposta do código de status 500 (Erro interno do servidor) ao cliente.

Para preservar as referências de objeto no JSON, adicione o seguinte código ao método **Iniciar de aplicativo\_** no arquivo Global.asax:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

Agora, a ação do controlador retornará json que se parece com isso:

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

Observe que o serializador adiciona uma &quot;propriedade $id&quot; a ambos os objetos. Além disso, detecta que a propriedade Employee.Department cria um loop, por isso&quot;&quot;substitui&quot;&quot;o valor por uma referência de objeto: { $ref : 1 }.

> [!NOTE]
> As referências de objeto não são padrão no JSON. Antes de usar esse recurso, considere se seus clientes serão capazes de analisar os resultados. Talvez seja melhor simplesmente remover ciclos do gráfico. Por exemplo, o link de funcionário de volta ao Departamento não é realmente necessário neste exemplo.

Para preservar as referências de objeto em XML, você tem duas opções. A opção mais `[DataContract(IsReference=true)]` simples é adicionar à sua classe de modelo. O parâmetro *IsReference* habilita referências de objeto. Lembre-se que **dataContract** faz opt-in de serialização, então você também precisará adicionar atributos **DataMember** às propriedades:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

Agora, a matéria produzirá XML semelhante ao seguinte:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

Se você quiser evitar atributos em sua classe modelo, há outra opção: Criar uma nova instância de **DataContractSerializer** específica do tipo e definir *preserveObjectReferences* para **true** no construtor. Em seguida, defina esta instância como um serializador por tipo no formatter tipo de mídia XML. O seguinte código mostra como fazer isso:

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>Testando serialização de objetos

Ao projetar sua API web, é útil testar como seus objetos de dados serão serializados. Você pode fazer isso sem criar um controlador ou invocar uma ação do controlador.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
