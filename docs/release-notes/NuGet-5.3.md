---
title: Note sulla versione di NuGet 5,3
description: Note sulla versione per NuGet 5,3, incluse nuove funzionalità, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 683ee7d1bef30d0a7414ec1694a9735d79b2ab45
ms.sourcegitcommit: c529f5944868a0692ca8550b716a73e05df0ccbf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2019
ms.locfileid: "71687894"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="6445c-103">Note sulla versione di NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="6445c-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="6445c-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="6445c-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="6445c-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="6445c-105">NuGet version</span></span> | <span data-ttu-id="6445c-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6445c-106">Available in Visual Studio version</span></span>| <span data-ttu-id="6445c-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6445c-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="6445c-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="6445c-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="6445c-109">Visual Studio 2019 versione 16,3</span><span class="sxs-lookup"><span data-stu-id="6445c-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="6445c-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="6445c-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="6445c-111"><sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="6445c-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="6445c-112">Riepilogo: Novità di 5,3</span><span class="sxs-lookup"><span data-stu-id="6445c-112">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="6445c-113">[L'icona del pacchetto può essere incorporata nel pacchetto](../reference/msbuild-targets.md#packing-an-icon-image-file), anziché richiedere un URL esterno.</span><span class="sxs-lookup"><span data-stu-id="6445c-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="6445c-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="6445c-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="6445c-115">Sicurezza migliorata con il rilevamento e l'imposizione di SHA per Packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="6445c-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="6445c-116">Abilitare la deprecazione dei pacchetti NuGet obsoleti/legacy [#2867](https://github.com/NuGet/Home/issues/2867) | [post di Blog](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span><span class="sxs-lookup"><span data-stu-id="6445c-116">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="6445c-117">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="6445c-117">Issues fixed in this release</span></span>

<span data-ttu-id="6445c-118">**Bug**</span><span class="sxs-lookup"><span data-stu-id="6445c-118">**Bugs**</span></span>

* <span data-ttu-id="6445c-119">I pacchetti NuGet prodotti con 3.0.100-preview9 SDK non possono essere usati dagli utenti di 2,2 SDK... a seconda del fuso orario [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="6445c-119">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="6445c-120">"I caratteri nel percorso hanno causato l'errore `nuget restore` " caratteri non validi nel percorso " [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="6445c-120">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="6445c-121">Visual Studio: gli assembly sono completamente NGen-ed non parzialmente NGen-ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="6445c-121">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="6445c-122">Ridurre l'utilizzo della memoria (annullare la sottoscrizione agli eventi)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="6445c-122">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="6445c-123">Il messaggio "Error_UnableToFindProjectInfo" non è grammaticalmente corretto- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="6445c-123">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="6445c-124">Miglioramenti di NU1403: convalida di tutti i pacchetti, inclusi i valori Sha previsti/effettivi [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="6445c-124">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="6445c-125">Enumerazione multipla `NuGetPackageManager.PreviewUpdatePackagesAsync`in  -  [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="6445c-125">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="6445c-126">Annulla la modifica "Public-> Internal" in PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="6445c-126">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="6445c-127">IVsPackageSourceProvider. GetSources (...) ha un comportamento di eccezione definito in modo non corretto- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="6445c-127">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="6445c-128">Rendere pubblico il costruttore PluginManager- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="6445c-128">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="6445c-129">Metriche per tenere traccia della frequenza di aggiornamento dell'interfaccia utente di PM- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="6445c-129">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="6445c-130">Ridurre il numero di aggiornamenti dell'interfaccia utente durante l'installazione tramite l'interfaccia utente di gestione pacchetti- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="6445c-130">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="6445c-131">Telemetria: i valori DateTime usano formati specifici delle impostazioni cultura- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="6445c-131">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="6445c-132">Ridurre gli aggiornamenti dell'interfaccia utente nella scheda Sfoglia dell'interfaccia utente di gestione pacchetti #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="6445c-132">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="6445c-133">[Errore test] "Impossibile analizzare il file di configurazione" richiede due volte [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="6445c-133">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="6445c-134">Genera un errore NU5037 con una pagina del documento corretta che illustra le correzioni dei clienti (nel pacchetto manca il file nuspec necessario)- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="6445c-134">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="6445c-135">Il ripristino in modalità bloccata non riesce quando viene modificato il RuntimeIdentifier di un progetto [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="6445c-135">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="6445c-136">Eseguire la lettura delle impostazioni in VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="6445c-136">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="6445c-137">La regressione `Nuget sources add` in fa sì che il carattere ":", valore esadecimale 0x3A, non possa essere incluso in un nome "Errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="6445c-137">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="6445c-138">Provider di credenziali del plug-in NuGet: nascondere la finestra del processo [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="6445c-138">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="6445c-139">Imponi PackagePathResolver è un percorso assoluto [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="6445c-139">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="6445c-140">Ridurre gli aggiornamenti dell'interfaccia utente nelle schede installa e aggiorna dell'interfaccia utente di gestione pacchetti- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="6445c-140">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="6445c-141">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="6445c-141">**DCR:**</span></span>

* <span data-ttu-id="6445c-142">Aggiornare i Framework Novell per eseguire il mapping a NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="6445c-142">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="6445c-143">Abilitare la copia del contenuto di gestione pacchetti "finestra di anteprima" per l'installazione/aggiornamento [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="6445c-143">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="6445c-144">Abilita ripristino nei file con estensione proj- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="6445c-144">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="6445c-145">Introdurre `NUGET_NETFX_PLUGIN_PATHS` e`NUGET_NETCORE_PLUGIN_PATHS` per supportare la configurazione di entrambi allo stesso tempo- [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="6445c-145">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="6445c-146">Abilitare più versioni per un PackageDownload tramite l'attributo Version [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="6445c-146">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="6445c-147">Opzioni Add-SolutionDirectory e-PackageDirectory per NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="6445c-147">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="6445c-148">**[Elenco di tutti i problemi risolti in questa versione-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="6445c-148">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>