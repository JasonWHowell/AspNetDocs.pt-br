---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: 'Iteração #4 – Faça o aplicativo livremente acoplado (C#) | Microsoft Docs'
author: rick-anderson
description: Nesta quarta iteração, aproveitamos vários padrões de design de software para facilitar a manutenção e modificação do aplicativo Contact Manager. Para...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: c4ba6c9a130995c095653f4316a5fefdfc03b91d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542359"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>Iteração nº 4 – tornar o aplicativo fracamente acoplado (C#)

pela [Microsoft](https://github.com/microsoft)

[Código de download](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> Nesta quarta iteração, aproveitamos vários padrões de design de software para facilitar a manutenção e modificação do aplicativo Contact Manager. Por exemplo, refatoramos nossa aplicação para usar o padrão repositório e o padrão de injeção de dependência.

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

Nesta quarta iteração do aplicativo Contact Manager, refatoramos o aplicativo para tornar o aplicativo mais livremente acoplado. Quando um aplicativo é acoplado vagamente, você pode modificar o código em uma parte do aplicativo sem precisar modificar o código em outras partes do aplicativo. Aplicações acopladas vagamente são mais resistentes à mudança.

Atualmente, toda a lógica de acesso e validação de dados utilizada pelo aplicativo Contact Manager está contida nas classes de controlador. Isto é uma má ideia. Sempre que você precisar modificar uma parte do seu aplicativo, você corre o risco de introduzir bugs em outra parte do seu aplicativo. Por exemplo, se você modificar sua lógica de validação, corre o risco de introduzir novos bugs em sua lógica de acesso a dados ou controlador.

> [!NOTE] 
> 
> (SRP), uma classe nunca deve ter mais de uma razão para mudar. Misturar a lógica do controlador, da validação e do banco de dados é uma violação maciça do Princípio da Responsabilidade Única.

Existem várias razões pelas quais você pode precisar modificar sua aplicação. Você pode precisar adicionar um novo recurso ao seu aplicativo, talvez precise corrigir um bug em seu aplicativo, ou talvez precise modificar a forma como um recurso do seu aplicativo é implementado. As aplicações raramente são estáticas. Eles tendem a crescer e sofrer mutações ao longo do tempo.

Imagine, por exemplo, que você decida mudar a forma como implementa sua camada de acesso a dados. No momento, o aplicativo Contact Manager usa o Microsoft Entity Framework para acessar o banco de dados. No entanto, você pode decidir migrar para uma tecnologia nova ou alternativa de acesso a dados, como ADO.NET Data Services ou NHibernate. No entanto, como o código de acesso a dados não está isolado do código de validação e do controlador, não há como modificar o código de acesso de dados em seu aplicativo sem modificar outro código que não esteja diretamente relacionado ao acesso aos dados.

Quando um aplicativo é acoplado vagamente, por outro lado, você pode fazer alterações em uma parte de um aplicativo sem tocar em outras partes de um aplicativo. Por exemplo, você pode alternar tecnologias de acesso a dados sem modificar sua lógica de validação ou controlador.

Nesta iteração, aproveitamos vários padrões de design de software que nos permitem refatorar nosso aplicativo Contact Manager em um aplicativo mais vagamente acoplado. Quando terminarmos, o Gerente de Contato não fará nada que não tenha feito antes. No entanto, poderemos mudar o aplicativo mais facilmente no futuro.

> [!NOTE] 
> 
> Refatoração é o processo de reescrever um aplicativo de tal forma que ele não perca nenhuma funcionalidade existente.

## <a name="using-the-repository-software-design-pattern"></a>Usando o padrão de design de software de repositório

Nossa primeira mudança é tirar proveito de um padrão de design de software chamado padrão repositório. Usaremos o padrão do Repositório para isolar nosso código de acesso de dados do resto do nosso aplicativo.

A implementação do padrão repositório requer que completemos as duas etapas seguintes:

1. Criar uma interface
2. Crie uma classe de concreto que implemente a interface

Primeiro, precisamos criar uma interface que descreva todos os métodos de acesso a dados que precisamos executar. A interface IContactManagerRepository está contida na Lista 1. Esta interface descreve cinco métodos: CreateContact(), DeleteContact(), EditContact(), GetContact e ListContacts().

**Listagem 1 - Modelos\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

Em seguida, precisamos criar uma classe de concreto que implemente a interface IContactManagerRepository. Como estamos usando o Microsoft Entity Framework para acessar o banco de dados, criaremos uma nova classe chamada EntityContactManagerRepository. Esta classe está contida na Lista 2.

**Listagem 2 - Modelos\EntidadeContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

Observe que a classe EntityContactManagerRepository implementa a interface IContactManagerRepository. A classe implementa todos os cinco métodos descritos por essa interface.

Você pode se perguntar por que precisamos nos preocupar com uma interface. Por que precisamos criar uma interface e uma classe que a implemente?

Com uma exceção, o restante do nosso aplicativo interagirá com a interface e não com a classe de concreto. Em vez de chamar os métodos expostos pela classe EntityContactManagerRepository, chamaremos os métodos expostos pela interface IContactManagerRepository.

Dessa forma, podemos implementar a interface com uma nova classe sem precisar modificar o restante do nosso aplicativo. Por exemplo, em alguma data futura, podemos querer implementar uma classe DataServicesContactManagerRepository que implementa a interface IContactManagerRepository. A classe DataServicesContactManagerRepository pode usar ADO.NET Data Services para acessar um banco de dados em vez do Microsoft Entity Framework.

Se nosso código de aplicativo for programado contra a interface IContactManagerRepository em vez da classe concreta EntityContactManagerRepository, então podemos alternar classes concretas sem modificar qualquer um dos outros códigos. Por exemplo, podemos mudar da classe EntityContactManagerRepository para a classe DataServicesContactManagerRepository sem modificar nossa lógica de acesso ou validação de dados.

A programação contra interfaces (abstrações) em vez de classes concretas torna nossa aplicação mais resistente à mudança.

> [!NOTE] 
> 
> Você pode criar rapidamente uma interface a partir de uma classe de concreto dentro do Visual Studio selecionando a opção de menu Refactor, Extract Interface. Por exemplo, você pode criar a classe EntityContactManagerRepository primeiro e, em seguida, usar a Interface extrato para gerar a interface IContactManagerRepository automaticamente.

## <a name="using-the-dependency-injection-software-design-pattern"></a>Usando o padrão de design de software de injeção de dependência

Agora que migramos nosso código de acesso de dados para uma classe de repositório separada, precisamos modificar nosso controlador de contato para usar essa classe. Vamos aproveitar um padrão de design de software chamado Dependency Injection para usar a classe Repository em nosso controlador.

O controlador de contato modificado está contido na Lista 3.

**Listagem 3 - Controladores\ContactController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

Observe que o controlador de contato na Listagem 3 possui dois construtores. O primeiro construtor passa uma instância concreta da interface IContactManagerRepository para o segundo construtor. A classe controladora de contato usa *injeção de dependência de constructor*.

O único lugar em que a classe EntityContactManagerRepository é usado é no primeiro construtor. O restante da classe usa a interface IContactManagerRepository em vez da classe concreta EntityContactManagerRepository.

Isso facilita a mudança de implementações da classe IContactManagerRepository no futuro. Se você quiser usar a classe DataServicesContactRepository em vez da classe EntityContactManagerRepository, basta modificar o primeiro construtor.

A injeção de dependência de construtores também torna a classe controlador a conferência de contato muito testada. Nos testes da unidade, você pode instanciar o controlador de contato passando por uma implementação simulada da classe IContactManagerRepository. Este recurso de Injeção de Dependência será muito importante para nós na próxima iteração quando construirmos testes unitários para o aplicativo Contact Manager.

> [!NOTE] 
> 
> Se você quiser desacoplar completamente a classe controlador de contato de uma implementação específica da interface IContactManagerRepository, então você pode tirar proveito de uma estrutura que suporta injeção de dependência, como o StructureMap ou o Microsoft Entity Framework (MEF). Aproveitando uma estrutura de injeção de dependência, você nunca precisa se referir a uma classe concreta em seu código.

## <a name="creating-a-service-layer"></a>Criando uma camada de serviço

Você deve ter notado que nossa lógica de validação ainda está misturada com nossa lógica de controlador na classe de controlador modificado na Listagem 3. Pela mesma razão que é uma boa ideia isolar nossa lógica de acesso a dados, é uma boa ideia isolar nossa lógica de validação.

Para corrigir esse problema, podemos criar uma camada de [*serviço*](http://martinfowler.com/eaaCatalog/serviceLayer.html)separada . A camada de serviço é uma camada separada que podemos inserir entre nossas classes de controlador e repositório. A camada de serviço contém nossa lógica de negócios, incluindo toda a nossa lógica de validação.

O ContactManagerService está contido na Lista 4. Ele contém a lógica de validação da classe controlador a partir de contato.

**Listagem 4 - Modelos\ContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

Observe que o construtor do ContactManagerService requer um Dicionário de Validação. A camada de serviço se comunica com a camada do controlador através deste Dicionário de Validação. Discutimos o Dicionário de Validação em detalhes na seção a seguir quando discutimos o padrão Decorador.

Observe, ainda, que o ContactManagerService implementa a interface IContactManagerService. Você deve sempre se esforçar para programar contra interfaces em vez de classes concretas. Outras classes no aplicativo Contact Manager não interagem diretamente com a classe ContactManagerService. Em vez disso, com uma exceção, o restante do aplicativo Contact Manager é programado contra a interface IContactManagerService.

A interface IContactManagerService está contida na Lista 5.

**Listagem 5 - Modelos\IContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

A classe de controlador de contato modificada está contida na Lista 6. Observe que o controlador de contato não interage mais com o repositório ContactManager. Em vez disso, o controlador de contato interage com o serviço ContactManager. Cada camada é isolada tanto quanto possível de outras camadas.

**Lista 6 - Controladores\ContactController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

Nosso aplicativo não funciona mais em desacordo com o Princípio da Responsabilidade Única (SRP). O controlador de contato na Listagem 6 foi destituído de todas as responsabilidades que não o controle do fluxo de execução do aplicativo. Toda a lógica de validação foi removida do controlador de contato e empurrada para a camada de serviço. Toda a lógica do banco de dados foi empurrada para a camada do repositório.

## <a name="using-the-decorator-pattern"></a>Usando o padrão de decoração

Queremos ser capazes de desacoplar completamente nossa camada de serviço de nossa camada de controlador. Em princípio, devemos ser capazes de compilar nossa camada de serviço em um conjunto separado da nossa camada controladora sem precisar adicionar uma referência ao nosso aplicativo MVC.

No entanto, nossa camada de serviço precisa ser capaz de passar mensagens de erro de validação de volta para a camada do controlador. Como podemos habilitar a camada de serviço para comunicar mensagens de erro de validação sem acoplar o controlador e a camada de serviço? Podemos aproveitar um padrão de design de software chamado [padrão Decorator](http://en.wikipedia.org/wiki/Decorator_pattern).

Um controlador usa um ModelStateDictionary chamado ModelState para representar erros de validação. Portanto, você pode ser tentado a passar ModelState da camada do controlador para a camada de serviço. No entanto, o uso do ModelState na camada de serviço tornaria sua camada de serviço dependente de um recurso da ASP.NET estrutura MVC. Isso seria ruim porque, um dia, você pode querer usar a camada de serviço com um aplicativo WPF em vez de um aplicativo MVC ASP.NET. Nesse caso, você não gostaria de fazer referência à ASP.NET estrutura MVC para usar a classe ModelStateDictionary.

O padrão Decorator permite que você envolva uma classe existente em uma nova classe, a fim de implementar uma interface. Nosso projeto de Contact Manager inclui a classe ModelStateWrapper contida na Lista 7. A classe ModelStateWrapper implementa a interface na Listagem 8.

**Lista 7 - Modelos\Validação\ModelStateWrapper.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**Lista 8 - Modelos\Validação\IValidationDictionary.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

Se você der uma olhada de perto na Lista 5, verá que a camada de serviço ContactManager usa exclusivamente a interface IValidationDictionary. O serviço ContactManager não depende da classe ModelStateDictionary. Quando o controlador de contato cria o serviço ContactManager, o controlador envolve seu ModelState assim:

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>Resumo

Nesta iteração, não adicionamos nenhuma nova funcionalidade ao aplicativo Contact Manager. O objetivo desta iteração foi refatorar o aplicativo Contact Manager para que seja mais fácil de manter e modificar.

Primeiro, implementamos o padrão de design de software repositório. Migramos todo o código de acesso de dados para uma classe de repositório contactmanager separada.

Também isolamos nossa lógica de validação da nossa lógica de controlador. Criamos uma camada de serviço separada que contém todo o nosso código de validação. A camada do controlador interage com a camada de serviço e a camada de serviço interage com a camada do repositório.

Quando criamos a camada de serviço, aproveitamos o padrão Decorator para isolar o ModelState da nossa camada de serviço. Em nossa camada de serviço, programamos contra a interface IValidationDictionary em vez de ModelState.

Finalmente, aproveitamos um padrão de design de software chamado padrão de injeção de dependência. Esse padrão nos permite programar contra interfaces (abstrações) em vez de classes concretas. A implementação do padrão de design de injeção de dependência também torna nosso código mais testado. Na próxima iteração, adicionamos testes unitários ao nosso projeto.

> [!div class="step-by-step"]
> [Próximo](iteration-3-add-form-validation-cs.md)
> [anterior](iteration-5-create-unit-tests-cs.md)
