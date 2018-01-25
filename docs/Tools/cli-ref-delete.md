---
title: Comando delete NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando delete nuget.exe
keywords: NuGet Elimina riferimento, eliminare il comando di pacchetto
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="7b09b-104">eliminazione di comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="7b09b-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="7b09b-105">**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="7b09b-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7b09b-106">Elimina o unlists un pacchetto da un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7b09b-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="7b09b-107">Per nuget.org, il comando delete [unlists il pacchetto](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="7b09b-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7b09b-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="7b09b-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="7b09b-109">dove `<packageID>` e `<packageVersion>` identificare il pacchetto esatto per eliminare o esclusione.</span><span class="sxs-lookup"><span data-stu-id="7b09b-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="7b09b-110">Il comportamento esatto dipende dall'origine.</span><span class="sxs-lookup"><span data-stu-id="7b09b-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="7b09b-111">Per le cartelle locali, ad esempio, il pacchetto viene eliminato; per nuget.org il pacchetto è incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="7b09b-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="7b09b-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="7b09b-112">Options</span></span>

| <span data-ttu-id="7b09b-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="7b09b-113">Option</span></span> | <span data-ttu-id="7b09b-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7b09b-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b09b-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="7b09b-115">ApiKey</span></span> | <span data-ttu-id="7b09b-116">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7b09b-116">The API key for the target repository.</span></span> <span data-ttu-id="7b09b-117">Se non è presente, quella specificata nella *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="7b09b-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="7b09b-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7b09b-118">ConfigFile</span></span> | <span data-ttu-id="7b09b-119">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="7b09b-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7b09b-120">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="7b09b-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="7b09b-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7b09b-121">ForceEnglishOutput</span></span> | <span data-ttu-id="7b09b-122">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="7b09b-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7b09b-123">?</span><span class="sxs-lookup"><span data-stu-id="7b09b-123">Help</span></span> | <span data-ttu-id="7b09b-124">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="7b09b-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="7b09b-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7b09b-125">NonInteractive</span></span> | <span data-ttu-id="7b09b-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="7b09b-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7b09b-127">Origine</span><span class="sxs-lookup"><span data-stu-id="7b09b-127">Source</span></span> | <span data-ttu-id="7b09b-128">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="7b09b-128">Specifies the server URL.</span></span> <span data-ttu-id="7b09b-129">L'URL per nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="7b09b-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="7b09b-130">Per i feed privati, sostituire il nome host, ad esempio, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="7b09b-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="7b09b-131">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="7b09b-131">Verbosity</span></span> | <span data-ttu-id="7b09b-132">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="7b09b-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7b09b-133">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7b09b-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7b09b-134">Esempi</span><span class="sxs-lookup"><span data-stu-id="7b09b-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
