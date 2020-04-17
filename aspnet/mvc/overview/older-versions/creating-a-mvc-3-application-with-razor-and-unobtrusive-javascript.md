---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Criando um aplicativo MVC 3 com Razor e JavaScript discreto | Microsoft Docs
author: rick-anderson
description: O aplicativo web de amostra de lista de usuário demonstra o quão simples é criar ASP.NET aplicativos MVC 3 usando o mecanismo razor view. A aplicação da amostra...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542450"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="86df0-104">Criação de um aplicativo do MVC 3 com Razor e JavaScript não obstrusivo</span><span class="sxs-lookup"><span data-stu-id="86df0-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="86df0-105">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="86df0-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="86df0-106">O aplicativo web de amostra de lista de usuário demonstra o quão simples é criar ASP.NET aplicativos MVC 3 usando o mecanismo razor view.</span><span class="sxs-lookup"><span data-stu-id="86df0-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="86df0-107">O aplicativo de exemplo mostra como usar o novo mecanismo razor view com ASP.NET mvc versão 3 e Visual Studio 2010 para criar um site fictício da Lista de Usuários que inclui funcionalidades como criação, exibição, edição e exclusão de usuários.</span><span class="sxs-lookup"><span data-stu-id="86df0-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="86df0-108">Este tutorial descreve as etapas que foram tomadas para construir a amostra da Lista de Usuários ASP.NET aplicativo MVC 3.</span><span class="sxs-lookup"><span data-stu-id="86df0-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="86df0-109">Um projeto do Visual Studio com código fonte C# e VB está disponível para acompanhar este tópico: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span><span class="sxs-lookup"><span data-stu-id="86df0-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="86df0-110">Se você tiver dúvidas sobre este tutorial, por favor, poste-as no [fórum MVC](https://forums.asp.net/1146.aspx).</span><span class="sxs-lookup"><span data-stu-id="86df0-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="86df0-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="86df0-111">Overview</span></span>

<span data-ttu-id="86df0-112">O aplicativo que você estará construindo é um site de lista de usuários simples.</span><span class="sxs-lookup"><span data-stu-id="86df0-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="86df0-113">Os usuários podem inserir, visualizar e atualizar as informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="86df0-113">Users can enter, view, and update user information.</span></span>

![Local da amostra](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="86df0-115">Você pode baixar o projeto vb e c# concluído [aqui](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span><span class="sxs-lookup"><span data-stu-id="86df0-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="86df0-116">Criando o Aplicativo web</span><span class="sxs-lookup"><span data-stu-id="86df0-116">Creating the Web Application</span></span>

<span data-ttu-id="86df0-117">Para iniciar o tutorial, abra o Visual Studio 2010 e crie um novo projeto usando o modelo *de aplicativo web ASP.NET MVC 3.*</span><span class="sxs-lookup"><span data-stu-id="86df0-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="86df0-118">Nomeie &quot;o aplicativo&quot;Mvc3Razor .</span><span class="sxs-lookup"><span data-stu-id="86df0-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="86df0-119">[![Novo projeto MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="86df0-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="86df0-120">Na caixa de diálogo **Projeto MVC 3 do Novo ASP.NET,** selecione **Aplicativo da Internet,** selecione o mecanismo de exibição de Navalha e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="86df0-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![Diálogo do Projeto MVC 3 do novo ASP.NET](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="86df0-122">Neste tutorial você não estará usando o provedor de associação ASP.NET, para que você possa excluir todos os arquivos associados ao logon e associação.</span><span class="sxs-lookup"><span data-stu-id="86df0-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="86df0-123">No **Solution Explorer,** remova os seguintes arquivos e diretórios:</span><span class="sxs-lookup"><span data-stu-id="86df0-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="86df0-124">*Controladores\AccountController*</span><span class="sxs-lookup"><span data-stu-id="86df0-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="86df0-125">*Modelos\Modelos de conta*</span><span class="sxs-lookup"><span data-stu-id="86df0-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="86df0-126">*Visualizações\_LogOnPartial\\compartilhadas*</span><span class="sxs-lookup"><span data-stu-id="86df0-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="86df0-127">*Visualizações\Conta* (e todos os arquivos neste diretório)</span><span class="sxs-lookup"><span data-stu-id="86df0-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="86df0-129">Edite `<div>` o `logindisplay` <em>&quot;</em>&quot; <em> \_arquivo Layout.cshtml</em> e substitua a marcação dentro do elemento nomeado com a mensagem Login Desativado .</span><span class="sxs-lookup"><span data-stu-id="86df0-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="86df0-130">O exemplo a seguir mostra a nova marcação:</span><span class="sxs-lookup"><span data-stu-id="86df0-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="86df0-131">Adicionando o Modelo</span><span class="sxs-lookup"><span data-stu-id="86df0-131">Adding the Model</span></span>

<span data-ttu-id="86df0-132">No **Solution Explorer,** clique com o botão direito do mouse na pasta *Modelos,* selecione **Adicionar**e clique em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="86df0-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![Nova classe Mdl do usuário](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="86df0-134">Nome da classe `UserModel`.</span><span class="sxs-lookup"><span data-stu-id="86df0-134">Name the class `UserModel`.</span></span> <span data-ttu-id="86df0-135">Substitua o conteúdo do arquivo *UserModel* pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="86df0-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="86df0-136">A `UserModel` classe representa os usuários.</span><span class="sxs-lookup"><span data-stu-id="86df0-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="86df0-137">Cada membro da classe é anotado com o atributo [Obrigatório](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) do namespace [DataAnnotations.](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)</span><span class="sxs-lookup"><span data-stu-id="86df0-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="86df0-138">Os atributos no [namespace DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) fornecem validação automática do lado do cliente e do servidor para aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="86df0-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="86df0-139">Abra `HomeController` a classe `using` e adicione uma diretiva `UserModel` para `Users` que você possa acessar as aulas e as classes:</span><span class="sxs-lookup"><span data-stu-id="86df0-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="86df0-140">Logo após `HomeController` a declaração, adicione o `Users` seguinte comentário e a referência a uma classe:</span><span class="sxs-lookup"><span data-stu-id="86df0-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="86df0-141">A `Users` classe é um armazenamento de dados simplificado na memória que você usará neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="86df0-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="86df0-142">Em um aplicativo real, você usaria um banco de dados para armazenar informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="86df0-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="86df0-143">As primeiras linhas `HomeController` do arquivo são mostradas no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="86df0-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="86df0-144">Construa o aplicativo para que o modelo do usuário esteja disponível para o assistente de andaimes na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="86df0-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="86df0-145">Criando a exibição padrão</span><span class="sxs-lookup"><span data-stu-id="86df0-145">Creating the Default View</span></span>

<span data-ttu-id="86df0-146">O próximo passo é adicionar um método de ação e exibição para exibir os usuários.</span><span class="sxs-lookup"><span data-stu-id="86df0-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="86df0-147">Exclua o arquivo *Views\Home\Index* existente.</span><span class="sxs-lookup"><span data-stu-id="86df0-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="86df0-148">Você criará um novo *arquivo Index* para exibir os usuários.</span><span class="sxs-lookup"><span data-stu-id="86df0-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="86df0-149">Na `HomeController` classe, substitua o `Index` conteúdo do método pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="86df0-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="86df0-150">Clique com o `Index` botão direito do mouse dentro do método e clique em **Adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="86df0-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![Adicionar visualização](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="86df0-152">Selecione a Opção Criar uma opção **de exibição fortemente digitada.**</span><span class="sxs-lookup"><span data-stu-id="86df0-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="86df0-153">Para **exibir classe de dados,** selecione **Mvc3Razor.Models.UserModel**.</span><span class="sxs-lookup"><span data-stu-id="86df0-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="86df0-154">(Se você não ver **Mvc3Razor.Models.UserModel** na caixa **de classe de dados Exibir,** você precisa construir o projeto.) Certifique-se de que o motor de exibição está definido como **Razor**.</span><span class="sxs-lookup"><span data-stu-id="86df0-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="86df0-155">Defina **exibir conteúdo** para **Lista** e clique **em Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86df0-155">Set **View content** to **List** and then click **Add**.</span></span>

![Adicionar visualização de índice](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="86df0-157">A nova exibição desarma automaticamente os dados do `Index` usuário que são passados para a exibição.</span><span class="sxs-lookup"><span data-stu-id="86df0-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="86df0-158">Examine o arquivo *Visualizações\Home\Index* recém-gerado.</span><span class="sxs-lookup"><span data-stu-id="86df0-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="86df0-159">Os links **Criar novo,** **editar,** **editar**e **excluir** não funcionam, mas o resto da página está funcional.</span><span class="sxs-lookup"><span data-stu-id="86df0-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="86df0-160">Execute a página.</span><span class="sxs-lookup"><span data-stu-id="86df0-160">Run the page.</span></span> <span data-ttu-id="86df0-161">Você vê uma lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="86df0-161">You see a list of users.</span></span>

![Página do Índice](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="86df0-163">Abra o arquivo *Index.cshtml* e `ActionLink` substitua a marcação para **Editar**, **Detalhes**e **Excluir** com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="86df0-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="86df0-164">O nome de usuário é usado como ID para encontrar o registro selecionado nos links **Editar,** **Detalhes**e **Excluir.**</span><span class="sxs-lookup"><span data-stu-id="86df0-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="86df0-165">Criando a exibição de detalhes</span><span class="sxs-lookup"><span data-stu-id="86df0-165">Creating the Details View</span></span>

<span data-ttu-id="86df0-166">O próximo passo é `Details` adicionar um método de ação e visualização para exibir os detalhes do usuário.</span><span class="sxs-lookup"><span data-stu-id="86df0-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![Detalhes](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="86df0-168">Adicione o `Details` seguinte método ao controlador doméstico:</span><span class="sxs-lookup"><span data-stu-id="86df0-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="86df0-169">Clique com o `Details` botão direito do mouse dentro do método e selecione <strong>Adicionar exibição</strong>.</span><span class="sxs-lookup"><span data-stu-id="86df0-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="86df0-170">Verifique se a caixa <strong>de classe de dados Exibir</strong> contém <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span><span class="sxs-lookup"><span data-stu-id="86df0-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="86df0-171">Defina <strong>o conteúdo de exibição</strong> para <strong>Detalhes</strong> e clique <strong>em Adicionar</strong>.</span><span class="sxs-lookup"><span data-stu-id="86df0-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![Adicionar visualização de detalhes](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="86df0-173">Execute o aplicativo e selecione um link de detalhes.</span><span class="sxs-lookup"><span data-stu-id="86df0-173">Run the application and select a details link.</span></span> <span data-ttu-id="86df0-174">O andaime automático mostra cada propriedade no modelo.</span><span class="sxs-lookup"><span data-stu-id="86df0-174">The automatic scaffolding shows each property in the model.</span></span>

![Detalhes](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="86df0-176">Criando a exibição editar</span><span class="sxs-lookup"><span data-stu-id="86df0-176">Creating the Edit View</span></span>

<span data-ttu-id="86df0-177">Adicione o `Edit` seguinte método ao controlador doméstico.</span><span class="sxs-lookup"><span data-stu-id="86df0-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="86df0-178">Adicione uma exibição como nas etapas anteriores, mas defina **exibir conteúdo** para **Editar**.</span><span class="sxs-lookup"><span data-stu-id="86df0-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![Adicionar exibição editar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="86df0-180">Execute o aplicativo e edite o primeiro e sobrenome de um dos usuários.</span><span class="sxs-lookup"><span data-stu-id="86df0-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="86df0-181">Se você `DataAnnotation` violar quaisquer restrições que `UserModel` tenham sido aplicadas à classe, ao enviar o formulário, verá erros de validação que são produzidos pelo código do servidor.</span><span class="sxs-lookup"><span data-stu-id="86df0-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="86df0-182">Por exemplo, se você &quot;alterar&quot; &quot;o&quot;primeiro nome Ann para A, quando você enviar o formulário, o seguinte erro será exibido no formulário:</span><span class="sxs-lookup"><span data-stu-id="86df0-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="86df0-183">Neste tutorial, você está tratando o nome de usuário como a chave principal.</span><span class="sxs-lookup"><span data-stu-id="86df0-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="86df0-184">Portanto, a propriedade do nome do usuário não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="86df0-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="86df0-185">No arquivo *Edit.cshtml,* logo `Html.BeginForm` após a declaração, defina o nome de usuário como um campo oculto.</span><span class="sxs-lookup"><span data-stu-id="86df0-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="86df0-186">Isso faz com que a propriedade seja aprovada no modelo.</span><span class="sxs-lookup"><span data-stu-id="86df0-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="86df0-187">O fragmento de código a `Hidden` seguir mostra a colocação da declaração:</span><span class="sxs-lookup"><span data-stu-id="86df0-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="86df0-188">Substitua `TextBoxFor` `ValidationMessageFor` a marcação e a `DisplayFor` marcação para o nome de usuário por uma chamada.</span><span class="sxs-lookup"><span data-stu-id="86df0-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="86df0-189">O `DisplayFor` método exibe a propriedade como um elemento somente leitura.</span><span class="sxs-lookup"><span data-stu-id="86df0-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="86df0-190">O exemplo a seguir mostra a marcação concluída.</span><span class="sxs-lookup"><span data-stu-id="86df0-190">The following example shows the completed markup.</span></span> <span data-ttu-id="86df0-191">O `TextBoxFor` original `ValidationMessageFor` e as chamadas são comentados com os`@* *@`caracteres de início de navalha e comentários finais ( )</span><span class="sxs-lookup"><span data-stu-id="86df0-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="86df0-192">Habilitando a validação do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="86df0-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="86df0-193">Para habilitar a validação do lado do cliente em ASP.NET MVC 3, você deve definir dois sinalizadores e deve incluir três arquivos JavaScript.</span><span class="sxs-lookup"><span data-stu-id="86df0-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="86df0-194">Abra o arquivo *Web.config* do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86df0-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="86df0-195">Verifique `that ClientValidationEnabled` `UnobtrusiveJavaScriptEnabled` e esteja definido como verdadeiro nas configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86df0-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="86df0-196">O fragmento a seguir do arquivo *root Web.config* mostra as configurações corretas:</span><span class="sxs-lookup"><span data-stu-id="86df0-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="86df0-197">A `UnobtrusiveJavaScriptEnabled` configuração para true permite a validação discreta do Ajax e do cliente discreto.</span><span class="sxs-lookup"><span data-stu-id="86df0-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="86df0-198">Quando você usa validação discreta, as regras de validação são transformadas em atributos HTML5.</span><span class="sxs-lookup"><span data-stu-id="86df0-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="86df0-199">Os nomes de atributos HTML5 podem consistir apenas em letras minúsculas, números e traços.</span><span class="sxs-lookup"><span data-stu-id="86df0-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="86df0-200">A `ClientValidationEnabled` configuração para true permite a validação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="86df0-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="86df0-201">Ao definir essas chaves no arquivo *Web.config* do aplicativo, você habilita a validação do cliente e o JavaScript discreto para todo o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86df0-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="86df0-202">Você também pode habilitar ou desativar essas configurações em visualizações individuais ou em métodos de controlador usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="86df0-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="86df0-203">Você também precisa incluir vários arquivos JavaScript na exibição renderizada.</span><span class="sxs-lookup"><span data-stu-id="86df0-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="86df0-204">Uma maneira fácil de incluir o JavaScript em todas as exibições é adicioná-los ao arquivo *Views\Shared\\_Layout.cshtml.*</span><span class="sxs-lookup"><span data-stu-id="86df0-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="86df0-205">Substitua `<head>` o \* \_\* elemento do arquivo Layout.cshtml pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="86df0-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="86df0-206">Os dois primeiros scripts jQuery são hospedados pela Microsoft Ajax Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="86df0-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="86df0-207">Aproveitando o CDN do Microsoft Ajax, você pode melhorar significativamente o desempenho de primeiro hit de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="86df0-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="86df0-208">Execute o aplicativo e clique em um link de edição.</span><span class="sxs-lookup"><span data-stu-id="86df0-208">Run the application and click an edit link.</span></span> <span data-ttu-id="86df0-209">Veja a fonte da página no navegador.</span><span class="sxs-lookup"><span data-stu-id="86df0-209">View the page's source in the browser.</span></span> <span data-ttu-id="86df0-210">A fonte do navegador mostra `data-val` muitos atributos do formulário (para validação de dados).</span><span class="sxs-lookup"><span data-stu-id="86df0-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="86df0-211">Quando a validação do cliente e o JavaScript discreto são habilitados, os `data-val="true"` campos de entrada com uma regra de validação do cliente contêm o atributo para desencadear a validação discreta do cliente.</span><span class="sxs-lookup"><span data-stu-id="86df0-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="86df0-212">Por exemplo, `City` o campo no modelo foi decorado com o atributo [Obrigatório,](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) o que resulta no HTML mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="86df0-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="86df0-213">Para cada regra de validação do cliente, `data-val-rulename="message"`é adicionado um atributo que tem o formulário .</span><span class="sxs-lookup"><span data-stu-id="86df0-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="86df0-214">Usando `City` o exemplo de campo mostrado anteriormente, `data-val-required` a regra &quot;de validação&quot;do cliente necessária gera o atributo e a mensagem O campo Cidade é necessário .</span><span class="sxs-lookup"><span data-stu-id="86df0-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="86df0-215">Execute o aplicativo, edite um dos `City` usuários e limpe o campo.</span><span class="sxs-lookup"><span data-stu-id="86df0-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="86df0-216">Quando você faz a guia para fora do campo, você vê uma mensagem de erro de validação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="86df0-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![Cidade necessária](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="86df0-218">Da mesma forma, para cada parâmetro na regra de validação do `data-val-rulename-paramname=paramvalue`cliente, é adicionado um atributo que tem o formulário .</span><span class="sxs-lookup"><span data-stu-id="86df0-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="86df0-219">Por exemplo, `FirstName` a propriedade é anotada com o atributo [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) e especifica um comprimento mínimo de 3 e um comprimento máximo de 8.</span><span class="sxs-lookup"><span data-stu-id="86df0-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="86df0-220">A regra de `length` validação de `max` dados nomeada tem o nome do parâmetro e o valor do parâmetro 8.</span><span class="sxs-lookup"><span data-stu-id="86df0-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="86df0-221">A seguir, mostra o HTML `FirstName` gerado para o campo quando você edita um dos usuários:</span><span class="sxs-lookup"><span data-stu-id="86df0-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="86df0-222">Para obter mais informações sobre validação de clientes discretas, consulte a entrada [Validação de ClienteS Discretas em ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) no blog de Brad Wilson.</span><span class="sxs-lookup"><span data-stu-id="86df0-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="86df0-223">Em ASP.NET MVC 3 Beta, às vezes você precisa enviar o formulário para iniciar a validação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="86df0-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="86df0-224">Isso pode ser alterado para a versão final.</span><span class="sxs-lookup"><span data-stu-id="86df0-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="86df0-225">Criando a visualização de criação</span><span class="sxs-lookup"><span data-stu-id="86df0-225">Creating the Create View</span></span>

<span data-ttu-id="86df0-226">O próximo passo é `Create` adicionar um método de ação e visualização para permitir que o usuário crie um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="86df0-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="86df0-227">Adicione o `Create` seguinte método ao controlador doméstico:</span><span class="sxs-lookup"><span data-stu-id="86df0-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="86df0-228">Adicione uma exibição como nas etapas anteriores, mas defina **exibir conteúdo** para **Criar**.</span><span class="sxs-lookup"><span data-stu-id="86df0-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Criar exibição](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="86df0-230">Execute o aplicativo, selecione o link **Criar** e adicione um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="86df0-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="86df0-231">O `Create` método aproveita automaticamente a validação do lado do cliente e do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="86df0-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="86df0-232">Tente inserir um nome de usuário que &quot;contenha espaço em branco, como Ben X&quot;.</span><span class="sxs-lookup"><span data-stu-id="86df0-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="86df0-233">Quando você faz a guia para fora do campo`White space is not allowed`nome de usuário, um erro de validação do lado do cliente () é exibido.</span><span class="sxs-lookup"><span data-stu-id="86df0-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="86df0-234">Adicionar o método Excluir</span><span class="sxs-lookup"><span data-stu-id="86df0-234">Add the Delete method</span></span>

<span data-ttu-id="86df0-235">Para completar o tutorial, `Delete` adicione o seguinte método ao controlador doméstico:</span><span class="sxs-lookup"><span data-stu-id="86df0-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="86df0-236">Adicionar `Delete` uma exibição como nas etapas anteriores, definindo **Exibir conteúdo** para **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="86df0-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![Excluir Exibição](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="86df0-238">Agora você tem um aplicativo simples, mas totalmente funcional ASP.NET MVC 3 com validação.</span><span class="sxs-lookup"><span data-stu-id="86df0-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
