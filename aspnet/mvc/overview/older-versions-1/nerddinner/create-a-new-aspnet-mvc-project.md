---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Criar um Novo Projeto ASP.NET MVC | Microsoft Docs
author: rick-anderson
description: O passo 1 mostra como colocar a estrutura básica do aplicativo NerdDinner no lugar.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541475"
---
# <a name="create-a-new-aspnet-mvc-project"></a>Criar um novo projeto do ASP.NET MVC

pela [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Este é o passo 1 de um tutorial gratuito do [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que mostra como construir um pequeno, mas completo, aplicativo web usando ASP.NET MVC 1.
> 
> O passo 1 mostra como colocar a estrutura básica do aplicativo NerdDinner no lugar.
> 
> Se você estiver usando ASP.NET MVC 3, recomendamos que você siga os tutoriais da [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner Passo 1:&gt;Arquivo- Novo Projeto

Começaremos nosso aplicativo NerdDinner selecionando o item do menu **File-&gt;New Project** dentro do Visual Studio 2008 ou do Visual Web Developer 2008 Express gratuito.

Isso trará à tona o diálogo "Novo Projeto". Para criar um novo aplicativo mvc ASP.NET, selecionaremos o nó "Web" no lado esquerdo da caixa de diálogo e, em seguida, escolheremos o modelo de projeto "ASP.NET MVC Web Application" à direita:

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*Importante: Certifique-se de que você baixou e instalou ASP.NET MVC - caso contrário, ele não aparecerá na caixa de diálogo Do Novo Projeto. Você pode usar o V2 do [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) se ainda não o tiver instalado&gt;(ASP.NET MVC está disponível na seção "Plataforma web- Frameworks e Runtimes").*

Vamos nomear o novo projeto que vamos criar "NerdDinner" e, em seguida, clique no botão "ok" para criá-lo.

Quando clicarmos em "ok" o Visual Studio trará uma caixa de diálogo adicional que nos leva a criar opcionalmente um projeto de teste de unidade para o novo aplicativo também. Este projeto de teste unitário nos permite criar testes automatizados que verifiquem a funcionalidade e o comportamento do nosso aplicativo (algo que abordaremos como fazer mais tarde neste tutorial).

![](create-a-new-aspnet-mvc-project/_static/image2.png)

A lista suspensa "Test framework" na caixa de diálogo acima está preenchida com todos os modelos de projeto de teste de unidade ASP.NET mVC disponíveis instalados na máquina. As versões podem ser baixadas para NUnit, MBUnit e XUnit. A estrutura de teste da unidade visual incorporada também é suportada.

*Nota: O Visual Studio Unit Test Framework só está disponível com versões profissionais e superiores do Visual Studio 2008. Se você estiver usando vs 2008 Standard Edition ou Visual Web Developer 2008 Express, você precisará baixar e instalar as extensões NUnit, MBUnit ou XUnit para ASP.NET MVC para que esta caixa de diálogo seja mostrada. A caixa de diálogo não será exibida se não houver nenhuma estrutura de teste instalada.*

Usaremos o nome padrão "NerdDinner.Tests" para o projeto de teste que criamos e usaremos a opção de framework "Visual Studio Unit Test". Quando clicarmos no botão "ok" o Visual Studio criará uma solução para nós com dois projetos nele - um para nossa aplicação web e outro para nossos testes unitários:

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>Examinando a estrutura do diretório NerdDinner

Quando você cria um novo aplicativo mvc ASP.NET com o Visual Studio, ele adiciona automaticamente uma série de arquivos e diretórios ao projeto:

![](create-a-new-aspnet-mvc-project/_static/image4.png)

ASP.NET projetos de MVC por padrão têm seis diretórios de nível superior:

| **Diretório** | **Finalidade** |
| --- | --- |
| **/Controladores** | Onde você coloca classes de controlador que lidam com solicitações de URL |
| **/Modelos** | Onde você coloca classes que representam e manipulam dados |
| **/Visualizações** | Onde você coloca arquivos de modelo de UI que são responsáveis pela renderização de saída |
| **/Scripts** | Onde você coloca arquivos e scripts da biblioteca JavaScript (.js) |
| **/Conteúdo** | Onde você coloca CSS e arquivos de imagem, e outros conteúdos não dinâmicos/não-JavaScript |
| **/Dados\_do aplicativo** | Onde você armazena arquivos de dados que deseja ler/gravar. |

ASP.NET MVC não requer essa estrutura. Na verdade, os desenvolvedores que trabalham em grandes aplicativos normalmente particionam o aplicativo em vários projetos para torná-lo mais gerenciável (por exemplo: classes de modelos de dados geralmente vão em um projeto de biblioteca de classes separado do aplicativo web). A estrutura padrão do projeto, no entanto, fornece uma agradável convenção de diretório padrão que podemos usar para manter nossas preocupações de aplicativos limpas.

Quando expandimos o diretório /Controladores, descobriremos que o Visual Studio adicionou duas classes de controlador – HomeController e AccountController – por padrão ao projeto:

![](create-a-new-aspnet-mvc-project/_static/image5.png)

Quando expandimos o diretório /Views, encontraremos três subdiretórios – /Home, /Account e /Shared – bem como vários arquivos de modelo dentro deles também foram adicionados ao projeto por padrão:

![](create-a-new-aspnet-mvc-project/_static/image6.png)

Quando expandimos os diretórios /Conteúdo e /Scripts, encontraremos um arquivo Site.css que é usado para estilizar todos os HTML no site, bem como bibliotecas JavaScript que podem habilitar ASP.NET suporte a AJAX e jQuery dentro do aplicativo:

![](create-a-new-aspnet-mvc-project/_static/image7.png)

Quando expandimos o projeto NerdDinner.Tests, encontraremos duas classes que contêm testes unitários para nossas classes de controlador:

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Esses arquivos padrão adicionados pelo Visual Studio nos fornecem uma estrutura básica para um aplicativo de trabalho - completa com página inicial, sobre página, páginas de login/logout/registro da conta e uma página de erro não manipulada (tudo conectado e funcionando fora da caixa).

### <a name="running-the-nerddinner-application"></a>Executando o aplicativo NerdDinner

Podemos executar o projeto escolhendo os itens do **menu Debug-Start&gt;** ou **&gt;Debug- Start sem depuração** de itens do menu:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

Isso iniciará o servidor web integrado ASP.NET que vem com o Visual Studio e executará nosso aplicativo:

![](create-a-new-aspnet-mvc-project/_static/image10.png)

Abaixo está a página inicial do nosso novo projeto (URL: "/") quando ele é executado:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

Clicar na guia "Sobre" exibe uma página sobre (URL: "/Home/About"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

Clicar no link "Fazer logon" no canto superior direito nos leva a uma página de login (URL: "/Account/LogOn")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

Se não tivermos uma conta de login, podemos clicar no link de registro (URL: "/Account/Register") para criar um:

![](create-a-new-aspnet-mvc-project/_static/image14.png)

O código para implementar a funcionalidade de home, about e logout/register foi adicionado por padrão quando criamos nosso novo projeto. Vamos usá-lo como ponto de partida da nossa aplicação.

### <a name="testing-the-nerddinner-application"></a>Testando o aplicativo NerdDinner

Se estivermos usando a Edição Profissional ou a versão superior do Visual Studio 2008, podemos usar o suporte de teste de unidade incorporada do IDE dentro do Visual Studio para testar o projeto:

![](create-a-new-aspnet-mvc-project/_static/image15.png)

A escolha de uma das opções acima abrirá o painel "Resultados de Teste" dentro do IDE e nos fornecerá status de aprovação/falha nos testes de 27 unidades incluídos em nosso novo projeto que abrangem a funcionalidade incorporada:

![](create-a-new-aspnet-mvc-project/_static/image16.png)

Mais tarde, neste tutorial, falaremos mais sobre testes automatizados e adicionaremos testes adicionais de unidade que cobrem a funcionalidade do aplicativo que implementamos.

### <a name="next-step"></a>Próxima etapa

Agora temos uma estrutura básica de aplicação. Vamos agora criar um banco de [dados para armazenar nossos dados de aplicativos.](create-a-database.md)

> [!div class="step-by-step"]
> [Próximo](introducing-the-nerddinner-tutorial.md)
> [anterior](create-a-database.md)
