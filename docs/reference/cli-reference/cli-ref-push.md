---
title: Comando push dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando Push di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327628"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="82c19-103">comando Push (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="82c19-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="82c19-104">**Si applica a:** &bullet; **versioni supportate** per la pubblicazione di pacchetti: All; 4.1.0 + required for NuGet.org</span><span class="sxs-lookup"><span data-stu-id="82c19-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="82c19-105">Per eseguire il push dei pacchetti in nuget.org è necessario usare NuGet. exe v 4.1.0 +, che implementa i [protocolli NuGet](../../api/nuget-protocols.md)necessari.</span><span class="sxs-lookup"><span data-stu-id="82c19-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="82c19-106">Inserisce un pacchetto in un'origine del pacchetto e lo pubblica.</span><span class="sxs-lookup"><span data-stu-id="82c19-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="82c19-107">La configurazione predefinita di NuGet `%AppData%\NuGet\NuGet.Config` si ottiene caricando (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), quindi caricando `.nuget\Nuget.Config` qualsiasi `Nuget.Config` file o a partire dalla radice dell'unità e terminando con la directory corrente (vedere [NuGet comune). configurazioni](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="82c19-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="82c19-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="82c19-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="82c19-109">dove `<packagePath>` identifica il pacchetto da inserire nel server.</span><span class="sxs-lookup"><span data-stu-id="82c19-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="82c19-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="82c19-110">Options</span></span>

| <span data-ttu-id="82c19-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="82c19-111">Option</span></span> | <span data-ttu-id="82c19-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="82c19-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="82c19-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="82c19-113">ApiKey</span></span> | <span data-ttu-id="82c19-114">Chiave API per il repository di destinazione.</span><span class="sxs-lookup"><span data-stu-id="82c19-114">The API key for the target repository.</span></span> <span data-ttu-id="82c19-115">Se non è presente, viene utilizzato quello specificato nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="82c19-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="82c19-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="82c19-116">ConfigFile</span></span> | <span data-ttu-id="82c19-117">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="82c19-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="82c19-118">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="82c19-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="82c19-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="82c19-119">DisableBuffering</span></span> | <span data-ttu-id="82c19-120">Disabilita la memorizzazione nel buffer quando si effettua il push a un server HTTP (s) per ridurre gli utilizzi della memoria.</span><span class="sxs-lookup"><span data-stu-id="82c19-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="82c19-121">Attenzione: quando si usa questa opzione, l'autenticazione integrata di Windows potrebbe non funzionare.</span><span class="sxs-lookup"><span data-stu-id="82c19-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="82c19-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="82c19-122">ForceEnglishOutput</span></span> | <span data-ttu-id="82c19-123">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="82c19-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="82c19-124">Help</span><span class="sxs-lookup"><span data-stu-id="82c19-124">Help</span></span> | <span data-ttu-id="82c19-125">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="82c19-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="82c19-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="82c19-126">NonInteractive</span></span> | <span data-ttu-id="82c19-127">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="82c19-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="82c19-128">Nosymbols</span><span class="sxs-lookup"><span data-stu-id="82c19-128">NoSymbols</span></span> | <span data-ttu-id="82c19-129">*(3.5 +)* Se esiste un pacchetto di simboli, non verrà eseguito il push in un server di simboli.</span><span class="sxs-lookup"><span data-stu-id="82c19-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="82c19-130">Source</span><span class="sxs-lookup"><span data-stu-id="82c19-130">Source</span></span> | <span data-ttu-id="82c19-131">Specifica l'URL del server.</span><span class="sxs-lookup"><span data-stu-id="82c19-131">Specifies the server URL.</span></span> <span data-ttu-id="82c19-132">NuGet identifica un'origine UNC o di cartella locale ed esegue semplicemente la copia del file, anziché eseguire il push usando il protocollo HTTP.</span><span class="sxs-lookup"><span data-stu-id="82c19-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="82c19-133">Inoltre, a partire da NuGet 3.4.2, si tratta di un parametro obbligatorio a `NuGet.Config` meno che il file non specifichi un valore *DefaultPushSource* (vedere [configurazione del comportamento di NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="82c19-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="82c19-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="82c19-134">SkipDuplicate</span></span> | <span data-ttu-id="82c19-135">*(5.1 +)* Se un pacchetto e una versione esiste già, ignorarlo e continuare con il pacchetto successivo nell'eventuale push.</span><span class="sxs-lookup"><span data-stu-id="82c19-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="82c19-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="82c19-136">SymbolSource</span></span> | <span data-ttu-id="82c19-137">*(3.5 +)* Specifica l'URL del server di simboli. nuget.smbsrc.net viene usato quando si esegue il push in nuget.org</span><span class="sxs-lookup"><span data-stu-id="82c19-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="82c19-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="82c19-138">SymbolApiKey</span></span> | <span data-ttu-id="82c19-139">*(3.5 +)* Specifica la chiave API per l'URL specificato in `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="82c19-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="82c19-140">Timeout</span><span class="sxs-lookup"><span data-stu-id="82c19-140">Timeout</span></span> | <span data-ttu-id="82c19-141">Specifica il timeout, in secondi, per il push in un server.</span><span class="sxs-lookup"><span data-stu-id="82c19-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="82c19-142">Il valore predefinito è 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="82c19-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="82c19-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="82c19-143">Verbosity</span></span> | <span data-ttu-id="82c19-144">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="82c19-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="82c19-145">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="82c19-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="82c19-146">Esempi</span><span class="sxs-lookup"><span data-stu-id="82c19-146">Examples</span></span>

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
