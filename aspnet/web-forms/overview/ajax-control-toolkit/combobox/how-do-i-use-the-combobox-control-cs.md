---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: Como uso o Controle ComboBox? (C#) | Microsoft Docs
author: rick-anderson
description: O ComboBox é um controle AJAX ASP.NET que combina a flexibilidade de uma TextBox com uma lista de opções das quais os usuários podem escolher.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2adb9663cb7bdc38f28a127f7932f45a3447d1de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543789"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>Como uso o Controle ComboBox? (C#)

pela [Microsoft](https://github.com/microsoft)

> O ComboBox é um controle AJAX ASP.NET que combina a flexibilidade de uma TextBox com uma lista de opções das quais os usuários podem escolher.

O objetivo deste tutorial é explicar o controle AJAX Control Toolkit ComboBox. O ComboBox funciona como uma combinação entre um controle padrão ASP.NET DropDownList e um controle TextBox. Você pode selecionar a partir de uma lista pré-existente de itens ou inserir um novo item.

O ComboBox é semelhante ao extensor de controle AutoComplete, mas os controles são usados em diferentes cenários. O extensor AutoComplete consulta um serviço web para obter entradas correspondentes. O controle ComboBox, em contraste, é inicializado com um conjunto de itens. Usar o extensor AutoComplete faz sentido quando você está trabalhando com um grande conjunto de dados (milhões de peças de carro) enquanto usa o controle ComboBox faz sentido ao trabalhar com um pequeno conjunto de dados (dezenas de peças de carro).

## <a name="selecting-from-a-static-list-of-items"></a>Selecionando a partir de uma lista estática de itens

Vamos começar com uma amostra simples de usar o controle ComboBox. Imagine que você deseja exibir uma lista estática de itens em uma lista de itens parado. No entanto, você quer deixar em aberto a possibilidade de que a lista não está completa. Você deseja permitir que um usuário insira um valor personalizado na lista.

Criaremos uma nova página de Formulários da ASP.NET web e usaremos o controle ComboBox na página. Adicione a nova página de ASP.NET ao seu projeto e mude para exibição Design.

Se você quiser usar o controle ComboBox na página, então você deve adicionar um controle ScriptManager à página. Arraste o controle scriptmanager abaixo da guia Extensões AJAX para a superfície do Designer. Você deve adicionar o controle ScriptManager na parte superior da página; você pode adicioná-lo imediatamente abaixo &lt;&gt; da tag de formulário do lado do servidor de abertura.

Em seguida, arraste o controle ComboBox para a página. Você pode encontrar o controle ComboBox na caixa de ferramentas com os outros controles e extensores de controle do AJAX Control Toolkit (ver figura1).

[![Formulário simples para criar um cartão de visita](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**Figura 01**: Selecionando o controle ComboBox na caixa de ferramentas[(Clique para ver a imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image2.png)

Usaremos o controle ComboBox para exibir uma lista estática de opções. O usuário pode selecionar um nível particular de picante para sua comida a partir de uma lista de três opções: Leve, Médio e Quente (ver Figura 2).

[![Selecionando a partir de uma lista estática de itens](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**Figura 02**: Seleção a partir de uma lista estática de itens[(Clique para exibir imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image4.png)

Há duas maneiras de adicionar essas opções ao controle comboBox. Primeiro, selecione a opção Editar opções ao passar o mouse sobre o controle na exibição Design e abrir o Editor de itens (consulte Figura 3).

[![Edição de itens da ComboBox](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**Figura 03**: Edição de itens da ComboBox[(Clique para ver imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image6.png)

A segunda opção é adicionar a lista de itens &lt;entre as tags&gt; de abertura e fechamento asp:ComboBox na exibição Origem. A página na Lista 1 contém o ComboBox atualizado que tem a lista de itens.

**Listagem 1 - Static.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

Ao abrir a página na Lista 1, você pode selecionar uma das opções pré-existentes na ComboBox. Em outras palavras, o ComboBox funciona como um controle DropDownList.

No entanto, você também tem a opção de entrar em uma nova escolha (por exemplo, Super Picante) que não está na lista existente. Assim, o ComboBox também funciona como um controle TextBox.

Independentemente de você escolher um item pré-existente ou digitar um item personalizado, quando você enviar o formulário, sua escolha aparece no controle do rótulo. Quando você envia o formulário,\_o manipulador btnSubmit Click executa e atualiza o rótulo (veja Figura 4).

[![Exibindo o item selecionado](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**Figura 04**: Exibindo o item selecionado[(Clique para exibir a imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image8.png)

O ComboBox suporta as mesmas propriedades do controle DropDownList para recuperar o item selecionado após o envio de um formulário:

- SelectedItem.Text - Exibe o valor da propriedade Texto do item selecionado.
- SelectedItem.Value - Exibe o valor da propriedade Valor do item selecionado ou exibe o texto digitado na ComboBox.
- SelectedValue - O mesmo que SelectedItem.Value, exceto que essa propriedade permite que você especifique o item selecionado padrão (inicial).

Se você digitar uma escolha personalizada na ComboBox, a escolha personalizada será atribuída às propriedades SelectedItem.Text e SelectedItem.Value.

## <a name="selecting-the-list-of-items-from-the-database"></a>Selecionando a Lista de Itens do Banco de Dados

Você pode recuperar a lista de itens que o ComboBox exibe a partir de um banco de dados. Por exemplo, você pode vincular o ComboBox a um controle SqlDataSource, um controle ObjectDataSource, um LinqDataSource ou um EntityDataSource.

Imagine que você deseja exibir uma lista de filmes em uma ComboBox. Você deseja recuperar a lista de filmes da tabela de banco de dados Filmes. Siga estas etapas:

1. Crie uma página chamada Movies.aspx
2. Adicione um controle scriptmanager à página arrastando o ScriptManager da guia Extensões AJAX na caixa de ferramentas para a página.
3. Adicione um controle ComboBox à página arrastando o ComboBox para a página.
4. Na exibição Design, passe o mouse sobre o controle do ComboBox e selecione a opção Escolher a tarefa **Origem de dados** (consulte Figura 5). O Assistente de Configuração de Origem de Dados é lançado.
5. Na **etapa Escolha uma Fonte de Dados,** selecione a &lt;opção Nova fonte de&gt; dados.
6. Na **etapa Escolher um tipo de origem de dados,** selecione Banco de Dados.
7. Na etapa **Escolher sua conexão de dados,** selecione seu banco de dados (por exemplo, MoviesDB.mdf).
8. Na **seqüência Salvar a seqüência de conexões na etapa Arquivo de configuração do aplicativo,** selecione a opção para salvar a seqüência de conexões.
9. Na **etapa Configurar a medida 'Selecionar',** selecione a tabela de banco de dados Filmes e selecione todas as colunas.
10. Na etapa **Consulta de teste,** clique no botão Concluir.
11. De volta na etapa **Escolher origem de dados,** selecione a coluna Título para o campo a ser exibido e a coluna 'Id' para o campo de dados (ver Figura).
12. Clique no botão OK para fechar o assistente.

[![Escolhendo uma fonte de dados](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**Figura 05**: Escolher uma fonte de dados[(Clique para visualizar imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image10.png)

[![Escolhendo os campos de texto e valor dos dados](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**Figura 06**: Escolhendo os campos de texto e valor dos dados[(Clique para visualizar a imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image12.png)

Depois de concluir as etapas acima, o ComboBox fica vinculado a um controle SqlDataSource que representa os filmes da tabela de banco de dados Filmes. A fonte para a página se parece com a Listagem 2 (eu limpei um pouco a formatação).

**Listagem 2 - Movies.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

Observe que o controle ComboBox tem uma propriedade DataSourceID que aponta para o controle SqlDataSource. Quando você abre a página em um navegador, a lista de filmes do banco de dados é exibida (veja Figura 7). Você pode escolher um filme da lista ou inserir um novo filme digitando o filme na ComboBox.

[![Exibindo uma lista de filmes](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**Figura 07**: Exibindo uma lista de filmes[(Clique para ver imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image14.png)

## <a name="setting-the-dropdownstyle"></a>Definindo o DropDownStyle

Você pode usar a propriedade ComboBox DropDownStyle para alterar o comportamento da ComboBox. Esta propriedade aceita valores possíveis:

- DropDown - (valor padrão) O ComboBox exibe uma lista de parada quando você clica na seta e você pode inserir um valor personalizado.
- Simples - O ComboBox exibe uma lista de isento automaticamente e você pode inserir um valor personalizado.
- DropDownList - O ComboBox funciona como um controle DropDownList.

A diferença entre DropDown e Simple é quando a lista de itens é exibida. No caso do Simple, a lista é exibida imediatamente quando você move o foco para a ComboBox. No caso do DropDown, você deve clicar na seta para ver a lista de itens.

O valor Do DropDownList faz com que o controle ComboBox funcione como um controle padrão do DropDownList. No entanto, há uma diferença importante aqui. Versões mais antigas do Internet Explorer exibem um controle DropDownList com um índice z infinito para que o controle apareça na frente de qualquer controle colocado na frente dele. Como o ComboBox renderiza &lt;uma&gt; tag de &lt;div HTML em vez de uma tag selecionada HTML,&gt; o ComboBox respeita corretamente o pedido z.

## <a name="setting-the-autocompletemode"></a>Configuração do modo autocompleto

Você usa a propriedade ComboBox AutoCompleteMode para especificar o que acontece quando alguém digita texto na ComboBox. Esta propriedade aceita os seguintes valores possíveis:

- Nenhum - (valor padrão) O ComboBox não fornece nenhum comportamento de auto-completo.
- Sugerir - O ComboBox exibe a lista e destaca o item correspondente na lista (ver Figura 8).
- Anexo - O ComboBox não exibe a lista e anexa o item correspondente da lista ao que você digitou (ver Figura 9).
- Sugestion - O ComboBox exibe a lista e anexa o item correspondente da lista para o que você digitou (veja Figura 10).

[![O ComboBox faz uma sugestão](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**Figura 08**: O ComboBox faz uma sugestão[(Clique para ver a imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image16.png)

[![ComboBox anexa texto correspondente](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**Figura 09**: AboBox anexa texto correspondente[(Clique para exibir imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image18.png)

[![O ComboBox sugere e anexa](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**Figura 10**: O ComboBox sugere e anexa[(Clique para ver imagem em tamanho real)](how-do-i-use-the-combobox-control-cs/_static/image20.png)

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu a usar o controle ComboBox para exibir um conjunto fixo de itens. Nós vinculamos o controle comboBox tanto a um conjunto estático de itens quanto a uma tabela de banco de dados. Finalmente, você aprendeu como modificar o comportamento do ComboBox definindo suas propriedades DropDownStyle e AutoCompleteMode.

> [!div class="step-by-step"]
> [Avançar](how-do-i-use-the-combobox-control-vb.md)
