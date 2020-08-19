---
title: Comando mirror CLI NuGet
description: Riferimento per il comando nuget.exe mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622967"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="1e3f4-103">comando mirror (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="1e3f4-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="1e3f4-104">**Si applica a:** versioni supportate per la pubblicazione di pacchetti &bullet; **:** deprecate in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="1e3f4-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="1e3f4-105">Rispecchia un pacchetto e le relative dipendenze dai repository di origine specificati al repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="1e3f4-106">NuGet.ServerExtensions.dll e NuGet-Signed.exe che in precedenza supportano questo comando in NuGet 2. x (rinominando NuGet-Signed.exe in nuget.exe) non sono più disponibili per il download.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="1e3f4-107">Per usare un comando simile a questo, provare [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="1e3f4-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="1e3f4-108">Uso</span><span class="sxs-lookup"><span data-stu-id="1e3f4-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="1e3f4-109">dove `<packageID>` è il pacchetto di cui eseguire il mirroring o `<configFilePath>` identifica il `packages.config` file in cui sono elencati i pacchetti di cui eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="1e3f4-110">`<listUrlTarget>`Specifica il repository di origine e `<publishUrlTarget>` specifica il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="1e3f4-111">Se il repository di destinazione è in `https://machine/repo` esecuzione [NuGet. Server](../../hosting-packages/nuget-server.md), l'elenco e gli URL push saranno `https://machine/repo/nuget` rispettivamente e `https://machine/repo/api/v2/package` .</span><span class="sxs-lookup"><span data-stu-id="1e3f4-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="1e3f4-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="1e3f4-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="1e3f4-113">Chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-113">The API key for the target repository.</span></span> <span data-ttu-id="1e3f4-114">Se non è presente, viene usato quello specificato nel file di configurazione ( `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="1e3f4-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="1e3f4-115">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="1e3f4-116">Impedisce a NuGet di usare pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="1e3f4-117">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1e3f4-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="1e3f4-118">Registra il risultato dell'operazione, ma non esegue le azioni; presuppone l'esito positivo delle operazioni push.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="1e3f4-119">Include pacchetti di versioni non definitive nell'operazione di mirroring.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="1e3f4-120">Elenco di origini dei pacchetti di cui eseguire il mirroring.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-120">A list of package sources to mirror.</span></span> <span data-ttu-id="1e3f4-121">Se non viene specificata alcuna origine, vengono usati quelli definiti nel file di configurazione (vedere ApiKey), per impostazione predefinita nuget.org se non ne viene specificato alcuno.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="1e3f4-122">Specifica il timeout, in secondi, per il push in un server.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="1e3f4-123"> Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="1e3f4-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="1e3f4-124">Versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-124">The version of the package to install.</span></span> <span data-ttu-id="1e3f4-125">Se non è specificato, viene riflessa la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="1e3f4-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="1e3f4-126">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1e3f4-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1e3f4-127">Esempi</span><span class="sxs-lookup"><span data-stu-id="1e3f4-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
