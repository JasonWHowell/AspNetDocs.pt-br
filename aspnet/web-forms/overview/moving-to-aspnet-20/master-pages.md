---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: Páginas-Mestre | Microsoft Docs
author: rick-anderson
description: Um dos componentes-chave de um site bem-sucedido é uma aparência consistente. Em ASP.NET 1.x, os desenvolvedores usaram controles de usuário para replicar a página comum...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b493feb21d2e3d6429f0a23df5aab66e0c4c5b07
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543178"
---
# <a name="master-pages"></a>Páginas mestras

pela [Microsoft](https://github.com/microsoft)

> Um dos componentes-chave de um site bem-sucedido é uma aparência consistente. Em ASP.NET 1.x, os desenvolvedores usaram controles de usuário para replicar elementos comuns da página em um aplicativo da Web. Embora essa seja certamente uma solução viável, usar controles de usuário tem algumas desvantagens. Por exemplo, uma alteração na posição de um controle de usuário requer uma alteração em várias páginas em um site. Os controles do usuário também não são renderizados na exibição Design depois de inseridos em uma página.

Um dos componentes-chave de um site bem-sucedido é uma aparência consistente. Em ASP.NET 1.x, os desenvolvedores usaram controles de usuário para replicar elementos comuns da página em um aplicativo da Web. Embora essa seja certamente uma solução viável, usar controles de usuário tem algumas desvantagens. Por exemplo, uma alteração na posição de um controle de usuário requer uma alteração em várias páginas em um site. Os controles do usuário também não são renderizados na exibição Design depois de inseridos em uma página.

ASP.NET 2.0 introduz páginas-mestre como uma maneira de manter uma aparência consistente e, como você verá em breve, as páginas-mestre representam uma melhoria significativa sobre o método de controle do usuário.

## <a name="why-master-pages"></a>Por que páginas-mestre?

Você deve estar se perguntando por que páginas-mestre eram necessárias em ASP.NET 2.0. Afinal, os desenvolvedores de sites da Web já estão usando controles de usuário em ASP.NET 1.x para compartilhar áreas de conteúdo entre páginas. Na verdade, existem várias razões pelas quais os controles de usuário são uma solução menos que ideal para criar um layout comum.

Os controles do usuário não definem o layout da página. Em vez disso, eles definem o layout e a funcionalidade para uma parte de uma página. A distinção entre esses dois é importante porque torna a gestão de uma solução de controle de usuário muito mais difícil. Por exemplo, quando você deseja alterar a posição de um controle de usuário em sua página, você deve editar a página real na qual o controle do usuário é exibido. Isso é bom se você tem apenas algumas páginas, mas em sites grandes, rapidamente se torna um pesadelo de gerenciamento de sites!

Outra desvantagem de usar controles de usuário para definir um layout comum está enraizada na arquitetura do próprio ASP.NET. Se algum membro público de um controle de usuário for alterado, ele exige que você recompile todas as páginas que usam o controle do usuário. Por sua vez, ASP.NET re-JIT suas páginas quando forem acessadas pela primeira vez. Isso, mais uma vez, produz uma arquitetura não escalável e um problema de gerenciamento de sites para sites maiores.

Ambos os problemas (e muitos mais) são bem abordados por páginas-mestre em ASP.NET 2.0.

## <a name="how-master-pages-work"></a>Como funcionam as páginas-mestre

Uma página-mestre é análoga a um modelo para outras páginas. Elementos de página que devem ser compartilhados entre outras páginas (menus, bordas, etc.) são adicionados à página-mestre. Quando novas páginas são adicionadas ao site, você pode associá-las a uma página-mestre. Uma página associada a uma página-mestre é chamada de **página de conteúdo**. Por padrão, uma página de conteúdo assume a aparência da página-mestre. No entanto, ao criar uma página-mestre, você pode definir partes da página que a página de conteúdo pode substituir com seu próprio conteúdo. Essas porções são definidas por meio de um novo controle introduzido em ASP.NET 2.0; o **controle ContentPlaceHolder.**

Uma página-mestre pode conter qualquer número de controles ContentPlaceHolder (ou nenhum.) Na página de conteúdo, o conteúdo dos controles ContentPlaceHolder aparece dentro dos controles de **conteúdo,** outro novo controle em ASP.NET 2.0. Por padrão, as páginas de conteúdo Os controles de conteúdo estão vazios para que você possa fornecer seu próprio conteúdo. Se você quiser usar o conteúdo da página-mestre dentro dos controles de conteúdo, você pode fazê-lo como você verá mais tarde neste módulo. O controle de conteúdo é mapeado para o controle ContentPlaceHolder através do atributo ContentPlaceHolderID do controle de conteúdo. O código abaixo mapeia um controle de conteúdo para um controle ContentPlaceHolder chamado mainBody em uma página-mestre.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> Muitas vezes você ouvirá as pessoas descreverem páginas-mestre como sendo uma classe base para outras páginas. Isso não é verdade. A relação entre páginas-mestre e páginas de conteúdo não é de herança.

**A Figura 1** mostra uma página-mestre e uma página de conteúdo associada como eles aparecem no Visual Studio 2005. Você pode ver o controle ContentPlaceHolder na página-mestre e o controle de conteúdo correspondente na página de conteúdo. Observe que o conteúdo das páginas-mestre que está fora do ContentPlaceHolder é visível, mas acinzentado na página de conteúdo. Somente o conteúdo dentro do ContentPlaceHolder pode ser suplantado pela página de conteúdo. Todos os outros conteúdos que vêm da página-mestre são imutáveis.

![Uma página-mestre e sua página de conteúdo associada](master-pages/_static/image1.jpg)

**Figura 1**: Uma página-mestre e sua página de conteúdo associada

## <a name="creating-a-master-page"></a>Criando uma página-mestre

Para criar uma nova página-mestre:

1. Abra o Visual Studio 2005 e crie um novo site.
2. Clique em Arquivo, Novo, Arquivo.
3. Escolha Arquivo mestre na caixa de diálogo Adicionar novo item, conforme mostrado na **figura 2**.
4. Clique em Adicionar.

![Criando uma nova página-mestre](master-pages/_static/image2.jpg)

**Figura 2**: Criando uma nova página-mestre

Observe que a extensão de arquivo para uma página-mestre é *.master*. Esta é uma das maneiras que uma página-mestre difere de uma página comum. A outra diferença primária é que, em vez de uma @Page diretiva, a página principal contém uma @Master diretiva. Mude para Source View para a página-mestre que você acabou de criar e revise o código.

Uma nova página-mestre terá um controle ContentPlaceHolder por padrão. Na maioria dos casos, faz mais sentido criar os elementos de página comuns primeiro e, em seguida, inserir controles ContentPlaceHolder onde o conteúdo personalizado é desejado. Nesses casos, os desenvolvedores desejam excluir o controle padrão do ContentPlaceHolder e inserir novos à medida que a página for desenvolvida. Os controles contentPlaceHolder não são redimensionáveis, apesar do fato de que eles exibem alças de dimensionamento. O controle ContentPlaceHolder dimensiona automaticamente com base no conteúdo que ele contém com uma exceção; se você colocar um controle ContentPlaceHolder dentro de um elemento de bloco, como uma célula de tabela, ele irá dimensionar de acordo com o tamanho do elemento.

## <a name="lab-1-working-with-master-pages"></a>Laboratório 1 Trabalhando com Páginas-Mestre

Neste laboratório, você criará uma nova página-mestre e definirá três controles ContentPlaceHolder. Em seguida, você criará uma nova página de conteúdo e substituirá o conteúdo de pelo menos um dos controles ContentPlaceHolder.

1. Crie uma página-mestre e insira controles ContentPlaceHolder. 

    1. Crie uma nova página-mestre como descrito acima.
    2. Exclua o controle Padrão ContentPlaceHolder.
    3. Selecione o controle ContentPlaceHolder clicando na borda superior sombreada do controle e, em seguida, exclua-o apertando a tecla DEL no teclado.
    4. Insira uma nova tabela usando o *cabeçalho e* o modelo lateral, conforme mostrado na figura 3. Mude a largura e a altura para 90% cada uma para que toda a tabela seja visível no designer.

![](master-pages/_static/image3.jpg)

**Figura 3**

1. Coloque o cursor em cada célula da tabela e coloque a propriedade *valign* para *cima*.
2. Na caixa de ferramentas, insira um controle ContentPlaceHolder na célula superior da tabela (a célula de cabeçalho.)
3. Ao inserir este controle ContentPlaceHolder, você notará que a altura da linha vai subir quase toda a página, conforme mostrado na figura 4. Não se preocupe com isso neste momento.

![O espaço vazio está na mesma célula que o ContentPlaceHolder](master-pages/_static/image1.gif)

**Figura 4**: O espaço vazio está na mesma célula que o ContentPlaceHolder

1. Coloque um controle ContentPlaceHolder nas outras duas células. Uma vez que os outros controles ContentPlaceHolder tenham sido inseridos, o tamanho das células de tabela deve ser como você esperaria. A página deve agora se parecer com a página mostrada na **figura 5**.

![O Mestre com todos os controles ContentPlaceHolder. Observe que a altura da célula para a célula de cabeçalho é agora o que deveria ser](master-pages/_static/image2.gif)

**Figura 5**: O Mestre com todos os controles ContentPlaceHolder. Observe que a altura da célula para a célula de cabeçalho é agora o que deveria ser

1. Digite algum texto de sua escolha em cada um dos três controles ContentPlaceHolder.
2. Salve a página-mestre como exercise1.master.
3. Crie um novo Formulário web e associe-o à página exercise1.master.
4. Selecione Arquivo, Novo, Arquivo no Visual Studio 2005.
5. Selecione **Formulário da Web** na caixa de diálogo Adicionar novo item.
6. Certifique-se de que a caixa de seleção da página mestre Select está verificada conforme mostrado na figura 6.

![Adicionando uma nova página de conteúdo](master-pages/_static/image3.gif)

**Figura 6:** Adicionando uma nova página de conteúdo

1. Clique em Adicionar.
2. Selecione exercise1.master na Caixa Selecionar uma caixa de diálogo de página-mestre, conforme mostrado na figura 7.
3. Clique em OK para adicionar a nova página de conteúdo.

A nova página de conteúdo aparece no Visual Studio com um controle de conteúdo para cada controle ContentPlaceHolder na página-mestre. Por padrão, os controles de conteúdo estão vazios para que você possa adicionar seu próprio conteúdo. Se você quiser que eles usem o conteúdo do controle ContentPlaceHolder na página-mestre, basta clicar no símbolo de tag inteligente (a pequena seta preta no canto superior direito do controle) e escolher *Padrão para Masters Conteúdo* da tag inteligente como mostrado na figura **8**. Quando você faz isso, o item do menu muda para *Criar conteúdo personalizado*. Clicar nele nesse ponto remove o conteúdo da página-mestre, permitindo que você defina conteúdo personalizado para esse controle de conteúdo em particular.

![Definindo um controle de conteúdo como padrão para o conteúdo das páginas-mestre](master-pages/_static/image4.gif)

**Figura 7**: Definir um controle de conteúdo como padrão para o conteúdo das páginas-mestre

## <a name="connecting-master-page-and-content-pages"></a>Conectando páginas de página-mestre e conteúdo

A associação entre uma página-mestre e uma página de conteúdo pode ser configurada de uma das quatro maneiras diferentes:

- O atributo <strong>MasterPageFile</strong> da @Page diretiva
- Definindo a propriedade **Page.MasterPageFile** em código.
- O elemento ** &lt;páginas&gt; ** no arquivo de configuração de aplicativos (web.config na pasta raiz do aplicativo)
- O elemento ** &lt;páginas&gt; ** em um arquivo de configuração de subpastas (web.config em uma subpasta)

## <a name="masterpagefile-attribute"></a>Atributo MasterPageFile

O atributo MasterPageFile facilita a aplicação de uma página-mestre a uma determinada página ASP.NET. É também o método usado para aplicar a página-mestre quando você verifica a caixa de seleção **Selecionar página mestre** como você fez no Exercício 1.

## <a name="setting-pagemasterpagefile-in-code"></a>Definindo Page.MasterPageFile em Código

Ao definir a propriedade MasterPageFile em código, você pode aplicar uma página-mestre específica ao seu conteúdo em tempo de execução. Isso é útil nos casos em que você pode precisar aplicar uma página-mestre específica com base em uma função de usuário ou em alguns outros critérios. A propriedade MasterPageFile deve ser definida no método PreInit. Se for definido após o método PreInit, uma InvalidOperationException será lançada. A página na qual esta propriedade está sendo definida também deve ter um controle de conteúdo como controle de nível superior para a página. Caso contrário, uma httpexception será lançada quando a propriedade MasterPageFile estiver definida.

## <a name="using-the-ltpagesgt-element"></a>Usando &lt;o&gt; elemento páginas

Você pode configurar uma página-mestre para suas páginas definindo o atributo masterPageFile no elemento &lt;páginas&gt; do arquivo Web.config. Ao usar este método, tenha em mente que arquivos web.config mais baixos na estrutura do aplicativo podem substituir essa configuração. Qualquer atributo MasterPageFile @Page definido em uma diretiva também substituirá essa configuração. O &lt;uso&gt; do elemento páginas torna mais simples criar *uma* página mestre que pode ser substituída se necessário em determinadas pastas ou arquivos.

## <a name="properties-in-master-pages"></a>Propriedades em páginas-mestre

Uma página-mestre pode expor propriedades simplesmente tornando essas propriedades públicas dentro da página-mestre. Por exemplo, o código a seguir define uma propriedade chamada SomeProperty:

[!code-csharp[Main](master-pages/samples/sample2.cs)]

Para acessar a propriedade SomeProperty da página Conteúdo, você precisará usar a propriedade Master assim:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>Páginas-mestre de aninhamento

As páginas-mestre são a solução perfeita para garantir uma aparência comum em um grande aplicativo da Web. No entanto, não é incomum ter certas partes de um grande site compartilhando uma interface comum, enquanto outras partes compartilham uma interface diferente. Para atender a essa necessidade, várias páginas-mestre são a solução perfeita. No entanto, isso ainda não aborda o fato de que um grande aplicativo pode ter certos componentes (como um menu, por exemplo) que são compartilhados entre todas as páginas e outros componentes que são compartilhados apenas entre certas seções do site. Para esse tipo de situação, páginas-mestre aninhadas preenchem bem a necessidade. Como você viu, uma página-mestre normal consiste em uma página-mestre e uma página de conteúdo. Em uma situação de página-mestre aninhada, há duas páginas-mestre; um mestre dos pais e um mestre infantil. A página-mestre da criança também é uma página de conteúdo e seu mestre é a página-mestre dos pais.

Aqui está o código para uma página-mestre típica:

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

Em um cenário mestre aninhado, este seria o mestre dos pais. Outra página-mestre usaria esta página como sua página-mestre, e esse código seria assim:

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

Observe que, neste cenário, o mestre da criança também é uma página de conteúdo para o pai mestre. Todo o conteúdo do mestre da criança é exibido dentro de um controle de conteúdo que obtém seu conteúdo a partir do controle ContentPlaceHolder do pai.

> [!NOTE]
> O suporte ao designer não está disponível para páginas-mestre aninhadas. Quando você está desenvolvendo usando mestres aninhados, você precisará usar a visualização de origem.

Este vídeo mostra um passo a passo do uso de páginas-mestre aninhadas.

![](master-pages/_static/image1.png)

[Abra o vídeo em tela cheia](master-pages/_static/nested1.wmv)

![Selecionando uma página-mestre](master-pages/_static/image4.jpg)

**Figura 8**: Selecionando uma página-mestre
