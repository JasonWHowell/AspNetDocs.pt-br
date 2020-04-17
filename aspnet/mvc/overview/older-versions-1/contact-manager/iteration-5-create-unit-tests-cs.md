---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: 'Iteração #5 – Criar testes unitários (C#) | Microsoft Docs'
author: rick-anderson
description: Na quinta iteração, tornamos nossa aplicação mais fácil de manter e modificar adicionando testes unitários. Nós zombamos de nossas classes de modelo de dados e construímos testes unitários para o...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: c005a8ffc3b09c126d796f2feb74d402cb784aa2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542346"
---
# <a name="iteration-5--create-unit-tests-c"></a>Iteração nº 5 – criar testes de unidade (C#)

pela [Microsoft](https://github.com/microsoft)

[Código de download](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> Na quinta iteração, tornamos nossa aplicação mais fácil de manter e modificar adicionando testes unitários. Zombamos de nossas classes de modelo de dados e construímos testes unitários para nossos controladores e lógica de validação.

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

Na iteração anterior do aplicativo Contact Manager, refatoriamos o aplicativo para ser mais acoplado. Separamos o aplicativo em camadas distintas de controlador, serviço e repositório. Cada camada interage com a camada abaixo dela através de interfaces.

Refatoramos o aplicativo para tornar o aplicativo mais fácil de manter e modificar. Por exemplo, se precisarmos usar uma nova tecnologia de acesso a dados, podemos simplesmente alterar a camada do repositório sem tocar no controlador ou na camada de serviço. Ao tornar o Contact Manager livremente acoplado, fizemos o aplicativo mais resistente à mudança.

Mas, o que acontece quando precisamos adicionar um novo recurso ao aplicativo Contact Manager? Ou, o que acontece quando consertamos um inseto? Uma triste, mas bem comprovada, verdade de escrever código é que sempre que você toca código você cria o risco de introduzir novos bugs.

Por exemplo, um belo dia, seu gerente pode pedir que você adicione um novo recurso ao Gerenciador de Contatos. Ela quer que você adicione suporte para grupos de contato. Ela quer que você habilite os usuários a organizar seus contatos em grupos como Amigos, Negócios e assim por diante.

Para implementar esse novo recurso, você precisará modificar todas as três camadas do aplicativo Contact Manager. Você precisará adicionar novas funcionalidades aos controladores, à camada de serviço e ao repositório. Assim que você começa a modificar código, você corre o risco de quebrar a funcionalidade que funcionou antes.

Refatorar nossa aplicação em camadas separadas, como fizemos na iteração anterior, foi uma coisa boa. Foi uma coisa boa porque nos permite fazer alterações em camadas inteiras sem tocar no resto da aplicação. No entanto, se você quiser tornar o código dentro de uma camada mais fácil de manter e modificar, você precisa criar testes unitários para o código.

Você usa um teste de unidade para testar uma unidade individual de código. Essas unidades de código são menores do que camadas inteiras de aplicação. Normalmente, você usa um teste de unidade para verificar se um determinado método em seu código se comporta da maneira que você espera. Por exemplo, você criaria um teste de unidade para o método CreateContact() exposto pela classe ContactManagerService.

Os testes unitários para uma aplicação funcionam como uma rede de segurança. Sempre que você modificar o código em um aplicativo, você pode executar um conjunto de testes unitários para verificar se a modificação quebra a funcionalidade existente. Testes unitários tornam seu código seguro para modificar. Testes unitários tornam todo o código em sua aplicação mais resistente à alteração.

Nesta iteração, adicionamos testes unitários ao nosso aplicativo de Contact Manager. Dessa forma, na próxima iteração, podemos adicionar Grupos de Contato ao nosso aplicativo sem nos preocuparmos em quebrar a funcionalidade existente.

> [!NOTE] 
> 
> Existem uma variedade de estruturas de teste de unidade, incluindo NUnit, xUnit.net e MbUnit. Neste tutorial, usamos a estrutura de testes unitária incluída no Visual Studio. No entanto, você poderia facilmente usar uma dessas estruturas alternativas.

## <a name="what-gets-tested"></a>O que é testado

No mundo perfeito, todo o seu código seria coberto por testes unitários. No mundo perfeito, você teria a rede de segurança perfeita. Você seria capaz de modificar qualquer linha de código em seu aplicativo e saber instantaneamente, executando seus testes unitários, se a alteração quebrou a funcionalidade existente.

No entanto, não vivemos em um mundo perfeito. Na prática, ao escrever testes unitários, você se concentra em escrever testes para a lógica do seu negócio (por exemplo, lógica de validação). Em particular, você *não* escreve testes unitários para sua lógica de acesso a dados ou sua lógica de visualização.

Para ser útil, os testes unitários devem ser executados muito rapidamente. Você pode facilmente acumular centenas (ou até milhares) de testes unitários para uma aplicação. Se os testes da unidade demorarem muito para serem executados, então você evitará executá-los. Em outras palavras, testes de unidade de longa duração são inúteis para fins de codificação diária.

Por essa razão, você normalmente não escreve testes de unidade para código que interage com um banco de dados. Executar centenas de testes de unidade em um banco de dados ao vivo seria muito lento. Em vez disso, você zomba do seu banco de dados e escreve código que interage com o banco de dados simulado (discutimos zombar de um banco de dados abaixo).

Por uma razão semelhante, você normalmente não escreve testes de unidade para visualizações. Para testar uma visualização, você deve girar um servidor web. Como girar um servidor web é um processo relativamente lento, não é recomendado criar testes unitários para suas visualizações.

Se sua visão contém lógica complicada, então você deve considerar mover a lógica para métodos auxiliares. Você pode escrever testes unitários para métodos auxiliares que executam sem girar um servidor web.

> [!NOTE] 
> 
> Embora escrever testes para lógica de acesso a dados ou lógica de visualização não seja uma boa ideia ao escrever testes de unidade, esses testes podem ser muito valiosos ao construir testes funcionais ou de integração.

> [!NOTE] 
> 
> ASP.NET MVC é o Mecanismo de Exibição de Formulários da Web. Embora o Web Forms View Engine dependa de um servidor web, outros mecanismos de exibição podem não ser.

## <a name="using-a-mock-object-framework"></a>Usando uma estrutura de objeto simulado

Ao construir testes de unidade, você quase sempre precisa tirar proveito de uma estrutura de Objeto Simulado. Uma estrutura mock Object permite que você crie simulações e stubs para as classes em seu aplicativo.

Por exemplo, você pode usar uma estrutura de objeto simulado para gerar uma versão simulada da sua classe de repositório. Dessa forma, você pode usar a classe de repositório simulado em vez da classe de repositório real em seus testes unitários. O uso do repositório simulado permite evitar a execução do código do banco de dados ao executar um teste de unidade.

O Visual Studio não inclui uma estrutura mock object. No entanto, existem várias estruturas de objetomock comercial e de código aberto disponíveis para a estrutura .NET:

1. Moq - Esta estrutura está disponível sob a licença BSD de código aberto. Você pode baixar [https://code.google.com/p/moq/](https://code.google.com/p/moq/)Moq de .
2. Rhino Mocks - Esta estrutura está disponível sob a licença BSD de código aberto. Você pode baixar Rhino [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)Mocks de .
3. Typemock Isolator - Esta é uma estrutura comercial. Você pode baixar uma [http://www.typemock.com/](http://www.typemock.com/)versão de teste de .

Neste tutorial, resolvi usar o Moq. No entanto, você poderia facilmente usar Rhino Mocks ou Typemock Isolator para criar os objetos Mock para o aplicativo Contact Manager.

Antes de usar o Moq, você precisa completar as seguintes etapas:

1. .
2. Antes de abrir o zíper do download, certifique-se de clicar com o botão com o botão e-se clicar no botão denominado **Desbloquear** (ver Figura 1).
3. Descompacte o download.
4. Adicione uma referência ao conjunto Moq clicando com o botão direito do mouse na pasta Referências no projeto ContactManager.Tests e selecionando **Adicionar referência**. Na guia Procurar, navegue até a pasta onde você descompactou moq e selecione o conjunto Moq.dll. Clique no botão **OK**.
5. Depois de concluir essas etapas, sua pasta Referências deve se parecer com a Figura 2.

[![Desbloqueando Moq](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)

**Figura 01**: Desbloqueando moq[(Clique para ver imagem em tamanho real](iteration-5-create-unit-tests-cs/_static/image2.png))

[![Referências após a adição do Moq](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)

**Figura 02**: Referências após a adição de Moq[(Clique para exibir imagem em tamanho real)](iteration-5-create-unit-tests-cs/_static/image4.png)

## <a name="creating-unit-tests-for-the-service-layer"></a>Criando testes unitários para a camada de serviço

Vamos começar criando um conjunto de testes unitários para a camada de serviço do aplicativo do Contact Manager. Usaremos esses testes para verificar nossa lógica de validação.

Crie uma nova pasta chamada Modelos no projeto ContactManager.Tests. Em seguida, clique com o botão direito do mouse na pasta Modelos e **selecione Adicionar, Novo Teste**. A caixa de diálogo **Adicionar novo teste** mostrada na Figura 3 é exibida. Selecione o modelo **de teste** de unidade e nomeie seu novo teste ContactManagerServiceTest.cs. Clique no botão **OK** para adicionar seu novo teste ao seu Projeto de Teste.

> [!NOTE] 
> 
> Em geral, você quer que a estrutura de pasta do seu Projeto de Teste corresponda à estrutura da pasta do seu projeto MVC ASP.NET. Por exemplo, você coloca testes de controlador em uma pasta Controllers, modela testes em uma pasta Models e assim por diante.

[![Modelos\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)

**Figura 03:** Modelos\ContactManagerServiceTest.cs[(Clique para exibir imagem em tamanho real)](iteration-5-create-unit-tests-cs/_static/image6.png)

Inicialmente, queremos testar o método CreateContact() exposto pela classe ContactManagerService. Criaremos os seguintes cinco testes:

- CreateContact() - Testes que CreateContact() devolve o valor verdadeiro quando um Contato válido é passado para o método.
- CreateContactRequiredFirstName() - Testa que uma mensagem de erro é adicionada ao estado do modelo quando um contato com um primeiro nome ausente é passado para o método CreateContact().
- CreateContactRequiredLastName() - Testa que uma mensagem de erro é adicionada ao estado do modelo quando um contato com um sobrenome ausente é passado para o método CreateContact().
- CreateContactInvalidPhone() - Testa que uma mensagem de erro é adicionada ao estado do modelo quando um contato com um número de telefone inválido é passado para o método CreateContact().
- CreateContactInvalidEmail() - Testa que uma mensagem de erro é adicionada ao estado modelo quando um contato com um endereço de e-mail inválido é passado para o método CreateContact().

O primeiro teste verifica se um Contato válido não gera um erro de validação. Os demais testes verificam cada uma das regras de validação.

O código para estes testes está contido na Lista 1.

**Listagem 1 - Modelos\ContactManagerServiceTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]

Como usamos a classe Contato na Listagem 1, precisamos adicionar uma referência ao Microsoft Entity Framework ao nosso projeto de teste. Adicione uma referência ao conjunto System.Data.Entity.

A listagem 1 contém um método chamado Initialize() que é decorado com o atributo [TestInitialize]. Este método é chamado automaticamente antes de cada um dos testes unitários ser executado (é chamado 5 vezes antes de cada um dos testes unitários). O método Initialize() cria um repositório simulado com a seguinte linha de código:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

Esta linha de código usa a estrutura Moq para gerar um repositório simulado a partir da interface IContactManagerRepository. O repositório simulado é usado em vez do repositório entidaderealContactManagerRepository para evitar acessar o banco de dados quando cada teste de unidade é executado. O repositório simulado implementa os métodos da interface IContactManagerRepository, mas os métodos não fazem nada.

> [!NOTE] 
> 
> Ao usar a estrutura Moq, \_há uma distinção \_entre mockRepository e mockRepository.Object. O primeiro refere-se&lt;à classe Mock&gt; IContactManagerRepository que contém métodos para especificar como o repositório simulado se comportará. Este último refere-se ao repositório simulado real que implementa a interface IContactManagerRepository.

O repositório simulado é usado no método Initialize() ao criar uma instância da classe ContactManagerService. Todos os testes individuais da unidade usam esta instância da classe ContactManagerService.

A listagem 1 contém cinco métodos que correspondem a cada um dos testes unitários. Cada um desses métodos é decorado com o atributo [TestMethod]. Quando você executa os testes unitários, qualquer método que tenha esse atributo é chamado. Em outras palavras, qualquer método que seja decorado com o atributo [TestMethod] é um teste de unidade.

O primeiro teste de unidade, chamado CreateContact(), verifica se a chamada CreateContact() retorna o valor verdadeiro quando uma instância válida da classe Contato é passada para o método. O teste cria uma instância da classe Contato, chama o método CreateContact() e verifica se CreateContact() retorna o valor verdadeiro.

Os testes restantes verificam que quando o método CreateContact() é chamado com um contato inválido, o método retorna falso e a mensagem de erro de validação esperada é adicionada ao estado do modelo. Por exemplo, o teste CreateContactRequiredFirstName() cria uma instância da classe Contato com uma seqüência de string vazia para sua propriedade FirstName. Em seguida, o método CreateContact() é chamado com o Contato inválido. Finalmente, o teste verifica se o CreateContact() retorna falso e esse estado do modelo contém a mensagem de erro de validação esperada "O primeiro nome é necessário".

Você pode executar os testes unitários na Listagem 1 selecionando a opção de menu **Teste, Execução, Todos os Testes em Solução (CTRL+R, A)**. Os resultados dos testes são exibidos na janela Resultados do Teste (ver Figura 4).

[![Resultados do teste](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)

**Figura 04**: Resultados do teste[(Clique para ver a imagem em tamanho real](iteration-5-create-unit-tests-cs/_static/image8.png))

## <a name="creating-unit-tests-for-controllers"></a>Criação de testes unitários para controladores

O aplicativo ASP.NETMVC controla o fluxo de interação do usuário. Ao testar um controlador, você deseja testar se o controlador retorna o resultado de ação certo e visualiza os dados. Você também pode querer testar se um controlador interage com as classes de modelo da maneira esperada.

Por exemplo, a Listagem 2 contém dois testes de unidade para o método Criar() do controlador de contato. O primeiro teste de unidade verifica que quando um contato válido é passado para o método Criar() o método Criar() redireciona para a ação Índice. Em outras palavras, quando aprovado um contato válido, o método Criar() deve retornar um RedirectToRouteResult que representa a ação Índice.

Não queremos testar a camada de serviço ContactManager quando estamos testando a camada do controlador. Portanto, simulamos a camada de serviço com o seguinte código no método Initialize:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

No teste da unidade CreateValidContact(), zombamos do comportamento de chamar o método CreateContact() da camada de serviço com a seguinte linha de código:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

Essa linha de código faz com que o serviço mock ContactManager retorne o valor verdadeiro quando seu método CreateContact() é chamado. Ao zombar da camada de serviço, podemos testar o comportamento do nosso controlador sem precisar executar qualquer código na camada de serviço.

O segundo teste de unidade verifica se a ação Criar() retorna a exibição Criar quando um contato inválido é passado para o método. Fazemos com que o método CreateContact() da camada de serviço dedevolva o valor falso com a seguinte linha de código:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

Se o método Criar() se comportar como esperamos, ele deve retornar a exibição Criar quando a camada de serviço retornar o valor falso. Dessa forma, o controlador pode exibir as mensagens de erro de validação na exibição Criar e o usuário tem a chance de corrigir essas propriedades de contato inválidas.

Se você planeja construir testes unitários para seus controladores, então você precisa retornar nomes de exibição explícitos das ações do seu controlador. Por exemplo, não retorne uma visão como esta:

exibição de retorno();

Em vez disso, retorne a visão assim:

exibição de retorno ("Criar");

Se você não estiver explícito ao retornar uma exibição, a propriedade ViewResult.ViewName retorna uma seqüência de string sumida.

**Listagem 2 - Controladores\ContactControllerTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a>Resumo

Nesta iteração, criamos testes unitários para o aplicativo Contact Manager. Podemos executar esses testes unitários a qualquer momento para verificar se nossa aplicação ainda se comporta da maneira que esperamos. Os testes unitários atuam como uma rede de segurança para nossa aplicação, permitindo-nos modificar nossa aplicação com segurança no futuro.

Criamos dois conjuntos de testes unitários. Primeiro, testamos nossa lógica de validação criando testes unitários para nossa camada de serviço. Em seguida, testamos nossa lógica de controle de fluxo criando testes unitários para nossa camada de controlador. Ao testar nossa camada de serviço, isolamos nossos testes para nossa camada de serviço de nossa camada de repositório zombando de nossa camada de repositório. Ao testar a camada do controlador, isolamos nossos testes para a camada do controlador zombando da camada de serviço.

Na próxima iteração, modificamos o aplicativo Contact Manager para que ele suporte grupos de contato. Adicionaremos essa nova funcionalidade ao nosso aplicativo usando um processo de design de software chamado desenvolvimento orientado por testes.

> [!div class="step-by-step"]
> [Próximo](iteration-4-make-the-application-loosely-coupled-cs.md)
> [anterior](iteration-6-use-test-driven-development-cs.md)
