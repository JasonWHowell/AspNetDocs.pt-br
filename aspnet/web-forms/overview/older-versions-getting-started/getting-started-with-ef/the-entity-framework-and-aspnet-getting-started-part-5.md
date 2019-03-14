---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: Introdução ao banco de dados do Entity Framework 4.0 First e 4 do ASP.NET Web Forms - parte 5 | Microsoft Docs
author: tdykstra
description: Aplicativo web de exemplo Contoso University demonstra como criar aplicativos Web Forms do ASP.NET usando o Entity Framework. O aplicativo de exemplo é...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 3209ab3bca58e0dde90cf279732d177418b034e4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036043"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a><span data-ttu-id="7755b-104">Introdução ao banco de dados do Entity Framework 4.0 First e 4 do Web Forms do ASP.NET – parte 5</span><span class="sxs-lookup"><span data-stu-id="7755b-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 5</span></span>
====================
<span data-ttu-id="7755b-105">por [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7755b-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="7755b-106">Aplicativo web de exemplo Contoso University demonstra como criar aplicativos Web Forms do ASP.NET usando o Entity Framework 4.0 e o Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="7755b-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="7755b-107">Para obter informações sobre a série de tutoriais, consulte [o primeiro tutorial na série](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="7755b-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="working-with-related-data-continued"></a><span data-ttu-id="7755b-108">Trabalhando com dados relacionados, continuação</span><span class="sxs-lookup"><span data-stu-id="7755b-108">Working with Related Data, Continued</span></span>

<span data-ttu-id="7755b-109">No tutorial anterior, você começou a usar o `EntityDataSource` controle para trabalhar com dados relacionados.</span><span class="sxs-lookup"><span data-stu-id="7755b-109">In the previous tutorial you began to use the `EntityDataSource` control to work with related data.</span></span> <span data-ttu-id="7755b-110">Exibidos vários níveis de hierarquia e editar dados nas propriedades de navegação.</span><span class="sxs-lookup"><span data-stu-id="7755b-110">You displayed multiple levels of hierarchy and edited data in navigation properties.</span></span> <span data-ttu-id="7755b-111">Neste tutorial, você continuará a trabalhar com dados relacionados, adicionando e excluindo relações e adicionando uma nova entidade que tem uma relação com uma entidade existente.</span><span class="sxs-lookup"><span data-stu-id="7755b-111">In this tutorial you'll continue to work with related data by adding and deleting relationships and by adding a new entity that has a relationship to an existing entity.</span></span>

<span data-ttu-id="7755b-112">Você criará uma página que adiciona cursos são atribuídos aos departamentos.</span><span class="sxs-lookup"><span data-stu-id="7755b-112">You'll create a page that adds courses that are assigned to departments.</span></span> <span data-ttu-id="7755b-113">Os departamentos já existirem, e quando você cria um novo curso, ao mesmo tempo, você vai estabelecer uma relação entre ele e um departamento existente.</span><span class="sxs-lookup"><span data-stu-id="7755b-113">The departments already exist, and when you create a new course, at the same time you'll establish a relationship between it and an existing department.</span></span>

<span data-ttu-id="7755b-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7755b-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span></span>

<span data-ttu-id="7755b-115">Você também criará uma página que funciona com uma relação muitos-para-muitos, atribuindo um instrutor a um curso (adicionando uma relação entre duas entidades que você selecionar) ou removendo um instrutor de um curso (para remover uma relação entre duas entidades que você Selecione).</span><span class="sxs-lookup"><span data-stu-id="7755b-115">You'll also create a page that works with a many-to-many relationship by assigning an instructor to a course (adding a relationship between two entities that you select) or removing an instructor from a course (removing a relationship between two entities that you select).</span></span> <span data-ttu-id="7755b-116">No banco de dados, adicionando uma relação entre um instrutor e um curso resulta em uma nova linha que está sendo adicionada para o `CourseInstructor` tabela de associação; removendo envolve a exclusão de uma linha de uma relação a `CourseInstructor` tabela de associação.</span><span class="sxs-lookup"><span data-stu-id="7755b-116">In the database, adding a relationship between an instructor and a course results in a new row being added to the `CourseInstructor` association table; removing a relationship involves deleting a row from the `CourseInstructor` association table.</span></span> <span data-ttu-id="7755b-117">No entanto, você fazer isso no Entity Framework, definindo as propriedades de navegação, sem fazer referência à `CourseInstructor` explicitamente de tabela.</span><span class="sxs-lookup"><span data-stu-id="7755b-117">However, you do this in the Entity Framework by setting navigation properties, without referring to the `CourseInstructor` table explicitly.</span></span>

<span data-ttu-id="7755b-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7755b-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span></span>

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a><span data-ttu-id="7755b-119">Adicionando uma entidade com uma relação a uma entidade existente</span><span class="sxs-lookup"><span data-stu-id="7755b-119">Adding an Entity with a Relationship to an Existing Entity</span></span>

<span data-ttu-id="7755b-120">Criar uma nova página da web denominado *CoursesAdd.aspx* que usa o *Master* página mestra e adicione a seguinte marcação para o `Content` controle chamado `Content2`:</span><span class="sxs-lookup"><span data-stu-id="7755b-120">Create a new web page named *CoursesAdd.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

<span data-ttu-id="7755b-121">Essa marcação cria um `EntityDataSource` controle que seleciona cursos, que permite a inserção, e que especifica um manipulador para o `Inserting` eventos.</span><span class="sxs-lookup"><span data-stu-id="7755b-121">This markup creates an `EntityDataSource` control that selects courses, that enables inserting, and that specifies a handler for the `Inserting` event.</span></span> <span data-ttu-id="7755b-122">Você usará o manipulador para atualizar o `Department` propriedade de navegação quando um novo `Course` entidade é criada.</span><span class="sxs-lookup"><span data-stu-id="7755b-122">You'll use the handler to update the `Department` navigation property when a new `Course` entity is created.</span></span>

<span data-ttu-id="7755b-123">A marcação também cria uma `DetailsView` controle a ser usado para adicionar novos `Course` entidades.</span><span class="sxs-lookup"><span data-stu-id="7755b-123">The markup also creates a `DetailsView` control to use for adding new `Course` entities.</span></span> <span data-ttu-id="7755b-124">A marcação usa campos associados para `Course` propriedades da entidade.</span><span class="sxs-lookup"><span data-stu-id="7755b-124">The markup uses bound fields for `Course` entity properties.</span></span> <span data-ttu-id="7755b-125">Você precisará inserir o `CourseID` valor porque isso não é um campo de ID gerada pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="7755b-125">You have to enter the `CourseID` value because this is not a system-generated ID field.</span></span> <span data-ttu-id="7755b-126">Em vez disso, ele é um número de curso que deve ser especificado manualmente, quando o curso é criado.</span><span class="sxs-lookup"><span data-stu-id="7755b-126">Instead, it's a course number that must be specified manually when the course is created.</span></span>

<span data-ttu-id="7755b-127">Você usa um campo de modelo para o `Department` propriedade de navegação porque as propriedades de navegação não podem ser usadas com `BoundField` controles.</span><span class="sxs-lookup"><span data-stu-id="7755b-127">You use a template field for the `Department` navigation property because navigation properties cannot be used with `BoundField` controls.</span></span> <span data-ttu-id="7755b-128">O campo de modelo fornece uma lista suspensa para selecionar o departamento.</span><span class="sxs-lookup"><span data-stu-id="7755b-128">The template field provides a drop-down list to select the department.</span></span> <span data-ttu-id="7755b-129">A lista suspensa é associada à `Departments` definida por meio de entidade `Eval` em vez de `Bind`, novamente porque você não pode diretamente associar propriedades de navegação para atualizá-los.</span><span class="sxs-lookup"><span data-stu-id="7755b-129">The drop-down list is bound to the `Departments` entity set by using `Eval` rather than `Bind`, again because you cannot directly bind navigation properties in order to update them.</span></span> <span data-ttu-id="7755b-130">Especifique um manipulador para o `DropDownList` do controle `Init` evento para que você possa armazenar uma referência para o controle para uso pelo código que atualiza o `DepartmentID` chave estrangeira.</span><span class="sxs-lookup"><span data-stu-id="7755b-130">You specify a handler for the `DropDownList` control's `Init` event so that you can store a reference to the control for use by the code that updates the `DepartmentID` foreign key.</span></span>

<span data-ttu-id="7755b-131">Na *CoursesAdd.aspx.cs* logo após a declaração de classe parcial, adicione um campo de classe para conter uma referência para o `DepartmentsDropDownList` controle:</span><span class="sxs-lookup"><span data-stu-id="7755b-131">In *CoursesAdd.aspx.cs* just after the partial-class declaration, add a class field to hold a reference to the `DepartmentsDropDownList` control:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

<span data-ttu-id="7755b-132">Adicionar um manipulador para o `DepartmentsDropDownList` do controle `Init` eventos para que você possa armazenar uma referência ao controle.</span><span class="sxs-lookup"><span data-stu-id="7755b-132">Add a handler for the `DepartmentsDropDownList` control's `Init` event so that you can store a reference to the control.</span></span> <span data-ttu-id="7755b-133">Isso permite que você obtenha o valor que o usuário inseriu e usá-lo para atualizar o `DepartmentID` valor da `Course` entidade.</span><span class="sxs-lookup"><span data-stu-id="7755b-133">This lets you get the value the user has entered and use it to update the `DepartmentID` value of the `Course` entity.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

<span data-ttu-id="7755b-134">Adicionar um manipulador para o `DetailsView` do controle `Inserting` eventos:</span><span class="sxs-lookup"><span data-stu-id="7755b-134">Add a handler for the `DetailsView` control's `Inserting` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

<span data-ttu-id="7755b-135">Quando o usuário clica `Insert`, o `Inserting` evento é gerado antes que o novo registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="7755b-135">When the user clicks `Insert`, the `Inserting` event is raised before the new record is inserted.</span></span> <span data-ttu-id="7755b-136">Obtém o código no manipulador do `DepartmentID` do `DropDownList` controlar e usa-o para definir o valor que será usado para o `DepartmentID` propriedade do `Course` entidade.</span><span class="sxs-lookup"><span data-stu-id="7755b-136">The code in the handler gets the `DepartmentID` from the `DropDownList` control and uses it to set the value that will be used for the `DepartmentID` property of the `Course` entity.</span></span>

<span data-ttu-id="7755b-137">O Entity Framework cuidará de adicionar este curso para o `Courses` propriedade de navegação de associado `Department` entidade.</span><span class="sxs-lookup"><span data-stu-id="7755b-137">The Entity Framework will take care of adding this course to the `Courses` navigation property of the associated `Department` entity.</span></span> <span data-ttu-id="7755b-138">Ele também adiciona o departamento para o `Department` propriedade de navegação do `Course` entidade.</span><span class="sxs-lookup"><span data-stu-id="7755b-138">It also adds the department to the `Department` navigation property of the `Course` entity.</span></span>

<span data-ttu-id="7755b-139">Execute a página.</span><span class="sxs-lookup"><span data-stu-id="7755b-139">Run the page.</span></span>

<span data-ttu-id="7755b-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7755b-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span></span>

<span data-ttu-id="7755b-141">Insira uma ID, um título, um número de créditos e selecione um departamento, clique **inserir**.</span><span class="sxs-lookup"><span data-stu-id="7755b-141">Enter an ID, a title, a number of credits, and select a department, then click **Insert**.</span></span>

<span data-ttu-id="7755b-142">Execute o *Courses.aspx* página e, em seguida, selecione o mesmo departamento para ver o novo curso.</span><span class="sxs-lookup"><span data-stu-id="7755b-142">Run the *Courses.aspx* page, and select the same department to see the new course.</span></span>

<span data-ttu-id="7755b-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7755b-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span></span>

## <a name="working-with-many-to-many-relationships"></a><span data-ttu-id="7755b-144">Trabalhando com relações muitos-para-muitos</span><span class="sxs-lookup"><span data-stu-id="7755b-144">Working with Many-to-Many Relationships</span></span>

<span data-ttu-id="7755b-145">A relação entre o `Courses` conjunto de entidades e o `People` conjunto de entidades é uma relação muitos-para-muitos.</span><span class="sxs-lookup"><span data-stu-id="7755b-145">The relationship between the `Courses` entity set and the `People` entity set is a many-to-many relationship.</span></span> <span data-ttu-id="7755b-146">Um `Course` entidade tem uma propriedade de navegação nomeada `People` que pode conter zero, um ou mais relacionadas `Person` entidades (representando instrutores atribuídos para ensinar curso).</span><span class="sxs-lookup"><span data-stu-id="7755b-146">A `Course` entity has a navigation property named `People` that can contain zero, one, or more related `Person` entities (representing instructors assigned to teach that course).</span></span> <span data-ttu-id="7755b-147">E um `Person` entidade tem uma propriedade de navegação nomeada `Courses` que pode conter zero, um ou mais relacionadas `Course` entidades (representando cursos instrutor é atribuído a ensinar).</span><span class="sxs-lookup"><span data-stu-id="7755b-147">And a `Person` entity has a navigation property named `Courses` that can contain zero, one, or more related `Course` entities (representing courses that instructor is assigned to teach).</span></span> <span data-ttu-id="7755b-148">Um instrutor pode ministrar vários cursos e um curso pode ser ministrado por vários instrutores.</span><span class="sxs-lookup"><span data-stu-id="7755b-148">One instructor might teach multiple courses, and one course might be taught by multiple instructors.</span></span> <span data-ttu-id="7755b-149">Nesta seção do passo a passo, você irá adicionar e remover relações entre `Person` e `Course` entidades pela atualização das propriedades de navegação de entidades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="7755b-149">In this section of the walkthrough, you'll add and remove relationships between `Person` and `Course` entities by updating the navigation properties of the related entities.</span></span>

<span data-ttu-id="7755b-150">Criar uma nova página da web denominado *InstructorsCourses.aspx* que usa o *Master* página mestra e adicione a seguinte marcação para o `Content` controle chamado `Content2`:</span><span class="sxs-lookup"><span data-stu-id="7755b-150">Create a new web page named *InstructorsCourses.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

<span data-ttu-id="7755b-151">Essa marcação cria um `EntityDataSource` que recupera o nome do controle e `PersonID` de `Person` entidades para os instrutores.</span><span class="sxs-lookup"><span data-stu-id="7755b-151">This markup creates an `EntityDataSource` control that retrieves the name and `PersonID` of `Person` entities for instructors.</span></span> <span data-ttu-id="7755b-152">Um `DropDrownList` controle está vinculado a `EntityDataSource` controle.</span><span class="sxs-lookup"><span data-stu-id="7755b-152">A `DropDrownList` control is bound to the `EntityDataSource` control.</span></span> <span data-ttu-id="7755b-153">O `DropDownList` controle especifica um manipulador para o `DataBound` eventos.</span><span class="sxs-lookup"><span data-stu-id="7755b-153">The `DropDownList` control specifies a handler for the `DataBound` event.</span></span> <span data-ttu-id="7755b-154">Você usará esse manipulador para listas suspensas databind os dois que exibem os cursos.</span><span class="sxs-lookup"><span data-stu-id="7755b-154">You'll use this handler to databind the two drop-down lists that display courses.</span></span>

<span data-ttu-id="7755b-155">A marcação também cria o seguinte grupo de controles a serem usados para atribuir um curso para o instrutor selecionado:</span><span class="sxs-lookup"><span data-stu-id="7755b-155">The markup also creates the following group of controls to use for assigning a course to the selected instructor:</span></span>

- <span data-ttu-id="7755b-156">Um `DropDownList` controle para selecionar um curso para atribuir.</span><span class="sxs-lookup"><span data-stu-id="7755b-156">A `DropDownList` control for selecting a course to assign.</span></span> <span data-ttu-id="7755b-157">Esse controle será preenchido com os cursos que atualmente não estão atribuídos ao instrutor selecionado.</span><span class="sxs-lookup"><span data-stu-id="7755b-157">This control will be populated with courses that are currently not assigned to the selected instructor.</span></span>
- <span data-ttu-id="7755b-158">Um `Button` controle para iniciar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="7755b-158">A `Button` control to initiate the assignment.</span></span>
- <span data-ttu-id="7755b-159">Um `Label` controle para exibir uma mensagem de erro se a atribuição falhará.</span><span class="sxs-lookup"><span data-stu-id="7755b-159">A `Label` control to display an error message if the assignment fails.</span></span>

<span data-ttu-id="7755b-160">Por fim, a marcação também cria um grupo de controles a ser usado para remover um curso do instrutor selecionado.</span><span class="sxs-lookup"><span data-stu-id="7755b-160">Finally, the markup also creates a group of controls to use for removing a course from the selected instructor.</span></span>

<span data-ttu-id="7755b-161">Na *InstructorsCourses.aspx.cs*, adicionar uma instrução:</span><span class="sxs-lookup"><span data-stu-id="7755b-161">In *InstructorsCourses.aspx.cs*, add a using statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

<span data-ttu-id="7755b-162">Adicione um método para preencher as duas listas suspensos que exibem cursos:</span><span class="sxs-lookup"><span data-stu-id="7755b-162">Add a method for populating the two drop-down lists that display courses:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

<span data-ttu-id="7755b-163">Esse código obtém todos os cursos do `Courses` entidade definida e obtém os cursos do `Courses` propriedade de navegação do `Person` entidade para o instrutor selecionado.</span><span class="sxs-lookup"><span data-stu-id="7755b-163">This code gets all courses from the `Courses` entity set and gets the courses from the `Courses` navigation property of the `Person` entity for the selected instructor.</span></span> <span data-ttu-id="7755b-164">Em seguida, ele determina quais cursos são atribuídos ao instrutor e preenche as listas suspensas de acordo.</span><span class="sxs-lookup"><span data-stu-id="7755b-164">It then determines which courses are assigned to that instructor and populates the drop-down lists accordingly.</span></span>

<span data-ttu-id="7755b-165">Adicionar um manipulador para o `Assign` do botão `Click` eventos:</span><span class="sxs-lookup"><span data-stu-id="7755b-165">Add a handler for the `Assign` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

<span data-ttu-id="7755b-166">Esse código obtém os `Person` obtém de entidade para o instrutor selecionado, o `Course` entidade para o curso selecionado e adiciona o curso selecionado para o `Courses` propriedade de navegação do instrutor `Person` entidade.</span><span class="sxs-lookup"><span data-stu-id="7755b-166">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and adds the selected course to the `Courses` navigation property of the instructor's `Person` entity.</span></span> <span data-ttu-id="7755b-167">Em seguida, ele salva as alterações no banco de dados e preenche as listas suspensas para que os resultados podem ser vistos imediatamente.</span><span class="sxs-lookup"><span data-stu-id="7755b-167">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="7755b-168">Adicionar um manipulador para o `Remove` do botão `Click` eventos:</span><span class="sxs-lookup"><span data-stu-id="7755b-168">Add a handler for the `Remove` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

<span data-ttu-id="7755b-169">Esse código obtém os `Person` obtém de entidade para o instrutor selecionado, o `Course` entidade para o curso selecionado e remove o curso selecionado do `Person` da entidade `Courses` propriedade de navegação.</span><span class="sxs-lookup"><span data-stu-id="7755b-169">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and removes the selected course from the `Person` entity's `Courses` navigation property.</span></span> <span data-ttu-id="7755b-170">Em seguida, ele salva as alterações no banco de dados e preenche as listas suspensas para que os resultados podem ser vistos imediatamente.</span><span class="sxs-lookup"><span data-stu-id="7755b-170">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="7755b-171">Adicione código para o `Page_Load` método que garante que as mensagens de erro não são visíveis quando não houver nenhum erro de relatório e adicionar manipuladores para o `DataBound` e `SelectedIndexChanged` eventos da lista suspensa de instrutores para preencher as listas suspensas de cursos:</span><span class="sxs-lookup"><span data-stu-id="7755b-171">Add code to the `Page_Load` method that makes sure the error messages are not visible when there's no error to report, and add handlers for the `DataBound` and `SelectedIndexChanged` events of the instructors drop-down list to populate the courses drop-down lists:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

<span data-ttu-id="7755b-172">Execute a página.</span><span class="sxs-lookup"><span data-stu-id="7755b-172">Run the page.</span></span>

<span data-ttu-id="7755b-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7755b-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span></span>

<span data-ttu-id="7755b-174">Selecione um instrutor.</span><span class="sxs-lookup"><span data-stu-id="7755b-174">Select an instructor.</span></span> <span data-ttu-id="7755b-175">O <strong>atribuir um curso</strong> lista suspensa exibe os cursos que o instrutor não ensina, e o <strong>remover um curso</strong> lista suspensa exibe os cursos que o instrutor já está atribuído a.</span><span class="sxs-lookup"><span data-stu-id="7755b-175">The <strong>Assign a Course</strong> drop-down list displays the courses that the instructor doesn't teach, and the <strong>Remove a Course</strong> drop-down list displays the courses that the instructor is already assigned to.</span></span> <span data-ttu-id="7755b-176">No <strong>atribuir um curso</strong> seção, selecione um curso e, em seguida, clique em <strong>atribuir</strong>.</span><span class="sxs-lookup"><span data-stu-id="7755b-176">In the <strong>Assign a Course</strong> section, select a course and then click <strong>Assign</strong>.</span></span> <span data-ttu-id="7755b-177">O curso se move para o <strong>remover um curso</strong> lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="7755b-177">The course moves to the <strong>Remove a Course</strong> drop-down list.</span></span> <span data-ttu-id="7755b-178">Selecione um curso na <strong>remover um curso</strong> seção e clique em <strong>remover</strong><em>.</em></span><span class="sxs-lookup"><span data-stu-id="7755b-178">Select a course in the <strong>Remove a Course</strong> section and click <strong>Remove</strong><em>.</em></span></span> <span data-ttu-id="7755b-179">O curso se move para o <strong>atribuir um curso</strong> lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="7755b-179">The course moves to the <strong>Assign a Course</strong> drop-down list.</span></span>

<span data-ttu-id="7755b-180">Agora você já viu alguns mais maneiras de trabalhar com dados relacionados.</span><span class="sxs-lookup"><span data-stu-id="7755b-180">You have now seen some more ways to work with related data.</span></span> <span data-ttu-id="7755b-181">O tutorial a seguir, você aprenderá como usar a herança no modelo de dados para melhorar a facilidade de manutenção do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7755b-181">In the following tutorial, you'll learn how to use inheritance in the data model to improve the maintainability of your application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7755b-182">[Anterior](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [Próximo](the-entity-framework-and-aspnet-getting-started-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="7755b-182">[Previous](the-entity-framework-and-aspnet-getting-started-part-4.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-6.md)</span></span>