---
title: Note sulla versione 1.5 di NuGet
description: Note sulla versione per NuGet 1.5 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548725"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="b7b46-103">Note sulla versione 1.5 di NuGet</span><span class="sxs-lookup"><span data-stu-id="b7b46-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="b7b46-104">[Note sulla versione di NuGet 1.4](../release-notes/nuget-1.4.md) | [note sulla versione di NuGet 1.6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="b7b46-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="b7b46-105">NuGet 1.5 è stato rilasciato il 30 agosto 2011.</span><span class="sxs-lookup"><span data-stu-id="b7b46-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="b7b46-106">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="b7b46-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="b7b46-107">Modelli di progetto con i pacchetti NuGet preinstallati</span><span class="sxs-lookup"><span data-stu-id="b7b46-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="b7b46-108">Quando si crea un nuovo modello di progetto ASP.NET MVC 3, le librerie di script jQuery è incluse nel progetto vengono effettivamente inserite da installazione di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="b7b46-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="b7b46-109">Il modello di progetto ASP.NET MVC 3 include un set di pacchetti NuGet che vengono installati quando viene richiamato il modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="b7b46-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="b7b46-110">La possibilità di includere i pacchetti NuGet con un modello di progetto è ora una funzionalità di NuGet che _qualsiasi_ modello di progetto possa ora sfruttare.</span><span class="sxs-lookup"><span data-stu-id="b7b46-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="b7b46-111">Per altre informazioni su questa funzionalità, leggi questo [post di blog dallo sviluppatore della funzionalità](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7b46-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="b7b46-112">Riferimenti espliciti agli Assembly</span><span class="sxs-lookup"><span data-stu-id="b7b46-112">Explicit Assembly References</span></span>

<span data-ttu-id="b7b46-113">Aggiunto un nuovo `<references />` elemento usato per specificare in modo esplicito gli assembly all'interno del pacchetto deve essere fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="b7b46-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="b7b46-114">Ad esempio, se si aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b7b46-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="b7b46-115">Quindi solo le `xunit.dll` e `xunit.extensions.dll` verrà fatto riferimento da appropriato [sottocartella/profilo del framework](../reference/nuspec.md#explicit-assembly-references) del `lib` cartella anche se sono presenti altri assembly nella cartella.</span><span class="sxs-lookup"><span data-stu-id="b7b46-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="b7b46-116">Se questo elemento viene omesso, quindi si applica al normale funzionamento, che consiste nel fare riferimento a tutti gli assembly nel `lib` cartella.</span><span class="sxs-lookup"><span data-stu-id="b7b46-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="b7b46-117">__Cosa serve per questa funzionalità?__</span><span class="sxs-lookup"><span data-stu-id="b7b46-117">__What is this feature used for?__</span></span>

<span data-ttu-id="b7b46-118">Questa funzionalità supporta gli assembly soli in fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="b7b46-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="b7b46-119">Ad esempio, quando si utilizzano contratti di codice, gli assembly del contratto devono essere in prossimità degli assembly di runtime che essi aumentano in modo che Visual Studio possa trovarli, ma gli assembly di contratto non devono effettivamente essere fatto riferimento dal progetto e non devono essere copiati nella il `bin` cartella.</span><span class="sxs-lookup"><span data-stu-id="b7b46-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="b7b46-120">Analogamente, la funzionalità è utilizzabile per Framework di unit test, come XUnit che necessitano di relativi assembly di strumenti che si trova accanto agli assembly di runtime, ma escluso da riferimenti del progetto.</span><span class="sxs-lookup"><span data-stu-id="b7b46-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="b7b46-121">Aggiunta di funzionalità per escludere i file nei file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="b7b46-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="b7b46-122">Il `<file>` elemento all'interno di un `.nuspec` file può essere utilizzato per includere un file specifico o un set di file usando un carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="b7b46-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="b7b46-123">Quando si usa un carattere jolly, non è possibile escludere un subset specifico di file inclusi.</span><span class="sxs-lookup"><span data-stu-id="b7b46-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="b7b46-124">Ad esempio, si supponga di che voler tutti i file di testo all'interno di una cartella, ad eccezione di uno specifico.</span><span class="sxs-lookup"><span data-stu-id="b7b46-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="b7b46-125">Usare un punto e virgola per specificare più file.</span><span class="sxs-lookup"><span data-stu-id="b7b46-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="b7b46-126">Oppure usare un carattere jolly per escludere un set di file, ad esempio tutti i file di backup</span><span class="sxs-lookup"><span data-stu-id="b7b46-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="b7b46-127">Rimozione di pacchetti tramite la finestra di dialogo chiede se si desidera per rimuovere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="b7b46-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="b7b46-128">Quando si disinstalla un pacchetto con dipendenze, NuGet richiede, consentendo la rimozione delle dipendenze del pacchetto insieme al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b7b46-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Rimozione di pacchetti dipendenti](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="b7b46-130">`Get-Package` miglioramento di comando</span><span class="sxs-lookup"><span data-stu-id="b7b46-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="b7b46-131">Il `Get-Package` comando supporta ora un `-ProjectName` parametro.</span><span class="sxs-lookup"><span data-stu-id="b7b46-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="b7b46-132">Pertanto, il comando</span><span class="sxs-lookup"><span data-stu-id="b7b46-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="b7b46-133">Elenca tutti i pacchetti installati nel progetto r.</span><span class="sxs-lookup"><span data-stu-id="b7b46-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="b7b46-134">Supporto per i proxy che richiedono l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="b7b46-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="b7b46-135">Quando si usa NuGet dietro un proxy che richiede l'autenticazione, NuGet ora richiederà di credenziali del proxy.</span><span class="sxs-lookup"><span data-stu-id="b7b46-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="b7b46-136">Immissione delle credenziali consente a NuGet per la connessione al repository remoto.</span><span class="sxs-lookup"><span data-stu-id="b7b46-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="b7b46-137">Supporto per i repository che richiede l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="b7b46-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="b7b46-138">NuGet supporta ora la connessione a [repository privati](../hosting-packages/local-feeds.md) che richiedono l'autenticazione di base o NTLM.</span><span class="sxs-lookup"><span data-stu-id="b7b46-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="b7b46-139">Verrà aggiunto il supporto per l'autenticazione del Digest in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="b7b46-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="b7b46-140">Miglioramenti delle prestazioni per il repository nuget.org</span><span class="sxs-lookup"><span data-stu-id="b7b46-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="b7b46-141">Sono stati apportati diversi miglioramenti delle prestazioni per la raccolta nuget.org per rendere pacchetto listato e la ricerca più velocemente.</span><span class="sxs-lookup"><span data-stu-id="b7b46-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="b7b46-142">Progetto di soluzione finestra di dialogo Filtro</span><span class="sxs-lookup"><span data-stu-id="b7b46-142">Solution dialog project filtering</span></span>
<span data-ttu-id="b7b46-143">Nella finestra di livello di soluzione, quando vengono richieste per i quali progetti per l'installazione, viene illustrato solo i progetti che sono compatibili con il pacchetto selezionato.</span><span class="sxs-lookup"><span data-stu-id="b7b46-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="b7b46-144">Note sulla versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="b7b46-144">Package Release Notes</span></span>
<span data-ttu-id="b7b46-145">I pacchetti NuGet includono ora il supporto per le note sulla versione.</span><span class="sxs-lookup"><span data-stu-id="b7b46-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="b7b46-146">Le note sulla versione Mostra solo backup quando si visualizzano _aggiornamenti_ per un pacchetto, pertanto non ha senso per aggiungerli al primo rilascio.</span><span class="sxs-lookup"><span data-stu-id="b7b46-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Note sulla versione all'interno della scheda degli aggiornamenti](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="b7b46-148">Per aggiungere note sulla versione per un pacchetto, usare il nuovo `<releaseNotes />` elemento dei metadati nel file NuSpec.</span><span class="sxs-lookup"><span data-stu-id="b7b46-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="b7b46-149">file con estensione nuspec & ltfiles /&gt; analisi utilizzo software</span><span class="sxs-lookup"><span data-stu-id="b7b46-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="b7b46-150">Il `.nuspec` file consente ora vuota `<files />` elemento, che indica a nuget.exe di non includere tutti i file nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b7b46-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b7b46-151">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="b7b46-151">Bug Fixes</span></span>
<span data-ttu-id="b7b46-152">1.5 NuGet ha un totale di 107 fisso di elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b7b46-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="b7b46-153">103 di questi sono stati contrassegnati come bug.</span><span class="sxs-lookup"><span data-stu-id="b7b46-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="b7b46-154">Per un elenco completo di lavoro gli elementi corretti in 1.5, NuGet, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b7b46-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="b7b46-155">Correzioni di bug la pena notare:</span><span class="sxs-lookup"><span data-stu-id="b7b46-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="b7b46-156">[Problema 1273](http://nuget.codeplex.com/workitem/1273): apportate `packages.config` controllo della versione più descrittivo ordinando alfabeticamente i pacchetti e la rimozione di uno spazio vuoto aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="b7b46-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="b7b46-157">[Problema 844](http://nuget.codeplex.com/workitem/844): i numeri di versione ora vengono normalizzati in modo che `Install-Package 1.0` funziona in un pacchetto con la versione `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="b7b46-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="b7b46-158">[Problema 1060](http://nuget.codeplex.com/workitem/1060): quando si crea un pacchetto utilizzando nuget.exe, il `-Version` flag sostituzioni di `<version />` elemento.</span><span class="sxs-lookup"><span data-stu-id="b7b46-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
