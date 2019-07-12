---
title: Note sulla versione 5.1 RTM di NuGet
description: Note sulla versione per NuGet 5.1 incluse nuove funzionalità, correzioni di bug e dcr.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842571"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="77dfa-103">Note sulla versione 5.1 di NuGet</span><span class="sxs-lookup"><span data-stu-id="77dfa-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="77dfa-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="77dfa-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="77dfa-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="77dfa-105">NuGet version</span></span> | <span data-ttu-id="77dfa-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77dfa-106">Available in Visual Studio version</span></span>| <span data-ttu-id="77dfa-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="77dfa-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="77dfa-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="77dfa-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="77dfa-109">Visual Studio 2019 versione 16.1</span><span class="sxs-lookup"><span data-stu-id="77dfa-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="77dfa-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="77dfa-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="77dfa-111"><sup>1</sup>installata con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="77dfa-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="77dfa-112"><sup>2</sup>disponibile in un'installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="77dfa-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="77dfa-113">Riepilogo: Quali sono le novità nella versione 5.1</span><span class="sxs-lookup"><span data-stu-id="77dfa-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="77dfa-114">Supporto per ignorare un push del pacchetto se esiste già per consentire una migliore integrazione con flussi di lavoro di integrazione continua/recapito Continuo - [1630 #](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="77dfa-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="77dfa-115">Visual Studio offre ora un comodo collegamento per la pagina di gallery del pacchetto nuget.org - [5299 #](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="77dfa-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="77dfa-116">Il supporto per nuovi asset di .NET Core 3.0 come [Targeting Pack](https://github.com/dotnet/cli/issues/10006) e [pacchetti di Runtime](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="77dfa-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="77dfa-117">NuGet pack e restore di supporto per FrameworkReferences abilitare i riferimenti ai pacchetti di runtime e di destinazione - [7342 #](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="77dfa-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="77dfa-118">Scenario del pacchetto "solo download" di supporto con PackageDownload - [7339 #](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="77dfa-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="77dfa-119">Runtime Exlcude e targeting Pack da risultati della ricerca e ripristino del grafico utilizzando PackageType - [7337 #](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="77dfa-119">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="77dfa-120">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="77dfa-120">Issues fixed in this release</span></span>

<span data-ttu-id="77dfa-121">**Bug**</span><span class="sxs-lookup"><span data-stu-id="77dfa-121">**Bugs**</span></span>

* <span data-ttu-id="77dfa-122">Plug-in: i dettagli dell'eccezione persi durante la creazione del plug-in - [8057 #](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="77dfa-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="77dfa-123">Intervallo di PackageReference con limite inferiore a esclusivo non funziona se il limite inferiore è presente in una delle origini.</span><span class="sxs-lookup"><span data-stu-id="77dfa-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="77dfa-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="77dfa-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="77dfa-125">Migliorare IsPackableFalseError messaggio - [8021 #](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="77dfa-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="77dfa-126">I pacchetti di File di blocco - file di blocco rigenerare quando viene modificato grafico progetto - [8019 #](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="77dfa-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="77dfa-127">Bug Project System: Rimuovere i pacchetti NuGet recupero automatico - [8017 #](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="77dfa-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="77dfa-128">Aggiungere una destinazione per la restituzione di FrameworkReference simile a CollectPackageDownloads e CollectPackageReferences - [8005 #](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="77dfa-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="77dfa-129">Cache HTTP:  Risorsa RepositoryResources non viene memorizzato nella cache in modo con controllo delle versioni - [7997 #](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="77dfa-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="77dfa-130">La registrazione: eccezione gli stack di chiamate non vengono segnalati con livello di dettaglio massimo - [7955 #](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="77dfa-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="77dfa-131">Modificare tutti gli URL di documentazione di NuGet per usare HTTPS - [7950 #](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="77dfa-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="77dfa-132">Migliorare il messaggio di avviso NU3024 - [7933 #](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="77dfa-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="77dfa-133">file di blocco non vengono aggiornati quando packagereference rimosso - [7930 #](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="77dfa-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="77dfa-134">Migliorare la gestione di casi di errore durante la convalida di un elemento licenseurl e licenza in nuspec - [7915 #](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="77dfa-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="77dfa-135">UI PM - fare clic sull'intestazione della scheda e facendo clic su "Apri percorso file" risultati errore - [7913 #](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="77dfa-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="77dfa-136">Plug-in: accedere al termine del processo di plug-in - [7907 #](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="77dfa-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="77dfa-137">Plug-in: frequenza dei conflitti elevata nei valori di data/ora di registrazione - [7899 #](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="77dfa-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="77dfa-138">Manifest.ReadFrom non riesce in qualsiasi file nuspec con LicenseExpression - [7894 #](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="77dfa-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="77dfa-139">RestoreLockedMode: NU1004 imprevisto quando ProjectReference fa riferimento a un progetto con personalizzato AssemblyName - [7889 #](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="77dfa-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="77dfa-140">Messaggio di errore migliore quando si verifica un errore di avvio del plug-in con un'eccezione - [7857 #](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="77dfa-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="77dfa-141">Quando si esegue un ripristino NoOp, evitare \*. dgspec.json scrittura nella directory obj - [7854 #](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="77dfa-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="77dfa-142">GeneratePathProperty = true non riesce a generare proprietà sulla mancata corrispondenza maiuscole - [7843 #](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="77dfa-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="77dfa-143">Impostazioni: carattere non valido nel percorso di origine può arrestarsi in modo anomalo Visual Studio - [7820 #](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="77dfa-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="77dfa-144">Se si elimina il file di blocco, restore non genera file di blocco su NoOp - [7807 #](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="77dfa-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="77dfa-145">URL della licenza e le cause di licenza con i metadati - errore di lettura [7547 #](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="77dfa-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="77dfa-146">Eccezioni non gestite nel V2FeedParser - [7523 #](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="77dfa-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="77dfa-147">NuGet.exe restituisce il codice di uscita zero per argomenti non validi - [7178 #](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="77dfa-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="77dfa-148">Aggiornare gli errori e alla documentazione di avviso in modo da riflettere scenari correlati firma - [6498 #](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="77dfa-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="77dfa-149">File di asset debba usare percorsi relativi per attivare lo spostamento dei progetti più facilmente - [4582 #](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="77dfa-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="77dfa-150">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="77dfa-150">**DCRs**</span></span>

* <span data-ttu-id="77dfa-151">Plug-in: abilitare la registrazione diagnostica - [7859 #](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="77dfa-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="77dfa-152">Marca 6 Tizen mappa alla versione 2.1 NetStandard - [7773 #](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="77dfa-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="77dfa-153">**[Elenco di tutti i problemi risolti in questa versione: 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="77dfa-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
