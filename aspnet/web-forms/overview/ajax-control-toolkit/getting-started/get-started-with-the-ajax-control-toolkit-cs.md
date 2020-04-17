---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Comece com o AJAX Control Toolkit (C#) | Microsoft Docs
author: rick-anderson
description: Aprenda tudo o que você precisa saber para começar a usar o AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: b5954019ec3312f06f38012e4d3f9b1f71573f76
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543581"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a>Introdução ao AJAX Control Toolkit (C#)

pela [Microsoft](https://github.com/microsoft)

> Aprenda tudo o que você precisa saber para começar a usar o AJAX Control Toolkit.

O AJAX Control Toolkit contém mais de 30 controles gratuitos que você pode usar em seus aplicativos de ASP.NET. Neste tutorial, você aprende a baixar o AJAX Control Toolkit e adicionar os controles do kit de ferramentas à sua caixa de ferramentas Visual Studio/Visual Web Developer Express.

## <a name="downloading-the-ajax-control-toolkit"></a>Baixando o AJAX Control Toolkit

O [AJAX Control Toolkit](http://devexpress.com/act) é um projeto de código aberto desenvolvido pelos membros da comunidade ASP.NET e da equipe ASP.NET. 

[![Baixando o AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**Figura 01**: Baixar o AJAX Control Toolkit[(Clique para ver imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png)

Depois de baixar o arquivo, você precisa desbloquear o arquivo. Clique com o botão direito do mouse no arquivo, selecione Propriedades e clique no botão **Desbloquear** (consulte Figura 2).

[![Desbloqueando o arquivo ZIP do AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**Figura 02**: Desbloquear o arquivo ZIP do AJAX Control Toolkit[(Clique para exibir a imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png)

Depois de desbloquear o arquivo, você pode descompactar o arquivo: Clique com o botão direito do mouse no arquivo e selecione a opção **Extrato Todos** o menu. Agora, estamos prontos para adicionar o kit de ferramentas à caixa de ferramentas visual studio/visual web developer.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Adicionando o Kit de Ferramentas de Controle AJAX à caixa de ferramentas

A maneira mais fácil de usar o AJAX Control Toolkit é adicionar o kit de ferramentas à sua caixa de ferramentas Visual Studio/Visual Web Developer (ver Figura 3). Dessa forma, você pode simplesmente arrastar um controle de kit de ferramentas para uma página quando quiser usá-lo.

[![AJAX Control Toolkit aparece na caixa de ferramentas](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**Figura 03**: AJAX Control Toolkit aparece na caixa de ferramentas[(Clique para exibir imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png)

Primeiro, você precisa adicionar uma guia AJAX Control Toolkit à caixa de ferramentas. Siga estas etapas.

1. Crie um novo site ASP.NET selecionando a opção menu Arquivo, Novo Site. Clique duas vezes no Default.aspx na janela Solution Explorer para abrir o arquivo no editor.
2. Clique com o botão direito do mouse na caixa de ferramentas abaixo da Guia Geral e selecione a opção de menu **Adicionar guia** (ver Figura 4).
3. Digite uma nova guia chamada AJAX Control Toolkit.

[![Adicionando uma nova guia](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**Figura 04**: Adicionando uma nova guia[(Clique para exibir imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)

Em seguida, você precisa adicionar os controles ajax control toolkit à nova guia. Siga estas etapas:

- Clique com o botão direito do mouse abaixo da guia AJAX Control Toolkit e selecione a opção menu **Escolha itens (veja Figura 5)**.
- Navegue até o local onde você descompactou o AJAX Control Toolkit e selecione o conjunto AjaxControlToolkit.dll.

[![Escolha itens para adicionar à caixa de ferramentas](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**Figura 05**: Escolha itens para adicionar à caixa de ferramentas[(Clique para exibir imagem em tamanho real)](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)

Depois de concluir essas etapas, todos os controles do kit de ferramentas aparecerão em sua caixa de ferramentas.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Atualizando para uma nova versão do Kit de ferramentas

Se você estava usando uma versão mais antiga do Toolkit e agora precisa passar para uma versão posterior aqui estão as etapas recomendadas:

- Binários - Exclua a versão antiga do conjunto AjaxControlToolkit.dll da pasta Bin do seu site.
- Itens da caixa de ferramentas - Exclua a guia AJAX Control Toolkit e siga os passos acima para recriar a guia com a nova versão do conjunto AjaxControlToolkit.dll.

> [!div class="step-by-step"]
> [Avançar](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
