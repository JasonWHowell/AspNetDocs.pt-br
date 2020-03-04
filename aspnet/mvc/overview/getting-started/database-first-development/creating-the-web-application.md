---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'Tutorial: Criar o aplicativo Web e os modelos de dados para o banco de dados do EF primeiro com o ASP.NET MVC'
description: Este tutorial se concentra em criar o aplicativo web e gerar os modelos de dados com base em suas tabelas de banco de dados.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59404514"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="375ed-103">Tutorial: Criar o aplicativo Web e os modelos de dados para o banco de dados do EF primeiro com o ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="375ed-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="375ed-104">Usando o MVC, Entity Framework e o Scaffolding do ASP.NET, você pode criar um aplicativo web que fornece uma interface para um banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="375ed-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="375ed-105">Esta série de tutoriais mostra como automaticamente gerar um código que permite aos usuários exibir, editar, criar e excluir dados que residem em uma tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="375ed-106">O código gerado corresponde às colunas na tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="375ed-107">Este tutorial se concentra em criar o aplicativo web e gerar os modelos de dados com base em suas tabelas de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="375ed-108">Neste tutorial, você:</span><span class="sxs-lookup"><span data-stu-id="375ed-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="375ed-109">Criar um aplicativo Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="375ed-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="375ed-110">Gerar modelos</span><span class="sxs-lookup"><span data-stu-id="375ed-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="375ed-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="375ed-111">Prerequisites</span></span>

* [<span data-ttu-id="375ed-112">Introdução ao Entity Framework 6 Database First usando MVC 5</span><span class="sxs-lookup"><span data-stu-id="375ed-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="375ed-113">Criar um aplicativo Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="375ed-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="375ed-114">Em uma nova solução ou a mesma solução que o projeto de banco de dados, crie um novo projeto no Visual Studio e selecione o **aplicativo Web ASP.NET** modelo.</span><span class="sxs-lookup"><span data-stu-id="375ed-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="375ed-115">Nomeie o projeto **ContosoSite**.</span><span class="sxs-lookup"><span data-stu-id="375ed-115">Name the project **ContosoSite**.</span></span>

![Criar projeto](creating-the-web-application/_static/image1.png)

<span data-ttu-id="375ed-117">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="375ed-117">Click **OK**.</span></span>

<span data-ttu-id="375ed-118">Na janela novo projeto ASP.NET, selecione o **MVC** modelo.</span><span class="sxs-lookup"><span data-stu-id="375ed-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="375ed-119">Você pode limpar a **hospedar na nuvem** opção por enquanto porque você implantará o aplicativo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="375ed-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="375ed-120">Clique em **Okey** para criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="375ed-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="375ed-121">O projeto é criado com o padrão de arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="375ed-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="375ed-122">Neste tutorial, você usará o Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="375ed-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="375ed-123">Você pode verificar a versão do Entity Framework em seu projeto por meio da janela Gerenciar pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="375ed-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="375ed-124">Se necessário, atualize sua versão do Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="375ed-124">If necessary, update your version of Entity Framework.</span></span>

![Mostrar versão](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="375ed-126">Gerar modelos</span><span class="sxs-lookup"><span data-stu-id="375ed-126">Generate the models</span></span>

<span data-ttu-id="375ed-127">Agora você irá criar modelos do Entity Framework das tabelas do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="375ed-128">Esses modelos são classes que você usará para trabalhar com os dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="375ed-129">Cada modelo espelha a uma tabela no banco de dados e contém propriedades que correspondem às colunas na tabela.</span><span class="sxs-lookup"><span data-stu-id="375ed-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="375ed-130">Clique com botão direito do **modelos** pasta e selecione **Add** e **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="375ed-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="375ed-131">Na janela Adicionar Novo Item, selecione **dados** no painel esquerdo e **modelo de dados de entidade ADO.NET** nas opções do painel central.</span><span class="sxs-lookup"><span data-stu-id="375ed-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="375ed-132">Nomeie o novo arquivo de modelo **ContosoModel**.</span><span class="sxs-lookup"><span data-stu-id="375ed-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="375ed-133">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="375ed-133">Click **Add**.</span></span>

<span data-ttu-id="375ed-134">No Assistente de modelo de dados de entidade, selecione **EF Designer do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="375ed-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="375ed-135">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="375ed-135">Click **Next**.</span></span>

<span data-ttu-id="375ed-136">Se você tiver conexões de banco de dados definidas dentro do ambiente de desenvolvimento, você poderá ver uma dessas conexões pré-selecionada.</span><span class="sxs-lookup"><span data-stu-id="375ed-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="375ed-137">No entanto, você deseja criar uma nova conexão ao banco de dados que você criou na primeira parte deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="375ed-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="375ed-138">Clique o **nova Conexão** botão.</span><span class="sxs-lookup"><span data-stu-id="375ed-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="375ed-139">Na janela Propriedades de Conexão, forneça o nome do servidor local em que seu banco de dados foi criado (neste caso **\ProjectsV13 (localdb)** ).</span><span class="sxs-lookup"><span data-stu-id="375ed-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="375ed-140">Depois de fornecer o nome do servidor, selecione o ContosoUniversityData de bancos de dados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="375ed-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![definir propriedades de conexão](creating-the-web-application/_static/image8.png)

<span data-ttu-id="375ed-142">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="375ed-142">Click **OK**.</span></span>

<span data-ttu-id="375ed-143">As propriedades de conexão corretas são exibidas agora.</span><span class="sxs-lookup"><span data-stu-id="375ed-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="375ed-144">Você pode usar o nome padrão para a conexão no arquivo Web. config.</span><span class="sxs-lookup"><span data-stu-id="375ed-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="375ed-145">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="375ed-145">Click **Next**.</span></span>

<span data-ttu-id="375ed-146">Selecione a versão mais recente do Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="375ed-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="375ed-147">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="375ed-147">Click **Next**.</span></span>

<span data-ttu-id="375ed-148">Selecione **tabelas** para gerar modelos para todas as três tabelas.</span><span class="sxs-lookup"><span data-stu-id="375ed-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="375ed-149">Clique em **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="375ed-149">Click **Finish**.</span></span>

<span data-ttu-id="375ed-150">Se você receber um aviso de segurança, selecione **Okey** para continuar a execução do modelo.</span><span class="sxs-lookup"><span data-stu-id="375ed-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="375ed-151">Os modelos são gerados a partir de tabelas de banco de dados e é exibido um diagrama que mostra as propriedades e relacionamentos entre as tabelas.</span><span class="sxs-lookup"><span data-stu-id="375ed-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![diagrama de modelo](creating-the-web-application/_static/image11.png)

<span data-ttu-id="375ed-153">A pasta de modelos agora inclui muitos novos arquivos relacionados aos modelos que foram gerados por banco de dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="375ed-154">O **ContosoModel.Context.cs** arquivo contém uma classe que deriva de **DbContext** de classe e fornece uma propriedade para cada classe de modelo que corresponde a uma tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="375ed-155">O **Course.cs**, **Enrollment.cs**, e **Student.cs** arquivos contêm as classes de modelo que representam as tabelas de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="375ed-156">Você usará a classe de contexto e as classes de modelo ao trabalhar com o scaffolding.</span><span class="sxs-lookup"><span data-stu-id="375ed-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="375ed-157">Antes de continuar com este tutorial, compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="375ed-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="375ed-158">Na próxima seção, você irá gerar código com base em modelos de dados, mas essa seção não funcionarão se o projeto não tiver sido compilado.</span><span class="sxs-lookup"><span data-stu-id="375ed-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="375ed-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="375ed-159">Next steps</span></span>

<span data-ttu-id="375ed-160">Neste tutorial, você:</span><span class="sxs-lookup"><span data-stu-id="375ed-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="375ed-161">Criado um aplicativo web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="375ed-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="375ed-162">Geradas de modelos</span><span class="sxs-lookup"><span data-stu-id="375ed-162">Generated the models</span></span>

<span data-ttu-id="375ed-163">Vá para o próximo tutorial para aprender a criar gerar código com base em modelos de dados.</span><span class="sxs-lookup"><span data-stu-id="375ed-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="375ed-164">Gerando exibições</span><span class="sxs-lookup"><span data-stu-id="375ed-164">Generating views</span></span>](generating-views.md)
