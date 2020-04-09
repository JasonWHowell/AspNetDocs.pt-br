---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: Introdução ASP.NET Páginas da Web - Noções Básicas de Formulário HTML | Microsoft Docs
author: Rick-Anderson
description: Este tutorial mostra o básico de como criar um formulário de entrada e como lidar com a entrada do usuário quando você usa ASP.NET Páginas da Web (Razor). E agora que você...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676324"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>Introdução de páginas da Web ASP.NET - Noções básicas do formulário HTML

 por [Tom FitzMacken](https://github.com/tfitzmac)

> Este tutorial mostra o básico de como criar um formulário de entrada e como lidar com a entrada do usuário quando você usa ASP.NET Páginas da Web (Razor). E agora que você tem um banco de dados, você usará suas habilidades de formulário para permitir que os usuários encontrem filmes específicos no banco de dados. Ele assume que você completou a série através da [introdução à exibição de dados usando ASP.NET páginas da Web](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).
> 
> O que você aprenderá:
> 
> - Como criar um formulário usando elementos HTML padrão.
> - Como ler a entrada do usuário em um formulário.
> - Como criar uma consulta SQL que obtém dados seletivamente usando um termo de pesquisa que o usuário fornece.
> - Como ter campos na página "lembrar" o que o usuário inseriu.
>   
> 
> Características/tecnologias discutidas:
> 
> - O objeto `Request`.
> - A cláusula `Where` SQL.

## <a name="what-youll-build"></a>O que você vai construir

No tutorial anterior, você criou um banco de dados, `WebGrid` adicionou dados a ele e, em seguida, usou o ajudante para exibir os dados. Neste tutorial, você adicionará uma caixa de pesquisa que permite encontrar filmes de um gênero específico ou cujo título contém qualquer palavra que você digite. (Por exemplo, você poderá encontrar todos os filmes cujo gênero seja "Ação" ou cujo título contenha "Harry" ou "Adventure").

Quando você terminar este tutorial, você terá uma página como esta:

![Página de filmes com pesquisa de Gênero e Título](form-basics/_static/image1.png)

A parte de listagem da página é &mdash; a mesma do último tutorial de uma grade. A diferença será que a grade mostrará apenas os filmes que você procurou.

## <a name="about-html-forms"></a>Sobre formulários HTML

(Se você tem experiência com a criação de `GET` `POST`formulários HTML e com a diferença entre e , você pode pular esta seção.)

Um formulário tem &mdash; caixas de texto de elementos de entrada do usuário, botões, botões de rádio, caixas de seleção, listas de paradas e assim por diante. Os usuários preenchem esses controles ou fazem seleções e, em seguida, enviam o formulário clicando em um botão.

A sintaxe HTML básica de um formulário é ilustrada por este exemplo:

[!code-html[Main](form-basics/samples/sample1.html)]

Quando esta marcação é executada em uma página, ela cria um formulário simples que se parece com esta ilustração:

![Forma HTML básica como renderizado no navegador](form-basics/_static/image2.png)

O `<form>` elemento inclui elementos HTML a serem submetidos. (Um erro fácil de cometer é adicionar elementos à página, mas depois esquecer de colocá-los dentro de um `<form>` elemento. Nesse caso, nada é apresentado.) O `method` atributo informa ao navegador como enviar a entrada do usuário. Você define `post` isso para se você estiver executando uma `get` atualização no servidor ou se você está apenas buscando dados do servidor.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET, POST e HTTP Verb Safety**
> 
> HTTP, o protocolo que navegadores e servidores usam para trocar informações, é notavelmente simples em suas operações básicas. Os navegadores usam apenas alguns verbos para fazer solicitações aos servidores. Quando você escreve código para a web, é útil entender esses verbos e como o navegador e o servidor os usam. De longe, os verbos mais usados são:
> 
> - `GET`. O navegador usa este verbo para buscar algo do servidor. Por exemplo, quando você digita uma URL `GET` no seu navegador, o navegador executa uma operação para solicitar a página desejada. Se a página incluir gráficos, `GET` o navegador realizará operações adicionais para obter as imagens. Se `GET` a operação tiver que passar informações para o servidor, as informações são passadas como parte da URL na seqüência de consultas.
> - `POST`. O navegador `POST` envia uma solicitação para enviar dados a serem adicionados ou alterados no servidor. Por exemplo, `POST` o verbo é usado para criar registros em um banco de dados ou alterar os existentes. Na maioria das vezes, quando você preenche um formulário e `POST` clica no botão enviar, o navegador realiza uma operação. Em `POST` uma operação, os dados que estão sendo passados para o servidor estão no corpo da página.
> 
> Uma distinção importante entre esses `GET` verbos é que uma operação não deve mudar nada no servidor `GET` — ou colocá-lo de forma um pouco mais abstrata, uma operação não resulta em uma mudança de estado no servidor. Você pode `GET` executar uma operação nos mesmos recursos quantas vezes quiser, e esses recursos não mudam. (Uma `GET` operação é muitas vezes dita como "segura", ou para usar um termo técnico, é *idempotente*.) Em contraste, é `POST` claro, uma solicitação muda algo no servidor cada vez que você executa a operação.
> 
> Dois exemplos ajudarão a ilustrar essa distinção. Quando você realiza uma pesquisa usando um mecanismo como Bing ou Google, você preenche um formulário que consiste em uma caixa de texto e, em seguida, você clica no botão de pesquisa. O navegador `GET` realiza uma operação, com o valor que você inseriu na caixa passada como parte da URL. Usar `GET` uma operação para este tipo de formulário é bom, porque uma operação de pesquisa não altera nenhum recurso no servidor, ele apenas busca informações.
> 
> Agora considere o processo de encomendar algo online. Você preenche os detalhes do pedido e, em seguida, clique no botão enviar. Essa operação será `POST` uma solicitação, pois a operação resultará em alterações no servidor, como um novo registro de pedidos, uma alteração nas informações da sua conta e talvez muitas outras alterações. Ao `GET` contrário da operação, `POST` você não pode repetir sua solicitação — se o fizesse, cada vez que reenviado a solicitação, geraria uma nova ordem no servidor. (Em casos como este, os sites muitas vezes avisarão para não clicar em um botão de envio mais de uma vez, ou desativarão o botão enviar para que você não reenvie o formulário acidentalmente.)
> 
> No decorrer deste tutorial, você usará `GET` uma `POST` operação e uma operação para trabalhar com formulários HTML. Explicaremos em cada caso por que o verbo que você usa é o apropriado.
> 
> (Para saber mais sobre verbos HTTP, consulte o artigo [Definições de Método](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) no site do W3C.)

A maioria dos `<input>` elementos de entrada do usuário são elementos HTML. Eles se `<input type="type" name="name">,` parecem com onde *o tipo* indica o tipo de controle de entrada do usuário que você deseja. Esses elementos são os comuns:

- Caixa de texto:`<input type="text">`
- Caixa de seleção:`<input type="check">`
- Botão de rádio:`<input type="radio">`
- Botão:`<input type="button">`
- Enviar botão:`<input type="submit">`

Você também pode `<textarea>` usar o elemento para criar `<select>` uma caixa de texto multilinha e o elemento para criar uma lista para dada ou rolável. (Para obter mais informações sobre os elementos de formulário HTML, consulte [Formulários html e entrada](http://www.w3schools.com/html/html_forms.asp) no site da W3Schools.)

O `name` atributo é muito importante, porque o nome é como você vai obter o valor do elemento mais tarde, como você verá em breve.

A parte interessante é o que você, o desenvolvedor de páginas, faz com a entrada do usuário. Não há nenhum comportamento embutido associado a esses elementos. Em vez disso, você tem que obter os valores que o usuário inseriu ou selecionou e fazer algo com eles. Isso é o que você vai aprender neste tutorial.

> [!TIP] 
> 
> **Formulários de entrada e HTML5**
> 
> Como você deve saber, o HTML está em transição e a versão mais recente (HTML5) inclui suporte para maneiras mais intuitivas para os usuários inserirem informações. Por exemplo, no HTML5, você (o desenvolvedor da página) pode dizer à página que deseja que o usuário insira uma data. O navegador pode exibir automaticamente um calendário em vez de exigir que o usuário insira uma data manualmente. No entanto, o HTML5 é novo e ainda não é suportado em todos os navegadores.
> 
> ASP.NET Páginas da Web suporta a entrada HTML5 na medida em que o navegador do usuário o faz. Para uma idéia dos novos `<input>` atributos para o elemento em HTML5, consulte [HTML &lt;tipo de&gt; entrada Atributo](http://www.w3schools.com/html/html_form_input_types.asp) no site W3Schools.

## <a name="creating-the-form"></a>Criando o formulário

No WebMatrix, no espaço de trabalho **Arquivos,** abra a página *Movies.cshtml.*

Após a `</h1>` tag de `<div>` fechamento e `grid.GetHtml` antes da tag de abertura da chamada, adicione a seguinte marcação:

[!code-html[Main](form-basics/samples/sample2.html)]

Esta marcação cria um formulário que `searchGenre` tem uma caixa de texto nomeada e um botão de envio. A caixa de texto e o `<form>` botão `method` de envio `get`estão incluídos em um elemento cujo atributo está definido como . (Lembre-se que se você não colocar a `<form>` caixa de texto e enviar o botão dentro de um elemento, nada será enviado quando você clicar no botão.) Você usa `GET` o verbo aqui porque está criando um formulário que não faz nenhuma alteração no servidor — isso apenas resulta em uma pesquisa. (No tutorial anterior, você `post` usou um método, que é como você envia alterações para o servidor. Você verá isso no próximo tutorial novamente.)

Execute a página. Embora você não tenha definido qualquer comportamento para o formulário, você pode ver como ele se parece:

![Página de filmes com caixa de pesquisa para Gênero](form-basics/_static/image3.png)

Digite um valor na caixa de texto, como "Comédia". Em seguida, clique **em 'Gênero de pesquisa ''**

Anote a URL da página. Como você `<form>` define o `method` atributo do elemento para `get`, o valor que você inseriu agora é parte da seqüência de consulta na URL, assim:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>Leitura de valores do formulário

A página já contém algum código que obtém dados do banco de dados e exibe os resultados em uma grade. Agora você tem que adicionar algum código que leia o valor da caixa de texto para que você possa executar uma consulta SQL que inclui o termo de pesquisa.

Como você define o método `get`do formulário para, você pode ler o valor que foi inserido na caixa de texto usando código como o seguinte:

`var searchTerm = Request.QueryString["searchGenre"];`

O `Request.QueryString` objeto `QueryString` (propriedade `Request` do objeto) inclui os valores dos elementos `GET` que foram submetidos como parte da operação. A `Request.QueryString` propriedade contém uma *coleção* (uma lista) dos valores que são submetidos no formulário. Para obter qualquer valor individual, você especifica o nome do elemento que deseja. É por isso que você `name` tem `<input>` que`searchTerm`ter um atributo no elemento ( ) que cria a caixa de texto. (Para saber `Request` mais sobre o objeto, consulte a [barra lateral](#BKMK_TheRequestObject) mais tarde.)

É simples o suficiente para ler o valor da caixa de texto. Mas se o usuário não inseceu nada na caixa de texto, mas clicou em **Pesquisar** de qualquer maneira, você pode ignorar esse clique, já que não há nada para pesquisar.

O código a seguir é um exemplo que mostra como implementar essas condições. (Você não precisa adicionar este código ainda; você vai fazer isso em um momento.)

[!code-csharp[Main](form-basics/samples/sample3.cs)]

O teste se decompõe desta forma:

- Obtenha o `Request.QueryString["searchGenre"]`valor de , ou seja, o valor que foi inserido no `<input>` elemento nomeado `searchGenre`.
- Descubra se está vazio usando `IsEmpty` o método. Este método é a maneira padrão de determinar se algo (por exemplo, um elemento de forma) contém um valor. Mas realmente, você só se importa se *não* estiver vazio, portanto...
- Adicione `!` o operador na `IsEmpty` frente do teste. (O `!` operador significa não lógico).

Em inglês simples, `if` toda a condição se traduz no seguinte: *Se o elemento searchGenre do formulário não estiver vazio, então ...*

Este bloco define o estágio para criar uma consulta que usa o termo de pesquisa. Você fará isso na próxima seção.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **O objeto de solicitação**
> 
> O `Request` objeto contém todas as informações que o navegador envia ao seu aplicativo quando uma página é solicitada ou enviada. Este objeto inclui qualquer informação que o usuário forneça, como valores de caixa de texto ou um arquivo para carregar. Ele também inclui todos os tipos de informações adicionais, como cookies, valores na seqüência de consulta de URL (se houver), o caminho do arquivo da página que está sendo executado, o tipo de navegador que o usuário está usando, a lista de idiomas que estão definidos no navegador e muito mais.
> 
> O `Request` objeto é uma *coleção* (lista) de valores. Você recebe um valor individual fora da coleção especificando seu nome:
> 
> `var someValue = Request["name"];`
> 
> O `Request` objeto realmente expõe vários subconjuntos. Por exemplo:
> 
> - `Request.Form`lhe dá valores de `<form>` elementos dentro do `POST` elemento enviado se a solicitação for uma solicitação.
> - `Request.QueryString`dá-lhe apenas os valores na seqüência de consulta da URL. (Em uma `http://mysite/myapp/page?searchGenre=action&page=2`URL `?searchGenre=action&page=2` como , a seção da URL é a seqüência de consulta.)
> - `Request.Cookies`a coleção dá-lhe acesso aos cookies que o navegador enviou.
> 
> Para obter um valor que você sabe que está `Request["name"]`no formulário enviado, você pode usar . Alternativamente, você pode usar `Request.Form["name"]` as `POST` versões `Request.QueryString["name"]` mais `GET` específicas (para solicitações) ou (para solicitações). Claro, *nome* é o nome do item para obter.
> 
> O nome do item que você quer obter tem que ser único dentro da coleção que você está usando. É por isso `Request` que o objeto `Request.Form` `Request.QueryString`fornece os subconjuntos como e . Suponha que sua página `userName` contenha um `userName`elemento de formulário nomeado e *também* contenha um cookie chamado . Se você `Request["userName"]`conseguir, é ambíguo se você quer o valor do formulário ou o cookie. No entanto, `Request.Form["userName"]` `Request.Cookie["userName"]`se você conseguir ou , você está sendo explícito sobre qual valor obter.
> 
> É uma boa prática ser específico e usar `Request` o subconjunto do `Request.Form` que `Request.QueryString`você está interessado, como ou . Para as páginas simples que você está criando neste tutorial, provavelmente não faz nenhuma diferença. No entanto, à medida que você `Request.Form` `Request.QueryString` cria páginas mais complexas, usando a versão explícita ou pode ajudá-lo a evitar problemas que podem surgir quando a página contém um formulário (ou vários formulários), cookies, valores de seqüência de consultas e assim por diante.

## <a name="creating-a-query-by-using-a-search-term"></a>Criando uma consulta usando um termo de pesquisa

Agora que você sabe como obter o termo de pesquisa que o usuário inseriu, você pode criar uma consulta que o use. Lembre-se que para obter todos os itens do filme fora do banco de dados, você está usando uma consulta SQL que se parece com esta declaração:

`SELECT * FROM Movies`

Para obter apenas certos filmes, você tem que `Where` usar uma consulta que inclui uma cláusula. Esta cláusula permite definir uma condição sobre a qual as linhas são devolvidas pela consulta. Aqui está um exemplo:

`SELECT * FROM Movies WHERE Genre = 'Action'`

O formato `WHERE column = value`básico é . Você pode usar diferentes `=`operadores além de apenas , como `>` (maior do `<` que), (menor que), `<>` (não igual a), `<=` (menor ou igual a), etc., dependendo do que você está procurando.

Caso esteja se perguntando, as declarações &mdash; `SELECT` SQL `Select` não são `select`sensíveis a casos é o mesmo que (ou mesmo ). No entanto, muitas vezes as pessoas capitalizam palavras-chave em uma declaração SQL, como `SELECT` e `WHERE`, para facilitar a leitura.

### <a name="passing-the-search-term-as-a-parameter"></a>Passando o termo de pesquisa como parâmetro

Procurar um gênero específico é`WHERE Genre = 'Action'`bastante fácil ( ), mas você quer ser capaz de procurar por qualquer gênero que o usuário insira. Para fazer isso, você cria como consulta SQL que inclui um espaço reservado para o valor a ser pesquisado. Vai parecer com este comando:

`SELECT * FROM Movies WHERE Genre = @0`

O espaço reservado `@` é o personagem seguido de zero. Como você pode imaginar, uma consulta pode conter vários espaços `@0` `@1`reservados, e eles seriam nomeados, , `@2`etc.

Para configurar a consulta e realmente passar o valor, você usa o código como o seguinte:

[!code-sql[Main](form-basics/samples/sample4.sql)]

Este código é semelhante ao que você já fez para exibir dados na grade. As únicas diferenças são:

- A consulta contém um`WHERE Genre = @0"`espaço reservado ( ).
- A consulta é colocada em`selectCommand`uma variável ( ); antes, você passou a consulta `db.Query` diretamente para o método.
- Quando você `db.Query` chama o método, você passa tanto a consulta quanto o valor a ser usado para o espaço reservado. (Se a consulta tivesse vários espaços reservados, você passaria todos como valores separados para o método.)

Se você juntar todos esses elementos, você terá o seguinte código:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **Importante!** Usar espaços reservados `@0`(como) para passar valores para um comando SQL é *extremamente importante* para a segurança. A maneira como você vê isso aqui, com espaços reservados para dados variáveis, é a única maneira de construir comandos SQL.
> 
> Nunca construa uma declaração SQL juntando (concatenando) texto e valores literais que você recebe do usuário. A concatenação da entrada do usuário em uma declaração SQL abre seu site para um *ataque de injeção SQL* onde um usuário mal-intencionado envia valores para sua página que hackeiam seu banco de dados. (Você pode ler mais no artigo [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) no site do MSDN.)

## <a name="updating-the-movies-page-with-search-code"></a>Atualizando a página de filmes com código de pesquisa

Agora você pode atualizar o código no arquivo *Movies.cshtml.* Para começar, substitua o código no bloco de código na parte superior da página por este código:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

A diferença aqui é que você colocou `selectCommand` a consulta na variável, `db.Query` que você vai passar para mais tarde. Colocar a declaração SQL em uma variável permite alterar a declaração, que é o que você fará para realizar a pesquisa.

Você também removeu essas duas linhas, que você vai colocar de volta mais tarde:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

Você não quer executar a consulta ainda (isto é, chamada) `db.Query`e você `WebGrid` não quer inicializar o ajudante ainda. Você vai fazer essas coisas depois de descobrir qual declaração SQL tem que ser executada.

Após este bloco reescrito, você pode adicionar a nova lógica para lidar com a pesquisa. O código completo será parecido com o seguinte. Atualize o código em sua página para que corresponda a este exemplo:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

A página agora funciona assim. Toda vez que a página é `selectCommand` executada, o código abre o banco de dados `Movies` e a variável é definida como a declaração SQL que obtém todos os registros da tabela. O código também inicializa a `searchTerm` variável.

No entanto, se a solicitação `searchGenre` atual incluir um `selectCommand` valor para o elemento, o código `Where` define para uma consulta diferente — ou seja, para uma que inclui a cláusula de pesquisa de um gênero. Ele também `searchTerm` define para o que foi passado para a caixa de pesquisa (que pode não ser nada).

Independentemente de qual declaração `selectCommand`SQL `db.Query` está, o código então chama `searchTerm`para executar a consulta, passando-a o que estiver dentro . Se não há `searchTerm`nada dentro, não importa, porque nesse caso não há parâmetro `selectCommand` para passar o valor de qualquer maneira.

Finalmente, o código inicializa o `WebGrid` ajudante usando os resultados da consulta, como antes.

Você pode ver que colocando a declaração SQL e o termo de pesquisa em variáveis, você adicionou flexibilidade ao código. Como você verá mais tarde neste tutorial, você pode usar este framework básico e continuar adicionando lógica para diferentes tipos de pesquisas.

## <a name="testing-the-search-by-genre-feature"></a>Testando o recurso Pesquisa por Gênero

No WebMatrix, execute a página *Movies.cshtml.* Você vê a página com a caixa de texto para o gênero.

Digite um gênero que você inseriu para um de seus registros de teste e clique **em Pesquisar**. Desta vez, você vê uma lista de apenas os filmes que correspondem a esse gênero:

![Lista de páginas de filmes após procurar o gênero 'Comédias'](form-basics/_static/image4.png)

Digite um gênero diferente e pesquise novamente. Tente entrar no gênero usando todas as letras minúsculas ou todas as letras maiúsculas para que você possa ver que a pesquisa não é sensível ao caso.

## <a name="remembering-what-the-user-entered"></a>"Lembrando" o que o Usuário inseriu

Você deve ter notado que depois que entrou em um gênero e clicou **em Search Genre,** você viu uma listagem para esse gênero. No entanto, a &mdash; caixa de texto de pesquisa estava vazia em outras palavras, não se lembrava o que você tinha entrado.

É importante entender por que esse comportamento ocorre. Quando você envia uma página, o navegador envia uma solicitação para o servidor web. Quando ASP.NET recebe a solicitação, ela cria uma nova instância da página, executa o código nela e, em seguida, renderiza a página para o navegador novamente. Na verdade, porém, a página não sabe que você estava apenas trabalhando com uma versão anterior de si mesmo. Tudo o que ele sabe é que ele recebeu um pedido que tinha alguns dados de formulário nele.

Toda vez que &mdash; você solicita uma página, &mdash; seja pela primeira vez ou enviando-a, você está recebendo uma nova página. O servidor web não tem memória de sua última solicitação. Nem ASP.NET, nem o navegador. A única conexão entre essas instâncias separadas da página são os dados que você transmite entre eles. Se você enviar uma página, por exemplo, a nova instância da página poderá obter os dados do formulário enviados pela instância anterior. (Outra maneira de passar dados entre páginas é usar cookies.)

Uma maneira formal de descrever essa situação é dizer que as páginas da web são *apátridas.* Os servidores da Web e as próprias páginas e os elementos da página não mantêm nenhuma informação sobre o estado anterior de uma página. A web foi projetada dessa forma porque manter o estado para solicitações individuais esgotaria rapidamente os recursos dos servidores web, que muitas vezes lidam com milhares, talvez até centenas de milhares, de solicitações por segundo.

Então é por isso que a caixa de texto estava vazia. Depois que você enviou a página, ASP.NET criou uma nova instância da página e correu através do código e marcação. Não havia nada nesse código que ASP.NET dissesse para colocar um valor na caixa de texto. Então ASP.NET não fez nada, e a caixa de texto foi renderizada sem um valor nela.

Na verdade, há uma maneira fácil de contornar este problema. O gênero que você inseriu na caixa &mdash; de texto `Request.QueryString["searchGenre"]` *está* disponível para você no código em que está .

Atualize a marcação da caixa `value` de texto para `searchTerm`que o atributo obtenha seu valor, como este exemplo:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

Nesta página, você também poderia `value` ter `searchTerm` definido o atributo para a variável, já que essa variável também contém o gênero que você inseriu. Mas usar `Request` o objeto `value` para definir o atributo como mostrado aqui é a maneira padrão de realizar essa tarefa. (Supondo que você &mdash; queira fazer isso em algumas situações, você pode querer renderizar a página *sem* valores nos campos. Tudo depende do que está acontecendo com seu aplicativo.)

> [!NOTE]
> Você não pode "lembrar" o valor de uma caixa de texto que é usada para senhas. Seria uma brecha de segurança para permitir que as pessoas preencham um campo de senha usando código.

Execute a página novamente, insira um gênero e clique **em 'Gênero de pesquisa ''** Desta vez, você não só vê os resultados da pesquisa, mas a caixa de texto lembra o que você inseriu da última vez:

![Página mostrando que a caixa de texto 'lembrou' a entrada anterior](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>Procurando qualquer palavra no título

Agora você pode procurar por qualquer gênero, mas também pode querer procurar um título. É difícil obter um título exatamente certo quando você pesquisa, então, em vez disso, você pode procurar por uma palavra que aparece em qualquer lugar dentro de um título. Para fazer isso no SQL, você usa o operador e a `LIKE` sintaxe como o seguinte:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

Este comando recebe todos os filmes cujos títulos contêm "aventura". Quando você `LIKE` usa o operador, você `%` inclui o caractere curinga como parte do termo de pesquisa. A `LIKE 'adventure%'` busca significa "começar com 'aventura'". (Tecnicamente, significa "A corda 'aventura' seguida de qualquer coisa.") Da mesma forma, `LIKE '%adventure'` o termo de busca significa "qualquer coisa seguida pela corda 'aventura'", que é outra maneira de dizer "terminar com 'aventura'".

O termo `LIKE '%adventure%'` de busca, portanto, significa "com 'aventura' em qualquer lugar do título". (Tecnicamente, "qualquer coisa no título, seguida de 'aventura', seguida de qualquer coisa.")

Dentro `<form>` do elemento, adicione a seguinte `</div>` marcação bem abaixo da tag `</form>` de fechamento para a pesquisa de gênero (pouco antes do elemento de fechamento):

[!code-html[Main](form-basics/samples/sample10.html)]

O código para lidar com essa pesquisa é semelhante ao código para `LIKE` a pesquisa de gênero, exceto que você tem que montar a pesquisa. Dentro do bloco de código na parte `if` superior da `if` página, adicione este bloco logo após o bloco para a pesquisa de gênero:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

Este código usa a mesma lógica que você `LIKE` viu anteriormente,`%`exceto que a pesquisa usa um operador e o código coloca " " antes e depois do termo de pesquisa.

Observe como foi fácil adicionar outra pesquisa à página. Tudo o que você tinha que fazer era:

- Crie `if` um bloco testado para ver se a caixa de pesquisa relevante tinha um valor.
- Defina `selectCommand` a variável como uma nova declaração SQL.
- Defina `searchTerm` a variável para o valor a ser aprovado para a consulta.

Aqui está o bloco de código completo, que contém a nova lógica para uma pesquisa de títulos:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

Veja a seguir um resumo do que esse código faz:

- As variáveis `searchTerm` `selectCommand` e são inicializadas no topo. Você vai definir essas variáveis para o termo de pesquisa apropriado (se houver) e o comando SQL apropriado com base no que o usuário faz na página. A pesquisa padrão é o caso simples de obter todos os filmes do banco de dados.
- Nos testes `searchGenre` para `searchTitle`e , `searchTerm` o código define para o valor que você deseja pesquisar. Esses blocos `selectCommand` de código também são definidos como um comando SQL apropriado para essa pesquisa.
- O `db.Query` método é invocado apenas uma vez, `selectedCommand` usando qualquer comando `searchTerm`SQL e qualquer valor em . Se não houver um termo de pesquisa (sem `searchTerm` gênero e sem palavra de título), o valor de é uma seqüência vazia. No entanto, isso não importa, porque nesse caso a consulta não requer um parâmetro.

## <a name="testing-the-title-search-feature"></a>Testando o recurso de pesquisa de títulos

Agora você pode testar sua página de pesquisa concluída. Executar *Movies.cshtml*.

Digite um gênero e clique **em Pesquisar gênero**. A grade exibe filmes desse gênero, como antes.

Digite uma palavra de título e clique **em Título de pesquisa**. A grade exibe filmes que têm essa palavra no título.

![Lista de páginas de filmes após procurar por 'The' no título](form-basics/_static/image6.png)

Deixe as duas caixas de texto em branco e clique em ambos os botões. A grade exibe todos os filmes.

## <a name="combining-the-queries"></a>Combinando as consultas

Você pode notar que as pesquisas que você pode realizar são exclusivas. Você não pode pesquisar o título e o gênero ao mesmo tempo, mesmo que ambas as caixas de pesquisa tenham valores neles. Por exemplo, você não pode procurar por todos os filmes de ação cujo título contém "Aventura". (Como a página está codificada agora, se você inserir valores para o gênero e o título, a pesquisa de título susceptência.) Para criar uma pesquisa que combine as condições, você teria que criar uma consulta SQL que tenha sintaxe como a seguinte:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

E você teria que executar a consulta usando uma declaração como a seguinte (aproximadamente falando):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

Criar lógica para permitir muitas permutações de critérios de pesquisa pode se envolver um pouco, como você pode ver. Por isso, vamos parar aqui.

## <a name="coming-up-next"></a>Coming Up Next

No próximo tutorial, você criará uma página que usa um formulário para permitir que os usuários adicionem filmes ao banco de dados.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>Lista completa para página de filme (atualizada com pesquisa)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>Recursos adicionais

- [Introdução a O ASP.NET que programa usando a sintaxe razor](https://go.microsoft.com/fwlink/?LinkID=202890)
- [SQL WHERE Clause](http://www.w3schools.com/sql/sql_where.asp) no site da W3Schools
- [Definições de método](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) artigo no site W3C

> [!div class="step-by-step"]
> [Próximo](displaying-data.md)
> [anterior](entering-data.md)
