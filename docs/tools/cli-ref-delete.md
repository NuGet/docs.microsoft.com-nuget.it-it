---
title: Comando delete NuGet CLI
description: Informazioni di riferimento per il comando delete nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548510"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="602e0-103">eliminazione di comando (CLI di NuGet)</span><span class="sxs-lookup"><span data-stu-id="602e0-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="602e0-104">**Si applica a:** pacchetto di pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="602e0-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="602e0-105">Dall'elenco o elimina un pacchetto da un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="602e0-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="602e0-106">Per nuget.org, il comando delete [Elimina il pacchetto](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="602e0-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="602e0-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="602e0-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="602e0-108">in cui `<packageID>` e `<packageVersion>` identificare l'esatto del pacchetto per eliminare o rimuovere dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="602e0-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="602e0-109">Il comportamento esatto dipende dall'origine.</span><span class="sxs-lookup"><span data-stu-id="602e0-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="602e0-110">Per le cartelle locali, ad esempio, il pacchetto viene eliminato. per nuget.org il pacchetto è incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="602e0-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="602e0-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="602e0-111">Options</span></span>

| <span data-ttu-id="602e0-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="602e0-112">Option</span></span> | <span data-ttu-id="602e0-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="602e0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="602e0-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="602e0-114">ApiKey</span></span> | <span data-ttu-id="602e0-115">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="602e0-115">The API key for the target repository.</span></span> <span data-ttu-id="602e0-116">Se non è presente, viene utilizzato quello specificato nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="602e0-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="602e0-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="602e0-117">ConfigFile</span></span> | <span data-ttu-id="602e0-118">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="602e0-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="602e0-119">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="602e0-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="602e0-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="602e0-120">ForceEnglishOutput</span></span> | <span data-ttu-id="602e0-121">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="602e0-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="602e0-122">Help</span><span class="sxs-lookup"><span data-stu-id="602e0-122">Help</span></span> | <span data-ttu-id="602e0-123">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="602e0-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="602e0-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="602e0-124">NonInteractive</span></span> | <span data-ttu-id="602e0-125">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="602e0-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="602e0-126">Source</span><span class="sxs-lookup"><span data-stu-id="602e0-126">Source</span></span> | <span data-ttu-id="602e0-127">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="602e0-127">Specifies the server URL.</span></span> <span data-ttu-id="602e0-128">L'URL per nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="602e0-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="602e0-129">Per i feed privati, sostituire il nome host, ad esempio, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="602e0-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="602e0-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="602e0-130">Verbosity</span></span> | <span data-ttu-id="602e0-131">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="602e0-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="602e0-132">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="602e0-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="602e0-133">Esempi</span><span class="sxs-lookup"><span data-stu-id="602e0-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
