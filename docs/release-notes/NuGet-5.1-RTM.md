---
title: Note sulla versione di NuGet 5,1 RTM
description: Note sulla versione per NuGet 5,1, incluse nuove funzionalità, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699856"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="1f7d7-103">Note sulla versione di NuGet 5,1</span><span class="sxs-lookup"><span data-stu-id="1f7d7-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="1f7d7-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="1f7d7-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="1f7d7-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="1f7d7-105">NuGet version</span></span> | <span data-ttu-id="1f7d7-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f7d7-106">Available in Visual Studio version</span></span>| <span data-ttu-id="1f7d7-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1f7d7-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="1f7d7-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="1f7d7-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="1f7d7-109">Visual Studio 2019 versione 16,1</span><span class="sxs-lookup"><span data-stu-id="1f7d7-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="1f7d7-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="1f7d7-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="1f7d7-111"><sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="1f7d7-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="1f7d7-112"><sup>2</sup> Disponibile come installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="1f7d7-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="1f7d7-113">Riepilogo: novità di 5,1</span><span class="sxs-lookup"><span data-stu-id="1f7d7-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="1f7d7-114">Supporto per ignorare un push del pacchetto se esiste già per consentire una migliore integrazione con i flussi di lavoro CI/CD- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="1f7d7-115">Visual Studio offre ora un comodo collegamento alla pagina della raccolta di nuget.org del pacchetto: [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="1f7d7-116">Supporto per le nuove risorse di .NET Core 3,0 come [Targeting Pack](https://github.com/dotnet/cli/issues/10006) e [Runtime Pack](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="1f7d7-117">Supporto di pacchetti NuGet e ripristino per FrameworkReferences per abilitare i riferimenti ai pacchetti di runtime e di destinazione- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="1f7d7-118">Supporto dello scenario "solo download" del pacchetto con PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="1f7d7-119">Escludi i pacchetti di runtime e targeting dai risultati della ricerca & Restore Graph con PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="1f7d7-120">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="1f7d7-120">Issues fixed in this release</span></span>

<span data-ttu-id="1f7d7-121">**Bug**</span><span class="sxs-lookup"><span data-stu-id="1f7d7-121">**Bugs**</span></span>

* <span data-ttu-id="1f7d7-122">Plug-in: Dettagli eccezione persi durante la creazione del plug- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="1f7d7-123">L'intervallo di PackageReference con limite inferiore esclusivo non funziona se il limite inferiore è presente in una delle origini.</span><span class="sxs-lookup"><span data-stu-id="1f7d7-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="1f7d7-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="1f7d7-125">Migliorare [#8021](https://github.com/NuGet/Home/issues/8021) messaggi di IsPackableFalseError</span><span class="sxs-lookup"><span data-stu-id="1f7d7-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="1f7d7-126">Packages lock file-Rigenera file di blocco quando viene modificato il grafico del progetto: [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="1f7d7-127">Bug ProjectSystem: i pacchetti NuGet vengono rimossi automaticamente- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="1f7d7-128">Aggiungere una destinazione per la restituzione di FrameworkReference simile a CollectPackageDownloads e CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="1f7d7-129">Cache HTTP: la risorsa RepositoryResources non viene memorizzata nella cache in modalità [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="1f7d7-130">Registrazione: l'eccezione stack non viene segnalata con un livello di dettaglio dettagliato- [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="1f7d7-131">Modificare tutti gli URL di documentazione NuGet per usare HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="1f7d7-132">Miglioramento del messaggio di avviso NU3024- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="1f7d7-133">Impossibile aggiornare il file di blocco quando packagereference è stato rimosso- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="1f7d7-134">Migliorare la gestione dei casi di errore durante la convalida dell'elemento licenseUrl e License in NuSpec- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="1f7d7-135">Interfaccia utente PM: fare clic con il pulsante destro del mouse sull'intestazione della scheda e fare clic su "Apri percorso file" genera un errore [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="1f7d7-136">Plug-in: registra quando viene chiuso il processo del plug- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="1f7d7-137">Plug-in: velocità di collisione elevata nella registrazione dei valori DateTime- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="1f7d7-138">Il file manifest. ReadFrom ha esito negativo in qualsiasi NuSpec con LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="1f7d7-139">RestoreLockedMode: NU1004 imprevisto quando ProjectReference fa riferimento a un progetto con AssemblyName personalizzato- [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="1f7d7-140">Messaggio di errore migliore quando l'avvio del plug-in ha esito negativo con un'eccezione- [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="1f7d7-141">Quando si esegue un ripristino NoOp, evitare \* .dgspec.jsdurante la scrittura nella directory obj- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="1f7d7-142">GeneratePathProperty = true non riesce a generare la proprietà in caso di mancata corrispondenza [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="1f7d7-143">Impostazioni: il carattere non valido nel percorso di origine del pacchetto può arrestarsi in modo anomalo e [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="1f7d7-144">Se il file di blocco viene eliminato, Restore non genera il file di blocco in NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="1f7d7-145">L'URL di licenza e la licenza causano un errore di lettura con i metadati [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="1f7d7-146">Eccezioni non gestite in V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="1f7d7-147">nuget.exe restituisce zero del codice di uscita per argomenti non validi- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="1f7d7-148">Aggiornare i documenti degli errori e degli avvisi per riflettere gli scenari correlati alla firma: [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="1f7d7-149">Il file degli asset deve usare percorsi relativi per consentire lo stato di trasferimento dei progetti più facilmente [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="1f7d7-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="1f7d7-150">**DCRs**</span></span>

* <span data-ttu-id="1f7d7-151">Plug-in: abilitazione della registrazione diagnostica- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="1f7d7-152">Eseguire il mapping di Tizen 6 a NetStandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="1f7d7-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="1f7d7-153">**[Elenco di tutti i problemi risolti in questa versione-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="1f7d7-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
