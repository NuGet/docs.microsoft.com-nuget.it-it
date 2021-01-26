---
title: Note sulla versione di 3,5 RC
description: Note sulla versione per NuGet 3,5 RC, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780197"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="8c672-103">Note sulla versione di NuGet 3,5 RC</span><span class="sxs-lookup"><span data-stu-id="8c672-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="8c672-104">Note sulla versione [di NuGet 3,5-beta2](../release-notes/nuget-3.5-Beta2.md)  |  [Note sulla versione di NuGet 3,5-RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="8c672-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="8c672-105">3,5 versione è incentrata sul miglioramento della qualità e delle prestazioni dei client NuGet.</span><span class="sxs-lookup"><span data-stu-id="8c672-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="8c672-106">Sono state inoltre fornite alcune funzionalità come il supporto per le [cartelle di fallback](https://github.com/NuGet/Home/issues/2899), il supporto [PackageType](https://github.com/NuGet/Home/issues/2476) in `.nuspec` e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="8c672-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="8c672-107">Elenco dei problemi</span><span class="sxs-lookup"><span data-stu-id="8c672-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="8c672-108">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="8c672-108">Bug Fixes</span></span>

* <span data-ttu-id="8c672-109">L'installazione o il ripristino di un pacchetto ha esito negativo con "il pacchetto contiene più `.nuspec` file".</span><span class="sxs-lookup"><span data-stu-id="8c672-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="8c672-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="8c672-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="8c672-111">il pacchetto NuGet aggiunge `.tt` in modo forzato i file alla cartella del contenuto indipendentemente dalla [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="8c672-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="8c672-112">NuGet Pack csproj (con `project.json` ) si arresta in modo anomalo se non sono presenti packOptions e Owner nel file JSON [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="8c672-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="8c672-113">il pacchetto NuGet per `project.json` Ignora i tag packOptions come Summary, authors, owners e così via [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="8c672-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="8c672-114">il pacchetto NuGet ignora le dipendenze nell'output `.nuspec` per `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="8c672-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="8c672-115">L'aggiornamento di più pacchetti con rollback lascia il progetto in uno stato di interruzione- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="8c672-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="8c672-116">ContentFiles in any non sono stati aggiunti per i progetti netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="8c672-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="8c672-117">Non è possibile creare un pacchetto della libreria di destinazione .NET standard correttamente- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="8c672-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="8c672-118">File > nuovo progetto-> progetto libreria di classi (portabile) non riesce in VS2015 e Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="8c672-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="8c672-119">Errore NuGet-1.0.0-\* non è una stringa di versione valida- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="8c672-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="8c672-120">Find-Package non viene visualizzato ma Install-Package funziona- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="8c672-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="8c672-121">Errore durante "Install-Package jQuery. Validation" in dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="8c672-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="8c672-122">Quando si esegue l'installazione di Visual Studio 2015 Update 3 su un Visual Studio che usa la versione NuGet 3.5.0 si verifica un errore [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="8c672-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="8c672-123">Interfaccia utente di gestione pacchetti: non Visualizza la nuova versione dopo l'aggiornamento di un pacchetto- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="8c672-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="8c672-124">-ApiKey nella riga di comando DELETE non è stato letto/inviato in 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="8c672-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="8c672-125">Stringa non corretta: una versione stabile di un pacchetto non deve avere una dipendenza della versione provvisoria.</span><span class="sxs-lookup"><span data-stu-id="8c672-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="8c672-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="8c672-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="8c672-127">Creazione dell'eccezione NullRef del progetto PCL (' net46 e Windows 10).</span><span class="sxs-lookup"><span data-stu-id="8c672-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="8c672-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="8c672-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="8c672-129">L'aggiornamento di NuGet deve fornire un messaggio informativo quando una versione più alta è limitata dal vincolo allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="8c672-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="8c672-130">Il plug-in delle credenziali è stato terminato con errore-1/errore durante il download del pacchetto quando si usano i provider di credenziali con più origini [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="8c672-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="8c672-131">pacchetto NuGet-mancata Newtonsoft.Jssulla dipendenza del pacchetto- [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="8c672-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="8c672-132">Bug in ExecuteSynchronizedCore in Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="8c672-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="8c672-133">VS non supporta variabili di ambiente in repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="8c672-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="8c672-134">Risolvere i problemi di accessibilità- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="8c672-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="8c672-135">I Framework portabili con profili con sillabazione vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="8c672-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="8c672-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="8c672-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="8c672-137">Gestione pacchetti NuGet dovrebbe rendere chiaro che l'elenco di opzioni nei pacchetti non si applica ai `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="8c672-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="8c672-138">L'aggiornamento di NuGet 3.3.0 ha esito negativo con ' un vincolo aggiuntivo... definito in packages.config impedisce questa operazione.</span><span class="sxs-lookup"><span data-stu-id="8c672-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="8c672-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="8c672-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="8c672-140">L'installazione di un pacchetto da un'origine locale che non esiste genera un messaggio fasullo [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="8c672-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="8c672-141">Il filtro "Aggiorna disponibili" Mostra gli aggiornamenti che violano il vincolo di versione [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="8c672-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="8c672-142">Miglioramenti alle prestazioni</span><span class="sxs-lookup"><span data-stu-id="8c672-142">Performance Improvements</span></span>

* <span data-ttu-id="8c672-143">Prestazioni: migliorare l'analisi del Framework di destinazione ContentModel- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="8c672-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="8c672-144">Prestazioni: evitare `runtime.json` di leggere i file per i ripristini che non dispongono di rid [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="8c672-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="8c672-145">Nei computer CI, il ripristino di un'applicazione Web ASP.NET di esempio è ridotto da oltre 15 secondi a 3 secondi.</span><span class="sxs-lookup"><span data-stu-id="8c672-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="8c672-146">Prestazioni: la console di gestione pacchetti init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956)tempi di caricamento.</span><span class="sxs-lookup"><span data-stu-id="8c672-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="8c672-147">Il tempo necessario per aprire PackageManagerConsole è migliorato in alcuni casi da 132S a 10s.</span><span class="sxs-lookup"><span data-stu-id="8c672-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="8c672-148">Risolvere i problemi di prestazioni più nitidi nell'aggiornamento [#3044](https://github.com/NuGet/Home/issues/3044)di NuGet: in un progetto di esempio, il tempo necessario per installare i pacchetti è ridotto da 140S a 68S.</span><span class="sxs-lookup"><span data-stu-id="8c672-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="8c672-149">DCR</span><span class="sxs-lookup"><span data-stu-id="8c672-149">DCRs</span></span>

* <span data-ttu-id="8c672-150">NuGet deve informare gli utenti che l'aggiornamento o l'installazione in una libreria PCL basata su DotNet TFM può causare problemi: [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="8c672-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="8c672-151">Avviso di installazione/aggiornamento errato per il progetto w/TFM = "DotNet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="8c672-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="8c672-152">Aggiungere il supporto per netcoreapp11 e netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="8c672-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="8c672-153">Stampa il contenuto dell'intestazione NuGet-Warning nella console di nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="8c672-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="8c672-154">Utilizzare l'attributo AssemblyMetadata per le `.nuspec` sostituzioni di token- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="8c672-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="8c672-155">Rimuovere la proprietà Locked dal file di blocco- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="8c672-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="8c672-156">I pacchetti di simboli non devono mai essere usati in installazione o aggiornamento #2807</span><span class="sxs-lookup"><span data-stu-id="8c672-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="8c672-157">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="8c672-157">Features</span></span>

* <span data-ttu-id="8c672-158">Supporto per le cartelle dei pacchetti di fallback- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="8c672-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="8c672-159">Progettare e implementare una nozione di tipo di pacchetto per supportare pacchetti di strumenti- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="8c672-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="8c672-160">API per ottenere il percorso della cartella dei pacchetti globali- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="8c672-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="8c672-161">Supporto per l'aggiornamento dei pacchetti nativi- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="8c672-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
