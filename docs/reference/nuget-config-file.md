---
title: riferimento a un File NuGet. config
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 504a48224051265164f9ab183e63fa5e7f5867e6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546915"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="98100-103">riferimento di NuGet. config</span><span class="sxs-lookup"><span data-stu-id="98100-103">nuget.config reference</span></span>

<span data-ttu-id="98100-104">Il comportamento di NuGet è controllato da impostazioni in diversi file `NuGet.Config`, come descritto in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="98100-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="98100-105">`nuget.config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="98100-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="98100-106">Ogni sezione contiene zero o più elementi `<add>` con gli attributi `key` e `value`.</span><span class="sxs-lookup"><span data-stu-id="98100-106">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="98100-107">Vedere il [file di configurazione di esempio](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="98100-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="98100-108">Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="98100-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="98100-109">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="98100-109">In this topic:</span></span>

- [<span data-ttu-id="98100-110">Sezione config</span><span class="sxs-lookup"><span data-stu-id="98100-110">config section</span></span>](#config-section)
- [<span data-ttu-id="98100-111">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="98100-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="98100-112">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="98100-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="98100-113">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="98100-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="98100-114">[Sezioni per le origini dei pacchetti](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="98100-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="98100-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="98100-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="98100-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="98100-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="98100-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="98100-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="98100-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="98100-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="98100-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="98100-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="98100-120">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="98100-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="98100-121">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="98100-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="98100-122">Sezione config</span><span class="sxs-lookup"><span data-stu-id="98100-122">config section</span></span>

<span data-ttu-id="98100-123">Contiene varie impostazioni di configurazione, che possono essere impostate con il [comando `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="98100-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="98100-124">`dependencyVersion` e `repositoryPath` si applicano solo ai progetti che usano `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="98100-124">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="98100-125">`globalPackagesFolder` si applica solo ai progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="98100-125">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="98100-126">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-126">Key</span></span> | <span data-ttu-id="98100-127">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-128">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="98100-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="98100-129">Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="98100-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="98100-130">Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="98100-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="98100-131">I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="98100-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="98100-132">globalPackagesFolder (progetti usando solo PackageReference)</span><span class="sxs-lookup"><span data-stu-id="98100-132">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="98100-133">Percorso della cartella dei pacchetti globale predefinita.</span><span class="sxs-lookup"><span data-stu-id="98100-133">The location of the default global packages folder.</span></span> <span data-ttu-id="98100-134">L'impostazione predefinita è `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="98100-134">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="98100-135">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="98100-135">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="98100-136">Questa impostazione viene sostituita dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="98100-136">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="98100-137">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="98100-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="98100-138">Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita.</span><span class="sxs-lookup"><span data-stu-id="98100-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="98100-139">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="98100-139">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="98100-140">Questa impostazione viene sostituita dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="98100-140">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="98100-141">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="98100-141">defaultPushSource</span></span> | <span data-ttu-id="98100-142">Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione.</span><span class="sxs-lookup"><span data-stu-id="98100-142">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="98100-143">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="98100-143">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="98100-144">Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="98100-144">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="98100-145">Le password vengono crittografate e non possono essere aggiunte manualmente.</span><span class="sxs-lookup"><span data-stu-id="98100-145">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="98100-146">Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy.</span><span class="sxs-lookup"><span data-stu-id="98100-146">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="98100-147">In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori.</span><span class="sxs-lookup"><span data-stu-id="98100-147">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="98100-148">Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="98100-148">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="98100-149">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="98100-149">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="98100-150">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="98100-150">bindingRedirects section</span></span>

<span data-ttu-id="98100-151">Specifica se NuGet esegue o meno i reindirizzamenti di binding automatici quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="98100-151">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="98100-152">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-152">Key</span></span> | <span data-ttu-id="98100-153">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-153">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-154">skip</span><span class="sxs-lookup"><span data-stu-id="98100-154">skip</span></span> | <span data-ttu-id="98100-155">Valore booleano che indica se ignorare i reindirizzamenti di binding automatici.</span><span class="sxs-lookup"><span data-stu-id="98100-155">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="98100-156">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="98100-156">The default is false.</span></span> |

<span data-ttu-id="98100-157">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="98100-157">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="98100-158">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="98100-158">packageRestore section</span></span>

<span data-ttu-id="98100-159">Controlla il ripristino dei pacchetti durante le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="98100-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="98100-160">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-160">Key</span></span> | <span data-ttu-id="98100-161">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-162">enabled</span><span class="sxs-lookup"><span data-stu-id="98100-162">enabled</span></span> | <span data-ttu-id="98100-163">Valore booleano che indica se NuGet può eseguire il ripristino automatico.</span><span class="sxs-lookup"><span data-stu-id="98100-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="98100-164">È anche possibile impostare la variabile di ambiente `EnableNuGetPackageRestore` con il valore `True` invece di impostare questa chiave nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="98100-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="98100-165">automatico</span><span class="sxs-lookup"><span data-stu-id="98100-165">automatic</span></span> | <span data-ttu-id="98100-166">Valore booleano che indica se NuGet deve controllare se mancano pacchetti durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="98100-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="98100-167">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="98100-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="98100-168">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="98100-168">solution section</span></span>

<span data-ttu-id="98100-169">Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="98100-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="98100-170">Questa sezione funziona solo nei file `nuget.config` in una cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="98100-170">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="98100-171">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-171">Key</span></span> | <span data-ttu-id="98100-172">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="98100-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="98100-174">Valore booleano che indica se ignorare la cartella dei pacchetti quando si utilizza il controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="98100-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="98100-175">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="98100-175">The default value is false.</span></span> |

<span data-ttu-id="98100-176">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="98100-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="98100-177">Sezioni per le origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="98100-177">Package source sections</span></span>

<span data-ttu-id="98100-178">Le sezioni `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` e `disabledPackageSources` interagiscono tutte per configurare il funzionamento di NuGet con i repository dei pacchetti durante le operazioni di installazione, ripristino e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="98100-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="98100-179">Il [comando `nuget sources`](../tools/cli-ref-sources.md) viene generalmente usato per gestire queste impostazioni, ad eccezione della sezione `apikeys` che viene gestita con il [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="98100-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="98100-180">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="98100-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="98100-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="98100-181">packageSources</span></span>

<span data-ttu-id="98100-182">Elenca tutte le origini di pacchetti note.</span><span class="sxs-lookup"><span data-stu-id="98100-182">Lists all known package sources.</span></span> <span data-ttu-id="98100-183">L'ordine viene ignorato durante le operazioni di ripristino e con qualsiasi progetto usando il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="98100-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="98100-184">NuGet rispetta l'ordine delle origini per l'installazione e operazioni di aggiornamento con i progetti che usano `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="98100-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="98100-185">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-185">Key</span></span> | <span data-ttu-id="98100-186">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-187">(nome da assegnare all'origine di pacchetti)</span><span class="sxs-lookup"><span data-stu-id="98100-187">(name to assign to the package source)</span></span> | <span data-ttu-id="98100-188">Percorso o URL dell'origine di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="98100-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="98100-189">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="98100-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="98100-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="98100-190">packageSourceCredentials</span></span>

<span data-ttu-id="98100-191">Archivia i nomi utente e le password per le origini, in genere specificati con le opzioni `-username` e `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="98100-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="98100-192">Le password vengono crittografate per impostazione predefinita, a meno che non venga usata anche l'opzione `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="98100-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="98100-193">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-193">Key</span></span> | <span data-ttu-id="98100-194">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-195">nomeutente</span><span class="sxs-lookup"><span data-stu-id="98100-195">username</span></span> | <span data-ttu-id="98100-196">Nome utente per l'origine in testo normale.</span><span class="sxs-lookup"><span data-stu-id="98100-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="98100-197">password</span><span class="sxs-lookup"><span data-stu-id="98100-197">password</span></span> | <span data-ttu-id="98100-198">Password crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="98100-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="98100-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="98100-199">cleartextpassword</span></span> | <span data-ttu-id="98100-200">Password non crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="98100-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="98100-201">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="98100-201">**Example:**</span></span>

<span data-ttu-id="98100-202">Nel file di configurazione, l'elemento `<packageSourceCredentials>` contiene i nodi figlio per ogni nome di origine applicabile (gli spazi nel nome vengono sostituiti con `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="98100-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="98100-203">Per le origini denominate "Contoso" e "Test Source", il file di configurazione contiene quanto segue quando si usano password crittografate:</span><span class="sxs-lookup"><span data-stu-id="98100-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="98100-204">Quando si usano password non crittografate:</span><span class="sxs-lookup"><span data-stu-id="98100-204">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="98100-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="98100-205">apikeys</span></span>

<span data-ttu-id="98100-206">Archivia le chiavi per le origini che usano l'autenticazione con chiave API, in base alle impostazioni specificate con il [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="98100-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="98100-207">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-207">Key</span></span> | <span data-ttu-id="98100-208">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-209">(URL di origine)</span><span class="sxs-lookup"><span data-stu-id="98100-209">(source URL)</span></span> | <span data-ttu-id="98100-210">Chiave API crittografata.</span><span class="sxs-lookup"><span data-stu-id="98100-210">The encrypted API key.</span></span> |

<span data-ttu-id="98100-211">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="98100-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="98100-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="98100-212">disabledPackageSources</span></span>

<span data-ttu-id="98100-213">Identifica le origini attualmente disabilitate.</span><span class="sxs-lookup"><span data-stu-id="98100-213">Identified currently disabled sources.</span></span> <span data-ttu-id="98100-214">Può essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="98100-214">May be empty.</span></span>

| <span data-ttu-id="98100-215">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-215">Key</span></span> | <span data-ttu-id="98100-216">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-217">(nome dell'origine)</span><span class="sxs-lookup"><span data-stu-id="98100-217">(name of source)</span></span> | <span data-ttu-id="98100-218">Valore booleano che indica se l'origine è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="98100-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="98100-219">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="98100-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="98100-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="98100-220">activePackageSource</span></span>

<span data-ttu-id="98100-221">*(Solo versione 2.x; deprecata nella versione 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="98100-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="98100-222">Identifica l'origine attualmente attiva o indica l'aggregazione di tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="98100-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="98100-223">Chiave</span><span class="sxs-lookup"><span data-stu-id="98100-223">Key</span></span> | <span data-ttu-id="98100-224">Valore</span><span class="sxs-lookup"><span data-stu-id="98100-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98100-225">(nome dell'origine) o `All`</span><span class="sxs-lookup"><span data-stu-id="98100-225">(name of source) or `All`</span></span> | <span data-ttu-id="98100-226">Se la chiave è il nome di un'origine, il valore è il percorso o l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="98100-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="98100-227">Se `All`, il valore deve essere `(Aggregate source)` per combinare tutte le origini di pacchetti non disabilitate in altro modo.</span><span class="sxs-lookup"><span data-stu-id="98100-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="98100-228">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="98100-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="98100-229">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="98100-229">Using environment variables</span></span>

<span data-ttu-id="98100-230">È possibile usare variabili di ambiente nei valori `nuget.config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="98100-230">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="98100-231">Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="98100-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="98100-232">In modo analogo, se la variabile `HOME` in Mac/Linux è impostata su `/home/myStuff`, `%HOME%/NuGetRepository` nel file di configurazione viene risolto in `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="98100-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="98100-233">Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="98100-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="98100-234">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="98100-234">Example config file</span></span>

<span data-ttu-id="98100-235">Di seguito è riportato un file `nuget.config` di esempio che illustra una serie di impostazioni:</span><span class="sxs-lookup"><span data-stu-id="98100-235">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
</configuration>
```
