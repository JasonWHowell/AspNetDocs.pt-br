---
uid: single-page-application/overview/templates/breezeknockout-template
title: Modelo Breeze/Knockout | Microsoft Docs
author: madskristensen
description: Modelo de aplicativo de página única do Breeze/Knockout
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 006d360748674a645ceddb82017f68b0f80f041b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025833"
---
<a name="breezeknockout-template"></a><span data-ttu-id="e43c4-103">Modelo Breeze/Knockout</span><span class="sxs-lookup"><span data-stu-id="e43c4-103">Breeze/Knockout template</span></span>
====================
<span data-ttu-id="e43c4-104">por [Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="e43c4-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="e43c4-105">Modelo Breeze/Knockout MVC foi escrito por Ward Bell</span><span class="sxs-lookup"><span data-stu-id="e43c4-105">The Breeze/Knockout MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="e43c4-106">Baixe o modelo do MVC Breeze/Knockout</span><span class="sxs-lookup"><span data-stu-id="e43c4-106">Download the Breeze/Knockout MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282649)


<span data-ttu-id="e43c4-107">Você já ouviu falar do "aplicativo de página única" (SPA) e se perguntou o que é.</span><span class="sxs-lookup"><span data-stu-id="e43c4-107">You've heard of "single page application" (SPA) and wondered what it is.</span></span> <span data-ttu-id="e43c4-108">Enquanto você pode ler sobre isso, você faria em vez disso, a experiência por conta própria.</span><span class="sxs-lookup"><span data-stu-id="e43c4-108">While you could read about it, you'd rather experience it for yourself.</span></span> <span data-ttu-id="e43c4-109">Mas quem tem tempo para baixar um exemplo?</span><span class="sxs-lookup"><span data-stu-id="e43c4-109">But who has time to download a sample?</span></span> <span data-ttu-id="e43c4-110">Se você tiver o Visual Studio, você terá um SPA de exemplo para cima e em execução em menos de 60 segundos com o ASP.NET MVC 4 modelo de "Breeze/Knockout aplicativo de página única".</span><span class="sxs-lookup"><span data-stu-id="e43c4-110">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds with the ASP.NET MVC 4 "Breeze/Knockout Single Page Application" template.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a><span data-ttu-id="e43c4-111">O que é o modelo do SPA Breeze/Knockout?</span><span class="sxs-lookup"><span data-stu-id="e43c4-111">What is the Breeze/Knockout SPA Template?</span></span>

<span data-ttu-id="e43c4-112">A maioria dos modelos de projeto geram um esqueleto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e43c4-112">Most project templates generate an application skeleton.</span></span> <span data-ttu-id="e43c4-113">Colocar pele nesses ossos adicionando seu código e, eventualmente, fornecer um aplicativo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e43c4-113">You put flesh on those bones by adding your code and eventually deliver a working application.</span></span> <span data-ttu-id="e43c4-114">Modelo Breeze/Knockout SPA é diferente.</span><span class="sxs-lookup"><span data-stu-id="e43c4-114">The Breeze/Knockout SPA template is different.</span></span> <span data-ttu-id="e43c4-115">Ele gera um aplicativo de exemplo para que você possa estudar.</span><span class="sxs-lookup"><span data-stu-id="e43c4-115">It generates a sample application for you to study.</span></span> <span data-ttu-id="e43c4-116">Ela demonstra um design de aplicativo do SPA e muitas das técnicas para a criação de um SPA.</span><span class="sxs-lookup"><span data-stu-id="e43c4-116">It demonstrates a SPA application design and many of the techniques for building a SPA.</span></span>

<span data-ttu-id="e43c4-117">Modelo Breeze/Knockout é uma variação sobre o [modelo KnockoutJS SPA](../introduction/knockoutjs-template.md) incluídas no ASP.NET e Web Tools 2012.2 atualização.</span><span class="sxs-lookup"><span data-stu-id="e43c4-117">The Breeze/Knockout template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="e43c4-118">O modelo de SPA Breeze gera um aplicativo com a mesma experiência de usuário, mas tem uma implementação diferente, usando a Breeze para gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e43c4-118">The Breeze SPA template generates an application with the same user experience, but it has a different implementation, using Breeze for data management.</span></span>

<span data-ttu-id="e43c4-119">O modelo do SPA KnockoutJS faz solicitações de serviço com o jQuery bruto AJAX, que é adequado para um aplicativo simples.</span><span class="sxs-lookup"><span data-stu-id="e43c4-119">The KnockoutJS SPA template makes service requests with raw jQuery AJAX, which is adequate for a simple application.</span></span> <span data-ttu-id="e43c4-120">Mas aplicativos mais sofisticados têm requisitos mais exigentes de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e43c4-120">But more sophisticated apps have more demanding data management requirements.</span></span> <span data-ttu-id="e43c4-121">Por exemplo, a maioria dos aplicativos:</span><span class="sxs-lookup"><span data-stu-id="e43c4-121">For example, most applications:</span></span>

- <span data-ttu-id="e43c4-122">Consultar e consultar novamente o servidor durante uma sessão de usuário estendido.</span><span class="sxs-lookup"><span data-stu-id="e43c4-122">Query and re-query the server during an extended user session.</span></span>
- <span data-ttu-id="e43c4-123">Adicione filtros de consulta, classificação e paginação.</span><span class="sxs-lookup"><span data-stu-id="e43c4-123">Add query filters, sorting, and paging.</span></span>
- <span data-ttu-id="e43c4-124">Compartilhe os mesmos dados em várias telas.</span><span class="sxs-lookup"><span data-stu-id="e43c4-124">Share the same data across multiple screens.</span></span>
- <span data-ttu-id="e43c4-125">Acumular alterações a muitos objetos e, em seguida, salvá-los como uma única transação.</span><span class="sxs-lookup"><span data-stu-id="e43c4-125">Accumulate changes to many objects, then save them as a single transaction.</span></span>
- <span data-ttu-id="e43c4-126">Valide alterações no cliente, para que o usuário pode corrigir erros antes de confirmar as alterações no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e43c4-126">Validate changes on the client, so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="e43c4-127">A biblioteca de BreezeJS trata essas tarefas para você, liberando você para desenvolver a experiência de usuário e a lógica de aplicativo mais importantes.</span><span class="sxs-lookup"><span data-stu-id="e43c4-127">The BreezeJS library handles these chores for you, freeing you to develop the application logic and user experience that matter most.</span></span>

<span data-ttu-id="e43c4-128">[**Breeze** ](http://www.breezejs.com/?utm_source=ms-spa) é uma biblioteca de software livre para criar aplicativos de dados avançados no JavaScript e HTML, os tipos de aplicativos que tenham sido historicamente entregues como aplicativos de área de trabalho autônomos.</span><span class="sxs-lookup"><span data-stu-id="e43c4-128">[**Breeze**](http://www.breezejs.com/?utm_source=ms-spa) is an open source library for building rich data applications in JavaScript and HTML, the kinds of apps that have historically been delivered as stand-alone desktop applications.</span></span>

<span data-ttu-id="e43c4-129">Modelo Breeze/Knockout ajuda você a fazer a primeira etapa crucial em direção a uma infra-estrutura mais robusta de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e43c4-129">The Breeze/Knockout template helps you take that first crucial step toward a more robust data management infrastructure.</span></span> <span data-ttu-id="e43c4-130">Ele produz um aplicativo de tarefas pendentes de exemplo externamente idêntica ao modelo KnockoutJS SPA.</span><span class="sxs-lookup"><span data-stu-id="e43c4-130">It produces a sample Todo application that is outwardly identical to the KnockoutJS SPA template.</span></span> <span data-ttu-id="e43c4-131">No interior, ela substitui a camada de dados do AJAX com a Breeze, para que você possa comparar as duas abordagens de lado a lado.</span><span class="sxs-lookup"><span data-stu-id="e43c4-131">On the inside, it replaces the AJAX data layer with Breeze, so you can compare the two approaches side-by-side.</span></span> <span data-ttu-id="e43c4-132">É claro, mal toca o potencial de um aplicativo muito simples.</span><span class="sxs-lookup"><span data-stu-id="e43c4-132">Of course, it barely touches the potential of a Breeze application.</span></span> <span data-ttu-id="e43c4-133">Mas você verá como a Breeze funciona e como é necessário para tornar essa transição.</span><span class="sxs-lookup"><span data-stu-id="e43c4-133">But you'll see how Breeze works and how little is required to make that transition.</span></span>

<span data-ttu-id="e43c4-134">Vamos começar.</span><span class="sxs-lookup"><span data-stu-id="e43c4-134">Let's get started.</span></span>

## <a name="create-a-breezeknockout-template-project"></a><span data-ttu-id="e43c4-135">Criar um projeto de modelo Breeze/Knockout</span><span class="sxs-lookup"><span data-stu-id="e43c4-135">Create a Breeze/Knockout Template Project</span></span>

<span data-ttu-id="e43c4-136">Baixe e instale o modelo clicando no botão de Download acima.</span><span class="sxs-lookup"><span data-stu-id="e43c4-136">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="e43c4-137">O modelo é empacotado como um arquivo de extensão VSIX (Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="e43c4-137">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="e43c4-138">Talvez você precise reiniciar o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e43c4-138">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="e43c4-139">No painel **Modelos**, selecione **Modelos Instalados** e expanda o nó **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-139">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="e43c4-140">Em **Visual C#**, selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="e43c4-141">Na lista de modelos de projeto, selecione **aplicativo Web do ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-141">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="e43c4-142">Nomeie o projeto e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-142">Name the project and click **OK**.</span></span>

<span data-ttu-id="e43c4-143">No **novo projeto** assistente, selecione **Breeze Knockout SPA**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-143">In the **New Project** wizard, select **Breeze Knockout SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

<span data-ttu-id="e43c4-144">Pressione Ctrl-F5 para compilar e executar o aplicativo sem depuração ou pressione F5 para executar com depuração.</span><span class="sxs-lookup"><span data-stu-id="e43c4-144">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

<span data-ttu-id="e43c4-145">Quando o aplicativo é executado pela primeira vez, ele exibe uma tela de logon.</span><span class="sxs-lookup"><span data-stu-id="e43c4-145">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="e43c4-146">Clique no link de "Inscrição" e uma nova página glides no modo de exibição, onde você pode inserir um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="e43c4-146">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="e43c4-147">(As páginas de logon e registro são criadas usando o ASP.NET MVC). Quando você envia o formulário de registro, o servidor gera uma lista de tarefas pendentes com dois itens para sua conta.</span><span class="sxs-lookup"><span data-stu-id="e43c4-147">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="e43c4-148">Ele apresenta a você uma nota amarelo.</span><span class="sxs-lookup"><span data-stu-id="e43c4-148">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="e43c4-149">Agora você está no land do SPA.</span><span class="sxs-lookup"><span data-stu-id="e43c4-149">Now you are in the land of SPA.</span></span> <span data-ttu-id="e43c4-150">Tudo o que você vê e apresentar enquanto manipular Todos é renderizado e gerenciado no cliente com a Ajuda do Knockout e Breeze.</span><span class="sxs-lookup"><span data-stu-id="e43c4-150">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="e43c4-151">Explore o aplicativo como um usuário...</span><span class="sxs-lookup"><span data-stu-id="e43c4-151">Explore the app as a user …</span></span> <span data-ttu-id="e43c4-152">mas com o olho do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="e43c4-152">but with a developer's eye.</span></span> <span data-ttu-id="e43c4-153">Use as ferramentas de desenvolvedor em seu navegador para capturar o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="e43c4-153">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="e43c4-154">(No Internet Explorer: Pressione F12, selecione a **rede** guia e, em seguida, clique em **inicia a captura**.) Agora, tente o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e43c4-154">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="e43c4-155">Adicione um novo item de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="e43c4-155">Add a new Todo item.</span></span>
- <span data-ttu-id="e43c4-156">Clique no rótulo e editar o título do item de tarefas pendentes</span><span class="sxs-lookup"><span data-stu-id="e43c4-156">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="e43c4-157">Marque uma caixa de seleção para marcar um item concluído.</span><span class="sxs-lookup"><span data-stu-id="e43c4-157">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="e43c4-158">Observe que a caixa de texto está desabilitada, portanto, o título não é mais editável.</span><span class="sxs-lookup"><span data-stu-id="e43c4-158">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="e43c4-159">Clique em 'x' à direita do rótulo.</span><span class="sxs-lookup"><span data-stu-id="e43c4-159">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="e43c4-160">O item desaparece e é excluído do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e43c4-160">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="e43c4-161">Escolher outro item e limpar seu título.</span><span class="sxs-lookup"><span data-stu-id="e43c4-161">Pick another item and clear its title.</span></span> <span data-ttu-id="e43c4-162">Você obterá um erro de validação que o título é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="e43c4-162">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="e43c4-163">Após uma pequena pausa, o título anterior é restaurado.</span><span class="sxs-lookup"><span data-stu-id="e43c4-163">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="e43c4-164">Digite um título ridiculamente longo.</span><span class="sxs-lookup"><span data-stu-id="e43c4-164">Type in a ridiculously long title.</span></span> <span data-ttu-id="e43c4-165">Você obterá um erro de validação diferente que o título é muito longo.</span><span class="sxs-lookup"><span data-stu-id="e43c4-165">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="e43c4-166">Clique no botão "Adicionar a lista de tarefas".</span><span class="sxs-lookup"><span data-stu-id="e43c4-166">Click the "Add Todo List" button.</span></span> <span data-ttu-id="e43c4-167">Uma nova lista é exibida à esquerda da lista anterior.</span><span class="sxs-lookup"><span data-stu-id="e43c4-167">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="e43c4-168">Brincar com o título de lista de tarefas pendentes, acionar seu necessária e validações de comprimento.</span><span class="sxs-lookup"><span data-stu-id="e43c4-168">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="e43c4-169">Clique na caixa de texto de título para limpar a mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="e43c4-169">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="e43c4-170">Clique no "x" no círculo no canto superior direito para excluir a lista de tarefas e suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="e43c4-170">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>

<span data-ttu-id="e43c4-171">A lógica de validação é executada no lado do cliente pelo Breeze.</span><span class="sxs-lookup"><span data-stu-id="e43c4-171">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="e43c4-172">Atributos de validação nas classes de modelo de servidor são propagados para o cliente e executados automaticamente antes do cliente contata o servidor.</span><span class="sxs-lookup"><span data-stu-id="e43c4-172">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="e43c4-173">Analise o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="e43c4-173">Review the network traffic.</span></span> <span data-ttu-id="e43c4-174">Observe que não havia nenhuma chamada para o servidor quando a Breeze detectou um erro.</span><span class="sxs-lookup"><span data-stu-id="e43c4-174">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="e43c4-175">Cada alteração válida resultou em uma solicitação POST para "/ api/Todo/SaveChanges".</span><span class="sxs-lookup"><span data-stu-id="e43c4-175">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="e43c4-176">Breeze agrupa as alterações e envia-os juntos como uma única solicitação para o controlador de API da Web `SaveChanges` método.</span><span class="sxs-lookup"><span data-stu-id="e43c4-176">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="e43c4-177">Isso é diferente do modelo KockoutJS SPA, o que torna o PUT, POST e excluir solicitações para cada item individualmente.</span><span class="sxs-lookup"><span data-stu-id="e43c4-177">That's different from KockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="e43c4-178">Olhar dentro</span><span class="sxs-lookup"><span data-stu-id="e43c4-178">Peek inside</span></span>

<span data-ttu-id="e43c4-179">Este aplicativo tem um cliente e um servidor.</span><span class="sxs-lookup"><span data-stu-id="e43c4-179">This application has a client side and a server side.</span></span> <span data-ttu-id="e43c4-180">A pilha do lado do cliente consiste em HTML uma pequena e uma combinação de módulos de JavaScript do aplicativo (na pasta "aplicativo") além de bibliotecas JavaScript de terceiros (na pasta "Scripts").</span><span class="sxs-lookup"><span data-stu-id="e43c4-180">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

<span data-ttu-id="e43c4-181">Se você investigamos o modelo KnockoutJS SPA, isso deve ser bastante familiar.</span><span class="sxs-lookup"><span data-stu-id="e43c4-181">If you've investigated the KnockoutJS SPA template, this should look very familiar.</span></span> <span data-ttu-id="e43c4-182">Focalizar as caixas azuis.</span><span class="sxs-lookup"><span data-stu-id="e43c4-182">Focus on the blue boxes.</span></span> <span data-ttu-id="e43c4-183">A arquitetura de interface do usuário é Model-View-ViewModel (MVVM), na qual os widgets HTML da exibição corretamente são separados do código de apresentação suporte no modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="e43c4-183">The UI architecture is Model-View-ViewModel (MVVM), in which the HTML widgets of the view are cleanly separated from the supporting presentation code in the view-model.</span></span> <span data-ttu-id="e43c4-184">Um sistema de associação de dados (neste caso, o Knockout) coordena a exibição e o modelo de exibição para que cada um pode fazer seu trabalho sem conhecimento profundo das outras.</span><span class="sxs-lookup"><span data-stu-id="e43c4-184">A data binding system (Knockout in this case) coordinates the view and view-model so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="e43c4-185">O modelo encapsula os dados de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="e43c4-185">The model encapsulates the Todo data.</span></span> <span data-ttu-id="e43c4-186">Entidades no modelo são construídas pelo Breeze com propriedades observáveis do Knockout, portanto, eles podem ser associados diretamente a widgets no modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="e43c4-186">Entities in the model are constructed by Breeze with Knockout observable properties, so they can be bound directly to widgets in the view.</span></span> <span data-ttu-id="e43c4-187">O modelo de exibição solicita que o contexto de dados para adquirir e salvar as entidades de modelo.</span><span class="sxs-lookup"><span data-stu-id="e43c4-187">The view-model asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="e43c4-188">O contexto de dados delega a maior parte do trabalho a Breeze.</span><span class="sxs-lookup"><span data-stu-id="e43c4-188">The data context delegates most of the work to Breeze.</span></span>

<span data-ttu-id="e43c4-189">A pilha do lado do servidor consiste em um código de desenvolvedor e três bibliotecas .NET de princípio: API da Web, Entity Framework e Breeze.NET:</span><span class="sxs-lookup"><span data-stu-id="e43c4-189">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="e43c4-190">A arquitetura básica é o mesmo que o modelo do SPA KockoutJS.</span><span class="sxs-lookup"><span data-stu-id="e43c4-190">The basic architecture is the same as the KockoutJS SPA template.</span></span> <span data-ttu-id="e43c4-191">No entanto, a implementação é muito mais simples: Os DTOs foram excluídos, e a maioria dos detalhes do Entity Framework foram delegadas a Breeze.NET.</span><span class="sxs-lookup"><span data-stu-id="e43c4-191">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e43c4-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e43c4-192">Next Steps</span></span>

<span data-ttu-id="e43c4-193">Sugerimos que você explore o código, orientado pela [discussão abrangente](http://www.breezejs.com/spa-template?utm_source=ms-spa) do cliente e as pilhas de servidor no site da Breeze.</span><span class="sxs-lookup"><span data-stu-id="e43c4-193">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="e43c4-194">Você pode experimentar, brincar com consulta do lado do cliente Breeze; Adicione alguns filtros e classificações.</span><span class="sxs-lookup"><span data-stu-id="e43c4-194">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="e43c4-195">Você pode adicionar mais propriedades de modelo e entidades mais para obter uma ideia melhor para desenvolvimento de ponta a ponta do SPA.</span><span class="sxs-lookup"><span data-stu-id="e43c4-195">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="e43c4-196">Quando estiver certo do design, você pode desfazer os recursos de Todo e substitua-os pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="e43c4-196">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="e43c4-197">Logo você estará pronto para a próxima grande etapa: Adicionando telas do lado do cliente e navegar entre eles.</span><span class="sxs-lookup"><span data-stu-id="e43c4-197">Soon you'll be ready for the next big step: Adding client-side screens and navigating among them.</span></span> <span data-ttu-id="e43c4-198">Você deixar este modelo do SPA para trás e ativar a uma pilha SPA mais completa, como [toalha quente do John Papa](https://github.com/johnpapa/HotTowel#readme "Hot Towel"), que adiciona Durandal à combinação de Breeze e Knockout.</span><span class="sxs-lookup"><span data-stu-id="e43c4-198">You'll leave this SPA template behind and turn to a more complete SPA stack, such as [John Papa's Hot Towel](https://github.com/johnpapa/HotTowel#readme "Hot Towel"), which adds Durandal to the Breeze and Knockout mix.</span></span>