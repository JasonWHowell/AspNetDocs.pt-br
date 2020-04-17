---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: Autenticação de usuários com autenticação do Windows (C#) | Microsoft Docs
author: rick-anderson
description: Aprenda a usar a autenticação do Windows no contexto de um aplicativo MVC. Você aprende como ativar a autenticação do Windows na web co...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: fb6ba3d52d7c70d61c6aa16b4ada67cc6bdd4f96
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540734"
---
# <a name="authenticating-users-with-windows-authentication-c"></a>Autenticar usuários com a autenticação do Windows (C#)

pela [Microsoft](https://github.com/microsoft)

> Aprenda a usar a autenticação do Windows no contexto de um aplicativo MVC. Você aprende como ativar a autenticação do Windows no arquivo de configuração web do seu aplicativo e como configurar a autenticação com o IIS. Finalmente, você aprende a usar o atributo [Autorizar] para restringir o acesso a ações de controlador a determinados usuários ou grupos do Windows.

O objetivo deste tutorial é explicar como você pode aproveitar os recursos de segurança incorporados nos Serviços de Informação da Internet para proteger por senha as visualizações em seus aplicativos MVC. Você aprende como permitir que as ações do controlador sejam invocadas apenas por usuários ou usuários específicos do Windows que são membros de determinados grupos do Windows.

Usar a autenticação do Windows faz sentido quando você está construindo um site interno da empresa (um site de intranet) e você quer que seus usuários possam usar seus nomes de usuário e senhas padrão do Windows ao acessar o site. Se você estiver construindo um site voltado para fora (um site da Internet) considere usar a autenticação forms em vez disso.

#### <a name="enabling-windows-authentication"></a>Habilitando a autenticação do Windows

Quando você cria um novo aplicativo ASP.NET MVC, a autenticação do Windows não é ativada por padrão. Autenticação de formulários é o tipo de autenticação padrão habilitado para aplicativos MVC. Você deve habilitar a autenticação do Windows modificando a configuração web do aplicativo MVC (web.config). Encontre &lt;a&gt; seção de autenticação e modifique-a para usar o Windows em vez da autenticação de Formulários como esta:

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

Quando você habilita a autenticação do Windows, seu servidor web torna-se responsável pela autenticação dos usuários. Normalmente, existem dois tipos diferentes de servidores web que você usa ao criar e implantar um aplicativo MVC ASP.NET.

Primeiro, ao desenvolver um aplicativo MVC, você usa o ASP.NET Development Web Server incluído no Visual Studio. Por padrão, o ASP.NET Development Web Server executa todas as páginas no contexto da conta atual do Windows (qualquer conta que você usou para fazer login no Windows).

O ASP.NET Development Web Server também suporta autenticação NTLM. Você pode habilitar a autenticação NTLM clicando com o botão direito do mouse sobre o nome do seu projeto na janela Solution Explorer e selecionando Propriedades. Em seguida, selecione a guia Web e verifique a caixa de seleção NTLM (consulte Figura 1).

**Figura 1 – Habilitando a autenticação NTLM para o servidor Web de desenvolvimento de ASP.NET**

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

Para um aplicativo web de produção, por outro lado, você usa o IIS como seu servidor web. O IIS suporta vários tipos de autenticação, incluindo:

- Autenticação Básica – Definida como parte do protocolo HTTP 1.0. Envia nomes de usuário e senhas em texto claro (Base64 codificado) pela Internet. - Autenticação Digest – Envia um hash de uma senha, em vez da própria senha, através da internet. - Autenticação integrada do Windows (NTLM) – O melhor tipo de autenticação para usar em ambientes de intranet usando janelas. - Autenticação de certificados – Permite a autenticação usando um certificado do lado do cliente. O certificado é mapeado para uma conta de usuário do Windows.

> [!NOTE] 
> 
> Para obter uma visão geral mais detalhada desses [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)diferentes tipos de autenticação, consulte .

Você pode usar o Gerenciador de Serviços de Informações da Internet para habilitar um determinado tipo de autenticação. Esteja ciente de que todos os tipos de autenticação não estão disponíveis no caso de todos os sistemas operacionais. Além disso, se você estiver usando o IIS 7.0 com o Windows Vista, você precisará habilitar os diferentes tipos de autenticação do Windows antes que eles apareçam no Gerenciador de Serviços de Informações da Internet. **Painel de controle aberto, programas, programas e recursos, ativar ou desativar os recursos do Windows**e expandir o nó serviços de informação da Internet (ver Figura 2).

**Figura 2 – Habilitando os recursos do Windows IIS**

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

Usando os Serviços de Informação da Internet, você pode ativar ou desativar diferentes tipos de autenticação. Por exemplo, a Figura 3 ilustra desabilitando a autenticação anônima e ativando a autenticação NTLM Integrada do Windows (Ao usar o IIS 7.0).

**Figura 3 – Habilitando a autenticação integrada do Windows**

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Autorizando usuários e grupos do Windows

Depois de habilitar a autenticação do Windows, você pode usar o atributo [Autorizar] para controlar o acesso a controladores ou ações do controlador. Este atributo pode ser aplicado a um controlador MVC inteiro ou a uma ação específica do controlador.

Por exemplo, o controlador Home na Listagem 1 expõe três ações denominadas Index(), CompanySecrets() e StephenSecrets(). Qualquer um pode invocar a ação Index(). No entanto, apenas membros do grupo de gerentes locais do Windows podem invocar a ação CompanySecrets(). Finalmente, apenas o usuário de domínio do Windows chamado Stephen (no domínio de Redmond) pode invocar a ação StephenSecrets().

**Listagem 1 – Controladores\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> Devido ao Controle de Conta de Usuário do Windows (UAC), ao trabalhar com o Windows Vista ou o Windows Server 2008, o grupo de administradores locais se comportará de forma diferente de outros grupos. O atributo [Autorizar] não reconhecerá corretamente um membro do grupo administradores locais, a menos que você modifique as configurações de UAC do seu computador.

Exatamente o que acontece quando você tenta invocar uma ação do controlador sem ser as permissões certas depende do tipo de autenticação habilitada. Por padrão, ao usar o ASP.NET Development Server, basta obter uma página em branco. A página é servida com um Status de Resposta HTTP **não autorizado 401.**

Se, por outro lado, você estiver usando o IIS com autenticação anônima desativada e a autenticação básica ativada, então você continuará recebendo um prompt de diálogo de login cada vez que você solicitar a página protegida (consulte Figura 4).

**Figura 4 – Diálogo de login de autenticação básica**

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a>Resumo

Este tutorial explicou como você pode usar a autenticação do Windows no contexto de um aplicativo MVC ASP.NET. Você aprendeu como ativar a autenticação do Windows no arquivo de configuração web do seu aplicativo e como configurar a autenticação com o IIS. Finalmente, você aprendeu como usar o atributo [Autorizar] para restringir o acesso a ações de controlador a determinados usuários ou grupos do Windows.

> [!div class="step-by-step"]
> [Próximo](authenticating-users-with-forms-authentication-cs.md)
> [anterior](preventing-javascript-injection-attacks-cs.md)
