---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: 'Iteração #3 – Adicionar validação de formulário (C#) | Microsoft Docs'
author: rick-anderson
description: Na terceira iteração, adicionamos validação de formulário básico. Impedimos que as pessoas enviem um formulário sem preencher os campos de formulário necessários. Também validamos a Emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: c8442574d4901045f044f53ea12cd8330e8eaaa3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542372"
---
# <a name="iteration-3--add-form-validation-c"></a>Iteração nº 3 – adicionar validação de formulário (C#)

pela [Microsoft](https://github.com/microsoft)

[Código de download](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> Na terceira iteração, adicionamos validação de formulário básico. Impedimos que as pessoas enviem um formulário sem preencher os campos de formulário necessários. Também validamos endereços de e-mail e números de telefone.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Construindo um aplicativo mvc de gerenciamento de ASP.NET de contato (C#)

Nesta série de tutoriais, construímos todo um aplicativo de Gerenciamento de Contatos do início ao fim. O aplicativo Contact Manager permite que você armazene informações de contato - nomes, números de telefone e endereços de e-mail - para uma lista de pessoas.

Nós construímos o aplicativo sobre várias iterações. A cada iteração, melhoramos gradualmente a aplicação. O objetivo desta abordagem de iteração múltipla é permitir que você entenda a razão de cada mudança.

- Iteração #1 - Crie o aplicativo. Na primeira iteração, criamos o Contact Manager da maneira mais simples possível. Adicionamos suporte para operações básicas de banco de dados: Criar, Ler, Atualizar e Excluir (CRUD).

- Iteração #2 - Faça a aplicação parecer bonita. Nesta iteração, melhoramos a aparência do aplicativo modificando o padrão ASP.NET página-mestre de exibição mVC e folha de estilo em cascata.

- Iteração #3 - Adicionar validação de formulário. Na terceira iteração, adicionamos validação de formulário básico. Impedimos que as pessoas enviem um formulário sem preencher os campos de formulário necessários. Também validamos endereços de e-mail e números de telefone.

- Iteração #4 - Faça a aplicação livremente acoplada. Nesta quarta iteração, aproveitamos vários padrões de design de software para facilitar a manutenção e modificação do aplicativo Contact Manager. Por exemplo, refatoramos nossa aplicação para usar o padrão repositório e o padrão de injeção de dependência.

- Iteração #5 - Crie testes unitários. Na quinta iteração, tornamos nossa aplicação mais fácil de manter e modificar adicionando testes unitários. Zombamos de nossas classes de modelo de dados e construímos testes unitários para nossos controladores e lógica de validação.

- Iteração #6 - Use o desenvolvimento orientado para o teste. Nesta sexta iteração, adicionamos nova funcionalidade ao nosso aplicativo escrevendo primeiro testes de unidade e escrevendo código satisfaz os testes da unidade. Nesta iteração, adicionamos grupos de contato.

- Iteração #7 - Adicionar funcionalidade Ajax. Na sétima iteração, melhoramos a capacidade de resposta e o desempenho de nossa aplicação adicionando suporte ao Ajax.

## <a name="this-iteration"></a>Esta Iteração

Nesta segunda iteração do aplicativo Contact Manager, adicionamos validação de formulário básico. Impedimos que as pessoas submetam um contato sem inserir valores para os campos de formulário necessários. Também validamos números de telefone e endereços de e-mail (ver Figura 1).

[![A caixa de diálogo Novo Projeto](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)

**Figura 01**: Um formulário com validação ([Clique para ver a imagem em tamanho real](iteration-3-add-form-validation-cs/_static/image2.png))

Nesta iteração, adicionamos a lógica de validação diretamente às ações do controlador. Em geral, esta não é a maneira recomendada de adicionar validação a um aplicativo mvc ASP.NET. Uma abordagem melhor é colocar a lógica de validação de um aplicativo em uma camada de [serviço](http://martinfowler.com/eaaCatalog/serviceLayer.html)separada . Na próxima iteração, refatoramos o aplicativo Contact Manager para tornar o aplicativo mais sustentável.

Nesta iteração, para manter as coisas simples, escrevemos todo o código de validação manualmente. Em vez de escrever mos o código de validação nós mesmos, poderíamos tirar vantagem de uma estrutura de validação. Por exemplo, você pode usar o VAB (Microsoft Enterprise Library Validation Application Block, bloco de aplicativos de validação da biblioteca corporativa) para implementar a lógica de validação do seu aplicativo MVC ASP.NET. Para saber mais sobre o Bloco de Aplicativos de Validação, consulte:

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>Adicionando validação à exibição criar

Vamos começar adicionando lógica de validação à exibição Criar. Felizmente, como geramos a exibição Criar com o Visual Studio, a exibição Criar já contém toda a lógica necessária da interface do usuário para exibir mensagens de validação. A exibição Criar está contida na Lista 1.

**Listagem 1 - \Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

Observe a chamada para o método auxiliar Html.ValidationSummary() que aparece imediatamente acima do formulário HTML. Se houver mensagens de erro de validação, este método exibirá mensagens de validação em uma lista com caracteres.

Observe, ainda, as chamadas para Html.ValidationMessage() que aparecem ao lado de cada campo de formulário. O ajudante validationMessage() exibe uma mensagem de erro de validação individual. No caso da Listagem 1, um asterisco é exibido quando há um erro de validação.

Finalmente, o ajudante html.textbox() renderiza automaticamente uma classe Cascading Style Sheet quando há um erro de validação associado à propriedade exibida pelo ajudante. O ajudante html.textBox() renderiza uma classe chamada **input-validation-error**.

Quando você cria um novo aplicativo ASP.NET MVC, uma folha de estilos chamada Site.css é criada automaticamente na pasta Conteúdo. Esta folha de estilos contém as seguintes definições para classes CSS relacionadas ao aparecimento de mensagens de erro de validação:

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

A classe de erro de validação de campo é usada para estilizar a saída renderizada pelo ajudante Html.ValidationMessage(). A classe de erro de validação de entrada é usada para estilizar a caixa de texto (entrada) renderizada pelo ajudante Html.TextBox(). A classe validação-summary-errors é usada para estilizar a lista não ordenada renderizada pelo ajudante html.ValidationSummary().

> [!NOTE] 
> 
> Você pode modificar as classes de folha de estilo descritas nesta seção para personalizar a aparência das mensagens de erro de validação.

## <a name="adding-validation-logic-to-the-create-action"></a>Adicionando lógica de validação à ação de criação

No momento, a exibição Criar nunca exibe mensagens de erro de validação porque não escrevemos a lógica para gerar mensagens. Para exibir mensagens de erro de validação, você precisa adicionar as mensagens de erro ao ModelState.

> [!NOTE] 
> 
> O método UpdateModel() adiciona mensagens de erro ao ModelState automaticamente quando há um erro atribuindo o valor de um campo de formulário a uma propriedade. Por exemplo, se você tentar atribuir a string "apple" a uma propriedade BirthDate que aceita valores DateTime, então o método UpdateModel() adicionará um erro ao ModelState.

O método Create() modificado na Listagem 2 contém uma nova seção que valida as propriedades da classe Contato antes que o novo contato seja inserido no banco de dados.

**Listagem 2 - Controladores\ContactController.cs (Criar com validação)**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

A seção validar impõe quatro regras de validação distintas:

- A propriedade FirstName deve ter um comprimento maior que zero (e não pode consistir apenas em espaços)
- A propriedade LastName deve ter um comprimento maior que zero (e não pode consistir apenas em espaços)
- Se a propriedade Phone tiver um valor (tem um comprimento maior que 0), então a propriedade Phone deve corresponder a uma expressão regular.
- Se a propriedade Email tiver um valor (tem um comprimento maior que 0), então a propriedade Email deve corresponder a uma expressão regular.

Quando há uma violação da regra de validação, uma mensagem de erro é adicionada ao ModelState com a ajuda do método AddModelError(). Quando você adiciona uma mensagem ao ModelState, você fornece o nome de uma propriedade e o texto de uma mensagem de erro de validação. Esta mensagem de erro é exibida na exibição pelos métodos auxiliares Html.ValidationSummary() e Html.ValidationMessage().

Depois que as regras de validação são executadas, a propriedade IsValid do ModelState é verificada. A propriedade IsValid retorna falsa quando quaisquer mensagens de erro de validação foram adicionadas ao ModelState. Se a validação falhar, o formulário Criar será reexibido com as mensagens de erro.

> [!NOTE] 
> 
> Eu tenho as expressões regulares para validar o número de telefone e endereço de e-mail do repositório de expressão regular em[*http://regexlib.com*](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>Adicionando lógica de validação à ação de edição

A ação Editar() atualiza um contato. A ação Editar() precisa executar exatamente a mesma validação que a ação Criar(). Em vez de duplicar o mesmo código de validação, devemos refatorar o controlador de contato para que as ações Criar() e Editar() chamem o mesmo método de validação.

A classe de controlador de contato modificada está contida na Lista 3. Essa classe tem um novo método ValidateContact() que é chamado dentro das ações Criar() e Editar().

**Listagem 3 - Controladores\ContactController.cs**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a>Resumo

Nesta iteração, adicionamos validação de formulário básico ao nosso aplicativo de Contact Manager. Nossa lógica de validação impede que os usuários enviem um novo contato ou editem um contato existente sem fornecer valores para as propriedades FirstName e LastName. Além disso, os usuários devem fornecer números de telefone válidos e endereços de e-mail.

Nesta iteração, adicionamos a lógica de validação ao nosso aplicativo Contact Manager da maneira mais fácil possível. No entanto, misturar nossa lógica de validação em nossa lógica de controlador criará problemas para nós a longo prazo. Nosso aplicativo será mais difícil de manter e modificar ao longo do tempo.

Na próxima iteração, refatoraremos nossa lógica de validação e lógica de acesso ao banco de dados de nossos controladores. Vamos aproveitar vários princípios de design de software para nos permitir criar uma aplicação mais frouxamente acoplada e mais sustentável.

> [!div class="step-by-step"]
> [Próximo](iteration-2-make-the-application-look-nice-cs.md)
> [anterior](iteration-4-make-the-application-loosely-coupled-cs.md)
