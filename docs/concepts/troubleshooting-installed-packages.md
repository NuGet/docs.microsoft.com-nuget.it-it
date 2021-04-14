---
title: Risoluzione dei problemi relativi ai pacchetti installati
description: Come trovare l'origine del pacchetto usata per i singoli pacchetti
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387571"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="49ab5-103">Risoluzione dei problemi relativi ai pacchetti installati</span><span class="sxs-lookup"><span data-stu-id="49ab5-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="49ab5-104">In alcuni casi può essere necessario convalidare l'origine da cui è stato installato un pacchetto specifico.</span><span class="sxs-lookup"><span data-stu-id="49ab5-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="49ab5-105">Ecco alcuni modi per verificare.</span><span class="sxs-lookup"><span data-stu-id="49ab5-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="49ab5-106">Alcune origini di pacchetti supportano un concetto noto come origini upstream.</span><span class="sxs-lookup"><span data-stu-id="49ab5-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="49ab5-107">Ad esempio, [Azure Artifacts origini upstream](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="49ab5-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="49ab5-108">I client NuGet non sanno se un pacchetto proveniva da un'origine upstream.</span><span class="sxs-lookup"><span data-stu-id="49ab5-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="49ab5-109">Pertanto, qualsiasi registrazione dell'origine del pacchetto ese elencata l'origine configurata, non l'origine upstream.</span><span class="sxs-lookup"><span data-stu-id="49ab5-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="49ab5-110">`.nupkg.metadata` file nella cartella dei pacchetti globali</span><span class="sxs-lookup"><span data-stu-id="49ab5-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="49ab5-111">Quando un pacchetto viene estratto nella *cartella global-packages,* viene scritto `.nupkg.metadata` un file.</span><span class="sxs-lookup"><span data-stu-id="49ab5-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="49ab5-112">A partire da NuGet 5.9.0, NuGet aggiungerà l'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="49ab5-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="49ab5-113">Vedere di seguito per eseguire il mapping delle versioni di NuGet Visual Studio o .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="49ab5-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="49ab5-114">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="49ab5-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="49ab5-115">Se la cartella *global-packages* contiene pacchetti estratti prima dell'aggiornamento a una versione più recente degli strumenti con NuGet 5.9.0, il file sarà la versione 1 e non conterrà l'origine del `.nupkg.metadata` pacchetto.</span><span class="sxs-lookup"><span data-stu-id="49ab5-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="49ab5-116">È possibile [cancellare la cartella *global-packages* per assicurarsi](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) che tutti i pacchetti contengano l'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="49ab5-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="49ab5-117">NuGet scrive il `.nupkg.metadata` file solo nella cartella *global-packages.*</span><span class="sxs-lookup"><span data-stu-id="49ab5-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="49ab5-118">I progetti `packages.config` che usano usano una cartella dei pacchetti della soluzione, che non crea un `.nupkg.metadata` file.</span><span class="sxs-lookup"><span data-stu-id="49ab5-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="49ab5-119">Messaggio di log del pacchetto installato</span><span class="sxs-lookup"><span data-stu-id="49ab5-119">Installed package log message</span></span>

<span data-ttu-id="49ab5-120">A partire da NuGet 5.9.0, NuGet restituisce l'origine del pacchetto nel messaggio di ripristino che informa che è stato installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="49ab5-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="49ab5-121">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="49ab5-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="49ab5-122">Questo messaggio viene restituito al livello di dettaglio normale/informativo.</span><span class="sxs-lookup"><span data-stu-id="49ab5-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="49ab5-123">Visual Studio e l'interfaccia della riga di comando hanno un livello di dettaglio minimo, quindi questo `dotnet` messaggio non sarà visibile per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="49ab5-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="49ab5-124">Per `msbuild` impostazione predefinita, gli strumenti e dell'interfaccia della riga di comando hanno un livello di dettaglio normale, quindi questo messaggio `nuget` sarà visibile per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="49ab5-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="49ab5-125">Messaggio di log HTTP</span><span class="sxs-lookup"><span data-stu-id="49ab5-125">HTTP log message</span></span>

<span data-ttu-id="49ab5-126">Quando un pacchetto non è disponibile in locale, nella cartella *global-packages,* in una cartella di fallback o in un'origine file locale, NuGet lo scarica da qualsiasi origine pacchetto configurata tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="49ab5-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="49ab5-127">Le richieste e le risposte HTTP vengono registrate al livello di dettaglio normale e dovrebbero essere presenti solo una singola richiesta e risposta per ogni versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="49ab5-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="49ab5-128">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="49ab5-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="49ab5-129">Se i file sono stati scaricati di recente, potrebbero essere recuperati dalla *http-cache di NuGet*</span><span class="sxs-lookup"><span data-stu-id="49ab5-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="49ab5-130">Il formato dell'URL può essere diverso per le diverse implementazioni del server HTTP NuGet e per l'implementazione del protocollo HTTP NuGet V2 o V3.</span><span class="sxs-lookup"><span data-stu-id="49ab5-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="49ab5-131">Se sono definite più origini HTTP, verranno visualizzati più richieste al file di ogni `nuget.config` `index.json` pacchetto, una per ogni origine.</span><span class="sxs-lookup"><span data-stu-id="49ab5-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="49ab5-132">Tuttavia, per ogni versione del pacchetto sarà disponibile un solo `nupkg` download.</span><span class="sxs-lookup"><span data-stu-id="49ab5-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="49ab5-133">Messaggio del log della firma del pacchetto</span><span class="sxs-lookup"><span data-stu-id="49ab5-133">Package signature log message</span></span>

<span data-ttu-id="49ab5-134">Se il pacchetto scaricato è firmato, NuGet convalida la firma e registra il messaggio seguente con un livello di dettaglio dettagliato:</span><span class="sxs-lookup"><span data-stu-id="49ab5-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="49ab5-135">Questo messaggio verrà segnalato se il pacchetto è stato scaricato da un'origine del pacchetto HTTP o copiato da un'origine del pacchetto locale.</span><span class="sxs-lookup"><span data-stu-id="49ab5-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="49ab5-136">Non verrà restituito se il pacchetto è già disponibile nella *cartella global-packages* o in una cartella di fallback.</span><span class="sxs-lookup"><span data-stu-id="49ab5-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="49ab5-137">A causa [della rimozione dell'attendibilità di VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet, la verifica dei pacchetti firmati è stata disabilitata in determinate piattaforme, in determinate versioni di NuGet e .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="49ab5-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="49ab5-138">Di conseguenza, gli stessi pacchetti possono avere log o tali log potrebbero non essere presenti, a seconda della piattaforma in cui si esegue il ripristino e della versione di .NET o NuGet in `PackageSignatureVerificationLog` uso.</span><span class="sxs-lookup"><span data-stu-id="49ab5-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="49ab5-139">Mappa delle versioni di NuGet</span><span class="sxs-lookup"><span data-stu-id="49ab5-139">NuGet Version Map</span></span>

<span data-ttu-id="49ab5-140">Le versioni seguenti di NuGet hanno modifiche importanti relative alla registrazione dell'origine del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="49ab5-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="49ab5-141">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="49ab5-141">NuGet Version</span></span>|<span data-ttu-id="49ab5-142">Versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="49ab5-142">Visual Studio Version</span></span>|<span data-ttu-id="49ab5-143">Versione di .NET SDK</span><span class="sxs-lookup"><span data-stu-id="49ab5-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="49ab5-144">NuGet 5.9.0</span><span class="sxs-lookup"><span data-stu-id="49ab5-144">NuGet 5.9.0</span></span>|<span data-ttu-id="49ab5-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="49ab5-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="49ab5-146">.NET 5 SDK 5.0.200</span><span class="sxs-lookup"><span data-stu-id="49ab5-146">.NET 5 SDK 5.0.200</span></span>|
