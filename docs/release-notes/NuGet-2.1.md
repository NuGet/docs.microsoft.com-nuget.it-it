---
title: Note sulla versione di NuGet 2,1
description: Note sulla versione per NuGet 2,1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777024"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="cc230-103">Note sulla versione di NuGet 2,1</span><span class="sxs-lookup"><span data-stu-id="cc230-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="cc230-104">Note sulla versione di [NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Note sulla versione di NuGet 2,2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="cc230-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="cc230-105">NuGet 2,1 è stato rilasciato il 4 ottobre 2012.</span><span class="sxs-lookup"><span data-stu-id="cc230-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="cc230-106">Nuget.Config gerarchico</span><span class="sxs-lookup"><span data-stu-id="cc230-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="cc230-107">NuGet 2,1 offre una maggiore flessibilità nel controllo delle impostazioni di NuGet in modo ricorsivo la struttura di cartelle che cerca `NuGet.Config` i file e quindi compila la configurazione dal set di tutti i file trovati.</span><span class="sxs-lookup"><span data-stu-id="cc230-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="cc230-108">Si consideri ad esempio uno scenario in cui un team ha un repository di pacchetti interno per le compilazioni CI di altre dipendenze interne.</span><span class="sxs-lookup"><span data-stu-id="cc230-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="cc230-109">La struttura di cartelle per un singolo progetto potrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="cc230-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="cc230-110">Inoltre, se il ripristino dei pacchetti è abilitato per la soluzione, sarà disponibile anche la cartella seguente:</span><span class="sxs-lookup"><span data-stu-id="cc230-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="cc230-111">Per fare in modo che il repository dei pacchetti interno del team sia disponibile per tutti i progetti su cui il team lavora, senza renderlo disponibile per ogni progetto nel computer, è possibile creare un nuovo file di Nuget.Config e inserirlo nella cartella c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="cc230-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="cc230-112">Non esiste alcun modo per la specifica di una cartella di pacchetti per ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="cc230-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="cc230-113">È ora possibile vedere che l'origine è stata aggiunta eseguendo il comando ' nuget.exe sources ' da qualsiasi cartella sotto c:\myteam, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cc230-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Origini pacchetti dalla configurazione di NuGet padre](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="cc230-115">`NuGet.Config` i file vengono cercati nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="cc230-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="cc230-116">Percorso ricorsivo dalla cartella del progetto alla radice</span><span class="sxs-lookup"><span data-stu-id="cc230-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="cc230-117">Globale `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="cc230-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="cc230-118">Le configurazioni vengono applicate in *ordine inverso*, vale a dire che in base all'ordinamento precedente, viene applicata prima l'Nuget.Config globale, seguita dalla Nuget.Config file individuati dalla radice alla cartella del progetto, seguiti da `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="cc230-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="cc230-119">Questa operazione è particolarmente importante se si usa l' `<clear/>` elemento per rimuovere un set di elementi dalla configurazione.</span><span class="sxs-lookup"><span data-stu-id="cc230-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="cc230-120">Specificare il percorso della cartella ' Packages '</span><span class="sxs-lookup"><span data-stu-id="cc230-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="cc230-121">In passato, NuGet ha gestito i pacchetti di una soluzione da una cartella "Packages" nota trovata sotto la cartella radice della soluzione.</span><span class="sxs-lookup"><span data-stu-id="cc230-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="cc230-122">Per i team di sviluppo con diverse soluzioni con pacchetti NuGet installati, questo può comportare l'installazione dello stesso pacchetto in molte posizioni diverse sul file system.</span><span class="sxs-lookup"><span data-stu-id="cc230-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="cc230-123">NuGet 2,1 fornisce un controllo più granulare sul percorso della cartella dei pacchetti tramite l' `repositoryPath` elemento nel `NuGet.Config` file.</span><span class="sxs-lookup"><span data-stu-id="cc230-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="cc230-124">Basandosi sull'esempio precedente di supporto gerarchico Nuget.Config, si supponga di voler fare in modo che tutti i progetti in C:\myteam\ condividano la stessa cartella pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cc230-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="cc230-125">A tale scopo, aggiungere semplicemente la voce seguente a `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="cc230-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="cc230-126">In questo esempio, il `Nuget.Config` file condiviso specifica una cartella di pacchetti condivisi per ogni progetto creato al di sotto di C:\myteam, indipendentemente dalla profondità.</span><span class="sxs-lookup"><span data-stu-id="cc230-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="cc230-127">Si noti che se si dispone di una cartella pacchetti esistente sotto la radice della soluzione, è necessario eliminarla prima che NuGet inserisca i pacchetti nella nuova posizione.</span><span class="sxs-lookup"><span data-stu-id="cc230-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="cc230-128">Supporto per le librerie portabili</span><span class="sxs-lookup"><span data-stu-id="cc230-128">Support for Portable Libraries</span></span>

<span data-ttu-id="cc230-129">Le [librerie](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) portabili sono una funzionalità introdotta per la prima volta con .NET 4 che consente di compilare assembly che possono funzionare senza modifiche su diverse piattaforme Microsoft, da versioni di The.NET Framework a Silverlight a Windows Phone e persino a Xbox 360 (anche se al momento, NuGet non supporta la destinazione della libreria portabile Xbox).</span><span class="sxs-lookup"><span data-stu-id="cc230-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="cc230-130">Estendendo le [convenzioni dei pacchetti](../create-packages/supporting-multiple-target-frameworks.md) per le versioni e i profili del Framework, NuGet 2,1 supporta ora le librerie portabili consentendo di creare pacchetti con cartelle di destinazione del profilo e del Framework composto `lib` .</span><span class="sxs-lookup"><span data-stu-id="cc230-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="cc230-131">Si considerino, ad esempio, le piattaforme di destinazione disponibili della libreria di classi portabile seguenti.</span><span class="sxs-lookup"><span data-stu-id="cc230-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Finestra di dialogo Creazione libreria portabile](./media/releasenotes-21-plib.png)

<span data-ttu-id="cc230-133">Dopo che la libreria è stata compilata e il comando `nuget.exe pack MyPortableProject.csproj` è stato eseguito, è possibile visualizzare la nuova struttura di cartelle dei pacchetti della libreria portabile esaminando il contenuto del pacchetto NuGet generato.</span><span class="sxs-lookup"><span data-stu-id="cc230-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Layout del pacchetto della libreria portatile](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="cc230-135">Come si può notare, la convenzione relativa al nome della cartella della libreria portabile segue il modello ' Portable-{Framework 1} + {Framework n}', in cui gli identificatori del Framework seguono le [convenzioni di versione e il nome del Framework](../reference/target-frameworks.md)esistente.</span><span class="sxs-lookup"><span data-stu-id="cc230-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="cc230-136">Un'eccezione alle convenzioni di nome e versione è disponibile nell'identificatore del Framework usato per Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="cc230-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="cc230-137">Questo moniker deve usare il nome di Framework ' wp ' (WP7, wp71 o WP8).</span><span class="sxs-lookup"><span data-stu-id="cc230-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="cc230-138">Se si usa ' Silverlight-WP7', ad esempio, verrà generato un errore.</span><span class="sxs-lookup"><span data-stu-id="cc230-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="cc230-139">Quando si installa il pacchetto creato da questa struttura di cartelle, NuGet è ora in grado di applicare le regole del Framework e del profilo a più destinazioni, come specificato nel nome della cartella.</span><span class="sxs-lookup"><span data-stu-id="cc230-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="cc230-140">Dietro le regole di corrispondenza di NuGet è il principio che gli obiettivi "più specifici" avranno la precedenza su quelli "meno specifici".</span><span class="sxs-lookup"><span data-stu-id="cc230-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="cc230-141">Ciò significa che i moniker destinati a una piattaforma specifica verranno sempre preferiti rispetto a quelli portabili se sono entrambi compatibili con un progetto.</span><span class="sxs-lookup"><span data-stu-id="cc230-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="cc230-142">Inoltre, se più destinazioni portabili sono compatibili con un progetto, NuGet preferisce quello in cui il set di piattaforme supportate è "più vicino" al progetto che fa riferimento al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc230-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="cc230-143">Destinazione di progetti Windows 8 e Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="cc230-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="cc230-144">Oltre ad aggiungere il supporto per la destinazione dei progetti di libreria portabile, NuGet 2,1 fornisce nuovi moniker di Framework per i progetti Windows 8 Store e Windows Phone 8, oltre ad alcuni nuovi moniker generali per i progetti Windows Store e Windows Phone che saranno più facili da gestire nelle versioni future delle rispettive piattaforme.</span><span class="sxs-lookup"><span data-stu-id="cc230-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="cc230-145">Per le applicazioni Windows 8 Store, gli identificatori hanno un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cc230-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="cc230-146">NuGet 2,0 e versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="cc230-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="cc230-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="cc230-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="cc230-148">winRT45, . NETCore45</span><span class="sxs-lookup"><span data-stu-id="cc230-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="cc230-149">Windows, Windows8, Win, Win8</span><span class="sxs-lookup"><span data-stu-id="cc230-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="cc230-150">Per i progetti Windows Phone, gli identificatori hanno un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cc230-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="cc230-151">Sistema operativo telefono</span><span class="sxs-lookup"><span data-stu-id="cc230-151">Phone OS</span></span> | <span data-ttu-id="cc230-152">NuGet 2,0 e versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="cc230-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="cc230-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="cc230-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc230-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="cc230-154">Windows Phone 7</span></span> | <span data-ttu-id="cc230-155">silverlight3-WP</span><span class="sxs-lookup"><span data-stu-id="cc230-155">silverlight3-wp</span></span> | <span data-ttu-id="cc230-156">WP, WP7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="cc230-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="cc230-157">Windows Phone 7,5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="cc230-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="cc230-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="cc230-158">silverlight4-wp71</span></span> | <span data-ttu-id="cc230-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="cc230-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="cc230-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="cc230-160">Windows Phone 8</span></span> | <span data-ttu-id="cc230-161">(non supportato)</span><span class="sxs-lookup"><span data-stu-id="cc230-161">(not supported)</span></span> | <span data-ttu-id="cc230-162">WP8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="cc230-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="cc230-163">In tutte le modifiche precedenti, i nomi di Framework precedenti continueranno a essere completamente supportati da NuGet 2,1.</span><span class="sxs-lookup"><span data-stu-id="cc230-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="cc230-164">In futuro, è consigliabile usare i nuovi nomi perché saranno più stabili nelle versioni future delle rispettive piattaforme.</span><span class="sxs-lookup"><span data-stu-id="cc230-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="cc230-165">I nuovi nomi *non* saranno supportati nelle versioni di NuGet precedenti alla 2,1, quindi pianificare di conseguenza il momento in cui eseguire l'opzione.</span><span class="sxs-lookup"><span data-stu-id="cc230-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="cc230-166">Miglioramento della ricerca nella finestra di dialogo Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="cc230-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="cc230-167">Nel corso delle diverse iterazioni sono state introdotte modifiche alla raccolta NuGet che hanno migliorato notevolmente la velocità e la pertinenza delle ricerche di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cc230-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="cc230-168">Tuttavia, questi miglioramenti erano limitati al sito Web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cc230-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="cc230-169">NuGet 2,1 rende disponibile l'esperienza di ricerca migliorata tramite la finestra di dialogo Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc230-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="cc230-170">Si supponga, ad esempio, di voler trovare il pacchetto di anteprima di Caching di Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="cc230-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="cc230-171">Una query di ricerca ragionevole per questo pacchetto può essere "cache di Azure".</span><span class="sxs-lookup"><span data-stu-id="cc230-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="cc230-172">Nelle versioni precedenti della finestra di dialogo Gestione pacchetti, il pacchetto desiderato non è incluso nella prima pagina di risultati.</span><span class="sxs-lookup"><span data-stu-id="cc230-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="cc230-173">Tuttavia, in NuGet 2,1, il pacchetto desiderato ora viene visualizzato nella parte superiore dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="cc230-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Finestra di dialogo Gestione pacchetti-ricerca](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="cc230-175">Forza aggiornamento pacchetto</span><span class="sxs-lookup"><span data-stu-id="cc230-175">Force Package Update</span></span>

<span data-ttu-id="cc230-176">Prima di NuGet 2,1, NuGet ignorava l'aggiornamento di un pacchetto in assenza di un numero di versione elevato.</span><span class="sxs-lookup"><span data-stu-id="cc230-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="cc230-177">Questo ha introdotto un attrito per determinati scenari, in particolare nel caso di scenari di compilazione o CI in cui il team non ha voluto incrementare il numero di versione del pacchetto con ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="cc230-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="cc230-178">Il comportamento desiderato consisteva nel forzare un aggiornamento indipendentemente da.</span><span class="sxs-lookup"><span data-stu-id="cc230-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="cc230-179">NuGet 2,1 risolve questo problema con il flag ' reinstall '.</span><span class="sxs-lookup"><span data-stu-id="cc230-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="cc230-180">Ad esempio, le versioni precedenti di NuGet generano quanto segue quando si tenta di aggiornare un pacchetto che non dispone di una versione più recente del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="cc230-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="cc230-181">Con il flag REINSTALL, il pacchetto verrà aggiornato indipendentemente dal fatto che sia presente una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="cc230-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="cc230-182">Un altro scenario in cui il flag di reinstallazione dimostra vantaggioso è quello della ridefinizione della destinazione del Framework.</span><span class="sxs-lookup"><span data-stu-id="cc230-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="cc230-183">Quando si modifica il Framework di destinazione di un progetto, ad esempio da .NET 4 a .NET 4,5, Update-Package-REINSTALL può aggiornare i riferimenti agli assembly corretti per tutti i pacchetti NuGet installati nel progetto.</span><span class="sxs-lookup"><span data-stu-id="cc230-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="cc230-184">Modificare le origini del pacchetto in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc230-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="cc230-185">Nelle versioni precedenti di NuGet, per aggiornare un'origine del pacchetto dalla finestra di dialogo Opzioni di Visual Studio, è necessario eliminare e aggiungere nuovamente l'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc230-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="cc230-186">NuGet 2,1 migliora questo flusso di lavoro supportando Update come una funzione di prima classe dell'interfaccia utente di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cc230-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Finestra di dialogo di configurazione di gestione pacchetti](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="cc230-188">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="cc230-188">Bug Fixes</span></span>

<span data-ttu-id="cc230-189">NuGet 2,1 include numerose correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="cc230-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="cc230-190">Per un elenco completo degli elementi di lavoro corretti in NuGet 2,0, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="cc230-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
