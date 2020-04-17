---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: O modelo de página 2.0 ASP.NET | Microsoft Docs
author: rick-anderson
description: Em ASP.NET 1.x, os desenvolvedores escolheram entre um modelo de código inline e um modelo de código por trás do código. O code-behind pode ser implementado usando o Src attr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542853"
---
# <a name="the-aspnet-20-page-model"></a>O modelo de página ASP.NET 2.0

pela [Microsoft](https://github.com/microsoft)

> Em ASP.NET 1.x, os desenvolvedores escolheram entre um modelo de código inline e um modelo de código por trás do código. O code-behind pode ser implementado usando o atributo @Page Src ou o atributo CodeBehind da diretiva. No ASP.NET 2.0, os desenvolvedores ainda têm uma escolha entre código inline e código atrás, mas houve melhorias significativas no modelo de código atrás.

Em ASP.NET 1.x, os desenvolvedores escolheram entre um modelo de código inline e um modelo de código por trás do código. O code-behind pode ser implementado usando o atributo @Page Src ou o atributo CodeBehind da diretiva. No ASP.NET 2.0, os desenvolvedores ainda têm uma escolha entre código inline e código atrás, mas houve melhorias significativas no modelo de código atrás.

## <a name="improvements-in-the-code-behind-model"></a>Melhorias no modelo de código atrás

Para entender completamente as mudanças no modelo de código traseiro no ASP.NET 2.0, é melhor rever rapidamente o modelo como existia no ASP.NET 1.x.

## <a name="the-code-behind-model-in-aspnet-1x"></a>O modelo de código atrás em ASP.NET 1.x

Em ASP.NET 1.x, o modelo de código atrás consistia de um arquivo ASPX (o Webform) e um arquivo por trás de código contendo código de programação. Os dois arquivos foram @Page conectados usando a diretiva no arquivo ASPX. Cada controle na página ASPX tinha uma declaração correspondente no arquivo de código atrás como uma variável de ocorrência. O arquivo de código atrás também continha código para vinculação de eventos e código gerado necessário para o designer do Visual Studio. Este modelo funcionou muito bem, mas como cada elemento ASP.NET na página ASPX exigia código correspondente no arquivo de código atrás, não havia uma verdadeira separação de código e conteúdo. Por exemplo, se um designer adicionasse um novo controle de servidor a um arquivo ASPX fora do Visual Studio IDE, o aplicativo quebraria devido à ausência de uma declaração para esse controle no arquivo de código atrás.

## <a name="the-code-behind-model-in-aspnet-20"></a>O modelo de código atrás em ASP.NET 2.0

ASP.NET 2.0 melhora muito nesse modelo. Em ASP.NET 2.0, o code-behind é implementado usando as novas *classes parciais* fornecidas no ASP.NET 2.0. A classe de código atrás em ASP.NET 2.0 é definida como uma classe parcial, o que significa que contém apenas parte da definição de classe. A parte restante da definição de classe é gerada dinamicamente por ASP.NET 2.0 usando a página ASPX em tempo de execução ou quando o site da Web é pré-compilado. O link entre o arquivo de código atrás e a página ASPX ainda é estabelecido usando a diretiva @ Page. No entanto, em vez de um atributo CodeBehind ou Src, ASP.NET 2.0 agora usa o atributo CodeFile. O atributo Herdado também é usado para especificar o nome da classe para a página.

Uma diretiva típica @ Page pode ser assim:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

Uma definição de classe típica em um arquivo de código 2.0 ASP.NET pode ser assim:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C# e Visual Basic são os únicos idiomas gerenciados que atualmente suportam classes parciais. Portanto, os desenvolvedores que usam J# não poderão usar o modelo de código atrás em ASP.NET 2.0.

O novo modelo aprimora o modelo de código atrás porque os desenvolvedores agora terão arquivos de código que contêm apenas o código que eles criaram. Ele também prevê uma verdadeira separação de código e conteúdo porque não há declarações de variável de ocorrência no arquivo de código atrás.

> [!NOTE]
> Como a classe parcial da página ASPX é onde a vinculação de eventos ocorre, os desenvolvedores do Visual Basic podem realizar um leve aumento de desempenho usando a palavra-chave Handles no code-behind para vincular eventos. C# não tem palavra-chave equivalente.

## <a name="new--page-directive-attributes"></a>Novos atributos da diretiva @ page

ASP.NET 2.0 adiciona muitos novos atributos à diretiva @ Page. Os atributos a seguir são novos em ASP.NET 2.0.

## <a name="async"></a>Assíncrono

O atributo Assync permite configurar a página para ser executada de forma assíncrona. Bem, cubra páginas assíncronas mais tarde neste módulo.

## <a name="asynctimeout"></a>Asynctimeout

Especificou o tempo para páginas assíncronas. O padrão é 45 segundos.

## <a name="codefile"></a>Codefile

O atributo CodeFile é a substituição do atributo CodeBehind no Visual Studio 2002/2003.

### <a name="codefilebaseclass"></a>Codefilebaseclass

O atributo CodeFileBaseClass é usado nos casos em que você deseja que várias páginas derivam de uma única classe base. Devido à implementação de classes parciais em ASP.NET, sem esse atributo, uma classe base que usa campos comuns compartilhados para controles de referência declarados em uma página ASPX não funcionaria corretamente porque o mecanismo de compilação ASP.NETs criará automaticamente novos membros com base em controles na página. Portanto, se você quiser uma classe base comum para duas ou mais páginas em ASP.NET, você precisará definir especificar sua classe base no atributo CodeFileBaseClass e, em seguida, derivar cada classe de páginas dessa classe base. O atributo CodeFile também é necessário quando este atributo é usado.

## <a name="compilationmode"></a>Compilationmode

Este atributo permite definir a propriedade CompilationMode da página ASPX. A propriedade CompilationMode é uma enumeração que contém os valores **Always**, **Auto**e **Never**. O padrão é **Always**. A configuração **Auto** impedirá que ASP.NET compilem a página dinamicamente, se possível. A exclusão de páginas de compilação dinâmica aumenta o desempenho. No entanto, se uma página excluída contiver esse código que deve ser compilado, um erro será jogado quando a página for navegada.

## <a name="enableeventvalidation"></a>Enableeventvalidation

Este atributo especifica se os eventos de pós-retorno e retorno de chamada são validados ou não. Quando isso é ativado, os argumentos para eventos de pós-retorno ou retorno de chamada são verificados para garantir que eles se originaram do controle do servidor que originalmente os tornou.

## <a name="enabletheming"></a>Enabletheming

Este atributo especifica se ASP.NET temas são usados ou não em uma página. O padrão é **falso.** ASP.NET temas estão abordados no [Módulo 10](profiles-themes-and-web-parts.md).

## <a name="linepragmas"></a>LinePragmas

Este atributo especifica se os pragmas de linha devem ser adicionados durante a compilação. Pragmas de linha são opções usadas por depuradores para marcar seções específicas de código.

## <a name="maintainscrollpositiononpostback"></a>Maintainscrollpositiononpostback

Este atributo especifica se javaScript é injetado ou não na página, a fim de manter a posição de rolagem entre postbacks. Este atributo é **falso** por padrão.

Quando esse atributo for **verdadeiro,** ASP.NET adicionará um &lt;bloco de script&gt; no postback que se parece com isso:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

Observe que o src para este bloco de script é WebResource.axd. Este recurso não é um caminho físico. Quando este script é solicitado, ASP.NET constrói dinamicamente o script.

### <a name="masterpagefile"></a>Masterpagefile

Este atributo especifica o arquivo de página-mestre para a página atual. O caminho pode ser relativo ou absoluto. As páginas-mestre são cobertas no [Módulo 4](master-pages.md).

## <a name="stylesheettheme"></a>Stylesheettheme

Este atributo permite que você sobreponha as propriedades de aparência da interface do usuário definidas por um tema ASP.NET 2.0. Os temas estão abordados no [Módulo 10](profiles-themes-and-web-parts.md).

## <a name="theme"></a>Tema

Especifica o tema da página. Se um valor não for especificado para o atributo StyleSheetTheme, o atributo Tema substitui todos os estilos aplicados aos controles na página.

## <a name="title"></a>Title

Define o título da página. O valor especificado aqui &lt;aparecerá no elemento título&gt; da página renderizada.

### <a name="viewstateencryptionmode"></a>Viewstateencryptionmode

Define o valor para a enumeração ViewStateEncryptionMode. Os valores disponíveis são **Always**, **Auto**e **Never**. O valor padrão é **Auto**. Quando este atributo é definido como um valor de **Auto**, viewstate é criptografado é um controle solicita-o chamando o método **RegisterRequiresViewStateEncryption.**

## <a name="setting-public-property-values-via-the--page-directive"></a>Definindo valores de propriedade pública através da Diretiva @ Página

Outra nova capacidade da diretiva @ Page em ASP.NET 2.0 é a capacidade de definir o valor inicial das propriedades públicas de uma classe base. Suponha, por exemplo, que você tenha uma propriedade pública chamada **SomeText** em sua classe base e gostaria que fosse inicializada para **Olá** quando uma página é carregada. Você pode fazer isso simplesmente definindo o valor na diretiva @ Page assim:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

O atributo **SomeText** da diretiva @ Page define o valor inicial da propriedade SomeText na classe base para *Hello!*. O vídeo abaixo é um passo a passo para definir o valor inicial de uma propriedade pública em uma classe base usando a diretiva @ Page.

![](the-asp-net-2-0-page-model/_static/image1.png)

[Abra o vídeo em tela cheia](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>Novas Propriedades Públicas da Classe de Página

As seguintes propriedades públicas são novas em ASP.NET 2.0.

## <a name="apprelativetemplatesourcedirectory"></a>Apprelativetemplatesourcedirectory

Retorna o caminho relativo ao aplicativo para a página ou controle. Por exemplo, para uma http://app/folder/page.aspxpágina localizada em , a propriedade retorna ~/folder/.

## <a name="apprelativevirtualpath"></a>Apprelativevirtualpath

Retorna o caminho relativo do diretório virtual para a página ou controle. Por exemplo, para uma http://app/folder/page.aspxpágina localizada em , a propriedade retorna ~/folder/page.aspx.

## <a name="asynctimeout"></a>Asynctimeout

Obtém ou define o tempo hámenos usado para o manuseio assíncrono da página. (As páginas assíncronas serão abordadas mais tarde neste módulo.)

## <a name="clientquerystring"></a>ClientQueryString

Uma propriedade somente leitura que retorna a parte de seqüência de consulta da URL solicitada. Este valor é codificado por URL. Você pode usar o método UrlDecode da classe HttpServerUtility para decodificá-lo.

## <a name="clientscript"></a>Clientscript

Essa propriedade retorna um objeto ClientScriptManager que pode ser usado para gerenciar a emissão de ASP.NETs de script do lado do cliente. (A classe ClientScriptManager é coberta mais tarde neste módulo.)

## <a name="enableeventvalidation"></a>Enableeventvalidation

Esta propriedade controla se a validação do evento está ativada ou não para eventos de pós-retorno e retorno de chamada. Quando ativado, os argumentos para eventos de pós-retorno ou retorno de chamada são verificados para garantir que eles se originaram do controle do servidor que originalmente os tornou.

## <a name="enabletheming"></a>Enabletheming

Esta propriedade recebe ou define um Boolean o que especifica se um tema ASP.NET 2.0 se aplica à página.

## <a name="form"></a>Formulário

Esta propriedade retorna o formulário HTML na página ASPX como um objeto HtmlForm.

## <a name="header"></a>Cabeçalho

Esta propriedade retorna uma referência a um objeto HtmlHead que contém o cabeçalho da página. Você pode usar o objeto HtmlHead retornado para obter/definir folhas de estilo, metas Meta, etc.

## <a name="idseparator"></a>Idseparator

Esta propriedade somente leitura obtém o caractere que é usado para separar identificadores de controle quando ASP.NET está construindo um ID exclusivo para controles em uma página. Não é destinado a ser utilizado diretamente do seu código.

## <a name="isasync"></a>Isasync

Esta propriedade permite páginas assíncronas. Páginas assíncronas são discutidas mais tarde neste módulo.

## <a name="iscallback"></a>Iscallback

Esta propriedade somente leitura retorna **verdadeira** se a página for o resultado de uma chamada de volta. Os retornos das chamadas são discutidos mais tarde neste módulo.

## <a name="iscrosspagepostback"></a>Iscrosspagepostback

Esta propriedade somente leitura retorna **verdadeira** se a página for parte de um postback de página cruzada. Os postbacks de páginas cruzadas são cobertos mais tarde neste módulo.

## <a name="items"></a>Itens

Retorna uma referência a uma instância do IDictionary que contém todos os objetos armazenados no contexto das páginas. Você pode adicionar itens a este objeto iDictionary e eles estarão disponíveis para você durante toda a vida útil do contexto.

## <a name="maintainscrollpositiononpostback"></a>Maintainscrollpositiononpostback

Esta propriedade controla se ASP.NET emite ou não JavaScript que mantém a posição de rolagem de páginas no navegador após a ocorrência de um postback. (Detalhes desta propriedade foram discutidos anteriormente neste módulo.)

## <a name="master"></a>Principal

Esta propriedade somente leitura retorna uma referência à instância MasterPage para uma página à qual uma página-mestre foi aplicada.

## <a name="masterpagefile"></a>Masterpagefile

Obtém ou define o nome do arquivo da página principal para a página. Esta propriedade só pode ser definida no método PreInit.

## <a name="maxpagestatefieldlength"></a>Maxpagestatefieldlength

Esta propriedade obtém ou define o comprimento máximo para o estado das páginas em bytes. Se a propriedade for definida como um número positivo, o estado de exibição de páginas será dividido em vários campos ocultos para que não exceda o número de bytes especificados. Se a propriedade for um número negativo, o estado de exibição não será dividido em pedaços.

## <a name="pageadapter"></a>Pageadapter

Retorna uma referência ao objeto PageAdapter que modifica a página para o navegador solicitante.

## <a name="previouspage"></a>Previouspage

Retorna uma referência à página anterior em casos de um Servidor.Transfer ou um postback de página cruzada.

## <a name="skinid"></a>Skinid

Especifica a ASP.NET pele 2.0 para aplicar na página.

## <a name="stylesheettheme"></a>Stylesheettheme

Esta propriedade obtém ou define a folha de estilos aplicada a uma página.

## <a name="templatecontrol"></a>Templatecontrol

Retorna uma referência ao controle contendo para a página.

## <a name="theme"></a>Tema

Obtém ou define o nome do tema ASP.NET 2.0 aplicado à página. Este valor deve ser definido antes do método PreInit.

## <a name="title"></a>Title

Esta propriedade obtém ou define o título da página conforme obtido no cabeçalho de páginas.

## <a name="viewstateencryptionmode"></a>Viewstateencryptionmode

Obtém ou define o Modo de exibiçãoStateEncryptionMode da página. Veja uma discussão detalhada desta propriedade no início deste módulo.

## <a name="new-protected-properties-of-the-page-class"></a>Novas propriedades protegidas da classe de página

A seguir estão as novas propriedades protegidas da classe Page em ASP.NET 2.0.

## <a name="adapter"></a>Adaptador

Retorna uma referência ao ControlAdapter que renderiza a página no dispositivo que a solicitou.

## <a name="asyncmode"></a>Modo Assincronia

Esta propriedade indica se a página é processada assíncronamente. Destina-se a ser usado pelo tempo de execução e não diretamente em código.

## <a name="clientidseparator"></a>Oridparte do cliente

Essa propriedade retorna o caractere usado como separador ao criar IDs de cliente exclusivos para controles. Destina-se a ser usado pelo tempo de execução e não diretamente em código.

## <a name="pagestatepersister"></a>Pagestatepersister

Esta propriedade retorna o objeto PageStatePersister para a página. Esta propriedade é usada principalmente por desenvolvedores de controle de ASP.NET.

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

Esta propriedade retorna um sufixo exclusivo que é anexado ao caminho do arquivo para cache de navegadores. O valor \_ \_padrão é ufps= e um número de 6 dígitos.

## <a name="new-public-methods-for-the-page-class"></a>Novos métodos públicos para a classe de página

Os seguintes métodos públicos são novos na classe Page em ASP.NET 2.0.

## <a name="addonprerendercompleteasync"></a>Addonprerendercompleteasync

Este método registra os delegados manipuladores de eventos para execução de página assíncrona. Páginas assíncronas são discutidas mais tarde neste módulo.

## <a name="applystylesheetskin"></a>Applystylesheetskin

Aplica as propriedades em uma folha de estilo de páginas na página.

## <a name="executeregisteredasynctasks"></a>Executeregisteredasynctasks

Este método é uma tarefa assíncrona.

### <a name="getvalidators"></a>Getvalidators

Retorna uma coleção de validadores para o grupo de validação especificado ou para o grupo de validação padrão, se nenhum for especificado.

## <a name="registerasynctask"></a>Registerasynctask

Este método registra uma nova tarefa de assincronia. Páginas assíncronas são cobertas mais tarde neste módulo.

## <a name="registerrequirescontrolstate"></a>Registerrequirescontrolstate

Este método diz a ASP.NET que o estado de controle de páginas deve ser persistido.

## <a name="registerrequiresviewstateencryption"></a>Registerrequiresviewstateencryption

Este método diz a ASP.NET que o estado de visualização de páginas requer criptografia.

## <a name="resolveclienturl"></a>Resolveclienturl

Retorna uma URL relativa que pode ser usada para solicitações de clientes para imagens, etc.

## <a name="setfocus"></a>SetFocus

Este método definirá o foco para o controle especificado quando a página é inicialmente carregada.

## <a name="unregisterrequirescontrolstate"></a>Unregisterrequirescontrolstate

Este método desregistrará o controle que é passado a ele como não mais exigindo persistência do estado de controle.

## <a name="changes-to-the-page-lifecycle"></a>Alterações no ciclo de vida da página

O ciclo de vida da página no ASP.NET 2.0 não mudou drasticamente, mas existem alguns novos métodos que você deve estar ciente. O ciclo de vida da página ASP.NET 2.0 é descrito abaixo.

## <a name="preinit-new-in-aspnet-20"></a>PreInit (Novo em ASP.NET 2.0)

O evento PreInit é o estágio mais antigo do ciclo de vida que um desenvolvedor pode acessar. A adição deste evento permite alterar programáticamente ASP.NET temas 2.0, páginas-mestre, propriedades de acesso para um perfil ASP.NET 2.0, etc. Se você está em um estado de pós-volta, é importante perceber que o Viewstate ainda não foi aplicado aos controles neste momento do ciclo de vida. Portanto, se um desenvolvedor mudar uma propriedade de um controle nesta fase, ele provavelmente será substituído mais tarde no ciclo de vida das páginas.

## <a name="init"></a>Init

O evento Init não mudou de ASP.NET 1.x. É aqui que você gostaria de ler ou inicializar propriedades de controles em sua página. Nesta fase, páginas-mestre, temas, etc. já são aplicados à página.

## <a name="initcomplete-new-in-20"></a>InitComplete (Novo em 2.0)

O evento InitComplete é chamado no final da fase de inicialização de páginas. Neste ponto do ciclo de vida, você pode acessar controles na página, mas seu estado ainda não foi preenchido.

## <a name="preload-new-in-20"></a>Pré-Carga (Novo em 2.0)

Este evento é chamado depois que todos os dados\_de pós-retorno foram aplicados e pouco antes do Page Load.

## <a name="load"></a>Carregar

O evento Load não mudou de ASP.NET 1.x.

## <a name="loadcomplete-new-in-20"></a>LoadComplete (Novo em 2.0)

O evento LoadComplete é o último evento na fase de carga de páginas. Nesta fase, todos os dados de postback e viewstate foram aplicados à página.

## <a name="prerender"></a>Prerender

Se você quiser que o estado de exibição seja mantido adequadamente para controles adicionados à página dinamicamente, o evento PreRender é a última oportunidade para adicioná-los.

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete (Novo em 2.0)

Na fase PreRenderComplete, todos os controles foram adicionados à página e a página está pronta para ser renderizada. O evento PreRenderComplete é o último evento levantado antes que o estado de exibição das páginas seja salvo.

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete (Novo em 2.0)

O evento SaveStateComplete é chamado imediatamente após a salvação de todos os estados de exibição e controle da página. Este é o último evento antes que a página seja realmente renderizada para o navegador.

## <a name="render"></a>Renderizar

O método Render não mudou desde ASP.NET 1.x. É aqui que o HtmlTextWriter é inicializado e a página é renderizada para o navegador.

## <a name="cross-page-postback-in-aspnet-20"></a>Postback de página cruzada em ASP.NET 2.0

Em ASP.NET 1.x, os postbacks eram necessários para postar na mesma página. Postbacks de páginas cruzadas não eram permitidos. ASP.NET 2.0 adiciona a capacidade de postar de volta a uma página diferente através da interface IButtonControl. Qualquer controle que implemente a nova interface IButtonControl (Button, LinkButton e ImageButton, além de controles personalizados de terceiros) pode tirar proveito dessa nova funcionalidade através do uso do atributo PostBackUrl. O código a seguir mostra um controle button que é posta de volta para uma segunda página.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

Quando a página é postada de volta, a página que inicia o postback fica acessível através da propriedade PreviousPage na segunda página. Essa funcionalidade é implementada através\_da nova função webform DoPostBackWithOptions do lado do cliente que ASP.NET 2.0 renderiza na página quando um controle posta de volta para uma página diferente. Esta função JavaScript é fornecida pelo novo manipulador WebResource.axd que emite script para o cliente.

O vídeo abaixo é um passo a passo de um postback de página cruzada.

![](the-asp-net-2-0-page-model/_static/image2.png)

[Abra o vídeo em tela cheia](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>Mais detalhes sobre postbacks de páginas cruzadas

### <a name="viewstate"></a>Viewstate

Você já deve ter se perguntado sobre o que acontece com o estado de exibição da primeira página em um cenário de postback de página cruzada. Afinal, qualquer controle que não implemente o IPostBackDataHandler persistirá seu estado via viewstate, de modo que para ter acesso às propriedades desse controle na segunda página de um postback de página cruzada, você deve ter acesso ao estado de exibição para a página. ASP.NET 2.0 cuida desse cenário usando um novo campo \_ \_oculto na segunda página chamada PREVIOUSPAGE. O \_ \_campo de formulário PREVIOUSPAGE contém o estado de exibição da primeira página para que você possa ter acesso às propriedades de todos os controles na segunda página.

### <a name="circumventing-findcontrol"></a>Contornando o FindControl

No passo a passo de um postback de página cruzada, usei o método FindControl para obter uma referência ao controle TextBox na primeira página. Esse método funciona bem para esse fim, mas o FindControl é caro e requer a escrita de código adicional. Felizmente, ASP.NET 2.0 oferece uma alternativa ao FindControl para este fim que funcionará em muitos cenários. A diretiva PreviousPageType permite que você tenha uma referência fortemente digitada à página anterior usando o TypeName ou o atributo VirtualPath. O atributo TypeName permite especificar o tipo da página anterior, enquanto o atributo VirtualPath permite que você consulte a página anterior usando um caminho virtual. Depois de definir a diretiva PreviousPageType, você deve então expor os controles, etc. aos quais deseja permitir o acesso usando propriedades públicas.

## <a name="lab-1-cross-page-postback"></a>Postback de página cruzada do laboratório 1

Neste laboratório, você criará um aplicativo que usa a nova funcionalidade de postback de página cruzada de ASP.NET 2.0.

1. Abra o Visual Studio 2005 e crie um novo site ASP.NET.
2. Adicione um novo Webform chamado page2.aspx.
3. Abra o 'Default.aspx' na exibição Design e adicione um controle button e um controle TextBox. 

    1. Dê ao botão o controle de um ID do **SubmitButton** e a TextBox controle um ID de **UserName**.
    2. Defina a propriedade PostBackUrl do Botão para page2.aspx.
4. Abra a página2.aspx na exibição Origem.
5. Adicione uma diretiva @ PreviousPageType como mostrado abaixo:
6. Adicione o seguinte código\_à carga de página do código de page2.aspx: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. Construa o projeto clicando em Build no menu Build.
8. Adicione o seguinte código ao código-traseiro de Default.aspx: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. Alterar a\_carga de página em page2.aspx para o seguinte: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. Compile o projeto.
11. Execute o projeto.
12. Digite seu nome na TextBox e clique no botão.
13. Qual é o resultado?

## <a name="asynchronous-pages-in-aspnet-20"></a>Páginas Assíncronas em ASP.NET 2.0

Muitos problemas de contenção na ASP.NET são causados pela latência de chamadas externas (como serviços web ou chamadas de banco de dados), latência de IO de arquivo, etc. Quando uma solicitação é feita contra um aplicativo de ASP.NET, ASP.NET usa um de seus threads de trabalhador para atender a essa solicitação. Essa solicitação possui esse segmento até que a solicitação esteja concluída e a resposta tenha sido enviada. ASP.NET 2.0 busca resolver problemas de latência com esses tipos de problemas, adicionando a capacidade de executar páginas de forma assíncrona. Isso significa que um segmento de trabalhador pode iniciar a solicitação e, em seguida, entregar a execução adicional para outro segmento, retornando assim ao pool de segmentos disponível rapidamente. Quando o iO do arquivo, a chamada do banco de dados, etc. tiver sido concluída, um novo segmento é obtido no pool de segmentos para concluir a solicitação.

O primeiro passo para fazer uma página ser executada de forma assíncrona é definir o atributo **Assync** da diretiva de página assim:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

Este atributo diz ao ASP.NET para implementar o IHttpAsyncHandler para a página.

O próximo passo é chamar o método AddOnPreRenderCompleteAsync em um ponto do ciclo de vida da página antes do PreRender. (Este método é tipicamente\_chamado de Carga de Página.) O método AddOnPreRenderCompleteAsync tem dois parâmetros; um StartEventHandler e um EndEventHandler. O StartEventHandler retorna um IAsyncResultado que é então passado como parâmetro para o EndEventHandler.

O vídeo abaixo é um passo a passo de uma solicitação de página assíncrona.

![](the-asp-net-2-0-page-model/_static/image3.png)

[Abra o vídeo em tela cheia](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> Uma página de async não é renderizada no navegador até que o EndEventHandler tenha sido concluído. Sem dúvida, mas que alguns desenvolvedores pensarão em pedidos de sincronia como sendo semelhantes a revisincronia. É importante perceber que eles não são. O benefício das solicitações assíncronas é que o primeiro segmento de trabalhador pode ser devolvido ao pool de segmentos para atender novas solicitações, reduzindo assim a contenção devido ao limite de IO, etc.

## <a name="script-callbacks-in-aspnet-20"></a>Chamadas de script em ASP.NET 2.0

Os desenvolvedores da Web sempre procuraram maneiras de evitar a cintilação associada a um retorno de chamada. Em ASP.NET 1.x, o SmartNavigation foi o método mais comum para evitar cintilações, mas o SmartNavigation causou problemas para alguns desenvolvedores devido à complexidade de sua implementação no cliente. ASP.NET 2.0 aborda esse problema com retornos de chamadas de script. Os retornos de script utilizam o XMLHttp para fazer solicitações contra o servidor Web via JavaScript. A solicitação XMLHttp retorna dados XML que podem ser manipulados através do DOM do navegador. O código XMLHttp é oculto do usuário pelo novo manipulador WebResource.axd.

Existem várias etapas necessárias para configurar um retorno de chamada de script em ASP.NET 2.0.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>Passo 1: Implementar a interface ICallbackEventHandler

Para que ASP.NET reconheçam sua página como participante de um retorno de chamada de script, você deve implementar a interface ICallbackEventHandler. Você pode fazer isso no seu arquivo de código atrás assim:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

Você também pode fazer isso usando a diretiva @ Implements assim:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

Você normalmente usaria a diretiva @ Implements ao usar o código ASP.NET inline.

## <a name="step-2--call-getcallbackeventreference"></a>Passo 2 : Chamada GetCallbackReferência de evento

Como mencionado anteriormente, a chamada XMLHttp está encapsulada no manipulador WebResource.axd. Quando sua página for renderizada, ASP.NET adicionará uma chamada ao WebForm\_DoCallback, um script cliente fornecido pelo WebResource.axd. A função\_WebForm DoCallback \_ \_substitui a função doPostBack por um retorno de chamada. Lembre-se que \_ \_o doPostBack envia programáticamente o formulário na página. Em um cenário de retorno de chamada, você \_ \_deseja evitar um postback, então doPostBack não será suficiente.

> [!NOTE]
> \_\_doPostBack ainda é renderizado na página em um cenário de chamada de script do cliente. No entanto, não é usado para o retorno de chamada.

Os argumentos para\_a função webForm DoCallback lado do cliente são fornecidos através da função\_getcallbackEventReference do lado do servidor, que normalmente seria chamada de Carga de Página. Uma chamada típica para GetCallbackEventReference pode ser assim:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> Neste caso, cm é uma instância do ClientScriptManager. A classe ClientScriptManager será coberta mais tarde neste módulo.

Existem várias versões sobrecarregadas do GetCallbackEventReference. Neste caso, os argumentos são os seguintes:

`this`

Uma referência ao controle onde GetCallbackEventReference está sendo chamado. Neste caso, é a própria página.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

Um argumento de seqüência que será passado do código do lado do cliente para o evento do lado do servidor. Neste caso, estou passando o valor de uma dropdown chamada ddlCompany.

`ShowCompanyName`

O nome da função lado do cliente que aceitará o valor de retorno (como string) do evento de retorno do lado do servidor. Essa função só será chamada quando a chamada do lado do servidor for bem sucedida. Portanto, por uma questão de robustez, geralmente é recomendável usar a versão sobrecarregada do GetCallbackEventReference que leva um argumento de seqüência adicional especificando o nome de uma função do lado do cliente para executar no caso de um erro.

`null`

Uma seqüência representando uma função do lado do cliente que ela iniciou antes do retorno de chamada para o servidor. Neste caso, não existe tal script, então o argumento é nulo.

`true`

Um booleano especificando se deve ou não conduzir o retorno de chamada de forma assíncrona.

A chamada para\_WebForm DoCallback no cliente passará esses argumentos. Portanto, quando esta página é renderizada no cliente, esse código será assim:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

Observe que a assinatura da função no cliente é um pouco diferente. A função do lado do cliente passa 5 cordas e um Boolean. A seqüência adicional (que é nula no exemplo acima) contém a função do lado do cliente que lidará com quaisquer erros da chamada do lado do servidor.

## <a name="step-3--hook-the-client-side-control-event"></a>Passo 3 : Gancho o evento de controle do lado do cliente

Observe que o valor de retorno de GetCallbackEventReference acima foi atribuído a uma variável de seqüência. Essa string é usada para conectar um evento do lado do cliente para o controle que inicia o retorno de chamada. Neste exemplo, o retorno de chamada é iniciado por um dropdown na página, então eu quero ligar o evento *OnChange.*

Para conectar o evento do lado do cliente, basta adicionar um manipulador à marcação do lado do cliente da seguinte forma:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

Lembre-se de que *cbRef* é o valor de retorno da chamada para GetCallbackEventReference. Ele contém a chamada\_para WebForm DoCallback que foi mostrado acima.

## <a name="step-4--register-the-client-side-script"></a>Passo 4 : Registre o script lado do cliente

Lembre-se de que a chamada para GetCallbackEventReference especificava que um script do lado do cliente chamado **ShowCompanyName** seria executado quando o retorno de chamada do lado do servidor for bem sucedido. Esse script precisa ser adicionado à página usando uma instância do ClientScriptManager. (A classe ClientScriptManager será discutida mais tarde neste módulo.) Você faz isso assim:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>Passo 5 : Chame os métodos da interface ICallbackEventHandler

O ICallbackEventHandler contém dois métodos que você precisa implementar em seu código. Eles são **RaiseCallbackEvent** e **GetCallbackEvent**.

**RaiseCallbackEvent** pega uma seqüência como argumento e não retorna nada. O argumento string é passado da chamada\_do lado do cliente para o WebForm DoCallback. Neste caso, esse valor é o atributo de *valor* da dropdown chamada ddlCompany. O código do lado do servidor deve ser colocado no método RaiseCallbackEvent. Por exemplo, se o seu retorno de chamada estiver fazendo uma Solicitação da Web contra um recurso externo, esse código deve ser colocado no RaiseCallbackEvent.

**GetCallbackEvent** é responsável por processar o retorno do retorno de chamada ao cliente. Não é preciso argumentos e retorna uma corda. A seqüência que ele retorna será passada como um argumento para a função do lado do cliente, neste caso *ShowCompanyName*.

Depois de completar as etapas acima, você está pronto para executar um retorno de chamada de script em ASP.NET 2.0.

![](the-asp-net-2-0-page-model/_static/image4.png)

[Abra o vídeo em tela cheia](the-asp-net-2-0-page-model/_static/callback1.wmv)

Os retornos de chamadas de script em ASP.NET são suportados em qualquer navegador que suporte a chamadas XMLHttp. Isso inclui todos os navegadores modernos em uso hoje. O Internet Explorer usa o objeto XMLHttp ActiveX, enquanto outros navegadores modernos (incluindo o próximo IE 7) usam um objeto XMLHttp intrínseco. Para determinar programáticamente se um navegador suporta retornos de chamadas, você pode usar a propriedade **Request.Browser.SupportCallback.** Essa propriedade retornará **verdadeira** se o cliente solicitante suportar retornos de chamadas de script.

## <a name="working-with-client-script-in-aspnet-20"></a>Trabalhando com script de cliente em ASP.NET 2.0

Os scripts do cliente em ASP.NET 2.0 são gerenciados através do uso da classe ClientScriptManager. A classe ClientScriptManager mantém o controle dos scripts do cliente usando um tipo e um nome. Isso impede que o mesmo script seja programáticamente inserido em uma página mais de uma vez.

> [!NOTE]
> Depois que um script tiver sido registrado com sucesso em uma página, qualquer tentativa subseqüente de registrar o mesmo script simplesmente resultará em que o script não seja registrado uma segunda vez. Não são adicionados scripts duplicados e nenhuma exceção ocorre. Para evitar cálculos desnecessários, existem métodos que você pode usar para determinar se um script já está registrado para que você não tente registrá-lo mais de uma vez.

Os métodos do ClientScriptManager devem ser familiares a todos os desenvolvedores atuais ASP.NET:

## <a name="registerclientscriptblock"></a>Registerclientscriptblock

Este método adiciona um script ao topo da página renderizada. Isso é útil para adicionar funções que serão explicitamente chamadas ao cliente.

Há duas versões sobrecarregadas deste método. Três dos quatro argumentos são comuns entre eles. Eles são:

`type (string)`

O ***argumento de tipo*** identifica um tipo para o script. Geralmente é uma boa ideia usar o tipo de página (isso. GetType()) para o tipo.

`key (string)`

O ***argumento-chave*** é uma chave definida pelo usuário para o script. Isso deve ser único para cada roteiro. Se você tentar adicionar um script com a mesma chave e tipo de um script já adicionado, ele não será adicionado.

`script (string)`

O argumento ***do script*** é uma string contendo o script real a ser adicionado. Recomenda-se que você use um StringBuilder para criar o script e, em seguida, use o método ToString() no StringBuilder para atribuir o argumento do ***script.***

Se você usar o RegisterClientScriptBlock sobrecarregado que leva apenas três&lt;argumentos, você deve incluir elementos de script (script&gt; e &lt;/script)&gt;no seu script.

Você pode optar por usar a sobrecarga do RegisterClientScriptBlock que leva um quarto argumento. O quarto argumento é um Boolean o que especifica se ASP.NET deve ou não adicionar elementos de script para você. Se esse argumento for **verdadeiro,** seu script não deve incluir explicitamente os elementos do script.

Use o método IsClientScriptBlockRegistered para determinar se um script já foi registrado. Isso permite evitar uma tentativa de recadastrar um script que já foi registrado.

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude (Novo em 2.0)

A tag RegisterClientScriptInclude cria um bloco de script que se vincula a um arquivo de script externo. Tem duas sobrecargas. Um leva uma chave e uma URL. O segundo adiciona um terceiro argumento especificando o tipo.

Por exemplo, o código a seguir gera um bloco de script que se vincula a jsfunctions.js na raiz da pasta scripts do aplicativo:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

Este código produz o seguinte código na página renderizada:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> O bloco de script é renderizado na parte inferior da página.

Use o método IsClientScriptIncludeRegistered para determinar se um script já foi registrado. Isso permite evitar uma tentativa de reregistrar um script.

## <a name="registerstartupscript"></a>Registerstartupscript

O método RegisterStartupScript tem os mesmos argumentos do método RegisterClientScriptBlock. Um script registrado no RegisterStartupScript é executado após o carregamento da página, mas antes do evento do lado do cliente do OnLoad. Em 1.X, os scripts registrados no RegisterStartupScript &lt;foram&gt; colocados pouco antes da tag de fechamento /formulário,&gt; enquanto os scripts registrados no RegisterClientScriptBlock foram colocados imediatamente após a tag de formulário de abertura. &lt; Em ASP.NET 2.0, ambos são colocados imediatamente antes da tag de fechamento &lt;/formulário.&gt;

> [!NOTE]
> Se você registrar uma função com RegisterStartupScript, essa função não será executada até que você a chame explicitamente no código do lado do cliente.

Use o método IsStartupScriptRegistered para determinar se um script já foi registrado e evitar uma tentativa de reregistrar um script.

## <a name="other-clientscriptmanager-methods"></a>Outros métodos de clientscriptmanager

Aqui estão alguns dos outros métodos úteis da classe ClientScriptManager.

|  <strong>Getcallbackeventreference</strong>   |                                                 Consulte os retornos de chamadas de script anteriormente neste módulo.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>Getpostbackclienthyperlink</strong>  |                Obtém uma referência JavaScript&lt;&gt;(javascript: call) que pode ser usada para postar de volta de um evento do lado do cliente.                 |
|  <strong>Getpostbackeventreference</strong>   |                                   Obtém uma seqüência que pode ser usada para iniciar um post de volta do cliente.                                    |
|      <strong>Getwebresourceurl</strong>       | Retorna uma URL a um recurso incorporado em um conjunto. Deve ser usado em conjunto com <strong>RegisterClientScriptResource</strong>. |
| <strong>Registerclientscriptresource</strong> |     Registra um recurso da Web com a página. Estes são recursos incorporados em um conjunto e manipulados pelo novo manipulador WebResource.axd.      |
|     <strong>Registerhiddenfield</strong>      |                                                 Registra um campo de formulário oculto com a página.                                                 |
|  <strong>Registeronsubmitstatement</strong>   |                                  Registra o código do lado do cliente que é executado quando o formulário HTML é enviado.                                   |
