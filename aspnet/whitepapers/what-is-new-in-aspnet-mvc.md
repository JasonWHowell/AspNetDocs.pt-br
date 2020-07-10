---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: O que há de novo no ASP.NET MVC 2 | Microsoft Docs
author: rick-anderson
description: Este documento descreve os novos recursos e melhorias introduzidos no ASP.NET MVC 2. Este documento também está disponível para download.
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: 1a0a29241d8afecd295b11013b27621b21c9ed52
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162691"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>Novidades no ASP.NET MVC 2

> Este documento descreve os novos recursos e melhorias introduzidos no ASP.NET MVC 2. Este documento também está disponível para [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)

[Apresentações](#_TOC1)   
[Atualizando um projeto ASP.NET MVC 1,0 para o ASP.NET MVC 2](#_TOC2)   
[Novos recursos](#_TOC3)   
[Auxiliares modelados](#_TOC3_1)   
[Área](#_TOC3_2)   
[Suporte para controladores assíncronos](#_TOC3_3)   
[Suporte para DefaultValueAttribute em parâmetros de método de ação](#_TOC3_4)   
[Suporte para associação de dados binários com ASSOCIADORES de modelo](#_TOC3_5)   
[Classes ModelMetadata e ModelMetadataProvider](#_TOC3_6)   
[Suporte para atributos Annotations](#_TOC3_7)   
[Provedores de validador de modelo](#_TOC3_8)   
[Validação no lado do cliente](#_TOC3_9)   
[Novos trechos de código para o Visual Studio 2010](#_TOC3_10)   
[Novo filtro de ação RequireHttpsAttribute](#_TOC3_11)   
[Substituindo o verbo do método HTTP](#_TOC3_12)   
[Nova classe HiddenInputAttribute para auxiliares modelados](#_TOC3_13)   
[O método auxiliar HTML. ValidationSummary pode exibir erros no nível do modelo](#_TOC3_14)   
[Os modelos T4 no Visual Studio geram código que é específico para a versão de destino do .NET Framework](#_TOC3_15)[aprimoramentos da API](#_TOC4)  
[Alterações de quebra](#_TOC5)  
[Isenção de responsabilidade](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>Apresentações

O ASP.NET MVC 2 se baseia no ASP.NET MVC 1,0 e apresenta um grande conjunto de aprimoramentos e recursos que se concentram em aumentar a produtividade. Esta versão é compatível com o ASP.NET MVC 1,0, portanto, todos os seus conhecimentos, habilidades, códigos e extensões para o ASP.NET MVC 1,0 continuam a ser aplicados.

Para obter mais informações sobre o ASP.NET MVC, visite os seguintes recursos:

- [Documentação do ASP.NET MVC no MSDN](https://go.microsoft.com/fwlink/?LinkId=159758)
- [O site do ASP.NET MVC](https://asp.net/mvc/)
- [Os fóruns do ASP.NET MVC](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>Atualizando um projeto ASP.NET MVC 1,0 para o ASP.NET MVC 2

O ASP.NET MVC 2 pode ser instalado lado a lado com o ASP.NET MVC 1,0 no mesmo servidor, o que oferece aos desenvolvedores de aplicativos flexibilidade para escolher quando atualizar um aplicativo ASP.NET MVC 1,0 para o ASP.NET MVC 2. Para obter informações sobre como atualizar, consulte o documento [atualizando um aplicativo ASP.net mvc 1,0 para o ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185459).

## <a name="new-features"></a><a id="_TOC3"></a>Novos recursos

Esta seção descreve os recursos que foram introduzidos na versão MVC 2.

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>Auxiliares modelados

Os auxiliares modelados permitem associar automaticamente elementos HTML para edição e exibição com tipos de dados. Por exemplo, quando dados do tipo System. DateTime são exibidos em uma exibição, um elemento de interface do usuário do seletor de data pode ser renderizado automaticamente. Isso é semelhante a como os modelos de campo funcionam no ASP.NET Dados Dinâmicos. Para obter mais informações, consulte [usando auxiliares de modelo para exibir dados](https://go.microsoft.com/fwlink/?LinkId=159062) no site do MSDN.

### <a name="areas"></a><a id="_TOC3_2"></a>Área

As áreas permitem organizar um projeto grande em várias seções menores, a fim de gerenciar a complexidade de um aplicativo Web grande. Cada seção ("Area") normalmente representa uma seção separada de um grande site da Web e é usada para agrupar conjuntos relacionados de controladores e modos de exibição. Para obter mais informações, consulte [Walkthrough: organizando um aplicativo MVC ASP.net por áreas](https://go.microsoft.com/fwlink/?LinkId=158978) no site do MSDN.

Para criar uma nova área, em Gerenciador de Soluções, clique com o botão direito do mouse no projeto, clique em Adicionar e, em seguida, clique em área. Isso exibe uma caixa de diálogo que solicita o nome da área. Depois de inserir o nome da área, o Visual Studio adiciona uma nova área ao projeto.

A figura a seguir mostra um exemplo de layout para um projeto com duas áreas, administradores e Blogs.

![](what-is-new-in-aspnet-mvc/_static/image1.png)

Quando você cria uma área, o Visual Studio adiciona uma classe derivada de AreaRegistration a cada área. Essa classe é necessária para registrar a área e suas rotas, conforme mostrado no exemplo a seguir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

O modelo de projeto padrão para o ASP.NET MVC 2 inclui uma chamada para o método RegisterAllAreas no código para o arquivo global. asax. Esse método registra cada área no projeto procurando todos os tipos que derivam da classe AreaRegistration, instanciando uma instância do tipo e, em seguida, chamando o método RegisterArea na instância. O exemplo a seguir mostra como isso é feito.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

Se você não especificar o namespace no método RegisterArea chamando o contexto. Namespace. Add o método, o namespace da classe de registro é usado por padrão.

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>Suporte para controladores assíncronos

O ASP.NET MVC 2 agora permite que os controladores processem solicitações de forma assíncrona. Isso pode levar a ganhos de desempenho, permitindo que os servidores que freqüentemente chamam operações de bloqueio (como solicitações de rede) chamem contrapartes sem bloqueio. Para obter mais informações, consulte o tópico [usando um controlador assíncrono no ASP.NET MVC](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) no msdn.

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>Suporte para DefaultValueAttribute em parâmetros de método de ação

A classe System. ComponentModel. DefaultValueAttribute permite que um valor padrão seja fornecido para o parâmetro Argument para um método Action. Por exemplo, suponha que a rota padrão a seguir seja definida:

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.json)]

Além disso, suponha que o controlador e o método de ação a seguir estejam definidos:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

Qualquer uma das URLs de solicitação a seguir invocará o método view action definido no exemplo anterior.

- /Article/View/123
- /Article/View/123? Page = 1 (efetivamente igual à solicitação anterior)
- /Article/View/123? página = 2

Sem o atributo DefaultValueAttribute, a primeira URL da lista anterior não funcionaria, porque o argumento Page é um tipo de valor não anulável cujo valor não foi fornecido.

Se seu código for escrito em Visual Basic 2010 ou Visual C# 2010, você poderá usar parâmetros opcionais em vez do atributo DefaultValueAttribute, conforme mostrado no exemplo a seguir:

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>Suporte para associação de dados binários com ASSOCIADORES de modelo

Há duas novas sobrecargas do auxiliar HTML. Hidden que codificam valores binários como cadeias de caracteres codificadas em base 64:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

Um uso típico é inserir um carimbo de data/hora para um objeto na exibição. Por exemplo, seu aplicativo pode incluir o seguinte objeto de produto:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

Um formulário de edição pode renderizar a Propriedade TimeStamp no formulário, conforme mostrado no exemplo a seguir:

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

Essa marcação renderiza um elemento de entrada oculto com o valor de carimbo de data/hora como uma cadeia de caracteres codificada em base 64 que se assemelha ao exemplo a seguir:

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

Esse formulário pode ser Postado em um método de ação que tem um argumento do tipo Product, conforme mostrado no exemplo a seguir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

No método de ação, a Propriedade TimeStamp é populada corretamente porque a cadeia de caracteres codificada em base 64 lançada é convertida em uma matriz de bytes.

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>Classes ModelMetadata e ModelMetadataProvider

A classe ModelMetadataProvider fornece uma abstração para obter metadados para o modelo em uma exibição. O MVC 2 inclui um provedor padrão que disponibiliza os metadados expostos pelos atributos no namespace System. ComponentModel. Annotations. É possível criar provedores de metadados que fornecem metadados de outros armazenamentos de dados, como bancos de dados ou arquivos XML.

A classe ViewDataDictionary expõe um objeto ModelMetadata que contém os metadados que são extraídos do modelo pela classe ModelMetadataProvider. Isso permite que os auxiliares do modelo consumam esses metadados e ajustem sua saída de acordo.

Para obter mais informações, consulte a documentação para as classes [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) e [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) .

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>Suporte para atributos Annotations

O ASP.NET MVC 2 dá suporte ao uso dos atributos RangeAttribute, requerido, StringLengthAttribute e regexattribute (definidos no namespace System. ComponentModel. Annotations) quando você se associa a um modelo para fornecer validação de entrada.

Para obter mais informações, consulte [como: validar dados de modelo usando atributos Annotations](https://go.microsoft.com/fwlink/?LinkId=159063) no site do MSDN. Um projeto de exemplo que ilustra o uso desses atributos está disponível para download em [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) .

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>Provedores de validador de modelo

A classe de provedor de validação de modelo representa uma abstração que fornece lógica de validação para o modelo. O ASP.NET MVC inclui um provedor padrão baseado em atributos de validação que são incluídos no namespace System. ComponentModel. Annotations. Você também pode criar seus próprios provedores de validação que definem regras de validação personalizadas e mapeamentos personalizados de regras de validação para o modelo. Para obter mais informações, consulte a documentação da classe [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) .

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>Validação no lado do cliente

A classe de provedor de validador de modelo expõe metadados de validação para o navegador na forma de dados serializados em JSON que podem ser consumidos por uma biblioteca de validação do lado do cliente. O ASP.NET MVC 2 inclui uma biblioteca de validação de cliente e um adaptador que dá suporte aos atributos de validação de namespace DataAnnotations observados anteriormente. A classe Provider também permite que você use outras bibliotecas de validação de cliente escrevendo um adaptador que processa os dados JSON e chama a biblioteca alternativa.

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>Novos trechos de código para o Visual Studio 2010

Um conjunto de trechos de código HTML para o ASP.NET MVC 2 é instalado com o Visual Studio 2010. Para exibir uma lista desses trechos, no menu ferramentas, selecione Gerenciador de trechos de código. Para o idioma, selecione HTML e, para local, selecione ASP.NET MVC 2. Para obter mais informações sobre como usar trechos de código, consulte a documentação do Visual Studio.

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>Novo filtro de ação RequireHttpsAttribute

O ASP.NET MVC 2 inclui uma nova classe RequireHttpsAttribute que pode ser aplicada a métodos e controladores de ação. Por padrão, o filtro redireciona uma solicitação não SSL (HTTP) para o equivalente habilitado para SSL (HTTPS).

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>Substituindo o verbo do método HTTP

Quando você cria um site usando o estilo de arquitetura REST, os verbos HTTP são usados para determinar qual ação executar para um recurso. O REST exige que os aplicativos ofereçam suporte a toda a gama de verbos HTTP comuns, incluindo GET, PUT, POST e DELETE.

O ASP.NET MVC 2 inclui novos atributos que você pode aplicar a métodos de ação e essa sintaxe de compactação de recurso. Esses atributos permitem que o ASP.NET MVC selecione um método de ação baseado no verbo HTTP. No exemplo a seguir, uma solicitação POST chamará o primeiro método Action e uma solicitação PUT chamará o segundo método Action.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

Em versões anteriores do ASP.NET MVC, esses métodos de ação exigiam uma sintaxe mais detalhada, conforme mostrado no exemplo a seguir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

Como os navegadores dão suporte apenas aos verbos HTTP GET e POST, não é possível postar em uma ação que exija um verbo diferente. Portanto, não é possível dar suporte nativo a todas as solicitações RESTful.

No entanto, para dar suporte a solicitações RESTful durante operações de POSTAgem, o ASP.NET MVC 2 apresenta um novo método auxiliar HTML HttpMethodOverride. Esse método renderiza um elemento de entrada oculto que faz com que o formulário eMule efetivamente qualquer método HTTP. Por exemplo, usando o método auxiliar HTML HttpMethodOverride, você pode fazer com que um envio de formulário seja exibido como uma solicitação PUT ou DELETE. O comportamento de HttpMethodOverride afeta os seguintes atributos:

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

O elemento de entrada oculto tem seu nome X-HTTP-Method-override e seu valor definido para o verbo HTTP a ser emulado. O valor de substituição também pode ser especificado em um cabeçalho HTTP ou em um valor de cadeia de caracteres de consulta como um par de nome/valor.

A substituição só pode ser usada quando a solicitação real é uma solicitação POST. O valor de substituição será ignorado para solicitações que usam qualquer outro verbo HTTP.

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>Nova classe HiddenInputAttribute para auxiliares modelados

Você pode aplicar o novo atributo HiddenInputAttribute a uma propriedade de modelo para indicar se um elemento de entrada oculto deve ser renderizado ao exibir o modelo em um modelo de editor. (O atributo define um valor UIHint implícito de HiddenInput). A Propriedade DisplayValue do atributo permite especificar se o valor é exibido nos modos de exibição e editor. Quando DisplayValue é definido como false, nada é exibido, nem mesmo a marcação HTML que normalmente envolve um campo. O valor padrão de DisplayValue é true.

Você pode usar o atributo HiddenInputAttribute nos seguintes cenários:

- Quando uma exibição permite que os usuários editem a ID de um objeto e seja necessário exibir o valor, bem como fornecer um elemento de entrada oculto que contém a ID antiga para que possa ser passado de volta para o controlador.
- Quando uma exibição permite que os usuários editem uma propriedade binária que nunca deve ser exibida, como uma propriedade Timestamp. Nesse caso, o valor e a marcação HTML ao redor (como o rótulo e o valor) não são exibidos.

O exemplo a seguir mostra como usar a classe HiddenInputAttribute.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

Quando o atributo é definido como true (ou nenhum parâmetro é especificado), ocorre o seguinte:

- Em modelos de exibição, um rótulo é renderizado e o valor é exibido para o usuário.
- Em modelos do editor, um rótulo é renderizado e o valor é renderizado em um elemento de entrada oculto.

Quando o atributo é definido como false, ocorre o seguinte:

- Em modelos de exibição, nada é renderizado para esse campo.
- Em modelos do editor, nenhum rótulo é renderizado e o valor é renderizado em um elemento de entrada oculto.

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>O método auxiliar HTML. ValidationSummary pode exibir erros no nível do modelo

Em vez de sempre exibir todos os erros de validação, o método auxiliar HTML. ValidationSummary tem uma nova opção para exibir apenas erros de nível de modelo. Isso permite que os erros de nível de modelo sejam exibidos no Resumo de validação e erros específicos de campo a serem exibidos ao lado de cada campo.

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>Os modelos T4 no Visual Studio geram código específico para a versão de destino do .NET Framework

Uma nova propriedade está disponível para arquivos T4 do host ASP.NET MVC T4 que especifica a versão do .NET Framework usado pelo aplicativo. Isso permite que modelos T4 gerem código e marcação específicos para uma versão do .NET Framework. No Visual Studio 2008, o valor é sempre .NET 3,5. No Visual Studio 2010, o valor é .NET 3,5 ou .NET 4.

## <a name="api-improvements"></a><a id="_TOC4"></a>Aprimoramentos da API

Esta seção descreve as alterações nos tipos e membros existentes do ASP.NET MVC.

- Adicionou um método CreateActionInvoker virtual protegido na classe Controller. Esse método é invocado pela Propriedade ActionInvoker do controlador e permite a instanciação lenta do chamador se nenhum chamador já estiver definido.
- Adicionou um método HandleUnauthorizedRequest virtual protegido na classe Authorattribute. Isso habilita filtros que derivam de Authorattribute para controlar o comportamento quando a autorização falha.
- Adicionado um método Add (chave de cadeia de caracteres, valor de objeto) na classe ValueProviderDictionary. Isso permite que você use a sintaxe do inicializador de dicionário para ValueProviderDictionary, como no exemplo a seguir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- Adicionado um \_ método Get Object na classe Sys. Mvc. AjaxContext. Esse é um método JavaScript semelhante ao \_ método Get Data, mas se o tipo de conteúdo da resposta for application/json, \_ o objeto Get retornará o objeto JSON.
- Adicionada uma Propriedade ActionDescriptor na classe AuthorizationContext.
- Adição de um token UrlParameter. optional que pode ser usado para solucionar problemas ao associar a um modelo que contém uma propriedade de ID quando a propriedade está ausente em uma postagem de formulário. Para obter mais detalhes, consulte a entrada [parâmetros de URL opcionais do ASP.NET MVC 2](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) no blog de Phil Haack.

## <a name="breaking-changes"></a><a id="_TOC5"></a>Alterações recentes

As alterações a seguir podem causar erros nos aplicativos existentes do ASP.NET MVC 1,0.

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>Alteração no comportamento de validação de propriedade para classes que implementam IDataErrorInfo

Para objetos de modelo que usam IDataErrorInfo para executar a validação, cada propriedade é validada, independentemente de um novo valor ter sido definido. No ASP.NET MVC 1,0, somente as propriedades que tinham novos valores definidos foram validadas. No ASP.NET MVC 2, a Propriedade Error de IDataErrorInfo será chamada somente se todos os validadores de propriedade tiverem sido bem-sucedidos.

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>O script de mapeamento de script do IIS não está mais disponível no instalador

O script de mapeamento de script do IIS é um script de linha de comando usado para configurar mapas de script para o IIS 6 e para o IIS 7 no modo clássico. O script de mapeamento de script não será necessário se você usar o Visual Studio Development Server ou se usar o IIS 7 no modo integrado. Os scripts estão disponíveis como um download sem suporte separado no [Webstack do ASP.net](https://github.com/aspnet/AspNetWebStack).

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>O método auxiliar HTML. substituto no futuro do MVC não está mais disponível

Devido a alterações no comportamento de renderização dos mecanismos de exibição do MVC, o método auxiliar HTML. substituto não funciona e foi removido.

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>A interface IValueProvider substitui todos os usos de IDictionary

Cada argumento de propriedade ou método que aceitou IDictionary no MVC 1,0 agora aceita IValueProvider. Essa alteração afeta apenas os aplicativos que incluem provedores de valor personalizado ou ASSOCIADORES de modelo personalizados. Exemplos de propriedades e métodos que são afetados por essa alteração incluem o seguinte:

- A propriedade ValueProvider das classes ControllerBase e ModelBindingContext.
- Os métodos TryUpdateModel da classe Controller.

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>Novas classes CSS foram adicionadas ao arquivo site. css

O arquivo site. CSS nos modelos de projeto do ASP.NET MVC foi atualizado para incluir novos estilos usados pela funcionalidade de validação e pelos auxiliares do modelo.

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>Os auxiliares agora retornam um objeto MvcHtmlString

Para aproveitar a nova sintaxe de expressão de codificação HTML no ASP.NET 4, o tipo de retorno para auxiliares HTML agora é MvcHtmlString em vez de uma cadeia de caracteres. Se você usar o ASP.NET MVC 2 e os novos auxiliares no ASP.NET 3,5, não poderá aproveitar a sintaxe de codificação HTML; a nova sintaxe está disponível somente quando você executa o ASP.NET MVC 2 no ASP.NET 4.

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult agora responde apenas às solicitações HTTP POST

Para reduzir os ataques de seqüestro de JSON que têm o potencial de divulgação de informações, por padrão, a classe JsonResult agora responde apenas às solicitações HTTP POST. As chamadas GET Ajax para métodos de ação que retornam um objeto JsonResult devem ser alteradas para usar POST em vez disso. Se necessário, você pode substituir esse comportamento definindo a nova propriedade JsonRequestBehavior de JsonResult. Para obter mais informações sobre a exploração em potencial, consulte a postagem no blog [seqüestro de JSON](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) no blog de Phil Haack.

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>Os setters de Propriedade Model e ModelType em ModelBindingContext estão obsoletos

Uma nova Propriedade ModelMetadata configurável foi adicionada à classe ModelBindingContext. A nova propriedade encapsula o modelo e as propriedades ModelType. Embora as propriedades Model e ModelType sejam obsoletas, para compatibilidade com versões anteriores, os getters de propriedade ainda funcionam; Eles delegam para a Propriedade ModelMetadata para recuperar o valor.

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>Alterações na classe DefaultControllerFactory quebram fábricas de controlador personalizado que derivam dela

A classe DefaultControllerFactory foi corrigida removendo a Propriedade RequestContext. No lugar dessa propriedade, a instância de contexto de solicitação é passada para os métodos GetControllerInstance e getcontrollertype virtuais protegidos. Essa alteração afeta as fábricas de controlador personalizado que derivam de DefaultControllerFactory.

Fábricas de controlador personalizado geralmente são usadas para fornecer injeção de dependência para aplicativos MVC ASP.NET. Para atualizar as fábricas do controlador personalizado para dar suporte ao ASP.NET MVC 2, altere a assinatura do método ou as assinaturas para que correspondam às novas assinaturas e use o parâmetro de contexto de solicitação em vez da propriedade.

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"Area" é uma chave de valor de rota reservada

A cadeia de caracteres "Area" em valores de rota agora tem um significado especial no ASP.NET MVC, da mesma forma que "Controller" e "Action". Uma implicação é que, se os auxiliares HTML forem fornecidos com um dicionário de valor de rota contendo "Area", os auxiliares não acrescentarão mais "Area" na cadeia de caracteres de consulta.

Se você estiver usando o recurso de áreas, certifique-se de não usar {Area} como parte da sua URL de rota.

## <a name="disclaimer"></a><a id="_TOC6"></a>Enção

Este é um documento preliminar e pode ser alterado substancialmente antes da versão comercial final do software descrito aqui.

As informações contidas neste documento representam a visão atual da Microsoft Corporation acerca das questões discutidas até a data da publicação. Como a Microsoft deve reagir às dinâmicas condições do mercado, essas informações não devem ser interpretadas como um compromisso por parte da Microsoft e a Microsoft não garante a precisão de qualquer informação apresentada após a data de publicação.

Este whitepaper é apenas para fins informativos. A MICROSOFT NÃO OFERECE GARANTIA, EXPRESSA, IMPLÍCITA OU ESTATUTÁRIA, DAS INFORMAÇÕES CONTIDAS NESTE DOCUMENTO.

Obedecer a todas as leis de direitos autorais aplicáveis é responsabilidade do usuário. Sem limitar os direitos autorais, nenhuma parte deste documento pode ser reproduzida, armazenada ou introduzida em um sistema de recuperação, ou transmitida de qualquer forma ou por qualquer meio (seja eletrônico, mecânico, fotocópia, gravação ou outro), ou para qualquer finalidade, sem a permissão expressa e por escrito da Microsoft Corporation.

A Microsoft pode ter patentes ou requisições para obtenção de patente, marcas comerciais, direitos autorais ou outros direitos de propriedade intelectual que abrangem o conteúdo deste documento. A posse deste documento não lhe confere nenhum direito sobre patentes, marcas comerciais, direitos autorais ou outros direitos de propriedade intelectual, salvo aqueles expressamente mencionados em um contrato de licença, por escrito, da Microsoft.

Salvo indicação em contrário, os exemplos de empresas, organizações, produtos, nomes de domínio, endereços de email, logotipos, pessoas, lugares e eventos aqui mencionados são fictícios e nenhuma associação com qualquer empresa, organização, produto, nome de domínio, endereço de email, logotipo, pessoa, lugar ou evento real é intencional ou deve ser inferida.

© 2010 Microsoft Corporation. Todos os direitos reservados.

Microsoft e Windows são marcas registradas ou comerciais da Microsoft Corporation nos Estados Unidos e/ou em outros países.

Os nomes de empresas reais e produtos mencionados aqui podem ser marcas comerciais de seus respectivos proprietários.
