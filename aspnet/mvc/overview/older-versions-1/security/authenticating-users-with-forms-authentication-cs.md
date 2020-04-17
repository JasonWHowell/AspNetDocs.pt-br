---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: Autenticação de usuários com autenticação de formulários (C#) | Microsoft Docs
author: rick-anderson
description: Saiba como usar o atributo [Autorizar] para proteger por senha páginas específicas em seu aplicativo MVC. Você aprende a usar a administração do site também...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: f14f996c0b3a438647b5d181675457735e473354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540968"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>Autenticar usuários com a autenticação de formulários (C#)

pela [Microsoft](https://github.com/microsoft)

> Saiba como usar o atributo [Autorizar] para proteger por senha páginas específicas em seu aplicativo MVC. Você aprende a usar a Ferramenta de Administração de Sites para criar e gerenciar usuários e funções. Você também aprende a configurar onde as informações da conta do usuário e da função são armazenadas.

O objetivo deste tutorial é explicar como você pode usar a autenticação de Formulários para proteger por senha as visualizações em seus aplicativos mvc ASP.NET. Você aprende a usar a Ferramenta de Administração de Sites para criar usuários e funções. Você também aprende como evitar que usuários não autorizados inudigam ações do controlador. Finalmente, você aprende a configurar onde os nomes de usuário e senhas são armazenados.

#### <a name="using-the-web-site-administration-tool"></a>Usando a ferramenta de administração de sites

Antes de fazer qualquer outra coisa, devemos começar criando alguns usuários e funções. A maneira mais fácil de criar novos usuários e funções é aproveitar a Ferramenta de Administração de Sites do Visual Studio 2008. Você pode iniciar esta ferramenta selecionando a opção menu **Projeto, configuração ASP.NET**. Alternativamente, você pode iniciar a Ferramenta de Administração de Sites clicando no ícone (um tanto assustador) do martelo que atinge o mundo que aparece no topo da janela do Solution Explorer (ver Figura 1).

**Figura 1 – Lançamento da Ferramenta de Administração de Sites**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

Dentro da Ferramenta de Administração de Sites da Web, você cria novos usuários e funções selecionando a guia Segurança. Clique no link **Criar usuário** para criar um novo usuário chamado Stephen (ver Figura 2). Forneça ao usuário stephen qualquer senha que você quiser (por exemplo, *secreta).*

**Figura 2 – Criação de um novo usuário**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

Você cria novos papéis, permitindo primeiro funções e definindo um ou mais papéis. Habilite funções clicando no link **Ativar funções.** Em seguida, crie uma função chamada *Administradores* clicando no link **Criar ou Gerenciar funções** (consulte Figura 3).

**Figura 3 – Criação de um novo papel**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

Finalmente, crie um novo usuário chamado Sally e associe Sally à função Administradores clicando no link Criar usuário e selecionando Administradores ao criar Sally (ver Figura 4).

**Figura 4 – Adicionar um usuário a uma função**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

Quando tudo estiver dito e feito, você deve ter dois novos usuários chamados Stephen e Sally. Você também deve ter uma nova função chamada Administradores. Sally é um membro do papel de Administradores e Stephen não.

#### <a name="requiring-authorization"></a>Exigindo autorização

Você pode exigir que um usuário seja autenticado antes que o usuário invoque uma ação do controlador adicionando o atributo [Autorizar] à ação. Você pode aplicar o atributo [Autorizar] a uma ação de controlador individual ou pode aplicar esse atributo a toda uma classe de controlador.

Por exemplo, o controlador na Listagem 1 expõe uma ação chamada CompanySecrets(). Como essa ação é decorada com o atributo [Autorizar], essa ação não pode ser invocada a menos que um usuário seja autenticado.

**Listagem 1 – Controladores\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

Se você invocar a ação CompanySecrets() inserindo a URL /Home/CompanySecrets na barra de endereços do seu navegador e você não for um usuário autenticado, então você será redirecionado automaticamente para a exibição Login (ver Figura 5).

**Figura 5 – A visualização de login**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

Você pode usar a exibição Login para inserir seu nome de usuário e senha. Se você não é um usuário registrado, então você pode clicar no link **de registro** para navegar até a exibição Registrar (ver Figura 6). Você pode usar a exibição Registrar para criar uma nova conta de usuário.

**Figura 6 – A visualização do Registro**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

Depois de fazer login com sucesso, você pode ver a exibição CompanySecrets (ver Figura 7). Por padrão, você continuará a ser conectado até fechar a janela do seu navegador.

**Figura 7 – A visão CompanySecrets**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>Autorizando pelo nome do usuário ou função do usuário

Você pode usar o atributo [Autorizar] para restringir o acesso a uma ação do controlador a um determinado conjunto de usuários ou a um determinado conjunto de funções do usuário. Por exemplo, o controlador home modificado na Listagem 2 contém duas novas ações chamadas StephenSecrets() e AdministratorSecrets().

**Listagem 2 – Controladores\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

Apenas um usuário com o nome de usuário Stephen pode invocar a ação StephenSecrets(). Todos os outros usuários são redirecionados para a exibição Login. A propriedade Usuários aceita uma lista separada de comma de nomes de conta de usuário.

Somente os usuários na função Administradores podem invocar a ação AdministradorSecrets(). Por exemplo, como Sally é membro do grupo Administradores, ela pode invocar a ação AdministradorSecrets(). Todos os outros usuários são redirecionados para a exibição Login. A propriedade Roles aceita uma lista separada de comma de nomes de funções.

#### <a name="configuring-authentication"></a>Configuração de autenticação

Neste ponto, você pode estar se perguntando onde a conta de usuário e as informações da função estão sendo armazenadas. Por padrão, as informações são armazenadas em um banco de dados SQL Express (RANU) chamado\_ASPNETDB.mdf localizado na pasta Dados do aplicativo do aplicativo MVC. Esse banco de dados é gerado pela ASP.NET framework automaticamente quando você começa a usar a adesão.

Para ver o banco de dados ASPNETDB.mdf na janela Solution Explorer, primeiro você precisa selecionar a opção de menu Projeto, Mostrar todos os arquivos.

Usar o banco de dados SQL Express padrão é bom ao desenvolver um aplicativo. Provavelmente, no entanto, você não vai querer usar o banco de dados ASPNETDB.mdf padrão para um aplicativo de produção. Nesse caso, você pode alterar onde as informações da conta de usuário são armazenadas completando as duas etapas seguintes:

1. Adicione os objetos de banco de dados do Application Services ao seu banco de dados de produção - Altere sua seqüência de conexões de aplicativos para apontar para o banco de dados de produção

O primeiro passo é adicionar todos os objetos de banco de dados necessários (tabelas e procedimentos armazenados) ao seu banco de dados de produção. A maneira mais fácil de adicionar esses objetos a um novo banco de dados é aproveitar o ASP.NET Assistente de Configuração do Servidor SQL (ver Figura 8). Você pode iniciar esta ferramenta abrindo o Prompt de Comando Visual Studio 2008 do grupo de programas Microsoft Visual Studio 2008 e executando o seguinte comando a partir do prompt de comando:

aspnet\_regsql

**Figura 8 – O assistente de configuração do servidor SQL ASP.NET**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

O ASP.NET SQL Server Setup Wizard permite selecionar um banco de dados SQL Server em sua rede e instalar todos os objetos de banco de dados exigidos pelos serviços de aplicativo ASP.NET. O servidor de banco de dados não é necessário para ser localizado em sua máquina local.

> [!NOTE] 
> 
> Se você não quiser usar o ASP.NET Assistente de configuração do servidor SQL, então você poderá encontrar scripts SQL para adicionar os objetos do banco de dados de serviços de aplicativos na seguinte pasta:
> 
> > C:\Windows\Microsoft.NET\Framework\v2.0.50727

Depois de criar os objetos de banco de dados necessários, você precisa modificar a conexão de banco de dados usada pelo aplicativo MVC. Modifique a seqüência de conexão ApplicationServices no seu arquivo de configuração web (web.config) para que ele aponte para o banco de dados de produção. Por exemplo, a conexão modificada na Listagem 3 pontos para um banco de dados chamado MyProductionDB (a seqüência de conexão ApplicationServices original foi comentada).

**Listagem 3 – Web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>Configuração de permissões de banco de dados

Se você usar o Integrated Security para se conectar ao seu banco de dados, então você precisará adicionar a conta de usuário correta do Windows como um login ao seu banco de dados. A conta correta depende se você está usando o ASP.NET Development Server ou os Serviços de Informações da Internet como seu servidor web. A conta de usuário correta também depende do seu sistema operacional.

Se você estiver usando o ASP.NET Development Server (o servidor web padrão usado pelo Visual Studio) então seu aplicativo será executado dentro do contexto da sua conta de usuário do Windows. Nesse caso, você precisa adicionar sua conta de usuário do Windows como um login de servidor de banco de dados.

Alternativamente, se você estiver usando serviços de informações da Internet, você precisa adicionar a conta ASPNET ou a conta NT AUTHORITY/NETWORK SERVICE como um login de servidor de banco de dados. Se você estiver usando o Windows XP, adicione a conta ASPNET como um login ao seu banco de dados. Se você estiver usando um sistema operacional mais recente, como o Windows Vista ou o Windows Server 2008, adicione a conta NT AUTHORITY/NETWORK SERVICE como login de banco de dados.

Você pode adicionar uma nova conta de usuário ao seu banco de dados usando o Microsoft SQL Server Management Studio (ver Figura 9).

**Figura 9 – Criação de um novo login do Microsoft SQL Server**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

Depois de criar o login necessário, você precisa mapear o login para um usuário de banco de dados com as funções de banco de dados certas. Clique duas vezes no login e selecione a guia Mapeamento do usuário. Selecione uma ou mais funções de banco de dados de serviços de aplicativos. Por exemplo, para autenticar usuários, você precisa ativar\_a\_função de banco de dados Aspnet Membership BasicAccess. Para criar novos usuários, você precisa ativar\_a\_função de banco de dados Aspnet Membership FullAccess (ver Figura 10).

**Figura 10 – Adicionar funções de banco de dados de serviços de aplicativos**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>Resumo

Neste tutorial, você aprendeu a usar a autenticação de Formulários ao construir um aplicativo mvc ASP.NET. Primeiro, você aprendeu a criar novos usuários e funções aproveitando a Ferramenta de Administração de Sites. Em seguida, você aprendeu como usar o atributo [Autorizar] para evitar que usuários não autorizados invocassem ações do controlador. Finalmente, você aprendeu como configurar seu aplicativo MVC para armazenar informações de usuário e função em um banco de dados de produção.

> [!div class="step-by-step"]
> [Avançar](authenticating-users-with-windows-authentication-cs.md)
