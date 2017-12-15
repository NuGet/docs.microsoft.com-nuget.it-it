---
title: Note sulla versione 1.3 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5d1c2191-783f-4faa-b72e-356a59323d39
description: "Note sulla versione per NuGet 1.3 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "1.3 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bc39efd5b9c550c3fdeddf9ad980c0bd9d4dcb3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="3adae-104">Note sulla versione 1.3 di NuGet</span><span class="sxs-lookup"><span data-stu-id="3adae-104">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="3adae-105">[Note sulla versione di NuGet 1.2](../release-notes/nuget-1.2.md) | [note sulla versione 1.4 di NuGet](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="3adae-105">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="3adae-106">NuGet 1.3 è stata rilasciata il 25 aprile 2011.</span><span class="sxs-lookup"><span data-stu-id="3adae-106">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="3adae-107">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="3adae-107">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="3adae-108">Creazione del pacchetto ottimizzata con l'integrazione di server di simboli</span><span class="sxs-lookup"><span data-stu-id="3adae-108">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="3adae-109">Il team di NuGet collaborato con i colleghi [SymbolSource.org](http://www.symbolsource.org/) per offrire un modo semplice di pubblicare le origini e del file PDB con il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="3adae-109">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="3adae-110">Questo consente ai consumer del pacchetto di eseguire l'istruzione di origine per il pacchetto nel debugger.</span><span class="sxs-lookup"><span data-stu-id="3adae-110">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="3adae-111">Per altre informazioni, leggere [creazione e la pubblicazione di un pacchetto di simboli](../create-packages/symbol-packages.md) il modo più semplice per pubblicare i pacchetti NuGet con origini.</span><span class="sxs-lookup"><span data-stu-id="3adae-111">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="3adae-112">È anche possibile guardare una dimostrazione in tempo reale di questa funzionalità, come parte di NuGet in modo approfondito comunicare in Mix11.</span><span class="sxs-lookup"><span data-stu-id="3adae-112">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="3adae-113">Questa funzionalità è completamente illustrata a partire dal contrassegno di 20 minuti del video.</span><span class="sxs-lookup"><span data-stu-id="3adae-113">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="3adae-114">`Open-PackagePage`Comando</span><span class="sxs-lookup"><span data-stu-id="3adae-114">`Open-PackagePage` Command</span></span>

<span data-ttu-id="3adae-115">Questo comando consente di connettersi alla pagina del progetto per un pacchetto dall'interno della Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3adae-115">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="3adae-116">Fornisce inoltre opzioni per aprire l'URL di licenza e la pagina del report abusi per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="3adae-116">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="3adae-117">La sintassi per il comando è:</span><span class="sxs-lookup"><span data-stu-id="3adae-117">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="3adae-118">Il `-PassThru` opzione viene utilizzata per restituire il valore dell'URL specificato.</span><span class="sxs-lookup"><span data-stu-id="3adae-118">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="3adae-119">Esempi:</span><span class="sxs-lookup"><span data-stu-id="3adae-119">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="3adae-120">Apre un browser all'URL di progetto specificato nel pacchetto Ninject.</span><span class="sxs-lookup"><span data-stu-id="3adae-120">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="3adae-121">Apre un browser all'URL della licenza specificato nel pacchetto Ninject.</span><span class="sxs-lookup"><span data-stu-id="3adae-121">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="3adae-122">Apre un browser all'URL nell'origine pacchetto corrente usato per segnalare abusi per il pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="3adae-122">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="3adae-123">Assegna l'URL della licenza alla variabile, $url, senza aprire l'URL in un browser.</span><span class="sxs-lookup"><span data-stu-id="3adae-123">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="3adae-124">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="3adae-124">Performance Improvements</span></span>

<span data-ttu-id="3adae-125">1.3 NuGet introduce numerosi miglioramenti delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3adae-125">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="3adae-126">1.3 NuGet consente di evitare il download di più volte la stessa versione di un pacchetto con l'inclusione di una cache locale per ogni utente.</span><span class="sxs-lookup"><span data-stu-id="3adae-126">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="3adae-127">La cache siano accessibili e mediante la finestra di dialogo Impostazioni di gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="3adae-127">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Finestra di dialogo Opzioni NuGet con le impostazioni della Cache di pacchetto](./media/nuget-options.png)

<span data-ttu-id="3adae-129">Altri miglioramenti delle prestazioni includono l'aggiunta del supporto per la compressione HTTP e migliorare la velocità di installazione del pacchetto all'interno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3adae-129">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="3adae-130">Visual Studio e nuget.exe utilizza lo stesso elenco di origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="3adae-130">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="3adae-131">Prima di NuGet 1.3, l'elenco delle origini pacchetto utilizzato da nuget.exe e il componente aggiuntivo NuGet Visual Studio non sono stati archiviati nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="3adae-131">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="3adae-132">1.3 NuGet ora utilizza lo stesso elenco in entrambe le posizioni.</span><span class="sxs-lookup"><span data-stu-id="3adae-132">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="3adae-133">L'elenco viene archiviato `NuGet.Config` e archiviati nella cartella AppData.</span><span class="sxs-lookup"><span data-stu-id="3adae-133">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="3adae-134">NuGet.exe ignora i file e cartelle che iniziano con '.' per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="3adae-134">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="3adae-135">Per rendere NuGet funzionano bene con sistemi di controllo codice sorgente, ad esempio Subversion e Mercurial, nuget.exe ignora le cartelle e i file che iniziano con il '.' carattere durante la creazione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3adae-135">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="3adae-136">Può essere sottoposta a override utilizzando due nuovi flag:</span><span class="sxs-lookup"><span data-stu-id="3adae-136">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="3adae-137">__-NoDefaultExcludes__ viene utilizzato per eseguire l'override di questa impostazione e include tutti i file.</span><span class="sxs-lookup"><span data-stu-id="3adae-137">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="3adae-138">__-Consente di escludere__ viene utilizzato per aggiungere altri file e cartelle da escludere usando un modello.</span><span class="sxs-lookup"><span data-stu-id="3adae-138">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="3adae-139">Ad esempio, per escludere tutti i file con estensione '. bak'</span><span class="sxs-lookup"><span data-stu-id="3adae-139">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="3adae-140">_Nota: il modello non è ricorsiva per impostazione predefinita._</span><span class="sxs-lookup"><span data-stu-id="3adae-140">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="3adae-141">Supporto per i progetti di WiX e Micro .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3adae-141">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="3adae-142">Grazie ai contributi della community, NuGet include il supporto per i tipi di progetto WiX nonché Micro .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3adae-142">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="3adae-143">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="3adae-143">Bug Fixes</span></span>

<span data-ttu-id="3adae-144">Per un elenco completo delle correzioni di bug, visitare il [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="3adae-144">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="3adae-145">Correzioni di bug non degni di nota</span><span class="sxs-lookup"><span data-stu-id="3adae-145">Bug fixes worth noting</span></span>

* <span data-ttu-id="3adae-146">Pacchetti con file di origine funzionano in entrambi i siti Web e progetti di applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="3adae-146">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="3adae-147">Per i siti Web, file di origine vengono copiati nel `App_Code` cartella</span><span class="sxs-lookup"><span data-stu-id="3adae-147">For Websites, source files are copied into the `App_Code` folder</span></span>
