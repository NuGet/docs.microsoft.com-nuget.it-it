---
title: Comando mirror NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di nuget.exe mirror
keywords: riferimento mirror NuGet, comando mirror
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 80b8f9a3b74030ffd3f1c7b784204d98be67d684
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="ef528-104">comando mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ef528-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="ef528-105">**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** deprecata in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="ef528-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="ef528-106">Riflette un pacchetto e le relative dipendenze dal repository di origine specificato per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ef528-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="ef528-107">Per abilitare questo comando per le versioni di NuGet prima 3.2, passare a [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), selezionare la versione stabile più recente, scaricare `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` al disco locale e ridenominazione `Nuget-Signed.exe` per `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ef528-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="ef528-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="ef528-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="ef528-109">dove `<packageID>` è il pacchetto per eseguire il mirroring, o `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti per eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="ef528-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="ef528-110">Il `<listUrlTarget>` specifica il repository di origine e `<publishUrlTarget>` specifica del repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ef528-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="ef528-111">Se il repository di destinazione si trova in `https://machine/repo` che esegue [NuGet.Server](../hosting-packages/nuget-server.md), gli URL di elenco e push sarà `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="ef528-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="ef528-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="ef528-112">Options</span></span>

| <span data-ttu-id="ef528-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="ef528-113">Option</span></span> | <span data-ttu-id="ef528-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ef528-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef528-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="ef528-115">ApiKey</span></span> | <span data-ttu-id="ef528-116">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ef528-116">The API key for the target repository.</span></span> <span data-ttu-id="ef528-117">Se non è presente, quella specificata nella *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ef528-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ef528-118">?</span><span class="sxs-lookup"><span data-stu-id="ef528-118">Help</span></span> | <span data-ttu-id="ef528-119">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="ef528-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="ef528-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="ef528-120">NoCache</span></span> | <span data-ttu-id="ef528-121">Impedisce l'utilizzo di pacchetti dalla cache locale NuGet.</span><span class="sxs-lookup"><span data-stu-id="ef528-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="ef528-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="ef528-122">Noop</span></span> | <span data-ttu-id="ef528-123">Registra quali possono essere eseguite, ma non esegue le azioni; si presuppone che l'esito positivo per le operazioni di push.</span><span class="sxs-lookup"><span data-stu-id="ef528-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="ef528-124">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="ef528-124">PreRelease</span></span> | <span data-ttu-id="ef528-125">Include i pacchetti della versione provvisoria nell'operazione di mirroring.</span><span class="sxs-lookup"><span data-stu-id="ef528-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="ef528-126">Origine</span><span class="sxs-lookup"><span data-stu-id="ef528-126">Source</span></span> | <span data-ttu-id="ef528-127">Un elenco delle origini pacchetto per eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="ef528-127">A list of package sources to mirror.</span></span> <span data-ttu-id="ef528-128">Se non vengono specificata alcuna origine, quelli definiti in *%AppData%\NuGet\NuGet.Config* vengono utilizzati, l'impostazione nuget.org se non è specificato.</span><span class="sxs-lookup"><span data-stu-id="ef528-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="ef528-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="ef528-129">Timeout</span></span> | <span data-ttu-id="ef528-130">Specifica il timeout in secondi, per l'inserimento di un server.</span><span class="sxs-lookup"><span data-stu-id="ef528-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="ef528-131">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="ef528-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="ef528-132">Versione</span><span class="sxs-lookup"><span data-stu-id="ef528-132">Version</span></span> | <span data-ttu-id="ef528-133">La versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="ef528-133">The version of the package to install.</span></span> <span data-ttu-id="ef528-134">Se non specificato, la versione più recente è il mirroring.</span><span class="sxs-lookup"><span data-stu-id="ef528-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="ef528-135">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ef528-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ef528-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="ef528-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
