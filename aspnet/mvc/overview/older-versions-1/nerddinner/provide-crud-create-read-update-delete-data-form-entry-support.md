---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: Fornecer suporte de entrada de formulário de dados CRUD (Criar, Ler, Atualizar, Excluir) Microsoft Docs
author: rick-anderson
description: O passo 5 mostra como levar nossa aula de DinnersController mais adiante, habilitando o suporte para edição, criação e exclusão de jantares com ela também.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542619"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>Fornecer suporte de CRUD (criar, ler, atualizar e excluir) ao formulário de entrada de dados

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 5 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O passo 5 mostra como levar nossa aula de DinnersController mais adiante, habilitando o suporte para edição, criação e exclusão de jantares com ela também.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner Passo 5: Criar, atualizar, excluir cenários de formulário

Nós introduzimos controladores e visualizações, e cobrimos como usá-los para implementar uma experiência de listagem/detalhes para jantares no local. Nosso próximo passo será levar nossa aula de DinnersController mais adiante e permitir suporte para edição, criação e exclusão de jantares com ela também.

### <a name="urls-handled-by-dinnerscontroller"></a>URLs manipulados por DinnersController

Anteriormente, adicionamos métodos de ação ao DinnersController que implementou suporte para dois URLs: */Dinners* e */Dinners/Details/[id]*.

| **URL** | **Verbo** | **Finalidade** |
| --- | --- | --- |
| */Jantares/* | GET | Exibir uma lista HTML dos próximos jantares. |
| */Jantares/Detalhes/[id]* | GET | Exiba detalhes sobre um jantar específico. |

Agora adicionaremos métodos de ação para implementar três URLs adicionais: */Dinners/Edit/[id]*, */Dinners/Create*e */Dinners/Delete/[id]*. Esses URLs permitirão o suporte para editar jantares existentes, criar novos jantares e excluir jantares.

Suportaremos interações de verbos HTTP GET e HTTP POST com esses novos URLs. HTTP GET solicitações a essas URLs exibirão a exibição inicial html dos dados (um formulário preenchido com os dados do Jantar no caso de "editar", um formulário em branco no caso de "criar" e uma tela de confirmação de exclusão no caso de "excluir"). As solicitações HTTP POST para essas URLs salvarão/atualizarão/excluirão os dados do Jantar em nosso DinnerRepository (e de lá para o banco de dados).

| **URL** | **Verbo** | **Finalidade** |
| --- | --- | --- |
| */Jantares/Editar/[id]* | GET | Exibir um formulário HTML editável preenchido com dados do Jantar. |
| POST | Guarde as alterações de formulário para um jantar específico no banco de dados. |
| */Jantares/Criar* | GET | Exibir um formulário HTML vazio que permite que os usuários definam novos Jantares. |
| POST | Crie um novo jantar e salve-o no banco de dados. |
| */Jantares/Exclusão/[id]* | GET | Exibir tela de confirmação de exclusão. |
| POST | Exclui o jantar especificado do banco de dados. |

### <a name="edit-support"></a>Editar suporte

Vamos começar implementando o cenário de "editar".

#### <a name="the-http-get-edit-action-method"></a>O método de ação de edição HTTP-GET

Começaremos implementando o comportamento HTTP "GET" do nosso método de ação de edição. Este método será invocado quando a URL */Dinners/Edit/[id]* for solicitada. Nossa implementação será como:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

O código acima usa o DinnerRepository para recuperar um objeto Dinner. Em seguida, ele renderiza um modelo de exibição usando o objeto Jantar. Como não passamos explicitamente um nome de modelo para o método de ajuda *Exibir(),* ele usará o caminho padrão baseado em convenção para resolver o modelo de exibição: /Views/Dinners/Edit.aspx.

Vamos agora criar este modelo de exibição. Faremos isso clicando com o botão direito do mouse no método Editar e selecionando o comando menu de contexto "Add View":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

Dentro da caixa de diálogo "Adicionar exibição", vamos indicar que estamos passando um objeto jantar para o nosso modelo de exibição como seu modelo, e optar por um modelo de "Editar" automaticamente:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

Quando clicarmos no botão "Adicionar", o Visual Studio adicionará um novo arquivo de modelo de exibição "Edit.aspx" para nós dentro do diretório "\Views\Dinners". Ele também abrirá o novo modelo de exibição "Edit.aspx" dentro do editor de código – preenchido com uma implementação inicial de andaimes "Editar" como abaixo:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

Vamos fazer algumas alterações no andaime padrão de "editar" gerado e atualizar o modelo de exibição de edição para ter o conteúdo abaixo (que remove algumas das propriedades que não queremos expor):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

Quando executarmos o aplicativo e solicitarmos a URL *"/Dinners/Edit/1",* veremos a seguinte página:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

A marcação HTML gerada pela nossa visão parece abaixo. É html padrão – &lt;&gt; com um elemento de formulário que executa um POST HTTP &lt;para a URL */Dinners/Edit/1* quando o tipo de entrada "Salvar"="enviar"/&gt; é pressionado. Um &lt;tipo de entrada HTML="texto"/&gt; elemento foi produzido para cada propriedade editável:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() e Html.TextBox() Métodos de ajuda html

Nosso modelo de exibição "Edit.aspx" está usando vários métodos "Html Helper": Html.ValidationSummary(), Html.BeginForm(), Html.TextBox() e Html.ValidationMessage(). Além de gerar marcação HTML para nós, esses métodos auxiliares fornecem suporte de manipulação e validação de erros incorporados.

##### <a name="htmlbeginform-helper-method"></a>Método auxiliar html.BeginForm()

O método de ajuda Html.BeginForm() &lt;é&gt; o que produz o elemento de forma HTML em nossa marcação. Em nosso modelo de exibição Edit.aspx, você notará que estamos aplicando uma declaração C# "usando" ao usar este método. A cinta encaracolada aberta &lt;indica&gt; o início do conteúdo do formulário, e &lt;a&gt; cinta encaracolada de fechamento é o que indica o fim do elemento /form:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

Alternativamente, se você encontrar a abordagem de declaração "usando" não natural para um cenário como este, você pode usar uma combinação Html.BeginForm() e Html.EndForm() (que faz a mesma coisa):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

Chamar Html.BeginForm() sem quaisquer parâmetros fará com que ele produza um elemento de formulário que faça um HTTP-POST na URL da solicitação atual. É por isso que nossa exibição Editar gera um * &lt;método action="/Dinners/Edit/1" method="post".&gt; * Poderíamos ter passado parâmetros explícitos para Html.BeginForm() se quiséssemos postar em uma URL diferente.

##### <a name="htmltextbox-helper-method"></a>Método de ajuda html.TextBox()

Nossa exibição Edit.aspx usa o método de ajuda &lt;Html.TextBox()&gt; para output input type="text"/ elementos:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

O método Html.TextBox() acima leva um único parâmetro – que está sendo usado &lt;para especificar tanto&gt; os atributos de id/nome do tipo de entrada="texto"/ elemento para saída, quanto a propriedade modelo para preencher o valor da caixa de texto. Por exemplo, o objeto Jantar que passamos para a exibição Editar tinha um valor de propriedade "Título" de "Futuros de NET", e assim nossa saída de chamada do método Html.TextBox("Título"): * &lt;entrada id="Title" nome="Title" type="text" value=".NET Futures" / .&gt;*

Alternativamente, podemos usar o primeiro parâmetro Html.TextBox() para especificar o id/nome do elemento e, em seguida, passar explicitamente no valor para usar como um segundo parâmetro:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

Muitas vezes, queremos executar formatação personalizada no valor que é a saída. O método estático String.Format() incorporado ao .NET é útil para esses cenários. Nosso modelo de exibição Edit.aspx está usando isso para formatar o valor EventDate (que é do tipo DateTime) para que ele não apareça segundos para o tempo:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Um terceiro parâmetro para Html.TextBox() pode ser usado opcionalmente para produzir atributos HTML adicionais. O trecho de código abaixo demonstra como renderizar um atributo adicional de tamanho="30" e &lt;um atributo class="mycssclass" no elemento tipo de entrada="texto"/&gt; element. Note como estamos escapando do nome do@" character because "atributo de classe usando uma " classe" é uma palavra-chave reservada em C#:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>Implementação do método de ação de edição HTTP-POST

Agora temos a versão HTTP-GET do nosso método de ação Editar implementado. Quando um usuário solicita a URL */Dinners/Edit/1,* ele recebe uma página HTML como a seguinte:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

Pressionar o botão "Salvar" faz com que uma postagem de formulário para &lt;&gt; a URL */Dinners/Edit/1* e envie os valores do formulário de entrada HTML usando o verbo HTTP POST. Vamos agora implementar o comportamento HTTP POST do nosso método de ação de edição – que lidará com a salvação do Jantar.

Começaremos adicionando um método de ação "Editar" sobrecarregado ao nosso DinnersController que tem um atributo "AcceptVerbs" nele que indica que ele lida com cenários HTTP POST:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

Quando o atributo [AcceptVerbs] é aplicado a métodos de ação sobrecarregados, ASP.NET MVC lida automaticamente com solicitações de expedição para o método de ação apropriado, dependendo do verbo HTTP de entrada. As solicitações HTTP POST para */Dinners/Edit/[id]* URLs irão para o método de edição acima, enquanto todas as outras solicitações de verbo HTTP `[AcceptVerbs]` para */Dinners/Edit/[id]* URLs irão para o primeiro método de edição que implementamos (que não tinha um atributo).

| **Tópico Lateral: Por que diferenciar através de verbos HTTP?** |
| --- |
| Você pode perguntar – por que estamos usando uma única URL e diferenciando seu comportamento através do verbo HTTP? Por que não ter apenas duas URLs separadas para lidar com as alterações de edição de carregamento e salvamento? Por exemplo: /Dinners/Edit/[id] para exibir o formulário inicial e /Jantares/Salvar/[id] para lidar com o post de formulário para salvá-lo? A desvantagem com a publicação de duas URLs separadas é que nos casos em que postamos para /Dinners/Save/2 e, em seguida, precisamos reexibir o formulário HTML por causa de um erro de entrada, o usuário final acabará tendo a URL /Dinners/Save/2 na barra de endereços do navegador (já que essa era a URL que o formulário postou). Se o usuário final marcar essa página reexibida na lista de favoritos do navegador ou copiar/colar a URL e enviar e-mails para um amigo, eles acabarão salvando uma URL que não funcionará no futuro (já que essa URL depende dos valores de postagem). Ao expor uma única URL (como: /Dinners/Edit/[id]) e diferenciar o processamento dele pelo verbo HTTP, é seguro para os usuários finais marcar a página de edição e/ou enviar a URL para outros. |

#### <a name="retrieving-form-post-values"></a>Recuperando valores de pós-formulário

Há uma variedade de maneiras que podemos acessar parâmetros de formulário postados dentro do nosso método HTTP POST "Editar". Uma abordagem simples é apenas usar a propriedade Solicitar na classe base do Controlador para acessar a coleta do formulário e recuperar os valores postados diretamente:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

A abordagem acima é um pouco verbosa, especialmente quando adicionamos lógica de manipulação de erros.

Uma abordagem melhor para este cenário é aproveitar o método de ajuda *built-in UpdateModel()* na classe base controller. Ele suporta a atualização das propriedades de um objeto que passamos usando os parâmetros de formulário de entrada. Ele usa a reflexão para determinar os nomes de propriedade no objeto e, em seguida, converte e atribui automaticamente valores a eles com base nos valores de entrada enviados pelo cliente.

Poderíamos usar o método UpdateModel() para simplificar nossa Ação de Edição HTTP-POST usando este código:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

Agora podemos visitar a URL */Dinners/Edit/1* e alterar o título do nosso Jantar:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

Quando clicarmos no botão "Salvar", executaremos uma postagem de formulário para nossa ação Editar, e os valores atualizados serão persistidos no banco de dados. Em seguida, seremos redirecionados para a URL Detalhes para o Jantar (que exibirá os valores recém-salvos):

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>Manipulação de erros de edição

Nossa implementação HTTP-POST atual funciona bem – exceto quando há erros.

Quando um usuário comete um erro ao editar um formulário, precisamos ter certeza de que o formulário é reexibido com uma mensagem de erro informativa que os orienta a corrigi-lo. Isso inclui casos em que um usuário final publica entrada incorreta (por exemplo: uma seqüência de datamalformada), bem como casos em que o formato de entrada é válido, mas há uma violação de regra de negócios. Quando ocorrem erros, o formulário deve preservar os dados de entrada inseridos originalmente pelo usuário para que não precise recarregar suas alterações manualmente. Este processo deve repetir quantas vezes for necessário até que o formulário seja concluído com sucesso.

ASP.NET MVC inclui alguns recursos embutidos agradáveis que facilitam o manuseio de erros e a forma de reexibição fácil. Para ver esses recursos em ação, vamos atualizar nosso método de ação Editar com o seguinte código:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

O código acima é semelhante à nossa implementação anterior – exceto que agora estamos embrulhando um bloco de manipulação de erro de tentativa/captura em torno de nosso trabalho. Se uma exceção ocorrer ao chamar UpdateModel(), ou quando tentarmos salvar o DinnerRepository (que abrirá uma exceção se o objeto Dinner que estamos tentando salvar for inválido por causa de uma violação de regra dentro do nosso modelo), nosso bloqueio de manipulação de erros de captura será executado. Dentro dele, fazemos loop sobre quaisquer violações de regras que existem no objeto Jantar e adicioná-las a um objeto ModelState (que discutiremos em breve). Em seguida, reexibimos a vista.

Para ver isso funcionando, vamos reexecutar o aplicativo, editar um jantar e alterá-lo para ter um título vazio, uma data de evento de "BOGUS", e usar um número de telefone do Reino Unido com um valor de país dos EUA. Quando pressionarmos o botão "Salvar" nosso método HTTP POST Edit não será capaz de salvar o Jantar (porque há erros) e reexibirá o formulário:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

Nossa aplicação tem uma experiência de erro decente. Os elementos de texto com a entrada inválida são destacados em vermelho, e as mensagens de erro de validação são exibidas ao usuário final sobre elas. O formulário também está preservando os dados de entrada que o usuário inseriu originalmente – para que eles não precisem reabastecer nada.

Como, você pode perguntar, isso ocorreu? Como as caixas de texto Title, EventDate e ContactPhone se destacaram em vermelho e sabem como produzir os valores de usuário inseridos originalmente? E como as mensagens de erro foram exibidas na lista no topo? A boa notícia é que isso não ocorreu por magia - pelo contrário, foi porque usamos alguns dos recursos embutidos ASP.NET MVC que facilitam a validação de entrada e o manuseio de erros.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>Entendendo o ModelState e os métodos de ajuda html de validação

As classes de controladortêm uma coleção de propriedades "ModelState" que fornece uma maneira de indicar que existem erros com um objeto modelo sendo passado para uma exibição. As entradas de erro na coleção ModelState identificam o nome da propriedade modelo com o problema (por exemplo: "Título", "Data de evento" ou "ContactPhone"), e permitem que uma mensagem de erro amigável ao homem seja especificada (por exemplo: "Título é necessário").

O método de ajuda *UpdateModel()* preenche automaticamente a coleção ModelState quando encontra erros ao tentar atribuir valores de formulário às propriedades do objeto modelo. Por exemplo, a propriedade EventDate do nosso objeto Jantar é do tipo DateTime. Quando o método UpdateModel() não foi capaz de atribuir o valor de string "BOGUS" a ele no cenário acima, o método UpdateModel() adicionou uma entrada à coleção ModelState indicando que um erro de atribuição havia ocorrido com essa propriedade.

Os desenvolvedores também podem escrever código para adicionar explicitamente entradas de erro na coleção ModelState como estamos fazendo abaixo dentro do nosso bloco de manipulação de erros "catch", que está povoando a coleção ModelState com entradas baseadas nas violações de regras ativas no objeto Jantar:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>Integração do Ajudante html com modelstate

Métodos de ajuda HTML - como Html.TextBox() - verifique maquinam a coleção ModelState ao renderizar a saída. Se houver um erro para o item, ele renderiza rá o valor inserido pelo usuário e uma classe de erro CSS.

Por exemplo, em nossa exibição "Editar", estamos usando o método de ajuda Html.TextBox() para renderizar o EventDate do nosso objeto Jantar:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

Quando a exibição foi renderizada no cenário de erro, o método Html.TextBox() verificou a coleção ModelState para ver se havia algum erro associado à propriedade "EventDate" do nosso objeto Jantar. Quando determinou que houve um erro, tornou a entrada do usuário submetida ("BOGUS") como o &lt;valor e adicionou&gt; uma classe de erro css ao tipo de entrada="caixa de texto"/ marcação que gerou:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

Você pode personalizar a aparência da classe de erro css para olhar como quiser. A classe de erro CSS padrão – "input-validation-error" – é definida na planilha de estilos *\content\site\css* e parece abaixo:

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

Esta regra CSS é o que fez com que nossos elementos de entrada inválidos fossem destacados como abaixo:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Método de ajuda html.validationMessage()

O método de ajuda Html.ValidationMessage() pode ser usado para produzir a mensagem de erro ModelState associada a uma determinada propriedade do modelo:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

As saídas de código acima: * &lt;span class="field-validation-error"&gt; &lt;O valor 'BOGUS' é inválido /span&gt;*

O método de ajuda Html.ValidationMessage() também suporta um segundo parâmetro que permite aos desenvolvedores substituir a mensagem de texto de erro exibida:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

As saídas de código acima: * &lt;span class="field-validation-error"&gt;\*&lt;/span&gt; * em vez do texto de erro padrão quando um erro está presente na propriedade EventDate.

##### <a name="htmlvalidationsummary-helper-method"></a>Método auxiliar html.ValidationSummary()

O método de ajuda Html.ValidationSummary() pode ser usado para renderizar &lt;uma&gt;&lt;mensagem de erro de resumo, acompanhada de uma lista ul li/&gt;&lt;/ul&gt; de todas as mensagens de erro detalhadas na coleção ModelState:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

O método de ajuda Html.ValidationSummary() requer um parâmetro de seqüência opcional – que define uma mensagem de erro de resumo para exibir acima da lista de erros detalhados:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

Você pode usar css opcionalmente para substituir como a lista de erros se parece.

#### <a name="using-a-addruleviolations-helper-method"></a>Usando um método auxiliar addruleviolações

Nossa implementação inicial http-post edit usou uma declaração forcada dentro de seu bloco de captura para loop sobre as Violações de Regras do objeto Jantar e adicioná-las à coleção ModelState do controlador:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

Podemos tornar esse código um pouco mais limpo adicionando uma classe "ControllerHelpers" ao projeto NerdDinner e implementar um método de extensão "AddRuleViolations" dentro dele que adiciona um método auxiliar à classe ASP.NET MVC ModelStateDictionary. Este método de extensão pode encapsular a lógica necessária para preencher o ModelStateDictionary com uma lista de erros de Violação de Regras:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

Podemos então atualizar nosso método de ação HTTP-POST Edit para usar este método de extensão para preencher a coleção ModelState com nossas Violações de Regras do Jantar.

#### <a name="complete-edit-action-method-implementations"></a>Implementações completas do método de ação de edição

O código abaixo implementa toda a lógica do controlador necessária para o nosso cenário de Edição:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

O bom da nossa implementação do Edit é que nem a nossa classe Controller nem o nosso modelo de Visualização devem saber nada sobre a validação específica ou as regras de negócios que estão sendo aplicadas pelo nosso modelo de Jantar. Podemos adicionar regras adicionais ao nosso modelo no futuro e não temos que fazer nenhuma alteração de código em nosso controlador ou exibição para que eles sejam suportados. Isso nos dá flexibilidade para evoluir facilmente nossos requisitos de aplicativos no futuro com um mínimo de mudanças de código.

### <a name="create-support"></a>Criar suporte

Terminamos de implementar o comportamento "Editar" da nossa classe DinnersController. Vamos agora implementar o suporte "Criar" nele – o que permitirá que os usuários adicionem novos Jantares.

#### <a name="the-http-get-create-action-method"></a>O método de ação HTTP-GET Create

Começaremos implementando o comportamento HTTP "GET" do nosso método de ação de criação. Esse método será chamado quando alguém visitar a *URL /Dinners/Create.* Nossa implementação parece:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

O código acima cria um novo objeto Dinner e atribui que sua propriedade EventDate seja uma semana no futuro. Em seguida, torna uma exibição baseada no novo objeto Dinner. Como não passamos explicitamente um nome para o método de ajuda *View(),* ele usará o caminho padrão baseado em convenção para resolver o modelo de exibição: /Views/Dinners/Create.aspx.

Vamos agora criar este modelo de exibição. Podemos fazer isso clicando com o botão direito do mouse dentro do método criar ação e selecionando o comando menu de contexto "Adicionar exibição". Na caixa de diálogo "Adicionar exibição", vamos indicar que estamos passando um objeto jantar para o modelo de exibição e optar por um modelo "Criar" de "Criar":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

Quando clicamos no botão "Adicionar", o Visual Studio salvará uma nova exibição "Create.aspx" baseada em andaimes no diretório "\Views\Dinners" e abrirá-a dentro do IDE:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

Vamos fazer algumas alterações no arquivo padrão de andaime "criar" que foi gerado para nós e modificá-lo para parecer abaixo:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

E agora, quando executarmos nosso aplicativo e acessarmos a URL *"/Dinners/Create"* dentro do navegador, ela renderizará a interface do usuário como abaixo da nossa implementação de ação Criar:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>Implementando o método de ação http-post create

Temos a versão HTTP-GET do nosso método de ação Create implementado. Quando um usuário clica no botão "Salvar", ele executa uma postagem de &lt;formulário&gt; para a *URL /Dinners/Create* e envia os valores do formulário de entrada HTML usando o verbo HTTP POST.

Vamos agora implementar o comportamento HTTP POST do nosso método de ação de criação. Começaremos adicionando um método de ação "Criar" sobrecarregado ao nosso DinnersController que tem um atributo "AcceptVerbs" nele que indica que ele lida com cenários HTTP POST:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

Há uma variedade de maneiras pelas quais podemos acessar os parâmetros de formulário postados dentro do nosso método "Criar" ativado pelo HTTP-POST.

Uma abordagem é criar um novo objeto Dinner e, em seguida, usar o método de ajuda *UpdateModel()* (como fizemos com a ação Editar) para preenche-lo com os valores de formulário publicados. Podemos então adicioná-lo ao nosso DinnerRepository, persistir no banco de dados e redirecionar o usuário para nossa ação Detalhes para mostrar o jantar recém-criado usando o código abaixo:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

Alternativamente, podemos usar uma abordagem onde temos nosso método de ação Create() tomar um objeto Jantar como parâmetro de método. ASP.NET MVC, então, instanciar automaticamente um novo objeto dinner para nós, preencher suas propriedades usando os inputs do formulário e passá-lo para o nosso método de ação:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

Nosso método de ação acima verifica se o objeto Dinner foi preenchido com sucesso com os valores de postagem do formulário verificando a propriedade ModelState.IsValid. Isso retornará falso se houver problemas de conversão de entrada (por exemplo: uma seqüência de "BOGUS" para a propriedade EventDate), e se houver quaisquer problemas nosso método de ação reexibirá o formulário.

Se os valores de entrada forem válidos, então o método de ação tentará adicionar e salvar o novo Jantar no DinnerRepository. Ele envolve este trabalho dentro de um bloco de tentativa/captura e reexibe o formulário se houver alguma violação de regra de negócios (o que faria com que o método DinnerRepository.Save() levantasse uma exceção).

Para ver esse comportamento de manipulação de erros em ação, podemos solicitar o *URL /Dinners/Create* e preencher detalhes sobre um novo Jantar. A entrada ou os valores incorretos farão com que o formulário de criação seja reexibido com os erros destacados como abaixo:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

Observe como nosso formulário Criar está honrando exatamente as mesmas regras de validação e negócios que nosso formulário Editar. Isso porque nossas regras de validação e de negócios foram definidas no modelo, e não foram incorporadas na interface do usuário ou controlador do aplicativo. Isso significa que podemos mudar/evoluir mais tarde nossas regras de validação ou de negócios em um único lugar e fazê-los aplicar em toda a nossa aplicação. Não teremos que alterar nenhum código dentro de nossos métodos de ação Editar ou Criar para honrar automaticamente quaisquer novas regras ou modificações nas existentes.

Quando corrigirmos os valores de entrada e clicarmos no botão "Salvar" novamente, nossa adição ao DinnerRepository será bem sucedida, e um novo Jantar será adicionado ao banco de dados. Em seguida, seremos redirecionados para a URL */Dinners/Details/[id]* – onde seremos apresentados com detalhes sobre o recém-criado Jantar:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>Excluir suporte

Vamos agora adicionar suporte "Delete" ao nosso DinnersController.

#### <a name="the-http-get-delete-action-method"></a>O método de ação http-get excluir

Começaremos implementando o comportamento HTTP GET do nosso método de ação de exclusão. Esse método será chamado quando alguém visitar a URL */Dinners/Delete/[id].* Abaixo está a implementação:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

O método de ação tenta recuperar o Jantar para ser excluído. Se o Jantar existir, ele renderiza uma exibição com base no objeto Jantar. Se o objeto não existir (ou já tiver sido excluído), ele retornará uma exibição que renderiza o modelo de exibição "NotFound" que criamos anteriormente para o método de ação "Detalhes".

Podemos criar o modelo de exibição "Excluir" clicando com o botão direito do mouse no método de ação Excluir e selecionando o comando menu de contexto "Adicionar exibição". Dentro da caixa de diálogo "Adicionar exibição", vamos indicar que estamos passando um objeto jantar para o nosso modelo de exibição como seu modelo e optar por criar um modelo vazio:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

Quando clicarmos no botão "Adicionar", o Visual Studio adicionará um novo arquivo de modelo de exibição "Delete.aspx" para nós dentro do nosso diretório "\Views\Dinners". Adicionaremos alguns HTML e código ao modelo para implementar uma tela de confirmação de exclusão como abaixo:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

O código acima exibe o título do Jantar a &lt;ser&gt; excluído e produz um elemento de formulário que faz uma URL DE POST para a URL /Dinners/Delete/[id] se o usuário final clicar no botão "Excluir" dentro dele.

Quando executamos nosso aplicativo e acessamos a URL *"/Dinners/Delete/[id]"* para um objeto de Jantar válido, ele torna a Interface do Usuário como abaixo:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **Tópico Lateral: Por que estamos fazendo um POST?** |
| --- |
| Você pode perguntar – por que passamos &lt;&gt; pelo esforço de criar um formulário dentro da nossa tela de confirmação excluir? Por que não usar um hiperlink padrão para vincular a um método de ação que faça a operação de exclusão real? A razão é porque queremos ter cuidado para proteger contra web-crawlers e mecanismos de busca descobrindo nossos URLs e inadvertidamente fazendo com que os dados sejam excluídos quando eles seguem os links. UrLs baseados em HTTP-GET são considerados "seguros" para que eles acessem/rastreiem, e eles devem não seguir os DO HTTP-POST. Uma boa regra é garantir que você sempre coloque operações destrutivas ou modificadoras de dados por trás das solicitações HTTP-POST. |

#### <a name="implementing-the-http-post-delete-action-method"></a>Implementando o método de ação de exclusão HTTP-POST

Agora temos a versão HTTP-GET do nosso método de ação Delete implementado que exibe uma tela de confirmação de exclusão. Quando um usuário final clica no botão "Excluir", ele executará uma postagem de formulário na URL */Dinners/Dinner/[id].*

Vamos agora implementar o comportamento HTTP "POST" do método de ação de exclusão usando o código abaixo:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

A versão HTTP-POST do nosso método de ação Excluir tenta recuperar o objeto do jantar para excluir. Se ele não conseguir encontrá-lo (porque já foi excluído), ele renderiza nosso modelo "NotFound". Se ele encontrar o Jantar, ele o exclui do DinnerRepository. Em seguida, ele renderiza um modelo "Excluído".

Para implementar o modelo "Excluído", clique com o botão direito do mouse no método de ação e escolha o menu de contexto "Adicionar exibição". Nomearemos nossa exibição "Excluída" e se ele for um modelo vazio (e não pegar um objeto de modelo fortemente digitado). Em seguida, adicionaremos algum conteúdo HTML a ele:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

E agora, quando executarmos nosso aplicativo e acessarmos a URL *"/Dinners/Delete/[id]"* para um objeto de Jantar válido, ele renderizará nossa tela de confirmação do Jantar como abaixo:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

Quando clicarmos no botão "Excluir", ele executará um HTTP-POST na URL */Dinners/Delete/[id],* que excluirá o Jantar do nosso banco de dados e exibirá nosso modelo de exibição "Excluído":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>Segurança de vinculação do modelo

Discutimos duas maneiras diferentes de usar os recursos incorporados de vinculação de modelos de ASP.NET MVC. O primeiro usando o método UpdateModel() para atualizar propriedades em um objeto modelo existente e o segundo usando ASP.NET suporte do MVC para passar objetos de modelo em parâmetros de método de ação. Ambas as técnicas são muito poderosas e extremamente úteis.

Esse poder também traz consigo a responsabilidade. É importante ser sempre paranóico com a segurança ao aceitar qualquer entrada do usuário, e isso também é verdade quando objetos de vinculação para formar entrada. Você deve ter cuidado para sempre codificar quaisquer valores inseridos pelo usuário para evitar ataques de injeção HTML e JavaScript, e ter cuidado com ataques de injeção SQL (nota: estamos usando LINQ para SQL para nossa aplicação, que codifica automaticamente parâmetros para evitar esses tipos de ataques). Você nunca deve confiar apenas na validação do lado do cliente e sempre empregar a validação do lado do servidor para se proteger contra hackers que tentam enviar valores falsos.

Um item de segurança adicional para se certificar de que você pensa ao usar os recursos de vinculação de ASP.NET MVC é o escopo dos objetos que você está vinculando. Especificamente, você quer ter certeza de entender as implicações de segurança das propriedades que você está permitindo ser vinculadas, e certifique-se de que você só permite que essas propriedades que realmente devem ser atualizadas por um usuário final sejam atualizadas.

Por padrão, o método UpdateModel() tentará atualizar todas as propriedades no objeto modelo que correspondem aos valores do parâmetro de formulário de entrada. Da mesma forma, os objetos passados como parâmetros do método de ação também por padrão podem ter todas as suas propriedades definidas através de parâmetros de formulário.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>Bloqueando a vinculação por uso

Você pode bloquear a política de vinculação por uso, fornecendo uma "lista de inclusão" explícita de propriedades que podem ser atualizadas. Isso pode ser feito passando um parâmetro extra de matriz de strings para o método UpdateModel() como abaixo:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

Os objetos passados como parâmetros do método de ação também suportam um atributo [Bind] que permite que uma "lista de incluir" de propriedades permitidas seja especificada como abaixo:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>Bloqueando a vinculação em uma base de tipo

Você também pode bloquear as regras de vinculação por tipo. Isso permite que você especifique as regras de vinculação uma vez e, em seguida, faça com que elas se apliquem em todos os cenários (incluindo cenários de parâmetros de Método de Atualização e Deação) em todos os controladores e métodos de ação.

Você pode personalizar as regras de vinculação por tipo adicionando um atributo [Vincular] em um tipo ou registrando-o no arquivo Global.asax do aplicativo (útil para cenários em que você não possui o tipo). Em seguida, você pode usar as propriedades Incluir e Excluir do atributo Vincular para controlar quais propriedades são vinculáveis para a classe ou interface em particular.

Usaremos essa técnica para a aula de Jantar em nosso aplicativo NerdDinner e adicionaremos um atributo [Bind] a ele que restringe a lista de propriedades vinculáveis ao seguinte:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

Observe que não estamos permitindo que a coleção de RSVPs seja manipulada por meio de vinculação, nem estamos permitindo que as propriedades DinnerID ou HostedBy sejam definidas via vinculação. Por razões de segurança, em vez disso, apenas manipularemos essas propriedades específicas usando código explícito dentro de nossos métodos de ação.

### <a name="crud-wrap-up"></a>CRUD Wrap-Up

ASP.NET MVC inclui uma série de recursos incorporados que ajudam na implementação de cenários de postagem de formulários. Nós usamos uma variedade desses recursos para fornecer suporte crud ui em cima do nosso DinnerRepository.

Estamos usando uma abordagem focada em modelos para implementar nossa aplicação. Isso significa que toda a nossa lógica de validação e regra de negócios é definida dentro da nossa camada de modelo – e não dentro de nossos controladores ou visualizações. Nem nossa classe Controller nem nossos modelos de Visualização sabem nada sobre as regras específicas de negócios que estão sendo aplicadas pela nossa classe modelo Dinner.

Isso manterá nossa arquitetura de aplicativo limpa e facilitará o teste. Podemos adicionar regras de negócios adicionais à nossa camada de modelo no futuro e *não temos que fazer nenhuma alteração de código* em nosso Controlador ou Exibição para que elas sejam suportadas. Isso nos dará muita agilidade para evoluir e mudar nossa aplicação no futuro.

Nosso DinnersController agora habilita as listagens/detalhes do Jantar, bem como criar, editar e excluir suporte. O código completo da classe pode ser encontrado abaixo:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>Próxima etapa

Agora temos o suporte básico crud (Create, Read, Update and Delete) dentro da nossa classe DinnersController.

Vamos agora ver como podemos usar as classes ViewData e ViewModel para habilitar a ui ainda mais rica em nossos formulários.

> [!div class="step-by-step"]
> [Próximo](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [anterior](use-viewdata-and-implement-viewmodel-classes.md)
