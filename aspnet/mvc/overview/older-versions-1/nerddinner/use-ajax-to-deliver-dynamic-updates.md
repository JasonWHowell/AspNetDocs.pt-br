---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Use o AJAX para oferecer atualizações dinâmicas | Microsoft Docs
author: rick-anderson
description: O Passo 10 implementa o suporte para usuários conectados ao RSVP seu interesse em participar de um jantar, usando uma abordagem baseada em Ajax integrada dentro do detalhe do jantar...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541241"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="2e14b-103">Usar o AJAX para fornecer atualizações dinâmicas</span><span class="sxs-lookup"><span data-stu-id="2e14b-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="2e14b-104">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2e14b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2e14b-105">Baixar PDF</span><span class="sxs-lookup"><span data-stu-id="2e14b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="2e14b-106">Este é o passo 10 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="2e14b-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="2e14b-107">O Passo 10 implementa o suporte para usuários conectados ao RSVP sobre seu interesse em participar de um jantar, usando uma abordagem baseada em Ajax integrada na página de detalhes do jantar.</span><span class="sxs-lookup"><span data-stu-id="2e14b-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="2e14b-108">Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="2e14b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="2e14b-109">NerdDinner Passo 10: AJAX habilitando RSVPs aceita</span><span class="sxs-lookup"><span data-stu-id="2e14b-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="2e14b-110">Vamos agora implementar o suporte para usuários conectados ao RSVP seu interesse em participar de um jantar.</span><span class="sxs-lookup"><span data-stu-id="2e14b-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="2e14b-111">Habilitaremos isso usando uma abordagem baseada em AJAX integrada na página de detalhes do jantar.</span><span class="sxs-lookup"><span data-stu-id="2e14b-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="2e14b-112">Indicando se o usuário é RSVP'd</span><span class="sxs-lookup"><span data-stu-id="2e14b-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="2e14b-113">Os usuários podem visitar a URL */Dinners/Details/[id]* para ver detalhes sobre um jantar específico:</span><span class="sxs-lookup"><span data-stu-id="2e14b-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="2e14b-114">O método de ação Detalhes() é implementado assim:</span><span class="sxs-lookup"><span data-stu-id="2e14b-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="2e14b-115">Nosso primeiro passo para implementar o suporte ao RSVP será adicionar um método de ajuda "IsUserRegistered(nome de usuário)" ao nosso objeto Dinner (dentro da Dinner.cs classe parcial que construímos anteriormente).</span><span class="sxs-lookup"><span data-stu-id="2e14b-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="2e14b-116">Este método auxiliar retorna verdadeiro ou falso, dependendo se o usuário está atualmente RSVP'd para o Jantar:</span><span class="sxs-lookup"><span data-stu-id="2e14b-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="2e14b-117">Em seguida, podemos adicionar o seguinte código ao nosso modelo de exibição Details.aspx para exibir uma mensagem apropriada indicando se o usuário está registrado ou não para o evento:</span><span class="sxs-lookup"><span data-stu-id="2e14b-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="2e14b-118">E agora, quando um usuário visita um jantar, ele está registrado para ver esta mensagem:</span><span class="sxs-lookup"><span data-stu-id="2e14b-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="2e14b-119">E quando eles visitam um jantar eles não estão registrados para eles vão ver a mensagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="2e14b-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="2e14b-120">Implementação do Método de Ação de Registro</span><span class="sxs-lookup"><span data-stu-id="2e14b-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="2e14b-121">Vamos agora adicionar a funcionalidade necessária para habilitar os usuários ao RSVP para um jantar a partir da página de detalhes.</span><span class="sxs-lookup"><span data-stu-id="2e14b-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="2e14b-122">Para implementar isso, criaremos uma nova classe "RSVPController" clicando com o botão direito&gt;do mouse no diretório \Controllers e escolhendo o comando 'Adicionar-Controlador' no menu.</span><span class="sxs-lookup"><span data-stu-id="2e14b-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="2e14b-123">Implementaremos um método de ação "Registrar" dentro da nova classe RSVPController que toma um id para um jantar como argumento, recupera o objeto jantar apropriado, verifica se o usuário logado está atualmente na lista de usuários que se registraram para ele e, se não adicionar um objeto RSVP para eles:</span><span class="sxs-lookup"><span data-stu-id="2e14b-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="2e14b-124">Observe acima como estamos retornando uma seqüência simples como a saída do método de ação.</span><span class="sxs-lookup"><span data-stu-id="2e14b-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="2e14b-125">Poderíamos ter incorporado essa mensagem em um modelo de exibição – mas como ela é tão pequena, usaremos o método de ajuda content() na classe base do controlador e retornaremos uma mensagem de seqüência como acima.</span><span class="sxs-lookup"><span data-stu-id="2e14b-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="2e14b-126">Chamando o método de ação RSVPForEvent usando o AJAX</span><span class="sxs-lookup"><span data-stu-id="2e14b-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="2e14b-127">Usaremos o AJAX para invocar o método de ação Registrar a partir de nossa exibição Detalhes.</span><span class="sxs-lookup"><span data-stu-id="2e14b-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="2e14b-128">Implementar isso é muito fácil.</span><span class="sxs-lookup"><span data-stu-id="2e14b-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="2e14b-129">Primeiro, adicionaremos duas referências à biblioteca de scripts:</span><span class="sxs-lookup"><span data-stu-id="2e14b-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="2e14b-130">A primeira biblioteca faz referência ao núcleo ASP.NET biblioteca de scripts do lado do cliente AJAX.</span><span class="sxs-lookup"><span data-stu-id="2e14b-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="2e14b-131">Este arquivo tem aproximadamente 24k de tamanho (compactado) e contém a funcionalidade AJAX do lado do cliente principal.</span><span class="sxs-lookup"><span data-stu-id="2e14b-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="2e14b-132">A segunda biblioteca contém funções de utilidade que se integram com ASP.NET métodos de ajuda AJAX incorporados do MVC (que usaremos em breve).</span><span class="sxs-lookup"><span data-stu-id="2e14b-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="2e14b-133">Em seguida, podemos atualizar o código do modelo de exibição que adicionamos anteriormente para que, em vez de colocar uma mensagem "Você não está registrado para este evento", em vez disso, renderizamos um link que quando pressionado executa uma chamada AJAX que invoca nosso método de ação RSVPForEvent em nosso controlador RSVP e RSVPs o usuário:</span><span class="sxs-lookup"><span data-stu-id="2e14b-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="2e14b-134">O método auxiliar Ajax.ActionLink() usado acima é incorporado ASP.NET MVC e é semelhante ao método de ajuda Html.ActionLink(), exceto que, em vez de realizar uma navegação padrão, faz uma chamada AJAX para o método de ação quando o link é clicado.</span><span class="sxs-lookup"><span data-stu-id="2e14b-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="2e14b-135">Acima estamos chamando o método de ação "Registrar" no controlador "RSVP" e passando o DinnerID como o parâmetro "id" para ele.</span><span class="sxs-lookup"><span data-stu-id="2e14b-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="2e14b-136">O parâmetro final do AjaxOptions que estamos passando indica que queremos pegar o &lt;conteúdo&gt; devolvido do método de ação e atualizar o elemento div HTML na página cujo id é "rsvpmsg".</span><span class="sxs-lookup"><span data-stu-id="2e14b-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="2e14b-137">E agora, quando um usuário navega para um jantar, ele ainda não está registrado, verá um link para o RSVP para ele:</span><span class="sxs-lookup"><span data-stu-id="2e14b-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="2e14b-138">Se eles clicarem no link "RSVP para este evento", eles farão uma chamada AJAX para o método de ação Registrar no controlador RSVP, e quando ele for concluído, eles verão uma mensagem atualizada como abaixo:</span><span class="sxs-lookup"><span data-stu-id="2e14b-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="2e14b-139">A largura de banda da rede e o tráfego envolvidos ao fazer esta chamada AJAX são realmente leves.</span><span class="sxs-lookup"><span data-stu-id="2e14b-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="2e14b-140">Quando o usuário clica no link "RSVP para este evento", uma pequena solicitação de rede HTTP POST é feita para a URL */Dinners/Register/1* que parece abaixo no fio:</span><span class="sxs-lookup"><span data-stu-id="2e14b-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="2e14b-141">E a resposta do nosso método de ação Registrar é simplesmente:</span><span class="sxs-lookup"><span data-stu-id="2e14b-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="2e14b-142">Esta chamada leve é rápida e funcionará mesmo em uma rede lenta.</span><span class="sxs-lookup"><span data-stu-id="2e14b-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="2e14b-143">Adicionando uma animação jQuery</span><span class="sxs-lookup"><span data-stu-id="2e14b-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="2e14b-144">A funcionalidade AJAX que implementamos funciona bem e rápido.</span><span class="sxs-lookup"><span data-stu-id="2e14b-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="2e14b-145">Às vezes, pode acontecer tão rápido, porém, que um usuário pode não notar que o link RSVP foi substituído por um novo texto.</span><span class="sxs-lookup"><span data-stu-id="2e14b-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="2e14b-146">Para tornar o resultado um pouco mais óbvio, podemos adicionar uma animação simples para chamar a atenção para a mensagem de atualização.</span><span class="sxs-lookup"><span data-stu-id="2e14b-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="2e14b-147">O modelo padrão ASP.NET de projeto MVC inclui o jQuery – uma excelente (e muito popular) biblioteca JavaScript de código aberto que também é suportada pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2e14b-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="2e14b-148">jQuery fornece uma série de recursos, incluindo uma boa biblioteca de seleção e efeitos HTML DOM.</span><span class="sxs-lookup"><span data-stu-id="2e14b-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="2e14b-149">Para usar jQuery, primeiro adicionaremos uma referência de script a ele.</span><span class="sxs-lookup"><span data-stu-id="2e14b-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="2e14b-150">Como vamos usar o jQuery dentro de uma variedade de lugares dentro do nosso site, adicionaremos a referência de script no nosso arquivo de página mestre do Site.master para que todas as páginas possam usá-lo.</span><span class="sxs-lookup"><span data-stu-id="2e14b-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="2e14b-151">*Dica: certifique-se de ter instalado o hotfix do Intellisense JavaScript para VS 2008 SP1 que permite suporte mais rico ao intellisense para arquivos JavaScript (incluindo jQuery). Você pode baixá-lo a partir de:http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="2e14b-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="2e14b-152">O código escrito usando o JQuery muitas vezes usa um método JavaScript global "$()" que recupera um ou mais elementos HTML usando um seletor CSS.</span><span class="sxs-lookup"><span data-stu-id="2e14b-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="2e14b-153">Por exemplo, *$("#rsvpmsg")* seleciona qualquer elemento HTML com o id de rsvpmsg, enquanto *$(".something")* selecionaria todos os elementos com o nome de classe CSS "algo".</span><span class="sxs-lookup"><span data-stu-id="2e14b-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="2e14b-154">Você também pode escrever consultas mais avançadas, como "retornar todos os botões de rádio verificados" usando uma consulta seletorcomo: *$("entrada[=rádio][]).@type@checked*</span><span class="sxs-lookup"><span data-stu-id="2e14b-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="2e14b-155">Depois de selecionar elementos, você pode chamar métodos para que eles tomem medidas, como escondê-los: *$("#rsvpmsg").ocultar();*</span><span class="sxs-lookup"><span data-stu-id="2e14b-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="2e14b-156">Para o nosso cenário RSVP, definiremos uma simples função JavaScript chamada "AnimateRSVPMessage" &lt;que&gt; seleciona a div "rsvpmsg" e anima o tamanho do seu conteúdo de texto.</span><span class="sxs-lookup"><span data-stu-id="2e14b-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="2e14b-157">O código abaixo inicia o texto pequeno e, em seguida, faz com que ele aumente em um período de 400 milissegundos:</span><span class="sxs-lookup"><span data-stu-id="2e14b-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="2e14b-158">Podemos então conectar esta função JavaScript para ser chamada depois que nossa chamada AJAX for concluída com sucesso, passando seu nome para o nosso método auxiliar Ajax.ActionLink() (via a propriedade de eventos AjaxOptions "OnSuccess"):</span><span class="sxs-lookup"><span data-stu-id="2e14b-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="2e14b-159">E agora, quando o link "RSVP para este evento" é clicado e nossa chamada AJAX é concluída com sucesso, a mensagem de conteúdo enviada de volta irá animar e crescer muito:</span><span class="sxs-lookup"><span data-stu-id="2e14b-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="2e14b-160">Além de fornecer um evento "OnSuccess", o objeto AjaxOptions expõe eventos OnBegin, OnFailure e OnComplete que você pode lidar (juntamente com uma variedade de outras propriedades e opções úteis).</span><span class="sxs-lookup"><span data-stu-id="2e14b-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="2e14b-161">Limpeza - Refatorar uma visão parcial do RSVP</span><span class="sxs-lookup"><span data-stu-id="2e14b-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="2e14b-162">Nosso modelo de visualização de detalhes está começando a ficar um pouco longo, o que as horas extras tornarão um pouco mais difícil de entender.</span><span class="sxs-lookup"><span data-stu-id="2e14b-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="2e14b-163">Para ajudar a melhorar a legibilidade do código, vamos terminar criando uma exibição parcial – RSVPStatus.ascx – que encapsula todo o código de exibição RSVP para nossa página Detalhes.</span><span class="sxs-lookup"><span data-stu-id="2e14b-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="2e14b-164">Podemos fazer isso clicando com o botão direito do mouse na&gt;pasta \Views\Dinners e, em seguida, escolhendo o comando Adicionar-Exibir menu.</span><span class="sxs-lookup"><span data-stu-id="2e14b-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="2e14b-165">Vamos tê-lo tomar um objeto jantar como seu viewmodel fortemente digitado.</span><span class="sxs-lookup"><span data-stu-id="2e14b-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="2e14b-166">Podemos então copiar/colar o conteúdo RSVP da nossa exibição Details.aspx nele.</span><span class="sxs-lookup"><span data-stu-id="2e14b-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="2e14b-167">Depois de fazer isso, vamos também criar outra visualização parcial – EditAndDeleteLinks.ascx – que encapsula nosso código de exibição de link editar e excluir.</span><span class="sxs-lookup"><span data-stu-id="2e14b-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="2e14b-168">Também o manteremos levando um objeto Dinner como seu ViewModel fortemente digitado e copiaremos/colaremos a lógica Editar e Excluir da nossa exibição Details.aspx nele.</span><span class="sxs-lookup"><span data-stu-id="2e14b-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="2e14b-169">Nosso modelo de visualização de detalhes pode incluir apenas duas chamadas do método Html.RenderPartial() na parte inferior:</span><span class="sxs-lookup"><span data-stu-id="2e14b-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="2e14b-170">Isso torna o código mais limpo para ler e manter.</span><span class="sxs-lookup"><span data-stu-id="2e14b-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="2e14b-171">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="2e14b-171">Next Step</span></span>

<span data-ttu-id="2e14b-172">Vamos agora ver como podemos usar o AJAX ainda mais e adicionar suporte de mapeamento interativo ao nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2e14b-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2e14b-173">[Próximo](secure-applications-using-authentication-and-authorization.md)
> [anterior](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="2e14b-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
