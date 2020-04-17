---
uid: signalr/overview/older-versions/troubleshooting
title: Solução de problemas do SignalR (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: Este artigo descreve problemas comuns com o desenvolvimento de aplicativos SignalR.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543087"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>Solução de problemas do SignalR (SignalR 1.x)

por [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este documento descreve problemas comuns de solução de problemas com o SignalR.

Este documento contém as seguintes seções.

- [Os métodos de chamada entre o cliente e o servidor falham silenciosamente](#connection)
- [Outros problemas de conexão](#other)
- [Erros de compilação e lado do servidor](#server)
- [Problemas do Visual Studio](#vs)
- [Problemas de Serviços de Informação na Internet](#iis)
- [Problemas do Azure](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>Os métodos de chamada entre o cliente e o servidor falham silenciosamente

Esta seção descreve possíveis causas para que uma chamada de método entre cliente e servidor falhe sem uma mensagem de erro significativa. Em um aplicativo SignalR, o servidor não tem informações sobre os métodos que o cliente implementa; quando o servidor invoca um método cliente, o nome do método e os dados do parâmetro são enviados ao cliente, e o método é executado somente se existir no formato que o servidor especificou. Se nenhum método de correspondência for encontrado no cliente, nada acontecerá e nenhuma mensagem de erro será levantada no servidor.

Para investigar melhor os métodos do cliente que não estão sendo chamados, você pode ativar o registro antes de ligar para o método de início no hub para ver quais chamadas estão vindo do servidor. Para habilitar o login em um aplicativo JavaScript, consulte [Como ativar o registro do lado do cliente (versão do cliente JavaScript)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging). Para habilitar o login em um aplicativo cliente .NET, consulte [Como habilitar o registro do lado do cliente (versão do cliente.NET)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>Método mal escrito, assinatura de método incorreta ou nome do hub incorreto

Se o nome ou assinatura de um método chamado não corresponder exatamente a um método apropriado no cliente, a chamada falhará. Verifique se o nome do método chamado pelo servidor corresponde ao nome do método no cliente. Além disso, o SignalR cria o proxy do hub usando métodos com maiúsculas e minúsculas, como é apropriado no JavaScript, de modo que um método chamado `SendMessage` no servidor seria chamado `sendMessage` no proxy do cliente. Se você `HubName` usar o atributo no código do lado do servidor, verifique se o nome usado corresponde ao nome usado para criar o hub no cliente. Se você não `HubName` usar o atributo, verifique se o nome do hub em um cliente JavaScript é camel-cased, como chatHub em vez de ChatHub.

### <a name="duplicate-method-name-on-client"></a>Nome do método duplicado no cliente

Verifique se você não tem um método duplicado no cliente que difere apenas por caso. Se o seu aplicativo `sendMessage`cliente tiver um método chamado, `SendMessage` verifique se também não há um método chamado.

### <a name="missing-json-parser-on-the-client"></a>Faltando analisador JSON no cliente

SignalR requer que um analisador JSON esteja presente para serializar chamadas entre o servidor e o cliente. Se o seu cliente não tiver um analisador JSON integrado (como o Internet Explorer 7), você precisará incluir um em seu aplicativo. Você pode baixar o analisador JSON [aqui](http://nuget.org/packages/json2).

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Mixing Hub e PersistentConnection sintaxe

O SignalR usa dois modelos de comunicação: Hubs e PersistentConnections. A sintaxe para chamar esses dois modelos de comunicação é diferente no código do cliente. Se você adicionou um hub no código do servidor, verifique se todo o código do seu cliente usa a sintaxe do hub adequada.

**Código cliente JavaScript que cria uma Conexão Persistente em um cliente JavaScript**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**Código cliente JavaScript que cria um Proxy hub em um cliente Javascript**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**C# código do servidor que mapeia uma rota para uma Conexão Persistente**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C# código de servidor que mapeia uma rota para um Hub ou para vários hubs se você tiver vários aplicativos**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>A conexão foi iniciada antes da assinatura ser adicionada

Se a conexão do Hub for iniciada antes que os métodos que podem ser chamados do servidor sejam adicionados ao proxy, as mensagens não serão recebidas. O seguinte código JavaScript não iniciará o hub corretamente:

**Código cliente JavaScript incorreto que não permitirá que mensagens do Hubs sejam recebidas**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

Em vez disso, adicione as assinaturas do método antes de chamar Iniciar:

**Código cliente JavaScript que adiciona corretamente assinaturas a um hub**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>Nome do método ausente no proxy do hub

Verifique se o método definido no servidor está subscrito no cliente. Mesmo que o servidor defina o método, ele ainda deve ser adicionado ao proxy do cliente. Os métodos podem ser adicionados ao proxy do cliente das `client` seguintes maneiras (Observe que o método é adicionado ao membro do hub, não diretamente ao hub):

**Código cliente JavaScript que adiciona métodos a um proxy de hub**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>Métodos de hub ou hub não declarados como Públicos

Para ser visível no cliente, a implementação do `public`hub e os métodos devem ser declarados como .

### <a name="accessing-hub-from-a-different-application"></a>Acessando o hub a partir de um aplicativo diferente

Os SignalR Hubs só podem ser acessados através de aplicativos que implementam clientes SignalR. O SignalR não pode interoperar com outras bibliotecas de comunicação (como serviços web SOAP ou WCF.) Se não houver um cliente SignalR disponível para sua plataforma de destino, você não poderá acessar o ponto final do servidor diretamente.

### <a name="manually-serializing-data"></a>Serialização manual de dados

O SignalR usará automaticamente o JSON para serializar os parâmetros do seu método, não há necessidade de fazê-lo você mesmo.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>Método do Hub remoto não executado no cliente na função OnDisconnected

Este comportamento ocorre por design. Quando `OnDisconnected` é chamado, o hub `Disconnected` já entrou no estado, o que não permite que outros métodos de hub sejam chamados.

**C# código do servidor que executa corretamente o código no evento OnDisconnected**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>Limite de conexão atingido

Ao usar a versão completa do IIS em um sistema operacional cliente como o Windows 7, um limite de 10 conexões é imposto. Ao usar um sistema operacional cliente, use o IIS Express para evitar esse limite.

### <a name="cross-domain-connection-not-set-up-properly"></a>A conexão entre domínios não é configurada corretamente

Se uma conexão entre domínios (uma conexão para a qual a URL SignalR não está no mesmo domínio da página de hospedagem) não for configurada corretamente, a conexão pode falhar sem uma mensagem de erro. Para obter informações sobre como ativar a comunicação entre [domínios, consulte Como estabelecer uma conexão entre domínios](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>Conexão usando NTLM (Active Directory) que não funciona no cliente .NET

Uma conexão em um aplicativo cliente .NET que usa segurança de domínio pode falhar se a conexão não estiver configurada corretamente. Para usar signalR em um ambiente de domínio, defina a propriedade de conexão necessária da seguinte forma:

**C# código cliente que implementa credenciais de conexão**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>Outros problemas de conexão

Esta seção descreve as causas e soluções para sintomas específicos ou mensagens de erro que ocorrem durante uma conexão.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>Erro "Iniciar deve ser chamado antes que os dados possam ser enviados"

Esse erro é comumente visto se o código faz referência a objetos SignalR antes de a conexão ser iniciada. O fio para manipuladores e assim que chamará métodos definidos no servidor deve ser adicionado após a conexão ser concluída. Observe que a `Start` chamada é assíncrona, portanto, o código após a chamada pode ser executado antes de ser concluída. A melhor maneira de adicionar manipuladores depois que uma conexão é iniciada completamente é colocá-los em uma função de retorno de chamada que é passada como um parâmetro para o método de inicialização:

**JavaScript código cliente que adiciona corretamente manipuladores de eventos que referenciam objetos SignalR**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

Esse erro também será visto se uma conexão parar enquanto os objetos SignalR ainda estiverem sendo referenciados.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>Erro "301 movido permanentemente" ou "302 movido temporariamente"

Esse erro pode ser visto se o projeto contiver uma pasta chamada SignalR, que interferirá com o proxy criado automaticamente. Para evitar esse erro, não `SignalR` use uma pasta chamada em seu aplicativo ou desligue a geração automática de proxy. Consulte [o Proxy gerado e o que ele faz para obter](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) mais detalhes.

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>Erro "403 Proibido" no cliente .NET ou Silverlight

Esse erro pode ocorrer em ambientes entre domínios onde a comunicação entre domínios não está adequadamente ativada. Para obter informações sobre como ativar a comunicação entre [domínios, consulte Como estabelecer uma conexão entre domínios](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain). Para estabelecer uma conexão entre domínios em um cliente Silverlight, consulte [conexões de domínio cruzado de clientes Silverlight](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).

### <a name="404-not-found-error"></a>Erro "404 Não Encontrado"

Há várias causas para este problema. Verifique tudo o que puder:

- **Referência de endereço proxy do hub não formatado corretamente:** Esse erro é comumente visto se a referência ao endereço proxy do hub gerado não for formatado corretamente. Verifique se a referência ao endereço do hub é feita corretamente. Veja [como fazer referência ao proxy gerado dinamicamente](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) para obter detalhes.
- **Adicionando rotas ao aplicativo antes de adicionar a rota do hub:** Se o aplicativo usar outras rotas, verifique se `MapHubs`a primeira rota adicionada é a chamada para .

### <a name="500-internal-server-error"></a>"Erro do servidor interno 500"

Este é um erro muito genérico que poderia ter uma grande variedade de causas. Os detalhes do erro devem aparecer no registro de eventos do servidor ou podem ser encontrados através da depuração do servidor. Informações de erro mais detalhadas podem ser obtidas ligando erros detalhados no servidor. Para obter mais informações, consulte [Como lidar com erros na classe Hub](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>Erro &lt;"TypeError:&gt; hubType is indefined"

Este erro resultará se `MapHubs` a chamada não for feita corretamente. Veja [Como registrar a rota SignalR e configurar as opções SignalR](../guide-to-the-api/hubs-api-guide-server.md#route) para obter mais informações.

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException não foi tratada pelo código do usuário

Verifique se os parâmetros enviados aos seus métodos não incluem tipos não serializáveis (como alças de arquivo ou conexões de banco de dados). Se você precisar usar membros em um objeto do lado do servidor que você não deseja ser enviado ao `JSONIgnore` cliente (seja por segurança ou por razões de serialização), use o atributo.

### <a name="protocol-error-unknown-transport-error"></a>Erro de "erro de protocolo: transporte desconhecido"

Esse erro pode ocorrer se o cliente não suportar os transportes que o SignalR usa. Consulte [Transportes e Recuos](../getting-started/introduction-to-signalr.md#transports) para obter informações sobre quais navegadores podem ser usados com o SignalR.

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"A geração de proxy javaScript Hub foi desativada."

Esse erro ocorrerá `DisableJavaScriptProxies` se for definido, incluindo também uma `signalr/hubs`referência ao proxy gerado dinamicamente em . Para obter mais informações sobre a criação manual do proxy, consulte [O proxy gerado e o que ele faz por você](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"O ID de conexão está no formato incorreto" ou "A identidade do usuário não pode ser alterada durante um erro de signalr ativo"

Esse erro pode ser visto se a autenticação estiver sendo usada e o cliente estiver conectado antes que a conexão seja interrompida. A solução é parar a conexão SignalR antes de fazer logon do cliente.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"Erro não capturado: SignalR: jQuery não encontrado. Certifique-se de que jQuery é referenciado antes do erro do arquivo SignalR.js

O cliente SignalR JavaScript requer que jQuery seja executado. Verifique se sua referência ao jQuery está correta, se o caminho utilizado é válido e que a referência a jQuery é anterior à referência ao SignalR.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>Erro de "Erro de tipo&lt;&gt;não capturado: não é possível ler propriedade ' propriedade ' de erro indefinido"

Este erro resulta de não ter jQuery ou os hubs proxy referenciados corretamente. Verifique se sua referência ao jQuery e ao proxy hubs está correta, se o caminho usado é válido e que a referência ao jQuery é anterior à referência ao proxy hubs. A referência padrão ao proxy de hubs deve ser pareada com a seguinte:

**Código do lado do cliente HTML que faz referência correta ao proxy hubs**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"RuntimeBinderException não foi manipulado pelo código do usuário"

Este erro pode ocorrer quando `Hub.On` a sobrecarga incorreta é usada. Se o método tiver um valor de retorno, o tipo de retorno deve ser especificado como um parâmetro de tipo genérico:

**Método definido no cliente (sem proxy gerado)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>O ID de conexão é inconsistente ou quebras de conexão entre cargas de página

Este comportamento ocorre por design. Uma vez que o objeto do hub está hospedado no objeto da página, o hub é destruído quando a página é atualizada. Um aplicativo de várias páginas precisa manter a associação entre usuários e IDs de conexão para que eles sejam consistentes entre as cargas de página. Os IDs de conexão podem ser `ConcurrentDictionary` armazenados no servidor em um objeto ou em um banco de dados.

### <a name="value-cannot-be-null-error"></a>Erro "Valor não pode ser nulo"

Os métodos do lado do servidor com parâmetros opcionais não são suportados no momento; se o parâmetro opcional for omitido, o método falhará. Para obter mais informações, consulte [Parâmetros Opcionais](https://github.com/SignalR/SignalR/issues/324).

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox não pode estabelecer uma conexão com o servidor no &lt;endereço"&gt;erro no Firebug

Esta mensagem de erro pode ser vista no Firebug se a negociação do transporte WebSocket falhar e outro transporte for usado em vez disso. Este comportamento ocorre por design.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>"O certificado remoto é inválido de acordo com o procedimento de validação" erro no aplicativo cliente .NET

Se o seu servidor precisar de certificados de cliente personalizados, então você pode adicionar um certificado x509 à conexão antes que a solicitação seja feita. Adicione o certificado à `Connection.AddClientCertificate`conexão usando .

### <a name="connection-drops-after-authentication-times-out"></a>A conexão cai após os tempos de autenticação fora

Este comportamento ocorre por design. As credenciais de autenticação não podem ser modificadas enquanto uma conexão estiver ativa; para atualizar credenciais, a conexão deve ser interrompida e reiniciada.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>OnConnected é chamado duas vezes ao usar jQuery Mobile

A função de `initializePage` jQuery Mobile força os scripts em cada página a serem reexecutados, criando assim uma segunda conexão. As soluções para este problema incluem:

- Inclua a referência ao jQuery Mobile antes do arquivo JavaScript.
- Desativar a `initializePage` função `$.mobile.autoInitializePage = false`configurando .
- Aguarde que a página termine de inicializar antes de iniciar a conexão.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>As mensagens estão atrasadas em aplicativos Silverlight usando eventos enviados pelo servidor

As mensagens são atrasadas ao usar eventos enviados pelo servidor no Silverlight. Para forçar uma votação longa a ser usada, use o seguinte ao iniciar a conexão:

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>"Permissão negada" usando o protocolo Forever Frame

Esta é uma questão conhecida, descrita [aqui.](https://github.com/SignalR/SignalR/issues/1963) Esse sintoma pode ser visto usando a mais recente biblioteca JQuery; a solução é fazer o downgrade do aplicativo para o JQuery 1.8.2.

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>Erros de compilação e lado do servidor

 A seção a seguir contém possíveis soluções para erros de tempo de execução do compilador e do lado do servidor. 

### <a name="reference-to-hub-instance-is-null"></a>A referência à instância do Hub é nula

Uma vez que uma instância de hub é criada para cada conexão, você não pode criar uma instância de um hub em seu código você mesmo. Para chamar métodos em um hub de fora do próprio hub, consulte [Como chamar os métodos do cliente e gerenciar grupos de fora da classe Hub](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) para obter uma referência ao contexto do hub.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.Current.Session é nulo

Este comportamento ocorre por design. O SignalR não suporta o estado de sessão ASP.NET, uma vez que permitir o estado da sessão quebraria as mensagens duplex.

### <a name="no-suitable-method-to-override"></a>Nenhum método adequado para substituir

Você pode ver esse erro se estiver usando código de documentação ou blogs antigos. Verifique se você não está fazendo referência a nomes de métodos `OnConnectedAsync`que foram alterados ou preteridos (como ).

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions.WebSocketServerUrl é nulo

Este comportamento ocorre por design. Este membro é preterido e não deve ser usado.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"Um erro de "signalr.hubs" já está na coleção de rotas

Este erro será `MapHubs` visto se for chamado duas vezes pela sua aplicação. Alguns exemplos `MapHubs` de aplicativos chamam diretamente no arquivo global do aplicativo; outros fazem a chamada em uma aula de invólucro. Certifique-se de que sua aplicação não faça as duas coisas.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Problemas do Visual Studio

Esta seção descreve problemas encontrados no Visual Studio.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>O nó script documents não aparece no Solution Explorer

Alguns de nossos tutoriais direcionam você para o nó "Script Documents" no Solution Explorer durante a depuração. Este nó é produzido pelo depurador JavaScript e só aparecerá durante a depuração de clientes do navegador no Internet Explorer; o nó não aparecerá se o Chrome ou o Firefox forem usados. O depurador JavaScript também não será executado se outro depurador de cliente estiver sendo executado, como o depurador Silverlight.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR não funciona no Visual Studio 2008 ou anterior

Este comportamento ocorre por design. SignalR requer .NET Framework 4 ou posterior; isso requer que os aplicativos SignalR sejam desenvolvidos no Visual Studio 2010 ou posterior.

<a id="iis"></a>

## <a name="iis-issues"></a>Questões do IIS

Esta seção contém problemas com os Serviços de Informação da Internet.

### <a name="web-site-crashes-after-maphubs-call"></a>Site falha após chamada do MapHubs

Este problema foi corrigido na versão mais recente do SignalR. Verifique se você está usando a versão mais recente lançada do SignalR atualizando sua instalação usando nuGet.

<a id="azure"></a>

## <a name="azure-issues"></a>Problemas do Azure

Esta seção contém problemas com o Microsoft Azure.

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>As mensagens não são recebidas através do backplane do Azure depois de alterar nomes de tópicos

Os tópicos usados pelo backplane do Azure não se destinam a ser configuráveis pelo usuário.
