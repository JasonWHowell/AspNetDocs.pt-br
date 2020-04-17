---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET e Web Tools para notas de lançamento do Visual Studio 2013 | Microsoft Docs
author: rick-anderson
description: Este documento descreve o lançamento de ASP.NET e Web Tools para visual studio 2013.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543490"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>Notas de versão do ASP.NET and Web Tools para Visual Studio 2013

pela [Microsoft](https://github.com/microsoft)

> Este documento descreve o lançamento de ASP.NET e Web Tools para visual studio 2013.

## <a name="contents"></a>Conteúdo

- [Notas de instalação](#TOC1)
- [Documentação](#TOC2)
- [Requisitos de software](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Novos recursos em ASP.NET e Web Tools para visual studio 2013

- [Um ASP.NET](#TOC6)
- [Nova experiência do Projeto Web](#newproj)
- [andaimes de ASP.NET](#scaffold)
- [Link do navegador](#browser-link)
- [Aprimoramentos do Visual Studio Web Editor](#web-editor)
- [Suporte a aplicativos web do azure App Service no Visual Studio](#waws)
- [Aprimoramentos de publicação da Web](#publish)
- [NuGet 2.7](#nuget)
- [formulários da Web ASP.NET](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Componentes do Microsoft OWIN](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [ASP.NET suspensão do aplicativo](#TOC15)
- [Problemas conhecidos e mudanças de quebra](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>Notas de instalação

ASP.NET e Web Tools para Visual Studio 2013 estão empacotadas no instalador principal e podem ser baixadas [aqui](https://www.asp.net/downloads).

<a id="TOC2"></a>
## <a name="documentation"></a>Documentação

Tutoriais e outras informações sobre ASP.NET e Web Tools para visual studio 2013 estão disponíveis no [site ASP.NET](https://www.asp.net/).

<a id="TOC4"></a>
## <a name="software-requirements"></a>Requisitos de software

ASP.NET e Web Tools requer o Visual Studio 2013.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Novos recursos em ASP.NET e Web Tools para visual studio 2013

As seções a seguir descrevem os recursos que foram introduzidos na versão.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>Um ASP.NET

Com o lançamento do Visual Studio 2013, demos um passo para unificar a experiência de uso de tecnologias ASP.NET, para que você possa facilmente misturar e combinar com as que você deseja. Por exemplo, você pode iniciar um projeto usando MVC e adicionar facilmente páginas de Formulários da Web ao projeto mais tarde, ou APIs da Web de andaime em um projeto formulários da Web. Uma ASP.NET é tornar mais fácil para você, como desenvolvedor, fazer as coisas que você ama em ASP.NET. Não importa qual tecnologia você escolha, você pode ter confiança de que está construindo na estrutura subjacente confiável do One ASP.NET.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>Nova experiência do Projeto Web

Melhoramos a experiência de criação de novos projetos web no Visual Studio 2013. Na caixa de diálogo **Projeto Web nova ASP.NET,** você pode selecionar o tipo de projeto que deseja, configurar qualquer combinação de tecnologias (Formulários Web, MVC, API da Web), configurar opções de autenticação e adicionar um projeto de teste de unidade.

![Projeto Nova ASP.NET](release-notes/_static/image1.png)

O novo diálogo permite alterar as opções de autenticação padrão para muitos dos modelos. Por exemplo, quando você cria um projeto ASP.NET Formulários da Web, você pode selecionar qualquer uma das seguintes opções:

- Sem Autenticação
- Contas de Usuário Individuais (ASP.NET adesão ou login do provedor social)
- Contas organizacionais (Active Directory em um aplicativo de internet)
- Autenticação do Windows (Active Directory em um aplicativo de intranet)

![Opções de autenticação](release-notes/_static/image2.png)

Para obter mais informações sobre o novo processo de criação de projetos web, consulte [Criando projetos ASP.NET Web no Visual Studio 2013](creating-web-projects-in-visual-studio.md). Para obter mais informações sobre as novas opções de autenticação, consulte [ASP.NET Identidade](#TOC8) mais tarde neste documento.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>andaimes de ASP.NET

ASP.NET Andaimes é uma estrutura de geração de código para aplicações ASP.NET Web. Facilita a adição de código de caldeira ao seu projeto que interage com um modelo de dados.

Nas versões anteriores do Visual Studio, os andaimes eram limitados a projetos ASP.NET MVC. Com o Visual Studio 2013, agora você pode usar andaimes para qualquer projeto ASP.NET, incluindo Formulários web. O Visual Studio 2013 não suporta atualmente páginas de geração para um projeto de Formulários Web, mas você ainda pode usar andaimes com Formulários Web adicionando dependências MVC ao projeto. O suporte para gerar páginas para Formulários da Web será adicionado em uma atualização futura.

Ao usar andaimes, garantimos que todas as dependências necessárias sejam instaladas no projeto. Por exemplo, se você começar com um projeto ASP.NET Web Forms e usar andaimes para adicionar um Controlador de API da Web, os pacotes e referências NuGet necessários serão adicionados ao seu projeto automaticamente.

Para adicionar andaimes MVC a um projeto Formulários da Web, adicione um **novo item de andaimes** e selecione **dependências MVC 5** na janela de diálogo. Existem duas opções para andaimes MVC; Mínimo e completo. Se você selecionar Mínimo, apenas os pacotes e referências do NuGet para ASP.NET MVC serão adicionados ao seu projeto. Se você selecionar a opção Completa, as dependências mínimas serão adicionadas, bem como os arquivos de conteúdo necessários para um projeto MVC.

O suporte para controladores assync de andaimes usa os novos recursos de assync do Entity Framework 6.

Para obter mais informações e tutoriais, consulte ASP.NET Visão [Geral do Andaime](aspnet-scaffolding-overview.md).

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>Link do Navegador – Canal SignalR entre navegador e Visual Studio

O novo recurso [Browser Link](using-browser-link.md) permite conectar vários navegadores ao Visual Studio e atualizá-los todos clicando em um botão na barra de ferramentas. Você pode conectar vários navegadores ao seu site de desenvolvimento, incluindo emuladores móveis, e clicar em atualizar todos os navegadores ao mesmo tempo. O Browser Link também expõe uma API para permitir que os desenvolvedores escrevam extensões do Browser Link.

![](release-notes/_static/image3.png)

Ao permitir que os desenvolvedores aproveitem a API do Browser Link, torna-se possível criar cenários muito avançados que cruzam fronteiras entre o Visual Studio e qualquer navegador conectado. A Web Essentials aproveita a API para criar uma experiência integrada entre o Visual Studio e as ferramentas de desenvolvedor do navegador, emuladores móveis de controle remoto e muito mais.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Aprimoramentos do Visual Studio Web Editor

Visual Studio 2013 inclui um novo editor HTML para arquivos Razor e arquivos HTML em aplicações web. O novo editor HTML fornece um único esquema unificado baseado em HTML5. Tem conclusão automática de suporte, iLic jQuery e atributo AngularJS IntelliSense, atributo IntelliSense Grouping, ID e nome de classe Intellisense, e outras melhorias, incluindo melhor desempenho, formatação e SmartTags.

A captura de tela a seguir demonstra o uso do atributo Bootstrap IntelliSense no editor HTML.

![Intellisense no editor HTML](release-notes/_static/image4.png)

O Visual Studio 2013 também vem com editores CoffeeScript e LESS embutidos. O editor LESS vem com todos os recursos legais do editor CSS e tem Intellisense @import específico para variáveis e mixins em todos os documentos LESS da cadeia.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Suporte a aplicativos web do azure App Service no Visual Studio

No Visual Studio 2013 com o Azure SDK para .NET 2.2, você pode usar **o Server Explorer** para interagir diretamente com seus aplicativos web remotos. Você pode fazer login na sua conta do Azure, criar novos aplicativos da Web, configurar aplicativos, visualizar logs em tempo real e muito mais. Logo após o lançamento do SDK 2.2, você poderá ser executado no modo de depuração remotamente no Azure. A maioria dos novos recursos para azure App Service Web Apps também funcionam no Visual Studio 2012 quando você instala a versão atual do Azure SDK para .NET.

Para saber mais, consulte os recursos a seguir:

- [Crie um aplicativo web ASP.NET no Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Solucionar problemas de um aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Aprimoramentos de publicação da Web

O Visual Studio 2013 inclui novos e aprimorados recursos da Web Publish. Veja algumas opções:

- [Automatize facilmente a criptografia de arquivos Web.config](https://go.microsoft.com/fwlink/?LinkId=325529). (Este link e os dois seguintes apontam para a documentação no MSDN que pode não estar disponível até o final do dia em 17/10.)
- [Automatize facilmente tirar um aplicativo offline durante a implantação](https://go.microsoft.com/fwlink/?LinkId=325530).
- Configure o Web Deploy para usar a [soma de verificação de arquivos em vez da data alterada pela última vez](https://go.microsoft.com/fwlink/?LinkId=325531) para determinar quais arquivos devem ser copiados para o servidor.
- Publique rapidamente arquivos selecionados individuais (incluindo Web.config) quando estiver usando os métodos de publicação do FTP ou do sistema de arquivos, bem como com o Web Deploy.

Para obter mais informações sobre ASP.NET implantação na Web, consulte [o site ASP.NET](https://go.microsoft.com/fwlink/?LinkId=322027).

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

O NuGet 2.7 inclui um rico conjunto de novos recursos que são descritos em detalhes no [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).

Esta versão do NuGet também remove a necessidade de fornecer consentimento explícito para o recurso de restauração de pacotes do NuGet para baixar pacotes. O consentimento (e a caixa de seleção associada na caixa de diálogo preferências do NuGet) agora é concedida instalando o NuGet. Agora, a restauração do pacote simplesmente funciona por padrão.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>Web Forms do ASP.NET

### <a name="one-aspnet"></a>Um ASP.NET

Os modelos de projeto Web Forms integram-se perfeitamente com a nova experiência one ASP.NET. Você pode adicionar suporte a MVC e API web ao seu projeto Formulários da Web e pode configurar a autenticação usando o assistente de criação de projetos One ASP.NET. Para obter mais informações, consulte [Criando projetos web ASP.NET no Visual Studio 2013](creating-web-projects-in-visual-studio.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Os modelos de projeto Web Forms suportam a nova estrutura de identidade ASP.NET. Além disso, os modelos agora suportam a criação de um projeto de intranet Web Forms. Para obter mais informações, consulte [Métodos de Autenticação](creating-web-projects-in-visual-studio.md#auth) na **Criação de projetos ASP.NET Web no Visual Studio 2013**.

### <a name="bootstrap"></a>Inicialização

Os modelos web forms usam [bootstrap](http://twitter.github.io/bootstrap/) para fornecer um visual elegante e responsivo e sentir que você pode facilmente personalizar. Para obter mais informações, consulte [Bootstrap nos modelos de projeto web do Visual Studio 2013.](creating-web-projects-in-visual-studio.md#bootstrap)

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>Um ASP.NET

Os modelos de projeto Web MVC integram-se perfeitamente com a nova experiência do One ASP.NET. Você pode personalizar seu projeto MVC e configurar a autenticação usando o assistente de criação de projetos One ASP.NET. Um tutorial introdutório para ASP.NET MVC 5 pode ser encontrado em [Getting Started com ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

Para obter informações sobre como atualizar projetos MVC 4 para MVC 5, consulte [Como atualizar um projeto de API ASP.NET MVC 4 e Web para ASP.NET MVC 5 e Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Os modelos de projeto MVC foram atualizados para usar ASP.NET Identidade para autenticação e gerenciamento de identidade. Um tutorial com a autenticação do Facebook e do Google e a nova API de associação pode ser encontrado no [Create a ASP.NET MVC 5 App com Facebook e Google OAuth2 e OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) e [Criar um aplicativo MVC ASP.NET com auth e SQL DB e implantar no Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).

### <a name="bootstrap"></a>Inicialização

O modelo de projeto MVC foi atualizado para usar [o Bootstrap](http://getbootstrap.com/) para fornecer um visual elegante e responsivo que você pode personalizar facilmente. Para obter mais informações, consulte [Bootstrap nos modelos de projeto web do Visual Studio 2013.](creating-web-projects-in-visual-studio.md#bootstrap)

### <a name="authentication-filters"></a>Filtros de autenticação

Os filtros de autenticação são um novo tipo de filtro em ASP.NET MVC que são executados antes dos filtros de autorização no pipeline mvc ASP.NET e permitem que você especifique a lógica de autenticação por ação, por controlador ou globalmente para todos os controladores. A autenticação filtra as credenciais do processo na solicitação e fornece um principal correspondente. Os filtros de autenticação também podem adicionar desafios de autenticação em resposta a solicitações não autorizadas.

### <a name="filter-overrides"></a>Substituições do filtro

Agora você pode substituir quais filtros se aplicam a um determinado método de ação ou controlador especificando um filtro de substituição. Os filtros de substituição especificam um conjunto de tipos de filtros que não devem ser executados para um determinado escopo (ação ou controlador). Isso permite configurar filtros que se aplicam globalmente, mas depois excluir certos filtros globais de aplicar em ações ou controladores específicos.

### <a name="attribute-routing"></a>Roteamento de atributo

ASP.NET MVC agora suporta roteamento de atributos, graças [http://attributerouting.net](http://attributerouting.net)a uma contribuição de Tim McCall, o autor de . Com o roteamento de atributos, você pode especificar suas rotas anotando suas ações e controladores.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>Roteamento de atributo

ASP.NET API da Web agora suporta roteamento de atributos, [http://attributerouting.net](http://attributerouting.net)graças a uma contribuição de Tim McCall, o autor de . Com o roteamento de atributos, você pode especificar suas rotas de API da Web anotando suas ações e controladores como este:

[!code-csharp[Main](release-notes/samples/sample1.cs)]

O roteamento de atributos oferece mais controle sobre as URIs em sua API web. Por exemplo, você pode definir facilmente uma hierarquia de recursos usando um único controlador de API:

[!code-csharp[Main](release-notes/samples/sample2.cs)]

O roteamento de atributos também fornece uma sintaxe conveniente para especificar parâmetros opcionais, valores padrão e restrições de rota:

[!code-csharp[Main](release-notes/samples/sample3.cs)]

Para obter mais informações sobre roteamento de atributos, consulte [Roteamento de atributos na API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)da Web .

### <a name="oauth-20"></a>OAuth 2.0

Os modelos de projeto de API e Aplicativo de Página Única da Web agora suportam a autorização usando o OAuth 2.0. OOAuth 2.0 é uma estrutura para autorizar o acesso do cliente a recursos protegidos. Funciona para uma variedade de clientes, incluindo navegadores e dispositivos móveis.

O suporte ao OAuth 2.0 é baseado em novos middlewares de segurança fornecidos pelos Componentes OWIN da Microsoft para autenticação do portador e implementação da função de servidor de autorização. Alternativamente, os clientes podem ser autorizados usando um servidor de autorização organizacional, como o Azure Active Directory ou o ADFS no Windows Server 2012 R2.

### <a name="odata-improvements"></a>Melhorias de odata

**Suporte para $select, $expand, $batch e $value**

ASP.NET OOData da Web atualmente tem suporte total para $select, $expand e $value. Você também pode usar $batch para solicitar loteamento e processamento de conjuntos de alterações.

As opções $select e $expand permitem alterar a forma dos dados que são retornados de um ponto final da OData. Para obter mais informações, consulte [Introdução $select e suporte $expand no Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).

**Extensibilidade melhorada**

Os Assuntos OData são agora extensíveis. Você pode adicionar metadados de entrada do Átomo, suportar entradas de stream e link de mídia nomeadas, adicionar anotações de instância e personalizar como os links são gerados.

**Suporte sem tipo**

Agora você pode construir serviços OData sem precisar definir tipos de CLR para seus tipos de entidade. Em vez disso, os controladores OData podem pegar ou retornar instâncias do **IEdmObject**, que são os Assuntos oData serializar/desserializar.

**Reutilizar um modelo existente**

Se você já tem um modelo de dados de entidade existente (EDM), agora você pode reutilizá-lo diretamente, em vez de ter que construir um novo. Por exemplo, se você estiver usando entityframework, você pode usar o EDM que a EF constrói para você.

### <a name="request-batching"></a>Solicitar loteamento

O batching de solicitação combina várias operações em uma única solicitação HTTP POST, para reduzir o tráfego de rede e fornecer uma interface de usuário mais suave e menos tagarela. ASP.NET API da Web agora suporta várias estratégias para solicitação de loteamento:

- Use o ponto final $batch de um serviço OData.
- Empacote várias solicitações em uma única solicitação de várias partes mime.
- Use um formato de loteamento personalizado.

Para habilitar o loteamento de solicitação, basta adicionar uma rota com um manipulador de lote à configuração da API da Web:

[!code-csharp[Main](release-notes/samples/sample4.cs)]

Você também pode controlar se solicitações ou executados sequencialmente ou em qualquer ordem.

### <a name="portable-aspnet-web-api-client"></a>Cliente de API web ASP.NET portátil

Agora você pode usar o ASP.NET Cliente de API da Web para criar bibliotecas de classe portáteis que funcionam em seus aplicativos Windows Store e Windows Phone 8. Você também pode criar formatters portáteis que podem ser compartilhados entre cliente e servidor.

### <a name="improved-testability"></a>Testability aprimorada

A API 2 da Web torna muito mais fácil testar seus controladores de API. Basta instanciar seu controlador de API com sua mensagem de solicitação e configuração e, em seguida, chamar o método de ação que deseja testar. Também é fácil zombar da classe **UrlHelper,** para métodos de ação que executam a geração de links.

### <a name="ihttpactionresult"></a>IhttpActionresult

Agora você pode implementar o IHttpActionResult para encapsular o resultado de seus métodos de ação da API da Web. Um IHttpActionResult retornado de um método de ação da API da Web é executado pela ASP.NET tempo de execução da API da Web para produzir a mensagem de resposta resultante. Um IHttpActionResult pode ser retornado de qualquer ação da API da Web para simplificar o teste unitário da implementação da API da Web. Para conveniência, uma série de implementações do IHttpActionResult são fornecidas fora da caixa, incluindo resultados para o retorno de códigos de status específicos, conteúdo formatado ou respostas negociadas com conteúdo.

### <a name="httprequestcontext"></a>HttpRequestContext

O novo **HttpRequestContext** rastreia qualquer estado vinculado à solicitação, mas não está disponível imediatamente a partir da solicitação. Por exemplo, você pode usar o **HttpRequestContext** para obter dados de rota, o principal associado à solicitação, o certificado do cliente, o **UrlHelper** e a raiz do caminho virtual. Você pode facilmente criar um **HttpRequestContext** para fins de teste de unidade.

Como o principal da solicitação é fluído com a solicitação em vez de depender do **Thread.CurrentPrincipal,** o principal agora está disponível durante toda a vida útil da solicitação enquanto estiver no pipeline da API da Web.

### <a name="cors"></a>CORS

Graças a outra grande contribuição de Brock Allen, ASP.NET agora apoia totalmente o Cross Origin Request Sharing (CORS).

A segurança do navegador impede que uma página da Web envie solicitações do AJAX para outro domínio. [Cors](http://www.w3.org/TR/cors/) é um padrão W3C que permite que um servidor relaxe a política de mesma origem. Usando o CORS, um servidor pode explicitamente permitir algumas solicitações entre origens e rejeitar outras.

A Web API 2 agora suporta CORS, incluindo o manuseio automático de solicitações de pré-vôo. Para saber mais, confira [Permitindo solicitações entre origens na ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).

### <a name="authentication-filters"></a>Filtros de autenticação

Os filtros de autenticação são um novo tipo de filtro em ASP.NET API da Web que são executados antes dos filtros de autorização no pipeline de API da ASP.NET e permitem que você especifique a lógica de autenticação por ação, por controlador ou globalmente para todos os controladores. A autenticação filtra as credenciais do processo na solicitação e fornece um principal correspondente. Os filtros de autenticação também podem adicionar desafios de autenticação em resposta a solicitações não autorizadas.

### <a name="filter-overrides"></a>Substituições do filtro

Agora você pode substituir quais filtros se aplicam a um determinado método de ação ou controlador, especificando um filtro de substituição. Os filtros de substituição especificam um conjunto de tipos de filtros que não devem ser executados para um determinado escopo (ação ou controlador). Isso permite adicionar filtros globais, mas depois excluir alguns de ações ou controladores específicos.

### <a name="owin-integration"></a>Integração OWIN

ASP.NET API da Web agora suporta totalmente o OWIN e pode ser executada em qualquer host capaz de OWIN. Também está incluído um **HostAuthenticationFilter** que fornece integração com o sistema de autenticação OWIN.

Com a integração OWIN, você pode hospedar a API da Web em seu próprio processo ao lado de outros middleware oWIN, como o SignalR. Para obter mais informações, consulte [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2.0

As seções a seguir descrevem características do SignalR 2.0.

- [Construído em OWIN](#builtonowin)
- [MapHubs e MapConnection agora são MapSignalR](#MapSignalR)
- [Suporte entre domínios](#crossdomain)
- [Suporte para iOS e Android via MonoTouch e MonoDroid](#mobile)
- [Cliente portátil .NET](#portable)
- [Novo pacote de auto-host](#selfhost)
- [Suporte ao servidor compatível com atraso](#backwardcompat)
- [Suporte ao servidor removido para .NET 4.0](#remove40)
- [Enviando uma mensagem para uma lista de clientes e grupos](#messagelist)
- [Enviando uma mensagem para um usuário específico](#sendtouser)
- [Melhor suporte para manipulação de erros](#errorhandling)
- [Teste unitário mais fácil de hubs](#unittesting)
- [Manuseio de erros JavaScript](#javascripterror)

Para obter um exemplo de como atualizar um projeto 1.x existente para o SignalR 2.0, consulte [Atualizando um Projeto SignalR 1.x](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>Construído em OWIN

O SignalR 2.0 é construído completamente no [OWIN (a Interface Web Aberta para .NET)](http://owin.org/). Essa alteração torna o processo de configuração do SignalR muito mais consistente entre aplicativos SignalR hospedados na Web e auto-hospedados, mas também exigiu uma série de alterações de API.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs e MapConnection agora são MapSignalR

Para compatibilidade com as normas OWIN, esses `MapSignalR`métodos foram renomeados para . `MapSignalR`chamado sem parâmetros mapeará `MapHubs` todos os hubs (como faz na versão 1.x); para mapear objetos individuais **persistentConnection,** especificar o tipo de conexão como parâmetro de tipo e a extensão URL para a conexão como o primeiro argumento.

O `MapSignalR` método é chamado em uma aula de startup Owin. Visual Studio 2013 contém um novo modelo para uma classe de inicialização Owin; para usar este modelo, faça o seguinte:

1. Clique com o botão direito do mouse no projeto
2. Selecione **Adicionar,** **Novo Item...**
3. Selecione **a classe Owin Startup**. Nomeie o novo **Startup.cs de**classe.

Em um **aplicativo da Web,** a `MapSignalR` classe de inicialização Owin que contém o método é adicionada ao processo de inicialização da Owin usando uma entrada no nó de configurações do arquivo Web.Config, conforme mostrado abaixo.

Em um **aplicativo auto-hospedado,** a classe Startup é passada `WebApp.Start` como parâmetro de tipo do método.

**Mapeamento de hubs e conexões no SignalR 1.x (a partir do arquivo de aplicativo global em um aplicativo web):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**Mapeamento de hubs e conexões no SignalR 2.0 (a partir de um arquivo de classe Owin Startup):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

Em um **aplicativo auto-hospedado,** a classe Startup é passada `WebApp.Start` como parâmetro de tipo para o método, conforme mostrado abaixo.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>Suporte entre domínios

No SignalR 1.x, as solicitações de domínio cruzado eram controladas por um único sinalizador EnableCrossDomain. Esta bandeira controlava tanto as solicitações JSONP quanto CORS. Para maior flexibilidade, todo o suporte ao CORS foi removido do componente do servidor do SignalR (os clientes JavaScript ainda usam o CORS normalmente se for detectado que o navegador o suporta), e novos middleware oWIN foram disponibilizados para suportar esses cenários.

No SignalR 2.0, se o JSONP for necessário no cliente (para suportar solicitações de domínio cruzado `EnableJSONP` em `HubConfiguration` navegadores mais antigos), ele precisará ser ativado explicitamente definindo o objeto para `true`, como mostrado abaixo. O JSONP é desativado por padrão, pois é menos seguro que o CORS.

Para adicionar o novo middleware CORS no SignalR 2.0, adicione a `Microsoft.Owin.Cors` biblioteca ao seu projeto e ligue `UseCors` antes do seu middleware SignalR, como mostrado na seção abaixo.

**Adicionando Microsoft.Owin.Cors ao seu projeto**: Para instalar esta biblioteca, execute o seguinte comando no Console do Gerenciador de Pacotes:

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

Este comando adicionará a versão 2.0.0 do pacote ao seu projeto.

**Chamando UseCors**

Os seguintes trechos de código demonstram como implementar conexões entre domínios no SignalR 1.x e 2.0.

**Implementação de solicitações de domínio cruzado no SignalR 1.x (a partir do arquivo de aplicativo global)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**Implementação de solicitações de domínio cruzado no SignalR 2.0 (a partir de um arquivo de código C#)**

O código a seguir demonstra como ativar cors ou JSONP em um projeto SignalR 2.0. Esta amostra `Map` de `RunSignalR` código `MapSignalR`usa e, em vez de, de modo que o middleware CORS é executado apenas `MapSignalR`para as solicitações SignalR que requerem suporte ao CORS (em vez de todo o tráfego no caminho especificado em .) `Map` também pode ser usado para qualquer outro middleware que precise ser executado para um prefixo de URL específico, em vez de para toda a aplicação.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>Suporte para iOS e Android via MonoTouch e MonoDroid

O suporte foi adicionado para clientes iOS e Android usando componentes MonoTouch e MonoDroid da [biblioteca Xamarin](https://xamarin.com/). Para obter mais informações sobre como usá-los, consulte [Usando componentes de Xamarin](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln). Esses componentes estarão disponíveis na [Loja Xamarin](https://store.xamarin.com/) quando a versão SignalR RTW estiver disponível.

<a id="portable"></a>### Cliente portátil .NET

Para facilitar melhor o desenvolvimento entre plataformas, os clientes Silverlight, WinRT e Windows Phone foram substituídos por um único cliente portátil .NET que suporta as seguintes plataformas:

- NET 4.5
- Silverlight 5
- WinRT (.NET para aplicativos da Windows Store)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>Novo pacote de auto-host

Agora há um pacote NuGet para facilitar o início do SignalR Self-Host (aplicativos SignalR que estão hospedados em um processo ou outro aplicativo, em vez de serem hospedados em um servidor web). Para atualizar um projeto de auto-host construído com o SignalR 1.x, remova o pacote Microsoft.AspNet.SignalR.Owin e adicione o pacote Microsoft.AspNet.SignalR.SelfHost. Para obter mais informações sobre como começar com o pacote de auto-host, consulte [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>Suporte ao servidor compatível com atraso

Nas versões anteriores do SignalR, as versões do pacote SignalR utilizada no cliente e no servidor precisavam ser idênticas. Para suportar aplicativos de cliente grosso que seriam difíceis de atualizar, o SignalR 2.0 agora suporta o uso de uma versão de servidor mais recente com um cliente mais antigo. **Nota: O SignalR 2.0 não suporta servidores construídos com versões mais antigas com clientes mais novos.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>Suporte ao servidor removido para .NET 4.0

O SignalR 2.0 deixou de lado o suporte para interoperabilidade do servidor com o .NET 4.0. .NET 4.5 deve ser usado com servidores SignalR 2.0. Ainda há um cliente .NET 4.0 para SignalR 2.0.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>Enviando uma mensagem para uma lista de clientes e grupos

No SignalR 2.0, é possível enviar uma mensagem usando uma lista de IDs de cliente e grupo. Os seguintes trechos de código demonstram como fazer isso.

**Enviando uma mensagem para uma lista de clientes e grupos usando PersistentConnection**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**Enviando uma mensagem para uma lista de clientes e grupos usando hubs**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>Enviando uma mensagem para um usuário específico

Esse recurso permite que os usuários especifiquem o que o IId é baseado em uma IRequest através de uma nova interface IUserIdProvider:

**A interface IUserIdProvider**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

Por padrão, haverá uma implementação que usa o IPrincipal.Identity.Name do usuário como o nome do usuário.

Nos hubs, você poderá enviar mensagens para esses usuários através de uma nova API:

**Usando a API Clientes.Usuário**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>Melhor suporte para manipulação de erros

Os usuários agora podem jogar **hubException** de qualquer invocação do hub. O construtor do **HubException** pode levar uma mensagem de seqüência e um objeto de erro extra. O SignalR serializará automaticamente a exceção e enviará ao cliente onde ela será usada para rejeitar/falhar a invocação do método hub.

A configuração **de exceções de hub detalhadas** não tem qualquer relação com **o HubException** sendo enviado de volta ao cliente ou não; ele é sempre enviado.

**Código do lado do servidor demonstrando o envio de um HubException para o cliente**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**Código cliente JavaScript demonstrando responder a um HubException enviado do servidor**

[!code-html[Main](release-notes/samples/sample16.html)]

**.NET código de cliente demonstrando responder a um HubException enviado do servidor**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>Teste unitário mais fácil de hubs

O SignalR 2.0 inclui `IHubCallerConnectionContext` uma interface chamada no Hubs que facilita a criação de invocações falsas do lado do cliente. Os seguintes trechos de código demonstram o uso desta interface com arreios de teste populares [xUnit.net](https://github.com/xunit/xunit) e [moq](https://code.google.com/p/moq/).

**Sinalizador de teste da unidade com xUnit.net**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Sinal de teste unitário com moq**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>Manuseio de erros JavaScript

No SignalR 2.0, todos os retornos de chamada de manipulação de erros JavaScript retornam objetos de erro JavaScript em vez de strings cruas. Isso permite que o SignalR flua informações mais ricas para seus manipuladores de erros. Você pode obter a `source` exceção interna da propriedade do erro.

**Código cliente JavaScript que lida com a exceção Start.Fail**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Identity

### <a name="new-aspnet-membership-system"></a>Novo sistema de adesão ASP.NET

ASP.NET Identity é o novo sistema de adesão para aplicações ASP.NET. ASP.NET Identidade facilita a integração de dados de perfil específicos do usuário com dados de aplicativos. ASP.NET Identity também permite que você escolha o modelo de persistência para perfis de usuários em seu aplicativo. Você pode armazenar os dados em um banco de dados do SQL Server ou outro dispositivo de armazenamento de dados, incluindo dispositivos de armazenamento de dados NoSQL como Tabelas de Armazenamento do Azure. Para obter mais informações, consulte [Contas de Usuário Individuais](creating-web-projects-in-visual-studio.md#indauth) na Criação de projetos ASP.NET Web no Visual Studio **2013**.

### <a name="claims-based-authentication"></a>Autenticação baseada em declarações

ASP.NET agora suporta autenticação baseada em sinistros, onde a identidade do usuário é representada como um conjunto de reivindicações de um emissor confiável. Os usuários podem ser autenticados usando um nome de usuário e senha mantidos em um banco de dados de aplicativos, ou usando provedores de identidade social (por exemplo: Contas Microsoft, Facebook, Google, Twitter), ou usando contas organizacionais através do Azure Active Directory ou Active Directory Federation Services (ADFS).

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Integração com o Azure Active Directory e o Windows Server Active Directory

Agora você pode criar ASP.NET projetos que usam o Azure Active Directory ou o Windows Server Active Directory (AD) para autenticação. Para obter mais informações, consulte [Contas Organizacionais](creating-web-projects-in-visual-studio.md#orgauth) na **Criação de projetos ASP.NET Web no Visual Studio 2013**.

### <a name="owin-integration"></a>Integração OWIN

ASP.NET autenticação agora é baseada em middleware OWIN que pode ser usado em qualquer host baseado em OWIN. Para obter mais informações sobre o OWIN, consulte a seguinte seção [componentes do Microsoft OWIN.](#TOC7)

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Componentes do Microsoft OWIN

[A Interface Web aberta para .NET](http://owin.org/) (OWIN) define uma abstração entre servidores web .NET e aplicativos web. OOWIN desacopla o aplicativo web do servidor, tornando os aplicativos web host-agnósticos. Por exemplo, você pode hospedar um aplicativo web baseado em OWIN no IIS ou hospedá-lo em um processo personalizado.

As alterações introduzidas nos componentes do Microsoft OWIN (também conhecido como projeto Katana) incluem novos componentes de servidor e host, novas bibliotecas de ajudantes e middleware e novos middlewares de autenticação.

Para obter mais informações sobre o OWIN e a Katana, veja [o que há de novo na OWIN e katana](../../../aspnet/overview/owin-and-katana/index.md).

**Nota: Os aplicativos [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) não podem ser executados no modo clássico Do IIS; eles devem ser executados no modo integrado.**

**Nota: As aplicações [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) devem ser executadas em total confiança.**

### <a name="new-servers-and-hosts"></a>Novos servidores e hosts

Com esta versão, novos componentes foram adicionados para permitir cenários de auto-host. Esses componentes incluem os seguintes pacotes NuGet:

- **Microsoft.Owin.Host.HttpListener**. Fornece um servidor OWIN que usa **httplistener** para ouvir solicitações HTTP e direcioná-las para o pipeline OWIN.
- **Microsoft.Owin.Hosting** Fornece uma biblioteca para desenvolvedores que desejam hospedar um pipeline OWIN em um processo personalizado, como um aplicativo de console ou serviço Windows.
- **OwinHost**. Fornece um executável autônomo que `Microsoft.Owin.Hosting` envolve e permite que você hospede um pipeline OWIN sem ter que escrever um aplicativo host personalizado.

Além disso, `Microsoft.Owin.Host.SystemWeb` o pacote agora permite que o middleware forneça dicas ao servidor **SystemWeb,** indicando que o middleware deve ser chamado durante um estágio específico de ASP.NET pipeline. Esse recurso é particularmente útil para middleware de autenticação, que deve ser executado no início do ASP.NET pipeline.

### <a name="helper-libraries-and-middleware"></a>Bibliotecas auxiliares e Middleware

Embora você possa escrever componentes OWIN usando apenas as definições de `Microsoft.Owin` função e tipo da especificação OWIN, o novo pacote fornece um conjunto mais fácil de usar abstrações. Este pacote combina vários pacotes anteriores `Owin.Extensions`(por exemplo, ) `Owin.Types`em um único modelo de objeto bem estruturado que pode ser facilmente usado por outros componentes OWIN. Na verdade, a maioria dos componentes do Microsoft OWIN agora usa este pacote.

> [!NOTE]
> Os aplicativos [OWIN](http://www.owin.org) não podem ser executados no modo clássico Do IIS; eles devem ser executados no modo integrado.

> [!NOTE]
> As aplicações [OWIN](http://www.owin.org) devem ser executadas em total confiança.

Esta versão também inclui o pacote Microsoft.Owin.Diagnostics, que inclui middleware para validar um aplicativo OWIN em execução, além de middleware de página de erro para ajudar a investigar falhas.

### <a name="authentication-components"></a>Componentes de autenticação

Os seguintes componentes de autenticação estão disponíveis.

- **Microsoft.Owin.Security.ActiveDirectory**. Permite a autenticação usando serviços de diretório on-premise ou baseados em nuvem.
- **Microsoft.Owin.Security.Cookies** Habilita a autenticação usando cookies. Este pacote foi `Microsoft.Owin.Security.Forms`previamente nomeado .
- **Microsoft.Owin.Security.Facebook** Permite a autenticação usando o serviço baseado em OAuth do Facebook.
- **Microsoft.Owin.Security.Google** Habilita a autenticação usando o serviço baseado em OpenID do Google.
- **Microsoft.Owin.Security.Jwt** Habilita a autenticação usando tokens JWT.
- **Microsoft.Owin.Security.MicrosoftAccount** Habilita a autenticação usando contas microsoft.
- **Microsoft.Owin.Security.OAuth**. Fornece um servidor de autorização OAuth, bem como middleware para autenticar tokens do portador.
- **Microsoft.Owin.Security.Twitter** Permite a autenticação usando o serviço baseado em OAuth do Twitter.

Esta versão também `Microsoft.Owin.Cors` inclui o pacote, que contém middleware para processar solicitações HTTP de origem cruzada.

> [!NOTE]
> O suporte para assinatura jwt foi removido na versão final do Visual Studio 2013.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Para obter uma lista de novos recursos e outras alterações no Quadro de Entidades 6, consulte [Entity Framework Version History](https://msdn.com/data/jj574253).

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3 inclui os seguintes novos recursos:

- Suporte para edição de guias. Anteriormente, o comando **Format Document,** o recuo automático e a formatação automática no Visual Studio não funcionavam corretamente ao usar a opção **'Manter guias'.** Esta alteração corrige a formatação do Visual Studio para código Razor para formatação de guias.
- Suporte para regras de regravação de URL ao gerar links.
- Remoção do atributo transparente de segurança.
  > [!NOTE]
  > Esta é uma mudança de ruptura, e torna razor 3 incompatível com MVC4 e anteriormente, enquanto Razor 2 é incompatível com MVC5 ou conjuntos compilados contra MVC5.

Os problemas de Razor 3 corrigidos no Visual Studio 2013 a partir de versões de pré-lançamento podem ser encontrados [aqui](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET suspensão do aplicativo

ASP.NET App Suspend é um recurso que muda o jogo no .NET Framework 4.5.1 que muda radicalmente a experiência do usuário e o modelo econômico para hospedar um grande número de sites de ASP.NET em uma única máquina. Para obter mais informações, consulte [ASP.NET App Suspend – responsivo de hospedagem web .NET](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>Problemas conhecidos e mudanças de quebra

Esta seção descreve problemas conhecidos e alterações de quebra no ASP.NET e Web Tools para visual studio 2013.

### <a name="nuget"></a>NuGet

- [A nova restauração do pacote não funciona no Mono ao usar o arquivo SLN](https://nuget.codeplex.com/workitem/3596) – será corrigida em um próximo download nuget.exe e atualização [do pacote NuGet.CommandLine.](http://www.nuget.org/packages/NuGet.CommandLine/)
- [A nova restauração do pacote não funciona com projetos Wix](https://nuget.codeplex.com/workitem/3598) – será corrigida em um próximo download nuget.exe e atualização [do pacote NuGet.CommandLine.](http://www.nuget.org/packages/NuGet.CommandLine/)
- [A restauração automática do pacote não funciona para projetos em uma pasta de solução](https://nuget.codeplex.com/workitem/3625) – será corrigida no NuGet 2.8.

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`não retorna `IQueryable<T>` sempre, como adicionamos `$select` `$expand`apoio e .

    Nossas amostras `ODataQueryOptions<T>` anteriores para sempre `ApplyTo` lançaram o valor de retorno de . `IQueryable<T>` Isso funcionou antes porque as opções`$filter`de `$orderby` `$skip`consulta `$top`que suportamos anteriormente ( , , ) não alteram a forma da consulta. Agora que `$select` apoiamos e `$expand` `ApplyTo` o valor `IQueryable<T>` de retorno não será sempre.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    Se você estiver usando o código de amostra de anteriormente, ele continuará funcionando se o cliente não enviar `$select` e `$expand`. No entanto, se `$select` `$expand` você deseja apoiar e você tem que alterar esse código para isso.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **Request.Url ou RequestContext.Url é nulo durante uma solicitação em lote**

    Em um cenário de loteamento, **o UrlHelper** é nulo quando acessado em **Request.Url** ou **RequestContext.Url**.

    Este problema está atualmente rastreado aqui: [BatchRequestContext.Url é nulo para solicitação de loteamento](http://aspnetwebstack.codeplex.com/workitem/1301).

    A solução alternativa para este problema é criar uma nova instância do **UrlHelper,** como no exemplo a seguir:

    **Criando uma nova instância do UrlHelper**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. Ao usar o MVC5 e o OrgAuth, se você tiver visualizações que fazem validação antiforgerToken, você pode se deparar com o seguinte erro ao postar dados na exibição:

    **Erro**:

    *Erro de servidor no aplicativo '/'.*

    <em>Uma reivindicação do<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>tipo<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' ou ' ' não estava presente no ClaimsIdentity fornecido. Para habilitar o suporte a tokens anti-falsificação com autenticação baseada em sinistros, verifique se o provedor de sinistros configurado está fornecendo essas duas reclamações nas instâncias de Identidade de Sinistros que gera. Se o provedor de sinistros configurado usar um tipo de reclamação diferente como um identificador exclusivo, ele pode ser configurado definindo a propriedade estática AntiForgeryConfig.UniqueClaimTypeIdentifier.</em>

    **Solução do problema**:

    Adicione a seguinte linha em Global.asax para corrigi-la:

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    Isso será corrigido para o próximo lançamento.
2. Depois de atualizar um aplicativo MVC4 para MVC5, construa a solução e inicie-a. Você deve ver o seguinte erro:

    [A] System.Web.WebPages.Razor.Configuration.HostSection não pode ser lançado para [B]System.Web.WebPages.Razor.Configuration.HostSection. O tipo A é originário de 'System.Web.WebPages.Razor, Version=2.0.0.0, Cultura=neutro, PublicKeyToken=31bf3856ad364e35' no contexto 'Padrão' no local\_'C:\windows\Microsoft.Net\assembly\ASSEMBLY\GAC\_MSIL\System.Web.WebPages.Razor\v4.0 2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'. O tipo B se origina de 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' no contexto 'Padrão' no local 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Arquivos de ASP.NET temporários\root\6 d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.

    Para corrigir o erro acima, abra *todos os* arquivos Web.config (incluindo os da pasta Views) em seu projeto e faça o seguinte:

   1. Atualizar todas as ocorrências da versão "4.0.0.0" de "System.Web.Mvc" para "5.0.0.0".
   2. Atualize todas as ocorrências da versão "2.0.0.0" &quot;de "System.Web.Helpers", System.Web.WebPages&quot; e &quot;System.Web.WebPages.Razor&quot; para "3.0.0.0"

      Por exemplo, depois de fazer as alterações acima, as vinculações de montagem devem ser assim:

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      Para obter informações sobre como atualizar projetos MVC 4 para MVC 5, consulte [Como atualizar um projeto de API ASP.NET MVC 4 e Web para ASP.NET MVC 5 e Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).
3. Ao usar a validação do lado do cliente com a validação unobtrusive jQuery, a mensagem de validação às vezes é incorreta para um elemento de entrada HTML com type='number'. O erro de validação de um valor necessário ("O campo Age é necessário") é mostrado quando um número inválido é inserido em vez da mensagem correta de que um número válido é necessário.

    Este problema é comumente encontrado com código andaime para um modelo com uma propriedade inteira nas visualizações Criar e Editar.

    Para contornar esse problema, mude o ajudante do editor de:

    `@Html.EditorFor(person => person.Age)`

    Para:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 não suporta mais confiança parcial. Os projetos vinculados aos binários MVC ou WebAPI devem remover o atributo [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) e o atributo [AllowPartiallyTrustedCallers.](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) A remoção desses atributos eliminará erros de compilador, como o seguinte.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > Observe, como efeito colateral disso, você não pode usar conjuntos 4.0 e 5.0 no mesmo aplicativo. Você precisa atualizar todos eles para 5.0.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>Modelo spa com autorização do Facebook pode causar instabilidade no IE enquanto o site está hospedado na zona intranet

O modelo SPA fornece login externo com o Facebook. Quando o projeto criado com o modelo estiver sendo executado localmente, a assinatura pode causar a falha do IE.

Solução:

1. Hospedar o site na região da internet; Ou

2. Teste o cenário em um navegador diferente do IE.

### <a name="web-forms-scaffolding"></a>Scaffolding de Web Forms

O Web Forms Sandaiming foi removido do VS2013 e estará disponível em uma futura atualização para o Visual Studio. No entanto, você ainda pode usar andaimes dentro de um projeto Web Forms adicionando dependências de MVC e gerando andaimes para MVC. Seu projeto conterá uma combinação de Formulários Web e MVC.

Para adicionar MVC ao seu projeto Formulários web, adicione um novo item andaime e selecione **Dependências MVC 5**. Selecione Mínimo ou Completo, dependendo se você precisa de todos os arquivos de conteúdo, como scripts. Em seguida, adicione um item andaime para MVC, que criará visualizações e um controlador em seu projeto.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>Andaimes mvc e Web API - HTTP 404, erro não encontrado

Se um erro for encontrado ao adicionar um item andaime a um projeto, é possível que seu projeto seja deixado em um estado inconsistente. Algumas das mudanças feitas serão feitas em andaimes, mas outras alterações, como os pacotes NuGet instalados, não serão revertidas. Se as alterações de configuração de roteamento forem revertidas, os usuários receberão um erro HTTP 404 ao navegar em itens de andaime.

Solução alternativa:

- Para corrigir esse erro para MVC, adicione um novo item andaime e selecione Dependências MVC 5 (mínima ou completa). Este processo adicionará todas as alterações necessárias ao seu projeto.
- Para corrigir esse erro para API da Web:

  1. Adicione a classe WebApiConfig ao seu projeto.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. Configure o WebApiConfig.Registre-se no método Iniciar de aplicativos\_em Global.asax da seguinte forma:

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
