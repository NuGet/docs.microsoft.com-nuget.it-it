---
title: NuGet cross-platform i plug-in
description: NuGet cross platform i plug-in per NuGet.exe, dotnet.exe, msbuild.exe e Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794194"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="9e710-103">NuGet cross-platform i plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="9e710-104">In NuGet 4.8 è stato aggiunto il supporto per la cross-platform i plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="9e710-105">Si è ottenuta con creando un nuovo modello di estendibilità di plug-in, che deve essere conforme a un set di regole dell'operazione di tipo strict.</span><span class="sxs-lookup"><span data-stu-id="9e710-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="9e710-106">I plug-in sono file eseguibili indipendenti (runnables nel mondo .NET Core), che avviano i client di NuGet in un processo separato.</span><span class="sxs-lookup"><span data-stu-id="9e710-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="9e710-107">Si tratta di una scrittura true una sola volta, eseguire ovunque plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="9e710-108">Funzionerà con tutti gli strumenti client NuGet.</span><span class="sxs-lookup"><span data-stu-id="9e710-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="9e710-109">I plug-in può essere solo .NET Framework (NuGet.exe, MSBuild.exe e Visual Studio), o .NET Core (dotnet.exe).</span><span class="sxs-lookup"><span data-stu-id="9e710-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="9e710-110">È definito un protocollo di comunicazione con controllo delle versioni tra il Client di NuGet e il plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="9e710-111">Durante l'handshake di avvio, i 2 processi negoziano la versione del protocollo.</span><span class="sxs-lookup"><span data-stu-id="9e710-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="9e710-112">Per coprire tutti gli scenari di strumenti client NuGet, uno necessarie di .NET Framework sia un plug-in .NET Core.</span><span class="sxs-lookup"><span data-stu-id="9e710-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="9e710-113">Di seguito vengono descritte le combinazioni di framework client/del plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="9e710-114">Strumento client</span><span class="sxs-lookup"><span data-stu-id="9e710-114">Client tool</span></span>  | <span data-ttu-id="9e710-115">Framework</span><span class="sxs-lookup"><span data-stu-id="9e710-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="9e710-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e710-116">Visual Studio</span></span> | <span data-ttu-id="9e710-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="9e710-117">.NET Framework</span></span> |
| <span data-ttu-id="9e710-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="9e710-118">dotnet.exe</span></span> | <span data-ttu-id="9e710-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="9e710-119">.NET Core</span></span> |
| <span data-ttu-id="9e710-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="9e710-120">NuGet.exe</span></span> | <span data-ttu-id="9e710-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="9e710-121">.NET Framework</span></span> |
| <span data-ttu-id="9e710-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="9e710-122">MSBuild.exe</span></span> | <span data-ttu-id="9e710-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="9e710-123">.NET Framework</span></span> |
| <span data-ttu-id="9e710-124">NuGet.exe su Mono</span><span class="sxs-lookup"><span data-stu-id="9e710-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="9e710-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="9e710-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="9e710-126">Come funziona</span><span class="sxs-lookup"><span data-stu-id="9e710-126">How does it work</span></span>

<span data-ttu-id="9e710-127">Il flusso di lavoro di alto livello può essere descritte come segue:</span><span class="sxs-lookup"><span data-stu-id="9e710-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="9e710-128">NuGet consente di individuare i plug-in disponibili.</span><span class="sxs-lookup"><span data-stu-id="9e710-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="9e710-129">Quando applicabile, NuGet scorre i plug-in ordine di priorità e viene avviato uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="9e710-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="9e710-130">NuGet verrà utilizzato il primo plug-in grado di servire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="9e710-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="9e710-131">I plug-in verrà arrestata quando non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="9e710-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="9e710-132">Requisiti di plug-in generale</span><span class="sxs-lookup"><span data-stu-id="9e710-132">General plugin requirements</span></span>

<span data-ttu-id="9e710-133">È la versione corrente del protocollo *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="9e710-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="9e710-134">In questa versione, i requisiti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e710-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="9e710-135">Dispone di un assembly firma Authenticode in valida e attendibile che verrà eseguito in Windows e Mono.</span><span class="sxs-lookup"><span data-stu-id="9e710-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="9e710-136">È richiesta alcun trust speciali per gli assembly ancora in esecuzione in Linux e Mac.</span><span class="sxs-lookup"><span data-stu-id="9e710-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="9e710-137">Problema pertinente</span><span class="sxs-lookup"><span data-stu-id="9e710-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="9e710-138">Supporta l'avvio senza stato nel contesto di sicurezza corrente degli strumenti client NuGet.</span><span class="sxs-lookup"><span data-stu-id="9e710-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="9e710-139">Ad esempio, gli strumenti client NuGet non eseguirà l'elevazione dei privilegi o un'inizializzazione aggiuntiva all'esterno del protocollo di plug-in descritti più avanti.</span><span class="sxs-lookup"><span data-stu-id="9e710-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="9e710-140">Modo non interattivo, a meno che non specificato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="9e710-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="9e710-141">Rispettare la versione del protocollo negoziato plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="9e710-142">Rispondere a tutte le richieste nel periodo di tempo ragionevole.</span><span class="sxs-lookup"><span data-stu-id="9e710-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="9e710-143">Soddisfa le richieste di annullamento per qualsiasi operazione in corso.</span><span class="sxs-lookup"><span data-stu-id="9e710-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="9e710-144">Le specifiche tecniche sono descritto più dettagliatamente le specifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e710-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="9e710-145">Plug-in di Download del pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="9e710-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="9e710-146">NuGet cross-plat plug-in di autenticazione</span><span class="sxs-lookup"><span data-stu-id="9e710-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="9e710-147">Client - l'interazione di plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-147">Client - Plugin interaction</span></span>

<span data-ttu-id="9e710-148">Strumenti client NuGet e il plug-in di comunicare con JSON nei flussi standard (stdin, stdout, stderror).</span><span class="sxs-lookup"><span data-stu-id="9e710-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="9e710-149">Tutti i dati devono essere con codificata UTF-8.</span><span class="sxs-lookup"><span data-stu-id="9e710-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="9e710-150">I plug-in vengono avviate con l'argomento "-plug-in".</span><span class="sxs-lookup"><span data-stu-id="9e710-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="9e710-151">Nel caso in cui un utente avvia direttamente un plug-in eseguibile senza questo argomento, il plug-in può concedere a un messaggio informativo anziché attendere un handshake del protocollo.</span><span class="sxs-lookup"><span data-stu-id="9e710-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="9e710-152">Timeout di handshake del protocollo è 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="9e710-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="9e710-153">Il plug-in deve completare l'installazione in come oltre a una quantità possibile.</span><span class="sxs-lookup"><span data-stu-id="9e710-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="9e710-154">Strumenti client NuGet saranno supportati per di un plug-in operazioni di query passando l'indice del servizio per un'origine NuGet.</span><span class="sxs-lookup"><span data-stu-id="9e710-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="9e710-155">Un plug-in può usare l'indice del servizio per verificare la presenza di tipi di servizio supportato.</span><span class="sxs-lookup"><span data-stu-id="9e710-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="9e710-156">La comunicazione tra gli strumenti client NuGet e il plug-in è bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="9e710-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="9e710-157">Ogni richiesta ha un timeout di 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="9e710-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="9e710-158">Se le operazioni sono considerate allungamento dei tempi per il processo corrispondente deve inviare un messaggio di stato di avanzamento a evitare il timeout della richiesta. Dopo un minuto di inattività un plug-in è considerato inattivo e viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="9e710-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="9e710-159">Individuazione e l'installazione di plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-159">Plugin installation and discovery</span></span>

<span data-ttu-id="9e710-160">I plug-in verrà individuato tramite una struttura di directory basato sulle convenzioni.</span><span class="sxs-lookup"><span data-stu-id="9e710-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="9e710-161">Scenari di integrazione continua/recapito Continuo e gli utenti esperti possono usare una variabile di ambiente per eseguire l'override del comportamento.</span><span class="sxs-lookup"><span data-stu-id="9e710-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="9e710-162">`NUGET_PLUGIN_PATHS` -Definisce i plug-in che verrà usato per tale processo di NuGet, priorità sono riservate.</span><span class="sxs-lookup"><span data-stu-id="9e710-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="9e710-163">Se è impostata questa variabile di ambiente, viene eseguito l'override dell'individuazione basato sulle convenzioni.</span><span class="sxs-lookup"><span data-stu-id="9e710-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="9e710-164">Percorso utente, il percorso della home page di NuGet in `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="9e710-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="9e710-165">Questo percorso non può essere sottoposta a override.</span><span class="sxs-lookup"><span data-stu-id="9e710-165">This location cannot be overriden.</span></span> <span data-ttu-id="9e710-166">Verrà usata una directory radice diversa per plug-in .NET Core e .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9e710-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="9e710-167">Framework</span><span class="sxs-lookup"><span data-stu-id="9e710-167">Framework</span></span> | <span data-ttu-id="9e710-168">Percorso radice individuazione</span><span class="sxs-lookup"><span data-stu-id="9e710-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="9e710-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="9e710-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="9e710-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="9e710-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="9e710-171">Ogni plug-in deve essere installato nella relativa cartella.</span><span class="sxs-lookup"><span data-stu-id="9e710-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="9e710-172">Il punto di ingresso di plug-in è il nome della cartella di installazione, con le estensioni di file DLL per .NET Core ed estensione .exe per .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9e710-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="9e710-173">Attualmente non è disponibile nessuna storia utente per l'installazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="9e710-174">È semplice, basta spostare i file necessari nel percorso predeterminato.</span><span class="sxs-lookup"><span data-stu-id="9e710-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="9e710-175">Operazioni supportate</span><span class="sxs-lookup"><span data-stu-id="9e710-175">Supported operations</span></span>

<span data-ttu-id="9e710-176">Due operazioni sono supportate con il nuovo protocollo di plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="9e710-177">Nome dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-177">Operation name</span></span> | <span data-ttu-id="9e710-178">Versione minima del protocollo</span><span class="sxs-lookup"><span data-stu-id="9e710-178">Minimum protocol version</span></span> | <span data-ttu-id="9e710-179">Versione client NuGet minima</span><span class="sxs-lookup"><span data-stu-id="9e710-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="9e710-180">Scaricare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-180">Download Package</span></span> | <span data-ttu-id="9e710-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9e710-181">1.0.0</span></span> | <span data-ttu-id="9e710-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="9e710-182">4.3.0</span></span> |
| [<span data-ttu-id="9e710-183">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="9e710-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="9e710-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9e710-184">2.0.0</span></span> | <span data-ttu-id="9e710-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="9e710-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="9e710-186">Esecuzione di plug-in con il runtime corretto</span><span class="sxs-lookup"><span data-stu-id="9e710-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="9e710-187">Per NuGet negli scenari dotnet.exe, necessario essere in grado di eseguire in tale specifica del runtime del dotnet.exe plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="9e710-188">È attivo il provider di plug-in e i consumer per assicurarsi che viene utilizzata una combinazione di dotnet.exe/plugin compatibile.</span><span class="sxs-lookup"><span data-stu-id="9e710-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="9e710-189">Potrebbe verificarsi un problema potenziale con i plug-in di percorso utente quando, ad esempio, un dotnet.exe sotto il runtime 2.0 tenta di usare un plug-in scritto per il runtime 2.1.</span><span class="sxs-lookup"><span data-stu-id="9e710-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="9e710-190">Funzionalità di memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="9e710-190">Capabilities caching</span></span>

<span data-ttu-id="9e710-191">La verifica di sicurezza e le istanze di plug-in è costosa.</span><span class="sxs-lookup"><span data-stu-id="9e710-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="9e710-192">L'operazione di download accade molto più frequente rispetto dell'operazione di autenticazione, tuttavia, l'utente medio di NuGet è solo potrebbe avere un plug-in di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9e710-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="9e710-193">Per migliorare l'esperienza, NuGet memorizza nella cache le attestazioni di operazione per la richiesta specificata.</span><span class="sxs-lookup"><span data-stu-id="9e710-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="9e710-194">Questa cache è per ogni plug-in con la chiave di plug-in corso il percorso del plug-in, e la scadenza per la cache questa funzionalità è di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="9e710-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="9e710-195">La cache si trova `%LocalAppData%/NuGet/plugins-cache` e di eseguire l'override con la variabile di ambiente `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="9e710-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="9e710-196">Per cancellare questa [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), sarà possibile eseguire le variabili locali con il `plugins-cache` opzione.</span><span class="sxs-lookup"><span data-stu-id="9e710-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="9e710-197">Il `all` opzione variabili locali adesso eliminerà anche la cache di plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="9e710-198">Indice dei messaggi di protocollo</span><span class="sxs-lookup"><span data-stu-id="9e710-198">Protocol messages index</span></span>

<span data-ttu-id="9e710-199">Versione del protocollo *1.0.0* messaggi:</span><span class="sxs-lookup"><span data-stu-id="9e710-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="9e710-200">Chiudi</span><span class="sxs-lookup"><span data-stu-id="9e710-200">Close</span></span>
    * <span data-ttu-id="9e710-201">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="9e710-202">La richiesta non conterrà alcun payload</span><span class="sxs-lookup"><span data-stu-id="9e710-202">The request will contain no payload</span></span>
    * <span data-ttu-id="9e710-203">È prevista alcuna risposta.</span><span class="sxs-lookup"><span data-stu-id="9e710-203">No response is expected.</span></span>  <span data-ttu-id="9e710-204">La risposta appropriata è per il processo di plug-in uscire immediatamente.</span><span class="sxs-lookup"><span data-stu-id="9e710-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="9e710-205">Copiare i file nel pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-205">Copy files in package</span></span>
    * <span data-ttu-id="9e710-206">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="9e710-207">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-207">The request will contain:</span></span>
        * <span data-ttu-id="9e710-208">l'ID del pacchetto e versione</span><span class="sxs-lookup"><span data-stu-id="9e710-208">the package ID and version</span></span>
        * <span data-ttu-id="9e710-209">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-209">the package source repository location</span></span>
        * <span data-ttu-id="9e710-210">percorso di directory di destinazione</span><span class="sxs-lookup"><span data-stu-id="9e710-210">destination directory path</span></span>
        * <span data-ttu-id="9e710-211">enumerabile di file del pacchetto da copiare nel percorso di directory di destinazione</span><span class="sxs-lookup"><span data-stu-id="9e710-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="9e710-212">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-212">A response will contain:</span></span>
        * <span data-ttu-id="9e710-213">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="9e710-214">enumerabile di percorsi completi per i file copiati nella directory di destinazione se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="9e710-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="9e710-215">Copiare il file di pacchetto (con estensione nupkg)</span><span class="sxs-lookup"><span data-stu-id="9e710-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="9e710-216">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="9e710-217">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-217">The request will contain:</span></span>
        * <span data-ttu-id="9e710-218">l'ID del pacchetto e versione</span><span class="sxs-lookup"><span data-stu-id="9e710-218">the package ID and version</span></span>
        * <span data-ttu-id="9e710-219">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-219">the package source repository location</span></span>
        * <span data-ttu-id="9e710-220">il percorso del file di destinazione</span><span class="sxs-lookup"><span data-stu-id="9e710-220">the destination file path</span></span>
    * <span data-ttu-id="9e710-221">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-221">A response will contain:</span></span>
        * <span data-ttu-id="9e710-222">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="9e710-223">Ottenere le credenziali</span><span class="sxs-lookup"><span data-stu-id="9e710-223">Get credentials</span></span>
    * <span data-ttu-id="9e710-224">Richiesta direzione: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="9e710-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="9e710-225">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-225">The request will contain:</span></span>
        * <span data-ttu-id="9e710-226">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-226">the package source repository location</span></span>
        * <span data-ttu-id="9e710-227">il codice di stato HTTP ottenuto dal repository di origine del pacchetto usando le credenziali correnti</span><span class="sxs-lookup"><span data-stu-id="9e710-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="9e710-228">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-228">A response will contain:</span></span>
        * <span data-ttu-id="9e710-229">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="9e710-230">un nome utente, se disponibile</span><span class="sxs-lookup"><span data-stu-id="9e710-230">a username, if available</span></span>
        * <span data-ttu-id="9e710-231">una password, se disponibile</span><span class="sxs-lookup"><span data-stu-id="9e710-231">a password, if available</span></span>

5.  <span data-ttu-id="9e710-232">Ottenere i file di pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-232">Get files in package</span></span>
    * <span data-ttu-id="9e710-233">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="9e710-234">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-234">The request will contain:</span></span>
        * <span data-ttu-id="9e710-235">l'ID del pacchetto e versione</span><span class="sxs-lookup"><span data-stu-id="9e710-235">the package ID and version</span></span>
        * <span data-ttu-id="9e710-236">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-236">the package source repository location</span></span>
    * <span data-ttu-id="9e710-237">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-237">A response will contain:</span></span>
        * <span data-ttu-id="9e710-238">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="9e710-239">oggetto enumerabile di percorsi di file del pacchetto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="9e710-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="9e710-240">Ottenere le attestazioni di operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-240">Get operation claims</span></span> 
    * <span data-ttu-id="9e710-241">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="9e710-242">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-242">The request will contain:</span></span>
        * <span data-ttu-id="9e710-243">il servizio Index per un'origine pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="9e710-244">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-244">the package source repository location</span></span>
    * <span data-ttu-id="9e710-245">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-245">A response will contain:</span></span>
        * <span data-ttu-id="9e710-246">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="9e710-247">oggetto enumerabile di operazioni supportate (ad esempio: download del pacchetto) se l'operazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="9e710-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="9e710-248">Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="9e710-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="9e710-249">Questo messaggio è stato aggiornato nella versione *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="9e710-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="9e710-250">È nel client per mantenere la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="9e710-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="9e710-251">Ottenere l'hash del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-251">Get package hash</span></span>
    * <span data-ttu-id="9e710-252">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="9e710-253">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-253">The request will contain:</span></span>
        * <span data-ttu-id="9e710-254">l'ID del pacchetto e versione</span><span class="sxs-lookup"><span data-stu-id="9e710-254">the package ID and version</span></span>
        * <span data-ttu-id="9e710-255">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-255">the package source repository location</span></span>
        * <span data-ttu-id="9e710-256">l'algoritmo hash</span><span class="sxs-lookup"><span data-stu-id="9e710-256">the hash algorithm</span></span>
    * <span data-ttu-id="9e710-257">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-257">A response will contain:</span></span>
        * <span data-ttu-id="9e710-258">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="9e710-259">un hash del file del pacchetto usando l'algoritmo hash richiesto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="9e710-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="9e710-260">Ottenere le versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="9e710-260">Get package versions</span></span>
    * <span data-ttu-id="9e710-261">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="9e710-262">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-262">The request will contain:</span></span>
        * <span data-ttu-id="9e710-263">l'ID del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-263">the package ID</span></span>
        * <span data-ttu-id="9e710-264">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-264">the package source repository location</span></span>
    * <span data-ttu-id="9e710-265">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-265">A response will contain:</span></span>
        * <span data-ttu-id="9e710-266">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="9e710-267">enumerabile di versioni del pacchetto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="9e710-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="9e710-268">Ottenere l'indice del servizio</span><span class="sxs-lookup"><span data-stu-id="9e710-268">Get service index</span></span>
    * <span data-ttu-id="9e710-269">Richiesta direzione: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="9e710-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="9e710-270">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-270">The request will contain:</span></span>
        * <span data-ttu-id="9e710-271">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-271">the package source repository location</span></span>
    * <span data-ttu-id="9e710-272">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-272">A response will contain:</span></span>
        * <span data-ttu-id="9e710-273">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="9e710-274">l'indice del servizio se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="9e710-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="9e710-275">Handshake</span><span class="sxs-lookup"><span data-stu-id="9e710-275">Handshake</span></span>
     * <span data-ttu-id="9e710-276">Richiesta direzione: plug-in NuGet <> –</span><span class="sxs-lookup"><span data-stu-id="9e710-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="9e710-277">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-277">The request will contain:</span></span>
         * <span data-ttu-id="9e710-278">la versione corrente del protocollo plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="9e710-279">la versione minima supportata di versione del protocollo plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="9e710-280">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-280">A response will contain:</span></span>
         * <span data-ttu-id="9e710-281">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="9e710-282">la versione del protocollo negoziato se l'operazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="9e710-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="9e710-283">Un errore comporterà la terminazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="9e710-284">inizializzare</span><span class="sxs-lookup"><span data-stu-id="9e710-284">Initialize</span></span>
     * <span data-ttu-id="9e710-285">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="9e710-286">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-286">The request will contain:</span></span>
         * <span data-ttu-id="9e710-287">la versione dello strumento client di NuGet</span><span class="sxs-lookup"><span data-stu-id="9e710-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="9e710-288">NuGet lingua del client degli strumenti efficace.</span><span class="sxs-lookup"><span data-stu-id="9e710-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="9e710-289">Si prende in considerazione l'impostazione ForceEnglishOutput, se utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9e710-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="9e710-290">il timeout di richiesta predefinito, che sostituisce il valore predefinito di protocollo.</span><span class="sxs-lookup"><span data-stu-id="9e710-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="9e710-291">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-291">A response will contain:</span></span>
         * <span data-ttu-id="9e710-292">un codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="9e710-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="9e710-293">Un errore comporterà la terminazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="9e710-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="9e710-294">Registro</span><span class="sxs-lookup"><span data-stu-id="9e710-294">Log</span></span>
     * <span data-ttu-id="9e710-295">Richiesta direzione: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="9e710-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="9e710-296">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-296">The request will contain:</span></span>
         * <span data-ttu-id="9e710-297">il livello di registrazione per la richiesta</span><span class="sxs-lookup"><span data-stu-id="9e710-297">the log level for the request</span></span>
         * <span data-ttu-id="9e710-298">un messaggio da registrare</span><span class="sxs-lookup"><span data-stu-id="9e710-298">a message to log</span></span>
     * <span data-ttu-id="9e710-299">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-299">A response will contain:</span></span>
         * <span data-ttu-id="9e710-300">un codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="9e710-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="9e710-301">Uscita dal processo di monitoraggio NuGet</span><span class="sxs-lookup"><span data-stu-id="9e710-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="9e710-302">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="9e710-303">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-303">The request will contain:</span></span>
         * <span data-ttu-id="9e710-304">l'ID di processo di NuGet</span><span class="sxs-lookup"><span data-stu-id="9e710-304">the NuGet process ID</span></span>
     * <span data-ttu-id="9e710-305">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-305">A response will contain:</span></span>
         * <span data-ttu-id="9e710-306">un codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="9e710-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="9e710-307">Prelettura del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-307">Prefetch package</span></span>
     * <span data-ttu-id="9e710-308">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="9e710-309">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-309">The request will contain:</span></span>
         * <span data-ttu-id="9e710-310">l'ID del pacchetto e versione</span><span class="sxs-lookup"><span data-stu-id="9e710-310">the package ID and version</span></span>
         * <span data-ttu-id="9e710-311">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-311">the package source repository location</span></span>
     * <span data-ttu-id="9e710-312">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-312">A response will contain:</span></span>
         * <span data-ttu-id="9e710-313">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="9e710-314">Insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="9e710-314">Set credentials</span></span>
     * <span data-ttu-id="9e710-315">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="9e710-316">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-316">The request will contain:</span></span>
         * <span data-ttu-id="9e710-317">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-317">the package source repository location</span></span>
         * <span data-ttu-id="9e710-318">l'ultimo pacchetto noti origine nome utente, se disponibile</span><span class="sxs-lookup"><span data-stu-id="9e710-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="9e710-319">l'ultima password di origine di pacchetti note, se disponibile</span><span class="sxs-lookup"><span data-stu-id="9e710-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="9e710-320">l'ultimo noti nome utente proxy, se disponibile</span><span class="sxs-lookup"><span data-stu-id="9e710-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="9e710-321">l'ultima password nota proxy, se disponibile</span><span class="sxs-lookup"><span data-stu-id="9e710-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="9e710-322">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-322">A response will contain:</span></span>
         * <span data-ttu-id="9e710-323">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="9e710-324">Livello del set di log</span><span class="sxs-lookup"><span data-stu-id="9e710-324">Set log level</span></span>
     * <span data-ttu-id="9e710-325">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="9e710-326">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-326">The request will contain:</span></span>
         * <span data-ttu-id="9e710-327">il livello di registrazione predefinito</span><span class="sxs-lookup"><span data-stu-id="9e710-327">the default log level</span></span>
     * <span data-ttu-id="9e710-328">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-328">A response will contain:</span></span>
         * <span data-ttu-id="9e710-329">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="9e710-330">Versione del protocollo *2.0.0* messaggi</span><span class="sxs-lookup"><span data-stu-id="9e710-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="9e710-331">Ottenere le attestazioni di operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-331">Get Operation Claims</span></span>

* <span data-ttu-id="9e710-332">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="9e710-333">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-333">The request will contain:</span></span>
        * <span data-ttu-id="9e710-334">il servizio Index per un'origine pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="9e710-335">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9e710-335">the package source repository location</span></span>
    * <span data-ttu-id="9e710-336">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="9e710-336">A response will contain:</span></span>
        * <span data-ttu-id="9e710-337">un codice di risposta che indica il risultato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="9e710-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="9e710-338">oggetto enumerabile di operazioni supportate se l'operazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="9e710-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="9e710-339">Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="9e710-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="9e710-340">Se l'origine di indice e pacchetto del servizio è null, il plug-in può rispondere con l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9e710-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="9e710-341">Ottenere le credenziali di autenticazione</span><span class="sxs-lookup"><span data-stu-id="9e710-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="9e710-342">Richiesta direzione: NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="9e710-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="9e710-343">Conterrà la richiesta:</span><span class="sxs-lookup"><span data-stu-id="9e710-343">The request will contain:</span></span>
    * <span data-ttu-id="9e710-344">URI</span><span class="sxs-lookup"><span data-stu-id="9e710-344">Uri</span></span>
    * <span data-ttu-id="9e710-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="9e710-345">isRetry</span></span>
    * <span data-ttu-id="9e710-346">Non interattive</span><span class="sxs-lookup"><span data-stu-id="9e710-346">NonInteractive</span></span>
    * <span data-ttu-id="9e710-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="9e710-347">CanShowDialog</span></span>
* <span data-ttu-id="9e710-348">Conterrà una risposta</span><span class="sxs-lookup"><span data-stu-id="9e710-348">A response will contain</span></span>
    * <span data-ttu-id="9e710-349">Nome utente</span><span class="sxs-lookup"><span data-stu-id="9e710-349">Username</span></span>
    * <span data-ttu-id="9e710-350">Password</span><span class="sxs-lookup"><span data-stu-id="9e710-350">Password</span></span>
    * <span data-ttu-id="9e710-351">Messaggio</span><span class="sxs-lookup"><span data-stu-id="9e710-351">Message</span></span>
    * <span data-ttu-id="9e710-352">Elenco dei tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="9e710-352">List of Auth Types</span></span>
    * <span data-ttu-id="9e710-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="9e710-353">MessageResponseCode</span></span>