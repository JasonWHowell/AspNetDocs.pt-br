---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: Usando controles de controle e extensores de controle (VB) do AJAX ControlKit | Microsoft Docs
author: rick-anderson
description: Aprenda a adicionar controles e extensores do AJAX Control Toolkit às suas páginas de ASP.NET.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 129d6841bc4db62ecbe5f26c4830d1ce2f199bff
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540006"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>Uso de controles e extensores de controle do AJAX Control Toolkit (VB)

pela [Microsoft](https://github.com/microsoft)

> Aprenda a adicionar controles e extensores do AJAX Control Toolkit às suas páginas de ASP.NET.

O AJAX Control Toolkit contém um conjunto de controles e extensores de controle. Neste breve tutorial, você aprende a adicionar controles e extensores de controle a uma página ASP.NET.

> [!NOTE] 
> 
> Para obter instruções sobre como instalar o AJAX Control Toolkit e adicionar o AJAX Control Toolkit à caixa de ferramentas do Visual Studio/Visual Web Developer, consulte o tutorial [Get Started com o AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).

## <a name="using-ajax-control-toolkit-controls"></a>Usando controles de ferramentas de controle AJAX

Um controle AJAX Control Toolkit funciona como um controle normal de ASP.NET. Você pode arrastar o controle da caixa de ferramentas para uma página ASP.NET. Você pode adicionar o controle à página na exibição Design ou na exibição Origem.

Há um requisito especial ao usar os controles do AJAX Control Toolkit. A página deve conter um controle ScriptManager. O controle do ScriptManager é responsável por incluir todos os JavaScript necessários pelos controles AJAX Control Toolkit.

Por exemplo, a guia AJAX Control Toolkit inclui um controle chamado controle Editor. Este controle exibe um editor HTML rico. Siga estas etapas para adicionar o controle do Editor a uma página:

1. Crie uma nova página de ASP.NET chamada ShowEditor.aspx
2. Selecione o controle ScriptManager abaixo da guia Extensões AJAX na caixa de ferramentas e arraste o controle para a página.
3. Selecione o controle do Editor abaixo da guia AJAX Control Toolkit na caixa de ferramentas e arraste o controle para a página (consulte Figura 1). O Designer deve parecer a Figura 2.
4. Execute o site selecionando a opção de menu **Debug, Start Debugging** ou atingindo a tecla F5.
5. Você deve ver a página na Figura 3.

[![Selecionando o controle do Editor HTML](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**Figura 01**: Selecionando o controle do editor HTML[(Clique para exibir a imagem em tamanho real)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png)

[![Visual Studio Designer com ScriptManager e controle de edição](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**Figura 02**: Visual Studio Designer com scriptmanager e controle de edição[(Clique para ver imagem em tamanho real)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png)

[![A página DisplayEditor.aspx](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**Figura 03**: A página DisplayEditor.aspx[(Clique para exibir imagem em tamanho real)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png)

## <a name="using-ajax-control-toolkit-control-extenders"></a>Usando extensores de controle de ferramentas de controle AJAX

O AJAX Control Toolkit também contém extensores de controle. Como o nome sugere, um extensor de controle amplia a funcionalidade de um controle existente. Por exemplo, o extensor de controle ConfirmButton amplia o controle padrão de botão ASP.NET. O extensor altera o comportamento do controle button para que o botão exiba uma caixa de confirmação quando você clica nele.

Um extensor de controle, assim como um controle AJAX Control Toolkit, requer um controle ScriptManager. Você deve adicionar um controle ScriptManager a uma página antes de começar a usar extensores de controle na página.

Siga estas etapas para usar o extensor de controle ConfirmButton:

1. Crie uma nova página de ASP.NET chamada ShowConfirmButton.aspx
2. Adicione um controle scriptmanager à página arrastando o controle para a página abaixo da guia Extensões AJAX.
3. Adicione um controle padrão de botão à página arrastando o botão abaixo da guia Padrão na caixa de ferramentas para a superfície do Designer.
4. Clique na opção **Adicionar extensor** (consulte Figura 4).
5. Na caixa de diálogo Escolher extensor, selecione ConfirmarBotãoExtender (ver Figura 5) e clique no botão OK.
6. Selecione o controle Button no Designer e\_expanda os extensores, botão1 confirmaro nó extensor na janela Propriedades (ver Figura 6). Atribuir o valor *realmente à* propriedade ConfirmText.
7. Execute a página selecionando a opção de menu **Depurar, Iniciar Depuração** ou apertar a tecla F5.

[![A opção de tarefa Adicionar extensor](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**Figura 04**: A opção de tarefa Adicionar extensor[(Clique para exibir a imagem em tamanho real)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png)

[![Selecionando o extensor de controle ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**Figura 05**: Selecionando o extensor de controle ConfirmButton[(Clique para exibir a imagem em tamanho real)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png)

[![Configuração de uma propriedade ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**Figura 06**: Configuração de uma propriedade ConfirmButton[(Clique para exibir a imagem em tamanho real)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png)

Quando a página é aberta, você deve ver um botão. Quando você clica no botão, você recebe a caixa de diálogo de confirmação na Figura 7.

[![Exibindo a caixa de confirmação](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**Figura 07**: Exibindo a caixa de confirmação[(Clique para exibir a imagem em tamanho real)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png)

Observe que você normalmente não arrasta um extensor de controle para uma página. Em vez disso, você usa a opção **adicionar** extensor para adicionar um extensor a um controle que você já adicionou a uma página. Observe, ainda, que você define propriedades de extensor de controle abrindo a folha de propriedade para que o controle seja estendido.

Um único controle ASP.NET pode ser estendido por vários extensores de controle. A folha de propriedades para o controle que está sendo estendido listará todos os extensores de controle associados ao controle.

> [!div class="step-by-step"]
> [Próximo](get-started-with-the-ajax-control-toolkit-vb.md)
> [anterior](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
