---
title: Comando di eliminazione CLI di NuGet
description: Informazioni di riferimento sul comando NuGet. exe delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327838"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="c9ecc-103">comando Delete (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="c9ecc-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="c9ecc-104">**Si applica a:** &bullet; **versioni supportate** per la pubblicazione di pacchetti: tutti</span><span class="sxs-lookup"><span data-stu-id="c9ecc-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c9ecc-105">Elimina o rimuove dall'elenco un pacchetto da un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="c9ecc-106">Per nuget.org, il comando delete Annulla [l'elenco del pacchetto](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c9ecc-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c9ecc-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c9ecc-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="c9ecc-108">dove `<packageID>` e`<packageVersion>` identificano il pacchetto esatto da eliminare o rimuovere dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="c9ecc-109">Il comportamento esatto dipende dall'origine.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="c9ecc-110">Per le cartelle locali, ad esempio, il pacchetto viene eliminato. per nuget.org il pacchetto viene riincluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="c9ecc-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="c9ecc-111">Options</span></span>

| <span data-ttu-id="c9ecc-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="c9ecc-112">Option</span></span> | <span data-ttu-id="c9ecc-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9ecc-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c9ecc-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="c9ecc-114">ApiKey</span></span> | <span data-ttu-id="c9ecc-115">Chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-115">The API key for the target repository.</span></span> <span data-ttu-id="c9ecc-116">Se non è presente, viene utilizzato quello specificato nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="c9ecc-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c9ecc-117">ConfigFile</span></span> | <span data-ttu-id="c9ecc-118">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c9ecc-119">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c9ecc-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c9ecc-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c9ecc-120">ForceEnglishOutput</span></span> | <span data-ttu-id="c9ecc-121">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c9ecc-122">Help</span><span class="sxs-lookup"><span data-stu-id="c9ecc-122">Help</span></span> | <span data-ttu-id="c9ecc-123">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="c9ecc-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c9ecc-124">NonInteractive</span></span> | <span data-ttu-id="c9ecc-125">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c9ecc-126">Source</span><span class="sxs-lookup"><span data-stu-id="c9ecc-126">Source</span></span> | <span data-ttu-id="c9ecc-127">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-127">Specifies the server URL.</span></span> <span data-ttu-id="c9ecc-128">L'URL per nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="c9ecc-129">Per i feed privati, sostituire il nome host, ad esempio *% hostname%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="c9ecc-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="c9ecc-130">Verbosity</span></span> | <span data-ttu-id="c9ecc-131">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="c9ecc-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c9ecc-132">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c9ecc-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c9ecc-133">Esempi</span><span class="sxs-lookup"><span data-stu-id="c9ecc-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
