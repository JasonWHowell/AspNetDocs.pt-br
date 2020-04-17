---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: Criando layouts de páginas com páginas-mestre de exibição (VB) | Microsoft Docs
author: rick-anderson
description: Neste tutorial, você aprende como criar um layout de página comum para várias páginas em seu aplicativo, aproveitando as páginas-mestre de exibição. Você pode usar um...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 37b8d858c72357ebbe51458f76511a9672b01b4d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542489"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>Criar layouts de página com Exibir páginas mestras (VB)

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> Neste tutorial, você aprende como criar um layout de página comum para várias páginas em seu aplicativo, aproveitando as páginas-mestre de exibição. Você pode usar uma página-mestre de exibição, por exemplo, para definir um layout de página de duas colunas e usar o layout de duas colunas para todas as páginas do seu aplicativo web.

## <a name="creating-page-layouts-with-view-master-pages"></a>Criando layouts de página com páginas-mestre de exibição

Neste tutorial, você aprende como criar um layout de página comum para várias páginas em seu aplicativo, aproveitando as páginas-mestre de exibição. Você pode usar uma página-mestre de exibição, por exemplo, para definir um layout de página de duas colunas e usar o layout de duas colunas para todas as páginas do seu aplicativo web.

Você também pode aproveitar as páginas-mestre de exibição para compartilhar conteúdo comum em várias páginas em seu aplicativo. Por exemplo, você pode colocar o logotipo do seu site, links de navegação e anúncios de banner em uma página-mestre de exibição. Dessa forma, cada página do seu aplicativo exibiria esse conteúdo automaticamente.

Neste tutorial, você aprende como criar uma nova página-mestre de exibição e criar uma nova página de conteúdo de exibição com base na página-mestre.

### <a name="creating-a-view-master-page"></a>Criando uma página-mestre de exibição

Vamos começar criando uma página-mestre de exibição que define um layout de duas colunas. Você adiciona uma nova página-mestre de exibição a um projeto MVC clicando com o botão direito do mouse na pasta 'Exibição\', selecionando a opção menu **Adicionar, Novo Item**e selecionar o modelo MVC Exibir página mestre (ver Figura 1).

[![Adicionando uma página-mestre de exibição](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**Figura 01**: Adicionar uma página-mestre de exibição[(Clique para exibir imagem em tamanho real)](creating-page-layouts-with-view-master-pages-vb/_static/image3.png)

Você pode criar mais de uma página-mestre de exibição em um aplicativo. Cada página-mestre de exibição pode definir um layout de página diferente. Por exemplo, você pode querer que certas páginas tenham um layout de duas colunas e outras páginas para ter um layout de três colunas.

Uma página-mestre de exibição se parece muito com uma exibição padrão ASP.NET MVC. No entanto, ao contrário de uma exibição normal, uma página-mestre de exibição contém uma ou mais `<asp:ContentPlaceHolder>` tags. As `<contentplaceholder>` tags são usadas para marcar as áreas da página-mestre que podem ser substituídas em uma página de conteúdo individual.

Por exemplo, a página-mestre de exibição na Listagem 1 define um layout de duas colunas. Contém duas `<contentplaceholder>` etiquetas. Uma `<ContentPlaceHolder>` para cada coluna.

**Listagem 1 –`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

O corpo da página-mestre de `<div>` exibição na Lista 1 contém duas tags que correspondem às duas colunas. A classe de coluna Folha de estilo `<div>` em cascata é aplicada a ambas as tags. Esta classe é definida na folha de estilos declarada na parte superior da página-mestre. Você pode visualizar como a página-mestre de exibição será renderizada mudando para exibição design. Clique na guia Design no canto inferior esquerdo do editor de código-fonte (consulte Figura 2).

[![Visualização de uma página mestra no designer](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**Figura 02**: Visualização de uma página-mestre no designer[(Clique para ver imagem em tamanho real)](creating-page-layouts-with-view-master-pages-vb/_static/image6.png)

### <a name="creating-a-view-content-page"></a>Criando uma página de conteúdo de exibição

Depois de criar uma página-mestre de exibição, você pode criar uma ou mais páginas de conteúdo de exibição com base na página-mestre da exibição. Por exemplo, você pode criar uma página de conteúdo de exibição de índice para o controlador Home clicando com o botão direito do mouse na pasta Views\Home, selecionando **Adicionar, Novo Item,** selecionando o modelo **de página de conteúdo de exibição do MVC,** digitando o nome Index.aspx e clicando no botão Adicionar (ver Figura 3).

[![Adicionando uma página de conteúdo de exibição](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**Figura 03**: Adicionar uma página de conteúdo de exibição[(Clique para exibir imagem em tamanho real)](creating-page-layouts-with-view-master-pages-vb/_static/image9.png)

Depois de clicar no botão Adicionar, aparece uma nova caixa de diálogo que permite selecionar uma página-mestre de exibição para associar-se à página de conteúdo de exibição (consulte Figura 4). Você pode navegar até a página-mestre do Site.master view que criamos na seção anterior.

[![Selecionando uma página-mestre](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**Figura 04**: Selecionando uma página-mestre[(Clique para exibir imagem em tamanho real)](creating-page-layouts-with-view-master-pages-vb/_static/image12.png)

Depois de criar uma nova página de conteúdo de exibição com base na página do Site.master, você recebe o arquivo na Lista 2.

**Listagem 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

Observe que esta `<asp:Content>` exibição contém uma tag `<asp:ContentPlaceHolder>` que corresponde a cada uma das tags na página-mestre da exibição. Cada `<asp:Content>` tag inclui um atributo ContentPlaceHolderID `<asp:ContentPlaceHolder>` que aponta para o particular que ele substitui.

Observe, ainda, que a página de exibição de conteúdo na Listagem 2 não contém nenhuma das tags HTML de abertura e fechamento normais. Por exemplo, não contém a `<html>` abertura `<head>` e o fechamento ou as tags. Todas as tags normais de abertura e fechamento estão contidas na página mestre da exibição.

Qualquer conteúdo que você deseja exibir em uma página `<asp:Content>` de conteúdo de exibição deve ser colocado dentro de uma tag. Se você colocar qualquer HTML ou outro conteúdo fora dessas tags, então você terá um erro ao tentar visualizar a página.

Você não precisa substituir todas `<asp:ContentPlaceHolder>` as tag de uma página-mestre em uma página de exibição de conteúdo. Você só precisa substituir `<asp:ContentPlaceHolder>` uma tag quando quiser substituir a tag por conteúdo específico.

Por exemplo, a exibição Índice modificado `<asp:Content>` na Listagem 3 contém apenas duas tags. Cada uma `<asp:Content>` das tags inclui algum texto.

**Lista 3 –`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

Quando a exibição na Lista 3 é solicitada, ela renderiza a página na Figura 5. Observe que a exibição renderiza uma página com duas colunas. Observe, ainda, que o conteúdo da página de conteúdo de exibição é mesclado com o conteúdo da página-mestre da exibição.

[![A página de conteúdo de exibição do Índice](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**Figura 05**: A página de conteúdo de exibição do Índice[(Clique para ver a imagem em tamanho real)](creating-page-layouts-with-view-master-pages-vb/_static/image15.png)

### <a name="modifying-view-master-page-content"></a>Modificando o conteúdo da página-mestre de exibição

Um problema que você encontra quase imediatamente ao trabalhar com páginas-mestre de exibição é o problema de modificar o conteúdo da página-mestre de exibição quando diferentes páginas de conteúdo de exibição são solicitadas. Por exemplo, você quer que cada página em seu aplicativo web tenha um título exclusivo. No entanto, o título é declarado na página-mestre de exibição e não na página de conteúdo de exibição. Então, como você personaliza o título da página para cada página de conteúdo de exibição?

Existem duas maneiras de modificar o título exibido por uma página de conteúdo de exibição. Primeiro, você pode atribuir um título de `<%@ page %>` página ao atributo título da diretiva declarada na parte superior de uma página de conteúdo de exibição. Por exemplo, se você quiser atribuir o título da página "Super Grande Site" à exibição Índice, então você pode incluir a seguinte diretiva na parte superior da exibição Índice:

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

Quando a exibição Índice é renderizada no navegador, o título desejado aparece na barra de título do navegador:

[![Barra de título do navegador](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

Há um requisito importante que uma página de exibição mestre deve satisfazer para que o atributo título funcione. A página-mestre de `<head runat="server">` exibição deve `<head>` conter uma tag em vez de uma tag normal para seu cabeçalho. Se `<head>` a tag não incluir o atributo runat="server", o título não aparecerá. A página-mestre de exibição padrão inclui a tag necessária. `<head runat="server">`

Uma abordagem alternativa para modificar o conteúdo da página de conteúdo de página `<asp:ContentPlaceHolder>` de exibição individual é envolver a região que você deseja modificar em uma tag. Por exemplo, imagine que você deseja alterar não apenas o título, mas também as metas de visualização, renderizadas por uma página de exibição mestre. A página de exibição `<asp:ContentPlaceHolder>` mestre na `<head>` Lista 4 contém uma tag dentro de sua tag.

**Lista 4 –`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

Observe que `<asp:ContentPlaceHolder>` a tag na Lista 4 inclui conteúdo padrão: um título padrão e metas de meta padrão. Se você não substituir `<asp:ContentPlaceHolder>` essa tag em uma página de conteúdo de exibição individual, o conteúdo padrão será exibido.

A página de exibição de `<asp:ContentPlaceHolder>` conteúdo na Lista 5 substitui a tag para exibir um título personalizado e metas de metas personalizadas.

**Lista 5 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>Resumo

Este tutorial forneceu uma introdução básica para exibir páginas-mestre e visualizar páginas de conteúdo. Você aprendeu a criar novas páginas-mestre de exibição e criar páginas de conteúdo de exibição com base nelas. Também examinamos como você pode modificar o conteúdo de uma página-mestre de exibição a partir de uma página de conteúdo de exibição específica.

> [!div class="step-by-step"]
> [Próximo](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [anterior](passing-data-to-view-master-pages-vb.md)
