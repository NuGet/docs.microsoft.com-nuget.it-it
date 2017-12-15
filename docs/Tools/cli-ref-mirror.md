---
title: Comando mirror NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: Riferimento per il comando di nuget.exe mirror
keywords: riferimento mirror NuGet, comando mirror
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="17cc0-104">comando mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="17cc0-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="17cc0-105">**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** deprecata in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="17cc0-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="17cc0-106">Riflette un pacchetto e le relative dipendenze dal repository di origine specificato per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="17cc0-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="17cc0-107">Per abilitare questo comando per le versioni di NuGet prima 3.2, passare a [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), selezionare la versione stabile più recente, scaricare `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` al disco locale e ridenominazione `Nuget-Signed.exe` per `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="17cc0-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="17cc0-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="17cc0-108">Usage</span></span>

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="17cc0-109">dove `<packageID>` è il pacchetto per eseguire il mirroring, o `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti per eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="17cc0-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="17cc0-110">Il `<listUrlTarget>` specifica il repository di origine e `<publishUrlTarget>` specifica del repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="17cc0-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="17cc0-111">Se il repository di destinazione si trova in `https://machine/repo` che esegue [NuGet.Server](../hosting-packages/NuGet-Server.md), gli URL di elenco e push sarà `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="17cc0-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/NuGet-Server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="17cc0-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="17cc0-112">Options</span></span>

| <span data-ttu-id="17cc0-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="17cc0-113">Option</span></span> | <span data-ttu-id="17cc0-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="17cc0-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="17cc0-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="17cc0-115">ApiKey</span></span> | <span data-ttu-id="17cc0-116">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="17cc0-116">The API key for the target repository.</span></span> <span data-ttu-id="17cc0-117">Se non è presente, quella specificata nella *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="17cc0-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="17cc0-118">?</span><span class="sxs-lookup"><span data-stu-id="17cc0-118">Help</span></span> | <span data-ttu-id="17cc0-119">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="17cc0-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="17cc0-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="17cc0-120">NoCache</span></span> | <span data-ttu-id="17cc0-121">Impedisce l'utilizzo di pacchetti dalla cache locale NuGet.</span><span class="sxs-lookup"><span data-stu-id="17cc0-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="17cc0-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="17cc0-122">Noop</span></span> | <span data-ttu-id="17cc0-123">Registra quali possono essere eseguite, ma non esegue le azioni; si presuppone che l'esito positivo per le operazioni di push.</span><span class="sxs-lookup"><span data-stu-id="17cc0-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="17cc0-124">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="17cc0-124">PreRelease</span></span> | <span data-ttu-id="17cc0-125">Include i pacchetti della versione provvisoria nell'operazione di mirroring.</span><span class="sxs-lookup"><span data-stu-id="17cc0-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="17cc0-126">Origine</span><span class="sxs-lookup"><span data-stu-id="17cc0-126">Source</span></span> | <span data-ttu-id="17cc0-127">Un elenco delle origini pacchetto per eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="17cc0-127">A list of package sources to mirror.</span></span> <span data-ttu-id="17cc0-128">Se non vengono specificata alcuna origine, quelli definiti in *%AppData%\NuGet\NuGet.Config* vengono utilizzati, l'impostazione nuget.org se non è specificato.</span><span class="sxs-lookup"><span data-stu-id="17cc0-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="17cc0-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="17cc0-129">Timeout</span></span> | <span data-ttu-id="17cc0-130">Specifica il timeout in secondi, per l'inserimento di un server.</span><span class="sxs-lookup"><span data-stu-id="17cc0-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="17cc0-131">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="17cc0-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="17cc0-132">Versione</span><span class="sxs-lookup"><span data-stu-id="17cc0-132">Version</span></span> | <span data-ttu-id="17cc0-133">La versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="17cc0-133">The version of the package to install.</span></span> <span data-ttu-id="17cc0-134">Se non specificato, la versione più recente è il mirroring.</span><span class="sxs-lookup"><span data-stu-id="17cc0-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="17cc0-135">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="17cc0-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="17cc0-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="17cc0-136">Examples</span></span>

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
