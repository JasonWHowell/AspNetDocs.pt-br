---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: Negociação de conteúdo em ASP.NET Web API-ASP.NET 4. x
author: MikeWasson
description: Descreve como ASP.NET Web API implementa a negociação de conteúdo HTTP para ASP.NET 4. x.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622265"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="96b73-103">Negociação de conteúdo no ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="96b73-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="96b73-104">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="96b73-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="96b73-105">Este artigo descreve como ASP.NET Web API implementa a negociação de conteúdo para ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="96b73-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="96b73-106">A especificação HTTP (RFC 2616) define a negociação de conteúdo como "o processo de selecionar a melhor representação para uma determinada resposta quando há várias representações disponíveis".</span><span class="sxs-lookup"><span data-stu-id="96b73-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="96b73-107">O mecanismo primário para a negociação de conteúdo em HTTP são estes cabeçalhos de solicitação:</span><span class="sxs-lookup"><span data-stu-id="96b73-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="96b73-108">**Aceitar:** Quais tipos de mídia são aceitáveis para a resposta, como "Application/JSON", "application/xml", ou um tipo de mídia personalizado, como &quot;application/vnd. example + XML&quot;</span><span class="sxs-lookup"><span data-stu-id="96b73-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="96b73-109">**Accept-charset:** Quais conjuntos de caracteres são aceitáveis, como UTF-8 ou ISO 8859-1.</span><span class="sxs-lookup"><span data-stu-id="96b73-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="96b73-110">**Aceitação-codificação:** Quais codificações de conteúdo são aceitáveis, como gzip.</span><span class="sxs-lookup"><span data-stu-id="96b73-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="96b73-111">**Accept-Language:** A linguagem natural preferida, como "en-US".</span><span class="sxs-lookup"><span data-stu-id="96b73-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="96b73-112">O servidor também pode examinar outras partes da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="96b73-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="96b73-113">Por exemplo, se a solicitação contiver um cabeçalho X solicitado-com, indicando uma solicitação AJAX, o servidor poderá padronizar para JSON se não houver cabeçalho Accept.</span><span class="sxs-lookup"><span data-stu-id="96b73-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="96b73-114">Neste artigo, veremos como a API da Web usa os cabeçalhos Accept e Accept-charset.</span><span class="sxs-lookup"><span data-stu-id="96b73-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="96b73-115">(Neste momento, não há suporte interno para Accept-Encoding ou Accept-Language.)</span><span class="sxs-lookup"><span data-stu-id="96b73-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="96b73-116">Serialização</span><span class="sxs-lookup"><span data-stu-id="96b73-116">Serialization</span></span>

<span data-ttu-id="96b73-117">Se um controlador da API Web retornar um recurso como tipo CLR, o pipeline serializará o valor de retorno e o gravará no corpo da resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="96b73-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="96b73-118">Por exemplo, considere a seguinte ação do controlador:</span><span class="sxs-lookup"><span data-stu-id="96b73-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="96b73-119">Um cliente pode enviar esta solicitação HTTP:</span><span class="sxs-lookup"><span data-stu-id="96b73-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="96b73-120">Em resposta, o servidor pode enviar:</span><span class="sxs-lookup"><span data-stu-id="96b73-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="96b73-121">Neste exemplo, o cliente solicitou JSON, JavaScript ou "qualquer coisa" (\*/\*).</span><span class="sxs-lookup"><span data-stu-id="96b73-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="96b73-122">O servidor respondeu com uma representação JSON do objeto `Product`.</span><span class="sxs-lookup"><span data-stu-id="96b73-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="96b73-123">Observe que o cabeçalho Content-Type na resposta é definido como &quot;Application/JSON&quot;.</span><span class="sxs-lookup"><span data-stu-id="96b73-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="96b73-124">Um controlador também pode retornar um objeto **HttpResponseMessage** .</span><span class="sxs-lookup"><span data-stu-id="96b73-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="96b73-125">Para especificar um objeto CLR para o corpo da resposta, chame o método de extensão **CreateResponse** :</span><span class="sxs-lookup"><span data-stu-id="96b73-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="96b73-126">Essa opção oferece mais controle sobre os detalhes da resposta.</span><span class="sxs-lookup"><span data-stu-id="96b73-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="96b73-127">Você pode definir o código de status, adicionar cabeçalhos HTTP e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="96b73-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="96b73-128">O objeto que serializa o recurso é chamado de *formatador de mídia*.</span><span class="sxs-lookup"><span data-stu-id="96b73-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="96b73-129">Os formatadores de mídia derivam da classe **MediaTypeFormatter** .</span><span class="sxs-lookup"><span data-stu-id="96b73-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="96b73-130">A API Web fornece formatadores de mídia para XML e JSON, e você pode criar formatadores personalizados para dar suporte a outros tipos de mídia.</span><span class="sxs-lookup"><span data-stu-id="96b73-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="96b73-131">Para obter informações sobre como escrever um formatador personalizado, consulte [formatadores de mídia](media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="96b73-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="96b73-132">Como a negociação de conteúdo funciona</span><span class="sxs-lookup"><span data-stu-id="96b73-132">How Content Negotiation Works</span></span>

<span data-ttu-id="96b73-133">Primeiro, o pipeline Obtém o serviço **IContentNegotiator** do objeto **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="96b73-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="96b73-134">Ele também obtém a lista de formatadores de mídia da coleção **HttpConfiguration. Formatters** .</span><span class="sxs-lookup"><span data-stu-id="96b73-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="96b73-135">Em seguida, o pipeline chama **IContentNegotiator. Negotiate**, passando em:</span><span class="sxs-lookup"><span data-stu-id="96b73-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="96b73-136">O tipo de objeto a ser serializado</span><span class="sxs-lookup"><span data-stu-id="96b73-136">The type of object to serialize</span></span>
- <span data-ttu-id="96b73-137">A coleção de formatadores de mídia</span><span class="sxs-lookup"><span data-stu-id="96b73-137">The collection of media formatters</span></span>
- <span data-ttu-id="96b73-138">A solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="96b73-138">The HTTP request</span></span>

<span data-ttu-id="96b73-139">O método **Negotiate** retorna duas partes de informação:</span><span class="sxs-lookup"><span data-stu-id="96b73-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="96b73-140">Qual formatador usar</span><span class="sxs-lookup"><span data-stu-id="96b73-140">Which formatter to use</span></span>
- <span data-ttu-id="96b73-141">O tipo de mídia para a resposta</span><span class="sxs-lookup"><span data-stu-id="96b73-141">The media type for the response</span></span>

<span data-ttu-id="96b73-142">Se nenhum formatador for encontrado, o método **Negotiate** retornará **NULL**e o cliente receberá o erro http 406 (não aceitável).</span><span class="sxs-lookup"><span data-stu-id="96b73-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="96b73-143">O código a seguir mostra como um controlador pode invocar diretamente a negociação de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="96b73-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="96b73-144">Esse código é equivalente ao que o pipeline faz automaticamente.</span><span class="sxs-lookup"><span data-stu-id="96b73-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="96b73-145">Negociador de conteúdo padrão</span><span class="sxs-lookup"><span data-stu-id="96b73-145">Default Content Negotiator</span></span>

<span data-ttu-id="96b73-146">A classe **DefaultContentNegotiator** fornece a implementação padrão de **IContentNegotiator**.</span><span class="sxs-lookup"><span data-stu-id="96b73-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="96b73-147">Ele usa vários critérios para selecionar um formatador.</span><span class="sxs-lookup"><span data-stu-id="96b73-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="96b73-148">Primeiro, o formatador deve ser capaz de serializar o tipo.</span><span class="sxs-lookup"><span data-stu-id="96b73-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="96b73-149">Isso é verificado chamando **MediaTypeFormatter. Canwritetype**.</span><span class="sxs-lookup"><span data-stu-id="96b73-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="96b73-150">Em seguida, o conteúdo negociador examina cada formatador e avalia o quão bem ele corresponde à solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="96b73-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="96b73-151">Para avaliar a correspondência, o conteúdo negociador examina duas coisas no formatador:</span><span class="sxs-lookup"><span data-stu-id="96b73-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="96b73-152">A coleção **SupportedMediaTypes** , que contém uma lista de tipos de mídia com suporte.</span><span class="sxs-lookup"><span data-stu-id="96b73-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="96b73-153">O conteúdo negociador tenta corresponder a essa lista com o cabeçalho Accept de solicitação.</span><span class="sxs-lookup"><span data-stu-id="96b73-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="96b73-154">Observe que o cabeçalho Accept pode incluir intervalos.</span><span class="sxs-lookup"><span data-stu-id="96b73-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="96b73-155">Por exemplo, "texto/simples" é uma correspondência para texto/\* ou \*/\*.</span><span class="sxs-lookup"><span data-stu-id="96b73-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="96b73-156">A coleção **MediaTypeMappings** , que contém uma lista de objetos **MediaTypeMapping** .</span><span class="sxs-lookup"><span data-stu-id="96b73-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="96b73-157">A classe **MediaTypeMapping** fornece uma maneira genérica de fazer a correspondência de solicitações HTTP com tipos de mídia.</span><span class="sxs-lookup"><span data-stu-id="96b73-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="96b73-158">Por exemplo, ele poderia mapear um cabeçalho HTTP personalizado para um tipo de mídia específico.</span><span class="sxs-lookup"><span data-stu-id="96b73-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="96b73-159">Se houver várias correspondências, a correspondência com o fator de qualidade mais alto vence.</span><span class="sxs-lookup"><span data-stu-id="96b73-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="96b73-160">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="96b73-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="96b73-161">Neste exemplo, Application/JSON tem um fator de qualidade implícito de 1,0, portanto, é preferível em Application/XML.</span><span class="sxs-lookup"><span data-stu-id="96b73-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="96b73-162">Se nenhuma correspondência for encontrada, o conteúdo negociador tentará corresponder ao tipo de mídia do corpo da solicitação, se houver.</span><span class="sxs-lookup"><span data-stu-id="96b73-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="96b73-163">Por exemplo, se a solicitação contiver dados JSON, o conteúdo negociador procurará um formatador JSON.</span><span class="sxs-lookup"><span data-stu-id="96b73-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="96b73-164">Se ainda não houver nenhuma correspondência, o conteúdo negociador simplesmente escolhe o primeiro formatador que pode serializar o tipo.</span><span class="sxs-lookup"><span data-stu-id="96b73-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="96b73-165">Selecionando uma codificação de caracteres</span><span class="sxs-lookup"><span data-stu-id="96b73-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="96b73-166">Depois que um formatador é selecionado, o conteúdo negociador escolhe a melhor codificação de caractere examinando a propriedade **SupportedEncodings** no formatador e correspondendo-o com o cabeçalho Accept-charset na solicitação (se houver).</span><span class="sxs-lookup"><span data-stu-id="96b73-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
