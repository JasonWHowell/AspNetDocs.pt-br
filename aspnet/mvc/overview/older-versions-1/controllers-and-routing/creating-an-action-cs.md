---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Criando uma Ação (C#) | Microsoft Docs
author: rick-anderson
description: Aprenda a adicionar uma nova ação a um controlador MVC ASP.NET. Conheça os requisitos para que um método seja uma ação.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c1edfbab41afa58c7cb2c0d306995e9fe491c90
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542268"
---
# <a name="creating-an-action-c"></a>Criar uma ação (C#)

pela [Microsoft](https://github.com/microsoft)

> Aprenda a adicionar uma nova ação a um controlador MVC ASP.NET. Conheça os requisitos para que um método seja uma ação.

O objetivo deste tutorial é explicar como você pode criar uma nova ação de controlador. Você aprende sobre os requisitos de um método de ação. Você também aprende como evitar que um método seja exposto como uma ação.

## <a name="adding-an-action-to-a-controller"></a>Adicionando uma ação a um controlador

Você adiciona uma nova ação a um controlador adicionando um novo método ao controlador. Por exemplo, o controlador na Listagem 1 contém uma ação chamada Index() e uma ação chamada SayHello(). Ambos os métodos são expostos como ações.

**Listagem 1 - Controladores\HomeController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

Para ser exposto ao universo como uma ação, um método deve atender a certos requisitos:

- O método deve ser público.
- O método não pode ser um método estático.
- O método não pode ser um método de extensão.
- O método não pode ser um construtor, getter ou setter.
- O método não pode ter tipos genéricos abertos.
- O método não é um método da classe base do controlador.
- O método não pode conter parâmetros **de ref** ou **out.**

Observe que não há restrições sobre o tipo de retorno de uma ação do controlador. Uma ação do controlador pode retornar uma seqüência, uma Hora de Data, uma instância da classe Random ou anular. A ASP.NET estrutura MVC converterá qualquer tipo de retorno que não seja um resultado de ação em uma seqüência e renderizará a seqüência para o navegador.

Quando você adiciona qualquer método que não viole esses requisitos a um controlador, o método é exposto como uma ação do controlador. Tenha cuidado aqui. Uma ação do controlador pode ser invocada por qualquer pessoa conectada à Internet. Não crie, por exemplo, uma ação de controlador DeleteMySite().

## <a name="preventing-a-public-method-from-being-invoked"></a>Impedindo que um método público seja invocado

Se você precisa criar um método público em uma classe controladora e não quiser expor o método como uma ação do controlador, então você pode impedir que o método seja invocado usando o atributo [NonAction]. Por exemplo, o controlador na Listagem 2 contém um método público chamado CompanySecrets() que é decorado com o atributo [NonAction].

**Listagem 2 - Controladores\WorkController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

Se você tentar invocar a ação do controlador CompanySecrets() digitando /Work/CompanySecrets na barra de endereços do seu navegador, então você receberá a mensagem de erro na Figura 1.

[![Invocando um método de não ação](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**Figura 01**: Invocar um método de não ação[(Clique para exibir imagem em tamanho real)](creating-an-action-cs/_static/image2.png)

> [!div class="step-by-step"]
> [Próximo](creating-a-controller-cs.md)
> [anterior](asp-net-mvc-routing-overview-vb.md)
