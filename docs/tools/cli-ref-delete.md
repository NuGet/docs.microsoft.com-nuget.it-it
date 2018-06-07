---
title: Comando delete NuGet CLI
description: Riferimento per il comando delete nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0f33dd5475521da47972a6f032ac6ea86d98c83
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817178"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="a10cb-103">eliminazione di comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="a10cb-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="a10cb-104">**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="a10cb-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a10cb-105">Elimina o unlists un pacchetto da un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a10cb-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="a10cb-106">Per nuget.org, il comando delete [unlists il pacchetto](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a10cb-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a10cb-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="a10cb-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="a10cb-108">dove `<packageID>` e `<packageVersion>` identificare il pacchetto esatto per eliminare o esclusione.</span><span class="sxs-lookup"><span data-stu-id="a10cb-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="a10cb-109">Il comportamento esatto dipende dall'origine.</span><span class="sxs-lookup"><span data-stu-id="a10cb-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="a10cb-110">Per le cartelle locali, ad esempio, il pacchetto viene eliminato; per nuget.org il pacchetto è incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="a10cb-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="a10cb-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="a10cb-111">Options</span></span>

| <span data-ttu-id="a10cb-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="a10cb-112">Option</span></span> | <span data-ttu-id="a10cb-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a10cb-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a10cb-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="a10cb-114">ApiKey</span></span> | <span data-ttu-id="a10cb-115">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a10cb-115">The API key for the target repository.</span></span> <span data-ttu-id="a10cb-116">Se non è presente, viene utilizzato quello specificato nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a10cb-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="a10cb-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a10cb-117">ConfigFile</span></span> | <span data-ttu-id="a10cb-118">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="a10cb-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a10cb-119">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a10cb-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a10cb-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a10cb-120">ForceEnglishOutput</span></span> | <span data-ttu-id="a10cb-121">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="a10cb-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a10cb-122">?</span><span class="sxs-lookup"><span data-stu-id="a10cb-122">Help</span></span> | <span data-ttu-id="a10cb-123">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="a10cb-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="a10cb-124">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="a10cb-124">NonInteractive</span></span> | <span data-ttu-id="a10cb-125">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="a10cb-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a10cb-126">Origine</span><span class="sxs-lookup"><span data-stu-id="a10cb-126">Source</span></span> | <span data-ttu-id="a10cb-127">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="a10cb-127">Specifies the server URL.</span></span> <span data-ttu-id="a10cb-128">L'URL per nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="a10cb-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="a10cb-129">Per i feed privati, sostituire il nome host, ad esempio, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="a10cb-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="a10cb-130">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="a10cb-130">Verbosity</span></span> | <span data-ttu-id="a10cb-131">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="a10cb-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a10cb-132">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a10cb-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a10cb-133">Esempi</span><span class="sxs-lookup"><span data-stu-id="a10cb-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
