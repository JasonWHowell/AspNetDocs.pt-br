---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: Autenticação e Autorização em ASP.NET API web | Microsoft Docs
author: MikeWasson
description: Dá uma visão geral da autenticação e da autorização em ASP.NET API da Web.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676254"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>Autenticação e autorização no ASP.NET Web API

por [Mike Wasson](https://github.com/MikeWasson)

Você criou uma API web, mas agora quer controlar o acesso a ela. Nesta série de artigos, veremos algumas opções para proteger uma API web de usuários não autorizados. Esta série cobrirá tanto a autenticação quanto a autorização.

- *Autenticação* é saber a identidade do usuário. Por exemplo, Alice faz login com seu nome de usuário e senha, e o servidor usa a senha para autenticar Alice.
- *A autorização* é decidir se um usuário pode realizar uma ação. Por exemplo, Alice tem permissão para obter um recurso, mas não criar um recurso.

O primeiro artigo da série dá uma visão geral da autenticação e da autorização em ASP.NET API da Web. Outros tópicos descrevem cenários comuns de autenticação para API web.

> [!NOTE]
> Graças às pessoas que revisaram esta série e forneceram feedback valioso: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.

## <a name="authentication"></a>Autenticação

A API da Web pressupõe que a autenticação acontece no host. Para hospedagem na Web, o host é o IIS, que usa módulos HTTP para autenticação. Você pode configurar seu projeto para usar qualquer um dos módulos de autenticação incorporados ao IIS ou ASP.NET, ou escrever seu próprio módulo HTTP para executar a autenticação personalizada.

Quando o host autentica o usuário, ele cria um *principal*, que é um objeto [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) que representa o contexto de segurança sob o qual o código está sendo executado. O host conecta o principal ao segmento atual definindo **Thread.CurrentPrincipal**. O principal contém um objeto **de identidade** associado que contém informações sobre o usuário. Se o usuário for autenticado, a propriedade **Identity.IsAuthenticated** será **verdadeira**. Para solicitações anônimas, **o IsAuthenticated** retorna **falso**. Para obter mais informações sobre os diretores, consulte [Segurança baseada em papéis](https://msdn.microsoft.com/library/shz8h065.aspx).

### <a name="http-message-handlers-for-authentication"></a>Manipuladores de mensagens HTTP para autenticação

Em vez de usar o host para autenticação, você pode colocar a lógica de autenticação em um [manipulador de mensagens HTTP](../advanced/http-message-handlers.md). Nesse caso, o manipulador de mensagens examina a solicitação HTTP e define o principal.

Quando você deve usar manipuladores de mensagens para autenticação? Aqui estão algumas trocas:

- Um módulo HTTP vê todas as solicitações que passam pelo ASP.NET pipeline. Um manipulador de mensagens só vê solicitações que são roteadas para a API da Web.
- Você pode definir manipuladores de mensagens por rota, o que permite aplicar um esquema de autenticação a uma rota específica.
- Os módulos HTTP são específicos do IIS. Os manipuladores de mensagens são agnósticos de host, para que possam ser usados tanto com hospedagem na Web quanto com auto-hospedagem.
- Os módulos HTTP participam do registro, auditoria do IIS e assim por diante.
- Módulos HTTP executados mais cedo no pipeline. Se você lidar com a autenticação em um manipulador de mensagens, o principal não será definido até que o manipulador seja executado. Além disso, o principal volta para o principal anterior quando a resposta deixa o manipulador de mensagens.

Geralmente, se você não precisa suportar auto-hospedagem, um módulo HTTP é uma opção melhor. Se você precisar apoiar a auto-hospedagem, considere um manipulador de mensagens.

### <a name="setting-the-principal"></a>Definindo o Principal

Se o aplicativo executa qualquer lógica de autenticação personalizada, você deve definir o principal em dois lugares:

- **Thread.CurrentPrincipal**. Esta propriedade é a maneira padrão de definir o principal do segmento em .NET.
- **Httpcontext.current.user**. Esta propriedade é específica para ASP.NET.

O código a seguir mostra como definir o principal:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Para hospedagem na Web, você deve definir o principal em ambos os lugares; caso contrário, o contexto de segurança pode se tornar inconsistente. Para auto-hospedagem, no entanto, **httpContext.Current** é nulo. Para garantir que seu código seja agnóstico de host, portanto, verifique se há nulo antes de atribuir ao **HttpContext.Current**, como mostrado.

## <a name="authorization"></a>Autorização

A autorização acontece mais tarde no oleoduto, mais perto do controlador. Isso permite que você faça escolhas mais granulares quando você concede acesso aos recursos.

- *Os filtros de autorização* são executados antes da ação do controlador. Se a solicitação não for autorizada, o filtro retorna uma resposta de erro e a ação não é invocada.
- Dentro de uma ação de controlador, você pode obter o principal atual da propriedade **ApiController.User.** Por exemplo, você pode filtrar uma lista de recursos com base no nome do usuário, devolvendo apenas os recursos que pertencem a esse usuário.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>Usando o atributo [Autorizar]

A API da Web fornece um filtro de autorização incorporado, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx). Este filtro verifica se o usuário está autenticado. Caso assim, ele retorna o código de status HTTP 401 (Não Autorizado), sem invocar a ação.

Você pode aplicar o filtro globalmente, no nível do controlador ou no nível de ações individuais.

**Globalmente**: Para restringir o acesso a cada controlador de API da Web, adicione o filtro **AuthorizeAttribute** à lista global de filtros:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**Controlador**: Para restringir o acesso a um controlador específico, adicione o filtro como um atributo ao controlador:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**Ação**: Para restringir o acesso a ações específicas, adicione o atributo ao método de ação:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

Alternativamente, você pode restringir o controlador e, em seguida, permitir acesso anônimo a ações específicas, usando o atributo. `[AllowAnonymous]` No exemplo a `Post` seguir, o método `Get` é restrito, mas o método permite acesso anônimo.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

Nos exemplos anteriores, o filtro permite que qualquer usuário autenticado acesse os métodos restritos; apenas usuários anônimos são mantidos fora. Você também pode limitar o acesso a usuários específicos ou a usuários em funções específicas:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> O filtro **AuthorizeAttribute** para controladores de API da Web está localizado no **namespace System.Web.Http.** Há um filtro semelhante para controladores MVC no **namespace System.Web.Mvc,** que não é compatível com controladores de API web.

### <a name="custom-authorization-filters"></a>Filtros de autorização personalizados

Para escrever um filtro de autorização personalizado, deriva de um desses tipos:

- **AutorizaçãoAtributo**. Estender essa classe para executar a lógica de autorização com base nas funções atuais do usuário e do usuário.
- **AutorizaçãoFilterAttribute**. Amplie essa classe para executar uma lógica de autorização síncrona que não seja necessariamente baseada no usuário ou função atual.
- **IAuthorizationFilter**. Implementar esta interface para executar a lógica de autorização assíncrona; por exemplo, se sua lógica de autorização fizer chamadas assíncronas de I/O ou rede. (Se sua lógica de autorização estiver vinculada à CPU, é mais simples derivar do **AuthorizationFilterAttribute,** porque então você não precisa escrever um método assíncrono.)

O diagrama a seguir mostra a hierarquia de classe para a classe **AuthorizeAttribute.**

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>Autorização dentro de uma ação do controlador

Em alguns casos, você pode permitir que um pedido prossiga, mas mude o comportamento com base no principal. Por exemplo, as informações que você retorna podem mudar dependendo da função do usuário. Dentro de um método controlador, você pode obter o principal atual da propriedade **ApiController.User.**

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
