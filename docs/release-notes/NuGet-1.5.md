---
title: Note sulla versione di NuGet 1,5
description: Note sulla versione per NuGet 1,5, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383349"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="a6979-103">Note sulla versione di NuGet 1,5</span><span class="sxs-lookup"><span data-stu-id="a6979-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="a6979-104">[Note sulla versione di nuget 1,4](../release-notes/nuget-1.4.md) | [Note sulla versione di NuGet 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="a6979-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="a6979-105">NuGet 1,5 è stato rilasciato il 30 agosto 2011.</span><span class="sxs-lookup"><span data-stu-id="a6979-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="a6979-106">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="a6979-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="a6979-107">Modelli di progetto con pacchetti NuGet preinstallati</span><span class="sxs-lookup"><span data-stu-id="a6979-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="a6979-108">Quando si crea un nuovo modello di progetto ASP.NET MVC 3, le librerie di script jQuery incluse nel progetto vengono effettivamente posizionate installando i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6979-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="a6979-109">Il modello di progetto ASP.NET MVC 3 include un set di pacchetti NuGet che vengono installati quando viene richiamato il modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="a6979-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="a6979-110">Questa possibilità di includere i pacchetti NuGet con un modello di progetto è ora una funzionalità di NuGet che può ora essere sfruttata da _qualsiasi_ modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="a6979-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="a6979-111">Per ulteriori informazioni su questa funzionalità, leggere questo [post di Blog dallo sviluppatore della funzionalità](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6979-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="a6979-112">Riferimenti ad assembly espliciti</span><span class="sxs-lookup"><span data-stu-id="a6979-112">Explicit Assembly References</span></span>

<span data-ttu-id="a6979-113">È stato aggiunto un nuovo elemento `<references />` usato per specificare in modo esplicito quali assembly all'interno del pacchetto deve essere fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="a6979-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="a6979-114">Ad esempio, se si aggiungono gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6979-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="a6979-115">Verrà quindi fatto riferimento solo alla `xunit.dll` e alla `xunit.extensions.dll` dalla [sottocartella del Framework/profilo](../reference/nuspec.md#explicit-assembly-references) appropriata della cartella `lib` anche se sono presenti altri assembly nella cartella.</span><span class="sxs-lookup"><span data-stu-id="a6979-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="a6979-116">Se questo elemento viene omesso, viene applicato il comportamento consueto, ovvero per fare riferimento a ogni assembly nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="a6979-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="a6979-117">__Per cosa si usa questa funzionalità?__</span><span class="sxs-lookup"><span data-stu-id="a6979-117">__What is this feature used for?__</span></span>

<span data-ttu-id="a6979-118">Questa funzionalità supporta solo assembly in fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="a6979-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="a6979-119">Quando si usano contratti di codice, ad esempio, è necessario che gli assembly del contratto si trovino accanto agli assembly di runtime che aumentano, in modo che Visual Studio possa trovarli, ma gli assembly del contratto non devono essere effettivamente usati come riferimento dal progetto e non devono essere copiati nella cartella `bin`.</span><span class="sxs-lookup"><span data-stu-id="a6979-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="a6979-120">Analogamente, la funzionalità può essere usata per unit test Framework, ad esempio XUnit, che richiedono la posizione degli assembly degli strumenti accanto agli assembly di runtime, esclusi i riferimenti ai progetti.</span><span class="sxs-lookup"><span data-stu-id="a6979-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="a6979-121">Aggiunta della possibilità di escludere i file nel file con estensione NuSpec</span><span class="sxs-lookup"><span data-stu-id="a6979-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="a6979-122">L'elemento `<file>` all'interno di un file di `.nuspec` può essere utilizzato per includere un file specifico o un set di file utilizzando un carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="a6979-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="a6979-123">Quando si usa un carattere jolly, non è possibile escludere un subset specifico dei file inclusi.</span><span class="sxs-lookup"><span data-stu-id="a6979-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="a6979-124">Si supponga, ad esempio, di volere tutti i file di testo all'interno di una cartella tranne uno specifico.</span><span class="sxs-lookup"><span data-stu-id="a6979-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="a6979-125">Usare i punti e virgola per specificare più file.</span><span class="sxs-lookup"><span data-stu-id="a6979-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="a6979-126">In alternativa, usare un carattere jolly per escludere un set di file, ad esempio tutti i file di backup</span><span class="sxs-lookup"><span data-stu-id="a6979-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="a6979-127">Rimozione di pacchetti utilizzando la finestra di dialogo richiesta per rimuovere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="a6979-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="a6979-128">Quando si disinstalla un pacchetto con dipendenze, NuGet richiede, consentendo la rimozione delle dipendenze di un pacchetto insieme al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a6979-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Rimozione di pacchetti dipendenti](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="a6979-130">miglioramento del comando `Get-Package`</span><span class="sxs-lookup"><span data-stu-id="a6979-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="a6979-131">Il `Get-Package` comando supporta ora un parametro di `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="a6979-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="a6979-132">Quindi, il comando</span><span class="sxs-lookup"><span data-stu-id="a6979-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="a6979-133">Elenca tutti i pacchetti installati nel progetto A.</span><span class="sxs-lookup"><span data-stu-id="a6979-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="a6979-134">Supporto per proxy che richiedono l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="a6979-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="a6979-135">Quando si usa NuGet dietro un proxy che richiede l'autenticazione, NuGet ora richiede le credenziali proxy.</span><span class="sxs-lookup"><span data-stu-id="a6979-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="a6979-136">L'immissione di credenziali consente a NuGet di connettersi al repository remoto.</span><span class="sxs-lookup"><span data-stu-id="a6979-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="a6979-137">Supporto per repository che richiedono l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="a6979-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="a6979-138">NuGet supporta ora la connessione a [repository privati](../hosting-packages/local-feeds.md) che richiedono l'autenticazione di base o NTLM.</span><span class="sxs-lookup"><span data-stu-id="a6979-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="a6979-139">Il supporto per l'autenticazione del digest verrà aggiunto in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="a6979-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="a6979-140">Miglioramenti delle prestazioni per il repository nuget.org</span><span class="sxs-lookup"><span data-stu-id="a6979-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="a6979-141">Sono stati apportati diversi miglioramenti alle prestazioni della raccolta nuget.org per rendere più veloce l'elenco e la ricerca di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="a6979-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="a6979-142">Filtro progetto finestra di dialogo soluzione</span><span class="sxs-lookup"><span data-stu-id="a6979-142">Solution dialog project filtering</span></span>
<span data-ttu-id="a6979-143">Nella finestra di dialogo a livello di soluzione, quando viene richiesto di specificare i progetti da installare, vengono visualizzati solo i progetti compatibili con il pacchetto selezionato.</span><span class="sxs-lookup"><span data-stu-id="a6979-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="a6979-144">Note sulla versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="a6979-144">Package Release Notes</span></span>
<span data-ttu-id="a6979-145">I pacchetti NuGet ora includono il supporto per le note sulla versione.</span><span class="sxs-lookup"><span data-stu-id="a6979-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="a6979-146">Le note sulla versione vengono visualizzate solo quando si visualizzano _gli aggiornamenti_ per un pacchetto, pertanto non è opportuno aggiungerle alla prima versione.</span><span class="sxs-lookup"><span data-stu-id="a6979-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Note sulla versione nella scheda aggiornamenti](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="a6979-148">Per aggiungere note sulla versione a un pacchetto, usare il nuovo elemento dei metadati `<releaseNotes />` nel file NuSpec.</span><span class="sxs-lookup"><span data-stu-id="a6979-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="a6979-149">. NuSpec & ltfiles/&gt; Improvement</span><span class="sxs-lookup"><span data-stu-id="a6979-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="a6979-150">Il file `.nuspec` ora consente l'elemento `<files />` vuoto, che indica a NuGet. exe di non includere alcun file nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a6979-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a6979-151">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="a6979-151">Bug Fixes</span></span>
<span data-ttu-id="a6979-152">NuGet 1,5 aveva un totale di 107 elementi di lavoro corretti.</span><span class="sxs-lookup"><span data-stu-id="a6979-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="a6979-153">103 di questi sono stati contrassegnati come bug.</span><span class="sxs-lookup"><span data-stu-id="a6979-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="a6979-154">Per un elenco completo degli elementi di lavoro corretti in NuGet 1,5, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a6979-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="a6979-155">Correzioni di bug degni di Nota:</span><span class="sxs-lookup"><span data-stu-id="a6979-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="a6979-156">[Problema 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` reso più intuitivo il controllo della versione, ordinando i pacchetti alfabeticamente e rimuovendo gli spazi vuoti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="a6979-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="a6979-157">[Problema 844](http://nuget.codeplex.com/workitem/844): i numeri di versione vengono ora normalizzati in modo che `Install-Package 1.0` funzioni in un pacchetto con la versione `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="a6979-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="a6979-158">[Problema 1060](http://nuget.codeplex.com/workitem/1060): quando si crea un pacchetto con NuGet. exe, il flag di `-Version` esegue l'override dell'elemento `<version />`.</span><span class="sxs-lookup"><span data-stu-id="a6979-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
