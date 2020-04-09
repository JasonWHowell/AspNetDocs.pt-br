---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (inclui atualização de ferramentas de abril de 2011) ASP.NET MVC 3 é uma estrutura para a construção de aplicativos web escaláveis e baseados em padrões usando um padrão de design bem estabelecido...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675132"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(inclui atualização de ferramentas de abril de 2011)*
> 
> ASP.NET MVC 3 é uma estrutura para a construção de aplicativos web escaláveis e baseados em padrões usando padrões de design bem estabelecidos e o poder do ASP.NET e do .NET Framework.
> 
> Ele se instala lado a lado com ASP.NET MVC 2, então comece a usá-lo hoje!
> 
> Baixe o [instalador aqui](https://microsoft.com/download/details.aspx?id=4211)

## <a name="top-features"></a>Principais características

- Sistema integrado de andaimes extensível via NuGet
- Modelos de projeto habilitados para HTML 5
- Visualizações expressivas, incluindo o novo Razor View Engine
- Ganchos poderosos com injeção de dependência e filtros de ação global
- Suporte a JavaScript rico com JavaScript discreto, validação jQuery e vinculação JSON
- *Leia a lista completa de destaques [abaixo](#overview)*

## <a name="top-links"></a>Principais Links

O que há de novo em ASP.NET MVC 3

- Phil Haack: [ASP.NET MVC 3 lançado](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express e Orchard lançados - O lançamento da Microsoft January Em Contexto](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [Anunciando o lançamento de ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [Notas de lançamento para ASP.NET MVC 3](../whitepapers/mvc3-release-notes.md)

Instalação e Ajuda

- Instale ASP.NET MVC 3 usando o [Instalador de Plataforma Web (recomendado)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- Instale ASP.NET MVC 3 usando o executor do [instalador](https://go.microsoft.com/fwlink/?LinkID=208140)
- Instale [ASP.NET MVC 3 para visualização do desenvolvedor do Visual Studio 11](https://go.microsoft.com/fwlink/?LinkID=208140)
- Leia o [tutorial de Introdução ao ASP.NET MVC 3](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- Procure ajuda e discuta ASP.NET MVC 3 nos [fóruns](https://forums.asp.net/1146.aspx)

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>visão geral ASP.NET MVC 3

ASP.NET MVC 3 se baseia em ASP.NET MVC 1 e 2, adicionando ótimos recursos que simplificam seu código e permitem uma extensibilidade mais profunda. Este tópico fornece uma visão geral de muitos dos novos recursos que estão incluídos nesta versão, organizados nas seguintes seções:

- [Andaimes extensíveis com integração MvcScaffold](#BM_MvcScaffolding)
- [Modelos de projeto habilitados para HTML 5](#BM_HTML5)
- [O motor razor view](#BM_TheRazorViewEngine)
- [Suporte para motores de exibição múltipla](#BM_Support_for_Multiple_View_Engines)
- [Melhorias do controlador](#BM_Controller_Improvements)
- [JavaScript e Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [Melhorias na validação do modelo](#BM_Model_Validation_Improvements)
- [Melhorias na injeção de dependência](#BM_Dependency_Injection_Improvements)
- [Outras novidades](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>Andaimes extensíveis com integração MvcScaffold

O novo sistema de andaimes torna mais fácil pegar e começar a usar produtivamente se você é inteiramente novo na estrutura, e automatizar tarefas comuns de desenvolvimento se você é experiente e já sabe o que está fazendo.

Isso é suportado pelo novo pacote *de andaimes* NuGet chamado **MvcSandand**. O termo "Andaimes" é usado por muitas tecnologias de software para significar "gerar rapidamente um esboço básico do seu software que você pode então editar e personalizar". O pacote de andaimes que estamos criando para ASP.NET MVC é muito benéfico em vários cenários:

- **Se você está aprendendo ASP.NET MVC pela primeira vez,** porque lhe dá uma maneira rápida de obter algum código útil e de trabalho, que você pode então editar e adaptar de acordo com suas necessidades. Ele te salva do trauma de olhar para uma página em branco e não ter idéia de por onde começar!
- **Se você conhece ASP.NET bem mvc e agora está explorando alguma nova tecnologia adicional,** como um mapeador de objetos relacionais, um mecanismo de exibição, uma biblioteca de testes, etc., porque o criador dessa tecnologia também pode ter criado um pacote de andaimes para ele.
- **Se o seu trabalho envolve criar repetidamente classes ou arquivos semelhantes de algum tipo,** porque você pode criar pastas personalizadas que desembedam dispositivos de teste, scripts de implantação ou o que mais você precisar. Todos na sua equipe também podem usar suas pastas personalizadas.

Outras características no MvcSandandandando incluem:

- Suporte para projetos C# e VB
- Suporte para os motores de visualização Razor e ASPX
- Suporta andaimes em áreas ASP.NET MVC e usando layouts/mestres de exibição personalizados
- Você pode facilmente personalizar a saída editando modelos T4
- Você pode adicionar pastas inteiramente novas usando a lógica PowerShell personalizada e modelos T4 personalizados. Estes (e quaisquer parâmetros personalizados que você lhes deu) aparecem automaticamente na lista de conclusão de guias do console.
- Você pode obter pacotes NuGet contendo pastas adicionais para diferentes tecnologias (por exemplo, há uma prova de conceito para LINQ para SQL agora) e misturar e combiná-las

O ASP.NET MVC 3 Tools Update inclui um ótimo suporte visual studio para este sistema de andaimes, tais como:

- Adicionar diálogo controlador agora suporta andaimes automáticos completos de ações do controlador Criar, Ler, Atualizar e Excluir e visualizações correspondentes. Por padrão, este andaime de acesso de dados código usando EF Code First.
- Adicionar controlador de diálogo suporta *andaimes extensíveis* através de pacotes NuGet, como *MvcSandand*. Isso permite conectar andaimes personalizados na caixa de diálogo, o que permitiria criar andaimes para outras tecnologias de acesso a dados, como nhibernate ou mesmo JET com ODBCDirect se você estiver tão inclinado!

Para obter mais informações sobre andaimes em ASP.NET MVC 3, consulte os seguintes recursos:

- Steve Sanderson post series, incluindo: 

    1. [Introdução: Andaime seu projeto MVC 3 ASP.NET com o pacote MvcScaffolding](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [Uso padrão: Casos e opções de uso típicos](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [Um para muitos relacionamentos](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [Ações de andaimes e testes unitários](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [Sobrepondo os modelos T4](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [Este post: Criando scaffolders personalizados](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- O post de Scott Hanselman de sua sessão pdc 2010 [construindo um blog com a Microsoft "Pacote sem nome de Amor na Web"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [Notas de versão do MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>Modelos de projeto HTML 5

A caixa de diálogo Novo Projeto inclui uma caixa de seleção que habilita as versões HTML 5 de modelos de projeto. Esses modelos aproveitam o Modernizr 1.7 para fornecer suporte à compatibilidade para HTML 5 e CSS 3 em navegadores de nível baixo.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>O motor razor view

ASP.NET MVC 3 vem com um novo mecanismo de visualização chamado Razor que oferece os seguintes benefícios:

- A sintaxe da navalha é limpa e concisa, exigindo um número mínimo de teclas.
- Razor é fácil de aprender, em parte porque é baseado em linguagens existentes como C# e Visual Basic.
- Visual Studio inclui IntelliSense e coloração de código para sintaxe de navalha.
- As visualizações de navalha podem ser testadas por unidade sem exigir que você execute o aplicativo ou inicie um servidor web.

Alguns novos recursos do Razor incluem o seguinte:

- `@model`sintaxe para especificar o tipo que está sendo passado para a exibição.
- `@* *@`sintaxe comentário.
- A capacidade de especificar `layoutpage`padrões (como ) uma vez para um site inteiro.
- O `Html.Raw` método para exibir texto sem codificação HTML.
- Suporte para compartilhamento de código entre vários visualizações*\_(viewstart.cshtml* ou * \_viewstart.vbhtml* files).

Razor também inclui novos ajudantes HTML, como o seguinte:

- `Chart`. Renderiza um gráfico, oferecendo os mesmos recursos do controle de gráfico sinASP.NET 4.
- `WebGrid`. Renderiza uma grade de dados, completa com funcionalidade de paginação e classificação.
- `Crypto`. Usa algoritmos de hashing para criar senhas salgadas e hashed adequadamente.
- `WebImage`. Faz uma imagem.
- `WebMail`. Envia uma mensagem de email.

Para obter mais informações sobre razor, consulte os seguintes recursos:

- [Post no blog de Scott Guthrie apresentando Razor](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Post de Scott Guthrie no @model blog introduzindo a palavra-chave](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Post no blog de Scott Guthrie introduzindo layouts de Razor](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Referência rápida da API da Razor](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [Notas de versão do MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>Suporte para motores de exibição múltipla

A caixa de diálogo **Adicionar exibição** no ASP.NET MVC 3 permite que você escolha o mecanismo de exibição com o qual deseja trabalhar, e a caixa de diálogo **Novo Projeto** permite especificar o mecanismo de exibição padrão de um projeto. Você pode escolher o mecanismo de exibição web forms (ASPX), Razor ou um mecanismo de exibição de código aberto, como [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/)ou [NDjango](http://ndjango.org/).

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>Melhorias do controlador

### <a name="global-action-filters"></a>Filtros de ação global

Às vezes, você deseja executar a lógica antes que um método de ação seja executado ou depois de um método de ação ser executado. Para suportar isso, ASP.NET MVC 2 forneceu filtros de ação. Filtros de ação são atributos personalizados que fornecem meios declaratórios para adicionar comportamento de pré-ação e pós-ação a métodos específicos de ação do controlador. No entanto, em alguns casos, você pode querer especificar comportamento de pré-ação ou pós-ação que se aplica a todos os métodos de ação. O MVC 3 permite especificar filtros `GlobalFilters` globais adicionando-os à coleção. Para obter mais informações sobre filtros de ação globais, consulte os seguintes recursos:

- [Blog de Scott Guthrie no MVC 3 Preview](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [Filtragem em ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>Nova propriedade "ViewBag"

Os controladores MVC `ViewData` 2 suportam uma propriedade que permite que você passe dados para um modelo de exibição usando uma API de dicionário vinculada tardia. No MVC 3, você também pode usar uma `ViewBag` sintaxe um pouco mais simples com o imóvel para realizar o mesmo propósito. Por exemplo, em `ViewData["Message"]="text"`vez de `ViewBag.Message="text"`escrever, você pode escrever . Você não precisa definir nenhuma classe fortemente digitada para usar a `ViewBag` propriedade. Por ser uma propriedade dinâmica, você pode, em vez disso, apenas obter ou definir propriedades e irá resolvê-las dinamicamente no tempo de execução. Internamente, `ViewBag` as propriedades são armazenadas como `ViewData` pares de nome/valor no dicionário. (Nota: na maioria das versões `ViewBag` de pré-lançamento do MVC 3, a propriedade foi nomeada propriedade.) `ViewModel`

### <a name="new-actionresult-types"></a>Novos tipos de "ActionResult"

Os `ActionResult` seguintes tipos e métodos auxiliares correspondentes são novos ou aprimorados no MVC 3:

- [httpnotfoundresult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). Retorna um código de status HTTP 404 ao cliente.
- [Redirecionarresultado](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). Retorna um redirecionamento temporário (código de status HTTP 302) ou um redirecionamento permanente (código de status HTTP 301), dependendo de um parâmetro booleano. Em conjunto com essa mudança, a classe [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) agora possui três `RedirectPermanent` `RedirectToRoutePermanent`métodos `RedirectToActionPermanent`para realizar redirecionamentos permanentes: , e . Esses métodos retornam `RedirectResult` uma `Permanent` instância de `true`com a propriedade definida para .
- [HttpStatusCodeResultado](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). Retorna um código de status HTTP especificado pelo usuário.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>Melhorias javascript e Ajax

Por padrão, o Ajax e os ajudantes de validação no MVC 3 usam uma abordagem JavaScript discreta. Unobtrusive JavaScript evita injetar JavaScript inline em HTML. Isso torna seu HTML menor e menos desordenado, e torna mais fácil trocar ou personalizar bibliotecas JavaScript. Os auxiliares de validação no `jQueryValidate` MVC 3 também usam o plugin por padrão. Se você quiser comportamento MVC 2, você pode desativar javaScript discreto usando uma configuração de arquivo *web.config.* Para obter mais informações sobre as melhorias do JavaScript e do Ajax, consulte os seguintes recursos:

- [Introdução básica ao JavaScript discreto no site da Wikipédia](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson's Unobtrusive JavaScript Post](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Post de validação javascript unobtrusivo de Brad Wilson](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Criando um aplicativo MVC 3 com Razor e Unobtrusive JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (tutorial no site ASP.NET)
- [Notas de versão do MVC 3](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>Validação do lado do cliente habilitada por padrão

Em versões anteriores do MVC, `Html.EnableClientValidation` você precisa chamar explicitamente o método de uma exibição para permitir a validação do lado do cliente. No MVC 3 isso não é mais necessário porque a validação do lado do cliente é ativada por padrão. (Você pode desabilitar isso usando uma configuração no arquivo *Web.config.)*

Para que a validação do lado do cliente funcione, você ainda precisa referenciar as bibliotecas de validação jQuery e jQuery apropriadas em seu site. Você pode hospedar essas bibliotecas em seu próprio servidor ou referencia-las a partir de uma rede de entrega de conteúdo (CDN) como os CDNs da Microsoft ou do Google.

### <a name="remote-validator"></a>Validador remoto

ASP.NET o MVC 3 suporta a nova classe [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) que permite que você aproveite o suporte remoto do validador de validação do jQuery Validation. Isso permite que a biblioteca de validação do lado do cliente chame automaticamente um método personalizado que você define no servidor para executar uma lógica de validação que só pode ser feita do lado do servidor.

No exemplo a `Remote` seguir, o atributo especifica que `UserNameAvailable` a `UsersController` validação do cliente `UserName` chamará uma ação nomeada na classe para validar o campo.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

O exemplo a seguir mostra o controlador correspondente.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

Para obter mais informações `Remote` sobre como usar o atributo, consulte [Como: Implementar validação remota em ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) na biblioteca MSDN.

### <a name="json-binding-support"></a>Suporte de vinculação JSON

ASP.NET o MVC 3 inclui suporte de vinculação JSON incorporado que permite que os métodos de ação recebam dados codificados pelo JSON e os vinculem a parâmetros de método de ação. Esse recurso é útil em cenários envolvendo modelos de clientes e vinculação de dados. (Os modelos do cliente permitem que você forme e exiba um único item de dados ou conjunto de itens de dados usando modelos que executam no cliente.) O MVC 3 permite conectar facilmente modelos de clientes com métodos de ação no servidor que enviam e recebem dados JSON. Para obter mais informações sobre o suporte de vinculação JSON, consulte a seção **JavaScript e AJAX Improvements** do [post do blog MVC 3 Preview de Scott Guthrie](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>Melhorias na validação do modelo

### <a name="dataannotations-metadata-attributes"></a>Atributos de metadados "DataAnnotations"

ASP.NET MVC 3 `DataAnnotations` suporta atributos `DisplayAttribute`de metadados como .

### <a name="validationattribute-class"></a>Classe "ValidaçãoAtributo"

A `ValidationAttribute` classe foi aprimorada no .NET Framework `IsValid` 4 para suportar uma nova sobrecarga que fornece mais informações sobre o contexto de validação atual, como qual objeto está sendo validado. Isso permite cenários mais ricos onde você pode validar o valor atual com base em outra propriedade do modelo. Por exemplo, `CompareAttribute` o novo atributo permite comparar os valores de duas propriedades de um modelo. No exemplo a `ComparePassword` seguir, a `Password` propriedade deve corresponder ao campo para ser válida.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>Interfaces de validação

A interface [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) permite que você execute a validação em nível de modelo e permite que você forneça mensagens de erro de validação específicas do estado do modelo geral ou entre duas propriedades dentro do modelo. O MVC 3 agora `IValidatableObject` recupera erros da interface quando o modelo vincula, e sinaliza ou destaca automaticamente os campos afetados em uma exibição usando os ajudantes de formulário HTML incorporados.

A interface [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) permite que ASP.NET MVC descubram em tempo de execução se um validador tem suporte para validação do cliente. Esta interface foi projetada para que possa ser integrada com uma variedade de frameworks de validação.

Para obter mais informações sobre interfaces de validação, consulte a seção **Melhorias** de validação de modelos [do post do blog MVC 3 Preview de Scott Guthrie](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx). (No entanto, observe que a referência a "IValidateObject" no blog deve ser "IValidatableObject".)

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>Melhorias na injeção de dependência

ASP.NET MVC 3 oferece melhor suporte para a aplicação de di injeção de dependência (DI) e para integração com recipientes de Injeção de Dependência ou Inversão de Controle (COI). O suporte ao DI foi adicionado nas seguintes áreas:

- Controladores (registrando e injetando fábricas de controladores, injetando controladores).
- Visualizações (registrar e injetar mecanismos de exibição, injetando dependências em páginas de exibição).
- Filtros de ação (filtragem e injeção de filtros).
- Pastas modelo (registro e injeção).
- Provedores de validação de modelos (registro e injeção).
- Provedores de metadados modelo (registro e injeção).
- Provedores de valor (registro e injeção).

O MVC 3 suporta a biblioteca [Common Service Locator](https://github.com/unitycontainer/commonservicelocator) e `IServiceLocator` qualquer contêiner DI que suporte a interface dessa biblioteca. Ele também suporta `IDependencyResolver` uma nova interface que facilita a integração de frameworks DI.

Para obter mais informações sobre DI em MVC 3, consulte os seguintes recursos:

- [A série de posts de Brad Wilson sobre localização de serviço](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [Notas de versão do MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>Outras novidades

### <a name="nuget-integration"></a>Integração NuGet

ASP.NET MVC 3 instala e habilita o NuGet como parte de sua configuração. O NuGet é um gerenciador gratuito de pacotes de código aberto que facilita a descoberta, instalação e uso de bibliotecas e ferramentas .NET em seus projetos. Ele funciona com todos os tipos de projetos do Visual Studio (incluindo ASP.NET Web Forms e ASP.NET MVC).

O NuGet permite que desenvolvedores que mantenham projetos de código aberto (por exemplo, projetos como Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks e Elmah) empacotem suas bibliotecas e as registrem em uma galeria online. Então é fácil para os desenvolvedores do .NET que querem usar uma dessas bibliotecas para encontrar o pacote e instalá-lo em projetos em que estão trabalhando.

Com a atualização de ferramentas de ASP.NET 3, os modelos de projeto incluem bibliotecas JavaScript pré-instaladas pacotes NuGet, para que sejam atualizáveis via NuGet. O Entity Framework Code First também está pré-instalado como um pacote NuGet.

Para saber mais sobre o NuGet, veja a [documentação do NuGet](https://docs.microsoft.com/nuget/).

### <a name="partial-page-output-caching"></a>Cache de saída de página parcial

ASP.NET MVC suporta cache de saída de respostas de página inteira desde a versão 1. O MVC 3 também suporta cache de saída de página parcial, o que permite que você cachem facilmente regiões ou fragmentos de uma resposta. Para obter mais informações sobre cache, consulte a seção **Caching** de saída parcial de página do post do blog de [Scott Guthrie sobre o candidato à versão mVC 3](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) e a seção De saída de ação **infantil** das Notas de [Versão mvc 3](../whitepapers/mvc3-release-notes.md).

### <a name="granular-control-over-request-validation"></a>Controle granular sobre validação de solicitações

ASP.NET MVC tem validação de solicitação incorporada que ajuda automaticamente a proteger contra ataques de injeção XSS e HTML. No entanto, às vezes você deseja desativar explicitamente a validação da solicitação, como se você quiser deixar os usuários postarem conteúdo HTML (por exemplo, em entradas de blog ou conteúdo CMS). Agora você pode adicionar um atributo [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) a modelos ou exibir modelos para desativar a validação de solicitação em uma base por propriedade durante a vinculação do modelo. Para obter mais informações sobre validação de solicitações, consulte os seguintes recursos:

- A seção **Unobtrusive JavaScript and Validation** no [post do blog de Scott Guthrie sobre o candidato à versão MVC 3](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).
- [Notas de versão do MVC 3](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>Caixa de diálogo "Novo Projeto" extensível

Em ASP.NET MVC 3, você pode adicionar modelos de projeto, exibir mecanismos e estruturas de projeto de teste de unidade à caixa de diálogo **Novo Projeto.**

### <a name="template-scaffolding-improvements"></a>Melhorias nos andaimes de modelo

ASP.NET modelos de andaimes MVC 3 fazem um trabalho melhor de identificar propriedades de chave primária em modelos e manuseá-los adequadamente do que nas versões anteriores do MVC. (Por exemplo, os modelos de andaimes agora certifiquem-se de que a chave principal não está cadavez como um campo de formulário editável.)

Por padrão, os andaimes Criar e `Html.EditorFor` Editar agora `Html.TextBoxFor` usam o ajudante em vez do ajudante. Isso melhora o suporte a metadados no modelo na forma de anotações de dados atributos quando a caixa de diálogo **Adicionar exibição** gera uma exibição.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>Novas sobrecargas para "Html.LabelFor" e "Html.LabelForModel"

Novas sobrecargas de método `LabelFor` foram `LabelForModel` adicionadas para os métodos e auxiliares. As novas sobrecargas permitem especificar ou substituir o texto do rótulo.

### <a name="sessionless-controller-support"></a>Suporte ao controlador sem sessão

Em ASP.NET MVC 3, você pode indicar se deseja que uma classe controladora use o estado de sessão e, se for o caso, se o estado da sessão deve ser lido/escrito ou somente leitura. Para obter mais informações sobre o suporte ao controlador sem sessão, consulte [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).

### <a name="new-additionalmetadataattribute-class"></a>Nova classe "AdditionalMetadataAttribute"

Você pode usar o atributo `ModelMetadata.AdditionalValues` [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) para preencher o dicionário para uma propriedade modelo. Por exemplo, se um modelo de exibição tiver uma propriedade que deve ser exibida apenas para um administrador, você poderá anotar essa propriedade como mostrado no exemplo a seguir:

[!code-csharp[Main](mvc3/samples/sample4.cs)]

Esses metadados são disponibilizados para qualquer modelo de exibição ou editor quando um modelo de exibição de produto é renderizado. Cabe a você interpretar as informações de metadados.

### <a name="accountcontroller-improvements"></a>Melhorias no AccountController

O AccountController no modelo de projeto da Internet foi muito melhorado.

### <a name="new-intranet-project-template"></a>Novo modelo de projeto intranet

Um novo modelo de projeto intranet está incluído que permite a autenticação do Windows e remove o AccountController.
