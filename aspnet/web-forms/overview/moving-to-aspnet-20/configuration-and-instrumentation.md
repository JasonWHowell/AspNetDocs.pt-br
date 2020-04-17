---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: Configuração e Instrumentação | Microsoft Docs
author: rick-anderson
description: Há grandes mudanças na configuração e instrumentação no ASP.NET 2.0. A nova aPI de configuração ASP.NET permite que as alterações de configuração sejam feitas pr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 30ea2ffd3d055c5373a33615bc19a8f68fb568ab
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543048"
---
# <a name="configuration-and-instrumentation"></a>Configuração e instrumentação

pela [Microsoft](https://github.com/microsoft)

> Há grandes mudanças na configuração e instrumentação no ASP.NET 2.0. A nova API de configuração ASP.NET permite que as alterações de configuração sejam feitas de forma programática. Além disso, muitas novas configurações existem permitem novas configurações e instrumentação.

Há grandes mudanças na configuração e instrumentação no ASP.NET 2.0. A nova API de configuração ASP.NET permite que as alterações de configuração sejam feitas de forma programática. Além disso, muitas novas configurações existem permitem novas configurações e instrumentação.

Neste módulo, discutiremos ASP.NET a API de configuração no que se refere à leitura e escrita para arquivos de configuração ASP.NET, e também abordaremos ASP.NET instrumentação. Também abordaremos os novos recursos disponíveis em ASP.NET rastreamento.

## <a name="aspnet-configuration-api"></a>API de configuração de ASP.NET

A API de configuração ASP.NET permite que você desenvolva, implante e gerencie dados de configuração de aplicativos usando uma única interface de programação. Você pode usar a API de configuração para desenvolver e modificar configurações completas de ASP.NET programáticas sem editar diretamente o XML nos arquivos de configuração. Além disso, você pode usar a API de configuração em aplicativos de console e scripts que você desenvolve, em ferramentas de gerenciamento baseadas na Web e em snap-ins do Microsoft Management Console (MMC).

As duas ferramentas de gerenciamento de configuração a seguir usam a API de configuração e estão incluídas na versão 2.0 do .NET Framework:

- O ASP.NET snap-in MMC, que usa a API de configuração para simplificar tarefas administrativas, fornecendo uma visão integrada dos dados de configuração local de todos os níveis da hierarquia de configuração.
- A Ferramenta de Administração de Sites da Web, que permite gerenciar configurações para aplicativos locais e remotos, incluindo sites hospedados.

A API de configuração ASP.NET compreende um conjunto de objetos de gerenciamento de ASP.NET que você pode usar para configurar sites e aplicativos da Web de forma programática. Os objetos de gerenciamento são implementados como uma biblioteca de classes .NET Framework. O modelo de programação da API de configuração ajuda a garantir a consistência e a confiabilidade do código, aplicando os tipos de dados no momento da compilação. Para facilitar o gerenciamento das configurações do aplicativo, a API de configuração permite visualizar dados mesclados de todos os pontos da hierarquia de configuração como uma única coleção, em vez de visualizar os dados como coleções separadas de diferentes arquivos de configuração. Além disso, a API de configuração permite manipular configurações inteiras do aplicativo sem editar diretamente o XML nos arquivos de configuração. Finalmente, a API simplifica as tarefas de configuração, suportando ferramentas administrativas, como a Ferramenta de Administração de Sites. A API de configuração simplifica a implantação, suportando a criação de arquivos de configuração em um computador e executando scripts de configuração em vários computadores.

> [!NOTE]
> A API de configuração não suporta a criação de aplicativos IIS.

## <a name="working-with-local-and-remote-configuration-settings"></a>Trabalhando com configurações locais e remotas

Um objeto configuração representa a exibição mesclada das configurações que se aplicam a uma entidade física específica, como um computador ou a uma entidade lógica, como um aplicativo ou um site da Web. A entidade lógica especificada pode existir no computador local ou em um servidor remoto. Quando não existe um arquivo de configuração para uma entidade especificada, o objeto Configuração representa as configurações padrão definidas pelo arquivo Machine.config.

Você pode obter um objeto de configuração usando um dos métodos de configuração aberta das seguintes classes:

1. A classe ConfigurationManager, se sua entidade for um aplicativo cliente.
2. A classe WebConfigurationManager, se sua entidade for um aplicativo da Web.

Esses métodos retornarão um objeto de configuração, que por sua vez fornece os métodos e propriedades necessários para lidar com os arquivos de configuração subjacentes. Você pode acessar esses arquivos para leitura ou escrita.

### <a name="reading"></a>Leitura

Você usa o método GetSection ou GetSectionGroup para ler informações de configuração. O usuário ou processo que lê deve ter permissões de leitura em todos os arquivos de configuração na hierarquia.

> [!NOTE]
> Se você usar um método getsection estático que leva um parâmetro de caminho, o parâmetro de caminho deve se referir ao aplicativo em que o código está sendo executado. Caso contrário, o parâmetro é ignorado e as informações de configuração do aplicativo em execução são devolvidas.

### <a name="writing"></a>Gravação

Você usa um dos métodos Salvar para gravar informações de configuração. O usuário ou processo que grava deve ter permissões de gravação no arquivo de configuração e diretório no nível de hierarquia de configuração atual, bem como permissões de leitura em todos os arquivos de configuração na hierarquia.

Para gerar um arquivo de configuração que represente as configurações herdadas de uma entidade especificada, use um dos seguintes métodos de configuração de salvamento:

1. O método Salvar para criar um novo arquivo de configuração.
2. O método SaveAs para gerar um novo arquivo de configuração em outro local.

## <a name="configuration-classes-and-namespaces"></a>Classes de configuração e namespaces

Muitas classes de configuração e métodos são semelhantes entre si. A tabela a seguir descreve as classes de configuração e namespaces mais usados.

| **Classe de configuração ou namespace** | **Descrição** |
| --- | --- |
| [Sistema.Espaço de nome de configuração](https://msdn.microsoft.com/library/system.configuration.aspx) | Contém as principais classes de configuração para todos os aplicativos .NET Framework. As classes de manipulador de seção são usadas para obter dados de configuração para uma seção de métodos, como GetSection e GetSectionGroup. Estes dois métodos não são estáticos. |
| System.Configuration.Configuration.Configuration class | Representa um conjunto de dados de configuração para um computador, aplicativo, diretório Web ou outro recurso. Esta classe contém métodos úteis, como GetSection e GetSectionGroup, para atualizar as configurações e obter referências a seções e grupos de seção. Essa classe é usada como um tipo de retorno para métodos que obtém dados de configuração de tempo de projeto, como os métodos das classes WebConfigurationManager e ConfigurationManager. |
| System.Web.Configuration namespace | Contém as classes de manipulador de seção para as seções de configuração ASP.NET definidas em [configurações de configuração ASP.NET](https://msdn.microsoft.com/library/b5ysx397.aspx). As classes de manipulador de seção são usadas para obter dados de configuração para uma seção de métodos, como GetSection e GetSectionGroup. |
| Classe System.Web.Configuration.WebConfigurationManager | Fornece métodos úteis para obter referências às configurações de configuração em tempo de execução e tempo de projeto. Esses métodos usam a classe System.Configuration.Configuration(Configuração).como um tipo de retorno. Você pode usar o método getsection estático desta classe ou o método GetSection não estático da classe System.Configuration.ConfigurationManager intercambiavelmente. Para configurações de aplicativos Da Web, a classe System.Web.Configuration.WebConfigurationManager é recomendada em vez da classe System.Configuration.ConfigurationManager. |
| [System.Configuration.Provider](https://msdn.microsoft.com/library/system.configuration.provider.aspx) namespace | Fornece uma maneira de personalizar e estender o provedor de configuração. Esta é a classe base para todas as classes de provedorno sistema de configuração. |
| [System.Web.Site.Management](https://msdn.microsoft.com/library/system.web.management.aspx) namespace | Contém classes e interfaces para gerenciar e monitorar a saúde dos aplicativos Web. Estritamente falando, este namespace não é considerado parte da API de configuração. Por exemplo, o rastreamento e o disparo de eventos são realizados pelas classes neste namespace. |
| [Sistema.Management.Instrumentação](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) namespace | Fornece as classes necessárias para a instrumentação de aplicativos para expor suas informações de gerenciamento e eventos através do Windows Management Instrumentation (WMI) a potenciais consumidores. ASP.NET o monitoramento de saúde usa o WMI para realizar eventos. Estritamente falando, este namespace não é considerado parte da API de configuração. |

## <a name="reading-from-aspnet-configuration-files"></a>Leitura de arquivos de configuração ASP.NET

A classe WebConfigurationManager é a classe principal para leitura de arquivos de configuração ASP.NET. Existem essencialmente três etapas para ler arquivos de configuração ASP.NET:

1. Obtenha um objeto de configuração usando o método OpenWebConfiguration.
2. Obtenha uma referência à seção desejada no arquivo de configuração.
3. Leia as informações desejadas no arquivo de configuração.

O objeto Configuração representa não representa um arquivo de configuração específico. Em vez disso, representa uma visão mesclada da configuração de um computador, aplicativo ou site. A amostra de código a seguir instancia um objeto de configuração representando a configuração de um aplicativo web chamado *ProductInfo*.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> Observe que se o caminho /ProductInfo não existir, o código acima retornará a configuração padrão conforme especificado no arquivo machine.config.

Depois de ter o objeto Configuração, você pode usar o método GetSection ou GetSectionGroup para perfurar as configurações. O exemplo a seguir recebe uma referência às configurações de personificação para o aplicativo ProductInfo acima:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>Gravação para arquivos de configuração ASP.NET

Como na leitura de arquivos de configuração, a classe WebConfigurationManager é o núcleo para escrever para Asp.NET arquivos de configuração. Há também três etapas para escrever para ASP.NET arquivos de configuração.

1. Obtenha um objeto de configuração usando o método OpenWebConfiguration.
2. Obtenha uma referência à seção desejada no arquivo de configuração.
3. Escreva as informações desejadas do arquivo de configuração usando o método Salvar ou SalvarAs.

O código a seguir altera &lt;o&gt; atributo **de depuração** do elemento compilação para falso:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

Quando este código for executado, o &lt;atributo **de depuração** do elemento compilação&gt; será definido como falso para o arquivo web.config do aplicativo *webApp.*

## <a name="systemwebmanagement-namespace"></a>System.Web.Management Namespace

O namespace System.Web.Management fornece as classes e interfaces para gerenciar e monitorar a saúde dos aplicativos ASP.NET.

O registro é realizado definindo uma regra que associa eventos a um provedor. A regra define o tipo de eventos que são enviados ao provedor. Os seguintes eventos base estão disponíveis para você registrar:

| **Webbaseevent** | A aula de eventos de base para todos os eventos. Contém as propriedades necessárias para todos os eventos, como código de evento, código de detalhes do evento, data e hora em que o evento foi levantado, número de seqüência, mensagem do evento e detalhes do evento. |
| --- | --- |
| **Webmanagementevent** | A classe de eventos base para eventos de gerenciamento, como vida útil do aplicativo, solicitação, erro e eventos de auditoria. |
| **Webheartbeatevent** | O evento gerado pelo aplicativo em intervalos regulares para capturar informações úteis do estado de execução. |
| **Webauditevent** | A classe base para eventos de auditoria de segurança, que são usadas para marcar condições como falha de autorização, falha de descriptografia, *etc.* |
| **Webrequestevent** | A classe base para todos os eventos de solicitação informacional. |
| **Webbaseerrorevent** | A classe base para todos os eventos que indiquem condições de erro. |

Os tipos de provedores disponíveis permitem enviar a saída de eventos para o Event Viewer, SQL Server, Windows Management Instrumentation (WMI) e e-mail. Os provedores pré-configurados e os mapeamentos de eventos reduzem a quantidade de trabalho necessária para obter a saída de eventos registrada.

ASP.NET 2.0 usa o provedor de registro de eventos fora da caixa para registrar eventos com base em domínios de aplicativos iniciando e parando, bem como registrando quaisquer exceções não tratadas. Isso ajuda a cobrir alguns dos cenários básicos. Por exemplo, digamos que seu aplicativo lança uma exceção, mas o usuário não salva o erro e você não pode reproduzi-lo. Com a regra padrão do Registro de Eventos, você seria capaz de reunir a exceção e empilhar informações para ter uma ideia melhor do tipo de erro ocorrido. Outro exemplo se aplica se sua aplicação estiver perdendo o estado de sessão. Nesse caso, você pode procurar no Registro de Eventos para determinar se o domínio do aplicativo está sendo reciclado e por que o domínio do aplicativo parou em primeiro lugar.

Além disso, o sistema de vigilância em saúde é extensível. Por exemplo, você pode definir eventos web personalizados, demiti-los dentro do seu aplicativo e, em seguida, definir uma regra para enviar as informações do evento para um provedor, como seu e-mail. Isso permite que você ligue facilmente sua instrumentação aos prestadores de serviços de vigilância em saúde. Como outro exemplo, você pode disparar um evento cada vez que um pedido é processado e configurar uma regra que envia cada evento para o banco de dados do SQL Server. Você também pode disparar um evento quando um usuário não faz logon várias vezes seguidas e configurar o evento para usar os provedores baseados em e-mail.

A configuração para os provedores e eventos padrão é armazenada no arquivo global Web.config. O arquivo Global Web.config armazena todas as configurações baseadas na Web armazenadas no arquivo Machine.config em ASP.NET 1x. O arquivo Web.config global está localizado no seguinte diretório:

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

A &lt;seção healthMonitoring&gt; do arquivo Global Web.config fornece configurações padrão de configuração. Você pode substituir essas configurações ou configurar suas &lt;próprias&gt; configurações implementando a seção healthMonitoring no arquivo Web.config para seu aplicativo.

A &lt;seção healthMonitoring&gt; do arquivo global Web.config contém os seguintes itens:

| **Provedores** | Contém provedores configurados para o Visualizador de Eventos, WMI e SQL Server. |
| --- | --- |
| **Eventmappings** | Contém mapeamentos para as várias classes do WebBase. Você pode estender esta lista se gerar sua própria classe de eventos. Gerar sua própria classe de eventos lhe dá uma granularidade mais fina sobre os provedores para os os que você envia informações. Por exemplo, você pode configurar exceções não manipuladas a serem enviadas ao SQL Server, enquanto envia seus próprios eventos personalizados para e-mail. |
| **Regras** | Vincula os eventMappings ao provedor. |
| **Buffer** | Usado com sql server e provedores de e-mail para determinar com que frequência para lavar os eventos para o provedor. |

Abaixo está um exemplo de código do arquivo global Web.config.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>Como armazenar eventos para o Event Viewer

Como mencionado anteriormente, o provedor para registrar eventos no Visualizador de eventos está configurado para você no arquivo Global Web.config. Por padrão, todos os eventos baseados no **WebBaseErrorEvent** e **no WebFailureAuditEvent** são registrados. Você pode adicionar regras adicionais para registrar informações adicionais ao Registro de Eventos. Por exemplo, se você quiser registrar todos os eventos *(ou seja,* todos os eventos baseados no **WebBaseEvent),** você pode adicionar a seguinte regra ao seu arquivo Web.config:

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

Essa regra vincularia o mapa de eventos **all events** ao provedor de Registro de Eventos. Tanto eventMapping quanto o provedor estão incluídos no arquivo global Web.config.

## <a name="how-to-store-events-to-sql-server"></a>Como armazenar eventos no SQL Server

Este método usa o banco de dados **ASPNETDB,** que é gerado pela ferramenta Aspnet\_regsql.exe. O provedor padrão usa a seqüência de conexões LocalSqlServer, que usa um banco de dados baseado em arquivos na pasta de dados do App\_ou a instância local do SQLExpress do SQL Server. Tanto a seqüência de conexão LocalSqlServer quanto o SqlProvider estão configurados no arquivo Global Web.config.

A seqüência de conexão LocalSqlServer no arquivo global Web.config é assim:

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

Se você quiser usar outra instância do SQL Server, você\_precisará usar a ferramenta Aspnet regsql.exe, que pode ser encontrada no %windir%\Microsoft.Net\Framework\v2.0. \* pasta. Use a ferramenta\_Aspnet regsql.exe para gerar um banco de dados **ASPNETDB** personalizado na instância do SQL Server e, em seguida, adicione a seqüência de conexões ao arquivo de configuração de aplicativos e, em seguida, adicione um provedor usando a nova seqüência de conexão. Depois de criar o banco de dados **ASPNETDB,** você precisará definir uma regra para vincular um eventoMapping ao sqlProvider.

Se você usar o SqlProvider padrão ou configurar seu próprio provedor, você precisará adicionar uma regra que vincule o provedor a um mapa de eventos. A regra a seguir liga o novo provedor que você criou acima ao mapa de eventos **de Todos os Eventos.** Esta regra registrará todos os eventos baseados no **WebBaseEvent** e os enviará ao MySqlWebEventProvider que usará a seqüência de conexões MYASPNETDB. O código a seguir adiciona uma regra para vincular o provedor a um mapa de eventos:

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

Se você quisesse enviar apenas erros para o SQL Server, você poderia adicionar a seguinte regra:

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>Como encaminhar eventos para o WMI

Você também pode encaminhar os eventos para o WMI. O provedor WMI está configurado para você no arquivo Global Web.config por padrão.

O exemplo de código a seguir adiciona uma regra para encaminhar os eventos ao WMI:

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

Você precisará adicionar uma regra para associar um eventMapping ao provedor, e também um aplicativo de ouvinte WMI para ouvir os eventos. O exemplo de código a seguir adiciona uma regra para vincular o provedor WMI ao mapa de eventos **de todos os eventos:**

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>Como encaminhar eventos para e-mail

Você também pode encaminhar eventos para e-mail. Tenha cuidado com quais regras de evento você mapeia para o seu provedor de e-mail, pois você pode enviar involuntariamente um monte de informações que podem ser mais adequadas para o SQL Server ou o Registro de Eventos. Existem dois provedores de e-mail; SimpleMailWebEventProvider e TemplatedMailWebEventProvider. Cada um tem os mesmos atributos de configuração, com exceção dos atributos "template" e "detailedTemplateErrors", ambos disponíveis apenas no TemplatedMailWebEventProvider.

> [!NOTE]
> Nenhum desses provedores de e-mail está configurado para você. Você precisará adicioná-los ao seu arquivo Web.config.

A principal diferença entre esses dois provedores de e-mail é que o SimpleMailWebEventProvider envia e-mails em um modelo genérico que não pode ser modificado. O arquivo Web.config de exemplo adiciona este provedor de e-mail à lista de provedores configurados usando a seguinte regra:

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

A seguinte regra também é adicionada para vincular o provedor de e-mail ao mapa de eventos **de Todos os Eventos:**

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 Tracing

Há três grandes melhorias para rastrear em ASP.NET 2.0.

1. Funcionalidade integrada de rastreamento
2. Acesso programático a mensagens de rastreamento
3. Rastreamento aprimorado no nível do aplicativo

## <a name="integrated-tracing-functionality"></a>Funcionalidade de rastreamento integrado

Agora você pode encaminhar mensagens emitidas pela classe System.Diagnostics.Trace para ASP.NET saída de rastreamento e direcionar mensagens emitidas por ASP.NET rastreamento para System.Diagnostics.Trace. Você também pode encaminhar ASP.NET eventos de instrumentação para System.Diagnostics.Trace. Essa funcionalidade é fornecida pelo novo atributo **writeToDiagnosticsTrace** do &lt;elemento trace.&gt; Quando esse valor booleano é verdadeiro, ASP.NET mensagens Trace são encaminhadas para a infra-estrutura de rastreamento do System.Diagnostics para uso por quaisquer ouvintes que estejam registrados para exibir mensagens Trace.

## <a name="programmatic-access-to-trace-messages"></a>Acesso programático a mensagens de rastreamento

ASP.NET 2.0 permite o acesso programático a todas as mensagens de rastreamento através da classe **TraceContextRecord** e da coleção **TraceRecords.** A maneira mais eficiente de acessar mensagens de rastreamento é registrar um delegado **TraceContextEventHandler** (também novo em ASP.NET 2.0) para lidar com o novo evento **TraceFinished.** Em seguida, você pode fazer loop através das mensagens de rastreamento como desejar.

A seguinte amostra de código ilustra isso:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

No exemplo acima, eu faço loop através da coleção TraceRecords e, em seguida, escrevo cada mensagem para o fluxo Resposta.

## <a name="improved-application-level-tracing"></a>Rastreamento aprimorado no nível de aplicativo

O rastreamento em nível de aplicativo é melhorado através da &lt;&gt; introdução do novo atributo **mais recente** do elemento trace. Este atributo especifica se a saída de rastreamento em nível de aplicativo mais recente é exibida e dados de rastreamento mais antigos além dos limites indicados pela solicitaçãoLimite são descartados. Se for falso, os dados de rastreamento serão exibidos para solicitações até que o atributo requestLimit seja atingido.

## <a name="aspnet-command-line-tools"></a>ferramentas de linha de comando ASP.NET

Existem várias ferramentas de linha de comando para ajudar na configuração de ASP.NET. ASP.NET desenvolvedores devem estar familiarizados\_com a ferramenta aspnet regiis.exe. ASP.NET 2.0 fornece três outras ferramentas de linha de comando para ajudar na configuração.

As seguintes ferramentas de linha de comando estão disponíveis:

| **Ferramenta** | **Usar** |
| --- | --- |
| **aspnet\_regiis.exe** | Permite o registro de ASP.NET com o IIS. Existem duas versões desta ferramenta que são fornecidas com ASP.NET 2.0, uma para sistemas de 32 bits (na pasta Framework) e outra para sistemas de 64 bits (na pasta Framework64.) A versão de 64 bits não será instalada em um sistema operacional de 32 bits. |
| **aspnet\_regsql.exe** | A ferramenta ASP.NET SQL Server Registration é usada para criar um banco de dados Microsoft SQL Server para uso pelos provedores do SQL Server em ASP.NET, ou para adicionar ou remover opções de um banco de dados existente. O arquivo\_Aspnet regsql.exe está localizado na pasta [unidade:]\WINDOWS\Microsoft\Microsoft.NET\version\versionNumber no servidor Web. |
| **aspnet\_regbrowsers.exe** | A ferramenta ASP.NET Browser Registration analisa e compila todas as definições do navegador em todo o sistema em um conjunto e instala o conjunto no cache global de montagem. A ferramenta usa os arquivos de definição do navegador (. Arquivos BROWSER) do subdiretório .NET Framework Browsers. A ferramenta pode ser encontrada no diretório %SystemRoot%\Microsoft.NET\Framework\version\. |
| **aspnet\_compiler.exe** | A ferramenta ASP.NET Compilação permite que você compile um aplicativo ASP.NET Web, no local ou para implantação em um local de destino, como um servidor de produção. A compilação no local ajuda o desempenho do aplicativo porque os usuários finais não encontram um atraso na primeira solicitação ao aplicativo enquanto o aplicativo é compilado. |

Como a ferramenta\_aspnet regiis.exe não é nova para ASP.NET 2.0, não vamos discutir isso aqui.

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET Ferramenta de Registro do Servidor\_SQL - aspnet regsql.exe

Você pode definir vários tipos de opções usando a ferramenta ASP.NET SQL Server Registration. Você pode especificar uma conexão SQL, especificar quais ASP.NET os serviços de aplicativos usam o SQL Server para gerenciar informações, indicar qual banco de dados ou tabela é usado para dependência de cache SQL e adicionar ou remover suporte para usar o SQL Server para armazenar procedimentos e estado de sessão.

Vários serviços de aplicativos ASP.NET dependem de um provedor para gerenciar armazenamento e recuperação de dados de uma fonte de dados. Cada provedor é específico para a fonte de dados. ASP.NET inclui um provedor de SQL Server para os seguintes recursos ASP.NET:

- Adesão (a classe [SqlMembershipProvider).](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)
- Gerenciamento de função (a classe [SqlRoleProvider).](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)
- Perfil (a classe [SqlProfileProvider).](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)
- Personalização de Peças web (a classe [SqlPersonalizationProvider).](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)
- Eventos web (a classe [SqlWebEventProvider).](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)

Quando você instala ASP.NET, o arquivo Machine.config para o seu servidor inclui elementos de configuração que especificam provedores de SQL Server para cada um dos recursos ASP.NET que dependem de um provedor. Esses provedores são configurados, por padrão, para se conectar a uma instância de usuário local do SQL Server Express 2005. Se você alterar a seqüência de conexão padrão usada pelos provedores, antes de poder usar qualquer um dos recursos ASP.NET configurados na\_configuração da máquina, você deve instalar o banco de dados SQL Server e os elementos do banco de dados para o recurso escolhido usando a aspnet regsql.exe. Se o banco de dados que você especificar com a ferramenta de registro SQL ainda não existir (o aspnetdb será o banco de dados padrão se não for especificado na linha de comando), então o usuário atual deve ter o direito de criar bancos de dados no SQL Server, bem como criar elementos de esquema dentro de um banco de dados.

### <a name="sql-cache-dependency"></a>Dependência de cache SQL

Um recurso avançado de cache de saída ASP.NET é a dependência de cache SQL. A dependência de cache SQL suporta dois modos diferentes de operação: um que usa uma ASP.NET implementação de pesquisa de tabela e um segundo modo que usa os recursos de notificação de consulta do SQL Server 2005. A ferramenta de registro SQL pode ser usada para configurar o modo de operação de votação de tabela.

### <a name="session-state"></a>Estado de sessão

Por padrão, os valores e informações do estado de sessão são armazenados na memória dentro do processo de ASP.NET. Alternativamente, você pode armazenar dados de sessão em um banco de dados do SQL Server, onde eles podem ser compartilhados por vários servidores da Web. Se o banco de dados especificado para o estado de sessão com a ferramenta de registro SQL ainda não existir, então o usuário atual deve ter o direito de criar bancos de dados no SQL Server, bem como para criar elementos de esquema dentro de um banco de dados. Se o banco de dados existe, então o usuário atual deve ter o direito de criar elementos de esquema no banco de dados existente.

Para instalar o banco de dados de estado de\_sessão no SQL Server, execute a ferramenta Aspnet regsql.exe e forneça as seguintes informações com o comando:

- O nome da instância do SQL Server, usando a opção **-S.**
- As credenciais de logon para uma conta que tem permissão para criar um banco de dados em um computador executando o SQL Server. Use a opção **-E** para usar o usuário atualmente conectado ou use a opção **-U** para especificar um ID do usuário juntamente com a opção **-P** para especificar uma senha.
- A opção **-ssadd** de linha de comando para adicionar o banco de dados de estado de sessão.

Por padrão, você não pode\_usar a ferramenta Aspnet regsql.exe para instalar o banco de dados de estado de sessão em um computador executando o SQL Server 2005 Express Edition.

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>A ferramenta de registro do\_navegador ASP.NET - aspnet regbrowsers.exe

Em ASP.NET versão 1.1, o arquivo Machine.config continha uma seção chamada &lt;browserCaps&gt;. Esta seção continha uma série de entradas XML que definiam as configurações para vários navegadores com base em uma expressão regular. Para ASP.NET versão 2.0, uma nova . O arquivo BROWSER define os parâmetros de um determinado navegador usando entradas XML. Você adiciona informações em um novo navegador adicionando um novo . Arquivo BROWSER para a pasta localizada em %SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers em seu sistema.

Como um aplicativo não está lendo um arquivo .config toda vez que requer informações do navegador, você pode criar um novo . Arquivo browser e execute\_Aspnet regbrowsers.exe para adicionar as alterações necessárias ao conjunto. Isso permite que o servidor acesse as novas informações do navegador imediatamente para que você não precise desligar nenhum de seus aplicativos para pegar as informações. Um aplicativo pode acessar os recursos do navegador através da propriedade Browser do HttpRequest atual.

As seguintes opções estão\_disponíveis ao executar aspnet regbrowser.exe:

| **Opção** | **Descrição** |
| --- | --- |
| **-?** | Exibe o texto\_Aspnet regbbrowsers.exe Help na janela de comando. |
| **-I** | Cria o conjunto de recursos do navegador em tempo de execução e instala-o no cache global de montagem. |
| **-u** | Desinstala o conjunto de recursos do navegador em tempo de execução a partir do cache global de montagem. |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>A ferramenta de compilação\_ASP.NET - aspnet compiler.exe

A ferramenta ASP.NET Compilação pode ser usada de duas maneiras gerais: para compilação e compilação no local para implantação, onde um diretório de saída de destino é especificado.

### <a name="compiling-an-application-in-place"></a>[Compilando um aplicativo no lugar](https://msdn.microsoft.com/library/ms229863.aspx)

A ferramenta ASP.NET Compilação pode compilar um aplicativo no local, ou seja, imita o comportamento de fazer várias solicitações ao aplicativo, causando assim uma compilação regular. Os usuários de um site pré-compilado não sofrerão um atraso causado pela compilação da página na primeira solicitação.

Quando você pré-compila um site no lugar, os seguintes itens se aplicam:

- O site mantém seus arquivos e estrutura de diretórios.
- Você deve ter compiladores para todas as linguagens de programação usadas pelo site no servidor.
- Se algum arquivo falhar na compilação, todo o site falhará na compilação.

Você também pode recompilar um aplicativo no local depois de adicionar novos arquivos de origem a ele. A ferramenta compila apenas os arquivos novos ou alterados, a menos que você inclua a opção **-c.**

> [!NOTE]
> A compilação de um aplicativo que contém um aplicativo aninhado não compila o aplicativo aninhado. O aplicativo aninhado deve ser compilado separadamente.

### <a name="compiling-an-application-for-deployment"></a>[Compilando um aplicativo para implantação](https://msdn.microsoft.com/library/ms229863.aspx)

Você compila um aplicativo para implantação (compilação para um local de destino) especificando o parâmetro TargetDir. O targetDir pode ser o local final para o aplicativo web, ou o aplicativo compilado pode ser implantado. O uso da opção **-u** compila o aplicativo de tal forma que você pode fazer alterações em certos arquivos no aplicativo compilado sem recompilá-lo. O aspnet\_compiler.exe faz uma distinção entre tipos de arquivos estáticos e dinâmicos, e os lida de forma diferente ao criar o aplicativo resultante.

- Os tipos de arquivos estáticos são aqueles que não possuem um compilador associado ou um provedor de compilação, como arquivos cujos nomes têm extensões como .css, .gif, .htm, .html, .jpg, .js e assim por diante. Esses arquivos são simplesmente copiados para o local de destino, com seus lugares relativos na estrutura do diretório preservados.
- Os tipos de arquivos dinâmicos são aqueles que têm um compilador associado ou um provedor de compilação, incluindo arquivos com extensões de nome de arquivo específicos de ASP.NET, como .asax, .ascx, .ashx, .aspx, .browser, .master e assim por diante. A ferramenta ASP.NET Compilação gera montagens a partir desses arquivos. Se a opção **-u** for omitida, a ferramenta também criará arquivos com a extensão do nome do arquivo . COMPILOU que mapeie os arquivos de origem originais para sua montagem. Para garantir que a estrutura do diretório da fonte do aplicativo seja preservada, a ferramenta gera arquivos de espaço reservado nos locais correspondentes no aplicativo de destino.

Você deve usar a opção **-u** para indicar que o conteúdo do aplicativo compilado pode ser modificado. Caso contrário, as modificações subseqüentes são ignoradas ou causam erros de tempo de execução.

A tabela a seguir descreve como a ferramenta ASP.NET Compilação lida com diferentes tipos de arquivos quando a opção **-u** está incluída.

| **Tipo de arquivo** | **Ação do compilador** |
| --- | --- |
| .ascx, .aspx, .master | Esses arquivos são divididos em marcação e código-fonte, que inclui arquivos de &lt;código atrás e&gt; qualquer código que esteja incluído em elementos de script runat="servidor". O código fonte é compilado em assembléias, com nomes derivados de um algoritmo de hashing, e as assembléias são colocadas no diretório Bin. Qualquer código inline, ou seja, ** &lt; ** código ** % ** incluído entre os suportes, está incluído com marcação e não compilado. Novos arquivos com o mesmo nome dos arquivos de origem são criados para conter a marcação e colocados nos diretórios de saída correspondentes. |
| .ashx, .asmx | Esses arquivos não são compilados e são movidos para os diretórios de saída como é e não compilados. Se desejar ter o código do manipulador compilado, coloque o\_código em arquivos de código-fonte no diretório Código do aplicativo. |
| .cs, .vb, .jsl, .cpp (sem incluir arquivos de código para os tipos de arquivos listados anteriormente) | Esses arquivos são compilados e incluídos como um recurso em assembléias que os referenciam. Os arquivos de origem não são copiados para o diretório de saída. Se um arquivo de código não for referenciado, ele não será compilado. |
| Tipos de arquivos personalizados | Esses arquivos não são compilados. Esses arquivos são copiados para os diretórios de saída correspondentes. |
| Arquivos de código-fonte no subdiretório App\_Code | Esses arquivos são compilados em montagens e colocados no diretório Bin. |
| arquivos .resx e .resource\_no subdiretório App GlobalResources | Esses arquivos são compilados em montagens e colocados no diretório Bin. Nenhum\_subdiretório Do App GlobalResources é criado sob o diretório principal de saída, e nenhum arquivo .resx ou .resources localizados no diretório de origem são copiados para os diretórios de saída. |
| .resx e .resource files\_no subdiretório App LocalResources | Esses arquivos não são compilados e são copiados para os diretórios de saída correspondentes. |
| .arquivos de pele\_no subdiretório App Themes | Os arquivos .skin e os arquivos temáticos estáticos não são compilados e são copiados para os diretórios de saída correspondentes. |
| .browser Web.config Tipos de arquivos estáticos Conjuntos já presentes no diretório Bin | Esses arquivos são copiados como para os diretórios de saída. |

A tabela a seguir descreve como a ferramenta ASP.NET Compilação lida com diferentes tipos de arquivos quando a opção **-u** é omitida.

| **Tipo de arquivo** | **Ação do compilador** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | Esses arquivos são divididos em marcação e código-fonte, que inclui arquivos de &lt;código atrás e&gt; qualquer código que esteja incluído em elementos de script runat="servidor". O código fonte é compilado em assembléias, com nomes derivados de um algoritmo de hashing. As assembléias resultantes são colocadas no diretório Bin. Qualquer código inline, ou seja, ** &lt; ** código ** % ** incluído entre os suportes, está incluído com marcação e não compilado. O compilador cria novos arquivos para conter a marcação com o mesmo nome dos arquivos de origem. Esses arquivos resultantes são colocados no diretório Bin. O compilador também cria arquivos com o mesmo nome dos arquivos de origem, mas com a extensão . COMPILADO que contêm informações de mapeamento. O. Os arquivos COMPILADOS são colocados nos diretórios de saída correspondentes à localização original dos arquivos de origem. |
| .ascx | Esses arquivos são divididos em marcação e código fonte. O código fonte é compilado em assembléias e colocado no diretório Bin, com nomes derivados de um algoritmo de hashing. Nenhum arquivo de marcação é gerado. |
| .cs, .vb, .jsl, .cpp (sem incluir arquivos de código para os tipos de arquivos listados anteriormente) | O código-fonte que é referenciado pelos conjuntos gerados a partir de arquivos .ascx, .ashx ou .aspx é compilado em conjuntos e colocado no diretório Bin. Nenhum arquivo de origem é copiado. |
| Tipos de arquivos personalizados | Esses arquivos são compilados como arquivos dinâmicos. Dependendo do tipo de arquivo em que eles são baseados, o compilador pode colocar arquivos de mapeamento nos diretórios de saída. |
| Arquivos no\_subdiretório App Code | Os arquivos de código-fonte neste subdiretório são compilados em montagens e colocados no diretório Bin. |
| Arquivos no\_subdiretório App GlobalResources | Esses arquivos são compilados em montagens e colocados no diretório Bin. Nenhum\_subdiretório Do App GlobalResources é criado sob o diretório principal de saída. Se o arquivo de configuração especificar se aplicaTo="Todos", arquivos .resx e .resources serão copiados para os diretórios de saída. Eles não são copiados se forem referenciados por um [BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx). |
| .resx e .resource files\_no subdiretório App LocalResources | Esses arquivos são compilados em montagens com nomes únicos e colocados no diretório Bin. Nenhum arquivo .resx ou .resource são copiados para os diretórios de saída. |
| .arquivos de pele\_no subdiretório App Themes | Os temas são compilados em montagens e colocados no diretório Bin. Os arquivos stub são criados para arquivos .skin e colocados no diretório de saída correspondente. Os arquivos estáticos (como .css) são copiados para os diretórios de saída. |
| .browser Web.config Tipos de arquivos estáticos Conjuntos já presentes no diretório Bin | Esses arquivos são copiados como é para o diretório de saída. |

### <a name="fixed-assembly-names"></a>[Nomes de montagem fixos](https://msdn.microsoft.com/library/ms229863.aspx##)

Alguns cenários, como a implantação de um aplicativo da Web usando o MSI Windows Installer, exigem o uso de nomes e conteúdos de arquivos consistentes, bem como estruturas de diretório consistentes para identificar conjuntos ou configurações para atualizações. Nesses casos, você pode usar a opção **-fixednames** para especificar que a ferramenta ASP.NET Compilação deve compilar um conjunto para cada arquivo de origem em vez de usar o local onde várias páginas são compiladas em conjuntos. Isso pode levar a um grande número de montagens, por isso, se você está preocupado com a escalabilidade, você deve usar esta opção com cautela.

### <a name="strong-name-compilation"></a>[Compilação de nomes fortes](https://msdn.microsoft.com/library/ms229863.aspx##)

As opções **-aptca**, **-delaysign**, **-keycontainer** e **-keyfile** são\_fornecidas para que você possa usar a aspnet compiler.exe para criar conjuntos fortemente nomeados sem usar a [Ferramenta de Nome Forte (Sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) separadamente. Essas opções correspondem, respectivamente, a **AllowPartiallyTrustedCallersAttribute,** **AssemblyDelaySignAttribute,** **AssemblyKeyNameAttribute**e **AssemblyKeyFileAttribute**.

A discussão desses atributos está fora do escopo deste curso.

## <a name="labs"></a>Laboratórios

Cada um dos seguintes laboratórios se baseia nos laboratórios anteriores. Você vai precisar fazê-los em ordem.

## <a name="lab-1-using-the-configuration-api"></a>Laboratório 1: Usando a API de configuração

1. Crie um novo site chamado *mod9lab*.
2. Adicione um novo arquivo de configuração da Web ao site.
3. Adicione o seguinte ao arquivo Web.config:

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

Isso garantirá que você tenha permissão para salvar alterações no arquivo Web.config.

1. Adicione um novo controle de rótulo ao Default.aspx e altere o ID para **lblDebugStatus**.
2. Adicione um novo controle de botão ao Default.aspx.
3. Altere o ID do controle do botão para **btnToggleDebug** e o Texto para **Alternar O Status de Depuração**.
4. Abra a exibição de código para o arquivo de código atrás de Default.aspx e adicione uma declaração **de uso** para **System.Web.Configuração** da seguinte forma:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. Adicione duas variáveis privadas à\_classe e um método Page Init, conforme mostrado abaixo:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. Adicione o seguinte\_código à carga de página:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. Salvar e navegar default.aspx. Observe que o controle Label exibe o status atual de depuração.
2. Clique duas vezes no controle Button no designer e adicione o seguinte código ao evento Clique para o controle button:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. Salve e navegue em default.aspx e clique no botão.
2. Abra o arquivo web.config após cada botão clicar &lt;e&gt; observe o atributo **de depuração** na seção compilação.

## <a name="lab-2-logging-application-restarts"></a>Laboratório 2: Reinicialização do aplicativo de registro

Neste laboratório, você criará um código que permitirá alternar o registro de desligamentos de aplicativos, startups e recompilações no Event Viewer.

1. Adicione uma Lista de DropDown para default.aspx e altere o ID para ddlLogAppEvents.
2. Defina a propriedade **AutoPostBack** para a lista de dropdownlist como **true**.
3. Adicione três itens à coleção Itens para a Lista de Itens. Faça o **Texto** para o primeiro item *Selecionar Valor* e o valor -1. Torne o **Texto** e o **Valor** do segundo item **Verdadeiro** e o **Texto** e **o Valor** do terceiro item **Falso**.
4. Adicione um novo Rótulo ao default.aspx. Altere o ID para **lblLogAppEvents**.
5. Abra a exibição de código atrás para default.aspx e adicione uma nova declaração para uma variável do tipo HealthMonitoringSection, conforme mostrado abaixo:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. Adicione o seguinte código ao código\_existente na Página Init:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. Clique duas vezes na Lista de DropDowne e adicione o seguinte código ao evento SelectedIndexChanged:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Navegue por default.aspx.
2. Defina a isto como **False**.
3. Limpe o login do aplicativo no Visualizador de Eventos.
4. Clique no botão para alterar o atributo Depuração para o aplicativo.
5. Atualize o login do aplicativo no Visualizador de Eventos. 

    1. Algum evento foi registrado?
    2. Por que ou não?
6. Defina a isto para **True.**
7. Clique no botão para alternar o atributo Debug para o aplicativo.
8. Atualize o login do aplicativo no Visualizador de Eventos. 

    1. Algum evento foi registrado?
    2. Qual foi o motivo do desligamento do aplicativo?
9. Experimente ligar e desligar o registro e olhar para as alterações feitas no arquivo web.config.

## <a name="more-information"></a>Obter mais informações:

ASP.NET modelo de Provedor do 2.0 permite que você crie seus próprios provedores não apenas para instrumentação de aplicativos, mas para muitos outros usos, bem como Membros, Perfis, etc. Para obter informações detalhadas sobre como escrever um provedor personalizado para registrar eventos de aplicativos em um arquivo de texto, visite [este link](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp).
