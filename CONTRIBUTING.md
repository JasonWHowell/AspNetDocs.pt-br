# <a name="contribute-to-the-aspnet-documentation"></a><span data-ttu-id="be953-101">Contribuir para a documentação do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="be953-101">Contribute to the ASP.NET documentation</span></span>

<span data-ttu-id="be953-102">Este documento aborda o processo para contribuir para os artigos e exemplos de código hospedados no [site de documentação do ASP.NET](https://docs.microsoft.com/aspnet/).</span><span class="sxs-lookup"><span data-stu-id="be953-102">This document covers the process for contributing to the articles and code samples that are hosted on the [ASP.NET documentation site](https://docs.microsoft.com/aspnet/).</span></span> <span data-ttu-id="be953-103">Correções de erros de digitação e novos artigos são contribuições bem-vindas.</span><span class="sxs-lookup"><span data-stu-id="be953-103">Typo corrections and new articles are welcome contributions.</span></span>

## <a name="how-to-make-a-simple-correction-or-suggestion"></a><span data-ttu-id="be953-104">Como fazer uma correção ou sugestão simples</span><span class="sxs-lookup"><span data-stu-id="be953-104">How to make a simple correction or suggestion</span></span>

<span data-ttu-id="be953-105">Artigos são armazenados no repositório, como arquivos de Markdown.</span><span class="sxs-lookup"><span data-stu-id="be953-105">Articles are stored in the repository as Markdown files.</span></span> <span data-ttu-id="be953-106">São feitas alterações simples ao conteúdo de um arquivo Markdown no navegador selecionando o link **Editar** no canto superior direito da janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="be953-106">Simple changes to the content of a Markdown file are made in the browser by selecting the **Edit** link in the upper-right corner of the browser window.</span></span> <span data-ttu-id="be953-107">(Em uma janela estreita do navegador, expanda a barra de **Opções** para ver o link **Editar** .) Siga as instruções para criar uma solicitação de pull (PR).</span><span class="sxs-lookup"><span data-stu-id="be953-107">(In a narrow browser window, expand the **options** bar to see the **Edit** link.) Follow the directions to create a pull request (PR).</span></span> <span data-ttu-id="be953-108">Vamos examinar a PR e aceitá-la ou sugerir alterações.</span><span class="sxs-lookup"><span data-stu-id="be953-108">We will review the PR and accept it or suggest changes.</span></span>

## <a name="how-to-make-a-more-complex-submission"></a><span data-ttu-id="be953-109">Como fazer um envio mais complexo</span><span class="sxs-lookup"><span data-stu-id="be953-109">How to make a more complex submission</span></span>

<span data-ttu-id="be953-110">Você precisa de uma compreensão básica do [Git e do GitHub.com](https://guides.github.com/activities/hello-world/).</span><span class="sxs-lookup"><span data-stu-id="be953-110">You need a basic understanding of [Git and GitHub.com](https://guides.github.com/activities/hello-world/).</span></span>

* <span data-ttu-id="be953-111">Abra um [Problema](https://github.com/dotnet/AspNetDocs/issues/new) descrevendo o que você deseja fazer, como alterar um artigo existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="be953-111">Open an [issue](https://github.com/dotnet/AspNetDocs/issues/new) describing what you want to do, such as changing an existing article or creating a new one.</span></span> <span data-ttu-id="be953-112">Geralmente, solicitamos uma estrutura de tópicos para uma nova sugestão de tópico.</span><span class="sxs-lookup"><span data-stu-id="be953-112">We often request an outline for a new topic suggestion.</span></span> <span data-ttu-id="be953-113">Aguarde a aprovação da equipe antes de investir muito tempo.</span><span class="sxs-lookup"><span data-stu-id="be953-113">Wait for approval from the team before you invest much time.</span></span>
* <span data-ttu-id="be953-114">Bifurcar o repositório [dotnet/AspNetDocs](https://github.com/dotnet/AspNetDocs/) e criar uma ramificação para suas alterações.</span><span class="sxs-lookup"><span data-stu-id="be953-114">Fork the [dotnet/AspNetDocs](https://github.com/dotnet/AspNetDocs/) repository and create a branch for your changes.</span></span>
* <span data-ttu-id="be953-115">Enviar um PR para mestre com suas alterações.</span><span class="sxs-lookup"><span data-stu-id="be953-115">Submit a PR to master with your changes.</span></span>
* <span data-ttu-id="be953-116">Se a PR tiver o rótulo 'cla-required' atribuído, [conclua o CLA (Contrato de Licença de Contribuição)](https://cla.dotnetfoundation.org/).</span><span class="sxs-lookup"><span data-stu-id="be953-116">If your PR has the label 'cla-required' assigned, [complete the Contribution License Agreement (CLA)](https://cla.dotnetfoundation.org/).</span></span>
* <span data-ttu-id="be953-117">Responda aos comentários de PR.</span><span class="sxs-lookup"><span data-stu-id="be953-117">Respond to PR feedback.</span></span>

<span data-ttu-id="be953-118">Para obter um exemplo em que esse processo levou à publicação de um novo artigo, confira [Problema &num;67](https://github.com/dotnet/docs/issues/67) e [Solicitação Pull &num;798](https://github.com/dotnet/docs/pull/798) no repositório de Documentos do .NET.</span><span class="sxs-lookup"><span data-stu-id="be953-118">For an example where this process led to publication of a new article, see [Issue &num;67](https://github.com/dotnet/docs/issues/67) and [Pull Request &num;798](https://github.com/dotnet/docs/pull/798) in the .NET Docs repository.</span></span> <span data-ttu-id="be953-119">O novo artigo é [Documentando seu código](https://docs.microsoft.com/dotnet/articles/csharp/codedoc).</span><span class="sxs-lookup"><span data-stu-id="be953-119">The new article is [Documenting your code](https://docs.microsoft.com/dotnet/articles/csharp/codedoc).</span></span>

## <a name="docs-authoring-pack-extension-in-visual-studio-code"></a><span data-ttu-id="be953-120">Extensão do Pacote de Criação de Documentos no Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="be953-120">Docs Authoring Pack extension in Visual Studio Code</span></span>

<span data-ttu-id="be953-121">Se você usar o Visual Studio Code para contribuir para a documentação do ASP.NET, você poderá aumentar sua produtividade instalando a extensão [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack).</span><span class="sxs-lookup"><span data-stu-id="be953-121">If you use Visual Studio Code to contribute to the ASP.NET documentation, you can boost your productivity by installing the [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) extension.</span></span> <span data-ttu-id="be953-122">A extensão fornece uma variedade de ferramentas que ajudam com linting de Markdown, verificação ortográfica do código e modelos de artigo.</span><span class="sxs-lookup"><span data-stu-id="be953-122">The extension provides a variety of tools that helps with Markdown linting, code spell checking, and article templates.</span></span>

## <a name="markdown-syntax"></a><span data-ttu-id="be953-123">Sintaxe de markdown</span><span class="sxs-lookup"><span data-stu-id="be953-123">Markdown syntax</span></span>

<span data-ttu-id="be953-124">Os artigos são escritos em [Markdown para DocFx](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html), que é um superconjunto de [GFM (Markdown para GitHub)](https://guides.github.com/features/mastering-markdown/).</span><span class="sxs-lookup"><span data-stu-id="be953-124">Articles are written in [DocFx-flavored Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html), which is a superset of [GitHub-flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown/).</span></span> <span data-ttu-id="be953-125">Para obter exemplos de sintaxe de DFM para recursos de interface do usuário comumente usados na documentação do ASP.NET, consulte [modelo de redução e metadados](https://github.com/dotnet/docs/blob/master/styleguide/template.md) no guia de estilo de repositório do .net docs.</span><span class="sxs-lookup"><span data-stu-id="be953-125">For examples of DFM syntax for UI features commonly used in the ASP.NET documentation, see [Metadata and Markdown Template](https://github.com/dotnet/docs/blob/master/styleguide/template.md) in the .NET Docs repository style guide.</span></span>

## <a name="folder-structure-conventions"></a><span data-ttu-id="be953-126">Convenções de estrutura de pasta</span><span class="sxs-lookup"><span data-stu-id="be953-126">Folder structure conventions</span></span>

<span data-ttu-id="be953-127">Para cada arquivo de Markdown, podem existir uma pasta para imagens e uma pasta para o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="be953-127">For each Markdown file, a folder for images and a folder for sample code may exist.</span></span> <span data-ttu-id="be953-128">Se o artigo for [signalr/Overview/avançado/Dependency-disparation. MD](https://github.com/dotnet/AspNetDocs/blob/master/aspnet/signalr/overview/advanced/dependency-injection.md), as imagens estarão em [signalr/Overview/avançado/Dependency-disparation/\_static](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/_static) e os arquivos de projeto do aplicativo de exemplo estarão em [signalr/Overview/avançado/Dependency-disjeções/Samples](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/samples).</span><span class="sxs-lookup"><span data-stu-id="be953-128">If the article is [signalr/overview/advanced/dependency-injection.md](https://github.com/dotnet/AspNetDocs/blob/master/aspnet/signalr/overview/advanced/dependency-injection.md), the images are in [signalr/overview/advanced/dependency-injection/\_static](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/_static) and the sample app project files are in [signalr/overview/advanced/dependency-injection/samples](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/samples).</span></span> <span data-ttu-id="be953-129">Uma imagem no arquivo *signaler/Overview/Advanced/Dependency-injeção. MD* é renderizada pela seguinte redução:</span><span class="sxs-lookup"><span data-stu-id="be953-129">An image in the *signalr/overview/advanced/dependency-injection.md* file is rendered by the following Markdown:</span></span>

```md
![description of image for alt attribute](dependency-injection/_static/image1.png)
```

<span data-ttu-id="be953-130">Todas as imagens devem ter um [texto alternativo (alt)](https://wikipedia.org/wiki/Alt_attribute).</span><span class="sxs-lookup"><span data-stu-id="be953-130">All images should have [alternative (alt) text](https://wikipedia.org/wiki/Alt_attribute).</span></span> <span data-ttu-id="be953-131">Para orientação sobre a especificação de texto alternativo, confira recursos online, como [WebAIM: Texto Alternativo](https://webaim.org/techniques/alttext/).</span><span class="sxs-lookup"><span data-stu-id="be953-131">For advice on specifying alt text, see online resources, such as [WebAIM: Alternative Text](https://webaim.org/techniques/alttext/).</span></span>

<span data-ttu-id="be953-132">Use letras minúsculas para nomes de arquivo de Markdown e nomes de arquivo de imagem.</span><span class="sxs-lookup"><span data-stu-id="be953-132">Use lowercase for Markdown file names and image file names.</span></span>

## <a name="internal-links"></a><span data-ttu-id="be953-133">Links internos</span><span class="sxs-lookup"><span data-stu-id="be953-133">Internal links</span></span>

<span data-ttu-id="be953-134">Links internos devem usar o `uid` do artigo de destino com um link xref (o texto do link está definido como o título do conteúdo vinculado):</span><span class="sxs-lookup"><span data-stu-id="be953-134">Internal links should use the `uid` of the target article with an xref link (link text is set to the linked content's title):</span></span>

```md
<xref:uid_of_the_topic>
```

<span data-ttu-id="be953-135">Se o título do artigo for inadequado para o texto do link (por exemplo, uma palavra ou frase em uma sentença for o texto do link), especifique o texto do link e o link xref com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="be953-135">If the title of the article is unsuitable for link text (for example, a word or phrase in a sentence is the link text), specify the xref link and link text with the following:</span></span>

```md
[link text](xref:uid_of_the_topic)
```

<span data-ttu-id="be953-136">Para obter mais informações, confira a [Referência Cruzada do DocFX](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference).</span><span class="sxs-lookup"><span data-stu-id="be953-136">For more information, see the [DocFX Cross Reference](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference).</span></span>

## <a name="images-and-screenshots"></a><span data-ttu-id="be953-137">Imagens e capturas de tela</span><span class="sxs-lookup"><span data-stu-id="be953-137">Images and screenshots</span></span>

<span data-ttu-id="be953-138">Não inclua imagens nos artigos, exceto:</span><span class="sxs-lookup"><span data-stu-id="be953-138">Don't include images with articles, except:</span></span>

* <span data-ttu-id="be953-139">Nos tutoriais básicos de integração (iniciante).</span><span class="sxs-lookup"><span data-stu-id="be953-139">In basic onboarding (beginner) tutorials.</span></span>
* <span data-ttu-id="be953-140">Quando uma imagem é necessária para esclarecimento.</span><span class="sxs-lookup"><span data-stu-id="be953-140">When an image is needed for clarity.</span></span>

<span data-ttu-id="be953-141">Essas restrições reduzem o tamanho do repositório.</span><span class="sxs-lookup"><span data-stu-id="be953-141">These restrictions reduce the size of the repository.</span></span>

<span data-ttu-id="be953-142">Como uma etapa opcional, compacte as imagens e as capturas de tela usadas na documentação, o que ajuda com o desempenho de carregamento de página e o tamanho do arquivo.</span><span class="sxs-lookup"><span data-stu-id="be953-142">As an optional step, ensure that any images and screenshots used in the documentation are compressed, which helps with file size and page load performance.</span></span> <span data-ttu-id="be953-143">Algumas ferramentas populares incluem TinyPNG (usando o [site TinyPNG](https://tinypng.com/) ou a [API TinyPNG](https://tinypng.com/developers)) ou a extensão [Otimizador de Imagem](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be953-143">A few popular tools include TinyPNG (using the [TinyPNG website](https://tinypng.com/) or the [TinyPNG API](https://tinypng.com/developers)) or the [Image Optimizer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) Visual Studio extension.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="be953-144">Snippets de código</span><span class="sxs-lookup"><span data-stu-id="be953-144">Code snippets</span></span>

<span data-ttu-id="be953-145">Artigos geralmente contêm snippets de código para ilustrar os pontos.</span><span class="sxs-lookup"><span data-stu-id="be953-145">Articles frequently contain code snippets to illustrate points.</span></span> <span data-ttu-id="be953-146">O DFM permite que você copie o código para o arquivo de Markdown ou consulte um arquivo de código separado.</span><span class="sxs-lookup"><span data-stu-id="be953-146">DFM allows you to copy code into the Markdown file or refer to a separate code file.</span></span> <span data-ttu-id="be953-147">Preferimos usar arquivos de código separados sempre que possível para minimizar a chance de erros no código.</span><span class="sxs-lookup"><span data-stu-id="be953-147">We prefer to use separate code files whenever possible to minimize the chance of errors in the code.</span></span> <span data-ttu-id="be953-148">Os arquivos de código são armazenados no repositório usando a estrutura de pastas descrita anteriormente para projetos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="be953-148">The code files are stored in the repository using the folder structure described earlier for sample projects.</span></span>

<span data-ttu-id="be953-149">Os exemplos a seguir ilustram a [sintaxe do snippet de código do DFM](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet) a ser usada em um arquivo *configuration/index.md*.</span><span class="sxs-lookup"><span data-stu-id="be953-149">The following examples illustrate [DFM code snippet syntax](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet) for use in a *configuration/index.md* file.</span></span>

<span data-ttu-id="be953-150">Para renderizar um arquivo de código inteiro como um snippet:</span><span class="sxs-lookup"><span data-stu-id="be953-150">To render an entire code file as a snippet:</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs)]
```

<span data-ttu-id="be953-151">Para renderizar uma parte de um arquivo como um snippet usando números de linha:</span><span class="sxs-lookup"><span data-stu-id="be953-151">To render a portion of a file as a snippet by using line numbers:</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?range=1-10,20,30,40-50]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=1-10,20,30,40-50]
```

<span data-ttu-id="be953-152">Para snippets C#, faça referência a uma [região do C#](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region).</span><span class="sxs-lookup"><span data-stu-id="be953-152">For C# snippets, reference a [C# region](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region).</span></span> <span data-ttu-id="be953-153">Sempre que possível, use regiões, em vez de números de linha, pois números de linha em um arquivo de código tendem a mudar e sair de sincronia com referências de número de linha em Markdown.</span><span class="sxs-lookup"><span data-stu-id="be953-153">Whenever possible, use regions rather than line numbers because line numbers in a code file tend to change and become out of sync with line number references in Markdown.</span></span> <span data-ttu-id="be953-154">Regiões do C# podem ser aninhadas.</span><span class="sxs-lookup"><span data-stu-id="be953-154">C# regions can be nested.</span></span> <span data-ttu-id="be953-155">Se estiver fazendo referência à região externa, as diretivas `#region` e `#endregion` internas não serão renderizadas em um snippet.</span><span class="sxs-lookup"><span data-stu-id="be953-155">If referencing the outer region, the inner `#region` and `#endregion` directives aren't rendered in a snippet.</span></span>

<span data-ttu-id="be953-156">Para renderizar uma região C# chamada "snippet_Example":</span><span class="sxs-lookup"><span data-stu-id="be953-156">To render a C# region named "snippet_Example":</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example)]
```

<span data-ttu-id="be953-157">Para realçar as linhas selecionadas em um snippet renderizado (geralmente é renderizado como a cor da tela de fundo amarela):</span><span class="sxs-lookup"><span data-stu-id="be953-157">To highlight selected lines in a rendered snippet (usually renders as yellow background color):</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example&highlight=1-3,10,20-25)]
[!code-csharp[](configuration/index/sample/Program.cs?range=10-20&highlight=1-3]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=10-20&highlight=1-3]
[!code-javascript[](configuration/index/sample/UsingOptionsSample.csproj?range=10-20&highlight=1-3]
```

## <a name="test-changes-with-docfx"></a><span data-ttu-id="be953-158">Testar alterações com o DocFX</span><span class="sxs-lookup"><span data-stu-id="be953-158">Test changes with DocFX</span></span>

<span data-ttu-id="be953-159">Teste suas alterações com a [ferramenta de linha de comando do DocFX](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool), que cria uma versão hospedada localmente do site.</span><span class="sxs-lookup"><span data-stu-id="be953-159">Test your changes with the [DocFX command-line tool](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool), which creates a locally hosted version of the site.</span></span> <span data-ttu-id="be953-160">O DocFX não renderiza extensões de site e estilo criadas para docs.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="be953-160">DocFX doesn't render style and site extensions created for docs.microsoft.com.</span></span>

<span data-ttu-id="be953-161">O DocFX requer:</span><span class="sxs-lookup"><span data-stu-id="be953-161">DocFX requires:</span></span>

* <span data-ttu-id="be953-162">.NET framework no Windows.</span><span class="sxs-lookup"><span data-stu-id="be953-162">.NET Framework on Windows.</span></span>
* <span data-ttu-id="be953-163">Mono para Linux ou macOS.</span><span class="sxs-lookup"><span data-stu-id="be953-163">Mono for Linux or macOS.</span></span>

### <a name="windows-instructions"></a><span data-ttu-id="be953-164">Instruções do Windows</span><span class="sxs-lookup"><span data-stu-id="be953-164">Windows instructions</span></span>

* <span data-ttu-id="be953-165">Baixe e descompacte *docfx.zip* de [versões do DocFX](https://github.com/dotnet/docfx/releases).</span><span class="sxs-lookup"><span data-stu-id="be953-165">Download and unzip *docfx.zip* from [DocFX releases](https://github.com/dotnet/docfx/releases).</span></span>
* <span data-ttu-id="be953-166">Adicione DocFX ao seu PATH.</span><span class="sxs-lookup"><span data-stu-id="be953-166">Add DocFX to your PATH.</span></span>
* <span data-ttu-id="be953-167">Em um shell de comando, navegue até a pasta *ASPNET* que contém o arquivo *docfx. JSON* e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="be953-167">In a command shell, navigate to the *aspnet* folder that contains the *docfx.json* file and run the following command:</span></span>

  ```console
  docfx --serve
  ```

* <span data-ttu-id="be953-168">Em um navegador, navegue até `http://localhost:8080/group1-dest/`.</span><span class="sxs-lookup"><span data-stu-id="be953-168">In a browser, navigate to `http://localhost:8080/group1-dest/`.</span></span>

### <a name="mono-instructions"></a><span data-ttu-id="be953-169">Instruções do mono</span><span class="sxs-lookup"><span data-stu-id="be953-169">Mono instructions</span></span>

* <span data-ttu-id="be953-170">Instalar o Mono por meio do Homebrew:</span><span class="sxs-lookup"><span data-stu-id="be953-170">Install Mono via Homebrew:</span></span>

  ```console
  brew install mono
  ```

* <span data-ttu-id="be953-171">Baixe a [versão mais recente do DocFX](https://github.com/dotnet/docfx/releases).</span><span class="sxs-lookup"><span data-stu-id="be953-171">Download the [latest version of DocFX](https://github.com/dotnet/docfx/releases).</span></span>
* <span data-ttu-id="be953-172">Extraia o arquivo para *$HOME/bin/docfx*.</span><span class="sxs-lookup"><span data-stu-id="be953-172">Extract the archive to *$HOME/bin/docfx*.</span></span>
* <span data-ttu-id="be953-173">Crie um par de aliases para **docfx** em um shell de Busca.</span><span class="sxs-lookup"><span data-stu-id="be953-173">Create a pair of aliases for **docfx** in a bash shell.</span></span> <span data-ttu-id="be953-174">O primeiro alias é usado para criar a documentação.</span><span class="sxs-lookup"><span data-stu-id="be953-174">The first alias is used to build the documentation.</span></span> <span data-ttu-id="be953-175">O segundo alias é usado para criar e fornecer a documentação.</span><span class="sxs-lookup"><span data-stu-id="be953-175">The second alias is used to build and serve the documentation.</span></span>

  ```console
  alias docfx='mono $HOME/bin/docfx/docfx.exe'
  alias docfx-serve='mono $HOME/bin/docfx/docfx.exe --serve'
  ```

* <span data-ttu-id="be953-176">Em um shell de comando, navegue até a pasta *ASPNET* que contém o arquivo *docfx. JSON* e execute o comando a seguir para criar e fornecer os documentos por meio de seu alias:</span><span class="sxs-lookup"><span data-stu-id="be953-176">In a command shell, navigate to the *aspnet* folder that contains the *docfx.json* file  and run the following command to build and serve the docs via its alias:</span></span>

  ```console
  docfx-serve
  ```

* <span data-ttu-id="be953-177">Em um navegador, navegue até `http://localhost:8080/group1-dest/`.</span><span class="sxs-lookup"><span data-stu-id="be953-177">In a browser, navigate to `http://localhost:8080/group1-dest/`.</span></span>

## <a name="voice-and-tone"></a><span data-ttu-id="be953-178">Voz e tom</span><span class="sxs-lookup"><span data-stu-id="be953-178">Voice and tone</span></span>

<span data-ttu-id="be953-179">Nossa meta é escrever uma documentação que possa ser facilmente compreendida pelo maior público possível.</span><span class="sxs-lookup"><span data-stu-id="be953-179">Our goal is to write documentation that is easily understandable by the widest possible audience.</span></span> <span data-ttu-id="be953-180">Para esse fim, estabelecemos diretrizes para estilo de escrita que pedimos que nosso colaboradores sigam.</span><span class="sxs-lookup"><span data-stu-id="be953-180">To that end, we established guidelines for writing style that we ask our contributors to follow.</span></span> <span data-ttu-id="be953-181">Para obter mais informações, consulte [diretrizes de voz e Tom](https://github.com/dotnet/docs/blob/master/styleguide/voice-tone.md) no repositório do .net.</span><span class="sxs-lookup"><span data-stu-id="be953-181">For more information, see [Voice and tone guidelines](https://github.com/dotnet/docs/blob/master/styleguide/voice-tone.md) in the .NET repository.</span></span>

## <a name="microsoft-writing-style-guide"></a><span data-ttu-id="be953-182">Guia de Estilo de Escrita da Microsoft</span><span class="sxs-lookup"><span data-stu-id="be953-182">Microsoft Writing Style Guide</span></span>

<span data-ttu-id="be953-183">O [Guia de Estilo de Escrita da Microsoft](https://docs.microsoft.com/style-guide/welcome/) fornece orientação sobre estilo e terminologia de escrita para todas as formas de comunicação de tecnologia, incluindo a documentação do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="be953-183">The [Microsoft Writing Style Guide](https://docs.microsoft.com/style-guide/welcome/) provides writing style and terminology guidance for all forms of technology communication, including the ASP.NET Core documentation.</span></span>

## <a name="redirects"></a><span data-ttu-id="be953-184">Redirecionamentos</span><span class="sxs-lookup"><span data-stu-id="be953-184">Redirects</span></span>

<span data-ttu-id="be953-185">Se você excluir um artigo, altere seu nome de arquivo ou mova-o para uma pasta diferente, crie um redirecionamento para que as pessoas que marcaram o artigo como favorito não recebem um erro *404 Não Encontrado*.</span><span class="sxs-lookup"><span data-stu-id="be953-185">If you delete an article, change its file name, or move it to a different folder, create a redirect so that people who bookmarked the article don't receive a *404 Not Found* error.</span></span> <span data-ttu-id="be953-186">Adicione redirecionamentos para o [arquivo de redirecionamento mestre](https://github.com/dotnet/AspNetDocs/blob/master/.openpublishing.redirection.json).</span><span class="sxs-lookup"><span data-stu-id="be953-186">Add redirects to the [master redirect file](https://github.com/dotnet/AspNetDocs/blob/master/.openpublishing.redirection.json).</span></span>
