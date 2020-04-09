---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: Manipulação global de erros na API 2 da Web ASP.NET - ASP.NET 4.x
author: davidmatson
description: Uma visão geral do tratamento global de erros na API 2 ASP.NET web para ASP.NET 4.x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 5ff54d2e4ed881ce927d0a401fb79d9b8bc5b8a1
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675422"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>Manipulação global de erros na API 2 da Web ASP.NET

por [David Matson](https://github.com/davidmatson), [Rick Anderson](https://twitter.com/RickAndMSFT)

Este tópico fornece uma visão geral do tratamento global de erros em ASP.NET API 2 da Web para ASP.NET 4.x. Hoje não há uma maneira fácil na API da Web de registrar ou lidar com erros globalmente. Algumas exceções não tratadas podem ser processadas através de filtros de [exceção,](exception-handling.md)mas há vários casos em que filtros de exceção não conseguem lidar. Por exemplo:

1. Exceções geradas por construtores de controlador.
2. Exceções geradas por manipuladores de mensagens.
3. Exceções geradas durante o roteamento.
4. Exceções geradas durante a serialização de conteúdo da resposta.

Queremos fornecer uma maneira simples e consistente de registrar e lidar (sempre que possível) essas exceções. 

Existem dois casos importantes para lidar com exceções, o caso em que somos capazes de enviar uma resposta de erro e o caso em que tudo o que podemos fazer é registrar a exceção. Um exemplo para este último caso é quando uma exceção é lançada no meio do conteúdo de resposta ao streaming; nesse caso, é tarde demais para enviar uma nova mensagem de resposta, uma vez que o código de status, cabeçalhos e conteúdo parcial já passaram pelo fio, então simplesmente abortamos a conexão. Mesmo que a exceção não possa ser tratada para produzir uma nova mensagem de resposta, ainda apoiamos o registro da exceção. Nos casos em que podemos detectar um erro, podemos retornar uma resposta de erro apropriada, conforme mostrado no seguinte:

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>Opções existentes

Além dos filtros de [exceção,](exception-handling.md) [os manipuladores de mensagens](../advanced/http-message-handlers.md) podem ser usados hoje para observar todas as respostas de 500 níveis, mas agir sobre essas respostas é difícil, pois eles não têm contexto sobre o erro original. Os manipuladores de mensagens também têm algumas das mesmas limitações que filtros de exceção em relação aos casos que podem lidar. Embora a API da Web tenha infra-estrutura de rastreamento que captura condições de erro, a infra-estrutura de rastreamento é para fins diagnósticos e não é projetada ou adequada para funcionar em ambientes de produção. O tratamento e o registro de exceções globais devem ser serviços que podem ser executados durante a produção e conectados às soluções de monitoramento existentes (por exemplo, [ELMAH](https://code.google.com/p/elmah/)).

### <a name="solution-overview"></a>Visão geral da solução

 Fornecemos dois novos serviços substituíveis pelo usuário, [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) e IExceptionHandler, para registrar e lidar com exceções não tratadas. Os serviços são muito semelhantes, com duas principais diferenças:

1. Nós suportamos o registro de vários loggers de exceção, mas apenas um único manipulador de exceção.
2. Os madeireiros de exceção sempre são chamados, mesmo que estamos prestes a abortar a conexão. Os manipuladores de exceção só são chamados quando ainda podemos escolher qual mensagem de resposta enviar.

Ambos os serviços fornecem acesso a um contexto de exceção contendo informações relevantes a partir do ponto em que a exceção foi detectada, particularmente o [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), o [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), a exceção lançada e a fonte de exceção (detalhes abaixo).

### <a name="design-principles"></a>Princípios de design

1. **Sem mudanças de quebra** Como essa funcionalidade está sendo adicionada em uma versão menor, uma restrição importante que afeta a solução é que não há alterações de quebra, seja para tipos de contratos ou para o comportamento. Esta restrição excluiu alguma limpeza que gostaríamos de ter feito em termos de blocos de captura existentes transformando exceções em 500 respostas. Esta limpeza adicional é algo que podemos considerar para um lançamento importante subsequente. Se isso é importante para você, por favor, vote nele em [ASP.NET voz de usuário da Web API](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception).
2. **Mantendo a consistência com os construtos da Web API** O pipeline de filtros da Web API é uma ótima maneira de lidar com preocupações transversais com a flexibilidade de aplicar a lógica em um escopo específico de ação, específico do controlador ou global. Os filtros, incluindo filtros de exceção, sempre possuem contextos de ação e controlador, mesmo quando registrados no âmbito global. Esse contrato faz sentido para filtros, mas significa que os filtros de exceção, mesmo os de escopo global, não são adequados para alguns casos de tratamento de exceções, como exceções de manipuladores de mensagens, onde não existe nenhuma ação ou contexto de controlador. Se quisermos usar o escopo flexível oferecido pelos filtros para o manuseio de exceções, ainda precisamos de filtros de exceção. Mas se precisamos lidar com exceção fora de um contexto controlador, também precisamos de um construto separado para o manuseio total de erros globais (algo sem as restrições de contexto de ação e contexto do controlador).

### <a name="when-to-use"></a>Quando usar

- Os loggers de exceção são a solução para ver todas as exceções não tratadas capturadas pela API da Web.
- Os manipuladores de exceção são a solução para personalizar todas as respostas possíveis a exceções não tratadas capturadas pela API da Web.
- Os filtros de exceção são a solução mais fácil para processar as exceções não manuseadas do subconjunto relacionadas a uma ação ou controlador específico.

### <a name="service-details"></a>Detalhes do serviço

 As interfaces de serviço de logger e handler de exceção são métodos simples de sincronia que tomam os respectivos contextos: 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 Também fornecemos classes básicas para ambas as interfaces. Sobrepor os métodos de núcleo (sincronização ou assincronização) é tudo o que é necessário para registrar ou manusear nos horários recomendados. Para o `ExceptionLogger` registro, a classe base garantirá que o método de registro de núcleo seja chamado apenas uma vez para cada exceção (mesmo que mais tarde se propague mais acima da pilha de chamadas e seja pego novamente). A `ExceptionHandler` classe base chamará o método de manuseio principal apenas para exceções na parte superior da pilha de chamadas, ignorando blocos de captura aninhados legados. (As versões simplificadas dessas classes base estão no apêndice abaixo.) Ambos `IExceptionLogger` `IExceptionHandler` e receber informações sobre `ExceptionContext`a exceção através de um .

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

Quando o framework chama um logger de exceção `Exception` ou `Request`um manipulador de exceção, ele sempre fornecerá um e um . Com exceção dos testes unitários, ele também sempre fornecerá um `RequestContext`. Ele raramente fornecerá um `ControllerContext` e `ActionContext` (somente quando ligar do bloco de captura para filtros de exceção). Ele raramente fornecerá `Response`um (apenas em certos casos de IIS quando no meio de tentar escrever a resposta). Observe que, como algumas `null` dessas propriedades podem ser, `null` cabe ao consumidor verificar antes de acessar os membros da classe de exceção.`CatchBlock` é uma string indicando qual bloco de captura viu a exceção. As strings do bloco de captura são as seguintes:

- HttpServer (método SendAsync)
- HttpControllerDispatcher (método SendAsync)
- HttpBatchHandler (método SendAsync)
- IExceptionFilter (processamento do apiController do pipeline de filtro de exceção no ExecuteAsync)
- Anfitrião OWIN:

    - HttpMessageHandlerAdapter.BufferResponseContentAsync (para saída de buffer)
    - HttpMessageHandlerAdapter.CopyResponseContentAsync (para saída de streaming)
- Host web:

    - HttpControllerHandler.WriteBufferedResponseContentAsync (para saída de buffer)
    - HttpControllerHandler.WriteStreamedResponseContentAsync (para saída de streaming)
    - HttpControllerHandler.WriteErrorResponseContentAsync (para falhas na recuperação de erros no modo de saída tamponado)

A lista de strings de bloco de captura também está disponível através de propriedades estáticas somente leitura. (A seqüência de blocos de captura do núcleo está na estático ExceptionCatchBlocks; o restante aparece em uma classe estática cada para OWIN e web host).`IsTopLevelCatchBlock` é útil para seguir o padrão recomendado de exceções de manuseio apenas na parte superior da pilha de chamadas. Em vez de transformar exceções em 500 respostas em qualquer lugar que ocorra um bloco de captura aninhado, um manipulador de exceção pode deixar as exceções se propagarem até que elas estejam prestes a ser vistas pelo host.

Além do `ExceptionContext`, um logger recebe mais uma `ExceptionLoggerContext`informação através da íntegra :

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

A segunda `CanBeHandled`propriedade, permite que um madeireiro identifique uma exceção que não pode ser tratada. Quando a conexão estiver prestes a ser abortada e nenhuma nova mensagem de resposta puder ser enviada, os madeireiros serão chamados, mas o manipulador ***não*** será chamado, e os madeireiros podem identificar esse cenário a partir desta propriedade.

Além do `ExceptionContext`, um manipulador obtém mais uma `ExceptionHandlerContext` propriedade que pode definir na íntegra para lidar com a exceção:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

Um manipulador de exceção indica que ele `Result` lidou com uma exceção definindo a propriedade como um resultado de ação (por exemplo, um [Resultado de Exceção,](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx) [InternalServerErrorResult,](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx) [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)ou um resultado personalizado). Se `Result` a propriedade for nula, a exceção não será tratada e a exceção original será relançada.

Para exceções na parte superior da pilha de chamadas, demos um passo extra para garantir que a resposta seja apropriada para os chamadores de API. Se a exceção se propagar até o host, o chamador verá a tela amarela da morte ou algum outro host forneceu resposta que é tipicamente HTML e normalmente não é uma resposta de erro de API apropriada. Nestes casos, o Resultado começa sem nulidade, e somente se `null` um manipulador de exceção personalizado o definir explicitamente para (não manipulado) a exceção se propagará para o host. A `Result` `null` definição nesses casos pode ser útil para dois cenários:

1. OOWIN hospedou a API da Web com middleware de tratamento de exceção personalizado registrado antes/fora da API da Web.
2. Depuração local através de um navegador, onde a tela amarela da morte é na verdade uma resposta útil para uma exceção não tratada.

Para ambos os loggers exceção e manipuladores de exceção, não fazemos nada para recuperar se o logger ou o próprio manipulador lançar uma exceção. (Além de deixar a exceção se propagar, deixe feedback no final desta página se você tiver uma abordagem melhor.) O contrato para madeireiros e manipuladores de exceção é que eles não devem deixar que exceções se propagarem para seus chamadores; caso contrário, a exceção apenas se propagará, muitas vezes até o host, resultando em um erro HTML (como ASP. A tela amarela da NET) sendo enviada de volta ao cliente (que geralmente não é a opção preferida para chamadores de API que esperam JSON ou XML).

## <a name="examples"></a>Exemplos

### <a name="tracing-exception-logger"></a>Registro de exceção de rastreamento

O logger de exceção abaixo envia dados de exceção para fontes de rastreamento configuradas (incluindo a janela de saída Debug no Visual Studio).

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>Manipulador de exceção de mensagens de erro personalizado

O manipulador de exceção abaixo produz uma resposta de erro personalizada aos clientes, incluindo um endereço de e-mail para o suporte de contato.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>Registrando filtros de exceção

Se você usar o modelo de projeto "ASP.NET MVC 4 Web Application" para `WebApiConfig` criar seu projeto, coloque o código de configuração da API da Web dentro da classe, na pasta *App_Start:*

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>Apêndice: Detalhes da classe base

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
