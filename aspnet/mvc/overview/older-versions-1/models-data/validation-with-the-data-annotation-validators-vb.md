---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: Validação com os Validadores de Anotação de Dados (VB) | Microsoft Docs
author: rick-anderson
description: Aproveite o Binder modelo de anotação de dados para realizar a validação dentro de um aplicativo MVC ASP.NET. Saiba como usar os diferentes tipos de validador...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: cabdf6dab9e5de53a45adcf126705533fca02de7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542632"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>Validação com os validadores de anotação de dados (VB)

pela [Microsoft](https://github.com/microsoft)

> Aproveite o Binder modelo de anotação de dados para realizar a validação dentro de um aplicativo MVC ASP.NET. Aprenda a usar os diferentes tipos de atributos validadores e trabalhe com eles no Microsoft Entity Framework.

Neste tutorial, você aprende a usar os validadores de Anotação de Dados para realizar a validação em um aplicativo mvc ASP.NET. A vantagem de usar os validadores de anotação de dados é que eles permitem que você execute a validação simplesmente adicionando um ou mais atributos – como o atributo Required ou StringLength – a uma propriedade de classe.

Antes de usar os validadores de anotação de dados, você deve baixar o Binder modelo de anotações de dados. Você pode baixar a Amostra de Anotações de Dados Modelo Binder do site codePlex clicando [aqui](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).

É importante entender que o Modelo de Anotações de Dados Binder não é uma parte oficial da estrutura mvc ASP.NET Microsoft. Embora o Modelo de Anotações de Dados Binder tenha sido criado pela equipe de MVC ASP.NET Da Microsoft, a Microsoft não oferece suporte oficial ao produto para o Modelo de Anotações de Dados Binder descrito e usado neste tutorial.

## <a name="using-the-data-annotation-model-binder"></a>Usando o binder modelo de anotação de dados

Para usar o Binder de Anotações de Dados em um aplicativo mVC ASP.NET, primeiro você precisa adicionar uma referência ao conjunto Microsoft.Web.Mvc.DataAnnotations.dll e ao conjunto System.ComponentModel.DataAnnotations.dll assembly. Selecione a opção de menu **Projeto, Adicionar referência**. Em seguida, clique na guia **Procurar** e navegue até o local onde você baixou (e descompactou) a amostra de Tecelagem do Modelo de Anotações de Dados (ver **Figura 1**).

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**Figura 1**: Adicionar uma referência ao Binder modelo de anotações de dados[(Clique para exibir a imagem em tamanho real)](validation-with-the-data-annotation-validators-vb/_static/image3.png)

Selecione o conjunto Microsoft.Web.Mvc.DataAnnotations.dll e o system.componentModel.DataAnnotations.dll assembly e clique no botão **OK.**

Não é possível usar o conjunto System.ComponentModel.DataAnotations.dll incluído no .NET Framework Service Pack 1 com o Modelo de Anotações de Dados Binder. Você deve usar a versão do system.componentModel.DataAnotations.dll assembly incluído com o download da amostra do modelo de anotações de dados.

Finalmente, você precisa registrar o DataAnnotations Model Binder no arquivo Global.asax. Adicione a seguinte linha de\_código ao manipulador de eventos\_Iniciar de aplicativo() para que o método Start() do aplicativo seja assim:

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

Esta linha de código registra o DataAnnotationsModelBinder como o aglutinante de modelo padrão para toda a aplicação ASP.NET MVC.

## <a name="using-the-data-annotation-validator-attributes"></a>Usando os atributos validadores de anotação de dados

Quando você usa o Binder de anotações de dados, você usa atributos validadores para realizar a validação. O namespace System.ComponentModel.DataAnnotations inclui os seguintes atributos validadores:

- Intervalo – Permite validar se o valor de uma propriedade está entre uma faixa de valores especificada.
- RegularExpression – Permite validar se o valor de uma propriedade corresponde a um padrão de expressão regular especificado.
- Obrigatório – Permite que você marque uma propriedade conforme necessário.
- StringLength – Permite especificar um comprimento máximo para uma propriedade de string.
- Validação – A classe base para todos os atributos validadores.

> [!NOTE] 
> 
> Se suas necessidades de validação não forem satisfeitas por qualquer um dos validadores padrão, você sempre terá a opção de criar um atributo validador personalizado herdando um novo atributo validador do atributo de validação base.

A classe Produto na **Listagem 1** ilustra como usar esses atributos validadores. As propriedades Nome, Descrição e Preço unitário são marcadas conforme necessário. A propriedade Name deve ter um comprimento de seqüência inferior a 10 caracteres. Finalmente, a propriedade UnitPrice deve corresponder a um padrão de expressão regular que representa um valor de moeda.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**Lista 1:** Modelos\Product.vb

A classe Produto ilustra como usar um atributo adicional: o atributo DisplayName. O atributo DisplayName permite modificar o nome da propriedade quando a propriedade é exibida em uma mensagem de erro. Em vez de exibir a mensagem de erro "O campo UnitPrice é necessário" você pode exibir a mensagem de erro "O campo Preço é necessário".

> [!NOTE] 
> 
> Se você quiser personalizar completamente a mensagem de erro exibida por um validador, então você pode atribuir uma mensagem de erro personalizada à propriedade ErrorMessage do validador assim:`<Required(ErrorMessage:="This field needs a value!")>`

Você pode usar a classe Produto na **Listagem 1** com a ação do controlador Criar() na **Listagem 2**. Esta ação do controlador exibe reexibição na exibição Criar quando o estado do modelo contém quaisquer erros.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**Lista 2:** Controladores\ProductController.vb

Finalmente, você pode criar a exibição na **Listagem 3** clicando com o botão direito do mouse na ação Criar() e selecionando a opção de menu **Adicionar exibição**. Crie uma visão fortemente digitada com a classe Produto como a classe modelo. Selecione **Criar** na lista de isto de conteúdo de exibição (ver **Figura 2**).

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**Figura 2**: Adicionando a exibição criar

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**Listagem 3:** Views\Product\Create.aspx

> [!NOTE] 
> 
> Remova o campo '''''''''Criar', o formulário Criar gerado pela opção **Adicionar** exibição de menu.'. Como o campo Identificar corresponde a uma coluna Identidade, você não deseja permitir que os usuários insiram um valor para este campo.

Se você enviar o formulário para criar um Produto e não inserir valores para os campos necessários, as mensagens de erro de validação na **Figura 3** serão exibidas.

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**Figura 3:** Faltam campos necessários

Se você inserir um valor de moeda inválido, a mensagem de erro na **Figura 4** será exibida.

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**Figura 4**: Valor da moeda inválida

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Usando validadores de anotação de dados com o Framework entity

Se você estiver usando o Microsoft Entity Framework para gerar suas classes de modelo de dados, não poderá aplicar os atributos validadores diretamente às suas classes. Como o Entity Framework Designer gera as classes de modelo, quaisquer alterações que você fizer nas classes de modelo serão substituídas na próxima vez que você fizer qualquer alteração no Designer.

Se você quiser usar os validadores com as classes geradas pelo Quadro de Entidades, então você precisa criar classes de meta dados. Você aplica os validadores à classe meta dados em vez de aplicar os validadores à classe real.

Por exemplo, imagine que você criou uma classe de filme usando o Quadro de Entidades (ver **Figura 5**). Imagine, além disso, que você deseja fazer as propriedades do Título do Filme e do Diretor necessárias. Nesse caso, você pode criar a classe parcial e a classe meta dados na **Listagem 4**.

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**Figura 5**: Classe de filme gerada pelo Entity Framework

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**Lista 4**: Modelos\Movie.vb

O arquivo na **Lista 4** contém duas classes chamadas Movie e MovieMetaData. A aula de cinema é uma aula parcial. Corresponde à classe parcial gerada pelo Quadro de Entidades contida no arquivo DataModel.Designer.vb.

Atualmente, o framework .NET não suporta propriedades parciais. Portanto, não há como aplicar os atributos validadores às propriedades da classe Movie definidas no arquivo DataModel.Designer.vb aplicando os atributos validadores às propriedades da classe Movie definidas no arquivo na **Listagem 4**.

Observe que a classe parcial do Filme é decorada com um atributo MetadataType que aponta para a classe MovieMetaData. A classe MovieMetaData contém propriedades proxy para as propriedades da classe Movie.

Os atributos do validador são aplicados às propriedades da classe MovieMetaData. As propriedades Title, Director e DateReleased são todas marcadas como propriedades necessárias. A propriedade Director deve ser atribuída a uma seqüência que contenha menos de 5 caracteres. Finalmente, o atributo DisplayName é aplicado à propriedade DateReleased para exibir uma mensagem de erro como "O campo Data lançada é necessário". em vez do erro "O campo DateReleased é necessário".

> [!NOTE] 
> 
> Observe que as propriedades proxy na classe MovieMetaData não precisam representar os mesmos tipos que as propriedades correspondentes na classe Movie. Por exemplo, a propriedade Director é uma propriedade de string na classe Movie e uma propriedade de objeto na classe MovieMetaData.

A página na **Figura 6** ilustra as mensagens de erro retornadas quando você insere valores inválidos para as propriedades Movie.

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**Figura 6**: Usando validadores com o Framework Entity ([Clique para exibir imagem em tamanho real](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu como aproveitar o Modelo de Anotação de Dados Binder para realizar a validação dentro de um aplicativo mvc ASP.NET. Você aprendeu a usar os diferentes tipos de atributos validadores, como os atributos Required e StringLength. Você também aprendeu a usar esses atributos ao trabalhar com o Microsoft Entity Framework.

> [!div class="step-by-step"]
> [Anterior](validating-with-a-service-layer-vb.md)
