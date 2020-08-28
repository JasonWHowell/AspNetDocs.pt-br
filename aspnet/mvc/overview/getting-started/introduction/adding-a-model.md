---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Adicionando um modelo | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045111"
---
# <a name="adding-a-model"></a><span data-ttu-id="ef408-102">Adicionar um modelo</span><span class="sxs-lookup"><span data-stu-id="ef408-102">Adding a Model</span></span>

<span data-ttu-id="ef408-103">por [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ef408-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="ef408-104">Nesta seção, você adicionará algumas classes para gerenciar filmes em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ef408-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="ef408-105">Essas classes serão a &quot; parte do modelo &quot; do aplicativo MVC ASP.net.</span><span class="sxs-lookup"><span data-stu-id="ef408-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="ef408-106">Você usará uma .NET Framework tecnologia de acesso a dados conhecida como [Entity Framework](https://docs.microsoft.com/ef/) para definir e trabalhar com essas classes de modelo.</span><span class="sxs-lookup"><span data-stu-id="ef408-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="ef408-107">A Entity Framework (geralmente conhecida como EF) dá suporte a um paradigma de desenvolvimento chamado *Code First*.</span><span class="sxs-lookup"><span data-stu-id="ef408-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="ef408-108">Code First permite que você crie objetos de modelo escrevendo classes simples.</span><span class="sxs-lookup"><span data-stu-id="ef408-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="ef408-109">(Elas também são conhecidas como classes POCO, de &quot; objetos CLR antigos. &quot; ) Em seguida, você pode fazer com que o banco de dados seja criado dinamicamente de suas classes, o que permite um fluxo de trabalho de desenvolvimento muito limpo e rápido.</span><span class="sxs-lookup"><span data-stu-id="ef408-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="ef408-110">Se for necessário primeiro criar o banco de dados, você ainda poderá seguir este tutorial para saber mais sobre o desenvolvimento de aplicativos MVC e EF.</span><span class="sxs-lookup"><span data-stu-id="ef408-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="ef408-111">Em seguida, você pode seguir Tom Fizmakens [ASP.net scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, que aborda a primeira abordagem do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ef408-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="ef408-112">Adicionando classes de modelo</span><span class="sxs-lookup"><span data-stu-id="ef408-112">Adding Model Classes</span></span>

<span data-ttu-id="ef408-113">Em **Gerenciador de soluções**, clique com o botão direito do mouse na pasta *modelos* , selecione **Adicionar**e, em seguida, selecione **classe**.</span><span class="sxs-lookup"><span data-stu-id="ef408-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="ef408-114">Insira o nome da *classe* &quot; Movie &quot; .</span><span class="sxs-lookup"><span data-stu-id="ef408-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="ef408-115">Adicione as cinco propriedades a seguir à `Movie` classe:</span><span class="sxs-lookup"><span data-stu-id="ef408-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="ef408-116">Usaremos a `Movie` classe para representar filmes em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ef408-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="ef408-117">Cada instância de um `Movie` objeto corresponderá a uma linha dentro de uma tabela de banco de dados, e cada propriedade da `Movie` classe será mapeada para uma coluna na tabela.</span><span class="sxs-lookup"><span data-stu-id="ef408-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="ef408-118">Observação: para usar System. Data. Entity e a classe relacionada, você precisa instalar o [Entity Framework pacote NuGet](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="ef408-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="ef408-119">Siga o link para obter mais instruções.</span><span class="sxs-lookup"><span data-stu-id="ef408-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="ef408-120">No mesmo arquivo, adicione a seguinte `MovieDBContext` classe:</span><span class="sxs-lookup"><span data-stu-id="ef408-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="ef408-121">A `MovieDBContext` classe representa o contexto de banco de dados de Entity Framework filme, que lida com a busca, o armazenamento e a atualização de `Movie` instâncias de classe em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ef408-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="ef408-122">O `MovieDBContext` deriva da `DbContext` classe base fornecida pelo Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="ef408-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="ef408-123">Para poder fazer referência a `DbContext` e `DbSet` , você precisa adicionar a seguinte `using` instrução na parte superior do arquivo:</span><span class="sxs-lookup"><span data-stu-id="ef408-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="ef408-124">Você pode fazer isso adicionando manualmente a instrução using, ou pode passar o mouse sobre as linhas onduladas vermelhas, clicar `Show potential fixes` e clicar em `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="ef408-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="ef408-125">Observação: várias instruções não utilizadas foram `using` removidas.</span><span class="sxs-lookup"><span data-stu-id="ef408-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="ef408-126">O Visual Studio mostrará dependências não utilizadas como cinza.</span><span class="sxs-lookup"><span data-stu-id="ef408-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="ef408-127">Você pode remover dependências não utilizadas passando o mouse sobre as dependências de cinza, clicar `Show potential fixes` e clicar em **remover não usado usando.**</span><span class="sxs-lookup"><span data-stu-id="ef408-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="ef408-128">Finalmente adicionamos um modelo (o M no MVC).</span><span class="sxs-lookup"><span data-stu-id="ef408-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="ef408-129">Na próxima seção, você trabalhará com a cadeia de conexão do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ef408-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ef408-130">[Anterior](adding-a-view.md) 
>  [Avançar](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="ef408-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
