---
title: Comando push NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di nuget.exe push
keywords: riferimento push NuGet, il comando push
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: df8ef42f650a20b92a281fff3e597ac8d484544e
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="1ae36-104">comando push (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1ae36-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="1ae36-105">**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** tutti; 4.1.0+ necessari per nuget.org</span><span class="sxs-lookup"><span data-stu-id="1ae36-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="1ae36-106">Per inviare pacchetti a nuget.org è necessario utilizzare nuget.exe v4.1.0 +, che implementa la [NuGet protocolli](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="1ae36-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="1ae36-107">Inserisce un pacchetto a un'origine del pacchetto e la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="1ae36-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="1ae36-108">Configurazione predefinita di NuGet consente di ottenere il caricamento `%AppData%\NuGet\NuGet.Config`, quindi caricare qualsiasi `Nuget.Config` o `.nuget\Nuget.Config` file a partire dalla radice dell'unità e di fine nella directory corrente (vedere [configurazione NuGet comportamento](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="1ae36-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="1ae36-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="1ae36-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="1ae36-110">dove `<packagePath>` identifica il pacchetto da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="1ae36-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="1ae36-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="1ae36-111">Options</span></span>

| <span data-ttu-id="1ae36-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="1ae36-112">Option</span></span> | <span data-ttu-id="1ae36-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1ae36-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ae36-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="1ae36-114">ApiKey</span></span> | <span data-ttu-id="1ae36-115">La chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1ae36-115">The API key for the target repository.</span></span> <span data-ttu-id="1ae36-116">Se non è presente, quella specificata nella *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1ae36-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="1ae36-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1ae36-117">ConfigFile</span></span> | <span data-ttu-id="1ae36-118">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="1ae36-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1ae36-119">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1ae36-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="1ae36-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="1ae36-120">DisableBuffering</span></span> | <span data-ttu-id="1ae36-121">Disabilita la memorizzazione nel buffer quando push a un server HTTP (s) per ridurre l'utilizzo di memoria.</span><span class="sxs-lookup"><span data-stu-id="1ae36-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="1ae36-122">Attenzione: quando si utilizza questa opzione, l'autenticazione integrata di Windows potrebbe non funzionare.</span><span class="sxs-lookup"><span data-stu-id="1ae36-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="1ae36-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1ae36-123">ForceEnglishOutput</span></span> | <span data-ttu-id="1ae36-124">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="1ae36-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1ae36-125">?</span><span class="sxs-lookup"><span data-stu-id="1ae36-125">Help</span></span> | <span data-ttu-id="1ae36-126">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="1ae36-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="1ae36-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1ae36-127">NonInteractive</span></span> | <span data-ttu-id="1ae36-128">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="1ae36-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1ae36-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="1ae36-129">NoSymbols</span></span> | <span data-ttu-id="1ae36-130">*(3.5 +)*  Se esiste un pacchetto di simboli, non sarà inserito in un server di simboli.</span><span class="sxs-lookup"><span data-stu-id="1ae36-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="1ae36-131">Origine</span><span class="sxs-lookup"><span data-stu-id="1ae36-131">Source</span></span> | <span data-ttu-id="1ae36-132">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="1ae36-132">Specifies the server URL.</span></span> <span data-ttu-id="1ae36-133">NuGet identifica un origine cartella locale o UNC e copiato il file anziché il push tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ae36-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="1ae36-134">Inoltre, a partire da NuGet sezione 3.4.2, questo è un parametro obbligatorio, a meno che il `NuGet.Config` file specifica un *DefaultPushSource* valore (vedere [il comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="1ae36-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="1ae36-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="1ae36-135">SymbolSource</span></span> | <span data-ttu-id="1ae36-136">*(3.5 +)*  Specifica l'URL del server di simboli; nuget.smbsrc.net viene usato quando l'inserimento di nuget.org</span><span class="sxs-lookup"><span data-stu-id="1ae36-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="1ae36-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="1ae36-137">SymbolApiKey</span></span> | <span data-ttu-id="1ae36-138">*(3.5 +)*  Specifica la chiave API per l'URL specificato nel `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="1ae36-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="1ae36-139">Timeout</span><span class="sxs-lookup"><span data-stu-id="1ae36-139">Timeout</span></span> | <span data-ttu-id="1ae36-140">Specifica il timeout in secondi, per l'inserimento di un server.</span><span class="sxs-lookup"><span data-stu-id="1ae36-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="1ae36-141">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="1ae36-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="1ae36-142">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="1ae36-142">Verbosity</span></span> | <span data-ttu-id="1ae36-143">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="1ae36-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1ae36-144">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1ae36-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1ae36-145">Esempi</span><span class="sxs-lookup"><span data-stu-id="1ae36-145">Examples</span></span>

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
