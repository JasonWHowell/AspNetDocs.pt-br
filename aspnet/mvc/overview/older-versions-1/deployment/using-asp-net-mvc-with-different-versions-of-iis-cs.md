---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: Usando ASP.NET MVC com diferentes versões do IIS (C#) | Microsoft Docs
author: rick-anderson
description: Neste tutorial, você aprende a usar ASP.NET MVC e ROTEAmento de URL, com diferentes versões dos Serviços de Informação da Internet. Você aprende estratégias diferentes...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c239c3c7cbbaae5d9c5e4dd91dc66ff4e98bcfb
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542073"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a>Uso do ASP.NET MVC com diferentes versões de IIS (C#)

pela [Microsoft](https://github.com/microsoft)

> Neste tutorial, você aprende a usar ASP.NET MVC e ROTEAmento de URL, com diferentes versões dos Serviços de Informação da Internet. Você aprende diferentes estratégias para usar ASP.NET MVC com IIS 7.0 (modo clássico), IIS 6.0 e versões anteriores do IIS.

A ASP.NET estrutura MVC depende do roteamento ASP.NET para direcionar as solicitações do navegador às ações do controlador. Para aproveitar ASP.NET Roteamento, você pode ter que executar etapas adicionais de configuração em seu servidor web. Tudo depende da versão do Internet Information Services (IIS) e do modo de processamento de solicitação para o seu aplicativo.

Aqui está um resumo das diferentes versões do IIS:

- IIS 7.0 (modo integrado) - Não é necessária uma configuração especial para usar ASP.NET Roteamento.
- IIS 7.0 (modo clássico) - Você precisa executar configuração especial para usar ASP.NET Roteamento.
- IIS 6.0 ou abaixo - Você precisa executar configuração especial para usar ASP.NET Roteamento.

A versão mais recente do IIS é a versão 7.5 (no Win7). O IIS 7 do IIS está incluído no Windows Server 2008 e VISTA/SP1 e superior. Você também pode instalar o IIS 7.0 em qualquer versão [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)do sistema operacional Vista, exceto Home Basic (ver ).

O IIS 7.0 suporta dois modos para processar solicitações. Você pode usar o modo integrado ou o modo clássico. Você não precisa executar nenhuma etapa de configuração especial ao usar o IIS 7.0 no modo integrado. No entanto, você precisa executar configuração adicional ao usar o IIS 7.0 no modo clássico.

O Microsoft Windows Server 2003 inclui o IIS 6.0. Não é possível atualizar o IIS 6.0 para o IIS 7.0 ao usar o sistema operacional Windows Server 2003. Você deve executar etapas adicionais de configuração ao usar o IIS 6.0.

O Microsoft Windows XP Professional inclui o IIS 5.1. Você deve executar etapas adicionais de configuração ao usar o IIS 5.1.

Finalmente, o Microsoft Windows 2000 e o Microsoft Windows 2000 Professional incluem o IIS 5.0. Você deve executar etapas adicionais de configuração ao usar o IIS 5.0.

## <a name="integrated-versus-classic-mode"></a>Modo Integrado versus Clássico

O IIS 7.0 pode processar solicitações usando dois modos diferentes de processamento de solicitação: integrado e clássico. O modo integrado proporciona melhor desempenho e mais recursos. O modo clássico está incluído para retrocompatibilidade com versões anteriores do IIS.

O modo de processamento da solicitação é determinado pelo pool de aplicativos. Você pode determinar qual modo de processamento está sendo usado por um aplicativo web específico, determinando o pool de aplicativos associado ao aplicativo. Siga estas etapas:

1. Inicie o Gerenciador de Serviços de Informação da Internet
2. Na janela Conexões, selecione um aplicativo
3. Na janela Ações, clique no link **Configurações básicas** para abrir a caixa de diálogo Editar aplicativo (ver Figura 1)
4. Anote o pool de aplicativos selecionado.

Por padrão, o IIS está configurado para suportar dois pools de aplicativos: **DefaultAppPool** e **Classic .NET AppPool**. Se DefaultAppPool estiver selecionado, seu aplicativo será executado no modo de processamento integrado de solicitações. Se o Classic .NET AppPool for selecionado, seu aplicativo será executado no modo clássico de processamento de solicitações.

[![A caixa de diálogo Novo Projeto](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)

**Figura 1**: Detectando o modo de processamento de solicitação[(Clique para exibir a imagem em tamanho real)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png)

Observe que você pode modificar o modo de processamento de solicitações na caixa de diálogo Editar aplicativo. Clique no botão Selecionar e altere o pool de aplicativos associado ao aplicativo. Perceba que há problemas de compatibilidade ao alterar um aplicativo ASP.NET do modo clássico para o integrado. Para obter mais informações, consulte os seguintes artigos:

- Atualizando ASP.NET 1.1 para o IIS 7.0 no Windows Vista e no Windows Server 2008 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)
- ASP.NET Integração com o IIS 7.0 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

Se um aplicativo ASP.NET estiver usando o DefaultAppPool, então você não precisa executar nenhuma etapa adicional para que ASP.NET Roteamento (e, portanto, ASP.NET MVC) funcione. No entanto, se o aplicativo ASP.NET estiver configurado para usar o Classic .NET AppPool e continuar lendo, você terá mais trabalho a fazer.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>Usando ASP.NET MVC com versões mais antigas do IIS

Se você precisa usar ASP.NET MVC com uma versão mais antiga do IIS do que o IIS 7.0, ou você precisa usar o IIS 7.0 no modo clássico, então você tem duas opções. Primeiro, você pode modificar a tabela de rota para usar extensões de arquivo. Por exemplo, em vez de solicitar uma URL como /Store/Details, você solicitaria uma URL como /Store.aspx/Details.

A segunda opção é criar algo chamado *mapa de script curinga.* Um mapa de script curinga permite mapear cada solicitação na estrutura ASP.NET.

Se você não tiver acesso ao seu servidor web (por exemplo, seu aplicativo mvc ASP.NET está sendo hospedado por um provedor de serviços de Internet) então você precisará usar a primeira opção. Se você não quiser modificar a aparência de seus URLs e tiver acesso ao seu servidor web, então você pode usar a segunda opção.

Exploramos cada opção em detalhes nas seções a seguir.

## <a name="adding-extensions-to-the-route-table"></a>Adicionando extensões à tabela de rotas

A maneira mais fácil de obter ASP.NET Roteamento para trabalhar com versões mais antigas do IIS é modificar sua tabela de rotas no arquivo Global.asax. O arquivo Global.asax padrão e não modificado na Listagem 1 configura uma rota chamada de rota Padrão.

**Listagem 1 - Global.asax (não modificado)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

A rota Padrão configurada na Listagem 1 permite que você roteie URLs que se parecem com isso:

/Home/Índice

/Produto/Detalhes/3

/Produto

Infelizmente, as versões mais antigas do IIS não passarão esses pedidos para o quadro ASP.NET. Portanto, essas solicitações não serão encaminhadas para um controlador. Por exemplo, se você fizer uma solicitação do navegador para a URL /Home/Index, então você terá a página de erro na Figura 2.

[![A caixa de diálogo Novo Projeto](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)

**Figura 2**: Receber um erro 404 Não Encontrado[(Clique para exibir a imagem em tamanho real](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))

Versões mais antigas do IIS apenas mapeiam certas solicitações para o ASP.NET quadro. A solicitação deve ser para uma URL com a extensão de arquivo certa. Por exemplo, uma solicitação de /SomePage.aspx é mapeada para a estrutura ASP.NET. No entanto, uma solicitação de /SomePage.htm não.

Portanto, para que ASP.NET roteamento funcione, devemos modificar a rota Padrão para que ela inclua uma extensão de arquivo mapeada para o ASP.NET framework.

Isso é feito usando `registermvc.wsf`um script chamado . Foi incluído no lançamento ASP.NET MVC 1, `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`mas a partir de ASP.NET 2 este [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)script foi movido para o ASP.NET Futures, disponível em .

A execução deste script registra uma nova extensão .mvc com o IIS. Depois de registrar a extensão .mvc, você pode modificar suas rotas no arquivo Global.asax para que as rotas usem a extensão .mvc.

O arquivo Global.asax modificado na Listagem 2 funciona com versões mais antigas do IIS.

**Listagem 2 - Global.asax (modificado com extensões)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

**Importante**: lembre-se de construir seu ASP.NET aplicativo MVC novamente depois de alterar o arquivo Global.asax.

Existem duas alterações importantes no arquivo Global.asax na Listagem 2. Existem agora duas rotas definidas no Global.asax. O padrão de URL para a rota Padrão, a primeira rota, agora parece:

{controller}.mvc/{action}/{id}

A adição da extensão .mvc altera o tipo de arquivos que o módulo de roteamento ASP.NET intercepta. Com essa mudança, o aplicativo mvc ASP.NET agora encaminha solicitações como:

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

A segunda rota, a rota Root, é nova. Este padrão de URL para a rota Root é uma seqüência de string vazia. Esta rota é necessária para corresponder solicitações feitas contra a raiz de sua aplicação. Por exemplo, a rota Root corresponderá a uma solicitação que se parece com isso:

[http://www.YourApplication.com/](http://www.YourApplication.com/)

Depois de fazer essas modificações na sua tabela de rotas, você precisará ter certeza de que todos os links do seu aplicativo são compatíveis com esses novos padrões de URL. Em outras palavras, certifique-se de que todos os seus links incluam a extensão .mvc. Se você usar o método de ajuda Html.ActionLink() para gerar seus links, então você não precisará fazer nenhuma alteração.

Em vez de usar o script registermvc.wcf, você pode adicionar uma nova extensão ao IIS que é mapeada para a ASP.NET framework manualmente. Ao adicionar uma nova extensão você mesmo, certifique-se de que a caixa de seleção rotulada **Verificar que o arquivo existe** não é verificado.

## <a name="hosted-server"></a>Servidor hospedado

Você nem sempre tem acesso ao seu servidor web. Por exemplo, se você estiver hospedando seu aplicativo MVC ASP.NET usando um provedor de hospedagem de Internet, então você não terá necessariamente acesso ao IIS.

Nesse caso, você deve usar uma das extensões de arquivo existentes que são mapeadas para a estrutura ASP.NET. Exemplos de extensões de arquivo mapeadas para ASP.NET incluem as extensões .aspx, .axd e .ashx.

Por exemplo, o arquivo Global.asax modificado na Listagem 3 usa a extensão .aspx em vez da extensão .mvc.

**Listagem 3 - Global.asax (modificada com extensões .aspx)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

O arquivo Global.asax na Listagem 3 é exatamente o mesmo do arquivo Global.asax anterior, exceto pelo fato de que ele usa a extensão .aspx em vez da extensão .mvc. Você não precisa executar nenhuma configuração no servidor web remoto para usar a extensão .aspx.

## <a name="creating-a-wildcard-script-map"></a>Criando um mapa de script curinga

Se você não quiser modificar os URLs para o seu aplicativo MVC ASP.NET e tiver acesso ao seu servidor web, então você tem uma opção adicional. Você pode criar um mapa de script curinga que mapeia todas as solicitações para o servidor web para a estrutura ASP.NET. Dessa forma, você pode usar a tabela de rota padrão ASP.NET MVC com IIS 7.0 (no modo clássico) ou IIS 6.0.

Esteja ciente de que essa opção faz com que o IIS intercepte todas as solicitações feitas contra o servidor web. Isso inclui solicitações de imagens, páginas ASP clássicas e páginas HTML. Portanto, permitir que um mapa de script curinga ASP.NET tem implicações de desempenho.

Veja como você habilita um mapa de script curinga para OIS 7.0:

1. Selecione seu aplicativo na janela Conexões
2. Certifique-se **de** que a exibição Recursos está selecionada
3. Clique duas vezes no botão **'Mapeamentos do manipulador'**
4. Clique no **link Adicionar mapa de script curinga** (ver Figura 3)
5. Digite o caminho para\_o arquivo aspnet isapi.dll (Você pode copiar este caminho a partir do mapa de script PageHandlerFactory)
6. Digite o nome MVC
7. Clique no botão **OK**

[![A caixa de diálogo Novo Projeto](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)

**Figura 3**: Criação de um mapa de script curinga com IIS 7.0[(Clique para ver imagem em tamanho real)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png)

Siga estas etapas para criar um mapa de script curinga com o IIS 6.0:

1. Clique com o botão direito do mouse em um site e selecione Propriedades
2. Selecione a **guia Diretório inicial**
3. Clique no botão **Configuração**
4. Selecione a guia **Mapeamentos**
5. Clique no botão **Inserir** (ver Figura 4)
6. Cole o caminho para o\_aspnet isapi.dll no campo Executável (você pode copiar este caminho do mapa de script para arquivos .aspx)
7. Desmarque a caixa de seleção rotulada **Verificar se esse arquivo existe**
8. Clique no botão **OK**

[![A caixa de diálogo Novo Projeto](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)

**Figura 4**: Criação de um mapa de script curinga com IIS 6.0[(Clique para ver imagem em tamanho real)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png)

Depois de habilitar mapas de script curinga, você precisa modificar a tabela de rotas no arquivo Global.asax para que inclua uma rota Root. Caso contrário, você receberá a página de erro na Figura 5 quando fizer uma solicitação para a página raiz do seu aplicativo. Você pode usar o arquivo Global.asax modificado na Listagem 4.

[![A caixa de diálogo Novo Projeto](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)

**Figura 5**: Erro de rota raiz ausente[(Clique para exibir imagem em tamanho real](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))

**Listagem 4 - Global.asax (modificado com rota Raiz)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

Depois de habilitar um mapa de script curinga para IIS 7.0 ou IIS 6.0, você pode fazer solicitações que funcionam com a tabela de rota padrão que se parece com isso:

/

/Home/Índice

/Produto/Detalhes/3

/Produto

## <a name="summary"></a>Resumo

O objetivo deste tutorial foi explicar como você pode usar ASP.NET MVC ao usar uma versão mais antiga do IIS (ou IIS 7.0 no modo clássico). Discutimos dois métodos para obter ASP.NET Roteamento para trabalhar com versões mais antigas do IIS: Modificar a tabela de rotas padrão ou criar um mapa de script curinga.

A primeira opção exige que você modifique os URLs usados em seu aplicativo MVC ASP.NET. Uma vantagem muito significativa desta primeira opção é que você não precisa acessar um servidor web para modificar a tabela de rotas. Isso significa que você pode usar essa primeira opção mesmo ao hospedar seu aplicativo ASP.NET MVC com uma empresa de hospedagem na Internet.

A segunda opção é criar um mapa de script curinga. A vantagem desta segunda opção é que você não precisa modificar seus URLs. A desvantagem desta segunda opção é que ela pode afetar o desempenho do seu ASP.NET aplicativo MVC.

> [!div class="step-by-step"]
> [Avançar](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
