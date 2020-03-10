---
uid: whitepapers/request-validation
title: Validação de solicitação-prevenção de ataques de script | Microsoft Docs
author: rick-anderson
description: Este documento descreve o recurso de validação de solicitação do ASP.NET, em que, por padrão, o aplicativo é impedido de processar o envio de conteúdo HTML não codificado...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640843"
---
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="69468-103">Solicitação de validação – Impedir ataques de Script</span><span class="sxs-lookup"><span data-stu-id="69468-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="69468-104">Este documento descreve o recurso de validação de solicitação do ASP.NET, em que, por padrão, o aplicativo é impedido de processar o conteúdo HTML não codificado enviado ao servidor.</span><span class="sxs-lookup"><span data-stu-id="69468-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="69468-105">Esse recurso de validação de solicitação pode ser desabilitado quando o aplicativo tiver sido projetado para processar dados HTML com segurança.</span><span class="sxs-lookup"><span data-stu-id="69468-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="69468-106">Aplica-se a ASP.NET 1,1 e ASP.NET 2,0.</span><span class="sxs-lookup"><span data-stu-id="69468-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="69468-107">A validação de solicitação, um recurso do ASP.NET oferecido desde a versão 1.1, impede que o servidor aceite conteúdo sem HTML codificado.</span><span class="sxs-lookup"><span data-stu-id="69468-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="69468-108">Esse recurso foi criado para evitar alguns ataques de injeção de script, em que o código de script ou HTML do cliente pode ser enviado inadvertidamente para um servidor, armazenado e, em seguida, apresentado a outros usuários.</span><span class="sxs-lookup"><span data-stu-id="69468-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="69468-109">Ainda recomendamos que você valide todos os dados de entrada e os codifique com HTML quando for apropriado.</span><span class="sxs-lookup"><span data-stu-id="69468-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="69468-110">Por exemplo, você cria uma página da Web que solicita o endereço de email de um usuário e, em seguida, armazena esse endereço de email em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="69468-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="69468-111">Se o usuário inserir &lt;SCRIPT&gt;alerta ("Olá do script")&lt;/SCRIPT&gt; em vez de um endereço de email válido, quando esses dados forem apresentados, esse script poderá ser executado se o conteúdo não tiver sido codificado corretamente.</span><span class="sxs-lookup"><span data-stu-id="69468-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="69468-112">O recurso de validação de solicitação do ASP.NET impede que isso aconteça.</span><span class="sxs-lookup"><span data-stu-id="69468-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="69468-113">Por que esse recurso é útil</span><span class="sxs-lookup"><span data-stu-id="69468-113">Why this feature is useful</span></span>

<span data-ttu-id="69468-114">Muitos sites não sabem que estão abertos para ataques de injeção de script simples.</span><span class="sxs-lookup"><span data-stu-id="69468-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="69468-115">Se a finalidade desses ataques é Deface o site exibindo HTML ou potencialmente executar script de cliente para redirecionar o usuário para o site de um hacker, os ataques de injeção de script são um problema que os desenvolvedores da Web devem enfrentar.</span><span class="sxs-lookup"><span data-stu-id="69468-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="69468-116">Ataques de injeção de script são uma preocupação de todos os desenvolvedores da Web, estejam eles usando ASP.NET, ASP ou outras tecnologias de desenvolvimento para a Web.</span><span class="sxs-lookup"><span data-stu-id="69468-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="69468-117">O recurso de validação de solicitação do ASP.NET impede proativamente esses ataques, não permitindo que o conteúdo HTML não codificado seja processado pelo servidor, a menos que o desenvolvedor decida permitir esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="69468-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="69468-118">O que esperar: página de erro</span><span class="sxs-lookup"><span data-stu-id="69468-118">What to expect: Error Page</span></span>

<span data-ttu-id="69468-119">A captura de tela abaixo mostra alguns exemplos de código ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="69468-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="69468-120">A execução desse código resulta em uma página simples que permite que você insira algum texto na TextBox, clique no botão e exiba o texto no controle rótulo:</span><span class="sxs-lookup"><span data-stu-id="69468-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="69468-121">No entanto, era o JavaScript, como `<script>alert("hello!")</script>` a ser inserido e enviado, obtemos uma exceção:</span><span class="sxs-lookup"><span data-stu-id="69468-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="69468-122">A mensagem de erro informa que um valor "possivelmente perigoso de solicitação. Form foi detectado" e fornece mais detalhes na descrição para exatamente o que ocorreu e como alterar o comportamento.</span><span class="sxs-lookup"><span data-stu-id="69468-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="69468-123">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="69468-123">For example:</span></span>

<span data-ttu-id="69468-124">A validação da solicitação detectou um valor de entrada de cliente potencialmente perigoso e o processamento da solicitação foi anulado.</span><span class="sxs-lookup"><span data-stu-id="69468-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="69468-125">Esse valor pode indicar uma tentativa de comprometer a segurança do seu aplicativo, como um ataque de script entre sites.</span><span class="sxs-lookup"><span data-stu-id="69468-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="69468-126">Você pode desabilitar a validação de solicitação definindo `validateRequest=false` na diretiva de página ou na seção de configuração.</span><span class="sxs-lookup"><span data-stu-id="69468-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="69468-127">No entanto, é altamente recomendável que seu aplicativo Verifique explicitamente todas as entradas nesse caso.</span><span class="sxs-lookup"><span data-stu-id="69468-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="69468-128">Desabilitando a validação de solicitação em uma página</span><span class="sxs-lookup"><span data-stu-id="69468-128">Disabling request validation on a page</span></span>

<span data-ttu-id="69468-129">Para desabilitar a validação de solicitação em uma página, você deve definir o atributo `validateRequest` da diretiva Page como `false`:</span><span class="sxs-lookup"><span data-stu-id="69468-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="69468-130">Quando a validação de solicitação está desabilitada, o conteúdo pode ser enviado para uma página; é responsabilidade do desenvolvedor da página garantir que o conteúdo seja codificado ou processado corretamente.</span><span class="sxs-lookup"><span data-stu-id="69468-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="69468-131">Desabilitando a validação de solicitação para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="69468-131">Disabling request validation for your application</span></span>

<span data-ttu-id="69468-132">Para desabilitar a validação de solicitação para seu aplicativo, você deve modificar ou criar um arquivo Web. config para seu aplicativo e definir o atributo validateRequest da seção `<pages />` como `false`:</span><span class="sxs-lookup"><span data-stu-id="69468-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="69468-133">Se você quiser desabilitar a validação de solicitação para todos os aplicativos em seu servidor, poderá fazer essa modificação no arquivo Machine. config.</span><span class="sxs-lookup"><span data-stu-id="69468-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="69468-134">Quando a validação de solicitação está desabilitada, o conteúdo pode ser enviado para seu aplicativo; é responsabilidade do desenvolvedor do aplicativo garantir que o conteúdo seja codificado ou processado corretamente.</span><span class="sxs-lookup"><span data-stu-id="69468-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="69468-135">O código abaixo é modificado para desativar a validação da solicitação:</span><span class="sxs-lookup"><span data-stu-id="69468-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="69468-136">Agora, se o seguinte JavaScript foi inserido na caixa de texto `<script>alert("hello!")</script>` o resultado seria:</span><span class="sxs-lookup"><span data-stu-id="69468-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="69468-137">Para evitar que isso aconteça, com a validação de solicitação desativada, precisamos codificar o conteúdo em HTML.</span><span class="sxs-lookup"><span data-stu-id="69468-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="69468-138">Como codificar conteúdo em HTML</span><span class="sxs-lookup"><span data-stu-id="69468-138">How to HTML encode content</span></span>

<span data-ttu-id="69468-139">Se você tiver desabilitado a validação de solicitação, é uma boa prática para codificar em HTML o conteúdo que será armazenado para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="69468-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="69468-140">A codificação HTML substituirá automaticamente qualquer '&lt;' ou '&gt;' (junto com vários outros símbolos) com a representação codificada HTML correspondente.</span><span class="sxs-lookup"><span data-stu-id="69468-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="69468-141">Por exemplo, '&lt;' é substituído por '&amp;lt; ' e '&gt;' é substituído por '&amp;gt; '.</span><span class="sxs-lookup"><span data-stu-id="69468-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="69468-142">Os navegadores usam esses códigos especiais para exibir o '&lt;' ou '&gt;' no navegador.</span><span class="sxs-lookup"><span data-stu-id="69468-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="69468-143">O conteúdo pode ser facilmente codificado em HTML no servidor usando a API `Server.HtmlEncode(string)`.</span><span class="sxs-lookup"><span data-stu-id="69468-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="69468-144">O conteúdo também pode ser facilmente decodificado em HTML, ou seja, revertido para HTML padrão usando o método `Server.HtmlDecode(string)`.</span><span class="sxs-lookup"><span data-stu-id="69468-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="69468-145">Resultando em:</span><span class="sxs-lookup"><span data-stu-id="69468-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
