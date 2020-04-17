---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Criando um aplicativo MVC 3 com Razor e JavaScript discreto | Microsoft Docs
author: rick-anderson
description: O aplicativo web de amostra de lista de usuário demonstra o quão simples é criar ASP.NET aplicativos MVC 3 usando o mecanismo razor view. A aplicação da amostra...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542450"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Criação de um aplicativo do MVC 3 com Razor e JavaScript não obstrusivo

pela [Microsoft](https://github.com/microsoft)

> O aplicativo web de amostra de lista de usuário demonstra o quão simples é criar ASP.NET aplicativos MVC 3 usando o mecanismo razor view. O aplicativo de exemplo mostra como usar o novo mecanismo razor view com ASP.NET mvc versão 3 e Visual Studio 2010 para criar um site fictício da Lista de Usuários que inclui funcionalidades como criação, exibição, edição e exclusão de usuários.
> 
> Este tutorial descreve as etapas que foram tomadas para construir a amostra da Lista de Usuários ASP.NET aplicativo MVC 3. Um projeto do Visual Studio com código fonte C# e VB está disponível para acompanhar este tópico: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114). Se você tiver dúvidas sobre este tutorial, por favor, poste-as no [fórum MVC](https://forums.asp.net/1146.aspx).

## <a name="overview"></a>Visão geral

O aplicativo que você estará construindo é um site de lista de usuários simples. Os usuários podem inserir, visualizar e atualizar as informações do usuário.

![Local da amostra](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

Você pode baixar o projeto vb e c# concluído [aqui](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).

## <a name="creating-the-web-application"></a>Criando o Aplicativo web

Para iniciar o tutorial, abra o Visual Studio 2010 e crie um novo projeto usando o modelo *de aplicativo web ASP.NET MVC 3.* Nomeie &quot;o aplicativo&quot;Mvc3Razor .

[![Novo projeto MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

Na caixa de diálogo **Projeto MVC 3 do Novo ASP.NET,** selecione **Aplicativo da Internet,** selecione o mecanismo de exibição de Navalha e clique em **OK**.

![Diálogo do Projeto MVC 3 do novo ASP.NET](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

Neste tutorial você não estará usando o provedor de associação ASP.NET, para que você possa excluir todos os arquivos associados ao logon e associação. No **Solution Explorer,** remova os seguintes arquivos e diretórios:

- *Controladores\AccountController*
- *Modelos\Modelos de conta*
- *Visualizações\_LogOnPartial\\compartilhadas*
- *Visualizações\Conta* (e todos os arquivos neste diretório)

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

Edite `<div>` o `logindisplay` <em>&quot;</em>&quot; <em> \_arquivo Layout.cshtml</em> e substitua a marcação dentro do elemento nomeado com a mensagem Login Desativado . O exemplo a seguir mostra a nova marcação:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>Adicionando o Modelo

No **Solution Explorer,** clique com o botão direito do mouse na pasta *Modelos,* selecione **Adicionar**e clique em **Classe**.

![Nova classe Mdl do usuário](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

Nome da classe `UserModel`. Substitua o conteúdo do arquivo *UserModel* pelo seguinte código:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

A `UserModel` classe representa os usuários. Cada membro da classe é anotado com o atributo [Obrigatório](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) do namespace [DataAnnotations.](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) Os atributos no [namespace DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) fornecem validação automática do lado do cliente e do servidor para aplicativos web.

Abra `HomeController` a classe `using` e adicione uma diretiva `UserModel` para `Users` que você possa acessar as aulas e as classes:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

Logo após `HomeController` a declaração, adicione o `Users` seguinte comentário e a referência a uma classe:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

A `Users` classe é um armazenamento de dados simplificado na memória que você usará neste tutorial. Em um aplicativo real, você usaria um banco de dados para armazenar informações do usuário. As primeiras linhas `HomeController` do arquivo são mostradas no seguinte exemplo:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

Construa o aplicativo para que o modelo do usuário esteja disponível para o assistente de andaimes na próxima etapa.

## <a name="creating-the-default-view"></a>Criando a exibição padrão

O próximo passo é adicionar um método de ação e exibição para exibir os usuários.

Exclua o arquivo *Views\Home\Index* existente. Você criará um novo *arquivo Index* para exibir os usuários.

Na `HomeController` classe, substitua o `Index` conteúdo do método pelo seguinte código:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

Clique com o `Index` botão direito do mouse dentro do método e clique em **Adicionar exibição**.

![Adicionar visualização](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

Selecione a Opção Criar uma opção **de exibição fortemente digitada.** Para **exibir classe de dados,** selecione **Mvc3Razor.Models.UserModel**. (Se você não ver **Mvc3Razor.Models.UserModel** na caixa **de classe de dados Exibir,** você precisa construir o projeto.) Certifique-se de que o motor de exibição está definido como **Razor**. Defina **exibir conteúdo** para **Lista** e clique **em Adicionar**.

![Adicionar visualização de índice](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

A nova exibição desarma automaticamente os dados do `Index` usuário que são passados para a exibição. Examine o arquivo *Visualizações\Home\Index* recém-gerado. Os links **Criar novo,** **editar,** **editar**e **excluir** não funcionam, mas o resto da página está funcional. Execute a página. Você vê uma lista de usuários.

![Página do Índice](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

Abra o arquivo *Index.cshtml* e `ActionLink` substitua a marcação para **Editar**, **Detalhes**e **Excluir** com o seguinte código:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

O nome de usuário é usado como ID para encontrar o registro selecionado nos links **Editar,** **Detalhes**e **Excluir.**

## <a name="creating-the-details-view"></a>Criando a exibição de detalhes

O próximo passo é `Details` adicionar um método de ação e visualização para exibir os detalhes do usuário.

![Detalhes](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

Adicione o `Details` seguinte método ao controlador doméstico:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

Clique com o `Details` botão direito do mouse dentro do método e selecione <strong>Adicionar exibição</strong>. Verifique se a caixa <strong>de classe de dados Exibir</strong> contém <strong>Mvc3Razor.Models.UserModel</strong><em>.</em> Defina <strong>o conteúdo de exibição</strong> para <strong>Detalhes</strong> e clique <strong>em Adicionar</strong>.

![Adicionar visualização de detalhes](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

Execute o aplicativo e selecione um link de detalhes. O andaime automático mostra cada propriedade no modelo.

![Detalhes](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>Criando a exibição editar

Adicione o `Edit` seguinte método ao controlador doméstico.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

Adicione uma exibição como nas etapas anteriores, mas defina **exibir conteúdo** para **Editar**.

![Adicionar exibição editar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

Execute o aplicativo e edite o primeiro e sobrenome de um dos usuários. Se você `DataAnnotation` violar quaisquer restrições que `UserModel` tenham sido aplicadas à classe, ao enviar o formulário, verá erros de validação que são produzidos pelo código do servidor. Por exemplo, se você &quot;alterar&quot; &quot;o&quot;primeiro nome Ann para A, quando você enviar o formulário, o seguinte erro será exibido no formulário:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

Neste tutorial, você está tratando o nome de usuário como a chave principal. Portanto, a propriedade do nome do usuário não pode ser alterada. No arquivo *Edit.cshtml,* logo `Html.BeginForm` após a declaração, defina o nome de usuário como um campo oculto. Isso faz com que a propriedade seja aprovada no modelo. O fragmento de código a `Hidden` seguir mostra a colocação da declaração:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

Substitua `TextBoxFor` `ValidationMessageFor` a marcação e a `DisplayFor` marcação para o nome de usuário por uma chamada. O `DisplayFor` método exibe a propriedade como um elemento somente leitura. O exemplo a seguir mostra a marcação concluída. O `TextBoxFor` original `ValidationMessageFor` e as chamadas são comentados com os`@* *@`caracteres de início de navalha e comentários finais ( )

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>Habilitando a validação do lado do cliente

Para habilitar a validação do lado do cliente em ASP.NET MVC 3, você deve definir dois sinalizadores e deve incluir três arquivos JavaScript.

Abra o arquivo *Web.config* do aplicativo. Verifique `that ClientValidationEnabled` `UnobtrusiveJavaScriptEnabled` e esteja definido como verdadeiro nas configurações do aplicativo. O fragmento a seguir do arquivo *root Web.config* mostra as configurações corretas:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

A `UnobtrusiveJavaScriptEnabled` configuração para true permite a validação discreta do Ajax e do cliente discreto. Quando você usa validação discreta, as regras de validação são transformadas em atributos HTML5. Os nomes de atributos HTML5 podem consistir apenas em letras minúsculas, números e traços.

A `ClientValidationEnabled` configuração para true permite a validação do lado do cliente. Ao definir essas chaves no arquivo *Web.config* do aplicativo, você habilita a validação do cliente e o JavaScript discreto para todo o aplicativo. Você também pode habilitar ou desativar essas configurações em visualizações individuais ou em métodos de controlador usando o seguinte código:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

Você também precisa incluir vários arquivos JavaScript na exibição renderizada. Uma maneira fácil de incluir o JavaScript em todas as exibições é adicioná-los ao arquivo *Views\Shared\\_Layout.cshtml.* Substitua `<head>` o * \_* elemento do arquivo Layout.cshtml pelo seguinte código:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

Os dois primeiros scripts jQuery são hospedados pela Microsoft Ajax Content Delivery Network (CDN). Aproveitando o CDN do Microsoft Ajax, você pode melhorar significativamente o desempenho de primeiro hit de seus aplicativos.

Execute o aplicativo e clique em um link de edição. Veja a fonte da página no navegador. A fonte do navegador mostra `data-val` muitos atributos do formulário (para validação de dados). Quando a validação do cliente e o JavaScript discreto são habilitados, os `data-val="true"` campos de entrada com uma regra de validação do cliente contêm o atributo para desencadear a validação discreta do cliente. Por exemplo, `City` o campo no modelo foi decorado com o atributo [Obrigatório,](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) o que resulta no HTML mostrado no exemplo a seguir:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

Para cada regra de validação do cliente, `data-val-rulename="message"`é adicionado um atributo que tem o formulário . Usando `City` o exemplo de campo mostrado anteriormente, `data-val-required` a regra &quot;de validação&quot;do cliente necessária gera o atributo e a mensagem O campo Cidade é necessário . Execute o aplicativo, edite um dos `City` usuários e limpe o campo. Quando você faz a guia para fora do campo, você vê uma mensagem de erro de validação do lado do cliente.

![Cidade necessária](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

Da mesma forma, para cada parâmetro na regra de validação do `data-val-rulename-paramname=paramvalue`cliente, é adicionado um atributo que tem o formulário . Por exemplo, `FirstName` a propriedade é anotada com o atributo [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) e especifica um comprimento mínimo de 3 e um comprimento máximo de 8. A regra de `length` validação de `max` dados nomeada tem o nome do parâmetro e o valor do parâmetro 8. A seguir, mostra o HTML `FirstName` gerado para o campo quando você edita um dos usuários:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

Para obter mais informações sobre validação de clientes discretas, consulte a entrada [Validação de ClienteS Discretas em ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) no blog de Brad Wilson.

> [!NOTE]
> Em ASP.NET MVC 3 Beta, às vezes você precisa enviar o formulário para iniciar a validação do lado do cliente. Isso pode ser alterado para a versão final.

## <a name="creating-the-create-view"></a>Criando a visualização de criação

O próximo passo é `Create` adicionar um método de ação e visualização para permitir que o usuário crie um novo usuário. Adicione o `Create` seguinte método ao controlador doméstico:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

Adicione uma exibição como nas etapas anteriores, mas defina **exibir conteúdo** para **Criar**.

![Criar exibição](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

Execute o aplicativo, selecione o link **Criar** e adicione um novo usuário. O `Create` método aproveita automaticamente a validação do lado do cliente e do lado do servidor. Tente inserir um nome de usuário que &quot;contenha espaço em branco, como Ben X&quot;. Quando você faz a guia para fora do campo`White space is not allowed`nome de usuário, um erro de validação do lado do cliente () é exibido.

## <a name="add-the-delete-method"></a>Adicionar o método Excluir

Para completar o tutorial, `Delete` adicione o seguinte método ao controlador doméstico:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

Adicionar `Delete` uma exibição como nas etapas anteriores, definindo **Exibir conteúdo** para **Excluir**.

![Excluir Exibição](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

Agora você tem um aplicativo simples, mas totalmente funcional ASP.NET MVC 3 com validação.
