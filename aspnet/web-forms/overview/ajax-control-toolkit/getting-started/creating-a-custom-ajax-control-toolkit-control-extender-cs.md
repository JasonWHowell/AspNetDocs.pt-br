---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: Criando um extensor de controle de controle ajax personalizado (C#) | Microsoft Docs
author: rick-anderson
description: Os extensores personalizados permitem personalizar e ampliar os recursos dos controles de ASP.NET sem ter que criar novas classes.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543022"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>Criação de um extensor personalizado do AJAX Control Toolkit (C#)

pela [Microsoft](https://github.com/microsoft)

> Os extensores personalizados permitem personalizar e ampliar os recursos dos controles de ASP.NET sem ter que criar novas classes.

Neste tutorial, você aprende como criar um extensor de controle AJAX Control Toolkit personalizado. Criamos um novo extensor simples, mas útil, que altera o estado de um botão de desativado para habilitado quando você digita texto em uma TextBox. Depois de ler este tutorial, você poderá estender o ASP.NET AJAX Toolkit com seus próprios extensores de controle.

Você pode criar extensores de controle personalizados usando o Visual Studio ou o Visual Web Developer (certifique-se de que você tem a versão mais recente do Visual Web Developer).

## <a name="overview-of-the-disabledbutton-extender"></a>Visão geral do extensor de botão desativado

Nosso novo extensor de controle é chamado de extensor DisabledButton. Este extensor terá três propriedades:

- TargetControlID - A TextBox que o controle estende.
- TargetButtonIID - O botão desativado ou habilitado.
- DisabledText - O texto que é exibido inicialmente no botão. Quando você começa a digitar, o botão exibe o valor da propriedade Texto de botão.

Você liga o extensor DisabledButton a um controle TextBox e Button. Antes de digitar qualquer texto, o botão está desativado e a TextBox e o Botão ficam assim:

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

(Clique[para ver a imagem em tamanho real](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))

Depois de começar a digitar texto, o botão está ativado e a TextBox e o Botão ficam assim:

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

(Clique[para ver a imagem em tamanho real](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))

Para criar nosso extensor de controle, precisamos criar os seguintes três arquivos:

- DisabledButtonExtender.cs - Este arquivo é a classe de controle do lado do servidor que gerenciará a criação do extensor e permitirá que você defina as propriedades na hora do projeto. Ele também define as propriedades que podem ser definidas no seu extensor. Essas propriedades são acessíveis via código e na hora do projeto e propriedades de correspondência definidas no arquivo DisableButtonBehavior.js.
- DisabledButtonBehavior.js -- Este arquivo é onde você adicionará toda a sua lógica de script cliente.
- DisabledButtonDesigner.cs - Esta classe permite a funcionalidade de tempo de projeto. Você precisa desta classe se quiser que o extensor de controle funcione corretamente com o Visual Studio/Visual Web Developer Designer.

Assim, um extensor de controle consiste em um controle do lado do servidor, um comportamento do lado do cliente e uma classe de designer do lado do servidor. Você aprende como criar todos esses três arquivos nas seções a seguir.

## <a name="creating-the-custom-extender-website-and-project"></a>Criando o site e o projeto do extensor personalizado

O primeiro passo é criar um projeto de biblioteca de classes e um site no Visual Studio/Visual Web Developer. Criaremos o extensor personalizado no projeto da biblioteca de classe e testaremos o extensor personalizado no site.

Vamos começar pelo site. Siga estas etapas para criar o site:

1. Selecione a opção menu **Arquivo, Novo Site**da Web .
2. Selecione o **modelo ASP.NET do Site.**
3. Nomeie o novo site *Site1*.
4. Clique no botão **OK**.

Em seguida, precisamos criar o projeto de biblioteca de classe que conterá o código para o extensor de controle:

1. Selecione a opção menu **Arquivo, Adicionar, Novo Projeto**.
2. Selecione o modelo **Biblioteca de** classe.
3. Nomeie a nova biblioteca de classes com o nome **CustomExtenders**.
4. Clique no botão **OK**.

Depois de concluir essas etapas, a janela Solution Explorer deve parecer a Figura 1.

[![Solução com projeto de biblioteca de sites e classes](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**Figura 01**: Solução com site e projeto de biblioteca de classes[(Clique para ver imagem em tamanho real)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png)

Em seguida, você precisa adicionar todas as referências de montagem necessárias ao projeto da biblioteca de classes:

1. Clique com o botão direito do mouse no projeto PersonalExtenders e selecione a opção de menu **Adicionar referência**.
2. Selecione a guia .NET.
3. Adicione referências aos assemblies a seguir:

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. Selecione a guia Procurar.
5. Adicione uma referência ao conjunto AjaxControlToolkit.dll. Este conjunto está localizado na pasta onde você baixou o AJAX Control Toolkit.

Depois de concluir essas etapas, a pasta referências do projeto da biblioteca de classe deve parecer a Figura 2.

[![Pasta de referências com referências necessárias](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**Figura 02**: Pasta de referências com referências necessárias[(Clique para exibir imagem em tamanho real](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))

## <a name="creating-the-custom-control-extender"></a>Criando o extensor de controle personalizado

Agora que temos nossa biblioteca de classe, podemos começar a construir nosso controle extensor. Vamos começar com os ossos nus de uma classe de controle de extensor personalizado (ver Lista 1).

**Lista 1 - MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

Há várias coisas que você nota sobre a classe de extensor de controle na Listagem 1. Primeiro, observe que a classe herda da classe base ExtenderControlBase. Todos os controles extensores do AJAX Control Toolkit derivam desta classe base. Por exemplo, a classe base inclui a propriedade TargetID que é uma propriedade obrigatória de cada extensor de controle.

Em seguida, observe que a classe inclui os dois atributos a seguir relacionados ao script do cliente:

- WebResource - Faz com que um arquivo seja incluído como um recurso incorporado em uma montagem.
- ClientScriptResource - Faz com que um recurso de script seja recuperado de um conjunto.

O atributo WebResource é usado para incorporar o arquivo JavaScript MyControlBehavior.js no conjunto quando o extensor personalizado é compilado. O atributo ClientScriptResource é usado para recuperar o script MyControlBehavior.js do conjunto quando o extensor personalizado é usado em uma página da Web.

Para que os atributos WebResource e ClientScriptResource funcionem, você deve compilar o arquivo JavaScript como um recurso incorporado. Selecione o arquivo na janela Do Explorador de soluções, abra a planilha de propriedades e atribua o valor *Recurso Incorporado* à propriedade **Build Action.**

Observe que o extensor de controle também inclui um atributo TargetControlType. Este atributo é usado para especificar o tipo de controle que é estendido pelo extensor de controle. No caso da Listagem 1, o extensor de controle é usado para estender uma TextBox.

Finalmente, observe que o extensor personalizado inclui uma propriedade chamada MyProperty. A propriedade está marcada com o atributo ExtenderControlProperty. Os métodos GetPropertyValue() e SetPropertyValue() são usados para passar o valor da propriedade do extensor de controle do lado do servidor para o comportamento do lado do cliente.

Vamos em frente e implemente o código para o nosso extensor DisabledButton. O código deste extensor pode ser encontrado na Lista 2.

**Lista 2 - DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

O extensor DisabledButton na Listagem 2 tem duas propriedades chamadas TargetButtonID e DisabledText. O IDReferenceProperty aplicado à propriedade TargetButtonID impede que você atribua qualquer coisa que não seja o ID de um controle de botão a esta propriedade.

Os atributos WebResource e ClientScriptResource associam um comportamento do lado do cliente localizado em um arquivo chamado DisabledButtonBehavior.js com este extensor. Discutimos este arquivo JavaScript na próxima seção.

## <a name="creating-the-custom-extender-behavior"></a>Criando o comportamento do extensor personalizado

O componente do lado do cliente de um extensor de controle é chamado de comportamento. A lógica real para desativar e ativar o botão está contida no comportamento DisabledButton. O código JavaScript para o comportamento está incluído na Lista 3.

**Listagem 3 - DisabledButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

O arquivo JavaScript na Lista 3 contém uma classe do lado do cliente chamada DisabledButtonBehavior. Essa classe, como seu gêmeo do lado do servidor, inclui duas propriedades chamadas\_TargetButtonID e\_DisabledText que\_você pode\_acessar usando o TargetButtonID/set TargetButtonID e obter DisabledText/set DisabledText.

O método initialize() associa um manipulador de eventos keyup com o elemento-alvo para o comportamento. Cada vez que você digita uma letra na TextBox associada a esse comportamento, o manipulador de keyup é executado. O manipulador de keyup ativa ou desativa o botão, dependendo se a TextBox associada ao comportamento contém algum texto.

Lembre-se de que você deve compilar o arquivo JavaScript na Lista 3 como um recurso incorporado. Selecione o arquivo na janela Solution Explorer, abra a folha de propriedades e atribua o valor *Recurso Incorporado* à propriedade **Build Action** (consulte Figura 3). Esta opção está disponível tanto no Visual Studio quanto no Visual Web Developer.

[![Adicionando um arquivo JavaScript como um recurso incorporado](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**Figura 03**: Adicionar um arquivo JavaScript como um recurso incorporado[(Clique para exibir imagem em tamanho real)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png)

## <a name="creating-the-custom-extender-designer"></a>Criando o designer de extensor personalizado

Há uma última classe que precisamos criar para completar nosso extensor. Precisamos criar a classe de designer na Lista 4. Esta classe é necessária para que o extensor se comporte corretamente com o Visual Studio/Visual Web Developer Designer.

**Lista 4 - DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

Você associa o designer na Listagem 4 com o extensor DisabledButton com o atributo Designer. Você precisa aplicar o atributo Designer à classe DisabledButtonExtender assim:

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>Usando o extensor personalizado

Agora que terminamos de criar o extensor de controle DisabledButton, é hora de usá-lo em nosso ASP.NET site. Primeiro, precisamos adicionar o extensor personalizado à caixa de ferramentas. Siga estas etapas:

1. Abra uma página de ASP.NET clicando duas vezes na página na janela Do Explorador de Soluções.
2. Clique com o botão direito do mouse na caixa de ferramentas e selecione a opção menu **Escolha itens**.
3. Na caixa de diálogo Escolher itens da caixa de ferramentas, navegue até o conjunto CustomExtenders.dll.
4. Clique no botão **OK** para fechar a caixa de diálogo.

Depois de concluir essas etapas, o extensor de controle DisabledButton deve aparecer na caixa de ferramentas (veja Figura 4).

[![Botão desativado na caixa de ferramentas](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**Figura 04**: DesativadaBotão na caixa de ferramentas[(Clique para ver a imagem em tamanho real](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))

Em seguida, precisamos criar uma nova página ASP.NET. Siga estas etapas:

1. Crie uma nova página de ASP.NET chamada ShowDisabledButton.aspx.
2. Arraste um ScriptManager para a página.
3. Arraste um controle TextBox para a página.
4. Arraste um controle button para a página.
5. Na janela Propriedades, altere a propriedade ID de botão para o valor <em>btnSave</em> e a propriedade Text para o valor *\*Salvar*.

Criamos uma página com um padrão ASP.NET controle TextBox e Button.

Em seguida, precisamos estender o controle textbox com o extensor DisabledButton:

1. Selecione a opção **Adicionar extensor** para abrir a caixa de diálogo Assistente de Extensão (consulte Figura 5). Observe que a caixa de diálogo inclui nosso extensor de botões desativados personalizados.
2. Selecione o extensor DisabledButton e clique no botão **OK.**

[![A caixa de diálogo Assistente extensor](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**Figura 05**: A caixa de diálogo Assistente do Extensor[(Clique para exibir a imagem em tamanho real](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))

Finalmente, podemos definir as propriedades do extensor DisabledButton. Você pode modificar as propriedades do extensor DisabledButton modificando as propriedades do controle TextBox:

1. Selecione a TextBox no Designer.
2. Na janela Propriedades, expanda o nó Extensores (ver Figura 6).
3. Atribuir o valor *Salvar* à propriedade DisabledText e o valor *btnSave* à propriedade TargetButtonID.

[![Definindo propriedades do extensor](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**Figura 06**: Configuração das propriedades do extensor[(Clique para exibir a imagem em tamanho real](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))

Quando você executa a página (apertando F5), o controle Button é inicialmente desativado. Assim que você começar a inserir texto na TextBox, o controle Button está ativado (veja Figura 7).

[![O extensor Debotão desativado em ação](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**Figura 07**: O extensor DisabledButton em ação[(Clique para exibir imagem em tamanho real](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))

## <a name="summary"></a>Resumo

O objetivo deste tutorial foi explicar como você pode estender o AJAX Control Toolkit com controles de extensão personalizados. Neste tutorial, criamos um simples extensor de controle DisabledButton. Implementamos este extensor criando uma classe DisabledButtonExtender, um comportamento JavaScript deDisabledButtonBehavior e uma classe DisabledButtonDesigner. Você segue um conjunto semelhante de etapas sempre que criar um extensor de controle personalizado.

> [!div class="step-by-step"]
> [Próximo](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [anterior](get-started-with-the-ajax-control-toolkit-vb.md)
