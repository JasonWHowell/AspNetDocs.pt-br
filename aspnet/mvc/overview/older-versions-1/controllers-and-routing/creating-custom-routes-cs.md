---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Criando rotas personalizadas (C#) | Microsoft Docs
author: rick-anderson
description: Aprenda a adicionar rotas personalizadas a um aplicativo MVC ASP.NET. Neste tutorial, você aprende como modificar a tabela de rotas padrão no arquivo Global.asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542749"
---
# <a name="creating-custom-routes-c"></a>Criação de rotas personalizadas (C#)

pela [Microsoft](https://github.com/microsoft)

> Aprenda a adicionar rotas personalizadas a um aplicativo MVC ASP.NET. Neste tutorial, você aprende como modificar a tabela de rotas padrão no arquivo Global.asax.

Neste tutorial, você aprende como adicionar uma rota personalizada a um aplicativo mvc ASP.NET. Você aprende como modificar a tabela de rota padrão no arquivo Global.asax com uma rota personalizada.

Para muitos aplicativos simples de MVC ASP.NET, a tabela de rotas padrão funcionará muito bem. No entanto, você pode descobrir que você tem necessidades de roteamento especializadas. Nesse caso, você pode criar uma rota personalizada.

Imagine, por exemplo, que você está construindo um aplicativo de blog. Você pode querer lidar com pedidos de entrada que se parecem com isso:

/Arquivo/12-25-2009

Quando um usuário insere essa solicitação, você deseja retornar a entrada do blog que corresponde à data de 25/12/2009. Para lidar com esse tipo de solicitação, você precisa criar uma rota personalizada.

O arquivo Global.asax na Listagem 1 contém uma nova rota personalizada, chamada Blog, que lida com solicitações que se parecem com /Archive/data*de entrada*.

**Listagem 1 - Global.asax (com rota personalizada)**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

A ordem das rotas que você adiciona à tabela de rotas é importante. Nossa nova rota personalizada do Blog é adicionada antes da rota Padrão existente. Se você inverteu a ordem, então a rota Padrão sempre será chamada em vez da rota personalizada.

A rota do Blog personalizado corresponde a qualquer solicitação que comece com /Archive/. Então, corresponde a todas as seguintes URLs:

- /Arquivo/12-25-2009

- /Arquivo/10-6-2004

- /Arquivo/maçã

A rota personalizada mapeia a solicitação recebida para um controlador chamado Archive e invoca a ação Entrada(). Quando o método Entry() é chamado, a data de entrada é passada como um parâmetro chamado entryDate.

Você pode usar a rota personalizada do Blog com o controlador na Lista 2.

**Listagem 2 - ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

Observe que o método Entry() na Listagem 2 aceita um parâmetro do tipo DateTime. A estrutura MVC é inteligente o suficiente para converter a data de entrada da URL em um valor DateTime automaticamente. Se o parâmetro de data de entrada da URL não puder ser convertido em data-hora, um erro será levantado (consulte Figura 1).

**Figura 1 - Erro ao converter parâmetro**

[![A caixa de diálogo Novo Projeto](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**Figura 01**: Erro ao converter parâmetro[(Clique para exibir imagem em tamanho real)](creating-custom-routes-cs/_static/image2.png)

## <a name="summary"></a>Resumo

O objetivo deste tutorial foi demonstrar como você pode criar uma rota personalizada. Você aprendeu como adicionar uma rota personalizada à tabela de rotas no arquivo Global.asax que representa entradas de blog. Discutimos como mapear solicitações de entradas de blog para um controlador chamado ArchiveController e uma ação controladora chamada Entry().

> [!div class="step-by-step"]
> [Próximo](aspnet-mvc-controllers-overview-cs.md)
> [anterior](creating-a-route-constraint-cs.md)
