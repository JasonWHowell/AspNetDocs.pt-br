---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Criando projetos ASP.NET Web no Visual Studio 2013 | Microsoft Docs
author: tdykstra
description: Este tópico explica as opções para criar ASP.NET projetos web no Visual Studio 2013 com a Atualização 3 Aqui estão algumas das novidades para o desenvolvimento web c...
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676044"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Criação de Projetos Web do ASP.NET no Visual Studio 2013

por [Tom Dykstra](https://github.com/tdykstra)

> Este tópico explica as opções para criar projetos web ASP.NET no Visual Studio 2013 com a Atualização 3
> 
> Aqui estão alguns dos novos recursos para o desenvolvimento web em comparação com as versões anteriores do Visual Studio:
> 
> - Uma interface do usuário simples para criar projetos que ofereçam [suporte a múltiplas estruturas de ASP.NET (Formulários](#add) web, MVC e API web).
> - [ASP.NET Identity](#indauth), um novo sistema de associação ASP.NET que funciona da mesma forma em todas as ASP.NET frameworks e funciona com software de hospedagem web diferente do IIS.
> - O uso do [Bootstrap](#bootstrap) para fornecer recursos de design e tema responsivos.
> - Novos recursos para Formulários web que costumavam ser oferecidos apenas para MVC, como [criação automática de projetos de teste](#testproj) e um modelo de site da [Intranet](#winauth).
> 
> Para obter informações sobre como criar projetos web para o Azure Cloud Services ou Azure Mobile Services, consulte [Get Started com o Azure Cloud Services e ASP.NET](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) e criando um aplicativo de tabela de [classificação com o Azure Mobile Services .NET Backend](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/).

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Pré-requisitos

Este artigo se aplica ao [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) com [a Atualização 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) instalada.

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Projetos de aplicativos web versus projetos de sites

ASP.NET lhe dá uma escolha entre dois tipos de projetos web: projetos de *aplicativos web* e projetos de *sites web.* Recomendamos projetos de aplicações web para novos desenvolvimentos, e este artigo se aplica apenas a projetos de aplicativos web. Para obter mais informações, consulte [Projetos de Aplicativos Web versus Projetos de Sites no Visual Studio](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) no site do MSDN.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Visão geral da criação de projetos de aplicativos web

As etapas a seguir mostram como criar um projeto web:

1. Clique em **Novo projeto** na página **Iniciar** ou no menu **Arquivo.**
2. Na caixa de diálogo **Novo Projeto,** clique em **Web** no painel esquerdo e **ASP.NET Web Application** no painel do meio.

    ![Caixa de diálogo Novo Projeto](creating-web-projects-in-visual-studio/_static/image1.png)

    Você pode escolher **Cloud** no painel esquerdo para criar um [Azure Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [Azure Mobile Service](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)ou [Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs). Este tópico não cobre esses modelos.
3. No painel direito, clique na caixa **de seleção Adicionar insights de aplicativo ao projeto** se quiser monitoramento de saúde e uso para sua aplicação. Para obter mais informações, consulte [Monitorar desempenho em aplicativos Web](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/).
4. Especifique **nome do**projeto, **localização**e outras opções e clique em **OK**.

    O **diálogo Projeto Novo ASP.NET** é exibido.

    ![Caixa de diálogo Novo Projeto](creating-web-projects-in-visual-studio/_static/image2.png)
5. Clique em um modelo.

    ![Selecione um modelo](creating-web-projects-in-visual-studio/_static/image3.png)
6. Se você quiser adicionar suporte para estruturas adicionais não incluídas no modelo, clique na caixa de seleção apropriada. (No exemplo mostrado, você pode adicionar MVC e/ou API da Web a um projeto de Formulários da Web.)

    ![Adicionar frameworks](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>Se você quiser adicionar um projeto de teste de unidade, clique **em Adicionar testes unitários**.

    ![Adicionar testes de unidade](creating-web-projects-in-visual-studio/_static/image5.png)
8. Se você quiser um método de autenticação diferente do que o modelo fornece por padrão, clique **em Autenticação de alteração**.

    ![Configurar botão de autenticação](creating-web-projects-in-visual-studio/_static/image6.png)

    ![Configurar caixa de diálogo de autenticação](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Crie um aplicativo web ou uma máquina virtual no Azure

O Visual Studio inclui recursos que facilitam o trabalho com os serviços do Azure para hospedagem de aplicativos web. Por exemplo, você pode fazer todos os seguintes diretos do Visual Studio IDE:

- Crie e gerencie aplicativos web ou máquinas virtuais que disponibilizem seu aplicativo pela Internet.
- Exibir registros criados pelo aplicativo enquanto ele é executado na nuvem.
- Execute no modo de depuração remotamente enquanto o aplicativo é executado na nuvem.
- Exibir e gerenciar outros serviços do Azure, como bancos de dados SQL.

Você pode [criar uma conta do Azure](https://www.windowsazure.com/pricing/free-trial/) que inclui serviços básicos, como aplicativos web gratuitamente, e se você é um assinante DoMDN, você pode ativar [benefícios](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) que lhe dão créditos mensais para serviços adicionais do Azure. 

Por padrão, a caixa de diálogo **Projeto Novo ASP.NET** permite criar um aplicativo web ou uma máquina virtual para um novo projeto web. Se você não quiser criar um novo aplicativo web ou uma máquina virtual, limpe o Host na caixa de **seleção na nuvem.**

![Criar recursos remotos](creating-web-projects-in-visual-studio/_static/image8.png)

A legenda da caixa de seleção pode ser **Host na nuvem** ou Criar recursos **remotos,** e em ambos os casos o efeito é o mesmo. Se você deixar a caixa de seleção selecionada, o Visual Studio criará um aplicativo web no Azure App Service por padrão. Você pode usar a caixa de entrada para mudar isso para uma **Máquina Virtual,** se preferir. Se você ainda não entrou no Azure, você é solicitado para credenciais do Azure. Depois de fazer login, uma caixa de diálogo permite configurar os recursos que o Visual Studio criará para o seu projeto. A ilustração a seguir mostra o diálogo para um aplicativo web; diferentes opções aparecem se você optar por criar uma máquina virtual.

![Configure as configurações do aplicativo Azure](creating-web-projects-in-visual-studio/_static/image9.png)

Para obter mais informações sobre como usar esse processo para criar recursos do Azure, consulte [Get Started com o Azure e ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) e criando uma máquina virtual para um site com o Visual [Studio](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/).

O restante deste artigo fornece mais informações sobre os modelos disponíveis e suas opções. O artigo também introduz bootstrap, o layout e a estrutura de tema usada nos modelos.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Modelos de projetos web do Visual Studio 2013

O Visual Studio usa modelos para criar projetos web. Um modelo de projeto pode criar arquivos e pastas no novo projeto, instalar pacotes NuGet e fornecer código de amostra para um aplicativo de trabalho rudimentar. Os modelos implementam os mais recentes padrões web e têm como objetivo demonstrar as melhores práticas de como usar ASP.NET tecnologias, bem como dar um salto na criação de seu próprio aplicativo.

O Visual Studio 2013 fornece as seguintes opções para modelos de projetos web para projetos que visam .NET 4.5 ou versões posteriores do framework .NET:

- [Modelo vazio](#empty)
- [Modelo de Formulários da Web](#wf)
- [Modelo do MVC](#mvc)
- [Modelo de API da Web](#webapi)
- [Modelo de aplicativo de página única](#spa)
- [Modelo de Serviço Móvel Azure](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Modelos do Visual Studio 2012](#vs2012)

Você também pode instalar uma extensão do Visual Studio que fornece um [modelo do Facebook](#facebook).

Para obter informações sobre como criar projetos que visam o .NET 4, consulte [Os Modelos do Visual Studio 2012](#vs2012) mais tarde neste tópico.

Para obter informações sobre como criar aplicativos ASP.NET para clientes móveis, consulte [Suporte Móvel em ASP.NET](../../../mobile/overview.md).

<a id="empty"></a>
### <a name="empty-template"></a>Modelo vazio

O modelo Empty fornece as pastas e arquivos mínimos para um aplicativo web ASP.NET, como um arquivo de projeto (*.csproj* ou .* vbproj*) e um arquivo *Web.config.* Você pode adicionar suporte para Formulários web, MVC e/ou API da Web usando as caixas de seleção sob as **pastas Adicionar e referências principais para:** rótulo.

Para o modelo Empty, não há opções de autenticação disponíveis. A funcionalidade de autenticação é implementada em aplicativos de exemplo, e o modelo Empty não cria um aplicativo de exemplo.

<a id="wf"></a>
### <a name="web-forms-template"></a>Modelo de formulários da Web

O framework Formulários da Web fornece os seguintes recursos que permitem criar rapidamente sites que são ricos em recursos de acesso a ui e dados:

- Um designer wysiwyg no Visual Studio.
- Controles de servidor que renderizam HTML e que você pode personalizar definindo propriedades e estilos.
- Uma rica variedade de controles para acesso a dados e exibição de dados.
- Um modelo de evento que expõe eventos que você pode programar como você programaria um aplicativo cliente, como o WPF.
- Preservação automática de estado (dados) entre solicitações HTTP.

Em geral, criar um aplicativo de Formulários Web requer menos esforço de programação do que criar o mesmo aplicativo usando a estrutura mvc ASP.NET. No entanto, o Web Forms não é apenas para o desenvolvimento rápido de aplicativos. Existem muitas aplicações comerciais complexas e frameworks construídos em cima de Formulários Web.

Como uma página de Formulários da Web e os controles na página geram automaticamente grande parte da marcação enviada ao navegador, você não tem o tipo de controle fino sobre o HTML que ASP.NET MVC oferece. O modelo declarativo para configurar páginas e controles minimiza a quantidade de código que você tem para escrever, mas esconde parte do comportamento de HTML e HTTP. Por exemplo, nem sempre é possível especificar exatamente qual marcação pode ser gerada por um controle.

A estrutura de Formulários web não se presta tão facilmente quanto ASP.NET MVC a práticas de desenvolvimento baseadas em padrões, como [desenvolvimento orientado a testes,](http://en.wikipedia.org/wiki/Test-driven_development) [separação de preocupações,](http://en.wikipedia.org/wiki/Separation_of_concerns) [inversão de controle](http://en.wikipedia.org/wiki/Inversion_of_control)e injeção de [dependência.](http://en.wikipedia.org/wiki/Dependency_injection) Se você quiser escrever código fatorado dessa forma, você pode; só não é tão automático quanto no quadro mvc ASP.NET. O projeto [MVP ASP.NET Web Forms](http://webformsmvp.com/) mostra uma abordagem que facilita a separação de preocupações e testabilidade, mantendo o rápido desenvolvimento que o Web Forms foi construído para fornecer. O Microsoft SharePoint é construído no MVP do Web Forms.

O modelo Formulários da Web cria um aplicativo de formulários da Web de exemplo que usa [o Bootstrap](#bootstrap) para fornecer recursos de design e tema responsivos. A ilustração a seguir mostra a página inicial.

![Página inicial do aplicativo de modelo Formulários da Web](creating-web-projects-in-visual-studio/_static/image10.png)

Para obter mais informações sobre formulários web, consulte [ASP.NET Formulários da Web](https://asp.net/web-forms). Para obter informações sobre o que o modelo Formulários da Web faz para você, consulte [Construindo um aplicativo básico de Formulários da Web usando o Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx).

<a id="mvc"></a>
### <a name="mvc-template"></a>Modelo MVC

ASP.NET MVC foi projetado para facilitar práticas de desenvolvimento baseadas em padrões, como [desenvolvimento orientado a testes,](http://en.wikipedia.org/wiki/Test-driven_development) [separação de preocupações,](http://en.wikipedia.org/wiki/Separation_of_concerns) [inversão de controle](http://en.wikipedia.org/wiki/Inversion_of_control)e injeção de [dependência.](http://en.wikipedia.org/wiki/Dependency_injection) A estrutura incentiva a separação da camada lógica de negócios de um aplicativo web de sua camada de apresentação. Dividindo a aplicação em modelos (M), views (V) e controladores (C), ASP.NET MVC pode facilitar o gerenciamento da complexidade em aplicações maiores.

Com ASP.NET MVC, você trabalha mais diretamente com HTML e HTTP do que em Formulários web. Por exemplo, os Formulários da Web podem preservar automaticamente o estado entre as solicitações HTTP, mas você tem que codificar isso explicitamente em MVC. A vantagem do modelo MVC é que ele permite que você tenha controle total sobre exatamente o que seu aplicativo está fazendo e como ele se comporta no ambiente web. A desvantagem é que você tem que escrever mais código.

A MVC foi projetada para ser extensível, proporcionando aos desenvolvedores de energia a capacidade de personalizar a estrutura para suas necessidades de aplicativos. Além disso, o código-fonte ASP.NET MVC está disponível sob uma licença OSI.

O modelo MVC cria um aplicativo MVC 5 de amostra que usa [bootstrap](#bootstrap) para fornecer recursos de design e tema responsivos. A ilustração a seguir mostra a página inicial.

![Aplicação de amostra MVC](creating-web-projects-in-visual-studio/_static/image11.png)

Para obter mais informações sobre o MVC, consulte [ASP.NET MVC](https://asp.net/mvc). Para obter informações sobre como selecionar o modelo MVC 4, consulte [os modelos do Visual Studio 2012](#vs2012) mais tarde neste artigo.

<a id="webapi"></a>
### <a name="web-api-template"></a>Modelo de API web

O modelo de API da Web cria um serviço web de exemplo baseado na API da Web, incluindo páginas de ajuda da API com base em MVC.

O ASP.NET Web API é uma estrutura que facilita o desenvolvimento de serviços HTTP que alcançam uma ampla variedade de clientes, incluindo navegadores e dispositivos móveis. ASP.NET API da Web é uma plataforma ideal para a construção de serviços RESTful no .NET Framework.

O modelo de API da Web cria um serviço web de exemplo. As ilustrações a seguir mostram páginas de ajuda de amostras.

![Página de ajuda da Web API](creating-web-projects-in-visual-studio/_static/image12.png)

![Página de ajuda da API da Web para OBTER API](creating-web-projects-in-visual-studio/_static/image13.png)

Para obter mais informações sobre a API web, consulte [ASP.NET API web](https://asp.net/web-api).

<a id="spa"></a>
### <a name="single-page-application-template"></a>Modelo de aplicativo de página única

O modelo SPA (Single Page Application, aplicativo de página única) cria um aplicativo de exemplo que usa JavaScript, HTML 5 e [KnockoutJS](http://knockoutjs.com/) no cliente e ASP.NET API da Web no servidor.

A única opção de autenticação para o modelo SPA é [Contas de Usuário Individuais](#indauth).

A ilustração a seguir mostra o estado inicial do aplicativo de amostra que o modelo SPA constrói.

![Aplicação de amostra spa](creating-web-projects-in-visual-studio/_static/image14.png)

Para obter informações sobre como criar um aplicativo usando o modelo SPA, consulte [API Web - Serviços de Autenticação Externa](../../../web-api/overview/security/external-authentication-services.md).

Para obter mais informações sobre ASP.NET aplicativos de página única e sobre modelos adicionais de SPA que usam frameworks JavaScript diferentes do KnockoutJS, consulte os seguintes recursos:

- [ASP.NET aplicativo de página única](../../../single-page-application/index.md).
- [Entendendo os recursos de segurança no modelo SPA para VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [Aplicativos de página única: construa aplicativos web modernos e responsivos com ASP.NET](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Modelo do Facebook

Você pode instalar uma [extensão do Visual Studio que fornece um modelo do Facebook](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409). Este modelo cria um aplicativo de exemplo projetado para ser executado dentro do site do Facebook. Ele é baseado em ASP.NET MVC e usa API da Web para funcionalidade de atualização em tempo real.

Não estão disponíveis opções de autenticação para o modelo do Facebook porque os aplicativos do Facebook são executados no site do Facebook e dependem da autenticação do Facebook.

Para obter mais informações sobre ASP.NET aplicativos do Facebook, consulte [Atualizar a API do Facebook do MVC](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx).

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Modelos do Visual Studio 2012

O diálogo de criação de projetos web do Visual Studio 2013 não fornece acesso a alguns modelos que estavam disponíveis no Visual Studio 2012. Se você quiser usar um desses modelos, você pode clicar no nó Visual Studio 2012 no painel esquerdo da caixa de diálogo Visual Studio New Project.

![Modelos do Visual Studio 2012](creating-web-projects-in-visual-studio/_static/image15.png)

O **nó Visual Studio 2012** permite que você escolha os seguintes modelos da Web aos quais você não tem acesso na lista padrão de modelos para o Visual Studio 2013:

- Aplicativo Web ASP.NET MVC 4
- Aplicativo Web de entidades de dados dinâmicos ASP.NET
- ASP.NET controle do servidor AJAX
- Extensor de controle de servidor ajax ASP.NET
- controle do servidor ASP.NET

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Bootstrap nos modelos de projeto web do Visual Studio 2013

Os modelos de projeto do Visual Studio 2013 usam [bootstrap](http://getbootstrap.com/), uma estrutura de layout e tema criada pelo Twitter. Bootstrap usa CSS3 para fornecer design responsivo, o que significa que os layouts podem se adaptar dinamicamente a diferentes tamanhos de janela do navegador. Por exemplo, em uma janela ampla do navegador, a página inicial criada pelo modelo Formulários da Web parece a seguinte ilustração:

![Página inicial do aplicativo de modelo Formulários da Web](creating-web-projects-in-visual-studio/_static/image16.png)

Faça com que a janela se estreita, e as colunas horizontalmente dispostas se movam para o arranjo vertical:

![Arranjo da coluna vertical bootstrap](creating-web-projects-in-visual-studio/_static/image17.png)

Reduza um pouco mais a janela, e o menu superior horizontal se transforma em um ícone que você pode clicar para expandir para um menu orientado verticalmente:

![Ícone do menu Bootstrap](creating-web-projects-in-visual-studio/_static/image18.png)

![Menu vertical bootstrap](creating-web-projects-in-visual-studio/_static/image19.png)

Você também pode usar o recurso de temática do Bootstrap para efetuar facilmente uma alteração na aparência e sensação do aplicativo. Por exemplo, você pode fazer as seguintes etapas para alterar o tema.

1. No seu navegador, [http://Bootswatch.com](http://Bootswatch.com)vá para , escolha um tema e, em seguida, clique em **Baixar**. (Isso baixa *bootstrap.min.css* por padrão; se você quiser examinar o código CSS, obtenha *bootstrap.css* em vez da versão minified.)
2. Copie o conteúdo do arquivo CSS baixado.
3. No Visual Studio, crie um novo arquivo **de folha de estilos** chamado *bootstrap-theme.css* na pasta *Conteúdo* e cole o código CSS baixado nele.
4. Abra *\_o App Start/Bundle.config* e mude *bootstrap.css* para *bootstrap-theme.css*.

Execute o projeto novamente, e o aplicativo tem um novo visual. A ilustração a seguir mostra o efeito do tema Amelia:

![Bootstrap Amelia tema](creating-web-projects-in-visual-studio/_static/image20.png)

Muitos temas bootstrap estão disponíveis, tanto versões gratuitas quanto premium. O Bootstrap também oferece uma grande variedade de componentes de interface do iu, como [drop-downs,](http://twitter.github.io/bootstrap/components.html#dropdowns)grupos de [botões](http://twitter.github.io/bootstrap/components.html#buttonGroups)e [ícones.](http://twitter.github.io/bootstrap/base-css.html#images) Para obter mais informações sobre bootstrap, consulte [o site Bootstrap](http://twitter.github.io/bootstrap/).

Se você usar o designer web forms no Visual Studio, observe que o designer não suporta CSS3, então ele não mostra com precisão todos os efeitos dos temas bootstrap ou alterações de layout responsivas. No entanto, as páginas Formulários da Web serão exibidas corretamente quando visualizadas com um navegador.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>Adicionando suporte para estruturas adicionais

Quando você seleciona um modelo, a caixa de seleção para as estruturas usadas pelo modelo é automaticamente selecionada. Por exemplo, se você selecionar o modelo **Formulários** da Web, a caixa de seleção **Formulários da Web** será selecionada e você não poderá limpá-la.

![Selecione um modelo](creating-web-projects-in-visual-studio/_static/image21.png)

![Adicionar frameworks](creating-web-projects-in-visual-studio/_static/image22.png)

Você pode selecionar a caixa de seleção para uma estrutura que não está incluída no modelo, a fim de adicionar suporte para essa estrutura quando o projeto for criado. Por exemplo, para habilitar o uso de páginas Web Forms *.aspx* quando você tiver selecionado o modelo MVC, selecione a caixa de seleção **Formulários da Web.** Ou para ativar o MVC quando estiver usando o modelo Formulários da Web, clique na caixa de seleção **Do MVC.** A adição de uma estrutura permite o tempo de projeto, bem como o suporte em tempo de execução. Por exemplo, se você adicionar suporte a MVC a um projeto de Formulários da Web, você poderá usar controladores e visualizações de andaimes.

Se você combinar Formulários web e MVC em um projeto e habilitar [URLs amigáveis](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) em Formulários da Web, pode haver problemas de roteamento inesperados onde uma URL tem vários alvos possíveis. As rotas definidas primeiro terão precedência. Por exemplo, se `Home` você tiver um controlador e uma `http://contoso.com/home` página *Home.aspx,* a URL `EnableFriendlyUrls` irá para `MapRoute` *Home.aspx* se você chamar o método antes de `MapRoute` chamar `EnableFriendlyUrls`o método *em RouteConfig.cs,* ou a mesma URL irá para a exibição padrão do seu `Home` controlador se você ligar antes .

Adicionar uma estrutura não adiciona nenhuma funcionalidade de aplicativo de amostra. Por exemplo, se você adicionar o suporte a Formulários da Web quando tiver selecionado o modelo MVC, nenhum arquivo de página inicial *Do Padrão.aspx* será criado. Apenas as pastas, arquivos e referências necessárias para suportar o framework são adicionados. Por essa razão, a adição de frameworks não altera as opções de autenticação, que são implementadas por código em aplicativos de exemplo criados pelos modelos. Por exemplo, se você selecionar o modelo Vazio e adicionar formulários da Web ou suporte a MVC, o botão **Configurar autenticação** ainda será desativado.

As seções a seguir descrevem brevemente o efeito de cada caixa de seleção.

### <a name="add-web-forms-support"></a>Adicionar suporte a formulários web

Cria pastas vazias *de\_dados* e *modelos de aplicativos* e um arquivo *Global.asax.* Estes já são criados por todos os modelos que não sejam o modelo Vazio, portanto, selecionar a caixa de seleção formulários da Web não faz diferença para outros modelos.

O modelo Formulários da Web permite URLs amigáveis por padrão, mas quando você adiciona o suporte a Formulários da Web a outros modelos, selecionando urLs amigáveis da caixa de seleção formulários da Web não estão ativados automaticamente.

### <a name="add-mvc-support"></a>Adicionar suporte a MVC

Instala pacotes MVC, Razor e WebPages NuGet, cria pastas vazias de Dados de *\_Aplicativos,* *Controladores,* *Modelos*e *Visualizações,* cria pasta *App\_Start* com arquivo *RouteConfig.cs* e cria arquivo *Global.asax.*

### <a name="add-web-api-support"></a>Adicionar suporte à API web

Instala pacotes WebApi e Newtonsoft.Json NuGet, cria pastas vazias de Dados de *Aplicativos,\_* *Controladores*e *Modelos,* cria pasta *App\_Start* com *WebApiConfig.cs* arquivo e cria arquivo *Global.asax.*

<a id="auth"></a>
## <a name="authentication-methods"></a>Métodos de autenticação

O Visual Studio 2013 oferece várias opções de autenticação para os modelos de Web Forms, MVC e API da Web:

- [Sem autenticação](#noauth)
- [Contas de Usuário Individuais](#indauth) (identidade ASP.NET, anteriormente conhecida como associação ASP.NET)
- [Contas organizacionais](#orgauth) (Diretório Ativo do Servidor Windows ou Diretório Ativo do Azure)
- [Autenticação do Windows](#winauth) (Intranet)

![Configurar caixa de diálogo de autenticação](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>Sem Autenticação

Se você selecionar **Nenhuma Autenticação,** o aplicativo de exemplo não conterá páginas da Web para fazer login, nenhuma interface do usuário indicando quem está conectado, nenhuma classe de entidade para um banco de dados de membros e nenhuma seqüência de conexão para um banco de dados de membros.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>Contas Individuais de Usuário

Se você selecionar **Contas de Usuário Individuais,** o aplicativo de exemplo será configurado para usar ASP.NET Identidade (anteriormente conhecida como ASP.NET) para autenticação do usuário. ASP.NET Identidade permite que um usuário registre uma conta, criando um nome de usuário e senha no site ou fazendo login com provedores sociais como Facebook, Google, Microsoft Account ou Twitter. O armazenamento de dados padrão para perfis de usuário em ASP.NET Identity é um banco de dados SQL Server LocalDB, que você pode implantar no SQL Server ou no Azure SQL Database para o local de produção.

No Visual Studio 2013, esses recursos são os mesmos do Visual Studio 2012, mas o código subjacente para o sistema de associação ASP.NET foi reescrito. As vantagens da nova base de código incluem:

- O novo sistema de adesão é baseado no [OWIN](http://owin.org/) em vez do módulo de autenticação de formulários ASP.NET. Isso significa que você pode usar o mesmo mecanismo de autenticação, quer esteja usando Formulários da Web ou MVC no IIS, ou você está hospedando a API ou signalR da Web.
- O novo banco de dados de membros é gerenciado pelo Entity Framework Code First, e todas as tabelas são representadas por classes de entidadeque você pode modificar. Isso significa que você pode facilmente personalizar o esquema do banco de dados e a ui web relacionada ao perfil para atender às suas próprias necessidades, e você pode facilmente implantar suas atualizações usando as Migrações do Código Primeiro.

O novo sistema de adesão é implementado automaticamente nos novos modelos, e pode ser implementado manualmente em qualquer projeto que tenha como alvo o .NET 4.5 ou posterior.

ASP.NET Identidade é uma boa escolha se você estiver criando um site da Internet que é principalmente para clientes externos. Se sua organização usar o Active Directory ou o Office 365 e você quiser criar um projeto que habilite o login único para funcionários e parceiros de negócios, a opção **Contas Organizacionais** pode ser uma escolha melhor.

Para obter mais informações sobre a opção Contas de Usuário Individual, consulte os seguintes recursos:

- [www.asp.net/identity.](../../../identity/index.md) Documentação sobre identidade ASP.NET no site ASP.NET.
- [Crie um aplicativo mvc 5 ASP.NET com Facebook e Google OAuth2 e OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md). Também mostra como personalizar dados do perfil do usuário.
- [API Web - Serviços de Autenticação Externa](../../../web-api/overview/security/external-authentication-services.md)
- [Adicionando logins externos ao seu aplicativo de ASP.NET no Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>Contas organizacionais

Se você selecionar **Contas Organizacionais,** o aplicativo de exemplo será configurado para usar o Windows Identity Foundation (WIF) para autenticação com base em contas de usuário no Azure Active Directory (Azure AD, que inclui o Office 365) ou o Windows Server Active Directory. Para obter mais informações, consulte [opções de autenticação de conta organizacional](#orgauthoptions) mais tarde neste tópico.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Autenticação do Windows

Se você selecionar **autenticação do Windows,** o aplicativo de exemplo será configurado para usar o módulo IIS de autenticação do Windows para autenticação. O aplicativo exibirá o iD de domínio e usuário do diretório Ativo ou da conta da máquina local que está logado no Windows, mas não incluirá registro de usuário ou interface do usuário. Esta opção é destinada a sites da Intranet.

Alternativamente, você pode criar um site da Intranet que usa autenticação de AD escolhendo a [opção On-Premises em Contas Organizacionais](#orgauthonprem). A opção On-Premises usa o Windows Identity Foundation (WIF) em vez do módulo de autenticação do Windows. Algumas etapas adicionais são necessárias para configurar a opção On-Premises, mas o WIF habilita recursos que não estão disponíveis com o módulo de autenticação do Windows. Por exemplo, com o WIF, você pode configurar o acesso ao aplicativo no Active Directory e nos dados do diretório de consulta.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>Opções de autenticação de contas organizacionais

A caixa de diálogo **Configurar autenticação** oferece várias opções para o Azure Active Directory (Azure AD, que inclui a autenticação da conta do Office 365) ou do Windows Server Active Directory (AD):

- [Cloud - Organização Única](#orgauthsingle) (Azure AD, ou AD usando integração de diretório com Azure AD)
- [Cloud - Multi Organization](#orgauthmulti) (Azure AD, ou AD usando integração de diretório com a Ad do Azure)
- [Locais](#orgauthonprem) (AD)

Se você quiser experimentar uma das opções do Azure AD, mas ainda não tem uma conta, [clique aqui para se inscrever em uma conta AD do Azure](https://go.microsoft.com/fwlink/?LinkId=309942).

> [!NOTE]
> Se você escolher uma das opções do Azure AD, seu projeto requer um banco de dados e você terá que fazer login em uma conta de administrador global para o seu inquilino Azure AD. Digite o nome e a senha admin@contoso.onmicrosoft.comde uma conta organizacional (por exemplo, ) que tenha permissões administrativas para seu inquilino Azure AD.
> 
> **Não insira credenciais para uma contoso@hotmail.comconta Microsoft (por exemplo) na caixa de diálogo de login.**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>Nuvem - Autenticação de Organização Única

![Autenticação de organização única](creating-web-projects-in-visual-studio/_static/image24.png)

Escolha esta opção se você quiser habilitar a autenticação para contas de usuário definidas em um [inquilino](https://technet.microsoft.com/library/jj573650.aspx)AZure AD . Por exemplo, o site é contoso.com e será disponibilizado aos funcionários da Empresa Contoso que estão no contoso.onmicrosoft.com inquilino. Você não poderá configurar o Azure AD para permitir que usuários de outros inquilinos acessem o aplicativo.

#### <a name="domain"></a>Domínio

Digite o domínio Azure AD no que deseja configurar `contoso.onmicrosoft.com`o aplicativo, por exemplo: . Se você tem um [domínio personalizado,](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)como `contoso.com` em vez de `contoso.onmicrosoft.com`, você pode inserir isso aqui.

#### <a name="access-level"></a>Nível de acesso

Se o aplicativo precisar consultar ou atualizar informações do diretório usando a API do gráfico, escolha **'API de registro único', 'Dados do diretório de leitura'** ou dados de diretório **de registro único.** Caso contrário, escolha **o single sign-on**. Para obter mais informações, consulte [Níveis de acesso ao aplicativo](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) e usando a [API do gráfico para consultar o Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx).

#### <a name="application-id-uri"></a>Uri de id de aplicação

Por padrão, o modelo cria um URI de ID de aplicativo para você anexando o nome do projeto ao domínio Azure AD. Por exemplo, se o `Example` nome do `contoso.onmicrosoft.com`projeto for e `https://contoso.onmicrosoft.com/Example`o domínio for, o ID URI do aplicativo se tornará . Se você quiser especificar manualmente o Uri ID do aplicativo, expanda a seção **Mais Opções** e digite o Uri ID do aplicativo na caixa de texto. O ID uri de `https://`aplicação deve começar com .

Por padrão, se um aplicativo que já está provisionado no Azure AD tiver o mesmo ID URI de aplicativo que o Visual Studio está usando para o projeto, o projeto será conectado ao aplicativo existente em vez de provisionar um novo. Se você quiser que um novo aplicativo seja provisionado nesse caso, limpe a **entrada do aplicativo de sobregravar se um com o mesmo ID já existir** caixa de seleção.

Se a caixa de seleção **Sobregravar** for limpa e o Visual Studio encontrar um aplicativo existente com o mesmo ID URI do aplicativo, ele criará um novo URI anexando um número ao URI que ele usaria. Por exemplo, suponha `Example`que o nome do projeto seja , você deixa a caixa de texto em branco, `https://contoso.onmicrosoft.com/Example`limpa a caixa de seleção De gravação de **sobregravação** e o inquilino Azure AD já tem um aplicativo com o URI . Nesse caso, um novo aplicativo será provisionado com `https://contoso.onmicrosoft.com/Example_20130619330903`um URI de ID de aplicativo como .

#### <a name="provisioning-the-application-in-azure-ad"></a>Provisionamento do aplicativo no Azure AD

Para provisionar o aplicativo no Azure AD ou conectar o projeto a um aplicativo existente, o Visual Studio precisa das credenciais de um administrador global para o domínio. Quando você clica em **OK** na caixa de diálogo **Configurar autenticação,** você é solicitado para o nome de usuário e senha de um administrador global para o domínio especificado. Mais tarde, quando você **clica** em Criar projeto na caixa de diálogo **Projeto de nova ASP.NET,** o Visual Studio fornece o aplicativo no Azure AD. Observe que, como parte deste processo, o Visual Studio incorpora valores secretos do cliente no arquivo Web.config que expiram um ano após a criação.

Para obter informações sobre como criar aplicativos que usam a autenticação **Cloud - Organização Única,** consulte os seguintes recursos:

- [Autenticação Azure](../2012/windows-azure-authentication.md)
- [Adicionando logon ao seu aplicativo Web usando o Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Desenvolvendo aplicativos do ASP.NET com o Azure Active Directory](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [API da Web de ASP.NET seguro com componentes Azure AD e Microsoft OWIN](https://msdn.microsoft.com/magazine/dn463788.aspx)

Os tutoriais ainda não foram atualizados para o Visual Studio 2013; alguns dos tutoriais que direcionam você a fazer manualmente é automatizado no Visual Studio 2013.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>Cloud - Autenticação multi-organização

![Autenticação múltipla da organização](creating-web-projects-in-visual-studio/_static/image25.png)

Escolha esta opção se você quiser habilitar a autenticação para contas de usuário definidas em vários [inquilinos](https://technet.microsoft.com/library/jj573650.aspx)Azure AD . Por exemplo, o site é contoso.com e será disponibilizado para funcionários da Empresa Contoso que estão no contoso.onmicrosoft.com inquilino, e funcionários da Empresa Fabrikam que estão no fabrikam.onmicrosoft.com inquilino.

As configurações digitadas e a etapa de provisionamento de aplicativos são semelhantes à [autenticação de uma única organização.](#orgauthsingle)

Para obter informações sobre como criar aplicativos que usam autenticação **Cloud - Multi Organization,** consulte os seguintes recursos:

- [Integração fácil do aplicativo Web com &amp; o Azure Active Directory, ASP.NET Visual Studio](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) no blog Active Directory Team.
- [Desenvolvendo aplicações web multi-inquilinos com tutorial Azure AD.](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) O tutorial ainda não foi atualizado para o Visual Studio 2013; um pouco do que o tutorial orienta você a fazer manualmente é automatizado no Visual Studio 2013.
- [Você tem que se inscrever com suas próprias organizações ASP.NET aplicativo antes de entrar.](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/) Blog de Vittorio Bertocci que explica como resolver um problema comum que as pessoas encontram ao criar um projeto que usa autenticação multi-organização.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>Autenticação Organizacional no Local

![Autenticação organizacional no local](creating-web-projects-in-visual-studio/_static/image26.png)

Escolha esta opção se quiser habilitar a autenticação para contas de usuário definidas no AD (Windows Server Active Directory, diretório ativo do servidor) e você não deseja usar o Azure AD. Você pode usar esta opção para criar um site da Intranet ou um site da Internet. Para um site na Internet, use o Active Directory Federation Services (ADFS) para fornecer acesso ao AD. Para obter mais informações, consulte [Usar a Opção de Autenticação Organizacional No Local (ADFS) com ASP.NET no Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/).

Para um site da Intranet, como alternativa, você pode escolher [a Autenticação](#winauth) do Windows em vez desta opção. Para a opção Autenticação do Windows, você não precisa fornecer uma URL de documento de metadados. No entanto, a autenticação do Windows não lhe dá a capacidade de controlar o acesso ao aplicativo no Active Directory ou de consultar dados do diretório.

#### <a name="on-premises-authority"></a>Autoridade no Local

Digite uma URL que aponte para o documento de metadados. O documento de metadados contém as coordenadas da autoridade. O aplicativo usará essas coordenadas para impulsionar o fluxo de login da Web.

#### <a name="application-id-uri"></a>Uri de id de aplicação

Forneça um URI exclusivo que o AD pode usar para identificar este aplicativo ou deixe em branco para deixar o Visual Studio criar um.

<a id="nextsteps"></a>
## <a name="next-steps"></a>Próximas etapas

Este documento forneceu alguma ajuda básica para a criação de um novo projeto web ASP.NET no Visual Studio 2013. Para obter mais informações sobre como usar [https://www.asp.net/visual-studio/](../../index.md)o Visual Studio para desenvolvimento web, consulte .
