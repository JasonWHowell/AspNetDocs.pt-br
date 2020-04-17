---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Melhorias no Visual Studio 2005 | Microsoft Docs
author: rick-anderson
description: O Visual Studio 2005 fornece aos desenvolvedores de aplicativos da Web uma longa lista de melhorias e melhorias em projetos web.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: e98771614bf4e0095f8ff596e7cdb26c8c9de1ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542970"
---
# <a name="improvements-in-visual-studio-2005"></a>Aprimoramentos no Visual Studio 2005

pela [Microsoft](https://github.com/microsoft)

> O Visual Studio 2005 fornece aos desenvolvedores de aplicativos da Web uma longa lista de melhorias e melhorias em projetos web.

O Visual Studio 2005 fornece aos desenvolvedores de aplicativos da Web uma longa lista de melhorias e melhorias em projetos web. Por mais poderosos que o Visual Studio .NET 2002 e 2003 sejam, houve muitas reclamações na forma como os projetos web foram tratados. Visual Studio 2005 adiciona um número significativo de novos recursos para resolver essas reclamações. Para aqueles que preferem a maneira que o Visual Studio .NET 2003 lidou com a compilação de aplicações Web, consulte [Projetos de Aplicativos Web](https://go.microsoft.com/fwlink/?LinkId=57870).

Neste módulo, cobre melhorias na criação, gerenciamento e desenvolvimento de projetos web. Em um módulo posterior, cobre bem melhorias na construção de projetos Web e implantação deles.

## <a name="frontpage-server-extensions"></a>Extensões do servidor frontpage

O Visual Studio .NET 2002 e 2003 exigiram extensões do Servidor FrontPage na caixa para criar ou construir projetos web. Os desenvolvedores escolheram entre dois modos de acesso diferentes (Extensões do Servidor frontpage ou modo de acesso a arquivos), ambos usaram extensões do Servidor FrontPage para executar tarefas como definir a raiz do aplicativo no IIS, etc.

Visual Studio 2005 remove a dependência de extensões do Servidor FrontPage para projetos locais. O Visual Studio 2005 agora acessa a metabase do IIS diretamente em vez de usar as extensões do servidor FrontPage. O Visual Studio 2005 também adiciona suporte ao FTP, que permite acesso remoto a projetos sem precisar de extensões do FrontPage Server.

Para aqueles desenvolvedores que desejam usar o FrontPage Server Extensions em seus projetos, a opção ainda está disponível. No entanto, com base no forte feedback da comunidade de desenvolvedores ASP.NET, não é um requisito.

> [!NOTE]
> As extensões do Servidor FrontPage ainda são necessárias para criação remota de projetos, abertura, etc.

## <a name="aspnet-development-server"></a>ASP.NET Development Server

O Visual Studio 2005 é fornecido com um novo servidor Web chamado ASP.NET Development Server. (Este servidor Web era anteriormente conhecido como Cassini.)

Existem vários benefícios do Servidor de Desenvolvimento ASP.NET.

- Agora é possível que os não-administradores desenvolvam e depuram um servidor Web.
- O ASP.NET Development Server mapeia dinamicamente diretórios virtuais para qualquer local do sistema de arquivos, permitindo locais flexíveis do projeto.
- Os usuários do Windows XP Professional que já estão usando o IIS agora poderão criar novos aplicativos da Web que não afetarão a estrutura de arquivos ou pastas de seu Site padrão no IIS.

Nenhuma configuração especial é necessária para aproveitar o ASP.NET Development Server. Quando um projeto web hospedado no sistema de arquivos é depurado ou navegado, o Visual Studio 2005 iniciará automaticamente uma instância do ASP.NET Development Server em uma porta aleatória para atender a solicitação.

Mais informações serão abordadas no ASP.NET Development Server mais tarde neste módulo.

## <a name="improved-file-management"></a>Gerenciamento aprimorado de arquivos

No Visual Studio 2002 e 2003, um arquivo de projeto (.vbproj para VB.NET e .csproj para C#) armazenava informações em todos os arquivos do aplicativo Web. O visor do Solution Explorer é baseado nas informações do arquivo no arquivo do projeto. Por causa disso, o Solution Explorer frequentemente exibia informações imprecisas nos casos em que editores externos foram usados. Visual Studio 2002 e 2003 muitas vezes sobreporiam alterações de arquivo ou não exibiam a versão mais recente dos arquivos.

Visual Studio 2005 acaba com o arquivo do projeto. Em vez disso, ele lê as informações do arquivo e da pasta diretamente do disco, resultando em uma exibição precisa dos arquivos em seu projeto. Como a pasta Referências no Visual Studio 2002 e 2003 não representa uma pasta real em seu aplicativo web, o Visual Studio 2005 também remove a pasta Referências do Solution Explorer. Para acessar as referências do seu projeto no Visual Studio 2005, você deve usar as páginas de Propriedade para o projeto.

## <a name="creating-web-projects"></a>Criando Projetos web

Os desenvolvedores web têm muitas novas opções disponíveis para criação de projetos no Visual Studio 2005. Os sites da Web agora podem ser criados em qualquer lugar do sistema de arquivos e, em seguida, podem ser depurados ou navegados usando o novo ASP.NET Development Server. Os desenvolvedores também podem criar novos sites usando FTP.

Clique aqui para ver um passo a passo da criação de projetos web no Visual Studio 2005.

![](improvements-in-visual-studio-2005/_static/image1.png)

[Abra o vídeo em tela cheia](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>Projetos do sistema de arquivos

Como você viu no passo a passo do vídeo, você pode optar por criar sites na Web no sistema de arquivos na máquina local ou em um local remoto através de um compartilhamento de arquivos. Os sites criados no sistema de arquivos são navegados e depurados usando o ASP.NET Development Server.

> [!NOTE]
> O ASP.NET Development Server pode causar alguma confusão para os clientes. Se um projeto web for criado no sistema de arquivos na estrutura do diretório IISs (ou seja, c:/inetpub/wwwroot), o site ainda será navegado através do ASP.NET Development Server quando lançado a partir de dentro do Visual Studio 2005. Portanto, qualquer configuração de IIS (ou seja, métodos de autenticação) não é aplicável.

O projeto web padrão também remove grande parte da sobrecarga, incluindo apenas uma página Default.aspx, default.cs arquivo e uma pasta App/_Data. O web.config e as pastas especiais (ou seja, aplicativo/_code) são adicionados conforme necessário. Seu projeto web só inclui os arquivos e pastas que você precisa.

### <a name="http-projects"></a>Projetos HTTP

Projetos HTTP podem ser projetos criados em um site local do IIS ou em um site remoto. O local padrão `http://localhost`do projeto é . Se você clicar no botão Procurar, há duas opções HTTP: IIS local e Site remoto. A principal diferença nessas duas opções é o método no qual as informações do site são exibidas na caixa de diálogo Escolher local e em como os arquivos são copiados para o servidor web.

A opção IIS local lê as informações do site da metabase na máquina local e os arquivos são copiados usando o sistema de arquivos. A opção Site remoto usa as extensões do servidor frontpage e as informações e arquivos do site são copiados usando chamadas RPC HTTP e FrontPage Server Extensions.

> [!NOTE]
> O arquivo vs###/_tmp.htm e get/_aspx/_ver.aspx não são mais usados para determinar informações da versão.

A opção HTTP padrão é IIS local. Esta opção lê o Metabase do IIS para determinar quais sites estão disponíveis e o local em que criar conteúdo. Você pode selecionar uma pasta ou diretório virtual diferente selecionando-o na exibição da árvore. Você também pode criar um novo diretório virtual, marcar pastas como aplicativos, bem como excluir diretórios virtuais existentes a partir desta caixa de diálogo.

![A caixa de diálogo Escolher local](improvements-in-visual-studio-2005/_static/image1.gif)

**Figura 1**: A caixa de diálogo Escolher local

Ao contrário das versões anteriores do Visual Studio, se você verificar a caixa de seleção **Use Secure Sockets Layer** e o certificado SSL não corresponder à URL que você está navegando, você será apresentado com uma caixa de diálogo Alerta de Segurança perguntando se você gostaria de prosseguir. Usando o Visual Studio .NET 2003, se o certificado não fosse compatível, a criação do projeto falharia.

![Alerta de segurança em relação ao certificado SSL](improvements-in-visual-studio-2005/_static/image2.gif)

**Figura 2:** Alerta de segurança em relação ao certificado SSL

### <a name="note-on-host-headers"></a>Nota sobre cabeçalhos de host

Se você estiver criando um aplicativo da Web em um site vinculado a um IP específico, você precisará garantir que um cabeçalho de host esteja configurado. Caso contrário, o Visual Studio `http://localhost`criará o site em , mas o endereço IP não será resolvido corretamente quando o site for navegado ou depurado de dentro do IDE.

Se você selecionar a opção Site remoto, a caixa de diálogo será alterado para permitir que você insira a URL de destino para o novo site da Web. Esta URL deve estar em um servidor que tenha as extensões do servidor frontpage ativadas. Se você quiser trabalhar com o servidor web local usando as extensões do servidor frontpage, você pode usar a opção Site remoto e especificar uma URL local.

![Criando um site em um servidor remoto](improvements-in-visual-studio-2005/_static/image1.jpg)

**Figura 3:** Criando um site em um servidor remoto

Ao criar um aplicativo em um site remoto via SSL, se o certificado SSL não corresponder, a caixa de diálogo de confirmação será ligeiramente diferente da caixa de diálogo exibida ao usar a opção IIS local.

![O alerta de segurança do local remoto](improvements-in-visual-studio-2005/_static/image3.gif)

**Figura 4:** O alerta de segurança do local remoto

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 introduz a opção de criar sites via FTP. Quando você usa essa opção, o IDE cria os arquivos localmente na pasta temporária dos usuários e, em seguida, usa FTP para mover os arquivos para o local FTP.

> [!NOTE]
> O local da pasta temporária é c:/Documentos e&lt;Configurações/ Usuário&gt;/Configurações&lt;&gt;locais/Temp/VWDWebCache/ Nome do aplicativo Server /_&lt;&gt;

Ao usar a opção FTP, você será apresentado com uma caixa de diálogo Escolher local. Você insere as informações de conexão FTP necessárias nesta caixa de diálogo, conforme mostrado abaixo.

![O diálogo escolher local para FTP](improvements-in-visual-studio-2005/_static/image2.jpg)

**Figura 5**: O diálogo de localização de escolha para FTP

## <a name="lab-setup-ftp-site-and-create-a-project"></a>Laboratório: Configure o site ftp e crie um projeto

As etapas a seguir configuram o site FTP para que um usuário tenha um local que só eles podem carregar via FTP.

### <a name="install-the-ftp-service"></a>Instale o serviço FTP

1. Abrir adicionar programas de remover, selecionar adicionar/remover componentes do Windows
2. Selecione serviços de informações da Internet (Servidor de aplicativos no Windows 2003) e clique em **Detalhes**.
3. Verifique **o serviço do Protocolo de Transferência de Arquivos (FTP)** e clique em **OK**.
4. Clique **em Next** para instalar o serviço FTP.

### <a name="create-a-new-folder-for-content"></a>Criar uma nova pasta para conteúdo

1. No Windows Explorer, crie uma nova pasta chamada **User1** dentro de c:/inetpub/wwwroot.

#### <a name="configure-folders-and-permissions-on-folders"></a>Configure pastas e permissões em pastas.

1. Abra o snap-in dos Serviços de Informação da Internet a partir de Ferramentas Administrativas. Agora você terá uma pasta FTP Sites sob o nó nome do computador.
2. Expandir **sites FTP**.
3. Clique com o botão direito do mouse no **site FTP padrão,** selecione **Novo,** depois **Diretório Virtual,** e clique em **Next**.
4. Digite **User1** para o nome do diretório virtual e clique **em Next**.
5. Digite **c:/inetpub/wwwroot/User1** para o caminho e clique **em Next**.
6. Clique **em Avançar** e, em seguida, **termine** para completar o assistente.
7. Clique com o botão direito do mouse no diretório virtual **User1** em Default FTP Site e selecione **Propriedades**.
8. Verifique a **caixa de** seleção Escrever e clique em **OK** para fechar a caixa de diálogo.
9. Clique com o botão direito do mouse **no site FTP padrão** e selecione **Propriedades**.
10. Na guia **Contas de segurança,** desfaça **a verificação De permitir conexões anônimas**.
11. Clique em **Sim** na caixa de diálogo perguntando se você deseja continuar.
12. Clique em **OK** para fechar o diálogo.
13. Expanda **o site padrão no** nó **Sites** da Web.
14. Clique com o botão direito do mouse no diretório **User1** e selecione **Propriedades**
15. Na seção Configurações do **aplicativo,** clique em **Criar** para marcar a pasta como um aplicativo.
16. Clique em **OK** para fechar o diálogo.
17. Feche o snap-in dos Serviços de Informação da Internet.

### <a name="create-web-project"></a>Criar projeto web

1. Open Visual Studio 2005.
2. No menu **Arquivo,** selecione **Novo site**.
3. Na queda **de localização,** selecione **FTP**.
4. Clique em **Procurar**.
5. Digite **localhost** na caixa de texto **do servidor.**
6. Digite **User1** na caixa de texto do Diretório.
7. Clique em **Abrir**. A localização do FTP será inserida na caixa de diálogo Novo Site.
8. Clique em **OK**.
9. Desmarcar **o logon anônimo** na caixa de diálogo Log On do FTP, digite suas credenciais e clique em **OK**.
10. Qual é a URL do projeto? (A URL do projeto será exibida no Solution Explorer.)
11. No menu **Build,** selecione **Build Web Site** ou Build **Solution**.
12. Clique com o botão direito do mouse no Default.aspx no Solution Explorer e selecione **Exibir no Navegador**.
13. Na caixa de diálogo url `http://localhost/user1` do site da Web, digite a URL e clique em **OK**.

> [!NOTE]
> Se você tiver um erro que indique uma incapacidade de carregar o tipo /_Default, certifique-se de que você está executando ASP.NET 2.0 em seu site e não em uma versão anterior. Você pode fazer isso a partir da guia ASP.NET em Serviços de Informação da Internet.

## <a name="opening-web-projects"></a>Abrindo projetos web

Abrir projetos web é semelhante à criação de projetos. As seções a seguir chamam as áreas para ficar de olho enquanto trabalham dentro do IDE. Também abrange trabalhar com projetos web usando HTTP e FTP.

Para abrir um projeto web, selecione Abrir o site no menu Arquivo. Você será solicitado com a mesma caixa de diálogo Escolher local coberta anteriormente e você tem as mesmas quatro opções disponíveis para você: Sistema de arquivos, IIS local, FTP e Local Remoto.

<a id="_Toc116100245"></a>

## <a name="file-system"></a>Sistema de Arquivos

Como indicado anteriormente neste módulo, o Visual Studio não usa mais um arquivo de projeto. Portanto, se você optar por abrir um site da Web a partir do sistema de arquivos, você realmente tem a opção de escolher qualquer pasta que desejar, mesmo que a pasta que você escolher não tenha sido criada como um projeto web inicialmente no Visual Studio. Por exemplo, você pode optar por abrir a pasta Meus Documentos como um site da Web e o Visual Studio a abrirá alegremente e exibirá seus arquivos como mostrado abaixo.

![Meus documentos abertos como um site](improvements-in-visual-studio-2005/_static/image3.jpg)

**Figura 6**: *Meus documentos* abertos como um site

Como o Visual Studio só cria arquivos e pastas adicionais quando necessário, nenhum arquivo ou pasta adicional é adicionado ao local aberto. Um efeito colateral dessa arquitetura é que ela impede que você aninham sites da Web no sistema de arquivos. Por exemplo, considere a seguinte estrutura de diretório.

Projeto web em C:/MyWebSite

Outro projeto web em C:/MyWebSite/Aninhado

Quando você abrir o site da Web em c:/MyWebSite, a pasta Aninhado aparecerá como uma subpasta desse aplicativo.

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

Ao abrir sites da Web via HTTP, as configurações são lidas a partir da metabase IIS (IIS local) ou usando extensões do servidor frontpage (Local remoto).) Se houver aplicativos web aninhados, estes também serão exibidos com um ícone que os identifica como um aplicativo. Se você está familiarizado com o trabalho com aplicativos web no FrontPage, o comportamento no Visual Studio 2005 é semelhante.

Embora o Visual Studio exiba um ícone para aplicativos aninhados abaixo do aplicativo que está atualmente aberto dentro do IDE, ele não permitirá que você os expanda para ver seu conteúdo. Você pode, no entanto, clicar duas vezes neles para abri-los. Quando o fizer, será apresentado um diálogo solicitando que você abra o aplicativo web (e substitua a solução aberta atualmente) ou adicione o aplicativo da Web à sua solução atual.

![Clicar duas vezes em um ícone de aplicativo aninhado apresenta-lhe esta caixa de diálogo](improvements-in-visual-studio-2005/_static/image4.jpg)

**Figura 7**: Clicar duas vezes em um ícone de aplicativo aninhado apresenta-lhe esta caixa de diálogo

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>Site FTP

Quando você abre um site via FTP, os arquivos são todos copiados localmente para sua pasta temporária. O caminho completo para o local de armazenamento local é exibido no painel Propriedades para o projeto e é criado usando o seguinte formato.

C:/Documentos e&lt;Configurações/ Usuário&gt;/Configurações locais/Temp/VWDWebCache/&lt;Nome do aplicativo Server&gt;/_&lt;&gt;

Ao usar o FTP, o Visual Studio precisará especificar a URL base do seu projeto para que você possa navegá-lo como mostrado abaixo. Se você não especificar uma URL base, o Visual Studio pedirá a você na primeira vez que você tentar navegar em uma página no site da Web.

![Especificando uma URL base para sites FTP](improvements-in-visual-studio-2005/_static/image5.jpg)

**Figura 8:** Especificando uma URL base para sites FTP

## <a name="improvements-in-compilation"></a>Melhorias na Compilação

Trabalhar com aplicações web no Visual Studio 2005 é visivelmente mais rápido do que as versões anteriores. Isso se deve, em grande parte, às mudanças na arquitetura de compilação.

No Visual Studio 2002 e 2003, os aplicativos da Web foram compilados em um conjunto primário residente na pasta /bin. No Visual Studio 2005, uma pasta app/_Code foi adicionada. Classes e outros códigos não-UI são adicionados à pasta App/_Code. Quando o Visual Studio constrói o projeto, todos os arquivos da pasta App/_Code são compilados em um único arquivo App/_Code.dll. O resultado dessa mudança é que as compilações subseqüentes são muito mais rápidas do que nas versões anteriores.

> [!NOTE]
> O utilitário de linha de comando MSBuild também pode ser usado para criar aplicativos ASP.NET Web. Essa ferramenta será coberta no módulo 9.

Outro aprimoramento de compilação é a nova opção Build Page no menu Build. Esse recurso permite que um desenvolvedor reconstrua apenas a página atual (juntamente com, é claro, e dependências) para que as alterações possam ser compiladas mais rapidamente. Como c# não oferece compilação em segundo plano para fins de atualização do IntelliSense, etc., eles se beneficiarão imensamente desse recurso porque permitirá que o IntelliSense seja atualizado rapidamente simplesmente reconstruindo uma única página.

As propriedades Build para um projeto permitem configurar o tipo de compilação que ocorre antes da página de inicialização ser executada. Os desenvolvedores podem optar por construir apenas a página atual para que o Visual Studio possa começar a depurar aplicativos mais rapidamente após alterações de código.

![A ação iniciar da página de compilação](improvements-in-visual-studio-2005/_static/image6.jpg)

**Figura 9**: A ação iniciar a página de compilação

Outro grande aprimoramento para o Visual Studio e a arquitetura ASP.NET está na área de editar e continuar. No Visual Studio 2005, os desenvolvedores podem começar a depurar um projeto e fazer alterações de código no projeto sem desprender o depurador. Na verdade, você pode literalmente começar a depurar um projeto, adicionar uma nova classe, adicionar código a essa classe, adicionar código à sua página que cria uma nova instância dessa classe e executar um método da classe, tudo sem separar o depurador. Executar o novo código é literalmente tão fácil quanto atualizar o navegador!

Clique aqui para ver um passo a passo da edição e continuar no Visual Studio 2005.

![](improvements-in-visual-studio-2005/_static/image2.png)

[Abra o vídeo em tela cheia](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

A funcionalidade robusta de edição e continuidade em ASP.NET 2.0 e Visual Studio 2005 deve-se a uma mudança arquitetônica para aplicações ASP.NET. Em ASP.NET 1.x, os aplicativos criados no Visual Studio 2002/2003 foram compilados em um conjunto primário que foi armazenado na pasta /bin. Todas as classes, páginas, etc. para a aplicação foram compiladas em que um DLL. Em seguida, em tempo de execução, ASP.NET compilaria todos os controles, marcação e código ASP.NET dentro das páginas e copiaria esses DLLs na pasta temporária ASP.NET.

No Visual Studio 2005, utilizando ASP.NET 2.0, os dois modelos de compilação contornoacima (um para o Visual Studio e um para ASP.NET em tempo de execução) foram fundidos em um modelo de compilação comum. Isso significa que todos os problemas de compilação são agora pegos durante a fase de desenvolvimento em vez de em tempo de execução. Ele também permite o suporte de designer e IntelliSense para recursos como controles de usuário e páginas-mestre.

Clique aqui para ver um passo a passo do suporte do designer para controles de usuário.

![](improvements-in-visual-studio-2005/_static/image3.png)

[Abra o vídeo em tela cheia](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> Quando um controle de usuário é @Register removido de uma página, a diretiva permanece na marcação e deve ser removida manualmente para evitar erros de analisador se o controle do usuário for excluído do site da Web.

Outra melhoria no modelo de compilação do Visual Studio é o recurso Publish Web Site. Como o recurso Publicar pré-compila o site da Web, os desenvolvedores podem desfrutar do desempenho adicional de não ter que compilar nada sob demanda. Ele também précompila todo o código-fonte na pasta App/_Code em uma DLL para que nenhum código fonte tenha que ser implantado.

![O diálogo do site publicar](improvements-in-visual-studio-2005/_static/image7.jpg)

**Figura 10**: O Diálogo do Site publicar

> [!NOTE]
> O utilitário aspnet/_compile.exe também pode ser usado para pré-compilar um aplicativo ASP.NET Web. Essa ferramenta será coberta no módulo 9.

Quando você publica um site da Web, os arquivos pré-compilados são armazenados na pasta Arquivos ASP.NET Temporários, conforme mostrado abaixo. Arquivos com uma extensão de arquivo *.compilada* são arquivos XML que definem dependências para DLLs específicos. Qualquer Webform ou controles de usuário são compilados em DLLs aleatórios que começam com *App/_Web/_*.

Se você deixar que este site pré-compilado seja verificado na caixa de *seleção updatable,* a marcação dentro de seus Webforms e controles de usuário não será pré-compilada em uma DLL permitindo que você faça alterações após a implantação. Se preferir bloquear a marcação para que as alterações no conteúdo implantado não sejam permitidas, desmarque esta caixa.

A *caixa de seleção Use nomeação fixa e conjuntos de páginas únicas* permite desabilitar a compilação em lote para que cada página seja compilada em um conjunto com nome fixo. Deixar esta caixa sem controle permite que você aproveite a compilação em lote.

A *caixa de seleção Ativar forte nomeação em conjuntos pré-compilados* permite que você nomeie fortemente seus conjuntos pré-compilados.

> [!NOTE]
> Em ASP.NET 1.x, conjuntos com nome forte tiveram que ser instalados no Global Assembly Cache (GAC). Em ASP.NET 2.0, você não é obrigado a instalar conjuntos com nomes fortes no GAC.

![Um ASP.NET aplicativos pré-compilados arquivos](improvements-in-visual-studio-2005/_static/image8.jpg)

**Figura 11:** Um ASP.NET aplicativos arquivos pré-compilados

> [!NOTE]
> No aplicativo acima, não havia nenhum arquivo web.config. Se houvesse, teria sido chamado *de PrecompileApp.config* após o processo publicar o site.

## <a name="improvements-in-deployment"></a>Melhorias na Implantação

Assim como no Visual Studio 2002 e 2003, o Visual Studio 2005 oferece um recurso copy project. No entanto, o recurso foi reforçado no Visual Studio 2005 e agora é chamado de Copy Web Site.

A caixa de diálogo Copiar o site é dividida em um quadro esquerdo e um quadro direito. O quadro esquerdo é chamado de Site da Fonte e o quadro direito é chamado de Site Remoto. Uma coisa que pode confundir alguns desenvolvedores é que o site exibido no quadro certo não é necessariamente um site remoto. Pode ser um site no sistema de arquivos local ou na instância local do IIS. Além disso, o site exibido no quadro esquerdo não é necessariamente o site de origem porque a caixa de diálogo permite que você publique do site remoto *para* o site de origem.

Se você estiver copiando um projeto para um site remoto, esse site deve ter as Extensões do Servidor frontpage instaladas nele. Se isso não acontecer, você precisará se conectar usando FTP. Por outro lado, se você estiver copiando um projeto para a instância IIS local, as extensões do servidor frontpage não serão necessárias.

> [!NOTE]
> Se você tentar criar um novo site na instância IIS local e as extensões do servidor frontpage 2002 estiverem instaladas, você receberá uma mensagem de erro dizendo que a criação de sites da Web não é suportada em um servidor SharePoint. Nesse caso, você tem a opção de instalar as extensões do servidor FrontPage 2000 ou remover as extensões do servidor frontpage.

Clique aqui para obter um passo a passo do recurso Copy Web Site.

![](improvements-in-visual-studio-2005/_static/image4.png)

[Abra o vídeo em tela cheia](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>Melhorias na depuração

Existem quatro melhorias importantes na depuração no Visual Studio 2005.

- Depurar localmente como um não-administrador é possível fora da caixa.
- O atributo Debug para o elemento Compilação agora é falso por padrão.
- A configuração e configuração de depuração remota é mais fácil do que antes.
- Agora você pode depurar um site aberto através de um local FTP.

## <a name="debugging-as-a-non-administrator"></a>Depuração como não-administrador

A adição do ASP.NET Development Server permite que os não-administradores depuram facilmente ASP.NET aplicativos logo de fora da caixa. Quando um aplicativo ASP.NET em execução no sistema de arquivos local é depurado, o Visual Studio inicia o ASP.NET Development Server sob o contexto do usuário conectado. Esse usuário pode então depurar esse aplicativo sem qualquer configuração adicional.

## <a name="debug-is-false-by-default"></a>Depuração é falsa por padrão

Em ASP.NET 1.x, o atributo *de depuração* no elemento *compilação* do arquivo web.config foi definido *como verdadeiro* por padrão. Sempre foi recomendado que os desenvolvedores definissem esse atributo como *falso* antes de implantar um aplicativo para a produção, mas como a maioria dos desenvolvedores não entende completamente as consequências de deixar o atributo de depuração definido como verdadeiro, eles simplesmente deixaram-no como está.

O problema mais grave de ter o atributo de depuração definido como verdadeiro é que ele desativa o modelo de compilação em lote ASP.NETs. Portanto, cada página é compilada em um DLL separado. Se um aplicativo da Web consiste em milhares de páginas (não inéditas por qualquer meio), isso significa que vários milhares de Pequenos DLLs serão criados por esse aplicativo. Embora esses DLLs sejam pequenos em tamanho, eles não são carregados em nenhum local específico na memória. Portanto, eles causam fragmentação na memória do sistema e podem contribuir para ocorrências outofmemoryexception.

Em ASP.NET 2.0, o atributo de depuração é definido como falso por padrão. Como você já viu, quando um desenvolvedor depura um aplicativo ASP.NET no Visual Studio 2005, eles são solicitados a adicionar um arquivo web.config com depuração ativada. Ao fazer isso, incorre nas mesmas desvantagens que estavam presentes em ASP.NET 1.x, mas agora o desenvolvedor está claramente avisado de que o atributo deve ser redefinido para falso antes de mover o aplicativo para a produção.

## <a name="remote-debugging-setup-and-configuration"></a>Configuração e configuração de depuração remota

No Visual Studio 2002/2003, a depuração remota contava com o Gerenciador de Depuração de Máquinas (mdm.exe) e o processo vs7jit.exe. Por causa disso, a solução de problemas de depuração remota era muitas vezes uma caixa preta para os clientes e muitas vezes não era muito melhor para pss.

Visual Studio 2005 remove a dependência dos processos mdm.exe e vs7jit.exe. Em vez disso, ele agora usa o serviço Remote Debug Monitor (msvsmon.exe.)

A exigência de depuração no Visual Studio 2005 remotamente é bastante simples. Você precisa executar msvsmon.exe no servidor remoto antes de depurar. Você pode instalar o Monitor de Depuração Remota a partir do CD do Visual Studio ou simplesmente executar msvsmon.exe a partir de um compartilhamento sem instalar nada no servidor web.

Quando você executa msvsmon.exe, é provável que ele reclame sobre as portas serem bloqueadas para depuração remota. Felizmente, você pode facilmente desbloquear as portas da direita dentro da caixa de diálogo de aviso, conforme mostrado abaixo.

![Notificação de que o Firewall do Windows está bloqueando a depuração remota](improvements-in-visual-studio-2005/_static/image9.jpg)

**Figura 12**: Notificação de que o Firewall do Windows está bloqueando a depuração remota

Depois de desbloquear as portas necessárias para a depuração, você verá o Monitor de Depuração Remota como mostrado abaixo. A partir desta interface, você pode monitorar conexões e alterar facilmente as permissões de depuração.

![O monitor de depuração remota](improvements-in-visual-studio-2005/_static/image10.jpg)

**Figura 13**: O monitor de depuração remota

Também é possível depurar remotamente um aplicativo web aberto via FTP. Os passos são os mesmos que os anteriormente cobertos. No entanto, você precisará especificar uma URL base para navegar no projeto FTP como descrito anteriormente neste módulo.

## <a name="lab-2"></a>Laboratório 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Depuração remota com Visual Studio 2005

Este laboratório vai levá-lo através de depuração remota com visual studio 2005.

Clique aqui para um vídeo passo a passo deste laboratório.

![](improvements-in-visual-studio-2005/_static/image5.png)

[Abra o vídeo em tela cheia](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

Este laboratório exige que você tenha duas máquinas, uma executando o Visual Studio 2005 e a outra executando o IIS 5 ou superior.

1. Abra o Visual Studio 2005 e crie um novo site no servidor remoto.

> [!NOTE]
> Você pode criar o site em uma instância IIS remota ou via FTP.

1. A partir do servidor Web remoto, localize msvsmon.exe na máquina de desenvolvimento usando um caminho UNC e execute-o.  
 O local padrão para msvsmon.exe é //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.
2. Se solicitado a desbloquear portas para depuração remota, faça-o.
3. A partir da máquina de desenvolvimento, abra o code-behind para Default.aspx e defina um ponto de ruptura no método Página/_Load.
4. Comece a depurar da máquina de desenvolvimento.

Você deve acertar o ponto de ruptura como esperado.

## <a name="aspnet-development-server"></a>ASP.NET Development Server

Como já discutimos, o Visual Studio 2005 é fornecido com um servidor Web chamado ASP.NET Development Server. (O servidor de desenvolvimento ASP.NET às vezes é referido como Cassini.) Este servidor Web é um meio conveniente para navegar e depurar aplicativos da Web em execução no sistema de arquivos.

O ASP.NET Development Server é um servidor Web restrito. Ele não permite conexões remotas, não permite nenhuma solicitação de qualquer usuário que não seja o usuário que iniciou o servidor Web. Ele também não tem a capacidade de servir páginas ASP. Apenas ASP.NET recursos e recursos HTML (incluindo imagens, arquivos CSS, etc.) são servidos.

O ASP.NET Development Server pode ser iniciado através da linha de comando executando o arquivo WebDev.WebServer.exe localizado em*/*/*/* c:/Windows/Microsoft.NET/Framework/v2.0./ /*. A caixa de diálogo a seguir exibe os parâmetros disponíveis.

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**Figura 14**

> [!NOTE]
> O ASP.NET Development Server não é suportado quando lançado explicitamente através da linha de comando.
