---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programação ASP.NET Páginas da Web (Razor) Usando o Visual Studio | Microsoft Docs
author: Rick-Anderson
description: Este apêndice explica como você pode usar o Visual Studio 2010 ou o Visual Web Developer 2010 Express para programar ASP.NET Páginas da Web com a sintaxe Razor.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542892"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Programação ASP.NET Páginas da Web (Razor) usando o Visual Studio

 por [Tom FitzMacken](https://github.com/tfitzmac)

> Este artigo explica como você pode usar o Visual Studio ou visual Web Developer Express para programar ASP.NET sites da Web Pages (Razor).
>
> O que você aprenderá
>
> - O que você precisa instalar (se alguma coisa) para trabalhar com ASP.NET Páginas da Web em sua versão do Visual Studio.
> - Como adicionar suporte para ASP.NET Páginas da Web ao Visual Web Developer 2010 Express.
> - Como usar recursos no Visual Studio para trabalhar com páginas ASP.NET Razor, incluindo o IntelliSense e o depurador.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Versões de software usadas no tutorial
>
>
> - páginas da Web ASP.NET (Navalha) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> Este tutorial também funciona com ASP.NET Páginas web 2, Visual Studio 2012, Visual Studio 2010 e WebMatrix 2.

Você pode programar páginas da Web ASP.NET com sintaxe de Navalha usando WebMatrix ou muitos outros editores de código. Você também pode usar o Microsoft Visual Studio, que é um ambiente de desenvolvimento integrado (IDE) completo que fornece um poderoso conjunto de ferramentas para criar muitos tipos de aplicativos (não apenas sites). Para trabalhar com páginas ASP.NET Razor, você pode usar [o Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

Dois recursos particularmente úteis que o Visual Studio fornece para programação com ASP.NET páginas da Web Razor são:

- *IntelliSense*. O recurso IntelliSense incorporado ao Visual Studio é mais abrangente do que o IntelliSense no WebMatrix.
- *Depurador.* O depurador permite que você solucionem seu código interrompendo um programa enquanto ele está em execução, examinando variáveis e passando pela linha de código por linha.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Usando o Visual Studio com diferentes versões de páginas da Web ASP.NET

Para desenvolver ASP.NET aplicativos web no Visual Studio 2017, instale a carga de trabalho **de ASP.NET e desenvolvimento web.**

Visual Studio 2012 e Visual Studio 2013 incluem suporte para páginas da Web ASP.NET. (Os pacotes necessários para suportar ASP.NET Páginas da Web são instalados quando você instala o Visual Studio.)

O Visual Studio 2010 não inclui suporte por padrão para páginas da Web ASP.NET. Para usar ASP.NET Páginas da Web com o Visual Studio 2010, você deve instalar o pacote mvc ASP.NET. Para obter ASP.NET Páginas da Web 2, você instala ASP.NET MVC 4.

A tabela a seguir resume o suporte para ASP.NET Páginas da Web em diferentes versões do Visual Studio.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **Páginas da Web do ASP.NET 2** | Instalar ASP.NET MVC 4 | (Incluído) | (Incluído) |
| **Páginas da Web do ASP.NET 3** |  | Atualização para ASP.NET Páginas da Web 3 através do NuGet | (Incluído) |

Para trabalhar com o Visual Studio 2010, consulte [Instalando suporte para páginas da Web ASP.NET no Visual Studio 2010](#vs2010support).

## <a name="launching-visual-studio-from-webmatrix"></a>Lançando o Visual Studio da WebMatrix

Se você começou um projeto no WebMatrix e deseja mudar para o Visual Studio, o WebMatrix fornece um botão para abrir facilmente o projeto no Visual Studio. Você deve ter o Visual Studio instalado no seu computador para que este botão seja ativado. A imagem a seguir mostra o botão no WebMatrix.

![lançar Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

Quando você clica no botão, o projeto é aberto no Visual Studio. Você pode alternar para frente e para trás entre webmatrix e visual studio sem quaisquer problemas. Você será notificado se algum arquivo tiver sido alterado no outro ambiente e precisar ser recarregado para obter as últimas alterações.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Criando ASP.NET Razor Site no Visual Studio

Para criar um site ASP.NET Razor no Visual Studio:

1. Abra o Visual Studio.
2. No menu **Arquivo,** clique **em Novo site**.

    ![criar um novo site](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. Na caixa de diálogo **Novo Site,** selecione o idioma a ser usado (Visual C# ou Visual Basic).
4. Selecione o modelo **ASP.NET Site (Razor).**

    ![local de navalha](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. Clique em **OK**.

Seu novo projeto existe e está preenchido com algumas páginas da Web padrão para ajudá-lo a começar.

### <a name="using-intellisense"></a>Usando IntelliSense

Agora que você criou um site, você pode ver como o IntelliSense funciona no Visual Studio.

1. No site que você acabou de criar, abra a página *Default.cshtml.*
2. Após `<h3>` as tags na `@ServerInfo.` página, digite (incluindo o dot). Observe como o IntelliSense exibe `ServerInfo` os métodos disponíveis para o ajudante em uma lista de baixa.

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. Selecione `GetHtml` o método na lista e, em seguida, pressione Enter. O IntelliSense preenche automaticamente o método. (Como em qualquer método em C#, você deve adicionar `()` caracteres após o método.) O código completo `GetHtml` para o método parece o seguinte exemplo:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Pressione Ctrl+F5 para executar a página. É assim que a página se parece quando exibida em um navegador:

    ![página padrão no navegador](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. Feche o navegador.

### <a name="using-the-debugger"></a>Usando o Depurador

1. Na parte superior da página *Default.cshtml,* após `Page.Title`a linha que começa com , adicione a seguinte linha de código:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. Na margem cinza do editor à esquerda do código, clique ao lado desta nova linha para adicionar um *ponto de ruptura*. Um ponto de ruptura é um marcador que diz ao depurador para parar de executar o programa nesse ponto para que você possa ver o que está acontecendo.

    ![definir ponto de interrupção](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. Remova a chamada `ServerInfo.GetHtml` para o método e `@myTime` adicione uma chamada à variável em seu lugar. Esta chamada exibe o valor de tempo atual que é devolvido pela nova linha de código.
4. Pressione F5 para executar a página no depurador. A página pára no ponto de partida que você definiu. A imagem a seguir mostra como a página se parece no editor com o ponto de partida (em amarelo).

    ![ponto de ruptura depuração](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. Na barra de ferramentas Debug, clique no botão **Passo a passo** (ou pressione F11) para executar a próxima linha de código. Cada vez que você clica neste botão, você avança a execução para a próxima linha de código.

    ![Passo no botão](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. Examine o valor `myTime` da variável segurando o ponteiro do mouse sobre ele ou inspecionando os valores **exibidos** nas janelas Locals e **Call Stack.** Visual Studio exibe o valor da variável.

    ![mostrar valor do tempo](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. Quando terminar de examinar a variável e passar pelo código, pressione F5 para continuar executando a página sem parar em cada linha. Quando você terminar de passar por todo o código, o navegador exibe a página.

Para saber mais sobre o depurador e sobre como depurar código no Visual Studio, consulte [Passo a Passo: Depurando Páginas da Web no Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Usando razor em ASP.NET projetos de MVC com Visual Studio

A sintaxe Razor também é usada extensivamente em ASP.NET projetos de MVC. O MVC é uma maneira poderosa e baseada em padrões de construir sites dinâmicos. Se o seu site de páginas da ASP.NET se tornar difícil de manter, você pode querer considerar convertê-lo em um aplicativo mvc ASP.NET. Para um exemplo de criação de um aplicativo MVC, consulte [Getting Started com ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Instalando suporte para páginas da Web ASP.NET no Visual Studio 2010

Esta seção mostra como instalar o Visual Web Developer Express 2010 e o ASP.NET Web Pages Tools para o Visual Studio.

1. Se você ainda não tiver o Instalador de Plataforma web, baixe-o na seguinte URL:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Execute o Instalador de Plataforma Web.
3. Clique na guia **Produtos.**

    ![Guia Produtos WebPI](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. Procure **por ASP.NET MVC 4** (para ASP.NET Páginas da Web 2) e clique em **Adicionar**. Esses produtos incluem ferramentas do Visual Studio para construir sites ASP.NET Razor.

    ![Opções de instalação do WebPi](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. Clique **em Instalar** para concluir a instalação.
