---
title: Comando mirror NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il comando di nuget.exe mirror
keywords: riferimento mirror NuGet, comando mirror
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="c1f5d-104">comando mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c1f5d-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="c1f5d-105">**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** deprecata in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="c1f5d-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="c1f5d-106">Riflette un pacchetto e le relative dipendenze dal repository di origine specificato per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c1f5d-107">Per abilitare questo comando per le versioni di NuGet prima 3.2, passare a [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), selezionare la versione stabile più recente, scaricare `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` al disco locale e ridenominazione `Nuget-Signed.exe` a `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="c1f5d-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c1f5d-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="c1f5d-109">dove `<packageID>` è il pacchetto per eseguire il mirroring, o `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti per eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="c1f5d-110">Il `<listUrlTarget>` specifica il repository di origine e `<publishUrlTarget>` specifica del repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="c1f5d-111">Se il repository di destinazione si trova in `https://machine/repo` che esegue [NuGet.Server](../hosting-packages/nuget-server.md), gli URL di elenco e push sarà `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c1f5d-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="c1f5d-112">Options</span></span>

| <span data-ttu-id="c1f5d-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="c1f5d-113">Option</span></span> | <span data-ttu-id="c1f5d-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c1f5d-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c1f5d-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="c1f5d-115">ApiKey</span></span> | <span data-ttu-id="c1f5d-116">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-116">The API key for the target repository.</span></span> <span data-ttu-id="c1f5d-117">Se non è presente, quello specificato nel file di configurazione viene utilizzato (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux)).</span><span class="sxs-lookup"><span data-stu-id="c1f5d-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="c1f5d-118">?</span><span class="sxs-lookup"><span data-stu-id="c1f5d-118">Help</span></span> | <span data-ttu-id="c1f5d-119">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="c1f5d-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="c1f5d-120">NoCache</span></span> | <span data-ttu-id="c1f5d-121">Impedisce l'uso memorizzati nella cache dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="c1f5d-122">Vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c1f5d-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c1f5d-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="c1f5d-123">Noop</span></span> | <span data-ttu-id="c1f5d-124">Registra quali possono essere eseguite, ma non esegue le azioni; si presuppone che l'esito positivo per le operazioni di push.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="c1f5d-125">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="c1f5d-125">PreRelease</span></span> | <span data-ttu-id="c1f5d-126">Include i pacchetti della versione provvisoria nell'operazione di mirroring.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="c1f5d-127">Origine</span><span class="sxs-lookup"><span data-stu-id="c1f5d-127">Source</span></span> | <span data-ttu-id="c1f5d-128">Un elenco delle origini pacchetto per eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-128">A list of package sources to mirror.</span></span> <span data-ttu-id="c1f5d-129">Se non vengono specificata alcuna origine, quelli definiti nel file di configurazione (vedere ApiKey precedente) vengono utilizzati, l'impostazione nuget.org se è stata specificata alcuna.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="c1f5d-130">Timeout</span><span class="sxs-lookup"><span data-stu-id="c1f5d-130">Timeout</span></span> | <span data-ttu-id="c1f5d-131">Specifica il timeout in secondi, per l'inserimento di un server.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c1f5d-132">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="c1f5d-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="c1f5d-133">Versione</span><span class="sxs-lookup"><span data-stu-id="c1f5d-133">Version</span></span> | <span data-ttu-id="c1f5d-134">La versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-134">The version of the package to install.</span></span> <span data-ttu-id="c1f5d-135">Se non specificato, la versione più recente è il mirroring.</span><span class="sxs-lookup"><span data-stu-id="c1f5d-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="c1f5d-136">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c1f5d-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c1f5d-137">Esempi</span><span class="sxs-lookup"><span data-stu-id="c1f5d-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
