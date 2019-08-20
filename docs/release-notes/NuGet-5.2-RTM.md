---
title: Note sulla versione di NuGet 5,2 RTM
description: Note sulla versione per NuGet 5,2, incluse nuove funzionalità, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471184"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="85fd7-103">Note sulla versione di NuGet 5,2</span><span class="sxs-lookup"><span data-stu-id="85fd7-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="85fd7-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="85fd7-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="85fd7-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="85fd7-105">NuGet version</span></span> | <span data-ttu-id="85fd7-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="85fd7-106">Available in Visual Studio version</span></span>| <span data-ttu-id="85fd7-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="85fd7-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="85fd7-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="85fd7-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="85fd7-109">Visual Studio 2019 versione 16,2</span><span class="sxs-lookup"><span data-stu-id="85fd7-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="85fd7-110">[2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1) <sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="85fd7-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="85fd7-111"><sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="85fd7-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="85fd7-112"><sup>2</sup> Disponibile come installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="85fd7-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="85fd7-113">Riepilogo: Novità di 5,2</span><span class="sxs-lookup"><span data-stu-id="85fd7-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="85fd7-114">Correzione di un bug critico che ha causato errori di operazioni NuGet occasionali a causa di problemi di percorso in Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="85fd7-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="85fd7-115">Velocità di risposta dell'interfaccia utente migliorata quando si esplorano i pacchetti usando l'interfaccia utente di gestione pacchetti NuGet in Visual Studio particolarmente evidente per le origini lente- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="85fd7-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="85fd7-116">Tonnellate di correzioni di affidabilità per il file di blocco ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) e il plug-in di autenticazione ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span><span class="sxs-lookup"><span data-stu-id="85fd7-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="85fd7-117">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="85fd7-117">Issues fixed in this release</span></span>

<span data-ttu-id="85fd7-118">**Bug**</span><span class="sxs-lookup"><span data-stu-id="85fd7-118">**Bugs**</span></span>

* <span data-ttu-id="85fd7-119">Prestazioni Console di gestione pacchetti:  Aggiornamento temporizzato dell'interfaccia utente "progetto predefinito" valore selezionato casella combinata- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="85fd7-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="85fd7-120">Prestazioni Miglioramenti delle prestazioni nell'interfaccia utente di PM- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="85fd7-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="85fd7-121">Prestazioni Ritardo dell'interfaccia utente durante la lettura del progetto predefinito in PMC- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="85fd7-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="85fd7-122">Prestazioni: [vsfeedback] la scheda aggiornamento NuGet si blocca per un'origine pacchetto locale- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="85fd7-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="85fd7-123">Plug-in  NuGet attende il timeout di handshake completo se il plug-in non viene avviato o termina in anticipo [#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="85fd7-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="85fd7-124">Plug-in: migliorare la diagnostica dell'errore di avvio del plug- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="85fd7-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="85fd7-125">Plug-in Problema relativo all'individuazione di NuGet. exe dei plug-in predefiniti- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="85fd7-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="85fd7-126">Plug-in: il file di cache non è mai letto [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="85fd7-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="85fd7-127">Plug-in  "Un'attività è stata annullata".</span><span class="sxs-lookup"><span data-stu-id="85fd7-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="85fd7-128">errori con il plug-in di autenticazione durante il ripristino- [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="85fd7-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="85fd7-129">Cache di plug-in non individuabile in modo intermittente nelle piattaforme Linux: [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="85fd7-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="85fd7-130">LockFile: con ATF, ha false NU1004 a causa di un controllo di uguaglianza del Framework di destinazione non valido. [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="85fd7-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="85fd7-131">LockFile: il flag di ripristino "--Locked-Mode" non è rispettato se il file di blocco è vuoto o non valido [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="85fd7-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="85fd7-132">LockFile Non è necessario che i progetti minuscoli con nomi di assembly personalizzati nei pacchetti blocchino [#8114](https://github.com/NuGet/Home/issues/8114) file</span><span class="sxs-lookup"><span data-stu-id="85fd7-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="85fd7-133">LockFile Crea riferimento a progetto in minuscolo nel file di blocco- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="85fd7-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="85fd7-134">Ripristino: l'installazione di un pacchetto con firma manomessa comporta più tentativi di installazione non riusciti (con output ripetuto)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="85fd7-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="85fd7-135">VS: le opzioni utente della soluzione non vengono deserializzate dopo l'aggiornamento di NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="85fd7-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="85fd7-136">DotNet-list-package in un progetto UnitTest restituisce un errore [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="85fd7-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="85fd7-137">Creare un gruppo di pacchetti NuGet per Visual Studio Installer-correzione di alcuni problemi di configurazione VSIX- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="85fd7-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="85fd7-138">GeneratePackageOnBuild non deve impostare nobuild.</span><span class="sxs-lookup"><span data-stu-id="85fd7-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="85fd7-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="85fd7-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="85fd7-140">La nuova opzione "-SymbolPackageFormat snupkg" genera un errore quando il file con estensione NuSpec contiene un elemento di riferimento esplicito all'assembly [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="85fd7-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="85fd7-141">NuGet. targets (498, 5): errore: Impossibile trovare una parte del percorso '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="85fd7-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="85fd7-142">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="85fd7-142">**DCR:**</span></span>

* <span data-ttu-id="85fd7-143">Aggiungere una proprietà di MSBuild che indica che PackageDownload è supportato- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="85fd7-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="85fd7-144">FrameworkReference disattivare il flusso delle dipendenze tramite FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="85fd7-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="85fd7-145">Meccanismo per fornire Runtime. JSON all'esterno di un pacchetto- [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="85fd7-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="85fd7-146">**[Elenco di tutti i problemi risolti in questa versione-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="85fd7-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


