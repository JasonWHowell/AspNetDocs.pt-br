---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: Perfis, Temas e Web Parts | Microsoft Docs
author: rick-anderson
description: Há grandes mudanças na configuração e instrumentação no ASP.NET 2.0. A nova aPI de configuração ASP.NET permite que as alterações de configuração sejam feitas pr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: 4bc98cca226a0bd9bd766a21e88b0facf2a4b610
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543633"
---
# <a name="profiles-themes-and-web-parts"></a>Perfis, temas e Web Parts

pela [Microsoft](https://github.com/microsoft)

> Há grandes mudanças na configuração e instrumentação no ASP.NET 2.0. A nova API de configuração ASP.NET permite que as alterações de configuração sejam feitas de forma programática. Além disso, muitas novas configurações existem permitem novas configurações e instrumentação.

ASP.NET 2.0 representa uma melhoria substancial na área de sites personalizados. Além dos recursos de associação que já cobrimos, ASP.NET perfis, temas e partes da Web melhoram significativamente a personalização em sites da Web.

## <a name="aspnet-profiles"></a>perfis de ASP.NET

ASP.NET perfis são semelhantes às sessões. A diferença é que um perfil é persistente enquanto uma sessão é perdida quando o navegador é fechado. Outra grande diferença entre sessões e perfis é que os perfis são fortemente digitados, fornecendo assim o IntelliSense durante o processo de desenvolvimento.

Um perfil é definido no arquivo de configuração das máquinas ou no arquivo web.config para o aplicativo. (Não é possível definir um perfil em um arquivo web.config de subpastas.) O código abaixo define um perfil para armazenar o primeiro e sobrenome dos visitantes do site.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

O tipo de dados padrão de uma propriedade de perfil é System.String. No exemplo acima, nenhum tipo de dados foi especificado. Portanto, as propriedades FirstName e LastName são ambas do tipo String. Como mencionado anteriormente, as propriedades do perfil são fortemente digitadas. O código abaixo adiciona uma nova propriedade para a idade que é do tipo Int32.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

Os perfis são geralmente usados com ASP.NET autenticação Forms. Quando usado em combinação com a autenticação de Formulários, cada usuário tem um perfil separado associado ao seu ID de usuário. No entanto, também é possível permitir o uso de &lt;perfis&gt; em um aplicativo anônimo usando o elemento identificador anônimo no arquivo de configuração, juntamente com o atributo **allowAnonymous,** conforme mostrado abaixo:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

Quando um usuário anônimo navega pelo site, ASP.NET cria uma instância do **ProfileCommon** para o usuário. Este perfil usa um ID exclusivo armazenado em um cookie no navegador para identificar o usuário como um visitante único. Desta forma, você pode armazenar informações de perfil para usuários que estão navegando anonimamente.

## <a name="profile-groups"></a>Grupos de perfil

É possível agrupar propriedades de perfis. Ao agrupar propriedades, é possível simular vários perfis para um aplicativo específico.

A configuração a seguir configura uma propriedade FirstName e LastName para dois grupos; Compradores e Prospects.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

Em seguida, é possível definir propriedades em um determinado grupo da seguinte forma:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>Armazenamento de objetos complexos

Até agora, os exemplos que cobrimos armaram tipos de dados simples em um perfil. Também é possível armazenar tipos de dados complexos em um perfil especificando o método de serialização usando o atributo **serializeAs** a seguir:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

Neste caso, o tipo é PurchaseInvoice. A classe PurchaseInvoice precisa ser marcada como serializável e pode conter qualquer número de propriedades. Por exemplo, se purchaseinvoice tiver um imóvel chamado **NumItemsComprado,** você pode consultar essa propriedade em código da seguinte forma:

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>Herança de perfil

É possível criar um perfil para uso em vários aplicativos. Ao criar uma classe de perfil que deriva do ProfileBase, você pode reutilizar um perfil em vários aplicativos usando o atributo **herdado** como mostrado abaixo:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

Neste caso, a classe **BuyingProfile** seria assim:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>Provedores de perfil

ASP.NET perfis usam o modelo do provedor. O provedor padrão armazena as informações em um banco\_de dados SQL Server Express na pasta Dados do aplicativo da Web usando o provedor SqlProfileProvider. Se o banco de dados não existir, ASP.NET o criará automaticamente quando o perfil tentar armazenar informações.

Em alguns casos, no entanto, você pode querer desenvolver seu próprio provedor de perfil. O recurso de perfil ASP.NET permite que você use facilmente diferentes provedores.

Você cria um provedor de perfil personalizado quando:

- Você precisa armazenar informações de perfil em uma fonte de dados, como em um banco de dados FoxPro ou em um banco de dados Oracle, que não é suportado pelos provedores de perfil incluídos no .NET Framework.
- Você precisa gerenciar informações de perfil usando um esquema de banco de dados diferente do esquema de banco de dados usado pelos provedores incluídos no .NET Framework. Um exemplo comum é que você deseja integrar informações de perfil com dados do usuário em um banco de dados SQL Server existente.

### <a name="required-classes"></a>Aulas obrigatórias

Para implementar um provedor de perfil, você cria uma classe que herda a classe abstrata System.Web.Profile.ProfileProvider. A classe abstrata **ProfileProvider,** por sua vez, herda a classe abstrata System.Configuration.SettingsProvider, que herda a classe abstrata System.Configuration.Provider.Provider.ProviderBase. Devido a essa cadeia de herança, além dos membros necessários da classe **ProfileProvider,** você deve implementar os membros necessários das classes **SettingsProvider** e **ProviderBase.**

As tabelas a seguir descrevem as propriedades e métodos que você deve implementar nas classes de resumo **ProviderBase,** **SettingsProvider**e **ProfileProvider.**

### <a name="providerbase-members"></a>Membros da ProviderBase

| **Membro** | **Descrição** |
| --- | --- |
| Método Initialize | Toma como entrada o nome da instância do provedor e uma NameValueCollection de configurações. Usado para definir opções e valores de propriedade para a instância do provedor, incluindo valores e opções específicos de implementação especificados na configuração da máquina ou no arquivo Web.config. |

### <a name="settingsprovider-members"></a>ConfiguraçõesMembros do provedor

| **Membro** | **Descrição** |
| --- | --- |
| Propriedade ApplicationName | O nome do aplicativo que é armazenado em cada perfil. O provedor de perfil usa o nome do aplicativo para armazenar informações de perfil separadamente para cada aplicativo. Isso permite que vários aplicativos ASP.NET usem a mesma fonte de dados sem um conflito se o mesmo nome de usuário for criado em diferentes aplicativos. Alternativamente, vários aplicativos de ASP.NET podem compartilhar uma fonte de dados de perfil especificando o mesmo nome do aplicativo. |
| Método GetPropertyValues | Toma como entrada um objeto ConfiguraçõesContexto e ConfiguraçõesPropriedadeCollection. O **ConfiguraçõesContexto** fornece informações sobre o usuário. Você pode usar as informações como uma chave primária para recuperar informações de propriedade do perfil para o usuário. Use o objeto **ConfiguraçõesContexto** para obter o nome de usuário e se o usuário está autenticado ou anônimo. O **SettingsPropertyCollection** contém uma coleção de objetos SettingsProperty. Cada objeto **SettingsProperty** fornece o nome e o tipo da propriedade, bem como informações adicionais, como o valor padrão da propriedade e se a propriedade é somente leitura. O método **GetPropertyValues** preenche uma ConfiguraçãoPropriedadesValueCollection com configuraçõesObjetosPropriedadeCom base nas **configuraçõesObjetos** de propriedade fornecidos como entrada. Os valores da fonte de dados do usuário especificado são atribuídos às propriedades PropertyValue para cada objeto **SettingsPropertyValue** e toda a coleção é devolvida. A chamada do método também atualiza o valor LastActivityDate para o perfil de usuário especificado para a data e hora atuais. |
| Método SetPropertyValues | Toma como entrada um **objeto ConfiguraçõesContexto** e **ConfiguraçõesPropriedadeValueCollection.** O **ConfiguraçõesContexto** fornece informações sobre o usuário. Você pode usar as informações como uma chave primária para recuperar informações de propriedade do perfil para o usuário. Use o objeto **ConfiguraçõesContexto** para obter o nome de usuário e se o usuário está autenticado ou anônimo. As **configuraçõesPropriedadePropriedadeCollection** contém uma coleção de **objetos SettingsPropertyValue.** Cada objeto **SettingsPropertyValue** fornece o nome, o tipo e o valor da propriedade, bem como informações adicionais, como o valor padrão da propriedade e se a propriedade é somente leitura. O método **SetPropertyValues** atualiza os valores de propriedade do perfil na fonte de dados para o usuário especificado. A chamada do método também atualiza os valores **LastActivityDate** e LastUpdatedDate para o perfil de usuário especificado até a data e hora atuais. |

### <a name="profileprovider-members"></a>Membros do Provedor de Perfil

| **Membro** | **Descrição** |
| --- | --- |
| Método DeleteProfiles | Toma como entrada uma matriz de strings de nomes de usuário e exclui da fonte de dados todas as informações de perfil e valores de propriedade para os nomes especificados onde o nome do aplicativo corresponde ao valor de propriedade **ApplicationName.** Se sua fonte de dados suportar transações, é recomendável que você inclua todas as operações de exclusão em uma transação e que você reverta a transação e lance uma exceção se qualquer operação de exclusão falhar. |
| Método DeleteProfiles | Toma como entrada uma coleção de objetos ProfileInfo e exclui da fonte de dados todas as informações de perfil e valores de propriedade para cada perfil onde o nome do aplicativo corresponde ao valor de propriedade **ApplicationName.** Se sua fonte de dados suportar transações, é recomendável que você inclua todas as operações de exclusão em uma transação e reverta a transação e lance uma exceção se qualquer operação de exclusão falhar. |
| Método DeleteInactiveProfiles | Toma como entrada um valor de Autenticação de perfil e um objeto DateTime e exclui da fonte de dados todas as informações de perfil e valores de propriedade onde a última data de atividade é menor ou igual à data e hora especificadas e onde o nome do aplicativo corresponde ao valor de propriedade **ApplicationName.** O parâmetro **ProfileAuthenticationOption** especifica se apenas perfis anônimos, apenas perfis autenticados ou todos os perfis devem ser excluídos. Se sua fonte de dados suportar transações, é recomendável que você inclua todas as operações de exclusão em uma transação e reverta a transação e lance uma exceção se qualquer operação de exclusão falhar. |
| Método GetAllProfiles | Toma como entrada um valor **Deautenticação de perfil,** um inteiro que especifica o índice da página, um inteiro que especifica o tamanho da página e uma referência a um inteiro que será definido para a contagem total de perfis. Retorna uma ProfileInfoCollection que contém objetos **ProfileInfo** para todos os perfis na fonte de dados onde o nome do aplicativo corresponde ao valor de propriedade **ApplicationName.** O parâmetro **ProfileAuthenticationOption** especifica se apenas perfis anônimos, apenas perfis autenticados ou todos os perfis devem ser retornados. Os resultados retornados pelo método **GetAllProfiles** são limitados pelo índice de página e valores de tamanho da página. O valor do tamanho da página especifica o número máximo de objetos **ProfileInfo** a serem retornados no **ProfileInfoCollection**. O valor do índice da página especifica qual página de resultados a retornar, onde 1 identifica a primeira página. O parâmetro para registros totais é um parâmetro out (você pode usar **ByRef** no Visual Basic) que é definido para o número total de perfis. Por exemplo, se o armazenamento de dados contiver 13 perfis para o aplicativo e o valor do índice da página for 2 com um tamanho de página de 5, o **ProfileInfoCollection** retornado contém o sexto através dos décimos perfis. O valor total dos registros é definido como 13 quando o método retorna. |
| Método GetAllInactiveProfiles | Toma como entrada um valor **Deautenticação de perfil,** um objeto **DateTime,** um inteiro que especifica o índice de página, um inteiro que especifica o tamanho da página e uma referência a um inteiro que será definido para a contagem total de perfis. Retorna uma **ProfileInfoCollection** que contém objetos **ProfileInfo** para todos os perfis na fonte de dados onde a última data de atividade é menor ou igual à **Data-hora** especificada e onde o nome do aplicativo corresponde ao valor de propriedade **ApplicationName.** O parâmetro **ProfileAuthenticationOption** especifica se apenas perfis anônimos, apenas perfis autenticados ou todos os perfis devem ser retornados. Os resultados retornados pelo método **GetAllInactiveProfiles** são limitados pelo índice de página e valores de tamanho da página. O valor do tamanho da página especifica o número máximo de objetos **ProfileInfo** a serem retornados no **ProfileInfoCollection**. O valor do índice da página especifica qual página de resultados a retornar, onde 1 identifica a primeira página. O parâmetro para registros totais é um parâmetro out (você pode usar **ByRef** no Visual Basic) que é definido para o número total de perfis. Por exemplo, se o armazenamento de dados contiver 13 perfis para o aplicativo e o valor do índice da página for 2 com um tamanho de página de 5, o **ProfileInfoCollection** retornado contém o sexto através dos décimos perfis. O valor total dos registros é definido como 13 quando o método retorna. |
| EncontrarperfilsByUserName método | Toma como entrada um valor **Deautenticação de perfil,** uma seqüência contendo um nome de usuário, um inteiro que especifica o índice da página, um inteiro que especifica o tamanho da página e uma referência a um inteiro que será definido para a contagem total de perfis. Retorna uma **ProfileInfoCollection** que contém objetos **ProfileInfo** para todos os perfis na fonte de dados onde o nome de usuário corresponde ao nome de usuário especificado e onde o nome do aplicativo corresponde ao valor de propriedade **ApplicationName.** O parâmetro **ProfileAuthenticationOption** especifica se apenas perfis anônimos, apenas perfis autenticados ou todos os perfis devem ser retornados. Se sua fonte de dados oferecer suporte a recursos adicionais de pesquisa, como caracteres curinga, você poderá fornecer recursos de pesquisa mais extensos para nomes de usuários. Os resultados retornados pelo método **FindProfilesByUserName** são limitados pelos valores de índice de página e tamanho da página. O valor do tamanho da página especifica o número máximo de objetos **ProfileInfo** a serem retornados no **ProfileInfoCollection**. O valor do índice da página especifica qual página de resultados a retornar, onde 1 identifica a primeira página. O parâmetro para registros totais é um parâmetro out (você pode usar **ByRef** no Visual Basic) que é definido para o número total de perfis. Por exemplo, se o armazenamento de dados contiver 13 perfis para o aplicativo e o valor do índice da página for 2 com um tamanho de página de 5, o **ProfileInfoCollection** retornado contém o sexto através dos décimos perfis. O valor total dos registros é definido como 13 quando o método retorna. |
| EncontrarInactiveProfilesByUserName método | Toma como entrada um valor **Deautenticação de perfil,** uma seqüência contendo um nome de usuário, um objeto **DateTime,** um inteiro que especifica o índice de página, um inteiro que especifica o tamanho da página e uma referência a um inteiro que será definido para a contagem total de perfis. Retorna uma **ProfileInfoCollection** que contém objetos **ProfileInfo** para todos os perfis na fonte de dados onde o nome de usuário corresponde ao nome de usuário especificado, onde a última data de atividade é menor ou igual à **data-hora**especificada e onde o nome do aplicativo corresponde ao valor de propriedade **ApplicationName.** O parâmetro **ProfileAuthenticationOption** especifica se apenas perfis anônimos, apenas perfis autenticados ou todos os perfis devem ser retornados. Se sua fonte de dados oferecer suporte a recursos adicionais de pesquisa, como caracteres curinga, você poderá fornecer recursos de pesquisa mais extensos para nomes de usuários. Os resultados retornados pelo método **FindInactiveProfilesByUserName** são limitados pelos valores de índice de página e tamanho da página. O valor do tamanho da página especifica o número máximo de objetos **ProfileInfo** a serem retornados no **ProfileInfoCollection**. O valor do índice da página especifica qual página de resultados a retornar, onde 1 identifica a primeira página. O parâmetro para registros totais é um parâmetro out (você pode usar **ByRef** no Visual Basic) que é definido para o número total de perfis. Por exemplo, se o armazenamento de dados contiver 13 perfis para o aplicativo e o valor do índice da página for 2 com um tamanho de página de 5, o **ProfileInfoCollection** retornado contém o sexto através dos décimos perfis. O valor total dos registros é definido como 13 quando o método retorna. |
| Método GetNumberOfInActiveProfiles | Toma como entrada um valor **de Autenticação de perfil** e um objeto **DateTime** e retorna uma contagem de todos os perfis na fonte de dados onde a última data de atividade é menor ou igual à **Data de data** especificada e onde o nome do aplicativo corresponde ao valor de propriedade **ApplicationName.** O parâmetro **ProfileAuthenticationOption** especifica se apenas perfis anônimos, apenas perfis autenticados ou todos os perfis devem ser contados. |

### <a name="applicationname"></a>ApplicationName

Como os provedores de perfil armazenam informações de perfil separadamente para cada aplicativo, você deve garantir que seu esquema de dados inclua o nome do aplicativo e que as consultas e atualizações também incluam o nome do aplicativo. Por exemplo, o comando a seguir é usado para recuperar um valor de propriedade de um banco de dados com base no nome do usuário e se o perfil é anônimo e garante que o valor **do ApplicationName** esteja incluído na consulta.

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>temas ASP.NET

## <a name="what-are-aspnet-20-themes"></a>Quais são ASP.NET temas 2.0?

Um dos aspectos mais importantes de um aplicativo web é uma aparência consistente em todo o site. ASP.NET desenvolvedores 1.x geralmente usam Folhas de Estilo em Cascata (CSS) para implementar uma aparência consistente. ASP.NET temas 2.0 melhoram significativamente o CSS porque dão ao desenvolvedor ASP.NET a capacidade de definir a aparência de ASP.NET controles de servidor, bem como elementos HTML. ASP.NET temas podem ser aplicados a controles individuais, uma página web específica ou a um aplicativo da Web inteiro. Os temas usam uma combinação de arquivos CSS, um arquivo de pele opcional e um diretório de imagens opcional se as imagens forem necessárias. O arquivo de pele controla a aparência visual dos controles do servidor ASP.NET.

## <a name="where-are-themes-stored"></a>Onde estão armazenados os temas?

O local onde os temas são armazenados difere com base em seu escopo. Os temas que podem ser aplicados a qualquer aplicativo são armazenados na seguinte pasta:

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

Um tema específico para um determinado aplicativo `App\_Themes\<Theme\_Name>` é armazenado em um diretório na raiz do site.

> [!NOTE]
> Um arquivo de pele só deve modificar as propriedades de controle do servidor que afetam a aparência.

Um tema global é um tema que pode ser aplicado a qualquer aplicativo ou site em execução no servidor Web. Esses temas são armazenados por padrão no diretório ASP.NETClientfiles\Themes que está dentro do diretório v2.x.xxxxx. Alternativamente, você pode mover os arquivos temáticos para a pasta aspnet\_client/system\_web/[version]/Themes/[nome do tema]\_na raiz do seu site.

Temas específicos do aplicativo só podem ser aplicados ao aplicativo em que os arquivos residem. Esses arquivos são `App\_Themes/<theme\_name>` armazenados no diretório na raiz do site.

## <a name="the-components-of-a-theme"></a>Os componentes de um tema

Um tema é composto por um ou mais arquivos CSS, um arquivo de pele opcional e uma pasta de Imagens opcional. Os arquivos CSS podem ser qualquer nome que você desejar (ou seja, default.css ou theme.css, etc.) e devem estar na raiz da pasta de temas. Os arquivos CSS são usados para definir classes css ordinárias e atributos para seletores específicos. Para aplicar uma das classes CSS a um elemento de página, a propriedade **CSSClass** é usada.

O arquivo de pele é um arquivo XML que contém definições de propriedade para ASP.NET controles de servidor. O código listado abaixo é um exemplo de arquivo de pele.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

**A Figura 1** abaixo mostra uma pequena página ASP.NET navegada sem um tema aplicado. **A Figura 2** mostra o mesmo arquivo com um tema aplicado. A cor de fundo e a cor do texto são configuradas através de um arquivo CSS. O aparecimento do botão e da caixa de texto são configurados usando o arquivo de pele listado acima.

![Sem tema](profiles-themes-and-web-parts/_static/image1.gif)

**Figura 1**: Sem tema

![Tema Aplicado](profiles-themes-and-web-parts/_static/image2.gif)

**Figura 2**: Tema Aplicado

O arquivo de pele listado acima define uma pele padrão para todos os controles textbox e controles de botão. Isso significa que todos os controles textbox e botão inseridos em uma página assumirão essa aparência. Você também pode definir uma pele que pode ser aplicada a instâncias específicas desses controles usando a propriedade **SkinID** do controle.

O código abaixo define uma pele para um controle button. Somente os controles button com uma propriedade **SkinID** do **goButton** assumirão a aparência da pele.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

Você só pode ter uma skin padrão por tipo de controle de servidor. Se você precisar de skins adicionais, você deve usar a propriedade SkinID.

## <a name="applying-themes-to-pages"></a>Aplicando temas em páginas

Um tema pode ser aplicado usando qualquer um dos seguintes métodos:

- No &lt;elemento&gt; páginas do arquivo web.config
- Na @Page diretiva de uma página
- Programaticamente

## <a name="applying-a-theme-in-the-configuration-file"></a>Aplicando um tema no arquivo de configuração

Para aplicar um tema no arquivo de configuração de aplicativos, use a seguinte sintaxe:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

O nome do tema aqui especificado deve corresponder ao nome da pasta de temas. Esta pasta pode existir em qualquer um dos locais mencionados anteriormente neste curso. Se você tentar aplicar um tema que não existe, um erro de configuração ocorrerá.

## <a name="applying-a-theme-in-the-page-directive"></a>Aplicando um tema na Diretiva de Página

Você também pode aplicar um tema na diretiva @ Page. Este método permite que você use um tema para uma página específica.

Para aplicar um tema na @Page diretiva, use a seguinte sintaxe:

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

Mais uma vez, o tema aqui especificado deve corresponder à pasta temática como mencionado anteriormente. Se você tentar aplicar um tema que não existe, uma falha de compilação ocorrerá. O Visual Studio também destacará o atributo e notificará que esse tema não existe.

## <a name="applying-a-theme-programmatically"></a>Aplicando um tema Programática

Para aplicar um tema de forma programática, você deve especificar a propriedade **Tema** para a página no método **Página\_PreInit.**

Para aplicar um tema de forma programática, use a seguinte sintaxe:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

É necessário aplicar o tema no método PreInit devido ao ciclo de vida da página. Se você aplicá-lo após esse ponto, o tema de páginas já terá sido aplicado pelo tempo de execução e uma alteração nesse ponto é tarde demais no ciclo de vida. Se você aplicar um tema que não existe, uma **HttpException** ocorrerá. Quando um tema é aplicado de forma programática, um aviso de compilação ocorrerá se algum controle de servidor tiver uma propriedade SkinID especificada. Este aviso destina-se a informá-lo de que nenhum tema é declaradomente aplicado e pode ser ignorado.

## <a name="exercise-1--applying-a-theme"></a>Exercício 1 : Aplicando um tema

Neste exercício, você aplicará um tema ASP.NET em um site.

> [!IMPORTANT]
> Se você estiver usando o Microsoft Word para inserir informações em um arquivo de pele, certifique-se de que não está substituindo aspas regulares por citações inteligentes. Citações inteligentes causarão problemas com arquivos de pele.

1. Criar um site do ASP.NET.
2. Clique com o botão direito do mouse sobre o projeto no Solution Explorer e escolha Adicionar novo item.
3. Escolha o Arquivo de Configuração da Web na lista de arquivos e clique em Adicionar.
4. Clique com o botão direito do mouse sobre o projeto no Solution Explorer e escolha Adicionar novo item.
5. Escolha Arquivo de pele e clique em Adicionar.
6. Clique em Sim quando perguntado se você gostaria de\_colocar o arquivo dentro da pasta Temas do aplicativo.
7. Clique com o botão direito do\_mouse na pasta SkinFile dentro da pasta Temas do aplicativo no Solution Explorer e escolha Adicionar novo item.
8. Escolha Folha de estilo na lista de arquivos e clique em Adicionar. Agora você tem todos os arquivos necessários para implementar seu novo tema. No entanto, o Visual Studio nomeou sua pasta de temas SkinFile. Clique com o botão direito do mouse nessa pasta e altere o nome para CoolTheme.
9. Abra o arquivo SkinFile.skin e adicione o seguinte código final do arquivo: 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. Salve o arquivo SkinFile.skin.
11. Abra o StyleSheet.css.
12. Substitua todo o texto nele pelo seguinte: 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. Salvar o arquivo StyleSheet.css.
14. Abra a página Default.aspx.
15. Adicione um controle TextBox e um controle de botão.
16. Salve a página. Agora navegue pela página Default.aspx. Ele deve ser exibido como uma forma web normal.
17. Abra o arquivo web.config.
18. Adicione o seguinte diretamente `<system.web>` abaixo da tag de abertura: 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. Salvar o arquivo web.config. Agora navegue pela página Default.aspx. Deve ser exibido com o tema aplicado.
20. Se ainda não estiver aberto, abra a página Default.aspx no Visual Studio.
21. Selecione o botão.
22. Altere a propriedade **SkinID** para goButton. Observe que o Visual Studio fornece um dropdown com valores SkinID válidos para um controle de botão.
23. Salve a página. Agora, visualize a página no seu navegador novamente. O botão agora deve dizer "ir" e deve ser mais amplo na aparência.

Usando a propriedade **SkinID,** você pode facilmente configurar diferentes skins para diferentes instâncias de um determinado tipo de controle de servidor.

## <a name="the-stylesheettheme-property"></a>A propriedade StyleSheetTheme

Até agora, falamos apenas sobre a aplicação de temas usando a propriedade Tema. Ao usar a propriedade Tema, o arquivo de pele substituirá quaisquer configurações declarativas para controles de servidor. Por exemplo, no exercício 1, você especificou um SkinID de "goButton" para o controle Button e que alterou o texto do botão para "ir". Você deve ter notado que a propriedade Text do Botão no designer foi definida como "Button", mas o tema anulou isso. O tema sempre substituirá qualquer configuração de propriedade no designer.

Se você quiser ser capaz de substituir as propriedades definidas no arquivo de pele do tema com propriedades especificadas no designer, você pode usar a propriedade **StyleSheetTheme** em vez da propriedade Theme. A propriedade StyleSheetTheme é a mesma da propriedade Theme, exceto que não anula todas as configurações explícitas de propriedade, como a propriedade Theme faz.

Para ver isso em ação, abra o arquivo web.config `<pages>` do projeto no exercício 1 e altere o elemento para o seguinte:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

Agora navegue na página Default.aspx e verá que o controle Button tem uma propriedade text of "Button" novamente. Isso porque a configuração de propriedade explícita no designer está substituindo a propriedade Text definida pelo goButton SkinID.

## <a name="overriding-themes"></a>Temas sobrepondo

Um tema global pode ser substituído aplicando um tema com\_o mesmo nome na pasta App Themes do aplicativo. No entanto, o tema não é aplicado em um verdadeiro cenário de substituição. Se o tempo de execução encontrar\_arquivos temáticos na pasta App Themes, ele aplicará o tema usando esses arquivos e ignorará o tema global.

A propriedade StyleSheetTheme é superridível e pode ser substituída em código da seguinte forma:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Partes de Web

ASP.NET Web Parts é um conjunto integrado de controles para criar sites da Web que permitem aos usuários finais modificar o conteúdo, a aparência e o comportamento das páginas da Web diretamente de um navegador. As modificações podem ser aplicadas a todos os usuários do site ou a usuários individuais. Quando os usuários modificam páginas e controles, as configurações podem ser salvas para reter as preferências pessoais de um usuário em futuras sessões do navegador, um recurso chamado personalização. Esses recursos de Web Parts significam que os desenvolvedores podem capacitar os usuários finais a personalizar um aplicativo da Web dinamicamente, sem a intervenção do desenvolvedor ou do administrador.

Usando o conjunto de controle Web Parts, você, como desenvolvedor, pode habilitar os usuários finais para:

- Personalize o conteúdo da página. Os usuários podem adicionar novos controles de Peças da Web a uma página, removê-los, escondê-los ou minimizá-los como janelas comuns.
- Personalize o layout da página. Os usuários podem arrastar um controle de Peças da Web para uma região diferente em uma página ou alterar sua aparência, propriedades e comportamento.
- Controles de exportação e importação. Os usuários podem importar ou exportar configurações de controle de Peças da Web para uso em outras páginas ou sites, mantendo as propriedades, aparência e até mesmo os dados nos controles. Isso reduz as demandas de entrada e configuração de dados em usuários finais.
- Criar conexões. Os usuários podem estabelecer conexões entre controles para que, por exemplo, um controle de gráfico possa exibir um gráfico para os dados em um controle de ticker de estoque. Os usuários poderiam personalizar não apenas a conexão em si, mas a aparência e detalhes de como o controle do gráfico exibe os dados.
- Gerencie e personalize as configurações de nível do site. Os usuários autorizados podem configurar configurações de nível de site, determinar quem pode acessar um site ou página, definir acesso baseado em função aos controles e assim por diante. Por exemplo, um usuário em uma função administrativa pode definir um controle de Partes da Web para ser compartilhado por todos os usuários e impedir que usuários que não são administradores personalizem o controle compartilhado.

Você normalmente trabalhará com Web Parts de uma das três maneiras: criando páginas que usam controles de Peças da Web, criando controles individuais de Web Parts ou criando aplicativos web completos e personalizáveis, como um portal.

## <a name="page-development"></a>Desenvolvimento de página

Os desenvolvedores de páginas podem usar ferramentas de design visual, como o Microsoft Visual Studio 2005, para criar páginas que usam Web Parts. Uma vantagem no uso de uma ferramenta como o Visual Studio é que o conjunto de controle Web Parts fornece recursos para criação de arrastar e soltar controles de Web Parts em um designer visual. Por exemplo, você pode usar o designer para arrastar uma região de Peças da Web ou um controle de editor de Peças da Web na superfície do design e, em seguida, configurar o controle direito no designer usando a ui fornecida pelo conjunto de controle Web Parts. Isso pode acelerar o desenvolvimento de aplicações web parts e reduzir a quantidade de código que você tem que escrever.

## <a name="control-development"></a>Desenvolvimento de Controle

Você pode usar qualquer controle de ASP.NET existente como um controle de Peças da Web, incluindo controles padrão do servidor Web, controles personalizados de servidor e controles de usuário. Para o controle programático máximo do seu ambiente, você também pode criar controles personalizados de Web Parts que derivam da classe WebPart. Para o desenvolvimento individual do controle de Web Parts, você normalmente criará um controle de usuário e o usará como um controle de Web Parts ou desenvolverá um controle personalizado de Web Parts.

Como exemplo de desenvolvimento de um controle personalizado de Web Parts, você pode criar um controle para fornecer qualquer um dos recursos fornecidos por outros controles de servidor de ASP.NET que possam ser úteis para embalar como um controle de Partes da Web personalizável: calendários, listas, informações financeiras, notícias, calculadoras, controles de texto ricos para atualização de conteúdo, grades editáveis que se conectam a bancos de dados, gráficos que atualizam dinamicamente seus displays , ou informações meteorológicas e de viagem. Se você fornecer um designer visual com o seu controle, então qualquer desenvolvedor de página que usa o Visual Studio pode simplesmente arrastar seu controle para uma região de Peças da Web e configurá-lo na hora do design sem ter que escrever código adicional.

A personalização é a base do recurso Web Parts. Ele permite que os usuários modifiquem - ou personalizem - o layout, a aparência e o comportamento dos controles de Peças da Web em uma página. As configurações personalizadas são de longa duração: elas são persistidas não apenas durante a sessão atual do navegador (como no estado de exibição), mas também no armazenamento de longo prazo, para que as configurações de um usuário sejam salvas para futuras sessões do navegador também. A personalização é habilitada por padrão para páginas de Partes da Web.

Os componentes estruturais da UI dependem da personalização e fornecem a estrutura central e os serviços necessários por todos os controles de Web Parts. Um componente estrutural de IA necessário em cada página de Partes da Web é o controle do WebPartManager. Embora nunca visível, esse controle tem a tarefa crítica de coordenar todos os controles de Web Parts em uma página. Por exemplo, ele rastreia todos os controles individuais da Web Parts. Ele gerencia as regiões web parts (regiões que contêm controles de Partes da Web em uma página) e quais controles são em quais regiões. Ele também rastreia e controla os diferentes modos de exibição em que uma página pode estar, como procurar, conectar, editar ou modo catálogo, e se as alterações de personalização se aplicam a todos os usuários ou a usuários individuais. Finalmente, inicia e rastreia conexões e comunicação entre controles de Web Parts.

O segundo tipo de componente estrutural da UI é a zona. As regiões atuam como gerentes de layout em uma página de Partes da Web. Eles contêm e organizam controles que derivam da classe Parte (controles de peça), e fornecem a capacidade de fazer layout de página modular em orientação horizontal ou vertical. As zonas também oferecem elementos de IA comuns e consistentes (como estilo de cabeçalho e rodapé, título, estilo de borda, botões de ação e assim por diante) para cada controle que contêm; esses elementos comuns são conhecidos como o cromo de um controle. Vários tipos especializados de zonas são usados nos diferentes modos de exibição e com vários controles. Os diferentes tipos de zonas são descritos na seção Controles Essenciais de Partes da Web abaixo.

Os controles de IU de Partes da Web, todos derivados da classe **Parte,** compreendem a ui principal em uma página de Partes da Web. O conjunto de controle Web Parts é flexível e inclusivo nas opções que lhe dá para criar controles de peças. Além de criar seus próprios controles personalizados de Web Parts, você também pode usar controles de servidor ASP.NET existentes, controles de usuário ou controles de servidor personalizados como controles de Web Parts. Os controles essenciais mais usados para criar páginas de Partes da Web são descritos na próxima seção.

## <a name="web-parts-essential-controls"></a>Controles essenciais de peças da Web

O conjunto de controle web parts é extenso, mas alguns controles são essenciais, seja porque são necessários para que as Web Parts funcionem, ou porque são os controles mais usados nas páginas de Web Parts. À medida que você começa a usar Web Parts e criar páginas básicas da Web Parts, é útil estar familiarizado com os controles essenciais de Partes da Web descritos na tabela a seguir.

| **Controle de Peças web** | **Descrição** |
| --- | --- |
| Webpartmanager | Gerencia todos os controles de Web Parts em uma página. Um (e único) controle **do WebPartManager** é necessário para cada página de Partes da Web. |
| Catalogzone | Contém controles CatalogPart. Use essa região para criar um catálogo de controles de Web Parts a partir do qual os usuários podem selecionar controles para adicionar a uma página. |
| Editorzone | Contém controles EditorPart. Use essa região para permitir que os usuários editem e personalizem controles de Peças da Web em uma página. |
| Webpartzone | Contém e fornece layout geral para os controles WebPart que compõem a ui principal de uma página. Use esta região sempre que criar páginas com controles de Partes da Web. As páginas podem conter uma ou mais zonas. |
| Connectionszone | Contém controles WebPartConnection e fornece uma iu para gerenciar conexões. |
| WebPart (GenericWebPart) | Torna a ui primária; a maioria dos controles de IU de Partes da Web se enquadram nessa categoria. Para o controle programático máximo, você pode criar controles personalizados da Web Parts que derivam do controle **base do WebPart.** Você também pode usar controles de servidor existentes, controles de usuário ou controles personalizados como controles de Web Parts. Sempre que qualquer um desses controles é colocado em uma região, o controle **do WebPartManager** os envolve automaticamente com controles **GenericWebPart** em tempo de execução para que você possa usá-los com a funcionalidade Web Parts. |
| Catalogpart | Contém uma lista de controles de Web Parts disponíveis que os usuários podem adicionar à página. |
| Webpartconnection | Cria uma conexão entre dois controles de Partes da Web em uma página. A conexão define um dos controles da Web Parts como provedor (de dados) e o outro como consumidor. |
| Editorpart | Serve como classe base para os controles especializados do editor. |
| Controles do EditorPart (AppearanceEditorPart, LayoutEditorPart, BehaviorEditorPart e PropertyGridEditorPart) | Permitir que os usuários personalizem vários aspectos dos controles de IA da Web Parts em uma página |

## <a name="lab-create-a-web-part-page"></a>Laboratório: Crie uma página de parte da Web

Neste laboratório, você criará uma página de parte da Web que persistirá as informações através de perfis ASP.NET.

### <a name="creating-a-simple-page-with-web-parts"></a>Criando uma página simples com peças da Web

Nesta parte do passo a passo, você cria uma página que usa controles web parts para mostrar conteúdo estático. O primeiro passo para trabalhar com web parts é criar uma página com dois elementos estruturais necessários. Primeiro, uma página de partes da Web precisa de um controle do WebPartManager para rastrear e coordenar todos os controles de Partes da Web. Em segundo lugar, uma página de Partes da Web precisa de uma ou mais regiões, que são controles compostos que contêm controles webpart ou outros servidores e ocupam uma região especificada de uma página.

> [!NOTE]
> Você não precisa fazer nada para habilitar a personalização de Web Parts; ele está habilitado por padrão para o conjunto de controle Web Parts. Quando você executa pela primeira vez uma página de Partes da Web em um site, ASP.NET configura um provedor de personalização padrão para armazenar as configurações de personalização do usuário. Para obter mais informações sobre personalização, consulte Visão geral da personalização de peças da Web.

### <a name="to-create-a-page-for-containing-web-parts-controls"></a>Para criar uma página para conter controles de Peças da Web

1. Feche a página padrão e adicione uma nova página ao site chamado WebPartsDemo.aspx.
2. Mude para **exibição Design.**
3. No menu **Exibir,** **certifique-se de** que as opções Controles e **Detalhes** Não Visuais sejam selecionados para que você possa ver tags de layout e controles que não possuem uma ui.
4. Coloque o ponto `<div>` de inserção antes das tags na superfície do projeto e pressione ENTER para adicionar uma nova linha. Posicione o ponto de inserção antes do novo caractere de linha, clique no controle de lista suspenso **do Formato** de bloco no menu e selecione a opção **Título 1.** No título, adicione a **página de demonstração de partes da Web do**texto .
5. Na guia **WebParts** da caixa de ferramentas, arraste um controle **do WebPartManager** para a `<div>`página, posicionando-o logo após o novo caractere da linha e antes das tags.   
  
   O controle **do WebPartManager** não renderiza nenhuma saída, por isso aparece como uma caixa cinza na superfície do designer.
6. Posicione o ponto `<div>` de inserção dentro das tags.
7. No menu **Layout,** clique **em Inserir tabela**e crie uma nova tabela com uma linha e três colunas. Clique no botão **Propriedades de célula,** selecione a **parte superior** da lista vertical **de alinhamento** de parabaixo, clique em **OK**e clique em **OK** novamente para criar a tabela.
8. Arraste um controle do WebPartZone para a coluna da tabela esquerda. Clique com o botão direito do mouse no controle **do WebPartZone,** escolha **Propriedades**e defina as seguintes propriedades:   
  
   ID: SidebarZone   
  
   HeaderText: Barra lateral
9. Arraste um segundo controle **do WebPartZone** para a coluna da mesa média e defina as seguintes propriedades:   
  
   ID: MainZone   
  
   HeaderText: Principal
10. Salve o arquivo.

Sua página agora tem duas zonas distintas que você pode controlar separadamente. No entanto, nenhuma das duas zonas tem conteúdo, então criar conteúdo é o próximo passo. Para este passo a passo, você trabalha com controles de Web Parts que exibem apenas conteúdo estático.

O layout de uma região de &lt;Partes&gt; da Web é especificado por um elemento de modelo de região. Dentro do modelo de região, você pode adicionar qualquer ASP.NET controle, seja um controle personalizado de Peças da Web, um controle de usuário ou um controle de servidor existente. Observe que aqui você está usando o controle Label, e para isso você está simplesmente adicionando texto estático. Quando você coloca um controle de servidor regular em uma região **WebPartZone,** ASP.NET trata o controle como um controle de Web Parts em tempo de execução, o que permite os recursos da Web Parts no controle.

**Para criar conteúdo para a região principal**

1. Na **exibição Design,** arraste um controle **de rótulo** da guia **Padrão** da caixa de ferramentas para a área de conteúdo da região cuja propriedade **de ID** está definida como MainZone.
2. Mude para **exibição Origem.** Observe que &lt;um&gt; elemento zonetemplate foi adicionado para envolver o **controle De rótulo** na MainZone.
3. Adicione um **title** atributo &lt;chamado título&gt; ao elemento asp:label e defina seu valor como Conteúdo. Remova o atributo Text="Label" do&gt; elemento asp:label. &lt; Entre as tags de &lt;abertura e&gt; fechamento do elemento asp:label, adicione algum &lt;texto&gt; como Welcome to my **Home Page** dentro de um par de tags de elemento h2. Seu código deve ser o seguinte. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. Salve o arquivo.

Em seguida, crie um controle de usuário que também possa ser adicionado à página como um controle de Partes da Web.

### <a name="to-create-a-user-control"></a>Para criar um controle de usuário

1. Adicione um novo controle de usuário da Web ao seu site para servir como um controle de pesquisa. Desmarque a opção **para colocar código-fonte em um arquivo separado**. Adicione-o no mesmo diretório que a página WebPartsDemo.aspx e nomeie-o SearchUserControl.ascx.   
  
    > [!NOTE]
    > O controle do usuário para este passo a passo não implementa a funcionalidade real de pesquisa; ele é usado apenas para demonstrar os recursos da Web Parts.
2. Mude para **exibição Design.** Na guia **Padrão** da caixa de ferramentas, arraste um controle TextBox para a página.
3. Coloque o ponto de inserção após a caixa de texto que você acabou de adicionar e pressione ENTER para adicionar uma nova linha.
4. Arraste um controle button para a página da nova linha abaixo da caixa de texto que você acabou de adicionar.
5. Mude para **exibição Origem.** Certifique-se de que o código-fonte para o controle do usuário se pareça com o seguinte exemplo. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. Salve e feche o arquivo.

Agora você pode adicionar controles de Peças da Web à zona Barra lateral. Você está adicionando dois controles à zona Barra lateral, um contendo uma lista de links e outro que é o controle de usuário que você criou no procedimento anterior. Os links são adicionados como um controle padrão do servidor **Label,** semelhante à maneira como você criou o texto estático para a região Principal. No entanto, embora os controles individuais de servidor contidos no controle do usuário possam ser contidos diretamente na região (como o controle de rótulo), neste caso não estão. Em vez disso, eles fazem parte do controle do usuário que você criou no procedimento anterior. Isso demonstra uma maneira comum de empacotar qualquer controle e funcionalidade extra que você deseja em um controle de usuário e, em seguida, referenciar esse controle em uma região como um controle de Web Parts.

No tempo de execução, o conjunto de controles Web Parts envolve ambos os controles com controles GenericWebPart. Quando um controle **GenericWebPart** envolve um controle de servidor Web, o controle de peça genérico é o controle dos pais e você pode acessar o controle do servidor através da propriedade ChildControl do controle pai. Esse uso de controles genéricos de peças permite que os controles padrão do servidor Web tenham o mesmo comportamento básico e atributos que os controles de Web Parts que derivam da classe **WebPart.**

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>Para adicionar controles de Peças web à zona de barra lateral

1. Abra a página WebPartsDemo.aspx.
2. Mude para **exibição Design.**
3. Arraste a página de controle de usuário que você criou, SearchUserControl.ascx, do **Solution Explorer** para a região cuja propriedade **de ID** está definida como SidebarZone e solte-a lá.
4. Salvar a página WebPartsDemo.aspx.
5. Mude para **exibição Origem.**
6. Dentro &lt;do elemento asp:webpartzone&gt; para a Barra Lateral, logo acima &lt;da referência&gt; ao controle do usuário, adicione um elemento asp:label com links contidos, conforme mostrado no exemplo a seguir. Além disso, adicione um atributo **Título** à tag de controle do usuário, com um valor de **Pesquisa,** como mostrado. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. Salve e feche o arquivo.

Agora você pode testar sua página navegando para ela no seu navegador. A página exibe as duas zonas. A captura de tela a seguir mostra a página.

**Página de demonstração de partes da Web com duas zonas**

![Web Parts VS Walkthrough 1 Captura de tela](profiles-themes-and-web-parts/_static/image3.gif)

**Figura 3**: Web Parts VS Walkthrough 1 Captura de tela

Na barra de título de cada controle há uma seta para baixo que fornece acesso a um menu de verbos de ações disponíveis que você pode executar em um controle. Clique no menu verbos para um dos controles e clique no verbo **Minimizar** e observe que o controle está minimizado. No menu verbos, clique em **Restaurar**e o controle retorne ao seu tamanho normal.

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>Habilitando os usuários a editar páginas e alterar layout

O Web Parts fornece o recurso para os usuários alterarem o layout dos controles de Web Parts arrastando-os de uma região para outra. Além de permitir que os usuários movam os controles do **WebPart** de uma região para outra, você pode permitir que os usuários editem várias características dos controles, incluindo sua aparência, layout e comportamento. O conjunto de controle Web Parts fornece funcionalidade básica de edição para controles **WebPart.** Embora você não o faça neste passo a passo, você também pode criar controles personalizados do editor que permitem aos usuários editar os recursos dos controles do **WebPart.** Assim como alterar a localização de um controle **do WebPart,** a edição das propriedades de um controle depende de ASP.NET personalização para salvar as alterações que os usuários fazem.

Nesta parte do passo a passo, você adiciona a capacidade dos usuários de editar as características básicas de qualquer controle **do WebPart** na página. Para habilitar esses recursos, você adiciona outro controle &lt;de usuário personalizado&gt; à página, juntamente com um elemento asp:editorzone e dois controles de edição.

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>Para criar um controle de usuário que permite alterar o layout da página

1. No Visual Studio, no menu **Arquivo,** selecione o submenu **Novo** e clique na opção **Arquivo.**
2. Na **caixa de diálogo Adicionar novo item,** selecione **Controle de usuário da Web**. Nomeie o novo arquivo DisplayModeMenu.ascx. Desmarque a opção **para colocar código-fonte em arquivo separado**.
3. Clique em Adicionar para criar o novo controle.
4. Mude para **exibição Origem.**
5. Remova todo o código existente no novo arquivo e cole no código a seguir. Este código de controle do usuário usa recursos do conjunto de controle Web Parts que permitem que uma página altere seu modo de exibição ou exibição, e também permite que você altere a aparência física e o layout da página enquanto você estiver em certos modos de exibição. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. Salve o arquivo clicando no ícone salvar na barra de ferramentas ou selecionando **Salvar** no menu **Arquivo.**

### <a name="to-enable-users-to-change-the-layout"></a>Para permitir que os usuários alterem o layout

1. Abra a página WebPartsDemo.aspx e mude para **exibição Design.**
2. Posicione o ponto de inserção na exibição **Design** logo após o controle **do WebPartManager** que você adicionou anteriormente. Adicione um retorno rígido após o texto para que haja uma linha em branco após o controle do **WebPartManager.** Coloque o ponto de inserção na linha em branco.
3. Arraste o controle de usuário que acabou de criar (o arquivo é chamado DisplayModeMenu.ascx) para a página WebPartsDemo.aspx e solte-o na linha em branco.
4. Arraste um controle EditorZone da seção **WebParts** da caixa de ferramentas para a célula de tabela aberta restante na página WebPartsDemo.aspx.
5. Na seção **WebParts** da Caixa de ferramentas, arraste um controle AppearanceEditorPart e um controle LayoutEditorPart no controle **do EditorZone.**
6. Mude para **exibição Origem.** O código resultante na célula da tabela deve ser semelhante ao seguinte código. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. Salve o arquivo WebPartsDemo.aspx. Você criou um controle de usuário que permite alterar os modos de exibição e alterar o layout da página, e você fez referência ao controle na página principal da Web.

Agora você pode testar a capacidade de editar páginas e alterar o layout.

### <a name="to-test-layout-changes"></a>Para testar as alterações de layout

1. Carregue a página em um navegador.
2. Clique no menu suspenso do modo de **exibição** e selecione **Editar**. Os títulos de zona são exibidos.
3. Arraste o controle **My Links** pela barra de título da zona barra lateral até a parte inferior da zona principal. Sua página deve parecer a seguinte captura de tela.

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>Página de demonstração de peças da Web com controle Meus links movido

![Web Parts VS Walkthrough 2 Captura de tela](profiles-themes-and-web-parts/_static/image4.gif)

**Figura 4**: Web Parts VS Walkthrough 2 Screenshot

1. Clique no menu suspenso do modo de **exibição** e selecione **Procurar**. A página é atualizada, os nomes de região desaparecem e o controle **Meus links** permanece onde você a posicionou.
2. Para demonstrar que a personalização está funcionando, feche o navegador e carregue a página novamente. As alterações feitas são salvas para futuras sessões do navegador.
3. No menu **Modo de exibição,** selecione **Editar**.   
  
   Cada controle na página é agora exibido com uma seta para baixo em sua barra de título, que contém o menu suspenso verbos.
4. Clique na seta para exibir o menu verbos no controle **Meus Links.** Clique no **verbo Editar.**   
  
   O controle **EditorZone** é exibido, exibindo os controles do EditorPart que você adicionou.
5. Na seção **Aparência** do controle de edição, altere o **Título** para Meus Favoritos, use a lista de isto de entrada **do Tipo De chrome** para selecionar Somente **título**e clique em **Aplicar**. A captura de tela a seguir mostra a página no modo de edição.

### <a name="web-parts-demo-page-in-edit-mode"></a>Página de demonstração de peças da Web no modo Editar

![Web Parts VS Walkthrough 3 Captura de tela](profiles-themes-and-web-parts/_static/image5.gif)

**Figura 5**: Web Parts VS Walkthrough 3 Screenshot

1. Clique no menu **Modo de exibição** e selecione **Procurar** para retornar ao modo de navegação.
2. O controle agora tem um título atualizado e sem borda, como mostrado na captura de tela a seguir.

### <a name="edited-web-parts-demo-page"></a>Página de demonstração de peças da Web editada

![Web Parts VS Walkthrough 4 Captura de tela](profiles-themes-and-web-parts/_static/image6.gif)

**Figura 4**: Web Parts VS Walkthrough 4 Screenshot

### <a name="adding-web-parts-at-run-time"></a>Adicionando peças da Web em tempo de execução

Você também pode permitir que os usuários adicionem controles de Peças da Web à sua página em tempo de execução. Para isso, configure a página com um catálogo de Web Parts, que contém uma lista de controles de Web Parts que você deseja disponibilizar aos usuários.

**Para permitir que os usuários adicionem Web Parts em tempo de execução**

1. Abra a página WebPartsDemo.aspx e mude para **exibição Design.**
2. Na guia **WebParts** da caixa de ferramentas, arraste um controle CatalogZone para a coluna direita da tabela, abaixo do controle **EditorZone.**   
  
   Ambos os controles podem estar na mesma célula de tabela porque não serão exibidos ao mesmo tempo.
3. No painel Propriedades, atribua a seqüência **Adicionar Partes da Web** à propriedade HeaderText do controle **CatalogZone.**
4. Na seção **WebParts** da Caixa de ferramentas, arraste um controle DeclarativeCatalogPart para a área de conteúdo do controle **CatalogZone.**
5. Clique na seta no canto superior direito do controle **DeclarativeCatalogPart** para expor seu menu Tarefas e, em seguida, selecione **Editar modelos**.
6. Na seção **Padrão** da caixa de ferramentas, arraste um controle **FileUpload** e um controle **Calendar** na seção **WebPartsTemplate** do controle **DeclarativeCatalogPart.**
7. Mude para **exibição Origem.** Inspecione o &lt;código-fonte do&gt; elemento asp:catalogzone. Observe que o controle **DeclarativeCatalogPart** contém um &lt;elemento webpartstemplate&gt; com os dois controles de servidor fechados que você poderá adicionar à sua página a partir do catálogo.
8. Adicione uma propriedade **Title** a cada um dos controles adicionados ao catálogo, usando o valor de string mostrado para cada título no exemplo de código abaixo. Mesmo que o título não seja uma propriedade que você normalmente pode definir nesses dois controles de servidor na hora do projeto, quando um usuário adiciona esses controles a uma região **webPartZone** do catálogo em tempo de execução, cada um deles é embrulhado com um controle **GenericWebPart.** Isso permite que eles atuem como controles de Web Parts, para que eles possam exibir títulos.   
  
   O código para os dois controles contidos no **controle DeclarativeCatalogPart** deve ser o seguinte. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. Salve a página.

Agora você pode testar o catálogo.

### <a name="to-test-the-web-parts-catalog"></a>Para testar o catálogo de Web Parts

1. Carregue a página em um navegador.
2. Clique no menu suspenso do modo de **exibição** e selecione **'Catálogo'.**   
  
   O catálogo intitulado **Adicionar Partes da Web** é exibido.
3. Arraste o controle **Meus Favoritos** da zona principal de volta para o topo da zona lateral, e deixe-o cair lá.
4. No catálogo **Adicionar peças da Web,** selecione ambas as caixas de seleção e selecione **Principal** na lista de baixa que contém as regiões disponíveis.
5. Clique em **Adicionar** no catálogo. Os controles são adicionados à zona principal. Se você quiser, você pode adicionar várias instâncias de controles do catálogo à sua página.   
  
   A captura de tela a seguir mostra a página com o controle de upload de arquivo e o calendário na região Principal. 

![Controles adicionados à zona principal do catálogo](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. Clique no menu suspenso do modo de **exibição** e selecione **Procurar**. O catálogo desaparece e a página é atualizada.
7. Feche o navegador. Carregue a página novamente. As mudanças que você fez persistem.
