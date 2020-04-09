---
uid: signalr/overview/security/introduction-to-security
title: Introdução à Segurança SignalR | Microsoft Docs
author: bradygaster
description: Descreve os problemas de segurança que você deve considerar ao desenvolver um aplicativo SignalR.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676191"
---
# <a name="introduction-to-signalr-security"></a>Introdução à segurança do SignalR

por [Patrick Fletcher](https://github.com/pfletcher), Tom [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este artigo descreve os problemas de segurança que você deve considerar ao desenvolver um aplicativo SignalR.
>
> ## <a name="software-versions-used-in-this-topic"></a>Versões de software usadas neste tópico
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR versão 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Versões anteriores deste tópico
>
> Para obter informações sobre versões anteriores do SignalR, consulte [SignalR Older Versions](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Perguntas e comentários
>
> Por favor, deixe comentários sobre como você gostou deste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página. Se você tiver perguntas que não estão diretamente relacionadas ao tutorial, você pode postá-las no [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Visão geral

Este documento contém as seguintes seções:

- [Conceitos de segurança do sinalizador](#concepts)

    - [Autenticação e autorização](#authentication)
    - [Token de conexão](#connectiontoken)
    - [Grupos de reintegração ao reconectar](#rejoingroup)
- [Como o SignalR impede a falsificação de solicitações entre sites](#csrf)
- [Recomendações de segurança signalR](#recommendations)

    - [Protocolo SSL (Secure Socket Layers, camadas de soquete seguro)](#ssl)
    - [Não use grupos como mecanismo de segurança](#groupsecurity)
    - [Manipulação segura de entradas de clientes](#input)
    - [Conciliar uma mudança no status do usuário com uma conexão ativa](#reconcile)
    - [Arquivos proxy JavaScript gerados automaticamente](#autogen)
    - [Exceções](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>Conceitos de segurança do sinalizador

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>Autenticação e autorização

O SignalR não fornece recursos para autenticar usuários. Em vez disso, você integra os recursos signalR na estrutura de autenticação existente para um aplicativo. Você autentica os usuários como normalmente faria em seu aplicativo e trabalha com os resultados da autenticação em seu código SignalR. Por exemplo, você pode autenticar seus usuários com ASP.NET autenticação de formulários e, em seguida, em seu hub, impor quais usuários ou funções estão autorizados a chamar um método. Em seu hub, você também pode passar informações de autenticação, como nome de usuário ou se um usuário pertence a uma função, ao cliente.

SignalR fornece o atributo [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) para especificar quais usuários têm acesso a um hub ou método. Você aplica o atributo Authorize a um hub ou métodos específicos em um hub. Sem o atributo Authorize, todos os métodos públicos no hub estão disponíveis para um cliente que está conectado ao hub. Para obter mais informações sobre hubs, consulte [Autenticação e Autorização para Hubs SignalR](hub-authorization.md).

Você aplica `Authorize` o atributo em hubs, mas não em conexões persistentes. Para aplicar as regras `PersistentConnection` de autorização `AuthorizeRequest` ao usar um, você deve substituir o método. Para obter mais informações sobre conexões persistentes, consulte [Autenticação e Autorização para Conexões Persistentes SignalR](persistent-connection-authorization.md).

<a id="connectiontoken"></a>

### <a name="connection-token"></a>Token de conexão

SignalR mitiga o risco de execução de comandos maliciosos validando a identidade do remetente. Para cada solicitação, o cliente e o servidor passam um token de conexão que contém o id de conexão e o nome de usuário para usuários autenticados. O id de conexão identifica exclusivamente cada cliente conectado. O servidor gera aleatoriamente o id de conexão quando uma nova conexão é criada, e persiste que o id durante a duração da conexão. O mecanismo de autenticação do aplicativo web fornece o nome de usuário. SignalR usa criptografia e uma assinatura digital para proteger o token de conexão.

![](introduction-to-security/_static/image2.png)

Para cada solicitação, o servidor valida o conteúdo do token para garantir que a solicitação esteja vindo do usuário especificado. O nome de usuário deve corresponder ao id de conexão. Ao validar tanto o id de conexão quanto o nome de usuário, o SignalR impede que um usuário mal-intencionado se faça facilmente se passar por outro usuário. Se o servidor não puder validar o token de conexão, a solicitação falhará.

![](introduction-to-security/_static/image4.png)

Como o id de conexão faz parte do processo de verificação, você não deve revelar a id de conexão de um usuário para outros usuários ou armazenar o valor no cliente, como em um cookie.

#### <a name="connection-tokens-vs-other-token-types"></a>Tokens de conexão vs. outros tipos de tokens

Os tokens de conexão são ocasionalmente sinalizados por ferramentas de segurança porque parecem ser tokens de sessão ou tokens de autenticação, o que representa um risco se exposto.

O token de conexão do SignalR não é um token de autenticação. É usado para confirmar que o usuário que faz essa solicitação é o mesmo que criou a conexão. O token de conexão é necessário porque ASP.NET SignalR permite que as conexões se movam entre servidores. O token associa a conexão com um usuário em particular, mas não afirma a identidade do usuário que faz a solicitação. Para que uma solicitação signalR seja devidamente autenticada, ele deve ter algum outro token que afirme a identidade do usuário, como um cookie ou um token portador. No entanto, o token de conexão em si não faz nenhuma alegação de que a solicitação foi feita por esse usuário, apenas que o ID de conexão contido no token está associado a esse usuário.

Como o token de conexão não fornece nenhuma reivindicação de autenticação própria, ele não é considerado um token de "sessão" ou "autenticação". Pegar o token de conexão de um determinado usuário e reanimá-lo em uma solicitação autenticada como um usuário diferente (ou uma solicitação não autenticada) falhará, porque a identidade do usuário da solicitação e a identidade armazenada no token não corresponderão.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>Grupos de reintegração ao reconectar

Por padrão, o aplicativo SignalR reatribuirá automaticamente um usuário aos grupos apropriados ao se reconectar de uma interrupção temporária, como quando uma conexão é descartada e restabelecida antes do tempo de conexão ser eliminado. Ao se reconectar, o cliente passa um token de grupo que inclui o id de conexão e os grupos atribuídos. O token do grupo é assinado digitalmente e criptografado. O cliente retém o mesmo id de conexão após uma reconexão; portanto, o id de conexão passado do cliente reconectado deve corresponder ao id de conexão anterior usado pelo cliente. Essa verificação impede que um usuário mal-intencionado passe solicitações para se juntar a grupos não autorizados ao se reconectar.

No entanto, é importante notar que o token de grupo não expira. Se um usuário pertencia a um grupo no passado, mas foi banido desse grupo, esse usuário pode ser capaz de imitar um token de grupo que inclui o grupo proibido. Se você precisar gerenciar com segurança quais usuários pertencem a quais grupos, você precisa armazenar esses dados no servidor, como em um banco de dados. Em seguida, adicione lógica ao seu aplicativo que verifica no servidor se um usuário pertence a um grupo. Para um exemplo de verificação de membros de grupo, consulte [Trabalhando com grupos](../guide-to-the-api/working-with-groups.md).

Os grupos de reintegração automática só se aplicam quando uma conexão é reconectada após uma interrupção temporária. Se um usuário se desconectar navegando para longe do aplicativo ou o aplicativo for reiniciado, seu aplicativo deve lidar com a forma de adicionar esse usuário aos grupos corretos. Para obter mais informações, consulte [Trabalhando com grupos](../guide-to-the-api/working-with-groups.md).

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>Como o SignalR impede a falsificação de solicitações entre sites

CSRF (Cross-Site Request Forgery) é um ataque no qual um site malicioso envia uma solicitação para um site vulnerável onde o usuário está atualmente conectado. O SignalR previne o CSRF, tornando extremamente improvável que um site mal-intencionado crie uma solicitação válida para o seu aplicativo SignalR.

### <a name="description-of-csrf-attack"></a>Descrição do ataque csrf

Aqui está um exemplo de um ataque CSRF:

1. Um usuário faz login em www.example.com, usando a autenticação de formulários.
2. O servidor autentica o usuário. A resposta do servidor inclui um cookie de autenticação.
3. Sem fazer logout, o usuário visita um site malicioso. Este site malicioso contém o seguinte formulário HTML:

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   Observe que o formulário de ação é posto no site vulnerável, não no site malicioso. Esta é a parte "cross-site" do CSRF.
4. O usuário clica no botão enviar. O navegador inclui o cookie de autenticação com a solicitação.
5. A solicitação é executada no servidor example.com com o contexto de autenticação do usuário, e pode fazer qualquer coisa que um usuário autenticado possa fazer.

Embora este exemplo exija que o usuário clique no botão de formulário, a página maliciosa poderia facilmente executar um script que envia uma solicitação AJAX para o seu aplicativo SignalR. Além disso, o uso do SSL não impede um ataque de CSRF, pois o site malicioso pode enviar uma solicitação "https://".

Normalmente, os ataques de CSRF são possíveis contra sites que usam cookies para autenticação, porque os navegadores enviam todos os cookies relevantes para o site de destino. No entanto, os ataques de CSRF não se limitam a explorar cookies. Por exemplo, a autenticação Básica e Digest também são vulneráveis. Depois que um usuário faz login com autenticação Básica ou Digest, o navegador envia automaticamente as credenciais até que a sessão termine.

### <a name="csrf-mitigations-taken-by-signalr"></a>Atenuações de CSRF tomadas pelo SignalR

O SignalR toma as seguintes etapas para evitar que um site mal-intencionado crie solicitações válidas para o seu aplicativo. SignalR toma essas etapas por padrão, você não precisa tomar nenhuma ação em seu código.

- **Desativar solicitações de domínio cruzado** O SignalR desativa solicitações de domínio cruzado para impedir que os usuários chamem um ponto final signalR de um domínio externo. O SignalR considera inválida qualquer solicitação de um domínio externo e bloqueia a solicitação. Recomendamos que você mantenha esse comportamento padrão; caso contrário, um site malicioso poderia enganar os usuários para enviar comandos para o seu site. Se você precisar usar solicitações de domínio cruzado, consulte [Como estabelecer uma conexão entre domínios](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .
- **Passe o token de conexão na seqüência de consulta, não no cookie** SignalR passa o token de conexão como um valor de seqüência de consulta, em vez de como um cookie. Armazenar o token de conexão em um cookie é inseguro porque o navegador pode encaminhar inadvertidamente o token de conexão quando o código malicioso é encontrado. Além disso, passar o token de conexão na seqüência de consultas impede que o token de conexão persista além da conexão atual. Portanto, um usuário mal-intencionado não pode fazer uma solicitação sob as credenciais de autenticação de outro usuário.
- **Verificar token de conexão** Conforme descrito na seção [Detonar conexão,](#connectiontoken) o servidor sabe qual id de conexão está associado a cada usuário autenticado. O servidor não processa nenhuma solicitação de um id de conexão que não corresponda ao nome do usuário. É improvável que um usuário mal-intencionado possa adivinhar uma solicitação válida porque o usuário mal-intencionado teria que saber o nome do usuário e o id de conexão gerado aleatoriamente atual. Esse id de conexão torna-se inválido assim que a conexão é encerrada. Usuários anônimos não devem ter acesso a informações confidenciais.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>Recomendações de segurança signalR

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>Protocolo SSL (Secure Socket Layers, camadas de soquete seguro)

O protocolo SSL usa criptografia para garantir o transporte de dados entre um cliente e um servidor. Se o aplicativo SignalR transmitir informações confidenciais entre o cliente e o servidor, use O SSL para o transporte. Para obter mais informações sobre como configurar o SSL, consulte [Como configurar o SSL no IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>Não use grupos como mecanismo de segurança

Os grupos são uma maneira conveniente de coletar usuários relacionados, mas não são um mecanismo seguro para limitar o acesso a informações confidenciais. Isso é especialmente verdade quando os usuários podem se reunir automaticamente em grupos durante uma reconexão. Em vez disso, considere adicionar usuários privilegiados a uma função e limitar o acesso a um método de hub apenas para membros dessa função. Para um exemplo de restringir o acesso com base em uma função, consulte [Autenticação e Autorização para Hubs SignalR](hub-authorization.md). Para um exemplo de verificar o acesso do usuário a grupos ao se reconectar, consulte [Trabalhando com grupos](../guide-to-the-api/working-with-groups.md).

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>Manipulação segura de entradas de clientes

Para garantir que um usuário mal-intencionado não envie script para outros usuários, você deve codificar todas as entradas de clientes que se destinam a transmitir para outros clientes. Você deve codificar mensagens nos clientes receptores em vez do servidor, porque seu aplicativo SignalR pode ter muitos tipos diferentes de clientes. Portanto, a codificação HTML funciona para um cliente web, mas não para outros tipos de clientes. Por exemplo, um método cliente web para exibir uma mensagem de `html()` bate-papo lidaria com segurança com o nome do usuário e a mensagem chamando a função.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>Conciliar uma mudança no status do usuário com uma conexão ativa

Se o status de autenticação de um usuário for alterado enquanto existir uma conexão ativa, o usuário receberá um erro que afirma: "A identidade do usuário não pode ser alterada durante uma conexão SignalR ativa." Nesse caso, seu aplicativo deve se reconectar ao servidor para garantir que o id de conexão e o nome de usuário sejam coordenados. Por exemplo, se o aplicativo permitir que o usuário faça logout enquanto existe uma conexão ativa, o nome de usuário da conexão não corresponderá mais ao nome que é passado para a próxima solicitação. Você vai querer interromper a conexão antes que o usuário faça logout e, em seguida, reiniciá-la.

No entanto, é importante notar que a maioria dos aplicativos não precisará parar manualmente e iniciar a conexão. Se o aplicativo redirecionar os usuários para uma página separada após o logoff, como o comportamento padrão em um aplicativo da Web Forms ou aplicativo MVC, ou atualizar a página atual após o logoff, a conexão ativa será automaticamente desconectada e não requer nenhuma ação adicional.

O exemplo a seguir mostra como parar e iniciar uma conexão quando o status do usuário foi alterado.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

Ou, o status de autenticação do usuário pode mudar se o site usar expiração deslizante com autenticação de formulários e não houver atividade para manter o cookie de autenticação válido. Nesse caso, o usuário estará logado e o nome de usuário não corresponderá mais ao nome de usuário no token de conexão. Você pode corrigir esse problema adicionando algum script que solicita periodicamente um recurso no servidor web para manter o cookie de autenticação válido. O exemplo a seguir mostra como solicitar um recurso a cada 30 minutos.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>Arquivos proxy JavaScript gerados automaticamente

Se você não quiser incluir todos os hubs e métodos no arquivo proxy JavaScript para cada usuário, você pode desativar a geração automática do arquivo. Você pode escolher essa opção se tiver vários hubs e métodos, mas não quer que todos os usuários estejam cientes de todos os métodos. Desabilita a geração automática definindo **EnableJavaScriptProxies** como **falso**.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

Para obter mais informações sobre os arquivos proxy JavaScript, consulte [O proxy gerado e o que ele faz por você](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy). <a id="exceptions"></a>

### <a name="exceptions"></a>Exceções

Você deve evitar passar objetos de exceção aos clientes porque os objetos podem expor informações confidenciais aos clientes. Em vez disso, chame um método no cliente que exibe a mensagem de erro relevante.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
