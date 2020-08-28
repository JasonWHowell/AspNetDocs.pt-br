---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: Usando controles do AJAX Control Toolkit e extensores de controle (C#) | Microsoft Docs
author: rick-anderson
description: Saiba como adicionar controles e extensores do AJAX Control Toolkit às suas páginas do ASP.NET.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 48c8479fce6d121b8a4f03d972ac4117ed974958
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044500"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>Uso de controles e extensores de controle do AJAX Control Toolkit (C#)

pela [Microsoft](https://github.com/microsoft)

> Saiba como adicionar controles e extensores do AJAX Control Toolkit às suas páginas do ASP.NET.

O AJAX Control Toolkit contém um conjunto de controles e extensores de controle. Neste breve tutorial, você aprenderá a adicionar controles e extensores de controle a uma página do ASP.NET.

> [!NOTE] 
> 
> Para obter instruções sobre como instalar o AJAX Control Toolkit e adicionar o AJAX Control Toolkit à caixa de ferramentas do Visual Studio/Visual Web Developer, consulte o tutorial [introdução ao AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).

## <a name="using-ajax-control-toolkit-controls"></a>Usando controles AJAX Control Toolkit

Um controle do AJAX Control Toolkit funciona exatamente como um controle ASP.NET normal. Você pode arrastar o controle da caixa de ferramentas para uma página do ASP.NET. Você pode adicionar o controle à página na exibição modo de exibição de Design ou código-fonte.

Há um requisito especial ao usar os controles do AJAX Control Toolkit. A página deve conter um controle ScriptManager. O controle ScriptManager é responsável por incluir todo o JavaScript necessário exigido pelos controles AJAX Control Toolkit.

Por exemplo, a guia AJAX Control Toolkit inclui um controle chamado de controle editor. Esse controle exibe um editor de HTML rico. Siga estas etapas para adicionar o controle do editor a uma página:

1. Crie uma nova página do ASP.NET denominada do defaultediter. aspx
2. Selecione o controle ScriptManager sob a guia extensões AJAX na caixa de ferramentas e arraste o controle para a página.
3. Selecione o controle editor sob a guia AJAX Control Toolkit na caixa de ferramentas e arraste o controle para a página (consulte a Figura 1). O designer deve ser semelhante à figura 2.
4. Execute o site selecionando a opção de menu **depurar, iniciar depuração** ou pressionar a tecla F5.
5. Você deve ver a página na Figura 3.

[![Selecionando o controle do editor de HTML](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**Figura 01**: selecionando o controle do editor de HTML ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))

[![Designer do Visual Studio com ScriptManager e controle de edição](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**Figura 02**: designer do Visual Studio com o ScriptManager e o controle de edição ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))

[![A página DisplayEditor. aspx](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**Figura 03**: a página DisplayEditor. aspx ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>Usando extensores de controle do AJAX Control Toolkit

O AJAX Control Toolkit também contém extensores de controle. Como o nome sugere, um extensor de controle estende a funcionalidade de um controle existente. Por exemplo, o extensor de controle ConfirmButton estende o controle de botão ASP.NET padrão. O extensor altera o comportamento do controle de botão para que o botão exiba uma caixa de diálogo de confirmação quando você clicar nele.

Um extensor de controle, assim como um controle AJAX Control Toolkit, requer um controle ScriptManager. Você deve adicionar um controle ScriptManager a uma página antes de começar a usar extensores de controle na página.

Siga estas etapas para usar o extensor de controle ConfirmButton:

1. Crie uma nova página do ASP.NET chamada ShowConfirmButton. aspx
2. Adicione um controle ScriptManager à página arrastando o controle para a página sob a guia extensões AJAX.
3. Adicione um controle botão padrão à página arrastando o botão de baixo da guia padrão na caixa de ferramentas para a superfície do designer.
4. Clique na opção Adicionar tarefa de **extensor** (consulte a Figura 4).
5. Na caixa de diálogo escolher extensor, selecione ConfirmButtonExtender (veja a Figura 5) e clique no botão OK.
6. Selecione o controle de botão no designer e expanda o nó Extenders, Button1 \_ ConfirmButtonExtender no janela Propriedades (consulte a Figura 6). Atribuir o valor *' realmente? '* para a propriedade ConfirmText.
7. Execute a página selecionando a opção de menu **depurar, iniciar depuração** ou pressionar a tecla F5.

[![A opção de tarefa adicionar extensor](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**Figura 04**: a opção Adicionar tarefa de extensor ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))

[![Selecionando o extensor de controle ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**Figura 05**: selecionando o extensor de controle ConfirmButton ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))

[![Definindo uma propriedade ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**Figura 06**: definindo uma propriedade ConfirmButton ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))

Quando a página for aberta, você deverá ver um botão. Ao clicar no botão, você receberá a caixa de diálogo de confirmação na Figura 7.

[![Exibindo a caixa de diálogo de confirmação](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**Figura 07**: exibindo a caixa de diálogo de confirmação ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))

Observe que você normalmente não arrasta um extensor de controle para uma página. Em vez disso, use a opção Adicionar tarefa de **extensor** para adicionar um extensor a um controle que você já adicionou a uma página. Observe, além disso, que você define as propriedades do extensor de controle abrindo a folha de propriedades para o controle que está sendo estendido.

Um único controle ASP.NET pode ser estendido por vários extensores de controle. A folha de propriedades do controle que está sendo estendido listará todos os extensores de controle associados ao controle.

> [!div class="step-by-step"]
> [Anterior](get-started-with-the-ajax-control-toolkit-cs.md) 
>  [Avançar](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
