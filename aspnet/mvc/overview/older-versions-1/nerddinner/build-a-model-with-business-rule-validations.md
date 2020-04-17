---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: Construa um modelo com validações de regras de negócios | Microsoft Docs
author: rick-anderson
description: O passo 3 mostra como criar um modelo que podemos usar tanto para consultar quanto atualizar o banco de dados para o nosso aplicativo NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541631"
---
# <a name="build-a-model-with-business-rule-validations"></a>Compilar um modelo com validações de regra de negócios

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 3 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O passo 3 mostra como criar um modelo que podemos usar tanto para consultar quanto atualizar o banco de dados para o nosso aplicativo NerdDinner.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner Passo 3: Construindo o Modelo

Em uma estrutura modelo-view-controller, o termo "modelo" refere-se aos objetos que representam os dados do aplicativo, bem como à lógica de domínio correspondente que integra as regras de validação e de negócios com ele. O modelo é, em muitos aspectos, o "coração" de um aplicativo baseado em MVC, e como veremos mais tarde, impulsiona fundamentalmente o comportamento dele.

A estrutura ASP.NET MVC suporta o uso de qualquer tecnologia de acesso a dados, e os desenvolvedores podem escolher entre uma variedade de opções de dados .NET ricas para implementar seus modelos, incluindo: LINQ para Entidades, LINQ para SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM ou apenas ADO.NET datareaders ou datasets.

Para o nosso aplicativo NerdDinner, vamos usar linq para SQL para criar um modelo simples que corresponde bastante de perto ao nosso design de banco de dados, e adiciona algumas lógicas de validação personalizadas e regras de negócios. Em seguida, implementaremos uma classe de repositório que ajuda a abstrair a implementação de persistência de dados do resto do aplicativo e nos permite testá-lo facilmente.

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ para SQL é um ORM (mapeador relacional de objetos) que é fornecido como parte do .NET 3.5.

LINQ para SQL fornece uma maneira fácil de mapear tabelas de banco de dados para classes .NET que podemos codificar contra. Para o nosso aplicativo NerdDinner, vamos usá-lo para mapear as tabelas Dinners e RSVP dentro do nosso banco de dados para as aulas de Jantar e RSVP. As colunas das mesas Dinners e RSVP corresponderão às propriedades nas aulas de Jantar e RSVP. Cada objeto Dinner e RSVP representará uma linha separada dentro das tabelas Dinners ou RSVP no banco de dados.

Linq para SQL nos permite evitar ter que construir manualmente instruções SQL para recuperar e atualizar objetos Dinner e RSVP com dados de banco de dados. Em vez disso, definiremos as classes Dinner e RSVP, como eles mapeiam para/a partir do banco de dados e as relações entre eles. Linq para SQL, então, se envida de gerar a lógica de execução SQL apropriada para usar em tempo de execução quando interagirmos e usá-los.

Podemos usar o suporte à linguagem LINQ dentro de VB e C# para escrever consultas expressivas que recuperam objetos Dinner e RSVP do banco de dados. Isso minimiza a quantidade de código de dados que precisamos escrever e nos permite construir aplicativos realmente limpos.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>Adicionando LINQ às Classes SQL ao nosso projeto

Começaremos clicando com o botão direito do mouse na pasta "Modelos" dentro do nosso projeto e selecionaremos o comando **'Adicionar-&gt;Novo item'** menu:

![](build-a-model-with-business-rule-validations/_static/image1.png)

Isso trará a caixa de diálogo "Adicionar novo item". Filtraremos pela categoria "Dados" e selecionaremos o modelo "LINQ para SQL Classes" dentro dele:

![](build-a-model-with-business-rule-validations/_static/image2.png)

Vamos nomear o item "NerdDinner" e clicar no botão "Adicionar". O Visual Studio adicionará um arquivo NerdDinner.dbml em nosso diretório \Models e, em seguida, abrirá o LINQ para o designer relacional de objetoS SQL:

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>Criando classes de modelo de dados com LINQ para SQL

Linq para SQL nos permite criar rapidamente classes de modelos de dados a partir de esquemas de banco de dados existentes. Para fazer isso, abriremos o banco de dados NerdDinner no Server Explorer e selecionaremos as Tabelas que queremos modelar nele:

![](build-a-model-with-business-rule-validations/_static/image4.png)

Podemos então arrastar as tabelas para a superfície do designer LINQ para sql. Quando fizermos isso LINQ para SQL criará automaticamente classes Dinner e RSVP usando o esquema das tabelas (com propriedades de classe que mapeiam as colunas de tabela do banco de dados):

![](build-a-model-with-business-rule-validations/_static/image5.png)

Por padrão, o designer LINQ para SQL "pluraliza" automaticamente nomes de tabela e coluna quando cria classes com base em um esquema de banco de dados. Por exemplo: a tabela "Jantares" em nosso exemplo acima resultou em uma aula de "Jantar". Essa nomenclatura de classe ajuda a tornar nossos modelos consistentes com convenções de nomeação .NET, e eu geralmente acho que ter o designer corrigir isso conveniente (especialmente quando adicionar muitas tabelas). Se você não gosta do nome de uma classe ou propriedade que o designer gera, no entanto, você sempre pode substituí-lo e alterá-lo para qualquer nome que você quiser. Você pode fazer isso editando o nome da entidade/propriedade em linha dentro do designer ou modificando-o através da grade de propriedade.

Por padrão, o designer LINQ para SQL também inspeciona as relações de chave primária/estrangeiras das tabelas e, com base nelas, cria automaticamente "associações de relacionamento" padrão entre as diferentes classes de modelo que cria. Por exemplo, quando arrastamos as mesas Dinners e RSVP para o linq para o designer SQL, uma associação de relacionamento de um a muitos entre os dois foi inferida com base no fato de que a tabela RSVP tinha uma chave estrangeira para a tabela Dinners (isso é indicado pela seta no designer):

![](build-a-model-with-business-rule-validations/_static/image6.png)

A associação acima fará com que linq para SQL adicione uma propriedade "Jantar" fortemente digitada à classe RSVP que os desenvolvedores podem usar para acessar o Jantar associado a um determinado RSVP. Também fará com que a classe Dinner tenha uma propriedade de coleção "RSVPs" que permite aos desenvolvedores recuperar e atualizar objetos RSVP associados a um jantar específico.

Abaixo você pode ver um exemplo de intelisense dentro do Visual Studio quando criamos um novo objeto RSVP e adicionamos-no à coleção RSVPs do jantar. Observe como o LINQ para o SQL adicionou automaticamente uma coleção de "RSVPs" no objeto Jantar:

![](build-a-model-with-business-rule-validations/_static/image7.png)

Adicionando o objeto RSVP à coleção de RSVPs do jantar, estamos dizendo à LINQ ao SQL para associar uma relação de chave estrangeira entre o Jantar e a linha RSVP em nosso banco de dados:

![](build-a-model-with-business-rule-validations/_static/image8.png)

Se você não gosta de como o designer modelou ou nomeou uma associação de mesa, você pode substituí-lo. Basta clicar na seta de associação dentro do designer e acessar suas propriedades através da grade de propriedade para renomeá-la, excluí-la ou modificá-la. Para o nosso aplicativo NerdDinner, porém, as regras de associação padrão funcionam bem para as classes de modelo de dados que estamos construindo e podemos apenas usar o comportamento padrão.

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext Class

O Visual Studio criará automaticamente classes .NET que representam os modelos e relacionamentos de banco de dados definidos usando o designer LINQ para SQL. Uma classe LINQ para SQL DataContext também é gerada para cada arquivo de designer LINQ para SQL adicionado à solução. Como nomeamos nosso item de classe LINQ para SQL "NerdDinner", a classe DataContext criada será chamada de "NerdDinnerDataContext". Esta aula nerdDinnerDataContext é a principal maneira de interagir com o banco de dados.

Nossa classe NerdDinnerDataContext expõe duas propriedades - "Dinners" e "RSVPs" - que representam as duas tabelas que modelamos dentro do banco de dados. Podemos usar C# para escrever consultas LINQ contra essas propriedades para consultar e recuperar objetos Dinner e RSVP do banco de dados.

O código a seguir demonstra como instanciar um objeto NerdDinnerDataContext e realizar uma consulta LINQ contra ele para obter uma seqüência de Jantares que ocorrem no futuro. O Visual Studio fornece intellisense completo ao escrever a consulta LINQ, e os objetos devolvidos a partir dele são fortemente digitados e também suportam o intellisense:

![](build-a-model-with-business-rule-validations/_static/image9.png)

Além de nos permitir consultar objetos de Jantar e RSVP, um NerdDinnerDataContext também rastreia automaticamente quaisquer alterações que fazemos posteriormente para os objetos Dinner e RSVP que recuperamos através dele. Podemos usar essa funcionalidade para salvar facilmente as alterações de volta ao banco de dados - sem ter que escrever qualquer código explícito de atualização SQL.

Por exemplo, o código abaixo demonstra como usar uma consulta LINQ para recuperar um único objeto do Dinner do banco de dados, atualizar duas propriedades do Jantar e, em seguida, salvar as alterações de volta ao banco de dados:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

O objeto NerdDinnerDataContext no código acima rastreou automaticamente as alterações de propriedade feitas no objeto Dinner que recuperamos dele. Quando chamamos o método "SubmitChanges()", ele executará uma declaração apropriada de "ATUALIZAÇÃO" SQL para o banco de dados para persistir os valores atualizados de volta.

### <a name="creating-a-dinnerrepository-class"></a>Criando uma Aula de Repositório de Jantar

Para aplicações pequenas, às vezes é bom que os controladores trabalhem diretamente contra uma classe LINQ para SQL DataContext e incorporem consultas LINQ dentro dos Controladores. À medida que as aplicações ficam maiores, porém, essa abordagem se torna complicada para manter e testar. Também pode nos levar a duplicar as mesmas consultas LINQ em vários lugares.

Uma abordagem que pode tornar os aplicativos mais fáceis de manter e testar é usar um padrão de "repositório". Uma classe de repositório ajuda a encapsular a lógica de consulta e persistência de dados e abstrai os detalhes de implementação da persistência de dados do aplicativo. Além de tornar o código de aplicativo mais limpo, o uso de um padrão de repositório pode facilitar a alteração das implementações de armazenamento de dados no futuro, e pode ajudar a facilitar o teste de unidade de um aplicativo sem precisar de um banco de dados real.

Para o nosso aplicativo NerdDinner, definiremos uma aula de DinnerRepository com a assinatura abaixo:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*Nota: Mais tarde, neste capítulo, extraíremos uma interface IDinnerRepository desta classe e habilitaremos a injeção de dependência com ela em nossos Controladores. Para começar, porém, vamos começar simples e apenas trabalhar diretamente com a classe DinnerRepository.*

Para implementar esta classe, clicaremos com o botão direito do mouse em nossa pasta "Modelos" e escolheremos o comando **'Adicionar-&gt;Novo item** menu'. Na caixa de diálogo "Adicionar novo item", selecionaremos o modelo "Classe" e nomearemos o arquivo "DinnerRepository.cs":

![](build-a-model-with-business-rule-validations/_static/image10.png)

Podemos então implementar nossa classe DinnerRepository usando o código abaixo:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>Recuperando, atualizando, inserindo e excluindo usando a classe DinnerRepository

Agora que criamos nossa aula de DinnerRepository, vamos olhar alguns exemplos de código que demonstram tarefas comuns que podemos fazer com ela:

#### <a name="querying-examples"></a>Exemplos de consulta

O código abaixo recupera um único Jantar usando o valor DinnerID:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

O código abaixo recupera todos os jantares próximos e loops sobre eles:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>Inserir e atualizar exemplos

O código abaixo demonstra a adição de dois novos jantares. As adições/modificações no repositório não são comprometidas no banco de dados até que o método "Salvar()" seja chamado nele. Linq para SQL envolve automaticamente todas as alterações em uma transação de banco de dados – de modo que todas as alterações acontecem ou nenhuma delas acontece quando nosso repositório salva:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

O código abaixo recupera um objeto de Jantar existente e modifica duas propriedades nele. As alterações são comprometidas de volta ao banco de dados quando o método "Salvar()" é chamado em nosso repositório:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

O código abaixo recupera um jantar e, em seguida, adiciona um RSVP a ele. Ele faz isso usando a coleção de RSVPs no objeto Dinner que linq para SQL criou para nós (porque há uma relação de chave primária/chave estrangeira entre os dois no banco de dados). Essa alteração é persistida de volta ao banco de dados como uma nova linha de tabela RSVP quando o método "Salvar()" é chamado no repositório:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Excluir exemplo

O código abaixo recupera um objeto de Jantar existente e, em seguida, marca-o para ser excluído. Quando o método "Salvar()" for chamado no repositório, ele comprometerá a exclusão de volta ao banco de dados:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>Integrando a lógica de validação e regra de negócios com classes de modelo

Integrar a lógica de validação e regra de negócios é uma parte fundamental de qualquer aplicativo que trabalhe com dados.

#### <a name="schema-validation"></a>Validação de esquemas

Quando as classes de modelo são definidas usando o designer LINQ para SQL, os tipos de dados das propriedades nas classes de modelo de dados correspondem aos tipos de dados da tabela de banco de dados. Por exemplo: se a coluna "EventDate" na tabela Jantares for uma "hora de data", a classe de modelo de dados criada pela LINQ para sql será do tipo "DateTime" (que é um tipo de dados .NET incorporado). Isso significa que você terá erros de compilação se tentar atribuir um inteiro ou booleano a ele a partir do código, e ele aumentará um erro automaticamente se você tentar converter implicitamente um tipo de string não-válido para ele em tempo de execução.

LINQ para SQL também lidará automaticamente com a fuga de valores SQL para você ao usar strings - o que ajuda a protegê-lo contra ataques de injeção SQL ao usá-lo.

#### <a name="validation-and-business-rule-logic"></a>Lógica de Validação e Regra de Negócios

A validação do esquema é útil como um primeiro passo, mas raramente é suficiente. A maioria dos cenários do mundo real requer a capacidade de especificar uma lógica de validação mais rica que pode abranger várias propriedades, executar códigos e, muitas vezes, ter consciência do estado de um modelo (por exemplo: ele está sendo criado /atualizado/excluído, ou dentro de um estado específico de domínio como "arquivado"). Existem uma variedade de padrões e frameworks diferentes que podem ser usados para definir e aplicar regras de validação para classes de modelo, e existem vários frameworks baseados em .NET lá fora que podem ser usados para ajudar com isso. Você pode usar praticamente qualquer um deles dentro de ASP.NET aplicativos MVC.

Para efeitos do nosso aplicativo NerdDinner, usaremos um padrão relativamente simples e direto onde exporemos uma propriedade IsValid e um método GetRuleViolations() em nosso objeto modelo Dinner. A propriedade IsValid retornará verdadeira ou falsa, dependendo se as regras de validação e de negócios são todas válidas. O método GetRuleViolations() retornará uma lista de quaisquer erros de regra.

Implementaremos IsValid e GetRuleViolations() para o nosso modelo de jantar adicionando uma "classe parcial" ao nosso projeto. As aulas parciais podem ser usadas para adicionar métodos/propriedades/eventos às classes mantidas por um designer VS (como a classe Dinner gerada pelo designer LINQ para SQL) e ajudar a evitar que a ferramenta se meta com nosso código. Podemos adicionar uma nova classe parcial ao nosso projeto clicando com o botão direito do mouse na pasta \Modelos e, em seguida, selecione o comando menu "Adicionar novo item". Em seguida, podemos escolher o modelo "Classe" na caixa de diálogo "Adicionar novo item" e nomeá-lo Dinner.cs.

![](build-a-model-with-business-rule-validations/_static/image11.png)

Clicar no botão "Adicionar" adicionará um arquivo Dinner.cs ao nosso projeto e o abrirá dentro do IDE. Podemos então implementar uma estrutura básica de aplicação de regras/validação usando o código abaixo:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

Algumas notas sobre o código acima:

- A classe Dinner é pré-confrontada com uma palavra-chave "parcial" – o que significa que o código contido nela será combinado com a classe gerada/mantida pelo designer LINQ para SQL e compilada em uma única classe.
- A classe RuleViolation é uma classe auxiliar que adicionaremos ao projeto que nos permite fornecer mais detalhes sobre uma violação de regras.
- O método Dinner.GetRuleViolations() faz com que nossas regras de validação e de negócios sejam avaliadas (vamos implementá-las em breve). Em seguida, ele retorna uma seqüência de objetos RuleViolation que fornecem mais detalhes sobre quaisquer erros de regra.
- A propriedade Dinner.IsValid fornece uma propriedade de ajuda conveniente que indica se o objeto Dinner tem alguma violação de regras ativa. Ele pode ser verificado proativamente por um desenvolvedor usando o objeto Dinner a qualquer momento (e não levanta uma exceção).
- O método parcial Dinner.OnValidate() é um gancho que linq para SQL fornece que nos permite ser notificados sempre que o objeto Dinner está prestes a ser persistido dentro do banco de dados. Nossa implementação onValidate() acima garante que o Jantar não tenha violações de regras antes de ser salvo. Se estiver em um estado inválido, ele levanta uma exceção, o que fará com que linq para SQL aborte a transação.

Essa abordagem fornece uma estrutura simples em que podemos integrar regras de validação e negócios. Por enquanto, vamos adicionar as regras abaixo ao nosso método GetRuleViolations(:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

Estamos usando o recurso "yield return" do C# para retornar uma seqüência de quaisquer Violações de Regras. As primeiras seis verificações de regras acima simplesmente impõem que as propriedades das cordas em nosso Jantar não podem ser nulas ou vazias. A última regra é um pouco mais interessante, e chama um método auxiliar PhoneValidator.IsValidNumber() que podemos adicionar ao nosso projeto para verificar se o formato do número do ContactPhone corresponde ao país do Jantar.

Podemos usar. O suporte de expressão regular da NET para implementar este suporte de validação de telefone. Abaixo está uma implementação simples do PhoneValidator que podemos adicionar ao nosso projeto que nos permite adicionar verificações de padrão Regex específicas do país:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>Manipulação de validação e violações lógicas de negócios

Agora que adicionamos o código de validação e regra de negócios acima, sempre que tentarmos criar ou atualizar um Jantar, nossas regras lógicas de validação serão avaliadas e aplicadas.

Os desenvolvedores podem escrever código satisfaz abaixo para determinar proativamente se um objeto Dinner é válido e recuperar uma lista de todas as violações nele sem levantar nenhuma exceção:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

Se tentarmos salvar um jantar em um estado inválido, uma exceção será levantada quando chamarmos o método Save() no DinnerRepository. Isso ocorre porque linq para SQL chama automaticamente o nosso método parcial Dinner.OnValidate() antes de salvar as alterações do Jantar, e adicionamos código ao Dinner.OnValidate() para abrir uma exceção se houver alguma violação de regra no Jantar. Podemos pegar essa exceção e recuperar reativamente uma lista das violações para corrigir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

Como nossas regras de validação e negócios são implementadas dentro da nossa camada de modelo, e não dentro da camada de Interface do Usuário, elas serão aplicadas e usadas em todos os cenários dentro do nosso aplicativo. Mais tarde, podemos mudar ou adicionar regras de negócios e ter todos os códigos que funcionam com nossos objetos de jantar honrá-los.

Ter a flexibilidade de mudar as regras de negócios em um só lugar, sem ter essas mudanças em toda a lógica de aplicação e interface do usuário, é um sinal de uma aplicação bem escrita, e um benefício que uma estrutura de MVC ajuda a incentivar.

### <a name="next-step"></a>Próxima etapa

Agora temos um modelo que podemos usar para consultar e atualizar nosso banco de dados.

Vamos agora adicionar alguns controladores e visualizações ao projeto que podemos usar para construir uma experiência de IU HTML em torno dele.

> [!div class="step-by-step"]
> [Próximo](create-a-database.md)
> [anterior](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
