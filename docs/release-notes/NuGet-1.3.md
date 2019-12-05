---
title: Note sulla versione di NuGet 1,3
description: Note sulla versione per NuGet 1,3, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825254"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="972c3-103">Note sulla versione di NuGet 1,3</span><span class="sxs-lookup"><span data-stu-id="972c3-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="972c3-104">[Note sulla versione di nuget 1,2](../release-notes/nuget-1.2.md) | [Note sulla versione di NuGet 1,4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="972c3-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="972c3-105">NuGet 1,3 è stato rilasciato il 25 aprile 2011.</span><span class="sxs-lookup"><span data-stu-id="972c3-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="972c3-106">Nuove funzioni e caratteristiche</span><span class="sxs-lookup"><span data-stu-id="972c3-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="972c3-107">Creazione semplificata di pacchetti con l'integrazione del server dei simboli</span><span class="sxs-lookup"><span data-stu-id="972c3-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="972c3-108">Il team NuGet ha collaborato con gli utenti di [symbolsource.org](http://www.symbolsource.org/) per offrire un modo molto semplice per pubblicare le origini e i file PDB insieme al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="972c3-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="972c3-109">Questo consente ai consumer del pacchetto di eseguire un'istruzione nell'origine del pacchetto nel debugger.</span><span class="sxs-lookup"><span data-stu-id="972c3-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="972c3-110">Per altri dettagli, vedere [creazione e pubblicazione di un pacchetto di simboli](../create-packages/symbol-packages.md) il modo più semplice per pubblicare pacchetti NuGet con origini.</span><span class="sxs-lookup"><span data-stu-id="972c3-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="972c3-111">È anche possibile guardare una dimostrazione diretta di questa funzionalità come parte di NuGet approfondita in Mix11.</span><span class="sxs-lookup"><span data-stu-id="972c3-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="972c3-112">Questa funzionalità è completamente illustrata a partire dal contrassegno di 20 minuti del video.</span><span class="sxs-lookup"><span data-stu-id="972c3-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="972c3-113">`Open-PackagePage` Command</span><span class="sxs-lookup"><span data-stu-id="972c3-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="972c3-114">Questo comando consente di ottenere facilmente la pagina del progetto per un pacchetto all'interno della console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="972c3-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="972c3-115">Sono inoltre disponibili opzioni per aprire l'URL della licenza e la pagina relativa all'abuso del report per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="972c3-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="972c3-116">La sintassi per il comando è:</span><span class="sxs-lookup"><span data-stu-id="972c3-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="972c3-117">L'opzione `-PassThru` viene utilizzata per restituire il valore dell'URL specificato.</span><span class="sxs-lookup"><span data-stu-id="972c3-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="972c3-118">Esempi:</span><span class="sxs-lookup"><span data-stu-id="972c3-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="972c3-119">Apre un browser per l'URL del progetto specificato nel pacchetto Ninject.</span><span class="sxs-lookup"><span data-stu-id="972c3-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="972c3-120">Apre un browser per l'URL di licenza specificato nel pacchetto Ninject.</span><span class="sxs-lookup"><span data-stu-id="972c3-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="972c3-121">Apre un browser per l'URL nell'origine del pacchetto corrente utilizzata per segnalare gli abusi per il pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="972c3-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="972c3-122">Assegna l'URL della licenza alla variabile, $url, senza aprire l'URL in un browser.</span><span class="sxs-lookup"><span data-stu-id="972c3-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="972c3-123">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="972c3-123">Performance Improvements</span></span>

<span data-ttu-id="972c3-124">NuGet 1,3 introduce un notevole miglioramento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="972c3-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="972c3-125">NuGet 1,3 evita di scaricare la stessa versione di un pacchetto più volte includendo una cache per utente locale.</span><span class="sxs-lookup"><span data-stu-id="972c3-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="972c3-126">È possibile accedere alla cache e cancellarla tramite la finestra di dialogo Impostazioni di gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="972c3-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Finestra di dialogo Opzioni NuGet con impostazioni della cache dei pacchetti](./media/nuget-options.png)

<span data-ttu-id="972c3-128">Altri miglioramenti alle prestazioni includono l'aggiunta del supporto per la compressione HTTP e il miglioramento della velocità di installazione dei pacchetti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="972c3-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="972c3-129">Visual Studio e NuGet. exe usano lo stesso elenco di origini di pacchetti</span><span class="sxs-lookup"><span data-stu-id="972c3-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="972c3-130">Prima di NuGet 1,3, l'elenco delle origini dei pacchetti usate da NuGet. exe e dal componente aggiuntivo NuGet di Visual Studio non veniva archiviato nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="972c3-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="972c3-131">NuGet 1,3 ora usa lo stesso elenco in entrambe le posizioni.</span><span class="sxs-lookup"><span data-stu-id="972c3-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="972c3-132">L'elenco viene archiviato in `NuGet.Config` e archiviato nella cartella AppData.</span><span class="sxs-lookup"><span data-stu-id="972c3-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="972c3-133">NuGet. exe ignora i file e le cartelle che iniziano con ' .' per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="972c3-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="972c3-134">Per consentire a NuGet di funzionare correttamente con sistemi di controllo del codice sorgente quali Subversion e Mercurial, NuGet. exe ignora le cartelle e i file che iniziano con il carattere ' .' durante la creazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="972c3-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="972c3-135">È possibile eseguirne l'override usando due nuovi flag:</span><span class="sxs-lookup"><span data-stu-id="972c3-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="972c3-136">__-NoDefaultExcludes__ viene usato per eseguire l'override di questa impostazione e includere tutti i file.</span><span class="sxs-lookup"><span data-stu-id="972c3-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="972c3-137">__-Exclude__ viene usato per aggiungere altri file o cartelle da escludere usando un modello.</span><span class="sxs-lookup"><span data-stu-id="972c3-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="972c3-138">Ad esempio, per escludere tutti i file con l'estensione di file '. bak '</span><span class="sxs-lookup"><span data-stu-id="972c3-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="972c3-139">_Nota: il criterio non è ricorsivo per impostazione predefinita._</span><span class="sxs-lookup"><span data-stu-id="972c3-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="972c3-140">Supporto per progetti WiX e .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="972c3-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="972c3-141">Grazie ai contributi della community, NuGet include il supporto per i tipi di progetto WiX e .NET Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="972c3-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="972c3-142">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="972c3-142">Bug Fixes</span></span>

<span data-ttu-id="972c3-143">Per un elenco completo delle correzioni di bug, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="972c3-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="972c3-144">Correzioni di bug da notare</span><span class="sxs-lookup"><span data-stu-id="972c3-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="972c3-145">I pacchetti con file di origine funzionano sia nei siti Web che nei progetti di applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="972c3-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="972c3-146">Per i siti Web, i file di origine vengono copiati nella cartella `App_Code`</span><span class="sxs-lookup"><span data-stu-id="972c3-146">For Websites, source files are copied into the `App_Code` folder</span></span>
