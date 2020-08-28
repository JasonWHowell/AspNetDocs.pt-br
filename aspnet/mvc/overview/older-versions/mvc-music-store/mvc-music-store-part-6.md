---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 'Parte 6: usando as anotações de dados para a validação do modelo | Microsoft Docs'
author: jongalloway
description: Esta série de tutoriais detalha todas as etapas usadas para criar o aplicativo de exemplo de loja de música MVC do ASP.NET. A parte 6 aborda o uso de anotações de dados para o modelo V...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 24d3f028a9a720e5b526518624c9c1c2ce2c37d4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044942"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="6299f-104">Parte 6: Uso de anotações de dados para a validação de modelo</span><span class="sxs-lookup"><span data-stu-id="6299f-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="6299f-105">por [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="6299f-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="6299f-106">A loja de música MVC é um aplicativo de tutorial que apresenta e explica passo a passo como usar o ASP.NET MVC e o Visual Studio para desenvolvimento para a Web.</span><span class="sxs-lookup"><span data-stu-id="6299f-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="6299f-107">A loja de música MVC é uma implementação de armazenamento de exemplo leve que vende os álbuns de música online e implementa a administração básica de site, a entrada do usuário e a funcionalidade do carrinho de compras.</span><span class="sxs-lookup"><span data-stu-id="6299f-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="6299f-108">Esta série de tutoriais detalha todas as etapas usadas para criar o aplicativo de exemplo de loja de música MVC do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6299f-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="6299f-109">A parte 6 aborda o uso de anotações de dados para a validação do modelo.</span><span class="sxs-lookup"><span data-stu-id="6299f-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="6299f-110">Temos um grande problema com nossos formulários de criação e edição: eles não estão fazendo nenhuma validação.</span><span class="sxs-lookup"><span data-stu-id="6299f-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="6299f-111">Podemos fazer coisas como deixar os campos obrigatórios em branco ou digitar letras no campo preço, e o primeiro erro que veremos é do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6299f-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="6299f-112">Podemos adicionar facilmente a validação ao nosso aplicativo Adicionando anotações de dados às nossas classes de modelo.</span><span class="sxs-lookup"><span data-stu-id="6299f-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="6299f-113">As anotações de dados nos permitem descrever as regras que queremos aplicar às propriedades do modelo, e o ASP.NET MVC cuidará da imposição delas e da exibição das mensagens apropriadas aos nossos usuários.</span><span class="sxs-lookup"><span data-stu-id="6299f-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="6299f-114">Adicionando validação aos nossos formulários de álbum</span><span class="sxs-lookup"><span data-stu-id="6299f-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="6299f-115">Usaremos os seguintes atributos de anotação de dados:</span><span class="sxs-lookup"><span data-stu-id="6299f-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="6299f-116">**Obrigatório** – indica que a propriedade é um campo obrigatório</span><span class="sxs-lookup"><span data-stu-id="6299f-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="6299f-117">**DisplayName** – define o texto a ser usado em campos de formulário e mensagens de validação</span><span class="sxs-lookup"><span data-stu-id="6299f-117">**DisplayName** – Defines the text to use on form fields and validation messages</span></span>
- <span data-ttu-id="6299f-118">**StringLength** – define um comprimento máximo para um campo de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6299f-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="6299f-119">**Range** – fornece um valor máximo e mínimo para um campo numérico</span><span class="sxs-lookup"><span data-stu-id="6299f-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="6299f-120">**BIND** – lista os campos a serem excluídos ou incluídos ao associar valores de parâmetro ou formulário a propriedades de modelo</span><span class="sxs-lookup"><span data-stu-id="6299f-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="6299f-121">**ScaffoldColumn** – permite ocultar campos de formulários do editor</span><span class="sxs-lookup"><span data-stu-id="6299f-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="6299f-122">*Observação: para obter mais informações sobre a validação de modelo usando atributos de anotação de dados, consulte a documentação do MSDN em*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="6299f-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="6299f-123">Abra a classe album e adicione as instruções *using* a seguir à parte superior.</span><span class="sxs-lookup"><span data-stu-id="6299f-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="6299f-124">Em seguida, atualize as propriedades para adicionar os atributos de exibição e validação, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6299f-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="6299f-125">Enquanto estamos lá, também alteramos o gênero e o artista para propriedades virtuais.</span><span class="sxs-lookup"><span data-stu-id="6299f-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="6299f-126">Isso permite que Entity Framework carregá-los, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="6299f-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="6299f-127">Depois de ter adicionado esses atributos ao nosso modelo de álbum, nossa tela criar e editar imediatamente começa a validar campos e usando os nomes de exibição que escolhemos (por exemplo, a URL de arte do álbum em vez de AlbumArtUrl).</span><span class="sxs-lookup"><span data-stu-id="6299f-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="6299f-128">Execute o aplicativo e navegue até/StoreManager/Create.</span><span class="sxs-lookup"><span data-stu-id="6299f-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="6299f-129">Em seguida, vamos interromper algumas regras de validação.</span><span class="sxs-lookup"><span data-stu-id="6299f-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="6299f-130">Insira um preço de 0 e deixe o título em branco.</span><span class="sxs-lookup"><span data-stu-id="6299f-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="6299f-131">Quando clicamos no botão criar, veremos o formulário exibido com mensagens de erro de validação mostrando quais campos não atenderam às regras de validação que definimos.</span><span class="sxs-lookup"><span data-stu-id="6299f-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="6299f-132">Testando a validação do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="6299f-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="6299f-133">A validação no lado do servidor é muito importante da perspectiva do aplicativo, pois os usuários podem burlar a validação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="6299f-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="6299f-134">No entanto, os formulários da página da Web que implementam apenas a validação no lado do servidor exibem três problemas significativos.</span><span class="sxs-lookup"><span data-stu-id="6299f-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="6299f-135">O usuário deve aguardar até que o formulário seja Postado, validado no servidor e para que a resposta seja enviada ao navegador.</span><span class="sxs-lookup"><span data-stu-id="6299f-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="6299f-136">O usuário não obtém comentários imediatos ao corrigir um campo para que agora passe as regras de validação.</span><span class="sxs-lookup"><span data-stu-id="6299f-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="6299f-137">Estamos desperdiçando recursos de servidor para executar a lógica de validação em vez de aproveitar o navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="6299f-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="6299f-138">Felizmente, os modelos do ASP.NET MVC 3 Scaffold têm validação do lado do cliente interna, não exigindo nenhum trabalho adicional.</span><span class="sxs-lookup"><span data-stu-id="6299f-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="6299f-139">A digitação de uma única letra no campo título atende aos requisitos de validação, portanto, a mensagem de validação é removida imediatamente.</span><span class="sxs-lookup"><span data-stu-id="6299f-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="6299f-140">[Anterior](mvc-music-store-part-5.md) 
>  [Avançar](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="6299f-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
