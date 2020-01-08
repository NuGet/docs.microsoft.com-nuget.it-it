---
title: Note sulla versione di NuGet 2,0
description: Note sulla versione per NuGet 2,0, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383067"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="b52b8-103">Note sulla versione di NuGet 2,0</span><span class="sxs-lookup"><span data-stu-id="b52b8-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="b52b8-104">[Note sulla versione di nuget 1,8](../release-notes/nuget-1.8.md) | [Note sulla versione di NuGet 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="b52b8-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="b52b8-105">NuGet 2,0 è stato rilasciato il 19 giugno 2012.</span><span class="sxs-lookup"><span data-stu-id="b52b8-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="b52b8-106">Problema di installazione noto</span><span class="sxs-lookup"><span data-stu-id="b52b8-106">Known Installation Issue</span></span>
<span data-ttu-id="b52b8-107">Se si esegue VS 2010 SP1, potrebbe essere rilevato un errore di installazione quando si tenta di aggiornare NuGet se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="b52b8-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="b52b8-108">La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b52b8-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="b52b8-109">Per ulteriori informazioni, vedere <https://support.microsoft.com/kb/2581019> o [passare direttamente all'hotfix di Visual](http://bit.ly/vsixcertfix)Studio.</span><span class="sxs-lookup"><span data-stu-id="b52b8-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="b52b8-110">Nota: se Visual Studio non consente di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), probabilmente è necessario riavviare Visual Studio usando "Esegui come amministratore".</span><span class="sxs-lookup"><span data-stu-id="b52b8-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="b52b8-111">Il consenso per il ripristino del pacchetto è ora attivo</span><span class="sxs-lookup"><span data-stu-id="b52b8-111">Package restore consent is now active</span></span>

<span data-ttu-id="b52b8-112">Come descritto in questo [post relativo al consenso per il ripristino dei pacchetti](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 richiederà il consenso per consentire il ripristino del pacchetto in modo che possa andare online e scaricare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="b52b8-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="b52b8-113">Assicurarsi che sia stato fornito il consenso tramite la finestra di dialogo di configurazione di gestione pacchetti o la variabile di ambiente EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="b52b8-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="b52b8-114">Raggruppare le dipendenze per Framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="b52b8-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="b52b8-115">A partire dalla versione 2,0, le dipendenze dei pacchetti possono variare in base al profilo del Framework del progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b52b8-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="b52b8-116">Questa operazione viene eseguita utilizzando uno schema `.nuspec` aggiornato.</span><span class="sxs-lookup"><span data-stu-id="b52b8-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="b52b8-117">L'elemento `<dependencies>` ora può contenere un set di `<group>` elementi.</span><span class="sxs-lookup"><span data-stu-id="b52b8-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="b52b8-118">Ogni gruppo contiene zero o più elementi `<dependency>` e un attributo `targetFramework`.</span><span class="sxs-lookup"><span data-stu-id="b52b8-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="b52b8-119">Tutte le dipendenze all'interno di un gruppo vengono installate insieme se il Framework di destinazione è compatibile con il profilo del Framework del progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b52b8-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="b52b8-120">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b52b8-120">For example:</span></span>

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

<span data-ttu-id="b52b8-121">Si noti che un gruppo può contenere **zero** dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b52b8-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="b52b8-122">Nell'esempio precedente, se il pacchetto viene installato in un progetto destinato a Silverlight 3,0 o versione successiva, non verrà installata alcuna dipendenza.</span><span class="sxs-lookup"><span data-stu-id="b52b8-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="b52b8-123">Se il pacchetto viene installato in un progetto destinato a .NET 4,0 o versione successiva, verranno installati due dipendenze, jQuery e WebActivator.</span><span class="sxs-lookup"><span data-stu-id="b52b8-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="b52b8-124">Se il pacchetto viene installato in un progetto destinato a una versione iniziale di questi due Framework, o qualsiasi altro Framework, verrà installato RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="b52b8-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="b52b8-125">Non esiste alcuna ereditarietà tra i gruppi.</span><span class="sxs-lookup"><span data-stu-id="b52b8-125">There is no inheritance between groups.</span></span> <span data-ttu-id="b52b8-126">Se il Framework di destinazione di un progetto corrisponde all'attributo `targetFramework` di un gruppo, verranno installate solo le dipendenze all'interno di tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="b52b8-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="b52b8-127">Un pacchetto può specificare le dipendenze del pacchetto in uno dei due formati seguenti: il formato precedente di un elenco semplice di elementi `<dependency>` o gruppi.</span><span class="sxs-lookup"><span data-stu-id="b52b8-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="b52b8-128">Se viene usato il formato `<group>`, il pacchetto non può essere installato in versioni di NuGet precedenti alla 2,0.</span><span class="sxs-lookup"><span data-stu-id="b52b8-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="b52b8-129">Si noti che non è consentito combinare i due formati.</span><span class="sxs-lookup"><span data-stu-id="b52b8-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="b52b8-130">Ad esempio, il frammento di codice seguente **non è valido** e verrà rifiutato da NuGet.</span><span class="sxs-lookup"><span data-stu-id="b52b8-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="b52b8-131">Raggruppamento di file di contenuto e script di PowerShell in base a Framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="b52b8-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="b52b8-132">Oltre ai riferimenti agli assembly, i file di contenuto e gli script di PowerShell possono essere raggruppati in base al Framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b52b8-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="b52b8-133">È ora possibile applicare la stessa struttura di cartelle presente nella cartella `lib` per specificare il Framework di destinazione nello stesso modo per le cartelle `content` e `tools`.</span><span class="sxs-lookup"><span data-stu-id="b52b8-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="b52b8-134">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b52b8-134">For example:</span></span>

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

<span data-ttu-id="b52b8-135">**Nota**: poiché `init.ps1` viene eseguita a livello di soluzione e non dipende da un singolo progetto, deve essere inserita direttamente nella cartella `tools`.</span><span class="sxs-lookup"><span data-stu-id="b52b8-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="b52b8-136">Se inserito in una cartella specifica del Framework, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="b52b8-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="b52b8-137">Inoltre, una nuova funzionalità di NuGet 2,0 è che una cartella del Framework può essere *vuota*. in questo caso, NuGet non aggiunge i riferimenti ad assembly, aggiunge i file di contenuto o esegue script di PowerShell per la versione specifica del Framework.</span><span class="sxs-lookup"><span data-stu-id="b52b8-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="b52b8-138">Nell'esempio precedente la cartella `content\net40` è vuota.</span><span class="sxs-lookup"><span data-stu-id="b52b8-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="b52b8-139">Miglioramento delle prestazioni di completamento tramite TAB</span><span class="sxs-lookup"><span data-stu-id="b52b8-139">Improved tab completion performance</span></span>
<span data-ttu-id="b52b8-140">La funzionalità di completamento tramite TAB nella console di gestione pacchetti NuGet è stata aggiornata per migliorare significativamente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b52b8-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="b52b8-141">Si verifica un ritardo molto inferiore dal momento in cui viene premuto il tasto TAB fino a quando non viene visualizzato l'elenco a discesa dei suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="b52b8-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b52b8-142">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="b52b8-142">Bug Fixes</span></span>
<span data-ttu-id="b52b8-143">NuGet 2,0 include molte correzioni di bug con particolare attenzione al consenso e alle prestazioni per il ripristino dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="b52b8-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="b52b8-144">Per un elenco completo degli elementi di lavoro corretti in NuGet 2,0, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b52b8-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
