---
title: riferimento a un File NuGet. config
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911088"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="1f9c7-103">riferimento di NuGet. config</span><span class="sxs-lookup"><span data-stu-id="1f9c7-103">nuget.config reference</span></span>

<span data-ttu-id="1f9c7-104">Il comportamento di NuGet è controllato da impostazioni in diversi file `NuGet.Config`, come descritto in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="1f9c7-105">`nuget.config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="1f9c7-106">Ogni sezione contiene zero o più elementi.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-106">Each section contains zero or more items.</span></span> <span data-ttu-id="1f9c7-107">Vedere il [file di configurazione di esempio](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="1f9c7-108">Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="1f9c7-109">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="1f9c7-109">In this topic:</span></span>

- [<span data-ttu-id="1f9c7-110">Sezione config</span><span class="sxs-lookup"><span data-stu-id="1f9c7-110">config section</span></span>](#config-section)
- [<span data-ttu-id="1f9c7-111">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="1f9c7-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="1f9c7-112">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="1f9c7-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="1f9c7-113">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="1f9c7-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="1f9c7-114">[Sezioni per le origini dei pacchetti](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="1f9c7-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="1f9c7-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="1f9c7-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="1f9c7-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="1f9c7-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="1f9c7-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="1f9c7-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="1f9c7-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="1f9c7-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="1f9c7-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="1f9c7-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="1f9c7-120">sezione trustedSigners</span><span class="sxs-lookup"><span data-stu-id="1f9c7-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="1f9c7-121">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="1f9c7-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="1f9c7-122">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="1f9c7-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="1f9c7-123">Sezione config</span><span class="sxs-lookup"><span data-stu-id="1f9c7-123">config section</span></span>

<span data-ttu-id="1f9c7-124">Contiene varie impostazioni di configurazione, che possono essere impostate con il [comando `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="1f9c7-125">`dependencyVersion` e `repositoryPath` si applicano solo ai progetti che usano `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="1f9c7-126">`globalPackagesFolder` si applica solo ai progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="1f9c7-127">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-127">Key</span></span> | <span data-ttu-id="1f9c7-128">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-129">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="1f9c7-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="1f9c7-130">Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="1f9c7-131">Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="1f9c7-132">I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="1f9c7-133">globalPackagesFolder (progetti usando solo PackageReference)</span><span class="sxs-lookup"><span data-stu-id="1f9c7-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="1f9c7-134">Percorso della cartella dei pacchetti globale predefinita.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-134">The location of the default global packages folder.</span></span> <span data-ttu-id="1f9c7-135">L'impostazione predefinita è `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="1f9c7-136">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="1f9c7-137">Questa impostazione viene sostituita dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="1f9c7-138">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="1f9c7-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="1f9c7-139">Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="1f9c7-140">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="1f9c7-141">Questa impostazione viene sostituita dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="1f9c7-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="1f9c7-142">defaultPushSource</span></span> | <span data-ttu-id="1f9c7-143">Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="1f9c7-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="1f9c7-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="1f9c7-145">Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="1f9c7-146">Le password vengono crittografate e non possono essere aggiunte manualmente.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="1f9c7-147">Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="1f9c7-148">In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="1f9c7-149">Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="1f9c7-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="1f9c7-150">signatureValidationMode</span></span> | <span data-ttu-id="1f9c7-151">Specifica la modalità di convalida utilizzata per verificare le firme dei pacchetti di installazione del pacchetto e il ripristino.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="1f9c7-152">I valori sono `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="1f9c7-153">Il valore predefinito è `accept`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-153">Defaults to `accept`.</span></span>

<span data-ttu-id="1f9c7-154">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="1f9c7-155">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="1f9c7-155">bindingRedirects section</span></span>

<span data-ttu-id="1f9c7-156">Specifica se NuGet esegue o meno i reindirizzamenti di binding automatici quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="1f9c7-157">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-157">Key</span></span> | <span data-ttu-id="1f9c7-158">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-159">skip</span><span class="sxs-lookup"><span data-stu-id="1f9c7-159">skip</span></span> | <span data-ttu-id="1f9c7-160">Valore booleano che indica se ignorare i reindirizzamenti di binding automatici.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="1f9c7-161">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-161">The default is false.</span></span> |

<span data-ttu-id="1f9c7-162">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="1f9c7-163">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="1f9c7-163">packageRestore section</span></span>

<span data-ttu-id="1f9c7-164">Controlla il ripristino dei pacchetti durante le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="1f9c7-165">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-165">Key</span></span> | <span data-ttu-id="1f9c7-166">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-167">enabled</span><span class="sxs-lookup"><span data-stu-id="1f9c7-167">enabled</span></span> | <span data-ttu-id="1f9c7-168">Valore booleano che indica se NuGet può eseguire il ripristino automatico.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="1f9c7-169">È anche possibile impostare la variabile di ambiente `EnableNuGetPackageRestore` con il valore `True` invece di impostare questa chiave nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="1f9c7-170">automatico</span><span class="sxs-lookup"><span data-stu-id="1f9c7-170">automatic</span></span> | <span data-ttu-id="1f9c7-171">Valore booleano che indica se NuGet deve controllare se mancano pacchetti durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="1f9c7-172">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="1f9c7-173">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="1f9c7-173">solution section</span></span>

<span data-ttu-id="1f9c7-174">Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="1f9c7-175">Questa sezione funziona solo nei file `nuget.config` in una cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="1f9c7-176">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-176">Key</span></span> | <span data-ttu-id="1f9c7-177">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="1f9c7-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="1f9c7-179">Valore booleano che indica se ignorare la cartella dei pacchetti quando si utilizza il controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="1f9c7-180">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-180">The default value is false.</span></span> |

<span data-ttu-id="1f9c7-181">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="1f9c7-182">Sezioni per le origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="1f9c7-182">Package source sections</span></span>

<span data-ttu-id="1f9c7-183">Il `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` e `trustedSigners` tutto il lavoro in modo da configurare come NuGet funziona con i repository dei pacchetti durante l'installazione, ripristino e le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="1f9c7-184">Il [ `nuget sources` comandi](../tools/cli-ref-sources.md) viene generalmente usato per gestire queste impostazioni, ad eccezione dei `apikeys` che viene gestita con il [ `nuget setapikey` comando](../tools/cli-ref-setapikey.md), e `trustedSigners` che è gestito usando il [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="1f9c7-185">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="1f9c7-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="1f9c7-186">packageSources</span></span>

<span data-ttu-id="1f9c7-187">Elenca tutte le origini di pacchetti note.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-187">Lists all known package sources.</span></span> <span data-ttu-id="1f9c7-188">L'ordine viene ignorato durante le operazioni di ripristino e con qualsiasi progetto usando il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="1f9c7-189">NuGet rispetta l'ordine delle origini per l'installazione e operazioni di aggiornamento con i progetti che usano `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="1f9c7-190">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-190">Key</span></span> | <span data-ttu-id="1f9c7-191">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-192">(nome da assegnare all'origine di pacchetti)</span><span class="sxs-lookup"><span data-stu-id="1f9c7-192">(name to assign to the package source)</span></span> | <span data-ttu-id="1f9c7-193">Percorso o URL dell'origine di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="1f9c7-194">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="1f9c7-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="1f9c7-195">packageSourceCredentials</span></span>

<span data-ttu-id="1f9c7-196">Archivia i nomi utente e le password per le origini, in genere specificati con le opzioni `-username` e `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="1f9c7-197">Le password vengono crittografate per impostazione predefinita, a meno che non venga usata anche l'opzione `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="1f9c7-198">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-198">Key</span></span> | <span data-ttu-id="1f9c7-199">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-200">nomeutente</span><span class="sxs-lookup"><span data-stu-id="1f9c7-200">username</span></span> | <span data-ttu-id="1f9c7-201">Nome utente per l'origine in testo normale.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="1f9c7-202">password</span><span class="sxs-lookup"><span data-stu-id="1f9c7-202">password</span></span> | <span data-ttu-id="1f9c7-203">Password crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="1f9c7-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="1f9c7-204">cleartextpassword</span></span> | <span data-ttu-id="1f9c7-205">Password non crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="1f9c7-206">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="1f9c7-206">**Example:**</span></span>

<span data-ttu-id="1f9c7-207">Nel file di configurazione, l'elemento `<packageSourceCredentials>` contiene i nodi figlio per ogni nome di origine applicabile (gli spazi nel nome vengono sostituiti con `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="1f9c7-208">Per le origini denominate "Contoso" e "Test Source", il file di configurazione contiene quanto segue quando si usano password crittografate:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="1f9c7-209">Quando si usano password non crittografate:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-209">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="1f9c7-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="1f9c7-210">apikeys</span></span>

<span data-ttu-id="1f9c7-211">Archivia le chiavi per le origini che usano l'autenticazione con chiave API, in base alle impostazioni specificate con il [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="1f9c7-212">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-212">Key</span></span> | <span data-ttu-id="1f9c7-213">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-214">(URL di origine)</span><span class="sxs-lookup"><span data-stu-id="1f9c7-214">(source URL)</span></span> | <span data-ttu-id="1f9c7-215">Chiave API crittografata.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-215">The encrypted API key.</span></span> |

<span data-ttu-id="1f9c7-216">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="1f9c7-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="1f9c7-217">disabledPackageSources</span></span>

<span data-ttu-id="1f9c7-218">Identifica le origini attualmente disabilitate.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-218">Identified currently disabled sources.</span></span> <span data-ttu-id="1f9c7-219">Può essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-219">May be empty.</span></span>

| <span data-ttu-id="1f9c7-220">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-220">Key</span></span> | <span data-ttu-id="1f9c7-221">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-222">(nome dell'origine)</span><span class="sxs-lookup"><span data-stu-id="1f9c7-222">(name of source)</span></span> | <span data-ttu-id="1f9c7-223">Valore booleano che indica se l'origine è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="1f9c7-224">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="1f9c7-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="1f9c7-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="1f9c7-225">activePackageSource</span></span>

<span data-ttu-id="1f9c7-226">*(Solo versione 2.x; deprecata nella versione 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="1f9c7-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="1f9c7-227">Identifica l'origine attualmente attiva o indica l'aggregazione di tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="1f9c7-228">Chiave</span><span class="sxs-lookup"><span data-stu-id="1f9c7-228">Key</span></span> | <span data-ttu-id="1f9c7-229">Value</span><span class="sxs-lookup"><span data-stu-id="1f9c7-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1f9c7-230">(nome dell'origine) o `All`</span><span class="sxs-lookup"><span data-stu-id="1f9c7-230">(name of source) or `All`</span></span> | <span data-ttu-id="1f9c7-231">Se la chiave è il nome di un'origine, il valore è il percorso o l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="1f9c7-232">Se `All`, il valore deve essere `(Aggregate source)` per combinare tutte le origini di pacchetti non disabilitate in altro modo.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="1f9c7-233">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="1f9c7-234">sezione trustedSigners</span><span class="sxs-lookup"><span data-stu-id="1f9c7-234">trustedSigners section</span></span>

<span data-ttu-id="1f9c7-235">Gli archivi attendibili i firmatari utilizzati per consentire di pacchetto durante l'installazione o il ripristino.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="1f9c7-236">Questo elenco non può essere vuoto quando l'utente imposta `signatureValidationMode` a `require`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="1f9c7-237">In questa sezione può essere aggiornata con le [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="1f9c7-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="1f9c7-238">**Schema**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-238">**Schema**:</span></span>

<span data-ttu-id="1f9c7-239">Un'entità attendibile è una raccolta di `certificate` gli elementi che integra tutti i certificati che identificano un firmatario specificato.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="1f9c7-240">Un'entità attendibile può essere un' `Author` o un `Repository`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="1f9c7-241">Attendibile *repository* specifica inoltre il `serviceIndex` per il repository (che deve essere un valore valido `https` uri) e può facoltativamente specificare un elenco delimitato da punti e virgola di `owners` per limitare ulteriormente chi è attendibile da quel repository specifico.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="1f9c7-242">Gli algoritmi hash supportati utilizzati per un'impronta digitale certificato vengono `SHA256`, `SHA384` e `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="1f9c7-243">Se un `certificate` specifica `allowUntrustedRoot` come `true` il certificato specificato è consentito concatenarsi a una radice non attendibile durante la compilazione della catena di certificati come parte della verifica della firma.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="1f9c7-244">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="1f9c7-245">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="1f9c7-245">Using environment variables</span></span>

<span data-ttu-id="1f9c7-246">È possibile usare variabili di ambiente nei valori `nuget.config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="1f9c7-247">Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="1f9c7-248">In modo analogo, se la variabile `HOME` in Mac/Linux è impostata su `/home/myStuff`, `%HOME%/NuGetRepository` nel file di configurazione viene risolto in `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="1f9c7-249">Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1f9c7-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="1f9c7-250">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="1f9c7-250">Example config file</span></span>

<span data-ttu-id="1f9c7-251">Di seguito è riportato un file `nuget.config` di esempio che illustra una serie di impostazioni:</span><span class="sxs-lookup"><span data-stu-id="1f9c7-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
