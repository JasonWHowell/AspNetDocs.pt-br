---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Usando contadores de desempenho do Signalr em uma função Web do Azure | Microsoft Docs
author: guardrex
description: Como instalar e usar contadores de desempenho do Signalr em uma função Web do Azure.
keywords: ASP. NET, signalr, contador de desempenho, função Web do Azure
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240635"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>Usando contadores de desempenho do Signalr em uma função Web do Azure

Por [Luke Latham](https://github.com/guardrex)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Os contadores de desempenho do signalr são usados para monitorar o desempenho do aplicativo em uma função Web do Azure. Os contadores são capturados por Diagnóstico do Microsoft Azure. Você instala contadores de desempenho do Signalr no Azure com *signalr.exe*, a mesma ferramenta usada para aplicativos autônomos ou locais. Como as funções do Azure são transitórias, você configura um aplicativo para instalar e registrar contadores de desempenho do Signalr na inicialização.

## <a name="prerequisites"></a>Pré-requisitos

* Visual Studio 2015 ou [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [SDK do Microsoft Azure para Visual Studio](https://azure.microsoft.com/downloads/) **Observação: reinicie o computador depois de instalar o SDK.**
* Assinatura do Microsoft Azure: para se inscrever em uma conta de avaliação gratuita do Azure, consulte [avaliação gratuita do Azure](https://azure.microsoft.com/free/dotnet/).

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>Criando um aplicativo de função Web do Azure que expõe contadores de desempenho do Signalr

1. Abra o Visual Studio.

2. No Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**.

3. Na caixa de diálogo **novo projeto** , selecione a categoria nuvem do **Visual C#**  >  **Cloud** à esquerda e, em seguida, selecione o modelo **serviço de nuvem do Azure** . Nomeie o aplicativo **SignalRPerfCounters** e selecione **OK**.

   ![Novo aplicativo de nuvem](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > Se você não vir a categoria de modelo de **nuvem** ou o modelo de **serviço de nuvem do Azure** , precisará instalar a carga de trabalho de **desenvolvimento do azure** para o Visual Studio 2017. Escolha o link **abrir instalador do Visual Studio** no lado inferior esquerdo da caixa de diálogo **novo projeto** para abrir o instalador do Visual Studio. Selecione a carga de trabalho de **desenvolvimento do Azure** e, em seguida, escolha **Modificar** para iniciar a instalação da carga de trabalho.
   >
   > ![Carga de trabalho de desenvolvimento do Azure no Instalador do Visual Studio](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. Na caixa de diálogo **novo serviço de nuvem Microsoft Azure** , selecione **função Web ASP.net** e selecione o botão > para adicionar a função ao projeto. Selecione **OK**.

   ![Adicionar função Web ASP.NET](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. Na caixa de diálogo **novo aplicativo Web ASP.net-WebRole1** , selecione o modelo **MVC** e, em seguida, selecione **OK**.

   ![Adicionar MVC e API Web](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. Em **Gerenciador de soluções**, abra o arquivo *Diagnostics. wadcfgx* em **WebRole1**.

   ![Gerenciador de Soluções Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. Substitua o conteúdo do arquivo pela configuração a seguir e salve o arquivo:

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. Abra o **console do Gerenciador de pacotes** em **ferramentas**  >  **Gerenciador de pacotes NuGet**. Insira os seguintes comandos para instalar a versão mais recente do Signalr e o pacote de utilitários do Signalr:

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. Configure o aplicativo para instalar os contadores de desempenho do Signalr na instância de função quando ele for iniciado ou reciclado. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **WebRole1** e selecione **Adicionar**  >  **nova pasta**. Nomeie a nova pasta de *inicialização*.

   ![Adicionar pasta de inicialização](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. Copie o arquivo de *signalr.exe* (adicionado com o pacote **Microsoft. AspNet. Signalr. utils** ) de \<project folder> /SignalRPerfCounters/Packages/Microsoft.AspNet.SignalR.utils. \<version> /Tools para a pasta de *inicialização* que você criou na etapa anterior.

11. Em **Gerenciador de soluções**, clique com o botão direito do mouse na pasta de *inicialização* e selecione **Adicionar**  >  **Item existente**. Na caixa de diálogo exibida, selecione *signalr.exe* e selecione **Adicionar**.

    ![Adicionar signalr.exe ao projeto](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. Clique com o botão direito do mouse na pasta de *inicialização* que você criou. Selecione **Adicionar**  >  **novo item**. Selecione o nó **geral** , selecione **arquivo de texto**e nomeie o novo item *SignalRPerfCounterInstall. cmd*. Esse arquivo de comando instalará os contadores de desempenho do Signalr na função Web.

    ![Criar arquivo em lotes de instalação do contador de desempenho do Signalr](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. Quando o Visual Studio cria o arquivo *SignalRPerfCounterInstall. cmd* , ele será aberto automaticamente na janela principal. Substitua o conteúdo do arquivo pelo script a seguir e, em seguida, salve e feche o arquivo. Esse script executa *signalr.exe*, que adiciona os contadores de desempenho do signalr à instância de função.

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. Selecione o arquivo de *signalr.exe* em **Gerenciador de soluções**. Nas **Propriedades**do arquivo, defina **copiar para diretório de saída** como **copiar sempre**.

    ![Defina copiar para diretório de saída como copiar sempre](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. Repita a etapa anterior para o arquivo *SignalRPerfCounterInstall. cmd* .

16. Clique com o botão direito do mouse no arquivo *SignalRPerfCounterInstall. cmd* e selecione **abrir com**. Na caixa de diálogo exibida, selecione **Editor de binários** e selecione **OK**.

    ![Abrir com editor binário](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. No editor binário, selecione qualquer byte à esquerda no arquivo e exclua-os. Salve e feche o arquivo.

    ![Excluir bytes à esquerda](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. Abra o Service *Definition. csdef* e adicione uma tarefa de inicialização que execute o arquivo *SignalrPerfCounterInstall. cmd* quando o serviço for iniciado:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. Abra `Views/Shared/_Layout.cshtml` e remova o script de pacote jQuery do final do arquivo.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. Adicione um cliente JavaScript que chama continuamente o `increment` método no servidor. Abra `Views/Home/Index.cshtml` e substitua o conteúdo pelo código a seguir:

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. Crie uma nova pasta no projeto **WebRole1** chamado *hubs*. Clique com o botão direito do mouse na pasta *hubs* em **Gerenciador de soluções** e selecione **Adicionar**  >  **novo item**. Na caixa de diálogo **Adicionar novo item** , selecione a categoria signalr **da Web**  >  **SignalR** e, em seguida, selecione o modelo de item **classe do Hub do signalr (v2)** . Nomeie o novo *MyHub.cs* de Hub e selecione **Adicionar**.

    ![Adicionando a classe de Hub do Signalr à pasta hubs na caixa de diálogo Adicionar novo item](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. O *MyHub.cs* será aberto automaticamente na janela principal. Substitua o conteúdo pelo código a seguir e, em seguida, salve e feche o arquivo:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank.exe](signalr-connection-density-testing-with-crank.md)* é uma ferramenta de teste de densidade de conexão fornecida com a base de código do signalr. Como o pedais requer uma conexão persistente, você adiciona uma ao seu site para uso durante o teste. Adicione uma nova pasta ao projeto **WebRole1** chamado *PersistentConnections*. Clique com o botão direito do mouse nessa pasta e selecione **Adicionar**  >  **classe**. Nomeie o novo arquivo de classe *MyPersistentConnections.cs* e selecione **Adicionar**.

24. O Visual Studio abrirá o arquivo *MyPersistentConnections.cs* na janela principal. Substitua o conteúdo pelo código a seguir e, em seguida, salve e feche o arquivo:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. Usando a `Startup` classe, os objetos signalr começam quando o OWIN é iniciado. Abra ou crie *Startup.cs* e substitua o conteúdo pelo código a seguir:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    No código acima, o `OwinStartup` atributo marca essa classe para iniciar OWIN. O `Configuration` método inicia o signalr.

26. Teste seu aplicativo no emulador de Microsoft Azure pressionando **F5**.

    > [!NOTE]
    > Se você encontrar um **FileLoadException** em **MapSignalR**, altere os redirecionamentos de associação em *web.config* para o seguinte:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. Aguarde cerca de um minuto. Abra a janela de ferramentas do Cloud Explorer no Visual Studio (**Exibir**  >  **Cloud Explorer**) e expanda o caminho `(Local)/Storage Accounts/(Development)/Tables` . Clique duas vezes em **WADPerformanceCountersTable**. Você deve ver os contadores do Signalr nos dados da tabela. Se você não vir a tabela, talvez seja necessário inserir novamente suas credenciais de armazenamento do Azure. Talvez seja necessário selecionar o botão **Atualizar** para ver a tabela no **Cloud Explorer** ou selecionar o botão **Atualizar** na janela Abrir tabela para ver os dados na tabela.

    ![Selecionando a tabela de contadores de desempenho WAD no Visual Studio Cloud Explorer](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![Mostrando os contadores coletados na tabela de contadores de desempenho WAD](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. Para testar seu aplicativo na nuvem, atualize o arquivo **. Cloud. cscfg** e defina `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` como uma cadeia de conexão de conta de armazenamento do Azure válida.

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. Implante o aplicativo em sua assinatura do Azure. Para obter detalhes sobre como implantar um aplicativo no Azure, consulte [como criar e implantar um serviço de nuvem](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).

30. Aguarde alguns minutos. No **Cloud Explorer**, localize a conta de armazenamento configurada acima e localize a `WADPerformanceCountersTable` tabela nela. Você deve ver os contadores do Signalr nos dados da tabela. Se você não vir a tabela, talvez seja necessário inserir novamente suas credenciais de armazenamento do Azure. Talvez seja necessário selecionar o botão **Atualizar** para ver a tabela no **Cloud Explorer** ou selecionar o botão **Atualizar** na janela Abrir tabela para ver os dados na tabela.

Obrigado especial a [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) pelo conteúdo original usado neste tutorial.
