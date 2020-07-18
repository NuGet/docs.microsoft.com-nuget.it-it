---
title: Riferimento al file di nuget.config
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 760bf09cb03608275e2c5406474f572a407a7379
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451125"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="3ca46-103">Riferimento nuget.config</span><span class="sxs-lookup"><span data-stu-id="3ca46-103">nuget.config reference</span></span>

<span data-ttu-id="3ca46-104">Il comportamento di NuGet è controllato dalle impostazioni in diversi `NuGet.Config` `nuget.config` file o, come descritto in [configurazioni comuni di NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3ca46-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="3ca46-105">`nuget.config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="3ca46-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="3ca46-106">Ogni sezione contiene zero o più elementi.</span><span class="sxs-lookup"><span data-stu-id="3ca46-106">Each section contains zero or more items.</span></span> <span data-ttu-id="3ca46-107">Vedere il [file di configurazione di esempio](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="3ca46-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="3ca46-108">Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="3ca46-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="3ca46-109">Sezione config</span><span class="sxs-lookup"><span data-stu-id="3ca46-109">config section</span></span>

<span data-ttu-id="3ca46-110">Contiene impostazioni di configurazione varie, che possono essere impostate tramite il [ `nuget config` comando](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="3ca46-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="3ca46-111">`dependencyVersion`e `repositoryPath` si applicano solo ai progetti che usano `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="3ca46-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="3ca46-112">`globalPackagesFolder`si applica solo ai progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3ca46-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="3ca46-113">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-113">Key</span></span> | <span data-ttu-id="3ca46-114">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-115">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="3ca46-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="3ca46-116">Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="3ca46-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="3ca46-117">Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ca46-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="3ca46-118">I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="3ca46-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="3ca46-119">globalPackagesFolder (progetti che usano solo PackageReference)</span><span class="sxs-lookup"><span data-stu-id="3ca46-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="3ca46-120">Percorso della cartella dei pacchetti globale predefinita.</span><span class="sxs-lookup"><span data-stu-id="3ca46-120">The location of the default global packages folder.</span></span> <span data-ttu-id="3ca46-121">L'impostazione predefinita è `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="3ca46-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="3ca46-122">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="3ca46-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3ca46-123">Questa impostazione viene sottoposta a override dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="3ca46-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3ca46-124">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="3ca46-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="3ca46-125">Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita.</span><span class="sxs-lookup"><span data-stu-id="3ca46-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="3ca46-126">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="3ca46-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3ca46-127">Questa impostazione viene sottoposta a override dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="3ca46-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3ca46-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="3ca46-128">defaultPushSource</span></span> | <span data-ttu-id="3ca46-129">Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione.</span><span class="sxs-lookup"><span data-stu-id="3ca46-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="3ca46-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="3ca46-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="3ca46-131">Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="3ca46-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="3ca46-132">Le password vengono crittografate e non possono essere aggiunte manualmente.</span><span class="sxs-lookup"><span data-stu-id="3ca46-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="3ca46-133">Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy.</span><span class="sxs-lookup"><span data-stu-id="3ca46-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="3ca46-134">In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori.</span><span class="sxs-lookup"><span data-stu-id="3ca46-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="3ca46-135">Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="3ca46-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="3ca46-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="3ca46-136">signatureValidationMode</span></span> | <span data-ttu-id="3ca46-137">Specifica la modalità di convalida utilizzata per verificare le firme dei pacchetti per l'installazione e il ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="3ca46-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="3ca46-138">I valori sono `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="3ca46-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="3ca46-139">Il valore predefinito è `accept`.</span><span class="sxs-lookup"><span data-stu-id="3ca46-139">Defaults to `accept`.</span></span>

<span data-ttu-id="3ca46-140">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="3ca46-141">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="3ca46-141">bindingRedirects section</span></span>

<span data-ttu-id="3ca46-142">Specifica se NuGet esegue o meno i reindirizzamenti di binding automatici quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="3ca46-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="3ca46-143">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-143">Key</span></span> | <span data-ttu-id="3ca46-144">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-145">skip</span><span class="sxs-lookup"><span data-stu-id="3ca46-145">skip</span></span> | <span data-ttu-id="3ca46-146">Valore booleano che indica se ignorare i reindirizzamenti di binding automatici.</span><span class="sxs-lookup"><span data-stu-id="3ca46-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="3ca46-147">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="3ca46-147">The default is false.</span></span> |

<span data-ttu-id="3ca46-148">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="3ca46-149">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="3ca46-149">packageRestore section</span></span>

<span data-ttu-id="3ca46-150">Controlla il ripristino dei pacchetti durante le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="3ca46-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="3ca46-151">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-151">Key</span></span> | <span data-ttu-id="3ca46-152">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-153">Enabled</span><span class="sxs-lookup"><span data-stu-id="3ca46-153">enabled</span></span> | <span data-ttu-id="3ca46-154">Valore booleano che indica se NuGet può eseguire il ripristino automatico.</span><span class="sxs-lookup"><span data-stu-id="3ca46-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="3ca46-155">È anche possibile impostare la variabile di ambiente `EnableNuGetPackageRestore` con il valore `True` invece di impostare questa chiave nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3ca46-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="3ca46-156">automatic</span><span class="sxs-lookup"><span data-stu-id="3ca46-156">automatic</span></span> | <span data-ttu-id="3ca46-157">Valore booleano che indica se NuGet deve controllare se mancano pacchetti durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="3ca46-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="3ca46-158">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="3ca46-159">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="3ca46-159">solution section</span></span>

<span data-ttu-id="3ca46-160">Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="3ca46-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="3ca46-161">Questa sezione funziona solo nei file `nuget.config` in una cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="3ca46-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="3ca46-162">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-162">Key</span></span> | <span data-ttu-id="3ca46-163">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="3ca46-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="3ca46-165">Valore booleano che indica se ignorare la cartella dei pacchetti quando si utilizza il controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="3ca46-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="3ca46-166">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="3ca46-166">The default value is false.</span></span> |

<span data-ttu-id="3ca46-167">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="3ca46-168">Sezioni per le origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="3ca46-168">Package source sections</span></span>

<span data-ttu-id="3ca46-169">`packageSources`,, `packageSourceCredentials` `apikeys` , `activePackageSource` `disabledPackageSources` E `trustedSigners` interagiscono tra loro per configurare il funzionamento di NuGet con i repository dei pacchetti durante le operazioni di installazione, ripristino e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3ca46-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="3ca46-170">Il [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) viene in genere usato per gestire queste impostazioni, ad eccezione di `apikeys` che viene gestito usando il [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md)e `trustedSigners` che viene gestito tramite il [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="3ca46-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="3ca46-171">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="3ca46-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="3ca46-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="3ca46-172">packageSources</span></span>

<span data-ttu-id="3ca46-173">Elenca tutte le origini di pacchetti note.</span><span class="sxs-lookup"><span data-stu-id="3ca46-173">Lists all known package sources.</span></span> <span data-ttu-id="3ca46-174">L'ordine viene ignorato durante le operazioni di ripristino e con qualsiasi progetto che usa il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3ca46-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="3ca46-175">NuGet rispetta l'ordine delle origini per le operazioni di installazione e aggiornamento con i progetti che usano `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="3ca46-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="3ca46-176">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-176">Key</span></span> | <span data-ttu-id="3ca46-177">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-178">(nome da assegnare all'origine di pacchetti)</span><span class="sxs-lookup"><span data-stu-id="3ca46-178">(name to assign to the package source)</span></span> | <span data-ttu-id="3ca46-179">Percorso o URL dell'origine di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3ca46-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="3ca46-180">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="3ca46-181">Quando `<clear />` è presente per un determinato nodo, NuGet ignora i valori di configurazione definiti in precedenza per tale nodo.</span><span class="sxs-lookup"><span data-stu-id="3ca46-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="3ca46-182">[Altre informazioni sulla modalità di applicazione delle impostazioni](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="3ca46-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="3ca46-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="3ca46-183">packageSourceCredentials</span></span>

<span data-ttu-id="3ca46-184">Archivia i nomi utente e le password per le origini, in genere specificati con le opzioni `-username` e `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="3ca46-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="3ca46-185">Le password vengono crittografate per impostazione predefinita, a meno che non venga usata anche l'opzione `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="3ca46-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="3ca46-186">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-186">Key</span></span> | <span data-ttu-id="3ca46-187">valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-188">username</span><span class="sxs-lookup"><span data-stu-id="3ca46-188">username</span></span> | <span data-ttu-id="3ca46-189">Nome utente per l'origine in testo normale.</span><span class="sxs-lookup"><span data-stu-id="3ca46-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="3ca46-190">password</span><span class="sxs-lookup"><span data-stu-id="3ca46-190">password</span></span> | <span data-ttu-id="3ca46-191">Password crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="3ca46-191">The encrypted password for the source.</span></span> <span data-ttu-id="3ca46-192">Le password crittografate sono supportate solo in Windows e possono essere decrittografate solo quando vengono usate nello stesso computer e tramite lo stesso utente della crittografia originale.</span><span class="sxs-lookup"><span data-stu-id="3ca46-192">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="3ca46-193">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="3ca46-193">cleartextpassword</span></span> | <span data-ttu-id="3ca46-194">Password non crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="3ca46-194">The unencrypted password for the source.</span></span> <span data-ttu-id="3ca46-195">Nota: le variabili di ambiente possono essere usate per una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="3ca46-195">Note: environment variables can be used for improved security.</span></span> |

<span data-ttu-id="3ca46-196">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="3ca46-196">**Example:**</span></span>

<span data-ttu-id="3ca46-197">Nel file di configurazione, l'elemento `<packageSourceCredentials>` contiene i nodi figlio per ogni nome di origine applicabile (gli spazi nel nome vengono sostituiti con `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="3ca46-197">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="3ca46-198">Per le origini denominate "Contoso" e "Test Source", il file di configurazione contiene quanto segue quando si usano password crittografate:</span><span class="sxs-lookup"><span data-stu-id="3ca46-198">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="3ca46-199">Quando si usano password non crittografate archiviate in una variabile di ambiente:</span><span class="sxs-lookup"><span data-stu-id="3ca46-199">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="3ca46-200">Quando si usano password non crittografate:</span><span class="sxs-lookup"><span data-stu-id="3ca46-200">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="3ca46-201">apikeys</span><span class="sxs-lookup"><span data-stu-id="3ca46-201">apikeys</span></span>

<span data-ttu-id="3ca46-202">Archivia le chiavi per le origini che usano l'autenticazione con chiave API, come impostato con il [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="3ca46-202">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="3ca46-203">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-203">Key</span></span> | <span data-ttu-id="3ca46-204">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-204">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-205">(URL di origine)</span><span class="sxs-lookup"><span data-stu-id="3ca46-205">(source URL)</span></span> | <span data-ttu-id="3ca46-206">Chiave API crittografata.</span><span class="sxs-lookup"><span data-stu-id="3ca46-206">The encrypted API key.</span></span> |

<span data-ttu-id="3ca46-207">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-207">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="3ca46-208">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="3ca46-208">disabledPackageSources</span></span>

<span data-ttu-id="3ca46-209">Identifica le origini attualmente disabilitate.</span><span class="sxs-lookup"><span data-stu-id="3ca46-209">Identified currently disabled sources.</span></span> <span data-ttu-id="3ca46-210">Può essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="3ca46-210">May be empty.</span></span>

| <span data-ttu-id="3ca46-211">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-211">Key</span></span> | <span data-ttu-id="3ca46-212">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-212">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-213">(nome dell'origine)</span><span class="sxs-lookup"><span data-stu-id="3ca46-213">(name of source)</span></span> | <span data-ttu-id="3ca46-214">Valore booleano che indica se l'origine è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="3ca46-214">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="3ca46-215">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="3ca46-215">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="3ca46-216">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="3ca46-216">activePackageSource</span></span>

<span data-ttu-id="3ca46-217">*(Solo versione 2.x; deprecata nella versione 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="3ca46-217">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="3ca46-218">Identifica l'origine attualmente attiva o indica l'aggregazione di tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="3ca46-218">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="3ca46-219">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-219">Key</span></span> | <span data-ttu-id="3ca46-220">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-220">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-221">(nome dell'origine) o `All`</span><span class="sxs-lookup"><span data-stu-id="3ca46-221">(name of source) or `All`</span></span> | <span data-ttu-id="3ca46-222">Se la chiave è il nome di un'origine, il valore è il percorso o l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="3ca46-222">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="3ca46-223">Se `All`, il valore deve essere `(Aggregate source)` per combinare tutte le origini di pacchetti non disabilitate in altro modo.</span><span class="sxs-lookup"><span data-stu-id="3ca46-223">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="3ca46-224">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-224">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="3ca46-225">sezione trustedSigners</span><span class="sxs-lookup"><span data-stu-id="3ca46-225">trustedSigners section</span></span>

<span data-ttu-id="3ca46-226">Archivia i firmatari attendibili utilizzati per consentire il pacchetto durante l'installazione o il ripristino.</span><span class="sxs-lookup"><span data-stu-id="3ca46-226">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="3ca46-227">Questo elenco non può essere vuoto quando l'utente imposta `signatureValidationMode` su `require` .</span><span class="sxs-lookup"><span data-stu-id="3ca46-227">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="3ca46-228">Questa sezione può essere aggiornata con il [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="3ca46-228">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="3ca46-229">**Schema**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-229">**Schema**:</span></span>

<span data-ttu-id="3ca46-230">Un firmatario attendibile dispone di una raccolta di `certificate` elementi che integrano tutti i certificati che identificano un determinato firmatario.</span><span class="sxs-lookup"><span data-stu-id="3ca46-230">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="3ca46-231">Un firmatario attendibile può essere un `Author` o un `Repository` .</span><span class="sxs-lookup"><span data-stu-id="3ca46-231">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="3ca46-232">Un *repository* attendibile specifica anche `serviceIndex` per il repository (che deve essere un URI valido `https` ) ed è possibile specificare facoltativamente un elenco delimitato da punti e virgola di `owners` per limitare ulteriormente l'attendibilità di tale repository specifico.</span><span class="sxs-lookup"><span data-stu-id="3ca46-232">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="3ca46-233">Gli algoritmi hash supportati usati per un'impronta digitale del certificato sono `SHA256` , `SHA384` e `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="3ca46-233">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="3ca46-234">Se un oggetto `certificate` specifica `allowUntrustedRoot` come `true` il certificato specificato può essere concatenato a una radice non attendibile durante la compilazione della catena di certificati come parte della verifica della firma.</span><span class="sxs-lookup"><span data-stu-id="3ca46-234">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="3ca46-235">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-235">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="3ca46-236">sezione fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="3ca46-236">fallbackPackageFolders section</span></span>

<span data-ttu-id="3ca46-237">*(3.5 +)* Consente di preinstallare i pacchetti in modo che non sia necessario eseguire alcuna operazione se il pacchetto viene trovato nelle cartelle di fallback.</span><span class="sxs-lookup"><span data-stu-id="3ca46-237">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="3ca46-238">Le cartelle dei pacchetti di fallback hanno esattamente la stessa struttura di cartelle e file della cartella del pacchetto globale: *. nupkg* è presente e tutti i file vengono estratti.</span><span class="sxs-lookup"><span data-stu-id="3ca46-238">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="3ca46-239">La logica di ricerca per questa configurazione è la seguente:</span><span class="sxs-lookup"><span data-stu-id="3ca46-239">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="3ca46-240">Cercare nella cartella del pacchetto globale per verificare se il pacchetto o la versione è già stata scaricata.</span><span class="sxs-lookup"><span data-stu-id="3ca46-240">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="3ca46-241">Esaminare le cartelle di fallback per una corrispondenza del pacchetto o della versione.</span><span class="sxs-lookup"><span data-stu-id="3ca46-241">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="3ca46-242">Se una delle due ricerche ha esito positivo, non è necessario eseguire il download.</span><span class="sxs-lookup"><span data-stu-id="3ca46-242">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="3ca46-243">Se non viene trovata alcuna corrispondenza, NuGet controlla le origini file e quindi le origini http, quindi Scarica i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3ca46-243">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="3ca46-244">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-244">Key</span></span> | <span data-ttu-id="3ca46-245">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-245">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-246">(nome della cartella di fallback)</span><span class="sxs-lookup"><span data-stu-id="3ca46-246">(name of fallback folder)</span></span> | <span data-ttu-id="3ca46-247">Percorso della cartella di fallback.</span><span class="sxs-lookup"><span data-stu-id="3ca46-247">Path to fallback folder.</span></span> |

<span data-ttu-id="3ca46-248">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-248">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="3ca46-249">sezione packageManagement</span><span class="sxs-lookup"><span data-stu-id="3ca46-249">packageManagement section</span></span>

<span data-ttu-id="3ca46-250">Imposta il formato di gestione dei pacchetti predefinito, ovvero *packages.config* o PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3ca46-250">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="3ca46-251">I progetti in stile SDK utilizzano sempre PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3ca46-251">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="3ca46-252">Chiave</span><span class="sxs-lookup"><span data-stu-id="3ca46-252">Key</span></span> | <span data-ttu-id="3ca46-253">Valore</span><span class="sxs-lookup"><span data-stu-id="3ca46-253">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3ca46-254">format</span><span class="sxs-lookup"><span data-stu-id="3ca46-254">format</span></span> | <span data-ttu-id="3ca46-255">Valore booleano che indica il formato di gestione dei pacchetti predefinito.</span><span class="sxs-lookup"><span data-stu-id="3ca46-255">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="3ca46-256">Se `1` , il formato è PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3ca46-256">If `1`, format is PackageReference.</span></span> <span data-ttu-id="3ca46-257">Se `0` , format è *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="3ca46-257">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="3ca46-258">disabled</span><span class="sxs-lookup"><span data-stu-id="3ca46-258">disabled</span></span> | <span data-ttu-id="3ca46-259">Valore booleano che indica se visualizzare la richiesta di selezione di un formato di pacchetto predefinito durante la prima installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="3ca46-259">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="3ca46-260">`False`nasconde la richiesta.</span><span class="sxs-lookup"><span data-stu-id="3ca46-260">`False` hides the prompt.</span></span> |

<span data-ttu-id="3ca46-261">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="3ca46-261">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="3ca46-262">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="3ca46-262">Using environment variables</span></span>

<span data-ttu-id="3ca46-263">È possibile usare variabili di ambiente nei valori `nuget.config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3ca46-263">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="3ca46-264">Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="3ca46-264">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="3ca46-265">Si noti che è necessario usare le variabili di ambiente di tipo Windows (inizia e termina con%) anche in Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="3ca46-265">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="3ca46-266">`$HOME/NuGetRepository`La presenza di in un file di configurazione non viene risolta.</span><span class="sxs-lookup"><span data-stu-id="3ca46-266">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="3ca46-267">In Mac/Linux il valore di `%HOME%\NuGetRepository` viene risolto in `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="3ca46-267">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="3ca46-268">Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3ca46-268">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="3ca46-269">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="3ca46-269">Example config file</span></span>

<span data-ttu-id="3ca46-270">Di seguito è riportato un esempio `nuget.config` di file che illustra una serie di impostazioni, tra cui quelle facoltative:</span><span class="sxs-lookup"><span data-stu-id="3ca46-270">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
