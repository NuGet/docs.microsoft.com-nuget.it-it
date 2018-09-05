---
title: Note sulla versione 2.0 per NuGet
description: Note sulla versione per NuGet 2.0 tra problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547575"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="b5390-103">Note sulla versione 2.0 per NuGet</span><span class="sxs-lookup"><span data-stu-id="b5390-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="b5390-104">[Note sulla versione di NuGet 1.8](../release-notes/nuget-1.8.md) | [note sulla versione di NuGet 2.1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="b5390-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="b5390-105">NuGet 2.0 è stato rilasciato il 19 giugno 2012.</span><span class="sxs-lookup"><span data-stu-id="b5390-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="b5390-106">Problema di installazione noti</span><span class="sxs-lookup"><span data-stu-id="b5390-106">Known Installation Issue</span></span>
<span data-ttu-id="b5390-107">Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="b5390-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="b5390-108">Per risolvere il problema è sufficiente disinstallare NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5390-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="b5390-109">Visualizzare [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) per altre informazioni, o [passare direttamente all'hotfix di Visual Studio](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="b5390-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="b5390-110">Nota: Se Visual Studio non consentirà di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), quindi probabile che sia necessario riavviare Visual Studio tramite "Esegui come amministratore".</span><span class="sxs-lookup"><span data-stu-id="b5390-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="b5390-111">Il consenso di ripristino del pacchetto è ora attivo</span><span class="sxs-lookup"><span data-stu-id="b5390-111">Package restore consent is now active</span></span>

<span data-ttu-id="b5390-112">Come descritto in questo [inserire un post nel package restore consenso](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 questo punto verrà richiesto il consenso per abilitare il ripristino dei pacchetti passare alla modalità online e scaricare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="b5390-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="b5390-113">Assicurarsi di aver specificato il consenso tramite la finestra di dialogo pacchetto configuration manager o la variabile di ambiente EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="b5390-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="b5390-114">Gruppo di dipendenze dal framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="b5390-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="b5390-115">A partire dalla versione 2.0, pacchetto dipendenze possono variare in base al profilo del framework del progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b5390-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="b5390-116">Ciò avviene utilizzando una versione aggiornata `.nuspec` dello schema.</span><span class="sxs-lookup"><span data-stu-id="b5390-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="b5390-117">Il `<dependencies>` elemento può ora contenere un set di `<group>` elementi.</span><span class="sxs-lookup"><span data-stu-id="b5390-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="b5390-118">Ogni gruppo contiene zero o più `<dependency>` elementi e un `targetFramework` attributo.</span><span class="sxs-lookup"><span data-stu-id="b5390-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="b5390-119">Tutte le dipendenze all'interno di un gruppo vengono installate insieme se il framework di destinazione è compatibile con il profilo del framework di progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b5390-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="b5390-120">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b5390-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="b5390-121">Si noti che un gruppo può contenere **zero** dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b5390-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="b5390-122">Nell'esempio precedente, se il pacchetto viene installato in un progetto destinato a Silverlight 3.0 o versione successiva, non verranno installate dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b5390-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="b5390-123">Se il pacchetto viene installata in un progetto destinato a .NET 4.0 o versioni successive, due dipendenze, jQuery e WebActivator, verranno installate.</span><span class="sxs-lookup"><span data-stu-id="b5390-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="b5390-124">Se il pacchetto viene installato in un progetto destinato a una versione precedente di tali 2 Framework, o qualsiasi altro framework, verrà installato RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="b5390-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="b5390-125">Non c'è Nessuna ereditarietà tra gruppi.</span><span class="sxs-lookup"><span data-stu-id="b5390-125">There is no inheritance between groups.</span></span> <span data-ttu-id="b5390-126">Se corrisponde al framework di destinazione di un progetto di `targetFramework` attributo di un gruppo, solo le dipendenze all'interno di tale gruppo verrà installato.</span><span class="sxs-lookup"><span data-stu-id="b5390-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="b5390-127">Un pacchetto è possibile specificare le dipendenze del pacchetto in uno dei due formati: il formato precedente di un elenco semplice di `<dependency>` elementi o gruppi.</span><span class="sxs-lookup"><span data-stu-id="b5390-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="b5390-128">Se il `<group>` formato viene usato, il pacchetto non può essere installato nelle versioni di NuGet precedenti alla 2.0.</span><span class="sxs-lookup"><span data-stu-id="b5390-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="b5390-129">Si noti che i due formati non è consentito combinare.</span><span class="sxs-lookup"><span data-stu-id="b5390-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="b5390-130">Ad esempio, è il seguente frammento **valido** e vengono rifiutati da NuGet.</span><span class="sxs-lookup"><span data-stu-id="b5390-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="b5390-131">Raggruppamento di file di contenuto e gli script di PowerShell dal framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="b5390-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="b5390-132">Oltre ai riferimenti di assembly, i file di contenuto e script di PowerShell anche possono essere raggruppati per framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b5390-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="b5390-133">La stessa struttura di cartelle trovato nel `lib` cartella per la specifica di framework di destinazione è ora possibile applicare nello stesso modo per il `content` e `tools` cartelle.</span><span class="sxs-lookup"><span data-stu-id="b5390-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="b5390-134">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b5390-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="b5390-135">**Nota**: poiché `init.ps1` viene eseguita a livello di soluzione e permane non dipendente da qualsiasi singolo progetto, deve essere inserito direttamente sotto il `tools` cartella.</span><span class="sxs-lookup"><span data-stu-id="b5390-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="b5390-136">Se posizionata all'interno di una cartella specifica del framework, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="b5390-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="b5390-137">Inoltre, una nuova funzionalità di NuGet 2.0 è che può essere una cartella framework *vuoto*, nel qual caso, NuGet non aggiungere riferimenti ad assembly, aggiungere i file di contenuto o eseguire gli script di PowerShell per la versione del framework specifico.</span><span class="sxs-lookup"><span data-stu-id="b5390-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="b5390-138">Nell'esempio precedente, la cartella `content\net40` è vuoto.</span><span class="sxs-lookup"><span data-stu-id="b5390-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="b5390-139">Prestazioni di completamento tab migliorato</span><span class="sxs-lookup"><span data-stu-id="b5390-139">Improved tab completion performance</span></span>
<span data-ttu-id="b5390-140">La funzionalità di completamento della scheda nella Console di gestione pacchetti NuGet è stata aggiornata per migliorare significativamente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b5390-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="b5390-141">Ci sarà molto meno ritardo dal momento in cui che viene premuto il tasto tab fino a quando non viene visualizzato l'elenco a discesa di suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="b5390-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b5390-142">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="b5390-142">Bug Fixes</span></span>
<span data-ttu-id="b5390-143">NuGet 2.0 include varie correzioni di bug con particolare attenzione alle prestazioni e il consenso di ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b5390-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="b5390-144">Per un elenco completo di lavoro gli elementi corretti in NuGet 2.0, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b5390-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
