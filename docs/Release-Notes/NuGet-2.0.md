---
title: Note sulla versione di NuGet 2.0 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 2.0, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.0 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="a71eb-104">Note sulla versione 2.0 di NuGet</span><span class="sxs-lookup"><span data-stu-id="a71eb-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="a71eb-105">[Note sulla versione 1.8 NuGet](../release-notes/nuget-1.8.md) | [note sulla versione 2.1 di NuGet](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="a71eb-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="a71eb-106">NuGet 2.0 è stata rilasciata il 19 giugno 2012.</span><span class="sxs-lookup"><span data-stu-id="a71eb-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="a71eb-107">Problema di installazione noti</span><span class="sxs-lookup"><span data-stu-id="a71eb-107">Known Installation Issue</span></span>
<span data-ttu-id="a71eb-108">Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="a71eb-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="a71eb-109">La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a71eb-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="a71eb-110">Vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) per ulteriori informazioni, o [passare direttamente all'hotfix di Visual Studio](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="a71eb-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="a71eb-111">Nota: Se Visual Studio non consente di disinstallare l'estensione (il pulsante di disinstallazione è disabilitato), quindi probabile che sia necessario riavviare Visual Studio utilizzando "Esegui come amministratore".</span><span class="sxs-lookup"><span data-stu-id="a71eb-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="a71eb-112">Consenso di ripristino del pacchetto è ora attivo</span><span class="sxs-lookup"><span data-stu-id="a71eb-112">Package restore consent is now active</span></span>

<span data-ttu-id="a71eb-113">Come descritto in questo [post nel pacchetto ripristino consenso](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 verrà ora richiesto il consenso per abilitare ripristino del pacchetto passare alla modalità online e scaricare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="a71eb-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="a71eb-114">Verificare di aver fornito il consenso tramite la finestra di dialogo pacchetto configuration manager o la variabile di ambiente EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="a71eb-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="a71eb-115">Gruppo di dipendenze da Framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="a71eb-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="a71eb-116">A partire dalla versione 2.0, pacchetto dipendenze possono variare in base al profilo del framework del progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a71eb-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="a71eb-117">Questa operazione viene eseguita utilizzando una versione aggiornata `.nuspec` dello schema.</span><span class="sxs-lookup"><span data-stu-id="a71eb-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="a71eb-118">Il `<dependencies>` elemento ora può contenere un set di `<group>` elementi.</span><span class="sxs-lookup"><span data-stu-id="a71eb-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="a71eb-119">Ogni gruppo che contiene zero o più `<dependency>` elementi e un `targetFramework` attributo.</span><span class="sxs-lookup"><span data-stu-id="a71eb-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="a71eb-120">Se il framework di destinazione è compatibile con il profilo del framework di destinazione progetto, vengono installate insieme tutte le dipendenze all'interno di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="a71eb-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="a71eb-121">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a71eb-121">For example:</span></span>

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

<span data-ttu-id="a71eb-122">Si noti che un gruppo può contenere **zero** dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a71eb-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="a71eb-123">Nell'esempio precedente, se il pacchetto è installato in un progetto destinato a Silverlight 3.0 o versione successiva, non verrà installata alcuna dipendenza.</span><span class="sxs-lookup"><span data-stu-id="a71eb-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="a71eb-124">Se il pacchetto è installato in un progetto destinato a .NET 4.0 o versioni successive, è possibile che due dipendenze, jQuery e WebActivator, verranno installate.</span><span class="sxs-lookup"><span data-stu-id="a71eb-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="a71eb-125">Se il pacchetto viene installato in un progetto destinato a una versione precedente di questi 2 Framework, o qualsiasi altro framework, RouteMagic 1.1.0 verrà installato.</span><span class="sxs-lookup"><span data-stu-id="a71eb-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="a71eb-126">C'è ereditarietà tra i gruppi.</span><span class="sxs-lookup"><span data-stu-id="a71eb-126">There is no inheritance between groups.</span></span> <span data-ttu-id="a71eb-127">Se corrisponde al framework di destinazione di un progetto di `targetFramework` verrà installato l'attributo di un gruppo, solo le dipendenze all'interno di tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="a71eb-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="a71eb-128">Un pacchetto è possibile specificare le dipendenze dei pacchetti in uno dei due formati: il formato precedente di un elenco semplice di `<dependency>` elementi o gruppi.</span><span class="sxs-lookup"><span data-stu-id="a71eb-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="a71eb-129">Se il `<group>` viene usato il formato, il pacchetto non può essere installato in versioni precedenti alla 2.0 di NuGet.</span><span class="sxs-lookup"><span data-stu-id="a71eb-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="a71eb-130">Si noti che i due formati non è consentito combinare.</span><span class="sxs-lookup"><span data-stu-id="a71eb-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="a71eb-131">Ad esempio, il frammento di codice seguente è **valido** e vengono rifiutati da NuGet.</span><span class="sxs-lookup"><span data-stu-id="a71eb-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="a71eb-132">Raggruppamento di file di contenuto e gli script di PowerShell per il framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="a71eb-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="a71eb-133">Oltre ai riferimenti agli assembly, i file di contenuto e gli script di PowerShell inoltre possono essere raggruppati per framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a71eb-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="a71eb-134">La stessa struttura di cartelle, vedere il `lib` cartella per la specifica di .NET framework di destinazione può essere applicato a questo punto nello stesso modo per il `content` e `tools` cartelle.</span><span class="sxs-lookup"><span data-stu-id="a71eb-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="a71eb-135">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a71eb-135">For example:</span></span>

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

<span data-ttu-id="a71eb-136">**Nota**: poiché `init.ps1` viene eseguita a livello di soluzione e viene non dipendente da un singolo progetto, deve essere inserito direttamente sotto il `tools` cartella.</span><span class="sxs-lookup"><span data-stu-id="a71eb-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="a71eb-137">Se inserito in una cartella specifica del framework, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="a71eb-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="a71eb-138">Inoltre, una nuova funzionalità di NuGet 2.0 è che può essere una cartella per framework *vuoto*, nel qual caso NuGet verrà non aggiungere riferimenti ad assembly, aggiungere i file di contenuto o eseguire gli script di PowerShell per la versione di framework specifici.</span><span class="sxs-lookup"><span data-stu-id="a71eb-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="a71eb-139">Nell'esempio precedente, la cartella `content\net40` è vuoto.</span><span class="sxs-lookup"><span data-stu-id="a71eb-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="a71eb-140">Prestazioni di completamento tab migliorato</span><span class="sxs-lookup"><span data-stu-id="a71eb-140">Improved tab completion performance</span></span>
<span data-ttu-id="a71eb-141">Questa funzionalità nella Console di gestione pacchetti NuGet è stata aggiornata per migliorare significativamente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="a71eb-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="a71eb-142">Esistere molto meno tempo dal momento in cui che viene premuto il tasto tab fino a quando non viene visualizzato l'elenco a discesa di suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="a71eb-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a71eb-143">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="a71eb-143">Bug Fixes</span></span>
<span data-ttu-id="a71eb-144">NuGet 2.0 include varie correzioni di bug con particolare attenzione alle prestazioni e di consenso di ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a71eb-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="a71eb-145">Per un elenco completo di lavoro gli elementi corretti in NuGet 2.0, visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a71eb-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
