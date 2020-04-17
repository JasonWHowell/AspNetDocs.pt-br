---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 Servidor de Autorização | Microsoft Docs
author: hongyes
description: Este tutorial irá guiá-lo sobre como implementar um Servidor de Autorização OAuth 2.0 usando middleware OWIN OAuth. Este é um tutorial avançado que só outlin...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540374"
---
<a name="owin-oauth-20-authorization-server"></a>Servidor de autorização OAuth 2.0 de OWIN
====================
por [Hongye Sun](https://github.com/hongyes) e [Praburaj Thiagarajan](https://github.com/Praburaj)

> Este tutorial irá guiá-lo sobre como implementar um Servidor de Autorização OAuth 2.0 usando middleware OWIN OAuth. Este é um tutorial avançado que apenas descreve as etapas para criar um Servidor de Autorização OWIN OAuth 2.0. Este não é um tutorial passo a passo. [Baixe o código de amostra](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).
>
> > [!NOTE]
> > Este esboço não deve ser usado para criar um aplicativo de produção seguro. Este tutorial destina-se a fornecer apenas um esboço sobre como implementar um Servidor de Autorização OAuth 2.0 usando middleware OWIN OAuth.
>
>
> ## <a name="software-versions"></a>Versões de software
>
> | **Mostrado no tutorial** | **Também trabalha com** |
> | --- | --- |
> | Windows 8.1 | Windows 8, Windows 7 |
> | [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [Visual Studio 2013 Express for Desktop](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). Visual Studio 2012 com a última atualização deve funcionar, mas o tutorial não foi testado com ele, e algumas seleções de menu e caixas de diálogo são diferentes. |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>Perguntas e Comentários
>
> Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [Katana Project no GitHub](https://github.com/aspnet/AspNetKatana/). Para dúvidas e comentários sobre o tutorial em si, consulte a seção de comentários na parte inferior da página.


A [estrutura OAuth 2.0](http://tools.ietf.org/html/rfc6749) permite que um aplicativo de terceiros obtenha acesso limitado a um serviço HTTP. Em vez de usar as credenciais do proprietário do recurso para acessar um recurso protegido, o cliente obtém um token de acesso (que é uma string que denota um escopo específico, vida útil e outros atributos de acesso). Os tokens de acesso são emitidos a clientes terceirizados por um servidor de autorização com a aprovação do proprietário do recurso.

Este tutorial abordará:

- Como criar um servidor de autorização para suportar quatro tipos de concessão de autorização e tokens de atualização:
    - Concessão de código de autorização
    - Concessão Implícita
    - Concessão de credenciais de senha do proprietário de recursos
    - Concessão de Credenciais do Cliente
- Criando um servidor de recursos protegido por um token de acesso.
- Criando clientes OAuth 2.0.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) ou o [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)gratuito, conforme indicado em **Versões de Software** no topo da página.
- Familiaridade com OWIN. Veja [Getting Started com o Projeto Katana](https://msdn.microsoft.com/magazine/dn451439.aspx) e as [novidades da OWIN e katana](index.md).
- Familiaridade com a terminologia [OAuth,](http://tools.ietf.org/html/rfc6749) incluindo [Funções,](http://tools.ietf.org/html/rfc6749#section-1.1) [Fluxo de Protocolo](http://tools.ietf.org/html/rfc6749#section-1.2)e [Concessão de Autorização.](http://tools.ietf.org/html/rfc6749#section-1.3) [A introdução do OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-1) proporciona uma boa introdução.

## <a name="create-an-authorization-server"></a>Criar um servidor de autorização

Neste tutorial, vamos esboçar como usar [o OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) e ASP.NET MVC para criar um servidor de autorização. Esperamos em breve fornecer um download para a amostra completa, já que este tutorial não inclui cada etapa. Primeiro, crie um aplicativo web vazio chamado *AuthorizationServer* e instale os seguintes pacotes:

- Microsoft.AspNet.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security
- Microsoft.Owin.Security.Google (Ou qualquer outro pacote de login social, como Microsoft.Owin.Security.Facebook)

Adicione uma [classe OWIN Startup](owin-startup-class-detection.md) sob a pasta raiz do projeto chamada *Inicialização*.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

Crie uma pasta *Iniciar de aplicativos.\_* Selecione a pasta Iniciar do *aplicativo\_* e use shift+Alt+A para adicionar a versão baixada do arquivo *AuthorizationServer\App\_Start\Startup.Auth.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

O código acima permite o login de aplicativos/externos em cookies e a autenticação do Google, que são usados pelo próprio servidor de autorização para gerenciar contas.

O `UseOAuthAuthorizationServer` método de extensão é configurar o servidor de autorização. As opções de configuração são:

- `AuthorizeEndpointPath`: O caminho de solicitação onde os aplicativos clientes redirecionarão o usuário-agente para obter o consentimento dos usuários para emitir um token ou código. Deve começar com uma barra principal,`/Authorize`por exemplo, ".
- `TokenEndpointPath`: Os aplicativos clientes do caminho de solicitação se comunicam diretamente para obter o token de acesso. Deve começar com uma barra principal, como "/Token". Se o cliente for emitido um [segredo de cliente,\_](http://tools.ietf.org/html/rfc6749#appendix-A.2)ele deve ser fornecido a este ponto final.
- `ApplicationCanDisplayErrors`: Defina para `true` se o aplicativo web quiser gerar uma `/Authorize` página de erro personalizada para os erros de validação do cliente no ponto final. Isso só é necessário para casos em que o navegador não é `client_id` redirecionado de volta para o aplicativo cliente, por exemplo, quando o ou `redirect_uri` está incorreto. O `/Authorize` ponto final deve esperar para ver o "oauth. Erro", "oauth. ErroDescrição", e "oauth. As propriedades errorUri" são adicionadas ao ambiente OWIN.

    > [!NOTE]
    > Se não for verdade, o servidor de autorização retornará uma página de erro padrão com os detalhes do erro.
- `AllowInsecureHttp`: É verdade permitir que solicitações de autorização e token `redirect_uri` cheguem em endereços HTTP URI e permitir que os parâmetros de solicitação de autorização de entrada tenham endereços HTTP URI.

    > [!WARNING]
    > Segurança - Isso é apenas para desenvolvimento.
- `Provider`: O objeto fornecido pelo aplicativo para processar eventos levantados pelo middleware do Servidor de Autorização. O aplicativo pode implementar a interface totalmente, `OAuthAuthorizationServerProvider` ou pode criar uma instância de e atribuir delegados necessários para os fluxos oAuth que este servidor suporta.
- `AuthorizationCodeProvider`: Produz um código de autorização de uso único para retornar ao aplicativo do cliente. Para que o servidor OAuth **MUST** seja seguro, `AuthorizationCodeProvider` o aplicativo deve `OnCreate/OnCreateAsync` fornecer uma instância para onde `OnReceive/OnReceiveAsync`o token produzido pelo evento é considerado válido para apenas uma chamada para .
- `RefreshTokenProvider`: Produz um token de atualização que pode ser usado para produzir um novo token de acesso quando necessário. Se não for fornecido, o servidor de autorização `/Token` não retornará tokens de atualização do ponto final.

## <a name="account-management"></a>Gerenciamento de Conta

OAuth não se importa onde ou como você gerencia as informações da sua conta de usuário. É [ASP.NET Identidade](../../../identity/index.md) que é responsável por isso. Neste tutorial, vamos simplificar o código de gerenciamento da conta e apenas garantir que o usuário possa fazer login usando o middleware de cookies OWIN. Aqui está o código de `AccountController`amostra simplificado para:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`é usado para validar o cliente com sua URL de redirecionamento registrada. `ValidateClientAuthentication`verifica o cabeçalho do esquema básico e o corpo de formulário para obter as credenciais do cliente.

A página de login é mostrada abaixo:

![](owin-oauth-20-authorization-server/_static/image1.png)

Reveja agora a seção de [concessão](http://tools.ietf.org/html/rfc6749#section-4.1) de código de autorização OAuth 2 do IETF.

**O provedor** (na tabela abaixo) é [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx). Provedor, que é `OAuthAuthorizationServerProvider`do tipo, que contém todos os eventos do servidor OAuth.

| Passos de fluxo da seção Autorização Code Grant | O download da amostra executa essas etapas com: |
| --- | --- |
|  |  |
| (A) O cliente inicia o fluxo direcionando o usuário-agente do proprietário do recurso para o ponto final da autorização. O cliente inclui seu identificador de cliente, escopo solicitado, estado local e um URI de redirecionamento para o qual o servidor de autorização enviará o usuário-agente de volta assim que o acesso for concedido (ou negado). | Provider.MatchEndpoint Provider.validateClientRedirectUri Provider.ValidateAuthorizeRequestProvider.AuthorizeEndPoint |
|  |  |
| (B) O servidor de autorização autentica o proprietário do recurso (através do usuário-agente) e estabelece se o proprietário do recurso concede ou nega a solicitação de acesso do cliente. | **Se o usuário conceder acesso&gt; &lt;** Provider.MatchEndpoint Provider.validateClientRedirectUri Provider.ValidateAuthorizeRequestRequestProvider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) Supondo que o proprietário do recurso conceda acesso, o servidor de autorização redireciona o usuário-agente de volta para o cliente usando o URI de redirecionamento fornecido anteriormente (na solicitação ou durante o registro do cliente). ... |  |
|  |  |
| (D) O cliente solicita um token de acesso do ponto final do token do servidor de autorização, incluindo o código de autorização recebido na etapa anterior. Ao fazer a solicitação, o cliente autentica com o servidor de autorização. O cliente inclui o URI de redirecionamento usado para obter o código de autorização para verificação. | Provedor.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |

Uma implementação `AuthorizationCodeProvider.CreateAsync` `ReceiveAsync` amostral para e para controlar a criação e validação do código de autorização é mostrada abaixo.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

O código acima usa um dicionário simultâneo na memória para armazenar o código e o ticket de identidade e restaurar a identidade após receber o código. Em um aplicativo real, ele seria substituído por um armazenamento de dados persistente. O ponto final da autorização é para que o proprietário do recurso conceda acesso ao cliente. Normalmente, ele precisa de uma interface de usuário para permitir que o usuário clique em um botão e confirme a concessão. O middleware OWIN OAuth permite que o código do aplicativo manuseie o ponto final da autorização. Em nosso aplicativo de exemplo, usamos `OAuthController` um controlador MVC chamado para lidar com isso. Aqui está a implementação da amostra:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

A `Authorize` ação primeiro verificará se o usuário fez login no servidor de autorização. Caso assim, o middleware de autenticação desafie o chamador a autenticar usando o cookie "Aplicativo" e redireciona para a página de login. (Veja o código destacado acima.) Se o usuário tiver logado, ele renderizará a exibição Autorizar, conforme mostrado abaixo:

![](owin-oauth-20-authorization-server/_static/image2.png)

Se o botão **Conceder** `Authorize` for selecionado, a ação criará uma nova identidade "Portador" e entrará com ele. Ele acionará o servidor de autorização para gerar um token portador e enviá-lo de volta ao cliente com carga útil JSON.

### <a name="implicit-grant"></a>Concessão Implícita

Consulte a seção [Subvenção Implícita](http://tools.ietf.org/html/rfc6749#section-4.2) OAuth 2 do IETF agora.

 O fluxo [de subvenção implícito](http://tools.ietf.org/html/rfc6749#section-4.2) mostrado na Figura 4 é o fluxo e mapeamento que o middleware OWIN OAuth segue.

| Passos de fluxo da seção Subvenção Implícita | O download da amostra executa essas etapas com: |
| --- | --- |
|  |  |
| (A) O cliente inicia o fluxo direcionando o usuário-agente do proprietário do recurso para o ponto final da autorização. O cliente inclui seu identificador de cliente, escopo solicitado, estado local e um URI de redirecionamento para o qual o servidor de autorização enviará o usuário-agente de volta assim que o acesso for concedido (ou negado). | Provider.MatchEndpoint Provider.validateClientRedirectUri Provider.ValidateAuthorizeRequestProvider.AuthorizeEndPoint |
|  |  |
| (B) O servidor de autorização autentica o proprietário do recurso (através do usuário-agente) e estabelece se o proprietário do recurso concede ou nega a solicitação de acesso do cliente. | **Se o usuário conceder acesso&gt; &lt;** Provider.MatchEndpoint Provider.validateClientRedirectUri Provider.ValidateAuthorizeRequestRequestProvider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) Supondo que o proprietário do recurso conceda acesso, o servidor de autorização redireciona o usuário-agente de volta para o cliente usando o URI de redirecionamento fornecido anteriormente (na solicitação ou durante o registro do cliente). ... |  |
|  |  |
| (D) O cliente solicita um token de acesso do ponto final do token do servidor de autorização, incluindo o código de autorização recebido na etapa anterior. Ao fazer a solicitação, o cliente autentica com o servidor de autorização. O cliente inclui o URI de redirecionamento usado para obter o código de autorização para verificação. |  |

Uma vez que já implementamos o endpoint de autorização (ação)`OAuthController.Authorize` para concessão de código de autorização, ele habilita automaticamente o fluxo implícito também. Nota: `Provider.ValidateClientRedirectUri` é usado para validar o ID do cliente com sua URL de redirecionamento, que protege o fluxo de subvenção implícito do envio do token de acesso a clientes mal-intencionados[(ataque man-in-the-middle).](https://www.owasp.org/index.php/Man-in-the-middle_attack)

### <a name="resource-owner-password-credentials-grant"></a>Concessão de credenciais de senha do proprietário de recursos

Consulte a seção [Desemao](http://tools.ietf.org/html/rfc6749#section-4.3) Centro de Concessão de Credenciais do Proprietário de Recursos OAuth 2.

 O fluxo [de concessão de credenciais de senha do proprietário de recursos](http://tools.ietf.org/html/rfc6749#section-4.3) mostrado na Figura 5 é o fluxo e mapeamento que o middleware OWIN OAuth segue.

| Passos de fluxo da seção de concessão de credenciais de senha do proprietário de recursos | O download da amostra executa essas etapas com: |
| --- | --- |
|  |  |
| (A) O proprietário do recurso fornece ao cliente seu nome de usuário e senha. |  |
|  |  |
| (B) O cliente solicita um token de acesso do ponto final do token do servidor de autorização, incluindo as credenciais recebidas do proprietário do recurso. Ao fazer a solicitação, o cliente autentica com o servidor de autorização. | Provider.MatchEndpoint Provider.ValidateClientClient.ValidateTokenRequestRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (C) O servidor de autorização autentica o cliente e valida as credenciais do proprietário do recurso e, se válido, emite um token de acesso. |  |

Aqui está a `Provider.GrantResourceOwnerCredentials`implementação da amostra para:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> O código acima destina-se a explicar esta seção do tutorial e não deve ser usado em aplicativos seguros ou de produção. Ele não verifica as credenciais dos proprietários de recursos. Ele assume que cada credencial é válida e cria uma nova identidade para ela. A nova identidade será usada para gerar o token de acesso e o token de atualização. Por favor, substitua o código por seu próprio código de gerenciamento de conta segura.


### <a name="client-credentials-grant"></a>Concessão de Credenciais do Cliente

Consulte a seção Subvenção de [Credenciais](http://tools.ietf.org/html/rfc6749#section-4.4) de Cliente OAuth 2 do IETF agora.

 O fluxo [de concessão de credenciais do cliente](http://tools.ietf.org/html/rfc6749#section-4.4) mostrado na Figura 6 é o fluxo e mapeamento que o middleware OWIN OAuth segue.

| Passos de fluxo da seção subvenção de credenciais do cliente | O download da amostra executa essas etapas com: |
| --- | --- |
|  |  |
| (A) O cliente autentica com o servidor de autorização e solicita um token de acesso a partir do ponto final do token. | Provider.MatchEndpoint Provider.ValidateClientClient.ValidateTokenRequestRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (B) O servidor de autorização autentica o cliente e, se válido, emite um token de acesso. |  |

Aqui está a `Provider.GrantClientCredentials`implementação da amostra para:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> O código acima destina-se a explicar esta seção do tutorial e não deve ser usado em aplicativos seguros ou de produção. Por favor, substitua o código por seu próprio código de gerenciamento de clienteseguro.


### <a name="refresh-token"></a>Atualizar Token

Consulte a seção [Token](http://tools.ietf.org/html/rfc6749#section-1.5) de atualização OAuth 2 do IETF agora.

 O fluxo [de token de atualização](http://tools.ietf.org/html/rfc6749#section-1.5) mostrado na Figura 2 é o fluxo e mapeamento que o middleware OWIN OAuth segue.

| Passos de fluxo da seção subvenção de credenciais do cliente | O download da amostra executa essas etapas com: |
| --- | --- |
|  |  |
| (G) O cliente solicita um novo token de acesso autenticando-se com o servidor de autorização e apresentando o token de atualização. Os requisitos de autenticação do cliente são baseados no tipo de cliente e nas políticas do servidor de autorização. | Provedor.MatchEndpoint Provider.ValidateClientAuthenticationRefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsyncRefreshTokenProvider.CreateAsync |
|  |  |
| (H) O servidor de autorização autentica o cliente e valida o token de atualização e, se válido, emite um novo token de acesso (e, opcionalmente, um novo token de atualização). |  |

Aqui está a `Provider.GrantRefreshToken`implementação da amostra para:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>Crie um servidor de recursos protegido pelo Access Token

Crie um projeto de aplicativo web vazio e instale os seguintes pacotes no projeto:

- Microsoft.AspNet.WebApi.Owin
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

Crie uma classe de inicialização e configure autenticação e API da Web. Consulte *AuthorizationServer\ResourceServer\Startup.cs* no download da amostra.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

Consulte *\_AuthorizationServer\ResourceServer\App Start\Startup.Auth.cs* no download da amostra.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

Consulte *\_AuthorizationServer\ResourceServer\App Start\Startup.WebApi.cs* no download da amostra.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`método permite CORS para todos os domínios.
- `UseOAuthBearerAuthentication`o método permite o meio termo de autenticação do token portador OAuth que receberá e validará o token do portador do cabeçalho de autorização na solicitação.
- `Config.SuppressDefaultHostAuthenticaiton`suprime o principal autenticado do host padrão do aplicativo, portanto, todas as solicitações serão anônimas após esta chamada.
- `HostAuthenticationFilter`permite a autenticação apenas para o tipo de autenticação especificado. Neste caso, é o tipo de autenticação do portador.

Para demonstrar a identidade autenticada, criamos um ApiController para produzir as reivindicações do usuário atual.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

Se o servidor de autorização e o servidor de recursos não estiverem no mesmo computador, o middleware OAuth usará as diferentes chaves da máquina para criptografar e descriptografar o token de acesso ao portador. Para compartilhar a mesma chave privada entre ambos `machinekey` os projetos, adicionamos a mesma configuração em ambos os arquivos *web.config.*

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>Criar clientes OAuth 2.0

 Usamos o pacote [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet para simplificar o código do cliente.

### <a name="authorization-code-grant-client"></a>Cliente de concessão de código de autorização

 Este cliente é um aplicativo MVC. Ele acionará um fluxo de concessão de código de autorização para obter o token de acesso do backend. Ele tem uma única página como mostrado abaixo:

![](owin-oauth-20-authorization-server/_static/image3.png)

- O botão **Autorizar** redirecionará o navegador para o servidor de autorização para notificar o proprietário do recurso para conceder acesso a esse cliente.
- O botão **Atualizar** receberá um novo token de acesso e token de atualização usando o token de atualização atual.
- O botão **API de recursos protegidos** de acesso ligará para o servidor de recursos para obter os dados de sinistros do usuário atual e mostrá-los na página.

Aqui está o código `HomeController` amostral do cliente.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`requer SSL por padrão. Uma vez que nossa demonstração está usando HTTP, você precisa adicionar a seguinte configuração no arquivo de configuração:

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> Segurança - Nunca desabilite o SSL em um aplicativo de produção. Suas credenciais de login estão sendo enviadas agora em texto claro através do fio. O código acima é apenas para depuração e exploração de amostras locais.


### <a name="implicit-grant-client"></a>Cliente de Subvenção Implícita

Este cliente está usando JavaScript para:

1. Abra uma nova janela e redirecione para o ponto final autorizado do Servidor de Autorização.
2. Obtenha o token de acesso a partir de fragmentos de URL quando ele redirecionar de volta.

A seguinte imagem mostra esse processo:

![](owin-oauth-20-authorization-server/_static/image4.png)

O cliente deve ter duas páginas: uma para home page e outra para retorno de chamada. Aqui está a amostra de código JavaScript encontrada no arquivo *Index.cshtml:*

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

Aqui está o código de tratamento de retorno de chamada no arquivo *SignIn.cshtml:*

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> Uma prática recomendada é mover o JavaScript para um arquivo externo e não incorporá-lo com a marcação Razor. Para manter esta amostra simples, eles foram combinados.


### <a name="resource-owner-password-credentials-grant-client"></a>Credenciais de senha do proprietário de recursos concedem cliente

Usamos um aplicativo de console para demo este cliente. Eis o código:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>Cliente de concessão de credenciais do cliente

Semelhante ao Concessão de Credenciais de Senha do Proprietário de Recursos, aqui está o código do aplicativo do console:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
