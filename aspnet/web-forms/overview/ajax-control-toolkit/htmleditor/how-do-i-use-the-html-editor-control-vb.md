---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: Como uso o Controle de Editor HTML? (VB) | Microsoft Docs
author: rick-anderson
description: HTMLEditor é um ASP.NET Controle AJAX que permite criar e editar facilmente conteúdo HTML através de botões em uma barra de ferramentas.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: bba42b4b6ff130b209b92c1608bc37f2f574c19c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542827"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a>Como uso o Controle de Editor HTML? (VB)

pela [Microsoft](https://github.com/microsoft)

> HTMLEditor é um ASP.NET Controle AJAX que permite criar e editar facilmente conteúdo HTML através de botões em uma barra de ferramentas.

O objetivo deste tutorial é fornecer uma visão geral do controle do Editor HTML incluído no AJAX Control Toolkit. O Editor HTML inclui opções para alterar o tamanho da fonte, selecionar uma fonte, alterar a cor de fundo, modificar a cor do primeiro plano, adicionar links, adicionar imagens, alterar o alinhamento de texto e executar operações de corte, cópia e colar (ver Figura 1).

[![O Editor HTML](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)

**Figura 01**: O Editor HTML[(Clique para ver imagem em tamanho real)](how-do-i-use-the-html-editor-control-vb/_static/image2.png)

O editor HTML permite que você insira conteúdo usando um modo de design ou você pode inserir HTML diretamente. Você também tem a opção de visualizar seu conteúdo HTML (veja figura 2).

[![Botões de design, HTML e Visualização](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)

**Figura 02**: Botões de design, HTML e visualização[(Clique para ver a imagem em tamanho real)](how-do-i-use-the-html-editor-control-vb/_static/image4.png)

Neste tutorial, você aprende como exibir o Editor HTML, como personalizar os botões da barra de ferramentas que aparecem no Editor HTML e como evitar ataques de scripts entre sites.

## <a name="displaying-the-html-editor"></a>Exibindo o Editor HTML

Antes de usar o Editor HTML em uma página ASP.NET, primeiro você deve adicionar um controle ScriptManager à página. O controle ScriptManager está localizado abaixo da guia Extensões AJAX na caixa de ferramentas Visual Studio/Visual Web Developer Express.

Você deve colocar o controle ScriptManager no topo da página antes de qualquer outro controle na página. Por exemplo, você pode colocá-lo imediatamente &lt;abaixo&gt; da tag de formulário do lado do servidor de abertura.

O controle do Editor HTML está localizado na caixa de ferramentas com o resto dos controles do AJAX Control Toolkit. Ele é chamado de controle editor (ver Figura 3).

[![O controle do Editor HTML](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)

**Figura 03**: O controle do editor HTML[(Clique para ver a imagem em tamanho real)](how-do-i-use-the-html-editor-control-vb/_static/image6.png)

Depois de arrastar o Editor HTML para uma página, você pode definir suas propriedades na folha de propriedades. Por exemplo, você normalmente deseja definir as propriedades Largura e Altura. A listagem 1 contém a fonte de uma página ASP.NET que contém um editor HTML.

**Listagem 1 - SimpleEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

A página na Lista 1 contém um controle HTML Editor, um controle button e um controle literal. Quando você clica no botão, o conteúdo do Editor HTML aparece no controle Literal (ver Figura 4).

[![Enviando um formulário com um editor HTML](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)

**Figura 04**: Enviar um formulário com um editor HTML[(Clique para exibir imagem em tamanho real)](how-do-i-use-the-html-editor-control-vb/_static/image8.png)

A propriedade HTML Editor Content é usada para recuperar o conteúdo HTML inserido no Editor HTML. Esteja ciente de que este conteúdo HTML pode conter JavaScript. Na próxima seção, discutimos como você pode prevenir ataques de injeção JavaScript.

## <a name="customizing-the-html-editor-toolbar"></a>Personalização da barra de ferramentas do editor HTML

Você pode personalizar exatamente quais botões aparecem no editor. Por exemplo, você pode querer remover a guia HTML para evitar que os usuários mudem o Editor HTML para o modo HTML. Ou, você pode querer remover a lista de isento de tamanho de fonte para evitar que os usuários criem textos excessivamente grandes em uma postagem de mensagem do fórum (ver Figura 5).

[![Um editor HTML personalizado](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)

**Figura 05**: Um editor HTML personalizado[(Clique para ver imagem em tamanho real)](how-do-i-use-the-html-editor-control-vb/_static/image10.png)

Você personaliza os botões da barra de ferramentas, derivando um novo Editor HTML da classe editor base. Por exemplo, o editor personalizado na Lista 2 contém apenas botões de barra de ferramentas para negrito e itálico. Todos os outros botões da barra de ferramentas foram removidos. Além disso, a guia HTML foi removida da parte inferior do editor (mas as guias Design e Preview ainda estão lá).

**Lista 2\_- Código do aplicativo\CustomEditor.vb**

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

Você deve adicionar a classe na\_Lista 2 à sua pasta Código do aplicativo para que a classe seja compilada automaticamente. Se a\_pasta Código do Aplicativo não existir em seu site, então você pode simplesmente adicionar a pasta.

Depois de criar um editor personalizado, você pode adicioná-lo a uma ASP.NET página da mesma forma que adicionar o Editor HTML normal (veja Lista 3).

**Listagem 3 - ShowCustomEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>Evitando ataques de scripts entre sites (XSS)

Sempre que você aceitar a entrada de um usuário e reexibir essa entrada em seu site, você potencialmente abrirá seu site para ataques de scripts de sites cruzados (XSS). Em teoria, um hacker mal-intencionado poderia enviar código JavaScript que é executado quando a entrada é reexibida. O JavaScript pode ser usado para roubar senhas de usuário ou outras informações confidenciais.

Normalmente, você pode derrotar ataques XSS codificando qualquer entrada que você recuperar de um usuário antes de exibi-lo em uma página da Web. No entanto, a codificação HTML da saída &lt;&gt; do Editor HTML não apenas codificaria tags de script, mas também codificaria todas as tags HTML. Em outras palavras, você perderia toda a formatação, como o tipo de fonte, o tamanho da fonte e a cor de fundo.

Se você está coletando informações confidenciais de seus usuários - como senhas, números de cartão de crédito e números de segurança social - então você não deve exibir conteúdo não codificado que você recupera de um usuário com o Editor HTML. Você deve usar o Editor HTML apenas em situações em que você não está reexibindo o conteúdo HTML, ou o conteúdo HTML está sendo submetido ao seu site por uma parte confiável.

Imagine, por exemplo, que você está criando um aplicativo de blog. Nesta situação, faz sentido usar o Editor HTML ao compor postagens de blog. Você é o único que envia um post de blog e, presumivelmente, você pode confiar em si mesmo para não enviar JavaScript malicioso. No entanto, não faz sentido usar o Editor HTML ao permitir que usuários anônimos publiquem comentários. Você deve ser especialmente cuidadoso em situações em que os usuários enviam informações confidenciais, como senhas. Potencialmente, um usuário mal-intencionado poderia postar um comentário que contenha o JavaScript certo para roubar uma senha.

## <a name="summary"></a>Resumo

Neste tutorial, você foi fornecido com uma breve visão geral do controle do Editor HTML incluído no AJAX Control Toolkit. Você aprendeu a usar o Editor HTML para aceitar conteúdo rico de um usuário e enviar o conteúdo para o servidor. Também discutimos como você pode personalizar os botões da barra de ferramentas que são exibidos pelo Editor HTML. Finalmente, você aprendeu como evitar ataques de scripts entre sites ao usar o Editor HTML para aceitar entradas potencialmente maliciosas.

> [!div class="step-by-step"]
> [Anterior](how-do-i-use-the-html-editor-control-cs.md)
