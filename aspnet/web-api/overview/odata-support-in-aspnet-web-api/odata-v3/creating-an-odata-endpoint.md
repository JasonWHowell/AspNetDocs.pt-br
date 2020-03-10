---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Criando um ponto de extremidade OData v3 com a API Web 2 | Microsoft Docs
author: MikeWasson
description: O Protocolo Open Data (OData) é um protocolo de acesso a dados para a Web. O OData fornece uma maneira uniforme de estruturar dados, consultar os dados e manipular os dados...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556409"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>Criando um ponto de extremidade OData v3 com a API Web 2

por [Mike Wasson](https://github.com/MikeWasson)

[Baixar projeto concluído](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> O [protocolo Open Data](http://www.odata.org/) (OData) é um protocolo de acesso a dados para a Web. O OData fornece uma maneira uniforme de estruturar dados, consultar os dados e manipular o conjunto de dados por meio de operações CRUD (criar, ler, atualizar e excluir). O OData dá suporte aos formatos AtomPub (XML) e JSON. O OData também define uma maneira de expor metadados sobre os dados. Os clientes podem usar os metadados para descobrir as informações de tipo e as relações para o conjunto de dados.
>
> ASP.NET Web API facilita a criação de um ponto de extremidade OData para um conjunto de dados. Você pode controlar exatamente a quais operações OData o ponto de extremidade dá suporte. Você pode hospedar vários pontos de extremidade OData, juntamente com pontos de extremidade não-OData. Você tem controle total sobre o modelo de dados, a lógica de negócios de back-end e a camada de dados.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Versões de software usadas no tutorial
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - API Web 2
> - Versão 3 do OData
> - Entity Framework 6
> - [Proxy de depuração da Web do Fiddler (opcional)](http://www.fiddler2.com)
>
> O suporte a API Web OData foi adicionado na [atualização do ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650). No entanto, este tutorial usa scaffolding que foi adicionado no Visual Studio 2013.

Neste tutorial, você criará um ponto de extremidade OData simples que os clientes podem consultar. Você também criará um C# cliente para o ponto de extremidade. Depois de concluir este tutorial, o próximo conjunto de tutoriais mostra como adicionar mais funcionalidade, incluindo relações de entidade, ações e $expand/$select.

- [Criar o projeto do Visual Studio](#create-project)
- [Adicionar um modelo de entidade](#add-model)
- [Adicionar um controlador OData](#add-controller)
- [Adicionar o EDM e a rota](#edm)
- [Propagar o banco de dados (opcional)](#seed-db)
- [Explorando o ponto de extremidade OData](#explore)
- [Formatos de serialização OData](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>Criar o projeto do Visual Studio

Neste tutorial, você criará um ponto de extremidade OData que dá suporte a operações CRUD básicas. O ponto de extremidade vai expor um único recurso, uma lista de produtos. Os tutoriais posteriores adicionarão mais recursos.

Inicie o Visual Studio e selecione **novo projeto** na página inicial. Ou, no menu **arquivo** , selecione **novo** e **projeto**.

No painel **modelos** , selecione **modelos instalados** e expanda o nó C# Visual. Em **Visual C#** , selecione **Web**. Selecione **o modelo de aplicativo Web ASP.net** .

![](creating-an-odata-endpoint/_static/image1.png)

Na caixa de diálogo **novo projeto ASP.net** , selecione o modelo **vazio** . Em &quot;adicionar pastas e referências principais para...&quot;, verifique a **API Web**. Clique em **OK**.

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>Adicionar um modelo de entidade

Um *modelo* é um objeto que representa os dados no seu aplicativo. Para este tutorial, precisamos de um modelo que represente um produto. O modelo corresponde ao nosso tipo de entidade OData.

No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Modelos. No menu de contexto, selecione **Adicionar** e, em seguida, selecione **Classe**.

![](creating-an-odata-endpoint/_static/image3.png)

Na caixa de diálogo **Adicionar novo** item, nomeie a classe &quot;produto&quot;.

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> Por convenção, as classes de modelo são colocadas na pasta modelos. Você não precisa seguir essa convenção em seus próprios projetos, mas vamos usá-la para este tutorial.

No arquivo Product.cs, adicione a seguinte definição de classe:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

A propriedade ID será a chave de entidade. Os clientes podem consultar produtos por ID. Esse campo também seria a chave primária no banco de dados back-end.

Compile o projeto agora. Na próxima etapa, usaremos algumas scaffolding do Visual Studio que usam a reflexão para localizar o tipo de produto.

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>Adicionar um controlador OData

Um *controlador* é uma classe que MANIPULA solicitações HTTP. Você define um controlador separado para cada conjunto de entidades no serviço OData. Neste tutorial, criaremos um único controlador.

Em Gerenciador de Soluções, clique com o botão direito do mouse na pasta controladores. Selecione **Adicionar** e, em seguida, selecione **Controlador**.

![](creating-an-odata-endpoint/_static/image5.png)

Na caixa de diálogo **Adicionar Scaffold** , selecione &quot;controlador ODATA da API Web 2 com ações, usando Entity Framework&quot;.

![](creating-an-odata-endpoint/_static/image6.png)

Na caixa de diálogo **Adicionar controlador** , nomeie o controlador "ProductsController". Marque a caixa de seleção &quot;usar ações do controlador assíncrono&quot;. Na lista suspensa **modelo** , selecione a classe produto.

![](creating-an-odata-endpoint/_static/image7.png)

Clique no botão **novo contexto de dados...** . Deixe o nome padrão para o tipo de contexto de dados e clique em **Adicionar**.

![](creating-an-odata-endpoint/_static/image8.png)

Clique em Adicionar na caixa de diálogo Adicionar controlador para adicionar o controlador.

![](creating-an-odata-endpoint/_static/image9.png)

Observação: se você receber uma mensagem de erro dizendo &quot;ocorreu um erro ao obter o tipo...&quot;, certifique-se de ter criado o projeto do Visual Studio depois de adicionar a classe Product. O scaffolding usa a reflexão para encontrar a classe.

![](creating-an-odata-endpoint/_static/image10.png)

O scaffolding adiciona dois arquivos de código ao projeto:

- Products.cs define o controlador da API Web que implementa o ponto de extremidade OData.
- O ProductServiceContext.cs fornece métodos para consultar o banco de dados subjacente, usando Entity Framework.

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>Adicionar o EDM e a rota

Em Gerenciador de Soluções, expanda a pasta\_iniciar o aplicativo e abra o arquivo chamado WebApiConfig.cs. Essa classe contém o código de configuração para a API da Web. Substitua este código pelo seguinte:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

Esse código faz duas coisas:

- Cria um Modelo de Dados de Entidade (EDM) para o ponto de extremidade OData.
- Adiciona uma rota para o ponto de extremidade.

Um EDM é um modelo abstrato dos dados. O EDM é usado para criar o documento de metadados e definir os URIs para o serviço. O **ODataConventionModelBuilder** cria um EDM usando um conjunto de convenções de nomenclatura padrão EDM. Essa abordagem requer o mínimo de código. Se você quiser mais controle sobre o EDM, poderá usar a classe **ODataModelBuilder** para criar o EDM adicionando Propriedades, chaves e propriedades de navegação explicitamente.

O método **EntitySet** adiciona um conjunto de entidades ao EDM:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

A cadeia de caracteres "Products" define o nome do conjunto de entidades. O nome do controlador deve corresponder ao nome do conjunto de entidades. Neste tutorial, o conjunto de entidades é chamado de "produtos" e o controlador é nomeado `ProductsController`. Se você tiver nomeado o conjunto de entidades "ProductSet", você nomearia o controlador `ProductSetController`. Observe que um ponto de extremidade pode ter vários conjuntos de entidades. Chame **EntitySet&lt;t&gt;** para cada conjunto de entidades e, em seguida, defina um controlador correspondente.

O método **MapODataRoute** adiciona uma rota para o ponto de extremidade OData.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

O primeiro parâmetro é um nome amigável para a rota. Os clientes do seu serviço não veem esse nome. O segundo parâmetro é o prefixo de URI para o ponto de extremidade. Dado esse código, o URI para o conjunto de entidades Products é http://<em>hostname</em>/OData/Products. Seu aplicativo pode ter mais de um ponto de extremidade OData. Para cada ponto de extremidade, chame <strong>MapODataRoute</strong> e forneça um nome de rota exclusivo e um prefixo URI exclusivo.

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>Propagar o banco de dados (opcional)

Nesta etapa, você usará Entity Framework para propagar o banco de dados com algum dado de teste. Esta etapa é opcional, mas permite testar seu ponto de extremidade OData imediatamente.

No menu **ferramentas** , selecione **Gerenciador de pacotes NuGet**e, em seguida, selecione **console do Gerenciador de pacotes**. Na janela Console do Gerenciador de Pacotes, digite o seguinte comando:

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

Isso adiciona uma pasta chamada migrações e um arquivo de código chamado Configuration.cs.

![](creating-an-odata-endpoint/_static/image12.png)

Abra esse arquivo e adicione o código a seguir ao método `Configuration.Seed`.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

Na janela do console do Gerenciador de pacotes, digite os seguintes comandos:

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

Esses comandos geram código que cria o banco de dados e, em seguida, executa esse código.

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>Explorando o ponto de extremidade OData

Nesta seção, usaremos o [proxy de depuração da Web do Fiddler](http://www.fiddler2.com) para enviar solicitações ao ponto de extremidade e examinar as mensagens de resposta. Isso ajudará você a entender os recursos de um ponto de extremidade OData.

No Visual Studio, pressione F5 para iniciar a depuração. Por padrão, o Visual Studio abre o navegador para `http://localhost:*port*`, em que *porta* é o número da porta configurado nas configurações do projeto.

Você pode alterar o número da porta nas configurações do projeto. Em Gerenciador de Soluções, clique com o botão direito do mouse no projeto e selecione **Propriedades**. Na janela Propriedades, selecione **Web**. Insira o número da porta na **URL do projeto**.

### <a name="service-document"></a>Documento de serviço

O *documento de serviço* contém uma lista dos conjuntos de entidades para o ponto de extremidade OData. Para obter o documento de serviço, envie uma solicitação GET para o URI raiz do serviço.

Usando o Fiddler, insira o seguinte URI na guia **compositor** : `http://localhost:port/odata/`, em que *Port* é o número da porta.

![](creating-an-odata-endpoint/_static/image13.png)

Clique no botão **Executar** . O Fiddler envia uma solicitação HTTP GET para seu aplicativo. Você deve ver a resposta na lista de sessões da Web. Se tudo estiver funcionando, o código de status será 200.

![](creating-an-odata-endpoint/_static/image14.png)

Clique duas vezes na resposta na lista sessões da Web para ver os detalhes da mensagem de resposta na guia inspetores.

![](creating-an-odata-endpoint/_static/image15.png)

A mensagem de resposta HTTP bruta deve ser semelhante ao seguinte:

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

Por padrão, a API da Web retorna o documento de serviço no formato AtomPub. Para solicitar o JSON, adicione o seguinte cabeçalho à solicitação HTTP:

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

Agora, a resposta HTTP contém uma carga JSON:

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>Documento de metadados de serviço

O *documento de metadados de serviço* descreve o modelo de dados do serviço, usando uma linguagem XML chamada de CSDL (linguagem de definição de esquema conceitual). O documento de metadados mostra a estrutura dos dados no serviço e pode ser usado para gerar o código do cliente.

Para obter o documento de metadados, envie uma solicitação GET para `http://localhost:port/odata/$metadata`. Aqui estão os metadados para o ponto de extremidade mostrado neste tutorial.

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>Conjunto de entidades

Para obter o conjunto de entidades de produtos, envie uma solicitação GET para `http://localhost:port/odata/Products`.

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>Entidade

Para obter um produto individual, envie uma solicitação GET para `http://localhost:port/odata/Products(1)`, onde "1" é a ID do produto.

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>Formatos de serialização OData

O OData dá suporte a vários formatos de serialização:

- Pub (XML) Atom
- JSON "Light" (introduzido no OData v3)
- JSON "detalhado" (OData v2)

Por padrão, a API Web usa o formato "Light" de AtomPubJSON.

Para obter o formato AtomPub, defina o cabeçalho Accept como "Application/Atom + XML". Aqui está um exemplo de corpo de resposta:

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

Você pode ver uma desvantagem óbvia do formato Atom: é muito mais detalhado do que a luz JSON. No entanto, se você tiver um cliente que entenda AtomPub, o cliente poderá preferir esse formato em JSON.

Esta é a versão clara do JSON da mesma entidade:

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

O formato JSON Light foi introduzido na versão 3 do protocolo OData. Para compatibilidade com versões anteriores, um cliente pode solicitar o formato JSON "detalhado" mais antigo. Para solicitar o JSON detalhado, defina o cabeçalho Accept como `application/json;odata=verbose`. Esta é a versão detalhada:

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

Esse formato transmite mais metadados no corpo da resposta, o que pode adicionar uma sobrecarga considerável em uma sessão inteira. Além disso, ele adiciona um nível de indireção encapsulando o objeto em uma propriedade chamada "d".

## <a name="next-steps"></a>Próximas etapas

- [Adicionar relações de entidade](working-with-entity-relations.md)
- [Adicionar ações OData](odata-actions.md)
- [Chamar o serviço OData de um cliente .NET](calling-an-odata-service-from-a-net-client.md)
