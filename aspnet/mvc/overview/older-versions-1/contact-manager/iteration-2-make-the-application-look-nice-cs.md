---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: 'Iteração #2 – Faça o aplicativo parecer bom (C#) | Microsoft Docs'
author: rick-anderson
description: Nesta iteração, melhoramos a aparência do aplicativo modificando o padrão ASP.NET página-mestre de exibição mVC e folha de estilo em cascata.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: ee1d7c92524f6cbdb0f2d7facf85b629e0d91318
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542437"
---
# <a name="iteration-2--make-the-application-look-nice-c"></a>Iteração nº 2 – dar uma boa aparência ao aplicativo (C#)

pela [Microsoft](https://github.com/microsoft)

[Código de download](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> Nesta iteração, melhoramos a aparência do aplicativo modificando o padrão ASP.NET página-mestre de exibição mVC e folha de estilo em cascata.

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

O objetivo desta iteração é melhorar a aparência do aplicativo Contact Manager. Atualmente, o Gerenciador de contatos usa o padrão ASP.NET página-mestre de exibição MVC e folha de estilo em cascata (ver Figura 1). Estes não parecem ruins, mas eu não quero que o Gerente de Contato se pareça com todos os outros ASP.NET site mvc. Quero substituir esses arquivos por arquivos personalizados.

[![A caixa de diálogo Novo Projeto](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)

**Figura 01**: A aparência padrão de um aplicativo MVC ASP.NET[(Clique para exibir imagem em tamanho real)](iteration-2-make-the-application-look-nice-cs/_static/image2.png)

Nesta iteração, discuto duas abordagens para melhorar o design visual da nossa aplicação. Primeiro, eu mostro como aproveitar a galeria ASP.NET MVC Design para baixar um modelo de design MVC de ASP.NET gratuito. A ASP.NET galeria MVC Design permite que você crie um aplicativo web profissional sem fazer nenhum trabalho.

Decidi não usar um modelo da galeria ASP.NET MVC Design para o aplicativo Contact Manager. Em vez disso, eu tinha um design personalizado criado por uma empresa de design profissional. Na segunda parte deste tutorial, explico como trabalhei com uma empresa de design profissional para criar o design final ASP.NET MVC.

## <a name="the-aspnet-mvc-design-gallery"></a>A Galeria de Design ASP.NET MVC

O ASP.NET MVC Design Gallery é um recurso gratuito fornecido pela Microsoft. A Galeria MVC ASP.NET está localizada no seguinte endereço:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

A ASP.NET MVC Design Gallery hospeda uma coleção de designs de sites gratuitos que foram criados especificamente para uso em um projeto mvc ASP.NET. Os desenhos são carregados por membros da comunidade. Os visitantes da Galeria podem votar em seus desenhos favoritos (ver Figura 2).

[![A caixa de diálogo Novo Projeto](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)

**Figura 02**: A ASP.NET MVC Design Gallery[(Clique para ver a imagem em tamanho real)](iteration-2-make-the-application-look-nice-cs/_static/image4.png)

Como eu escrevo este tutorial, o design mais popular na galeria é um design chamado outubro por David Hauser. Você pode usar este design para um projeto mvc ASP.NET completando as seguintes etapas:

1. Clique no botão **Baixar** para baixar o arquivo October.zip no seu computador.
2. Clique com o botão direito do mouse no arquivo october.zip baixado e clique no botão **Desbloquear** (ver Figura 3).
3. Descompacte o arquivo para uma pasta chamada Outubro.
4. Selecione todos os arquivos da pasta DesignTemplate contidos na pasta de outubro, clique com o botão direito do mouse nos arquivos e selecione a opção menu **Copiar**.
5. Clique com o botão direito do mouse no nó do projeto ContactManager na janela Visual Studio Solution Explorer e selecione a opção menu **Colar** (ver Figura 4).
6. Selecione a opção de menu Visual Studio **Edit, Find and Replace, Substitua rapidamente** e *substitua [MyProjectName]* pelo *ContactManager* (veja Figura 5).

[![A caixa de diálogo Novo Projeto](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)

**Figura 03**: Desbloquear um arquivo baixado da web ([Clique para exibir imagem em tamanho real](iteration-2-make-the-application-look-nice-cs/_static/image6.png))

[![A caixa de diálogo Novo Projeto](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)

**Figura 04**: Substituição de arquivos no Solution Explorer[(Clique para ver imagem em tamanho real)](iteration-2-make-the-application-look-nice-cs/_static/image8.png)

[![A caixa de diálogo Novo Projeto](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)

**Figura 05**: Substituição [ProjectName] pelo ContactManager[(Clique para exibir imagem em tamanho real)](iteration-2-make-the-application-look-nice-cs/_static/image10.png)

Depois de concluir essas etapas, seu aplicativo web usará o novo design. A página na Figura 6 ilustra a aparência do aplicativo Contact Manager com o design de outubro.

[![A caixa de diálogo Novo Projeto](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)

**Figura 06**: ContactManager com o modelo de outubro ([Clique para ver a imagem em tamanho real](iteration-2-make-the-application-look-nice-cs/_static/image12.png))

## <a name="creating-a-custom-aspnet-mvc-design"></a>Criando um design mvc de ASP.NET personalizado

A ASP.NET MVC Design Gallery tem uma boa seleção de diferentes estilos de design. A Galeria fornece uma maneira indolor de personalizar a aparência de seus aplicativos mvc ASP.NET. E, claro, a Galeria tem a grande vantagem de ser completamente livre.

No entanto, você pode precisar criar um design completamente exclusivo para o seu site. Nesse caso, faz sentido trabalhar com uma empresa de design de sites. Decidi fazer essa abordagem para o design do aplicativo Contact Manager.

Fechei o Contact Manager da Iteração #1 e enviei o projeto para a empresa de design. Eles não eram donos do Visual Studio (que vergonha!), mas isso não apresentou problema. Eles foram capazes de baixar o [https://www.asp.net](https://www.asp.net) Microsoft Visual Web Developer gratuitamente no site e abrir o aplicativo Contact Manager no Visual Web Developer. Em alguns dias, eles produziram o design na Figura 7.

[![A caixa de diálogo Novo Projeto](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)

**Figura 07**: O ASP.NET MVC Contact Manager Design[(Clique para ver a imagem em tamanho real)](iteration-2-make-the-application-look-nice-cs/_static/image14.png)

O novo design consistia em dois arquivos principais: um novo arquivo de folha de estilo em cascata e um novo arquivo de página-mestre de exibição. Uma página-mestre de exibição contém o layout e o conteúdo compartilhado para visualizações em um aplicativo MVC ASP.NET. Por exemplo, a página-mestre de exibição inclui o cabeçalho, as guias de navegação e o rodapé que aparecem na Figura 7. Eu sobreescrevi a página-mestre de exibição do Site.Master existente na pasta Views\Shared com o novo arquivo Site.Master da empresa de design,

A empresa de design também criou uma nova folha de estilo em cascata e um conjunto de imagens. Coloquei esses novos arquivos na pasta Conteúdo e sobreescrevi o arquivo Site.css existente. Você deve colocar todo o conteúdo estático na pasta Conteúdo.

Observe que o novo design para o Gerenciador de Contatos inclui imagens para edição e exclusão de contatos. Uma imagem Editar e Excluir aparecer ao lado de cada contato na tabela HTML de contatos.

Originalmente, esses links que foram renderizados com o HTML. Ajudador actionLink() como este:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

O método Html.ActionLink não suporta imagens (o método HTML codifica o texto do link por razões de segurança). Portanto, substituí as chamadas para Html.ActionLink() por chamadas para Url.Action() assim:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

O método Html.ActionLink renderiza um hiperlink HTML inteiro. O método Url.Action(), por outro lado, renderiza apenas &lt;&gt; a URL sem a tag.

Observe, ainda, que o novo design inclui guias selecionadas e não selecionadas. Por exemplo, na Figura 8, a guia **Criar novo contato** é selecionada e a guia Meus **contatos** não está selecionada.

[![A caixa de diálogo Novo Projeto](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)

**Figura 08**: Guias selecionadas e não selecionadas[(Clique para exibir a imagem em tamanho real)](iteration-2-make-the-application-look-nice-cs/_static/image16.png)

Para suportar a renderização de guias selecionadas e não selecionadas, criei um ajudante HTML personalizado chamado MenuItemHelper. Este método auxiliar renderiza &lt;uma&gt; tag &lt;li ou uma&gt; tag li class="selecionada", dependendo se o controlador atual e a ação correspondem ao controlador e nome de ação passados ao ajudante. O código do MenuItemHelper está contido na Lista 1.

**Listagem 1 - Helpers\MenuItemHelper.cs**

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

O MenuItemHelper usa a classe TagBuilder &lt;&gt; internamente para construir a tag li HTML. A classe TagBuilder é uma classe de utilidade muito útil que você pode usar sempre que precisar para construir uma nova tag HTML. Ele inclui métodos para adicionar atributos, adicionar classes CSS, gerar IDs e modificar o HTML interno da tag.

## <a name="summary"></a>Resumo

Nesta iteração, melhoramos o design visual do nosso ASP.NET aplicativo MVC. Primeiro, você foi apresentado à ASP.NET MVC Design Gallery. Você aprendeu a baixar modelos de design gratuitos da ASP.NET MVC Design Gallery que você pode usar em seus ASP.NET aplicativos MVC.

Em seguida, discutimos como você pode criar um design personalizado modificando o arquivo de folha de estilo em cascata padrão e o arquivo de página de exibição mestre. Para dar suporte ao novo design, tivemos que fazer algumas pequenas alterações no nosso aplicativo de Contact Manager. Por exemplo, adicionamos um novo ajudante HTML chamado MenuItemHelper que exibe guias selecionadas e não selecionadas.

Na próxima iteração, abordamos o tema muito importante da validação. Adicionamos código de validação ao nosso aplicativo para que um usuário não possa criar um novo contato sem fornecer valores necessários, como o primeiro e o sobrenome de uma pessoa.

> [!div class="step-by-step"]
> [Próximo](iteration-1-create-the-application-cs.md)
> [anterior](iteration-3-add-form-validation-cs.md)
