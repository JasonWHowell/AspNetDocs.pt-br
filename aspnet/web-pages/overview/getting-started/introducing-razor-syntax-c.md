---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Introdução à programação da Web do ASP.NET usando a sintaxeC#do Razor () | Microsoft Docs
author: Rick-Anderson
description: Este capítulo fornece uma visão geral da programação com Páginas da Web do ASP.NET usando o sintaxe Razor. ASP.NET é a tecnologia da Microsoft para executar o PA da Web dinâmico...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641571"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="8d55d-104">Introdução à programação da Web do ASP.NET usando a sintaxeC#do Razor ()</span><span class="sxs-lookup"><span data-stu-id="8d55d-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="8d55d-105">por [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8d55d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8d55d-106">Este artigo fornece uma visão geral da programação com Páginas da Web do ASP.NET usando o sintaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="8d55d-107">ASP.NET é a tecnologia da Microsoft para executar páginas da Web dinâmicas em servidores Web.</span><span class="sxs-lookup"><span data-stu-id="8d55d-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="8d55d-108">Este artigo se concentra no uso da C# linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="8d55d-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="8d55d-109">**O que você aprenderá**:</span><span class="sxs-lookup"><span data-stu-id="8d55d-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="8d55d-110">As 8 principais dicas de programação para introdução ao Páginas da Web do ASP.NET de programação usando sintaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="8d55d-111">Conceitos básicos de programação que você precisará.</span><span class="sxs-lookup"><span data-stu-id="8d55d-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="8d55d-112">O que é o código do servidor ASP.NET e a sintaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="8d55d-113">Versões de software</span><span class="sxs-lookup"><span data-stu-id="8d55d-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="8d55d-114">Páginas da Web do ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="8d55d-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="8d55d-115">Este tutorial também funciona com o Páginas da Web do ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="8d55d-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="8d55d-116">As 8 principais dicas de programação</span><span class="sxs-lookup"><span data-stu-id="8d55d-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="8d55d-117">Esta seção lista algumas dicas que você precisa saber ao começar a escrever o código do servidor ASP.NET usando o sintaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="8d55d-118">A sintaxe Razor é baseada na linguagem C# de programação, e essa é a linguagem usada com mais frequência com páginas da Web do ASP.net.</span><span class="sxs-lookup"><span data-stu-id="8d55d-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="8d55d-119">No entanto, o sintaxe Razor também dá suporte à linguagem de Visual Basic e tudo o que você vê também pode fazer em Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="8d55d-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="8d55d-120">Para obter detalhes, consulte o apêndice [Visual Basic linguagem e sintaxe](https://go.microsoft.com/fwlink/?LinkId=202908).</span><span class="sxs-lookup"><span data-stu-id="8d55d-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="8d55d-121">Você pode encontrar mais detalhes sobre a maioria dessas técnicas de programação posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="8d55d-122">1. você adiciona código a uma página usando o caractere @</span><span class="sxs-lookup"><span data-stu-id="8d55d-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="8d55d-123">O caractere `@` inicia expressões embutidas, blocos de instrução simples e blocos de várias instruções:</span><span class="sxs-lookup"><span data-stu-id="8d55d-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="8d55d-124">É assim que essas instruções se parecem quando a página é executada em um navegador:</span><span class="sxs-lookup"><span data-stu-id="8d55d-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="8d55d-126">**Codificação HTML**</span><span class="sxs-lookup"><span data-stu-id="8d55d-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="8d55d-127">Quando você exibe o conteúdo em uma página usando o caractere `@`, como nos exemplos anteriores, o ASP.NET HTML codifica a saída.</span><span class="sxs-lookup"><span data-stu-id="8d55d-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="8d55d-128">Isso substitui os caracteres HTML reservados (como `<` e `>` e `&`) por códigos que permitem que os caracteres sejam exibidos como caracteres em uma página da Web, em vez de serem interpretados como marcas HTML ou entidades.</span><span class="sxs-lookup"><span data-stu-id="8d55d-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="8d55d-129">Sem codificação HTML, a saída do código do servidor pode não ser exibida corretamente e pode expor uma página a riscos de segurança.</span><span class="sxs-lookup"><span data-stu-id="8d55d-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="8d55d-130">Se sua meta é gerar uma marcação HTML que renderiza marcas como marcação (por exemplo `<p></p>` para um parágrafo ou `<em></em>` para enfatizar o texto), consulte a seção [combinando texto, marcação e código em blocos de código](#BM_CombiningTextMarkupAndCode) mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="8d55d-131">Você pode ler mais sobre codificação HTML em [trabalhando com formulários](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="8d55d-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="8d55d-132">2. você coloca blocos de código entre chaves</span><span class="sxs-lookup"><span data-stu-id="8d55d-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="8d55d-133">Um *bloco de código* inclui uma ou mais instruções de código e é colocado entre chaves.</span><span class="sxs-lookup"><span data-stu-id="8d55d-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="8d55d-134">O resultado exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="8d55d-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="8d55d-136">3. dentro de um bloco, você encerra cada instrução de código com um ponto e vírgula</span><span class="sxs-lookup"><span data-stu-id="8d55d-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="8d55d-137">Dentro de um bloco de código, cada instrução de código completa deve terminar com um ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="8d55d-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="8d55d-138">Expressões embutidas não terminam com ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="8d55d-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="8d55d-139">4. você usa variáveis para armazenar valores</span><span class="sxs-lookup"><span data-stu-id="8d55d-139">4. You use variables to store values</span></span>

<span data-ttu-id="8d55d-140">Você pode armazenar valores em uma *variável*, incluindo cadeias de caracteres, números e datas, etc. Você cria uma nova variável usando a palavra-chave `var`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="8d55d-141">Você pode inserir valores de variáveis diretamente em uma página usando `@`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="8d55d-142">O resultado exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="8d55d-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="8d55d-144">5. você coloca valores de cadeia de caracteres literais entre aspas duplas</span><span class="sxs-lookup"><span data-stu-id="8d55d-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="8d55d-145">Uma *String* é uma sequência de caracteres que são tratados como texto.</span><span class="sxs-lookup"><span data-stu-id="8d55d-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="8d55d-146">Para especificar uma cadeia de caracteres, coloque-a entre aspas duplas:</span><span class="sxs-lookup"><span data-stu-id="8d55d-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="8d55d-147">Se a cadeia de caracteres que você deseja exibir contiver um caractere de barra invertida (`\`) ou aspas duplas (`"`), use um *literal de cadeia de caracteres textual* prefixado com o operador de `@`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="8d55d-148">(No C#, o caractere \ tem um significado especial, a menos que você use um literal de cadeia de caracteres textual.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="8d55d-149">Para inserir aspas duplas, use um literal de cadeia de caracteres textual e repita as aspas:</span><span class="sxs-lookup"><span data-stu-id="8d55d-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="8d55d-150">Este é o resultado do uso de ambos os exemplos em uma página:</span><span class="sxs-lookup"><span data-stu-id="8d55d-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="8d55d-152">Observe que o caractere `@` é usado para marcar literais de cadeia de caracteres C# textuais em e para marcar o código em páginas ASP.net.</span><span class="sxs-lookup"><span data-stu-id="8d55d-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="8d55d-153">6. o código diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="8d55d-153">6. Code is case sensitive</span></span>

<span data-ttu-id="8d55d-154">No C#, palavras-chave (como `var`, `true`e `if`) e nomes de variáveis diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8d55d-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="8d55d-155">As linhas de código a seguir criam duas variáveis diferentes, `lastName` e `LastName.`</span><span class="sxs-lookup"><span data-stu-id="8d55d-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="8d55d-156">Se você declarar uma variável como `var lastName = "Smith";` e tentar fazer referência a essa variável em sua página como `@LastName`, obteria o valor `"Jones"` em vez de `"Smith"`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-156">If you declare a variable as `var lastName = "Smith";` and try to reference that variable in your page as `@LastName`, you would get the value `"Jones"` instead of `"Smith"`.</span></span>

> [!NOTE]
> <span data-ttu-id="8d55d-157">Em Visual Basic, as palavras-chave e as variáveis *não* diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8d55d-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="8d55d-158">7. a maior parte da codificação envolve objetos</span><span class="sxs-lookup"><span data-stu-id="8d55d-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="8d55d-159">Um *objeto* representa algo que você pode programar com &#8212; uma página, uma caixa de texto, um arquivo, uma imagem, uma solicitação da Web, uma mensagem de email, um registro de cliente (linha de banco de dados), etc. Os objetos têm propriedades que descrevem suas características e que você pode ler ou &#8212; alterar um objeto de caixa de texto tem uma propriedade de `Text` (entre outros), um objeto de solicitação tem uma propriedade `Url`, uma mensagem de email tem uma propriedade `From` e um objeto Customer tem uma propriedade `FirstName`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="8d55d-160">Os objetos também têm métodos que são os verbos &quot;&quot; podem ser executados.</span><span class="sxs-lookup"><span data-stu-id="8d55d-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="8d55d-161">Os exemplos incluem o método de `Save` de um objeto de arquivo, o método `Rotate` de um objeto de imagem e um método de `Send` do objeto de email.</span><span class="sxs-lookup"><span data-stu-id="8d55d-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="8d55d-162">Com freqüência, você trabalhará com o objeto `Request`, que fornece informações como os valores das caixas de texto (campos de formulário) na página, que tipo de navegador fez a solicitação, a URL da página, a identidade do usuário, etc. O exemplo a seguir mostra como acessar as propriedades do objeto `Request` e como chamar o método `MapPath` do objeto `Request`, que fornece o caminho absoluto da página no servidor:</span><span class="sxs-lookup"><span data-stu-id="8d55d-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="8d55d-163">O resultado exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="8d55d-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="8d55d-165">8. você pode escrever código que toma decisões</span><span class="sxs-lookup"><span data-stu-id="8d55d-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="8d55d-166">Um recurso importante das páginas da Web dinâmicas é que você pode determinar o que fazer com base nas condições.</span><span class="sxs-lookup"><span data-stu-id="8d55d-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="8d55d-167">A maneira mais comum de fazer isso é com a instrução de `if` (e a instrução `else` opcional).</span><span class="sxs-lookup"><span data-stu-id="8d55d-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="8d55d-168">A instrução `if(IsPost)` é uma maneira abreviada de escrever `if(IsPost == true)`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="8d55d-169">Juntamente com `if` instruções, há várias maneiras de testar condições, repetir blocos de código e assim por diante, que são descritos posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="8d55d-170">O resultado exibido em um navegador (depois de clicar em **Enviar**):</span><span class="sxs-lookup"><span data-stu-id="8d55d-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="8d55d-172">Métodos GET e POST de HTTP e a propriedade IsPost</span><span class="sxs-lookup"><span data-stu-id="8d55d-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="8d55d-173">O protocolo usado para páginas da Web (HTTP) dá suporte a um número muito limitado de métodos (verbos) que são usados para fazer solicitações ao servidor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="8d55d-174">Os dois mais comuns são GET, que é usado para ler uma página e POST, que é usado para enviar uma página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="8d55d-175">Em geral, na primeira vez que um usuário solicita uma página, a página é solicitada usando GET.</span><span class="sxs-lookup"><span data-stu-id="8d55d-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="8d55d-176">Se o usuário preencher um formulário e clicar em um botão enviar, o navegador fará uma solicitação POST para o servidor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="8d55d-177">Na programação da Web, geralmente é útil saber se uma página está sendo solicitada como um GET ou como uma POSTAgem para que você saiba como processar a página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="8d55d-178">No Páginas da Web do ASP.NET, você pode usar a propriedade `IsPost` para ver se uma solicitação é GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="8d55d-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="8d55d-179">Se a solicitação for uma POSTAgem, a propriedade `IsPost` retornará true e você poderá fazer coisas como ler os valores das caixas de texto em um formulário.</span><span class="sxs-lookup"><span data-stu-id="8d55d-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="8d55d-180">Muitos exemplos que você verá mostram como processar a página de forma diferente, dependendo do valor de `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="8d55d-181">Um exemplo de código simples</span><span class="sxs-lookup"><span data-stu-id="8d55d-181">A Simple Code Example</span></span>

<span data-ttu-id="8d55d-182">Este procedimento mostra como criar uma página que ilustra as técnicas básicas de programação.</span><span class="sxs-lookup"><span data-stu-id="8d55d-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="8d55d-183">No exemplo, você cria uma página que permite aos usuários inserir dois números e, em seguida, adiciona-os e exibe o resultado.</span><span class="sxs-lookup"><span data-stu-id="8d55d-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="8d55d-184">No editor, crie um novo arquivo e nomeie-o como *AddNumbers. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8d55d-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="8d55d-185">Copie o código e a marcação a seguir para a página, substituindo qualquer coisa que já esteja na página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="8d55d-186">Aqui estão algumas coisas que você deve observar:</span><span class="sxs-lookup"><span data-stu-id="8d55d-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="8d55d-187">O caractere `@` inicia o primeiro bloco de código na página e precede a variável `totalMessage` que é inserida perto da parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="8d55d-188">O bloco na parte superior da página é colocado entre chaves.</span><span class="sxs-lookup"><span data-stu-id="8d55d-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="8d55d-189">No bloco na parte superior, todas as linhas terminam com um ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="8d55d-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="8d55d-190">As variáveis `total`, `num1`, `num2`e `totalMessage` armazenam vários números e uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d55d-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="8d55d-191">O valor da cadeia de caracteres literal atribuído à variável `totalMessage` está entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="8d55d-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="8d55d-192">Como o código diferencia maiúsculas de minúsculas, quando a variável de `totalMessage` é usada perto da parte inferior da página, seu nome deve corresponder à variável na parte superior exata.</span><span class="sxs-lookup"><span data-stu-id="8d55d-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="8d55d-193">A expressão `num1.AsInt() + num2.AsInt()` mostra como trabalhar com objetos e métodos.</span><span class="sxs-lookup"><span data-stu-id="8d55d-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="8d55d-194">O método `AsInt` em cada variável converte a cadeia de caracteres inserida por um usuário em um número (um inteiro) para que você possa executar aritmética nela.</span><span class="sxs-lookup"><span data-stu-id="8d55d-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="8d55d-195">A marca de `<form>` inclui um atributo de `method="post"`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="8d55d-196">Isso especifica que quando o usuário clicar em **Adicionar**, a página será enviada ao servidor usando o método http post.</span><span class="sxs-lookup"><span data-stu-id="8d55d-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="8d55d-197">Quando a página é enviada, o teste de `if(IsPost)` é avaliado como true e o código condicional é executado, exibindo o resultado da adição dos números.</span><span class="sxs-lookup"><span data-stu-id="8d55d-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="8d55d-198">Salve a página e execute-a em um navegador.</span><span class="sxs-lookup"><span data-stu-id="8d55d-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="8d55d-199">(Verifique se a página está selecionada no espaço de trabalho **arquivos** antes de executá-la.) Insira dois números inteiros e, em seguida, clique no botão **Adicionar** .</span><span class="sxs-lookup"><span data-stu-id="8d55d-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="8d55d-201">Conceitos básicos de programação</span><span class="sxs-lookup"><span data-stu-id="8d55d-201">Basic Programming Concepts</span></span>

<span data-ttu-id="8d55d-202">Este artigo fornece uma visão geral da programação da Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8d55d-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="8d55d-203">Não é uma análise exaustiva, apenas um tour rápido pelos conceitos de programação que você usará com mais frequência.</span><span class="sxs-lookup"><span data-stu-id="8d55d-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="8d55d-204">Mesmo assim, ele abrange quase tudo o que você precisará para começar a usar Páginas da Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8d55d-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="8d55d-205">Mas primeiro, uma pequena experiência técnica.</span><span class="sxs-lookup"><span data-stu-id="8d55d-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="8d55d-206">A sintaxe do Razor, o código do servidor e o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8d55d-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="8d55d-207">Sintaxe Razor é uma sintaxe de programação simples para inserir código baseado em servidor em uma página da Web.</span><span class="sxs-lookup"><span data-stu-id="8d55d-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="8d55d-208">Em uma página da Web que usa o sintaxe Razor, há dois tipos de conteúdo: conteúdo do cliente e código do servidor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="8d55d-209">O conteúdo do cliente é o que você está acostumado a usar em páginas da Web: marcação HTML (elementos), informações de estilo como CSS, talvez algum script de cliente como JavaScript e texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="8d55d-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="8d55d-210">Sintaxe Razor permite adicionar código de servidor a esse conteúdo de cliente.</span><span class="sxs-lookup"><span data-stu-id="8d55d-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="8d55d-211">Se houver código de servidor na página, o servidor executará esse código primeiro, antes de enviar a página para o navegador.</span><span class="sxs-lookup"><span data-stu-id="8d55d-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="8d55d-212">Ao executar no servidor, o código pode executar tarefas que podem ser muito mais complexas de usar o conteúdo do cliente, como acessar bancos de dados baseados em servidor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="8d55d-213">O mais importante é que o código do servidor pode &#8212; criar dinamicamente o conteúdo do cliente, ele pode gerar marcação HTML ou outro conteúdo imediatamente e, em seguida, enviá-lo ao navegador junto com qualquer HTML estático que a página possa conter.</span><span class="sxs-lookup"><span data-stu-id="8d55d-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="8d55d-214">Da perspectiva do navegador, o conteúdo do cliente gerado pelo código do servidor não é diferente de qualquer outro conteúdo de cliente.</span><span class="sxs-lookup"><span data-stu-id="8d55d-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="8d55d-215">Como você já viu, o código do servidor necessário é bem simples.</span><span class="sxs-lookup"><span data-stu-id="8d55d-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="8d55d-216">ASP.NET páginas da Web que incluem o sintaxe Razor ter uma extensão de arquivo especial ( *. cshtml* ou *. vbhtml*).</span><span class="sxs-lookup"><span data-stu-id="8d55d-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="8d55d-217">O servidor reconhece essas extensões, executa o código marcado com sintaxe Razor e, em seguida, envia a página para o navegador.</span><span class="sxs-lookup"><span data-stu-id="8d55d-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="8d55d-218">Onde o ASP.NET se encaixa?</span><span class="sxs-lookup"><span data-stu-id="8d55d-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="8d55d-219">O sintaxe Razor se baseia em uma tecnologia da Microsoft chamada ASP.NET, que por sua vez é baseado na estrutura de Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="8d55d-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="8d55d-220">A estrutura The.NET é uma estrutura de programação grande e abrangente da Microsoft para o desenvolvimento de praticamente qualquer tipo de aplicativo de computador.</span><span class="sxs-lookup"><span data-stu-id="8d55d-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="8d55d-221">ASP.NET é a parte da .NET Framework projetada especificamente para criar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="8d55d-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="8d55d-222">Os desenvolvedores usaram o ASP.NET para criar muitos dos maiores e mais grandes sites de tráfego do mundo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="8d55d-223">(Sempre que você vir a extensão de nome de arquivo *. aspx* como parte da URL em um site, saberá que o site foi escrito usando ASP.net.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="8d55d-224">O sintaxe Razor dá a você toda a potência do ASP.NET, mas usando uma sintaxe simplificada que é mais fácil de aprender se você for um principiante e isso o tornará mais produtivo se você for um especialista.</span><span class="sxs-lookup"><span data-stu-id="8d55d-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="8d55d-225">Embora essa sintaxe seja simples de usar, sua relação de família com ASP.NET e a .NET Framework significa que, à medida que seus sites se tornam mais sofisticados, você tem o poder das estruturas maiores disponíveis para você.</span><span class="sxs-lookup"><span data-stu-id="8d55d-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="8d55d-227">**Classes e instâncias**</span><span class="sxs-lookup"><span data-stu-id="8d55d-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="8d55d-228">O código do servidor ASP.NET usa objetos que, por sua vez, se baseiam na ideia de classes.</span><span class="sxs-lookup"><span data-stu-id="8d55d-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="8d55d-229">A classe é a definição ou o modelo de um objeto.</span><span class="sxs-lookup"><span data-stu-id="8d55d-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="8d55d-230">Por exemplo, um aplicativo pode conter uma classe `Customer` que define as propriedades e os métodos de que qualquer objeto de cliente precisa.</span><span class="sxs-lookup"><span data-stu-id="8d55d-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="8d55d-231">Quando o aplicativo precisa trabalhar com informações reais do cliente, ele cria uma instância de (ou *instancia*) um objeto de cliente.</span><span class="sxs-lookup"><span data-stu-id="8d55d-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="8d55d-232">Cada cliente individual é uma instância separada da classe `Customer`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="8d55d-233">Cada instância dá suporte às mesmas propriedades e métodos, mas os valores de propriedade para cada instância são normalmente diferentes, pois cada objeto de cliente é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="8d55d-234">Em um objeto Customer, a propriedade `LastName` pode ser "Smith"; em outro objeto de cliente, a propriedade `LastName` pode ser "Jones".</span><span class="sxs-lookup"><span data-stu-id="8d55d-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="8d55d-235">Da mesma forma, qualquer página da Web individual em seu site é um objeto `Page` que é uma instância da classe `Page`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="8d55d-236">Um botão na página é um objeto `Button` que é uma instância da classe `Button` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="8d55d-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="8d55d-237">Cada instância tem suas próprias características, mas todas elas se baseiam no que é especificado na definição de classe do objeto.</span><span class="sxs-lookup"><span data-stu-id="8d55d-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="8d55d-238">Sintaxe básica</span><span class="sxs-lookup"><span data-stu-id="8d55d-238">Basic Syntax</span></span>

<span data-ttu-id="8d55d-239">Anteriormente, você viu um exemplo básico de como criar uma página de Páginas da Web do ASP.NET e como você pode adicionar código de servidor à marcação HTML.</span><span class="sxs-lookup"><span data-stu-id="8d55d-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="8d55d-240">Aqui, você aprenderá as noções básicas de como escrever código de servidor &#8212; ASP.NET usando o sintaxe Razor ou seja, as regras de linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="8d55d-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="8d55d-241">Se você tiver experiência com programação (especialmente se tiver usado C, C++, C#, Visual Basic ou JavaScript), grande parte do que você lê aqui será familiar.</span><span class="sxs-lookup"><span data-stu-id="8d55d-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="8d55d-242">Você provavelmente precisará se familiarizar apenas com o modo como o código do servidor é adicionado à marcação em arquivos *. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="8d55d-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="8d55d-243">Combinando texto, marcação e código em blocos de código</span><span class="sxs-lookup"><span data-stu-id="8d55d-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="8d55d-244">Em blocos de código de servidor, muitas vezes você deseja produzir texto ou marcação (ou ambos) para a página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="8d55d-245">Se um bloco de código de servidor contiver texto que não seja código e que, em vez disso, deve ser renderizado como está, ASP.NET precisará ser capaz de distinguir esse texto do código.</span><span class="sxs-lookup"><span data-stu-id="8d55d-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="8d55d-246">Há várias maneiras de fazer isso.</span><span class="sxs-lookup"><span data-stu-id="8d55d-246">There are several ways to do this.</span></span>

- <span data-ttu-id="8d55d-247">Coloque o texto em um elemento HTML como `<p></p>` ou `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="8d55d-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="8d55d-248">O elemento HTML pode incluir texto, elementos HTML adicionais e expressões de código de servidor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="8d55d-249">Quando ASP.NET vê a marca HTML de abertura (por exemplo, `<p>`), ela processa tudo, incluindo o elemento e seu conteúdo como se encontra no navegador, resolvendo as expressões de código do servidor como ele vai.</span><span class="sxs-lookup"><span data-stu-id="8d55d-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="8d55d-250">Use o operador `@:` ou o elemento `<text>`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="8d55d-251">O `@:` gera uma única linha de conteúdo que contém texto sem formatação ou marcas HTML não correspondentes; o elemento `<text>` inclui várias linhas na saída.</span><span class="sxs-lookup"><span data-stu-id="8d55d-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="8d55d-252">Essas opções são úteis quando você não deseja renderizar um elemento HTML como parte da saída.</span><span class="sxs-lookup"><span data-stu-id="8d55d-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="8d55d-253">Se você quiser gerar várias linhas de texto ou marcas HTML sem correspondência, você pode preceder cada linha com `@:`, ou pode colocar a linha em um elemento `<text>`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="8d55d-254">Assim como o operador de `@:`, as marcas de`<text>` são usadas pelo ASP.NET para identificar o conteúdo de texto e nunca são renderizadas na saída da página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="8d55d-255">O primeiro exemplo repete o exemplo anterior, mas usa um único par de marcas `<text>` para colocar o texto a ser renderizado.</span><span class="sxs-lookup"><span data-stu-id="8d55d-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="8d55d-256">No segundo exemplo, as marcas `<text>` e `</text>` incluem três linhas, todas com texto não contido e marcas HTML não correspondentes (`<br />`), juntamente com o código do servidor e as marcas HTML correspondentes.</span><span class="sxs-lookup"><span data-stu-id="8d55d-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="8d55d-257">Novamente, você também pode preceder cada linha individualmente com o operador de `@:`; de qualquer forma funciona.</span><span class="sxs-lookup"><span data-stu-id="8d55d-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d55d-258">Quando você faz a saída de texto conforme mostrado &#8212; nesta seção usando um elemento HTML, o operador `@:` ou o elemento &#8212; `<text>` ASP.net não codifica a saída em HTML.</span><span class="sxs-lookup"><span data-stu-id="8d55d-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="8d55d-259">(Como observado anteriormente, o ASP.NET codifica a saída de expressões de código do servidor e os blocos de código do servidor que são precedidos por `@`, exceto nos casos especiais indicados nesta seção.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="8d55d-260">Espaço em branco</span><span class="sxs-lookup"><span data-stu-id="8d55d-260">Whitespace</span></span>

<span data-ttu-id="8d55d-261">Espaços extras em uma instrução (e fora de um literal de cadeia de caracteres) não afetam a instrução:</span><span class="sxs-lookup"><span data-stu-id="8d55d-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="8d55d-262">Uma quebra de linha em uma instrução não tem efeito sobre a instrução e você pode encapsular instruções para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="8d55d-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="8d55d-263">As seguintes instruções são iguais:</span><span class="sxs-lookup"><span data-stu-id="8d55d-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="8d55d-264">No entanto, não é possível encapsular uma linha no meio de um literal de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d55d-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="8d55d-265">O exemplo a seguir não funciona:</span><span class="sxs-lookup"><span data-stu-id="8d55d-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="8d55d-266">Para combinar uma cadeia de caracteres longa que envolve várias linhas como o código acima, há duas opções.</span><span class="sxs-lookup"><span data-stu-id="8d55d-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="8d55d-267">Você pode usar o operador de concatenação (`+`), que será exibido posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="8d55d-268">Você também pode usar o caractere `@` para criar um literal de cadeia de caracteres textual, como visto anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="8d55d-269">Você pode quebrar literais de cadeia de caracteres idênticas entre as linhas:</span><span class="sxs-lookup"><span data-stu-id="8d55d-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="8d55d-270">Comentários de código (e marcação)</span><span class="sxs-lookup"><span data-stu-id="8d55d-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="8d55d-271">Os comentários permitem que você deixe anotações para si mesmo ou para outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="8d55d-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="8d55d-272">Eles também permitem que você desabilite (*comente*) uma seção de código ou marcação que você não deseja executar, mas deseja manter em sua página por enquanto.</span><span class="sxs-lookup"><span data-stu-id="8d55d-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="8d55d-273">Há uma sintaxe de comentário diferente para o código do Razor e para marcação HTML.</span><span class="sxs-lookup"><span data-stu-id="8d55d-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="8d55d-274">Assim como acontece com todo o código do Razor, os comentários do Razor são processados (e, em seguida, removidos) no servidor antes que a página seja enviada para o navegador.</span><span class="sxs-lookup"><span data-stu-id="8d55d-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="8d55d-275">Portanto, a sintaxe de comentários do Razor permite que você coloque comentários no código (ou até mesmo na marcação) que você pode ver ao editar o arquivo, mas que os usuários não veem, mesmo na origem da página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="8d55d-276">Para comentários do ASP.NET Razor, você inicia o comentário com `@*` e o termina com `*@`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="8d55d-277">O comentário pode estar em uma linha ou em várias linhas:</span><span class="sxs-lookup"><span data-stu-id="8d55d-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="8d55d-278">Este é um comentário dentro de um bloco de código:</span><span class="sxs-lookup"><span data-stu-id="8d55d-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="8d55d-279">Aqui está o mesmo bloco de código, com a linha de código comentada para que ele não seja executado:</span><span class="sxs-lookup"><span data-stu-id="8d55d-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="8d55d-280">Dentro de um bloco de código, como uma alternativa ao uso da sintaxe de comentário do Razor, você pode usar a sintaxe de comentários da linguagem de programação que C#você está usando, como:</span><span class="sxs-lookup"><span data-stu-id="8d55d-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="8d55d-281">No C#, os comentários de linha única são precedidos pelo `//` caracteres e os comentários de várias linhas começam com `/*` e terminam com `*/`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="8d55d-282">(Assim como os comentários do C# Razor, os comentários não são renderizados para o navegador.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="8d55d-283">Para marcação, como você provavelmente sabe, você pode criar um comentário HTML:</span><span class="sxs-lookup"><span data-stu-id="8d55d-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="8d55d-284">Os comentários HTML começam com `<!--` caracteres e terminam com `-->`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="8d55d-285">Você pode usar comentários HTML para colocar não apenas texto, mas também qualquer marcação HTML que talvez você queira manter na página, mas não quer renderizar.</span><span class="sxs-lookup"><span data-stu-id="8d55d-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="8d55d-286">Este comentário HTML ocultará todo o conteúdo das marcas e o texto que eles contêm:</span><span class="sxs-lookup"><span data-stu-id="8d55d-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="8d55d-287">Ao contrário dos comentários do Razor, os comentários HTML *são* renderizados para a página e o usuário pode vê-los exibindo a fonte da página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="8d55d-288">O Razor tem limitações em blocos aninhados do C#.</span><span class="sxs-lookup"><span data-stu-id="8d55d-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="8d55d-289">Para obter mais informações [, C# consulte variáveis nomeadas e blocos aninhados geram código quebrado](http://aspnetwebstack.codeplex.com/workitem/1914)</span><span class="sxs-lookup"><span data-stu-id="8d55d-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="8d55d-290">variáveis</span><span class="sxs-lookup"><span data-stu-id="8d55d-290">Variables</span></span>

<span data-ttu-id="8d55d-291">Uma variável é um objeto nomeado que você usa para armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="8d55d-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="8d55d-292">Você pode nomear variáveis como qualquer coisa, mas o nome deve começar com um caractere alfabético e não pode conter espaços em branco ou caracteres reservados.</span><span class="sxs-lookup"><span data-stu-id="8d55d-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="8d55d-293">Variáveis e tipos de dados</span><span class="sxs-lookup"><span data-stu-id="8d55d-293">Variables and Data Types</span></span>

<span data-ttu-id="8d55d-294">Uma variável pode ter um tipo de dados específico, que indica que tipo de dados é armazenado na variável.</span><span class="sxs-lookup"><span data-stu-id="8d55d-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="8d55d-295">Você pode ter variáveis de cadeia de caracteres que armazenam valores de cadeia de caracteres (como &quot;Olá, mundo&quot;), variáveis de inteiro que armazenam valores de número inteiro (como 3 ou 79) e variáveis de data que armazenam valores de data em uma variedade de formatos (como 4/12/2012 ou 2009 de março).</span><span class="sxs-lookup"><span data-stu-id="8d55d-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="8d55d-296">E há muitos outros tipos de dados que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="8d55d-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="8d55d-297">No entanto, geralmente não é necessário especificar um tipo para uma variável.</span><span class="sxs-lookup"><span data-stu-id="8d55d-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="8d55d-298">Na maioria das vezes, o ASP.NET pode descobrir o tipo com base em como os dados na variável estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="8d55d-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="8d55d-299">(Ocasionalmente, você deve especificar um tipo; você verá exemplos em que isso é verdadeiro.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="8d55d-300">Você declara uma variável usando a palavra-chave `var` (se não quiser especificar um tipo) ou usando o nome do tipo:</span><span class="sxs-lookup"><span data-stu-id="8d55d-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="8d55d-301">O exemplo a seguir mostra alguns usos típicos de variáveis em uma página da Web:</span><span class="sxs-lookup"><span data-stu-id="8d55d-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="8d55d-302">Se você combinar os exemplos anteriores em uma página, verá isso exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="8d55d-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="8d55d-304">Convertendo e testando tipos de dados</span><span class="sxs-lookup"><span data-stu-id="8d55d-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="8d55d-305">Embora ASP.NET normalmente possa determinar um tipo de dados automaticamente, às vezes ele não pode.</span><span class="sxs-lookup"><span data-stu-id="8d55d-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="8d55d-306">Portanto, talvez seja necessário ajudar a ASP.NET com a execução de uma conversão explícita.</span><span class="sxs-lookup"><span data-stu-id="8d55d-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="8d55d-307">Mesmo que você não precise converter tipos, às vezes é útil testar para ver de que tipo de dados você pode estar trabalhando.</span><span class="sxs-lookup"><span data-stu-id="8d55d-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="8d55d-308">O caso mais comum é que você precisa converter uma cadeia de caracteres em outro tipo, como em um inteiro ou data.</span><span class="sxs-lookup"><span data-stu-id="8d55d-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="8d55d-309">O exemplo a seguir mostra um caso típico em que você deve converter uma cadeia de caracteres em um número.</span><span class="sxs-lookup"><span data-stu-id="8d55d-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="8d55d-310">Como regra, a entrada do usuário chega a você como cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d55d-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="8d55d-311">Mesmo que você tenha solicitado aos usuários que insiram um número e, mesmo que eles tenham inserido um dígito, quando a entrada do usuário for enviada e você lê-lo no código, os dados estão no formato de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d55d-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="8d55d-312">Portanto, você deve converter a cadeia de caracteres em um número.</span><span class="sxs-lookup"><span data-stu-id="8d55d-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="8d55d-313">No exemplo, se você tentar executar aritmética nos valores sem convertê-los, os seguintes resultados de erro, porque ASP.NET não pode adicionar duas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="8d55d-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="8d55d-314">*Não é possível converter implicitamente o tipo ' String ' em ' int '.*</span><span class="sxs-lookup"><span data-stu-id="8d55d-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="8d55d-315">Para converter os valores em inteiros, você chama o método `AsInt`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="8d55d-316">Se a conversão for bem-sucedida, você poderá adicionar os números.</span><span class="sxs-lookup"><span data-stu-id="8d55d-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="8d55d-317">A tabela a seguir lista alguns métodos comuns de conversão e teste para variáveis.</span><span class="sxs-lookup"><span data-stu-id="8d55d-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="8d55d-318"><strong>Método</strong></span><span class="sxs-lookup"><span data-stu-id="8d55d-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-319"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="8d55d-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-320"><strong>Exemplo</strong></span><span class="sxs-lookup"><span data-stu-id="8d55d-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-321">Converte uma cadeia de caracteres que representa um número inteiro (como "593") em um número inteiro.</span><span class="sxs-lookup"><span data-stu-id="8d55d-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-322">Converte uma cadeia de caracteres como &quot;true&quot; ou &quot;false&quot; em um tipo Boolean.</span><span class="sxs-lookup"><span data-stu-id="8d55d-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-323">Converte uma cadeia de caracteres que tem um valor decimal como &quot;1,3&quot; ou &quot;7,439&quot; para um número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="8d55d-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-324">Converte uma cadeia de caracteres que tem um valor decimal como &quot;1,3&quot; ou &quot;7,439&quot; em um número decimal.</span><span class="sxs-lookup"><span data-stu-id="8d55d-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="8d55d-325">(Em ASP.NET, um número decimal é mais preciso do que um número de ponto flutuante.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-326">Converte uma cadeia de caracteres que representa um valor de data e hora para o tipo de `DateTime` ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8d55d-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-327">Converte qualquer outro tipo de dados em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d55d-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="8d55d-328">Operadores</span><span class="sxs-lookup"><span data-stu-id="8d55d-328">Operators</span></span>

<span data-ttu-id="8d55d-329">Um operador é uma palavra-chave ou um caractere que informa ASP.NET que tipo de comando executar em uma expressão.</span><span class="sxs-lookup"><span data-stu-id="8d55d-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="8d55d-330">O C# idioma (e o sintaxe Razor que se baseia nele) dá suporte a muitos operadores, mas você só precisa reconhecer alguns para começar.</span><span class="sxs-lookup"><span data-stu-id="8d55d-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="8d55d-331">A tabela a seguir resume os operadores mais comuns.</span><span class="sxs-lookup"><span data-stu-id="8d55d-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="8d55d-332"><strong>Operador</strong></span><span class="sxs-lookup"><span data-stu-id="8d55d-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-333"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="8d55d-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-334"><strong>Exemplos</strong></span><span class="sxs-lookup"><span data-stu-id="8d55d-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="8d55d-335">`+` `-` `*` `/`</span><span class="sxs-lookup"><span data-stu-id="8d55d-335">`+` `-` `*` `/`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-336">Operadores matemáticos usados em expressões numéricas.</span><span class="sxs-lookup"><span data-stu-id="8d55d-336">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-337">Atribuição.</span><span class="sxs-lookup"><span data-stu-id="8d55d-337">Assignment.</span></span> <span data-ttu-id="8d55d-338">Atribui o valor no lado direito de uma instrução ao objeto no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-338">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-339">Igualdade.</span><span class="sxs-lookup"><span data-stu-id="8d55d-339">Equality.</span></span> <span data-ttu-id="8d55d-340">Retorna `true` se os valores forem iguais.</span><span class="sxs-lookup"><span data-stu-id="8d55d-340">Returns `true` if the values are equal.</span></span> <span data-ttu-id="8d55d-341">(Observe a distinção entre o operador de `=` e o operador de `==`.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-341">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-342">Desigualdade.</span><span class="sxs-lookup"><span data-stu-id="8d55d-342">Inequality.</span></span> <span data-ttu-id="8d55d-343">Retorna `true` se os valores não forem iguais.</span><span class="sxs-lookup"><span data-stu-id="8d55d-343">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-344">Menor que, maior que, menor que ou igual a, e maior que ou igual a.</span><span class="sxs-lookup"><span data-stu-id="8d55d-344">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-345">Concatenação, que é usada para unir cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d55d-345">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="8d55d-346">ASP.NET sabe a diferença entre esse operador e o operador de adição com base no tipo de dados da expressão.</span><span class="sxs-lookup"><span data-stu-id="8d55d-346">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="8d55d-347">`+=` `-=`</span><span class="sxs-lookup"><span data-stu-id="8d55d-347">`+=` `-=`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-348">Os operadores de incremento e decremento, que adicionam e subtraim 1 (respectivamente) de uma variável.</span><span class="sxs-lookup"><span data-stu-id="8d55d-348">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-349">Final.</span><span class="sxs-lookup"><span data-stu-id="8d55d-349">Dot.</span></span> <span data-ttu-id="8d55d-350">Usado para distinguir objetos e suas propriedades e métodos.</span><span class="sxs-lookup"><span data-stu-id="8d55d-350">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-351">Parênteses.</span><span class="sxs-lookup"><span data-stu-id="8d55d-351">Parentheses.</span></span> <span data-ttu-id="8d55d-352">Usado para agrupar expressões e para passar parâmetros para métodos.</span><span class="sxs-lookup"><span data-stu-id="8d55d-352">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-353">Colchetes.</span><span class="sxs-lookup"><span data-stu-id="8d55d-353">Brackets.</span></span> <span data-ttu-id="8d55d-354">Usado para acessar valores em matrizes ou coleções.</span><span class="sxs-lookup"><span data-stu-id="8d55d-354">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-355">Válido.</span><span class="sxs-lookup"><span data-stu-id="8d55d-355">Not.</span></span> <span data-ttu-id="8d55d-356">Reverte um valor de `true` para `false` e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="8d55d-356">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="8d55d-357">Normalmente usado como uma maneira abreviada de testar `false` (ou seja, para não `true`).</span><span class="sxs-lookup"><span data-stu-id="8d55d-357">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="8d55d-358">`&&` `||`</span><span class="sxs-lookup"><span data-stu-id="8d55d-358">`&&` `||`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="8d55d-359">AND lógico e OR, que são usados para vincular condições juntas.</span><span class="sxs-lookup"><span data-stu-id="8d55d-359">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="8d55d-360">Trabalhando com caminhos de arquivos e pastas no código</span><span class="sxs-lookup"><span data-stu-id="8d55d-360">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="8d55d-361">Com freqüência, você trabalhará com caminhos de arquivos e pastas em seu código.</span><span class="sxs-lookup"><span data-stu-id="8d55d-361">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="8d55d-362">Aqui está um exemplo de estrutura de pasta física para um site como pode aparecer em seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="8d55d-362">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="8d55d-363">Aqui estão alguns detalhes essenciais sobre URLs e caminhos:</span><span class="sxs-lookup"><span data-stu-id="8d55d-363">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="8d55d-364">Uma URL começa com um nome de domínio (`http://www.example.com`) ou um nome de servidor (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="8d55d-364">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="8d55d-365">Uma URL corresponde a um caminho físico em um computador host.</span><span class="sxs-lookup"><span data-stu-id="8d55d-365">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="8d55d-366">Por exemplo, `http://myserver` pode corresponder à pasta *C:\websites\mywebsite* no servidor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-366">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="8d55d-367">Um caminho virtual é abreviado para representar caminhos no código sem precisar especificar o caminho completo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-367">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="8d55d-368">Ele inclui a parte de uma URL que segue o nome do domínio ou do servidor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-368">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="8d55d-369">Ao usar caminhos virtuais, você pode mover seu código para um domínio ou servidor diferente sem precisar atualizar os caminhos.</span><span class="sxs-lookup"><span data-stu-id="8d55d-369">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="8d55d-370">Aqui está um exemplo para ajudá-lo a entender as diferenças:</span><span class="sxs-lookup"><span data-stu-id="8d55d-370">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="8d55d-371">URL completa</span><span class="sxs-lookup"><span data-stu-id="8d55d-371">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="8d55d-372">Nome do servidor</span><span class="sxs-lookup"><span data-stu-id="8d55d-372">Server name</span></span> | <span data-ttu-id="8d55d-373">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="8d55d-373">*mycompanyserver*</span></span> |
| <span data-ttu-id="8d55d-374">Caminho virtual</span><span class="sxs-lookup"><span data-stu-id="8d55d-374">Virtual path</span></span> | <span data-ttu-id="8d55d-375">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="8d55d-375">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="8d55d-376">Caminho físico</span><span class="sxs-lookup"><span data-stu-id="8d55d-376">Physical path</span></span> | <span data-ttu-id="8d55d-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="8d55d-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="8d55d-378">A raiz virtual é/, assim como a raiz da sua unidade C: é \.</span><span class="sxs-lookup"><span data-stu-id="8d55d-378">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="8d55d-379">(Os caminhos de pastas virtuais sempre usam barras "/".) O caminho virtual de uma pasta não precisa ter o mesmo nome que a pasta física; pode ser um alias.</span><span class="sxs-lookup"><span data-stu-id="8d55d-379">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="8d55d-380">(Em servidores de produção, o caminho virtual raramente corresponde a um caminho físico exato.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-380">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="8d55d-381">Quando você trabalha com arquivos e pastas no código, às vezes você precisa referenciar o caminho físico e, às vezes, um caminho virtual, dependendo de quais objetos você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="8d55d-381">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="8d55d-382">O ASP.NET fornece essas ferramentas para trabalhar com caminhos de arquivos e pastas no código: o método `Server.MapPath` e o operador `~` e o método `Href`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-382">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="8d55d-383">Convertendo caminhos virtuais em físicos: o método Server. MapPath</span><span class="sxs-lookup"><span data-stu-id="8d55d-383">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="8d55d-384">O método `Server.MapPath` converte um caminho virtual (como */Default.cshtml*) em um caminho físico absoluto (como *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="8d55d-384">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="8d55d-385">Você usa esse método sempre que precisar de um caminho físico completo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-385">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="8d55d-386">Um exemplo típico é quando você está lendo ou gravando um arquivo de texto ou de imagem no servidor Web.</span><span class="sxs-lookup"><span data-stu-id="8d55d-386">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="8d55d-387">Normalmente, você não sabe o caminho físico absoluto do seu site no servidor de um site de hospedagem, portanto, esse método pode converter o caminho que você conhece — o caminho virtual — para o caminho correspondente no servidor para você.</span><span class="sxs-lookup"><span data-stu-id="8d55d-387">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="8d55d-388">Você passa o caminho virtual para um arquivo ou pasta para o método e retorna o caminho físico:</span><span class="sxs-lookup"><span data-stu-id="8d55d-388">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="8d55d-389">Referenciando a raiz virtual: o operador ~ e o método href</span><span class="sxs-lookup"><span data-stu-id="8d55d-389">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="8d55d-390">Em um arquivo *. cshtml* ou *. vbhtml* , você pode fazer referência ao caminho raiz virtual usando o operador de `~`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-390">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="8d55d-391">Isso é muito útil porque você pode mover páginas em um site e quaisquer links que eles contêm para outras páginas não serão quebrados.</span><span class="sxs-lookup"><span data-stu-id="8d55d-391">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="8d55d-392">Também é útil caso você sempre mova seu site para um local diferente.</span><span class="sxs-lookup"><span data-stu-id="8d55d-392">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="8d55d-393">Estes são alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="8d55d-393">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="8d55d-394">Se o site for `http://myserver/myapp`, aqui está como o ASP.NET tratará esses caminhos quando a página for executada:</span><span class="sxs-lookup"><span data-stu-id="8d55d-394">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="8d55d-395">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="8d55d-395">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="8d55d-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="8d55d-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="8d55d-397">(Você realmente não verá esses caminhos como os valores da variável, mas ASP.NET tratará os caminhos como se fosse isso.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-397">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="8d55d-398">Você pode usar o operador de `~` no código do servidor (como acima) e na marcação, desta forma:</span><span class="sxs-lookup"><span data-stu-id="8d55d-398">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="8d55d-399">Na marcação, você usa o operador `~` para criar caminhos para recursos como arquivos de imagem, outras páginas da Web e arquivos CSS.</span><span class="sxs-lookup"><span data-stu-id="8d55d-399">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="8d55d-400">Quando a página é executada, o ASP.NET examina a página (código e marcação) e resolve todas as referências de `~` para o caminho apropriado.</span><span class="sxs-lookup"><span data-stu-id="8d55d-400">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="8d55d-401">Lógica condicional e loops</span><span class="sxs-lookup"><span data-stu-id="8d55d-401">Conditional Logic and Loops</span></span>

<span data-ttu-id="8d55d-402">O código do servidor ASP.NET permite executar tarefas com base em condições e escrever código que repete instruções um número específico de vezes (ou seja, o código que executa um loop).</span><span class="sxs-lookup"><span data-stu-id="8d55d-402">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="8d55d-403">Condições de teste</span><span class="sxs-lookup"><span data-stu-id="8d55d-403">Testing Conditions</span></span>

<span data-ttu-id="8d55d-404">Para testar uma condição simples, use a instrução `if`, que retorna true ou false com base em um teste que você especificar:</span><span class="sxs-lookup"><span data-stu-id="8d55d-404">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="8d55d-405">A palavra-chave `if` inicia um bloco.</span><span class="sxs-lookup"><span data-stu-id="8d55d-405">The `if` keyword starts a block.</span></span> <span data-ttu-id="8d55d-406">O teste real (condição) está entre parênteses e retorna true ou false.</span><span class="sxs-lookup"><span data-stu-id="8d55d-406">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="8d55d-407">As instruções que são executadas se o teste é true são colocadas entre chaves.</span><span class="sxs-lookup"><span data-stu-id="8d55d-407">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="8d55d-408">Uma instrução `if` pode incluir um bloco `else` que especifica as instruções a serem executadas se a condição for falsa:</span><span class="sxs-lookup"><span data-stu-id="8d55d-408">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="8d55d-409">Você pode adicionar várias condições usando um bloco de `else if`:</span><span class="sxs-lookup"><span data-stu-id="8d55d-409">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="8d55d-410">Neste exemplo, se a primeira condição no bloco If não for verdadeira, a condição de `else if` será verificada.</span><span class="sxs-lookup"><span data-stu-id="8d55d-410">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="8d55d-411">Se essa condição for atendida, as instruções no bloco de `else if` serão executadas.</span><span class="sxs-lookup"><span data-stu-id="8d55d-411">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="8d55d-412">Se nenhuma das condições for atendida, as instruções no bloco de `else` serão executadas.</span><span class="sxs-lookup"><span data-stu-id="8d55d-412">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="8d55d-413">Você pode adicionar qualquer número de outros blocos If e, em seguida, fechar com um bloco de `else` como o &quot;o restante&quot; condição.</span><span class="sxs-lookup"><span data-stu-id="8d55d-413">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="8d55d-414">Para testar um grande número de condições, use um bloco de `switch`:</span><span class="sxs-lookup"><span data-stu-id="8d55d-414">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="8d55d-415">O valor a ser testado está entre parênteses (no exemplo, a variável `weekday`).</span><span class="sxs-lookup"><span data-stu-id="8d55d-415">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="8d55d-416">Cada teste individual usa uma instrução `case` que termina com dois-pontos (:).</span><span class="sxs-lookup"><span data-stu-id="8d55d-416">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="8d55d-417">Se o valor de uma instrução `case` corresponder ao valor de teste, o código nesse bloco de casos será executado.</span><span class="sxs-lookup"><span data-stu-id="8d55d-417">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="8d55d-418">Você fecha cada instrução case com uma instrução `break`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-418">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="8d55d-419">(Se você se esquecer de incluir a quebra em cada bloco de `case`, o código da próxima instrução `case` será executado também.) Um bloco de `switch` geralmente tem uma instrução `default` como o último caso de uma opção de &quot;tudo mais&quot; que é executada se nenhum dos outros casos for verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="8d55d-419">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="8d55d-420">O resultado dos dois últimos blocos condicionais exibidos em um navegador:</span><span class="sxs-lookup"><span data-stu-id="8d55d-420">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="8d55d-422">Código de loop</span><span class="sxs-lookup"><span data-stu-id="8d55d-422">Looping Code</span></span>

<span data-ttu-id="8d55d-423">Muitas vezes, você precisa executar as mesmas instruções repetidamente.</span><span class="sxs-lookup"><span data-stu-id="8d55d-423">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="8d55d-424">Faça isso fazendo um loop.</span><span class="sxs-lookup"><span data-stu-id="8d55d-424">You do this by looping.</span></span> <span data-ttu-id="8d55d-425">Por exemplo, você geralmente executa as mesmas instruções para cada item em uma coleção de dados.</span><span class="sxs-lookup"><span data-stu-id="8d55d-425">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="8d55d-426">Se você souber exatamente quantas vezes deseja executar um loop, você pode usar um loop `for`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-426">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="8d55d-427">Esse tipo de loop é especialmente útil para contar ou contar para baixo:</span><span class="sxs-lookup"><span data-stu-id="8d55d-427">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="8d55d-428">O loop começa com a palavra-chave `for`, seguida por três instruções entre parênteses, cada uma termina com um ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="8d55d-428">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="8d55d-429">Dentro dos parênteses, a primeira instrução (`var i=10;`) cria um contador e inicializa-o como 10.</span><span class="sxs-lookup"><span data-stu-id="8d55d-429">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="8d55d-430">Você não precisa nomear o contador `i` &#8212; você pode usar qualquer variável.</span><span class="sxs-lookup"><span data-stu-id="8d55d-430">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="8d55d-431">Quando o loop de `for` é executado, o contador é incrementado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8d55d-431">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="8d55d-432">A segunda instrução (`i < 21;`) define a condição para o quanto você deseja contar.</span><span class="sxs-lookup"><span data-stu-id="8d55d-432">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="8d55d-433">Nesse caso, você deseja que ele vá para um máximo de 20 (ou seja, continue enquanto o contador for menor que 21).</span><span class="sxs-lookup"><span data-stu-id="8d55d-433">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="8d55d-434">A terceira instrução (`i++`) usa um operador de incremento, que simplesmente especifica que o contador deve ter 1 adicionado a cada vez que o loop é executado.</span><span class="sxs-lookup"><span data-stu-id="8d55d-434">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="8d55d-435">Dentro das chaves está o código que será executado para cada iteração do loop.</span><span class="sxs-lookup"><span data-stu-id="8d55d-435">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="8d55d-436">A marcação cria um novo parágrafo (`<p>` elemento) a cada vez e adiciona uma linha à saída, exibindo o valor de `i` (o contador).</span><span class="sxs-lookup"><span data-stu-id="8d55d-436">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="8d55d-437">Quando você executa essa página, o exemplo cria 11 linhas exibindo a saída, com o texto em cada linha indicando o número do item.</span><span class="sxs-lookup"><span data-stu-id="8d55d-437">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="8d55d-439">Se você estiver trabalhando com uma coleção ou matriz, geralmente usará um loop `foreach`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-439">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="8d55d-440">Uma coleção é um grupo de objetos semelhantes, e o loop de `foreach` permite que você execute uma tarefa em cada item da coleção.</span><span class="sxs-lookup"><span data-stu-id="8d55d-440">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="8d55d-441">Esse tipo de loop é conveniente para coleções, porque, ao contrário de um loop de `for`, você não precisa incrementar o contador ou definir um limite.</span><span class="sxs-lookup"><span data-stu-id="8d55d-441">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="8d55d-442">Em vez disso, o código de loop de `foreach` simplesmente prossegue pela coleção até que seja concluído.</span><span class="sxs-lookup"><span data-stu-id="8d55d-442">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="8d55d-443">Por exemplo, o código a seguir retorna os itens na coleção de `Request.ServerVariables`, que é um objeto que contém informações sobre o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="8d55d-443">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="8d55d-444">Ele usa um loop `foreac` h para exibir o nome de cada item criando um novo elemento `<li>` em uma lista com marcadores HTML.</span><span class="sxs-lookup"><span data-stu-id="8d55d-444">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="8d55d-445">A palavra-chave `foreach` é seguida por parênteses em que você declara uma variável que representa um único item na coleção (no exemplo, `var item`), seguido pela palavra-chave `in`, seguida pela coleção na qual você deseja executar o loop.</span><span class="sxs-lookup"><span data-stu-id="8d55d-445">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="8d55d-446">No corpo do loop de `foreach`, você pode acessar o item atual usando a variável que você declarou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8d55d-446">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="8d55d-448">Para criar um loop de finalidade mais geral, use a instrução `while`:</span><span class="sxs-lookup"><span data-stu-id="8d55d-448">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="8d55d-449">Um loop de `while` começa com a palavra-chave `while`, seguido por parênteses em que você especifica por quanto tempo o loop continua (aqui, desde que `countNum` seja menor que 50) e, em seguida, o bloco seja repetido.</span><span class="sxs-lookup"><span data-stu-id="8d55d-449">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="8d55d-450">Os loops normalmente incrementam (adicionam) ou decrementam (subtraim de) uma variável ou objeto usado para contagem.</span><span class="sxs-lookup"><span data-stu-id="8d55d-450">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="8d55d-451">No exemplo, o operador de `+=` adiciona 1 a `countNum` cada vez que o loop é executado.</span><span class="sxs-lookup"><span data-stu-id="8d55d-451">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="8d55d-452">(Para diminuir uma variável em um loop que conta inativo, você usaria o operador decremento `-=`).</span><span class="sxs-lookup"><span data-stu-id="8d55d-452">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="8d55d-453">Objetos e coleções</span><span class="sxs-lookup"><span data-stu-id="8d55d-453">Objects and Collections</span></span>

<span data-ttu-id="8d55d-454">Quase tudo em um site ASP.NET é um objeto, incluindo a própria página da Web.</span><span class="sxs-lookup"><span data-stu-id="8d55d-454">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="8d55d-455">Esta seção aborda alguns objetos importantes com os quais você trabalhará com frequência em seu código.</span><span class="sxs-lookup"><span data-stu-id="8d55d-455">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="8d55d-456">Objetos de página</span><span class="sxs-lookup"><span data-stu-id="8d55d-456">Page Objects</span></span>

<span data-ttu-id="8d55d-457">O objeto mais básico em ASP.NET é a página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-457">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="8d55d-458">Você pode acessar as propriedades do objeto Page diretamente sem nenhum objeto qualificado.</span><span class="sxs-lookup"><span data-stu-id="8d55d-458">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="8d55d-459">O código a seguir obtém o caminho do arquivo da página, usando o objeto `Request` da página:</span><span class="sxs-lookup"><span data-stu-id="8d55d-459">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="8d55d-460">Para tornar claro que você está fazendo referência a propriedades e métodos no objeto Page atual, você pode, opcionalmente, usar a palavra-chave `this` para representar o objeto Page em seu código.</span><span class="sxs-lookup"><span data-stu-id="8d55d-460">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="8d55d-461">Aqui está o exemplo de código anterior, com `this` adicionado para representar a página:</span><span class="sxs-lookup"><span data-stu-id="8d55d-461">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="8d55d-462">Você pode usar as propriedades do objeto `Page` para obter muitas informações, como:</span><span class="sxs-lookup"><span data-stu-id="8d55d-462">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="8d55d-463">`Request`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-463">`Request`.</span></span> <span data-ttu-id="8d55d-464">Como você já viu, trata-se de uma coleção de informações sobre a solicitação atual, incluindo que tipo de navegador fez a solicitação, a URL da página, a identidade do usuário, etc.</span><span class="sxs-lookup"><span data-stu-id="8d55d-464">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="8d55d-465">`Response`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-465">`Response`.</span></span> <span data-ttu-id="8d55d-466">Esta é uma coleção de informações sobre a resposta (página) que será enviada ao navegador quando o código do servidor terminar a execução.</span><span class="sxs-lookup"><span data-stu-id="8d55d-466">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="8d55d-467">Por exemplo, você pode usar essa propriedade para gravar informações na resposta.</span><span class="sxs-lookup"><span data-stu-id="8d55d-467">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="8d55d-468">Objetos de coleção (matrizes e dicionários)</span><span class="sxs-lookup"><span data-stu-id="8d55d-468">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="8d55d-469">Uma *coleção* é um grupo de objetos do mesmo tipo, como uma coleção de objetos `Customer` de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8d55d-469">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="8d55d-470">ASP.NET contém muitas coleções internas, como a coleção de `Request.Files`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-470">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="8d55d-471">Você geralmente trabalhará com dados em coleções.</span><span class="sxs-lookup"><span data-stu-id="8d55d-471">You'll often work with data in collections.</span></span> <span data-ttu-id="8d55d-472">Dois tipos de coleção comuns são a *matriz* e o *dicionário*.</span><span class="sxs-lookup"><span data-stu-id="8d55d-472">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="8d55d-473">Uma matriz é útil quando você deseja armazenar uma coleção de itens semelhantes, mas não quer criar uma variável separada para conter cada item:</span><span class="sxs-lookup"><span data-stu-id="8d55d-473">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="8d55d-474">Com matrizes, você declara um tipo de dados específico, como `string`, `int`ou `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-474">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="8d55d-475">Para indicar que a variável pode conter uma matriz, você adiciona colchetes à declaração (como `string[]` ou `int[]`).</span><span class="sxs-lookup"><span data-stu-id="8d55d-475">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="8d55d-476">Você pode acessar itens em uma matriz usando sua posição (índice) ou usando a instrução `foreach`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-476">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="8d55d-477">Os índices de matriz são baseados &#8212; em zero ou seja, o primeiro item está na posição 0, o segundo item está na posição 1 e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="8d55d-477">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="8d55d-478">Você pode determinar o número de itens em uma matriz obtendo sua propriedade `Length`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-478">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="8d55d-479">Para obter a posição de um item específico na matriz (para pesquisar a matriz), use o método `Array.IndexOf`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-479">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="8d55d-480">Você também pode fazer coisas como reverter o conteúdo de uma matriz (o método `Array.Reverse`) ou classificar o conteúdo (o método `Array.Sort`).</span><span class="sxs-lookup"><span data-stu-id="8d55d-480">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="8d55d-481">A saída do código da matriz de cadeia de caracteres exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="8d55d-481">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="8d55d-483">Um dicionário é uma coleção de pares de chave/valor, em que você fornece a chave (ou nome) para definir ou recuperar o valor correspondente:</span><span class="sxs-lookup"><span data-stu-id="8d55d-483">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="8d55d-484">Para criar um dicionário, use a palavra-chave `new` para indicar que você está criando um novo objeto Dictionary.</span><span class="sxs-lookup"><span data-stu-id="8d55d-484">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="8d55d-485">Você pode atribuir um dicionário a uma variável usando a palavra-chave `var`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-485">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="8d55d-486">Você indica os tipos de dados dos itens no dicionário usando colchetes angulares (`< >`).</span><span class="sxs-lookup"><span data-stu-id="8d55d-486">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="8d55d-487">No final da declaração, você deve adicionar um par de parênteses, porque esse é, na verdade, um método que cria um novo dicionário.</span><span class="sxs-lookup"><span data-stu-id="8d55d-487">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="8d55d-488">Para adicionar itens ao dicionário, você pode chamar o método `Add` da variável Dictionary (`myScores` nesse caso) e, em seguida, especificar uma chave e um valor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-488">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="8d55d-489">Como alternativa, você pode usar colchetes para indicar a chave e fazer uma atribuição simples, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d55d-489">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="8d55d-490">Para obter um valor do dicionário, especifique a chave entre colchetes:</span><span class="sxs-lookup"><span data-stu-id="8d55d-490">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="8d55d-491">Chamando métodos com parâmetros</span><span class="sxs-lookup"><span data-stu-id="8d55d-491">Calling Methods with Parameters</span></span>

<span data-ttu-id="8d55d-492">Conforme você lê anteriormente neste artigo, os objetos com os quais você programa pode ter métodos.</span><span class="sxs-lookup"><span data-stu-id="8d55d-492">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="8d55d-493">Por exemplo, um objeto `Database` pode ter um método `Database.Connect`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-493">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="8d55d-494">Muitos métodos também têm um ou mais parâmetros.</span><span class="sxs-lookup"><span data-stu-id="8d55d-494">Many methods also have one or more parameters.</span></span> <span data-ttu-id="8d55d-495">Um *parâmetro* é um valor que você passa para um método para permitir que o método conclua sua tarefa.</span><span class="sxs-lookup"><span data-stu-id="8d55d-495">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="8d55d-496">Por exemplo, examine uma declaração para o método `Request.MapPath`, que usa três parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8d55d-496">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="8d55d-497">(A linha foi encapsulada para torná-la mais legível.</span><span class="sxs-lookup"><span data-stu-id="8d55d-497">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="8d55d-498">Lembre-se de que você pode colocar quebras de linha quase qualquer lugar, exceto as cadeias de caracteres entre aspas.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-498">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="8d55d-499">Esse método retorna o caminho físico no servidor que corresponde a um caminho virtual especificado.</span><span class="sxs-lookup"><span data-stu-id="8d55d-499">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="8d55d-500">Os três parâmetros para o método são `virtualPath`, `baseVirtualDir`e `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-500">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="8d55d-501">(Observe que na declaração, os parâmetros são listados com os tipos de dados dos dados que eles aceitarão.) Ao chamar esse método, você deve fornecer valores para todos os três parâmetros.</span><span class="sxs-lookup"><span data-stu-id="8d55d-501">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="8d55d-502">O sintaxe Razor fornece duas opções para passar parâmetros para um método: *parâmetros posicionais* e *parâmetros nomeados*.</span><span class="sxs-lookup"><span data-stu-id="8d55d-502">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="8d55d-503">Para chamar um método usando parâmetros posicionais, você passa os parâmetros em uma ordem estrita que é especificada na declaração do método.</span><span class="sxs-lookup"><span data-stu-id="8d55d-503">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="8d55d-504">(Normalmente, você sabe esse pedido lendo a documentação do método.) Você deve seguir a ordem e não pode ignorar nenhum dos parâmetros &#8212; , se necessário, você passa uma cadeia de caracteres vazia (`""`) ou `null` para um parâmetro posicional para o qual você não tenha um valor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-504">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="8d55d-505">O exemplo a seguir pressupõe que você tenha uma pasta chamada *scripts* em seu site.</span><span class="sxs-lookup"><span data-stu-id="8d55d-505">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="8d55d-506">O código chama o método `Request.MapPath` e passa valores para os três parâmetros na ordem correta.</span><span class="sxs-lookup"><span data-stu-id="8d55d-506">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="8d55d-507">Em seguida, ele exibe o caminho mapeado resultante.</span><span class="sxs-lookup"><span data-stu-id="8d55d-507">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="8d55d-508">Quando um método tem muitos parâmetros, você pode manter seu código mais legível usando parâmetros nomeados.</span><span class="sxs-lookup"><span data-stu-id="8d55d-508">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="8d55d-509">Para chamar um método usando parâmetros nomeados, especifique o nome do parâmetro seguido por dois-pontos (:) e, em seguida, o valor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-509">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="8d55d-510">A vantagem dos parâmetros nomeados é que você pode passá-los em qualquer ordem desejada.</span><span class="sxs-lookup"><span data-stu-id="8d55d-510">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="8d55d-511">(Uma desvantagem é que a chamada de método não é compactada.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-511">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="8d55d-512">O exemplo a seguir chama o mesmo método mostrado acima, mas usa parâmetros nomeados para fornecer os valores:</span><span class="sxs-lookup"><span data-stu-id="8d55d-512">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="8d55d-513">Como você pode ver, os parâmetros são passados em uma ordem diferente.</span><span class="sxs-lookup"><span data-stu-id="8d55d-513">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="8d55d-514">No entanto, se você executar o exemplo anterior e este exemplo, eles retornarão o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="8d55d-514">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="8d55d-515">Tratando erros</span><span class="sxs-lookup"><span data-stu-id="8d55d-515">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="8d55d-516">Instruções Try-Catch</span><span class="sxs-lookup"><span data-stu-id="8d55d-516">Try-Catch Statements</span></span>

<span data-ttu-id="8d55d-517">Muitas vezes, você terá instruções em seu código que podem falhar por motivos fora do seu controle.</span><span class="sxs-lookup"><span data-stu-id="8d55d-517">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="8d55d-518">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8d55d-518">For example:</span></span>

- <span data-ttu-id="8d55d-519">Se o seu código tentar criar ou acessar um arquivo, todos os tipos de erros poderão ocorrer.</span><span class="sxs-lookup"><span data-stu-id="8d55d-519">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="8d55d-520">O arquivo desejado talvez não exista, ele pode estar bloqueado, o código pode não ter permissões e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="8d55d-520">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="8d55d-521">Da mesma forma, se o seu código tentar atualizar os registros em um banco de dados, poderá haver problemas de permissões, a conexão com o banco de dados pode ser descartada, o que pode ser salvo, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="8d55d-521">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="8d55d-522">Em termos de programação, essas situações são chamadas de *exceções*.</span><span class="sxs-lookup"><span data-stu-id="8d55d-522">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="8d55d-523">Se o código encontrar uma exceção, ele gerará (gera) uma mensagem de erro que é, no melhor, irritante para os usuários:</span><span class="sxs-lookup"><span data-stu-id="8d55d-523">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="8d55d-525">Em situações em que o código pode encontrar exceções e, para evitar mensagens de erro desse tipo, você pode usar instruções de `try/catch`.</span><span class="sxs-lookup"><span data-stu-id="8d55d-525">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="8d55d-526">Na instrução `try`, você executa o código que está verificando.</span><span class="sxs-lookup"><span data-stu-id="8d55d-526">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="8d55d-527">Em uma ou mais instruções `catch`, você pode procurar erros específicos (tipos específicos de exceções) que podem ter ocorrido.</span><span class="sxs-lookup"><span data-stu-id="8d55d-527">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="8d55d-528">Você pode incluir tantas `catch` instruções quantas forem necessárias para procurar erros que você está prevendo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-528">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="8d55d-529">Recomendamos que você evite usar o método `Response.Redirect` em instruções `try/catch`, pois isso pode causar uma exceção em sua página.</span><span class="sxs-lookup"><span data-stu-id="8d55d-529">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="8d55d-530">O exemplo a seguir mostra uma página que cria um arquivo de texto na primeira solicitação e, em seguida, exibe um botão que permite ao usuário abrir o arquivo.</span><span class="sxs-lookup"><span data-stu-id="8d55d-530">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="8d55d-531">O exemplo deliberadamente usa um nome de arquivo inadequado para que cause uma exceção.</span><span class="sxs-lookup"><span data-stu-id="8d55d-531">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="8d55d-532">O código inclui `catch` instruções para duas possíveis exceções: `FileNotFoundException`, que ocorrerá se o nome do arquivo for insatisfatório, e `DirectoryNotFoundException`, que ocorrerá se ASP.NET não conseguir localizar a pasta.</span><span class="sxs-lookup"><span data-stu-id="8d55d-532">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="8d55d-533">(Você pode remover o comentário de uma instrução no exemplo para ver como ela é executada quando tudo funciona corretamente.)</span><span class="sxs-lookup"><span data-stu-id="8d55d-533">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="8d55d-534">Se o código não tratar a exceção, você verá uma página de erro como a captura de tela anterior.</span><span class="sxs-lookup"><span data-stu-id="8d55d-534">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="8d55d-535">No entanto, a seção `try/catch` ajuda a impedir que o usuário veja esses tipos de erros.</span><span class="sxs-lookup"><span data-stu-id="8d55d-535">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="8d55d-536">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8d55d-536">Additional Resources</span></span>

<span data-ttu-id="8d55d-537">**Programando com Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="8d55d-537">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="8d55d-538">Apêndice: linguagem e sintaxe de Visual Basic</span><span class="sxs-lookup"><span data-stu-id="8d55d-538">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="8d55d-539">**Documentação de Referência**</span><span class="sxs-lookup"><span data-stu-id="8d55d-539">**Reference Documentation**</span></span>

[<span data-ttu-id="8d55d-540">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8d55d-540">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="8d55d-541">C#Idioma</span><span class="sxs-lookup"><span data-stu-id="8d55d-541">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
