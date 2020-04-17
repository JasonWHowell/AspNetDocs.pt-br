---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: Exibindo dados em um gráfico com páginas da Web ASP.NET (Razor) | Microsoft Docs
author: rick-anderson
description: Este capítulo explica como exibir dados em um gráfico. Nos capítulos anteriores, você aprendeu a exibir dados manualmente e em uma grade. Este capítulo explica...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: ad55d4898ee39e0239ef8b0bd5eea6387af3c816
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542879"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>Exibindo dados em um gráfico com páginas da Web ASP.NET (Razor)

pela [Microsoft](https://github.com/microsoft)

> Este artigo explica como usar um gráfico para exibir dados em um `Chart` site ASP.NET Web Pages (Razor) usando o helper.
> 
> **O que você vai aprender:**
> 
> - Como exibir dados em um gráfico.
> - Como estilizar gráficos usando temas incorporados.
> - Como salvar gráficos e como cachê-los para um melhor desempenho.
> 
> Estas são as ASP.NET características de programação introduzidas no artigo:
> 
> - O `Chart` ajudante.
> 
> > [!NOTE]
> > As informações deste artigo se aplicam a ASP.NET Páginas da Web 1.0 e páginas da Web 2.

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>O Ajudante de Gráficos

Quando você quiser exibir seus dados em forma `Chart` gráfica, você pode usar o helper. O `Chart` ajudante pode renderizar uma imagem que exibe dados em uma variedade de tipos de gráficos. Suporta muitas opções de formatação e rotulagem. O `Chart` ajudante pode renderizar mais de 30 tipos de gráficos, incluindo todos os tipos de gráficos com os que você pode estar familiarizado com o Microsoft Excel ou outras ferramentas &#8212; gráficos de área, gráficos de barras, gráficos de colunas, gráficos de linha e gráficos de tortas, juntamente com gráficos mais especializados, como gráficos de ações.

| **Descrição do gráfico** ![de área: Imagem do tipo gráfico de área](7-displaying-data-in-a-chart/_static/image1.jpg) | **Descrição do gráfico** ![de barras: Imagem do tipo gráfico de barras](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **Descrição do gráfico** ![da coluna: Imagem do tipo gráfico da coluna](7-displaying-data-in-a-chart/_static/image3.jpg) | **Descrição do gráfico** ![de linha: Imagem do tipo gráfico de linha](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **Descrição do gráfico** ![de tortas: Imagem do tipo gráfico de Pie](7-displaying-data-in-a-chart/_static/image5.jpg) | **Descrição do gráfico** ![de ações: Imagem do tipo gráfico de ações](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>Elementos do gráfico

Gráficos mostram dados e elementos adicionais como lendas, eixos, séries e assim por diante. A imagem a seguir mostra muitos dos elementos `Chart` do gráfico que você pode personalizar quando você usa o ajudante. Este artigo mostra como definir alguns (não todos) desses elementos.

![Descrição: Imagem mostrando os elementos do gráfico](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>Criando um gráfico a partir de dados

Os dados que você exibe em um gráfico podem ser de uma matriz, dos resultados retornados de um banco de dados ou de dados que estão em um arquivo XML.

### <a name="using-an-array"></a>Usando uma matriz

Como explicado em [Introdução à programação ASP.NET de páginas da Web usando a sintaxe de navalha,](https://go.microsoft.com/fwlink/?LinkId=202890)uma matriz permite que você armazene uma coleção de itens semelhantes em uma única variável. Você pode usar matrizes para conter os dados que deseja incluir em seu gráfico.

Este procedimento mostra como você pode criar um gráfico a partir de dados em arrays, usando o tipo de gráfico padrão. Ele também mostra como exibir o gráfico dentro da página.

1. Crie um novo arquivo chamado *ChartArrayBasic.cshtml*.
2. Substitua o conteúdo existente pelo seguinte: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    O código primeiro cria um novo gráfico e define sua largura e altura. Você especifica o título `AddTitle` do gráfico usando o método. Para adicionar dados, `AddSeries` você usa o método. Neste exemplo, você `name`usa `xValue`os `yValues` parâmetros `AddSeries` e parâmetros do método. O `name` parâmetro é exibido na legenda do gráfico. O `xValue` parâmetro contém um conjunto de dados exibidos ao longo do eixo horizontal do gráfico. O `yValues` parâmetro contém um conjunto de dados que é usado para traçar os pontos verticais do gráfico.

    O `Write` método realmente renderiza o gráfico. Neste caso, como você não especificou `Chart` um tipo de gráfico, o ajudante renderiza seu gráfico padrão, que é um gráfico de colunas.
3. Execute a página no navegador. O navegador exibe o gráfico. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>Usando uma consulta de banco de dados para dados gráficos

Se as informações que você deseja mapear estão em um banco de dados, você pode executar uma consulta de banco de dados e, em seguida, usar dados dos resultados para criar o gráfico. Este procedimento mostra como ler e exibir os dados do banco de dados criado no artigo [Introdução ao Trabalho com um Banco de Dados em sites de páginas ASP.NET.](https://go.microsoft.com/fwlink/?LinkId=202893)

1. Adicione uma pasta *De dados\_* do aplicativo à raiz do site se a pasta ainda não existir.
2. Na pasta Dados do *\_aplicativo,* adicione o arquivo de banco de dados chamado *SmallBakery.sdf* descrito em [Introdução ao Trabalho com um Banco de Dados em sites de páginas da ASP.NET.](https://go.microsoft.com/fwlink/?LinkId=202893)
3. Crie um novo arquivo chamado *ChartDataQuery.cshtml*.
4. Substitua o conteúdo existente pelo seguinte:   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    O código primeiro abre o banco de dados `db`SmallBakery e atribui-o a uma variável chamada . Esta variável representa `Database` um objeto que pode ser usado para ler e gravar no banco de dados. Em seguida, o código executa uma consulta SQL para obter o nome e o preço de cada produto. O código cria um novo gráfico e passa a consulta `DataBindTable` do banco de dados para ele chamando o método do gráfico. Este método tem dois `dataSource` parâmetros: o parâmetro é para `xField` os dados da consulta, e o parâmetro permite definir qual coluna de dados é usada para o eixo x do gráfico.

    Como alternativa ao `DataBindTable` uso do método, `AddSeries` você `Chart` pode usar o método do ajudante. O `AddSeries` método permite definir `xValue` `yValues` os parâmetros e. Por exemplo, em `DataBindTable` vez de usar o método como este:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    Você pode `AddSeries` usar o método assim:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    Ambos premem os mesmos resultados. O `AddSeries` método é mais flexível porque você pode especificar o `DataBindTable` tipo de gráfico e os dados de forma mais explícita, mas o método é mais fácil de usar se você não precisar da flexibilidade extra.
5. Execute a página em um navegador. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>Usando dados XML

A terceira opção para gráficos é usar um arquivo XML como os dados para o gráfico. Isso requer que o arquivo XML também tenha um arquivo de esquema (arquivo *.xsd)* que descreve a estrutura XML. Este procedimento mostra como ler dados de um arquivo XML.

1. Na pasta Dados do *aplicativo,\_* crie um novo arquivo XML chamado *data.xml*.
2. Substitua o XML existente pelo seguinte, que são alguns dados XML sobre funcionários em uma empresa fictícia. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. Na pasta Dados do *aplicativo,\_* crie um novo arquivo XML chamado *data.xsd*. (Observe que a extensão desta vez é *.xsd*.)
4. Substitua o XML existente pelo seguinte: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. Na raiz do site, crie um novo arquivo chamado *ChartDataXML.cshtml*.
6. Substitua o conteúdo existente pelo seguinte: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    O código primeiro `DataSet` cria um objeto. Este objeto é usado para gerenciar os dados lidos do arquivo XML e organizá-los de acordo com as informações no arquivo do esquema. (Observe que a parte superior do `using SystemData`código inclui a declaração . Isso é necessário para poder trabalhar `DataSet` com o objeto. Para obter mais informações, consulte [ &quot;Usando&quot; declarações e nomes totalmente qualificados](#SB_UsingStatements) mais tarde neste artigo.)

    Em seguida, o `DataView` código cria um objeto com base no conjunto de dados. A exibição de dados fornece um objeto que o gráfico pode vincular a &#8212; que seja, ler e plotar. O gráfico se liga aos `AddSeries` dados usando o método, como você viu anteriormente `xValue` `yValues` ao mapear os `DataView` dados do array, exceto que desta vez os parâmetros e parâmetros são definidos para o objeto.

    Este exemplo também mostra como especificar um determinado tipo de gráfico. Quando os dados são `AddSeries` adicionados `chartType` no método, o parâmetro também é definido para exibir um gráfico de tortas.
7. Execute a página em um navegador. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Usando" declarações e nomes totalmente qualificados
> 
> O Framework .NET que ASP.NET Páginas da Web com sintaxe de navalha é baseado em muitos milhares de componentes (classes). Para torná-lo gerenciável para trabalhar com todas essas classes, eles são organizados em *namespaces*, que são um pouco como bibliotecas. Por exemplo, `System.Web` o namespace contém classes que `System.Xml` suportam a comunicação do navegador/servidor, o namespace contém classes usadas para criar e ler arquivos XML e o `System.Data` namespace contém classes que permitem trabalhar com dados.
> 
> Para acessar qualquer classe dada no .NET Framework, o código precisa saber não apenas o nome da classe, mas também o namespace em que a classe está. Por exemplo, para usar `Chart` o ajudante, o `System.Web.Helpers.Chart` código precisa encontrar a classe, que combina o namespace (`System.Web.Helpers`) com o nome da classe (`Chart`). Isso é conhecido como o nome *totalmente qualificado* da classe &#8212; sua localização completa e inequívoca dentro da vastidão do Quadro .NET. Em código, isso se pareceria com o seguinte:
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> No entanto, é complicado (e propenso a erros) ter que usar esses nomes longos e totalmente qualificados toda vez que você quiser se referir a uma classe ou ajudante. Portanto, para facilitar o uso de nomes de classe, você pode *importar* os namespaces que você está interessado, o que geralmente é apenas um punhado entre os muitos namespaces no .NET Framework. Se você importou um namespace, você pode usar`Chart`apenas um nome de`System.Web.Helpers.Chart`classe ( ) em vez do nome totalmente qualificado (). Quando seu código é executado e encontra um nome de classe, ele pode olhar apenas nos namespaces que você importou para encontrar essa classe.
> 
> Quando você usa ASP.NET Páginas da Web com sintaxe de Navalha para criar `WebPage` páginas da Web, você normalmente usa o mesmo conjunto de classes todas as vezes, incluindo a classe, os vários ajudantes e assim por diante. Para salvar o trabalho de importar os namespaces relevantes toda vez que você criar um site, ASP.NET é configurado para que ele importe automaticamente um conjunto de espaços de nomes principais para cada site. É por isso que você não teve que lidar com namespaces ou importação até agora; todas as aulas com as quais você trabalhou estão em espaços de nomes que já são importados para você.
> 
> No entanto, às vezes você precisa trabalhar com uma classe que não está em um namespace que é automaticamente importado para você. Nesse caso, você pode usar o nome totalmente qualificado dessa classe ou importar manualmente o namespace que contém a classe. Para importar um namespace, `using` você`import` usa a declaração (no Visual Basic), como você viu em um exemplo anterior do artigo.
> 
> Por exemplo, `DataSet` a classe `System.Data` está no namespace. O `System.Data` namespace não está disponível automaticamente para ASP.NET páginas de Navalha. Portanto, para trabalhar `DataSet` com a classe usando seu nome totalmente qualificado, você pode usar código como este:
> 
> `var dataSet = new System.Data.DataSet();`
> 
> Se você tiver `DataSet` que usar a classe repetidamente, você pode importar um namespace como este e, em seguida, usar apenas o nome da classe em código:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> Você pode `using` adicionar instruções para quaisquer outros namespaces de nome .NET Framework que você deseja referenciar. No entanto, como observado, você não precisará fazer isso com frequência, porque a maioria das classes com as quais você trabalhará estão em espaços de nome que são importados automaticamente por ASP.NET para uso em páginas *.cshtml* e *.vbhtml.*

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>Exibindo gráficos dentro de uma página da Web

Nos exemplos que você viu até agora, você cria um gráfico e, em seguida, o gráfico é renderizado diretamente para o navegador como um gráfico. Em muitos casos, porém, você deseja exibir um gráfico como parte de uma página, não apenas por si só no navegador. Para fazer isso é necessário um processo de duas etapas. O primeiro passo é criar uma página que gere o gráfico, como você já viu.

O segundo passo é exibir a imagem resultante em outra página. Para exibir a imagem, `<img>` você usa um elemento HTML, da mesma forma que você faria para exibir qualquer imagem. No entanto, em vez de fazer referência a um arquivo *.jpg* ou `Chart` *.png,* o `<img>` elemento faz referência ao arquivo *.cshtml* que contém o helper que cria o gráfico. Quando a página de `<img>` exibição é `Chart` executada, o elemento obtém a saída do ajudante e renderiza o gráfico.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. Crie um arquivo chamado *ShowChart.cshtml*.
2. Substitua o conteúdo existente pelo seguinte: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    O código `<img>` usa o elemento para exibir o gráfico que você criou anteriormente no arquivo *ChartArrayBasic.cshtml.*
3. Execute a página da Web em um navegador. O arquivo *ShowChart.cshtml* exibe a imagem do gráfico com base no código contido no arquivo *ChartArrayBasic.cshtml.*

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>Estilizando um Gráfico

O `Chart` ajudante suporta um grande número de opções que permitem personalizar a aparência do gráfico. Você pode definir cores, fontes, bordas e assim por diante. Uma maneira fácil de personalizar a aparência de um gráfico é usar um *tema*. Os temas são conjuntos de informações que especificam como renderizar um gráfico usando fontes, cores, rótulos, paletas, bordas e efeitos. (Observe que o estilo de um gráfico não indica o tipo de gráfico.)

A tabela a seguir lista temas incorporados.

| Tema | Descrição |
| --- | --- |
| `Vanilla` | Exibe colunas vermelhas em um fundo branco. |
| `Blue` | Exibe colunas azuis em um fundo gradiente azul. |
| `Green` | Exibe colunas azuis em um fundo gradiente verde. |
| `Yellow` | Exibe colunas laranjas em um fundo gradiente amarelo. |
| `Vanilla3D` | Exibe colunas vermelhas 3D em um fundo branco. |

Você pode especificar o tema a ser usado quando criar um novo gráfico.

1. Crie um novo arquivo chamado *ChartStyleGreen.cshtml*.
2. Substitua o conteúdo existente na página pelo seguinte:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    Este código é o mesmo que o exemplo anterior que `theme` usa o banco `Chart` de dados para dados, mas adiciona o parâmetro quando cria o objeto. A seguir, mostra o código alterado:

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. Execute a página em um navegador. Você vê os mesmos dados de antes, mas o gráfico parece mais polido: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>Salvando um gráfico

Quando você `Chart` usa o ajudante como você viu até agora neste artigo, o ajudante recria o gráfico do zero cada vez que é invocado. Se necessário, o código do gráfico também reconsulta o banco de dados ou relê o arquivo XML para obter os dados. Em alguns casos, fazer isso pode ser uma operação complexa, como se o banco de dados que você está consultando é grande, ou se o arquivo XML contém um monte de dados. Mesmo que o gráfico não envolva muitos dados, o processo de criação dinâmica de uma imagem ocupa recursos do servidor, e se muitas pessoas solicitarem a página ou páginas que exibem o gráfico, pode haver um impacto no desempenho do seu site.

Para ajudá-lo a reduzir o impacto potencial de desempenho da criação de um gráfico, você pode criar um gráfico na primeira vez que precisar dele e, em seguida, salvá-lo. Quando o gráfico é necessário novamente, em vez de recomodá-lo, você pode simplesmente buscar a versão salva e render isso.

Você pode salvar um gráfico desta maneira:

- Cache do gráfico na memória do computador (no servidor).
- Salve o gráfico como um arquivo de imagem.
- Salve o gráfico como um arquivo XML. Esta opção permite modificar o gráfico antes de salvá-lo.

### <a name="caching-a-chart"></a>Cache andaum gráfico

Depois de criar um gráfico, você pode cachê-lo. Cache arqueiar um gráfico significa que ele não precisa ser recriado se precisar ser exibido novamente. Quando você salva um gráfico no cache, você dá a ele uma chave que deve ser exclusiva desse gráfico.

Os gráficos salvos no cache podem ser removidos se o servidor ficar sem memória. Além disso, o cache é limpo se o aplicativo for reiniciado por qualquer motivo. Portanto, a maneira padrão de trabalhar com um gráfico em cache é sempre verificar primeiro se ele está disponível no cache e, se não, para criá-lo ou recriá-lo.

1. Na raiz do seu site, crie um arquivo chamado *ShowCachedChart.cshtml*.
2. Substitua o conteúdo existente pelo seguinte: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    A `<img>` tag inclui `src` um atributo que aponta para o arquivo *ChartSaveToCache.cshtml* e passa uma chave para a página como uma seqüência de consulta. A chave contém &quot;o&quot;valor myChartKey . O arquivo *ChartSaveToCache.cshtml* contém o `Chart` helper que cria o gráfico. Você criará esta página em um momento.

    No final da página há um link para uma página chamada *ClearCache.cshtml*. Essa é uma página que você também criará em breve. Você precisa do *ClearCache.cshtml* apenas para testar o cache para este exemplo — não é um link ou página que você normalmente incluiria ao trabalhar com gráficos em cache.
3. Na raiz do seu site, crie um novo arquivo chamado *ChartSaveToCache.cshtml*.
4. Substitua o conteúdo existente pelo seguinte:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    O código primeiro verifica se algo foi passado como o valor-chave na seqüência de consultas. Se assim for, o código tenta ler um gráfico `GetFromCache` para fora do cache, chamando o método e passando-o a chave. Se não houver nada no cache sob essa tecla (o que aconteceria na primeira vez que o gráfico é solicitado), o código cria o gráfico como de costume. Quando o gráfico é concluído, o código o `SaveToCache`salva no cache chamando . Esse método requer uma chave (para que o gráfico possa ser solicitado mais tarde) e a quantidade de tempo que o gráfico deve ser salvo no cache. (A hora exata em que você armazena um gráfico dependeria de quantas vezes você pensou que os dados que ele representa poderiam mudar.) O `SaveToCache` método também `slidingExpiration` requer um parâmetro &#8212; se isso for definido como verdadeiro, o contador de tempo é redefinido cada vez que o gráfico é acessado. Neste caso, isso significa que a entrada de cache do gráfico expira 2 minutos após a última vez que alguém acessou o gráfico. (A alternativa ao vencimento deslizante é a expiração absoluta, o que significa que a entrada do cache expiraria exatamente 2 minutos após ser colocada no cache, não importa quantas vezes tivesse sido acessada.)

    Finalmente, o código `WriteFromCache` usa o método para buscar e renderizar o gráfico a partir do cache. Observe que este método `if` está fora do bloco que verifica o cache, porque ele obterá o gráfico do cache se o gráfico estava lá para começar ou teve que ser gerado e salvo no cache.

    Observe que, no `AddTitle` exemplo, o método inclui um carimbo de data e hora. (Ele adiciona a data `DateTime.Now` e a hora atuais &#8212; &#8212; ao título.)
5. Crie uma nova página chamada *ClearCache.cshtml* e substitua seu conteúdo pelo seguinte:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    Esta página `WebCache` usa o helper para remover o gráfico armazenado em cache no *ChartSaveToCache.cshtml*. Como observado anteriormente, você normalmente não precisa ter uma página como esta. Você está criando aqui apenas para facilitar o teste de cache.
6. Execute a página *showCachedChart.cshtml* em um navegador. A página exibe a imagem do gráfico com base no código contido no arquivo *ChartSaveToCache.cshtml.* Anote o que diz o carimbo de data e hora no título do gráfico. 

    ![Descrição: Imagem do gráfico básico com carimbo de tempo no título do gráfico](7-displaying-data-in-a-chart/_static/image13.jpg)
7. Feche o navegador.
8. Execute o *ShowCachedChart.cshtml* novamente. Observe que o carimbo de tempo é o mesmo de antes, o que indica que o gráfico não foi regenerado, mas foi lido a partir do cache.
9. Em *ShowCachedChart.cshtml,* clique no link **Limpar cache.** Isso leva você ao *ClearCache.cshtml*, que informa que o cache foi limpo.
10. Clique no **link 'Retornar ao ShowCachedChart.cshtml'** ou reexecute *ShowCachedChart.cshtml* do WebMatrix. Observe que desta vez o carimbo de tempo foi alterado, porque o cache foi limpo. Portanto, o código teve que regenerar o gráfico e colocá-lo de volta no cache.

### <a name="saving-a-chart-as-an-image-file"></a>Salvando um gráfico como um arquivo de imagem

Você também pode salvar um gráfico como um arquivo de imagem (por exemplo, como um arquivo *.jpg)* no servidor. Em seguida, você pode usar o arquivo de imagem da maneira que você faria qualquer imagem. A vantagem é que o arquivo é armazenado em vez de salvo em um cache temporário. Você pode salvar uma nova imagem de gráfico em momentos diferentes (por exemplo, a cada hora) e, em seguida, manter um registro permanente das alterações que ocorrem ao longo do tempo. Observe que você deve ter certeza de que seu aplicativo web tem permissão para salvar um arquivo para a pasta no servidor onde você deseja colocar o arquivo de imagem.

1. Na raiz do seu site, crie uma pasta chamada * \_ChartFiles* se ela ainda não existir.
2. Na raiz do seu site, crie um novo arquivo chamado *ChartSave.cshtml*.
3. Substitua o conteúdo existente pelo seguinte:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    O código primeiro verifica se o arquivo *.jpg* existe chamando o `File.Exists` método. Se o arquivo não existir, o `Chart` código cria um novo a partir de uma matriz. Desta vez, o `Save` código chama `path` o método e passa o parâmetro para especificar o caminho do arquivo e o nome do arquivo de onde salvar o gráfico. No corpo da página, `<img>` um elemento usa o caminho para apontar para o arquivo *.jpg* para exibir.
4. Execute o arquivo *ChartSave.cshtml.*
5. Retorne ao WebMatrix. Observe que um arquivo de imagem chamado *chart01.jpg* foi salvo na * \_pasta ChartFiles.*

### <a name="saving-a-chart-as-an-xml-file"></a>Salvando um gráfico como um arquivo XML

Finalmente, você pode salvar um gráfico como um arquivo XML no servidor. Uma vantagem de usar este método sobre cachedo do gráfico ou salvar o gráfico em um arquivo é que você pode modificar o XML antes de exibir o gráfico se você quiser. Seu aplicativo tem que ter permissões de leitura/gravação para a pasta no servidor onde você deseja colocar o arquivo de imagem.

1. Na raiz do seu site, crie um novo arquivo chamado *ChartSaveXml.cshtml*.
2. Substitua o conteúdo existente pelo seguinte:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    Este código é semelhante ao código que você viu anteriormente para armazenar um gráfico no cache, exceto que ele usa um arquivo XML. O código primeiro verifica se o arquivo XML existe chamando o `File.Exists` método. Se o arquivo existir, o `Chart` código cria um novo `themePath` objeto e passa o nome do arquivo como parâmetro. Isso cria o gráfico com base no que está no arquivo XML. Se o arquivo XML ainda não existir, o código cria `SaveXml` um gráfico como o normal e, em seguida, chama para salvá-lo. O gráfico é renderizado usando o `Write` método, como você já viu antes.

    Assim como na página que mostrava cache, este código inclui um carimbo de data e hora no título do gráfico.
3. Crie uma nova página chamada *ChartDisplayXMLChart.cshtml* e adicione a seguinte marcação: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. Execute a página *ChartDisplayXMLChart.cshtml.* O gráfico é exibido. Anote o carimbo de tempo no título do gráfico.
5. Feche o navegador.
6. No WebMatrix, clique com o botão **Refresh**direito do mouse na * \_pasta ChartFiles,* clique em Atualizar e, em seguida, abra a pasta. O arquivo *XMLChart.xml* nesta pasta foi `Chart` criado pelo ajudante. 

    ![Descrição: A pasta _ChartFiles mostrando o arquivo XMLChart.xml criado pelo ajudante de gráfico.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. Execute novamente a página *ChartDisplayXMLChart.cshtml.* O gráfico mostra o mesmo carimbo de tempo da primeira vez que você executou a página. Isso porque o gráfico está sendo gerado a partir do XML que você salvou anteriormente.
8. No WebMatrix, * \_* abra a pasta ChartFiles e exclua o arquivo *XMLChart.xml.*
9. Execute a página *ChartDisplayXMLChart.cshtml* mais uma vez. Desta vez, o carimbo de `Chart` tempo é atualizado, porque o ajudante teve que recriar o arquivo XML. Se você quiser, * \_* verifique a pasta ChartFiles e observe que o arquivo XML está de volta.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Recursos adicionais

- [Introdução ao trabalho com um banco de dados em sites de páginas da Web ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202893)
- [Usando cache em sites de páginas da Web ASP.NET para melhorar o desempenho](https://go.microsoft.com/fwlink/?LinkId=202903)
- [Classe de gráficos](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (ASP.NET referência de API de páginas da Web no MSDN)
