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
ms.openlocfilehash: 3412d38edbdb011d050b9b61c7c144568edd4cca
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="037d7-104">eliminazione di comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="037d7-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="037d7-105">**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="037d7-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="037d7-106">Elimina o unlists un pacchetto da un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="037d7-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="037d7-107">Per nuget.org, il comando delete [unlists il pacchetto](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="037d7-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="037d7-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="037d7-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="037d7-109">dove `<packageID>` e `<packageVersion>` identificare il pacchetto esatto per eliminare o esclusione.</span><span class="sxs-lookup"><span data-stu-id="037d7-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="037d7-110">Il comportamento esatto dipende dall'origine.</span><span class="sxs-lookup"><span data-stu-id="037d7-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="037d7-111">Per le cartelle locali, ad esempio, il pacchetto viene eliminato; per nuget.org il pacchetto è incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="037d7-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="037d7-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="037d7-112">Options</span></span>

| <span data-ttu-id="037d7-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="037d7-113">Option</span></span> | <span data-ttu-id="037d7-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="037d7-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="037d7-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="037d7-115">ApiKey</span></span> | <span data-ttu-id="037d7-116">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="037d7-116">The API key for the target repository.</span></span> <span data-ttu-id="037d7-117">Se non è presente, quella specificata nella *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="037d7-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="037d7-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="037d7-118">ConfigFile</span></span> | <span data-ttu-id="037d7-119">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="037d7-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="037d7-120">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="037d7-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="037d7-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="037d7-121">ForceEnglishOutput</span></span> | <span data-ttu-id="037d7-122">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="037d7-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="037d7-123">?</span><span class="sxs-lookup"><span data-stu-id="037d7-123">Help</span></span> | <span data-ttu-id="037d7-124">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="037d7-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="037d7-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="037d7-125">NonInteractive</span></span> | <span data-ttu-id="037d7-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="037d7-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="037d7-127">Origine</span><span class="sxs-lookup"><span data-stu-id="037d7-127">Source</span></span> | <span data-ttu-id="037d7-128">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="037d7-128">Specifies the server URL.</span></span> <span data-ttu-id="037d7-129">L'URL per nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="037d7-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="037d7-130">Per i feed privati, sostituire il nome host, ad esempio, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="037d7-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="037d7-131">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="037d7-131">Verbosity</span></span> | <span data-ttu-id="037d7-132">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="037d7-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="037d7-133">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="037d7-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="037d7-134">Esempi</span><span class="sxs-lookup"><span data-stu-id="037d7-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
