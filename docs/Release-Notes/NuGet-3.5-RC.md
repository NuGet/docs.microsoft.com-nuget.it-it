---
title: 3.5 note sulla versione RC | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 75a9b496-5762-48b6-922f-fdddf1369c45
description: "Note sulla versione per NuGet 3.5 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "NuGet 3.5 RC note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09d566de6f53bc0f0ddd8049143dc647f3075671
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
#<a name="35-rc-release-notes"></a><span data-ttu-id="c60d5-104">3.5 note sulla versione RC</span><span class="sxs-lookup"><span data-stu-id="c60d5-104">3.5 RC Release Notes</span></span>

<span data-ttu-id="c60d5-105">[Note sulla versione 3.5 alla versione Beta 2 di NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-note sulla versione RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="c60d5-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="c60d5-106">versione 3.5 è incentrata sul miglioramento della qualità e prestazioni dei client NuGet.</span><span class="sxs-lookup"><span data-stu-id="c60d5-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="c60d5-107">Inoltre, è stato fornito alcune funzionalità come il supporto per [cartelle Fallback](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) supporta in `.nuspec` e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="c60d5-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="c60d5-108">Elenco problemi</span><span class="sxs-lookup"><span data-stu-id="c60d5-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="c60d5-109">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="c60d5-109">Bug Fixes</span></span>

* <span data-ttu-id="c60d5-110">Installazione o il ripristino di un pacchetto ha esito negativo con "pacchetto contiene più `.nuspec` file."</span><span class="sxs-lookup"><span data-stu-id="c60d5-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="c60d5-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="c60d5-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="c60d5-112">pacchetto NuGet aggiunge in modo forzato `.tt` i file di contenuto cartella indipendentemente - [&#3203;](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="c60d5-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="c60d5-113">NuGet pack csproj (con `project.json`) si blocca se sono non presenti packOptions e proprietario nel file JSON - [&#3180;](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="c60d5-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="c60d5-114">pacchetto NuGet per `project.json` ignora i tag packOptions come riepilogo, gli autori e proprietari e così via - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="c60d5-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="c60d5-115">pacchetto NuGet ignora le dipendenze nell'output `.nuspec` per `project.json`  -  [&#3145;](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="c60d5-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="c60d5-116">Aggiornamento di più pacchetti con rollback lascia il progetto in uno stato danneggiato - [&#3139;](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="c60d5-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="c60d5-117">ContentFiles in presenza non vengono aggiunti per i progetti di moniker netstandard - [&#3118;](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="c60d5-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="c60d5-118">Impossibile creare pacchetto libreria per .net Standard correttamente - [&#3108;](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="c60d5-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="c60d5-119">File -> Nuovo progetto -> ha esito negativo al progetto libreria di classi (portabile) VS2015 e Dev15 - [&#3094;](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="c60d5-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="c60d5-120">Errore di NuGet - 1.0.0-* non è una stringa di versione valida - [&#3070;](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="c60d5-120">NuGet error - 1.0.0-* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="c60d5-121">Find-Package ha esito negativo per la visualizzazione, ma il funzionamento di Install-Package - [&#3068;](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="c60d5-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="c60d5-122">Errore quando "Install-Package jquery.validation" in dev15 - [&#3061;](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="c60d5-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="c60d5-123">Quando è installato Visual Studio 2015 update 3 in un Visual Studio che usa NuGet si verifica l'errore di versione 3.5.0 - [&#3053;](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="c60d5-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="c60d5-124">Pacchetto interfaccia utente di gestione: non visualizza una nuova versione dopo aver aggiornato un pacchetto- [&#3041;](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="c60d5-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="c60d5-125">-ApiKey nella riga di comando di eliminazione non viene in lettura/inviata 3.5.0-beta - [&#3037;](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="c60d5-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="c60d5-126">Stringa non corretto: una versione stabile di un pacchetto non deve avere in una versione non definitiva dipendenza.</span><span class="sxs-lookup"><span data-stu-id="c60d5-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="c60d5-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="c60d5-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="c60d5-128">Creazione di get progetto PCL (net46 e windows 10) NullRef eccezione.</span><span class="sxs-lookup"><span data-stu-id="c60d5-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="c60d5-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="c60d5-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="c60d5-130">Aggiornamento di NuGet deve fornire un messaggio informativo quando una versione successiva è limitata dal vincolo di attributo allowedversions valido - [&#3013;](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="c60d5-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="c60d5-131">Plug-in credenziali chiuso con errore -1 / errore di download del pacchetto quando si utilizzano provider di credenziali con più origini - [&#2885;](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="c60d5-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="c60d5-132">pacchetto NuGet - dipendenza di pacchetto mancante newtonsoft - [&#2876;](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="c60d5-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="c60d5-133">Bug in ExecuteSynchronizedCore su Linux/MacOS + Mono - [&#2860;](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="c60d5-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="c60d5-134">Visual Studio non supporta le variabili di ambiente in repositoryPath (nuget.exe non) - [&#2763;](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="c60d5-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="c60d5-135">Risolvere i problemi di accessibilità - [&#2745;](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="c60d5-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="c60d5-136">Framework portabili con profili sillabati vengono rifiutate.</span><span class="sxs-lookup"><span data-stu-id="c60d5-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="c60d5-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="c60d5-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="c60d5-138">Gestione pacchetti NuGet deve mettere in evidenza tale elenco di opzioni in dettaglio non è valida per i pacchetti `project.json`  -  [&#2665;](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="c60d5-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="c60d5-139">NuGet 3.3.0 aggiornamento ha esito negativo con '... un vincolo aggiuntivo definito nel file Packages. config impedisce questa operazione.'</span><span class="sxs-lookup"><span data-stu-id="c60d5-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="c60d5-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="c60d5-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="c60d5-141">L'installazione del pacchetto da un'origine locale che non esiste genera un messaggio fittizio - [&#1674;](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="c60d5-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="c60d5-142">"Aggiornamento disponibile" filtro consente di visualizzare gli aggiornamenti che violano il vincolo di versione - [&#1094;](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="c60d5-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="c60d5-143">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c60d5-143">Performance Improvements</span></span>

* <span data-ttu-id="c60d5-144">Prestazioni: Miglioramento ContentModel destinazione framework analisi - [&#3162;](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="c60d5-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="c60d5-145">Prestazioni: Evitare la lettura `runtime.json` file per i ripristini che non dispongono di RID [&#3150;](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="c60d5-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="c60d5-146">Nei computer degli elementi di configurazione, il ripristino di un esempio di che applicazione Web ASP.NET ridotto più di 15 secondi per 3 secondi.</span><span class="sxs-lookup"><span data-stu-id="c60d5-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="c60d5-147">Prestazioni: Tempo di caricamento Package Manager Console init.ps1 [&#2956;](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="c60d5-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="c60d5-148">Tempo di apertura PackageManagerConsole migliorate in alcuni casi 132s 10s.</span><span class="sxs-lookup"><span data-stu-id="c60d5-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="c60d5-149">Risolvere i problemi di prestazioni ReSharper in aggiornamento NuGet - [&#3044;](https://github.com/NuGet/Home/issues/3044): in un progetto di esempio, tempo impiegato per installare i pacchetti ridotto da 140s a 68s.</span><span class="sxs-lookup"><span data-stu-id="c60d5-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="c60d5-150">DCR</span><span class="sxs-lookup"><span data-stu-id="c60d5-150">DCRs</span></span>

* <span data-ttu-id="c60d5-151">NuGet è necessario informare gli utenti che l'aggiornamento o l'installazione in un tfm dotnet basato su PCL potrebbe provocare problemi - [&#3138;](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="c60d5-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="c60d5-152">Installazione/aggiornamento non valido per il progetto con tfm Avvisa = "dotnet" - [&#3137;](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="c60d5-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="c60d5-153">Aggiungere il supporto netcoreapp11 e netstandard17 - [&#2998;](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="c60d5-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="c60d5-154">Stampare il contenuto dell'intestazione NuGet avviso alla console in nuget.exe - [&#2934;](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="c60d5-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="c60d5-155">Attributo AssemblyMetadata sfruttare per `.nuspec` token sostituzioni - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="c60d5-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="c60d5-156">Rimuovere la proprietà bloccata dal file di blocco - [&#2379;](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="c60d5-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="c60d5-157">Pacchetti dei simboli non devono mai essere utilizzati nell'installare o aggiornare &#2807;</span><span class="sxs-lookup"><span data-stu-id="c60d5-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="c60d5-158">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="c60d5-158">Features</span></span>

* <span data-ttu-id="c60d5-159">Supporto per le cartelle pacchetto fallback - [&#2899;](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="c60d5-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="c60d5-160">Progettare e implementare una nozione di tipo di pacchetto per supportare i pacchetti strumento - [&#2476;](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="c60d5-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="c60d5-161">API per ottenere il percorso della cartella di pacchetti globale - [&#2403;](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="c60d5-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="c60d5-162">Pacchetti nativi aggiornare supporto - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="c60d5-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
