---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Release Notes for ASP.NET and Web Tools 2013.1 para Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: Este documento descreve o lançamento de ASP.NET e Web Tools 2013.1 para o Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543568"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Notas de versão do ASP.NET and Web Tools 2013.1 para Visual Studio 2012

pela [Microsoft](https://github.com/microsoft)

> Este documento descreve o lançamento de ASP.NET e Web Tools 2013.1 para o Visual Studio 2012.

## <a name="contents"></a>Conteúdo

- [Notas de instalação](#install)
- [Requisitos de software](#requirements)
- Novos recursos em ASP.NET e Web Tools 2013.1 para Visual Studio 2012

    - [Bootstrap](#bootstrap)
    - [Modelos](#templates)

        - [ASP.NET modelo MVC 5](#mvc5template)
        - [ASP.NET modelo de API 2 da Web](#apitemplate)
        - [Modelos de itens](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [andaimes de ASP.NET](#scaffold)
    - [Editor de Navalha](#razor)
    - [NuGet 2.7](#nuget)
- Problemas conhecidos e mudanças de quebra

    - [andaimes de ASP.NET](#issuescaffolding)

        - [Andaimes mvc e Web API - HTTP 404, erro não encontrado](#404issue)
        - [Visual Studio Express 2012 para Web pára de funcionar depois de adicionar um item andaime](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [Visualizar arquivo cshtml com Browse With ou F5 causa um erro no servidor](#browseissue)
        - [Url Rewrite e Tilde(~)](#rewriteissue)
    - [Modelos](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>Notas de instalação

[Instalar](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET e Web Tools 2013.1 para Visual Studio 2012.

<a id="requirements"></a>
## <a name="software-requirements"></a>Requisitos de software

Você deve ter o Visual Studio 2012 ou o Visual Studio Express 2012 para web.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Novos recursos em ASP.NET e Web Tools 2013.1 para Visual Studio 2012

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Inicialização

Quando você andaime controladores e visualizações MVC 5, a marcação para as visualizações usa [Bootstrap](http://getbootstrap.com/).

<a id="templates"></a>
### <a name="templates"></a>Modelos

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET modelo MVC 5

Adicionamos um novo modelo MVC 5. Ele faz referência aos pacotes MVC 5 NuGet mais recentes, e você pode usar andaimes para adicionar controladores e visualizações.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET modelo de API 2 da Web

Adicionamos um novo modelo de API 2 da Web. Ele faz referência aos pacotes NuGet da Web API 2, e você pode usar andaimes para adicionar controladores e visualizações.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>Modelos de item

Adicionamos novos modelos de itens para visualizações MVC 5, Páginas da Web (Razor 3) e controladores de API 2 da Web. Eles instalam os pacotes NuGet relacionados ao projeto enquanto adicionam novos itens.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Quando você andaime um controlador De MVC ou Web API usando Entity Framework, usamos o Framework 6. Para obter mais informações sobre o Entity Framework, consulte o [Histórico de Versões do Quadro de Entidades](https://msdn.com/data/jj574253).

Você também pode baixar e instalar o Entity Framework 6 Tools for Visual Studio 2012. Consulte o [Quadro de Entidades Get](https://msdn.com/data/ee712906#tooling).

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>andaimes de ASP.NET

ASP.NET Andaimes é uma estrutura de geração de código para aplicações ASP.NET Web. Facilita a adição de código de caldeira ao seu projeto que interage com um modelo de dados.

Nas versões anteriores do Visual Studio, os andaimes eram limitados a projetos ASP.NET MVC. Com esta atualização, agora você pode usar andaimes para qualquer projeto ASP.NET, incluindo Formulários da Web. Esta atualização não suporta a geração de páginas para um projeto de Formulários da Web, mas você ainda pode usar andaimes com Formulários web adicionando dependências De MVC ao projeto. O suporte para gerar páginas para Formulários da Web será adicionado em uma atualização futura.

Ao usar andaimes, garantimos que todas as dependências necessárias sejam instaladas no projeto. Por exemplo, se você começar com um projeto ASP.NET Web Forms e usar andaimes para adicionar um Controlador de API da Web, os pacotes e referências NuGet necessários serão adicionados ao seu projeto automaticamente.

Para adicionar andaimes MVC a um projeto Formulários da Web, adicione um **novo item de andaimes** e selecione **dependências MVC 5** na janela de diálogo. Existem duas opções para andaimes MVC; Mínimo e completo. Se você selecionar Mínimo, apenas os pacotes e referências do NuGet para ASP.NET MVC serão adicionados ao seu projeto. Se você selecionar a opção Completa, as dependências mínimas serão adicionadas, bem como os arquivos de conteúdo necessários para um projeto MVC.

O suporte para controladores assync de andaimes usa os novos recursos de assync do Entity Framework 6.

Para obter mais informações e tutoriais, consulte ASP.NET Visão [Geral do Andaime](../2013/aspnet-scaffolding-overview.md). Esses tutoriais mostram andaimes com o Visual Studio 2013, mas também são aplicáveis ao ASP.NET e Web Tools 2013.1 para o Visual Studio 2012.

<a id="razor"></a>
### <a name="razor-editor"></a>Editor de Navalha

Com esta atualização, o Visual Studio 2012 agora suporta ferramentas/edição do Razor 3.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

O NuGet 2.7 inclui um rico conjunto de novos recursos que são descritos em detalhes no [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).

Esta versão do NuGet remove a necessidade de os usuários permitirem explicitamente que o NuGet restaure pacotes perdidos. Ao instalar o NuGet 2.7, os usuários concordam implicitamente em restaurar automaticamente os pacotes perdidos. Os usuários podem explicitamente desativar a restauração do pacote através das configurações do NuGet no Visual Studio. Essa mudança simplifica como funciona a restauração do pacote.

## <a name="known-issues-and-breaking-changes"></a>Problemas conhecidos e mudanças de quebra

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>andaimes de ASP.NET

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>Andaimes mvc e Web API - HTTP 404, erro não encontrado

Se você encontrar um erro ao adicionar um item andaime a um projeto, é possível que seu projeto seja deixado em um estado inconsistente. Algumas das mudanças feitas serão feitas em andaimes, mas outras alterações, como os pacotes NuGet instalados, não serão revertidas. Se as alterações de configuração de roteamento forem revertidas, os usuários receberão um erro HTTP 404 ao navegar em itens de andaime.

Para corrigir esse erro para MVC, adicione um novo item andaime e selecione Dependências MVC 5 (mínima ou completa). Este processo adicionará todas as alterações necessárias ao seu projeto.

Para corrigir esse erro para API da Web:

1. Adicione a seguinte classe WebApiConfig ao seu projeto.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. Configure o WebApiConfig.Registre-se no método Iniciar de aplicativos\_em Global.asax da seguinte forma:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 para Web pára de funcionar depois de adicionar um item andaime

Se o Visual Studio Express 2012 para web parar de funcionar depois de adicionar item andaime com o Entity Framework (como o Controlador API 2 da Web com ações, usando o Entity Framework), é possível que o Visual Studio Express não tenha conseguido carregar a imagem nativa de um conjunto dependente do System.Web.Extensions.

Para corrigir esse problema, configure o Visual Studio Express para trabalhar com a imagem MSIL do System.Web.Extensions:

1. Abrir o prompt de comando no modo Administrador.
2. Vá para %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE ou %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (para Windows de 64 bits).
3. Abra o VWDExpress.exe.config em um editor de texto.
4. Adicione a seguinte &lt;linha&gt;/&lt;sob&gt; o elemento de tempo de execução de configuração:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Reiniciar visual studio express 2012 para Web.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Visualizar arquivo cshtml com Browse With ou F5 causa um erro no servidor

Quando você cria um projeto MVC 5 no Visual Studio 2012 (ou abre no Visual Studio 2012 um projeto MVC 5 que foi criado no Visual Studio 2013) e tenta visualizar um arquivo cshtml usando Browse With ou F5, você receberá um erro que afirma - **Erro do servidor no aplicativo '/'**. O servidor tenta navegar para`http://localhost:XXXX/Views/../XXXX.cshtml`

Para resolver esse problema, altere a configuração **Iniciar ação** em seu projeto para **Página Específica**. Você não precisa fornecer um valor para a página.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

Depois de fazer essa alteração, a seleção de`http://localhost:XXXX`F5 navega até a raiz de sua aplicação ( ). Esse comportamento não é o mesmo que o comportamento dos projetos MVC 5 no Visual Studio 2013, onde a configuração **Página Atual** lança a página aberta.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url Rewrite e Tilde(~)

Depois de atualizar para ASP.NET Razor 3 ou ASP.NET MVC 5, a notação tilde(~) pode não funcionar corretamente se você estiver usando regravações de URL. A reescrita de URL afeta a notação de tilde(~)&gt;em &lt;elementos HTML como &lt;A/&gt;, &lt;SCRIPT/ , LINK/&gt;, e, como resultado, o tilde não é mais mapeado para o diretório raiz.

Por exemplo, se você reescrever pedidos de **asp.net/content** para **asp.net**, o atributo href em &lt;A href="~/content/"/&gt; resolve **/content/content/** em vez de **/**. Para suprimir essa alteração, você pode definir o contexto **IIS\_WasUrlRewritten** como falso em cada página da Web ou no **\_Aplicativo BeginRequest** em Global.asax.

<a id="templateissue"></a>
### <a name="templates"></a>Modelos

Quando você cria ASP.NET projetos de MVC com o Visual Studio 2012 no Windows 8.1 ou No Windows Server 2012 R2, o Visual Studio exibe uma mensagem de erro que afirma "Configurando a Web [url] para falha ASP.NET 4.5".

![erro de configuração](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Você vê esse erro porque o Visual Studio 2012 não habilita o recurso ASP.NET 4.5 quando ele é instalado nessas versões do Windows. Para habilitar ASP.NET 4.5, execute as etapas descritas nos [recursos do Turn Windows ativado ou desdiário](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).

![ativar ou desativar os recursos do Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

Alternativamente, você pode habilitar ASP.NET 4.5 através da linha de comando.

1. Abrir o prompt de comando no modo Administrador.
2. Execute o seguinte comando para habilitar ASP.NET 4.5.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
