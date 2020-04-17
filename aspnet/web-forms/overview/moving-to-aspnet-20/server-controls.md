---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: Controles do servidor | Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0 melhora os controles do servidor de muitas maneiras. Neste módulo, vamos cobrir algumas das mudanças arquitetônicas na forma como ASP.NET 2.0 e Visual Studio 200...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543737"
---
# <a name="server-controls"></a>Controles de servidor

pela [Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 melhora os controles do servidor de muitas maneiras. Neste módulo, abordaremos algumas das mudanças arquitetônicas na forma como ASP.NET 2.0 e visual Studio 2005 lidam com controles de servidor.

ASP.NET 2.0 melhora os controles do servidor de muitas maneiras. Neste módulo, abordaremos algumas das mudanças arquitetônicas na forma como ASP.NET 2.0 e visual Studio 2005 lidam com controles de servidor.

## <a name="view-state"></a>Ver estado

A principal mudança no estado de visão em ASP.NET 2.0 é uma redução drástica do tamanho. Considere uma página com apenas um controle de calendário nela. Aqui está o estado de vista em ASP.NET 1.1.

[!code-css[Main](server-controls/samples/sample1.css)]

Agora, aqui está o estado de exibição em uma página idêntica em ASP.NET 2.0.

[!code-css[Main](server-controls/samples/sample2.css)]

Essa é uma mudança bastante significativa, e considerando que o estado de visão é transportado para frente e para trás sobre o fio, essa mudança pode dar aos desenvolvedores um aumento significativo de desempenho. A redução do tamanho do estado de visão deve-se, em grande parte, à maneira como lidamos com ele internamente. Lembre-se que o estado de exibição é uma seqüência codificada base64. Para entender melhor a mudança no estado de visão em ASP.NET 2.0, vamos dar uma olhada nos valores decodificados dos exemplos acima.

Aqui está o estado de exibição 1.1 decodificado:

[!code-css[Main](server-controls/samples/sample3.css)]

Isso pode parecer um pouco como uma bobagem, mas há um padrão aqui. Em ASP.NET 1.x, usamos caracteres únicos para identificar tipos &lt; &gt; de dados e valores delimitados usando os caracteres. O "t" na amostra de estado de visão acima representa um Trigêmeo. O Triplet contém um par de ArrayLists (o "l" representa uma ArrayList.) Um desses ArrayLists contém um Int32 ("i") com um valor de 1 e o outro contém outro Triplet. O Triplet contém um par de ArrayLists, etc. O importante a lembrar é que usamos Trigêmeos que contêm pares, identificamos os &lt; tipos &gt; de dados através de uma carta e usamos os personagens como delimitadores.

Em ASP.NET 2.0, o estado de exibição decodificado parece um pouco diferente.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

Você deve notar uma grande mudança na aparência do estado de exibição decodificado. Essa mudança tem vários fundamentos arquitetônicos. Exibir estado em ASP.NET 1.x usou o LosFormatter para serializar dados. No 2.0, usamos a nova classe ObjectStateFormatter. Esta classe foi especificamente projetada para auxiliar na serialização e desserialização do estado de visão e estado de controle. (O estado de controle será coberto na próxima seção.) Há muitos benefícios obtidos com a mudança do método pelo qual a serialização e a desserialização ocorrem. Um dos mais dramáticos é o fato de que, ao contrário do LosFormatter que usa um TextWriter, o ObjectStateFormatter usa um BinaryWriter. Isso permite que ASP.NET 2.0 armazene o estado de exibição de uma série de bytes em vez de strings. Veja, por exemplo, um inteiro. Em ASP.NET 1.1, um inteiro exigiu 4 bytes de estado de vista. Em ASP.NET 2.0, esse mesmo inteiro requer apenas 1 byte. Outros aprimoramentos foram feitos para diminuir a quantidade de estado de visão armazenado. Os valores DateTime, por exemplo, agora são armazenados usando um TickCount em vez de uma seqüência de string.

Como se tudo isso não bastasse, uma atenção especial foi dada ao fato de que um dos maiores consumidores de estado de visão em 1.x era o DataGrid e controles similares. Uma grande desvantagem de controles como o DataGrid no que diz respeito ao estado de exibição é que muitas vezes contém grandes quantidades de informações repetidas. Em ASP.NET 1.x, essa informação repetida foi simplesmente armazenada várias vezes, resultando em um estado de exibição inchado. Em ASP.NET 2.0, usamos a nova classe IndexedString para armazenar tais dados. Se uma string se repetir, apenas armazenamos o token para o IndexedString e o índice dentro de uma tabela em execução de objetos IndexedString.

## <a name="control-state"></a>Estado de Controle

Uma das principais queixas que os desenvolvedores tinham com o estado de visão foi o tamanho que ele adicionou à carga http. Como mencionado anteriormente, um dos maiores consumidores de estado de visão é o controle DataGrid. Para evitar as enormes quantidades de estado de exibição geradas por um DataGrid, muitos desenvolvedores simplesmente desativaram o estado de exibição para esse controle. Infelizmente, essa solução nem sempre foi boa. Exibir estado em ASP.NET 1.x contém não apenas dados necessários para a funcionalidade correta do controle. Também contém informações sobre o estado da ui do controle. Isso significa que, se você quiser permitir a paginação em um DataGrid, você deve habilitar o estado de exibição mesmo que você não precise de todas as informações de ia que o estado de exibição contém. É um cenário de tudo ou nada.

Em ASP.NET 2.0, o estado de controle resolve bem esse problema através da introdução do estado de controle. O estado de controle contém os dados que são absolutamente necessários para a funcionalidade adequada de um controle. Ao contrário do estado de exibição, o estado de controle não pode ser desativado. Portanto, é importante que os dados armazenados em estado de controle sejam cuidadosamente controlados.

> [!NOTE]
> O estado de controle é persistido juntamente com o estado de exibição no \_ \_campo de formulário oculto VIEWSTATE.

Este vídeo é um passo a passo do estado de visão e estado de controle.

![](server-controls/_static/image1.png)

[Abra o vídeo em tela cheia](server-controls/_static/state1.wmv)

Para que um controle de servidor leia e escreva para controlar o estado, você deve dar três passos.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>Passo 1: Ligue para o método RegisterRequiresControlState

O método RegisterRequiresControlState informa ASP.NET que um controle precisa persistir no estado de controle. É preciso um argumento do tipo Controle que é o controle que está sendo registrado.

É importante ressaltar que o registro não persiste de solicitação a solicitação. Portanto, este método deve ser chamado em cada solicitação se um controle persistir no estado de controle. Recomenda-se que o método seja chamado de OnInit.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>Passo 2: Substituir SaveControlState

O método SaveControlState salva alterações de estado de controle para um controle desde o último post de volta. Ele retorna um objeto representando o estado do controle.

## <a name="step-3-override-loadcontrolstate"></a>Passo 3: Substituir LoadControlState

O método LoadControlState carrega o estado salvo em um controle. O método pega um argumento do tipo Objeto que mantém o estado salvo para o controle.

## <a name="full-xhtml-compliance"></a>Conformidade xhtml completa

Qualquer desenvolvedor Web sabe a importância dos padrões em aplicações Web. Para manter um ambiente de desenvolvimento baseado em padrões, ASP.NET 2.0 é totalmente compatível com XHTML. Portanto, todas as tags são renderizadas de acordo com os padrões XHTML em navegadores que suportam HTML 4.0 ou superior.

A definição DOCTYPE em ASP.NET 1.1 foi a seguinte:

[!code-html[Main](server-controls/samples/sample6.html)]

Em ASP.NET 2.0, a definição padrão do DOCTYPE é a seguinte:

[!code-html[Main](server-controls/samples/sample7.html)]

Se você escolher, você pode alterar a conformidade XHTML padrão através do nó xhtmlConformância no arquivo de configuração. Por exemplo, o seguinte nó no arquivo web.config mudará a conformidade XHTML para XHTML 1.0 Strict:

[!code-xml[Main](server-controls/samples/sample8.xml)]

Se você escolher, você também pode configurar ASP.NET para usar a configuração legado usada em ASP.NET 1.x da seguinte forma:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>Renderização adaptativa usando adaptadores

Em ASP.NET 1.x, o &lt;arquivo&gt; de configuração continha uma seção browserCaps que preencheu um objeto HttpBrowserCapabilities. Este objeto permitiu que um desenvolvedor determinasse qual dispositivo está fazendo uma solicitação específica e renderizasse o código adequadamente. Em ASP.NET 2.0, o modelo melhorou e agora usa a nova classe ControlAdapter. A classe ControlAdapter substitui eventos no ciclo de vida do controle e controla a renderização de controles com base nas capacidades do agente de usuário. Os recursos de um agente de usuário específico são definidos por um arquivo de definição do navegador (um arquivo com uma extensão de arquivo .browser) armazenado no c:\windows\microsoft.net\framework\v2.0. \* \* \*\CONFIG\Pasta de navegadores. \*

> [!NOTE]
> A classe ControlAdapter é uma classe abstrata.

Assim como &lt;a&gt; seção browserCaps em 1.x, o arquivo de definição do navegador usa uma Expressão Regular para analisar a seqüência do agente de usuário, a fim de identificar o navegador solicitante. Ele define recursos particulares para esse agente usuário. O ControlAdapter renderiza o controle através do método Render. Portanto, se você substituir o método Render, você não deve chamar Render na classe base. Isso pode fazer com que a renderização ocorra duas vezes, uma para o adaptador e outra para o próprio controle.

## <a name="developing-a-custom-adapter"></a>Desenvolvendo um adaptador personalizado

Você pode desenvolver seu próprio adaptador personalizado herdando do ControlAdapter. Além disso, você pode herdar da classe abstrata PageAdapter nos casos em que um adaptador é necessário para uma página. O mapeamento dos controles para o seu &lt;adaptador&gt; personalizado é realizado através do elemento controlAdapters no arquivo de definição do navegador. Por exemplo, o XML a seguir de um arquivo de definição de navegador mapeia o controle menu para a classe MenuAdapter:

[!code-html[Main](server-controls/samples/sample10.html)]

Usando este modelo, torna-se bastante fácil para um desenvolvedor de controle atingir um determinado dispositivo ou navegador. Também é bastante simples para um desenvolvedor ter controle completo sobre como as páginas renderizam em cada dispositivo.

## <a name="per-device-rendering"></a>Renderização por dispositivo

As propriedades de controle do servidor em ASP.NET 2.0 podem ser especificadas por dispositivo usando um prefixo específico do navegador. Por exemplo, o código abaixo alterará o texto de um rótulo dependendo de qual dispositivo está sendo usado para navegar na página.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

Quando a página que contém este rótulo for navegada pelo Internet Explorer, o rótulo exibirá um texto dizendo "Você está navegando no Internet Explorer". Quando a página é navegada pelo Firefox, o rótulo exibirá o texto "Você está navegando no Firefox". Quando a página é navegada a partir de qualquer outro dispositivo, ela exibirá "Você está navegando a partir de um dispositivo desconhecido". Qualquer propriedade pode ser especificada usando esta sintaxe especial.

## <a name="setting-focus"></a>Definindo foco

ASP.NET desenvolvedores do 1.x frequentemente perguntados sobre como definir o foco inicial em um determinado controle. Por exemplo, em uma página de login, é útil que a caixa de texto do ID do usuário obtenha o foco quando a página é carregada pela primeira vez. Em ASP.NET 1.x, fazer isso exigiu escrever algum script do lado do cliente. Embora tal script seja uma tarefa trivial, ele não é mais necessário em ASP.NET 2.0 graças ao método SetFocus. O método SetFocus tem um argumento indicando o controle que deve receber foco. Esse argumento pode ser o ID do cliente do controle como uma string ou o nome do controle do Servidor como um objeto de controle. Por exemplo, para definir o foco inicial em um controle textbox chamado txtUserID\_quando a página for carregada pela primeira vez, adicione o seguinte código à Carga de Página:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

- ou

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 usa o manipulador Webresource.axd (discutido anteriormente) para renderizar uma função do lado do cliente que define o foco. O nome da função lado do\_cliente é WebForm AutoFocus como mostrado aqui:

[!code-html[Main](server-controls/samples/sample14.html)]

Alternativamente, você pode usar o método Focus para um controle para definir o foco inicial para esse controle. O método Focus deriva da classe Controle e está disponível para todos os controles ASP.NET 2.0. Também é possível definir o foco para um controle específico quando ocorre um erro de validação. Isso será coberto em um módulo posterior.

## <a name="new-server-controls-in-aspnet-20"></a>Novos controles de servidor em ASP.NET 2.0

A seguir, novos controles de servidor em ASP.NET 2.0. Vamos entrar em mais detalhes sobre alguns deles em módulos posteriores.

## <a name="imagemap-control"></a>Controle de ImageMap

O controle ImageMap permite adicionar pontos de acesso a uma imagem que pode iniciar uma postagem de volta ou navegar para uma URL. Existem três tipos de hotspots disponíveis; CircleHotSpot, RectangleHotSpot e PolygonHotSpot. Os hotspots são adicionados através de um editor de coleção no Visual Studio ou programáticamente em código. Não há interface de usuário disponível para desenhar pontos de acesso em uma imagem. As coordenadas e o tamanho ou raio do ponto de acesso devem ser especificados declarativamente. Também não há representação visual de um hotspot no designer. Se um hotspot estiver configurado para navegar até uma URL, a URL será especificada através da propriedade NavigateUrl do hotspot. No caso de um hotspot post back, a propriedade PostBackValue permite que você passe uma seqüência no post de volta que pode ser recuperada no código do lado do servidor.

![Editor de coleção hotspot em visual studio](server-controls/_static/image1.jpg)

**Figura 1**: Editor de coleção hotspot em Visual Studio

## <a name="bulletedlist-control"></a>Controle bulletedlist

O controle BulletedList é uma lista de balas que pode ser facilmente vinculada a dados. A lista pode ser encomendada (numerada) ou não ordenada através da propriedade BulletStyle. Cada item da lista é representado por um objeto ListItem.

![Controle bulletedlist no Visual Studio](server-controls/_static/image1.gif)

**Figura 2**: Controle de bulletedList no Visual Studio

## <a name="hiddenfield-control"></a>Controle de Campo Oculto

O controle HiddenField adiciona um campo de formulário oculto à sua página, o valor do qual está disponível no código do lado do servidor. Espera-se que o valor de um campo de formulário oculto permaneça inalterado entre os postbacks. No entanto, é possível que um usuário mal-intencionado altere o valor antes de postar de volta. Se isso acontecer, o controle HiddenField aumentará o evento ValueChanged. Se você tiver informações confidenciais no controle HiddenField e quiser garantir que elas permaneçam inalteradas, você deve lidar com o evento ValueChanged em seu código.

## <a name="fileupload-control"></a>Controle fileupload

O controle FileUpload em ASP.NET 2.0 torna possível carregar arquivos para um servidor da Web através de uma página ASP.NET. Este controle é bastante semelhante ao ASP.NET classe HtmlInputFile 1.x com algumas exceções. Em ASP.NET 1.x, foi recomendado que a propriedade PostedFile fosse verificada como nula, a fim de determinar se você tinha um bom arquivo. O controle FileUpload em ASP.NET 2.0 adiciona uma nova propriedade HasFile que você pode usar para o mesmo propósito e é um pouco mais eficiente.

A propriedade PostedFile ainda está disponível para acesso a um objeto HttpPostedFile, mas algumas das funcionalidades do HttpPostedFile estão agora disponíveis intrinsecamente com o controle FileUpload. Por exemplo, para salvar um arquivo carregado em ASP.NET 1.x, você chama o método SaveAs no objeto HttpPostedFile. Usando o controle FileUpload em ASP.NET 2.0, você chamaria o método SaveAs no próprio controle FileUpload.

Outra mudança significativa no comportamento 2.0 (e provavelmente a mudança mais significativa) é que não é mais necessário carregar um arquivo carregado inteiro na memória antes de salvá-lo. Em 1.x, qualquer arquivo que foi carregado é salvo inteiramente na memória antes de ser gravado em disco. Esta arquitetura impede o upload de arquivos grandes.

Em ASP.NET 2.0, o atributo requestLengthDiskThreshold do elemento httpRuntime permite configurar quantos Kilobytes são mantidos em um buffer na memória antes de serem gravados em disco.

**IMPORTANTE**: A documentação mSDN (e documentação em outros lugares) especifica que este valor está em bytes (não Kilobytes) e que o padrão é de 256. O valor é realmente especificado em Kilobytes e o valor padrão é 80. Ao ter um valor padrão de 80K, garantimos que o buffer não acabe no grande monte de objetos.

## <a name="wizard-control"></a>Controle de Assistente

É bastante comum encontrar ASP.NET desenvolvedores que lutam para tentar coletar informações em uma série de "páginas" usando painéis ou transferindo de página em página. Na maioria das vezes, o esforço é frustrante e demorado. O novo controle do Assistente resolve os problemas permitindo etapas lineares e não lineares em uma interface de assistente com a qual os usuários estão familiarizados. O controle wizard apresenta formulários de entrada em uma série de etapas. Cada passo é de um tipo específico especificado pela propriedade StepType do controle. Os tipos de etapas disponíveis são os seguintes:

| **Tipo de passo** | **Explicação** |
| --- | --- |
| Auto | O assistente determina automaticamente o tipo de passo com base em sua posição dentro da hierarquia de etapas. |
| Iniciar | O primeiro passo, muitas vezes usado para apresentar uma declaração introdutória. |
| Etapa | Um passo normal. |
| Concluir | O passo final, geralmente usado para apresentar um botão para terminar o assistente. |
| Concluído | Apresenta uma mensagem comunicando sucesso ou fracasso. |

> [!NOTE]
> O controle do Assistente mantém o controle de seu estado usando ASP.NET estado de controle. Portanto, a propriedade EnableViewState pode ser definida como falsa sem qualquer prejuízo.

Este vídeo é um passo a passo do controle do Assistente.

![](server-controls/_static/image2.png)

[Abra o vídeo em tela cheia](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>Controle localize

O controle Localize é semelhante a um controle literal. No entanto, o controle Localize tem uma propriedade **Mode** que controla como a marcação que é adicionada a ele é renderizada. A propriedade Mode suporta os seguintes valores:

| **Modo** | **Explicação** |
| --- | --- |
| Transformar | A marcação é transformada de acordo com o protocolo do navegador que faz a solicitação. |
| Passagem | A marcação é renderizada como está. |
| Codificar | A marcação adicionada ao controle é codificada usando HtmlEncode. |

## <a name="multiview-and-view-controls"></a>Controles MultiView e View

O controle MultiView atua como um contêiner para controles view, e o controle Exibir atua como um contêiner (muito parecido com um controle de painel) para outros controles. Cada exibição em um controle MultiView é representada por um único controle de exibição. O primeiro controle de exibição no MultiView é o view 0, o segundo é view 1, etc. Você pode alternar visualizações especificando o ActiveViewIndex do controle MultiView.

## <a name="substitution-control"></a>Controle de Substituição

O controle de substituição é usado em conjunto com ASP.NET cache. Nos casos em que você deseja aproveitar o cache, mas você tem partes de uma página que devem ser atualizadas em cada solicitação (em outras palavras, partes de uma página que estão isentas de cache), o componente Substituição fornece uma ótima solução. O controle não produz nenhuma saída por conta própria. Em vez disso, ele está vinculado a um método no código do lado do servidor. Quando a página é solicitada, o método é chamado e a marcação retornada é renderizada no lugar do controle de substituição.

O método ao qual o controle de substituição está vinculado é especificado através da propriedade **MethodName.** Esse método deve atender aos seguintes critérios:

- Deve ser um método estático (compartilhado em VB).
- Ele aceita um parâmetro do tipo HttpContext.
- Ele retorna uma seqüência representando a marcação que deve substituir o controle na página.

O controle de Substituição não tem a capacidade de modificar qualquer outro controle na página, mas ele tem acesso ao HttpContext atual através de seu parâmetro.

## <a name="gridview-control"></a>Controle gridview

O controle GridView é a substituição do controle DataGrid. Este controle será coberto com mais detalhes em um módulo posterior.

## <a name="detailsview-control"></a>DetalhesVer Controle

O controle DetailsView permite que você exiba um único registro de uma fonte de dados e edite ou exclua-o. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="formview-control"></a>Controle FormView

O controle FormView é usado para exibir um único registro de uma fonte de dados em uma interface configurável. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="accessdatasource-control"></a>Controle de fonte de acessoDataData

O controle AccessDataSource é usado para vincular dados a um banco de dados access. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="objectdatasource-control"></a>Controle objectDataSourceSource

O controle ObjectDataSource é usado para suportar uma arquitetura de três níveis para que os controles possam ser vinculados a um objeto de negócios de nível intermediário, em oposição a um modelo de dois níveis onde os controles estão vinculados diretamente à fonte de dados. Será discutido com mais detalhes em um módulo posterior.

## <a name="xmldatasource-control"></a>XmlDataSource Control

O controle XmlDataSource é usado para vincular dados a uma fonte de dados XML. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="sitemapdatasource-control"></a>SiteMapDataSource Control

O controle SiteMapDataSource fornece vinculação de dados para controles de navegação do site com base em um mapa do site. Será discutido com mais detalhes em um módulo posterior.

## <a name="sitemappath-control"></a>Controle do SiteMapPath

O controle SiteMapPath exibe uma série de links de navegação comumente referidos como migalhas de pão. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="menu-control"></a>Controle de Menu

O controle de menu exibe menus dinâmicos usando DHTML. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="treeview-control"></a>Controle TreeView

O controle TreeView é usado para exibir uma exibição hierárquica de dados em árvores. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="login-control"></a>Controle de login

O controle de login fornece um mecanismo para fazer login em um site da Web. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="loginview-control"></a>Controle de LoginView

O controle LoginView permite a exibição de diferentes modelos com base no status de login de um usuário. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="passwordrecovery-control"></a>Controle de Recuperação de Senhas

O controle PasswordRecovery é usado para recuperar senhas esquecidas pelos usuários de um aplicativo ASP.NET. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="loginstatus"></a>LoginStatus

O controle LoginStatus exibe o status de login do usuário. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="loginname"></a>LoginName

O controle LoginName exibe o nome de usuário de um usuário após ser conectado a um aplicativo ASP.NET. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="createuserwizard"></a>Createuserwizard

O CreateUserWizard é um assistente configurável que oferece aos usuários a capacidade de criar uma conta de associação ASP.NET para uso em um aplicativo ASP.NET. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="changepassword"></a>ChangePassword

O controle ChangePassword permite que os usuários alterem sua senha para um aplicativo ASP.NET. Ele é coberto com mais detalhes em um módulo posterior.

## <a name="various-webparts"></a>Várias WebParts

ASP.NET 2.0 naves com várias Web Parts. Estes serão cobertos em detalhes em um módulo posterior.
