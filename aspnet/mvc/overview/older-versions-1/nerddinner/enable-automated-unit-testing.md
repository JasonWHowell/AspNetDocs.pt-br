---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: Habilitar testes automatizados de unidades | Microsoft Docs
author: rick-anderson
description: O passo 12 mostra como desenvolver um conjunto de testes automatizados de unidades que verificam nossa funcionalidade nerdDinner, e que nos dará a confiança para fazer mudanças...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541462"
---
# <a name="enable-automated-unit-testing"></a>Habilitar o teste de unidade automatizado

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 12 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O passo 12 mostra como desenvolver um conjunto de testes automatizados de unidades que verificam nossa funcionalidade NerdDinner, e que nos dará a confiança para fazer mudanças e melhorias na aplicação no futuro.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner Passo 12: Testes unitários

Vamos desenvolver um conjunto de testes automatizados de unidades que verificam nossa funcionalidade NerdDinner, e que nos dará a confiança para fazer mudanças e melhorias na aplicação no futuro.

### <a name="why-unit-test"></a>Por que teste unitário?

No caminho para o trabalho uma manhã você tem um flash repentino de inspiração sobre um aplicativo que você está trabalhando. Você percebe que há uma mudança que você pode implementar que tornará a aplicação dramaticamente melhor. Pode ser uma refatoração que limpa o código, adiciona um novo recurso ou corrige um bug.

A pergunta que o confronta quando você chega ao seu computador é : "quão seguro é fazer essa melhoria?" E se fazer a mudança tiver efeitos colaterais ou quebrar alguma coisa? A mudança pode ser simples e levar apenas alguns minutos para ser implementada, mas e se levar horas para testar manualmente todos os cenários do aplicativo? E se você esquecer de cobrir um cenário e uma aplicação quebrada entrar em produção? Fazer essa melhoria realmente vale todo o esforço?

Testes automatizados de unidades podem fornecer uma rede de segurança que permite que você melhore continuamente suas aplicações e evite ter medo do código em que você está trabalhando. Ter testes automatizados que verificam rapidamente a funcionalidade permite que você codifique com confiança – e o capacite a fazer melhorias que você pode não ter se sentido confortável em fazer. Eles também ajudam a criar soluções que são mais mantenedoras e têm uma vida útil mais longa - o que leva a um retorno muito maior do investimento.

O ASP.NET MVC Framework facilita e é natural a funcionalidade do aplicativo de teste unitário. Ele também permite um fluxo de trabalho TDD (Test Driven Development, desenvolvimento orientado por teste) que permite o desenvolvimento baseado em primeiro teste.

### <a name="nerddinnertests-project"></a>Projeto NerdDinner.Tests

Quando criamos nosso aplicativo NerdDinner no início deste tutorial, fomos solicitados com um diálogo perguntando se queríamos criar um projeto de teste de unidade para acompanhar o projeto do aplicativo:

![](enable-automated-unit-testing/_static/image1.png)

Mantivemos o botão de rádio "Sim, crie um projeto de teste de unidade" selecionado – o que resultou em um projeto "NerdDinner.Tests" sendo adicionado à nossa solução:

![](enable-automated-unit-testing/_static/image2.png)

O projeto NerdDinner.Tests faz referência à montagem do projeto do aplicativo NerdDinner e nos permite adicionar facilmente testes automatizados a ele que verifiquem a funcionalidade do aplicativo.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>Criando testes unitários para nossa classe modelo de jantar

Vamos adicionar alguns testes ao nosso projeto NerdDinner.Tests que verificam a aula de Jantar que criamos quando construímos nossa camada de modelo.

Começaremos criando uma nova pasta dentro do nosso projeto de teste chamado "Modelos", onde colocaremos nossos testes relacionados ao modelo. Em seguida, clique com o botão direito do mouse na pasta e escolha o comando **Adicionar-Novo&gt;menu de teste.** Isso trará a caixa de diálogo "Adicionar novo teste".

Escolheremos criar um "Teste de Unidade" e nomeá-lo "DinnerTest.cs":

![](enable-automated-unit-testing/_static/image3.png)

Quando clicarmos no botão "ok" o Visual Studio adicionará (e abrirá) um arquivo DinnerTest.cs ao projeto:

![](enable-automated-unit-testing/_static/image4.png)

O modelo de teste padrão da unidade Visual Studio tem um monte de código de placa de caldeira dentro dele que eu acho um pouco confuso. Vamos limpá-lo para conter o código abaixo:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

O atributo [TestClass] na classe DinnerTest acima o identifica como uma classe que conterá testes, bem como inicialização de teste opcional e código de teardown. Podemos definir testes dentro dele adicionando métodos públicos que têm um atributo [TestMethod] neles.

Abaixo estão os primeiros de dois testes que vamos adicionar que o exercício nossa aula de jantar. O primeiro teste verifica se nosso Jantar é inválido se um novo Jantar for criado sem que todas as propriedades sejam definidas corretamente. O segundo teste verifica se nosso Jantar é válido quando um Jantar tem todas as propriedades definidas com valores válidos:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

Você notará acima que nossos nomes de teste são muito explícitos (e um pouco verbosos). Estamos fazendo isso porque podemos acabar criando centenas ou milhares de pequenos testes, e queremos facilitar a determinação rápida da intenção e comportamento de cada um deles (especialmente quando estamos olhando através de uma lista de falhas em um corredor de teste). Os nomes dos testes devem ser nomeados após a funcionalidade que estão testando. Acima estamos usando um\_padrão\_de nomeação "Noun Should Verb".

Estamos estruturando os testes usando o padrão de teste "AAA" – que significa "Organizar, Agir, Afirmar":

- Organizar: Configurar a unidade que está sendo testada
- Ato: Exercite a unidade sob resultados de teste e captura
- Afirmar: Verificar o comportamento

Quando fazemos testes, queremos evitar que os testes individuais façam demais. Em vez disso, cada teste deve verificar apenas um único conceito (o que tornará muito mais fácil identificar a causa das falhas). Uma boa orientação é tentar e ter apenas uma única declaração de afirmação para cada teste. Se você tiver mais de uma afirmação em um método de teste, certifique-se de que todos eles estão sendo usados para testar o mesmo conceito. Na dúvida, faça outro teste.

### <a name="running-tests"></a>Executando testes

Visual Studio 2008 Professional (e edições superiores) inclui um corredor de teste embutido que pode ser usado para executar projetos de teste de unidade visual studio dentro do IDE. Podemos selecionar o **comando&gt;Test-Run-&gt;All Tests in Solution** menu (ou tipo Ctrl R, A) para executar todos os testes da unidade. Ou, alternativamente, podemos posicionar nosso cursor dentro de uma classe de teste específica ou método de teste e usar o comando **Test-Run-Tests&gt;&gt;in Current Context menu** (ou tipo Ctrl R, T) para executar um subconjunto dos testes da unidade.

Vamos posicionar nosso cursor dentro da classe DinnerTest e digitar "Ctrl R, T" para executar os dois testes que acabamos de definir. Quando fizermos isso, uma janela "Resultados de teste" aparecerá dentro do Visual Studio e veremos os resultados da nossa série de testes listadas nele:

![](enable-automated-unit-testing/_static/image5.png)

*Nota: A janela de resultados do teste VS não mostra a coluna Nome de Classe por padrão. Você pode adicionar isso clicando com o botão direito do mouse na janela Resultados de teste e usando o comando Adicionar/Remover colunas do menu.*

Nossos dois testes levaram apenas uma fração de segundo para serem executados – e como você pode ver, ambos passaram. Agora podemos continuar e aumentá-los criando testes adicionais que verificam validações de regras específicas, bem como cobrir os dois métodos auxiliares - IsUserHost() e IsUserRegistered() – que adicionamos à classe Jantar. Ter todos esses testes em vigor para a aula de Jantar tornará muito mais fácil e seguro adicionar novas regras de negócios e validações a ele no futuro. Podemos adicionar nossa nova lógica de regras ao Jantar, e em segundos verificar que ele não quebrou nenhuma de nossas funcionalidades lógicas anteriores.

Observe como o uso de um nome de teste descritivo torna fácil entender rapidamente o que cada teste está verificando. Recomendo usar o comando **De dicas de&gt;ferramentas,** abrir a tela de configuração de execução de testes e&gt;verificar o resultado da unidade "Clicando duas vezes ou inconclusivos, exibe o ponto de falha na caixa de seleção do teste". Isso permitirá que você clique duas vezes em uma falha na janela de resultados do teste e pule imediatamente para a falha de afirmação.

### <a name="creating-dinnerscontroller-unit-tests"></a>Criando jantaresTestes unitários do Controlador

Vamos agora criar alguns testes de unidade que verifiquem nossa funcionalidade DinnersController. Começaremos clicando com o botão direito do mouse na pasta "Controladores" dentro do nosso projeto de teste e, em seguida, escolhero o comando **Adicionar-&gt;Novo menu de teste.** Vamos criar um "Teste de Unidade" e nomeá-lo "DinnersControllerTest.cs".

Criaremos dois métodos de teste que verificam o método de ação Details() no DinnersController. O primeiro verificará se uma exibição é devolvida quando um jantar existente é solicitado. A segunda verificará se uma exibição "NotFound" é retornada quando um Jantar inexistente é solicitado:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

O código acima compila limpo. Quando fazemos os testes, porém, ambos falham:

![](enable-automated-unit-testing/_static/image6.png)

Se olharmos para as mensagens de erro, veremos que a razão pela qual os testes falharam foi porque nossa turma do DinnersRepository não conseguiu se conectar a um banco de dados. Nosso aplicativo NerdDinner está usando uma seqüência de conexões para um\_arquivo local do SQL Server Express que vive sob o diretório \App Data do projeto do aplicativo NerdDinner. Como nosso projeto NerdDinner.Tests compila e executa em um diretório diferente, então o projeto do aplicativo, a localização relativa do caminho da nossa cadeia de conexão está incorreta.

*Podemos* corrigir isso copiando o arquivo de banco de dados SQL Express para o nosso projeto de teste e, em seguida, adicionar uma seqüência de conexão de teste apropriada para ele no App.config do nosso projeto de teste. Isso faria com que os testes acima desbloqueassem e funcionassem.

O código de teste unitário usando um banco de dados real, no entanto, traz consigo uma série de desafios. Especificamente:

- Diminui significativamente o tempo de execução dos testes unitários. Quanto mais tempo demorar para executar testes, menor a probabilidade de executá-los com freqüência. Idealmente, você quer que os testes da sua unidade sejam executados em segundos – e que seja algo que você faça tão naturalmente quanto compilar o projeto.
- Complica a lógica de configuração e limpeza dentro dos testes. Você quer que cada teste de unidade seja isolado e independente dos outros (sem efeitos colaterais ou dependências). Ao trabalhar contra um banco de dados real, você tem que estar atento ao estado e redefini-lo entre os testes.

Vamos olhar para um padrão de design chamado "injeção de dependência" que pode nos ajudar a contornar esses problemas e evitar a necessidade de usar um banco de dados real com nossos testes.

### <a name="dependency-injection"></a>Injeção de dependência

Neste momento, dinnersController está firmemente "acoplado" à classe DinnerRepository. "Acoplamento" refere-se a uma situação em que uma classe depende explicitamente de outra classe para funcionar:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

Como a classe DinnerRepository requer acesso a um banco de dados, a dependência acoplada que a classe DinnersController tem no DinnerRepository acaba exigindo que tenhamos um banco de dados para que os métodos de ação DinnersController sejam testados.

Podemos contornar isso empregando um padrão de design chamado "injeção de dependência" – que é uma abordagem onde as dependências (como classes de repositório que fornecem acesso aos dados) não são mais criadas implicitamente dentro de classes que as usam. Em vez disso, as dependências podem ser explicitamente passadas para a classe que as usa usando argumentos de construtores. Se as dependências forem definidas usando interfaces, então temos a flexibilidade de passar em implementações de dependência "falsas" para cenários de teste de unidade. Isso nos permite criar implementações de dependência específicas de teste que não requerem acesso a um banco de dados.

Para ver isso em ação, vamos implementar injeção de dependência com o nosso DinnersController.

#### <a name="extracting-an-idinnerrepository-interface"></a>Extraindo uma interface IDinnerRepository

Nosso primeiro passo será criar uma nova interface IDinnerRepository que encapsula o contrato de repositório que nossos controladores exigem para recuperar e atualizar Jantares.

Podemos definir este contrato de interface manualmente clicando com o botão direito do mouse na pasta \Modelos e, em seguida, escolhendo o comando **Menu&gt;Adicionar-Novo Item** e criando uma nova interface chamada IDinnerRepository.cs.

Alternativamente, podemos usar as ferramentas de refatoração incorporadas ao Visual Studio Professional (e edições superiores) para extrair e criar automaticamente uma interface para nós a partir de nossa classe DinnerRepository existente. Para extrair essa interface usando VS, basta posicionar o cursor no editor de texto na classe DinnerRepository e, em seguida, clicar com o botão direito do mouse e escolher o comando **Menu&gt;Refator-Extract Interface:**

![](enable-automated-unit-testing/_static/image7.png)

Isso iniciará a caixa de diálogo "Extrair interface" e nos solicitará o nome da interface a ser criada. Ele será padrão para iDinnerRepository e selecionará automaticamente todos os métodos públicos na classe DinnerRepository existente para adicionar à interface:

![](enable-automated-unit-testing/_static/image8.png)

Quando clicarmos no botão "ok", o Visual Studio adicionará uma nova interface IDinnerRepository ao nosso aplicativo:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

E nossa classe dinnerrepository existente será atualizada para que implemente a interface:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>Atualizando jantaresController para apoiar a injeção de construtores

Agora atualizaremos a classe DinnersController para usar a nova interface.

Atualmente, o DinnersController é codificado de tal forma que seu campo "dinnerRepository" é sempre uma classe DinnerRepository:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

Vamos mudá-lo para que o campo "dinnerRepository" seja do tipo IDinnerRepository em vez de DinnerRepository. Em seguida, adicionaremos dois jantares públicosConstrutores Controlador. Um dos construtores permite que um IDinnerRepository seja aprovado como argumento. O outro é um construtor padrão que usa nossa implementação de DinnerRepository existente:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

Como ASP.NET MVC por padrão cria classes de controladores usando construtores padrão, nosso DinnersController em tempo de execução continuará a usar a classe DinnerRepository para executar o acesso aos dados.

Agora podemos atualizar nossos testes de unidade, no entanto, para passar em uma implementação "falsa" do repositório de jantar usando o construtor de parâmetros. Este repositório de jantar "falso" não exigirá acesso a um banco de dados real e, em vez disso, usará dados de amostra na memória.

#### <a name="creating-the-fakedinnerrepository-class"></a>Criando a classe FakeDinnerRepository

Vamos criar uma aula de FakeDinnerRepository.

Começaremos criando um diretório "Fakes" dentro do nosso projeto NerdDinner.Tests e, em seguida, adicionaremos uma nova classe FakeDinnerRepository a ele (clique com o botão direito do mouse na pasta e escolha **Adicionar-&gt;Nova Classe**):

![](enable-automated-unit-testing/_static/image9.png)

Atualizaremos o código para que a classe FakeDinnerRepository implemente a interface IDinnerRepository. Em seguida, podemos clicar com o botão direito do mouse nele e escolher o menu de menu de contexto "Implementar interface IDinnerRepository":

![](enable-automated-unit-testing/_static/image10.png)

Isso fará com que o Visual Studio adicione automaticamente todos os membros da interface IDinnerRepository à nossa classe FakeDinnerRepository com implementações padrão de "stub out":

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

Podemos então atualizar a implementação do FakeDinnerRepository para&lt;&gt; trabalhar fora de uma coleção de jantar de lista na memória passada a ele como um argumento construtor:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

Agora temos uma implementação falsa do IDinnerRepository que não requer um banco de dados e pode, em vez disso, trabalhar fora de uma lista na memória de objetos do Jantar.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>Usando o FalsoDinnerRepository com testes unitários

Vamos voltar aos testes da unidade DinnersController que falharam antes porque o banco de dados não estava disponível. Podemos atualizar os métodos de teste para usar um FakeDinnerRepository preenchido com dados de jantar de amostra na memória para o DinnersController usando o código abaixo:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

E agora, quando fazemos esses testes, ambos passam:

![](enable-automated-unit-testing/_static/image11.png)

O melhor de tudo é que eles levam apenas uma fração de segundo para serem executados, e não requerem nenhuma lógica complicada de configuração/limpeza. Agora podemos testar todos os nossocódigo do método de ação DinnersController (incluindo listagem, paginação, detalhes, criar, atualizar e excluir) sem nunca precisar se conectar a um banco de dados real.

| **Tópico lateral: Frameworks de injeção de dependência** |
| --- |
| Realizar injeção manual de dependência (como estamos acima) funciona bem, mas torna-se mais difícil de manter à medida que o número de dependências e componentes em uma aplicação aumenta. Existem várias estruturas de injeção de dependência para .NET que podem ajudar a fornecer ainda mais flexibilidade de gerenciamento de dependência. Esses frameworks, também às vezes chamados de contêineres de "Inversão de Controle" (IoC), fornecem mecanismos que permitem um nível adicional de suporte à configuração para especificar e passar dependências para objetos em tempo de execução (na maioria das vezes usando injeção de construtor). Algumas das estruturas mais populares de injeção de dependência do OSS / COI em .NET incluem: AutoFac, Ninject, Spring.NET, StructureMap e Windsor. ASP.NET MVC expõe APIs de extensibilidade que permitem aos desenvolvedores participar na resolução e na instanciação dos controladores, e que permite que as estruturas de Injeção de Dependência/IoC sejam integradas de forma limpa dentro desse processo. O uso de uma estrutura DI/COI também nos permitiria remover o construtor padrão do nosso DinnersController – o que removeria completamente o acoplamento entre ele e o DinnerRepository. Não usaremos uma estrutura de injeção de dependência / COI com nosso aplicativo NerdDinner. Mas é algo que poderíamos considerar para o futuro se a base de códigos nerddinner e capacidades crescessem. |

### <a name="creating-edit-action-unit-tests"></a>Criando testes da unidade de ação de edição

Vamos agora criar alguns testes de unidade que verifiquem a funcionalidade Editar do DinnersController. Começaremos testando a versão HTTP-GET da nossa ação Editar:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

Criaremos um teste que verifica se uma exibição apoiada por um objeto DinnerFormViewModel é renderizada de volta quando um jantar válido é solicitado:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

Quando executamos o teste, porém, descobriremos que ele falha porque uma exceção de referência nula é lançada quando o método Editar acessa a propriedade User.Identity.Name para executar a verificação Dinner.IsHostedBy().

O objeto Usuário na classe base do Controlador encapsula detalhes sobre o usuário conectado e é preenchido por ASP.NET MVC quando cria o controlador em tempo de execução. Como estamos testando o DinnersController fora de um ambiente de servidor web, o objeto Usuário não está definido (daí a exceção de referência nula).

### <a name="mocking-the-useridentityname-property"></a>Zombando da propriedade User.Identity.Name

As estruturas de zombaria facilitam os testes, permitindo-nos criar dinamicamente versões falsas de objetos dependentes que suportam nossos testes. Por exemplo, podemos usar uma estrutura de zombaria em nosso teste de ação Editar para criar dinamicamente um objeto de usuário que nosso DinnersController pode usar para procurar um nome de usuário simulado. Isso evitará que uma referência nula seja lançada quando executarmos nosso teste.

Existem muitos frameworks .NET zombando que podem ser usados com [http://www.mockframeworks.com/](http://www.mockframeworks.com/)ASP.NET MVC (você pode ver uma lista deles aqui: ). Para testar nosso aplicativo NerdDinner, usaremos uma estrutura de zombaria de código [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)aberto chamada "Moq", que pode ser baixada gratuitamente a partir de .

Uma vez baixado, adicionaremos uma referência em nosso projeto NerdDinner.Tests ao conjunto Moq.dll:

![](enable-automated-unit-testing/_static/image12.png)

Em seguida, adicionaremos um método de ajuda "CreateDinnersControllerAs(nome de usuário)" à nossa classe de teste que toma um nome de usuário como parâmetro e que, em seguida, "zomba" da propriedade User.Identity.Name na instância DinnersController:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

Acima estamos usando o Moq para criar um objeto Mock que falsifica um objeto ControllerContext (que é o que ASP.NET MVC passa para as classes Controller para expor objetos de tempo de execução como Usuário, Solicitação, Resposta e Sessão). Estamos chamando o método "SetupGet" no Mock para indicar que a propriedade HttpContext.User.Identity.Name no ControllerContext deve retornar a string de nome de usuário que passamos para o método helper.

Podemos zombar de qualquer número de propriedades e métodos do ControllerContext. Para ilustrar isso, também adicionei uma chamada SetupGet() para a propriedade Request.IsAuthenticated (que não é realmente necessária para os testes abaixo – mas que ajuda a ilustrar como você pode simular propriedades de Solicitação). Quando terminamos, atribuímos uma instância do mock ControllerContext ao DinnersController, nosso método auxiliar retorna.

Agora podemos escrever testes unitários que usam este método auxiliar para testar cenários de edição envolvendo diferentes usuários:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

E agora, quando fazemos os testes, eles passam:

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>Testando os cenários do UpdateModel()

Criamos testes que cobrem a versão HTTP-GET da ação Editar. Vamos agora criar alguns testes que verificam a versão HTTP-POST da ação Editar:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

O novo cenário de teste interessante para suportarmos com este método de ação é o uso do método de ajuda UpdateModel() na classe base controller. Estamos usando este método auxiliar para vincular valores de postagem de formulário à nossa instância de objeto jantar.

Abaixo estão dois testes que demonstram como podemos fornecer valores postados para o método de ajuda UpdateModel() para usar. Faremos isso criando e povoando um objeto FormCollection e, em seguida, atribuiremos-o à propriedade "ValueProvider" no Controller.

O primeiro teste verifica se em um salvamento bem-sucedido o navegador é redirecionado para a ação de detalhes. O segundo teste verifica que, quando a entrada inválida é postada, a ação reexibe a exibição de edição novamente com uma mensagem de erro.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>Ensaio de envoltório

Nós cobrimos os conceitos principais envolvidos nas aulas de controlador de teste da unidade. Podemos usar essas técnicas para criar facilmente centenas de testes simples que verificam o comportamento de nossa aplicação.

Como nossos testes de controlador e modelo não exigem um banco de dados real, eles são extremamente rápidos e fáceis de executar. Seremos capazes de executar centenas de testes automatizados em segundos, e imediatamente obter feedback sobre se uma mudança que fizemos quebrou algo. Isso nos ajudará a fornecer a confiança para melhorar continuamente, refatorar e refinar nossa aplicação.

Cobrimos o teste como último tópico deste capítulo – mas não porque o teste é algo que você deve fazer no final de um processo de desenvolvimento! Pelo contrário, você deve escrever testes automatizados o mais cedo possível em seu processo de desenvolvimento. Isso permite que você obtenha feedback imediato à medida que você se desenvolve, ajuda você a pensar cuidadosamente sobre os cenários de caso de uso do seu aplicativo e orienta você a projetar seu aplicativo com camadas limpas e acoplamento em mente.

Um capítulo posterior do livro discutirá o TDD (Test Driven Development, desenvolvimento conduzido por teste) e como usá-lo com ASP.NET MVC. TDD é uma prática de codificação iterativa onde você escreve primeiro os testes que seu código resultante irá satisfazer. Com o TDD você inicia cada recurso criando um teste que verifica a funcionalidade que você está prestes a implementar. Escrever o teste de unidade primeiro ajuda a garantir que você entenda claramente o recurso e como ele deve funcionar. Somente depois que o teste é escrito (e você verificou que ele falha) você então implementa a funcionalidade real que o teste verifica. Como você já passou um tempo pensando no caso de uso de como o recurso deve funcionar, você terá uma melhor compreensão dos requisitos e a melhor maneira de implementá-los. Quando terminar a implementação, você pode reexecutar o teste – e obter feedback imediato sobre se o recurso funciona corretamente. Vamos cobrir mais TDD no Capítulo 10.

### <a name="next-step"></a>Próxima etapa

Alguns comentários finais.

> [!div class="step-by-step"]
> [Próximo](use-ajax-to-implement-mapping-scenarios.md)
> [anterior](nerddinner-wrap-up.md)
