---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: Usando o Extensor de Controle ColorPicker (VB) | Microsoft Docs
author: rick-anderson
description: O ColorPicker é um extensor aJAX ASP.NET que fornece a funcionalidade de escolha de cores do lado do cliente com a IU em um controle pop-up. Pode ser anexado a qualquer ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: c373102665ac17020ca8d5f14d3488a874bb68de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542840"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>Usando o extensor de controle colorpicker (VB)

pela [Microsoft](https://github.com/microsoft)

> O ColorPicker é um extensor aJAX ASP.NET que fornece a funcionalidade de escolha de cores do lado do cliente com a IU em um controle pop-up. Ele pode ser anexado a qualquer ASP.NET controle TextBox. Ele.

O objetivo deste tutorial é explicar como você pode usar o extensor de controle AJAX Control Toolkit ColorPicker. O extensor de controle ColorPicker exibe uma caixa de diálogo pop-up que permite selecionar uma cor. O ColorPicker é útil sempre que você quiser fornecer uma interface de usuário intuitiva para um usuário escolher uma cor.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>Estendendo um controle textbox com o extensor de controle colorpicker

Imagine, por exemplo, que você deseja criar um site que permita aos visitantes criar cartões de visita personalizados. Os visitantes podem inserir o texto para um cartão de visita e escolher a cor. A página ASP.NET na Lista 1 contém dois controles TextBox chamados txtCardText e txtCardColor. Ao enviar o formulário, os valores selecionados são exibidos (veja figura 1).

[![Formulário simples para criar um cartão de visita](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**Figura 01**: Formulário simples para criar um cartão de visita ([Clique para ver imagem em tamanho real](using-the-colorpicker-control-extender-vb/_static/image2.png))

**Listagem 1 - CreateCard.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

O formulário na Lista 1 funciona, mas não proporciona uma grande experiência ao usuário. O usuário tem que digitar uma cor na caixa de texto. Se o usuário quiser uma cor especializada - por exemplo, apenas o tom certo de verde ervilha - então o usuário deve descobrir o código de cor HTML sem qualquer ajuda.

Você pode usar o extensor de controle ColorPicker para criar uma melhor experiência do usuário. O ColorPicker exibe uma caixa de diálogo de cores quando você move o foco para um controle TextBox (ver Figura 2).

[![O extensor de controle colorpicker](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**Figura 02**: O extensor de controle ColorPicker[(Clique para exibir a imagem em tamanho real)](using-the-colorpicker-control-extender-vb/_static/image4.png)

Você precisa completar duas etapas para usar o extensor de controle ColorPicker com o formulário na Lista 1:

1. Adicione um controle scriptmanager à página
2. Adicione o extensor de controle ColorPicker à página

Antes de usar o ColorPicker, você deve adicionar um ScriptManager à sua página. Um bom lugar para adicionar o ScriptManager está &lt;&gt; logo abaixo da tag de formulário do lado do servidor de abertura. Você pode arrastar o ScriptManager para a página da caixa de ferramentas (o ScriptManager está localizado na guia Extensões AJAX). Alternativamente, você pode digitar a seguinte tag em Exibição de origem abaixo da tag de formulário do lado do servidor de abertura:

&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;

A maneira mais fácil de adicionar o extensor de controle ColorPicker à página está no Design View. Se você passar o mouse sobre o txtCardColor TextBox, uma opção de tarefa inteligente aparecerá, o permitirá adicionar um extensor (consulte Figura 3). Se você escolher esta opção, o Assistente extensor será exibido (consulte Figura 4).

[![Adicionando um extensor](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**Figura 03**: Adicionar um extensor[(Clique para exibir imagem em tamanho real)](using-the-colorpicker-control-extender-vb/_static/image6.png)

[![Selecionando um extensor de controle com o Assistente extensor](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**Figura 04**: Selecionando um extensor de controle com o Assistente extensor[(Clique para exibir a imagem em tamanho real)](using-the-colorpicker-control-extender-vb/_static/image8.png)

Você pode escolher o extensor ColorPicker para estender o txtCardColor TextBox com o extensor ColorPicker. Clique em OK para fechar o diálogo.

Depois de fazer essas alterações, a fonte da página se parece com a Listagem 2.

**Listagem 2 - CreateCard.aspx (com ColorPicker)**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

Observe que a página agora contém um controle ColorPickerExtender que aparece diretamente abaixo do controle txtCardColor TextBox. O controle ColorPickerExtender estende o controle txtCardColor para que ele exiba uma caixa de diálogo de seletor de cores.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>Usando um botão para iniciar a caixa de diálogo seletor de cores

O extensor ColorPicker suporta as seguintes propriedades:

- PopupButtonId - O ID de um botão na página que faz com que a caixa de diálogo do seletor de cores apareça.
- PopupPosition - A posição, em relação ao controle de destino, da caixa de diálogo do seletor de cores. Os valores possíveis são Absoluto, Central, Inferior Esquerdo, Inferior Direito, TopLeft, TopRight, Direita e Esquerda (o padrão é Bottom Left).
- SampleControlId - O ID de um controle que exibe a cor selecionada.
- SelectedColor - A cor inicial selecionada pelo ColorPicker.

Você pode usar essas propriedades para personalizar como a caixa de diálogo do seletor de cores é exibida e como a cor selecionada é exibida. A página na Lista 3 ilustra como você pode usar várias dessas propriedades.

**Listagem 3 - CreateCardButton.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

A página na Lista 3 inclui um botão Escolher cor (ver Figura 5). Quando você clica neste botão, a caixa de diálogo do seletor de cores aparece acima da TextBox. Se você selecionar uma cor na caixa de diálogo, a cor selecionada será exibida como a cor de fundo do controle lblSample Label.

A propriedade ColorPicker PopupButtonID é usada para associar o botão Pick Color com o extensor ColorPicker. Quando você fornece um valor para a propriedade PopupButtonID, a caixa de diálogo seletor de cores não aparece mais quando o controle de destino tem foco. Você deve clicar no botão para exibir a caixa de diálogo.

A propriedade SampleControlID é usada para associar um controle que exibe a cor selecionada com o ColorPicker. O ColorPicker altera a cor de fundo deste controle para a cor selecionada no momento.

[![Exibindo a caixa de diálogo do seletor de cores com um botão](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**Figura 05**: Exibindo a caixa de diálogo do seletor de cores com um botão[(Clique para ver a imagem em tamanho real)](using-the-colorpicker-control-extender-vb/_static/image10.png)

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu a usar o extensor de controle ColorPicker para exibir uma caixa de diálogo de seleção de cores popup. Primeiro, examinamos como você pode exibir a caixa de diálogo quando o foco é movido para um controle TextBox. Em seguida, você aprendeu como criar um botão que exibe a caixa de diálogo do seletor de cores quando o botão é clicado.

> [!div class="step-by-step"]
> [Anterior](using-the-colorpicker-control-extender-cs.md)
