---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET Web Pages (Razor) FAQ | Microsoft Docs
author: Rick-Anderson
description: Este artigo lista algumas perguntas frequentes sobre ASP.NET Páginas da Web (Razor) e WebMatrix. Versões de software usadas no tutorial ASP.NET Páginas da Web (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543698"
---
# <a name="aspnet-web-pages-razor-faq"></a>Perguntas frequentes sobre Páginas da Web do ASP.NET (Razor)

 por [Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > O WebMatrix não é mais recomendado como um ambiente de desenvolvimento integrado para ASP.NET Páginas da Web. Use [visual studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) ou visual studio [code](https://code.visualstudio.com/).
>
> Este artigo lista algumas perguntas frequentes sobre ASP.NET Páginas da Web (Razor) e WebMatrix.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Versões de software usadas no tutorial
> 
> 
> - páginas da Web ASP.NET (Navalha) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> Este tutorial também funciona com ASP.NET Páginas Web 2, WebMatrix 2 e Visual Studio 2012.

- [Qual é a diferença entre ASP.NET Páginas da Web, ASP.NET Formulários da Web e ASP.NET MVC?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Preciso do WebMatrix para trabalhar com páginas da Web?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Posso usar ASP.NET controles de Formulários da Web em uma página de páginas da Web?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [Posso implantar um site de páginas da Web ASP.NET sem usar o WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [Tenho que usar o assistente websecurity para fazer suporte a logins?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [As páginas da Web ASP.NET suportam HTML5?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Posso usar JavaScript e jQuery com páginas da Web?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [Recursos adicionais](#AdditionalResources)

Para obter dúvidas sobre erros e outros problemas, consulte o [Guia de solução de problemas de páginas da Web (Razor) da ASP.NET](https://go.microsoft.com/fwlink/?LinkId=253001).

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>Qual é a diferença entre ASP.NET Páginas da Web, ASP.NET Formulários da Web e ASP.NET MVC?

Todos os três são tecnologias ASP.NET para criar aplicações web dinâmicas:

- ASP.NET Páginas da Web se concentra em adicionar código dinâmico (lado do servidor) e acesso ao banco de dados a páginas HTML e apresenta sintaxe simples e leve.
- ASP.NET Web Forms é baseado em um modelo de objeto de página e controles tradicionais do tipo de janela (botões, listas, etc.). O Web Forms usa um modelo baseado em eventos que é familiar para aqueles que trabalharam com o desenvolvimento baseado em cliente (formulários windows).
- ASP.NET MVC implementa o padrão modelo-view-controller para ASP.NET. A ênfase é na "separação de preocupações" (processamento, dados e camadas de IU).

Todos os três quadros são totalmente apoiados e continuam a ser desenvolvidos pela equipe ASP.NET. Em geral, a escolha de qual estrutura usar depende de sua formação e experiência com ASP.NET.

ASP.NET Páginas da Web em particular foi projetado para facilitar que pessoas que já conhecem HTML adicionem processamento de servidor às suas páginas. É uma boa escolha para estudantes, hobbystas, pessoas em geral que são novas na programação. Também pode ser uma boa escolha para desenvolvedores que têm experiência com tecnologias web non-ASP.NET.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Preciso do WebMatrix para trabalhar com páginas da Web?

Não. O WebMatrix não é mais recomendado como um ambiente de desenvolvimento integrado para ASP.NET Páginas da Web. Use [visual studio](program-asp-net-web-pages-in-visual-studio.md) ou visual studio [code](https://code.visualstudio.com/).

Se você não quiser usar o Visual Studio ou o Visual Studio Code, você pode instalar os produtos componentes individualmente usando o [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx). Você precisa dos seguintes produtos:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (que também instala o framework páginas da Web ASP.NET)
- IIS Express (o servidor web)
- Microsoft SQL Server Compact 4.0 (o banco de dados)

Você pode usar um editor de texto para editar páginas *.cshtml* (ou *.vbhtml).*

Gerenciar bancos de dados SQL Server Compact *(arquivos .sdf)* sem uma ferramenta é um pouco mais difícil. O Visual Studio contém ferramentas para gerenciar bancos de dados *.sdf.* Você também pode executar comandos SQL em código para executar muitas tarefas de gerenciamento do SQL Server.

Para testar páginas *.cshtml* sem usar um ambiente de desenvolvimento integrado (IDE), você pode implantá-las em um servidor ao vivo. (Veja [Posso implantar um site de páginas da ASP.NET sem usar o WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))

### <a name="running-iis-express-without-using-an-ide"></a>Executando o IIS Express sem usar um IDE

Se você instalar o IIS Express no seu computador como um servidor web, você pode usá-lo para testar as páginas. Você pode executar o IIS Express a partir da linha de comando e associá-lo a um número de porta específico. Em seguida, você especifica essa porta quando solicita arquivos *.cshtml* no seu navegador.

No Windows, abra um prompt de comando com privilégios de administrador e altere para *C:\Arquivos do programa\IIS Express.* (Para sistemas de 64 bits, use a pasta *C:\Program Files (x86)\IIS Express.)* Em seguida, digite o seguinte comando, usando o caminho real para o seu site:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

Você pode usar qualquer número de porta que ainda não esteja reservado por algum outro processo. (Os números da porta acima de 1024 são tipicamente gratuitos.) Para `path` o valor, use o caminho da pasta do site onde estão os arquivos *.cshtml.*

Depois de executar este comando para configurar o IIS Express para servir suas páginas, você pode abrir um navegador e navegar para um arquivo *.cshtml.* Use uma URL como a seguinte:

`http://localhost:35896/default.cshtml`

Para obter ajuda com as opções de linha de comando do IIS Express, entre `iisexpress.exe /?` na linha de comando.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Posso usar ASP.NET controles de Formulários da Web em uma página de páginas da Web?

Não. Os controles do Formulário web, como o controle [do CheckBox,](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) os [controles de validação](https://msdn.microsoft.com/library/bwd43d0x)e o controle [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) funcionam apenas em páginas de Formulários da Web (arquivos *.aspx).* Esses controles requerem a estrutura da página Formulários da Web.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>Posso implantar um site de páginas da Web ASP.NET sem usar o WebMatrix?

Sim. Você pode copiar manualmente arquivos de sites para um servidor (normalmente usando FTP). Se você executar uma cópia manual, você também terá que copiar os arquivos que suportam o SQL Server Compact (o banco de dados). Para obter detalhes, consulte a entrada do blog [Implantando aplicativos páginas da Web sem uma ferramenta](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>Tenho que usar o assistente websecurity para fazer suporte a logins?

Não. O `SimpleMembership` provedor que faz parte ASP.NET Páginas da Web é uma opção. Os provedores de segurança que fazem parte de ASP.NET (com o que você pode estar acostumado a trabalhar em Formulários Web) também estão disponíveis. Por exemplo, você pode usar a autenticação de formulários em páginas da ASP.NET Da Web, assim como faria em Formulários da Web. Para um exemplo de como usar a autenticação de formulários, consulte o artigo do Microsoft Support [How To Implement Forms-Based Authentication in Your ASP.NET Application usando C#.NET](https://support.microsoft.com/kb/301240). Para baixar um exemplo simples, consulte [ASP.NET versão de "Senha de login &amp; ](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).

Para obter informações sobre como usar a autenticação do Windows, consulte o post do blog [Usando a autenticação do Windows em ASP.NET Páginas da Web](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>As páginas da Web ASP.NET suportam HTML5?

Sim. As páginas criadas com ASP.NET Páginas da Web *(páginas .cshtml* ou *.vbhtml)* são essencialmente páginas HTML que também contêm código que é executado no servidor, antes que a página seja renderizada. Enquanto o navegador do usuário suportar HTML5, você pode usar elementos HTML5 em uma página *.cshtml* ou *.vbhtml.*

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Posso usar JavaScript e jQuery com páginas da Web?

Com certeza. As páginas que você cria com páginas da Web ASP.NET *(páginas .cshtml* ou *.vbhtml)* são apenas páginas HTML com código de servidor nelas. Portanto, qualquer coisa que você pode fazer em uma página HTML normal usando JavaScript ou jQuery você também pode fazer em uma página *.cshtml* ou *.vbhtml.*

O **modelo de site inicial** no WebMatrix contém uma série de bibliotecas jQuery. Se você criar um site usando esse modelo, a pasta *Scripts* contém uma biblioteca do núcleo jQuery *(jquery-1.6.2.js)* e bibliotecas para validação jQuery *(jquery.validate.js,* etc.).

Aqui estão alguns posts de blog que ilustram maneiras de usar jQuery com ASP.NET Páginas da Web:

- [Adicionando jQuery Goodness a ASP.NET Páginas da Web usando WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) por Rachel Appel
- [5 min: WebMatrix + jQuery UI + json + jQuery modelos](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) por Jonas Eriksson
- [WebMatrix e jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) por Mike Brind

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Recursos adicionais

[Guia de solução de problemas de Páginas da Web do ASP.NET (Razor)](https://go.microsoft.com/fwlink/?LinkId=253001)

[Fórum web matrix e ASP.NET páginas](https://forums.asp.net/1224.aspx/1?WebMatrix) da web no site ASP.NET
