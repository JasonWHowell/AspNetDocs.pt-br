---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: Use o AJAX para implementar cenários de mapeamento | Microsoft Docs
author: rick-anderson
description: O passo 11 mostra como integrar o suporte de mapeamento AJAX em nosso aplicativo NerdDinner, permitindo que os usuários que estão criando, editando ou visualizando jantares vejam o l...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542580"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>Usar o AJAX para implementar cenários de mapeamento

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 11 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O Passo 11 mostra como integrar o suporte de mapeamento AJAX em nosso aplicativo NerdDinner, permitindo que os usuários que estão criando, editando ou visualizando jantares vejam a localização do jantar graficamente.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner Passo 11: Integrando um mapa AJAX

Agora, tornaremos nosso aplicativo um pouco mais interessante visualmente integrando o suporte de mapeamento AJAX. Isso permitirá que os usuários que estão criando, editando ou visualizando jantares vejam a localização do jantar graficamente.

### <a name="creating-a-map-partial-view"></a>Criando uma visão parcial do mapa

Vamos usar a funcionalidade de mapeamento em vários lugares dentro do nosso aplicativo. Para manter nosso código DRY, encapsularemos a funcionalidade do mapa comum dentro de um único modelo parcial que podemos reutilizar em várias ações e visualizações do controlador. Nomearemos esta exibição parcial de "map.ascx" e a criaremos dentro do diretório \Views\Dinners.

Podemos criar o map.ascx parcial clicando com o botão direito do mouse&gt;no diretório \Views\Dinners e escolhendo o comando Adicionar-Exibir menu. Vamos nomear a exibição "Map.ascx", verificar como uma exibição parcial e indicar que vamos passá-la uma classe de modelo "Jantar" fortemente digitada:

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

Quando clicarmos no botão "Adicionar", nosso modelo parcial será criado. Em seguida, atualizaremos o arquivo Map.ascx para ter o seguinte conteúdo:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

A &lt;primeira&gt; referência de script aponta para a biblioteca de mapeamento Microsoft Virtual Earth 6.2. A &lt;segunda&gt; referência de script aponta para um arquivo map.js que criaremos em breve, o que encapsulará nossa lógica comum de mapeamento Javascript. O &lt;elemento div id="theMap"&gt; é o contêiner HTML que a Terra Virtual usará para hospedar o mapa.

Em seguida, &lt;temos&gt; um bloco de script incorporado que contém duas funções JavaScript específicas para esta exibição. A primeira função usa jQuery para conectar uma função que é executada quando a página está pronta para executar o script do lado do cliente. Ele chama uma função de ajudante do LoadMap() que definiremos dentro do nosso arquivo de script Map.js para carregar o controle do mapa da terra virtual. A segunda função é um manipulador de eventos de retorno de chamada que adiciona um pino ao mapa que identifica um local.

Observe como estamos usando um &lt;bloco&gt; %= % do lado do servidor dentro do bloco de script do lado do cliente para incorporar a latitude e a longitude do Jantar que queremos mapear no JavaScript. Esta é uma técnica útil para produzir valores dinâmicos que podem ser usados pelo script do lado do cliente (sem exigir uma chamada AJAX separada de volta ao servidor para recuperar os valores – o que o torna mais rápido). Os &lt;blocos&gt; %= % serão executados quando a exibição estiver renderizada no servidor – e assim a saída do HTML acabará com valores JavaScript incorporados (por exemplo: var latitude = 47,64312;).

### <a name="creating-a-mapjs-utility-library"></a>Criando uma biblioteca de utilitários Map.js

Vamos agora criar o arquivo Map.js que podemos usar para encapsular a funcionalidade JavaScript para o nosso mapa (e implementar os métodos LoadMap e LoadPin acima). Podemos fazer isso clicando com o botão direito do mouse no diretório \Scripts dentro do nosso projeto e, em seguida, escolher o comando "Adicionar-novo&gt;item", selecionar o item JScript e nomeá-lo "Map.js".

Abaixo está o código JavaScript que adicionaremos ao arquivo Map.js que interagirá com a Terra Virtual para exibir nosso mapa e adicionar pinos de localização a ele para nossos jantares:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>Integrando o Mapa com formulários de criação e edição

Agora, integraremos o suporte do Mapa aos nossos cenários de Criação e Edição existentes. A boa notícia é que isso é muito fácil de fazer, e não exige que mudemos qualquer um dos nossos códigos controladores. Como nossas visualizações Criar e Editar compartilham uma visão parcial comum do "DinnerForm" para implementar a ui do formulário de jantar, podemos adicionar o mapa em um só lugar e ter nossos cenários de Criar e Editar usá-lo.

Tudo o que precisamos fazer é abrir a visualização parcial \Views\DinnerForm\DinnerForm.ascx e atualizá-la para incluir nossa nova parcial do mapa. Abaixo está como será o DinnerForm atualizado quando o mapa for adicionado (nota: os elementos de formulário HTML são omitidos do trecho de código abaixo para brevidade):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

A parte do DinnerForm acima leva um objeto do tipo "DinnerFormViewModel" como seu tipo de modelo (porque ele precisa tanto de um objeto Dinner, quanto de uma SelectList para preencher a lista de itens de lista de itens de baixa). Nossa parcial do Mapa só precisa de um objeto do tipo "Jantar" como seu tipo de modelo, e assim, quando tornamos o mapa parcial, estamos passando apenas a subpropriedade jantar do DinnerFormViewModel para ele:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

A função JavaScript que adicionamos ao jQuery de uso parcial para anexar um evento "desfoque" à caixa de texto HTML "Address". Você provavelmente já ouviu falar de eventos de "foco" que disparam quando um usuário clica ou guias em uma caixa de texto. O oposto é um evento "desfoque" que é acionado quando um usuário sai de uma caixa de texto. O manipulador de eventos acima limpa os valores da caixa de texto de latitude e longitude quando isso acontece e, em seguida, plota o novo local de endereço em nosso mapa. Um manipulador de eventos de retorno de chamada que definimos dentro do arquivo map.js atualizará as caixas de texto longitude e latitude em nosso formulário usando valores retornados pela terra virtual com base no endereço que demos a ele.

E agora, quando executarmos nosso aplicativo novamente e clicarmos na guia "Jantar do Anfitrião", veremos um mapa padrão exibido junto com nossos elementos padrão de formulário de jantar:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

Quando digitamos um endereço e, em seguida, a guia é afastada, o mapa será atualizado dinamicamente para exibir o local, e nosso manipulador de eventos preencherá as caixas de texto latitude/longitude com os valores de localização:

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

Se salvarmos o novo jantar e abri-lo novamente para edição, descobriremos que a localização do mapa é exibida quando a página é carregada:

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

Toda vez que o campo de endereço é alterado, o mapa e as coordenadas de latitude/longitude serão atualizados.

Agora que o mapa exibe o local do Jantar, também podemos alterar os campos de formulário de Latitude e Longitude de serem caixas de texto visíveis para, em vez disso, serem elementos ocultos (uma vez que o mapa está atualizando-os automaticamente cada vez que um endereço é inserido). Para fazer isso, mudaremos de usar o ajudante HTML.TextBox() HTML para usar o método de ajuda Html.Hidden():

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

E agora nossos formulários são um pouco mais fáceis de usar e evitam exibir a latitude/longitude crua (enquanto ainda os armazenam com cada Jantar no banco de dados):

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>Integrando o Mapa com a exibição de detalhes

Agora que temos o mapa integrado com nossos cenários de Criar e Editar, vamos também integrá-lo com o nosso cenário de Detalhes. Tudo o que precisamos fazer &lt;é chamar % Html.RenderPartial("mapa"); %&gt; na exibição Detalhes.

Abaixo está o código-fonte para a exibição completa de detalhes (com integração do mapa):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

E agora, quando um usuário navega para uma URL /Dinners/Details/[id] eles verão detalhes sobre o jantar, a localização do jantar no mapa (completo com um push-pin que ao passar por cima exibe o título do jantar e o endereço dele), e terá um link AJAX para o RSVP para ele:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>Implementando pesquisa de localização em nosso banco de dados e repositório

Para concluir nossa implementação do AJAX, vamos adicionar um Mapa à página inicial do aplicativo que permite que os usuários pesquisem graficamente por jantares perto deles.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Começaremos implementando suporte em nosso banco de dados e camada de repositório de dados para executar eficientemente uma pesquisa de raio baseada em localização para Jantares. Poderíamos usar as novas [características geoespaciais do SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) para implementar isso, ou, alternativamente, podemos usar [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) uma abordagem de função SQL que Gary Dryden discutiu no artigo aqui: e Rob Conery blogou sobre o uso com LINQ para SQL aqui:[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

Para implementar essa técnica, abriremos o "Server Explorer" no Visual Studio, selecionaremos o banco de dados NerdDinner e, em seguida, clicarem os direitos diretos no subnó sob ela e optaremos por criar uma nova "função de valor escalar":

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

Em seguida, colaremos na seguinte função DistanceBetween:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

Em seguida, criaremos uma nova função de valor de tabela no SQL Server que chamaremos de "Jantares mais próximos":

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

Esta função de tabela "NearestDinners" usa a função helper DistanceBetween para retornar todos os Jantares dentro de 160 km da latitude e longitude que fornecemos:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

Para chamar essa função, primeiro abriremos o LINQ para o designer SQL clicando duas vezes no arquivo NerdDinner.dbml dentro do nosso diretório \Models:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

Em seguida, arrastaremos as funções Mais próximas Jantares e DistânciaS entre o designer LINQ para SQL, o que fará com que eles sejam adicionados como métodos em nossa classe LINQ para SQL NerdDinnerDataContext:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

Podemos então expor um método de consulta "FindByLocation" em nossa classe DinnerRepository que usa a função NearestDinner para retornar jantares próximos que estão dentro de 160 km do local especificado:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>Implementando um método de ação de pesquisa AJAX baseado em JSON

Agora implementaremos um método de ação do controlador que se aproveita do novo método de repositório FindByLocation() para retornar uma lista de dados do Jantar que podem ser usados para preencher um mapa. Teremos este método de ação retorná-lo de volta os dados do Jantar em um formato JSON (JavaScript Object Notation) para que ele possa ser facilmente manipulado usando JavaScript no cliente.

Para implementar isso, criaremos uma nova classe "SearchController" clicando com o botão direito&gt;do mouse no diretório \Controllers e escolhendo o comando 'Adicionar-Controlador'. Em seguida, implementaremos um método de ação "SearchByLocation" dentro da nova classe SearchController como abaixo:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

O método de ação SearchByLocation do SearchController chama internamente o método FindByLocation no DinnerRepository para obter uma lista de jantares próximos. Em vez de devolver os objetos do Jantar diretamente ao cliente, no entanto, ele devolve objetos JsonDinner. A classe JsonDinner expõe um subconjunto de propriedades do Jantar (por exemplo: por razões de segurança, ele não divulga os nomes das pessoas que têm RSVP'd para um jantar). Ele também inclui uma propriedade RSVPCount que não existe no Jantar e que é calculada dinamicamente contando o número de objetos RSVP associados a um jantar específico.

Em seguida, estamos usando o método auxiliar Json() na classe base controller para retornar a seqüência de jantares usando um formato de fio baseado em JSON. JSON é um formato de texto padrão para representar estruturas de dados simples. Abaixo está um exemplo de como uma lista formatada em JSON de dois objetos JsonDinner se parece quando retornada do nosso método de ação:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>Chamando o método AJAX baseado em JSON usando jQuery

Agora estamos prontos para atualizar a página inicial do aplicativo NerdDinner para usar o método de ação SearchByLocation do SearchController. Para fazer isso, abriremos o modelo de exibição /Views/Home/Index.aspx e o atualizaremos para &lt;ter&gt; uma caixa de texto, botão de pesquisa, nosso mapa e um elemento div chamado dinnerList:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

Em seguida, podemos adicionar duas funções JavaScript à página:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

A primeira função JavaScript carrega o mapa quando a página é carregada pela primeira vez. A segunda função JavaScript liga um manipulador de eventos javaScript no botão de pesquisa. Quando o botão é pressionado, ele chama a função JavaScript FindDinnersGivenLocation() que adicionaremos ao nosso arquivo Map.js:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

Esta função FindDinnersGivenLocation() chama mapa. Encontre() no Virtual Earth Control para centralizar no local inserido. Quando o serviço de mapa da Terra virtual retorna, o mapa. O método Find() invoca o método de retorno de chamadaUpdateMapDinners que passamos como o argumento final.

O método callbackUpdateMapDinners() é onde o trabalho real é feito. Ele usa o método de ajuda $.post() do jQuery para executar uma chamada AJAX para o método de ação SearchByLocation() do searchcontroller – passando-o pela latitude e longitude do mapa recém-centrado. Ele define uma função inline que será chamada quando o método de ajuda $.post() forcomplete, e os resultados do jantar formatado sinuoso retornaram do método de ação SearchByLocation() será aprovado usando uma variável chamada "jantares". Em seguida, ele faz um foreach sobre cada jantar retornado, e usa a latitude do jantar e longitude e outras propriedades para adicionar um novo pino no mapa. Ele também adiciona uma entrada de jantar à lista HTML de jantares à direita do mapa. Em seguida, ele liga um evento de hover para os pushpins e a lista HTML para que os detalhes sobre o jantar sejam exibidos quando um usuário paira sobre eles:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

E agora, quando executarmos o aplicativo e visitarmos a home-page, seremos apresentados com um mapa. Quando digitarmos o nome de uma cidade, o mapa exibirá os próximos jantares perto dela:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

Pairando sobre um jantar mostrará detalhes sobre ele.

Clicar no título do Jantar na bolha ou no lado direito na lista HTML nos navegará até o jantar – que podemos, então, opcionalmente, RSVP para:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>Próxima etapa

Agora implementamos todas as funcionalidades do aplicativo NerdDinner. Vamos agora ver como podemos habilitar testes automatizados de unidade dele.

> [!div class="step-by-step"]
> [Próximo](use-ajax-to-deliver-dynamic-updates.md)
> [anterior](enable-automated-unit-testing.md)
