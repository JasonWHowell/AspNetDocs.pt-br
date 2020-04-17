---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: Use ViewData e implemente as classes de modelo de visualização | Microsoft Docs
author: rick-anderson
description: A etapa 6 mostra como habilitar o suporte para cenários de edição de formulários mais ricos, e também discute duas abordagens que podem ser usadas para passar dados de controladores para visualizações:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541098"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>Usar ViewData e implementar classes ViewModel

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 6 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> A etapa 6 mostra como habilitar o suporte para cenários de edição de formulários mais ricos, e também discute duas abordagens que podem ser usadas para passar dados de controladores para visualizações: ViewData e ViewModel.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>NerdDinner Passo 6: ViewData e ViewModel

Cobrimos uma série de cenários de postagem de formulários e discutimos como implementar o suporte a criar, atualizar e excluir (CRUD). Agora levaremos nossa implementação do DinnersController mais adiante e habilitaremos o suporte para cenários de edição de formulários mais ricos. Ao fazer isso, discutiremos duas abordagens que podem ser usadas para passar dados de controladores para visualizações: ViewData e ViewModel.

### <a name="passing-data-from-controllers-to-view-templates"></a>Passando dados de controladores para modelos de exibição

Uma das características definidoras do padrão MVC é a estrita "separação de preocupações" que ajuda a impor entre os diferentes componentes de uma aplicação. Modelos, Controladores e Views cada um tem papéis e responsabilidades bem definidos, e eles se comunicam entre si de maneiras bem definidas. Isso ajuda a promover a testabilidade e a reutilização do código.

Quando uma classe Controller decide renderizar uma resposta HTML de volta a um cliente, ela é responsável por passar explicitamente para o modelo de exibição todos os dados necessários para renderizar a resposta. Os modelos de exibição nunca devem executar qualquer recuperação de dados ou lógica de aplicativo – e, em vez disso, devem limitar-se a ter apenas um código de renderização que é expulso do modelo/dados passados a ele pelo controlador.

No momento, os dados do modelo que estão sendo passados pela nossa classe DinnersController para nossos modelos de exibição são simples e diretos – uma lista de objetos de Jantar no caso de Index(), e um único objeto Dinner no caso de Detalhes(), Editar(), Criar() e Excluir(). À medida que adicionamos mais recursos de interface do motorista ao nosso aplicativo, muitas vezes vamos precisar passar mais do que apenas esses dados para renderizar respostas HTML em nossos modelos de exibição. Por exemplo, podemos querer alterar o campo "País" em nossa Edição e Criar visualizações de ser uma caixa de texto HTML para uma lista de estíope. Em vez de codificar a lista suspensa de nomes de países no modelo de exibição, podemos querer gerá-la a partir de uma lista de países apoiados que povoamos dinamicamente. Precisaremos de uma maneira de passar tanto o objeto Dinner *quanto* a lista de países suportados do nosso controlador para nossos modelos de visão.

Vamos ver duas maneiras de conseguir isso.

### <a name="using-the-viewdata-dictionary"></a>Usando o Dicionário ViewData

A classe base do Controller expõe uma propriedade de dicionário "ViewData" que pode ser usada para passar itens de dados adicionais de Controladores para Visualizações.

Por exemplo, para apoiar o cenário em que queremos alterar a caixa de texto "País" em nossa exibição Editar de ser uma caixa de texto HTML para uma lista de paradas, podemos atualizar nosso método de ação Edit() para passar (além de um objeto Jantar) um objeto SelectList que pode ser usado como modelo de uma lista de estífica de países.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

O construtor da SelectList acima está aceitando uma lista de condados para preencher a lista de baixa sacada, bem como o valor selecionado no momento.

Podemos então atualizar nosso modelo de exibição Edit.aspx para usar o método de ajuda Html.DropDownList() em vez do método de ajuda Html.TextBox() que usamos anteriormente:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

O método de ajuda Html.DropDownList() acima leva dois parâmetros. O primeiro é o nome do elemento de forma HTML para saída. O segundo é o modelo "SelectList" que passamos através do dicionário ViewData. Estamos usando a palavra-chave C# "as" para lançar o tipo dentro do dicionário como uma SelectList.

E agora, quando executarmos nosso aplicativo e acessarmos a URL */Dinners/Edit/1* dentro do nosso navegador, veremos que nossa interface do usuário foi atualizada para exibir uma lista de estíoques de países em vez de uma caixa de texto:

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

Como também renderizamos o modelo de exibição De edição do método HTTP-POST Edit (em cenários em que ocorrem erros), queremos ter certeza de que também atualizamos esse método para adicionar a SelectList to ViewData quando o modelo de exibição for renderizado em cenários de erro:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

E agora nosso cenário de edição dinnersController suporta uma Lista de DropDown.

### <a name="using-a-viewmodel-pattern"></a>Usando um padrão de modelo de exibição

A abordagem do dicionário ViewData tem o benefício de ser bastante rápida e fácil de implementar. Alguns desenvolvedores não gostam de usar dicionários baseados em strings, porém, uma vez que erros de digitação podem levar a erros que não serão pegos no momento da compilação. O dicionário ViewData não digitado também requer o uso do operador "as" ou do casting ao usar uma linguagem fortemente digitada como C# em um modelo de exibição.

Uma abordagem alternativa que poderíamos usar é muitas vezes referida como o padrão "ViewModel". Ao usar esse padrão, criamos classes fortemente digitadas que são otimizadas para nossos cenários de exibição específicos e que expõem propriedades para os valores dinâmicos/conteúdo necessários por nossos modelos de exibição. Nossas classes de controladorpodem então preencher e passar essas classes otimizadas para o nosso modelo de exibição para usar. Isso permite a segurança do tipo, a verificação de tempo de compilação e o intellisense do editor dentro de modelos de exibição.

Por exemplo, para ativar cenários de edição de formulários de jantar, podemos criar uma classe "DinnerFormViewModel" como abaixo que expõe duas propriedades fortemente digitadas: um objeto Dinner e o modelo SelectList necessário para preencher a lista de itens de lista de itens:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

Podemos então atualizar nosso método de ação Edit() para criar o DinnerFormViewModel usando o objeto Dinner que recuperamos do nosso repositório e, em seguida, passá-lo para o nosso modelo de exibição:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

Em seguida, atualizaremos nosso modelo de exibição para que ele espere um "DinnerFormViewModel" em vez de um objeto "Jantar" alterando o atributo "herda" na parte superior da página edit.aspx assim:

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

Uma vez que fizermos isso, o intellisense da propriedade "Model" dentro do nosso modelo de exibição será atualizado para refletir o modelo de objeto do tipo DinnerFormViewModel que estamos passando:

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

Podemos então atualizar nosso código de exibição para trabalhar fora dele. Observe abaixo como não estamos alterando os nomes dos elementos de entrada que estamos criando (os elementos de formulário ainda serão chamados de "Título", "País") – mas estamos atualizando os métodos do Ajudador HTML para recuperar os valores usando a classe DinnerFormViewModel:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

Também atualizaremos nosso método editar post para usar a classe DinnerFormViewModel ao renderizar erros:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

Também podemos atualizar nossos métodos de ação Create() para reutilizar exatamente a mesma classe *DinnerFormViewModel* para habilitar os países DropDownList dentro deles também. Abaixo está a implementação HTTP-GET:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

Abaixo está a implementação do método HTTP-POST Create:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

E agora nossas telas Edit e Create suportam listas de baixa para escolher o país.

### <a name="custom-shaped-viewmodel-classes"></a>Classes de ViewModel em forma personalizada

No cenário acima, nossa classe DinnerFormViewModel expõe diretamente o objeto modelo Dinner como uma propriedade, juntamente com uma propriedade de modelo SelectList de suporte. Essa abordagem funciona bem para cenários onde a UI HTML que queremos criar dentro do nosso modelo de exibição corresponde relativamente perto aos nossos objetos de modelo de domínio.

Para cenários em que este não é o caso, uma opção que você pode usar é criar uma classe ViewModel em forma personalizada cujo modelo de objeto é mais otimizado para consumo pela visualização – e que pode parecer completamente diferente do objeto modelo de domínio subjacente. Por exemplo, ele poderia potencialmente expor diferentes nomes de propriedade e/ou propriedades agregadas coletadas de vários objetos de modelo.

As classes ViewModel em forma personalizada podem ser usadas tanto para passar dados de controladores para visualizações para renderização, quanto para ajudar a lidar com dados de formulário saem do método de ação de um controlador. Para este cenário posterior, você pode fazer com que o método de ação atualize um objeto ViewModel com os dados publicados no formulário e, em seguida, use a instância ViewModel para mapear ou recuperar um objeto de modelo de domínio real.

As classes ViewModel em forma personalizada podem fornecer uma grande flexibilidade, e são algo para investigar sempre que você encontrar o código de renderização dentro de seus modelos de visualização ou o código de postagem de formulário dentro de seus métodos de ação começando a ficar muito complicado. Isso é frequentemente um sinal de que seus modelos de domínio não correspondem limpamente à ui que você está gerando, e que uma classe intermediária em forma de ViewModel pode ajudar.

### <a name="next-step"></a>Próxima etapa

Vamos agora ver como podemos usar parciais e páginas-mestre para reutilizar e compartilhar interface do iu em nosso aplicativo.

> [!div class="step-by-step"]
> [Próximo](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [anterior](re-use-ui-using-master-pages-and-partials.md)
