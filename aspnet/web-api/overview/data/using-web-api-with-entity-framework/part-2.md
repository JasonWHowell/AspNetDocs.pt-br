---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: Adicionar modelos e controladores | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557536"
---
# <a name="add-models-and-controllers"></a><span data-ttu-id="cc3a3-102">Adicionar modelos e controladores</span><span class="sxs-lookup"><span data-stu-id="cc3a3-102">Add Models and Controllers</span></span>

<span data-ttu-id="cc3a3-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cc3a3-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="cc3a3-104">Baixar projeto concluído</span><span class="sxs-lookup"><span data-stu-id="cc3a3-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="cc3a3-105">Nesta seção, você adicionará classes de modelo que definem as entidades de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="cc3a3-106">Em seguida, você adicionará controladores de API da Web que executam operações CRUD nessas entidades.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="cc3a3-107">Adicionar classes de modelo</span><span class="sxs-lookup"><span data-stu-id="cc3a3-107">Add Model Classes</span></span>

<span data-ttu-id="cc3a3-108">Neste tutorial, criaremos o banco de dados usando a abordagem "Code First" para Entity Framework (EF).</span><span class="sxs-lookup"><span data-stu-id="cc3a3-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="cc3a3-109">Com Code First, você escreve C# classes que correspondem às tabelas de banco de dados e o EF cria o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="cc3a3-110">(Para obter mais informações, consulte [Entity Framework abordagens de desenvolvimento](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span><span class="sxs-lookup"><span data-stu-id="cc3a3-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="cc3a3-111">Começamos definindo nossos objetos de domínio como POCOs (objetos CLR antigos).</span><span class="sxs-lookup"><span data-stu-id="cc3a3-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="cc3a3-112">Criaremos o seguinte POCOs:</span><span class="sxs-lookup"><span data-stu-id="cc3a3-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="cc3a3-113">Autor</span><span class="sxs-lookup"><span data-stu-id="cc3a3-113">Author</span></span>
- <span data-ttu-id="cc3a3-114">Livro</span><span class="sxs-lookup"><span data-stu-id="cc3a3-114">Book</span></span>

<span data-ttu-id="cc3a3-115">Em Gerenciador de Soluções, clique com o botão direito do mouse na pasta modelos.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="cc3a3-116">Selecione **Adicionar**e selecione **classe**.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="cc3a3-117">Nome da classe `Author`.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="cc3a3-118">Substitua todo o código clichê em Author.cs pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="cc3a3-119">Adicione outra classe chamada `Book`, com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="cc3a3-120">Entity Framework usará esses modelos para criar tabelas de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="cc3a3-121">Para cada modelo, a propriedade `Id` se tornará a coluna de chave primária da tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="cc3a3-122">Na classe Book, o `AuthorId` define uma chave estrangeira na tabela `Author`.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="cc3a3-123">(Para simplificar, estou supondo que cada livro tenha um único autor.) A classe Book também contém uma propriedade de navegação para o `Author`relacionado.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="cc3a3-124">Você pode usar a propriedade de navegação para acessar os `Author` relacionados no código.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="cc3a3-125">Eu digo mais sobre as propriedades de navegação na parte 4, [tratando as relações entre entidades](part-4.md).</span><span class="sxs-lookup"><span data-stu-id="cc3a3-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="cc3a3-126">Adicionar controladores de API Web</span><span class="sxs-lookup"><span data-stu-id="cc3a3-126">Add Web API Controllers</span></span>

<span data-ttu-id="cc3a3-127">Nesta seção, adicionaremos controladores de API Web que dão suporte a operações CRUD (criar, ler, atualizar e excluir).</span><span class="sxs-lookup"><span data-stu-id="cc3a3-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="cc3a3-128">Os controladores usarão Entity Framework para se comunicar com a camada de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="cc3a3-129">Primeiro, você pode excluir os controladores de arquivo/ValuesController. cs.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="cc3a3-130">Esse arquivo contém um exemplo de controlador de API da Web, mas você não precisa dele para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="cc3a3-131">Em seguida, compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-131">Next, build the project.</span></span> <span data-ttu-id="cc3a3-132">A API Web scaffolding usa a reflexão para localizar as classes de modelo, portanto, ele precisa do assembly compilado.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="cc3a3-133">Em Gerenciador de Soluções, clique com o botão direito do mouse na pasta controladores.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="cc3a3-134">Selecione **Adicionar**e, em seguida, selecione **controlador**.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="cc3a3-135">Na caixa de diálogo **Adicionar Scaffold** , selecione "controlador da API Web 2 com ações, usando Entity Framework".</span><span class="sxs-lookup"><span data-stu-id="cc3a3-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="cc3a3-136">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="cc3a3-137">Na caixa de diálogo **Adicionar controlador** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cc3a3-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="cc3a3-138">Na lista suspensa **classe de modelo** , selecione a classe `Author`.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="cc3a3-139">(Se você não o vir listado na lista suspensa, certifique-se de que você criou o projeto.)</span><span class="sxs-lookup"><span data-stu-id="cc3a3-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="cc3a3-140">Marque "usar ações do controlador assíncrono".</span><span class="sxs-lookup"><span data-stu-id="cc3a3-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="cc3a3-141">Deixe o nome do controlador como &quot;AuthorsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="cc3a3-142">Clique no botão mais (+) ao lado de **classe de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="cc3a3-143">Na caixa de diálogo **novo contexto de dados** , deixe o nome padrão e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="cc3a3-144">Clique em **Adicionar** para concluir a caixa de diálogo **Adicionar controlador** .</span><span class="sxs-lookup"><span data-stu-id="cc3a3-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="cc3a3-145">A caixa de diálogo adiciona duas classes ao seu projeto:</span><span class="sxs-lookup"><span data-stu-id="cc3a3-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="cc3a3-146">`AuthorsController` define um controlador de API da Web.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="cc3a3-147">O controlador implementa a API REST que os clientes usam para executar operações CRUD na lista de autores.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="cc3a3-148">o `BookServiceContext` gerencia objetos de entidade durante o tempo de execução, o que inclui o preenchimento de objetos com dados de um Database, controle de alterações e persistência de dados no banco de dado.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="cc3a3-149">Herda de `DbContext`.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="cc3a3-150">Neste ponto, compile o projeto novamente.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-150">At this point, build the project again.</span></span> <span data-ttu-id="cc3a3-151">Agora, siga as mesmas etapas para adicionar um controlador de API para `Book` entidades.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="cc3a3-152">Desta vez, selecione `Book` para a classe de modelo e selecione a classe `BookServiceContext` existente para a classe de contexto de dados.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="cc3a3-153">(Não crie um novo contexto de dados.) Clique em **Adicionar** para adicionar o controlador.</span><span class="sxs-lookup"><span data-stu-id="cc3a3-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="cc3a3-154">[Anterior](part-1.md)
> [Próximo](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="cc3a3-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
