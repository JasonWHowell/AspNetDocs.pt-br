---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: Melhorando o desempenho com cache de saída (C#) | Microsoft Docs
author: rick-anderson
description: Neste tutorial, você aprende como pode melhorar drasticamente o desempenho de suas aplicações web ASP.NET MVC aproveitando o cache de saída. Você...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: a6dd43320117e235d12a13aa894302bbc767727c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542710"
---
# <a name="improving-performance-with-output-caching-c"></a>Melhorar o desempenho com o cache de saída (C#)

pela [Microsoft](https://github.com/microsoft)

> Neste tutorial, você aprende como pode melhorar drasticamente o desempenho de suas aplicações web ASP.NET MVC aproveitando o cache de saída. Você aprende a armazenar o resultado retornado de uma ação do controlador para que o mesmo conteúdo não precise ser criado toda vez que um novo usuário invoca a ação.

O objetivo deste tutorial é explicar como você pode melhorar drasticamente o desempenho de um aplicativo mVC ASP.NET aproveitando o cache de saída. O cache de saída permite que você faça o cache do conteúdo retornado por uma ação do controlador. Dessa forma, o mesmo conteúdo não precisa ser gerado toda vez que a mesma ação do controlador é invocada.

Imagine, por exemplo, que seu aplicativo mvc ASP.NET exibe uma lista de registros de banco de dados em uma exibição chamada Index. Normalmente, toda e qualquer vez que um usuário invoca a ação do controlador que retorna a exibição Índice, o conjunto de registros de banco de dados deve ser recuperado do banco de dados executando uma consulta de banco de dados.

Se, por outro lado, você tirar proveito do cache de saída, então você pode evitar executar uma consulta de banco de dados toda vez que qualquer usuário invocar a mesma ação do controlador. A exibição pode ser recuperada do cache em vez de ser regenerada a partir da ação do controlador. O cache permite que você evite realizar trabalhos redundantes no servidor.

## <a name="enabling-output-caching"></a>Ativando o cache de saída

Você habilita o cache de saída adicionando um atributo [OutputCache] a uma ação de controlador individual ou a uma classe inteira de controladores. Por exemplo, o controlador na Listagem 1 expõe uma ação chamada Index(). A saída da ação Index() é armazenada em cache por 10 segundos.

**Listagem 1 – Controladores\HomeController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

Nas versões Beta do ASP.NET MVC, o cache [http://www.MySite.com/](http://www.mysite.com/)de saída não funciona para uma URL como . Em vez disso, você [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)deve inserir uma URL como . 

Na Listagem 1, a saída da ação Index() é armazenada em cache por 10 segundos. Se preferir, você pode especificar uma duração de cache muito maior. Por exemplo, se você quiser armazenar a saída de uma ação do controlador por um dia, então \* você \* pode especificar uma duração de cache de 86400 segundos (60 segundos 60 minutos 24 horas).

Não há garantia de que o conteúdo será armazenado em cache pelo tempo que você especificar. Quando os recursos de memória ficam baixos, o cache começa a despejar conteúdo automaticamente.

O controlador Home na Listagem 1 retorna a exibição Índice na Listagem 2. Não há nada de especial nessa visão. A exibição Índice simplesmente exibe o tempo atual (ver Figura 1).

**Listagem 2 – Views\Home\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**Figura 1 – Exibição de índice em cache**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

Se você invocar a ação Index() várias vezes inserindo a URL /Home/Index na barra de endereços do seu navegador e apertando o botão Atualizar/Recarregar no seu navegador repetidamente, então o tempo exibido pela exibição Índice não mudará por 10 segundos. O mesmo tempo é exibido porque a exibição é armazenada em cache.

É importante entender que a mesma visualização é armazenada em cache para todos que visitam sua aplicação. Qualquer pessoa que invoque a ação Index() receberá a mesma versão em cache da exibição Índice. Isso significa que a quantidade de trabalho que o servidor web deve realizar para atender à exibição Índice é drasticamente reduzida.

A visão na Lista 2 está fazendo algo muito simples. A exibição apenas exibe a hora atual. No entanto, você poderia facilmente armazenar uma exibição que exibe um conjunto de registros de banco de dados. Nesse caso, o conjunto de registros de banco de dados não precisaria ser recuperado do banco de dados toda vez que a ação do controlador que retorna a exibição for invocada. O cache pode reduzir a quantidade de trabalho que seu servidor web e servidor de banco de dados devem realizar.

Não use a &lt;diretiva %@&gt; OutputCache % em uma exibição de MVC. Esta diretiva está sangrando sobre o mundo formulários web e não deve ser usada em uma aplicação mVC ASP.NET.

## <a name="where-content-is-cached"></a>Onde o conteúdo é armazenado em cache

Por padrão, quando você usa o atributo [OutputCache], o conteúdo é armazenado em cache em três locais: o servidor web, quaisquer servidores proxy e o navegador da Web. Você pode controlar exatamente onde o conteúdo é armazenado em cache modificando a propriedade Location do atributo [OutputCache].

Você pode definir a propriedade Localização para qualquer um dos seguintes valores:

> · Qualquer
> 
> · Cliente
> 
> · Jusante
> 
> · Servidor
> 
> · Nenhum
> 
> · Servidore cliente

Por padrão, a propriedade Localização tem o valor Qualquer. No entanto, há situações em que você pode querer fazer cache apenas no navegador ou apenas no servidor. Por exemplo, se você estiver armazenando informações personalizadas para cada usuário, então você não deve armazenar as informações no servidor. Se você estiver exibindo informações diferentes para diferentes usuários, então você deve armazenar as informações apenas no cliente.

Por exemplo, o controlador na Lista 3 expõe uma ação chamada GetName() que retorna o nome de usuário atual. Se Jack entrar no site e invocar a ação GetName(), a ação retorna a string "Hi Jack". Se, posteriormente, Jill entrar no site e invocar a ação GetName(), então ela também receberá a string "Hi Jack". A seqüência é armazenada em cache no servidor web para todos os usuários depois que Jack inicialmente invoca a ação do controlador.

**Listagem 3 – Controladores\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

Provavelmente, o controlador na Lista 3 não funciona da maneira que você deseja. Você não quer exibir a mensagem "Oi Jack" para Jill.

Você nunca deve armazenar conteúdo personalizado no cache do servidor. No entanto, você pode querer armazenar o conteúdo personalizado no cache do navegador para melhorar o desempenho. Se você armazenar conteúdo no navegador e um usuário invocar a mesma ação do controlador várias vezes, então o conteúdo pode ser recuperado do cache do navegador em vez do servidor.

O controlador modificado na Listagem 4 armazena a saída da ação GetName(). No entanto, o conteúdo é armazenado apenas no navegador e não no servidor. Dessa forma, quando vários usuários invocam o método GetName(), cada pessoa obtém seu próprio nome de usuário e não o nome de usuário de outra pessoa.

**Lista 4 – Controladores\UserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

Observe que o atributo [OutputCache] na Listagem 4 inclui uma propriedade De localização definida para o valor OutputCacheLocation.Client. O atributo [OutputCache] também inclui uma propriedade NoStore. A propriedade NoStore é usada para informar servidores proxy e navegador que eles não devem armazenar uma cópia permanente do conteúdo armazenado em cache.

## <a name="varying-the-output-cache"></a>Variando o cache de saída

Em algumas situações, você pode querer versões diferentes em cache do mesmo conteúdo. Imagine, por exemplo, que você está criando uma página de mestre/detalhe. A página-mestre exibe uma lista de títulos de filmes. Quando você clica em um título, você recebe detalhes para o filme selecionado.

Se você armazenar a página de detalhes, os detalhes para o mesmo filme serão exibidos não importa qual filme você clique. O primeiro filme selecionado pelo primeiro usuário será exibido para todos os futuros usuários.

Você pode corrigir esse problema aproveitando a propriedade VaryByParam do atributo [OutputCache]. Essa propriedade permite que você crie diferentes versões em cache do mesmo conteúdo quando um parâmetro de parâmetro de formulário ou parâmetro de seqüência de consultas varia.

Por exemplo, o controlador na Lista 5 expõe duas ações denominadas Master() e Detalhes(). A ação Master() retorna uma lista de títulos do filme e a ação Detalhes() retorna os detalhes para o filme selecionado.

**Lista 5 – Controladores\MoviesController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

A ação Master() inclui uma propriedade VaryByParam com o valor "nenhum". Quando a ação Master() é invocada, a mesma versão armazenada em cache da exibição Master é devolvida. Quaisquer parâmetros de formulário ou parâmetros de seqüência de consulta são ignorados (ver Figura 2).

**Figura 2 – A visão /Filmes/Mestre**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**Figura 3 – A exibição /Filmes/Detalhes**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

A ação Detalhes() inclui uma propriedade VaryByParam com o valor "Id". Quando diferentes valores do parâmetro Id são passados para a ação do controlador, diferentes versões em cache da exibição Detalhes são geradas.

É importante entender que o uso da propriedade VaryByParam resulta em mais cache e não menos. Uma versão em cache diferente da exibição Detalhes é criada para cada versão diferente do parâmetro Id.

Você pode definir a propriedade VaryByParam para os seguintes valores:

> \*= Crie uma versão em cache diferente sempre que um parâmetro de seqüência de formulários ou consultas variar.
> 
> nenhum = Nunca crie diferentes versões em cache
> 
> Lista de parâmetros do ponto e vírgula = Criar diferentes versões em cache sempre que qualquer um dos parâmetros de seqüência de formulários ou consulta na lista varia

## <a name="creating-a-cache-profile"></a>Criando um perfil de cache

Como alternativa à configuração das propriedades do cache de saída modificando propriedades do atributo [OutputCache], você pode criar um perfil de cache no arquivo de configuração web (web.config). Criar um perfil de cache no arquivo de configuração da Web oferece algumas vantagens importantes.

Primeiro, configurando o cache de saída no arquivo de configuração da Web, você pode controlar como o controlador adere ao conteúdo de cache em um local central. Você pode criar um perfil de cache e aplicar o perfil a vários controladores ou ações do controlador.

Em segundo lugar, você pode modificar o arquivo de configuração da Web sem recompilar seu aplicativo. Se você precisar desativar o cache de um aplicativo que já foi implantado para produção, então você pode simplesmente modificar os perfis de cache definidos no arquivo de configuração da Web. Quaisquer alterações no arquivo de configuração da Web serão detectadas automaticamente e aplicadas.

Por exemplo, &lt;a&gt; seção de configuração da Web de cache na Lista 6 define um perfil de cache chamado Cache1Hour. A &lt;seção de&gt; cache &lt;deve&gt; aparecer na seção system.web de um arquivo de configuração web.

**Listagem 6 - Seção de cache para web.config**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

O controlador na Lista 7 ilustra como você pode aplicar o perfil Cache1Hour a uma ação do controlador com o atributo [OutputCache].

**Lista 7 – Controladores\ProfileController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

Se você invocar a ação Índice() exposta pelo controlador na Listagem 7, o mesmo horário será devolvido por 1 hora.

## <a name="summary"></a>Resumo

O cache de saída fornece um método muito fácil de melhorar drasticamente o desempenho de seus ASP.NET aplicativos MVC. Neste tutorial, você aprendeu a usar o atributo [OutputCache] para armazenar em cache a saída de ações do controlador. Você também aprendeu como modificar propriedades do atributo [OutputCache], como as propriedades Duration e VaryByParam para modificar a forma como o conteúdo é armazenado em cache. Finalmente, você aprendeu como definir perfis de cache no arquivo de configuração da Web.

> [!div class="step-by-step"]
> [Próximo](understanding-action-filters-cs.md)
> [anterior](adding-dynamic-content-to-a-cached-page-cs.md)
