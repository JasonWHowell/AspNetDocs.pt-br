---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 'Iteração #6 – Use desenvolvimento orientado por testes (C#) | Microsoft Docs'
author: rick-anderson
description: Nesta sexta iteração, adicionamos nova funcionalidade ao nosso aplicativo escrevendo primeiro testes de unidade e escrevendo código satisfaz os testes da unidade. Nesta iteração,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: d0e8f30a075cc79c7410ffe1b8bf02da2bd44443
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542320"
---
# <a name="iteration-6--use-test-driven-development-c"></a>Iteração nº 6 – usar desenvolvimento controlado por testes (C#)

pela [Microsoft](https://github.com/microsoft)

[Código de download](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> Nesta sexta iteração, adicionamos nova funcionalidade ao nosso aplicativo escrevendo primeiro testes de unidade e escrevendo código satisfaz os testes da unidade. Nesta iteração, adicionamos grupos de contato.

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

Na iteração anterior do aplicativo Contact Manager, criamos testes unitários para fornecer uma rede de segurança para o nosso código. A motivação para criar os testes da unidade foi tornar nosso código mais resistente à mudança. Com testes unitários em vigor, podemos fazer qualquer alteração em nosso código e imediatamente saber se quebramos a funcionalidade existente.

Nesta iteração, usamos testes unitários para um propósito totalmente diferente. Nesta iteração, usamos testes unitários como parte de uma filosofia de design de aplicativos chamada *desenvolvimento orientado a testes.* Quando você pratica o desenvolvimento orientado para testes, você escreve primeiro os testes e, em seguida, escreve código contra os testes.

Mais precisamente, ao praticar o desenvolvimento orientado para o teste, existem três etapas que você completa ao criar código (Vermelho/ Verde/Refator):

1. Escreva um teste de unidade que falha (Vermelho)
2. Escrever código que passa no teste da unidade (Verde)
3. Refatorar seu código (Refatorar)

Primeiro, você escreve o teste da unidade. O teste da unidade deve expressar sua intenção de como você espera que seu código se comporte. Quando você criar o teste da unidade pela primeira vez, o teste da unidade deve falhar. O teste deve falhar porque você ainda não escreveu nenhum código de aplicação que satisfaça o teste.

Em seguida, você escreve apenas código suficiente para que o teste da unidade passe. O objetivo é escrever o código da maneira mais preguiçosa, desleixada e mais rápida possível. Você não deve perder tempo pensando na arquitetura de sua aplicação. Em vez disso, você deve se concentrar em escrever a quantidade mínima de código necessária para satisfazer a intenção expressa pelo teste unitário.

Finalmente, depois de ter escrito código suficiente, você pode dar um passo atrás e considerar a arquitetura geral do seu aplicativo. Nesta etapa, você reescreve (refatorar) seu código aproveitando padrões de design de software - como o padrão do repositório - para que seu código seja mais sustentável. Você pode reescrever seu código sem medo nesta etapa porque seu código está coberto por testes de unidade.

Há muitos benefícios que resultam da prática de desenvolvimento orientado a testes. Primeiro, o desenvolvimento orientado por testes força você a se concentrar em códigos que realmente precisam ser escritos. Como você está constantemente focado em apenas escrever código suficiente para passar em um determinado teste, você está impedido de vagar pelas sementes e escrever grandes quantidades de código que você nunca usará.

Em segundo lugar, uma metodologia de design "teste primeiro" força você a escrever código a partir da perspectiva de como seu código será usado. Em outras palavras, ao praticar o desenvolvimento orientado para testes, você está constantemente escrevendo seus testes de uma perspectiva de usuário. Portanto, o desenvolvimento orientado para testes pode resultar em APIs mais limpas e compreensíveis.

Finalmente, o desenvolvimento orientado ao teste força você a escrever testes unitários como parte do processo normal de escrever um aplicativo. À medida que um prazo de projeto se aproxima, o teste é tipicamente a primeira coisa que sai pela janela. Ao praticar o desenvolvimento orientado para testes, por outro lado, é mais provável que você seja virtuoso em relação aos testes de unidades de escrita, porque o desenvolvimento orientado por testes torna os testes unitários centrais para o processo de construção de um aplicativo.

> [!NOTE] 
> 
> Para saber mais sobre o desenvolvimento orientado para o teste, recomendo que você leia o livro de Michael Feathers **trabalhando efetivamente com o Código Legado**.

Nesta iteração, adicionamos um novo recurso ao nosso aplicativo de Contact Manager. Adicionamos suporte para grupos de contato. Você pode usar grupos de contato para organizar seus contatos em categorias como grupos de negócios e amigos.

Adicionaremos essa nova funcionalidade ao nosso aplicativo seguindo um processo de desenvolvimento orientado por testes. Escreveremos nossos testes de unidade primeiro e escreveremos todos os nossos códigos contra esses testes.

## <a name="what-gets-tested"></a>O que é testado

Como discutimos na iteração anterior, você normalmente não escreve testes unitários para lógica de acesso a dados ou lógica de visualização. Você não escreve testes de unidade para lógica de acesso a dados porque acessar um banco de dados é uma operação relativamente lenta. Você não escreve testes de unidade para lógica de visualização porque acessar uma visualização requer girar um servidor web que é uma operação relativamente lenta. Você não deve escrever um teste de unidade a menos que o teste possa ser executado uma e outra vez muito rápido

Como o desenvolvimento orientado para testes é impulsionado por testes unitários, focamos inicialmente na escrita do controlador e da lógica de negócios. Evitamos tocar no banco de dados ou visualizações. Não modificaremos o banco de dados ou criaremos nossas visualizações até o final deste tutorial. Começamos com o que pode ser testado.

## <a name="creating-user-stories"></a>Criando histórias de usuários

Ao praticar o desenvolvimento orientado para o teste, você sempre começa escrevendo um teste. Isso imediatamente levanta a questão: Como você decide qual teste escrever primeiro? Para responder a esta pergunta, você deve escrever um conjunto de [**histórias de usuários**](http://en.wikipedia.org/wiki/User_stories).

Uma história de usuário é uma descrição muito breve (geralmente uma frase) de um requisito de software. Deve ser uma descrição não técnica de um requisito escrito a partir de uma perspectiva de usuário.

Aqui está o conjunto de histórias de usuários que descrevem os recursos exigidos pela nova funcionalidade do Contact Group:

1. O usuário pode visualizar uma lista de grupos de contato.
2. O usuário pode criar um novo grupo de contato.
3. O usuário pode excluir um grupo de contato existente.
4. O usuário pode selecionar um grupo de contato ao criar um novo contato.
5. O usuário pode selecionar um grupo de contato ao editar um contato existente.
6. Uma lista de grupos de contato é exibida na exibição Índice.
7. Quando um usuário clica em um grupo de contato, uma lista de contatos correspondentes é exibida.

Observe que esta lista de histórias de usuários é completamente compreensível por um cliente. Não há menção a detalhes de implementação técnica.

Enquanto no processo de construção do seu aplicativo, o conjunto de histórias de usuários pode se tornar mais refinado. Você pode quebrar uma história de usuário em várias histórias (requisitos). Por exemplo, você pode decidir que a criação de um novo grupo de contato deve envolver validação. Enviar um grupo de contato sem nome deve retornar um erro de validação.

Depois de criar uma lista de histórias de usuários, você está pronto para escrever seu primeiro teste de unidade. Começaremos criando um teste de unidade para visualizar a lista de grupos de contato.

## <a name="listing-contact-groups"></a>Listando grupos de contato

Nossa primeira história de usuário é que um usuário deve ser capaz de visualizar uma lista de grupos de contato. Precisamos expressar essa história com um teste.

Crie um novo teste de unidade clicando com o botão direito do mouse na pasta Controladores no projeto ContactManager.Tests, selecionando **Adicionar, Novo Teste**e selecionando o modelo **de teste** de unidade (ver Figura 1). Nomeie o novo teste da unidade GroupControllerTest.cs e clique no botão **OK.**

[![Adicionando o teste da unidade GroupControllerTest](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**Figura 01**: Adicionando o teste da unidade GroupControllerTest[(Clique para exibir imagem em tamanho real)](iteration-6-use-test-driven-development-cs/_static/image2.png)

Nosso primeiro teste unitário está contido na Lista 1. Este teste verifica se o método Index() do controlador de grupo retorna um conjunto de Grupos. O teste verifica se uma coleção de Grupos é devolvida em dados de exibição.

**Listagem 1 - Controladores\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

Quando você digitar pela primeira vez o código na Listagem 1 no Visual Studio, você terá um monte de linhas vermelhas squiggly. Não criamos as classes GroupController ou Group.

Neste ponto, não podemos sequer construir nossa aplicação para que não possamos executar nosso primeiro teste de unidade. Isso é bom. Isso conta como um teste de reprovação. Portanto, agora temos permissão para começar a escrever o código do aplicativo. Precisamos escrever código suficiente para executar nosso teste.

A classe controladora de grupo na Lista 2 contém o mínimo de código necessário para passar no teste da unidade. A ação Index() retorna uma lista codificada estáticamente de Grupos (a classe Grupo é definida na Lista 3).

**Listagem 2 - Controladores\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**Listagem 3 - Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

Depois de adicionar as classes GroupController e Group ao nosso projeto, nosso primeiro teste de unidade é concluído com sucesso (ver Figura 2). Fizemos o trabalho mínimo necessário para passar no teste. É hora de comemorar.

[![Sucesso!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**Figura 02**: Sucesso! (Clique[para ver a imagem em tamanho real](iteration-6-use-test-driven-development-cs/_static/image4.png))

## <a name="creating-contact-groups"></a>Criando grupos de contato

Agora podemos passar para a segunda história do usuário. Precisamos ser capazes de criar novos grupos de contato. Precisamos expressar essa intenção com um teste.

O teste na Listagem 4 verifica se a chamada do método Criar() com um novo Grupo adiciona o Grupo à lista de Grupos retornados pelo método Index(). Em outras palavras, se eu criar um novo grupo, então eu deveria ser capaz de obter o novo Grupo de volta da lista de Grupos retornados pelo método Index().

**Listagem 4 - Controladores\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

O teste na Lista 4 chama o método De criar o controlador de grupo com um novo grupo de contato. Em seguida, o teste verifica se a chamada do método Índice do Controlador de Grupo retorna o novo Grupo em dados de exibição.

O controlador de grupo modificado na Lista 5 contém o mínimo de alterações necessárias para passar no novo teste.

**Listagem 5 - Controladores\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>O controlador do Grupo na Lista 5 tem uma nova ação Criar(). Esta ação adiciona um Grupo a uma coleção de Grupos. Observe que a ação Índice() foi modificada para devolver o conteúdo da coleção de Grupos.

Mais uma vez, realizamos a quantidade mínima de trabalho necessária para passar no teste da unidade. Depois de fazermos essas alterações no controlador do grupo, todos os testes da unidade passam.

## <a name="adding-validation"></a>Adicionando uma Validação

Essa exigência não foi explicitada na história do usuário. No entanto, é razoável exigir que um Grupo tenha um nome. Caso contrário, organizar contatos em Grupos não seria muito útil.

A listagem 6 contém um novo teste que expressa essa intenção. Este teste verifica que a tentativa de criar um Grupo sem fornecer um nome resulta em uma mensagem de erro de validação no estado modelo.

**Listagem 6 - Controladores\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

Para satisfazer este teste, precisamos adicionar uma propriedade Name à nossa classe de grupo (consulte Lista 7). Além disso, precisamos adicionar um pouco de lógica de validação à ação Create() do nosso controlador de grupo (ver Listagem 8).

**Listagem 7 - Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**Listagem 8 - Controladores\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

Observe que a ação Do controlador de grupo Criar() agora contém a lógica de validação e banco de dados. Atualmente, o banco de dados utilizado pelo controlador do Grupo consiste em nada mais do que uma coleção na memória.

## <a name="time-to-refactor"></a>Hora de Refatorar

O terceiro passo em Vermelho/Verde/Refator é a parte Refator. Neste ponto, precisamos recuar do nosso código e considerar como podemos refatorar nossa aplicação para melhorar seu design. A fase refatora é o estágio em que pensamos muito sobre a melhor maneira de implementar princípios e padrões de design de software.

Somos livres para modificar nosso código de qualquer maneira que optarmos por melhorar o design do código. Temos uma rede de testes de unidade que nos impedem de quebrar a funcionalidade existente.

Neste momento, nosso controlador de grupo está uma bagunça do ponto de vista do bom design de software. O controlador do Grupo contém uma confusão emaranhada de validação e código de acesso de dados. Para evitar violar o Princípio da Responsabilidade Única, precisamos separar essas preocupações em diferentes classes.

Nossa classe de controlador de grupo refatorada está contida na Lista 9. O controlador foi modificado para usar a camada de serviço ContactManager. Esta é a mesma camada de serviço que usamos com o controlador Contato.

A listagem 10 contém os novos métodos adicionados à camada de serviço ContactManager para suportar a validação, listagem e criação de grupos. A interface iContactManagerService foi atualizada para incluir os novos métodos.

A listagem 11 contém uma nova classe FakeContactManagerRepository que implementa a interface IContactManagerRepository. Ao contrário da classe EntityContactManagerRepository, que também implementa a interface IContactManagerRepository, nossa nova classe FakeContactManagerRepository não se comunica com o banco de dados. A classe FakeContactManagerRepository usa uma coleção na memória como proxy para o banco de dados. Usaremos esta aula em nossos testes de unidade como uma falsa camada de repositório.

**Listagem 9 - Controladores\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**Listagem 10 - Controladores\ContactManagerService.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**Listagem 11 - Controladores\FakeContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

Modificar a interface IContactManagerRepository requer o uso para implementar os métodos CreateGroup() e ListGroups() na classe EntityContactManagerRepository. A maneira mais preguiçosa e mais rápida de fazer isso é adicionar métodos de stub que se parecem com isso:   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

Finalmente, essas mudanças no design de nossa aplicação exigem que façamos algumas modificações em nossos testes unitários. Agora precisamos usar o FakeContactManagerRepository ao realizar os testes unitários. A classe GroupControllerTest atualizada está contida na Lista 12.

**Listagem 12 - Controladores\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

Depois de fazermos todas essas mudanças, mais uma vez, todos os testes da unidade passam. Completamos todo o ciclo do Red/Green/Refactor. Implementamos as duas primeiras histórias de usuários. Agora temos testes de unidade de suporte para os requisitos expressos nas histórias do usuário. A implementação do restante das histórias do usuário envolve repetir o mesmo ciclo do Red/Green/Refactor.

## <a name="modifying-our-database"></a>Modificando nosso banco de dados

Infelizmente, apesar de termos cumprido todos os requisitos expressos pelos testes de nossa unidade, nosso trabalho não está feito. Ainda precisamos modificar nosso banco de dados.

Precisamos criar uma nova tabela de banco de dados do Grupo. Siga estas etapas:

1. Na janela Server Explorer, clique com o botão direito do mouse na pasta Tabelas e selecione a opção **menu Adicionar nova tabela**.
2. Digite as duas colunas descritas abaixo no Table Designer.
3. Marque a coluna Id como uma chave principal e coluna identidade.
4. Salve a nova tabela com o nome Grupos clicando no ícone do disquete.

<a id="0.11_table01"></a>

| **Nome da coluna** | **Tipo de dados** | **Permitir Nulos** |
| --- | --- | --- |
| ID | INT | Falso |
| Nome | nvarchar (50) | Falso |

Em seguida, precisamos excluir todos os dados da tabela Contatos (caso contrário, não poderemos criar uma relação entre as tabelas Contatos e Grupos). Siga estas etapas:

1. Clique com o botão direito do mouse na tabela Contatos e selecione a opção **menu Mostrar dados da tabela**.
2. Exclua todas as linhas.

Em seguida, precisamos definir uma relação entre a tabela de banco de dados Grupos e a tabela de banco de dados contatos existente. Siga estas etapas:

1. Clique duas vezes na tabela Contatos na janela Server Explorer para abrir o Table Designer.
2. Adicione uma nova coluna inteira à tabela Contatos chamada GroupId.
3. Clique no botão Relacionamento para abrir a caixa de diálogo Relações de Chave Estrangeira (ver Figura 3).
4. Clique no botão Adicionar.
5. Clique no botão elipse que aparece ao lado do botão Especificação tabela e colunas.
6. Na caixa de diálogo Tabelas e Colunas, selecione Grupos como a tabela principal de tecla e Id como a coluna de tecla principal. Selecione Contatos como a tabela de tecla estrangeira e GroupId como a coluna de tecla estrangeira (ver Figura 4). Clique no botão OK.
7. Em **INSERT e UPDATE Specification**, selecione o valor **Cascata** para **Excluir Regra**.
8. Clique no botão Fechar para fechar a caixa de diálogo Relações de Chave Estrangeira.
9. Clique no botão Salvar para salvar as alterações na tabela Contatos.

[![Criando uma relação de tabela de banco de dados](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**Figura 03**: Criação de uma relação de tabela de banco de dados[(Clique para ver imagem em tamanho real)](iteration-6-use-test-driven-development-cs/_static/image6.png)

[![Especificando relacionamentos de tabela](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**Figura 04**: Especificando relações de tabela[(Clique para exibir imagem em tamanho real)](iteration-6-use-test-driven-development-cs/_static/image8.png)

### <a name="updating-our-data-model"></a>Atualizando nosso modelo de dados

Em seguida, precisamos atualizar nosso modelo de dados para representar a nova tabela de banco de dados. Siga estas etapas:

1. Clique duas vezes no arquivo ContactManagerModel.edmx na pasta Modelos para abrir o Entity Designer.
2. Clique com o botão direito do mouse na superfície do Designer e selecione a opção de menu **Modelo de atualização do banco de dados**.
3. No Assistente de atualização, selecione a tabela Grupos e clique no botão Concluir (consulte Figura 5).
4. Clique com o botão direito do mouse na entidade Grupos e selecione a opção menu **Renomear**. Mude o nome da entidade *grupos* para *Grupo* (singular).
5. Clique com o botão direito do mouse na propriedade de navegação Grupos que aparece na parte inferior da entidade Contato. Alterar o nome da propriedade de navegação *Grupos* para *Grupo* (singular).

[![Atualizando um modelo de framework de entidades a partir do banco de dados](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**Figura 05**: Atualização de um modelo de quadro de entidades a partir do banco de dados[(Clique para exibir imagem em tamanho real](iteration-6-use-test-driven-development-cs/_static/image10.png))

Depois de concluir essas etapas, seu modelo de dados representará as tabelas Contatos e Grupos. O Entity Designer deve mostrar ambas as entidades (ver Figura 6).

[![Entity Designer exibindo Grupo e Contato](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**Figura 06**: Entity Designer exibindo Grupo e Contato[(Clique para exibir imagem em tamanho real)](iteration-6-use-test-driven-development-cs/_static/image12.png)

### <a name="creating-our-repository-classes"></a>Criando nossas Classes de Repositório

Em seguida, precisamos implementar nossa classe de repositório. Ao longo desta iteração, adicionamos vários novos métodos à interface IContactManagerRepository enquanto escrevemos código para satisfazer nossos testes unitários. A versão final da interface IContactManagerRepository está contida na Lista 14.

**Listagem 14 - Modelos\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

Na verdade, não implementamos nenhum dos métodos relacionados ao trabalho com grupos de contato. Atualmente, a classe EntityContactManagerRepository possui métodos de stub para cada um dos métodos de grupo de contato listados na interface IContactManagerRepository. Por exemplo, o método ListGroups() atualmente se parece com isso:

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

Os métodos de stub nos permitiram compilar nossa aplicação e passar nos testes unitários. No entanto, agora é hora de realmente implementar esses métodos. A versão final da classe EntityContactManagerRepository está contida na Lista 13.

**Listagem 13 - Modelos\EntidadeContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>Criando as visualizações

ASP.NET aplicativo MVC quando você usa o mecanismo de visualização de ASP.NET padrão. Então, você não cria visualizações em resposta a um teste de unidade em particular. No entanto, como um aplicativo seria inútil sem visualizações, não podemos concluir essa iteração sem criar e modificar as visualizações contidas no aplicativo Contact Manager.

Precisamos criar as seguintes novas visões para gerenciar grupos de contato (ver Figura 7):

- Views\Group\Index.aspx - Exibe lista de grupos de contato
- Views\Group\Delete.aspx - Exibe formulário de confirmação para excluir um grupo de contato

[![A visão do Índice de Grupo](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**Figura 07**: A exibição Índice de Grupo[(Clique para ver a imagem em tamanho real)](iteration-6-use-test-driven-development-cs/_static/image14.png)

Precisamos modificar as seguintes visualizações existentes para que incluam grupos de contato:

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

Você pode ver as visualizações modificadas olhando para o aplicativo Visual Studio que acompanha este tutorial. Por exemplo, a Figura 8 ilustra a exibição Índice de contato.

[![A exibição do Índice de Contato](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**Figura 08**: A exibição índice de contato[(Clique para ver imagem em tamanho real)](iteration-6-use-test-driven-development-cs/_static/image16.png)

## <a name="summary"></a>Resumo

Nesta iteração, adicionamos novas funcionalidades ao nosso aplicativo Contact Manager seguindo uma metodologia de design de aplicativo de desenvolvimento orientada a testes. Começamos criando um conjunto de histórias de usuários. Criamos um conjunto de testes unitários que correspondem aos requisitos expressos pelas histórias do usuário. Finalmente, escrevemos código suficiente para satisfazer os requisitos expressos pelos testes unitários.

Depois que terminamos de escrever código suficiente para satisfazer os requisitos expressos pelos testes da unidade, atualizamos nosso banco de dados e visualizações. Adicionamos uma nova tabela de grupos ao nosso banco de dados e atualizamos nosso Modelo de Dados-Quadro de Entidades. Também criamos e modificamos um conjunto de pontos de vista.

Na próxima iteração, a iteração final, reescrevemos nosso aplicativo para tirar vantagem do Ajax. Aproveitando o Ajax, melhoraremos a capacidade de resposta e o desempenho do aplicativo Contact Manager.

> [!div class="step-by-step"]
> [Próximo](iteration-5-create-unit-tests-cs.md)
> [anterior](iteration-7-add-ajax-functionality-cs.md)
