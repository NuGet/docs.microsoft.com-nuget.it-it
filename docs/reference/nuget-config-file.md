---
title: informazioni di riferimento sul file NuGet. config
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: b03bb8da0191a679671e5898ac70fff2024d52f2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317215"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="ba61d-103">informazioni di riferimento su NuGet. config</span><span class="sxs-lookup"><span data-stu-id="ba61d-103">nuget.config reference</span></span>

<span data-ttu-id="ba61d-104">Il comportamento di NuGet è controllato da impostazioni `NuGet.Config` in file diversi, come descritto in [configurazioni comuni di NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ba61d-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="ba61d-105">`nuget.config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="ba61d-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="ba61d-106">Ogni sezione contiene zero o più elementi.</span><span class="sxs-lookup"><span data-stu-id="ba61d-106">Each section contains zero or more items.</span></span> <span data-ttu-id="ba61d-107">Vedere il [file di configurazione di esempio](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="ba61d-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="ba61d-108">Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="ba61d-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="ba61d-109">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="ba61d-109">In this topic:</span></span>

- [<span data-ttu-id="ba61d-110">Sezione config</span><span class="sxs-lookup"><span data-stu-id="ba61d-110">config section</span></span>](#config-section)
- [<span data-ttu-id="ba61d-111">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="ba61d-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="ba61d-112">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="ba61d-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="ba61d-113">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="ba61d-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="ba61d-114">[Sezioni per le origini dei pacchetti](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="ba61d-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="ba61d-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="ba61d-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="ba61d-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="ba61d-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="ba61d-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="ba61d-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="ba61d-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="ba61d-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="ba61d-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="ba61d-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="ba61d-120">sezione trustedSigners</span><span class="sxs-lookup"><span data-stu-id="ba61d-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="ba61d-121">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="ba61d-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="ba61d-122">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="ba61d-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="ba61d-123">Sezione config</span><span class="sxs-lookup"><span data-stu-id="ba61d-123">config section</span></span>

<span data-ttu-id="ba61d-124">Contiene varie impostazioni di configurazione, che possono essere impostate con il [comando `nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="ba61d-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="ba61d-125">`dependencyVersion`e `repositoryPath` si applicano solo ai `packages.config`progetti che usano.</span><span class="sxs-lookup"><span data-stu-id="ba61d-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="ba61d-126">`globalPackagesFolder`si applica solo ai progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ba61d-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="ba61d-127">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-127">Key</span></span> | <span data-ttu-id="ba61d-128">Valore</span><span class="sxs-lookup"><span data-stu-id="ba61d-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-129">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="ba61d-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="ba61d-130">Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="ba61d-131">Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="ba61d-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="ba61d-132">I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="ba61d-133">globalPackagesFolder (progetti che usano solo PackageReference)</span><span class="sxs-lookup"><span data-stu-id="ba61d-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="ba61d-134">Percorso della cartella dei pacchetti globale predefinita.</span><span class="sxs-lookup"><span data-stu-id="ba61d-134">The location of the default global packages folder.</span></span> <span data-ttu-id="ba61d-135">L'impostazione predefinita è `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ba61d-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="ba61d-136">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="ba61d-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="ba61d-137">Questa impostazione viene sottoposta a override dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="ba61d-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="ba61d-138">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="ba61d-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="ba61d-139">Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita.</span><span class="sxs-lookup"><span data-stu-id="ba61d-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="ba61d-140">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="ba61d-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="ba61d-141">Questa impostazione viene sottoposta a override dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="ba61d-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="ba61d-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="ba61d-142">defaultPushSource</span></span> | <span data-ttu-id="ba61d-143">Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione.</span><span class="sxs-lookup"><span data-stu-id="ba61d-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="ba61d-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="ba61d-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="ba61d-145">Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="ba61d-146">Le password vengono crittografate e non possono essere aggiunte manualmente.</span><span class="sxs-lookup"><span data-stu-id="ba61d-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="ba61d-147">Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy.</span><span class="sxs-lookup"><span data-stu-id="ba61d-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="ba61d-148">In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori.</span><span class="sxs-lookup"><span data-stu-id="ba61d-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="ba61d-149">Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="ba61d-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="ba61d-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="ba61d-150">signatureValidationMode</span></span> | <span data-ttu-id="ba61d-151">Specifica la modalità di convalida utilizzata per verificare le firme dei pacchetti per l'installazione e il ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ba61d-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="ba61d-152">I valori `accept`sono `require`,.</span><span class="sxs-lookup"><span data-stu-id="ba61d-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="ba61d-153">Il valore predefinito è `accept`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-153">Defaults to `accept`.</span></span>

<span data-ttu-id="ba61d-154">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="ba61d-155">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="ba61d-155">bindingRedirects section</span></span>

<span data-ttu-id="ba61d-156">Specifica se NuGet esegue o meno i reindirizzamenti di binding automatici quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ba61d-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="ba61d-157">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-157">Key</span></span> | <span data-ttu-id="ba61d-158">Valore</span><span class="sxs-lookup"><span data-stu-id="ba61d-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-159">skip</span><span class="sxs-lookup"><span data-stu-id="ba61d-159">skip</span></span> | <span data-ttu-id="ba61d-160">Valore booleano che indica se ignorare i reindirizzamenti di binding automatici.</span><span class="sxs-lookup"><span data-stu-id="ba61d-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="ba61d-161">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="ba61d-161">The default is false.</span></span> |

<span data-ttu-id="ba61d-162">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="ba61d-163">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="ba61d-163">packageRestore section</span></span>

<span data-ttu-id="ba61d-164">Controlla il ripristino dei pacchetti durante le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="ba61d-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="ba61d-165">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-165">Key</span></span> | <span data-ttu-id="ba61d-166">Value</span><span class="sxs-lookup"><span data-stu-id="ba61d-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-167">enabled</span><span class="sxs-lookup"><span data-stu-id="ba61d-167">enabled</span></span> | <span data-ttu-id="ba61d-168">Valore booleano che indica se NuGet può eseguire il ripristino automatico.</span><span class="sxs-lookup"><span data-stu-id="ba61d-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="ba61d-169">È anche possibile impostare la variabile di ambiente `EnableNuGetPackageRestore` con il valore `True` invece di impostare questa chiave nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ba61d-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="ba61d-170">automatico</span><span class="sxs-lookup"><span data-stu-id="ba61d-170">automatic</span></span> | <span data-ttu-id="ba61d-171">Valore booleano che indica se NuGet deve controllare se mancano pacchetti durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="ba61d-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="ba61d-172">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="ba61d-173">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="ba61d-173">solution section</span></span>

<span data-ttu-id="ba61d-174">Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="ba61d-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="ba61d-175">Questa sezione funziona solo nei file `nuget.config` in una cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="ba61d-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="ba61d-176">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-176">Key</span></span> | <span data-ttu-id="ba61d-177">Value</span><span class="sxs-lookup"><span data-stu-id="ba61d-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="ba61d-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="ba61d-179">Valore booleano che indica se ignorare la cartella dei pacchetti quando si utilizza il controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="ba61d-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="ba61d-180">Il valore predefinito è False.</span><span class="sxs-lookup"><span data-stu-id="ba61d-180">The default value is false.</span></span> |

<span data-ttu-id="ba61d-181">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="ba61d-182">Sezioni per le origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="ba61d-182">Package source sections</span></span>

<span data-ttu-id="ba61d-183">`packageSources` ,`packageSourceCredentials`, ,`trustedSigners` E interagiscono tra loro per configurare il funzionamento di NuGet con i repository dei pacchetti durante le operazioni di installazione, ripristino e aggiornamento. `activePackageSource` `apikeys` `disabledPackageSources`</span><span class="sxs-lookup"><span data-stu-id="ba61d-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="ba61d-184">Il `apikeys` `trustedSigners` [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) viene in genere usato per gestire queste impostazioni, ad eccezione di che viene gestito usando il [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md)e che viene gestito tramite il [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="ba61d-184">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="ba61d-185">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="ba61d-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="ba61d-186">packageSources</span></span>

<span data-ttu-id="ba61d-187">Elenca tutte le origini di pacchetti note.</span><span class="sxs-lookup"><span data-stu-id="ba61d-187">Lists all known package sources.</span></span> <span data-ttu-id="ba61d-188">L'ordine viene ignorato durante le operazioni di ripristino e con qualsiasi progetto che usa il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ba61d-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="ba61d-189">NuGet rispetta l'ordine delle origini per le operazioni di installazione e aggiornamento con `packages.config`i progetti che usano.</span><span class="sxs-lookup"><span data-stu-id="ba61d-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="ba61d-190">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-190">Key</span></span> | <span data-ttu-id="ba61d-191">Valore</span><span class="sxs-lookup"><span data-stu-id="ba61d-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-192">(nome da assegnare all'origine di pacchetti)</span><span class="sxs-lookup"><span data-stu-id="ba61d-192">(name to assign to the package source)</span></span> | <span data-ttu-id="ba61d-193">Percorso o URL dell'origine di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ba61d-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="ba61d-194">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="ba61d-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="ba61d-195">packageSourceCredentials</span></span>

<span data-ttu-id="ba61d-196">Archivia i nomi utente e le password per le origini, in genere specificati con le opzioni `-username` e `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="ba61d-197">Le password vengono crittografate per impostazione predefinita, a meno che non venga usata anche l'opzione `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="ba61d-198">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-198">Key</span></span> | <span data-ttu-id="ba61d-199">Value</span><span class="sxs-lookup"><span data-stu-id="ba61d-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-200">userName</span><span class="sxs-lookup"><span data-stu-id="ba61d-200">username</span></span> | <span data-ttu-id="ba61d-201">Nome utente per l'origine in testo normale.</span><span class="sxs-lookup"><span data-stu-id="ba61d-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="ba61d-202">password</span><span class="sxs-lookup"><span data-stu-id="ba61d-202">password</span></span> | <span data-ttu-id="ba61d-203">Password crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="ba61d-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="ba61d-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="ba61d-204">cleartextpassword</span></span> | <span data-ttu-id="ba61d-205">Password non crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="ba61d-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="ba61d-206">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="ba61d-206">**Example:**</span></span>

<span data-ttu-id="ba61d-207">Nel file di configurazione, l'elemento `<packageSourceCredentials>` contiene i nodi figlio per ogni nome di origine applicabile (gli spazi nel nome vengono sostituiti con `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="ba61d-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="ba61d-208">Per le origini denominate "Contoso" e "Test Source", il file di configurazione contiene quanto segue quando si usano password crittografate:</span><span class="sxs-lookup"><span data-stu-id="ba61d-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="ba61d-209">Quando si usano password non crittografate:</span><span class="sxs-lookup"><span data-stu-id="ba61d-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="ba61d-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="ba61d-210">apikeys</span></span>

<span data-ttu-id="ba61d-211">Archivia le chiavi per le origini che usano l'autenticazione con chiave API, in base alle impostazioni specificate con il [comando `nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="ba61d-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="ba61d-212">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-212">Key</span></span> | <span data-ttu-id="ba61d-213">Value</span><span class="sxs-lookup"><span data-stu-id="ba61d-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-214">(URL di origine)</span><span class="sxs-lookup"><span data-stu-id="ba61d-214">(source URL)</span></span> | <span data-ttu-id="ba61d-215">Chiave API crittografata.</span><span class="sxs-lookup"><span data-stu-id="ba61d-215">The encrypted API key.</span></span> |

<span data-ttu-id="ba61d-216">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="ba61d-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="ba61d-217">disabledPackageSources</span></span>

<span data-ttu-id="ba61d-218">Identifica le origini attualmente disabilitate.</span><span class="sxs-lookup"><span data-stu-id="ba61d-218">Identified currently disabled sources.</span></span> <span data-ttu-id="ba61d-219">Può essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="ba61d-219">May be empty.</span></span>

| <span data-ttu-id="ba61d-220">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-220">Key</span></span> | <span data-ttu-id="ba61d-221">Value</span><span class="sxs-lookup"><span data-stu-id="ba61d-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-222">(nome dell'origine)</span><span class="sxs-lookup"><span data-stu-id="ba61d-222">(name of source)</span></span> | <span data-ttu-id="ba61d-223">Valore booleano che indica se l'origine è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="ba61d-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="ba61d-224">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="ba61d-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="ba61d-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="ba61d-225">activePackageSource</span></span>

<span data-ttu-id="ba61d-226">*(Solo versione 2.x; deprecata nella versione 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="ba61d-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="ba61d-227">Identifica l'origine attualmente attiva o indica l'aggregazione di tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="ba61d-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="ba61d-228">Chiave</span><span class="sxs-lookup"><span data-stu-id="ba61d-228">Key</span></span> | <span data-ttu-id="ba61d-229">Value</span><span class="sxs-lookup"><span data-stu-id="ba61d-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ba61d-230">(nome dell'origine) o `All`</span><span class="sxs-lookup"><span data-stu-id="ba61d-230">(name of source) or `All`</span></span> | <span data-ttu-id="ba61d-231">Se la chiave è il nome di un'origine, il valore è il percorso o l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="ba61d-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="ba61d-232">Se `All`, il valore deve essere `(Aggregate source)` per combinare tutte le origini di pacchetti non disabilitate in altro modo.</span><span class="sxs-lookup"><span data-stu-id="ba61d-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="ba61d-233">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="ba61d-234">sezione trustedSigners</span><span class="sxs-lookup"><span data-stu-id="ba61d-234">trustedSigners section</span></span>

<span data-ttu-id="ba61d-235">Archivia i firmatari attendibili utilizzati per consentire il pacchetto durante l'installazione o il ripristino.</span><span class="sxs-lookup"><span data-stu-id="ba61d-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="ba61d-236">Questo elenco non può essere vuoto quando l'utente `signatureValidationMode` imposta `require`su.</span><span class="sxs-lookup"><span data-stu-id="ba61d-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="ba61d-237">Questa sezione può essere aggiornata con il [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="ba61d-237">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="ba61d-238">**Schema**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-238">**Schema**:</span></span>

<span data-ttu-id="ba61d-239">Un firmatario attendibile dispone di una `certificate` raccolta di elementi che integrano tutti i certificati che identificano un determinato firmatario.</span><span class="sxs-lookup"><span data-stu-id="ba61d-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="ba61d-240">Un firmatario attendibile può essere un `Author` o un `Repository`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="ba61d-241">Un *repository* attendibile specifica `serviceIndex` anche per il repository (che deve essere un URI valido `https` ) e può facoltativamente specificare un elenco delimitato da punti e virgola `owners` di per limitare ancora più chi è considerato attendibile da tale specifico repository.</span><span class="sxs-lookup"><span data-stu-id="ba61d-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="ba61d-242">Gli algoritmi hash supportati usati per un'impronta digitale del certificato `SHA256`sono `SHA384` , `SHA512`e.</span><span class="sxs-lookup"><span data-stu-id="ba61d-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="ba61d-243">Se un `certificate` oggetto `allowUntrustedRoot` specifica `true` come il certificato specificato può essere concatenato a una radice non attendibile durante la compilazione della catena di certificati come parte della verifica della firma.</span><span class="sxs-lookup"><span data-stu-id="ba61d-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="ba61d-244">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="ba61d-244">**Example**:</span></span>

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

## <a name="using-environment-variables"></a><span data-ttu-id="ba61d-245">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="ba61d-245">Using environment variables</span></span>

<span data-ttu-id="ba61d-246">È possibile usare variabili di ambiente nei valori `nuget.config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ba61d-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="ba61d-247">Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="ba61d-248">In modo analogo, se la variabile `HOME` in Mac/Linux è impostata su `/home/myStuff`, `%HOME%/NuGetRepository` nel file di configurazione viene risolto in `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="ba61d-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="ba61d-249">Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ba61d-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="ba61d-250">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="ba61d-250">Example config file</span></span>

<span data-ttu-id="ba61d-251">Di seguito è riportato un file `nuget.config` di esempio che illustra una serie di impostazioni:</span><span class="sxs-lookup"><span data-stu-id="ba61d-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
