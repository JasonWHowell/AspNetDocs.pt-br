---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 'Iteração #1 – Criar o Aplicativo (VB) | Microsoft Docs'
author: rick-anderson
description: 'Na primeira iteração, criamos o Contact Manager da maneira mais simples possível. Adicionamos suporte para operações básicas de banco de dados: Criar, Ler, Atualizar e D...'
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: 235f6f8812a2f584de8e07dcf97d5c1712c51776
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542528"
---
# <a name="iteration-1--create-the-application-vb"></a>Iteração nº 1 – criar o aplicativo (VB)

pela [Microsoft](https://github.com/microsoft)

[Código de download](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> Na primeira iteração, criamos o Contact Manager da maneira mais simples possível. Adicionamos suporte para operações básicas de banco de dados: Criar, Ler, Atualizar e Excluir (CRUD).

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Construindo um Aplicativo de ASP.NET De Gerenciamento de Contato (VB)

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

Nesta primeira iteração, construímos a aplicação básica. O objetivo é construir o Contact Manager da maneira mais rápida e simples possível. Em iterações posteriores, melhoramos o design da aplicação.

O aplicativo Contact Manager é um aplicativo básico orientado pelo banco de dados. Você pode usar o aplicativo para criar novos contatos, editar contatos existentes e excluir contatos.

Nesta iteração, completamos as seguintes etapas:

1. ASP.NET aplicação MVC
2. Crie um banco de dados para armazenar nossos contatos
3. Gerar uma classe modelo para o nosso banco de dados com o Microsoft Entity Framework
4. Crie uma ação e visualização do controlador que nos permite listar todos os contatos no banco de dados
5. Criar ações de controlador e uma visão que nos permita criar um novo contato no banco de dados
6. Criar ações de controlador e uma exibição que nos permita editar um contato existente no banco de dados
7. Criar ações de controlador e uma exibição que nos permita excluir um contato existente no banco de dados

## <a name="software-prerequisites"></a>Pré-requisitos de software

Em ASP.NET aplicativos MVC, você deve ter o Visual Studio 2008 ou o Visual Web Developer 2008 instalados em seu computador (Visual Web Developer é uma versão gratuita do Visual Studio que não inclui todos os recursos avançados do Visual Studio). Você pode baixar a versão de teste do Visual Studio 2008 ou do Visual Web Developer a partir do seguinte endereço:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Para ASP.NET aplicativos MVC com visual Web Developer, você deve ter o Visual Web Developer Service Pack 1 instalado. Sem o Service Pack 1, você não pode criar projetos de aplicativos da Web.

ASP.NET estrutura MVC. Você pode baixar a ASP.NET estrutura MVC a partir do seguinte endereço:

[https://www.asp.net/mvc](../../../index.md)

Neste tutorial, usamos o Microsoft Entity Framework para acessar um banco de dados. O Quadro de Entidades está incluído no .NET Framework 3.5 Service Pack 1. Você pode baixar este pacote de serviço sumal

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

Como alternativa para realizar cada um desses downloads, você pode aproveitar o Web Platform Installer (Web PI). Você pode baixar o Web PI a partir do seguinte endereço:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>Projeto MVC ASP.NET

ASP.NET Projeto de Aplicação Web MVC. Inicie o Visual Studio e selecione a opção menu **Arquivo, Novo Projeto**. A caixa de diálogo **Novo Projeto** é exibida (ver Figura 1). Selecione o tipo de projeto **Web** e o **modelo de aplicativo web ASP.NET MVC.** Nomeie seu novo projeto *ContactManager* e clique no botão OK.

Certifique-se de que você tenha o .NET Framework 3.5 selecionado na lista de isapé no canto superior direito da caixa de diálogo **Novo Projeto.** Caso contrário, o modelo ASP.NET mvc web application não aparecerá.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**Figura 01**: A caixa de diálogo Novo Projeto[(Clique para exibir imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image2.png)

ASP.NET aplicativo MVC, a caixa de diálogo **Criar projeto de teste de unidade** é exibida. Você pode usar esta caixa de diálogo para indicar que deseja criar e adicionar um projeto de teste de unidade à sua solução quando criar seu aplicativo MVC ASP.NET. Embora não estejamos construindo testes de unidade nesta iteração, você deve selecionar a opção **Sim, criar um projeto de teste de unidade** porque planejamos adicionar testes unitários em uma iteração posterior. Adicionar um projeto de teste quando você cria um novo projeto mvc ASP.NET é muito mais fácil do que adicionar um projeto de teste após a criação do projeto MVC ASP.NET.

> [!NOTE] 
> 
> Como o Visual Web Developer não suporta projetos de teste, você não recebe a caixa de diálogo Criar unidade de teste do projeto ao usar o Visual Web Developer.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**Figura 02**: A caixa de diálogo Projeto de teste da unidade de criação[(clique para exibir a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image4.png)

ASP.NET aplicativo MVC aparece na janela Visual Studio Solution Explorer (ver Figura 3). Se você não ver a janela Solution Explorer, então você pode abrir esta janela selecionando a opção menu **Exibir, Solution Explorer**. Observe que a solução contém dois projetos: o projeto mvc ASP.NET e o projeto Teste. O projeto mvc ASP.NET é chamado ContactManager e o projeto Teste é chamado ContactManager.Tests.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**Figura 03**: A janela Solution Explorer[(Clique para ver a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image6.png)

## <a name="deleting-the-project-sample-files"></a>Excluindo os arquivos de amostra de projeto

O modelo de projeto mvc ASP.NET inclui arquivos de exemplo para controladores e visualizações. Antes de criar um novo aplicativo mvc ASP.NET, você deve excluir esses arquivos. Você pode excluir arquivos e pastas na janela Solution Explorer clicando com o botão direito do mouse em um arquivo ou pasta e selecionando a opção menu **Excluir**.

Você precisa excluir os seguintes arquivos do projeto MVC ASP.NET:

- \Controladores\HomeController.vb

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

E, você precisa excluir o seguinte arquivo do projeto Teste:

\Controladores\HomeControllerTest.vb

## <a name="creating-the-database"></a>Criando o Banco de Dados

O aplicativo Contact Manager é um aplicativo web orientado pelo banco de dados. Usamos um banco de dados para armazenar as informações de contato.

O ASP.NET estrutura MVC com qualquer banco de dados moderno, incluindo bancos de dados Microsoft SQL Server, Oracle, MySQL e IBM DB2. Neste tutorial, usamos um banco de dados microsoft SQL Server. Quando você instala o Visual Studio, você tem a opção de instalar o Microsoft SQL Server Express, que é uma versão gratuita do banco de dados do Microsoft SQL Server.

Crie um novo banco de dados\_clicando com o botão direito do mouse na pasta Dados do aplicativo na janela Do Explorador de Soluções e selecionando a opção de menu **Adicionar, Novo Item**. Na caixa de diálogo **Adicionar novo item,** selecione a categoria **Dados** e o modelo **sql server database** (consulte Figura 4). Nomeie o novo banco de dados ContactManagerDB.mdf e clique no botão OK.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**Figura 04**: Criação de um novo banco de dados Microsoft SQL Server Express[(Clique para ver imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image8.png)

Depois de criar o novo banco de\_dados, o banco de dados aparece na pasta Dados do aplicativo na janela Solution Explorer. Clique duas vezes no arquivo ContactManager.mdf para abrir a janela Server Explorer e conectar-se ao banco de dados.

> [!NOTE] 
> 
> A janela Server Explorer é chamada de janela Database Explorer no caso do Microsoft Visual Web Developer.

Você pode usar a janela do Server Explorer para criar novos objetos de banco de dados, como tabelas de banco de dados, visualizações, gatilhos e procedimentos armazenados. Clique com o botão direito do mouse na pasta Tabelas e selecione a opção de menu **Adicionar nova tabela**. O Designer de Tabela de Banco de Dados é exibido (ver Figura 5).

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**Figura 05**: O Designer da Tabela do Banco de Dados[(Clique para ver a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image10.png)

Precisamos criar uma tabela que contenha as seguintes colunas:

<a id="0.2_table01"></a>

| **Nome da coluna** | **Tipo de dados** | **Permitir Nulos** |
| --- | --- | --- |
| ID | INT | false |
| Nome | nvarchar (50) | false |
| LastName | nvarchar (50) | false |
| Telefone | nvarchar (50) | false |
| Email | nvarchar (255) | false |

A primeira coluna, a coluna id, é especial. Você precisa marcar a coluna Id como uma coluna identidade e uma coluna Chave Principal. Você indica que uma coluna é uma coluna De identidade expandindo propriedades da coluna (olhe na parte inferior da Figura 6) e descendo até a propriedade Especificação de identidade. Defina a propriedade **(É identidade)** para o valor **Sim**.

Você marca uma coluna como uma coluna Chave Principal selecionando a coluna e clicando no botão com o ícone de uma tecla. Depois que uma coluna é marcada como uma coluna Chave Principal, um ícone de uma chave aparece ao lado da coluna (ver Figura 6).

Depois de terminar de criar a tabela, clique no botão Salvar (o botão com um ícone de um disquete) para salvar a nova tabela. Dê à sua nova tabela o nome *Contatos*.

Depois de terminar de criar a tabela de banco de dados Contatos, você deve adicionar alguns registros à tabela. Clique com o botão direito do mouse na tabela Contatos na janela Server Explorer e selecione a opção menu **Mostrar dados da tabela**. Digite um ou mais contatos na grade que aparece.

## <a name="creating-the-data-model"></a>Criando o modelo de dados

O ASP.NET aplicativo MVC consiste em Modelos, Visualizações e Controladores. Começamos criando uma classe Modelo que representa a tabela Contatos que criamos na seção anterior.

Neste tutorial, usamos o Microsoft Entity Framework para gerar uma classe modelo a partir do banco de dados automaticamente.

> [!NOTE] 
> 
> A ASP.NET estrutura MVC não está vinculada ao Microsoft Entity Framework de forma alguma. Você pode usar ASP.NET MVC com tecnologias alternativas de acesso ao banco de dados, incluindo NHibernate, LINQ para SQL ou ADO.NET.

Siga estas etapas para criar as classes do modelo de dados:

1. Clique com o botão direito do mouse na pasta Modelos na janela Solution Explorer e selecione **Adicionar, Novo Item**. A caixa de diálogo **Adicionar novo item** é exibida (consulte Figura 6).
2. Selecione a categoria **Dados** e o modelo **de modelo de dados de entidade ADO.NET.** Nomeie seu modelo de dados *ContactManagerModel.edmx* e clique no botão **Adicionar.** O assistente modelo de dados da entidade é exibido (ver Figura 7).
3. Na etapa **Escolher conteúdo de modelo,** selecione **Gerar no banco de dados** (ver Figura 7).
4. Na **etapa Escolha sua conexão de dados,** selecione o banco de dados ContactManagerDB.mdf e digite o nome *ContactManagerDBEntities* para as Configurações de Conexão de Entidade (ver Figura 8).
5. Na etapa **Escolher objetos do banco de dados,** selecione a caixa de seleção rotulada Tabelas (ver Figura 9). O modelo de dados incluirá todas as tabelas contidas em seu banco de dados (há apenas uma, a tabela Contatos). Digite o namespace *Models*. Clique no botão Concluir para completar o assistente.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**Figura 06**: A caixa de diálogo Adicionar novo item[(Clique para exibir a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image12.png)

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**Figura 07**: Escolha conteúdo do modelo ([Clique para ver a imagem em tamanho real](iteration-1-create-the-application-vb/_static/image14.png))

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**Figura 08**: Escolha sua conexão de dados[(Clique para ver a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image16.png)

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**Figura 09**: Escolha seus objetos de banco de dados ([Clique para ver a imagem em tamanho real](iteration-1-create-the-application-vb/_static/image18.png))

Depois de concluir o Assistente do Modelo de Dados da Entidade, o Designer de Modelo de Dados de Entidade será exibido. O designer exibe uma classe que corresponde a cada tabela que está sendo modelada. Você deveria ver uma classe chamada Contatos.

O assistente Modelo de Dados de Entidade gera nomes de classe com base em nomes de tabela de banco de dados. Você quase sempre precisa mudar o nome da classe gerada pelo assistente. Clique com o botão direito do mouse na classe Contatos no designer e selecione a opção menu **Renomear**. Mude o nome da classe de Contatos (plural) para Contato (singular). Depois de alterar o nome da classe, a classe deve aparecer como figura 10.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**Figura 10**: A classe Contato[(Clique para ver a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image20.png)

Neste ponto, criamos nosso modelo de banco de dados. Podemos usar a classe Contato para representar um registro de contato específico em nosso banco de dados.

## <a name="creating-the-home-controller"></a>Criando o Controlador Doméstico

O próximo passo é criar nosso controlador Home. O controlador Home é o controlador padrão invocado em um ASP.NET aplicativo MVC.

Crie a classe controlador a inicial, clicando com o botão direito do mouse na pasta Controladores na janela Do Explorador de Soluções e selecionando a opção menu **Adicionar, Controlador** (ver Figura 11). Observe a caixa de seleção rotulada **Adicionar métodos de ação para criar, atualizar e detalhes cenários**. Certifique-se de que esta caixa de seleção é verificada antes de clicar no botão **Adicionar.**

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**Figura 11**: Adicionando o controlador Home[(Clique para exibir a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image22.png)

Quando você cria o controlador Home, você recebe a classe na Listagem 1.

**Listagem 1 - Controladores\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>Listando os Contatos

Para exibir os registros na tabela de banco de dados Contatos, precisamos criar uma ação Index() e uma exibição de Índice.

O controlador Home já contém uma ação Index(). Precisamos modificar este método para que ele se pareça com a Lista 2.

**Listagem 2 - Controladores\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

Observe que a classe controladora Home na \_Listagem 2 contém um campo privado chamado entidades. O \_campo de entidades representa as entidades do modelo de dados. Usamos o \_campo de entidades para comunicar com o banco de dados.

O método Index() retorna uma exibição que representa todos os contatos da tabela de banco de dados Contatos. As \_entidades de expressão. ContactSet.ToList() retorna a lista de contatos como uma lista genérica.

Agora que criamos o controlador de índice, precisamos criar a exibição Índice. Antes de criar a exibição Índice, compile seu aplicativo selecionando a opção de menu **Build, Build Solution**. Você deve sempre compilar seu projeto antes de adicionar uma exibição para que a lista de classes de modelo seja exibida na caixa de diálogo **Adicionar exibição.**

Você cria a exibição Índice clicando com o botão direito do mouse no método Index() e selecionando a opção de menu **Adicionar exibição** (ver Figura 12). A seleção desta opção de menu abre a caixa de diálogo **Adicionar exibição** (consulte Figura 13).

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**Figura 12**: Adicionando a exibição Índice[(Clique para exibir imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image24.png)

Na **caixa de** diálogo Adicionar exibição, marque a caixa de seleção rotulada **Criar uma exibição fortemente digitada**. Selecione a classe exibir dados ContactManager.Contact e a Lista de conteúdo Exibir. A seleção dessas opções gera uma exibição que exibe uma lista de registros de contato.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**Figura 13**: A caixa de diálogo Adicionar exibição[(Clique para exibir a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image26.png)

Quando você **clica** no botão Adicionar, a exibição Índice na Listagem 3 é gerada. Observe &lt;a diretiva&gt; %@ Page % que aparece na parte superior do arquivo. A exibição Índice herda&lt;da classe&lt;ContactManager.Models.Contact.Contact.&gt; &gt; Em outras palavras, a classe Modelo na exibição representa uma lista de entidades de contato.

O corpo da exibição Índice contém um loop forcada que itera através de cada um dos contatos representados pela classe Modelo. O valor de cada propriedade da classe Contato é exibido dentro de uma tabela HTML.

**Listagem 3 - Views\Home\Index.aspx (não modificado)**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

Precisamos fazer uma modificação na visão do Índice. Como não estamos criando uma exibição Detalhes, podemos remover o link Detalhes. Encontre e remova o seguinte código da exibição Índice:

{.id = item. Id})%&gt;

Depois de modificar a exibição Índice, você pode executar o aplicativo Gerenciador de contatos. Selecione a opção de menu Debug, Start Debugging ou simplesmente pressione F5. A primeira vez que você executar o aplicativo, você recebe a caixa de diálogo na Figura 14. Selecione a opção **Modifique o arquivo Web.config para ativar a depuração** e clique no botão OK.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**Figura 14**: Habilitação da depuração[(Clique para exibir imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image28.png)

A exibição Índice é devolvida por padrão. Esta exibição lista todos os dados da tabela de banco de dados Contatos (ver Figura 15).

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**Figura 15**: A exibição Índice[(Clique para ver a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image30.png)

Observe que a exibição Índice inclui um link rotulado Criar novo na parte inferior da exibição. Na próxima seção, você aprende a criar novos contatos.

## <a name="creating-new-contacts"></a>Criando novos contatos

Para permitir que os usuários criem novos contatos, precisamos adicionar duas ações de Criar() ao controlador Home. Precisamos criar uma ação Create() que retorne um formulário HTML para criar um novo contato. Precisamos criar uma segunda ação de Criar() que realize a inserção real do banco de dados do novo contato.

Os novos métodos Create() que precisamos adicionar ao controlador Home estão contidos na Lista 4.

**Listagem 4 - Controladores\HomeController.vb (com métodos de criação)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

O primeiro método Criar() pode ser invocado com um HTTP GET enquanto o segundo método Criar() pode ser invocado apenas por um POST HTTP. Em outras palavras, o segundo método Create() só pode ser invocado ao postar um formulário HTML. O primeiro método Criar() simplesmente retorna uma exibição que contém o formulário HTML para criar um novo contato. O segundo método Create() é muito mais interessante: adiciona o novo contato ao banco de dados.

Observe que o segundo método Criar() foi modificado para aceitar uma instância da classe Contato. Os valores de formulário publicados a partir do formulário HTML estão vinculados a esta classe De contato pela ASP.NET estrutura MVC automaticamente. Cada campo de formulário do formulário HTML Criar é atribuído a uma propriedade do parâmetro Contato.

Observe que o parâmetro Contato é decorado com um atributo [Vincular]. O atributo [Vincular] é usado para excluir a propriedade Contact Id da vinculação. Como a propriedade de identificação representa uma propriedade de identidade, não queremos definir a propriedade de identificação.

No corpo do método Criar() o Framework entity é usado para inserir o novo Contato no banco de dados. O novo Contato é adicionado ao conjunto existente de Contatos e o método SaveChanges() é chamado para empurrar essas alterações de volta para o banco de dados subjacente.

Você pode gerar um formulário HTML para criar novos contatos clicando com o botão direito do mouse em qualquer um dos dois métodos Criar() e selecionando a opção de menu **Adicionar exibição** (ver Figura 16).

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**Figura 16**: Adicionando a exibição Criar[(Clique para exibir imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image32.png)

Na caixa de diálogo **Adicionar exibição,** selecione a classe **ContactManager.Contact** e a opção **Criar** para exibir conteúdo (consulte Figura 17). Quando você **clica** no botão Adicionar, uma exibição Criar é gerada automaticamente.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**Figura 17**: Ver uma página explodir[(Clique para ver a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image34.png)

A exibição Criar contém campos de formulário para cada uma das propriedades da classe Contato. O código para a exibição Criar está incluído na Lista 5.

**Listagem 5 - Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

Depois de modificar os métodos Criar e adicionar a exibição Criar, você pode executar o aplicativo Contact Manger e criar novos contatos. Clique no **link Criar novo** que aparece na exibição 'Índice' para navegar até a exibição Criar. Você deve ver a vista na Figura 18.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**Figura 18**: A exibição criar ([Clique para ver a imagem em tamanho real](iteration-1-create-the-application-vb/_static/image36.png))

## <a name="editing-contacts"></a>Edição de contatos

Adicionar a funcionalidade para editar um registro de contato é muito semelhante à adição da funcionalidade para criar novos registros de contato. Primeiro, precisamos adicionar dois novos métodos de edição à classe controlador a casa. Estes novos métodos de edição() estão contidos na Lista 6.

**Listagem 6 - Controladores\HomeController.vb (com métodos de edição)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

O primeiro método Editar() é invocado por uma operação HTTP GET. Um parâmetro de Id é passado para este método que representa a Id do registro de contato que está sendo editado. O Quadro de Entidades é usado para recuperar um contato que corresponda ao Id. Uma exibição que contém um formulário HTML para editar um registro é devolvida.

O segundo método Editar() executa a atualização real para o banco de dados. Este método aceita uma instância da classe Contato como parâmetro. A ASP.NET estrutura MVC vincula os campos de formulário do formulário editais a esta classe automaticamente. Observe que você não inclui o atributo [Vincular] ao editar um Contato (precisamos do valor da propriedade Id).

O Framework entity é usado para salvar o Contato modificado no banco de dados. O Contato original deve ser recuperado do banco de dados primeiro. Em seguida, o método Entity Framework ApplyPropertyChanges() é chamado para registrar as alterações no Contato. Finalmente, o método Entity Framework SaveChanges() é chamado para persistir as alterações no banco de dados subjacente.

Você pode gerar a exibição que contém o formulário Editar clicando com o botão direito do mouse no método Editar() e selecionar a opção de menu Adicionar exibição. Na caixa de diálogo Adicionar exibição, selecione a classe **ContactManager.Models.Contact** e o conteúdo de exibição **Editar** (consulte Figura 19).

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**Figura 19**: Adicionando uma exibição de edição[(Clique para exibir imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image38.png)

Quando você clica no botão Adicionar, uma nova exibição Editar é gerada automaticamente. O formulário HTML gerado contém campos que correspondem a cada uma das propriedades da classe Contato (ver Lista 7).

**Listagem 7 - Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>Excluindo contatos

Se você quiser excluir contatos, você precisa adicionar duas ações excluir() à classe controlador a home. A primeira ação Excluir() exibe um formulário de confirmação de exclusão. A segunda ação Excluir() executa a exclusão real.

> [!NOTE] 
> 
> Mais tarde, no Iteração #7, modificamos o Contact Manager para que ele suporte uma exclusão de um passo do Ajax.

Os dois novos métodos Delete() estão contidos na Lista 8.

**Lista 8 - Controladores\HomeController.vb (Métodos de exclusão)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

O primeiro método Excluir() retorna um formulário de confirmação para excluir um registro de contato do banco de dados (ver Figura20). O segundo método Excluir() executa a operação de exclusão real contra o banco de dados. Depois que o contato original foi recuperado do banco de dados, os métodos Entity Framework DeleteObject() e SaveChanges() são chamados para executar a exclusão do banco de dados.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**Figura 20**: A exibição de confirmação de exclusão[(Clique para exibir a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image40.png)

Precisamos modificar a exibição Índice para que ela contenha um link para excluir registros de contato (ver Figura 21). Você precisa adicionar o seguinte código à mesma célula de tabela que contém o link Editar:

{.id = item. Id})%&gt;

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**Figura 21**: Exibição de índice com link de edição[(Clique para ver imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image42.png)

Em seguida, precisamos criar a exibição de confirmação de exclusão. Clique com o botão direito do mouse no método Excluir() na classe controlador a home e selecione a opção de menu Adicionar exibição. A caixa de diálogo Adicionar exibição é exibida (consulte Figura 22).

Ao contrário do caso das exibições 'Lista,Criar e Editar', a caixa de diálogo Adicionar exibição não contém uma opção para criar uma exibição Excluir. Em vez disso, selecione a classe de dados **ContactManager.Models.Contact** e o conteúdo de exibição **Vazio.** Selecionar a opção de conteúdo de exibição vazia exigirá que criemos a exibição nós mesmos.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**Figura 22**: Adicionando a exibição de confirmação de exclusão[(Clique para exibir a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image44.png)

O conteúdo da exibição Excluir está contido na Lista 9. Esta exibição contém um formulário que confirma se um contato específico deve ou não ser excluído (ver Figura 21).

**Listagem 9 - Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>Alterando o nome do controlador padrão

Pode incomodá-lo que o nome da nossa classe de controladores para trabalhar com contatos seja chamado de classe HomeController. O controlador não deveria ser chamado contactcontroller?

Este problema é fácil de resolver. Primeiro, precisamos refatorar o nome do controlador doméstico. Abra a classe HomeController no Visual Studio Code Editor, clique com o botão direito do mouse no nome da classe e selecione a opção menu **Renomear**. A seleção desta opção de menu abre a caixa de diálogo Renomear.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**Figura 23**: Refatoração de um nome de controlador[(Clique para exibir imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image46.png)

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**Figura 24**: Usando a caixa de diálogo Renomear[(Clique para exibir a imagem em tamanho real)](iteration-1-create-the-application-vb/_static/image48.png)

Se você renomear sua classe de controlador, o Visual Studio atualizará o nome da pasta na pasta Visualizações também. O Visual Studio renomeará a pasta \Views\Home para a pasta \Views\Contact.

Depois de fazer essa alteração, seu aplicativo não terá mais um controlador Home. Quando você executar o seu aplicativo, você terá a página de erro na Figura 25.

[![A caixa de diálogo Novo Projeto](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**Figura 25**: Sem controlador padrão[(Clique para exibir imagem em tamanho real](iteration-1-create-the-application-vb/_static/image50.png))

Precisamos atualizar a rota padrão no arquivo Global.asax para usar o controlador Contato em vez do controlador Home. Abra o arquivo Global.asax e modifique o controlador padrão usado pela rota padrão (consulte Lista 10).

**Listagem 10 - Global.asax.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

Depois de fazer essas alterações, o Gerenciador de Contatos será executado corretamente. Agora, ele usará a classe controlador a partir da classe controladora de contato como controlador padrão.

## <a name="summary"></a>Resumo

Nesta primeira iteração, criamos um aplicativo básico de Contact Manager da maneira mais rápida possível. Aproveitamos o Visual Studio para gerar o código inicial para nossos controladores e visualizações automaticamente. Também aproveitamos o Framework de entidades para gerar automaticamente nossas classes de modelo de banco de dados.

Atualmente, podemos listar, criar, editar e excluir registros de contato com o aplicativo Contact Manager. Em outras palavras, podemos executar todas as operações básicas de banco de dados exigidas por um aplicativo web orientado por banco de dados.

Infelizmente, nossa aplicação tem alguns problemas. Primeiro e hesito em admitir isso, o aplicativo Contact Manager não é o aplicativo mais atraente. Precisa de um trabalho de design. Na próxima iteração, veremos como podemos alterar a página-mestre de exibição padrão e a folha de estilo em cascata para melhorar a aparência do aplicativo.

Em segundo lugar, não implementamos nenhuma validação de formulário. Por exemplo, não há nada que o impeça de enviar o formulário de contato Criar sem inserir valores para qualquer um dos campos de formulário. Além disso, você pode inserir números de telefone inválidos e endereços de e-mail. Começamos a resolver o problema da validação da forma na #3 de iteração.

Finalmente, e o mais importante, a iteração atual do aplicativo Contact Manager não pode ser facilmente modificada ou mantida. Por exemplo, a lógica de acesso ao banco de dados é assada nas ações do controlador. Isso significa que não podemos modificar nosso código de acesso de dados sem modificar nossos controladores. Em iterações posteriores, exploramos padrões de design de software que podemos implementar para tornar o Contact Manager mais resistente às mudanças.

> [!div class="step-by-step"]
> [Próximo](iteration-7-add-ajax-functionality-cs.md)
> [anterior](iteration-2-make-the-application-look-nice-vb.md)
