---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET e Web Tools 2012.2 Release Notes | Microsoft Docs
author: rick-anderson
description: Notas de versão para ASP.NET e Web Tools 2012.2.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676303"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>Notas de Versão do ASP.NET and Web Tools 2012.2

> Este documento descreve o lançamento de ASP.NET e Web Tools 2012.2. É uma atualização para o Visual Studio Web Tooling e ASP.NET.

- [Notas de instalação](#_Installation)
- [Documentação](#_Documentation)
- [Suporte](#_Support)
- [Requisitos de software](#_Software_Requirements)
- [Novos recursos em ASP.NET e Web Tools 2012.2](#_New_Features_in)

    - [Ferramentas](#_Tooling)
    - [Publicação web](#_Web_Publishing)
    - [modelos mvc de ASP.NET](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [URLs amigáveis do ASP.NET](#_ASP.NET_Friendly_URLs)
- [Problemas conhecidos e mudanças de quebra](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>Notas de instalação

ASP.NET e Web Tools 2012.2 para Visual Studio 2012 podem ser instalados usando [o instalador da Plataforma Web](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2). Esta é uma atualização para o Visual Studio 2012 ou Visual Studio Express 2012 para web, que é necessária. Se você não tiver o Visual Studio instalado, o Visual Studio Express 2012 para Web será instalado.

Você também pode instalar ASP.NET e Web Tools 2012.2 manualmente. Você deve ter o Visual Studio 2012 ou o Visual Studio Express 2012 para web instalado. Em seguida, use as seguintes instruções: 

1. Baixe ASP.NET e o instalador [Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) do Download Center.
2. Quando solicitado clique em Executar. Você também pode salvar o arquivo para executá-lo mais tarde.
3. Verifique a versão do Visual Studio que você atualizará. Você pode fazer isso lançando o Visual Studio que deseja atualizar. Em seguida, clique no item do menu Ajuda.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. Se você ver o &quot;item do menu Sobre&quot; o Microsoft Visual Studio 2012 para web, então baixe [Web Developer Tools 2012.2 - Visual Studio Express 2012 para Web](https://go.microsoft.com/fwlink/?LinkID=282228). De outra forma, baixe [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. Quando solicitado clique em Executar. Você também pode salvar o arquivo para executá-lo mais tarde.

> [!NOTE]
> ASP.NET e Web Tools 2012.2 não inclui ferramentas de dados do Servidor SQL. Os bancos de dados SQL Server e Windows Azure SQL fornecem um conjunto mais rico de ferramentas de banco de dados, incluindo desenvolvimento off-line apoiado por projetos, comparação de esquemas e recursos aprimorados de implantação de banco de dados. Para obter mais informações ou para instalar [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)o SQL Server Data Tools visite .

<a id="_Documentation"></a>
## <a name="documentation"></a>Documentação

Tutoriais e outras informações sobre ASP.NET e Web Tools 2012.2 estão disponíveis no site ASP.NET ( https://www.asp.net).

<a id="_Support"></a>
## <a name="support"></a>Suporte

ASP.NET e Web Tools 2012.2 é lançado oficialmente e suportado. Você pode usar seu canal de suporte normal. Você também pode postar perguntas nos[https://forums.asp.net/](https://forums.asp.net/)fóruns de ASP.NET ( ), onde membros da comunidade ASP.NET são frequentemente capazes de fornecer apoio informal.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>Requisitos de software

O ASP.NET e Web Tools 2012.2 requer o Visual Studio 2012 ou o Visual Studio Express 2012 para web.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>Novos recursos em ASP.NET e Web Tools 2012.2

Esta seção descreve recursos que foram introduzidos na versão ASP.NET e Web Tools 2012.2.

<a id="_Tooling"></a>
### <a name="tooling"></a>Ferramentas

- Inspetor de Página 

    - Suporte ao mapeamento de seleção JavaScript, permitindo que o Page Inspector mapeie itens que foram adicionados dinamicamente à página de volta ao código JavaScript correspondente.
    - A capacidade de ver as atualizações do CSS em tempo real.
    - Para obter mais informações, leia [CSS Auto-Sync e JavaScript Selection Mapping no Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).
- Editor 

    - Suporte a sintaxe de suporte para CoffeeScript, Mustache, Handlebars e JsRender.
    - O editor HTML fornece intellisense para vinculações knockout.
    - Menos suporte a edição e compilador para permitir a construção de CSS dinâmico usando MENOS.
    - Cole JSON como uma classe .NET. Usando este comando Special Paste para colar JSON em um arquivo de código C# ou VB.NET, o Visual Studio gerará automaticamente classes .NET inferidas a partir do JSON.
- O suporte ao Emulador Móvel adiciona ganchos de extensibilidade para que emuladores de terceiros possam ser instalados como um VSIX. Os emuladores instalados aparecerão no dropdown do F5, para que os desenvolvedores possam visualizar seus sites em uma variedade de dispositivos móveis. Leia mais sobre esse recurso na entrada do blog de Scott Hanselman sobre [a nova integração do BrowserStack com o Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Publicação web

- Os projetos de sites da Web agora têm a mesma experiência de publicação que projetos de Aplicativos Web, incluindo a publicação no Windows Azure Web Sites.
- A publicação seletiva &#8211; para um ou mais arquivos que você pode executar as seguintes ações (após a publicação em um ponto final da Web Deploy): 

    - Publique arquivos selecionados.
    - Veja a diferença entre um arquivo local e um arquivo remoto.
    - Atualize o arquivo local com o arquivo remoto ou atualize o arquivo remoto com o arquivo local.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>modelos mvc de ASP.NET

- O novo modelo de aplicativo do Facebook facilita a gravação de aplicativos Canvas do Facebook. Em alguns passos simples, é possível criar um aplicativo do Facebook que obtém dados de um usuário conectado e se integra com os amigos. O modelo inclui uma nova biblioteca para tratar de todo o encanamento envolvido na criação de um aplicativo do Facebook, incluindo autenticação, permissões, acesso aos dados do Facebook, entre outros. Para obter mais informações sobre [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)como usar o modelo do Aplicativo do Facebook, consulte .
- Um novo modelo MVC de aplicativo de página única permite aos desenvolvedores criar aplicativos da Web interativos de cliente usando HTML 5, CSS 3 e as bibliotecas populares Knockout e jQuery JavaScript, na parte superior do ASP.NET Web API. O modelo inclui um aplicativo de lista "todo" que demonstra práticas comuns para a construção de um aplicativo JavaScript HTML5 que usa uma API de servidor RESTful. Você pode ler [https://www.asp.net/single-page-application](../../../single-page-application/index.md)mais em .
- Agora você pode criar um VSIX que adiciona novos modelos à ASP.NET diálogo MVC New Project. Saiba como aqui:[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- Pacote FixedDisplayModes &#8211; os modelos do projeto MVC foram atualizados para incluir o novo pacote NuGet 'FixedDisplayModes', que contém uma solução para um bug no MVC 4. Para obter mais informações sobre a correção contida[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)no pacote, consulte este post do blog ( ) da equipe de MVC.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET API da Web foi aprimorada com vários novos recursos:

- ASP.NET Web API OData
- ASP.NET Web API Tracing
- ASP.NET página de ajuda da API da Web

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET API Da Web OData oferece a flexibilidade necessária para construir pontos finais de OData com rica lógica de negócios sobre qualquer fonte de dados. Com ASP.NET OData da API da Web você controla a quantidade de semântica OData que deseja expor. ASP.NET Web API OData está incluído nos modelos de projeto ASP.NET[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)MVC 4 e também está disponível no NuGet ( ).

ASP.NET OOData da API da Web atualmente suporta os seguintes recursos:

- Habilite a semântica de consulta oData aplicando o atributo [Queryable].
- Valide facilmente as consultas oData e restrinja o conjunto de opções de consulta suportadas, operadores e funções.
- Parâmetro saqueie-se diretamente a ODataQueryOptions para obter uma representação de árvore de sintaxe abstrata da consulta que pode ser validada e aplicada a um IQueryable ou IEnumerable.
- Habilite a paginação orientada por serviço e a geração do link da próxima página, especificando limites de resultado no atributo [queryable].
- Solicite uma contagem inline do número total de recursos correspondentes usando $inlinecount.
- Controle propagação nula.
- Todos os operadores em $filter.
- Infera um modelo de dados de entidade por convenção ou personalize explicitamente um modelo de forma semelhante ao Código-Quadro de Entidades Primeiro.
- Expor conjuntos de entidades derivando do EntitySetController.
- Convenções simples e personalizáveis para expor propriedades de navegação, manipular links e implementar ações de OData.
- Roteamento simplificado usando o método de extensão MapODataRoute.
- Suporte para versões expondo vários modelos EDM.
- Exponha o documento de serviço e $metadata para que você possa gerar clientes (.NET, Windows Phone, Windows Store, etc.) para sua API web.
- Suporte para os formatos verbos oData Atom, JSON e JSON.
- Criar, atualizar, atualizar parcialmente (PATCH) e excluir entidades.
- Consultar e manipular as relações entre entidades.
- Crie links de relacionamento que se ligam às suas rotas.
- Tipos complexos.
- Herança tipo entidade.
- Propriedades de coleta.
- Enums.
- Ações oData.
- Construído sobre a mesma fundação do WCF Data[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)Services, ou seja, ODataLib ( ).

Para obter mais informações sobre ASP.NET [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)OData da API web consulte .

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API Tracing

ASP.NET Web API Tracing integra dados de rastreamento de suas APIs da Web com o .NET Tracing. Ele agora está ativado por padrão no modelo de projeto da API da Web. O rastreamento de dados para suas APIs da Web é enviado para a janela Saída e é disponibilizado através do IntelliTrace. ASP.NET Web API Tracing permite rastrear informações sobre sua API da Web quando hospedado no Windows Azure através da integração com [o Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx). Você também pode instalar e habilitar ASP.NET API Tracing da Web em[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)qualquer aplicativo usando o pacote ASP.NET Web API Tracing NuGet ( ).

Para obter mais informações sobre a configuração [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)e o uso de ASP.NET Web API Tracing consulte .

#### <a name="aspnet-web-api-help-page"></a>ASP.NET página de ajuda da API da Web

A página de ajuda da API ASP.NET agora está incluída por padrão no modelo de projeto da API da Web. A página de ajuda da API ASP.NET gera automaticamente documentação para APIs da Web, incluindo os pontos finais HTTP, os métodos HTTP suportados, parâmetros e as cargas de solicitação e resposta de solicitação e resposta. A documentação é automaticamente retirada de comentários em seu código. Você também pode adicionar a página de ajuda da API ASP.NET a qualquer[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)aplicativo usando o pacote nuGet da página de ajuda da API ASP.NET ( pacote nuGet).

Para obter mais informações sobre como configurar e personalizar [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)a página de ajuda da API ASP.NET, consulte .

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR torna mais simples adicionar recursos web em tempo real ao seu aplicativo ASP.NET, usando WebSockets se disponível e automaticamente voltando a outras técnicas quando não está.

Para obter mais informações sobre [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)como usar ASP.NET SignalR consulte .

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>URLs amigáveis do ASP.NET

ASP.NET FriendlyURLs torna muito fácil para os desenvolvedores de formulários web gerar URLs mais limpas (sem a extensão .aspx). Ele requer pouca ou nenhuma configuração e pode ser usado com aplicativos v4.0 ASP.NET existentes. O recurso FriendlyURLs também facilita que os desenvolvedores adicionem suporte móvel aos seus aplicativos, suportando a troca entre visualizações de desktop e mobile.

Para obter mais informações sobre como instalar [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)e usar urls ASP.NET amigável consulte .

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>Problemas conhecidos e mudanças de quebra

Esta seção descreve problemas conhecidos e alterações de quebra que estão na versão ASP.NET e Web Tools 2012.2.

### <a name="installation-issues"></a>Problemas de instalação

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Instalações fora de ordem do Visual Studio 2012

A instalação de um SKU adicional do Visual Studio 2012 após a instalação do ASP.NET e do Web Tools 2012.2 exigirá uma operação de reparo. Considere a sequência a seguir:

1. Instale o Visual Studio 2012 Express para Web
2. Instalar ASP.NET e Web Tools 2012.2
3. Instale o Visual Studio 2012 Profissional, Premium ou Ultimate

O passo 2 só resultaria na instalação de atualizações para o Express for Web. Para garantir que o SKU adicional instalado durante a etapa 3 contenha a atualização, você precisará reparar o ASP.NET e o Web Tools 2012.2 para instalar as atualizações do último SKU instalado. Isso também se aplica se as SKUs nas Etapas 1 e 3 forem invertidas.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Instalando o Microsoft ASP.NET e web tools 2012.2 quando o Visual Studio estiver aberto

Se o VS estiver aberto durante a instalação do Microsoft ASP.NET e web tools 2012.2, o Visual Studio pode acabar em um estado ruim. Recomenda-se que os usuários fechem todas as instâncias do Visual Studio antes de prosseguir com a instalação.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>Cancelando ASP.NET e Web Tools 2012.2 no meio da instalação

O cancelamento ASP.NET e web tools 2012.2 no meio da instalação deixará o Visual Studio em péssimo estado. Para resolver esse problema, siga estas etapas: 

- Vá para Adicionar ou Remover Programas
- Desinstale o Microsoft ASP.NET e o Web Tools 2012.2, se estiver presente.
- Reinstalar o Microsoft ASP.NET e web tools 2012.2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>Depois de desinstalar ASP.NET e Web Tools 2012.2, faltam os modelos ASP.NET MVC 4 e modelos de Site do Razor v2

A desinstalação de ASP.NET e Web Tools 2012.2 também desinstalará todos os modelos de site ASP.NET MVC 4 e Razor v2 do Visual Studio 2012.

A solução é reparar sua instalação do Visual Studio 2012 para reinstalar ASP.NET modelos mvc 4 e razor v2.

### <a name="tooling-issues"></a>Problemas de ferramentas

#### <a name="nuget-error-reported-during-project-creation"></a>Erro NuGet relatado durante a criação do projeto

Depois de instalar ASP.NET e Web Tools 2012.2, você pode ver o seguinte erro ao criar um projeto MVC 4

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

O ASP.NET e web tools 2012.2 envia o NuGet 2.1 e atualizará a extensão no Visual Studio 2012. Em alguns casos, o instalador VSIX não atualizará corretamente o VSIX. As seguintes etapas permitirão que você resolva esse problema:

1. Inicie o Visual Studio 2012 como administrador
2. Vá para&gt;Ferramentas- Extensões e Atualizações e desinstale o NuGet.
3. Fechar o Visual Studio
4. Navegue até a pasta de instalação ASP.NET e Web Tools 2012.2:

    1. Para visual studio 2012: **Arquivos de programa\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**
    2. Para visual studio 2012 Express for Web: **Arquivos de programa\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 para Web**
5. Clique duas vezes no NuGet.Tools.vsix para reinstalar o NuGet

### <a name="web-api-issues"></a>Problemas de API da Web

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>Analisar problemas em literais $filter e DateTime

O analisador OData URI não analisa adequadamente os literais parciais de data-hora. Por exemplo, $filter=start eq datetime'2012-12-31T12:00' não consegue analisar corretamente. Uma solução é usar o literal completo, $filter=start eq datetime'2012-12-31T12:00:00'.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData não suporta nomes de propriedade insensíveis a casos.

OData não suporta nomes de propriedade insensíveis a casos em consultas oData e caminho de odata. Veja os itens de trabalho:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Se os usuários tiverem invólucros diferentes no lado do cliente javascript e no lado do servidor, eles provavelmente encontrarão esse problema. Este problema é por design no protocolo odata. No entanto, muitos usuários relatam esse problema. Para contornar isso, os usuários têm que corrigir seus casos na URL.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>As convenções de roteamento oData padrão não suportam POST/PUT na propriedade de navegação.

As convenções de roteamento oData padrão não suportam POST/PUT na propriedade de navegação. Veja o [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)item de trabalho . Estamos perdendo esta convenção comumente usada em convenções padrão.

Para contornar isso, os usuários precisam estender uma nova convenção de roteamento para apoiá-la.

### <a name="facebook-template-issues"></a>Problemas de modelo do Facebook

#### <a name="facebook-application-template-only-works-using-net-45"></a>O modelo do aplicativo do Facebook só funciona usando o .NET 4.5

Você deve selecionar .NET 4.5 na lista de isato de quadro na caixa de diálogo Novo Projeto para ver o modelo de aplicativo do Facebook em ASP.NET MVC 4.

#### <a name="real-time-update-controller"></a>Controlador de atualização em tempo real

O modelo do Aplicativo do Facebook permite que o usuário crie facilmente um Controlador de API da Web para lidar com atualizações em tempo real do Facebook. Se a sua máquina de desenvolvimento estiver por trás do NAT, o controlador pode não funcionar sem uma configuração adicional de rede. Veja aqui os detalhes:[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Valores de seqüência de consulta conflito com os parâmetros do Facebook OAuth

Os campos a seguir conflitam com a URL de retorno da chamada de chamada do Facebook OAuth. Não adicione seus próprios valores de seqüência de\_consulta\_com os seguintes nomes: código, erro, descrição de erro, razão de erro.

#### <a name="using-page-inspector-with-facebook-template"></a>Usando o Inspetor de Páginas com o Modelo do Facebook

Você não pode usar o recurso Page Inspector no Visual Studio 2012 enquanto depura seu aplicativo do Facebook. O Inspetor de Páginas não suporta atualmente iframes.

### <a name="single-page-application-template-issues"></a>Problemas do modelo do aplicativo de página única

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>Com a atualização JQuery 1.9/Knockout 2.2.1, ao executar o projeto MVC SPA padrão, o novo evento de edição de itens de todo item enter focus não é tratado corretamente.

Com a atualização JQuery 1.9/Knockout 2.2.1, ao executar o projeto MVC SPA padrão, a nova edição de item todo não se concentra mais na nova caixa de edição de itens de todo o item depois de inserir o novo item todo para a lista completa.

Para contornar [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)a referência e fazer uma correção semelhante ao seguinte código de amostra:

Arquivo todo.model.js  
 todolist de função (dados), adicione a seguir:  
 **self.isSelected = ko.observável(falso);**

função todoList.prototype.addTodo, adicione o seguinte texto escureciado:  
 **self.isSelected(verdadeiro);**  
 self.newTodoTitle;&quot;&quot;

Índice de arquivo.cshtml, adicione o seguinte texto escurecido:  
 &lt;form data-bind=&quot;submit: addTodo&quot;&gt;  
 &lt;classe de&quot;entrada= addTodo&quot; &quot;tipo= texto&quot; data-bind=&quot;valor: newTodoTitle, espaço reservado: 'Digite aqui para adicionar', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;  
 &lt;/forma&gt;
