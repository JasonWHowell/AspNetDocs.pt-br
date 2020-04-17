---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Usando um site CAPTCHA para impedir que bots usem seu ASP.NET Web Razor) site | Microsoft Docs
author: rick-anderson
description: Este artigo explica como usar o ReCaptcha (uma medida de segurança) para impedir que programas automatizados (bots) realizem tarefas em uma ASP.NET Páginas da Web (Razor) nós...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543750"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>Usando um site CAPTCHA para impedir que bots usem o seu ASP.NET Web Razor)

pela [Microsoft](https://github.com/microsoft)

> Este artigo explica como usar o ReCaptcha (uma medida de segurança) para impedir que programas automatizados (bots) realizem tarefas em um site de páginas da Web ASP.NET (Razor).
> 
> **O que você aprenderá:** 
> 
> - Como adicionar um teste CAPTCHA ao seu site.
> 
> Estas são as ASP.NET características introduzidas no artigo:
> 
> - O `ReCaptcha` ajudante.
> 
> > [!NOTE]
> > As informações deste artigo se aplicam a ASP.NET Páginas da Web 1.0 e páginas da Web 2.

## <a name="about-captchas"></a>Sobre a CAPTCHAs

Sempre que você permite que as pessoas se registrem em seu site, ou mesmo apenas digite um nome e URL (como para um comentário de blog), você pode obter uma enxurrada de nomes falsos. Estes são muitas vezes deixados por programas automatizados (bots) que tentam deixar URLs em todos os sites que podem encontrar. (Uma motivação comum é colocar os URLs de produtos à venda.)

Você pode ajudar a garantir que um usuário seja uma pessoa real e não um programa de computador usando um *CAPTCHA* para validar os usuários quando eles se registram ou digitam seu nome e site. CAPTCHA significa teste de Turing público completamente automatizado para diferenciar computadores e humanos. Um CAPTCHA é um teste *de resposta a desafios* no qual o usuário é solicitado a fazer algo que é fácil para uma pessoa fazer, mas difícil para um programa automatizado fazer. O tipo mais comum de CAPTCHA é aquele em que você vê algumas letras distorcidas e é solicitado a digitá-las. (A distorção deve dificultar a decifração das letras pelos bots.)

## <a name="adding-a-recaptcha-test"></a>Adicionando um teste de ReCaptcha

Em ASP.NET páginas, você `ReCaptcha` pode usar o ajudante para renderizar um teste[http://recaptcha.net](http://recaptcha.net)CAPTCHA baseado no serviço ReCaptcha ( ). O `ReCaptcha` ajudante exibe uma imagem de duas palavras distorcidas que os usuários têm que inserir corretamente antes que a página seja validada. A resposta do usuário é validada pelo serviço ReCaptcha.Net.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Cadastre-se[http://recaptcha.net](http://recaptcha.net)no seu site em ReCaptcha.Net ( ). Quando você concluir o registro, você terá uma chave pública e uma chave privada.
2. Adicione a biblioteca ASP.NET de ajudantes da Web ao seu site, conforme descrito na [instalação de ajudantes em um site de páginas da ASP.NET,](https://go.microsoft.com/fwlink/?LinkId=252372)se você ainda não tiver.
3. Se você ainda não tiver um * \_arquivo AppStart.cshtml,* na pasta raiz de um site crie um arquivo chamado * \_AppStart.cshtml*.
4. Adicione as `Recaptcha` seguintes configurações de ajuda no * \_arquivo AppStart.cshtml:* 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. Defina `PublicKey` `PrivateKey` as propriedades usando suas próprias chaves públicas e privadas.
6. Salve o arquivo * \_AppStart.cshtml* e feche-o.
7. Na pasta raiz de um site, crie uma nova página chamada *Recaptcha.cshtml*.
8. Substitua o conteúdo existente pelo seguinte: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. Execute a página *Recaptcha.cshtml* em um navegador. Se `PrivateKey` o valor for válido, a página exibirá o controle ReCaptcha e um botão. Se você não tivesse definido as teclas globalmente no * \_AppStart.html,* a página exibiria um erro. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. Digite as palavras para o teste. Se você passar no teste ReCaptcha, verá uma mensagem nesse sentido. Caso contrário, você verá uma mensagem de erro e o controle ReCaptcha será reexibido.

> [!NOTE]
> Se o computador estiver em um domínio que usa servidor `defaultproxy` proxy, talvez seja necessário configurar o elemento do arquivo *Web.config.* O exemplo a seguir mostra um `defaultproxy` arquivo *Web.config* com o elemento configurado para permitir que o serviço ReCaptcha funcione.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Recursos adicionais

- [Personalizando o comportamento em todo o site para sites de páginas da Web ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202906)
- [Site do ReCaptcha](https://www.google.com/recaptcha)
