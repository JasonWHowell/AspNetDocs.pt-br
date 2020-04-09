---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 'Apêndice: O aplicativo de amostra de correção (construindo aplicativos de nuvem do mundo real com o Azure) | Microsoft Docs'
author: MikeWasson
description: The Building Real World Cloud Apps with Azure e-book é baseado em uma apresentação desenvolvida por Scott Guthrie. Explica 13 padrões e práticas que ele pode...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675988"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>Apêndice: O aplicativo de amostra de correção (construindo aplicativos de nuvem do mundo real com o Azure)

por [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Baixe O Projeto Fix It](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> The **Building Real World Cloud Apps with Azure** e-book é baseado em uma apresentação desenvolvida por Scott Guthrie. Ele explica 13 padrões e práticas que podem ajudá-lo a ser bem sucedido desenvolvendo aplicativos web para a nuvem. Para obter informações sobre o e-book, consulte [o primeiro capítulo](introduction.md).

Este apêndice do Building Real World Cloud Apps com o e-book do Azure contém as seguintes seções que fornecem informações adicionais sobre o aplicativo de amostra Fix It que você pode baixar:

- [Problemas conhecidos](#knownissues)
- [Práticas recomendadas](#bestpractices)
- [Como executar o aplicativo do Visual Studio em seu computador local](#run-in-vs)
- [Como implantar o aplicativo base para aplicativos web do Azure App Service usando os scripts do Windows PowerShell](#deploybase)
- [Solução de problemas dos scripts do Windows PowerShell](#troubleshooting)
- [Como implantar o aplicativo com processamento de fila para aplicativos web do Azure App Service e um Serviço de Nuvem do Azure](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>Problemas conhecidos

O aplicativo Fix It foi originalmente desenvolvido para ilustrar o mais simples possível alguns dos padrões apresentados neste e-book. No entanto, como o e-book é sobre a construção de aplicativos do mundo real, submetemos o código Fix It a um processo de revisão e teste semelhante ao que faríamos para o software lançado. Encontramos uma série de problemas, e como em qualquer aplicação do mundo real, alguns deles corrigimos e alguns deles nós adiamos para uma versão posterior.

A lista a seguir inclui questões que devem ser abordadas em um aplicativo de produção, mas por uma razão ou outra decidimos não abordar na versão inicial do aplicativo de amostra Fix It.

### <a name="security"></a>Segurança

- Certifique-se de que você não pode atribuir uma tarefa a um proprietário inexistente.
- Certifique-se de que você só pode visualizar e modificar tarefas que você criou ou são atribuídos a você.
- Use HTTPS para páginas de login e cookies de autenticação.
- Especifique um limite de tempo para cookies de autenticação.

### <a name="input-validation"></a>Validação da entrada

Em geral, um aplicativo de produção faria mais validação de entrada do que o aplicativo Fix It. Por exemplo, o tamanho da imagem / tamanho do arquivo de imagem permitido para upload deve ser limitado.

### <a name="administrator-functionality"></a>Funcionalidade do administrador

Um administrador deve ser capaz de alterar a propriedade em tarefas existentes. Por exemplo, o criador de uma tarefa pode deixar a empresa, não deixando ninguém com autoridade para manter a tarefa, a menos que o acesso administrativo seja habilitado.

### <a name="queue-message-processing"></a>Processamento de mensagens na fila

O processamento de mensagens na fila no aplicativo Fix It foi projetado para ser simples para ilustrar o padrão de trabalho centrado na fila com uma quantidade mínima de código. Este código simples não seria adequado para uma aplicação de produção real.

- O código não garante que cada mensagem de fila será processada no máximo uma vez. Quando você recebe uma mensagem da fila, há um período de tempo, durante o qual a mensagem é invisível para outros ouvintes da fila. Se o intervalo expirar antes da mensagem ser excluída, a mensagem voltará a ser visível. Portanto, se uma instância de função do trabalhador passa muito tempo processando uma mensagem, é teoricamente possível que a mesma mensagem seja processada duas vezes, resultando em uma tarefa duplicada no banco de dados. Para obter mais informações sobre esse problema, consulte [Usando filas de armazenamento do Azure](https://msdn.microsoft.com/library/ff803365.aspx#sec7).
- A lógica de votação na fila poderia ser mais econômica, em loteamento de recuperação de mensagens. Toda vez que você liga para [CloudQueue.GetMessageAsync,](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)há um custo de transação. Em vez disso, você pode chamar [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (nota o plural 's'), que recebe várias mensagens em uma única transação. Os custos de transação para as filas de armazenamento do Azure são muito baixos, portanto, o impacto nos custos não é substancial na maioria dos cenários.
- O loop apertado no código de processamento de mensagens da fila causa afinidade da CPU, que não utiliza VMs multinúcleo de forma eficiente. Um design melhor usaria o paralelismo de tarefas para executar várias tarefas de sincronia em paralelo.
- O processamento de mensagens na fila tem apenas um tratamento rudimentar de exceção. Por exemplo, o código não lida com [mensagens venenosas.](https://msdn.microsoft.com/library/ms789028.aspx) (Quando o processamento de mensagens causa uma exceção, você tem que registrar o erro e excluir a mensagem, ou a função do trabalhador tentará processá-la novamente, e o loop continuará indefinidamente.)

### <a name="sql-queries-are-unbounded"></a>As consultas SQL não são limitadas

O código Fix It atual não coloca limite de quantas linhas as consultas para páginas de Índice podem retornar. Se um grande volume de tarefas for inserido no banco de dados, o tamanho das listas resultantes recebidas poderá causar problemas de desempenho. A solução é implementar a paginação. Por exemplo, consulte [Classificação, Filtragem e Paginação com o Framework da entidade em um aplicativo mvc ASP.NET](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).

### <a name="view-models-recommended"></a>Ver modelos recomendados

O aplicativo Corrigir It usa a classe de entidade FixItTask para passar informações entre o controlador e a exibição. Uma prática recomendada é usar modelos de visualização. O modelo de domínio (por exemplo, a classe de entidade FixItTask) é projetado em torno do necessário para a persistência de dados, enquanto um modelo de exibição pode ser projetado para apresentação de dados. Para obter mais informações, consulte [12 ASP.NET Práticas Recomendadas de MVC](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).

### <a name="secure-image-blob-recommended"></a>Bolha de imagem segura recomendada

O aplicativo Fix It armazena imagens enviadas como públicas, o que significa que qualquer pessoa que encontrar a URL pode acessar as imagens. As imagens poderiam ser protegidas em vez de públicas.

### <a name="no-powershell-automation-scripts-for-queues"></a>Sem scripts de automação PowerShell para filas

Os scripts de automação do Sample PowerShell foram gravados apenas para a versão base do Fix It que é executado inteiramente em Aplicativos Web do Azure App Service. Não fornecemos scripts para configurar e implantar no aplicativo web mais o ambiente cloud service necessário para o processamento de filas.

### <a name="special-handling-for-html-codes-in-user-input"></a>Tratamento especial para códigos HTML na entrada do usuário

ASP.NET automaticamente impede muitas maneiras pelas quais usuários mal-intencionados podem tentar ataques de script entre sites inserindo script em caixas de texto de entrada do usuário. E o `DisplayFor` ajudante de MVC usado para exibir títulos de tarefa e notas automaticamente HTML-codifica valores que ele envia para o navegador. Mas em um aplicativo de produção você pode querer tomar medidas adicionais. Para obter mais informações, consulte [Validação de solicitações em ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).

<a id="bestpractices"></a>
## <a name="best-practices"></a>Práticas recomendadas

A seguir, alguns problemas que foram corrigidos após serem descobertos na revisão de código e testes da versão original do aplicativo Fix It. Alguns foram causados pelo codificador original não estar ciente de uma determinada prática recomendada, alguns simplesmente porque o código foi escrito rapidamente e não foi destinado para software lançado. Estamos listando os problemas aqui no caso de haver algo que aprendemos com esta revisão e testes que podem ser úteis para outros que também estão desenvolvendo aplicativos web.

### <a name="dispose-the-database-repository"></a>Descarte o repositório do banco de dados

A `FixItTaskRepository` classe deve descartar `DbContext` a instância do Quadro de Entidades. Fizemos isso `IDisposable` implementando na `FixItTaskRepository` classe:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

Observe que o AutoFac `FixItTaskRepository` descartará automaticamente a instância, por isso não precisamos descartá-la explicitamente.

Outra opção é `DbContext` remover a `FixItTaskRepository`variável membro e, em vez disso, criar uma variável local `DbContext` dentro de cada método de repositório, dentro de uma `using` declaração. Por exemplo:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>Registre singletons como tal com DI

Uma vez que `PhotoService` apenas `Logger` uma instância da classe e classe é necessária, essas classes devem ser [registradas como instâncias únicas para injeção de dependência](https://code.google.com/p/autofac/wiki/InstanceScope) em *DependenciesConfig.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>Segurança: Não mostre detalhes de erro aos usuários

O aplicativo original Fix It não tinha uma página de erro genérica e apenas deixou todas as exceções borbulharem para a interface do usuário, de modo que algumas exceções, como erros de conexão de banco de dados, poderiam resultar em um rastreamento de pilha completa sendo exibido para o navegador. Informações detalhadas de erro às vezes podem facilitar ataques de usuários mal-intencionados. A solução é registrar os detalhes da exceção e exibir uma página de erro para o usuário que não inclua detalhes de erro. O aplicativo Fix It já estava registrando e, para `<customErrors mode=On>` exibir uma página de erro, adicionamos no arquivo Web.config.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

Por padrão, isso faz com *que as exibições\Shared\Error.cshtml* sejam exibidas para erros. Você pode personalizar *Error.cshtml* ou criar sua `defaultRedirect` própria exibição de página de erro e adicionar um atributo. Você também pode especificar diferentes páginas de erro para erros específicos.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>Segurança: só permita que uma tarefa seja editada por seu criador

A página Índice do Painel mostra apenas tarefas criadas pelo usuário conectado, mas um usuário mal-intencionado pode criar uma URL com um ID para a tarefa de outro usuário. Adicionamos código em *DashboardController.cs* para retornar um 404 nesse caso:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>Não engula exceções

O aplicativo original Fix It acabou de retornar nulo depois de registrar uma exceção resultante de uma consulta SQL:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

Isso faria parecer para o usuário como se a consulta tivesse sucesso, mas simplesmente não retornasse nenhuma linha. A solução é relançar a exceção depois de capturar e registrar:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>Pegue todas as exceções em funções de trabalhador

Quaisquer exceções não tratadas em uma função de trabalhador farão com que a VM seja reciclada, então você deseja envolver tudo o que você faz em um bloco de tentativa de captura e lidar com todas as exceções.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>Especificar comprimento para propriedades de string em classes de entidade

Para exibir um código simples, a versão original do aplicativo Fix It não especificou comprimentos para os campos da entidade FixItTask e, como resultado, eles foram definidos como varchar(max) no banco de dados. Como resultado, a ui aceitaria quase qualquer quantidade de entrada. A especificação de comprimentos define limites que se aplicam tanto à entrada do usuário na página da Web quanto ao tamanho da coluna no banco de dados:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>Marcar membros privados como readonly quando eles não são esperados para mudar

Por exemplo, `DashboardController` na classe `FixItTaskRepository` uma instância de é criada e não é esperado que mude, por isso defini-lo como [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>Use a lista. Qualquer () em vez de lista. Contagem() &gt; 0

Se você só se importa se um ou mais itens de uma lista se encaixam nos critérios especificados, use o método [Qualquer,](https://msdn.microsoft.com/library/bb534972.aspx) pois ele retorna assim que um item adequado aos critérios é encontrado, enquanto o `Count` método sempre tem que iterar em cada item. O arquivo Dashboard *Index.cshtml* originalmente tinha esse código:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

Nós mudamos para isso:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>Gerar URLs em visualizações MVC usando ajudantes De MVC

Para o botão **Criar uma Correção Na** página inicial, o aplicativo Fix It codificava um elemento âncora:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

Para links de exibição/ação como este, é melhor usar o ajudante [url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML, por exemplo:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>Use Task.Delay em vez de Thread.Sleep na função do trabalhador

O modelo do `Thread.Sleep` novo projeto coloca o código de exemplo para uma função do trabalhador, mas fazer com que o segmento durma pode fazer com que o pool de segmentos gere outros segmentos desnecessários. Você pode evitar isso usando [Task.Delay.](https://msdn.microsoft.com/library/hh139096.aspx)

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>Evite o vazio assincrono

Se um método assíncrono não precisar `Task` retornar um `void`valor, retorne um tipo em vez de .

Este exemplo é `FixItQueueManager` da classe:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

Você deve `async void` usar apenas para manipuladores de eventos de alto nível. Se você definir `async void`um método como , o chamador não pode **esperar** o método ou pegar quaisquer exceções que o método lança. Para obter mais informações, consulte [Práticas Recomendadas em Programação Assíncrona](https://msdn.microsoft.com/magazine/jj991977.aspx).

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>Use um token de cancelamento para quebrar o ciclo de função do trabalhador

Normalmente, o método **Executar** em uma função de trabalhador contém um loop infinito. Quando a função do trabalhador está parando, o método [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) é chamado. Você deve usar este método para cancelar o trabalho que está sendo feito dentro do método **Executar** e sair graciosamente. Caso contrário, o processo pode ser encerrado no meio de uma operação.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>Opte por desativar o procedimento automático de farejar mime

Em alguns casos, o Internet Explorer relata um tipo MIME diferente do tipo especificado pelo servidor web. Por exemplo, se o Internet Explorer encontrar conteúdo HTML em um arquivo entregue com o cabeçalho de resposta HTTP Tipo de conteúdo: texto/planície, o Internet Explorer determina que o conteúdo deve ser renderizado como HTML. Infelizmente, esse "farejamento de MIME" também pode levar a problemas de segurança para servidores que hospedam conteúdo não confiável. Para combater esse problema, o Internet Explorer 8 fez uma série de alterações no código de determinação do tipo MIME e permite que os desenvolvedores de aplicativos [optem por não cheirar mime](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx). O código a seguir foi adicionado ao arquivo *Web.config.*

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>Permitir agrupamento e minificação

Quando o Visual Studio cria um novo projeto web, o agrupamento e a minificação dos arquivos JavaScript não são habilitados por padrão. Adicionamos uma linha de código em BundleConfig.cs:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>Defina um tempo de validade para cookies de autenticação

Por padrão, os cookies de autenticação expiram em duas semanas. Um tempo menor é mais seguro. Você pode alterar esta configuração em *StartupAuth.cs:*

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>Como executar o aplicativo do Visual Studio em seu computador local

Existem duas maneiras de executar o aplicativo Fix It:

- Execute o aplicativo base que grava novas tarefas diretamente no banco de dados SQL.
- Execute o aplicativo usando uma fila mais um serviço de back-end para criar tarefas. O padrão de fila é descrito no padrão [de trabalho centrado](queue-centric-work-pattern.md)na fila do capítulo .

<a id="runbase"></a>
### <a name="run-the-base-application"></a>Execute a aplicação base

1. Instalar o [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).
2. Instale o [Azure SDK para .NET para Visual Studio](https://azure.microsoft.com/downloads/).
3. Baixe o arquivo .zip da Galeria de [Códigos MSDN](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).
4. No Explorador de arquivos, clique com o botão direito do mouse no arquivo .zip e clique em Propriedades e, em seguida, na janela Propriedades clique em Desbloquear.
5. Descompacte o arquivo.
6. Clique duas vezes no arquivo .sln para iniciar o Visual Studio.
7. No menu **Ferramentas,** clique em **NuGet Package Manager**e, em seguida, **console do gerenciador de pacotes**.
8. No PMC (Package Manager Console, console do gerenciador de pacotes), clique em Restaurar.
9. Saia do Visual Studio.
10. Inicie [o emulador de armazenamento Azure](/azure/storage/common/storage-use-emulator).
11. Reinicie o Visual Studio, abrindo o arquivo de solução que você fechou na etapa anterior.
12. Certifique-se de que o projeto FixIt está definido como o projeto de inicialização e, em seguida, pressione CTRL+F5 para executar o projeto.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>Execute o aplicativo com processamento de fila

1. Siga as instruções para [Executar o aplicativo base](#runbase)e, em seguida, feche o navegador e feche o Visual Studio.
2. Inicie o Visual Studio com privilégios de administrador. (Você estará usando o emulador de computação do Azure, e isso requer privilégios de administrador.)
3. No arquivo *Web.config* do aplicativo *MyFixIt* (o projeto web), altere o valor de `appSettings/UseQueues` "true":

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. Se o [emulador de armazenamento Azure](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) ainda não estiver funcionando, comece novamente.
5. Execute simultaneamente o projeto web FixIt e o projeto MyFixItCloudService.

    Usando o Visual Studio:

   1. Pressione **F5** para executar o projeto FixIt.
   2. No **Solution Explorer,** clique com o botão direito do mouse no projeto MyFixItCloudService e clique em **Depurar** > **Nova Instância**.

    Usando o Visual Studio 2013 Express para Web:

   3. No Solution Explorer, clique com o botão direito do mouse na solução FixIt e selecione **Propriedades**.
   4. Selecione **vários projetos de inicialização**.
   5. Na lista de isto **ação** em MyFixIt e MyFixItCloudService, selecione **Iniciar**.
   6. Clique em **OK**.
   7. Pressione **F5** para executar os dois projetos.

      Quando você executa o projeto MyFixItCloudService, o Visual Studio inicia o emulador de computação do Azure. Dependendo da configuração do firewall, talvez seja necessário permitir que o emulador através do firewall.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Como implantar o aplicativo base para aplicativos web do Azure App Service usando os scripts do Windows PowerShell

Para ilustrar o padrão [Automate Everything,](automate-everything.md) o aplicativo Fix It é fornecido com scripts que configuram um ambiente no Azure e implantam o projeto no novo ambiente. As instruções a seguir explicam como usar os scripts.

Se você quiser executar no Azure sem usar filas e fizer as alterações para executar localmente com filas, certifique-se de definir o valor de Configuração de Configuração de Uso sustais antes de prosseguir com as seguintes instruções.

Essas instruções supõem que você já baixou e executou a solução Fix It localmente, e que você tem uma conta azure ou tem uma assinatura do Azure que você está autorizado a gerenciar.

1. Instale **o console Azure PowerShell.** Para saber mais, confira [Como instalar e configurar o PowerShell do Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).

    Este console personalizado está configurado para funcionar com sua assinatura do Azure. O módulo Azure está instalado no diretório Arquivos do *programa* e é importado automaticamente em todos os usos do console Azure PowerShell.

    Se você preferir trabalhar em um programa de host diferente, como o Windows PowerShell ISE, [certifique-se de](https://go.microsoft.com/fwlink/?LinkID=141553) usar o cmdlet do Módulo de Importação para importar o módulo Azure ou usar um comando no módulo Azure para ativar a importação automática do módulo.
2. Inicie o Azure PowerShell com a opção **Executar como administrador.**
3. Execute o [cmdlet Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) para definir a diretiva `RemoteSigned`de execução do Azure PowerShell para . Digite **Y** (para Sim) para concluir a mudança de política.

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    Essa configuração permite executar scripts locais que não estão assinados digitalmente. (Você também pode definir `Unrestricted`a política de execução para , o que eliminaria a necessidade de desbloquear o passo mais tarde, mas isso não é recomendado por razões de segurança.)
4. Execute `Add-AzureAccount` o cmdlet para configurar o PowerShell com credenciais para sua conta.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    Essas credenciais expiram após um período de tempo `Add-AzureAccount` e você tem que executar o cmdlet. Como este e-book está sendo escrito, o prazo antes das credenciais expirarem é de 12 horas.
5. Se você tiver várias assinaturas, use o cmdlet Select-AzureSubscription para especificar a assinatura que deseja criar no ambiente de teste.
6. Importe um certificado de gerenciamento para a `Get-AzurePublishSettingsFile` `Import-AzurePublishSettingsFile` mesma assinatura do Azure usando os cmdlets. O primeiro desses cmdlets baixa um arquivo de certificado, e no segundo você especifica a localização desse arquivo para importá-lo. > [!IMPORTANT]
   > Mantenha o arquivo baixado em um local seguro ou exclua-o quando terminar com ele, porque ele contém um certificado que pode ser usado para gerenciar seus serviços do Azure.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    O certificado é usado para uma chamada de API REST que detecta o endereço IP da máquina de desenvolvimento para definir uma regra de firewall no servidor sql database.
7. Execute o [cmdlet Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) (aliases são `cd`, `chdir`e `sl`) para navegar até o diretório que contém os scripts. (Eles estão localizados na pasta *Automação* na pasta De correção it.) Coloque o caminho entre aspas se algum dos nomes do diretório contiver espaços. Por exemplo, para `c:\Sample Apps\FixIt\Automation` navegar até o diretório você pode inserir o seguinte comando:

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Para permitir que o Windows PowerShell execute esses scripts, use o cmdlet [Deblock-File.](https://go.microsoft.com/fwlink/p/?linkid=294021) (Os scripts são bloqueados porque foram baixados da Internet.)

    > [!WARNING]
    > Segurança - `Unblock-File` Antes de executar em qualquer script ou arquivo executável, abra o arquivo no Bloco de Notas, examine os comandos e verifique se eles não contêm nenhum código malicioso.

    Por exemplo, o comando `Unblock-File` a seguir executa o cmdlet em todos os scripts do diretório atual.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. Para criar o aplicativo web para o aplicativo base (sem filas processando) Corrija o aplicativo Fix It, execute o script de criação de ambientes.

    O `Name` parâmetro necessário especifica o nome do banco de dados e também é usado para a conta de armazenamento que o script cria. O nome deve ser globalmente único dentro do domínio azurewebsites.net. Se você especificar um nome que não seja único, como Fixit ou Teste `New-AzureWebsite` (ou mesmo como no exemplo, fixitdemo), o cmdlet falhará com um erro interno que relata um conflito. O script converte o nome em todas as minúsculas para atender aos requisitos de nome para aplicativos web, contas de armazenamento e bancos de dados.

    O `SqlDatabasePassword` parâmetro necessário especifica a senha da conta de administrador que será criada para o Banco de Dados SQL. Não inclua caracteres XML especiais&amp; &lt; &gt; na senha (;). Esta é uma limitação da forma como os roteiros foram escritos, não uma limitação do Azure.

    Por exemplo, se você quiser criar um aplicativo web chamado "fixitdemo" e usar uma senha de administrador do SQL Server de "Passw0rd1", você pode inserir o seguinte comando:

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    O nome deve ser único no domínio azurewebsites.net, e a senha deve atender aos requisitos do Banco de Dados SQL para a complexidade da senha. (O exemplo passw0rd1 atende aos requisitos.)

    Note que o comando começa com ". \". Para ajudar a evitar a execução maliciosa de scripts, o Windows PowerShell requer que você forneça o caminho totalmente qualificado para o arquivo de script quando executar um script. Você pode usar um pontilhado para indicar\"o diretório atual ("). ou fornecer o caminho totalmente qualificado, tais como:

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    Para obter mais informações sobre `Get-Help` o script, use o cmdlet.

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    Você pode `Detailed`usar `Full` `Parameters`os `Examples` parâmetros do cmdlet Get-Help para filtrar a ajuda que é devolvida.

    Se o script falhar ou gerar erros, como "New-AzureWebsite : Call Set-AzureSubscription e Select-AzureSubscription first", você pode não ter concluído a configuração do Azure PowerShell.

    Após o término do script, você pode usar o Portal de Gerenciamento do Azure para ver os recursos que foram criados, como mostrado no capítulo [Automate Everything.](automate-everything.md)
10. Para implantar o projeto FixIt no novo ambiente Azure, use o *script AzureSite.ps1.* Por exemplo:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    Quando a implantação é feita, o navegador abre com Fix It em execução no Azure.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Solução de problemas dos scripts do Windows PowerShell

Os erros mais comuns encontrados ao executar esses scripts estão relacionados às permissões. Certifique-se `Add-AzureAccount` `Import-AzurePublishSettingsFile` de que e foram bem sucedidos e que você os usou para a mesma assinatura do Azure. Mesmo `Add-AzureAccount` que fosse bem sucedido, você poderia ter que executá-lo novamente. As permissões `Add-AzureAccount` adicionadas expiram em 12 horas.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>a referência de objeto não está definida em uma instância de um objeto.

Se o script retornar erros, como "Referência de objeto não definida como uma instância de um objeto", o que significa que `Add-AzureAccount` o Windows PowerShell não pode encontrar um objeto para processar (esta é uma exceção de referência nula), execute o cmdlet e tente o script novamente.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: O servidor encontrou um erro interno.

O `New-AzureWebsite` cmdlet retorna um erro interno quando o nome não é único no domínio azurewebsites.net. Para resolver o erro, use um valor diferente para o nome, que está no parâmetro Nome de *New-AzureSiteEnv.ps1*.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>Reiniciando o script

Se você precisar reiniciar o script *New-AzureSiteEnv.ps1* porque ele falhou antes de imprimir a mensagem "Script está concluído", você pode querer excluir os recursos que o script criou antes de ser interrompido. Por exemplo, se o script já criou o aplicativo web ContosoFixItDemo e você executar o script novamente com o mesmo nome, o script falhará porque o nome está em uso.

Para determinar quais recursos o script criou antes de ser interrompido, use os seguintes cmdlets:

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: Para executar este cmdlet, encane o nome do servidor de banco de dados para: `Get-AzureSqlDatabase``Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

Para excluir esses recursos, use os seguintes comandos. Observe que se você excluir o servidor de banco de dados, você exclui automaticamente os bancos de dados associados ao servidor.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>Como implantar o aplicativo com processamento de fila para aplicativos web do Azure App Service e um Serviço de Nuvem do Azure

Para ativar filas, faça a seguinte alteração no arquivo MyFixIt\Web.config. Em `appSettings`, alterar `UseQueues` o valor de "verdadeiro":

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

Em seguida, implante o aplicativo MVC em um aplicativo web no Azure App Service, como descrito [anteriormente](#deploybase).

Em seguida, crie um novo serviço de nuvem do Azure. Os scripts incluídos no aplicativo Fix It não criam ou implantam o serviço em nuvem, então você deve usar o portal Azure para isso. No portal, clique em **New** -- **Compute** – **Cloud Service** -- **Quick Create**, e digite uma URL e uma localização de data center. Use o mesmo data center onde você implantou o aplicativo web.

![](the-fix-it-sample-application/_static/image1.png)

Antes de implantar o serviço em nuvem, você precisa atualizar alguns dos arquivos de configuração.

Em MyFixIt.WorkerRole\app.config, `connectionStrings`em , substitua o `appdb` valor da seqüência de conexão com a seqüência de conexão real para o Banco de Dados SQL. Você pode obter a seqüência de conexão do portal. No portal, clique em **SQL Databases** - **appdb** - **View SQL Database strings for ADO .Net, ODBC, PHP e JDBC**. Copie a ADO.NET string de conexão e cole o valor no arquivo app.config. Substitua "{sua\_senha\_aqui}" por sua senha de banco de dados. (Supondo que você usou os scripts para implantar o `SqlDatabasePassword` aplicativo MVC, você especificou a senha do banco de dados no parâmetro script.)

O resultado deve ser parecido com o seguinte:

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

No mesmo arquivo MyFixIt.WorkerRole\app.config, em `appSettings`, substitua os dois valores de espaço reservado para a conta de armazenamento DoZure.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

Você pode obter a chave de acesso a partir do portal. Veja [como gerenciar contas de armazenamento](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).

Em MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, substitua os mesmos dois valores de espaço reservado para a conta de armazenamento Azure.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

Agora você está pronto para implantar o serviço de nuvem. Em Solution Explore, clique com o botão direito do mouse no projeto MyFixItCloudService e **selecione Publicar**. Para obter mais informações, consulte "[Deploy the App to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", que está na parte 2 deste [tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).

> [!div class="step-by-step"]
> [Anterior](more-patterns-and-guidance.md)
