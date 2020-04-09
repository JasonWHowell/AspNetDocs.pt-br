---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'ASP.NET Web Deployment usando o Visual Studio: Web.config File Transformations | Microsoft Docs'
author: tdykstra
description: Esta série tutorial mostra como implantar (publicar) um aplicativo web ASP.NET para o Azure App Service Web Apps ou para um provedor de hospedagem de terceiros, por usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676121"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>ASP.NET Web Deployment usando o Visual Studio: Web.config Transformações de arquivos

por [Tom Dykstra](https://github.com/tdykstra)

[Baixar Projeto Inicial](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Esta série tutorial mostra como implantar (publicar) um aplicativo web ASP.NET para o Azure App Service Web Apps ou para um provedor de hospedagem de terceiros, usando o Visual Studio 2012 ou o Visual Studio 2010. Para obter informações sobre a série, consulte [o primeiro tutorial da série](introduction.md).

## <a name="overview"></a>Visão geral

Este tutorial mostra como automatizar o processo de alteração do arquivo *Web.config* quando você o implanta em diferentes ambientes de destino. A maioria dos aplicativos tem configurações no arquivo *Web.config* que devem ser diferentes quando o aplicativo é implantado. Automatizar o processo de fazer essas alterações evita que você tenha que fazê-las manualmente toda vez que você implantar, o que seria tedioso e propenso a erros.

Lembrete: Se você receber uma mensagem de erro ou algo não funcionar enquanto você passa pelo tutorial, certifique-se de verificar a [página de solução de problemas](troubleshooting.md).

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Transformações web.config versus parâmetros de Implantação da Web

Existem duas maneiras de automatizar o processo de alteração das configurações de arquivos *web.config:* [transformações web.config](https://msdn.microsoft.com/library/dd465326.aspx) e [parâmetros de Implantação da Web](https://msdn.microsoft.com/library/ff398068.aspx). Um arquivo *de transformação Web.config* contém marcação XML que especifica como alterar o arquivo *Web.config* quando ele é implantado. Você pode especificar diferentes alterações para configurações específicas de compilação e para perfis de publicação específicos. As configurações de compilação padrão são Debug e Release, e você pode criar configurações de compilação personalizadas. Um perfil de publicação normalmente corresponde a um ambiente de destino. (Você aprenderá mais sobre publicar perfis no [IIS como um](deploying-to-iis.md) tutorial de ambiente de teste.)

Os parâmetros de Implantação da Web podem ser usados para especificar muitos tipos diferentes de configurações que devem ser configuradas durante a implantação, incluindo configurações encontradas em arquivos *Web.config.* Quando usado para especificar alterações de arquivo *Web.config,* os parâmetros de Implantação da Web são mais complexos de configurar, mas são úteis quando você não sabe o valor a ser definido até que você seja implantado. Por exemplo, em um ambiente corporativo, você pode criar um *pacote de implantação* e dá-lo a uma pessoa no departamento de TI para instalar na produção, e essa pessoa tem que ser capaz de inserir strings de conexão ou senhas que você não conhece.

Para o cenário que esta série tutorial abrange, você sabe com antecedência tudo o que tem que ser feito para o arquivo *Web.config,* para que você não precise usar parâmetros de Implantação da Web. Você configurará algumas transformações que diferem dependendo da configuração de compilação usada, e algumas que diferem dependendo do perfil de publicação usado.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Especificando configurações web.config no Azure

Se as configurações de arquivo *Web.config* que `<connectionStrings>` você `<appSettings>` deseja alterar estiverem no elemento ou no elemento e se você estiver implantando no Web Apps no Azure App Service, você terá outra opção para automatizar alterações durante a implantação. Você pode inserir as configurações que deseja fazer no Azure na guia **Configurar** da página do portal de gerenciamento para o seu aplicativo web (role até as **configurações** do aplicativo e seções **de strings de conexão).** Quando você implanta o projeto, o Azure aplica automaticamente as alterações. Para obter mais informações, consulte [sites do Windows Azure: como funcionam as strings de aplicativos e as cadeias de conexão](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

## <a name="default-transformation-files"></a>Arquivos de transformação padrão

No **Solution Explorer,** expanda o *Web.config* para ver os arquivos *de transformação Web.Debug.config* e *Web.Release.config* que são criados por padrão para as duas configurações de compilação padrão.

![Web.config_transform_files](web-config-transformations/_static/image1.png)

Você pode criar arquivos de transformação para configurações de compilação personalizadas clicando com o botão direito do mouse no arquivo Web.config e escolhendo **Adicionar Transformações** de Config no menu de contexto. Para este tutorial você não precisa fazer isso, e a opção de menu está desativada, porque você não criou nenhuma configuração de compilação personalizada.

Mais tarde, você criará mais três arquivos de transformação, um cada para os perfis de teste, encenação e publicação de produção. Um exemplo típico de uma configuração que você lidaria em um arquivo de transformação de perfil de publicação porque depende do ambiente de destino é um ponto final wcf que é diferente para teste versus produção. Você criará arquivos de transformação de perfil publicados em tutoriais posteriores depois de criar os perfis de publicação com os que eles vão.

## <a name="disable-debug-mode"></a>Desativar o modo de depuração

Um exemplo de uma configuração que depende da `debug` configuração de compilação em vez do ambiente de destino é o atributo. Para uma compilação de lançamento, você normalmente deseja depurar desativado, independentemente de qual ambiente você está implantando. Portanto, por padrão, os modelos de projeto do Visual Studio criam arquivos `debug` de `compilation` *transformação web.release.config* com código que remove o atributo do elemento. Aqui está o *Web.Release.config*padrão: além de algum código de transformação `compilation` de amostra que `debug` é comentado, ele inclui código no elemento que remove o atributo:

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

O `xdt:Transform="RemoveAttributes(debug)"` atributo especifica que `debug` você deseja que `system.web/compilation` o atributo seja removido do elemento no arquivo *Web.config* implantado. Isso será feito sempre que você implantar uma compilação de liberação.

## <a name="limit-error-log-access-to-administrators"></a>Limitar o acesso ao registro de erros aos administradores

Se houver um erro durante a exibição do aplicativo, o aplicativo exibirá uma página de erro genérica no lugar da página de erro gerada pelo sistema e usará o [pacote Elmah NuGet](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) para registro e emissão de relatórios de erros. O `customErrors` elemento no arquivo *Web.config* do aplicativo especifica a página de erro:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

Para ver a página de `mode` erro, `customErrors` altere temporariamente o atributo do elemento de "RemoteOnly" para "On" e execute o aplicativo do Visual Studio. Causar um erro solicitando uma URL inválida, como *Studentsxxx.aspx*. Em vez de uma página de erro "O recurso não pode ser encontrado" gerado pelo IIS, você verá a página *GenericErrorPage.aspx.*

![Página de erro](web-config-transformations/_static/image2.png)

Para ver o registro de erros, substitua tudo na URL após o `http://localhost:51130/elmah.axd`número da porta por *elmah.axd* (por exemplo) e pressione Enter:

![Página elmah](web-config-transformations/_static/image3.png)

Não se esqueça de `customErrors` definir o elemento de volta ao modo "RemoteOnly" quando terminar.

Em seu computador de desenvolvimento é conveniente permitir acesso gratuito à página de registro de erros, mas na produção isso seria um risco para a segurança. Para o site de produção, você deseja adicionar uma regra de autorização que restringe o acesso de registro de erro aos administradores e garantir que a restrição funcione você também deseja em teste e encenação. Portanto, esta é outra mudança que você deseja implementar cada vez que você implantar uma compilação De sumar, e por isso ela pertence ao arquivo *Web.Release.config.*

Abra *web.release.config* e `location` adicione um novo `configuration` elemento imediatamente antes da tag de fechamento, como mostrado aqui.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

O `Transform` valor de atributo `location` de "Inserir" faz com que `location` esse elemento seja adicionado como um irmão a quaisquer elementos existentes no arquivo *Web.config.* (Já existe `location` um elemento que especifica regras de autorização para a página **Créditos** de Atualização.)

Agora você pode visualizar a transformação para ter certeza de que você codificou corretamente.

No **Solution Explorer,** clique com o botão direito do mouse *na Web.Release.config* e clique **em Transformar a visualização**.

![Visualizar menu Transformar](web-config-transformations/_static/image4.png)

Uma página é aberta que mostra o arquivo *Web.config* de desenvolvimento à esquerda e como será o arquivo *Web.config* implantado à direita, com alterações destacadas.

![Visualização da transformação de depuração](web-config-transformations/_static/image5.png)

![Visualização da transformação de localização](web-config-transformations/_static/image6.png)

( Na visualização, você pode notar algumas alterações adicionais para as quais você não escreveu transformações: estas normalmente envolvem a remoção de espaço em branco que não afeta a funcionalidade.)

Ao testar o site após a implantação, você também testará para verificar se a regra de autorização é eficaz.

> [!NOTE] 
> 
> **Nota de segurança** Nunca exiba detalhes de erro ao público em um aplicativo de produção ou armazene essas informações em um local público. Os atacantes podem usar informações de erro para descobrir vulnerabilidades em um site. Se você usar elmah em seu próprio aplicativo, configure ELMAH para minimizar os riscos de segurança. O exemplo ELMAH neste tutorial não deve ser considerado uma configuração recomendada. É um exemplo que foi escolhido para ilustrar como lidar com uma pasta em que o aplicativo deve ser capaz de criar arquivos. Para obter mais informações, consulte [a proteção do ponto final do ELMAH](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>Uma configuração que você vai lidar em publicar arquivos de transformação de perfil

Um cenário comum é ter configurações de arquivo *Web.config* que devem ser diferentes em cada ambiente para o qual você implanta. Por exemplo, um aplicativo que chama um serviço WCF pode precisar de um ponto final diferente em ambientes de teste e produção. O aplicativo da Universidade Contoso inclui uma configuração deste tipo também. Essa configuração controla um indicador visível nas páginas de um site que informa em que ambiente você está, como desenvolvimento, teste ou produção. O valor de configuração determina se o aplicativo anexará "(Dev)" ou "(Teste)" à posição principal na página-mestre *site.Master:*

![Indicador ambiental](web-config-transformations/_static/image7.png)

O indicador de ambiente é omitido quando a aplicação está em execução em estadiamento ou produção.

As páginas da Web da Universidade contoso leem um valor definido no `appSettings` arquivo *Web.config* para determinar em que ambiente o aplicativo está sendo executado:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

O valor deve ser "Teste" no ambiente de teste e "Prod" para encenação e produção.

O seguinte código em um arquivo de transformação implementará essa transformação:

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

O `xdt:Transform` valor do atributo "SetAttributes" indica que o propósito desta transformação é alterar os valores de atributo de um elemento existente no arquivo *Web.config.* O `xdt:Locator` valor do atributo "Match(key)" indica que `key` o elemento `key` a ser modificado é aquele cujo atributo corresponde ao atributo especificado aqui. O único outro `add` atributo `value`do elemento é , e é isso que será alterado no arquivo *Web.config* implantado. O código mostrado `value` aqui faz `Environment` `appSettings` com que o atributo do elemento seja definido como "Teste" no arquivo *Web.config* que é implantado.

Essa transformação pertence aos arquivos de transformação de perfil de publicação, que você ainda não criou. Você criará e atualizará os arquivos de transformação que implementam essa alteração quando criar os perfis de publicação para os ambientes de teste, encenação e produção. Você fará isso na [implantação para IIS](deploying-to-iis.md) e [implantará em](deploying-to-production.md) tutoriais de produção.

> [!NOTE]
> Como essa configuração `<appSettings>` está no elemento, você tem outra alternativa para especificar a transformação quando estiver implantando em Aplicativos web no Serviço de Aplicativos Do Azure [Ver especificando configurações da Web.config no Azure](#watransforms) mais cedo neste tópico.

## <a name="setting-connection-strings"></a>Configurar cadeias de conexão

Embora o arquivo de transformação padrão contenha um exemplo que mostra como atualizar uma seqüência de conexões, na maioria dos casos você não precisa configurar transformações de seqüência de conexões, porque você pode especificar strings de conexão no perfil de publicação. Você fará isso na [implantação para IIS](deploying-to-iis.md) e [implantará em](deploying-to-production.md) tutoriais de produção.

## <a name="summary"></a>Resumo

Você já fez o máximo que pode com as transformações *da Web.config* antes de criar os perfis de publicação e viu uma prévia do que estará no arquivo Web.config implantado.

![Visualização da transformação de localização](web-config-transformations/_static/image8.png)

No tutorial a seguir, você cuidará das tarefas de configuração de implantação que requerem a definição das propriedades do projeto.

## <a name="more-information"></a>Mais informações

Para obter mais informações sobre os tópicos abordados por este tutorial, consulte [Usando transformações da Web.config para alterar configurações no arquivo destino Web.config ou app.config file durante](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) a implantação no Mapa de Conteúdo de Implantação da Web para o Visual Studio e ASP.NET.

> [!div class="step-by-step"]
> [Próximo](preparing-databases.md)
> [anterior](project-properties.md)
