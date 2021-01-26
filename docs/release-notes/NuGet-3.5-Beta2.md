---
title: Note sulla versione di 3,5 beta2
description: Note sulla versione per NuGet 3,5 Beta 2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776386"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="c29d9-103">Note sulla versione di NuGet 3,5 beta2</span><span class="sxs-lookup"><span data-stu-id="c29d9-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="c29d9-104">Note sulla versione [di NuGet 3,5-beta](../release-notes/nuget-3.5-Beta.md)  |  [Note sulla versione di NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="c29d9-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="c29d9-105">NuGet 3,5 Beta 2 RTM è stato rilasciato il 27 giugno 2016 per Visual Studio 2013 e nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c29d9-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="c29d9-106">Changelog completo</span><span class="sxs-lookup"><span data-stu-id="c29d9-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="c29d9-107">Elenco dei problemi</span><span class="sxs-lookup"><span data-stu-id="c29d9-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="c29d9-108">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="c29d9-108">Bug Fixes</span></span>

* <span data-ttu-id="c29d9-109">Messaggio di errore aggiornato per la mancanza di supporto per la password decrpytion in .NET Core per i feed autenticati- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="c29d9-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="c29d9-110">La console di gestione pacchetti Get-Package ha esito negativo se il progetto .NET Core è aperto [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="c29d9-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="c29d9-111">Correzione della gestione errata di 403 nel comando Push NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="c29d9-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="c29d9-112">Risolvere i problemi di disinstallazione dei pacchetti in una soluzione associata al controllo del codice sorgente TFS quando disableSourceControlIntegration è impostato su true- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="c29d9-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="c29d9-113">Correzione dell'aggiornamento del pacchetto per tenere conto dei pacchetti non di destinazione- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="c29d9-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="c29d9-114">Usare il livello di dettaglio di MSBuild per impostare il livello del logger per le azioni dell'interfaccia utente di gestione pacchetti NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="c29d9-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="c29d9-115">Correggi la configurazione NuGet non è un errore valido nei progetti di siti Web-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="c29d9-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="c29d9-116">Risolvere i problemi di Pack da `.csproj` quando sono inclusi i file di contenuto- [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="c29d9-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="c29d9-117">DefaultPushSource `NuGetDefaults.Config` ( `ProgramData\NuGet` ) non funziona- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="c29d9-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="c29d9-118">Correzione del problema nella versione di NuGet 3.4.3: il valore non può essere null durante la creazione del pacchetto: [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="c29d9-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="c29d9-119">Il ripristino usa le credenziali archiviate da Nuget.Config per i feed VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="c29d9-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="c29d9-120">Prestazioni: correzione di allocazioni eccessive nel codice di comparizione delle versioni- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="c29d9-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="c29d9-121">Risolvere i problemi quando più istanze di nuget.exe tentano di installare lo stesso pacchetto in parallelo- [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="c29d9-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="c29d9-122">Prestazioni: informazioni sulle dipendenze della cache per le operazioni multiprogetto- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="c29d9-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="c29d9-123">Correzione del problema per cui le origini dei pacchetti Impossibile vengono aggiunte dalle impostazioni quando l'elenco di origine è vuoto [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="c29d9-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="c29d9-124">Correzione di un errore fuorviante durante il tentativo di installare il pacchetto che dipende dalle facciate della fase di progettazione- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="c29d9-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="c29d9-125">L'installazione di un pacchetto dalla console di PackageManager con l'impostazione "All" prova solo la prima origine- [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="c29d9-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="c29d9-126">Risolvere i problemi relativi ai pacchetti con file con tempi di scrittura in futuro (mono)- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="c29d9-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="c29d9-127">Visualizza l'eccezione quando si verifica un errore durante la ricerca di progetti nel comando Update- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="c29d9-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="c29d9-128">Il contenuto del pacchetto non viene ripristinato correttamente quando si installa un pacchetto da un feed NuGet v 3.3 + con l'argomento-NoCache quando il pacchetto contiene `.nupkg` file- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="c29d9-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="c29d9-129">Correzione di un problema con l'installazione del pacchetto (tutte le origini) quando manca il pacchetto da 1 origine- [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="c29d9-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="c29d9-130">Installa i blocchi se un'unica origine non riesce a eseguire l'autorizzazione- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="c29d9-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="c29d9-131">`.nuspec` l'intervallo di versioni deve eseguire l'override della versione-IncludeReferencedProjects- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="c29d9-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="c29d9-132">L'aggiornamento di NuGet 3.3.0 ha esito negativo con ' un vincolo aggiuntivo... definito in packages.config impedisce questa operazione.</span><span class="sxs-lookup"><span data-stu-id="c29d9-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="c29d9-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="c29d9-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="c29d9-134">nuget.exe aggiornamento elimina il nome sicuro e l'attributo privato dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="c29d9-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="c29d9-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="c29d9-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="c29d9-136">Risolvere i problemi relativi al percorso file relativo per "DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="c29d9-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="c29d9-137">Migliorare i messaggi di errore del resolver di aggiornamento- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="c29d9-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="c29d9-138">Funzionalità e modifiche funzionali</span><span class="sxs-lookup"><span data-stu-id="c29d9-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="c29d9-139">nuget.exe parametro di timeout push non funziona- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="c29d9-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="c29d9-140">nuget.exe Restore non `.props` produce `.targets` file e per i `.nuproj` progetti (regressione in v 3.4.3.855)- [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="c29d9-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="c29d9-141">È necessaria l'API di estendibilità per confrontare i Framework con le importazioni- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="c29d9-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="c29d9-142">Nascondi le opzioni di dipendenza quando si usa `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="c29d9-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="c29d9-143">Stampare l'intestazione della versione nuget.exe nell'output dettagliato- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="c29d9-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="c29d9-144">NuGet dovrebbe aggiungere il supporto per/Runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="c29d9-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>