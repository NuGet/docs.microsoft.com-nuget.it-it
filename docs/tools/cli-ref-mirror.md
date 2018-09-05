---
title: Comando di NuGet CLI mirror
description: Informazioni di riferimento per il comando mirror nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550206"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="ad691-103">Comando mirror (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="ad691-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="ad691-104">**Si applica a:** pacchetto di pubblicazione &bullet; **le versioni supportate:** deprecato in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="ad691-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="ad691-105">Riflette un pacchetto e le relative dipendenze dal repository di origine specificato per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ad691-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="ad691-106">Per abilitare questo comando per le versioni di NuGet prima 3.2, passare a [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), selezionare la versione stabile più recente, scaricare `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` al disco locale e ridenominazione `Nuget-Signed.exe` a `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ad691-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="ad691-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="ad691-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="ad691-108">in cui `<packageID>` è il pacchetto per eseguire il mirroring, oppure `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti per eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="ad691-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="ad691-109">Il `<listUrlTarget>` specifica il repository del codice sorgente, e `<publishUrlTarget>` consente di specificare il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ad691-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="ad691-110">Se il repository di destinazione si trova in `https://machine/repo` che esegue [NuGet. server](../hosting-packages/nuget-server.md), gli URL elenco ed effettuare il push verrà `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="ad691-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="ad691-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="ad691-111">Options</span></span>

| <span data-ttu-id="ad691-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="ad691-112">Option</span></span> | <span data-ttu-id="ad691-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ad691-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad691-114">Chiave API</span><span class="sxs-lookup"><span data-stu-id="ad691-114">ApiKey</span></span> | <span data-ttu-id="ad691-115">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ad691-115">The API key for the target repository.</span></span> <span data-ttu-id="ad691-116">Se non è presente, quello specificato nel file di configurazione viene usato (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="ad691-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="ad691-117">?</span><span class="sxs-lookup"><span data-stu-id="ad691-117">Help</span></span> | <span data-ttu-id="ad691-118">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="ad691-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="ad691-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="ad691-119">NoCache</span></span> | <span data-ttu-id="ad691-120">Impedisce l'uso di pacchetti memorizzati nella cache NuGet.</span><span class="sxs-lookup"><span data-stu-id="ad691-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="ad691-121">Visualizzare [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ad691-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="ad691-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="ad691-122">Noop</span></span> | <span data-ttu-id="ad691-123">Registra quali possono essere eseguiti, ma non esegue le azioni; si presuppone che l'esito positivo per operazioni di push.</span><span class="sxs-lookup"><span data-stu-id="ad691-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="ad691-124">Versione preliminare</span><span class="sxs-lookup"><span data-stu-id="ad691-124">PreRelease</span></span> | <span data-ttu-id="ad691-125">Include pacchetti versione non definitivo nell'operazione di mirroring.</span><span class="sxs-lookup"><span data-stu-id="ad691-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="ad691-126">Origine</span><span class="sxs-lookup"><span data-stu-id="ad691-126">Source</span></span> | <span data-ttu-id="ad691-127">Elenco di origini dei pacchetti per eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="ad691-127">A list of package sources to mirror.</span></span> <span data-ttu-id="ad691-128">Se non sono specificate origini, quelli definiti nel file di configurazione (vedere ApiKey precedente) vengono utilizzati, se è stato specificato nessuno. verrà utilizzato in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ad691-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="ad691-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="ad691-129">Timeout</span></span> | <span data-ttu-id="ad691-130">Specifica il timeout, espresso in secondi, per effettuare il push a un server.</span><span class="sxs-lookup"><span data-stu-id="ad691-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="ad691-131">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="ad691-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="ad691-132">Versione</span><span class="sxs-lookup"><span data-stu-id="ad691-132">Version</span></span> | <span data-ttu-id="ad691-133">La versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="ad691-133">The version of the package to install.</span></span> <span data-ttu-id="ad691-134">Se non specificato, la versione più recente è sottoposto a mirroring.</span><span class="sxs-lookup"><span data-stu-id="ad691-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="ad691-135">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ad691-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ad691-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="ad691-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
