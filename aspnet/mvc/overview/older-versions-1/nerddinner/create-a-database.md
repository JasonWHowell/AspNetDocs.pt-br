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
# <a name="create-a-database"></a><span data-ttu-id="d7375-103">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="d7375-103">Create a Database</span></span>

<span data-ttu-id="d7375-104">pela [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d7375-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d7375-105">Baixar PDF</span><span class="sxs-lookup"><span data-stu-id="d7375-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="d7375-106">Este é o passo 2 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="d7375-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="d7375-107">O passo 2 mostra os passos para criar o banco de dados que mantém todos os dados do jantar e rsvp para o nosso aplicativo NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="d7375-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="d7375-108">Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="d7375-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="d7375-109">NerdDinner Passo 2: Criando o Banco de Dados</span><span class="sxs-lookup"><span data-stu-id="d7375-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="d7375-110">Usaremos um banco de dados para armazenar todos os dados do Jantar e RSVP para o nosso aplicativo NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="d7375-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="d7375-111">As etapas abaixo mostram a criação do banco de dados usando a edição gratuita do SQL Server Express (que você pode facilmente instalar usando o V2 do [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d7375-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="d7375-112">Todo o código que vamos gravar funciona tanto com o SQL Server Express quanto com o SQL Server completo.</span><span class="sxs-lookup"><span data-stu-id="d7375-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="d7375-113">Criando um novo banco de dados SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="d7375-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="d7375-114">Começaremos clicando com o botão direito do mouse no nosso projeto web e, em seguida, selecionaro comando **'Adicionar-&gt;Novo item'** menu:</span><span class="sxs-lookup"><span data-stu-id="d7375-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="d7375-115">Isso trará à tona a caixa de diálogo "Adicionar novo item" do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7375-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="d7375-116">Filtraremos pela categoria "Dados" e selecionaremos o modelo de item "SQL Server Database":</span><span class="sxs-lookup"><span data-stu-id="d7375-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="d7375-117">Vamos nomear o banco de dados SQL Server Express que queremos criar "NerdDinner.mdf" e bater ok.</span><span class="sxs-lookup"><span data-stu-id="d7375-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="d7375-118">O Visual Studio nos perguntará se queremos adicionar\_esse arquivo ao nosso diretório \App Data (que é um diretório já configurado com ACLs de segurança de leitura e gravação):</span><span class="sxs-lookup"><span data-stu-id="d7375-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="d7375-119">Vamos clicar em "Sim" e nosso novo banco de dados será criado e adicionado ao nosso Solution Explorer:</span><span class="sxs-lookup"><span data-stu-id="d7375-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="d7375-120">Criando tabelas em nosso banco de dados</span><span class="sxs-lookup"><span data-stu-id="d7375-120">Creating Tables within our Database</span></span>

<span data-ttu-id="d7375-121">Agora temos um novo banco de dados vazio.</span><span class="sxs-lookup"><span data-stu-id="d7375-121">We now have a new empty database.</span></span> <span data-ttu-id="d7375-122">Vamos adicionar algumas tabelas a ele.</span><span class="sxs-lookup"><span data-stu-id="d7375-122">Let's add some tables to it.</span></span>

<span data-ttu-id="d7375-123">Para fazer isso, navegaremos até a janela de guia "Server Explorer" dentro do Visual Studio, que nos permite gerenciar bancos de dados e servidores.</span><span class="sxs-lookup"><span data-stu-id="d7375-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="d7375-124">Os bancos de dados SQL\_Server Express armazenados na pasta \App Data do nosso aplicativo aparecerão automaticamente dentro do Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7375-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="d7375-125">Podemos usar opcionalmente o ícone "Conectar ao banco de dados" na parte superior da janela "Server Explorer" para adicionar bancos de dados adicionais do SQL Server (local e remoto) à lista também:</span><span class="sxs-lookup"><span data-stu-id="d7375-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="d7375-126">Adicionaremos duas tabelas ao nosso banco de dados NerdDinner – uma para armazenar nossos jantares e outra para acompanhar as aceitações do RSVP a eles.</span><span class="sxs-lookup"><span data-stu-id="d7375-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="d7375-127">Podemos criar novas tabelas clicando com o botão direito do mouse na pasta "Tabelas" em nosso banco de dados e escolhendo o comando menu "Adicionar nova tabela":</span><span class="sxs-lookup"><span data-stu-id="d7375-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="d7375-128">Isso abrirá um designer de mesa que nos permite configurar o esquema da nossa tabela.</span><span class="sxs-lookup"><span data-stu-id="d7375-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="d7375-129">Para nossa tabela "Jantares", adicionaremos 10 colunas de dados:</span><span class="sxs-lookup"><span data-stu-id="d7375-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="d7375-130">Queremos que a coluna "DinnerID" seja uma chave primária única para a mesa.</span><span class="sxs-lookup"><span data-stu-id="d7375-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="d7375-131">Podemos configurá-lo clicando com o botão direito do mouse na coluna "DinnerID" e escolhendo o item do menu "Definir chave primária":</span><span class="sxs-lookup"><span data-stu-id="d7375-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="d7375-132">Além de fazer do DinnerID uma chave primária, também queremos configurá-la como uma coluna de "identidade" cujo valor é automaticamente incrementado à medida que novas linhas de dados são adicionadas à tabela (o que significa que a primeira linha de jantar inserida terá um DinnerID de 1, a segunda linha inserida terá um DinnerID de 2, etc).</span><span class="sxs-lookup"><span data-stu-id="d7375-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="d7375-133">Podemos fazer isso selecionando a coluna "DinnerID" e, em seguida, usar o editor "Propriedades da Coluna" para definir a propriedade "(É identidade)" na coluna como "Sim".</span><span class="sxs-lookup"><span data-stu-id="d7375-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="d7375-134">Usaremos os padrões de identidade padrão (início em 1 e incremento 1 em cada nova linha de Jantar):</span><span class="sxs-lookup"><span data-stu-id="d7375-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="d7375-135">Em seguida, salvaremos nossa tabela digitando Ctrl-S ou usando o comando **File-Save&gt;** menu.</span><span class="sxs-lookup"><span data-stu-id="d7375-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="d7375-136">Isso nos levará a nomear a mesa.</span><span class="sxs-lookup"><span data-stu-id="d7375-136">This will prompt us to name the table.</span></span> <span data-ttu-id="d7375-137">Vamos nomeá-lo "Jantares":</span><span class="sxs-lookup"><span data-stu-id="d7375-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="d7375-138">Nossa nova tabela dinners aparecerá em nosso banco de dados no explorador do servidor.</span><span class="sxs-lookup"><span data-stu-id="d7375-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="d7375-139">Em seguida, repetiremos as etapas acima e criaremos uma tabela "RSVP".</span><span class="sxs-lookup"><span data-stu-id="d7375-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="d7375-140">Esta tabela tem 3 colunas.</span><span class="sxs-lookup"><span data-stu-id="d7375-140">This table with have 3 columns.</span></span> <span data-ttu-id="d7375-141">Configuraremos a coluna RsvpID como a chave principal e também a tornaremos uma coluna de identidade:</span><span class="sxs-lookup"><span data-stu-id="d7375-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="d7375-142">Vamos salvá-lo e dar-lhe o nome "RSVP".</span><span class="sxs-lookup"><span data-stu-id="d7375-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="d7375-143">Configuração de uma relação de chave estrangeira entre tabelas</span><span class="sxs-lookup"><span data-stu-id="d7375-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="d7375-144">Agora temos duas tabelas em nosso banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d7375-144">We now have two tables within our database.</span></span> <span data-ttu-id="d7375-145">Nosso último passo de design de esquema será configurar uma relação "de um a muitos" entre essas duas tabelas – para que possamos associar cada linha de Jantar com zero ou mais linhas RSVP que se aplicam a ela.</span><span class="sxs-lookup"><span data-stu-id="d7375-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="d7375-146">Faremos isso configurando a coluna "DinnerID" da mesa RSVP para ter uma relação de tecla estrangeira com a coluna "DinnerID" na mesa "Jantares".</span><span class="sxs-lookup"><span data-stu-id="d7375-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="d7375-147">Para fazer isso, abriremos a tabela RSVP dentro do designer de tabela, clicando duas vezes no explorador do servidor.</span><span class="sxs-lookup"><span data-stu-id="d7375-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="d7375-148">Em seguida, selecionaremos a coluna "DinnerID" dentro dele, clique com o botão direito do mouse e escolha as "Relações..." comando menu de contexto:</span><span class="sxs-lookup"><span data-stu-id="d7375-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="d7375-149">Isso trará um diálogo que podemos usar para configurar relações entre tabelas:</span><span class="sxs-lookup"><span data-stu-id="d7375-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="d7375-150">Vamos clicar no botão "Adicionar" para adicionar uma nova relação à caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7375-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="d7375-151">Uma vez que um relacionamento tenha sido adicionado, expandiremos o nó de exibição de árvore "Tabelas e Especificação de Coluna" dentro da grade de propriedade à direita da caixa de diálogo e, em seguida, clicaremos no "..." botão à direita dele:</span><span class="sxs-lookup"><span data-stu-id="d7375-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="d7375-152">Clicando no "..." o botão trará outro diálogo que nos permite especificar quais tabelas e colunas estão envolvidas no relacionamento, bem como nos permitir nomear o relacionamento.</span><span class="sxs-lookup"><span data-stu-id="d7375-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="d7375-153">Mudaremos a Mesa-Chave Principal para ser "Jantares", e selecionaremos a coluna "DinnerID" dentro da mesa Dinners como a chave principal.</span><span class="sxs-lookup"><span data-stu-id="d7375-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="d7375-154">Nossa tabela RSVP será a tabela de chaves estrangeiras, e o RSVP. A coluna DinnerID será associada como a chave estrangeira:</span><span class="sxs-lookup"><span data-stu-id="d7375-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="d7375-155">Agora, cada linha na tabela RSVP será associada a uma linha na tabela Jantar.</span><span class="sxs-lookup"><span data-stu-id="d7375-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="d7375-156">O SQL Server manterá a integridade referencial para nós – e nos impedirá de adicionar uma nova linha RSVP se não apontar para uma linha de jantar válida.</span><span class="sxs-lookup"><span data-stu-id="d7375-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="d7375-157">Também nos impedirá de excluir uma linha de jantar se ainda houver linhas RSVP referentes a ela.</span><span class="sxs-lookup"><span data-stu-id="d7375-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="d7375-158">Adicionando dados às nossas tabelas</span><span class="sxs-lookup"><span data-stu-id="d7375-158">Adding Data to our Tables</span></span>

<span data-ttu-id="d7375-159">Vamos terminar adicionando alguns dados de amostra à nossa tabela jantares.</span><span class="sxs-lookup"><span data-stu-id="d7375-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="d7375-160">Podemos adicionar dados a uma tabela clicando com o botão direito do mouse sobre ele no Server Explorer e escolhendo o comando "Mostrar dados da tabela":</span><span class="sxs-lookup"><span data-stu-id="d7375-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="d7375-161">Adicionaremos algumas linhas de dados do Jantar que podemos usar mais tarde quando começarmos a implementar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d7375-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="d7375-162">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="d7375-162">Next Step</span></span>

<span data-ttu-id="d7375-163">Acabamos de criar nosso banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d7375-163">We've finished creating our database.</span></span> <span data-ttu-id="d7375-164">Vamos agora criar classes de modelo que podemos usar para consultar e atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="d7375-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d7375-165">[Próximo](create-a-new-aspnet-mvc-project.md)
> [anterior](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="d7375-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
