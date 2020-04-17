---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Criar um banco de dados | Microsoft Docs
author: rick-anderson
description: O passo 2 mostra os passos para criar o banco de dados que mantém todos os dados do jantar e rsvp para o nosso aplicativo NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541605"
---
# <a name="create-a-database"></a>Criar um banco de dados

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 2 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O passo 2 mostra os passos para criar o banco de dados que mantém todos os dados do jantar e rsvp para o nosso aplicativo NerdDinner.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner Passo 2: Criando o Banco de Dados

Usaremos um banco de dados para armazenar todos os dados do Jantar e RSVP para o nosso aplicativo NerdDinner.

As etapas abaixo mostram a criação do banco de dados usando a edição gratuita do SQL Server Express (que você pode facilmente instalar usando o V2 do [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)). Todo o código que vamos gravar funciona tanto com o SQL Server Express quanto com o SQL Server completo.

### <a name="creating-a-new-sql-server-express-database"></a>Criando um novo banco de dados SQL Server Express

Começaremos clicando com o botão direito do mouse no nosso projeto web e, em seguida, selecionaro comando **'Adicionar-&gt;Novo item'** menu:

![](create-a-database/_static/image1.png)

Isso trará à tona a caixa de diálogo "Adicionar novo item" do Visual Studio. Filtraremos pela categoria "Dados" e selecionaremos o modelo de item "SQL Server Database":

![](create-a-database/_static/image2.png)

Vamos nomear o banco de dados SQL Server Express que queremos criar "NerdDinner.mdf" e bater ok. O Visual Studio nos perguntará se queremos adicionar\_esse arquivo ao nosso diretório \App Data (que é um diretório já configurado com ACLs de segurança de leitura e gravação):

![](create-a-database/_static/image3.png)

Vamos clicar em "Sim" e nosso novo banco de dados será criado e adicionado ao nosso Solution Explorer:

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>Criando tabelas em nosso banco de dados

Agora temos um novo banco de dados vazio. Vamos adicionar algumas tabelas a ele.

Para fazer isso, navegaremos até a janela de guia "Server Explorer" dentro do Visual Studio, que nos permite gerenciar bancos de dados e servidores. Os bancos de dados SQL\_Server Express armazenados na pasta \App Data do nosso aplicativo aparecerão automaticamente dentro do Server Explorer. Podemos usar opcionalmente o ícone "Conectar ao banco de dados" na parte superior da janela "Server Explorer" para adicionar bancos de dados adicionais do SQL Server (local e remoto) à lista também:

![](create-a-database/_static/image5.png)

Adicionaremos duas tabelas ao nosso banco de dados NerdDinner – uma para armazenar nossos jantares e outra para acompanhar as aceitações do RSVP a eles. Podemos criar novas tabelas clicando com o botão direito do mouse na pasta "Tabelas" em nosso banco de dados e escolhendo o comando menu "Adicionar nova tabela":

![](create-a-database/_static/image6.png)

Isso abrirá um designer de mesa que nos permite configurar o esquema da nossa tabela. Para nossa tabela "Jantares", adicionaremos 10 colunas de dados:

![](create-a-database/_static/image7.png)

Queremos que a coluna "DinnerID" seja uma chave primária única para a mesa. Podemos configurá-lo clicando com o botão direito do mouse na coluna "DinnerID" e escolhendo o item do menu "Definir chave primária":

![](create-a-database/_static/image8.png)

Além de fazer do DinnerID uma chave primária, também queremos configurá-la como uma coluna de "identidade" cujo valor é automaticamente incrementado à medida que novas linhas de dados são adicionadas à tabela (o que significa que a primeira linha de jantar inserida terá um DinnerID de 1, a segunda linha inserida terá um DinnerID de 2, etc).

Podemos fazer isso selecionando a coluna "DinnerID" e, em seguida, usar o editor "Propriedades da Coluna" para definir a propriedade "(É identidade)" na coluna como "Sim". Usaremos os padrões de identidade padrão (início em 1 e incremento 1 em cada nova linha de Jantar):

![](create-a-database/_static/image9.png)

Em seguida, salvaremos nossa tabela digitando Ctrl-S ou usando o comando **File-Save&gt;** menu. Isso nos levará a nomear a mesa. Vamos nomeá-lo "Jantares":

![](create-a-database/_static/image10.png)

Nossa nova tabela dinners aparecerá em nosso banco de dados no explorador do servidor.

Em seguida, repetiremos as etapas acima e criaremos uma tabela "RSVP". Esta tabela tem 3 colunas. Configuraremos a coluna RsvpID como a chave principal e também a tornaremos uma coluna de identidade:

![](create-a-database/_static/image11.png)

Vamos salvá-lo e dar-lhe o nome "RSVP".

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>Configuração de uma relação de chave estrangeira entre tabelas

Agora temos duas tabelas em nosso banco de dados. Nosso último passo de design de esquema será configurar uma relação "de um a muitos" entre essas duas tabelas – para que possamos associar cada linha de Jantar com zero ou mais linhas RSVP que se aplicam a ela. Faremos isso configurando a coluna "DinnerID" da mesa RSVP para ter uma relação de tecla estrangeira com a coluna "DinnerID" na mesa "Jantares".

Para fazer isso, abriremos a tabela RSVP dentro do designer de tabela, clicando duas vezes no explorador do servidor. Em seguida, selecionaremos a coluna "DinnerID" dentro dele, clique com o botão direito do mouse e escolha as "Relações..." comando menu de contexto:

![](create-a-database/_static/image12.png)

Isso trará um diálogo que podemos usar para configurar relações entre tabelas:

![](create-a-database/_static/image13.png)

Vamos clicar no botão "Adicionar" para adicionar uma nova relação à caixa de diálogo. Uma vez que um relacionamento tenha sido adicionado, expandiremos o nó de exibição de árvore "Tabelas e Especificação de Coluna" dentro da grade de propriedade à direita da caixa de diálogo e, em seguida, clicaremos no "..." botão à direita dele:

![](create-a-database/_static/image14.png)

Clicando no "..." o botão trará outro diálogo que nos permite especificar quais tabelas e colunas estão envolvidas no relacionamento, bem como nos permitir nomear o relacionamento.

Mudaremos a Mesa-Chave Principal para ser "Jantares", e selecionaremos a coluna "DinnerID" dentro da mesa Dinners como a chave principal. Nossa tabela RSVP será a tabela de chaves estrangeiras, e o RSVP. A coluna DinnerID será associada como a chave estrangeira:

![](create-a-database/_static/image15.png)

Agora, cada linha na tabela RSVP será associada a uma linha na tabela Jantar. O SQL Server manterá a integridade referencial para nós – e nos impedirá de adicionar uma nova linha RSVP se não apontar para uma linha de jantar válida. Também nos impedirá de excluir uma linha de jantar se ainda houver linhas RSVP referentes a ela.

### <a name="adding-data-to-our-tables"></a>Adicionando dados às nossas tabelas

Vamos terminar adicionando alguns dados de amostra à nossa tabela jantares. Podemos adicionar dados a uma tabela clicando com o botão direito do mouse sobre ele no Server Explorer e escolhendo o comando "Mostrar dados da tabela":

![](create-a-database/_static/image16.png)

Adicionaremos algumas linhas de dados do Jantar que podemos usar mais tarde quando começarmos a implementar o aplicativo:

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>Próxima etapa

Acabamos de criar nosso banco de dados. Vamos agora criar classes de modelo que podemos usar para consultar e atualizá-lo.

> [!div class="step-by-step"]
> [Próximo](create-a-new-aspnet-mvc-project.md)
> [anterior](build-a-model-with-business-rule-validations.md)
