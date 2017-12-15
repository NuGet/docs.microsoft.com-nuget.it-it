---
title: 3.5 note sulla versione Beta2 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b76064f-0607-438a-bbf8-dd862690f48e
description: "Note sulla versione per NuGet 3.5 Beta 2, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 3.5 Beta 2 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6dd388e52308d2f3cd32d4d6c66c2868f0ae2a41
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="35-beta2-release-notes"></a><span data-ttu-id="3fae9-104">3.5 note sulla versione Beta2</span><span class="sxs-lookup"><span data-stu-id="3fae9-104">3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="3fae9-105">[Note sulla versione 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [note sulla versione 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="3fae9-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="3fae9-106">Versione RTM di NuGet 3.5 Beta 2 è stato rilasciato il 27 giugno 2016 per Visual Studio 2013 e nuget.exe</span><span class="sxs-lookup"><span data-stu-id="3fae9-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="3fae9-107">Log delle modifiche completo</span><span class="sxs-lookup"><span data-stu-id="3fae9-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="3fae9-108">Elenco problemi</span><span class="sxs-lookup"><span data-stu-id="3fae9-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

# <a name="notable-changes"></a><span data-ttu-id="3fae9-109">Modifiche significative</span><span class="sxs-lookup"><span data-stu-id="3fae9-109">Notable Changes</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="3fae9-110">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="3fae9-110">Bug Fixes</span></span>

* <span data-ttu-id="3fae9-111">Mancanza di supporto per password decrpytion in .NET Core per i feed autenticati - messaggio di errore aggiornato [&#2942;](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="3fae9-111">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="3fae9-112">Get-pacchetto Console di gestione pacchetti non riesce se il progetto .NET Core è aperto - [&#2932;](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="3fae9-112">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="3fae9-113">Correzione della gestione corretta di 403 nel comando push NuGet [&#2910;](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="3fae9-113">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="3fae9-114">Risolvere i problemi nel disinstallare i pacchetti in una soluzione associato al controllo del codice sorgente TFS quando disableSourceControlIntegration è impostata su true - [&#2739;](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="3fae9-114">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="3fae9-115">Correggere l'aggiornamento del pacchetto da eseguire in pacchetti bersaglio account - [&#2724;](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="3fae9-115">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="3fae9-116">Utilizzare il livello di dettaglio di MSBuild per impostare il livello di logger per Gestione pacchetti Nuget azioni dell'interfaccia utente - [&#2705;](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="3fae9-116">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="3fae9-117">Correggere la configurazione NuGet è un errore non valido nei progetti di sito Web - VS 2015 VSIX (v3.4.3) - [&#2667;](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="3fae9-117">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="3fae9-118">Risolvere i problemi di Service pack da `.csproj` quando i file di contenuto sono inclusi - [&#2658;](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="3fae9-118">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="3fae9-119">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) non funziona - [&#2653;](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="3fae9-119">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="3fae9-120">Risolvere un problema nella versione Nuget versione 3.4.3 - valore non può essere null per la creazione del pacchetto - [&#2648;](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="3fae9-120">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="3fae9-121">Ripristino utilizza le credenziali archiviate da NuGet. config per i feed di VSTS - [&#2647;](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="3fae9-121">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="3fae9-122">Prestazioni - correzione allocazioni eccessive nel codice di confronto versione - [&#2632;](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="3fae9-122">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="3fae9-123">Risolvere i problemi quando più istanze di nuget.exe tenta di installare lo stesso pacchetto in parallelo - [&#2628;](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="3fae9-123">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="3fae9-124">Prestazioni - Cache le informazioni sulle dipendenze per le operazioni multiprogetto - [&#2619;](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="3fae9-124">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="3fae9-125">Risolvere problema in cui non è possibile origini pacchetto aggiunte dall'impostazioni quando l'elenco di origine è vuota - [&#2617;](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="3fae9-125">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="3fae9-126">Correggere l'errore Misleading durante il tentativo di installare il pacchetto che dipende dalla fase di progettazione aspetti - [&#2594;](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="3fae9-126">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="3fae9-127">Installa un pacchetto dalla console PackageManager con l'impostazione "All" tenta prima origine - [&#2557;](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="3fae9-127">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="3fae9-128">Risolvere i problemi con i pacchetti che contengono file con tempi di scrittura in futuro (Mono) - [&#2518;](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="3fae9-128">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="3fae9-129">Visualizzare l'eccezione quando si verifica un errore per i progetti di ricerca nel comando update - [&#2418;](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="3fae9-129">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="3fae9-130">Contenuto del pacchetto non verrà ripristinato correttamente quando si installa un pacchetto da nuget 3.3 + feed con l'argomento - NoCache quando il pacchetto contiene `.nupkg` file - [&#2354;](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="3fae9-130">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="3fae9-131">Problema di correzione con pacchetto installa (tutte le origini) quando il pacchetto non è presente 1 origine - [&#2322;](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="3fae9-131">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="3fae9-132">Installare blocchi se una singola origine si verifica un errore di autorizzazione - [&#2034;](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="3fae9-132">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="3fae9-133">`.nuspec`versione intervallo deve eseguire l'override di versione - IncludeReferencedProjects - [&#1983;](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="3fae9-133">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="3fae9-134">NuGet 3.3.0 aggiornamento ha esito negativo con '... un vincolo aggiuntivo definito nel file Packages. config impedisce questa operazione.'</span><span class="sxs-lookup"><span data-stu-id="3fae9-134">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="3fae9-135"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="3fae9-135"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="3fae9-136">aggiornamento di NuGet.exe elimina il nome sicuro dell'assembly e l'attributo privata.</span><span class="sxs-lookup"><span data-stu-id="3fae9-136">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="3fae9-137"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="3fae9-137"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="3fae9-138">Risolvere i problemi con il percorso relativo del file per "DefaultPushSource" - [&#1746;](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="3fae9-138">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="3fae9-139">Migliorare i messaggi di errore di sistema di risoluzione Update - [&#1373;](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="3fae9-139">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="3fae9-140">Funzionalità e modifiche del comportamento</span><span class="sxs-lookup"><span data-stu-id="3fae9-140">Features and Behavior Changes</span></span>

* <span data-ttu-id="3fae9-141">NuGet.exe push: parametro di timeout non funziona - [&#2785;](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="3fae9-141">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="3fae9-142">non produce NuGet.exe restore `.props` e `.targets` file per `.nuproj` progetti (regressione in v3.4.3.855) - [&#2711;](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="3fae9-142">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="3fae9-143">È necessario confrontare Framework con importazioni - l'API di estensibilità [&#2633;](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="3fae9-143">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="3fae9-144">Nascondere le opzioni di dipendenza quando si utilizza `project.json`  -  [&#2486;](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="3fae9-144">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="3fae9-145">Stampa l'intestazione di versione nuget.exe in output dettagliato - [&#1887;](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="3fae9-145">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="3fae9-146">NuGet è necessario aggiungere il supporto per /nativeassets/ /runtimes/ {rid} {txm} / - [&#2782;](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="3fae9-146">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>