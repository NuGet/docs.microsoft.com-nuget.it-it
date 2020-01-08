---
title: informazioni di riferimento sul file NuGet. config
description: Informazioni di riferimento sul file NuGet.Config, incluse le sezioni config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: d6cad228eb052563fe57ea635bff0ea548cedc1f
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383564"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="cc00c-103">informazioni di riferimento su NuGet. config</span><span class="sxs-lookup"><span data-stu-id="cc00c-103">nuget.config reference</span></span>

<span data-ttu-id="cc00c-104">Il comportamento di NuGet è controllato dalle impostazioni in diversi file di `NuGet.Config` o `nuget.config`, come descritto in [configurazioni comuni di NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cc00c-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="cc00c-105">`nuget.config` è un file XML contenente un nodo `<configuration>` di livello superiore, che contiene a sua volta gli elementi per le sezioni descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="cc00c-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="cc00c-106">Ogni sezione contiene zero o più elementi.</span><span class="sxs-lookup"><span data-stu-id="cc00c-106">Each section contains zero or more items.</span></span> <span data-ttu-id="cc00c-107">Vedere il [file di configurazione di esempio](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="cc00c-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="cc00c-108">Per i nomi delle impostazioni non viene fatta distinzione tra maiuscole e minuscole e per i valori si possono usare [variabili di ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="cc00c-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="cc00c-109">Sezione config</span><span class="sxs-lookup"><span data-stu-id="cc00c-109">config section</span></span>

<span data-ttu-id="cc00c-110">Contiene varie impostazioni di configurazione, che possono essere impostate con il [comando `nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="cc00c-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="cc00c-111">`dependencyVersion` e `repositoryPath` si applicano solo ai progetti che usano `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="cc00c-112">`globalPackagesFolder` si applica solo ai progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cc00c-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="cc00c-113">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-113">Key</span></span> | <span data-ttu-id="cc00c-114">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-115">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="cc00c-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="cc00c-116">Valore `DependencyVersion` predefinito per l'installazione, il ripristino e l'aggiornamento del pacchetto, quando non viene specificata direttamente l'opzione `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="cc00c-117">Questo valore viene usato anche dall'interfaccia utente di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc00c-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="cc00c-118">I valori sono `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="cc00c-119">globalPackagesFolder (progetti che usano solo PackageReference)</span><span class="sxs-lookup"><span data-stu-id="cc00c-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="cc00c-120">Percorso della cartella dei pacchetti globale predefinita.</span><span class="sxs-lookup"><span data-stu-id="cc00c-120">The location of the default global packages folder.</span></span> <span data-ttu-id="cc00c-121">L'impostazione predefinita è `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="cc00c-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="cc00c-122">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="cc00c-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="cc00c-123">Questa impostazione viene sottoposta a override dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="cc00c-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="cc00c-124">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="cc00c-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="cc00c-125">Percorso in cui installare i pacchetti NuGet invece della cartella `$(Solutiondir)/packages` predefinita.</span><span class="sxs-lookup"><span data-stu-id="cc00c-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="cc00c-126">È possibile usare un percorso relativo nei file `nuget.config` specifici del progetto.</span><span class="sxs-lookup"><span data-stu-id="cc00c-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="cc00c-127">Questa impostazione viene sottoposta a override dalla variabile di ambiente NUGET_PACKAGES, che ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="cc00c-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="cc00c-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="cc00c-128">defaultPushSource</span></span> | <span data-ttu-id="cc00c-129">Identifica l'URL o il percorso dell'origine del pacchetto che deve essere usato come impostazione predefinita se non vengono trovate altre origini di pacchetti per un'operazione.</span><span class="sxs-lookup"><span data-stu-id="cc00c-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="cc00c-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="cc00c-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="cc00c-131">Impostazioni del proxy da usare per la connessione a origini di pacchetti. `http_proxy` deve essere nel formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="cc00c-132">Le password vengono crittografate e non possono essere aggiunte manualmente.</span><span class="sxs-lookup"><span data-stu-id="cc00c-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="cc00c-133">Per `no_proxy`, il valore è un elenco delimitato da virgole di domini per il bypass del server proxy.</span><span class="sxs-lookup"><span data-stu-id="cc00c-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="cc00c-134">In alternativa, è possibile usare le variabili di ambiente http_proxy e no_proxy per questi valori.</span><span class="sxs-lookup"><span data-stu-id="cc00c-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="cc00c-135">Per altri dettagli, vedere [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (Impostazioni del proxy NuGet) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="cc00c-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="cc00c-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="cc00c-136">signatureValidationMode</span></span> | <span data-ttu-id="cc00c-137">Specifica la modalità di convalida utilizzata per verificare le firme dei pacchetti per l'installazione e il ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc00c-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="cc00c-138">I valori sono `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="cc00c-139">Il valore predefinito è `accept`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-139">Defaults to `accept`.</span></span>

<span data-ttu-id="cc00c-140">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="cc00c-141">Sezione bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="cc00c-141">bindingRedirects section</span></span>

<span data-ttu-id="cc00c-142">Specifica se NuGet esegue o meno i reindirizzamenti di binding automatici quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc00c-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="cc00c-143">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-143">Key</span></span> | <span data-ttu-id="cc00c-144">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-145">skip</span><span class="sxs-lookup"><span data-stu-id="cc00c-145">skip</span></span> | <span data-ttu-id="cc00c-146">Valore booleano che indica se ignorare i reindirizzamenti di binding automatici.</span><span class="sxs-lookup"><span data-stu-id="cc00c-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="cc00c-147">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="cc00c-147">The default is false.</span></span> |

<span data-ttu-id="cc00c-148">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="cc00c-149">Sezione packageRestore</span><span class="sxs-lookup"><span data-stu-id="cc00c-149">packageRestore section</span></span>

<span data-ttu-id="cc00c-150">Controlla il ripristino dei pacchetti durante le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="cc00c-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="cc00c-151">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-151">Key</span></span> | <span data-ttu-id="cc00c-152">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-153">abilitato</span><span class="sxs-lookup"><span data-stu-id="cc00c-153">enabled</span></span> | <span data-ttu-id="cc00c-154">Valore booleano che indica se NuGet può eseguire il ripristino automatico.</span><span class="sxs-lookup"><span data-stu-id="cc00c-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="cc00c-155">È anche possibile impostare la variabile di ambiente `EnableNuGetPackageRestore` con il valore `True` invece di impostare questa chiave nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cc00c-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="cc00c-156">automatico</span><span class="sxs-lookup"><span data-stu-id="cc00c-156">automatic</span></span> | <span data-ttu-id="cc00c-157">Valore booleano che indica se NuGet deve controllare se mancano pacchetti durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="cc00c-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="cc00c-158">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="cc00c-159">Sezione solution</span><span class="sxs-lookup"><span data-stu-id="cc00c-159">solution section</span></span>

<span data-ttu-id="cc00c-160">Controlla se la cartella `packages` di una soluzione è inclusa nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="cc00c-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="cc00c-161">Questa sezione funziona solo nei file `nuget.config` in una cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="cc00c-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="cc00c-162">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-162">Key</span></span> | <span data-ttu-id="cc00c-163">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="cc00c-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="cc00c-165">Valore booleano che indica se ignorare la cartella dei pacchetti quando si utilizza il controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="cc00c-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="cc00c-166">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="cc00c-166">The default value is false.</span></span> |

<span data-ttu-id="cc00c-167">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="cc00c-168">Sezioni per le origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="cc00c-168">Package source sections</span></span>

<span data-ttu-id="cc00c-169">I `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` e `trustedSigners` tutti interagiscono per configurare il funzionamento di NuGet con i repository dei pacchetti durante le operazioni di installazione, ripristino e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="cc00c-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="cc00c-170">Il [comando`nuget sources`](../reference/cli-reference/cli-ref-sources.md) viene in genere usato per gestire queste impostazioni, ad eccezione di `apikeys` che viene gestito usando il [comando`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md)e `trustedSigners` che viene gestito con il [`nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="cc00c-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="cc00c-171">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="cc00c-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="cc00c-172">packageSources</span></span>

<span data-ttu-id="cc00c-173">Elenca tutte le origini di pacchetti note.</span><span class="sxs-lookup"><span data-stu-id="cc00c-173">Lists all known package sources.</span></span> <span data-ttu-id="cc00c-174">L'ordine viene ignorato durante le operazioni di ripristino e con qualsiasi progetto che usa il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cc00c-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="cc00c-175">NuGet rispetta l'ordine delle origini per le operazioni di installazione e aggiornamento con i progetti che usano `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="cc00c-176">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-176">Key</span></span> | <span data-ttu-id="cc00c-177">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-178">(nome da assegnare all'origine di pacchetti)</span><span class="sxs-lookup"><span data-stu-id="cc00c-178">(name to assign to the package source)</span></span> | <span data-ttu-id="cc00c-179">Percorso o URL dell'origine di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cc00c-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="cc00c-180">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="cc00c-181">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="cc00c-181">packageSourceCredentials</span></span>

<span data-ttu-id="cc00c-182">Archivia i nomi utente e le password per le origini, in genere specificati con le opzioni `-username` e `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-182">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="cc00c-183">Le password vengono crittografate per impostazione predefinita, a meno che non venga usata anche l'opzione `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-183">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="cc00c-184">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-184">Key</span></span> | <span data-ttu-id="cc00c-185">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-186">nomeutente</span><span class="sxs-lookup"><span data-stu-id="cc00c-186">username</span></span> | <span data-ttu-id="cc00c-187">Nome utente per l'origine in testo normale.</span><span class="sxs-lookup"><span data-stu-id="cc00c-187">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="cc00c-188">Password di</span><span class="sxs-lookup"><span data-stu-id="cc00c-188">password</span></span> | <span data-ttu-id="cc00c-189">Password crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="cc00c-189">The encrypted password for the source.</span></span> |
| <span data-ttu-id="cc00c-190">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="cc00c-190">cleartextpassword</span></span> | <span data-ttu-id="cc00c-191">Password non crittografata per l'origine.</span><span class="sxs-lookup"><span data-stu-id="cc00c-191">The unencrypted password for the source.</span></span> |

<span data-ttu-id="cc00c-192">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="cc00c-192">**Example:**</span></span>

<span data-ttu-id="cc00c-193">Nel file di configurazione, l'elemento `<packageSourceCredentials>` contiene i nodi figlio per ogni nome di origine applicabile (gli spazi nel nome vengono sostituiti con `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="cc00c-193">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="cc00c-194">Per le origini denominate "Contoso" e "Test Source", il file di configurazione contiene quanto segue quando si usano password crittografate:</span><span class="sxs-lookup"><span data-stu-id="cc00c-194">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="cc00c-195">Quando si usano password non crittografate:</span><span class="sxs-lookup"><span data-stu-id="cc00c-195">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="cc00c-196">apikeys</span><span class="sxs-lookup"><span data-stu-id="cc00c-196">apikeys</span></span>

<span data-ttu-id="cc00c-197">Archivia le chiavi per le origini che usano l'autenticazione con chiave API, in base alle impostazioni specificate con il [comando `nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="cc00c-197">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="cc00c-198">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-198">Key</span></span> | <span data-ttu-id="cc00c-199">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-200">(URL di origine)</span><span class="sxs-lookup"><span data-stu-id="cc00c-200">(source URL)</span></span> | <span data-ttu-id="cc00c-201">Chiave API crittografata.</span><span class="sxs-lookup"><span data-stu-id="cc00c-201">The encrypted API key.</span></span> |

<span data-ttu-id="cc00c-202">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-202">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="cc00c-203">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="cc00c-203">disabledPackageSources</span></span>

<span data-ttu-id="cc00c-204">Identifica le origini attualmente disabilitate.</span><span class="sxs-lookup"><span data-stu-id="cc00c-204">Identified currently disabled sources.</span></span> <span data-ttu-id="cc00c-205">Può essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="cc00c-205">May be empty.</span></span>

| <span data-ttu-id="cc00c-206">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-206">Key</span></span> | <span data-ttu-id="cc00c-207">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-208">(nome dell'origine)</span><span class="sxs-lookup"><span data-stu-id="cc00c-208">(name of source)</span></span> | <span data-ttu-id="cc00c-209">Valore booleano che indica se l'origine è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cc00c-209">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="cc00c-210">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="cc00c-210">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="cc00c-211">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="cc00c-211">activePackageSource</span></span>

<span data-ttu-id="cc00c-212">*(Solo versione 2.x; deprecata nella versione 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="cc00c-212">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="cc00c-213">Identifica l'origine attualmente attiva o indica l'aggregazione di tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="cc00c-213">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="cc00c-214">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-214">Key</span></span> | <span data-ttu-id="cc00c-215">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-216">(nome dell'origine) o `All`</span><span class="sxs-lookup"><span data-stu-id="cc00c-216">(name of source) or `All`</span></span> | <span data-ttu-id="cc00c-217">Se la chiave è il nome di un'origine, il valore è il percorso o l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="cc00c-217">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="cc00c-218">Se `All`, il valore deve essere `(Aggregate source)` per combinare tutte le origini di pacchetti non disabilitate in altro modo.</span><span class="sxs-lookup"><span data-stu-id="cc00c-218">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="cc00c-219">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-219">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="cc00c-220">sezione trustedSigners</span><span class="sxs-lookup"><span data-stu-id="cc00c-220">trustedSigners section</span></span>

<span data-ttu-id="cc00c-221">Archivia i firmatari attendibili utilizzati per consentire il pacchetto durante l'installazione o il ripristino.</span><span class="sxs-lookup"><span data-stu-id="cc00c-221">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="cc00c-222">Questo elenco non può essere vuoto quando l'utente imposta `signatureValidationMode` su `require`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-222">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="cc00c-223">Questa sezione può essere aggiornata con il [comando`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="cc00c-223">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="cc00c-224">**Schema**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-224">**Schema**:</span></span>

<span data-ttu-id="cc00c-225">Un firmatario attendibile dispone di una raccolta di elementi `certificate` che integrano tutti i certificati che identificano un determinato firmatario.</span><span class="sxs-lookup"><span data-stu-id="cc00c-225">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="cc00c-226">Un firmatario attendibile può essere un `Author` o una `Repository`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-226">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="cc00c-227">Un *repository* attendibile specifica anche il `serviceIndex` per il repository (che deve essere un uri di `https` valido) e può facoltativamente specificare un elenco delimitato da punti e virgola di `owners` per limitare ulteriormente l'attendibilità da tale repository specifico.</span><span class="sxs-lookup"><span data-stu-id="cc00c-227">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="cc00c-228">Gli algoritmi hash supportati usati per un'impronta digitale del certificato sono `SHA256`, `SHA384` e `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-228">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="cc00c-229">Se un `certificate` specifica `allowUntrustedRoot` `true` il certificato specificato può essere concatenato a una radice non attendibile durante la compilazione della catena di certificati come parte della verifica della firma.</span><span class="sxs-lookup"><span data-stu-id="cc00c-229">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="cc00c-230">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-230">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="cc00c-231">sezione fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="cc00c-231">fallbackPackageFolders section</span></span>

<span data-ttu-id="cc00c-232">*(3.5 +)* Consente di preinstallare i pacchetti in modo che non sia necessario eseguire alcuna operazione se il pacchetto viene trovato nelle cartelle di fallback.</span><span class="sxs-lookup"><span data-stu-id="cc00c-232">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="cc00c-233">Le cartelle dei pacchetti di fallback hanno esattamente la stessa struttura di cartelle e file della cartella del pacchetto globale: *. nupkg* è presente e tutti i file vengono estratti.</span><span class="sxs-lookup"><span data-stu-id="cc00c-233">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="cc00c-234">La logica di ricerca per questa configurazione è la seguente:</span><span class="sxs-lookup"><span data-stu-id="cc00c-234">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="cc00c-235">Cercare nella cartella del pacchetto globale per verificare se il pacchetto o la versione è già stata scaricata.</span><span class="sxs-lookup"><span data-stu-id="cc00c-235">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="cc00c-236">Esaminare le cartelle di fallback per una corrispondenza del pacchetto o della versione.</span><span class="sxs-lookup"><span data-stu-id="cc00c-236">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="cc00c-237">Se una delle due ricerche ha esito positivo, non è necessario eseguire il download.</span><span class="sxs-lookup"><span data-stu-id="cc00c-237">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="cc00c-238">Se non viene trovata alcuna corrispondenza, NuGet controlla le origini file e quindi le origini http, quindi Scarica i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cc00c-238">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="cc00c-239">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-239">Key</span></span> | <span data-ttu-id="cc00c-240">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-240">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-241">(nome della cartella di fallback)</span><span class="sxs-lookup"><span data-stu-id="cc00c-241">(name of fallback folder)</span></span> | <span data-ttu-id="cc00c-242">Percorso della cartella di fallback.</span><span class="sxs-lookup"><span data-stu-id="cc00c-242">Path to fallback folder.</span></span> |

<span data-ttu-id="cc00c-243">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-243">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="cc00c-244">sezione packageManagement</span><span class="sxs-lookup"><span data-stu-id="cc00c-244">packageManagement section</span></span>

<span data-ttu-id="cc00c-245">Imposta il formato di gestione dei pacchetti predefinito, ovvero *packages. config* o PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cc00c-245">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="cc00c-246">I progetti in stile SDK utilizzano sempre PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cc00c-246">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="cc00c-247">Key</span><span class="sxs-lookup"><span data-stu-id="cc00c-247">Key</span></span> | <span data-ttu-id="cc00c-248">Valore</span><span class="sxs-lookup"><span data-stu-id="cc00c-248">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cc00c-249">formato</span><span class="sxs-lookup"><span data-stu-id="cc00c-249">format</span></span> | <span data-ttu-id="cc00c-250">Valore booleano che indica il formato di gestione dei pacchetti predefinito.</span><span class="sxs-lookup"><span data-stu-id="cc00c-250">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="cc00c-251">Se `1`, format è PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cc00c-251">If `1`, format is PackageReference.</span></span> <span data-ttu-id="cc00c-252">Se `0`, format è *packages. config*.</span><span class="sxs-lookup"><span data-stu-id="cc00c-252">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="cc00c-253">disabilitati</span><span class="sxs-lookup"><span data-stu-id="cc00c-253">disabled</span></span> | <span data-ttu-id="cc00c-254">Valore booleano che indica se visualizzare la richiesta di selezione di un formato di pacchetto predefinito durante la prima installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc00c-254">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="cc00c-255">`False` nasconde la richiesta.</span><span class="sxs-lookup"><span data-stu-id="cc00c-255">`False` hides the prompt.</span></span> |

<span data-ttu-id="cc00c-256">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="cc00c-256">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="cc00c-257">Uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="cc00c-257">Using environment variables</span></span>

<span data-ttu-id="cc00c-258">È possibile usare variabili di ambiente nei valori `nuget.config` (NuGet 3.4 +) per applicare le impostazioni in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cc00c-258">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="cc00c-259">Ad esempio, se la variabile di ambiente `HOME` in Windows è impostata su `c:\users\username`, il valore di `%HOME%\NuGetRepository` nel file di configurazione viene risolto in `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-259">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="cc00c-260">In modo analogo, se la variabile `HOME` in Mac/Linux è impostata su `/home/myStuff`, `$HOME/NuGetRepository` nel file di configurazione viene risolto in `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="cc00c-260">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="cc00c-261">Se non viene trovata una variabile di ambiente, NuGet usa il valore letterale dal file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cc00c-261">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="cc00c-262">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="cc00c-262">Example config file</span></span>

<span data-ttu-id="cc00c-263">Di seguito è riportato un file `nuget.config` di esempio che illustra una serie di impostazioni:</span><span class="sxs-lookup"><span data-stu-id="cc00c-263">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
