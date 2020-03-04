---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'Tutorial: Aprimorar a validação de dados para o Database First do EF com o aplicativo ASP.NET MVC'
description: Este tutorial concentra-se sobre como adicionar anotações de dados para o modelo de dados para especificar os requisitos de validação e formatação de exibição.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039863"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a>Tutorial: Aprimorar a validação de dados para o Database First do EF com o aplicativo ASP.NET MVC

Usando o MVC, Entity Framework e o Scaffolding do ASP.NET, você pode criar um aplicativo web que fornece uma interface para um banco de dados existente. Esta série de tutoriais mostra como automaticamente gerar um código que permite aos usuários exibir, editar, criar e excluir dados que residem em uma tabela de banco de dados. O código gerado corresponde às colunas na tabela de banco de dados.

Este tutorial concentra-se sobre como adicionar anotações de dados para o modelo de dados para especificar os requisitos de validação e formatação de exibição. Ele foi aprimorado com base nos comentários dos usuários na seção de comentários.

Neste tutorial, você:

> [!div class="checklist"]
> * Adicionar anotações de dados
> * Adicionar classes de metadados

## <a name="prerequisites"></a>Prerequisites

* [Personalizar um modo de exibição](customizing-a-view.md)

## <a name="add-data-annotations"></a>Adicionar anotações de dados

Como você viu em um tópico anterior, algumas regras de validação de dados são aplicadas automaticamente para a entrada do usuário. Por exemplo, você só pode fornecer um número para a propriedade de nível empresarial. Para especificar mais regras de validação de dados, você pode adicionar anotações de dados à sua classe de modelo. Essas anotações são aplicadas em todo o seu aplicativo web para a propriedade especificada. Você também pode aplicar atributos de formatação que alterar como as propriedades são exibidas; Por exemplo, alterando o valor usado para rótulos de texto.

Neste tutorial, você irá adicionar anotações de dados para restringir o tamanho dos valores fornecidos para as propriedades FirstName, LastName e MiddleName. No banco de dados, esses valores são limitados a 50 caracteres. No entanto, em seu aplicativo web que limite de caracteres no momento, não é imposta. Se um usuário fornece mais de 50 caracteres para um desses valores, a página falhará ao tentar salvar o valor para o banco de dados. Também você restringirá a nível empresarial para valores entre 0 e 4.

Selecione **modelos** > **ContosoModel.edmx** > **ContosoModel.tt** e abra o *Student.cs* arquivo. Adicione o seguinte código realçado à classe.

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

Abra *Enrollment.cs* e adicione o seguinte código realçado.

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

Compile a solução.

Clique em **lista de alunos** e selecione **editar**. Se você tentar inserir mais de 50 caracteres, uma mensagem de erro será exibida.

![Mostrar mensagem de erro](enhancing-data-validation/_static/image1.png)

Volte para a home page. Clique em **lista de registros** e selecione **editar**. Tentativa de fornecer uma nota superior a 4. Você receberá esse erro: *O campo de que nível empresarial deve estar entre 0 e 4.*

## <a name="add-metadata-classes"></a>Adicionar classes de metadados

Adicionar os atributos de validação diretamente para a classe de modelo funciona quando você não espera que o banco de dados a ser alterado; No entanto, se as alterações de banco de dados e você precisar regenerar a classe de modelo, você perderá todos os atributos que você tivesse aplicado à classe de modelo. Essa abordagem pode ser muito ineficiente e propenso a perder as regras de validação importantes.

Para evitar esse problema, você pode adicionar uma classe de metadados que contém os atributos. Quando você associa a classe de modelo para a classe de metadados, esses atributos são aplicados ao modelo. Nessa abordagem, a classe de modelo pode ser regenerada sem perder todos os atributos que foram aplicados à classe de metadados.

No **modelos** pasta, adicione uma classe chamada *Metadata.cs*.

Substitua o código em *Metadata.cs* com o código a seguir.

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

Essas classes de metadados contêm todos os atributos de validação aplicados anteriormente para as classes de modelo. O **exibição** atributo é usado para alterar o valor usado para rótulos de texto.

Agora, você deve associar as classes de modelo com as classes de metadados.

No **modelos** pasta, adicione uma classe chamada *PartialClasses.cs*.

Substitua o conteúdo do arquivo pelo código a seguir.

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

Observe que cada classe é marcada como um `partial` classe e cada uma corresponde ao nome e namespace como a classe que é gerada automaticamente. Aplicando o atributo de metadados para a classe parcial, você certifique-se de que os atributos de validação de dados serão aplicados à classe gerada automaticamente. Esses atributos não serão perdidos quando você regenerar as classes de modelo porque o atributo de metadados é aplicado em classes parciais que não serão regeneradas.

Para regenerar as classes geradas automaticamente, abra o *ContosoModel.edmx* arquivo. Mais uma vez, com o botão direito na superfície do design e selecione **modelo de atualização do banco de dados**. Embora você não alterou o banco de dados, esse processo regenerará as classes. No **Refresh** guia, selecione **tabelas** e **concluir**.

Salvar a *ContosoModel.edmx* arquivo para aplicar as alterações.

Abra o *Student.cs* arquivo ou o *Enrollment.cs* arquivo e observe que os atributos de validação de dados que você aplicou anteriormente não estão mais no arquivo. No entanto, executar o aplicativo e observe que as regras de validação ainda são aplicadas quando você insere dados.

## <a name="conclusion"></a>Conclusão

Esta série fornecido um exemplo simples de como gerar o código de um banco de dados existente que permite aos usuários editar, atualizar, criar e excluir dados. Ele usado ASP.NET MVC 5, Entity Framework e Scaffolding do ASP.NET para criar o projeto. 

Para obter um exemplo introdutório de desenvolvimento Code First, consulte [Introdução ao ASP.NET MVC 5](../introduction/getting-started.md). 

Para obter um exemplo mais avançado, consulte [criando um modelo de dados do Entity Framework para um aplicativo do ASP.NET MVC 4](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Observe que a API DbContext que você usa para trabalhar com dados no banco de dados primeiro é o mesmo que a API que você pode usar para trabalhar com dados no Code First. Mesmo se você pretende usar o primeiro banco de dados, você pode aprender como lidar com cenários mais complexos, como ler e atualizar dados relacionados, tratamento de conflitos de simultaneidade, e assim por diante de um tutorial de Code First. A única diferença está em como o banco de dados, classe de contexto e classes de entidade são criadas.

## <a name="additional-resources"></a>Recursos adicionais

Para obter uma lista completa de anotações de validação de dados, você pode aplicar a classes e propriedades, consulte [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você:

> [!div class="checklist"]
> * Anotações de dados adicionados
> * Classes de metadados adicionados

Para saber como implantar um aplicativo web e o banco de dados SQL no serviço de aplicativo do Azure, consulte este tutorial:
> [!div class="nextstepaction"]
> [Implantar um aplicativo .NET no serviço de aplicativo do Azure](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
