---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: Aplicações seguras usando autenticação e autorização | Microsoft Docs
author: rick-anderson
description: O passo 9 mostra como adicionar autenticação e autorização para proteger nosso aplicativo NerdDinner, para que os usuários precisem se cadastrar e fazer login no site para criar...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542567"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>Proteger aplicativos usando autenticação e autorização

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 9 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O passo 9 mostra como adicionar autenticação e autorização para proteger nosso aplicativo NerdDinner, para que os usuários precisem se cadastrar e fazer login no site para criar novos jantares, e somente o usuário que está hospedando um jantar pode editá-lo mais tarde.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner Passo 9: Autenticação e Autorização

Neste momento, nosso aplicativo NerdDinner concede a qualquer um que visite o site a capacidade de criar e editar os detalhes de qualquer jantar. Vamos mudar isso para que os usuários precisem se cadastrar e fazer login no site para criar novos jantares e adicionar uma restrição para que apenas o usuário que está hospedando um jantar possa editá-lo mais tarde.

Para habilitar isso, usaremos autenticação e autorização para garantir nosso aplicativo.

### <a name="understanding-authentication-and-authorization"></a>Entendendo autenticação e autorização

*Autenticação* é o processo de identificação e validação da identidade de um cliente que acessa um aplicativo. Simplificando, trata-se de identificar "quem" é o usuário final quando visita um site. ASP.NET suporta várias maneiras de autenticar usuários do navegador. Para aplicações web da Internet, a abordagem de autenticação mais comum usada é chamada de "Autenticação de formulários". A autenticação de formulários permite que um desenvolvedor autorde um formulário de login HTML dentro de seu aplicativo e, em seguida, valide o nome de usuário/senha que um usuário final envia em um banco de dados ou outra loja de credenciais de senha. Se a combinação de nome de usuário/senha estiver correta, o desenvolvedor pode então pedir a ASP.NET emita um cookie HTTP criptografado para identificar o usuário em solicitações futuras. Usaremos a autenticação de formulários com nosso aplicativo NerdDinner.

*Autorização* é o processo de determinar se um usuário autenticado tem permissão para acessar um URL/recurso específico ou para executar alguma ação. Por exemplo, dentro do nosso aplicativo NerdDinner, queremos autorizar que apenas os usuários que estão conectados possam acessar a URL */Dinners/Create* e criar novos Jantares. Também queremos adicionar lógica de autorização para que apenas o usuário que está hospedando um jantar possa editá-lo – e negar o acesso editar a todos os outros usuários.

### <a name="forms-authentication-and-the-accountcontroller"></a>Autenticação de formulários e o AccountController

O modelo de projeto padrão do Visual Studio para ASP.NET MVC habilita automaticamente a autenticação de formulários quando novos aplicativos mvc ASP.NET são criados. Ele também adiciona automaticamente uma implementação de página de login de conta pré-construída ao projeto – o que torna muito fácil integrar a segurança dentro de um site.

A página padrão Site.master exibe um link "Log On" no canto superior direito do site quando o usuário que a acessa não é autenticado:

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

Clicar no link "Fazer logon" leva um usuário à URL */Account/LogOn:*

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

Os visitantes que não se registraram podem fazê-lo clicando no link "Registrar" – que os levará ao URL */Account/Register* e permitirá que eles insiram os detalhes da conta:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

Clicar no botão "Registrar" criará um novo usuário dentro do sistema de adesão ASP.NET e autenticará o usuário no site usando a autenticação de formulários.

Quando um usuário está logado, o Site.master altera o canto superior direito da página para produzir um "Bem-vindo [nome de usuário]!" mensagem e renderiza um link "Log Off" em vez de um "Log On". Clicando no link "Log Off" loga o usuário:

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

A funcionalidade de login, logout e registro acima é implementada dentro da classe AccountController que foi adicionada ao nosso projeto pelo Visual Studio quando criou o projeto. A ida de usuário do AccountController é implementada usando modelos de exibição dentro do diretório \Views\Account:

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

A classe AccountController usa o sistema ASP.NET Forms Authentication para emitir cookies de autenticação criptografado e a API de associação ASP.NET para armazenar e validar nomes de usuário/senhas. A API de associação ASP.NET é extensível e permite que qualquer loja de credenciais de senha seja usada. ASP.NET navios com implementações incorporadas de provedores de membros que armazenam nome de usuário/senhas dentro de um banco de dados SQL ou dentro do Active Directory.

Podemos configurar qual provedor de membros nosso aplicativo NerdDinner deve usar abrindo o arquivo "web.config" na raiz do projeto e procurando a &lt;seção de adesão&gt; dentro dele. A web.config padrão adicionada quando o projeto foi criado registra o provedor de membros SQL e o configura para usar uma seqüência de conexões chamada "ApplicationServices" para especificar o local do banco de dados.

A seqüência de conexão padrão "ApplicationServices" (especificada na seção &lt;conexãoStrings&gt; do arquivo Web.config) está configurada para usar o SQL Express. Ele aponta para um banco de dados SQL Express chamado "ASPNETDB. MDF" no diretório "App\_Data" do aplicativo. Se esse banco de dados não existir na primeira vez que a API de associação for usada dentro do aplicativo, ASP.NET criará automaticamente o banco de dados e providenciará o esquema de banco de dados de membros apropriado dentro dele:

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

Se, em vez de usar o SQL Express, quiséssemos usar uma instância completa do SQL Server (ou conectar-nos a um banco de dados remoto), tudo o que precisamos fazer é atualizar a seqüência de conexões "ApplicationServices" dentro do arquivo web.config e certificar-se de que o esquema de associação apropriado foi adicionado ao banco de dados em que ele aponta. Você pode executar o\_utilitário "aspnet regsql.exe" dentro do diretório \Windows\Microsoft.NET\Framework\v2.0.50727\ para adicionar o esquema apropriado para a adesão e os outros serviços de aplicativos ASP.NET a um banco de dados.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>Autorizando o /Dinners/Create URL usando o filtro [Autorizar]

Não tivemos que escrever nenhum código para permitir uma autenticação segura e implementação de gerenciamento de contas para o aplicativo NerdDinner. Os usuários podem registrar novas contas com nosso aplicativo e fazer login/logout do site.

Agora podemos adicionar lógica de autorização ao aplicativo, e usar o status de autenticação e o nome de usuário dos visitantes para controlar o que eles podem ou não fazer dentro do site. Vamos começar adicionando lógica de autorização aos métodos de ação "Criar" da nossa classe DinnersController. Especificamente, exigiremos que os usuários que acessem a URL */Dinners/Create* devem estar logados. Se eles não estiverem conectados, vamos redirecioná-los para a página de login para que eles possam fazer login.

Implementar essa lógica é muito fácil. Tudo o que precisamos fazer é adicionar um atributo de filtro [Autorizar] aos nossos métodos de ação Criar assim:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET mVC suporta a capacidade de criar "filtros de ação" que podem ser usados para implementar lógica reutilizável que pode ser aplicada declarativamente aos métodos de ação. O filtro [Autorizar] é um dos filtros de ação incorporados fornecidos por ASP.NET MVC, e permite que um desenvolvedor aplique declarativamente regras de autorização para métodos de ação e classes de controladores.

Quando aplicado sem quaisquer parâmetros (como acima) o filtro [Autorizar] impõe que o usuário que faz a solicitação do método de ação deve estar conectado – e ele redirecionará automaticamente o navegador para a URL de login se não estiver. Ao fazer isso, a URL solicitada originalmente é passada como um argumento de consultastring (por exemplo: /Account/LogOn? ReturnUrl=%2fDinners%2fCreate). Em seguida, o AccountController redirecionará o usuário de volta para a URL originalmente solicitada assim que fizer o login.

O filtro [Autorizar] suporta opcionalmente a capacidade de especificar uma propriedade "Usuários" ou "Funções" que pode ser usada para exigir que o usuário esteja conectado e dentro de uma lista de usuários permitidos ou um membro de uma função de segurança permitida. Por exemplo, o código abaixo só permite que dois usuários específicos, "scottgu" e "billg", acessem a URL /Dinners/Create:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

Incorporar nomes de usuário específicos dentro do código tende a ser bastante insustentável. Uma abordagem melhor é definir "funções" de nível superior que o código verifica e, em seguida, mapear os usuários para a função usando um banco de dados ou um sistema de diretório ativo (permitindo que a lista de mapeamento real do usuário seja armazenada externamente a partir do código). ASP.NET inclui uma API de gerenciamento de função incorporada, bem como um conjunto integrado de provedores de função (incluindo os do SQL e do Active Directory) que podem ajudar a executar esse mapeamento de usuário/função. Poderíamos então atualizar o código para permitir que os usuários dentro de uma função específica de "admin" acessem a URL /Dinners/Create:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>Usando a propriedade User.Identity.Name ao criar jantares

Podemos recuperar o nome de usuário do usuário atualmente conectado de uma solicitação usando a propriedade User.Identity.Name exposta na classe base controller.

Mais cedo, quando implementamos a versão HTTP-POST do nosso método de ação Create() tínhamos codificado a propriedade "HostedBy" do Dinner para uma seqüência estática. Agora podemos atualizar esse código para usar a propriedade User.Identity.Name, bem como adicionar automaticamente um RSVP para o host que cria o Jantar:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Como adicionamos um atributo [Autorizar] ao método Criar(), ASP.NET MVC garante que o método de ação só seja executado se o usuário visitar a URL /Dinners/Create estiver conectado no site. Como tal, o valor User.Identity.Name propriedade sempre conterá um nome de usuário válido.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>Usando a propriedade User.Identity.Name ao editar jantares

Vamos agora adicionar alguma lógica de autorização que restringe os usuários para que eles só possam editar as propriedades dos jantares que eles mesmos estão hospedando.

Para ajudar com isso, adicionaremos primeiro um método de ajuda "IsHostedBy(username)" ao nosso objeto Dinner (dentro da Dinner.cs classe parcial que construímos anteriormente). Este método auxiliar retorna verdadeiro ou falso, dependendo se um nome de usuário fornecido corresponde à propriedade Dinner HostedBy e encapsula a lógica necessária para realizar uma comparação de seqüência de strings insensível a maiúsculas e minúsculas:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

Em seguida, adicionaremos um atributo [Autorizar] aos métodos de ação Editar() dentro da nossa classe DinnersController. Isso garantirá que os usuários estejam conectados para solicitar uma URL */Dinners/Edit/[id].*

Em seguida, podemos adicionar código aos nossos métodos de edição que usam o método de ajuda Dinner.IsHostedBy (nome de usuário) para verificar se o usuário conectado corresponde ao host Jantar. Se o usuário não for o host, exibiremos uma exibição "InvalidOwner" e terminaremos a solicitação. O código para fazer isso parece abaixo:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

Em seguida, podemos clicar com o botão direito do mouse&gt;no diretório \Views\Dinners e escolher o comando Adicionar-Exibir menu para criar uma nova exibição "InvalidOwner". Vamos povoá-lo com a mensagem de erro abaixo:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

E agora, quando um usuário tenta editar um jantar que não possui, ele receberá uma mensagem de erro:

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

Podemos repetir as mesmas etapas para os métodos de ação Excluir() dentro do nosso controlador para bloquear a permissão para excluir jantares também, e garantir que apenas o host de um Jantar possa excluí-lo.

### <a name="showinghiding-edit-and-delete-links"></a>Mostrando/ocultando editar e excluir links

Estamos vinculando ao método de ação Editar e excluir da nossa classe DinnersController a partir de nossa URL Detalhes:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

Atualmente, estamos mostrando os links de ação Editar e Excluir, independentemente de o visitante da URL de detalhes ser o anfitrião do jantar. Vamos mudar isso para que os links só sejam exibidos se o usuário visitante for o dono do jantar.

O método de ação Details() dentro do nosso DinnersController recupera um objeto Dinner e, em seguida, passa-o como o objeto modelo para o nosso modelo de exibição:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

Podemos atualizar nosso modelo de exibição para mostrar/ocultar condicionalmente os links Editar e Excluir usando o método de ajuda Dinner.IsHostedBy() como abaixo:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>Próximas etapas

Vamos agora ver como podemos habilitar usuários autenticados para rsvp para jantares usando AJAX.

> [!div class="step-by-step"]
> [Próximo](implement-efficient-data-paging.md)
> [anterior](use-ajax-to-deliver-dynamic-updates.md)
