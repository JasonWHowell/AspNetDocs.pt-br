---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: Novidades em ASP.NET 4.5 e Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: Este documento descreve novos recursos e melhorias que estão sendo introduzidos em ASP.NET 4.5. Também descreve melhorias que estão sendo feitas para o desenvolvimento da web...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676282"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>Novidades no ASP.NET 4.5 e no Visual Studio 2012

> Este documento descreve novos recursos e melhorias que estão sendo introduzidos em ASP.NET 4.5. Ele também descreve melhorias que estão sendo feitas para o desenvolvimento web no Visual Studio 2012. Este documento foi originalmente publicado em 29 de fevereiro de 2012.

- [ASP.NET Core Runtime e Framework](#_Toc318097372)

    - [Leitura e respostas assíncronas de leitura e escrita http](#_Toc318097373)
    - [Melhorias no tratamento httpRequest](#_Toc318097374)
    - [Assíncronamente lavando uma resposta](#_Toc318097375)
    - [Suporte para *módulos* e manipuladores assíncronos baseados em espera e *tarefas*](#_Toc318097376)
    - [Módulos HTTP assíncronos](#_Toc318097377)
    - [Manipuladores HTTP assíncronos](#_Toc318097378)
    - [Novos recursos de validação de solicitações de ASP.NET](#_Toc318097379)
    - [Validação de solicitação diferida ("preguiçosa")](#_Toc318097380)
    - [Suporte para solicitações não validadas](#_Toc318097381)
    - [Biblioteca AntiXSS](#_Toc318097382)
    - [Suporte ao Protocolo de Soquetes Web](#_Toc318097383)
    - [Agrupamento e Minificação](#_Toc318097384)
    - [Melhorias de desempenho para hospedagem na Web](#_Toc_perf)

        - [Principais fatores de desempenho](#_Toc_perf_1)
        - [Requisitos para novos recursos de desempenho](#_Toc_perf_2)
        - [Compartilhando Assembléias Comuns](#_Toc_perf_3)
        - [Usando compilação JIT multi-Core para inicialização mais rápida](#_Toc_perf_4)
        - [Afinando a coleta de lixo para otimizar a memória](#_Toc_perf_5)
        - [Pré-candidatos a aplicações web](#_Toc_perf_6)
- [formulários da Web ASP.NET](#_Toc318097385)

    - [Controles de dados fortemente tipados](#_Toc318097386)
    - [Model binding](#_Toc318097387)

        - [Selecionando dados](#_Toc318097388)
        - [Provedores de valor](#_Toc318097389)
        - [Filtragem por valores de um controle](#_Toc318097390)
    - [Expressões codificadas de dados codificadas por HTML](#_Toc318097391)
    - [Validação Discreta](#_Toc318097392)
    - [Atualizações HTML5](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [Páginas da Web do ASP.NET 2](#_Toc318097395)
- [Candidato ao lançamento do Visual Studio 2012](#_Toc318097396)

    - [Compartilhamento de projetos entre o Visual Studio 2010 e o Candidato de Lançamento do Visual Studio 2012 (Compatibilidade do Projeto)](#project-compatibility)
    - [Alterações de configuração em ASP.NET 4.5 Modelos de sites](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [Suporte nativo no IIS 7 para roteamento de ASP.NET](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [Editor de HTML](#_Toc318097397)

        - [Tarefas inteligentes](#_Toc318097398)
        - [Suporte wai-aria](#_Toc318097399)
        - [Novos trechos HTML5](#_Toc318097400)
        - [Extrair para o controle do usuário](#_Toc318097401)
        - [IntelliSense para nuggets de código em atributos](#_Toc318097402)
        - [Renomeação automática da tag correspondente quando você renomear uma tag de abertura ou fechamento](#_Toc318097403)
        - [Geração de manipuladores de eventos](#_Toc318097404)
        - [Recuo inteligente](#_Toc318097405)
        - [Reduzir automaticamente a conclusão da declaração](#_Toc318097406)
    - [JavaScript Editor](#_Toc318097407)

        - [Delineamento de código](#_Toc318097408)
        - [Correspondência de cinta](#_Toc318097409)
        - [Ir para Definição](#_Toc318097410)
        - [Suporte ao ECMAScript5](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [Sobrecargas de assinatura VSDOC](#_Toc318097413)
        - [Referências implícitas](#_Toc318097414)
    - [Editor de CSS](#_Toc318097415)

        - [Reduzir automaticamente a conclusão da declaração](#_Toc318097416)
        - [Recuo hierárquico.](#_Toc318097417)
        - [Suporte a hacks CSS](#_Toc318097418)
        - [Esquemas específicos do fornecedor (-moz-,-webkit)](#_Toc318097419)
        - [Comentando e sem comentários suporte](#_Toc318097420)
        - [Seletor de cor](#_Toc318097421)
        - [Snippets](#_Toc318097422)
        - [Regiões aduaneiras](#_Toc318097423)
    - [Inspetor de Página](#_Toc318097424)
    - [Publicação](#_Toc318097425)

        - [Perfis de publicação](#_Toc318097426)
        - [ASP.NET pré-compilação e fusão](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [Isenção de responsabilidade](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core Runtime e Framework

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>Leitura e respostas assíncronas de leitura e escrita http

ASP.NET 4 introduziu a capacidade de ler uma entidade de solicitação HTTP como um fluxo usando o método *HttpRequest.GetBufferlessInputStream.* Este método forneceu acesso de streaming à entidade de solicitação. No entanto, executou ssincronizadamente, o que amarrou um fio durante a duração de uma solicitação.

ASP.NET 4.5 suporta a capacidade de ler fluxos de forma assíncrona em uma entidade de solicitação HTTP e a capacidade de fazer descarga assíncronamente. ASP.NET 4.5 também oferece a capacidade de buffer duplo de uma entidade de solicitação HTTP, o que fornece uma integração mais fácil com manipuladores HTTP a jusante, como manipuladores de página .aspx e controladores mvc ASP.NET.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>Melhorias no tratamento httpRequest

A referência De fluxo retornada por ASP.NET 4.5 de *HttpRequest.GetBufferlessInputStream* suporta métodos de leitura síncronos e assíncronos. O objeto *Stream* retornado do *GetBufferlessInputStream* agora implementa os métodos BeginRead e EndRead. Os métodos de *fluxo* assíncrono permitem que você leia assíncronamente a entidade de solicitação em pedaços, enquanto ASP.NET libera o segmento atual entre cada iteração de um loop de leitura assíncrona.

ASP.NET 4.5 também adicionou um método complementar para ler a entidade de solicitação de forma tamponada: *HttpRequest.GetBufferedInputStream*. Essa nova sobrecarga funciona como *GetBufferlessInputStream*, suportando leituras síncronas e assíncronas. No entanto, ao ler, *getBufferedInputStream* também copia os bytes da entidade em ASP.NET buffers internos para que os módulos e manipuladores a jusante ainda possam acessar a entidade de solicitação. Por exemplo, se algum código upstream no pipeline já tiver lido a entidade de solicitação usando *GetBufferedInputStream,* você ainda pode usar *HttpRequest.Form* ou *HttpRequest.Files*. Isso permite que você execute processamento assíncrono em uma solicitação (por exemplo, transmitindo um grande upload de arquivo para um banco de dados), mas ainda executar páginas .aspx e controladores de ASP.NET MVC depois.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>Assíncronamente lavando uma resposta

O envio de respostas a um cliente HTTP pode levar um tempo considerável quando o cliente está longe ou tem uma conexão de baixa largura de banda. Normalmente, ASP.NET buffers os bytes de resposta à medida que são criados por um aplicativo. ASP.NET então realiza uma única operação de envio dos buffers acumulados no final do processamento de solicitação.

Se a resposta tamponada for grande (por exemplo, transmitindo um grande arquivo para um cliente), você deve ligar periodicamente para *HttpResponse.Flush* para enviar saída tamponada ao cliente e manter o uso da memória sob controle. No entanto, como *flush* é uma chamada síncrona, iterativamente chamando *Flush* ainda consome um thread durante a duração de solicitações potencialmente longas.

ASP.NET 4.5 adiciona suporte para realizar descargas de forma assíncrona usando os métodos *BeginFlush* e *EndFlush* da classe *HttpResponse.* Usando esses métodos, você pode criar módulos assíncronos e manipuladores assíncronos que enviam dados incrementalmente para um cliente sem amarrar os segmentos do sistema operacional. Entre as chamadas *BeginFlush* e *EndFlush,* ASP.NET libera o segmento atual. Isso reduz substancialmente o número total de threads ativos necessários para suportar downloads HTTP de longa duração.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>Suporte para *espera* e *tarefa* - Módulos e manipuladores assíncronos baseados

O .NET Framework 4 introduziu um conceito de programação assíncrona referido como *uma tarefa*. As tarefas são representadas pelo tipo *Tarefa* e tipos relacionados no *namespace System.Threading.Tasks.* O .NET Framework 4.5 se baseia nisso com aprimoramentos do compilador que tornam o trabalho com objetos *de tarefa* simples. No Quadro .NET 4.5, os compiladores suportam duas novas palavras-chave: *aguardar* e *assincronizar*. A palavra-chave *aguardado* é abreviação sintática para indicar que um pedaço de código deve aguardar assíncronamente algum outro pedaço de código. A palavra-chave *assíncrona* representa uma dica que você pode usar para marcar métodos como métodos assíncronos baseados em tarefas.

A combinação de *espera*, *assincronismo*e objeto *Tarefa* torna muito mais fácil para você escrever código assíncrono em .NET 4.5. ASP.NET 4.5 suporta essas simplificações com novas APIs que permitem escrever módulos HTTP assíncronos e manipuladores HTTP assíncronos usando os novos aprimoramentos do compilador.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>Módulos HTTP assíncronos

Suponha que você queira executar um trabalho assíncrono dentro de um método que retorna um objeto *Tarefa.* O exemplo de código a seguir define um método assíncrono que faz uma chamada assíncrona para baixar a página inicial da Microsoft. Observe o uso da palavra-chave *assíncrona* na assinatura do método e a chamada *aguarde* *para DownloadStringTaskAsync*.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

Isso é tudo que você tem para escrever — o .NET Framework lidará automaticamente com o desenrolar da pilha de chamadas enquanto espera que o download seja concluído, bem como restaurará automaticamente a pilha de chamadas após o download ser feito.

Agora suponha que você queira usar este método assíncrono em um módulo HTTP assíncrono ASP.NET. ASP.NET 4.5 inclui um método auxiliar *(EventHandlerTaskAsyncHelper)* e um novo tipo de delegado *(TaskEventHandler)* que você pode usar para integrar métodos assíncronos baseados em tarefas com o modelo de programação assíncrona mais antigo exposto pelo ASP.NET pipeline HTTP. Este exemplo mostra como:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>Manipuladores HTTP assíncronos

A abordagem tradicional para escrever manipuladores assíncronos em ASP.NET é implementar a interface *IHttpAsyncHandler.* ASP.NET 4.5 introduz o tipo de base assíncrona *HttpTaskAsyncHandler* do qual você pode derivar, o que torna muito mais fácil escrever manipuladores assíncronos.

O tipo *HttpTaskAsyncHandler* é abstrato e exige que você anule o método *ProcessRequestAsync.* Internamente, ASP.NET cuida da integração da assinatura de retorno (um objeto *de tarefa)* do *ProcessRequestAsync* com o modelo de programação assíncrona mais antigo usado pelo pipeline ASP.NET.

O exemplo a seguir mostra como você pode usar *o Task* e *esperar* como parte da implementação de um manipulador HTTP assíncrono:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>Novos recursos de validação de solicitações de ASP.NET

Por padrão, ASP.NET realiza a validação de solicitações — examina solicitações para procurar marcação ou script em campos, cabeçalhos, cookies e assim por diante. Se algum for detectado, ASP.NET abre uma exceção. Isso funciona como uma primeira linha de defesa contra potenciais ataques de scripts entre sites.

ASP.NET 4.5 facilita a leitura seletiva de dados de solicitação não validados. ASP.NET 4.5 também integra a popular biblioteca AntiXSS, que antes era uma biblioteca externa.

Os desenvolvedores têm frequentemente solicitado a capacidade de desativar seletivamente a validação de solicitações para seus aplicativos. Por exemplo, se o seu aplicativo é um software de fórum, você pode querer permitir que os usuários enviem postagens e comentários em fóruns formatados por HTML, mas ainda assim certifique-se de que a validação da solicitação está verificando todo o resto.

ASP.NET 4.5 introduz dois recursos que facilitam o trabalho seletivo com entrada não validada: validação de solicitação diferida ("preguiçosa") e acesso a dados de solicitação não validados.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>Validação de solicitação diferida ("preguiçosa")

Em ASP.NET 4.5, por padrão todos os dados de solicitação estão sujeitos à validação da solicitação. No entanto, você pode configurar o aplicativo para adiar a validação da solicitação até que você realmente acesse os dados da solicitação. (Isso às vezes é referido como validação de solicitação preguiçosa, com base em termos como carregamento preguiçoso para determinados cenários de dados.) Você pode configurar o aplicativo para usar validação diferida no arquivo Web.config definindo o atributo *requestValidationMode* para 4.5 no elemento *httpRUntime,* como no exemplo a seguir:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

Quando o modo de validação da solicitação é definido como 4.5, a validação da solicitação é acionada apenas para um valor específico de solicitação e somente quando seu código acessa esse valor. Por exemplo, se o seu código receber o\_valor de Request.Form["forum post"], a validação da solicitação será invocada apenas para esse elemento na coleção de formulários. Nenhum dos outros elementos da coleção *formulário* é validado. Em versões anteriores de ASP.NET, a validação da solicitação foi acionada para toda a coleta de solicitações quando qualquer elemento do acervo foi acessado. O novo comportamento facilita que diferentes componentes do aplicativo olhem para diferentes partes dos dados de solicitação sem desencadear a validação de solicitações em outras peças.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>Suporte para solicitações não validadas

A validação de solicitação adiada por si só não resolve o problema de ignorar seletivamente a validação da solicitação. A chamada para Request.Form["forum\_post"] ainda aciona a validação da solicitação para esse valor específico de solicitação. No entanto, você pode querer acessar este campo sem acionar a validação porque você deseja permitir a marcação nesse campo.

Para permitir isso, ASP.NET 4.5 agora suporta acesso não validado aos dados de solicitação. ASP.NET 4.5 inclui uma nova propriedade de coleção *não validada* na classe *HttpRequest.* Esta coleção fornece acesso a todos os valores comuns de dados de solicitação, como *Formulário,* *QueryString,* *Cookies*e *Url.*

Usando o exemplo do fórum, para poder ler dados de solicitação não validados, primeiro você precisa configurar o aplicativo para usar o novo modo de validação de solicitações:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

Em seguida, você pode usar a propriedade *HttpRequest.Unvalidated* para ler o valor do formulário não validado:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> Segurança - *Use dados de solicitação não validados com cuidado!* ASP.NET 4.5 adicionou as propriedades e coletas de solicitação não validadas para facilitar o acesso a dados de solicitação não validados muito específicos. No entanto, você ainda deve executar a validação personalizada nos dados de solicitação bruta para garantir que o texto perigoso não seja renderizado aos usuários.

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>Biblioteca AntiXSS

Devido à popularidade da Biblioteca Microsoft AntiXSS, ASP.NET 4.5 agora incorpora rotinas de codificação principais a partir da versão 4.0 dessa biblioteca.

As rotinas de codificação são implementadas pelo tipo *AntiXssEncoder* no novo *namespace System.Web.Security.AntiXss.* Você pode usar o tipo *AntiXssEncoder* diretamente chamando qualquer um dos métodos de codificação estática que são implementados no tipo. No entanto, a abordagem mais fácil para usar as novas rotinas anti-XSS é configurar um aplicativo ASP.NET para usar a classe *AntiXssEncoder* por padrão. Para fazer isso, adicione o seguinte atributo ao arquivo Web.config:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

Quando o atributo *encoderType* é definido para usar o tipo *AntiXssEncoder,* toda a codificação de saída em ASP.NET usa automaticamente as novas rotinas de codificação.

Estas são as partes da biblioteca externa AntiXSS que foram incorporadas ao ASP.NET 4.5:

- *HtmlEncode,* *HtmlFormUrlEncode*e *HtmlAttributeEncode*
- *XmlAttributeEncode* e *XmlEncode*
- *UrlEncode* e *UrlPathEncode* (novo)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Suporte ao Protocolo de Soquetes Web

O protocolo WebSockets é um protocolo de rede baseado em padrões que define como estabelecer comunicações bidirecionais seguras e em tempo real entre um cliente e um servidor via HTTP. A Microsoft trabalhou com os órgãos de padrões IETF e W3C para ajudar a definir o protocolo. O protocolo WebSockets é suportado por qualquer cliente (não apenas navegadores), com a Microsoft investindo recursos substanciais que suportam o protocolo WebSockets em sistemas operacionais clientes e móveis.

O protocolo WebSockets facilita muito a criação de transferências de dados de longo prazo entre um cliente e um servidor. Por exemplo, escrever um aplicativo de bate-papo é muito mais fácil porque você pode estabelecer uma conexão verdadeira de longo prazo entre um cliente e um servidor. Você não precisa recorrer a solução sooral ou pesquisa de mora HTTP para simular o comportamento de um soquete.

ASP.NET 4.5 e O IIS 8 incluem suporte a WebSockets de baixo nível, permitindo que os desenvolvedores ASP.NET usem APIs gerenciadas para leitura e escrita assíncrona de ambos os dados de string e binários em um objeto WebSockets. Para ASP.NET 4.5, há um novo *namespace System.Web.WebSockets* que contém tipos para trabalhar com o protocolo WebSockets.

Um cliente do navegador estabelece uma conexão WebSockets criando um objeto *DOM WebSocket* que aponta para uma URL em um aplicativo ASP.NET, como no exemplo a seguir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

Você pode criar pontos finais do WebSockets em ASP.NET usando qualquer tipo de módulo ou manipulador. No exemplo anterior, um arquivo .ashx foi usado, porque arquivos .ashx são uma maneira rápida de criar um manipulador.

De acordo com o protocolo WebSockets, um aplicativo de ASP.NET aceita a solicitação de WebSockets de um cliente, indicando que a solicitação deve ser atualizada de uma solicitação HTTP GET para uma solicitação de WebSockets. Aqui está um exemplo:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

O método *AcceptWebSocketRequest* aceita um delegado de função porque ASP.NET desfaz a solicitação HTTP atual e, em seguida, transfere o controle para o delegado da função. Conceitualmente, essa abordagem é semelhante à forma como você usa *System.Threading.Thread*, onde você define um delegado de início de thread em que o trabalho de fundo é realizado.

Depois de ASP.NET e o cliente tiverem concluído com sucesso um aperto de mão do WebSockets, ASP.NET ligue para o delegado e o aplicativo WebSockets comece a ser executado. O exemplo de código a seguir mostra um aplicativo de eco simples que usa o suporte a WebSockets incorporado em ASP.NET:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

O suporte no .NET 4.5 para a *palavra-chave aguardado* e operações assíncronas baseadas em tarefas é um ajuste natural para escrever aplicativos WebSockets. O exemplo de código mostra que uma solicitação de WebSockets é executada completamente assíncronamente dentro ASP.NET. O aplicativo aguarda assíncronamente para que uma mensagem seja enviada de um cliente, chamando *o soquete de aguarde. ReceiveAsync*. Da mesma forma, você pode enviar uma mensagem assíncrona para um cliente chamando *o soquete de aguarde. Sendasync*.

No navegador, um aplicativo recebe mensagens de WebSockets através de uma função *onmessage.* Para enviar uma mensagem de um navegador, você chama o método de *envio* do tipo *WEBSocket* DOM, como mostrado neste exemplo:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

No futuro, podemos liberar atualizações para essa funcionalidade que abstraem algumas das codificações de baixo nível que são necessárias nesta versão para aplicativos WebSockets.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>Agrupamento e minificação

O agrupamento permite combinar arquivos JavaScript e CSS individuais em um pacote que pode ser tratado como um único arquivo. A minificação condensa arquivos JavaScript e CSS removendo o espaço em branco e outros caracteres que não são necessários. Esses recursos funcionam com Formulários web, ASP.NET MVC e Páginas da Web.

Os pacotes são criados usando a classe Bundle ou uma de suas classes infantis, ScriptBundle e StyleBundle. Depois de configurar uma instância de um pacote, o pacote é disponibilizado para solicitações recebidas, simplesmente adicionando-o a uma instância global do BundleCollection. Nos modelos padrão, a configuração do pacote é executada em um arquivo BundleConfig. Essa configuração padrão cria pacotes para todos os scripts principais e arquivos css usados pelos modelos.

Os pacotes são referenciados de dentro de visualizações usando um dos dois métodos possíveis de ajuda. A fim de suportar a renderização de diferentes marcações para um pacote quando no modo de depuração vs. de lançamento, as classes ScriptBundle e StyleBundle têm o método helper, Render. Quando estiver no modo de depuração, o Render gerará marcação para cada recurso no pacote. Quando estiver no modo de lançamento, o Render gerará um único elemento de marcação para todo o pacote. A mistura entre o modo de depuração e a liberação pode ser realizada modificando o atributo de depuração do elemento compilação na web.config, conforme mostrado abaixo:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

Além disso, a otimização de ativação ou desativação pode ser definida diretamente através da propriedade BundleTable.EnableOptimizations.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

Quando os arquivos são empacotados, eles são classificados pela primeira vez em ordem alfabética (a maneira como eles são exibidos no **Solution Explorer**). Eles são então organizados para que bibliotecas conhecidas e suas extensões personalizadas (como jQuery, MooTools e Dojo) sejam carregadas primeiro. Por exemplo, a ordem final para o agrupamento da pasta Scripts como mostrado acima será:

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

Os arquivos CSS também são ordenados alfabeticamente e depois reorganizados para que reset.css e normalize.css venham antes de qualquer outro arquivo. A classificação final do agrupamento da pasta Estilos mostrado acima será a seguinte:

1. Reset.css
2. content.css
3. forms.css
4. globals.css
5. menu.css
6. Styles.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Melhorias de desempenho para hospedagem na Web

O .NET Framework 4.5 e o Windows 8 introduzem recursos que podem ajudá-lo a obter um aumento significativo de desempenho para cargas de trabalho de servidor web. Isso inclui uma redução (até 35%) tanto no tempo de inicialização quanto na pegada de memória de sites de hospedagem que usam ASP.NET.

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>Principais fatores de desempenho

Idealmente, todos os sites devem estar ativos e na memória para garantir uma resposta rápida à próxima solicitação, sempre que ela vier. Os fatores que podem afetar a capacidade de resposta do local incluem:

- O tempo que leva para um site reiniciar após a reciclagem de um pool de aplicativos. Este é o tempo que leva para iniciar um processo de servidor web para o site quando as montagens do site não estão mais na memória. (Os conjuntos de plataformas ainda estão na memória, uma vez que são usados por outros sites.) Essa situação é referida como "local frio, inicial ização de estruturas quentes" ou apenas "inicialização de local frio".
- Quanta memória o site ocupa. Os termos para isso são "consumo de memória por site" ou "conjunto de trabalho não compartilhado".

As novas melhorias de desempenho se concentram em ambos os fatores.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>Requisitos para novos recursos de desempenho

Os requisitos para os novos recursos podem ser divididos nessas categorias:

- Melhorias que são executadas no Quadro .NET 4.
- Melhorias que requerem o .NET Framework 4.5, mas podem ser executadas em qualquer versão do Windows.
- Melhorias que estão disponíveis apenas com o .NET Framework 4.5 em execução no Windows 8.

O desempenho aumenta a cada nível de melhoria que você é capaz de habilitar.

Algumas das melhorias do .NET Framework 4.5 aproveitam recursos de desempenho mais amplos que se aplicam a outros cenários também.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>Compartilhando Assembléias Comuns

**Requisito:**.NET Framework 4 e Visual Studio 11 Developer Preview SDK

Diferentes sites em um servidor geralmente usam os mesmos conjuntos de ajudantes (por exemplo, conjuntos de um kit inicial ou aplicativo de amostra). Cada site tem sua própria cópia dessas assembléias em seu diretório Bin. Mesmo que o código do objeto para os conjuntos seja idêntico, eles são conjuntos fisicamente separados, então cada montagem tem que ser lida separadamente durante a inicialização do site frio e mantida separadamente na memória.

A nova funcionalidade de estágio resolve essa ineficiência e reduz tanto os requisitos de RAM quanto o tempo de carga. O estágio permite que o Windows mantenha uma única cópia de cada montagem no sistema de arquivos, e conjuntos individuais no site As pastas bin são substituídas por links simbólicos para a única cópia. Se um site individual precisar de uma versão distinta do conjunto, o link simbólico será substituído pela nova versão do conjunto, e somente esse site será afetado.

Compartilhar montagens usando links simbólicos requer\_uma nova ferramenta chamada aspnet intern.exe, que permite criar e gerenciar a loja de montagens internas. Ele é fornecido como parte do Visual Studio 11 Developer Preview SDK. (No entanto, ele funcionará em um sistema que tenha apenas o .NET Framework 4 instalado, assumindo que você tenha instalado a [última atualização](https://support.microsoft.com/kb/2468871).)

Para garantir que todas as assembléias elegíveis tenham\_sido internadas, você executa aspnet intern.exe periodicamente (por exemplo, uma vez por semana como uma tarefa programada). Um uso típico é o seguinte:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

Para ver todas as opções, execute a ferramenta sem argumentos.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>Usando compilação JIT multi-Core para inicialização mais rápida

**Requisito**: .NET Framework 4.5

Para uma inicialização de site frio, não só os conjuntos precisam ser lidos a partir do disco, mas o site deve ser compilado pelo JIT. Para um site complexo, isso pode adicionar atrasos significativos. Uma nova técnica de uso geral no .NET Framework 4.5 reduz esses atrasos espalhando compilação JIT entre os núcleos de processador disponíveis. Ele faz isso tanto quanto possível usando informações coletadas durante os lançamentos anteriores do site. Essa funcionalidade implementada pelo método [System.Runtime.ProfileOptimization.StartProfile.](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)

A compilação jit usando vários núcleos é habilitada por padrão em ASP.NET, portanto, você não precisa fazer nada para tirar proveito desse recurso. Se você quiser desativar esse recurso, faça a seguinte configuração no arquivo Web.config:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>Afinando a coleta de lixo para otimizar a memória

**Requisito**: .NET Framework 4.5

Uma vez que um site está em execução, seu uso do monte coletor de lixo (GC) pode ser um fator significativo no seu consumo de memória. Como qualquer coletor de lixo, o .NET Framework GC faz compensações entre o tempo da CPU (frequência e significado das coleções) e o consumo de memória (espaço extra que é usado para objetos novos, livres ou livres). Para versões anteriores, fornecemos orientações sobre como configurar o CG para alcançar o equilíbrio certo (por exemplo, consulte [ASP.NET configuração de hospedagem compartilhada 2.0/3.5](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).

Para o .NET Framework 4.5, em vez de várias configurações autônomas, está disponível uma configuração de configuração definida pela carga de trabalho que permite todas as configurações de GC recomendadas anteriormente, bem como uma nova sintonia que oferece desempenho adicional para o conjunto de trabalho por local.

Para habilitar o ajuste de memória GC, adicione a seguinte configuração ao arquivo Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(Se você estiver familiarizado com a orientação anterior para alterações em aspnet.config, observe que esta configuração substitui as configurações antigas — por exemplo, não há necessidade de definir gcServer, gcConcurrent, etc. Você não precisa remover as configurações antigas.)

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>Pré-candidatos a aplicações web

**Requisito:**.NET Framework 4.5 em execução no Windows 8

Para várias versões, o Windows incluiu uma tecnologia conhecida como [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) que reduz o custo de leitura de disco da inicialização do aplicativo. Como a inicialização fria é um problema predominantemente para aplicativos clientes, essa tecnologia não foi incluída no Windows Server, que inclui apenas componentes essenciais para um servidor. Prefetching está agora disponível na versão mais recente do Windows Server, onde pode otimizar o lançamento de sites individuais.

Para o Windows Server, o prefetcher não está habilitado por padrão. Para ativar e configurar o prefetcher para hospedagem web de alta densidade, execute o seguinte conjunto de comandos na linha de comando:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

Em seguida, para integrar o prefetcher com ASP.NET aplicativos, adicione o seguinte ao arquivo Web.config:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>Web Forms do ASP.NET

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>Controles de dados fortemente tipados

Em ASP.NET 4.5, o Web Forms inclui algumas melhorias para trabalhar com dados. A primeira melhoria são os controles de dados fortemente digitados. Para controles de Formulários da Web em versões anteriores de ASP.NET, você exibe um valor vinculado a dados usando *Eval* e uma expressão de vinculação de dados:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

Para vinculação de dados bidirecionais, você usa *Bind*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

No tempo de execução, essas chamadas usam reflexão para ler o valor do membro especificado e, em seguida, exibir o resultado na marcação. Essa abordagem facilita a vinculação de dados contra dados arbitrários e não moldados.

No entanto, expressões de vinculação de dados como esta não suportam recursos como o IntelliSense para nomes de membros, navegação (como Go To Definition) ou verificação de tempo de compilação para esses nomes.

Para resolver esse problema, ASP.NET 4.5 adiciona a capacidade de declarar o tipo de dados dos dados aos que um controle está vinculado. Você faz isso usando a nova propriedade *ItemType.* Quando você define esta propriedade, duas novas variáveis digitadas estão disponíveis no escopo de expressões de vinculação de dados: *Item* e *BindItem*. Como as variáveis são fortemente digitadas, você tem todos os benefícios da experiência de desenvolvimento do Visual Studio.

Para expressões de vinculação de dados bidirecionais, use a variável *BindItem:*

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

A maioria dos controles no ASP.NET estrutura de Formulários da Web que suportam a vinculação de dados foram atualizados para suportar a propriedade *ItemType.*

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>Model binding

A vinculação do modelo estende a vinculação de dados em ASP.NET controles da Web Forms para funcionar com acesso a dados focados em código. Ele incorpora conceitos do controle *ObjectDataSource* e da vinculação do modelo em ASP.NET MVC.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>Selecionando dados

Para configurar um controle de dados para usar a vinculação do modelo para selecionar dados, você define a propriedade *SelectMethod* do controle para o nome de um método no código da página. O controle de dados chama o método no momento apropriado no ciclo de vida da página e vincula automaticamente os dados retornados. Não há necessidade de chamar explicitamente o método *DataBind.*

No exemplo a seguir, o controle *GridView* é configurado para usar um método chamado *GetCategories*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

Você cria o método *GetCategories* no código da página. Para uma operação simples de seleção, o método não precisa de parâmetros e deve retornar um objeto *IEnumeravel* ou *IQueryable.* Se a nova propriedade *ItemType* for definida (o que permite expressões de vinculação de dados fortemente digitadas, conforme explicado em Controles de [dados fortemente digitados anteriormente),](#_Toc318097386) as versões genéricas dessas interfaces devem ser devolvidas — *IEnumerable&lt;T&gt; * ou *IQueryable&lt;T&gt;*, com o parâmetro *T* correspondendo ao tipo da propriedade *ItemType* (por exemplo, Categoria *&lt;&gt;IQueryable*).

O exemplo a seguir mostra o código de um método *GetCategories.* Este exemplo usa o modelo Entity Framework Code First com o banco de dados de amostra northwind. O código garante que a consulta retorne detalhes dos produtos relacionados para cada categoria por meio do método *Incluir.* (Isso garante que o elemento *TemplateField* na marcação exiba a contagem de produtos em cada categoria sem exigir uma [seleção n+1](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

Quando a página é executada, o controle *GridView* chama o método *GetCategories* automaticamente e renderiza os dados retornados usando os campos configurados:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Como o método selecionado retorna um objeto *IQueryable,* o controle *GridView* pode manipular ainda mais a consulta antes de executá-la. Por exemplo, o controle *GridView* pode adicionar expressões de consulta para classificação e paginação ao objeto *IQueryable* retornado antes de ser executado, de modo que essas operações sejam executadas pelo provedor LINQ subjacente. Neste caso, o Entity Framework garantirá que essas operações sejam realizadas no banco de dados.

O exemplo a seguir mostra o controle *GridView* modificado para permitir a classificação e paginação:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

Agora, quando a página é executada, o controle pode certificar-se de que apenas a página atual de dados é exibida e que ela é ordenada pela coluna selecionada:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

Para filtrar os dados retornados, os parâmetros devem ser adicionados ao método selecionado. Esses parâmetros serão preenchidos pela vinculação do modelo em tempo de execução, e você pode usá-los para alterar a consulta antes de retornar os dados.

Por exemplo, suponha que você deseja permitir que os usuários filtreprodutos inserindo uma palavra-chave na seqüência de consultas. Você pode adicionar um parâmetro ao método e atualizar o código para usar o valor do parâmetro:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

Este código inclui uma expressão *Onde* se um valor for fornecido para *palavra-chave* e, em seguida, retorna os resultados da consulta.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>Provedores de valor

O exemplo anterior não era específico sobre de onde vinha o valor do parâmetro *da palavra-chave.* Para indicar essas informações, você pode usar um atributo de parâmetro. Para este exemplo, você pode usar a classe *QueryStringAttribute* que está no espaço de nome *System.Web.ModelBinding:*

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

Isso instrui a vinculação do modelo para tentar vincular um valor da seqüência de consultas ao parâmetro *de palavra-chave* no tempo de execução. (Isso pode envolver a realização de conversão de tipo, embora não neste caso.) Se um valor não puder ser fornecido e o tipo não for anulado, uma exceção será lançada.

As fontes de valores desses métodos são referidas como provedores de valor, e os atributos de parâmetro que indicam qual provedor de valor usar são referidos como atributos de provedor de valor. Os Formulários da Web incluirão provedores de valor e atributos correspondentes para todas as fontes típicas de entrada do usuário em um aplicativo do Web Forms, como a seqüência de consultas, cookies, valores de formulário, controles, estado de exibição, estado de sessão e propriedades de perfil. Você também pode escrever provedores de valor personalizados.

Por padrão, o nome do parâmetro é usado como a chave para encontrar um valor na coleção do provedor de valor. No exemplo, o código procurará um valor de seqüência de consulta chamado palavra-chave (por exemplo, ~/default.aspx?keyword=chef). Você pode especificar uma chave personalizada passando-a como um argumento para o atributo parâmetro. Por exemplo, para usar o valor da variável de seqüência de consultas chamada q, você pode fazer isso:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

Se este método estiver no código da página, os usuários podem filtrar os resultados passando uma palavra-chave usando a seqüência de consultas:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

A vinculação do modelo realiza muitas tarefas que de outra forma você teria que codificar manualmente: ler o valor, verificar um valor nulo, tentar convertê-lo para o tipo apropriado, verificar se a conversão foi bem sucedida e, finalmente, usar o valor na consulta. A vinculação do modelo resulta em muito menos código e na capacidade de reutilizar a funcionalidade em toda a sua aplicação.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>Filtragem por valores de um controle

Suponha que você queira estender o exemplo para permitir que o usuário escolha um valor de filtro de uma lista de baixa. Adicione a seguinte lista de paradas à marcação e configure-a para obter seus dados de outro método usando a propriedade *SelectMethod:*

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

Normalmente, você também adicionaria um elemento *EmptyDataTemplate* ao controle *GridView* para que o controle exiba uma mensagem se nenhum produto correspondente for encontrado:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

No código da página, adicione o novo método select para a lista de paradas:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

Finalmente, atualize o método *getProducts* select para obter um novo parâmetro que contenha o ID da categoria selecionada na lista de parada:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

Agora, quando a página é executada, os usuários podem selecionar uma categoria na lista suspensa e o controle *GridView* é automaticamente revinculado para mostrar os dados filtrados. Isso é possível porque a vinculação do modelo rastreia os valores dos parâmetros para métodos selecionados e detecta se algum valor de parâmetro foi alterado após um postback. Nesse caso, a vinculação do modelo força o controle de dados associado a se revincular aos dados.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>Expressões codificadas de dados codificadas por HTML

Agora você pode codificar HTML o resultado de expressões de vinculação de dados. Adicione um cólon (:) até o final &lt;do prefixo %# que marca a expressão de vinculação de dados:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>Validação Discreta

Agora você pode configurar os controles de validador incorporados para usar javaScript discreto para lógica de validação do lado do cliente. Isso reduz significativamente a quantidade de JavaScript renderizado inline na marcação da página e reduz o tamanho geral da página. Você pode configurar javascript discreto para controles de validador em qualquer uma dessas maneiras:

- Globalmente, adicionando a * &lt;&gt; * seguinte configuração ao elemento AppSettings no arquivo Web.config: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- Globalmente, definindo a propriedade *Static System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* para *UnobtrusiveValidationMode.WebForms* (normalmente no método *Iniciar de aplicativos\_* no arquivo Global.asax).
- Individualmente para uma página, definindo a nova propriedade *UnobtrusiveValidationMode* da classe *Page* para *UnobtrusiveValidationMode.WebForms*.

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>Atualizações HTML5

Algumas melhorias foram feitas nos controles de servidor do Web Forms para aproveitar os novos recursos do HTML5:

- A propriedade *TextMode* do controle *TextBox* foi atualizada para suportar os novos tipos de entrada HTML5, como *e-mail,* *datae*e assim por diante.
- O controle *FileUpload* agora suporta vários uploads de arquivos de navegadores que suportam esse recurso HTML5.
- Os controles do validador agora suportam a validação de elementos de entrada HTML5.
- Novos elementos HTML5 que têm atributos que representam uma URL agora suportam runat="server". Como resultado, você pode usar ASP.NET convenções em caminhos de URL, como &lt;o ~ operador para representar a raiz do aplicativo (por&gt;exemplo, video runat="server" src="~/myVideo.wmv" / ).
- O controle *UpdatePanel* foi corrigido para suportar a postagem de campos de entrada HTML5.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta está agora incluído com visual studio 11 Beta. ASP.NET MVC é uma estrutura para o desenvolvimento de aplicações Web altamente testados e manecíveis, aproveitando o padrão Model-View-Controller (Model-View-Controller). ASP.NET MVC 4 facilita a construção de aplicativos para a Web móvel e inclui ASP.NET API web, que ajuda você a criar serviços HTTP que podem chegar a qualquer dispositivo. Para obter mais informações, consulte o [ASP.NET Notas de Versão MVC 4](mvc4-release-notes.md).

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>Páginas da Web do ASP.NET 2

Os novos recursos incluem o seguinte:

- Novos e atualizados modelos de site.
- Adicionando validação do lado do servidor e do lado do cliente usando o ajudante *de validação.*
- A capacidade de registrar scripts usando um gerenciador de ativos.
- Habilitando logins do Facebook e outros sites usando OAuth e OpenID.
- Adicionando mapas usando o ajudante do *Maps.*
- Executando aplicativos páginas da Web lado a lado.
- Renderização de páginas para dispositivos móveis.

Para obter mais informações sobre esses recursos e exemplos de código de página inteira, consulte [Os principais recursos nas páginas da Web 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 Beta

Esta seção fornece informações sobre melhorias para o desenvolvimento web no Visual Web Developer 11 Beta e Visual Studio 2012 Release Candidate.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Compartilhamento de projetos entre o Visual Studio 2010 e o Candidato de Lançamento do Visual Studio 2012 (Compatibilidade do Projeto)

Até o Visual Studio 2012 Release Candidate, abrindo um projeto existente em uma versão mais recente do Visual Studio lançou o Assistente de Conversão. Isso forçou uma atualização do conteúdo (ativos) de um projeto e solução para novos formatos que não eram compatíveis com o retrocesso. Portanto, após a conversão você não poderia abrir o projeto na versão mais antiga do Visual Studio.

Muitos clientes nos disseram que essa não era a abordagem correta. No Visual Studio 11 Beta, agora apoiamos o compartilhamento de projetos e soluções com o Visual Studio 2010 SP1. Isso significa que se você abrir um projeto de 2010 no Visual Studio 2012 Release Candidate, você ainda poderá abrir o projeto no Visual Studio 2010 SP1.

> [!NOTE]
> Alguns tipos de projetos não podem ser compartilhados entre o Visual Studio 2010 SP1 e o Visual Studio 2012 Release Candidate. Estes incluem alguns projetos mais antigos (como ASP.NET projetos MVC 2) ou projetos para fins especiais (como projetos de setup).

Quando você abre um projeto Web do Visual Studio 2010 SP1 pela primeira vez no Visual Studio 11 Beta, as seguintes propriedades são adicionadas ao arquivo do projeto:

- FileUpgradeFlags
- UpgradeBackupBackupLocalização
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags, UpgradeBackupLocation e OldToolsVersion são usados pelo processo que atualiza o arquivo do projeto. Eles não têm impacto em trabalhar com o projeto no Visual Studio 2010.

VisualStudioVersion é uma nova propriedade usada pelo MSBuild 4.5 que indica a versão do Visual Studio para o projeto atual. Como essa propriedade não existia no MSBuild 4.0 (a versão do MSBuild que o Visual Studio 2010 SP1 usa), injetamos um valor padrão no arquivo do projeto.

A propriedade VSToolsPath é usada para determinar o arquivo .targets correto para importar do caminho representado pela configuração MSBuildExtensionsPath32.

Há também algumas alterações relacionadas aos elementos de importação. Essas alterações são necessárias para suportar a compatibilidade entre ambas as versões do Visual Studio.

> [!NOTE]
> Se um projeto está sendo compartilhado entre o Visual Studio 2010 SP1 e o Visual Studio 11\_Beta em dois computadores diferentes, e se o projeto incluir um banco de dados local na pasta Dados do Aplicativo, você deve ter certeza de que a versão do SQL Server usada pelo banco de dados está instalada em ambos os computadores.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>Alterações de configuração em ASP.NET 4.5 Modelos de sites

As seguintes alterações foram feitas no arquivo *Web.config* padrão para o site que são criados usando modelos de site no Visual Studio 2012 Release Candidate:

- No `<httpRuntime>` elemento, `encoderType` o atributo agora é definido por padrão para usar os tipos AntiXSS que foram adicionados ao ASP.NET. Para obter detalhes, consulte [Biblioteca AntiXSS](#_Toc318097382).
- Também no `<httpRuntime>` elemento, `requestValidationMode` o atributo é definido como "4.5". Isso significa que, por padrão, a validação da solicitação está configurada para usar validação diferida ("preguiçosa"). Para obter detalhes, consulte [Novos recursos de validação de solicitações de solicitações de ASP.NET](#_Toc318097379).
- O `<modules>` elemento `<system.webServer>` da seção `runAllManagedModulesForAllRequests` não contém um atributo. (Seu valor padrão é falso.) Isso significa que se você estiver usando uma versão do IIS 7 que não foi atualizada para o SP1, você pode ter problemas com roteamento em um novo site. Para obter mais informações, consulte [suporte nativo no IIS 7 para roteamento de ASP.NET](#Native_Support_In_IIS7_For_ASPNET_Routine).

Essas alterações não afetam os aplicativos existentes. No entanto, eles podem representar uma diferença de comportamento entre sites existentes e novos sites que você cria para ASP.NET 4.5 usando os novos modelos.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>Suporte nativo no IIS 7 para roteamento de ASP.NET

Esta não é uma mudança para ASP.NET como tal, mas uma mudança nos modelos de novos projetos de sites que pode afetá-lo se você estiver trabalhando em uma versão do IIS 7 que não teve a atualização do SP1 aplicada.

Em ASP.NET, você pode adicionar a seguinte configuração aos aplicativos para suportar o roteamento:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

Quando **runAllManagedModulesForAllRequests** é verdade, `http://mysite/myapp/home` um URL like vai para ASP.NET, mesmo que não haja nenhuma extensão *.aspx*, *.mvc*ou similar na URL.

Uma atualização que foi feita no IIS 7 torna a **configuração runAllManagedModulesForAllRequests** desnecessária e suporta ASP.NET roteamento nativamente. (Para obter informações sobre a atualização, consulte o artigo do Suporte da Microsoft [Uma atualização está disponível que permite que certos manipuladores IIS 7.0 ou IIS 7.5 lidem com solicitações cujos URLs não terminem com um período](https://support.microsoft.com/kb/980368).)

Se o seu site estiver sendo executado no IIS 7 e se o IIS tiver sido atualizado, você não precisará definir **runAllManagedModulesForAllRequests** para true. Na verdade, defini-lo como verdadeiro não é recomendado, porque adiciona sobrecarga de processamento desnecessária à solicitação. Quando essa configuração for verdadeira, todas as solicitações, incluindo as de *.htm*, *.jpg*e outros arquivos estáticos, também passam pelo pipeline de solicitação de ASP.NET.

Se você criar um novo site ASP.NET 4.5 usando os modelos fornecidos no Visual Studio 2012 RC, a configuração para o site não inclui a configuração **runAllManagedModulesForAllRequests.** Isso significa que, por padrão, a configuração é falsa.

Se você executar o site no Windows 7 sem o SP1 instalado, o IIS 7 não incluirá a atualização necessária. Como conseqüência, o roteamento não funcionará e você verá erros. Se você tem um problema onde o roteamento não funciona, você pode fazer o seguinte:

- Atualize o Windows 7 para o SP1, que adicionará a atualização ao IIS 7.
- Instale a atualização descrita no artigo do Microsoft Support listado anteriormente.
- Definir **runAllManagedModulesForAllRequests** true no arquivo Web.config desse site. Observe que isso adicionará algumas despesas gerais às solicitações.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>Editor de HTML

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>Tarefas inteligentes

Na exibição Design, propriedades complexas dos controles de servidor geralmente têm caixas de diálogo associadas e assistentes para facilitar a sua configuração. Por exemplo, você pode usar uma caixa de diálogo especial para adicionar uma fonte de dados a um controle *do Repeater* ou adicionar colunas a um controle *GridView.*

No entanto, esse tipo de ajuda de iu para propriedades complexas não está disponível na exibição Origem. Portanto, o Visual Studio 11 introduz tarefas inteligentes para visualização de origem. Tarefas inteligentes são atalhos de reconhecimento de contexto para recursos comumente usados nos editores C# e Visual Basic.

Para ASP.NET controles de Formulários da Web, as Tarefas Inteligentes aparecem nas tags do servidor como um pequeno glifo quando o ponto de inserção está dentro do elemento:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

A tarefa inteligente se expande quando você clica no glifo ou pressiona CTRL+. (dot), assim como nos editores de código. Em seguida, ele exibe atalhos semelhantes à exibição Tarefas Inteligentes no Design.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

Por exemplo, a Tarefa Inteligente na ilustração anterior mostra as opções De tarefas do GridView. Se você escolher Editar colunas, a seguinte caixa de diálogo será exibida:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

O preenchimento da caixa de diálogo define as mesmas propriedades que você pode definir na exibição Design. Quando você clica em OK, a marcação para o controle é atualizada com as novas configurações:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>Suporte wai-aria

Escrever sites acessíveis está se tornando cada vez mais importante. O [padrão de acessibilidade WAI-ARIA](http://www.w3.org/WAI/intro/aria) define como os desenvolvedores devem escrever sites acessíveis. Este padrão agora é totalmente suportado no Visual Studio.

Por exemplo, o atributo de *função* agora tem o IntelliSense completo:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

O padrão WAI-ARIA também introduz atributos que são prefixados com *aria-* que permitem adicionar semântica a um documento HTML5. O Visual Studio também suporta totalmente esses atributos *de ária:*

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>Novos trechos HTML5

Para torná-lo mais rápido e fácil de escrever marcação HTML5 comumente usada, o Visual Studio inclui uma série de trechos. Um exemplo é o trecho de vídeo:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

Para invocar o trecho, pressione Tab duas vezes quando o elemento estiver selecionado no IntelliSense:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

Isso produz um trecho que você pode personalizar.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>Extrair para o controle do usuário

Em grandes páginas da Web, pode ser uma boa ideia mover peças individuais para controles de usuário. Essa forma de refatoração pode ajudar a aumentar a legibilidade da página e pode simplificar a estrutura da página.

Para facilitar isso, ao editar páginas da Web Forms na exibição Origem, agora você pode selecionar texto em uma página, clicar com o botão direito do mouse e, em seguida, escolher Extrair para Controle do Usuário:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>IntelliSense para nuggets de código em atributos

O Visual Studio sempre forneceu o IntelliSense para nuggets de código do lado do servidor em qualquer página ou controle. Agora o Visual Studio inclui o IntelliSense para nuggets de código em atributos HTML também.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

Isso facilita a criação de expressões vinculativas de dados:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>Renomeação automática da tag correspondente quando você renomear uma tag de abertura ou fechamento

Se você renomear um elemento HTML (por exemplo, você alterar uma tag *div* para ser uma tag *de cabeçalho),* a tag de abertura ou fechamento correspondente também será alterado em tempo real.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

Isso ajuda a evitar o erro onde você esquece de alterar uma tag de fechamento ou alterar a errada.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>Geração de manipuladores de eventos

O Visual Studio agora inclui recursos na exibição Origem para ajudá-lo a escrever manipuladores de eventos e vinculá-los manualmente. Se você estiver editando um nome de evento &lt;na&gt;exibição Origem, o IntelliSense exibirá Criar novo evento, o que criará um manipulador de eventos no código da página que tenha a assinatura certa:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

Por padrão, o manipulador de eventos usará o ID do controle para o nome do método de manipulação de eventos:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

O manipulador de eventos resultante será assim (neste caso, em C#):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>Recuo inteligente

Quando você pressiona Enter enquanto estiver dentro de um elemento HTML vazio, o editor colocará o ponto de inserção no lugar certo:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

Se você pressionar Enter neste local, a tag de fechamento é movida para baixo e recuada para corresponder à tag de abertura. O ponto de inserção também é recuado:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>Reduzir automaticamente a conclusão da declaração

A lista IntelliSense no Visual Studio agora filtra com base no que você digita para que ele exiba apenas opções relevantes:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

O IntelliSense também filtra com base no caso de título das palavras individuais na lista IntelliSense. Por exemplo, se você digitar "dl", tanto dl quanto asp:DataList serão exibidos:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

Esse recurso torna mais rápido obter a conclusão da declaração para elementos conhecidos.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>Editor JavaScript

O editor JavaScript no Visual Studio 2012 Release Candidate é completamente novo e melhora muito a experiência de trabalhar com JavaScript no Visual Studio.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>Estrutura de tópicos de código

As regiões delineamento agora são criadas automaticamente para todas as funções, permitindo que você colapse partes do arquivo que não são pertinentes ao seu foco atual.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>Correspondência de chaves

Quando você coloca o ponto de inserção em uma cinta de abertura ou fechamento, o editor destaca o correspondente.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>Ir para Definição

O comando Ir para Definição permite que você pule para a fonte de uma função ou variável.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>Suporte ao ECMAScript5

O editor suporta a nova sintaxe e APIs no ECMAScript5, a versão mais recente do padrão que descreve a linguagem JavaScript.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

O IntelliSense for DOM APIs foi aprimorado, com suporte para muitas novas APIs HTML5, incluindo *querySelector,* DOM Storage, mensagens entre documentos e *tela*. O DOM IntelliSense agora é impulsionado por um único arquivo JavaScript simples, em vez de por uma definição de biblioteca de tipo nativo. Isso facilita a extensão ou substituição.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>Sobrecargas de assinatura VSDOC

Comentários detalhados do IntelliSense agora podem ser declarados para sobrecargas separadas de funções JavaScript usando o novo * &lt;&gt; * elemento de assinatura, como mostrado neste exemplo:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>Referências implícitas

Agora você pode adicionar arquivos JavaScript a uma lista central que será implicitamente incluída na lista de arquivos que qualquer arquivo JavaScript ou referências de bloco, o que significa que você receberá o IntelliSense para seu conteúdo. Por exemplo, você pode adicionar arquivos jQuery à lista central de arquivos, e você obterá intelliSense para funções jQuery em qualquer bloco &lt;javaScript de arquivo, quer você tenha referenciado explicitamente (usando /// referência /&gt;) ou não.

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>Editor de CSS

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>Reduzir automaticamente a conclusão da declaração

A lista IntelliSense para CSS agora filtra com base nas propriedades e valores CSS suportados pelo esquema selecionado.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

O IntelliSense também suporta pesquisas de casos de título:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>Recuo hierárquico

O editor CSS usa recuo para exibir regras hierárquicas, o que lhe dá uma visão geral de como as regras em cascata são logicamente organizadas. No exemplo a seguir, o #list um seletor é uma criança em cascata da lista e, portanto, é recuado.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

O exemplo a seguir mostra herança mais complexa:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

O recuo de uma regra é determinado pelas regras dos pais. O recuo hierárquico é habilitado por padrão, mas você pode desabilitá-lo na caixa de diálogo Opções (Ferramentas, Opções da barra de menu):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>Suporte a hacks CSS

A análise de centenas de arquivos CSS do mundo real mostra que os hacks do CSS são muito comuns, e agora o Visual Studio suporta os mais usados. Este suporte inclui intelliSense e validação\*da estrela\_( ) e sublinhar () hacks de propriedade:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

Hacks típicos de seletores também são suportados para que o recuo hierárquico seja mantido mesmo quando eles são aplicados. Um hack típico de seletor usado para atingir o Internet Explorer 7 é preparar um seletor com * \*:first-child + html*. Usar essa regra manterá o recuo hierárquico:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>Esquemas específicos do fornecedor (-moz-, -webkit)

CSS3 introduz muitas propriedades que foram implementadas por diferentes navegadores em diferentes momentos. Isso anteriormente forçou os desenvolvedores a codificar para navegadores específicos usando sintaxe específica do fornecedor. Essas propriedades específicas do navegador estão agora incluídas no IntelliSense.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>Comentando e sem comentários suporte

Agora você pode comentar e descomentar as regras do CSS usando os mesmos atalhos que você usa no editor de código (Ctrl+K,C para comentar e Ctrl+K,você para descomentar).

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Seletor de cor

Nas versões anteriores do Visual Studio, o IntelliSense para atributos relacionados a cores consistia em uma lista suspensa de valores de cor nomeados. Essa lista foi substituída por um seletor de cores completo.

Quando você digita um valor de cor, o seletor de cores é exibido automaticamente e apresenta uma lista de cores usadas anteriormente seguidas por uma paleta de cores padrão. Você pode selecionar uma cor usando o mouse ou o teclado.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

A lista pode ser expandida para um seletor de cores completo. O seletor permite controlar o canal alfa convertendo automaticamente qualquer cor em RGBA quando você move o controle deslizante de opacidade:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>Snippets

Os trechos no editor CSS tornam mais fácil e rápido criar estilos entre navegadores. Muitas propriedades CSS3 que requerem configurações específicas do navegador foram agora enroladas em trechos.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

Os trechos do CSS suportam cenários avançados (como consultas de mídia CSS3) digitando o símbolo (@), que mostra a lista IntelliSense.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

Quando você @media seleciona valor e pressiona Guia, o editor CSS insere o seguinte trecho:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

Como com trechos de código, você pode criar seus próprios trechos de CSS.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>Regiões aduaneiras

Regiões de código nomeadas, que já estão disponíveis no editor de código, agora estão disponíveis para edição do CSS. Isso permite que você agrupe facilmente blocos de estilo relacionados.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

Quando uma região é colapsada, ela exibe o nome da região:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Inspetor de Página

Page Inspector é uma ferramenta que renderiza uma página da Web (HTML, Formulários da Web, ASP.NET MVC ou Páginas da Web) no Visual Studio IDE e permite examinar tanto o código-fonte quanto a saída resultante. Para ASP.NET páginas, o Page Inspector permite determinar qual código do lado do servidor produziu a marcação HTML que é renderizada no navegador.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

Para obter mais informações sobre o Page Inspector, consulte os seguintes tutoriais:

- Usando o Page Inspector em [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)
- Usando o Page Inspector em [formulários ASP.NET Web](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)

<a id="_Toc318097425"></a>
### <a name="publishing"></a>Publicação

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>Perfis de publicação

No Visual Studio 2010, a publicação de informações para projetos de aplicativos web não é armazenada no controle de versão e não foi projetada para compartilhar com outras pessoas. No Visual Studio 2012 Release Candidate, o formato do perfil de publicação foi alterado. Ele foi feito um artefato de equipe, e agora é fácil de aproveitar a partir de compilações baseadas no MSBuild. As informações de configuração de compilação estão na caixa de diálogo Publicar para que você possa alternar facilmente as configurações de compilação antes de publicar.

Os perfis de publicação são armazenados na pasta PublishProfiles. A localização da pasta depende da linguagem de programação que você está usando:

- C#: Propriedades\Publicarperfis
- Visual Basic: Meu Projeto\PublishProfiles

Cada perfil é um arquivo MSBuild. Durante a publicação, este arquivo é importado para o arquivo MSBuild do projeto. No Visual Studio 2010, se você quiser fazer alterações no processo de publicação ou pacote, você tem que colocar suas personalizações em um arquivo chamado **ProjectName**.wpp.targets. Isso ainda é suportado, mas agora você pode colocar suas personalizações no próprio perfil de publicação. Dessa forma, as personalizações serão usadas apenas para esse perfil.

Agora você também pode aproveitar os perfis de publicação do MSBuild. Para isso, use o seguinte comando ao construir o projeto:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

O valor project.csproj é o caminho do projeto, e ProfileName é o nome do perfil a ser publicado. Alternativamente, em vez de passar o nome do perfil para a propriedade *PublishProfile,* você pode passar no caminho completo para o perfil de publicação.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET pré-compilação e fusão

Para projetos de aplicativos da Web, o Visual Studio 2012 Release Candidate adiciona uma opção na página De propriedades do Pacote/Publicação da Web que permite pré-compilar e mesclar o conteúdo do seu site quando publicar ou empacotar o projeto. Para ver essas opções, clique com o botão direito do mouse no projeto no Solution Explorer, escolha Propriedades e escolha a página De propriedade Pacote/Publicar a Web. A ilustração a seguir mostra o Precompilar este aplicativo antes da opção de publicação.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

Quando esta opção é selecionada, o Visual Studio precompila o aplicativo sempre que você publica ou empacota o aplicativo web. Se você quiser controlar como o site é pré-compilado ou como os conjuntos são mesclados, clique no botão Avançado para configurar essas opções.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

O servidor web padrão para testar projetos web no Visual Studio agora é o IIS Express. O Visual Studio Development Server ainda é uma opção para servidor web local durante o desenvolvimento, mas o IIS Express agora é o servidor recomendado. A experiência de usar o IIS Express no Visual Studio 11 Beta é muito semelhante ao de usá-lo no Visual Studio 2010 SP1.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>Isenção de responsabilidade

Este é um documento preliminar e pode ser alterado substancialmente antes da versão comercial final do software descrito aqui.

As informações contidas neste documento representam a visão atual da Microsoft Corporation acerca das questões discutidas até a data da publicação. Como a Microsoft deve reagir às dinâmicas condições do mercado, essas informações não devem ser interpretadas como um compromisso por parte da Microsoft e a Microsoft não garante a precisão de qualquer informação apresentada após a data de publicação.

Este whitepaper é apenas para fins informativos. A MICROSOFT NÃO OFERECE GARANTIA, EXPRESSA, IMPLÍCITA OU ESTATUTÁRIA, DAS INFORMAÇÕES CONTIDAS NESTE DOCUMENTO.

Obedecer a todas as leis de direitos autorais aplicáveis é responsabilidade do usuário. Sem limitar os direitos autorais, nenhuma parte deste documento pode ser reproduzida, armazenada ou introduzida em um sistema de recuperação, ou transmitida de qualquer forma ou por qualquer meio (seja eletrônico, mecânico, fotocópia, gravação ou outro), ou para qualquer finalidade, sem a permissão expressa e por escrito da Microsoft Corporation.

A Microsoft pode ter patentes ou requisições para obtenção de patente, marcas comerciais, direitos autorais ou outros direitos de propriedade intelectual que abrangem o conteúdo deste documento. A posse deste documento não lhe confere nenhum direito sobre patentes, marcas comerciais, direitos autorais ou outros direitos de propriedade intelectual, salvo aqueles expressamente mencionados em um contrato de licença, por escrito, da Microsoft.

Salvo observação em contrário, o exemplo de empresas, organizações, produtos, nomes de domínio, endereços de e-mail, logotipos, pessoas, lugares e eventos aqui descritos são fictícios, e nenhuma associação com qualquer empresa real, organização, produto, nome de domínio, endereço de e-mail, logotipo, pessoa, local ou evento é pretendida ou deve ser inferida.

© 2012 Microsoft Corporation. Todos os direitos reservados.

Microsoft e Windows são marcas registradas ou comerciais da Microsoft Corporation nos Estados Unidos e/ou em outros países.

Os nomes de empresas reais e produtos mencionados aqui podem ser marcas comerciais de seus respectivos proprietários.
