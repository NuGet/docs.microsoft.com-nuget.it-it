---
title: Comando mirror CLI NuGet
description: Riferimento per il comando mirror di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327668"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="d4fa2-103">Comando mirror (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="d4fa2-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="d4fa2-104">**Si applica a:** &bullet; **versioni supportate** per la pubblicazione di pacchetti: deprecate in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="d4fa2-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="d4fa2-105">Rispecchia un pacchetto e le relative dipendenze dai repository di origine specificati al repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="d4fa2-106">Per abilitare questo comando per le versioni di NuGet prima del 3,2 [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), passare a, selezionare la versione stabile `NuGet.ServerExtensions.dll` più `Nuget-Signed.exe` recente, scaricare e nel disco `Nuget-Signed.exe` locale `nuget.exe` e rinominare in.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="d4fa2-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="d4fa2-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="d4fa2-108">dove `<packageID>` è il pacchetto di cui eseguire il `<configFilePath>` mirroring `packages.config` o identifica il file in cui sono elencati i pacchetti di cui eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="d4fa2-109">Specifica il repository di origine e `<publishUrlTarget>` specifica il repository di destinazione. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="d4fa2-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="d4fa2-110">Se il repository di destinazione è `https://machine/repo` in esecuzione [NuGet. Server](../../hosting-packages/nuget-server.md), l'elenco e gli URL `https://machine/repo/nuget` push saranno rispettivamente e. `https://machine/repo/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="d4fa2-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="d4fa2-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="d4fa2-111">Options</span></span>

| <span data-ttu-id="d4fa2-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="d4fa2-112">Option</span></span> | <span data-ttu-id="d4fa2-113">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="d4fa2-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4fa2-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="d4fa2-114">ApiKey</span></span> | <span data-ttu-id="d4fa2-115">Chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-115">The API key for the target repository.</span></span> <span data-ttu-id="d4fa2-116">Se non è presente, viene usato quello specificato nel file di configurazione (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="d4fa2-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="d4fa2-117">?</span><span class="sxs-lookup"><span data-stu-id="d4fa2-117">Help</span></span> | <span data-ttu-id="d4fa2-118">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="d4fa2-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="d4fa2-119">NoCache</span></span> | <span data-ttu-id="d4fa2-120">Impedisce a NuGet di usare pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="d4fa2-121">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d4fa2-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="d4fa2-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="d4fa2-122">Noop</span></span> | <span data-ttu-id="d4fa2-123">Registra il risultato dell'operazione, ma non esegue le azioni; presuppone l'esito positivo delle operazioni push.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="d4fa2-124">PreRelease</span><span class="sxs-lookup"><span data-stu-id="d4fa2-124">PreRelease</span></span> | <span data-ttu-id="d4fa2-125">Include pacchetti di versioni non definitive nell'operazione di mirroring.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="d4fa2-126">Source</span><span class="sxs-lookup"><span data-stu-id="d4fa2-126">Source</span></span> | <span data-ttu-id="d4fa2-127">Elenco di origini dei pacchetti di cui eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-127">A list of package sources to mirror.</span></span> <span data-ttu-id="d4fa2-128">Se non viene specificata alcuna origine, vengono usati quelli definiti nel file di configurazione (vedere ApiKey), per impostazione predefinita nuget.org se non ne viene specificato alcuno.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="d4fa2-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="d4fa2-129">Timeout</span></span> | <span data-ttu-id="d4fa2-130">Specifica il timeout, in secondi, per il push in un server.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="d4fa2-131">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="d4fa2-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="d4fa2-132">Version</span><span class="sxs-lookup"><span data-stu-id="d4fa2-132">Version</span></span> | <span data-ttu-id="d4fa2-133">Versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-133">The version of the package to install.</span></span> <span data-ttu-id="d4fa2-134">Se non è specificato, viene riflessa la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="d4fa2-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="d4fa2-135">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d4fa2-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d4fa2-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="d4fa2-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
