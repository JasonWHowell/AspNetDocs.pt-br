---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET e Web Tools 2013.2 para notas de lançamento do Visual Studio 2013 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 41b0f3ad43846bc5799ecd398188b0f6ffcc0d66
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543620"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>Notas de versão do ASP.NET and Web Tools 2013.2 para Visual Studio 2013

pela [Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>Notas de instalação

ASP.NET e Web Tools para Visual Studio 2013.2 são empacotados no instalador principal e podem ser baixados como parte do [Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521).

## <a name="documentation"></a>Documentação

Tutoriais e outras informações sobre ASP.NET e Web Tools para Visual Studio 2013.2 estão disponíveis no [site ASP.NET](https://www.asp.net/).

## <a name="software-requirements"></a>Requisitos de software

ASP.NET e Web Tools para Visual Studio 2013.2 requer visual studio 2013.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Novos recursos em ASP.NET e Ferramentas Web para Visual Studio 2013.2

As seções a seguir descrevem os recursos que foram introduzidos na versão.

- [Um ASP.NET modelos de projeto](#oneaspnet)
- [Suporte SSL ao lançar aplicativos web no IIS Express](#ssl)
- [Aprimoramentos do Visual Studio Web Editor](#vswebeditor)
- [Link do navegador](#browserlink)
- [Suporte para aplicativos web do azure App Service no Visual Studio](#waws)
- [Crie recursos remotos do Azure ao criar um novo projeto web](#AzureResources)
- [Aprimoramentos de publicação da Web](#webpublish)
- [andaimes de ASP.NET](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [formulários da Web ASP.NET](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET API web 2.1.2](#webapi)
- [ASP.NET Páginas da Web 3.1.2](#webpages)
- [Quadro de Entidades 6.1](#ef)
- [ASP.NET Identidade 2.0.0](#identity)
- [Componentes Microsoft OWIN](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>Um ASP.NET modelos de projeto

- Atualizações para ASP.NET modelos do Projeto para suportar confirmação de conta e redefinição de senha.
- Atualize ASP.NET modelo de API da Web para suportar a autenticação usando contas organizacionais on premises.
- O modelo de SPA ASP.NET agora contém autenticação baseada em visualizações mvc e lado do servidor. O modelo possui um controlador WebAPI que só pode ser acessado por usuários autenticados.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>Suporte SSL ao lançar aplicativos web no IIS Express

Para eliminar o aviso de segurança ao navegar e depurar HTTPS no localhost, adicionamos um diálogo para permitir que o Internet Explorer e o Chrome confiem no certificado SSL expresso auto-assinado.

Por exemplo, uma propriedade de projeto web pode ser definida para usar SSL. Clique em F4 para trazer a caixa de diálogo de propriedades. Alterar **SSL Ativado** para true. Copie a URL do SSL.

![Propriedade ativada pelo SSL](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

Defina a guia da página da página de propriedade do projeto `https://localhost:44300/` web para usar a URL baseada em HTTPS (a URL SSL será a menos que você tenha criado anteriormente sites da Web SSL.)

![Definir URL do projeto (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Pressione CTRL+F5 para executar o aplicativo. Siga as instruções para confiar no certificado auto-assinado que o IIS Express gerou.

![Aviso SSL](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

Leia a caixa de diálogo **Aviso de segurança** e clique em **Sim** se quiser instalar o certificado representando o host local.

![Aviso de segurança](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

O site será mostrado em IE ou Chrome sem o aviso de certificado no navegador.

![Página HTTPS sem avisos](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

O Firefox usa sua própria loja de certificados, por isso exibirá um aviso.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Aprimoramentos do Visual Studio Web Editor

- **Novo item e editor do projeto JSON**: Adicionamos um item de projeto JSON e editor ao Visual Studio. Os recursos atuais do editor JSON incluem colorização, validação de sintaxe, conclusão da cinta, delineamento, configuração de opções de ferramentas e muito mais.

    ![JSON Editor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    O IntelliSense agora suporta [JSON Schema](http://json-schema.org/) v3 e v4. Há uma caixa de combinação de esquema para escolher esquemas existentes, editar o caminho do esquema local ou simplesmente arrastar um arquivo JSON do projeto para obter o caminho relativo.

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON Schema editor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **Novo editor do Sass (SCSS):** Adicionamos LESS em VS2013 RTM, e agora temos um item e editor de projeto Sass. Os recursos do editor sass são comparáveis ao editor LESS, e incluem colorização, variável e Mixins IntelliSense, comentário/uncomment, informações rápidas, formatação, validação de sintaxe, delineamento, definição de goto, seletor de cores, configuração de opções de ferramentas etc.

    ![Adicionar novo item: folha de estilo SCSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![Editor de folha de estilo](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **Novo Seletor de URL em documentos HTML, Razor, CSS, LESS e Sass:** VS 2013 enviado sem seletor de URL fora das páginas do Web Forms. O novo seletor de URL para editores HTML, Razor, CSS, LESS e Sass é um seletor de digitação fluente e livre de diálogos que entende '.'. e filtra listas de arquivos apropriadamente para tags e links img.

    ![Seletor de URL para tag de imagem](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![Seletor de URL para visualizações](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![Seletor de URL para CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **Atualizações para o editor LESS adicionando mais recursos**
- **Atualização do KnockTellisense :** Adicionamos uma sintaxe KnockOut não padrão para VS intelliSense, "ko-vs-editor viewModel:" sintaxe. Ele pode ser usado para vincular a vários modelos de exibição em uma página usando comentários no formulário:

    ![Nocaute Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    Também adicionamos suporte para o ViewModel IntelliSense aninhado, para que você possa perfurar objetos profundamente aninhados no ViewModel.

    `<div data-bind="text: foo.bar.baz.etc" />`

    O IntelliSense exibido é o IntelliSense completo do Objeto JavaScript.

    ![Intellisense mostrando objeto JavaScript completo](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **Novo Seletor de URL em documentos HTML, Razor, CSS, LESS e Sass**: VS 2013 enviados sem seletor de URL fora das páginas do Web Forms. O novo seletor de URL para editores HTML, Razor, CSS, LESS e Sass é um seletor de digitação fluente e livre de diálogos que entende '.'. e filtra listas de arquivos apropriadamente para tags e links img.

    ![Seletor de URL para tag de imagem](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![Seletor de URL para visualizações](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![Seletor de URL para CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>Link do navegador

- O Browser Link agora suporta conexões HTTPS e lista isso no Dashboard com outras conexões, desde que o certificado seja confiável pelo navegador.
- Mapeamento de origem HTML estático
- Suporte a SPA para mapeamento de dados
- Dados de mapeamento de atualização automática

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Suporte para aplicativos web do azure App Service no Visual Studio

- **Apoie o login do Azure.**
- **Depuração remota e visualização remota para aplicativos web**: Agora suportamos [depuração remota para aplicativos web no Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) e visualização remota de arquivos de conteúdo de aplicativos da Web no explorador do servidor.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>Crie recursos remotos do Azure ao criar um novo projeto web

Adicionamos uma caixa de seleção ["Criar recursos remotos"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) do Azure na nova caixa de diálogo do aplicativo web. Ao escolhê-lo, você poderá integrar a experiência de criar um novo aplicativo web, configurar o site de publicação Azure para testes e criar perfil de publicação em alguns passos simples.

![Novo projeto com recursos do Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Publicando no Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Aprimoramentos de publicação da Web

- Melhore a experiência do usuário para publicação.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>andaimes de ASP.NET

- **Suporte enum:** Se o seu modelo estiver usando Enums, então a pasta MVC Scaffolder gerará dropdown para enum. Isso usa os ajudantes enum em MVC.
- **Suporte bootstrap**: Atualizado o EditorPara modelos em Andaimes MVC para que eles usem as classes Bootstrap.
- **Suporte ao pacote**: MVC e Web API Scaffolders adicionarão pacotes 5.1 para MVC e API Web

As capturas de tela a seguir demonstram modelos de andaimes.

- Código do modelo:

     ![Código do modelo](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- Compile o código do modelo, clique com o botão direito do mouse e **selecione Adicionar**, **Novo Item de Andaime**.

     ![Adicionar novo item andaime](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- Escolha **o Controlador MVC5 com visualizações, usando o Entity Framework**:

     ![Adicionar novo controlador MVC5 com visualizações](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- **Adicionar controlador** usando o modelo:

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- Verifique o código gerado, por exemplo Views/WeekdayModels/Edit.cshtml contém `@Html.EnumDropDownListFor`: ![Exibição contendo EnumDropDownListFor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- Execute a página para ver a caixa de combinação enum gerada, observe que se um valor pode ser nulo, uma seqüência vazia pode ser escolhida para a caixa de combinação. Por exemplo, a página **Criar** mostra o seguinte:

    ![Caixa de combinação permitindo string vazia](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM será lançado em abril de 2014. Aqui estão os pontos mais importantes das notas de lançamento, mas verifique as [notas de lançamento completas](http://docs.nuget.org/docs/release-notes/nuget-2.8) para obter mais informações sobre essas alterações.

- **Direcionar aplicativos windows phone 8.1**: NuGet 2.8.1 agora suporta aplicativos direcionados ao Windows Phone 8.1 usando os apelidos de framework de destino 'WindowsPhoneApp', 'WPA', 'WindowsPhoneApp81' e 'WPA81'.

- **Resolução de patches para dependências**: Ao resolver as dependências do pacote, a NuGet historicamente implementou uma estratégia de selecionar a versão de pacote menor e menor mais baixa que satisfaça as dependências do pacote. Ao contrário da versão principal e menor, no entanto, a versão patch sempre foi resolvida para a versão mais alta. Embora o comportamento tenha sido bem intencionado, criou uma falta de determinismo para a instalação de pacotes com dependências.
- **DependencyVersion Switch**: Embora o NuGet 2.8 altere o comportamento *padrão* para resolver dependências, ele também adiciona controle mais preciso sobre o processo de resolução de dependência através do switch -DependencyVersion no console do gerenciador de pacotes. O switch permite resolver dependências para a versão mais baixa possível (comportamento padrão), a versão mais alta possível ou a versão menor ou patch mais alta. Este switch só funciona para instalar-pacote no comando powershell.
- **Atributo DependencyVersion**: Além do switch -DependencyVersion detalhado acima, o NuGet também permitiu a capacidade de definir um novo atributo no arquivo nuget.config definindo qual é o valor padrão, se o switch -DependencyVersion não for especificado em uma invocação do pacote de instalação. Esse valor também será respeitado pelo NuGet Package Manager Para qualquer operação de pacote de instalação. Para definir esse valor, adicione o atributo abaixo ao seu arquivo nuget.config:

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **Visualizar Operações NuGet com -WhatIf**: Alguns pacotes NuGet podem ter gráficos de dependência profunda e, como tal, podem ser úteis durante uma operação de instalação, desinstalação ou atualização para primeiro ver o que vai acontecer. O NuGet 2.8 adiciona o PowerShell padrão - e se mudar para os comandos install-package, desinstall-package e update-package para permitir visualizar todo o fechamento de pacotes aos quais o comando será aplicado.
- **Pacote downgrade**: Não é incomum instalar uma versão de pré-lançamento de um pacote a fim de investigar novos recursos e, em seguida, decidir reverter para a última versão estável. Antes do NuGet 2.8, este era um processo de várias etapas para desinstalar o pacote de pré-lançamento e suas dependências e, em seguida, instalar a versão anterior. Com o NuGet 2.8, no entanto, o pacote de atualização agora reverterá todo o fechamento do pacote (por exemplo, a árvore de dependência do pacote) para a versão anterior.
- **Dependências de desenvolvimento**: Muitos tipos diferentes de recursos podem ser entregues como pacotes NuGet - incluindo ferramentas que são usadas para otimizar o processo de desenvolvimento. Esses componentes, embora possam ser fundamentais no desenvolvimento de um novo pacote, não devem ser considerados uma dependência do novo pacote quando ele for publicado posteriormente. O NuGet 2.8 permite que um pacote se identifique no arquivo .nuspec como um desenvolvimentoDependency. Quando instalado, esses metadados também serão adicionados ao arquivo packages.config do projeto no qual o pacote foi instalado. Quando esse arquivo packages.config for posteriormente analisado para dependências nuGet durante o pacote nuget.exe, ele excluirá essas dependências marcadas como dependências de desenvolvimento.
- **Pacotes individuais.config Arquivos para diferentes plataformas**: Ao desenvolver aplicativos para várias plataformas de destino, é comum ter arquivos de projeto diferentes para cada um dos respectivos ambientes de compilação. Também é comum consumir diferentes pacotes NuGet em diferentes arquivos de projeto, já que os pacotes têm diferentes níveis de suporte para diferentes plataformas. O NuGet 2.8 oferece suporte aprimorado para este cenário, criando diferentes pacotes.config files para diferentes arquivos de projeto específicos da plataforma.
- **Retorno ao cache local**: Embora os pacotes NuGet sejam normalmente consumidos de uma galeria remota, como a [galeria NuGet](http://www.nuget.org) usando uma conexão de rede, existem muitos cenários em que o cliente não está conectado. Sem uma conexão de rede, o cliente NuGet não foi capaz de instalar pacotes com sucesso - mesmo quando esses pacotes já estavam na máquina do cliente no cache NuGet local. O NuGet 2.8 adiciona o retorno automático do cache ao console de gerenciamento de pacotes.

    O recurso de recuo de cache não requer argumentos de comando específicos. Além disso, o backup de cache atualmente funciona apenas no console do gerenciador de pacotes - o comportamento não funciona atualmente na caixa de diálogo do gerenciador de pacotes.
- **Correções de**erro : Uma das principais correções de bugs feitas foi a melhoria de desempenho no comando update-package -reinstall.

    Além desses recursos e da correção de desempenho acima mencionada, esta versão do NuGet também inclui muitas outras correções de bugs. Houve 181 questões totais abordadas no comunicado. Para obter uma lista completa dos itens de trabalho corrigidos no NuGet 2.8, consulte o [NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) para esta versão.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>Web Forms do ASP.NET

- Os modelos formulários da Web agora mostram como fazer a confirmação da conta e a redefinição de senha para ASP.NET identidade.
- O controle da Fonte de Dados da Entidade e o Provedor Dinâmico de Dados para o Quadro de Entidades 6. Para obter mais detalhes, consulte o seguinte blog do MSDN: [Provedor de dados dinâmicos e controle EntityDataSource para Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx).

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [Melhorias no roteamento de atributos](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [Suporte bootstrap para modelos de editor](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [Suporte enum em visualizações](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [Suporte discreto para atributos MinLength/MaxLength](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [Apoiando o contexto 'isso' no Ajax Discreto](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- Várias [correções de bugs](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET API web 2.1.2

- [Manipulação global de erros](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [Aprimoramentos de roteamento de atributos](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [Melhorias na página de ajuda](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [Suporte ao IgnoreRoute](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [Assunto do tipo de mídia BSON](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [Melhor suporte para filtros de sincronização](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [Análise de análise para a biblioteca de formatação do cliente](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- Várias [correções de bugs](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Páginas da Web 3.1.2

- Várias [correções de bugs](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Quadro de Entidades 6.1

Entity Framework foi atualizado para a versão 6.1 para tempo de execução e ferramentas. Entity Framework (EF) 6.1 é uma pequena atualização para o Entity Framework 6 e inclui uma série de correções de bugs e novos recursos. Para obter informações detalhadas sobre o EF6.1, incluindo links para documentação para os novos recursos, consulte [Entity Framework Version History](https://msdn.microsoft.com/data/jj574253). Os novos recursos desta versão incluem:

- **A consolidação de ferramentas** fornece uma maneira consistente de criar um novo modelo EF. Esse recurso estende o assistente ADO.NET Entity Data Model para suportar a criação de modelos code first, incluindo engenharia reversa a partir de um banco de dados existente. Esses recursos estavam disponíveis anteriormente em qualidade Beta nas Ferramentas de Energia Da EF.
- **O tratamento de falhas de confirmação de transações** fornece o novo [System.Data.Entity.Infrastructure.CommitFailureHandler,](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) que faz uso da capacidade recém-introduzida de interceptar operações de transação. O **CommitFailureHandler** permite a recuperação automática de falhas de conexão enquanto comete uma transação.
- **IndexAttribute** permite que os índices sejam especificados colocando um atributo em uma propriedade (ou propriedades) no modelo Code First. Código Primeiro criará um índice correspondente no banco de dados.
- **A API de mapeamento público** fornece acesso às informações que a EF tem sobre como propriedades e tipos são mapeados para colunas e tabelas no banco de dados. Em versões passadas essa API era interna.
- **Capacidade de configurar interceptadores através do arquivo App/Web.config**(permitindo que interceptadores sejam adicionados sem recompilar o aplicativo).
- **DatabaseLogger** é um novo interceptador que facilita o registro de todas as operações de banco de dados em um arquivo. Em combinação com o recurso anterior, isso permite alternar facilmente o registro de operações de banco de dados para um aplicativo implantado, sem a necessidade de recompilação.
- **A detecção de mudanças de modelos de migrações** foi aprimorada para que as migrações de andaimes sejam mais precisas; o desempenho do processo de detecção de alterações também foi muito aprimorado.
- **Melhorias de desempenho,** incluindo operações reduzidas de banco de dados durante a inicialização, otimizações para comparação de igualdade nula em consultas LINQ, geração de visualização mais rápida (criação de modelos) em mais cenários e materialização mais eficiente de entidades rastreadas com múltiplas associações.

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identidade 2.0.0

- **Autenticação de dois fatores:** ASP.NET Identidade agora suporta autenticação de dois fatores. A autenticação de dois fatores fornece uma camada extra de segurança para suas contas de usuário no caso em que sua senha fica comprometida. Há também proteção para ataques de força bruta contra os dois códigos de fator.
- **Bloqueio da conta:** Fornece uma maneira de bloquear o usuário se o usuário inserir sua senha ou códigos de dois fatores incorretamente. O número de tentativas inválidas e o tempo de bloqueio para os usuários podem ser configurados. Um desenvolvedor pode, opcionalmente, desativar o bloqueio da conta para determinadas contas de usuário, caso precise.
- **Confirmação da conta:** O sistema de identidade ASP.NET agora suporta confirmação de conta. Este é um cenário bastante comum na maioria dos sites de hoje em dia onde, quando você se registra para uma nova conta no site, você é obrigado a confirmar seu e-mail antes de poder fazer qualquer coisa no site. A confirmação de e-mail é útil porque impede que contas falsas sejam criadas. Isso é extremamente útil se você estiver usando o e-mail como um método de comunicação com os usuários do seu site, como sites do Fórum, bancos, comércio eletrônico ou sites sociais.
- **Redefinição de senha:** Redefinição de senha é um recurso onde o usuário pode redefinir suas senhas se tiver esquecido sua senha.
- **Selo de segurança (Sair em todos os lugares):** Suporta uma maneira de regenerar o Token de Segurança para o usuário nos casos em que o Usuário altera sua senha ou qualquer outra informação relacionada à segurança, como a remoção de um login associado (como Facebook, Google, Conta Microsoft e assim por diante). Isso é necessário para garantir que quaisquer tokens gerados com a senha antiga sejam invalidados. No projeto de exemplo, se você alterar a senha do usuário, um novo token será gerado para o usuário e quaisquer tokens anteriores serão invalidados. Esse recurso fornece uma camada extra de segurança ao seu aplicativo, uma vez que quando você alterar sua senha, você estará logado de todos os lugares (todos os outros navegadores) onde você fez login neste aplicativo.
- **Faça com que o tipo de chave primária seja extensível para usuários e funções**: Em ASP.NET identidade 1.0, o tipo de chave principal para usuários e funções da tabela eram strings. Isso significa que quando o sistema ASP.NET Identity foi persistido no SQL Server usando Entity Framework, estávamos usando nvarchar. Houve muitas discussões em torno dessa implementação padrão no Stack Overflow e com base no feedback de entrada. Nós fornecemos um gancho de extensibilidade onde você pode especificar qual deve ser a chave principal da tabela Usuários e Funções. Este gancho de extensibilidade é particularmente útil se você estiver migrando seu aplicativo e o aplicativo estava armazenando UserIds são GUIDs ou ints.
- **Suporte iQueryable em usuários e funções**: Adicionado suporte para IQueryable no UsersStore e RolesStore, você pode facilmente obter a lista de Usuários e Funções.
- **Operação de exclusão de suporte através do UserManager**
- **Indexação no Nome do Usuário**: Na implementação ASP.NET Identity Entity Framework, adicionamos um índice único no Nome de Usuário usando o novo IndexAttribute no EF 6.1.0. Isso garante que os nomes de usuário sejam sempre únicos e que não havia nenhuma condição de raça na qual você poderia acabar com nomes de usuário duplicados.
- **Validador de senha aprimorado:** O validador de senha que foi enviado em ASP.NET Identidade 1.0 era um validador de senha bastante básico que estava apenas validando o comprimento mínimo. Há um novo validador de senha que lhe dá mais controle sobre a complexidade da senha. Por favor, note que mesmo que você ative todas as configurações nesta senha, nós encorajamos você a habilitar a autenticação de dois fatores para as contas de usuário.
- **IdentidadeFábrica De fábrica/ CreatePerOwinContext**:

    - **Gerente de usuário**: Você pode usar a implementação factory para obter uma instância do UserManager a partir do contexto OWIN. Este padrão é semelhante ao que usamos para obter AuthenticationManager do contexto OWIN para SignIn e SignOut. Esta é uma maneira recomendada de obter uma instância do UserManager por solicitação do aplicativo.
    - **DbContextFactory**: ASP.NET Identity usa Entity Framework para persistir o sistema de identidade no SQL Server. Para fazer isso, o Sistema de Identidade tem uma referência ao ApplicationDbContext. O DbContextFactory Middleware retorna uma instância do ApplicationDbContext por solicitação que você pode usar em seu aplicativo.
- **ASP.NET pacote NuGet amostras de identidade**: O pacote Samples NuGet pode facilitar a instalação e a execução de amostras para ASP.NET Identidade e seguir as melhores práticas. Esta é uma amostra ASP.NET aplicação MVC. Por favor, modifique o código para se adequar ao seu aplicativo antes de implantá-lo na produção. A amostra deve ser instalada em uma aplicação ASP.NET vazia. Para obter mais informações sobre o pacote, acesse o seguinte post no blog: [Anunciando rtm de ASP.NET Identidade 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Componentes Microsoft OWIN

Havia muitos bugs que foram corrigidos nesta versão. Consulte as [notas de lançamento da versão 2.1.0](https://katanaproject.codeplex.com/releases/view/113281) para obter informações mais detalhadas.

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

Havia muitos bugs que foram corrigidos nesta versão. Consulte as [notas de lançamento da versão 2.0.2](https://github.com/SignalR/SignalR/releases/tag/2.0.2) para obter informações mais detalhadas.
