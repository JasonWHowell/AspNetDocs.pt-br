---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
title: 'Iteração #7 – Adicionar funcionalidade Ajax (C#) | Microsoft Docs'
author: rick-anderson
description: Na sétima iteração, melhoramos a capacidade de resposta e o desempenho de nossa aplicação adicionando suporte ao Ajax.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1b0809e-8909-444e-b6bb-a5cd1dea3f72
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
msc.type: authoredcontent
ms.openlocfilehash: 12d7348382bc55af049567922bd6963970a9421b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542307"
---
# <a name="iteration-7--add-ajax-functionality-c"></a>Iteração nº 7 – adicionar funcionalidade do Ajax (C#)

pela [Microsoft](https://github.com/microsoft)

[Código de download](iteration-7-add-ajax-functionality-cs/_static/contactmanager_7_cs1.zip)

> Na sétima iteração, melhoramos a capacidade de resposta e o desempenho de nossa aplicação adicionando suporte ao Ajax.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Construindo um aplicativo mvc de gerenciamento de ASP.NET de contato (C#)

Nesta série de tutoriais, construímos todo um aplicativo de Gerenciamento de Contatos do início ao fim. O aplicativo Contact Manager permite que você armazene informações de contato - nomes, números de telefone e endereços de e-mail - para uma lista de pessoas.

Nós construímos o aplicativo sobre várias iterações. A cada iteração, melhoramos gradualmente a aplicação. O objetivo desta abordagem de iteração múltipla é permitir que você entenda a razão de cada mudança.

- Iteração #1 - Crie o aplicativo. Na primeira iteração, criamos o Contact Manager da maneira mais simples possível. Adicionamos suporte para operações básicas de banco de dados: Criar, Ler, Atualizar e Excluir (CRUD).

- Iteração #2 - Faça a aplicação parecer bonita. Nesta iteração, melhoramos a aparência do aplicativo modificando o padrão ASP.NET página-mestre de exibição mVC e folha de estilo em cascata.

- Iteração #3 - Adicionar validação de formulário. Na terceira iteração, adicionamos validação de formulário básico. Impedimos que as pessoas enviem um formulário sem preencher os campos de formulário necessários. Também validamos endereços de e-mail e números de telefone.

- Iteração #4 - Faça a aplicação livremente acoplada. Nesta quarta iteração, aproveitamos vários padrões de design de software para facilitar a manutenção e modificação do aplicativo Contact Manager. Por exemplo, refatoramos nossa aplicação para usar o padrão repositório e o padrão de injeção de dependência.

- Iteração #5 - Crie testes unitários. Na quinta iteração, tornamos nossa aplicação mais fácil de manter e modificar adicionando testes unitários. Zombamos de nossas classes de modelo de dados e construímos testes unitários para nossos controladores e lógica de validação.

- Iteração #6 - Use o desenvolvimento orientado para o teste. Nesta sexta iteração, adicionamos nova funcionalidade ao nosso aplicativo escrevendo primeiro testes de unidade e escrevendo código satisfaz os testes da unidade. Nesta iteração, adicionamos grupos de contato.

- Iteração #7 - Adicionar funcionalidade Ajax. Na sétima iteração, melhoramos a capacidade de resposta e o desempenho de nossa aplicação adicionando suporte ao Ajax.

## <a name="this-iteration"></a>Esta Iteração

Nesta iteração do aplicativo Contact Manager, refatoramos nosso aplicativo para fazer uso do Ajax. Aproveitando o Ajax, tornamos nossa aplicação mais responsiva. Podemos evitar renderizar uma página inteira quando precisamos atualizar apenas uma determinada região em uma página.

Vamos refatorar nossa visão de Índice para que não precisemos reexibir a página inteira sempre que alguém selecionar um novo grupo de contato. Em vez disso, quando alguém clica em um grupo de contatos, vamos atualizar a lista de contatos e deixar o resto da página em paz.

Também mudaremos a forma como nosso link de exclusão funciona. Em vez de exibir uma página de confirmação separada, exibiremos uma caixa de confirmação JavaScript. Se você confirmar que deseja excluir um contato, uma operação HTTP DELETE será realizada contra o servidor para excluir o registro de contato do banco de dados.

Além disso, aproveitaremos o jQuery para adicionar efeitos de animação à nossa exibição de Índice. Exibiremos uma animação quando a nova lista de contatos estiver sendo buscada no servidor.

Finalmente, aproveitaremos o suporte ASP.NET a estrutura AJAX para gerenciar o histórico do navegador. Criaremos pontos de histórico sempre que realizarmos uma chamada do Ajax para atualizar a lista de contatos. Dessa forma, os botões para trás e para frente do navegador funcionarão.

## <a name="why-use-ajax"></a>Por que usar a Jax?

Usar o Ajax tem muitos benefícios. Primeiro, adicionar a funcionalidade do Ajax a um aplicativo resulta em uma melhor experiência do usuário. Em um aplicativo web normal, toda a página deve ser postada de volta ao servidor toda vez que um usuário executa uma ação. Sempre que você executar uma ação, o navegador bloqueia e o usuário deve esperar até que toda a página seja buscada e reexibida.

Esta seria uma experiência inaceitável no caso de um aplicativo de desktop. Mas, tradicionalmente, convivemos com essa má experiência de usuário no caso de um aplicativo web porque não sabíamos que poderíamos fazer melhor. Pensamos que era uma limitação das aplicações web quando, na verdade, era apenas uma limitação de nossa imaginação.

Em um aplicativo Ajax, você não precisa parar a experiência do usuário apenas para atualizar uma página. Em vez disso, você pode executar uma solicitação assíncrona em segundo plano para atualizar a página. Você não força o usuário a esperar enquanto parte da página é atualizada.

Aproveitando o Ajax, você também pode melhorar o desempenho da sua aplicação. Considere como o aplicativo contact manager funciona agora sem a funcionalidade do Ajax. Quando você clica em um grupo de contato, toda a exibição Índice deve ser reexibida. A lista de contatos e lista de grupos de contato deve ser recuperada do servidor de banco de dados. Todos esses dados devem ser transmitidos através do fio do servidor web para o navegador da Web.

Depois de adicionar mos a funcionalidade do Ajax ao nosso aplicativo, no entanto, podemos evitar a reexibição de toda a página quando um usuário clica em um grupo de contato. Não precisamos mais pegar os grupos de contato do banco de dados. Também não precisamos empurrar toda a visão do Índice através do fio. Aproveitando o Ajax, reduzimos a quantidade de trabalho que nosso servidor de banco de dados deve realizar e reduzimos a quantidade de tráfego de rede exigido pelo nosso aplicativo.

## <a name="don-t-be-afraid-of-ajax"></a>Não tenha medo do Ajax

Alguns desenvolvedores evitam usar o Ajax porque se preocupam com navegadores de baixo nível. Eles querem ter certeza de que seus aplicativos web ainda funcionarão quando acessados por um navegador que não suporta JavaScript. Como o Ajax depende do JavaScript, alguns desenvolvedores evitam usar o Ajax.

No entanto, se você for cuidadoso sobre como implementar o Ajax, então você pode criar aplicativos que funcionam com navegadores de nível superior e de baixo. Nosso aplicativo Contact Manager funcionará com navegadores que suportam JavaScript e navegadores que não o fazem.

Se você usar o aplicativo Contact Manager com um navegador que suporta JavaScript, então você terá uma melhor experiência de usuário. Por exemplo, quando você clica em um grupo de contato, apenas a região da página que exibe contatos será atualizada.

Se, por outro lado, você usar o aplicativo Contact Manager com um navegador que não suporta JavaScript (ou que tem JavaScript desativado) então você terá uma experiência de usuário um pouco menos desejável. Por exemplo, quando você clica em um grupo de contato, toda a exibição Índice deve ser postada de volta no navegador para exibir a lista correspondente de contatos.

## <a name="adding-the-required-javascript-files"></a>Adicionando os arquivos JavaScript necessários

Precisaremos usar três arquivos JavaScript para adicionar a funcionalidade Ajax ao nosso aplicativo. Todos os três arquivos estão incluídos na pasta Scripts de um novo aplicativo mvc ASP.NET.

Se você planeja usar o Ajax em várias páginas do seu aplicativo, então faz sentido incluir os arquivos JavaScript necessários na página-mestre de exibição do aplicativo. Dessa forma, os arquivos JavaScript serão incluídos em todas as páginas do seu aplicativo automaticamente.

Adicione o seguinte JavaScript &lt;inclui&gt; dentro da tag principal da página-mestre do seu visor:

[!code-html[Main](iteration-7-add-ajax-functionality-cs/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Refatorando a exibição de índice para usar o Ajax

Vamos começar modificando nossa exibição índice para que clicar em um grupo de contato só atualize a região da exibição que exibe contatos. A caixa vermelha na Figura 1 contém a região que queremos atualizar.

[![Atualizando apenas contatos](iteration-7-add-ajax-functionality-cs/_static/image1.jpg)](iteration-7-add-ajax-functionality-cs/_static/image1.png)

**Figura 01**: Atualização apenas contatos[(Clique para ver imagem em tamanho real)](iteration-7-add-ajax-functionality-cs/_static/image2.png)

O primeiro passo é separar a parte da visão que queremos atualizar assíncronamente em uma parcial separada (exibir controle do usuário). A seção da exibição Índice que exibe a tabela de contatos foi movida para a parcial na Listagem 1.

**Listagem 1 - Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample2.aspx)]

Observe que a parcial na Listagem 1 tem um modelo diferente da exibição índice. O atributo *Herda* &lt;na&gt; diretiva %@ Page % especifica que&lt;a&gt; parte herda da classe ExibirUserControl Group.

A visão de índice atualizada está contida na Listagem 2.

**Listagem 2 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample3.aspx)]

Existem duas coisas que você deve notar sobre a exibição atualizada na Listagem 2. Primeiro, observe que todo o conteúdo movido para a parcial é substituído por uma chamada para Html.RenderPartial(). O método Html.RenderPartial() é chamado quando a exibição Índice é solicitada pela primeira vez para exibir o conjunto inicial de contatos.

Em segundo lugar, observe que o Html.ActionLink() usado para exibir grupos de contato foi substituído por um Ajax.ActionLink(). O Ajax.ActionLink() é chamado com os seguintes parâmetros:

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample4.aspx)]

O primeiro parâmetro representa o texto a ser exibido para o link, o segundo parâmetro representa os valores de rota e o terceiro parâmetro representa as opções Ajax. Neste caso, usamos a opção UpdateTargetId Ajax &lt;para&gt; apontar para a tag de div HTML que queremos atualizar após a solicitação do Ajax ser concluída. Queremos atualizar &lt;a&gt; tag div com a nova lista de contatos.

O método de índice atualizado() do controlador de contato está contido na Lista 3.

**Listagem 3 - Controladores\ContactController.cs (método de índice)**

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample5.cs)]

A ação do Índice atualizado retorna condicionalmente uma das duas coisas. Se a ação Index() for invocada por uma solicitação ajax, o controlador retorna uma parcial. Caso contrário, a ação Index() retorna uma visão inteira.

Observe que a ação Index() não precisa retornar tantos dados quando invocada por uma solicitação do Ajax. No contexto de uma solicitação normal, a ação Índice retorna uma lista de todos os grupos de contato e do grupo de contato selecionado. No contexto de uma solicitação do Ajax, a ação Index() retorna apenas o grupo selecionado. Ajax significa menos trabalho no seu servidor de banco de dados.

Nossa visão de índice modificado funciona no caso de navegadores de nível superior e de baixo. Se você clicar em um grupo de contatos e seu navegador suportar JavaScript, apenas a região da exibição que contém a lista de contatos será atualizada. Se, por outro lado, seu navegador não suportar JavaScript, então toda a visualização será atualizada.

Nossa visão atualizada do Índice tem um problema. Quando você clica em um grupo de contato, o grupo selecionado não é destacado. Como a lista de grupos é exibida fora da região que é atualizada durante uma solicitação do Ajax, o grupo certo não é destacado. Vamos resolver esse problema na próxima seção.

## <a name="adding-jquery-animation-effects"></a>Adicionando efeitos de animação jQuery

Normalmente, quando você clica em um link em uma página da Web, você pode usar a barra de progresso do navegador para detectar se o navegador está ou não buscando ativamente o conteúdo atualizado. Ao executar uma solicitação ajax, por outro lado, a barra de progresso do navegador não mostra nenhum progresso. Isso pode deixar os usuários nervosos. Como você sabe se o navegador congelou?

Existem várias maneiras que você pode indicar a um usuário que o trabalho está sendo executado durante a execução de uma solicitação ajax. Uma abordagem é exibir uma animação simples. Por exemplo, você pode desaparecer uma região quando uma solicitação do Ajax começa e desaparece na região quando a solicitação é concluída.

Usaremos a biblioteca jQuery que está incluída na estrutura mVC do Microsoft ASP.NET, para criar os efeitos de animação. A visão de índice atualizada está contida na Listagem 4.

**Listagem 4 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample6.aspx)]

Observe que a exibição Index atualizada contém três novas funções JavaScript. As duas primeiras funções usam jQuery para desaparecer e desaparecer na lista de contatos quando você clica em um novo grupo de contato. A terceira função exibe uma mensagem de erro quando uma solicitação do Ajax resulta em um erro (por exemplo, tempo livre da rede).

A primeira função também se dá para destacar o grupo selecionado. Um atributo selecionado classe= é adicionado ao elemento pai (o elemento LI) do elemento clicado. Novamente, jQuery facilita a seleção do elemento certo e a adição da classe CSS.

Esses scripts estão vinculados aos links de grupo com a ajuda do parâmetro Ajax.ActionLink() AjaxOptions. A chamada atualizada do método Ajax.ActionLink é assim:

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>Adicionando suporte ao histórico do navegador

Normalmente, quando você clica em um link para atualizar uma página, o histórico do seu navegador é atualizado. Dessa forma, você pode clicar no botão Voltar do navegador para voltar no tempo para o estado anterior da página. Por exemplo, se você clicar no grupo de contato Amigos e clicar no grupo de contato negócios, você pode clicar no botão 'Voltar do navegador' para navegar de volta para o estado da página quando o grupo de contato amigos foi selecionado.

Infelizmente, a execução de uma solicitação ajax não atualiza o histórico do navegador automaticamente. Se você clicar em um grupo de contatos e a lista de contatos correspondentes for recuperada com uma solicitação do Ajax, o histórico do navegador não será atualizado. Não é possível usar o botão 'Voltar' do navegador para navegar de volta a um grupo de contato depois de selecionar um novo grupo de contato.

Se você quiser que os usuários possam usar o botão De volta do navegador depois de executar as solicitações do Ajax, então você precisa realizar um pouco mais de trabalho. Você precisa aproveitar a funcionalidade de gerenciamento do histórico do navegador incorporada no ASP.NET AJAX Framework.

ASP.NET histórico do navegador AJAX, você precisa fazer três coisas:

1. Habilite o histórico do navegador definindo a propriedade enableBrowserHistory como true.
2. Salvar pontos de histórico quando o estado de uma exibição é alterado chamando o método addHistoryPoint().
3. Reconstrua o estado da visão quando o evento de navegação for levantado.

A visão de índice atualizada está contida na Lista 5.

**Listagem 5 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample8.aspx)]

Na Lista 5, o histórico do navegador está habilitado na função pageInit(). A função pageInit() também é usada para configurar o manipulador de eventos para o evento de navegação. O evento de navegação é levantado sempre que o botão Para frente ou para trás do navegador faz com que o estado da página seja alterado.

O método beginContactList() é chamado quando você clica em um grupo de contato. Este método cria um novo ponto de história chamando o método addHistoryPoint(). O id do grupo de contato clicado é adicionado ao histórico.

O id do grupo é recuperado de um atributo expando no link do grupo de contato. O link é renderizado com a seguinte chamada para Ajax.ActionLink().

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample9.aspx)]

O último parâmetro passado para o Ajax.ActionLink() adiciona um atributo expando chamado groupid ao link (minúscula para compatibilidade XHTML).

Quando um usuário aperta o botão Para trás ou para frente do navegador, o evento de navegação é levantado e o método de navegação é chamado. Este método atualiza os contatos exibidos na página para corresponder ao estado da página que corresponde ao ponto de histórico do navegador passado para o método de navegação.

## <a name="performing-ajax-deletes"></a>Realizando Ajax Deletes

Atualmente, para excluir um contato, você precisa clicar no link Excluir e, em seguida, clicar no botão Excluir exibido na página de confirmação de exclusão (ver Figura 2). Isso parece um monte de pedidos de página para fazer algo simples como excluir um registro de banco de dados.

[![A página de confirmação de exclusão](iteration-7-add-ajax-functionality-cs/_static/image2.jpg)](iteration-7-add-ajax-functionality-cs/_static/image3.png)

**Figura 02**: A página de confirmação de exclusão[(Clique para exibir imagem em tamanho real)](iteration-7-add-ajax-functionality-cs/_static/image4.png)

É tentador pular a página de confirmação de exclusão e excluir um contato diretamente da exibição Índice. Você deve evitar essa tentação, porque tomar essa abordagem abre sua aplicação para falhas de segurança. Em geral, você não deseja realizar uma operação HTTP GET ao invocar uma ação que modifique o estado do seu aplicativo web. Ao executar uma exclusão, você deseja executar um HTTP POST, ou melhor ainda, uma operação HTTP DELETE.

O link Excluir está contido na parcial Da Lista de Contatos. Uma versão atualizada da parcial contactlist está contida na Lista 6.

**Lista 6 - Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample10.aspx)]

O link Excluir é renderizado com a seguinte chamada para o método Ajax.ImageActionLink(:

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample11.aspx)]

> [!NOTE] 
> 
> O Ajax.ImageActionLink() não é uma parte padrão da estrutura ASP.NET MVC. O Ajax.ImageActionLink() é um método de ajuda personalizado incluído no projeto Contact Manager.

O parâmetro AjaxOptions tem duas propriedades. Primeiro, a propriedade Confirmar é usada para exibir uma caixa de confirmação JavaScript popup. Em segundo lugar, a propriedade HttpMethod é usada para executar uma operação HTTP DELETE.

A lista 7 contém uma nova ação AjaxDelete() que foi adicionada ao controlador de contato.

**Lista 7 - Controladores\ContactController.cs (AjaxDelete)**

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample12.cs)]

A ação AjaxDelete() é decorada com um atributo AcceptVerbs. Este atributo impede que a ação seja invocada, exceto por qualquer operação HTTP que não seja uma operação HTTP DELETE. Em particular, você não pode invocar esta ação com um HTTP GET.

Depois de excluir o registro do banco de dados, você precisa exibir a lista atualizada de contatos que não contêm o registro excluído. O método AjaxDelete() retorna a parcial da Lista de Contatos e a lista atualizada de contatos.

## <a name="summary"></a>Resumo

Nesta iteração, adicionamos a funcionalidade do Ajax ao nosso aplicativo de Contact Manager. Usamos o Ajax para melhorar a capacidade de resposta e o desempenho da nossa aplicação.

Primeiro, refatoriamos a exibição Índice para que clicar em um grupo de contato não atualize toda a exibição. Em vez disso, clicar em um grupo de contato apenas atualiza a lista de contatos.

Em seguida, usamos efeitos de animação jQuery para desaparecer e desaparecer na lista de contatos. Adicionar animação a um aplicativo Ajax pode ser usado para fornecer aos usuários do aplicativo o equivalente a uma barra de progresso do navegador.

Também adicionamos suporte ao histórico do navegador ao nosso aplicativo Ajax. Permitimos que os usuários clicassem nos botões De volta e para frente do navegador para alterar o estado da exibição Índice.

Finalmente, criamos um link de exclusão que suporta operações HTTP DELETE. Ao realizar exclusões do Ajax, permitimos que os usuários excluam registros de banco de dados sem exigir que o usuário solicite uma página de confirmação de exclusão adicional.

> [!div class="step-by-step"]
> [Próximo](iteration-6-use-test-driven-development-cs.md)
> [anterior](iteration-1-create-the-application-vb.md)
