---
title: Comando config di NuGet CLI
description: Informazioni di riferimento per il comando config nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426067"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="36233-103">comando config di NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="36233-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="36233-104">**Si applica a:** tutte &bullet; **le versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="36233-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="36233-105">Ottiene o imposta i valori di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="36233-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="36233-106">Per altre informazioni sulla sintassi, vedere [configurazioni comuni per NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="36233-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="36233-107">Per informazioni dettagliate sui nomi di chiave consentiti, vedere la [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="36233-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="36233-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="36233-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="36233-109">in cui `<name>` e `<value>` specificare una coppia chiave-valore da impostare nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="36233-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="36233-110">È possibile specificare un numero di coppie in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="36233-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="36233-111">Per rimuovere un valore, specificare il nome e il `=` sign ma nessun valore.</span><span class="sxs-lookup"><span data-stu-id="36233-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="36233-112">Per i nomi di chiave consentiti, vedere la [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="36233-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="36233-113">In NuGet 3.4 + `<value>` utilizzabile [variabili di ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="36233-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="36233-114">Opzioni</span><span class="sxs-lookup"><span data-stu-id="36233-114">Options</span></span>

| <span data-ttu-id="36233-115">Opzione</span><span class="sxs-lookup"><span data-stu-id="36233-115">Option</span></span> | <span data-ttu-id="36233-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="36233-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36233-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="36233-117">AsPath</span></span> | <span data-ttu-id="36233-118">Restituisce la configurazione di valore come percorso UNC, ignorati quando `-Set` viene usato.</span><span class="sxs-lookup"><span data-stu-id="36233-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="36233-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="36233-119">ConfigFile</span></span> | <span data-ttu-id="36233-120">Il file di configurazione di NuGet da modificare.</span><span class="sxs-lookup"><span data-stu-id="36233-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="36233-121">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="36233-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="36233-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="36233-122">ForceEnglishOutput</span></span> | <span data-ttu-id="36233-123">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="36233-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="36233-124">Help</span><span class="sxs-lookup"><span data-stu-id="36233-124">Help</span></span> | <span data-ttu-id="36233-125">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="36233-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="36233-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="36233-126">NonInteractive</span></span> | <span data-ttu-id="36233-127">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="36233-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="36233-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="36233-128">Verbosity</span></span> | <span data-ttu-id="36233-129">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="36233-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="36233-130">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="36233-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="36233-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="36233-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
