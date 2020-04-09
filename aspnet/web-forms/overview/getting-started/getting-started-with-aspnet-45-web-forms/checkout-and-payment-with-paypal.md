---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: Checkout e Pagamento com PayPal | Microsoft Docs
author: Erikre
description: Esta série tutorial ensinará o básico de construir um aplicativo ASP.NET Web Forms usando ASP.NET 4.5 e Microsoft Visual Studio Express 2013 para Nós...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676051"
---
# <a name="checkout-and-payment-with-paypal"></a>Check-out e pagamento com o PayPal

por [Erik Reitan](https://github.com/Erikre)

[Baixe Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) ou [Baixe e-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Esta série tutorial ensinará o básico de construir um aplicativo ASP.NET Formulários web usando ASP.NET 4.5 e Microsoft Visual Studio Express 2013 para web. Um projeto visual studio 2013 [com código fonte C#](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) está disponível para acompanhar esta série tutorial.

Este tutorial descreve como modificar o aplicativo de amostra Wingtip Toys para incluir a autorização do usuário, o registro e o pagamento usando o PayPal. Somente os usuários que estiverem logadoterão autorização para comprar produtos. A funcionalidade de registro de usuário incorporada do ASP.NET 4.5 Web Forms já inclui muito do que você precisa. Você adicionará a funcionalidade do PayPal Express Checkout. Neste tutorial você está usando o ambiente de testes de desenvolvedores do PayPal, para que nenhum fundo real seja transferido. No final do tutorial, você testará o aplicativo selecionando produtos para adicionar ao carrinho de compras, clicando no botão de checkout e transferindo dados para o site de testes do PayPal. No site de testes do PayPal, você confirmará suas informações de envio e pagamento e, em seguida, retornará ao aplicativo de amostra local Wingtip Toys para confirmar e concluir a compra.

Existem vários processadores de pagamento de terceiros experientes que se especializam em compras online que abordam escalabilidade e segurança. ASP.NET os desenvolvedores devem considerar as vantagens de utilizar uma solução de pagamento de terceiros antes de implementar uma solução de compras e compras.

> [!NOTE] 
> 
> O aplicativo de amostra Wingtip Toys foi projetado para mostrar conceitos e recursos específicos ASP.NET disponíveis para ASP.NET desenvolvedores web. Esta aplicação amostral não foi otimizada para todas as circunstâncias possíveis em relação à escalabilidade e segurança.

## <a name="what-youll-learn"></a>O que você aprenderá:

- Como restringir o acesso a páginas específicas em uma pasta.
- Como criar um carrinho de compras conhecido a partir de um carrinho de compras anônimo.
- Como ativar o SSL para o projeto.
- Como adicionar um provedor OAuth ao projeto.
- Como usar o PayPal para comprar produtos usando o ambiente de testes paypal.
- Como exibir detalhes do PayPal em um controle **DetailsView.**
- Como atualizar o banco de dados do aplicativo Wingtip Toys com detalhes obtidos do PayPal.

## <a name="adding-order-tracking"></a>Adicionando rastreamento de pedidos

Neste tutorial, você criará duas novas classes para rastrear dados da ordem que um usuário criou. As aulas acompanharão os dados referentes às informações de envio, total de compras e confirmação de pagamento.

### <a name="add-the-order-and-orderdetail-model-classes"></a>Adicione as classes de modelo de ordem e pedido

No início desta série tutorial, você definiu o esquema para categorias, produtos e `Category` `Product`itens `CartItem` de carrinho de compras, criando a , e classes na pasta *Models.* Agora você adicionará duas novas classes para definir o esquema para a ordem do produto e os detalhes do pedido.

1. Na pasta **Modelos,** adicione uma nova classe chamada *Order.cs*.   
   O novo arquivo de classe é exibido no editor.
2. Substitua o código padrão pelo seguinte:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. Adicione uma classe *OrderDetail.cs* à pasta *Modelos.*
4. Substitua o código padrão pelo código a seguir:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

As `Order` `OrderDetail` classes e as classes contêm o esquema para definir as informações de ordem utilizadas para compra e expedição.

Além disso, você precisará atualizar a classe de contexto do banco de dados que gerencia as classes da entidade e que fornece acesso de dados ao banco de dados. Para fazer isso, você adicionará as `OrderDetail` classes `ProductContext` de ordem e modelo recém-criadas à classe.

1. No **Solution Explorer,** encontre e abra o arquivo *ProductContext.cs.*
2. Adicione o código destacado ao arquivo *ProductContext.cs* como mostrado abaixo:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

Como mencionado anteriormente nesta série tutorial, *ProductContext.cs* o código `System.Data.Entity` no arquivo ProductContext.cs adiciona o namespace para que você tenha acesso a todas as funcionalidades principais do Framework entity. Essa funcionalidade inclui a capacidade de consultar, inserir, atualizar e excluir dados trabalhando com objetos fortemente digitados. O código acima `ProductContext` na classe adiciona acesso `Order` do `OrderDetail` Entity Framework às classes e séries recém-adicionadas.

## <a name="adding-checkout-access"></a>Adicionando acesso de checkout

O aplicativo de exemplo Wingtip Toys permite que usuários anônimos revisem e adicionem produtos a um carrinho de compras. No entanto, quando os usuários anônimos optam por comprar os produtos que adicionaram ao carrinho de compras, eles devem fazer logon no site. Uma vez conectados, eles podem acessar as páginas restritas do aplicativo Web que lidam com o processo de checkout e compra. Essas páginas restritas estão contidas na pasta *Checkout* do aplicativo.

### <a name="add-a-checkout-folder-and-pages"></a>Adicione uma pasta de checkout e páginas

Agora você criará a pasta *Checkout* e as páginas nela que o cliente verá durante o processo de checkout. Você atualizará essas páginas mais tarde neste tutorial.

1. Clique com o botão direito do mouse no nome do projeto **(Wingtip Toys)** no **Solution Explorer** e **selecione Adicionar uma nova pasta**. 

    ![Checkout e Pagamento com PayPal - Nova Pasta](checkout-and-payment-with-paypal/_static/image1.png)
2. Nomeie a nova pasta *Checkout*.
3. Clique com o botão direito do mouse na pasta *Checkout* e selecione **Adicionar**-&gt;**novo item**. 

    ![Checkout e Pagamento com PayPal - Novo Item](checkout-and-payment-with-paypal/_static/image2.png)
4. A caixa de diálogo **Adicionar novo item** é exibida.
5. Selecione o grupo de modelos **da Web** **Visual C#**  - &gt; à esquerda. Em seguida, a partir do painel do meio, selecione **Formulário da Web com página mestre**e nomeie-o *CheckoutStart.aspx*. 

    ![Checkout e Pagamento com PayPal - Adicionar diálogo de novos itens](checkout-and-payment-with-paypal/_static/image3.png)
6. Como antes, selecione o arquivo *Site.Master* como a página mestre.
7. Adicione as seguintes páginas adicionais à pasta *Checkout* usando as mesmas etapas acima:   

    - CheckoutReview.aspx
    - CheckoutComplete.aspx
    - CheckoutCancel.aspx
    - CheckoutError.aspx

### <a name="add-a-webconfig-file"></a>Adicionar um arquivo Web.config

Adicionando um novo arquivo *Web.config* à pasta *Checkout,* você poderá restringir o acesso a todas as páginas contidas na pasta.

1. Clique com o botão direito do mouse na pasta *Checkout* e **selecione Adicionar**  - &gt; **novo item**.  
   A caixa de diálogo **Adicionar novo item** é exibida.
2. Selecione o grupo de modelos **da Web** **Visual C#**  - &gt; à esquerda. Em seguida, a partir do painel do meio, selecione **Arquivo de configuração da Web,** aceite o nome padrão de *Web.config*e, em seguida, **selecione Adicionar**.
3. Substitua o conteúdo XML existente no arquivo *Web.config* pelo seguinte:  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. Salvar o arquivo *Web.config*.

O arquivo *Web.config* especifica que todos os usuários desconhecidos do aplicativo Web devem ser negados acesso às páginas contidas na pasta *Checkout.* No entanto, se o usuário tiver registrado uma conta e estiver conectado, ele será um usuário conhecido e terá acesso às páginas da pasta *Checkout.*

É importante notar que ASP.NET configuração segue uma hierarquia, onde cada arquivo *Web.config* aplica configurações à pasta em que está e a todos os diretórios infantis abaixo dele.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>Habilitar SSL para o projeto

 SSL é um protocolo que permite que os servidores Web e clientes Web se comuniquem de modo mais seguro, por meio de criptografia. Quando o SSL não é utilizado, os dados enviados entre o cliente e servidor ficam abertos à detecção de pacotes por qualquer um com acesso físico à rede. Adicionalmente, diversos esquemas comuns de autenticação não são seguros por HTTP puro. Em particular, a autenticação Básica e a autenticação de formulários enviam credenciais sem criptografia. Para serem seguros, esses esquemas de autenticação precisam utilizar SSL. 

1. No **Solution Explorer,** clique no projeto **WingtipToys** e pressione **F4** para exibir a janela **Propriedades.**
2. Alterar **SSL** ativado `true`para .
3. Copie a **URL do SSL** , de modo que você possa utilizá-la mais tarde.   
 A URL SSL `https://localhost:44300/` será a menos que você tenha criado sites SSL anteriormente (como mostrado abaixo).   
    ![Propriedades de projeto](checkout-and-payment-with-paypal/_static/image4.png)
4. No **Solution Explorer,** clique com o botão direito do mouse no projeto **WingtipToys** e clique **em Propriedades**.
5. Na guia à esquerda, clique em **Web**.
6. Alterar a URL do **projeto** para usar a **URL SSL** que você salvou anteriormente.   
    ![Propriedades da Web do Projeto](checkout-and-payment-with-paypal/_static/image5.png)
7. Salve a página pressionando **CTRL+S**.
8. Pressione **Ctrl+F5** para executar o aplicativo. O Visual Studio exibirá uma opção para que você possa evitar avisos do SSL.
9. Clique em **Sim** para confiar no certificado SSL IIS Express e continuar.   
    ![Detalhes do certificado SSL do IIS Express](checkout-and-payment-with-paypal/_static/image6.png)  
  Será exibido um aviso de segurança.
10. Clique em **Sim** para instalar o certificado em seu localhost.   
    ![Caixa de diálogo Aviso de Segurança](checkout-and-payment-with-paypal/_static/image7.png)  
  A janela do navegador será exibida.

Agora você pode testar facilmente seu aplicativo web localmente usando SSL.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>Adicionar um provedor de OAuth 2.0

Os Web Forms ASP.NET oferecem opções aprimoradas de associação e autenticação. Esses aprimoramentos incluem OAuth. O OAuth é um protocolo aberto que permite autorização segura em um método simples e padrão da web, aplicativos móveis e de área de trabalho. O modelo ASP.NET Web Forms usa o OAuth para expor o Facebook, o Twitter, o Google e a Microsoft como provedores de autenticação. Embora este tutorial use apenas o Google como o provedor de autenticação, você pode facilmente modificar o código para usar qualquer um dos provedores. As etapas para implementar outros provedores são muito semelhantes às etapas que você verá neste tutorial.

Além da autenticação, o tutorial também usará funções para implementar a autorização. Somente os usuários que você adicionar à função `canEdit` poderão alterar dados (criar, editar ou excluir contatos).

> [!NOTE] 
> 
> Os aplicativos windows live só aceitam uma URL ao vivo para um site em funcionamento, então você não pode usar uma URL de site local para testar logins.

As etapas a seguir permitirão que você adicione um provedor de autenticação do Google.

1. Abra o *arquivo Start\Startup.Auth.cs\_* do app start\.
2. Remove os caracteres do comentário do método para que o método `app.UseGoogleAuthentication()` pareça-se cm o seguinte: 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. Navegue até o [Console Para Desenvolvedores do Google](https://console.developers.google.com/). Você também precisará se autenticar com sua conta de email de desenvolvedor do Google (gmail.com). Se você não tiver uma conta do Google, selecione o link **Criar uma conta** .   
   Em seguida, você verá o **Console de desenvolvedores do Google**.   
    ![Console Para Desenvolvedores do Google](checkout-and-payment-with-paypal/_static/image8.png)
4. Clique no botão **Criar projeto** e digite um nome de projeto e ID (você pode usar os valores padrão). Em seguida, clique na **caixa de seleção de acordo** e no botão **Criar.**  

    ![Google - Novo Projeto](checkout-and-payment-with-paypal/_static/image9.png)

    Em poucos segundos o novo projeto será criado e o navegador exibirá a nova página de projetos.
5. Na guia esquerda, clique em **APIs &amp; auth**e clique em **Credenciais**.
6. Clique em **Criar novo ID do cliente** em **OAuth**.   
   A caixa de diálogo **Criar ID de Cliente** será exibida.   
    ![Google - Criar ID de Cliente](checkout-and-payment-with-paypal/_static/image10.png)
7. Na caixa de diálogo **Criar ID do cliente,** mantenha o **aplicativo Web** padrão para o tipo de aplicativo.
8. Defina o **JavaScript Origins autorizado** para a URL SSL que você usou anteriormente neste tutorial (a`https://localhost:44300/` menos que você tenha criado outros projetos SSL).   
   Esta URL é a origem para seu aplicativo. Para este exemplo, você irá inserir apenas a URL de teste do localhost. No entanto, você pode inserir vários URLs para explicar o host local e a produção.
9. Defina o **URI de Redirecionamento Autorizado** com o seguinte valor: 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   Este valor é o URI que o OAuth ASP.NET utiliza para comunicar-se com o servidor google OAuth. Lembre-se da URL SSL que você usou acima (a `https://localhost:44300/` menos que você tenha criado outros projetos SSL).
10. Clique no botão **Criar ID do cliente.**
11. No menu esquerdo do Google Developers Console, clique no item do menu **de tela Consentimento** e, em seguida, defina seu endereço de e-mail e nome do produto. Quando tiver concluído o formulário, clique **em Salvar**.
12. Clique no item do menu **APIs,** role para baixo e clique no botão **de desligar** ao lado **da API do Google+.**   
    Aceitar essa opção habilitará a API do Google+.
13. Você também deve atualizar o pacote **Microsoft.Owin** NuGet para a versão 3.0.0.   
    No menu **Ferramentas,** selecione **NuGet Package Manager** e selecione **Gerenciar pacotes NuGet para solução**.  
    Na janela **Gerenciar pacotes NuGet,** encontre e atualize o pacote **Microsoft.Owin** para a versão 3.0.0.
14. No Visual Studio, `UseGoogleAuthentication` atualize o método da página *Startup.Auth.cs* copiando e colando o **Customer ID** e **o Client Secret** no método. Os valores **de ID do Cliente** e do Client **Secret** mostrados abaixo são amostras e não funcionarão. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. Pressione **CTRL+F5** para construir e executar o aplicativo. Clique no link **Logon** .
16. Em **Use outro serviço para fazer login,** clique em **Google**.  
    ![Fazer logon](checkout-and-payment-with-paypal/_static/image11.png)
17. Se é necessário inserir suas credenciais, você será redirecionado ao site do Google, onde vai inserir essas credenciais.  
    ![Google - Entrar](checkout-and-payment-with-paypal/_static/image12.png)
18. Depois de inserir suas credenciais, você será solicitado a dar permissões ao aplicativo web que você acabou de criar.  
    ![Conta de Serviço do Projeto Padrão](checkout-and-payment-with-paypal/_static/image13.png)
19. Clique **em Aceitar**. Agora você será redirecionado de volta para a página **Registrar** do aplicativo **WingtipToys,** onde você pode registrar sua conta do Google.  
    ![Registre-se com sua Conta do Google](checkout-and-payment-with-paypal/_static/image14.png)
20. Você tem a opção de alterar o nome de registro de email local utilizado para sua conta do Gmail, mas normalmente você deverá preferir manter o alias de email padrão (ou seja, aquele utilizado por você para a autenticação). Clique **em Entrar** como mostrado acima.

### <a name="modifying-login-functionality"></a>Modificando a funcionalidade de login

Como mencionado anteriormente nesta série tutorial, grande parte da funcionalidade de registro do usuário foi incluída no modelo ASP.NET Formulários da Web por padrão. Agora você modificará as páginas *login.aspx* e *Register.aspx* padrão para chamar o `MigrateCart` método. O `MigrateCart` método associa um usuário recém-conectado a um carrinho de compras anônimo. Ao associar o usuário e o carrinho de compras, o aplicativo de amostra Wingtip Toys poderá manter o carrinho de compras do usuário entre as visitas.

1. No **Solution Explorer,** encontre e abra a pasta *Conta.*
2. Modifique a página de código-atrás nomeada *Login.aspx.cs* para incluir o código destacado em amarelo, de modo que ele apareça da seguinte forma:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. Salve o arquivo *Login.aspx.cs.*

Por enquanto, você pode ignorar o aviso `MigrateCart` de que não há definição para o método. Você vai adicioná-lo um pouco mais tarde neste tutorial.

O *arquivo Login.aspx.cs* por trás do código suporta um método LogIn. Ao inspecionar a página Login.aspx, você verá que esta página inclui um botão "Fazer login" que, quando clicar, aciona o `LogIn` manipulador no código atrás.

Quando `Login` o método no *Login.aspx.cs* é chamado, uma `usersShoppingCart` nova instância do carrinho de compras nomeado é criada. O ID do carrinho de compras (um GUID) `cartId` é recuperado e definido para a variável. Em seguida, o `MigrateCart` método é `cartId` chamado, passando o nome e o nome do usuário logado para este método. Quando o carrinho de compras é migrado, o GUID usado para identificar o carrinho de compras anônimo é substituído pelo nome do usuário.

Além de modificar o *Login.aspx.cs* arquivo de código atrás para migrar o carrinho de compras quando o usuário faz login, você também deve modificar o *arquivo Register.aspx.cs de código atrás* para migrar o carrinho de compras quando o usuário cria uma nova conta e faz login.

1. Na pasta *Conta,* abra o arquivo de código atrás chamado *Register.aspx.cs*.
2. Modifique o arquivo de código atrás, incluindo o código em amarelo, de modo que ele apareça da seguinte forma:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. Salve o arquivo *Register.aspx.cs.* Mais uma vez, ignore `MigrateCart` o aviso sobre o método.

Observe que o código `CreateUser_Click` usado no manipulador de eventos é `LogIn` muito semelhante ao código que você usou no método. Quando o usuário se registrar ou fazer login no `MigrateCart` site, uma chamada para o método será feita.

## <a name="migrating-the-shopping-cart"></a>Migrando o carrinho de compras

Agora que você tem o processo de login e registro atualizado, você `MigrateCart` pode adicionar o código para migrar o carrinho de compras usando o método.

1. No **Solution Explorer,** encontre a pasta *Logic* e abra o arquivo de classe *ShoppingCartActions.cs.*
2. Adicione o código destacado em amarelo ao código existente no arquivo *ShoppingCartActions.cs,* de modo que o código no arquivo *ShoppingCartActions.cs* seja exibido da seguinte forma:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

O `MigrateCart` método usa o carrinho existente para encontrar o carrinho de compras do usuário. Em seguida, o código faz loops em todos `CartId` os itens do carrinho `CartItem` de compras e substitui a propriedade (conforme especificado pelo esquema) pelo nome de usuário logado.

### <a name="updating-the-database-connection"></a>Atualizando a conexão do banco de dados

Se você estiver seguindo este tutorial usando o aplicativo de exemplo Wingtip Toys **pré-construído,** você deve recriar o banco de dados de membros padrão. Ao modificar a seqüência de conexões padrão, o banco de dados de membros será criado na próxima vez que o aplicativo for executado.

1. Abra o arquivo *Web.config* na raiz do projeto.
2. Atualize a seqüência de conexão padrão para que ela apareça da seguinte forma:   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>Integrando o PayPal

PayPal é uma plataforma de faturamento baseada na Web que aceita pagamentos por comerciantes online. Este tutorial explica em seguida como integrar a funcionalidade de Checkout Express do PayPal em seu aplicativo. O Express Checkout permite que seus clientes usem o PayPal para pagar pelos itens que adicionaram ao carrinho de compras.

### <a name="create-paypal-test-accounts"></a>Criar contas de teste do PayPal

Para usar o ambiente de testes do PayPal, você deve criar e verificar uma conta de teste do desenvolvedor. Você usará a conta de teste do desenvolvedor para criar uma conta de teste do comprador e uma conta de teste do vendedor. As credenciais da conta de teste do desenvolvedor também permitirão que o aplicativo de amostra Wingtip Toys acesse o ambiente de testes do PayPal.

1. Em um navegador, navegue até o site de testes do desenvolvedor do PayPal:   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. Se você não tiver uma conta de desenvolvedor do PayPal, crie uma nova conta clicando **em Cadasciná-lo**e seguindo as etapas de inscrição. Se você tiver uma conta de desenvolvedor do PayPal existente, faça login clicando **em Fazer login**. Você precisará de sua conta de desenvolvedor do PayPal para testar o aplicativo de exemplo Wingtip Toys mais tarde neste tutorial.
3. Se você acabou de se inscrever para sua conta de desenvolvedor do PayPal, talvez seja necessário verificar sua conta de desenvolvedor do PayPal com o PayPal. Você pode verificar sua conta seguindo as etapas que o PayPal enviou para sua conta de e-mail. Depois de verificar sua conta de desenvolvedor do PayPal, faça login novamente no site de testes do desenvolvedor do PayPal.
4. Depois de entrar no site do desenvolvedor do PayPal com sua conta de desenvolvedor do PayPal, você precisa criar uma conta de teste para comprador do PayPal se você ainda não tiver uma. Para criar uma conta de teste do comprador, no site do PayPal clique na guia **Aplicativos** e clique em **contas de Sandbox**.   
 A página **de contas de teste sandbox** é mostrada.   

    > [!NOTE] 
    > 
    > O site do Desenvolvedor PayPal já fornece uma conta de teste do comerciante.

    ![Checkout e Pagamento com contas de teste PayPal - Sandbox](checkout-and-payment-with-paypal/_static/image15.png)
5. Na página contas de teste sandbox, clique **em Criar conta**.
6. Na página **Criar conta de teste** escolha um e-mail da conta de teste do comprador e a senha de sua escolha.   

    > [!NOTE] 
    > 
    > Você precisará dos endereços de e-mail e senha do comprador para testar o aplicativo de exemplo Wingtip Toys no final deste tutorial.

    ![Checkout e Pagamento com contas de teste PayPal - Sandbox](checkout-and-payment-with-paypal/_static/image16.png)
7. Crie a conta de teste do comprador clicando no botão **Criar conta.**  
 A página **de contas de teste de caixa de** areia é exibida. 

    ![Checkout e Pagamento com PayPal - Contas PayPal](checkout-and-payment-with-paypal/_static/image17.png)
8. Na página **de contas de teste do Sandbox,** clique na conta de e-mail **facilitadora.**  
    **As** opções de perfil e **notificação** são exibidas.
9. Selecione a opção **Perfil** e clique em **credenciais de API** para visualizar suas credenciais de API para a conta de teste do comerciante.
10. Copie as credenciais da API TEST para o bloco de notas.

Você precisará de suas credenciais de API classictest (nome de usuário, senha e assinatura) para fazer chamadas de API do aplicativo de amostra Wingtip Toys para o ambiente de teste payPal. Você adicionará as credenciais no próximo passo.

### <a name="add-paypal-class-and-api-credentials"></a>Adicionar credenciais de classe e API do PayPal

Você colocará a maioria do código PayPal em uma única classe. Esta classe contém os métodos usados para se comunicar com o PayPal. Além disso, você adicionará suas credenciais do PayPal a esta classe.

1. No aplicativo de exemplo Wingtip Toys no Visual Studio, clique com o botão direito do mouse na pasta **Lógica** e selecione **Adicionar**  - &gt; **novo item**.   
   A caixa de diálogo **Adicionar novo item** é exibida.
2. Em **Visual C#** do painel **instalado** à esquerda, selecione **Código**.
3. Do painel médio, selecione **Classe**. Nomeie este novo **PayPalFunctions.cs de**classe.
4. Clique em **Adicionar**.  
   O novo arquivo de classe é exibido no editor.
5. Substitua o código padrão pelo código a seguir:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. Adicione as credenciais de API do Comerciante (Nome de usuário, senha e assinatura) que você exibiu anteriormente neste tutorial para que você possa fazer chamadas de função para o ambiente de teste do PayPal.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> Neste aplicativo de exemplo, você está simplesmente adicionando credenciais a um arquivo C# (.cs). No entanto, em uma solução implementada, você deve considerar criptografar suas credenciais em um arquivo de configuração.

A classe NVPAPICaller contém a maioria da funcionalidade PayPal. O código da classe fornece os métodos necessários para fazer uma compra de teste no ambiente de testes do PayPal. As seguintes três funções do PayPal são usadas para fazer compras:

- Função `SetExpressCheckout`
- Função `GetExpressCheckoutDetails`
- Função `DoExpressCheckoutPayment`

O `ShortcutExpressCheckout` método coleta as informações de compra do teste `SetExpressCheckout` e os detalhes do produto do carrinho de compras e chama a função PayPal. O `GetCheckoutDetails` método confirma os detalhes da compra e chama a `GetExpressCheckoutDetails` função PayPal antes de fazer a compra do teste. O `DoCheckoutPayment` método completa a compra do teste a `DoExpressCheckoutPayment` partir do ambiente de teste, chamando a função PayPal. O código restante suporta os métodos e o processo do PayPal, como codificação de strings, decodificação de strings, matrizes de processamento e determinação de credenciais.

> [!NOTE] 
> 
> O PayPal permite incluir detalhes opcionais de compra com base na [especificação da API do PayPal.](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout) Ao estender o código no aplicativo de exemplo Wingtip Toys, você pode incluir detalhes de localização, descrições de produtos, impostos, um número de atendimento ao cliente, bem como muitos outros campos opcionais.

Observe que os URLs de retorno e cancelamento especificados no método **ShortcutExpressCheckout** usam um número de porta.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Quando o Visual Web Developer executa um projeto web usando O SSL, geralmente a porta 44300 é usada para o servidor web. Como mostrado acima, o número da porta é 44300. Quando você executa o aplicativo, você pode ver um número de porta diferente. Seu número de porta precisa ser corretamente definido no código para que você possa executar com sucesso o aplicativo de exemplo Wingtip Toys no final deste tutorial. A próxima seção deste tutorial explica como recuperar o número da porta de host local e atualizar a classe PayPal.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>Atualize o número da porta localhost na classe PayPal

O aplicativo de amostra Wingtip Toys compra produtos navegando até o site de testes do PayPal e retornando à sua instância local do aplicativo de amostra Wingtip Toys. Para que o PayPal retorne à URL correta, você precisa especificar o número da porta do aplicativo de amostra em execução local no código PayPal mencionado acima.

1. Clique com o botão direito do mouse no nome do projeto **(WingtipToys)** no **Solution Explorer** e selecione **Propriedades**.
2. Na coluna esquerda, selecione a guia **Web.**
3. Recupere o número da porta na caixa Url do **projeto.**
4. Se necessário, `returnURL` atualize a classe `cancelURL` `NVPAPICaller`E na classe PayPal ( ) no arquivo *PayPalFunctions.cs* para usar o número de porta do seu aplicativo web:   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

Agora, o código adicionado corresponderá à porta esperada para o aplicativo local da Web. O PayPal poderá retornar à URL correta em sua máquina local.

### <a name="add-the-paypal-checkout-button"></a>Adicione o botão de checkout do PayPal

Agora que as funções principais do PayPal foram adicionadas ao aplicativo de exemplo, você pode começar a adicionar a marcação e o código necessários para chamar essas funções. Primeiro, você deve adicionar o botão de checkout que o usuário verá na página do carrinho de compras.

1. Abra o arquivo *ShoppingCart.aspx.*
2. Role até a parte inferior `<!--Checkout Placeholder -->` do arquivo e encontre o comentário.
3. Substitua o `ImageButton` comentário por um controle para que a marcação seja substituída da seguinte forma:  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. No arquivo *ShoppingCart.aspx.cs,* `UpdateBtn_Click` após o manipulador de eventos perto `CheckOutBtn_Click` do final do arquivo, adicione o manipulador de eventos:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. Também no *arquivo ShoppingCart.aspx.cs,* adicione `CheckoutBtn`uma referência ao , de modo que o novo botão de imagem seja referenciado da seguinte forma:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. Salve suas alterações no arquivo *ShoppingCart.aspx* e no *arquivo ShoppingCart.aspx.cs.*
7. No menu, selecione **Debug**-&gt;**Build WingtipToys**.  
   O projeto será reconstruído com o recém-adicionado controle **ImageButton.**

### <a name="send-purchase-details-to-paypal"></a>Envie detalhes de compra para o PayPal

Quando o usuário **clica** no botão Checkout na página do carrinho de compras *(ShoppingCart.aspx),* ele iniciará o processo de compra. O código a seguir chama a primeira função PayPal necessária para comprar produtos.

1. A partir da pasta *Checkout,* abra o arquivo de código atrás chamado *CheckoutStart.aspx.cs*.   
   Certifique-se de abrir o arquivo de código atrás.
2. Substitua o código existente pelo seguinte:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

Quando o usuário do aplicativo clica no botão **Checkout** na página do carrinho de compras, o navegador navegará até a página *CheckoutStart.aspx.* Quando a página *CheckoutStart.aspx* `ShortcutExpressCheckout` é carregada, o método é chamado. Neste ponto, o usuário é transferido para o site de testes do PayPal. No site do PayPal, o usuário insere suas credenciais do PayPal, analisa os detalhes da `ShortcutExpressCheckout` compra, aceita o contrato do PayPal e retorna ao aplicativo de amostra Wingtip Toys onde o método é concluído. Quando `ShortcutExpressCheckout` o método estiver concluído, ele redirecionará o usuário para a página `ShortcutExpressCheckout` *CheckoutReview.aspx* especificada no método. Isso permite que o usuário revise os detalhes do pedido dentro do aplicativo de amostra Wingtip Toys.

### <a name="review-order-details"></a>Detalhes do pedido de revisão

Após retornar do PayPal, a página *CheckoutReview.aspx* do aplicativo de exemplo Wingtip Toys exibe os detalhes do pedido. Esta página permite que o usuário revise os detalhes do pedido antes de comprar os produtos. A página *CheckoutReview.aspx* deve ser criada da seguinte forma:

1. Na pasta *Checkout,* abra a página chamada *CheckoutReview.aspx*.
2. Substitua a marcação existente pelo seguinte:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. Abra a página de código-atrás chamada *CheckoutReview.aspx.cs* e substitua o código existente pelo seguinte:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

O controle **DetailsView** é usado para exibir os detalhes do pedido que foram retornados do PayPal. Além disso, o código acima salva os detalhes `OrderDetail` do pedido no banco de dados Wingtip Toys como um objeto. Quando o usuário clica no botão **Ordem completa,** ele é redirecionado para a página *CheckoutComplete.aspx.*

> [!NOTE] 
> 
> **Ponta**
> 
> Na marcação da página *CheckoutReview.aspx,* `<ItemStyle>` observe que a tag é usada para alterar o estilo dos itens dentro do controle **DetailsView** perto da parte inferior da página. Ao visualizar a página no **Design View** (selecionando **Design** no canto inferior esquerdo do Visual Studio), selecionando o controle **DetailsView** e selecionando a **Tag Inteligente** (o ícone de seta no canto superior direito do controle), você poderá ver o **DetailsView Tasks**.
> 
> ![Checkout e Pagamento com PayPal - Editar campos](checkout-and-payment-with-paypal/_static/image18.png)
> 
> Ao selecionar **Editar campos,** a caixa de diálogo **Campos** será exibida. Nesta caixa de diálogo você pode controlar facilmente as propriedades visuais, como **ItemStyle**, do controle **DetailsView.**
> 
> ![Checkout e Pagamento com PayPal - Diálogo campos](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>Compra completa

*CheckoutPáginaPáginaComplete.aspx* faz a compra do PayPal. Como mencionado acima, o usuário deve clicar no botão **Ordem Completa** antes que o aplicativo navegue até a página *CheckoutComplete.aspx.*

1. Na pasta *Checkout,* abra a página chamada *CheckoutComplete.aspx*.
2. Substitua a marcação existente pelo seguinte:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. Abra a página de código-atrás chamada *CheckoutComplete.aspx.cs* e substitua o código existente pelo seguinte:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

Quando a página *CheckoutComplete.aspx* é `DoCheckoutPayment` carregada, o método é chamado. Como mencionado anteriormente, o `DoCheckoutPayment` método completa a compra do ambiente de testes do PayPal. Uma vez que o PayPal tenha concluído a compra do pedido, `ID` a página *CheckoutComplete.aspx* exibe uma transação de pagamento ao comprador.

### <a name="handle-cancel-purchase"></a>Lidar com a compra de cancelamento

Se o usuário decidir cancelar a compra, ele será direcionado para a página *CheckoutCancel.aspx,* onde verá que seu pedido foi cancelado.

1. Abra a página chamada *CheckoutCancel.aspx* na pasta *Checkout.*
2. Substitua a marcação existente pelo seguinte:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>Lidar com erros de compra

Erros durante o processo de compra serão tratados pela página *CheckoutError.aspx.* O código-atrás da página *CheckoutStart.aspx,* da página *CheckoutReview.aspx* e da página *CheckoutComplete.aspx* redirecionarão cada um para a página *CheckoutError.aspx* se ocorrer um erro.

1. Abra a página chamada *CheckoutError.aspx* na pasta *Checkout.*
2. Substitua a marcação existente pelo seguinte:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

A página *CheckoutError.aspx* é exibida com os detalhes de erro quando ocorre um erro durante o processo de checkout.

## <a name="running-the-application"></a>Executando o aplicativo

Execute o aplicativo para ver como comprar produtos. Observe que você estará executando no ambiente de testes do PayPal. Nenhum dinheiro de verdade está sendo trocado.

1. Certifique-se de que todos os seus arquivos estão salvos no Visual Studio.
2. Abra um navegador da [https://developer.paypal.com](https://developer.paypal.com/)Web e navegue para .
3. Faça login com sua conta de desenvolvedor do PayPal que você criou anteriormente neste tutorial.  
   Para o sandbox de desenvolvedor do PayPal, [https://developer.paypal.com](https://developer.paypal.com/) você precisa estar logado para testar o checkout expresso. Isso só se aplica aos testes de sandbox do PayPal, não ao ambiente ao vivo do PayPal.
4. No Visual Studio, pressione **F5** para executar o aplicativo de exemplo Wingtip Toys.  
   Depois que o banco de dados se reconstrói, o navegador será aberto e mostrará a página *Default.aspx.*
5. Adicione três produtos diferentes ao carrinho de compras selecionando a categoria do produto, como "Carros" e, em seguida, clique **em Adicionar ao Carrinho** ao lado de cada produto.  
   O carrinho de compras exibirá o produto selecionado.
6. Clique no botão **PayPal** para fazer o checkout. 

    ![Checkout e Pagamento com PayPal - Carrinho](checkout-and-payment-with-paypal/_static/image20.png)

   A verificação exigirá que você tenha uma conta de usuário para o aplicativo de exemplo Wingtip Toys.
7. Clique no link do **Google** no direito da página para fazer login com uma conta de e-mail gmail.com existente.  
   Se você não tiver uma conta gmail.com, você pode criar uma para fins de teste em [www.gmail.com](https://www.gmail.com/). Você também pode usar uma conta local padrão clicando em "Registrar". 

    ![Checkout e Pagamento com PayPal - Login](checkout-and-payment-with-paypal/_static/image21.png)
8. Faça login com sua conta do gmail e senha. 

    ![Checkout e Pagamento com PayPal - Login do Gmail](checkout-and-payment-with-paypal/_static/image22.png)
9. Clique **no** botão Fazer login para registrar sua conta do gmail com o nome de usuário do aplicativo de exemplo Wingtip Toys. 

    ![Checkout e Pagamento com PayPal - Conta de Registro](checkout-and-payment-with-paypal/_static/image23.png)
10. No site de teste do PayPal, adicione **o** endereço de e-mail e a senha que você criou anteriormente neste tutorial e clique no botão **Entrar.** 

    ![Checkout e Pagamento com PayPal - Login do PayPal](checkout-and-payment-with-paypal/_static/image24.png)
11. Concorde com a política do PayPal e clique no botão **Concordar e Continuar.**  
    Observe que esta página só é exibida na primeira vez que você usa esta conta do PayPal. Novamente note que esta é uma conta de teste, nenhum dinheiro real é trocado. 

    ![Checkout e Pagamento com PayPal - Política paypal](checkout-and-payment-with-paypal/_static/image25.png)
12. Revise as informações do pedido na página de revisão do ambiente de teste do PayPal e clique **em Continuar**. 

    ![Checkout e Pagamento com PayPal - Informações de revisão](checkout-and-payment-with-paypal/_static/image26.png)
13. Na página *CheckoutReview.aspx,* verifique a quantidade do pedido e visualize o endereço de envio gerado. Em seguida, clique no botão **Ordem completa.** 

    ![Checkout e Pagamento com PayPal - Revisão de Pedidos](checkout-and-payment-with-paypal/_static/image27.png)
14. A página **CheckoutComplete.aspx** é exibida com um ID de transação de pagamento. 

    ![Checkout e Pagamento com PayPal - Checkout completo](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>Revisão do banco de dados

Ao revisar os dados atualizados no banco de dados do aplicativo de exemplo Wingtip Toys após a execução do aplicativo, você pode ver que o aplicativo registrou com sucesso a compra dos produtos.

Você pode inspecionar os dados contidos no arquivo de banco de dados *Wingtiptoys.mdf* usando a janela **Database Explorer** (janela**Server Explorer** no Visual Studio) como você fez anteriormente nesta série tutorial.

1. Feche a janela do navegador se ela ainda estiver aberta.
2. No Visual Studio, selecione o ícone **Mostrar todos os arquivos** na parte superior do Solution **Explorer** para permitir que você expanda a pasta Dados do **Aplicativo.\_**
3. Expanda a pasta Dados do **aplicativo.\_**  
 Talvez seja necessário selecionar o ícone **Mostrar todos os arquivos** para a pasta.
4. Clique com o botão direito do mouse no arquivo de banco de dados *Wingtiptoys.mdf* e selecione **Abrir**.  
    **O Server Explorer** é exibido.
5. Expanda a pasta **Tabelas** .
6. Clique com o botão direito do mouse na tabela **Pedidos**e selecione **Mostrar dados da tabela**.  
 A **tabela Ordens** é exibida.
7. Revise a coluna **PaymentTransactionID** para confirmar transações bem-sucedidas. 

    ![Checkout e Pagamento com PayPal - Banco de Dados de Revisão](checkout-and-payment-with-paypal/_static/image29.png)
8. Feche a janela da mesa **de ordens.**
9. No Server Explorer, clique com o botão direito do mouse na tabela **Detalhes** do pedido e selecione **Mostrar dados da tabela**.
10. Revise `OrderId` `Username` os valores e valores na tabela **OrderDetails.** Observe que esses `OrderId` valores correspondem aos valores `Username` incluídos na tabela **Ordens.**
11. Feche a janela da tabela **OrderDetails.**
12. Clique com o botão direito do mouse no arquivo de banco de dados Wingtip Toys *(Wingtiptoys.mdf)* e selecione **Conexão fechada**.
13. Se você não ver a janela **Solution Explorer,** clique em **Solution Explorer** na parte inferior da janela **Server Explorer** para mostrar o Explorador **de soluções** novamente.

## <a name="summary"></a>Resumo

Neste tutorial você adicionou esquemas de detalhes de pedidos e pedidos para acompanhar a compra de produtos. Você também integrou a funcionalidade do PayPal no aplicativo de amostra Wingtip Toys.

## <a name="additional-resources"></a>Recursos adicionais

[visão geral da configuração ASP.NET](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[Implantar um aplicativo de formulários web ASP.NET seguro com banco de dados de adesão, OAuth e SQL para o serviço de aplicativos do Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure - Teste gratuito](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>Isenção de responsabilidade

Este tutorial contém código de amostra. Esse código de amostra é fornecido "como está" sem qualquer tipo de garantia. Assim, a Microsoft não garante a precisão, integridade ou qualidade do código de amostra. Você concorda em usar o código de amostra por sua conta e risco. Em nenhuma circunstância a Microsoft será responsável por você de qualquer forma por qualquer código de amostra, conteúdo, incluindo, mas não se limitando a, quaisquer erros ou omissões em qualquer código de amostra, conteúdo ou qualquer perda ou dano de qualquer tipo incorrido como resultado do uso de qualquer código de amostra. Você é notificado e concorda em indenizar, salvar e manter a Microsoft inofensiva de e contra toda e qualquer perda, alegações de perda, lesão ou dano de qualquer tipo, incluindo, sem limitação, aquelas ocasionadas ou decorrentes de material que você posta, transmite, usa ou confia, incluindo, mas não se limitando a, as opiniões nele expressas.

> [!div class="step-by-step"]
> [Próximo](shopping-cart.md)
> [anterior](membership-and-administration.md)
