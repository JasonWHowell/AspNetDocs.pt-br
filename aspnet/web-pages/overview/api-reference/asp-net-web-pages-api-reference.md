---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Web Pages (Razor) API Referência Rápida | Microsoft Docs
author: Rick-Anderson
description: Esta página contém uma lista com breves exemplos dos objetos, propriedades e métodos mais usados para programação ASP.NET Páginas da Web com sintaxe de Navalha.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676240"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET Web Pages (Razor) API Referência Rápida

 por [Tom FitzMacken](https://github.com/tfitzmac)

> Esta página contém uma lista com breves exemplos dos objetos, propriedades e métodos mais usados para programação ASP.NET Páginas da Web com sintaxe de Navalha.
> 
> As descrições marcadas com "(v2)" foram introduzidas na versão 2 da ASP.NET Páginas da Web.
> 
> Para obter documentação de referência de API, consulte a [documentação de referência de páginas da Web ASP.NET](https://go.microsoft.com/fwlink/?LinkId=208659) no MSDN.
> 
> ## <a name="software-versions"></a>Versões de software
> 
> 
> - páginas da Web ASP.NET (Navalha) 3
>   
> 
> Este tutorial também funciona com ASP.NET Páginas da Web 2 e ASP.NET Páginas da Web 1.0 (exceto para recursos marcados v2).

Esta página contém informações de referência para o seguinte:

- [Classes](#Classes)
- [Dados](#Data)
- [Auxiliares](#Helpers)
- [Validação](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>Classes

### `AppState[key], AppState[index],App`

Contém dados que podem ser compartilhados por qualquer página no aplicativo. Você pode usar `App` a propriedade dinâmica para acessar os mesmos dados, como no exemplo a seguir:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

Converte um valor de string em um valor booleano (verdadeiro/falso). Retorna falso ou o valor especificado se a string não representar verdadeiro/falso.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

Converte um valor de seqüência em data/hora. Retorna `DateTime.MinValue` ou o valor especificado se a seqüência não representar uma data/hora.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

Converte um valor de seqüência em um valor decimal. Retorna 0.0 ou o valor especificado se a seqüência não representar um valor decimal.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

Converte um valor de corda em um carro alegórico. Retorna 0.0 ou o valor especificado se a seqüência não representar um valor decimal.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

Converte um valor de string em um inteiro. Retorna 0 ou o valor especificado se a seqüência não representar um inteiro.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

Cria uma URL compatível com navegador a partir de um caminho de arquivo local, com partes adicionais de caminho opcionais.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

Renderiza *o valor* como marcação HTML em vez de torná-lo como saída codificada por HTML.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

Retorna verdadeiro se o valor pode ser convertido de uma seqüência de string para o tipo especificado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

Retorna verdadeiro se o objeto ou variável não tiver valor.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

Retorna verdadeiro se a solicitação for um POST. (As solicitações iniciais geralmente são um GET.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

Especifica o caminho de uma página de layout para aplicar a esta página.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

Contém dados compartilhados entre a página, páginas de layout e páginas parciais na solicitação atual. Você pode usar `Page` a propriedade dinâmica para acessar os mesmos dados, como no exemplo a seguir:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(Páginas de layout) Renderiza o conteúdo de uma página de conteúdo que não está em nenhuma seção nomeada.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

Renderiza uma página de conteúdo usando o caminho especificado e dados extras opcionais. Você pode obter os valores `PageData` dos parâmetros extras por posição (exemplo 1) ou chave (exemplo 2).

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(Páginas de layout) Renderiza uma seção de conteúdo que tem um nome. Conjunto *necessário* para falso para tornar uma seção opcional.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

Obtém ou define o valor de um cookie HTTP.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

Obtém os arquivos que foram carregados no pedido atual.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

Obtém dados que foram postados em um formulário (como strings). `Request[key]`verifica tanto `Request.Form` as `Request.QueryString` coleções quanto as coleções.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

Obtém dados que foram especificados na seqüência de consulta de URL. `Request[key]`verifica tanto `Request.Form` as `Request.QueryString` coleções quanto as coleções.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Desativa seletivamente a validação de solicitação para um elemento de formulário, valor da seqüência de consulta, cookie ou valor de cabeçalho. A validação da solicitação é ativada por padrão e impede que os usuários postem marcação ou outro conteúdo potencialmente perigoso.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

Adiciona um cabeçalho do servidor HTTP à resposta.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

Armazena a saída da página por um tempo especificado. Opcionalmente, defina o *deslizamento* para redefinir o tempo limitado em cada acesso à página e *varieByParams* para armazenar diferentes versões da página para cada seqüência de consulta diferente na solicitação da página.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

Redireciona a solicitação do navegador para um novo local.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

Define o código de status HTTP enviado para o navegador.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

Grava o conteúdo dos *dados* para a resposta com um tipo mime opcional.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

Grava o conteúdo de um arquivo para a resposta.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(Páginas de layout) Define uma seção de conteúdo que tenha um nome.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

Decodifica uma seqüência de caracteres HTML codificada.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

Codifica uma seqüência de renderização na marcação HTML.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

Retorna o caminho físico do servidor para o caminho virtual especificado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

Decodifica texto de uma URL.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

Codifica texto para colocar em uma URL.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

Obtém ou define um valor que existe até que o usuário feche o navegador.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

Exibe uma representação de string do valor do objeto.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

Obtém dados adicionais da URL (por exemplo, */MyPage/ExtraData*).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

Altera a senha para o usuário especificado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

Confirma uma conta usando o token de confirmação da conta.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

Cria uma nova conta de usuário com o nome de usuário e senha especificados. Para exigir um token de confirmação, passe verdadeiro para *exigirConfirmationToken.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

Obtém o identificador inteiro para o usuário atualmente conectado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

Obtém o nome do usuário atualmente conectado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

Gera um token de redefinição de senha que pode ser enviado por e-mail para um usuário para que o usuário possa redefinir a senha.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

Retorna o ID do usuário do nome de usuário.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

Retorna verdadeiro se o usuário atual estiver logado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

Retorna verdadeiro se o usuário tiver sido confirmado (por exemplo, através de um e-mail de confirmação).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

Retorna verdadeiro se o nome do usuário atual corresponder ao nome de usuário especificado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Registra o usuário definindo um token de autenticação no cookie.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

Faça loga do usuário removendo o cookie de token de autenticação.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

Se o usuário não estiver autenticado, define o status HTTP como 401 (Não autorizado).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

Se o usuário atual não for membro de uma das funções especificadas, definirá o status HTTP como 401 (Não autorizado).

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

Se o usuário atual não for o usuário especificado pelo *nome de usuário,* definirá o status HTTP como 401 (Não autorizado).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

Se o token de redefinição de senha for válido, altera a senha do usuário para a nova senha.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Dados

### `Database.Execute(SQLstatement [,parameters]`

Executa *sqlstatement* (com parâmetros opcionais) como INSERT, DELETE ou UPDATE e retorna uma contagem de registros afetados.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

Retorna a coluna de identidade da linha inserida mais recentemente.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

Abre o arquivo de banco de dados especificado ou o banco de dados especificado usando uma seqüência de conexão nomeada do arquivo *Web.config.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

Abre um banco de dados usando a seqüência de conexões. (Isso contrasta `Database.Open`com , que usa um nome de seqüência de conexão.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

Consulta o banco de dados usando *SQLstatement* (opcionalmente passando parâmetros) e retorna os resultados como uma coleção.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

Executa *sqlstatement* (com parâmetros opcionais) e retorna um único registro.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

Executa *sqlstatement* (com parâmetros opcionais) e retorna um único valor.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>Auxiliares

### `Analytics.GetGoogleHtml(webPropertyId)`

Renderiza o código JavaScript do Google Analytics para o ID especificado.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

Renderiza o código JavaScript do StatCounter Analytics para o projeto especificado.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

Renderiza o código JavaScript do Yahoo Analytics para a conta especificada.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Passa uma busca para Bing. Para especificar o site para pesquisar e um título `Bing.SiteUrl` `Bing.SiteTitle` para a caixa de pesquisa, você pode definir as propriedades e. Normalmente você define * \_* essas propriedades na página AppStart.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

Inicializa um gráfico.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

Adiciona uma lenda a um gráfico.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

Adiciona uma série de valores ao gráfico.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

Retorna um hash para os dados especificados. O algoritmo `sha256`padrão é .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Permite que os usuários do Facebook façam uma conexão com páginas.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

Renderiza ui para upload de arquivos.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

Renderiza a tag gamer Xbox especificada.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

Renderiza a imagem gravatar para o endereço de e-mail especificado.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

Converte um objeto de dados em uma seqüência no formato JSON (JavaScript Object Notation, notação de objeto sinuoso).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

Converte uma seqüência de entrada codificada pelo JSON em um objeto de dados que você pode iterar ou inserir em um banco de dados.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

Renderiza links de rede social usando o título especificado e url opcional.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

Associa uma mensagem de erro a um campo de formulário. Use `ModelState` o ajudante para acessar este membro.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

Associa uma mensagem de erro a um formulário. Use `ModelState` o ajudante para acessar este membro.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

Retorna verdadeiro se não houver erros de validação. Use `ModelState` o ajudante para acessar este membro.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

Torna as propriedades e valores de um objeto e quaisquer objetos infantis.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

Torna o teste de verificação reCAPTCHA.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

Define chaves públicas e privadas para o serviço reCAPTCHA. Normalmente você define * \_* essas propriedades na página AppStart.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

Retorna o resultado do teste reCAPTCHA.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

Renderiza informações de status sobre ASP.NET Páginas da Web.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

Renderiza um fluxo de Twitter para o usuário especificado.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

Renderiza um fluxo do Twitter para o texto de pesquisa especificado.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

Renderiza um reprodutor de vídeo Flash para o arquivo especificado com largura e altura opcionais.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

Renderiza um reprodutor de mídia do Windows para o arquivo especificado com largura e altura opcionais.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

Renderiza um leitor Silverlight para o arquivo *.xap* especificado com largura e altura necessárias.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

Retorna o objeto especificado por *chave*ou nulo se o objeto não for encontrado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

Remove o objeto especificado pela *chave* do cache.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

Coloca o *valor* no cache sob o nome especificado por *chave*.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

Cria um `WebGrid` novo objeto usando dados de uma consulta.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

Renderiza marcação para exibir dados em uma tabela HTML.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

Renderiza um pager `WebGrid` para o objeto.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

Carrega uma imagem do caminho especificado.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

Adiciona a imagem especificada como marca d'água.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

Adiciona o texto especificado à imagem.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

Inverte a imagem horizontal ou verticalmente.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

Carrega uma imagem quando uma imagem é postada em uma página durante um upload de arquivo.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

Redimensiona uma imagem.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

Gira a imagem para a esquerda ou para a direita.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

Salva a imagem no caminho especificado.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

Define a senha do servidor SMTP. Normalmente você define * \_* essa propriedade na página AppStart.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

Envia uma mensagem de email.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

Define o nome do servidor SMTP. Normalmente você define * \_* essa propriedade na página AppStart.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

Define o nome de usuário para o servidor SMTP. Normalmente, você deve * \_* definir essa propriedade na página AppStart.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>Validação

### `Html.ValidationMessage(field)`

(v2) Renderiza uma mensagem de erro de validação para o campo especificado.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

(v2) Exibe uma lista de todos os erros de validação.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

(v2) Registra um elemento de entrada do usuário para o tipo especificado de validação.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

(v2) Renderiza dinamicamente atributos de classe CSS para validação do lado do cliente para que você possa formatar mensagens de erro de validação. (Requer que você faça referência às bibliotecas de scripts de cliente apropriadas e que você defina classes CSS.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

(v2) Habilita a validação do lado do cliente para o campo de entrada do usuário. (Requer que você faça referência às bibliotecas de scripts de cliente apropriadas.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

(v2) Retorna verdadeiro se todos os elementos de entrada do usuário que forem cadastrados para validação contiverem valores válidos.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

(v2) Especifica que os usuários devem fornecer um valor para o elemento de entrada do usuário.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

(v2) Especifica que os usuários devem fornecer valores para cada um dos elementos de entrada do usuário. Este método não permite especificar uma mensagem de erro personalizada.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

(v2) Especifica um teste de validação `Validation.Add` quando você usa o método.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
