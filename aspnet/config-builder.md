---
uid: config-builder
title: Construtores de configuração para ASP.NET
author: rick-anderson
description: Saiba como obter dados de configuração de fontes diferentes de valores Web. config de fontes externas.
ms.author: riande
ms.date: 10/29/2018
msc.type: content
ms.openlocfilehash: 5299d9ab057c3096773955a7461e77a80673ebfe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586760"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="f6d15-103">Construtores de configuração para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f6d15-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="f6d15-104">Por [Stephen Molloy](https://github.com/StephenMolloy) e [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f6d15-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f6d15-105">Os construtores de configuração fornecem um mecanismo moderno e ágil para aplicativos ASP.NET obterem valores de configuração de fontes externas.</span><span class="sxs-lookup"><span data-stu-id="f6d15-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="f6d15-106">Construtores de configuração:</span><span class="sxs-lookup"><span data-stu-id="f6d15-106">Configuration builders:</span></span>

* <span data-ttu-id="f6d15-107">Estão disponíveis no .NET Framework 4.7.1 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="f6d15-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="f6d15-108">Forneça um mecanismo flexível para ler valores de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="f6d15-109">Resolva algumas das necessidades básicas dos aplicativos à medida que eles se movem para um ambiente voltado para a nuvem e um contêiner.</span><span class="sxs-lookup"><span data-stu-id="f6d15-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="f6d15-110">Pode ser usado para melhorar a proteção de dados de configuração por meio do desenho de fontes anteriormente indisponíveis (por exemplo, Azure Key Vault e variáveis de ambiente) no sistema de configuração do .NET.</span><span class="sxs-lookup"><span data-stu-id="f6d15-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="f6d15-111">Construtores de configuração de chave/valor</span><span class="sxs-lookup"><span data-stu-id="f6d15-111">Key/value configuration builders</span></span>

<span data-ttu-id="f6d15-112">Um cenário comum que pode ser tratado por construtores de configuração é fornecer um mecanismo básico de substituição de chave/valor para seções de configuração que seguem um padrão de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="f6d15-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="f6d15-113">O conceito de .NET Framework de ConfigurationBuilders não é limitado a seções ou padrões de configuração específicos.</span><span class="sxs-lookup"><span data-stu-id="f6d15-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="f6d15-114">No entanto, muitos dos construtores de configuração no `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) funcionam dentro do padrão de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="f6d15-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="f6d15-115">Configurações de construtores de configuração de chave/valor</span><span class="sxs-lookup"><span data-stu-id="f6d15-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="f6d15-116">As configurações a seguir se aplicam a todos os construtores de configuração de chave/valor no `Microsoft.Configuration.ConfigurationBuilders`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="f6d15-117">Mode.</span><span class="sxs-lookup"><span data-stu-id="f6d15-117">Mode</span></span>

<span data-ttu-id="f6d15-118">Os construtores de configuração usam uma fonte externa de informações de chave/valor para preencher os elementos de chave/valor selecionados do sistema de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="f6d15-119">Especificamente, as seções `<appSettings/>` e `<connectionStrings/>` recebem tratamento especial dos criadores de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="f6d15-120">Os criadores funcionam em três modos:</span><span class="sxs-lookup"><span data-stu-id="f6d15-120">The builders work in three modes:</span></span>

* <span data-ttu-id="f6d15-121">`Strict`-o modo padrão.</span><span class="sxs-lookup"><span data-stu-id="f6d15-121">`Strict` - The default mode.</span></span> <span data-ttu-id="f6d15-122">Nesse modo, o construtor de configuração opera apenas em seções de configuração bem conhecidas de chave/valor centrado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="f6d15-123">o modo de `Strict` enumera cada chave na seção.</span><span class="sxs-lookup"><span data-stu-id="f6d15-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="f6d15-124">Se uma chave correspondente for encontrada na fonte externa:</span><span class="sxs-lookup"><span data-stu-id="f6d15-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="f6d15-125">Os construtores de configuração substituem o valor na seção de configuração resultante pelo valor da fonte externa.</span><span class="sxs-lookup"><span data-stu-id="f6d15-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="f6d15-126">`Greedy`-esse modo está bem relacionado ao modo de `Strict`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="f6d15-127">Em vez de ser limitado a chaves que já existem na configuração original:</span><span class="sxs-lookup"><span data-stu-id="f6d15-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="f6d15-128">Os construtores de configuração adicionam todos os pares de chave/valor da fonte externa na seção de configuração resultante.</span><span class="sxs-lookup"><span data-stu-id="f6d15-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="f6d15-129">`Expand`-opera no XML bruto antes que ele seja analisado em um objeto da seção de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="f6d15-130">Pode ser pensado como uma expansão de tokens em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f6d15-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="f6d15-131">Qualquer parte da cadeia de caracteres XML bruta que corresponda ao padrão `${token}` é um candidato para a expansão do token.</span><span class="sxs-lookup"><span data-stu-id="f6d15-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="f6d15-132">Se nenhum valor correspondente for encontrado na origem externa, o token não será alterado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="f6d15-133">Os construtores neste modo não estão limitados às seções `<appSettings/>` e `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="f6d15-134">A marcação a seguir de *Web. config* habilita o [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) no modo de `Strict`:</span><span class="sxs-lookup"><span data-stu-id="f6d15-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="f6d15-135">O código a seguir lê o `<appSettings/>` e `<connectionStrings/>` mostrados no arquivo *Web. config* anterior:</span><span class="sxs-lookup"><span data-stu-id="f6d15-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="f6d15-136">O código anterior definirá os valores de propriedade como:</span><span class="sxs-lookup"><span data-stu-id="f6d15-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="f6d15-137">Os valores no arquivo *Web. config* se as chaves não estiverem definidas em variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="f6d15-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="f6d15-138">Os valores da variável de ambiente, se definido.</span><span class="sxs-lookup"><span data-stu-id="f6d15-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="f6d15-139">Por exemplo, `ServiceID` conterá:</span><span class="sxs-lookup"><span data-stu-id="f6d15-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="f6d15-140">"ServiceId valor de Web. config", se a variável de ambiente `ServiceID` não estiver definida.</span><span class="sxs-lookup"><span data-stu-id="f6d15-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="f6d15-141">O valor da variável de ambiente `ServiceID`, se definido.</span><span class="sxs-lookup"><span data-stu-id="f6d15-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="f6d15-142">A imagem a seguir mostra as `<appSettings/>` chaves/valores do arquivo *Web. config* anterior definido no editor de ambiente:</span><span class="sxs-lookup"><span data-stu-id="f6d15-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![Editor de ambiente](config-builder/static/env.png)

<span data-ttu-id="f6d15-144">Observação: Talvez seja necessário sair e reiniciar o Visual Studio para ver as alterações nas variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="f6d15-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="f6d15-145">Manipulação de prefixo</span><span class="sxs-lookup"><span data-stu-id="f6d15-145">Prefix handling</span></span>

<span data-ttu-id="f6d15-146">Os prefixos de chave podem simplificar a configuração de chaves porque:</span><span class="sxs-lookup"><span data-stu-id="f6d15-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="f6d15-147">A configuração de .NET Framework é complexa e aninhada.</span><span class="sxs-lookup"><span data-stu-id="f6d15-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="f6d15-148">As origens de chave/valor externas são normalmente básicas e planas por natureza.</span><span class="sxs-lookup"><span data-stu-id="f6d15-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="f6d15-149">Por exemplo, variáveis de ambiente não são aninhadas.</span><span class="sxs-lookup"><span data-stu-id="f6d15-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="f6d15-150">Use qualquer uma das abordagens a seguir para injetar `<appSettings/>` e `<connectionStrings/>` na configuração por meio de variáveis de ambiente:</span><span class="sxs-lookup"><span data-stu-id="f6d15-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="f6d15-151">Com a `EnvironmentConfigBuilder` no modo de `Strict` padrão e os nomes de chave apropriados no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="f6d15-152">O código e a marcação anteriores assumem essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="f6d15-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="f6d15-153">Usando essa abordagem, você **não** pode ter chaves nomeadas de forma idêntica nas `<appSettings/>` e `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="f6d15-154">Use dois `EnvironmentConfigBuilder`s no modo `Greedy` com prefixos e `stripPrefix`distintos.</span><span class="sxs-lookup"><span data-stu-id="f6d15-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="f6d15-155">Com essa abordagem, o aplicativo pode ler `<appSettings/>` e `<connectionStrings/>` sem a necessidade de atualizar o arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="f6d15-156">A próxima seção, [stripPrefix](#stripprefix), mostra como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="f6d15-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="f6d15-157">Use dois `EnvironmentConfigBuilder`s no modo `Greedy` com prefixos distintos.</span><span class="sxs-lookup"><span data-stu-id="f6d15-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="f6d15-158">Com essa abordagem, você não pode ter nomes de chave duplicados, pois nomes de chave devem ser diferentes por prefixo.</span><span class="sxs-lookup"><span data-stu-id="f6d15-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="f6d15-159">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6d15-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="f6d15-160">Com a marcação anterior, a mesma fonte de chave/valor simples pode ser usada para preencher a configuração de duas seções diferentes.</span><span class="sxs-lookup"><span data-stu-id="f6d15-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="f6d15-161">A imagem a seguir mostra as `<appSettings/>` e `<connectionStrings/>` chaves/valores do arquivo *Web. config* anterior definido no editor de ambiente:</span><span class="sxs-lookup"><span data-stu-id="f6d15-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![Editor de ambiente](config-builder/static/prefix.png)

<span data-ttu-id="f6d15-163">O código a seguir lê as `<appSettings/>` e `<connectionStrings/>` chaves/valores contidos no arquivo *Web. config* anterior:</span><span class="sxs-lookup"><span data-stu-id="f6d15-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="f6d15-164">O código anterior definirá os valores de propriedade como:</span><span class="sxs-lookup"><span data-stu-id="f6d15-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="f6d15-165">Os valores no arquivo *Web. config* se as chaves não estiverem definidas em variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="f6d15-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="f6d15-166">Os valores da variável de ambiente, se definido.</span><span class="sxs-lookup"><span data-stu-id="f6d15-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="f6d15-167">Por exemplo, usando o arquivo *Web. config* anterior, as chaves/valores na imagem do editor de ambiente anterior e o código anterior, os seguintes valores são definidos:</span><span class="sxs-lookup"><span data-stu-id="f6d15-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="f6d15-168">Chave</span><span class="sxs-lookup"><span data-stu-id="f6d15-168">Key</span></span>              | <span data-ttu-id="f6d15-169">Value</span><span class="sxs-lookup"><span data-stu-id="f6d15-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="f6d15-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="f6d15-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="f6d15-171">AppSetting_ServiceID de variáveis ENV</span><span class="sxs-lookup"><span data-stu-id="f6d15-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="f6d15-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="f6d15-172">AppSetting_default</span></span>            | <span data-ttu-id="f6d15-173">AppSetting_default valor de env</span><span class="sxs-lookup"><span data-stu-id="f6d15-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="f6d15-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="f6d15-174">ConnStr_default</span></span>         | <span data-ttu-id="f6d15-175">ConnStr_default Val de env</span><span class="sxs-lookup"><span data-stu-id="f6d15-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="f6d15-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="f6d15-176">stripPrefix</span></span>

<span data-ttu-id="f6d15-177">`stripPrefix`: booliano, o padrão é `false`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="f6d15-178">A marcação XML anterior separa as configurações do aplicativo das cadeias de conexão, mas requer que todas as chaves no arquivo *Web. config* usem o prefixo especificado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="f6d15-179">Por exemplo, o prefixo `AppSetting` deve ser adicionado à chave de `ServiceID` ("AppSetting_ServiceID").</span><span class="sxs-lookup"><span data-stu-id="f6d15-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="f6d15-180">Com `stripPrefix`, o prefixo não é usado no arquivo *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="f6d15-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="f6d15-181">O prefixo é necessário na origem do Configuration Builder (por exemplo, no ambiente). Prevemos que a maioria dos desenvolvedores usará `stripPrefix`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="f6d15-182">Normalmente, os aplicativos tiram o prefixo.</span><span class="sxs-lookup"><span data-stu-id="f6d15-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="f6d15-183">O *Web. config* a seguir remove o prefixo:</span><span class="sxs-lookup"><span data-stu-id="f6d15-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="f6d15-184">No arquivo *Web. config* anterior, a chave de `default` está tanto no `<appSettings/>` quanto no `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="f6d15-185">A imagem a seguir mostra as `<appSettings/>` e `<connectionStrings/>` chaves/valores do arquivo *Web. config* anterior definido no editor de ambiente:</span><span class="sxs-lookup"><span data-stu-id="f6d15-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![Editor de ambiente](config-builder/static/prefix.png)

<span data-ttu-id="f6d15-187">O código a seguir lê as `<appSettings/>` e `<connectionStrings/>` chaves/valores contidos no arquivo *Web. config* anterior:</span><span class="sxs-lookup"><span data-stu-id="f6d15-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="f6d15-188">O código anterior definirá os valores de propriedade como:</span><span class="sxs-lookup"><span data-stu-id="f6d15-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="f6d15-189">Os valores no arquivo *Web. config* se as chaves não estiverem definidas em variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="f6d15-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="f6d15-190">Os valores da variável de ambiente, se definido.</span><span class="sxs-lookup"><span data-stu-id="f6d15-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="f6d15-191">Por exemplo, usando o arquivo *Web. config* anterior, as chaves/valores na imagem do editor de ambiente anterior e o código anterior, os seguintes valores são definidos:</span><span class="sxs-lookup"><span data-stu-id="f6d15-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="f6d15-192">Chave</span><span class="sxs-lookup"><span data-stu-id="f6d15-192">Key</span></span>              | <span data-ttu-id="f6d15-193">Value</span><span class="sxs-lookup"><span data-stu-id="f6d15-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="f6d15-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="f6d15-194">ServiceID</span></span>           | <span data-ttu-id="f6d15-195">AppSetting_ServiceID de variáveis ENV</span><span class="sxs-lookup"><span data-stu-id="f6d15-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="f6d15-196">{1&gt;default&lt;1}</span><span class="sxs-lookup"><span data-stu-id="f6d15-196">default</span></span>            | <span data-ttu-id="f6d15-197">AppSetting_default valor de env</span><span class="sxs-lookup"><span data-stu-id="f6d15-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="f6d15-198">{1&gt;default&lt;1}</span><span class="sxs-lookup"><span data-stu-id="f6d15-198">default</span></span>         | <span data-ttu-id="f6d15-199">ConnStr_default Val de env</span><span class="sxs-lookup"><span data-stu-id="f6d15-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="f6d15-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="f6d15-200">tokenPattern</span></span>

<span data-ttu-id="f6d15-201">`tokenPattern`: cadeia de caracteres, o padrão é `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="f6d15-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="f6d15-202">O comportamento `Expand` dos construtores pesquisa o XML bruto em busca de tokens semelhantes a `${token}`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="f6d15-203">A pesquisa é feita com a expressão regular padrão `@"\$\{(\w+)\}"`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="f6d15-204">O conjunto de caracteres que corresponde a `\w` é mais estrito do que o XML e muitas fontes de configuração permitem.</span><span class="sxs-lookup"><span data-stu-id="f6d15-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="f6d15-205">Use `tokenPattern` quando mais caracteres do que `@"\$\{(\w+)\}"` forem necessários no nome do token.</span><span class="sxs-lookup"><span data-stu-id="f6d15-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="f6d15-206">`tokenPattern`: cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="f6d15-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="f6d15-207">Permite que os desenvolvedores alterem o Regex que é usado para correspondência de token.</span><span class="sxs-lookup"><span data-stu-id="f6d15-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="f6d15-208">Nenhuma validação é feita para garantir que se trata de um Regex bem formado e não perigoso.</span><span class="sxs-lookup"><span data-stu-id="f6d15-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="f6d15-209">Ele deve conter um grupo de captura.</span><span class="sxs-lookup"><span data-stu-id="f6d15-209">It must contain a capture group.</span></span> <span data-ttu-id="f6d15-210">O Regex inteiro deve corresponder ao token inteiro.</span><span class="sxs-lookup"><span data-stu-id="f6d15-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="f6d15-211">A primeira captura deve ser o nome do token a ser pesquisado na fonte de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="f6d15-212">Construtores de configuração em Microsoft. Configuration. ConfigurationBuilders</span><span class="sxs-lookup"><span data-stu-id="f6d15-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="f6d15-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="f6d15-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="f6d15-214">O [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="f6d15-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="f6d15-215">É a mais simples dos construtores de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="f6d15-216">Lê os valores do ambiente.</span><span class="sxs-lookup"><span data-stu-id="f6d15-216">Reads values from the environment.</span></span>
* <span data-ttu-id="f6d15-217">Não tem nenhuma opção de configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="f6d15-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="f6d15-218">O valor do atributo `name` é arbitrário.</span><span class="sxs-lookup"><span data-stu-id="f6d15-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="f6d15-219">**Observação:** Em um ambiente de contêiner do Windows, as variáveis definidas em tempo de execução são injetadas apenas no ambiente de processo EntryPoint.</span><span class="sxs-lookup"><span data-stu-id="f6d15-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="f6d15-220">Os aplicativos executados como um serviço ou um processo não-EntryPoint não pegam essas variáveis, a menos que eles sejam injetados por um mecanismo no contêiner.</span><span class="sxs-lookup"><span data-stu-id="f6d15-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="f6d15-221">Para o [IIS](https://github.com/Microsoft/iis-docker/pull/41)/contêineres baseados em [ASP.net](https://github.com/Microsoft/aspnet-docker), a versão atual do [Monitor. exe](https://github.com/Microsoft/iis-docker/pull/41) trata isso somente no *DefaultAppPool* .</span><span class="sxs-lookup"><span data-stu-id="f6d15-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="f6d15-222">Outras variantes de contêiner com base no Windows talvez precisem desenvolver seu próprio mecanismo de injeção para processos não EntryPoint.</span><span class="sxs-lookup"><span data-stu-id="f6d15-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="f6d15-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="f6d15-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="f6d15-224">Nunca armazene senhas, cadeias de conexão confidenciais ou outros dados confidenciais no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="f6d15-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="f6d15-225">Os segredos de produção não devem ser usados para desenvolvimento ou teste.</span><span class="sxs-lookup"><span data-stu-id="f6d15-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="f6d15-226">Este construtor de configuração fornece um recurso semelhante a [ASP.NET Core o Gerenciador de segredo](/aspnet/core/security/app-secrets).</span><span class="sxs-lookup"><span data-stu-id="f6d15-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="f6d15-227">O [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) pode ser usado em projetos .NET Framework, mas um arquivo de segredos deve ser especificado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="f6d15-228">Como alternativa, você pode definir a propriedade `UserSecretsId` no arquivo de projeto e criar o arquivo de segredos brutos no local correto para leitura.</span><span class="sxs-lookup"><span data-stu-id="f6d15-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="f6d15-229">Para manter as dependências externas do seu projeto, o arquivo secreto é XML formatado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="f6d15-230">A formatação XML é um detalhe de implementação e o formato não deve ser confiado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="f6d15-231">Se você precisar compartilhar um arquivo *segredos. JSON* com projetos do .NET Core, considere o uso de [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span><span class="sxs-lookup"><span data-stu-id="f6d15-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="f6d15-232">O formato de `SimpleJsonConfigBuilder` para o .NET Core também deve ser considerado um detalhe de implementação sujeito a alterações.</span><span class="sxs-lookup"><span data-stu-id="f6d15-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="f6d15-233">Atributos de configuração para `UserSecretsConfigBuilder`:</span><span class="sxs-lookup"><span data-stu-id="f6d15-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="f6d15-234">`userSecretsId`-esse é o método preferencial para identificar um arquivo de segredos XML.</span><span class="sxs-lookup"><span data-stu-id="f6d15-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="f6d15-235">Ele funciona semelhante ao .NET Core, que usa uma propriedade de projeto `UserSecretsId` para armazenar esse identificador.</span><span class="sxs-lookup"><span data-stu-id="f6d15-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="f6d15-236">A cadeia de caracteres deve ser exclusiva, não precisa ser uma GUID.</span><span class="sxs-lookup"><span data-stu-id="f6d15-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="f6d15-237">Com esse atributo, a `UserSecretsConfigBuilder` examinar um local local conhecido (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) para um arquivo de segredos que pertence a esse identificador.</span><span class="sxs-lookup"><span data-stu-id="f6d15-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="f6d15-238">`userSecretsFile`-um atributo opcional especificando o arquivo que contém os segredos.</span><span class="sxs-lookup"><span data-stu-id="f6d15-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="f6d15-239">O caractere `~` pode ser usado no início para fazer referência à raiz do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6d15-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="f6d15-240">Esse atributo ou o atributo `userSecretsId` é necessário.</span><span class="sxs-lookup"><span data-stu-id="f6d15-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="f6d15-241">Se ambos forem especificados, `userSecretsFile` terá precedência.</span><span class="sxs-lookup"><span data-stu-id="f6d15-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="f6d15-242">`optional`: booliano, valor padrão `true`-impede uma exceção se o arquivo de segredos não puder ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="f6d15-243">O valor do atributo `name` é arbitrário.</span><span class="sxs-lookup"><span data-stu-id="f6d15-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="f6d15-244">O arquivo de segredos tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f6d15-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="f6d15-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="f6d15-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="f6d15-246">O [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) lê os valores armazenados no [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="f6d15-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="f6d15-247">`vaultName` é necessário (o nome do cofre ou um URI para o cofre).</span><span class="sxs-lookup"><span data-stu-id="f6d15-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="f6d15-248">Os outros atributos permitem o controle sobre a qual cofre se conectar, mas são necessários apenas se o aplicativo não estiver em execução em um ambiente que funcione com `Microsoft.Azure.Services.AppAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="f6d15-249">A biblioteca de autenticação dos serviços do Azure é usada para escolher automaticamente as informações de conexão do ambiente de execução, se possível.</span><span class="sxs-lookup"><span data-stu-id="f6d15-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="f6d15-250">Você pode substituir a seleção automática de informações de conexão fornecendo uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="f6d15-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="f6d15-251">`vaultName`-necessário se `uri` não for fornecido.</span><span class="sxs-lookup"><span data-stu-id="f6d15-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="f6d15-252">Especifica o nome do cofre em sua assinatura do Azure a partir da qual os pares de chave/valor são lidos.</span><span class="sxs-lookup"><span data-stu-id="f6d15-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="f6d15-253">`connectionString`-uma cadeia de conexão utilizável por [o azureservicetokenprovider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span><span class="sxs-lookup"><span data-stu-id="f6d15-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="f6d15-254">`uri`-conecta-se a outros provedores de Key Vault com o valor de `uri` especificado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="f6d15-255">Se não for especificado, o Azure (`vaultName`) será o provedor de cofre.</span><span class="sxs-lookup"><span data-stu-id="f6d15-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="f6d15-256">`version`-Azure Key Vault fornece um recurso de controle de versão para segredos.</span><span class="sxs-lookup"><span data-stu-id="f6d15-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="f6d15-257">Se `version` for especificado, o Construtor recuperará somente os segredos correspondentes a esta versão.</span><span class="sxs-lookup"><span data-stu-id="f6d15-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="f6d15-258">`preloadSecretNames`-por padrão, esse construtor consulta **todos os** nomes de chave no cofre de chaves quando ele é inicializado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="f6d15-259">Para evitar a leitura de todos os valores de chave, defina esse atributo como `false`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="f6d15-260">Definir isso como `false` lê segredos um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="f6d15-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="f6d15-261">A leitura de segredos um de cada vez pode ser útil se o cofre permitir acesso "Get", mas não "lista".</span><span class="sxs-lookup"><span data-stu-id="f6d15-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="f6d15-262">**Observação:** Ao usar o modo de `Greedy`, `preloadSecretNames` deve ser `true` (o padrão.)</span><span class="sxs-lookup"><span data-stu-id="f6d15-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="f6d15-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="f6d15-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="f6d15-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) é um construtor de configuração básico que usa os arquivos de um diretório como uma fonte de valores.</span><span class="sxs-lookup"><span data-stu-id="f6d15-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="f6d15-265">O nome de um arquivo é a chave e o conteúdo é o valor.</span><span class="sxs-lookup"><span data-stu-id="f6d15-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="f6d15-266">Esse construtor de configuração pode ser útil ao ser executado em um ambiente de contêiner orquestrado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="f6d15-267">Sistemas como Docker Swarm e kubernetes fornecem `secrets` aos contêineres do Windows orquestrados nessa maneira de chave por arquivo.</span><span class="sxs-lookup"><span data-stu-id="f6d15-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="f6d15-268">Detalhes do atributo:</span><span class="sxs-lookup"><span data-stu-id="f6d15-268">Attribute details:</span></span>

* <span data-ttu-id="f6d15-269">`directoryPath`-obrigatório.</span><span class="sxs-lookup"><span data-stu-id="f6d15-269">`directoryPath` - Required.</span></span> <span data-ttu-id="f6d15-270">Especifica um caminho para procurar valores.</span><span class="sxs-lookup"><span data-stu-id="f6d15-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="f6d15-271">Os segredos de Docker for Windows são armazenados no diretório *C:\ProgramData\Docker\secrets* por padrão.</span><span class="sxs-lookup"><span data-stu-id="f6d15-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="f6d15-272">`ignorePrefix`-os arquivos que começam com esse prefixo são excluídos.</span><span class="sxs-lookup"><span data-stu-id="f6d15-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="f6d15-273">O padrão é "ignorar".</span><span class="sxs-lookup"><span data-stu-id="f6d15-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="f6d15-274">`keyDelimiter`-o valor padrão é `null`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="f6d15-275">Se especificado, o construtor de configuração atravessa vários níveis do diretório, criando nomes de chave com esse delimitador.</span><span class="sxs-lookup"><span data-stu-id="f6d15-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="f6d15-276">Se esse valor for `null`, o construtor de configuração apenas examinará o nível superior do diretório.</span><span class="sxs-lookup"><span data-stu-id="f6d15-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="f6d15-277">`optional`-o valor padrão é `false`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="f6d15-278">Especifica se o construtor de configuração deve causar erros se o diretório de origem não existir.</span><span class="sxs-lookup"><span data-stu-id="f6d15-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="f6d15-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="f6d15-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="f6d15-280">Nunca armazene senhas, cadeias de conexão confidenciais ou outros dados confidenciais no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="f6d15-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="f6d15-281">Os segredos de produção não devem ser usados para desenvolvimento ou teste.</span><span class="sxs-lookup"><span data-stu-id="f6d15-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="f6d15-282">Os projetos do .NET Core frequentemente usam arquivos JSON para configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d15-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="f6d15-283">O [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) Builder permite que os arquivos JSON do .NET Core sejam usados no .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f6d15-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="f6d15-284">Esse construtor de configuração fornece um mapeamento básico de uma fonte de chave/valor simples em áreas de chave/valor específicas da configuração de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f6d15-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="f6d15-285">Este construtor de configuração **não fornece configurações** hierárquicas.</span><span class="sxs-lookup"><span data-stu-id="f6d15-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="f6d15-286">O arquivo de backup JSON é semelhante a um dicionário, e não a um objeto hierárquico complexo.</span><span class="sxs-lookup"><span data-stu-id="f6d15-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="f6d15-287">Um arquivo hierárquico de vários níveis pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="f6d15-288">Esse provedor `flatten`a profundidade acrescentando o nome da propriedade em cada nível usando `:` como um delimitador.</span><span class="sxs-lookup"><span data-stu-id="f6d15-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="f6d15-289">Detalhes do atributo:</span><span class="sxs-lookup"><span data-stu-id="f6d15-289">Attribute details:</span></span>

* <span data-ttu-id="f6d15-290">`jsonFile`-obrigatório.</span><span class="sxs-lookup"><span data-stu-id="f6d15-290">`jsonFile` - Required.</span></span> <span data-ttu-id="f6d15-291">Especifica o arquivo JSON do qual ler.</span><span class="sxs-lookup"><span data-stu-id="f6d15-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="f6d15-292">O caractere de `~` pode ser usado no início para fazer referência à raiz do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6d15-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="f6d15-293">`optional`-booliano, o valor padrão é `true`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="f6d15-294">Impede o lançamento de exceções se o arquivo JSON não puder ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="f6d15-295">`jsonMode` - `[Flat|Sectional]`.</span><span class="sxs-lookup"><span data-stu-id="f6d15-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="f6d15-296">`Flat` é o padrão.</span><span class="sxs-lookup"><span data-stu-id="f6d15-296">`Flat` is the default.</span></span> <span data-ttu-id="f6d15-297">Quando `jsonMode` é `Flat`, o arquivo JSON é uma única origem de chave/valor simples.</span><span class="sxs-lookup"><span data-stu-id="f6d15-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="f6d15-298">As `EnvironmentConfigBuilder` e `AzureKeyVaultConfigBuilder` também são fontes simples de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="f6d15-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="f6d15-299">Quando a `SimpleJsonConfigBuilder` é configurada no modo de `Sectional`:</span><span class="sxs-lookup"><span data-stu-id="f6d15-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="f6d15-300">O arquivo JSON é dividido conceitualmente apenas no nível superior em vários dicionários.</span><span class="sxs-lookup"><span data-stu-id="f6d15-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="f6d15-301">Cada um dos dicionários só é aplicado à seção de configuração que corresponde ao nome de propriedade de nível superior anexado a eles.</span><span class="sxs-lookup"><span data-stu-id="f6d15-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="f6d15-302">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6d15-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="f6d15-303">Implementando um construtor de configuração de chave/valor personalizado</span><span class="sxs-lookup"><span data-stu-id="f6d15-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="f6d15-304">Se os construtores de configuração não atenderem às suas necessidades, você poderá escrever um personalizado.</span><span class="sxs-lookup"><span data-stu-id="f6d15-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="f6d15-305">A classe base `KeyValueConfigBuilder` lida com os modos de substituição e a maioria das preocupações com o prefixo.</span><span class="sxs-lookup"><span data-stu-id="f6d15-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="f6d15-306">Um projeto de implementação precisa apenas de:</span><span class="sxs-lookup"><span data-stu-id="f6d15-306">An implementing project need only:</span></span>

* <span data-ttu-id="f6d15-307">Herdar da classe base e implementar uma fonte básica de pares de chave/valor por meio do `GetValue` e `GetAllValues`:</span><span class="sxs-lookup"><span data-stu-id="f6d15-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="f6d15-308">Adicione o [Microsoft. Configuration. ConfigurationBuilders. base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) ao projeto.</span><span class="sxs-lookup"><span data-stu-id="f6d15-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="f6d15-309">A classe base `KeyValueConfigBuilder` fornece grande parte do comportamento de trabalho e consistente entre os construtores de configuração de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="f6d15-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6d15-310">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f6d15-310">Additional resources</span></span>

* [<span data-ttu-id="f6d15-311">Repositório GitHub de construtores de configuração</span><span class="sxs-lookup"><span data-stu-id="f6d15-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="f6d15-312">Autenticação serviço a serviço para Azure Key Vault usando o .NET</span><span class="sxs-lookup"><span data-stu-id="f6d15-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
