---
title: Comando mirror CLI NuGet
description: Riferimento per il comando mirror di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959717"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="31ea3-103">Comando mirror (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="31ea3-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="31ea3-104">**Si applica a:** &bullet; **versioni supportate** per la pubblicazione di pacchetti: deprecate in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="31ea3-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="31ea3-105">Rispecchia un pacchetto e le relative dipendenze dai repository di origine specificati al repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="31ea3-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="31ea3-106">NuGet. ServerExtensions. dll e NuGet-Signed. exe che in precedenza supportano questo comando in NuGet 2. x (rinominando NuGet-Signed. exe in NuGet. exe) non sono più disponibili per il download.</span><span class="sxs-lookup"><span data-stu-id="31ea3-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="31ea3-107">Per usare un comando simile a questo, provare [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="31ea3-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="31ea3-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="31ea3-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="31ea3-109">dove `<packageID>` è il pacchetto di cui eseguire il `<configFilePath>` mirroring `packages.config` o identifica il file in cui sono elencati i pacchetti di cui eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="31ea3-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="31ea3-110">Specifica il repository di origine e `<publishUrlTarget>` specifica il repository di destinazione. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="31ea3-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="31ea3-111">Se il repository di destinazione è `https://machine/repo` in esecuzione [NuGet. Server](../../hosting-packages/nuget-server.md), l'elenco e gli URL `https://machine/repo/nuget` push saranno rispettivamente e. `https://machine/repo/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="31ea3-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="31ea3-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="31ea3-112">Options</span></span>

| <span data-ttu-id="31ea3-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="31ea3-113">Option</span></span> | <span data-ttu-id="31ea3-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="31ea3-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31ea3-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="31ea3-115">ApiKey</span></span> | <span data-ttu-id="31ea3-116">Chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="31ea3-116">The API key for the target repository.</span></span> <span data-ttu-id="31ea3-117">Se non è presente, viene usato quello specificato nel file di configurazione (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="31ea3-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="31ea3-118">?</span><span class="sxs-lookup"><span data-stu-id="31ea3-118">Help</span></span> | <span data-ttu-id="31ea3-119">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="31ea3-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="31ea3-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="31ea3-120">NoCache</span></span> | <span data-ttu-id="31ea3-121">Impedisce a NuGet di usare pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="31ea3-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="31ea3-122">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="31ea3-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="31ea3-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="31ea3-123">Noop</span></span> | <span data-ttu-id="31ea3-124">Registra il risultato dell'operazione, ma non esegue le azioni; presuppone l'esito positivo delle operazioni push.</span><span class="sxs-lookup"><span data-stu-id="31ea3-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="31ea3-125">PreRelease</span><span class="sxs-lookup"><span data-stu-id="31ea3-125">PreRelease</span></span> | <span data-ttu-id="31ea3-126">Include pacchetti di versioni non definitive nell'operazione di mirroring.</span><span class="sxs-lookup"><span data-stu-id="31ea3-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="31ea3-127">Source</span><span class="sxs-lookup"><span data-stu-id="31ea3-127">Source</span></span> | <span data-ttu-id="31ea3-128">Elenco di origini dei pacchetti di cui eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="31ea3-128">A list of package sources to mirror.</span></span> <span data-ttu-id="31ea3-129">Se non viene specificata alcuna origine, vengono usati quelli definiti nel file di configurazione (vedere ApiKey), per impostazione predefinita nuget.org se non ne viene specificato alcuno.</span><span class="sxs-lookup"><span data-stu-id="31ea3-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="31ea3-130">Timeout</span><span class="sxs-lookup"><span data-stu-id="31ea3-130">Timeout</span></span> | <span data-ttu-id="31ea3-131">Specifica il timeout, in secondi, per il push in un server.</span><span class="sxs-lookup"><span data-stu-id="31ea3-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="31ea3-132">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="31ea3-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="31ea3-133">Version</span><span class="sxs-lookup"><span data-stu-id="31ea3-133">Version</span></span> | <span data-ttu-id="31ea3-134">Versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="31ea3-134">The version of the package to install.</span></span> <span data-ttu-id="31ea3-135">Se non è specificato, viene riflessa la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="31ea3-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="31ea3-136">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="31ea3-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="31ea3-137">Esempi</span><span class="sxs-lookup"><span data-stu-id="31ea3-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
