---
title: Comando push NuGet CLI
description: Informazioni di riferimento per il comando push nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548343"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="b4b46-103">comando push (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b4b46-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="b4b46-104">**Si applica a:** pacchetto di pubblicazione &bullet; **le versioni supportate:** tutte: versione 4.1.0 + necessari per nuget.org</span><span class="sxs-lookup"><span data-stu-id="b4b46-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="b4b46-105">Eseguire il push dei pacchetti in nuget.org è necessario usare nuget.exe verze 4.1.0 +, che implementa la necessaria [protocolli NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="b4b46-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="b4b46-106">Effettua il push di un pacchetto a un'origine di pacchetto e lo pubblica.</span><span class="sxs-lookup"><span data-stu-id="b4b46-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="b4b46-107">Configurazione predefinita di NuGet si ottiene caricando `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), quindi caricando qualsiasi `Nuget.Config` oppure `.nuget\Nuget.Config` file a partire dalla radice dell'unità e di fine nella directory corrente (vedere [configurazione Comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="b4b46-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="b4b46-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b4b46-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="b4b46-109">in cui `<packagePath>` identifica il pacchetto per effettuare il push nel server.</span><span class="sxs-lookup"><span data-stu-id="b4b46-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="b4b46-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="b4b46-110">Options</span></span>

| <span data-ttu-id="b4b46-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="b4b46-111">Option</span></span> | <span data-ttu-id="b4b46-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b4b46-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4b46-113">Chiave API</span><span class="sxs-lookup"><span data-stu-id="b4b46-113">ApiKey</span></span> | <span data-ttu-id="b4b46-114">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b4b46-114">The API key for the target repository.</span></span> <span data-ttu-id="b4b46-115">Se non è presente, viene utilizzato quello specificato nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b4b46-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="b4b46-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b4b46-116">ConfigFile</span></span> | <span data-ttu-id="b4b46-117">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="b4b46-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b4b46-118">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="b4b46-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b4b46-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="b4b46-119">DisableBuffering</span></span> | <span data-ttu-id="b4b46-120">Disabilita la memorizzazione nel buffer quando si effettua il push a un server HTTP (s) per ridurre gli utilizzi della memoria.</span><span class="sxs-lookup"><span data-stu-id="b4b46-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="b4b46-121">Attenzione: quando questa opzione viene usata, l'autenticazione integrata di Windows potrebbe non funzionare.</span><span class="sxs-lookup"><span data-stu-id="b4b46-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="b4b46-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b4b46-122">ForceEnglishOutput</span></span> | <span data-ttu-id="b4b46-123">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="b4b46-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b4b46-124">?</span><span class="sxs-lookup"><span data-stu-id="b4b46-124">Help</span></span> | <span data-ttu-id="b4b46-125">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="b4b46-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="b4b46-126">Non interattive</span><span class="sxs-lookup"><span data-stu-id="b4b46-126">NonInteractive</span></span> | <span data-ttu-id="b4b46-127">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b4b46-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b4b46-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="b4b46-128">NoSymbols</span></span> | <span data-ttu-id="b4b46-129">*(3.5 +)*  Se esiste un pacchetto di simboli, non verrà inserito in un server di simboli.</span><span class="sxs-lookup"><span data-stu-id="b4b46-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="b4b46-130">Origine</span><span class="sxs-lookup"><span data-stu-id="b4b46-130">Source</span></span> | <span data-ttu-id="b4b46-131">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="b4b46-131">Specifies the server URL.</span></span> <span data-ttu-id="b4b46-132">NuGet identifica un'origine di cartella locale o UNC e copia semplicemente il file invece di eseguirne il push tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="b4b46-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="b4b46-133">Inoltre, a partire da NuGet 3.4.2, questo è un parametro obbligatorio, a meno che il `NuGet.Config` file specifica un *DefaultPushSource* valore (vedere [del comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="b4b46-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="b4b46-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="b4b46-134">SymbolSource</span></span> | <span data-ttu-id="b4b46-135">*(3.5 +)*  Specifica l'URL del server di simboli; nuget.smbsrc.net viene usato quando il push in nuget.org</span><span class="sxs-lookup"><span data-stu-id="b4b46-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="b4b46-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="b4b46-136">SymbolApiKey</span></span> | <span data-ttu-id="b4b46-137">*(3.5 +)*  Specifica la chiave API per l'URL specificato in `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="b4b46-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="b4b46-138">Timeout</span><span class="sxs-lookup"><span data-stu-id="b4b46-138">Timeout</span></span> | <span data-ttu-id="b4b46-139">Specifica il timeout, espresso in secondi, per effettuare il push a un server.</span><span class="sxs-lookup"><span data-stu-id="b4b46-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="b4b46-140">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="b4b46-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="b4b46-141">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="b4b46-141">Verbosity</span></span> | <span data-ttu-id="b4b46-142">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="b4b46-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b4b46-143">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b4b46-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b4b46-144">Esempi</span><span class="sxs-lookup"><span data-stu-id="b4b46-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
