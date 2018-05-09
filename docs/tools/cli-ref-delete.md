---
title: Comando delete NuGet CLI
description: Riferimento per il comando delete nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="1532f-103">eliminazione di comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="1532f-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="1532f-104">**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="1532f-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1532f-105">Elimina o unlists un pacchetto da un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1532f-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="1532f-106">Per nuget.org, il comando delete [unlists il pacchetto](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="1532f-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="1532f-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="1532f-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="1532f-108">dove `<packageID>` e `<packageVersion>` identificare il pacchetto esatto per eliminare o esclusione.</span><span class="sxs-lookup"><span data-stu-id="1532f-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="1532f-109">Il comportamento esatto dipende dall'origine.</span><span class="sxs-lookup"><span data-stu-id="1532f-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="1532f-110">Per le cartelle locali, ad esempio, il pacchetto viene eliminato; per nuget.org il pacchetto è incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="1532f-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="1532f-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="1532f-111">Options</span></span>

| <span data-ttu-id="1532f-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="1532f-112">Option</span></span> | <span data-ttu-id="1532f-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1532f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1532f-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="1532f-114">ApiKey</span></span> | <span data-ttu-id="1532f-115">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1532f-115">The API key for the target repository.</span></span> <span data-ttu-id="1532f-116">Se non è presente, viene utilizzato quello specificato nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1532f-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="1532f-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1532f-117">ConfigFile</span></span> | <span data-ttu-id="1532f-118">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="1532f-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1532f-119">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1532f-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1532f-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1532f-120">ForceEnglishOutput</span></span> | <span data-ttu-id="1532f-121">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="1532f-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1532f-122">?</span><span class="sxs-lookup"><span data-stu-id="1532f-122">Help</span></span> | <span data-ttu-id="1532f-123">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="1532f-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="1532f-124">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="1532f-124">NonInteractive</span></span> | <span data-ttu-id="1532f-125">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="1532f-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1532f-126">Origine</span><span class="sxs-lookup"><span data-stu-id="1532f-126">Source</span></span> | <span data-ttu-id="1532f-127">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="1532f-127">Specifies the server URL.</span></span> <span data-ttu-id="1532f-128">L'URL per nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1532f-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="1532f-129">Per i feed privati, sostituire il nome host, ad esempio, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="1532f-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="1532f-130">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="1532f-130">Verbosity</span></span> | <span data-ttu-id="1532f-131">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="1532f-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1532f-132">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1532f-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1532f-133">Esempi</span><span class="sxs-lookup"><span data-stu-id="1532f-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
