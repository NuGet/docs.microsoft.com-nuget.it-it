---
title: Informazioni di riferimento sul file NuGet.Config | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: fbf31530-3bf4-478c-b26c-c2b24dd3406d
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
keywords: File NuGet. config, informazioni di riferimento sulla configurazione NuGet, opzioni di configurazione NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 830c622f622b894a228b18dfdb3a790bccfde8a3
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="68617-104">Informazioni di riferimento su NuGet.config</span><span class="sxs-lookup"><span data-stu-id="68617-104">NuGet.Config reference</span></span>

<span data-ttu-id="68617-105">Il comportamento di NuGet è controllato da impostazioni in diversi file `NuGet.Config`, come descritto in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="68617-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="68617-106">`NuGet.Config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="68617-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="68617-107">Ogni sezione contiene zero o più elementi `<add>` con gli attributi `key` e `value`.</span><span class="sxs-lookup"><span data-stu-id="68617-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="68617-108">Vedere il [file di configurazione di esempio](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="68617-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="68617-109">Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="68617-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="68617-110">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="68617-110">In this topic:</span></span>

- [<span data-ttu-id="68617-111">Sezione config</span><span class="sxs-lookup"><span data-stu-id="68617-111">config section</span></span>](#config-section)
- [<span data-ttu-id="68617-112">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="68617-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="68617-113">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="68617-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="68617-114">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="68617-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="68617-115">[Sezioni per le origini dei pacchetti](#package-source-sections): -[packageSources](#packagesources)</span><span class="sxs-lookup"><span data-stu-id="68617-115">[Package source sections](#package-source-sections): -[packageSources](#packagesources)</span></span>
  - [<span data-ttu-id="68617-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="68617-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="68617-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="68617-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="68617-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="68617-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="68617-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="68617-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="68617-120">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="68617-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="68617-121">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="68617-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="68617-122">Sezione config</span><span class="sxs-lookup"><span data-stu-id="68617-122">config section</span></span>

<span data-ttu-id="68617-123">Contiene varie impostazioni di configurazione, che possono essere impostate con il [comando `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="68617-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="68617-124">Nota: `dependencyVersion` e `repositoryPath` si applicano solo ai progetti che usano `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="68617-124">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="68617-125">`globalPackagesFolder` si applica solo ai progetti che usano `project.json` e i formati PackageReference.</span><span class="sxs-lookup"><span data-stu-id="68617-125">`globalPackagesFolder` applies only to projects using `project.json` and PackageReference formats.</span></span>

| <span data-ttu-id="68617-126">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-126">Key</span></span> | <span data-ttu-id="68617-127">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-128">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="68617-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="68617-129">Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="68617-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="68617-130">Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="68617-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="68617-131">I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="68617-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="68617-132">globalPackagesFolder (progetti che non usano `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="68617-132">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="68617-133">Percorso della cartella dei pacchetti globale predefinita.</span><span class="sxs-lookup"><span data-stu-id="68617-133">The location of the default global packages folder.</span></span> <span data-ttu-id="68617-134">L'impostazione predefinita è `%USERPROFILE%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="68617-134">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="68617-135">È possibile usare un percorso relativo nei file `Nuget.Config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="68617-135">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="68617-136">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="68617-136">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="68617-137">Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita.</span><span class="sxs-lookup"><span data-stu-id="68617-137">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="68617-138">È possibile usare un percorso relativo nei file `Nuget.Config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="68617-138">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="68617-139">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="68617-139">defaultPushSource</span></span> | <span data-ttu-id="68617-140">Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione.</span><span class="sxs-lookup"><span data-stu-id="68617-140">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="68617-141">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="68617-141">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="68617-142">Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="68617-142">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="68617-143">Le password vengono crittografate e non possono essere aggiunte manualmente.</span><span class="sxs-lookup"><span data-stu-id="68617-143">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="68617-144">Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy.</span><span class="sxs-lookup"><span data-stu-id="68617-144">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="68617-145">In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori.</span><span class="sxs-lookup"><span data-stu-id="68617-145">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="68617-146">Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="68617-146">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="68617-147">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="68617-147">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="68617-148">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="68617-148">bindingRedirects section</span></span>

<span data-ttu-id="68617-149">Specifica se NuGet esegue o meno i reindirizzamenti di binding automatici quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="68617-149">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="68617-150">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-150">Key</span></span> | <span data-ttu-id="68617-151">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-151">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-152">skip</span><span class="sxs-lookup"><span data-stu-id="68617-152">skip</span></span> | <span data-ttu-id="68617-153">Valore booleano che indica se ignorare i reindirizzamenti di binding automatici.</span><span class="sxs-lookup"><span data-stu-id="68617-153">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="68617-154">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="68617-154">The default is false.</span></span> |

<span data-ttu-id="68617-155">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="68617-155">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="68617-156">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="68617-156">packageRestore section</span></span>

<span data-ttu-id="68617-157">*Ignorata nella versione 2.7+*</span><span class="sxs-lookup"><span data-stu-id="68617-157">*Ignored in 2.7+*</span></span>

<span data-ttu-id="68617-158">Controlla il ripristino dei pacchetti durante le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="68617-158">Controls package restore during builds.</span></span>

| <span data-ttu-id="68617-159">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-159">Key</span></span> | <span data-ttu-id="68617-160">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-160">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-161">enabled</span><span class="sxs-lookup"><span data-stu-id="68617-161">enabled</span></span> | <span data-ttu-id="68617-162">Valore booleano che indica se NuGet può eseguire il ripristino automatico.</span><span class="sxs-lookup"><span data-stu-id="68617-162">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="68617-163">È anche possibile impostare la variabile di ambiente `EnableNuGetPackageRestore` con il valore `True` invece di impostare questa chiave nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="68617-163">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="68617-164">automatico</span><span class="sxs-lookup"><span data-stu-id="68617-164">automatic</span></span> | <span data-ttu-id="68617-165">Valore booleano che indica se NuGet deve controllare se mancano pacchetti durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="68617-165">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="68617-166">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="68617-166">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="68617-167">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="68617-167">solution section</span></span>

<span data-ttu-id="68617-168">Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="68617-168">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="68617-169">Questa sezione funziona solo nei file `Nuget.Config` in una cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="68617-169">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="68617-170">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-170">Key</span></span> | <span data-ttu-id="68617-171">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-171">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-172">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="68617-172">disableSourceControlIntegration</span></span> | <span data-ttu-id="68617-173">Valore booleano che indica se ignorare la cartella dei pacchetti quando si utilizza il controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="68617-173">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="68617-174">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="68617-174">The default value is false.</span></span> |

<span data-ttu-id="68617-175">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="68617-175">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="68617-176">Sezioni per le origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="68617-176">Package source sections</span></span>

<span data-ttu-id="68617-177">Le sezioni `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` e `disabledPackageSources` interagiscono tutte per configurare il funzionamento di NuGet con i repository dei pacchetti durante le operazioni di installazione, ripristino e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="68617-177">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="68617-178">Il [comando `nuget sources`](../tools/cli-ref-sources.md) viene generalmente usato per gestire queste impostazioni, ad eccezione della sezione `apikeys` che viene gestita con il [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="68617-178">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="68617-179">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="68617-179">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="68617-180">packageSources</span><span class="sxs-lookup"><span data-stu-id="68617-180">packageSources</span></span>

<span data-ttu-id="68617-181">Elenca tutte le origini di pacchetti note.</span><span class="sxs-lookup"><span data-stu-id="68617-181">Lists all known package sources.</span></span>

| <span data-ttu-id="68617-182">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-182">Key</span></span> | <span data-ttu-id="68617-183">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-183">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-184">(nome da assegnare all'origine di pacchetti)</span><span class="sxs-lookup"><span data-stu-id="68617-184">(name to assign to the package source)</span></span> | <span data-ttu-id="68617-185">Percorso o URL dell'origine di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="68617-185">The path or URL of the package source.</span></span> |

<span data-ttu-id="68617-186">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="68617-186">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="68617-187">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="68617-187">packageSourceCredentials</span></span>

<span data-ttu-id="68617-188">Archivia i nomi utente e le password per le origini, in genere specificati con le opzioni `-username` e `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="68617-188">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="68617-189">Le password vengono crittografate per impostazione predefinita, a meno che non venga usata anche l'opzione `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="68617-189">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="68617-190">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-190">Key</span></span> | <span data-ttu-id="68617-191">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-192">nomeutente</span><span class="sxs-lookup"><span data-stu-id="68617-192">username</span></span> | <span data-ttu-id="68617-193">Nome utente per l'origine in testo normale.</span><span class="sxs-lookup"><span data-stu-id="68617-193">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="68617-194">password</span><span class="sxs-lookup"><span data-stu-id="68617-194">password</span></span> | <span data-ttu-id="68617-195">Password crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="68617-195">The encrypted password for the source.</span></span> |
| <span data-ttu-id="68617-196">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="68617-196">cleartextpassword</span></span> | <span data-ttu-id="68617-197">Password non crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="68617-197">The unencrypted password for the source.</span></span> |

<span data-ttu-id="68617-198">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="68617-198">**Example:**</span></span>

<span data-ttu-id="68617-199">Nel file di configurazione, l'elemento `<packageSourceCredentials>` contiene i nodi figlio per ogni nome di origine applicabile (gli spazi nel nome vengono sostituiti con `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="68617-199">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="68617-200">Per le origini denominate "Contoso" e "Test Source", il file di configurazione contiene quanto segue quando si usano password crittografate:</span><span class="sxs-lookup"><span data-stu-id="68617-200">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="68617-201">Quando si usano password non crittografate:</span><span class="sxs-lookup"><span data-stu-id="68617-201">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="68617-202">apikeys</span><span class="sxs-lookup"><span data-stu-id="68617-202">apikeys</span></span>

<span data-ttu-id="68617-203">Archivia le chiavi per le origini che usano l'autenticazione con chiave API, in base alle impostazioni specificate con il [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="68617-203">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="68617-204">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-204">Key</span></span> | <span data-ttu-id="68617-205">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-205">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-206">(URL di origine)</span><span class="sxs-lookup"><span data-stu-id="68617-206">(source URL)</span></span> | <span data-ttu-id="68617-207">Chiave API crittografata.</span><span class="sxs-lookup"><span data-stu-id="68617-207">The encrypted API key.</span></span> |

<span data-ttu-id="68617-208">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="68617-208">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="68617-209">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="68617-209">disabledPackageSources</span></span>

<span data-ttu-id="68617-210">Identifica le origini attualmente disabilitate.</span><span class="sxs-lookup"><span data-stu-id="68617-210">Identified currently disabled sources.</span></span> <span data-ttu-id="68617-211">Può essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="68617-211">May be empty.</span></span>

| <span data-ttu-id="68617-212">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-212">Key</span></span> | <span data-ttu-id="68617-213">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-214">(nome dell'origine)</span><span class="sxs-lookup"><span data-stu-id="68617-214">(name of source)</span></span> | <span data-ttu-id="68617-215">Valore booleano che indica se l'origine è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="68617-215">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="68617-216">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="68617-216">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="68617-217">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="68617-217">activePackageSource</span></span>

<span data-ttu-id="68617-218">*(Solo versione 2.x; deprecata nella versione 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="68617-218">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="68617-219">Identifica l'origine attualmente attiva o indica l'aggregazione di tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="68617-219">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="68617-220">Chiave</span><span class="sxs-lookup"><span data-stu-id="68617-220">Key</span></span> | <span data-ttu-id="68617-221">Valore</span><span class="sxs-lookup"><span data-stu-id="68617-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68617-222">(nome dell'origine) o `All`</span><span class="sxs-lookup"><span data-stu-id="68617-222">(name of source) or `All`</span></span> | <span data-ttu-id="68617-223">Se la chiave è il nome di un'origine, il valore è il percorso o l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="68617-223">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="68617-224">Se `All`, il valore deve essere `(Aggregate source)` per combinare tutte le origini di pacchetti non disabilitate in altro modo.</span><span class="sxs-lookup"><span data-stu-id="68617-224">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="68617-225">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="68617-225">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="68617-226">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="68617-226">Using environment variables</span></span>

<span data-ttu-id="68617-227">È possibile usare variabili di ambiente nei valori `NuGet.Config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="68617-227">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="68617-228">Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="68617-228">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="68617-229">In modo analogo, se la variabile `HOME` in Mac/Linux è impostata su `/home/myStuff`, `$HOME/NuGetRepository` nel file di configurazione viene risolto in `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="68617-229">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="68617-230">Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="68617-230">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="68617-231">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="68617-231">Example config file</span></span>

<span data-ttu-id="68617-232">Di seguito è riportato un file `NuGet.Config` di esempio che illustra una serie di impostazioni:</span><span class="sxs-lookup"><span data-stu-id="68617-232">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
