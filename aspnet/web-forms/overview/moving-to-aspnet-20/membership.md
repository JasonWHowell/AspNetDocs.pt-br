---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: Adesão | Microsoft Docs
author: rick-anderson
description: ASP.NET A adesão baseia-se no sucesso do modelo de autenticação Forms de ASP.NET 1.x. ASP.NET autenticação de Formulários fornece uma maneira conveniente de incorp...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: ed48c11cbd483de088239bad7c2452b7fc60a1cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543763"
---
# <a name="membership"></a>Membership

pela [Microsoft](https://github.com/microsoft)

> ASP.NET A adesão baseia-se no sucesso do modelo de autenticação Forms de ASP.NET 1.x. ASP.NET a autenticação de Formulários fornece uma maneira conveniente de incorporar um formulário de login em seu aplicativo ASP.NET e validar usuários em um banco de dados ou outro armazenamento de dados.

ASP.NET A adesão baseia-se no sucesso do modelo de autenticação Forms de ASP.NET 1.x. ASP.NET a autenticação de Formulários fornece uma maneira conveniente de incorporar um formulário de login em seu aplicativo ASP.NET e validar usuários em um banco de dados ou outro armazenamento de dados. Os membros da classe FormsAuthentication tornam possível lidar com cookies para autenticação, verificar um login válido, fazer logde de um usuário etc. No entanto, a implementação de formulários de autenticação em um aplicativo ASP.NET 1.x pode exigir uma quantidade justa de código.

A adesão ao ASP.NET 2.0 é um grande avanço sobre o uso apenas da autenticação Forms. (A associação é mais robusta quando acoplada à autenticação de Formulários, mas o uso da autenticação de Formulários não é um requisito.) Como você verá em breve, você pode usar ASP.NET Membership e os controles de login em ASP.NET 2.0 para implementar um poderoso sistema de adesão sem escrever muito código.

## <a name="implementing-membership-in-aspnet-20"></a>Implementação de adesão ao ASP.NET 2.0

A adesão é implementada seguindo quatro etapas. Tenha em mente que existem muitas subetapas envolvidas, bem como configurações opcionais que também podem ser implementadas. Essas etapas destinam-se a ilustrar o panorama geral da configuração da associação.

1. Crie seu banco de dados de membros (se o SQL Server for usado como loja de membros.)
2. Especifique as opções de associação em seus arquivos de configuração de aplicativos. (A adesão é ativada por padrão.)
3. Determine o tipo de loja de membros que deseja usar. As opções são: 

    - Microsoft SQL Server (versão 7.0 ou posterior)
    - Loja de Diretórios Ativos
    - Provedor de adesão personalizado
4. Configure o aplicativo para autenticação de Formulários ASP.NET. Mais uma vez, a Associação foi projetada para aproveitar a autenticação de Formulários, mas o uso da autenticação de Formulários não é um requisito.
5. Defina contas de usuário para a adesão e configure funções se desejar.

## <a name="creating-the-membership-database"></a>Criando o banco de dados de membros

Se você estiver usando o SQL Server 7.0 ou posterior como\_sua loja de membros, você pode usar o utilitário aspnet regsql (disponível mais facilmente no Visual Studio .NET 2005 Command Prompt) para configurar seu banco de dados. O utilitário\_aspnet regsql pode ser usado como uma ferramenta de prompt de comando ou através de um assistente de GUI. O método do assistente é a maneira mais fácil de configurar seu banco de dados. Para acessar o assistente, basta executar o seguinte comando:

`aspnet_regsql W`

Uma vez executado esse comando, você será apresentado com o ASP.NET Assistente de Configuração do Servidor SQL, conforme mostrado abaixo.

![](membership/_static/image1.jpg)

**Figura 1**

O ASP.NET SQL Server Setup Wizard cria o site na instância que você especifica no assistente. No entanto, ASP.NET usará a seqüência de conexões no arquivo machine.config para se conectar ao seu banco de dados. Por padrão, essa seqüência de conexão apontará para uma instância do SQL Server 2005, portanto, se você estiver usando uma instância SQL Server 2000 ou SQL Server 7.0, você precisará modificar a seqüência de conexão no arquivo machine.config. Essa seqüência de conexões pode ser localizada aqui:

[!code-xml[Main](membership/samples/sample1.xml)]

Infelizmente, se você não modificar a seqüência de conexões, ASP.NET não lhe dará um erro descritivo. Ele só vai continuar reclamando dizendo que você não criou o banco de dados. No caso acima, modifiquei a seqüência de conexões para apontar para a minha instância local do SQL Server 2000.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>Especificando configuração e adicionando usuários e funções

O próximo passo na configuração da Associação é adicionar as informações necessárias ao arquivo web.config do aplicativo. Em ASP.NET 1.x, modificar o arquivo web.config às vezes era difícil devido ao uso de menorCamelCase e à falta de Intellisense. O Visual Studio .NET 2005 torna a tarefa muito mais fácil com o Intellisense para arquivos de configuração, mas ASP.NET 2.0 vai um passo adiante, fornecendo uma interface Web para edição de arquivos de configuração.

Você pode iniciar a interface da Web clicando no botão ASP.NET Configuração na barra de ferramentas do Solution Explorer, conforme mostrado abaixo. Você também pode iniciar a interface web através de pop-ups que são exibidos quando os controles de login são inseridos.

![](membership/_static/image2.jpg)

**Figura 2**

Isso lança a ferramenta de administração de sites ASP.NET mostrada abaixo. A ASP.NET Administração do Site é uma interface de quatro guias que facilita o gerenciamento das configurações do aplicativo. As seguintes guias estão disponíveis:

- **Início**
- **Segurança** Configure usuários, funções e acesso.
- **Aplicação** Configure as configurações do aplicativo.
- **Provedor** Configure e teste o provedor de adesão de aplicativos.

A Ferramenta de Administração de Sites permite criar facilmente novos usuários, criar novas funções e gerenciar usuários e funções. Essa habilidade não está disponível na interface do Windows. A interface do Windows permite definir facilmente as configurações de autorização e adicionar, excluir e gerenciar provedores, recursos que não estão na Ferramenta de Administração de Sites da Web.

Para iniciar a interface do Windows, abra o snap-in dos Serviços de Informação da Internet, clique com o botão direito do mouse no aplicativo e escolha Propriedades. Clique na guia ASP.NET e clique no botão Editar configuração. (O aplicativo deve estar em execução sob ASP.NET 2.0 para que o botão Editar configuração seja ativado. Você também pode configurar a versão ASP.NET na caixa de ASP.NET.) A ASP.NET configuração configuração é exibida conforme mostrado abaixo.

![](membership/_static/image3.jpg)

**Figura 3**

Na guia Geral, as strings de conexão e as configurações do aplicativo estão listadas. Todas as configurações em itálico são definidas em um arquivo de configuração pai (a máquina.config ou uma web.config em um nível mais alto) e as configurações que não estão em itálico são do arquivo de configuração de aplicativos. Se uma configuração for adicionada, removida ou editada no nível do aplicativo, ASP.NET adicionará, removerá ou modificará a configuração nos níveis de aplicativo web.config em vez de remover a configuração do arquivo de configuração do qual é herdada.

A guia Autenticação é mostrada abaixo. É aqui que você configurará suas configurações de associação. As configurações de autenticação de formulários, provedores de membros e provedores de função podem ser configurados aqui.

![](membership/_static/image4.jpg)

**Figura 4**

## <a name="implementing-membership-in-your-application"></a>Implementando a adesão em sua aplicação

A maneira mais fácil de implementar ASP.NET a de adesão 2.0 em seu aplicativo é usar os controles Logon fornecidos. Este método permite que você implemente o básico de ASP.NET 2.0 sem escrever nenhum código.

Os seguintes controles de Logon estão disponíveis em ASP.NET 2.0:

## <a name="login-control"></a>Controle de login

O controle de login fornece uma interface para alguém fazer login no seu sistema de adesão. Ele fornece uma caixa de texto de nome de usuário e senha e um botão de login. Muitos outros recursos comuns, como um link para se registrar para pessoas que ainda não o fizeram, uma caixa de seleção que permite ao usuário fazer login automaticamente em visitas subseqüentes, um link para um lembrete de senha, etc. Todos os recursos do controle de login são personalizáveis através das propriedades do controle.

Em ASP.NET 1.x, os desenvolvedores tiveram que escrever uma boa quantidade de código para fazer uma olhada ao usar a autenticação de Formulários. Com ASP.NET a de adesão 2.0, você pode validar usuários sem escrever nenhum código. ASP.NET fará automaticamente a busca do usuário para você. (Se você estiver usando o controle de login sem usar ASP.NET a de membros, você pode usar o método **OnAuthenticate** para validar o usuário.)

## <a name="loginview-control"></a>Controle de LoginView

O controle LoginView é um controle modelado que fornece dois modelos por padrão; o AnonymousTemplate e o LoggedInTemplate. O modelo exibido é determinado se o usuário está ou não conectado ao seu sistema de adesão. Esse controle é normalmente usado para exibir um controle de Login quando um usuário ainda não fez login e um controle de LoginStatus e/ou outros controles de login quando o usuário fez login. Se você estiver usando o gerenciamento de função em seu aplicativo ASP.NET, o controle LoginView pode exibir um modelo específico com base na função dos usuários. (Mais sobre ASP.NET gestão de papéis será coberto mais tarde.)

## <a name="passwordrecovery-control"></a>Controle de Recuperação de Senhas

O controle PasswordRecovery permite que os usuários recebam um e-mail com sua senha atual ou resete sua senha. Texto claro e senhas criptografadas podem ser recuperados e enviados por e-mail aos usuários. Se a senha for hashed, ela não pode ser recuperada. Em vez disso, o usuário será obrigado a executar uma redefinição de senha.

## <a name="loginstatus-control"></a>Controle de LoginStatus

O controle LoginStatus é usado para exibir um indicador de login para usuários que não estão conectados e um indicador de logout para usuários que estão conectados no momento. A propriedade Request.IsAuthenticated é usada para determinar qual indicador exibir. O indicador exibido pelo controle LoginStatus pode ser texto (implementado através das propriedades **LoginText** e **LogoutText)** ou imagens (implementadas através das propriedades **LoginImageUrl** e **LogoutImageUrl.)**

Quando um usuário faz logout através do controle LoginStatus, ele ou ela é redirecionado para a URL especificada pela propriedade **LogoutPageUrl.** Se essa propriedade não estiver definida, a página atual será atualizada. Uma vez que o site é provavelmente protegido pela autenticação Formulários, a atualização da página atual redirecionará o usuário para a página de login do site.

## <a name="loginname-control"></a>Controle de loginname

O controle LoginName exibe o nome de usuário do usuário atualmente logado no site.

## <a name="createuserwizard-control"></a>CriarcontroleDoUsuário-MÁGICO

O controle CreateUserWizard fornece aos usuários uma maneira conveniente de se registrar em seu sistema de membros. Você pode adicionar etapas (implementadas como uma coleção de WizardSteps) através da interface mostrada abaixo.

![](membership/_static/image5.jpg)

**Figura 5**

O CreateUserWizard é um controle de modelo que deriva da classe Assistente e fornece os seguintes modelos:

- **Modelo de cabeçalho** Este modelo controla a aparência do cabeçalho do assistente.
- **Modelo de barra lateral** Este modelo controla a aparência da barra lateral do assistente.
- **StartNavigationTemplate** Este modelo controla a aparência da navegação do assistente na etapa inicial.
- **Modelo de StepNavigation** Este modelo controla a aparência da área de navegação quando não está na etapa de início ou término.
- **Modelo de navegação de acabamento** Este modelo controla a aparência da área de navegação quando na etapa de acabamento.

Além disso, para cada etapa que você adicionar ao Assistente, ASP.NET criará um modelo personalizado que contenha um ContentTemplate e um CustomNavigationTemplate para essa etapa. Para obter detalhes completos sobre a personalização do CreateUserWizard, consulte a documentação VS.NET 2005:

## <a name="changepassword-control"></a>Controle de senha de alteração

O controle ChangePassword permite que os usuários alterem sua senha. Se a propriedade DisplayUserName for verdadeira (é falsa por padrão), o usuário poderá alterar sua senha quando não estiver logado. Se o usuário já *estiver* logado e a propriedade DisplayUserName for verdadeira, o usuário poderá alterar a senha de outro usuário que não esteja logado desde que saiba a ID do usuário.

Tenha em mente que se você quiser que os usuários sejam capazes de alterar senhas sem ter que fazer login, você precisará garantir que a página na qual o controle ChangePassword é exibido permita acesso anônimo. Obviamente, os usuários terão que fornecer sua senha antiga para alterar sua senha.

## <a name="role-management"></a>Gerenciamento de funções

O gerenciamento de função permite atribuir os usuários a uma determinada função e, em seguida, restringir o acesso a determinados arquivos ou pastas com base nessa função. O gerenciamento de função também fornece uma API para que você possa determinar programáticamente a função de alguém ou determinar todos os usuários em uma determinada função e responder de acordo.

A gestão de papéis não é um requisito na ASP.NET a de adesão, nem a adesão é um requisito para usar a gestão de papéis. No entanto, os dois complementam um ao outro muito bem e é provável que os desenvolvedores os usem em conjunto entre si.

Para habilitar o gerenciamento de função em seu aplicativo, faça a seguinte alteração no seu arquivo Web.config:

[!code-xml[Main](membership/samples/sample2.xml)]

Quando o atributo **cacheRolesInCookie** é definido como true, ASP.NET armazena em cache uma função de usuário em um cookie no cliente. Isso permite que as maquinações de função ocorram sem chamadas para o RoleProvider. Ao usar esse atributo, os desenvolvedores são encorajados a garantir que o atributo **cookieProtection** esteja definido como All. (Esta é a configuração padrão.) Isso garante que os dados dos cookies sejam criptografados e ajuda a garantir que o conteúdo dos cookies não tenha sido alterado. As funções podem ser adicionadas usando a Ferramenta de Administração de Sites. Ele permite definir facilmente funções, configurar o acesso a partes do site com base nessas funções e atribuir usuários a funções.

![](membership/_static/image6.jpg)

**Figura 6**

Como mostrado acima, novas funções podem ser adicionadas simplesmente digitando o nome da função e, em seguida, clicando em Adicionar função. As funções existentes podem ser gerenciadas ou excluídas clicando no link apropriado na lista de funções existentes.

Quando você gerencia uma função, você pode adicionar ou remover usuários como mostrado abaixo.

![](membership/_static/image7.jpg)

**Figura 7**

Ao verificar a caixa de seleção Usuário está em função, você pode facilmente adicionar um usuário a uma função específica. ASP.NET atualizará automaticamente seu banco de dados de membros com as entradas apropriadas. Você também vai querer configurar regras de acesso para o seu aplicativo. ASP.NET desenvolvedores do 1.x estão &lt;familiarizados em fazer isso através do elemento de autorização&gt; no arquivo web.config, e essa opção ainda está disponível em ASP.NET 2.0. No entanto, é mais fácil gerenciar as regras de acesso usando a Ferramenta de Administração de Sites, conforme mostrado abaixo.

![](membership/_static/image8.jpg)

**Figura 8**

Neste caso, destaca-se a pasta Administração (é difícil de ver porque a ferramenta a destaca em cinza claro) e a função Administradores tem acesso concedido. Todos os outros usuários são negados. Você pode clicar no ícone da cabeça para selecionar uma regra e, em seguida, usar os botões Mover para cima e mover para baixo para organizar as regras. Assim como &lt;o&gt; elemento de autorização ASP.NET, as regras são processadas na ordem em que aparecem. Ou seja, se a ordem das regras no tiro acima fosse invertida, ninguém teria acesso à pasta de Administração porque a primeira regra que ASP.NET encontraria seria a regra que nega a todos para a pasta.

ASP.NET 2.0 adiciona um arquivo web.config à pasta para a qual você está especificando uma regra de acesso. As regras de acesso podem ser editadas através do arquivo de configuração ou através da Ferramenta de Administração de Sites. Em outras palavras, a Ferramenta de Administração de Sites da Web é simplesmente uma interface através da qual o arquivo de configuração pode ser editado em um ambiente fácil de usar.

## <a name="using-roles-in-code"></a>Usando funções em código

A API para gerenciamento de papéis não mudou desde a versão 1.x. O método **IsInRole** é usado para determinar se um usuário está em uma função específica.

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET também cria uma instância RolePrincipal como membro do contexto atual. O objeto RolePrincipal pode ser usado para obter todas as funções a que o usuário pertence da seguinte forma:

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>Usando RoleGroups com o Controle LoginView

Agora que você tem uma compreensão do gerenciamento de papéis e da associação, vamos discutir brevemente como o controle do LoginView tira proveito desse recurso em ASP.NET 2.0. Como discutido anteriormente, o controle LoginView é um controle modelado que contém dois modelos por padrão; o AnonymousTemplate e o LoggedInTemplate. Dentro da caixa de diálogo LoginView Tasks está um link (mostrado abaixo) que permite editar RoleGroups.

![](membership/_static/image9.jpg)

**Figura 9**

Cada objeto RoleGroup contém uma matriz de strings que define quais funções o RoleGroup se aplica. Para adicionar um novo RoleGroup ao controle LoginView, clique no link Editar RoleGroups. Na imagem acima, você pode ver que eu adicionei um novo RoleGroup para administradores. Ao selecionar esse RoleGroup (RoleGroup[0]) a partir da suspenso Views, posso configurar um modelo que só será exibido para membros da função Administradores. Na imagem abaixo, adicionei um novo RoleGroup que se aplica aos membros da função Vendas e da função distribuição. Isso adiciona um segundo RoleGroup à parada de exibições na caixa de diálogo LoginView Tasks e qualquer coisa adicionada a esse modelo será visível por qualquer usuário na função Vendas ou Distribuição.

![](membership/_static/image10.jpg)

**Figura 10**

## <a name="overriding-the-existing-membership-provider"></a>Substituindo o provedor de adesão existente

Existem algumas maneiras que você pode estender a funcionalidade de ASP.NET a de adesão. Em primeiro lugar, você pode obviamente alterar a funcionalidade existente da classe SqlMembershipProvider herdando-a e substituindo seus métodos. Por exemplo, se você quiser implementar sua própria funcionalidade quando os usuários são criados, você pode criar sua própria classe que herda do SqlMembershipProvider da seguinte forma:

[!code-csharp[Main](membership/samples/sample5.cs)]

Se, por outro lado, você quiser criar seu próprio provedor (para armazenar suas informações de associação em um banco de dados access, por exemplo), você pode criar seu próprio provedor.

## <a name="creating-your-own-membership-provider"></a>Criando seu próprio provedor de adesão

Para criar seu próprio provedor de membros, primeiro você precisará criar uma classe que herda da classe MembershipProvider. Se você estiver usando VB.NET, o Visual Studio 2005 adicionará os stubs para todos os métodos que você precisa substituir. Se você estiver usando C#, cabe a você adicionar os stubs.

Você precisará substituir o seguinte:

- Propriedade ApplicationName
- Função ChangePassword
- Função ChangePasswordQuestionAndAnswer
- Função CreateUser
- ExcluirfunçãoUsuário
- Ativarpropriedade PasswordReset
- Ativar a propriedadePasswordRetrieval
- Encontrarusuáriospore-mail função
- Função FindUsersByName
- Função GetAllUsers
- ObternúmerodeusuáriosFunçãoOnline
- Função GetPassword
- Função GetUser
- ObterusuárioNomePorE-mail função
- Propriedade MaxInvalidPasswordAttempts
- MinRequiredNonAlphanumericCharacters property
- MinRequiredPasswordLength
- Propriedade PasswordAttemptWindow
- Propriedade PasswordFormat
- Propriedade PasswordStrengthRegularExpression
- Requeraquestãoeresponder propriedade
- Requer propriedadeUniqueEmail
- Função RedefinirSenha
- Desbloquear função do usuário
- AtualizaçãoFunçãousuário
- ValidarfunçãoUsuário

Isso é uma lista e tanto para implementar como desenvolvedor C#. Você pode achar mais fácil criar a classe em VB.NET sem qualquer implementação e, em seguida, usar o .NET Reflector ou uma ferramenta semelhante para converter o código em C#.

A seqüência de conexões e outras propriedades devem ser definidas como padrão no método Initialize. (O método Initialize é acionado quando o provedor é carregado em tempo de execução.) O segundo parâmetro para o método Initialize é do tipo System.Collections.Specialized.NameValueCollection e é uma referência ao elemento &lt;add&gt; que está associado ao seu provedor personalizado no arquivo web.config. Essa entrada parece a seguinte:

[!code-xml[Main](membership/samples/sample6.xml)]

Aqui está um exemplo do método Initialize.

[!code-csharp[Main](membership/samples/sample7.cs)]

Para validar o usuário quando ele enviar seu formulário de login, você precisará usar o método ValidateUser. Este método é acionado quando o usuário clica no botão de login no controle de login. Você colocará seu código que faz a procura do usuário neste método.

Como você pode ver, escrever seu próprio provedor de membros não é difícil e permite que você amplie essa poderosa funcionalidade de ASP.NET 2.0.
