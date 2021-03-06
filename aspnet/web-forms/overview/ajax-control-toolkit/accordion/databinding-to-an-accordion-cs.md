---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: Associação de dados a um acordeão (C#) | Microsoft Docs
author: wenz
description: O controle de acordeão no AJAX Control Toolkit fornece vários painéis e permite que o usuário exiba um deles de cada vez. Os painéis geralmente são declarados com w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c28cc958a1de9844627ae16175a5aed153993a8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614551"
---
# <a name="databinding-to-an-accordion-c"></a>Associação de Dados com um Accordion (C#)

por [Christian Wenz](https://github.com/wenz)

[Baixar código](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) ou [baixar PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)

> O controle de acordeão no AJAX Control Toolkit fornece vários painéis e permite que o usuário exiba um deles de cada vez. Os painéis geralmente são declarados dentro da própria página, mas a associação a uma fonte de dados oferece mais flexibilidade.

## <a name="overview"></a>Visão geral

O controle de acordeão no AJAX Control Toolkit fornece vários painéis e permite que o usuário exiba um deles de cada vez. Os painéis geralmente são declarados dentro da própria página, mas a associação a uma fonte de dados oferece mais flexibilidade.

## <a name="steps"></a>Etapas

Em primeiro lugar, uma fonte de dados é necessária. Este exemplo usa o banco de dados AdventureWorks e o Microsoft SQL Server 2005 Express Edition. O banco de dados é uma parte opcional de uma instalação do Visual Studio (incluindo a edição Express) e também está disponível como um download separado em [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). O banco de dados AdventureWorks faz parte dos exemplos SQL Server 2005 e bancos de dados de exemplo (download em [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). A maneira mais fácil de definir o banco de dados é usar o Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) e anexar o arquivo de banco de dados `AdventureWorks.mdf`.

Para este exemplo, presumimos que a instância do SQL Server 2005 Express Edition é chamada `SQLEXPRESS` e reside no mesmo computador que o servidor Web; Essa também é a configuração padrão. Se a configuração for diferente, você precisará adaptar as informações de conexão do banco de dados.

Para ativar a funcionalidade do ASP.NET AJAX e do kit de ferramentas de controle, o controle de `ScriptManager` deve ser colocado em qualquer lugar na página (mas dentro do elemento `<form>`):

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

Em seguida, adicione uma fonte de dados à página. Para usar uma quantidade limitada de dados, selecionamos apenas as cinco primeiras entradas na tabela de fornecedores do banco de dados AdventureWorks. Se você estiver usando o assistente do Visual Studio para criar a fonte de dados, lembre-se de que um bug na versão atual não prefixará o nome da tabela (`Vendor`) com `Purchasing`. A marcação a seguir mostra a sintaxe correta:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

Lembre-se do nome (ID) da fonte de dados. Essa identificação deve ser usada na propriedade `DataSourceID` do controle do acordeão:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

Dentro do controle de acordeão, você pode fornecer modelos para várias partes do controle, incluindo o cabeçalho (`<HeaderTemplate>`) e o conteúdo (`<ContentTemplate>`). Dentro desses elementos, basta gerar os dados da fonte de dados, usando o método `DataBinder.Eval()`:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

Quando a página é carregada, a fonte de dados deve estar associada ao acordeão com este código do lado do servidor:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

Para concluir este exemplo, você precisa definir as duas classes CSS que são referenciadas no controle de acordeão (em suas propriedades `HeaderCssClass` e `ContentCssClass`). Coloque a seguinte marcação na seção `<head>` da página:

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]

[![os dados no acordeão são fornecidos diretamente da fonte de dados](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)

Os dados no acordeão são fornecidos diretamente da fonte de dados ([clique para exibir a imagem em tamanho normal](databinding-to-an-accordion-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Próximo](dynamically-adding-an-accordion-pane-cs.md)
