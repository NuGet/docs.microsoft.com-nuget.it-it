---
title: Note sulla versione 1.5 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3ec1ff28-18fc-4d53-bd43-208619a7270a
description: "Note sulla versione per NuGet 1.5 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "1.5 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29792f4c7399155bcf5fb3361d7f10ddd1b18ca1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-15-release-notes"></a><span data-ttu-id="efd50-104">Note sulla versione 1.5 di NuGet</span><span class="sxs-lookup"><span data-stu-id="efd50-104">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="efd50-105">[Note sulla versione 1.4 NuGet](../release-notes/nuget-1.4.md) | [note sulla versione 1.6 NuGet](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="efd50-105">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="efd50-106">1.5 NuGet è stata rilasciata il 30 agosto 2011.</span><span class="sxs-lookup"><span data-stu-id="efd50-106">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="efd50-107">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="efd50-107">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="efd50-108">Modelli di progetto con i pacchetti NuGet preinstallati</span><span class="sxs-lookup"><span data-stu-id="efd50-108">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="efd50-109">Quando si crea un nuovo modello di progetto ASP.NET MVC 3, le librerie di script jQuery è incluse nel progetto sono effettivamente memorizzate da installazione dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="efd50-109">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="efd50-110">Il modello di progetto ASP.NET MVC 3 include un set di pacchetti NuGet a cui viene installato quando viene richiamato il modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="efd50-110">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="efd50-111">La possibilità di includere i pacchetti NuGet con un modello di progetto è ora una funzionalità di NuGet che _qualsiasi_ modello di progetto può ora sfruttare.</span><span class="sxs-lookup"><span data-stu-id="efd50-111">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="efd50-112">Per ulteriori informazioni su questa funzionalità, leggere questo [post di blog di sviluppo della funzionalità](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="efd50-112">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="efd50-113">Riferimenti agli Assembly esplicita</span><span class="sxs-lookup"><span data-stu-id="efd50-113">Explicit Assembly References</span></span>
<span data-ttu-id="efd50-114">Aggiunta di un nuovo `<references />` elemento utilizzato per specificare in modo esplicito gli assembly all'interno del pacchetto deve essere fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="efd50-114">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="efd50-115">Ad esempio, se si aggiungono le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="efd50-115">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="efd50-116">Quindi solo il `xunit.dll` e `xunit.extensions.dll` verrà fatto riferimento da appropriata [sottocartella/profilo del framework](../schema/nuspec.md#explicit-assembly-references) del `lib` cartella anche se sono presenti altri assembly nella cartella.</span><span class="sxs-lookup"><span data-stu-id="efd50-116">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../schema/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="efd50-117">Se questo elemento viene omesso, si applica al normale funzionamento, ovvero per fare riferimento a tutti gli assembly nel `lib` cartella.</span><span class="sxs-lookup"><span data-stu-id="efd50-117">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="efd50-118">__Per ciò che viene utilizzata questa funzionalità?__</span><span class="sxs-lookup"><span data-stu-id="efd50-118">__What is this feature used for?__</span></span>

<span data-ttu-id="efd50-119">Questa funzionalità supporta solo ad assembly in fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="efd50-119">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="efd50-120">Ad esempio, quando si utilizzano contratti di codice, i contratto gli assembly devono essere accanto agli assembly di runtime che essi aumentano in modo che Visual Studio è possibile trovarli, ma gli assembly di contratto non devono effettivamente essere fatto riferimento dal progetto e non devono essere copiati nella il `bin` cartella.</span><span class="sxs-lookup"><span data-stu-id="efd50-120">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="efd50-121">Analogamente, la funzionalità utilizzabile per il framework di unit test, ad esempio XUnit che richiedono i relativi assembly strumenti si trova accanto agli assembly di runtime, ma escluso da riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="efd50-121">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="efd50-122">Aggiunta la capacità di escludere i file del. nuspec</span><span class="sxs-lookup"><span data-stu-id="efd50-122">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="efd50-123">Il `<file>` elemento all'interno di un `.nuspec` file può essere utilizzato per includere un file specifico o un set di file mediante un carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="efd50-123">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="efd50-124">Quando si utilizza un carattere jolly, non è possibile escludere un sottoinsieme specifico di file inclusi.</span><span class="sxs-lookup"><span data-stu-id="efd50-124">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="efd50-125">Si supponga, ad esempio, che si desidera che tutti i file di testo all'interno di una cartella, ad eccezione di uno specifico.</span><span class="sxs-lookup"><span data-stu-id="efd50-125">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="efd50-126">Utilizzare un punto e virgola per specificare più file.</span><span class="sxs-lookup"><span data-stu-id="efd50-126">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="efd50-127">Oppure usare un carattere jolly per escludere un set di file, ad esempio tutti i file di backup</span><span class="sxs-lookup"><span data-stu-id="efd50-127">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="efd50-128">Rimozione dei pacchetti tramite la finestra di dialogo viene chiesto di rimuovere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="efd50-128">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="efd50-129">Quando si disinstalla un pacchetto con dipendenze, NuGet richiesto, consentendo la rimozione delle dipendenze di un pacchetto insieme al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="efd50-129">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Rimozione dei pacchetti dipendenti](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="efd50-131">`Get-Package`miglioramento di comando</span><span class="sxs-lookup"><span data-stu-id="efd50-131">`Get-Package` command improvement</span></span>
<span data-ttu-id="efd50-132">Il `Get-Package` comando supporta ora un `-ProjectName` parametro.</span><span class="sxs-lookup"><span data-stu-id="efd50-132">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="efd50-133">Pertanto, il comando</span><span class="sxs-lookup"><span data-stu-id="efd50-133">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="efd50-134">verranno elencati tutti i pacchetti installati nel progetto A.</span><span class="sxs-lookup"><span data-stu-id="efd50-134">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="efd50-135">Supporto per i proxy che richiede l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="efd50-135">Support for Proxies that require authentication</span></span>
<span data-ttu-id="efd50-136">Quando si usa NuGet dietro un proxy che richiede l'autenticazione, NuGet verrà ora richiesto per le credenziali del proxy.</span><span class="sxs-lookup"><span data-stu-id="efd50-136">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="efd50-137">Immissione delle credenziali consente NuGet per la connessione al repository remoto.</span><span class="sxs-lookup"><span data-stu-id="efd50-137">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="efd50-138">Supporto per i repository che richiede l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="efd50-138">Support for Repositories that require authentication</span></span>
<span data-ttu-id="efd50-139">NuGet supporta ora la connessione a [repository privati](../hosting-packages/local-feeds.md) che richiedono l'autenticazione di base o NTLM.</span><span class="sxs-lookup"><span data-stu-id="efd50-139">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="efd50-140">Verrà aggiunto il supporto per l'autenticazione del Digest in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="efd50-140">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="efd50-141">Miglioramenti delle prestazioni per il repository nuget.org</span><span class="sxs-lookup"><span data-stu-id="efd50-141">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="efd50-142">Sono stati apportati diversi miglioramenti delle prestazioni per la raccolta di nuget.org per rendere pacchetto elenco e la ricerca veloce.</span><span class="sxs-lookup"><span data-stu-id="efd50-142">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="efd50-143">Progetto di soluzione finestra di dialogo Filtro</span><span class="sxs-lookup"><span data-stu-id="efd50-143">Solution dialog project filtering</span></span>
<span data-ttu-id="efd50-144">Nella finestra di dialogo, a livello di soluzione quando viene richiesto per i progetti per l'installazione, vengono dimostrati solo i progetti che sono compatibili con il pacchetto selezionato.</span><span class="sxs-lookup"><span data-stu-id="efd50-144">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="efd50-145">Note sulla versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="efd50-145">Package Release Notes</span></span>
<span data-ttu-id="efd50-146">Pacchetti NuGet includono ora il supporto per le note sulla versione.</span><span class="sxs-lookup"><span data-stu-id="efd50-146">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="efd50-147">Le note sulla versione Mostra solo backup quando si visualizzano _aggiornamenti_ per un pacchetto, in modo non ha senso per aggiungerli al primo rilascio.</span><span class="sxs-lookup"><span data-stu-id="efd50-147">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Note sulla versione all'interno della scheda di aggiornamenti](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="efd50-149">Per aggiungere note sulla versione a un pacchetto, usare il nuovo `<releaseNotes />` elemento dei metadati nel file NuSpec.</span><span class="sxs-lookup"><span data-stu-id="efd50-149">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="efd50-150">. nuspec & ltfiles /&gt; analisi utilizzo software</span><span class="sxs-lookup"><span data-stu-id="efd50-150">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="efd50-151">Il `.nuspec` file consente ora vuota `<files />` elemento, che indica a nuget.exe non includere tutti i file nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="efd50-151">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="efd50-152">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="efd50-152">Bug Fixes</span></span>
<span data-ttu-id="efd50-153">1.5 NuGet era un totale di 107 fissati di elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="efd50-153">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="efd50-154">103 di quelli contrassegnati come bug.</span><span class="sxs-lookup"><span data-stu-id="efd50-154">103 of those were marked as bugs.</span></span>

<span data-ttu-id="efd50-155">Per un elenco completo di lavoro gli elementi corretti in NuGet 1.5,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="efd50-155">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="efd50-156">Correzioni di bug non degni di nota:</span><span class="sxs-lookup"><span data-stu-id="efd50-156">Bug fixes worth noting:</span></span>

* <span data-ttu-id="efd50-157">[Problema 1273](http://nuget.codeplex.com/workitem/1273): apportate `packages.config` controllo della versione più descrittivo per l'ordinamento in ordine alfabetico i pacchetti e la rimozione di uno spazio vuoto aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="efd50-157">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="efd50-158">[Problema 844](http://nuget.codeplex.com/workitem/844): i numeri di versione ora vengono normalizzati in modo che `Install-Package 1.0` funziona su un pacchetto con la versione `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="efd50-158">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="efd50-159">[Problema 1060](http://nuget.codeplex.com/workitem/1060): durante la creazione di un pacchetto utilizzando nuget.exe, il `-Version` flag esegue l'override di `<version />` elemento.</span><span class="sxs-lookup"><span data-stu-id="efd50-159">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
