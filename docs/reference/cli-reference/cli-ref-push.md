---
title: Comando push dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando nuget.exe push
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779184"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="6eceb-103">comando Push (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="6eceb-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="6eceb-104">**Si applica a:** &bullet; **versioni supportate** per la pubblicazione di pacchetti: All; 4.1.0 + required for NuGet.org</span><span class="sxs-lookup"><span data-stu-id="6eceb-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="6eceb-105">Per eseguire il push dei pacchetti in nuget.org è necessario usare nuget.exe v 4.1.0 +, che implementa i [protocolli NuGet](../../api/nuget-protocols.md)necessari.</span><span class="sxs-lookup"><span data-stu-id="6eceb-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="6eceb-106">Inserisce un pacchetto in un'origine del pacchetto e lo pubblica.</span><span class="sxs-lookup"><span data-stu-id="6eceb-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="6eceb-107">La configurazione predefinita di NuGet si ottiene caricando `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), quindi caricando tutti `Nuget.Config` `.nuget\Nuget.Config` i file o a partire dalla radice dell'unità e terminando con la directory corrente (vedere [configurazioni NuGet comuni](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="6eceb-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="6eceb-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="6eceb-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="6eceb-109">dove `<packagePath>` identifica il pacchetto da inserire nel server.</span><span class="sxs-lookup"><span data-stu-id="6eceb-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="6eceb-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="6eceb-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="6eceb-111">Chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6eceb-111">The API key for the target repository.</span></span> <span data-ttu-id="6eceb-112">Se non è presente, viene utilizzato quello specificato nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6eceb-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6eceb-113">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="6eceb-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6eceb-114">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6eceb-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="6eceb-115">Disabilita la memorizzazione nel buffer quando si effettua il push a un server HTTP (s) per ridurre gli utilizzi della memoria.</span><span class="sxs-lookup"><span data-stu-id="6eceb-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="6eceb-116">Attenzione: quando si usa questa opzione, l'autenticazione integrata di Windows potrebbe non funzionare.</span><span class="sxs-lookup"><span data-stu-id="6eceb-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6eceb-117">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="6eceb-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6eceb-118">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="6eceb-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6eceb-119">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6eceb-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="6eceb-120">Non viene accodato `api/v2/packages` all'URL di origine.</span><span class="sxs-lookup"><span data-stu-id="6eceb-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="6eceb-121">*(3.5 +)* Se esiste un pacchetto di simboli, non verrà eseguito il push in un server di simboli.</span><span class="sxs-lookup"><span data-stu-id="6eceb-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="6eceb-122">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="6eceb-122">Specifies the server URL.</span></span> <span data-ttu-id="6eceb-123">NuGet identifica un'origine UNC o di cartella locale ed esegue semplicemente la copia del file, anziché eseguire il push usando il protocollo HTTP.</span><span class="sxs-lookup"><span data-stu-id="6eceb-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="6eceb-124">Inoltre, a partire da NuGet 3.4.2, si tratta di un parametro obbligatorio a meno che il `NuGet.Config` file non specifichi un valore *DefaultPushSource* (vedere [configurazione del comportamento di NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="6eceb-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="6eceb-125">*(5.1 +)* Se un pacchetto e una versione esiste già, ignorarlo e continuare con il pacchetto successivo nell'eventuale push.</span><span class="sxs-lookup"><span data-stu-id="6eceb-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="6eceb-126">*(3.5 +)* Specifica l'URL del server di simboli. nuget.smbsrc.net viene usato quando si esegue il push in nuget.org</span><span class="sxs-lookup"><span data-stu-id="6eceb-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="6eceb-127">*(3.5 +)* Specifica la chiave API per l'URL specificato in `-SymbolSource` .</span><span class="sxs-lookup"><span data-stu-id="6eceb-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="6eceb-128">Specifica il timeout, in secondi, per il push in un server.</span><span class="sxs-lookup"><span data-stu-id="6eceb-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="6eceb-129"> Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="6eceb-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6eceb-130">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="6eceb-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="6eceb-131">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6eceb-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6eceb-132">Esempi</span><span class="sxs-lookup"><span data-stu-id="6eceb-132">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
