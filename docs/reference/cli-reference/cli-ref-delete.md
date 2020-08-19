---
title: Comando di eliminazione CLI di NuGet
description: Riferimento per il comando nuget.exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622863"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="c222b-103">comando Delete (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="c222b-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="c222b-104">**Si applica a:** versioni supportate per la pubblicazione di pacchetti &bullet; **:** tutti</span><span class="sxs-lookup"><span data-stu-id="c222b-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c222b-105">Elimina o rimuove dall'elenco un pacchetto da un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c222b-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="c222b-106">Per nuget.org, il comando delete Annulla [l'elenco del pacchetto](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c222b-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c222b-107">Uso</span><span class="sxs-lookup"><span data-stu-id="c222b-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="c222b-108">dove `<packageID>` e `<packageVersion>` identificano il pacchetto esatto da eliminare o rimuovere dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="c222b-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="c222b-109">Il comportamento esatto dipende dall'origine.</span><span class="sxs-lookup"><span data-stu-id="c222b-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="c222b-110">Per le cartelle locali, ad esempio, il pacchetto viene eliminato. per nuget.org il pacchetto viene riincluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="c222b-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="c222b-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="c222b-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="c222b-112">Chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c222b-112">The API key for the target repository.</span></span> <span data-ttu-id="c222b-113">Se non è presente, viene utilizzato quello specificato nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c222b-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c222b-114">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="c222b-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c222b-115">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c222b-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c222b-116">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="c222b-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c222b-117">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="c222b-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c222b-118">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c222b-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="c222b-119">Non chiedere conferma durante l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="c222b-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="c222b-120">**`-NoServiceEndpoint`** Non aggiunge "API/v2/Packages" all'URL di origine.</span><span class="sxs-lookup"><span data-stu-id="c222b-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="c222b-121">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="c222b-121">Specifies the server URL.</span></span> <span data-ttu-id="c222b-122">L'URL per nuget.org è `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="c222b-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="c222b-123">Per i feed privati, sostituire il nome host, ad esempio *% hostname%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="c222b-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c222b-124">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c222b-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="c222b-125">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c222b-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c222b-126">Esempi</span><span class="sxs-lookup"><span data-stu-id="c222b-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
