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
# <a name="use-ajax-to-deliver-dynamic-updates"></a>Usar o AJAX para fornecer atualizações dinâmicas

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 10 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O Passo 10 implementa o suporte para usuários conectados ao RSVP sobre seu interesse em participar de um jantar, usando uma abordagem baseada em Ajax integrada na página de detalhes do jantar.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner Passo 10: AJAX habilitando RSVPs aceita

Vamos agora implementar o suporte para usuários conectados ao RSVP seu interesse em participar de um jantar. Habilitaremos isso usando uma abordagem baseada em AJAX integrada na página de detalhes do jantar.

### <a name="indicating-whether-the-user-is-rsvpd"></a>Indicando se o usuário é RSVP'd

Os usuários podem visitar a URL */Dinners/Details/[id]* para ver detalhes sobre um jantar específico:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

O método de ação Detalhes() é implementado assim:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

Nosso primeiro passo para implementar o suporte ao RSVP será adicionar um método de ajuda "IsUserRegistered(nome de usuário)" ao nosso objeto Dinner (dentro da Dinner.cs classe parcial que construímos anteriormente). Este método auxiliar retorna verdadeiro ou falso, dependendo se o usuário está atualmente RSVP'd para o Jantar:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

Em seguida, podemos adicionar o seguinte código ao nosso modelo de exibição Details.aspx para exibir uma mensagem apropriada indicando se o usuário está registrado ou não para o evento:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

E agora, quando um usuário visita um jantar, ele está registrado para ver esta mensagem:

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

E quando eles visitam um jantar eles não estão registrados para eles vão ver a mensagem abaixo:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Implementação do Método de Ação de Registro

Vamos agora adicionar a funcionalidade necessária para habilitar os usuários ao RSVP para um jantar a partir da página de detalhes.

Para implementar isso, criaremos uma nova classe "RSVPController" clicando com o botão direito&gt;do mouse no diretório \Controllers e escolhendo o comando 'Adicionar-Controlador' no menu.

Implementaremos um método de ação "Registrar" dentro da nova classe RSVPController que toma um id para um jantar como argumento, recupera o objeto jantar apropriado, verifica se o usuário logado está atualmente na lista de usuários que se registraram para ele e, se não adicionar um objeto RSVP para eles:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

Observe acima como estamos retornando uma seqüência simples como a saída do método de ação. Poderíamos ter incorporado essa mensagem em um modelo de exibição – mas como ela é tão pequena, usaremos o método de ajuda content() na classe base do controlador e retornaremos uma mensagem de seqüência como acima.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>Chamando o método de ação RSVPForEvent usando o AJAX

Usaremos o AJAX para invocar o método de ação Registrar a partir de nossa exibição Detalhes. Implementar isso é muito fácil. Primeiro, adicionaremos duas referências à biblioteca de scripts:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

A primeira biblioteca faz referência ao núcleo ASP.NET biblioteca de scripts do lado do cliente AJAX. Este arquivo tem aproximadamente 24k de tamanho (compactado) e contém a funcionalidade AJAX do lado do cliente principal. A segunda biblioteca contém funções de utilidade que se integram com ASP.NET métodos de ajuda AJAX incorporados do MVC (que usaremos em breve).

Em seguida, podemos atualizar o código do modelo de exibição que adicionamos anteriormente para que, em vez de colocar uma mensagem "Você não está registrado para este evento", em vez disso, renderizamos um link que quando pressionado executa uma chamada AJAX que invoca nosso método de ação RSVPForEvent em nosso controlador RSVP e RSVPs o usuário:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

O método auxiliar Ajax.ActionLink() usado acima é incorporado ASP.NET MVC e é semelhante ao método de ajuda Html.ActionLink(), exceto que, em vez de realizar uma navegação padrão, faz uma chamada AJAX para o método de ação quando o link é clicado. Acima estamos chamando o método de ação "Registrar" no controlador "RSVP" e passando o DinnerID como o parâmetro "id" para ele. O parâmetro final do AjaxOptions que estamos passando indica que queremos pegar o &lt;conteúdo&gt; devolvido do método de ação e atualizar o elemento div HTML na página cujo id é "rsvpmsg".

E agora, quando um usuário navega para um jantar, ele ainda não está registrado, verá um link para o RSVP para ele:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

Se eles clicarem no link "RSVP para este evento", eles farão uma chamada AJAX para o método de ação Registrar no controlador RSVP, e quando ele for concluído, eles verão uma mensagem atualizada como abaixo:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

A largura de banda da rede e o tráfego envolvidos ao fazer esta chamada AJAX são realmente leves. Quando o usuário clica no link "RSVP para este evento", uma pequena solicitação de rede HTTP POST é feita para a URL */Dinners/Register/1* que parece abaixo no fio:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

E a resposta do nosso método de ação Registrar é simplesmente:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

Esta chamada leve é rápida e funcionará mesmo em uma rede lenta.

### <a name="adding-a-jquery-animation"></a>Adicionando uma animação jQuery

A funcionalidade AJAX que implementamos funciona bem e rápido. Às vezes, pode acontecer tão rápido, porém, que um usuário pode não notar que o link RSVP foi substituído por um novo texto. Para tornar o resultado um pouco mais óbvio, podemos adicionar uma animação simples para chamar a atenção para a mensagem de atualização.

O modelo padrão ASP.NET de projeto MVC inclui o jQuery – uma excelente (e muito popular) biblioteca JavaScript de código aberto que também é suportada pela Microsoft. jQuery fornece uma série de recursos, incluindo uma boa biblioteca de seleção e efeitos HTML DOM.

Para usar jQuery, primeiro adicionaremos uma referência de script a ele. Como vamos usar o jQuery dentro de uma variedade de lugares dentro do nosso site, adicionaremos a referência de script no nosso arquivo de página mestre do Site.master para que todas as páginas possam usá-lo.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*Dica: certifique-se de ter instalado o hotfix do Intellisense JavaScript para VS 2008 SP1 que permite suporte mais rico ao intellisense para arquivos JavaScript (incluindo jQuery). Você pode baixá-lo a partir de:http://tinyurl.com/vs2008javascripthotfix*

O código escrito usando o JQuery muitas vezes usa um método JavaScript global "$()" que recupera um ou mais elementos HTML usando um seletor CSS. Por exemplo, *$("#rsvpmsg")* seleciona qualquer elemento HTML com o id de rsvpmsg, enquanto *$(".something")* selecionaria todos os elementos com o nome de classe CSS "algo". Você também pode escrever consultas mais avançadas, como "retornar todos os botões de rádio verificados" usando uma consulta seletorcomo: *$("entrada[=rádio][]).@type@checked*

Depois de selecionar elementos, você pode chamar métodos para que eles tomem medidas, como escondê-los: *$("#rsvpmsg").ocultar();*

Para o nosso cenário RSVP, definiremos uma simples função JavaScript chamada "AnimateRSVPMessage" &lt;que&gt; seleciona a div "rsvpmsg" e anima o tamanho do seu conteúdo de texto. O código abaixo inicia o texto pequeno e, em seguida, faz com que ele aumente em um período de 400 milissegundos:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

Podemos então conectar esta função JavaScript para ser chamada depois que nossa chamada AJAX for concluída com sucesso, passando seu nome para o nosso método auxiliar Ajax.ActionLink() (via a propriedade de eventos AjaxOptions "OnSuccess"):

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

E agora, quando o link "RSVP para este evento" é clicado e nossa chamada AJAX é concluída com sucesso, a mensagem de conteúdo enviada de volta irá animar e crescer muito:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

Além de fornecer um evento "OnSuccess", o objeto AjaxOptions expõe eventos OnBegin, OnFailure e OnComplete que você pode lidar (juntamente com uma variedade de outras propriedades e opções úteis).

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>Limpeza - Refatorar uma visão parcial do RSVP

Nosso modelo de visualização de detalhes está começando a ficar um pouco longo, o que as horas extras tornarão um pouco mais difícil de entender. Para ajudar a melhorar a legibilidade do código, vamos terminar criando uma exibição parcial – RSVPStatus.ascx – que encapsula todo o código de exibição RSVP para nossa página Detalhes.

Podemos fazer isso clicando com o botão direito do mouse na&gt;pasta \Views\Dinners e, em seguida, escolhendo o comando Adicionar-Exibir menu. Vamos tê-lo tomar um objeto jantar como seu viewmodel fortemente digitado. Podemos então copiar/colar o conteúdo RSVP da nossa exibição Details.aspx nele.

Depois de fazer isso, vamos também criar outra visualização parcial – EditAndDeleteLinks.ascx – que encapsula nosso código de exibição de link editar e excluir. Também o manteremos levando um objeto Dinner como seu ViewModel fortemente digitado e copiaremos/colaremos a lógica Editar e Excluir da nossa exibição Details.aspx nele.

Nosso modelo de visualização de detalhes pode incluir apenas duas chamadas do método Html.RenderPartial() na parte inferior:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

Isso torna o código mais limpo para ler e manter.

### <a name="next-step"></a>Próxima etapa

Vamos agora ver como podemos usar o AJAX ainda mais e adicionar suporte de mapeamento interativo ao nosso aplicativo.

> [!div class="step-by-step"]
> [Próximo](secure-applications-using-authentication-and-authorization.md)
> [anterior](use-ajax-to-implement-mapping-scenarios.md)
