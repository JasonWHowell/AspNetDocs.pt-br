---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: Entendendo os serviços Web do ASP.NET AJAX | Microsoft Docs
author: scottcate
description: Os serviços Web são parte integrante do .NET Framework que fornecem uma solução de plataforma cruzada para a troca de dados entre sistemas distribuídos. Embora Web...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/12/2020
ms.locfileid: "86162732"
---
# <a name="understanding-aspnet-ajax-web-services"></a>Noções básicas sobre os serviços Web do AJAX ASP.NET

por [Scott Cate](https://github.com/scottcate)

[Baixar PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Os serviços Web são parte integrante do .NET Framework que fornecem uma solução de plataforma cruzada para a troca de dados entre sistemas distribuídos. Embora os serviços Web normalmente sejam usados para permitir diferentes sistemas operacionais, modelos de objeto e linguagens de programação para enviar e receber dados, eles também podem ser usados para injetar dados dinamicamente em uma página do ASP.NET AJAX ou enviar dados de uma página para um sistema back-end. Tudo isso pode ser feito sem recorrer a operações de postback.

## <a name="calling-web-services-with-aspnet-ajax"></a>Chamando serviços Web com o ASP.NET AJAX

Dan Wahlin

Os serviços Web são parte integrante do .NET Framework que fornecem uma solução de plataforma cruzada para a troca de dados entre sistemas distribuídos. Embora os serviços Web normalmente sejam usados para permitir diferentes sistemas operacionais, modelos de objeto e linguagens de programação para enviar e receber dados, eles também podem ser usados para injetar dados dinamicamente em uma página do ASP.NET AJAX ou enviar dados de uma página para um sistema back-end. Tudo isso pode ser feito sem recorrer a operações de postback.

Embora o controle ASP.NET AJAX UpdatePanel forneça uma maneira simples de habilitar qualquer página de ASP.NET em AJAX, pode haver ocasiões em que você precisa acessar dados dinamicamente no servidor sem usar um UpdatePanel. Neste artigo, você verá como fazer isso criando e consumindo serviços Web em páginas do ASP.NET AJAX.

Este artigo se concentrará na funcionalidade disponível nas principais extensões do AJAX ASP.NET, bem como um controle habilitado de serviço Web no kit de ferramentas AJAX ASP.NET chamado AutoCompleteExtender. Os tópicos abordados incluem a definição de serviços Web habilitados para AJAX, a criação de proxies de cliente e a chamada de serviços Web com o JavaScript. Você também verá como as chamadas de serviço Web podem ser feitas diretamente em métodos de página ASP.NET.

## <a name="web-services-configuration"></a>Configuração de serviços Web

Quando um novo projeto de site é criado com o Visual Studio 2008, o arquivo de web.config tem várias novas adições que podem não ser familiares aos usuários de versões anteriores do Visual Studio. Algumas dessas modificações mapeiam o prefixo "ASP" para controles ASP.NET AJAX para que possam ser usadas em páginas enquanto outras definem HttpHandlers e HttpModules necessários. A listagem 1 mostra as modificações feitas no `<httpHandlers>` elemento no web.config que afeta chamadas de serviço Web. O HttpHandler padrão usado para processar chamadas. asmx é removido e substituído por uma classe ScriptHandlerFactory localizada no assembly System.Web.Extensions.dll. System.Web.Extensions.dll contém toda a funcionalidade básica usada pelo ASP.NET AJAX.

**Listagem 1. Configuração do manipulador de serviço Web do ASP.NET AJAX**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

Essa substituição de HttpHandler é feita para permitir que chamadas de JavaScript Object Notation (JSON) sejam feitas de páginas AJAX ASP.NET para serviços Web .NET usando um proxy de serviço Web JavaScript. O ASP.NET AJAX envia mensagens JSON para serviços da Web, em oposição às chamadas SOAP (Simple Object Access Protocol) padrão normalmente associadas aos serviços da Web. Isso resulta em uma menor mensagem de solicitação e resposta em geral. Ele também permite um processamento mais eficiente do lado do cliente de dados, já que a biblioteca JavaScript do ASP.NET AJAX é otimizada para trabalhar com objetos JSON. A listagem 2 e a listagem 3 mostram exemplos de mensagens de solicitação e resposta de serviço Web serializadas para o formato JSON. A mensagem de solicitação mostrada na Listagem 2 passa um parâmetro de país com um valor de "Bélgica", enquanto a mensagem de resposta na Listagem 3 passa uma matriz de objetos Customer e suas propriedades associadas.

**Listagem 2. Mensagem de solicitação de serviço Web serializada para JSON**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>[!NOTE]o nome da operação é definido como parte da URL para o serviço Web; além disso, as mensagens de solicitação nem sempre são enviadas via JSON. Os serviços Web podem utilizar o atributo ScriptMethod com o parâmetro UseHttpGet definido como true, o que faz com que os parâmetros sejam passados por meio de parâmetros de cadeia de caracteres de consulta.*

**Listagem 3. Mensagem de resposta do serviço Web serializada para JSON**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

Na próxima seção, você verá como criar serviços Web capazes de manipular mensagens de solicitação JSON e responder com tipos simples e complexos.

## <a name="creating-ajax-enabled-web-services"></a>Criando Serviços Web habilitados para AJAX

A estrutura do ASP.NET AJAX fornece várias maneiras diferentes de chamar serviços da Web. Você pode usar o controle AutoCompleteExtender (disponível no kit de ferramentas AJAX do ASP.NET) ou JavaScript. No entanto, antes de chamar um serviço que você tem para AJAX, habilite-o para que ele possa ser chamado pelo código de script de cliente.

Independentemente de você ser novo no ASP.NET Web Services, você descobrirá que é simples criar e habilitar serviços AJAX. O .NET Framework tem suporte para a criação de serviços Web do ASP.NET desde sua versão inicial em 2002 e as extensões do ASP.NET AJAX fornecem funcionalidades adicionais do AJAX que se baseiam no conjunto de recursos padrão do .NET Framework. O Visual Studio .NET 2008 Beta 2 tem suporte interno para a criação de arquivos de serviço Web. asmx e automaticamente deriva o código associado ao lado das classes da classe System. Web. Services. WebService. Ao adicionar métodos à classe, você deve aplicar o atributo WebMethod para que eles sejam chamados por consumidores do serviço Web.

A listagem 4 mostra um exemplo de como aplicar o atributo WebMethod a um método chamado GetCustomersByCountry ().

**Listagem 4. Usando o atributo WebMethod em um serviço Web**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

O método GetCustomersByCountry () aceita um parâmetro country e retorna uma matriz de objeto Customer. O valor de país passado para o método é encaminhado para uma classe de camada de negócios que, por sua vez, chama uma classe de camada de dados para recuperar os dados do banco, preencher as propriedades de objeto do cliente com dados e retornar a matriz.

## <a name="using-the-scriptservice-attribute"></a>Usando o atributo ScriptService

Embora adicionar o atributo WebMethod permita que o método GetCustomersByCountry () seja chamado por clientes que enviam mensagens SOAP padrão para o serviço Web, ele não permite que chamadas JSON sejam feitas de aplicativos do ASP.NET AJAX prontos para uso. Para permitir que chamadas JSON sejam feitas, você precisa aplicar o atributo da extensão AJAX ASP.NET `ScriptService` à classe de serviço Web. Isso permite que um serviço Web envie mensagens de resposta formatadas usando JSON e permite que o script do lado do cliente chame um serviço enviando mensagens JSON.

A listagem 5 mostra um exemplo de aplicação do atributo ScriptService a uma classe de serviço da Web chamada CustomersService.

**Listagem 5. Usando o atributo ScriptService para habilitar o AJAX em um serviço Web**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

O atributo ScriptService atua como um marcador que indica que ele pode ser chamado a partir do código de script AJAX. Na verdade, ele não lida com nenhuma das tarefas de serialização ou desserialização JSON que ocorrem nos bastidores. O ScriptHandlerFactory (configurado no web.config) e outras classes relacionadas fazem a maior parte do processamento de JSON.

## <a name="using-the-scriptmethod-attribute"></a>Usando o atributo ScriptMethod

O atributo ScriptService é o único atributo ASP.NET AJAX que precisa ser definido em um serviço Web .NET para que ele seja usado por páginas do ASP.NET AJAX. No entanto, outro atributo chamado ScriptMethod também pode ser aplicado diretamente aos métodos da Web em um serviço. ScriptMethod define três propriedades `UseHttpGet` , incluindo `ResponseFormat` e `XmlSerializeString` . Alterar os valores dessas propriedades pode ser útil nos casos em que o tipo de solicitação aceita por um método da Web precisa ser alterado para GET, quando um método da Web precisa retornar dados XML brutos na forma de um `XmlDocument` `XmlElement` objeto ou ou quando os dados retornados de um serviço devem ser sempre serializados como XML em vez de JSON.

A propriedade UseHttpGet pode ser usada quando um método da Web deve aceitar solicitações GET em oposição às solicitações POST. As solicitações são enviadas usando uma URL com parâmetros de entrada de método da Web convertidos em parâmetros de QueryString. A propriedade UseHttpGet assume como padrão false e só deve ser definida como `true` quando as operações são conhecidas como seguras e quando dados confidenciais não são passados para um serviço Web. A listagem 6 mostra um exemplo de como usar o atributo ScriptMethod com a propriedade UseHttpGet.

**Listagem 6. Usando o atributo ScriptMethod com a propriedade UseHttpGet.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

Um exemplo dos cabeçalhos enviados quando o método Web HttpGetEcho mostrado na Listagem 6 é chamado são mostrados a seguir:

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

Além de permitir que os métodos da Web aceitem solicitações HTTP GET, o atributo ScriptMethod também pode ser usado quando as respostas XML precisam ser retornadas de um serviço em vez de JSON. Por exemplo, um serviço Web pode recuperar um RSS feed de um site remoto e retorná-lo como um objeto XmlDocument ou XmlElement. O processamento dos dados XML pode ocorrer no cliente.

A listagem 7 mostra um exemplo de como usar a propriedade ResponseFormat para especificar que os dados XML devem ser retornados de um método da Web.

**Listagem 7. Usando o atributo ScriptMethod com a propriedade ResponseFormat.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

A propriedade ResponseFormat também pode ser usada juntamente com a propriedade XmlSerializer. A propriedade XmlSerializer tem um valor padrão de false, o que significa que todos os tipos de retorno, exceto as cadeias de caracteres retornadas de um método da Web, são serializados como XML quando a `ResponseFormat` propriedade é definida como `ResponseFormat.Xml` . Quando `XmlSerializeString` é definido como `true` , todos os tipos retornados de um método da Web são serializados como XML, incluindo tipos de cadeia de caracteres. Se a propriedade ResponseFormat tiver um valor da `ResponseFormat.Json` Propriedade XmlSerializer é ignorada.

A listagem 8 mostra um exemplo de como usar a propriedade XmlSerializer para forçar a serialização de cadeias de caracteres como XML.

**Listagem 8. Usando o atributo ScriptMethod com a propriedade XmlSerializer**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

O valor retornado da chamada do método Web GetXmlString mostrado na Listagem 8 é mostrado a seguir:

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

Embora o formato JSON padrão minimize o tamanho geral das mensagens de solicitação e resposta e seja consumido mais prontamente por clientes ASP.NET AJAX em uma maneira cruzada, as propriedades ResponseFormat e XmlSerializer podem ser utilizadas quando aplicativos cliente, como o Internet Explorer 5 ou superior, esperam que os dados XML sejam retornados de um método da Web.

## <a name="working-with-complex-types"></a>Trabalhando com tipos complexos

A listagem 5 mostrou um exemplo de como retornar um tipo complexo chamado Customer de um serviço Web. A classe Customer define vários tipos simples diferentes internamente como propriedades como FirstName e LastName. Tipos complexos usados como um parâmetro de entrada ou tipo de retorno em um método Web habilitado para AJAX são automaticamente serializados em JSON antes de serem enviados para o lado do cliente. No entanto, tipos complexos aninhados (aqueles definidos internamente dentro de outro tipo) não são disponibilizados para o cliente como objetos autônomos por padrão.

Nos casos em que um tipo complexo aninhado usado por um serviço Web também deve ser usado em uma página de cliente, o atributo ASP.NET AJAX GenerateScriptType pode ser adicionado ao serviço Web. Por exemplo, a classe CustomerDetails mostrada na listagem 9 contém propriedades de endereço e gênero que ***representam tipos complexos aninhados.***

**Listagem 9. A classe CustomerDetails mostrada aqui contém dois tipos complexos aninhados.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

Os objetos de endereço e gênero definidos na classe CustomerDetails mostrados na listagem 9 não serão automaticamente disponibilizados para uso no lado do cliente por meio de JavaScript, já que eles são tipos aninhados (o endereço é uma classe e um gênero é uma enumeração). Em situações em que um tipo aninhado usado em um serviço Web deve estar disponível no lado do cliente, o atributo GenerateScriptType mencionado anteriormente pode ser usado (consulte a listagem 10). Esse atributo pode ser adicionado várias vezes nos casos em que tipos complexos aninhados diferentes são retornados de um serviço. Ele pode ser aplicado diretamente à classe de serviço Web ou a métodos da Web específicos.

**Listagem 10. Usando o atributo GenerateScriptService para definir tipos aninhados que devem estar disponíveis para o cliente.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

Ao aplicar o `GenerateScriptType` atributo ao serviço Web, os tipos de endereço e gênero serão disponibilizados automaticamente para uso pelo código JavaScript do ASP.NET AJAX no lado do cliente. Um exemplo do JavaScript que é gerado e enviado automaticamente para o cliente adicionando o atributo GenerateScriptType em um serviço Web é mostrado na listagem 11. Você verá como usar tipos complexos aninhados posteriormente neste artigo.

**Listagem 11. Tipos complexos aninhados disponibilizados para uma página AJAX do ASP.NET.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

Agora que você viu como criar serviços Web e torná-los acessíveis para as páginas do ASP.NET AJAX, vamos dar uma olhada em como criar e usar proxies JavaScript para que os dados possam ser recuperados ou enviados aos serviços da Web.

## <a name="creating-javascript-proxies"></a>Criando proxies JavaScript

Chamar um serviço Web padrão (.NET ou outra plataforma) normalmente envolve a criação de um objeto proxy que protege você das complexidades do envio de mensagens de solicitação e resposta SOAP. Com chamadas de serviço Web AJAX ASP.NET, os proxies JavaScript podem ser criados e usados para chamar facilmente os serviços sem se preocupar com a serialização e desserialização de mensagens JSON. Os proxies JavaScript podem ser gerados automaticamente usando o controle ScriptManager do ASP.NET AJAX.

A criação de um proxy JavaScript que pode chamar serviços Web é realizada usando a propriedade serviços do ScriptManager. Essa propriedade permite que você defina um ou mais serviços que uma página do ASP.NET AJAX pode chamar de forma assíncrona para enviar ou receber dados sem a necessidade de operações de postback. Você define um serviço usando o controle AJAX ASP.NET `ServiceReference` e atribui a URL do serviço Web à propriedade do controle `Path` . A listagem 12 mostra um exemplo de como fazer referência a um serviço chamado CustomersService. asmx.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**Listagem 12. Definição de um serviço Web usado em uma página AJAX do ASP.NET.**

Adicionar uma referência ao CustomersService. asmx por meio do controle ScriptManager faz com que um proxy JavaScript seja gerado dinamicamente e referenciado pela página. O proxy é inserido usando a &lt; marca de script &gt; e dinamicamente carregado chamando o arquivo CustomersService. asmx e acrescentando/js ao final dele. O exemplo a seguir mostra como o proxy JavaScript é inserido na página quando a depuração está desabilitada no web.config:

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]Se você quiser ver o código de proxy JavaScript real gerado, poderá digitar a URL para o serviço Web do .net desejado na caixa de endereço do Internet Explorer e acrescentar/js ao final dela.*

Se a depuração estiver habilitada no web.config uma versão de depuração do proxy JavaScript será inserida na página, conforme mostrado a seguir:

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

O proxy JavaScript criado pelo ScriptManager também pode ser inserido diretamente na página, em vez de referenciado usando &lt; o &gt; atributo src da marca de script. Isso pode ser feito definindo a propriedade InlineScript do controle imreference como true (o padrão é false). Isso pode ser útil quando um proxy não é compartilhado em várias páginas e quando você deseja reduzir o número de chamadas de rede feitas ao servidor. Quando InlineScript é definido como true, o script de proxy não será armazenado em cache pelo navegador para que o valor padrão false seja recomendado nos casos em que o proxy é usado por várias páginas em um aplicativo ASP.NET AJAX. Veja a seguir um exemplo de como usar a propriedade InlineScript:

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>Usando proxies JavaScript

Depois que um serviço Web é referenciado por uma página ASP.NET AJAX usando o controle ScriptManager, uma chamada pode ser feita ao serviço Web e os dados retornados podem ser tratados usando funções de retorno de chamada. Um serviço Web é chamado referenciando seu namespace (se houver), nome da classe e nome do método da Web. Todos os parâmetros passados para o serviço Web podem ser definidos junto com uma função de retorno de chamada que manipula os dados retornados.

Um exemplo de uso de um proxy JavaScript para chamar um método Web chamado GetCustomersByCountry () é mostrado na listagem 13. A função GetCustomersByCountry () é chamada quando um usuário final clica em um botão na página.

**Listagem 13. Chamar um serviço Web com um proxy JavaScript.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

Essa chamada referencia o namespace InterfaceTraining, a classe CustomersService e o método Web GetCustomersByCountry definido no serviço. Ele passa um valor de país obtido de uma caixa de texto, bem como uma função de chamada de retorno chamada OnWSRequestComplete que deve ser invocada quando a chamada de serviço Web assíncrona retorna. OnWSRequestComplete manipula a matriz de objetos Customer retornados do serviço e os converte em uma tabela que é exibida na página. A saída gerada a partir da chamada é mostrada na Figura 1.

[![Ligação de dados obtidos fazendo uma chamada AJAX assíncrona para um serviço Web.](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**Figura 1**: dados de associação obtidos ao fazer uma chamada AJAX assíncrona para um serviço Web.  ([Clique para exibir a imagem em tamanho normal](understanding-asp-net-ajax-web-services/_static/image3.png))

Os proxies JavaScript também podem fazer chamadas unidirecionais para serviços Web em casos em que um método da Web deve ser chamado, mas o proxy não deve esperar por uma resposta. Por exemplo, talvez você queira chamar um serviço Web para iniciar um processo, como um fluxo de trabalho, mas não aguardar um valor de retorno do serviço. Nos casos em que uma chamada unidirecional precisa ser feita a um serviço, a função de retorno de chamado mostrada na listagem 13 pode simplesmente ser omitida. Como nenhuma função de retorno de chamada é definida, o objeto proxy não aguardará o serviço Web retornar dados.

## <a name="handling-errors"></a>Manipulando erros

Retornos de chamada assíncronos para serviços Web podem encontrar diferentes tipos de erros, como a rede inoperante, o serviço Web que está sendo indisponível ou uma exceção que está sendo retornada. Felizmente, os objetos de proxy JavaScript gerados pelo ScriptManager permitem que vários retornos de chamada sejam definidos para lidar com erros e falhas, além do retorno de chamada bem-sucedido mostrado anteriormente. Uma função de retorno de chamada de erro pode ser definida imediatamente após a função de retorno de chamada padrão na chamada para o método Web, conforme mostrado na listagem 14.

**Listagem 14. Definição de uma função de retorno de chamada de erro e exibição de erros.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

Todos os erros que ocorrerem quando o serviço Web for chamado irão disparar a função de retorno de chamada OnWSRequestFailed () a ser chamada, que aceita um objeto que representa o erro como um parâmetro. O objeto de erro expõe várias funções diferentes para determinar a causa do erro, bem como se a chamada expirou ou não. A listagem 14 mostra um exemplo de como usar as diferentes funções de erro e a Figura 2 mostra um exemplo da saída gerada pelas funções.

[![Saída gerada chamando as funções de erro ASP.NET AJAX.](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**Figura 2**: saída gerada chamando as funções de erro do ASP.NET AJAX.  ([Clique para exibir a imagem em tamanho normal](understanding-asp-net-ajax-web-services/_static/image6.png))

## <a name="handling-xml-data-returned-from-a-web-service"></a>Manipulando dados XML retornados de um serviço Web

Anteriormente, você viu como um método Web poderia retornar dados XML brutos usando o atributo ScriptMethod junto com sua propriedade ResponseFormat. Quando ResponseFormat é definido como ResponseFormat.Xml, os dados retornados do serviço Web são serializados como XML em vez de JSON. Isso pode ser útil quando os dados XML precisam ser passados diretamente para o cliente para processamento usando JavaScript ou XSLT. Na hora atual, o Internet Explorer 5 ou superior fornece o melhor modelo de objeto do lado do cliente para análise e filtragem de dados XML devido ao seu suporte interno para MSXML.

A recuperação de dados XML de um serviço Web não é diferente de recuperar outros tipos de dados. Comece invocando o proxy JavaScript para chamar a função apropriada e definir uma função de retorno de chamada. Depois que a chamada retornar, você poderá processar os dados na função de retorno de chamada.

A listagem 15 mostra um exemplo de como chamar um método da Web chamado GetRssFeed () que retorna um objeto XmlElement. GetRssFeed () aceita um único parâmetro que representa a URL do RSS feed a ser recuperado.

**Listagem 15. Trabalhando com dados XML retornados de um serviço Web.**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

Este exemplo passa uma URL para um RSS feed e processa os dados XML retornados na função OnWSRequestComplete (). OnWSRequestComplete () primeiro verifica se o navegador é o Internet Explorer para saber se o analisador MSXML está ou não disponível. Se for, uma instrução XPath será usada para localizar todas as &lt; marcas de item &gt; no RSS feed. Em seguida, cada item é iterado e o &lt; título &gt; e as &lt; marcas de link associados &gt; são localizados e processados para exibir os dados de cada item. A Figura 3 mostra um exemplo da saída gerada por fazer uma chamada ASP.NET AJAX por meio de um proxy JavaScript para o método Web GetRssFeed ().

## <a name="handling-complex-types"></a>Manipulando tipos complexos

Tipos complexos aceitos ou retornados por um serviço Web são expostos automaticamente por meio de um proxy JavaScript. No entanto, tipos complexos aninhados não são diretamente acessíveis no lado do cliente, a menos que o atributo GenerateScriptType seja aplicado ao serviço, conforme discutido anteriormente. Por que você desejaria usar um tipo complexo aninhado no lado do cliente?

Para responder a essa pergunta, suponha que uma página do ASP.NET AJAX exiba dados do cliente e permite que os usuários finais atualizem o endereço de um cliente. Se o serviço Web especificar que o tipo de endereço (um tipo complexo definido em uma classe CustomerDetails) pode ser enviado para o cliente, o processo de atualização poderá ser dividido em funções separadas para um melhor uso de código.

[![Saída criando a partir da chamada de um serviço Web que retorna dados RSS.](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**Figura 3**: criação de saída da chamada de um serviço Web que retorna dados RSS.  ([Clique para exibir a imagem em tamanho normal](understanding-asp-net-ajax-web-services/_static/image9.png))

A listagem 16 mostra um exemplo de código do lado do cliente que invoca um objeto de endereço definido em um namespace de modelo, preenche-o com dados atualizados e o atribui à propriedade de endereço de um objeto CustomerDetails. O objeto CustomerDetails é passado para o serviço Web para processamento.

**Listagem 16. Usando tipos complexos aninhados**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>Criando e usando métodos de página

Os serviços Web fornecem uma excelente maneira de expor serviços reutilizados a uma variedade de clientes, incluindo páginas AJAX ASP.NET. No entanto, pode haver casos em que uma página precisa recuperar dados que nunca serão usados ou compartilhados por outras páginas. Nesse caso, tornar um arquivo. asmx para permitir que a página acesse os dados pode parecer um exagero, uma vez que o serviço é usado apenas por uma única página.

O ASP.NET AJAX fornece outro mecanismo para fazer chamadas semelhantes ao serviço da Web sem criar arquivos. asmx autônomos. Isso é feito usando uma técnica conhecida como "métodos de página". Os métodos de página são métodos estáticos (compartilhados em VB.NET) inseridos diretamente em um arquivo de página ou código ao lado do atributo WebMethod aplicado a eles. Ao aplicar o atributo WebMethod, eles podem ser chamados usando um objeto JavaScript especial chamado PageMethods que é criado dinamicamente no tempo de execução. O objeto PageMethods atua como um proxy que protege você do processo de serialização/desserialização JSON. Observe que para usar o objeto PageMethods, você deve definir a propriedade EnablePageMethods do ScriptManager como true.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

A listagem 17 mostra um exemplo de definição de dois métodos de página em uma classe code-beside ASP.NET. Esses métodos recuperam dados de uma classe de camada comercial localizada na \_ pasta de código do aplicativo do site.

**Listagem 17. Definindo métodos de página.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

Quando o ScriptManager detecta a presença de métodos da Web na página, ele gera uma referência dinâmica para o objeto PageMethods mencionado anteriormente. Chamar um método Web é feito referenciando a classe PageMethods seguida pelo nome do método e quaisquer dados de parâmetro necessários que devam ser passados. A listagem 18 mostra exemplos de como chamar os dois métodos de página mostrados anteriormente.

**Listagem 18. Chamando métodos de página com o objeto JavaScript PageMethods.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

O uso do objeto PageMethods é muito semelhante ao uso de um objeto proxy JavaScript. Primeiro, você especifica todos os dados de parâmetro que devem ser passados para o método Page e define a função de retorno de chamada que deve ser chamada quando a chamada assíncrona retorna. Um retorno de chamada de falha também pode ser especificado (consulte a listagem 14 para obter um exemplo de tratamento de falhas).

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>O AutoCompleteExtender e o ASP.NET AJAX Toolkit

O ASP.NET AJAX Toolkit (disponível em [http://ajax.asp.net](http://ajax.asp.net) ) oferece vários controles que podem ser usados para acessar os serviços da Web. Especificamente, o kit de ferramentas contém um controle útil chamado `AutoCompleteExtender` que pode ser usado para chamar serviços da Web e mostrar dados em páginas sem escrever nenhum código JavaScript.

O controle AutoCompleteExtender pode ser usado para estender a funcionalidade existente de uma caixa de texto e ajudar os usuários a localizar com mais facilidade os dados que estão procurando. Como eles digitam em uma caixa de texto, o controle pode ser usado para consultar um serviço Web e mostra os resultados abaixo da caixa de texto dinamicamente. A Figura 4 mostra um exemplo de como usar o controle AutoCompleteExtender para exibir IDs de cliente para um aplicativo de suporte. À medida que o usuário digita caracteres diferentes na caixa de texto, itens diferentes serão mostrados abaixo com base na entrada. Os usuários podem selecionar a ID do cliente desejada.

Usar o AutoCompleteExtender em uma página do ASP.NET AJAX requer que o assembly de AjaxControlToolkit.dll seja adicionado à pasta bin do site. Depois que o assembly do kit de ferramentas tiver sido adicionado, você desejará referenciá-lo em web.config para que os controles que ele contém estejam disponíveis para todas as páginas em um aplicativo. Isso pode ser feito adicionando a seguinte marca na &lt; marca Controls de web.config &gt; :

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

Nos casos em que você só precisa usar o controle em uma página específica, você pode referenciá-lo adicionando a diretiva de referência à parte superior de uma página, conforme mostrado a seguir em vez de atualizar web.config:

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![Usando o controle AutoCompleteExtender.](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**Figura 4**: usando o controle AutoCompleteExtender.  ([Clique para exibir a imagem em tamanho normal](understanding-asp-net-ajax-web-services/_static/image12.png))

Depois que o site foi configurado para usar o kit de ferramentas ASP.NET AJAX, um controle AutoCompleteExtender pode ser adicionado à página de forma muito semelhante a você adicionaria um controle de servidor ASP.NET regular. A listagem 19 mostra um exemplo de como usar o controle para chamar um serviço Web.

**Listagem 19. Usando o controle AutoCompleteExtender do ASP.NET AJAX Toolkit.**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

O AutoCompleteExtender tem várias propriedades diferentes, incluindo a ID padrão e as propriedades runat encontradas nos controles de servidor. Além disso, ele permite que você defina quantos caracteres um usuário final digita antes que o serviço Web seja consultado quanto a dados. A propriedade MinimumPrefixLength mostrada na listagem 19 faz com que o serviço seja chamado cada vez que um caractere é digitado na caixa de texto. Você desejará ter cuidado ao definir esse valor, pois cada vez que o usuário digitar um caractere, o serviço Web será chamado para pesquisar valores que correspondam aos caracteres na caixa de texto. O serviço Web para chamar, bem como o método Web de destino, é definido usando as propriedades ServiceName e Service Method, respectivamente. Finalmente, a propriedade TargetControlID identifica a qual caixa de texto vincular o controle AutoCompleteExtender.

O serviço Web que está sendo chamado deve ter o atributo ScriptService aplicado conforme discutido anteriormente e o método Web de destino deve aceitar dois parâmetros chamados prefixText e Count. O parâmetro prefixText representa os caracteres digitados pelo usuário final e o parâmetro Count representa o número de itens a serem retornados (o padrão é 10). A listagem 20 mostra um exemplo do método Web GetCustomerIDs chamado pelo controle AutoCompleteExtender mostrado anteriormente na listagem 19. O método Web chama um método de camada de negócios que, por sua vez, chama um método de camada de dados que manipula a filtragem de dados e o retorno dos resultados correspondentes. O código para o método de camada de dados é mostrado na listagem 21.

**Listagem 20. Filtrando dados enviados do controle AutoCompleteExtender.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**Listagem 21. Filtrando resultados com base na entrada do usuário final.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>Conclusão

O ASP.NET AJAX fornece excelente suporte para chamar serviços da Web sem escrever muito código JavaScript personalizado para lidar com as mensagens de solicitação e resposta. Neste artigo, você viu como habilitar o AJAX para os serviços Web do .NET para permitir que eles processem mensagens JSON e como definir proxies JavaScript usando o controle ScriptManager. Você também viu como os proxies JavaScript podem ser usados para chamar serviços da Web, manipular tipos simples e complexos e lidar com falhas. Por fim, você viu como os métodos de página podem ser usados para simplificar o processo de criação e realização de chamadas de serviço Web e como o controle AutoCompleteExtender pode fornecer ajuda aos usuários finais à medida que eles digitam. Embora o UpdatePanel disponível no ASP.NET AJAX certamente seja o controle de sua escolha para muitos programadores de AJAX devido à sua simplicidade, saber como chamar serviços da Web por meio de proxies JavaScript pode ser útil em muitos aplicativos.

## <a name="bio"></a>Biografia

Dan Wahlin (Microsoft Most Valuable Professional para ASP.NET e XML Web Services) é um instrutor de desenvolvimento .NET e consultor de arquitetura em treinamento técnico de interface ( [http://www.interfacett.com](http://www.interfacett.com) ). Dan fundou o site XML for ASP.NET Developers ([www.XMLforASP.net](http://www.XMLforASP.NET)), está na central do palestrante da INETA e fala em várias conferências. Dan My-autod Professional Windows DNA (Wrox), ASP.NET: Tips, tutoriais e código (SAMS), ASP.NET 1,1 insider Solutions, Professional ASP.NET 2,0 AJAX (Wrox), ASP.NET 2,0 de hacks MVP e XML autod for ASP.NET Developers (SAMS). Quando ele não está escrevendo código, artigos ou livros, Dan gosta de escrever e gravar música e jogar golfe e basquete com sua esposa e crianças.

Scott Cate tem trabalhado com tecnologias Web da Microsoft desde 1997 e é presidente da myKB.com ([www.myKB.com](http://www.myKB.com)), onde é especialista em escrever aplicativos baseados em ASP.net voltados para as soluções de software da base de dados de conhecimento. Scott pode ser contatado por email em [scott.cate@myKB.com](mailto:scott.cate@myKB.com) ou em seu blog em [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [Anterior](understanding-asp-net-ajax-localization.md) 
>  [Avançar](understanding-asp-net-ajax-debugging-capabilities.md)
