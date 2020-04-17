---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Criando ajudantes HTML personalizados (VB) | Microsoft Docs
author: rick-anderson
description: O objetivo deste tutorial é demonstrar como você pode criar ajudas HTML personalizadas que você pode usar dentro de suas visualizações MVC. Aproveitando o HTML Helper...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 52f16bf666edc9f1c95c01faf004e303fcb6a0b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542502"
---
# <a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="f8f6a-104">Criação de auxiliares de HTML personalizados (VB)</span><span class="sxs-lookup"><span data-stu-id="f8f6a-104">Creating Custom HTML Helpers (VB)</span></span>

<span data-ttu-id="f8f6a-105">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f8f6a-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f8f6a-106">Baixar PDF</span><span class="sxs-lookup"><span data-stu-id="f8f6a-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="f8f6a-107">O objetivo deste tutorial é demonstrar como você pode criar ajudas HTML personalizadas que você pode usar dentro de suas visualizações MVC.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="f8f6a-108">Aproveitando os Ajudadores HTML, você pode reduzir a quantidade de digitação tediosa de tags HTML que você deve executar para criar uma página HTML padrão.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="f8f6a-109">O objetivo deste tutorial é demonstrar como você pode criar ajudas HTML personalizadas que você pode usar dentro de suas visualizações MVC.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="f8f6a-110">Aproveitando os Ajudadores HTML, você pode reduzir a quantidade de digitação tediosa de tags HTML que você deve executar para criar uma página HTML padrão.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="f8f6a-111">Na primeira parte deste tutorial, descrevo alguns dos ajudantes HTML existentes incluídos com a estrutura mvc ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="f8f6a-112">Em seguida, descrevo dois métodos de criação de ajudas HTML personalizadas: explico como criar ajudadores HTML personalizados criando um método compartilhado e criando um método de extensão.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="f8f6a-113">Entendendo os ajudantes de HTML</span><span class="sxs-lookup"><span data-stu-id="f8f6a-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="f8f6a-114">Um HTML Helper é apenas um método que retorna uma string.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="f8f6a-115">A seqüência pode representar qualquer tipo de conteúdo que você quiser.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="f8f6a-116">Por exemplo, você pode usar ajudadores HTML `<input>` para `<img>` renderizar tags HTML padrão como HTML e tags.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="f8f6a-117">Você também pode usar ajudadores HTML para renderizar conteúdo mais complexo, como uma tira de guia ou uma tabela HTML de dados de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="f8f6a-118">A ASP.NET estrutura MVC inclui o seguinte conjunto de ajudantes HTML padrão (esta não é uma lista completa):</span><span class="sxs-lookup"><span data-stu-id="f8f6a-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="f8f6a-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-119">Html.ActionLink()</span></span>
- <span data-ttu-id="f8f6a-120">html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-120">Html.BeginForm()</span></span>
- <span data-ttu-id="f8f6a-121">html.Caixa de seleção()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-121">Html.CheckBox()</span></span>
- <span data-ttu-id="f8f6a-122">html.dropdownlist()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-122">Html.DropDownList()</span></span>
- <span data-ttu-id="f8f6a-123">html.endform()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-123">Html.EndForm()</span></span>
- <span data-ttu-id="f8f6a-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-124">Html.Hidden()</span></span>
- <span data-ttu-id="f8f6a-125">html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-125">Html.ListBox()</span></span>
- <span data-ttu-id="f8f6a-126">html.Password()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-126">Html.Password()</span></span>
- <span data-ttu-id="f8f6a-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-127">Html.RadioButton()</span></span>
- <span data-ttu-id="f8f6a-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-128">Html.TextArea()</span></span>
- <span data-ttu-id="f8f6a-129">html.textbox()</span><span class="sxs-lookup"><span data-stu-id="f8f6a-129">Html.TextBox()</span></span>

<span data-ttu-id="f8f6a-130">Por exemplo, considere o formulário na Lista 1.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="f8f6a-131">Este formulário é renderizado com a ajuda de dois dos ajudantes HTML padrão (ver Figura 1).</span><span class="sxs-lookup"><span data-stu-id="f8f6a-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="f8f6a-132">Esta forma `Html.BeginForm()` usa `Html.TextBox()` os métodos e Helper.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>

<span data-ttu-id="f8f6a-133">[![Página renderizada com ajudadores HTML](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f8f6a-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="f8f6a-134">**Figura 01**: Página renderizada com ajudadores HTML[(Clique para ver imagem em tamanho real)](creating-custom-html-helpers-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f8f6a-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>

<span data-ttu-id="f8f6a-135">**Listagem 1 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="f8f6a-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="f8f6a-136">O `Html.BeginForm()` método Helper é usado para `<form>` criar as tags HTML de abertura e fechamento.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="f8f6a-137">Observe que `Html.BeginForm()` o método é chamado dentro de uma declaração de uso.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="f8f6a-138">A declaração de `<form>` uso garante que a tag seja fechada no final do bloco de uso.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="f8f6a-139">Se preferir, em vez de criar um bloco de uso, você pode chamar `<form>` o método de ajuda Html.EndForm() para fechar a tag.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="f8f6a-140">Use qualquer abordagem para criar `<form>` uma tag de abertura e fechamento que pareça mais intuitiva para você.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="f8f6a-141">Os `Html.TextBox()` métodos Helper são usados `<input>` na Listagem 1 para renderizar tags HTML.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="f8f6a-142">Se você selecionar a fonte de exibição no seu navegador, verá a fonte HTML na Listagem 2.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="f8f6a-143">Observe que a fonte contém tags HTML padrão.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8f6a-144">observe que `Html.TextBox()`o -HTML Helper `<%= %>` é `<% %>` renderizado com tags em vez de tags.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="f8f6a-145">Se você não incluir o sinal de igual, então nada será renderizado para o navegador.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="f8f6a-146">A ASP.NET estrutura MVC contém um pequeno conjunto de ajudantes.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="f8f6a-147">Provavelmente, você precisará estender a estrutura MVC com ajudadores HTML personalizados.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="f8f6a-148">No restante deste tutorial, você aprende dois métodos de criação de ajudas HTML personalizadas.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="f8f6a-149">**Listagem 2 –`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="f8f6a-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="f8f6a-150">Criando ajudadores HTML com métodos compartilhados</span><span class="sxs-lookup"><span data-stu-id="f8f6a-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="f8f6a-151">A maneira mais fácil de criar um novo HTML Helper é criar um método compartilhado que retorne uma seqüência.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="f8f6a-152">Imagine, por exemplo, que você decida criar um novo `<label>` Html Helper que renderiza uma tag HTML.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="f8f6a-153">Você pode usar a classe na `<label>`Listagem 2 para renderizar um .</span><span class="sxs-lookup"><span data-stu-id="f8f6a-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="f8f6a-154">**Listagem 2 –`Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="f8f6a-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="f8f6a-155">Não há nada de especial na classe na Lista 2.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="f8f6a-156">O `Label()` método simplesmente retorna uma seqüência.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="f8f6a-157">A exibição Índice modificado `LabelHelper` na Listagem `<label>` 3 usa as tags HTML para renderizar.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="f8f6a-158">Observe que a exibição inclui uma `<%@ imports %>` diretiva que importa o namespace Application1.Helpers.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="f8f6a-159">**Listagem 2 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="f8f6a-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="f8f6a-160">Criando ajudadores HTML com métodos de extensão</span><span class="sxs-lookup"><span data-stu-id="f8f6a-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="f8f6a-161">Se você quiser criar ajudadores HTML que funcionam como os ajudantes HTML padrão incluídos na estrutura ASP.NET MVC, então você precisa criar métodos de extensão.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="f8f6a-162">Os métodos de extensão permitem adicionar novos métodos a uma classe existente.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="f8f6a-163">Ao criar um método HTML Helper, você `HtmlHelper` adiciona novos métodos à classe representada pela propriedade Html de uma exibição.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="f8f6a-164">O módulo Visual Basic na Listagem `Label()` 3 `HtmlHelper` adiciona um método de extensão nomeado para a classe.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="f8f6a-165">Há algumas coisas que você deve notar sobre este módulo.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="f8f6a-166">Primeiro, observe que o módulo `<Extension()>` é decorado com o atributo.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="f8f6a-167">Para usar este atributo, você `System.Runtime.CompilerServices` deve importar o namespace</span><span class="sxs-lookup"><span data-stu-id="f8f6a-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="f8f6a-168">Em segundo lugar, observe que `Label()` o primeiro `HtmlHelper` parâmetro do método representa a classe.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="f8f6a-169">O primeiro parâmetro de um método de extensão indica a classe que o método de extensão se estende.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="f8f6a-170">**Lista 3 –`Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="f8f6a-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="f8f6a-171">Depois de criar um método de extensão e construir seu aplicativo com sucesso, o método de extensão aparece no Visual Studio Intellisense como todos os outros métodos de uma classe (ver Figura 2).</span><span class="sxs-lookup"><span data-stu-id="f8f6a-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="f8f6a-172">A única diferença é que os métodos de extensão aparecem com um símbolo especial ao lado deles (um ícone de uma seta para baixo).</span><span class="sxs-lookup"><span data-stu-id="f8f6a-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="f8f6a-173">[![Usando o método de extensão Html.Label()](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f8f6a-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="f8f6a-174">**Figura 02**: Usando o método de extensão Html.Label()[(Clique para exibir imagem em tamanho real)](creating-custom-html-helpers-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="f8f6a-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>

<span data-ttu-id="f8f6a-175">A exibição Índice modificado na Listagem 4 usa o método &lt;de&gt; extensão Html.Label() para renderizar todas as suas tags de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="f8f6a-176">**Lista 4 –`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="f8f6a-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="f8f6a-177">Resumo</span><span class="sxs-lookup"><span data-stu-id="f8f6a-177">Summary</span></span>

<span data-ttu-id="f8f6a-178">Neste tutorial, você aprendeu dois métodos de criação de ajudas HTML personalizadas.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="f8f6a-179">Primeiro, você aprendeu como `Label()` criar um Html Helper personalizado criando um método compartilhado que retorna uma string.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="f8f6a-180">Em seguida, você aprendeu `Label()` como criar um método html `HtmlHelper` helper personalizado criando um método de extensão na classe.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="f8f6a-181">Neste tutorial, eu me concentrei em construir um método extremamente simples de Ajuda HTML.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="f8f6a-182">Perceba que um ajudante HTML pode ser tão complicado quanto você quiser.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="f8f6a-183">Você pode criar ajudadores HTML que renderizam conteúdo rico, como visualizações de árvores, menus ou tabelas de dados de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f8f6a-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f8f6a-184">[Próximo](asp-net-mvc-views-overview-vb.md)
> [anterior](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f8f6a-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>
