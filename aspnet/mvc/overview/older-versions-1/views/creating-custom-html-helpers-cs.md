---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Criando ajudantes HTML personalizados (C#) | Microsoft Docs
author: rick-anderson
description: O objetivo deste tutorial é demonstrar como você pode criar ajudas HTML personalizadas que você pode usar dentro de suas visualizações MVC. Aproveitando o HTML Helper...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 82e4118fd404051b891489b62d531169e83f450d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542554"
---
# <a name="creating-custom-html-helpers-c"></a>Criação de auxiliares de HTML personalizados (C#)

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> O objetivo deste tutorial é demonstrar como você pode criar ajudas HTML personalizadas que você pode usar dentro de suas visualizações MVC. Aproveitando os Ajudadores HTML, você pode reduzir a quantidade de digitação tediosa de tags HTML que você deve executar para criar uma página HTML padrão.

O objetivo deste tutorial é demonstrar como você pode criar ajudas HTML personalizadas que você pode usar dentro de suas visualizações MVC. Aproveitando os Ajudadores HTML, você pode reduzir a quantidade de digitação tediosa de tags HTML que você deve executar para criar uma página HTML padrão.

Na primeira parte deste tutorial, descrevo alguns dos ajudantes HTML existentes incluídos com a estrutura mvc ASP.NET. Em seguida, descrevo dois métodos de criação de ajudas HTML personalizadas: explico como criar ajudadores HTML personalizados criando um método estático e criando um método de extensão.

## <a name="understanding-html-helpers"></a>Entendendo os ajudantes de HTML

Um HTML Helper é apenas um método que retorna uma string. A seqüência pode representar qualquer tipo de conteúdo que você quiser. Por exemplo, você pode usar ajudadores HTML `<input>` para `<img>` renderizar tags HTML padrão como HTML e tags. Você também pode usar ajudadores HTML para renderizar conteúdo mais complexo, como uma tira de guia ou uma tabela HTML de dados de banco de dados.

A ASP.NET estrutura MVC inclui o seguinte conjunto de ajudantes HTML padrão (esta não é uma lista completa):

- Html.ActionLink()
- html.BeginForm()
- html.Caixa de seleção()
- html.dropdownlist()
- html.endform()
- Html.Hidden()
- html.ListBox()
- html.Password()
- Html.RadioButton()
- Html.TextArea()
- html.textbox()

Por exemplo, considere o formulário na Lista 1. Este formulário é renderizado com a ajuda de dois dos ajudantes HTML padrão (ver Figura 1). Este formulário `Html.BeginForm()` usa `Html.TextBox()` os métodos e Helper para renderizar um formulário HTML simples.

[![Página renderizada com ajudadores HTML](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**Figura 01**: Página renderizada com ajudadores HTML[(Clique para ver imagem em tamanho real)](creating-custom-html-helpers-cs/_static/image3.png)

**Listagem 1 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

O método Deajuda html.BeginForm() é usado para `<form>` criar as tags HTML de abertura e fechamento. Observe que `Html.BeginForm()` o método é chamado dentro de uma declaração de uso. A declaração de `<form>` uso garante que a tag seja fechada no final do bloco de uso.

Se preferir, em vez de criar um bloco de uso, você pode chamar `<form>` o método de ajuda Html.EndForm() para fechar a tag. Use qualquer abordagem para criar `<form>` uma tag de abertura e fechamento que pareça mais intuitiva para você.

Os `Html.TextBox()` métodos Helper são usados `<input>` na Listagem 1 para renderizar tags HTML. Se você selecionar a fonte de exibição no seu navegador, verá a fonte HTML na Listagem 2. Observe que a fonte contém tags HTML padrão.

> [!IMPORTANT]
> observe que `Html.TextBox()`o -HTML Helper `<%= %>` é `<% %>` renderizado com tags em vez de tags. Se você não incluir o sinal de igual, então nada será renderizado para o navegador.

A ASP.NET estrutura MVC contém um pequeno conjunto de ajudantes. Provavelmente, você precisará estender a estrutura MVC com ajudadores HTML personalizados. No restante deste tutorial, você aprende dois métodos de criação de ajudas HTML personalizadas.

**Listagem 2 –`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>Criando ajudadores HTML com métodos estáticos

A maneira mais fácil de criar um novo HTML Helper é criar um método estático que retorne uma seqüência. Imagine, por exemplo, que você decida criar um novo `<label>` Html Helper que renderiza uma tag HTML. Você pode usar a classe na `<label>` Listagem 2 para renderizar um .

**Listagem 2 –`Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

Não há nada de especial na classe na Lista 2. O `Label()` método simplesmente retorna uma seqüência.

A exibição Índice modificado `LabelHelper` na Listagem `<label>` 3 usa as tags HTML para renderizar. Observe que a exibição inclui `<%@ imports %>` `Application1.Helpers` uma diretiva que importa o namespace.

**Listagem 2 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Criando ajudadores HTML com métodos de extensão

Se você quiser criar ajudadores HTML que funcionam como os ajudantes HTML padrão incluídos na estrutura ASP.NET MVC, então você precisa criar métodos de extensão. Os métodos de extensão permitem adicionar novos métodos a uma classe existente. Ao criar um método HTML Helper, você adiciona novos métodos à classe HtmlHelper representada pela propriedade Html de uma exibição.

A classe na Listagem 3 adiciona `HtmlHelper` um `Label()`método de extensão à classe nomeada . Há algumas coisas que você deve notar sobre esta classe. Primeiro, note que a classe é uma classe estática. Você deve definir um método de extensão com uma classe estática.

Em segundo lugar, observe que `Label()` o primeiro parâmetro do `this`método é precedido pela palavra-chave . O primeiro parâmetro de um método de extensão indica a classe que o método de extensão se estende.

**Lista 3 –`Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

Depois de criar um método de extensão e construir seu aplicativo com sucesso, o método de extensão aparece no Visual Studio Intellisense como todos os outros métodos de uma classe (ver Figura 2). A única diferença é que os métodos de extensão aparecem com um símbolo especial ao lado deles (um ícone de uma seta para baixo).

[![Usando o método de extensão Html.Label()](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**Figura 02**: Usando o método de extensão Html.Label()[(Clique para exibir imagem em tamanho real)](creating-custom-html-helpers-cs/_static/image6.png)

A exibição Índice modificado na Listagem 4 usa o método `<label>` de extensão Html.Label() para renderizar todas as suas tags.

**Lista 4 –`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu dois métodos de criação de ajudas HTML personalizadas. Primeiro, você aprendeu como `Label()` criar um Html Helper personalizado criando um método estático que retorna uma string. Em seguida, você aprendeu `Label()` como criar um método html `HtmlHelper` helper personalizado criando um método de extensão na classe.

Neste tutorial, eu me concentrei em construir um método extremamente simples de Ajuda HTML. Perceba que um ajudante HTML pode ser tão complicado quanto você quiser. Você pode criar ajudadores HTML que renderizam conteúdo rico, como visualizações de árvores, menus ou tabelas de dados de banco de dados.

> [!div class="step-by-step"]
> [Próximo](asp-net-mvc-views-overview-cs.md)
> [anterior](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
