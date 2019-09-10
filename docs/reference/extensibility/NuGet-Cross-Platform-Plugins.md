---
title: Plug-in NuGet multipiattaforma
description: Plug-in NuGet multipiattaforma per NuGet. exe, dotnet. exe, MSBuild. exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815312"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="ce38f-103">Plug-in NuGet multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="ce38f-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="ce38f-104">È stato aggiunto il supporto NuGet 4.8 + per i plug-in di multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="ce38f-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="ce38f-105">Questa operazione è stata realizzata con creando un nuovo modello di estendibilità dei plug-in, che deve essere conforme a un set di regole di funzionamento rigoroso.</span><span class="sxs-lookup"><span data-stu-id="ce38f-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="ce38f-106">I plug-in sono file eseguibili autonomi (eseguibili in .NET Core World), che i client NuGet avviano in un processo separato.</span><span class="sxs-lookup"><span data-stu-id="ce38f-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="ce38f-107">Si tratta di una vera e propria scrittura, Esegui il plug-in Everywhere.</span><span class="sxs-lookup"><span data-stu-id="ce38f-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="ce38f-108">Funzionerà con tutti gli strumenti client NuGet.</span><span class="sxs-lookup"><span data-stu-id="ce38f-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="ce38f-109">I plug-in possono essere .NET Framework (NuGet. exe, MSBuild. exe e Visual Studio) o .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="ce38f-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="ce38f-110">Viene definito un protocollo di comunicazione con versione tra il client NuGet e il plug-in.</span><span class="sxs-lookup"><span data-stu-id="ce38f-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="ce38f-111">Durante l'handshake di avvio, i 2 processi negoziano la versione del protocollo.</span><span class="sxs-lookup"><span data-stu-id="ce38f-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="ce38f-112">Per coprire tutti gli scenari di strumenti client NuGet, è necessario disporre sia di un .NET Framework che di un plug-in .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ce38f-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="ce38f-113">Di seguito vengono descritte le combinazioni client/Framework dei plug-in.</span><span class="sxs-lookup"><span data-stu-id="ce38f-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="ce38f-114">Strumento client</span><span class="sxs-lookup"><span data-stu-id="ce38f-114">Client tool</span></span>  | <span data-ttu-id="ce38f-115">Framework</span><span class="sxs-lookup"><span data-stu-id="ce38f-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="ce38f-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ce38f-116">Visual Studio</span></span> | <span data-ttu-id="ce38f-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ce38f-117">.NET Framework</span></span> |
| <span data-ttu-id="ce38f-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="ce38f-118">dotnet.exe</span></span> | <span data-ttu-id="ce38f-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ce38f-119">.NET Core</span></span> |
| <span data-ttu-id="ce38f-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="ce38f-120">NuGet.exe</span></span> | <span data-ttu-id="ce38f-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ce38f-121">.NET Framework</span></span> |
| <span data-ttu-id="ce38f-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="ce38f-122">MSBuild.exe</span></span> | <span data-ttu-id="ce38f-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ce38f-123">.NET Framework</span></span> |
| <span data-ttu-id="ce38f-124">NuGet. exe in mono</span><span class="sxs-lookup"><span data-stu-id="ce38f-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="ce38f-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ce38f-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="ce38f-126">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="ce38f-126">How does it work</span></span>

<span data-ttu-id="ce38f-127">Il flusso di lavoro di alto livello può essere descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="ce38f-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="ce38f-128">NuGet individua i plug-in disponibili.</span><span class="sxs-lookup"><span data-stu-id="ce38f-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="ce38f-129">Quando applicabile, NuGet esegue l'iterazione dei plug-in in ordine di priorità e li avvia uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="ce38f-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="ce38f-130">NuGet userà il primo plug-in che può servire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="ce38f-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="ce38f-131">I plug-in verranno arrestati quando non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="ce38f-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="ce38f-132">Requisiti generali per il plug-in</span><span class="sxs-lookup"><span data-stu-id="ce38f-132">General plugin requirements</span></span>

<span data-ttu-id="ce38f-133">La versione del protocollo corrente è *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="ce38f-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="ce38f-134">In questa versione, i requisiti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ce38f-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="ce38f-135">Disporre di assembly di firma Authenticode attendibili validi che vengono eseguiti in Windows e mono.</span><span class="sxs-lookup"><span data-stu-id="ce38f-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="ce38f-136">Non esiste ancora un requisito di attendibilità speciale per gli assembly eseguiti in Linux e Mac.</span><span class="sxs-lookup"><span data-stu-id="ce38f-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="ce38f-137">Problema pertinente</span><span class="sxs-lookup"><span data-stu-id="ce38f-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="ce38f-138">Supportare l'avvio senza stato nel contesto di sicurezza corrente degli strumenti client NuGet.</span><span class="sxs-lookup"><span data-stu-id="ce38f-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="ce38f-139">Ad esempio, gli strumenti client NuGet non eseguono l'elevazione dei privilegi o l'inizializzazione aggiuntiva all'esterno del protocollo plug-in descritto più avanti.</span><span class="sxs-lookup"><span data-stu-id="ce38f-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="ce38f-140">Essere non interattivo, a meno che non venga specificato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="ce38f-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="ce38f-141">Rispettare la versione del protocollo di plug-in negoziato.</span><span class="sxs-lookup"><span data-stu-id="ce38f-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="ce38f-142">Rispondere a tutte le richieste entro un periodo di tempo ragionevole.</span><span class="sxs-lookup"><span data-stu-id="ce38f-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="ce38f-143">Rispettare le richieste di annullamento per qualsiasi operazione in corso.</span><span class="sxs-lookup"><span data-stu-id="ce38f-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="ce38f-144">Le specifiche tecniche sono descritte più dettagliatamente nelle specifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="ce38f-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="ce38f-145">Plug-in di download del pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="ce38f-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="ce38f-146">Plug-in autenticazione NuGet Cross Plat</span><span class="sxs-lookup"><span data-stu-id="ce38f-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="ce38f-147">Interazione client-plug-in</span><span class="sxs-lookup"><span data-stu-id="ce38f-147">Client - Plugin interaction</span></span>

<span data-ttu-id="ce38f-148">Gli strumenti client NuGet e i plug-in comunicano con JSON su flussi standard (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="ce38f-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="ce38f-149">Tutti i dati devono essere codificati in UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ce38f-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="ce38f-150">I plug-in vengono avviati con l'argomento "-plugin".</span><span class="sxs-lookup"><span data-stu-id="ce38f-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="ce38f-151">Se un utente avvia direttamente un eseguibile del plug-in senza questo argomento, il plug-in può fornire un messaggio informativo invece di attendere un handshake del protocollo.</span><span class="sxs-lookup"><span data-stu-id="ce38f-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="ce38f-152">Il timeout dell'handshake del protocollo è di 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="ce38f-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="ce38f-153">Il plug-in deve completare il programma di installazione nel minor tempo possibile.</span><span class="sxs-lookup"><span data-stu-id="ce38f-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="ce38f-154">Gli strumenti client NuGet eseguiranno una query sulle operazioni supportate da un plug-in tramite il passaggio dell'indice del servizio per un'origine NuGet.</span><span class="sxs-lookup"><span data-stu-id="ce38f-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="ce38f-155">Un plug-in può usare l'indice del servizio per verificare la presenza di tipi di servizio supportati.</span><span class="sxs-lookup"><span data-stu-id="ce38f-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="ce38f-156">La comunicazione tra gli strumenti client NuGet e il plug-in è bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="ce38f-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="ce38f-157">Ogni richiesta ha un timeout di 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="ce38f-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="ce38f-158">Se le operazioni dovrebbero richiedere più tempo, il rispettivo processo deve inviare un messaggio di stato per impedire il timeout della richiesta. Dopo 1 minuto di inattività, un plug-in viene considerato inattivo e viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="ce38f-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="ce38f-159">Installazione e individuazione di plug-in</span><span class="sxs-lookup"><span data-stu-id="ce38f-159">Plugin installation and discovery</span></span>

<span data-ttu-id="ce38f-160">I plug-in verranno individuati tramite una struttura di directory basata sulla convenzione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="ce38f-161">Gli scenari di integrazione continua/distribuzione continua e gli utenti esperti possono usare variabili di ambiente per eseguire l'override del comportamento.</span><span class="sxs-lookup"><span data-stu-id="ce38f-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="ce38f-162">Si noti `NUGET_NETFX_PLUGIN_PATHS` che `NUGET_NETCORE_PLUGIN_PATHS` e sono disponibili solo con la versione 5.3 + degli strumenti NuGet e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="ce38f-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="ce38f-163">`NUGET_NETFX_PLUGIN_PATHS`: definisce i plug-in che verranno usati dagli strumenti basati su .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="ce38f-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="ce38f-164">Ha la precedenza `NUGET_PLUGIN_PATHS`su.</span><span class="sxs-lookup"><span data-stu-id="ce38f-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="ce38f-165">(Solo NuGet versione 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="ce38f-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="ce38f-166">`NUGET_NETCORE_PLUGIN_PATHS`: definisce i plug-in che verranno usati dagli strumenti basati su .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="ce38f-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="ce38f-167">Ha la precedenza `NUGET_PLUGIN_PATHS`su.</span><span class="sxs-lookup"><span data-stu-id="ce38f-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="ce38f-168">(Solo NuGet versione 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="ce38f-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="ce38f-169">`NUGET_PLUGIN_PATHS`: definisce i plug-in che verranno usati per il processo NuGet, priorità riservata.</span><span class="sxs-lookup"><span data-stu-id="ce38f-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="ce38f-170">Se questa variabile di ambiente è impostata, sostituisce l'individuazione basata sulla convenzione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="ce38f-171">Viene ignorato se viene specificata una delle variabili specifiche del Framework.</span><span class="sxs-lookup"><span data-stu-id="ce38f-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="ce38f-172">Utente-location, il percorso Home di NuGet `%UserProfile%/.nuget/plugins`in.</span><span class="sxs-lookup"><span data-stu-id="ce38f-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="ce38f-173">Non è possibile eseguire l'override di questo percorso.</span><span class="sxs-lookup"><span data-stu-id="ce38f-173">This location cannot be overriden.</span></span> <span data-ttu-id="ce38f-174">Verrà usata una directory radice diversa per i plug-in .NET Core e .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ce38f-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="ce38f-175">Framework</span><span class="sxs-lookup"><span data-stu-id="ce38f-175">Framework</span></span> | <span data-ttu-id="ce38f-176">Percorso di individuazione radice</span><span class="sxs-lookup"><span data-stu-id="ce38f-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="ce38f-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ce38f-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="ce38f-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ce38f-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="ce38f-179">Ogni plug-in deve essere installato in una cartella specifica.</span><span class="sxs-lookup"><span data-stu-id="ce38f-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="ce38f-180">Il punto di ingresso del plug-in sarà il nome della cartella installata, con le estensioni dll per .NET Core e l'estensione exe per .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ce38f-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="ce38f-181">Attualmente non è disponibile alcuna storia utente per l'installazione dei plug-in.</span><span class="sxs-lookup"><span data-stu-id="ce38f-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="ce38f-182">È semplice quanto lo spostamento dei file necessari nella posizione predeterminata.</span><span class="sxs-lookup"><span data-stu-id="ce38f-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="ce38f-183">Operazioni supportate</span><span class="sxs-lookup"><span data-stu-id="ce38f-183">Supported operations</span></span>

<span data-ttu-id="ce38f-184">Sono supportate due operazioni nel nuovo protocollo plug-in.</span><span class="sxs-lookup"><span data-stu-id="ce38f-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="ce38f-185">Nome operazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-185">Operation name</span></span> | <span data-ttu-id="ce38f-186">Versione minima del protocollo</span><span class="sxs-lookup"><span data-stu-id="ce38f-186">Minimum protocol version</span></span> | <span data-ttu-id="ce38f-187">Versione minima del client NuGet</span><span class="sxs-lookup"><span data-stu-id="ce38f-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="ce38f-188">Scarica pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-188">Download Package</span></span> | <span data-ttu-id="ce38f-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="ce38f-189">1.0.0</span></span> | <span data-ttu-id="ce38f-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="ce38f-190">4.3.0</span></span> |
| [<span data-ttu-id="ce38f-191">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="ce38f-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="ce38f-192">2.0.0</span></span> | <span data-ttu-id="ce38f-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="ce38f-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="ce38f-194">Esecuzione di plug-in nel runtime corretto</span><span class="sxs-lookup"><span data-stu-id="ce38f-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="ce38f-195">Per gli scenari di NuGet in dotnet. exe, è necessario che i plug-in siano in grado di eseguire il runtime specifico di DotNet. exe.</span><span class="sxs-lookup"><span data-stu-id="ce38f-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="ce38f-196">Si tratta del provider di plug-in e del consumer per assicurarsi che venga usata una combinazione dotnet. exe/plugin compatibile.</span><span class="sxs-lookup"><span data-stu-id="ce38f-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="ce38f-197">Un potenziale problema può verificarsi con i plug-in della posizione utente quando, ad esempio, un file dotnet. exe nel runtime di 2,0 prova a usare un plug-in scritto per il runtime di 2,1.</span><span class="sxs-lookup"><span data-stu-id="ce38f-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="ce38f-198">Caching delle funzionalità</span><span class="sxs-lookup"><span data-stu-id="ce38f-198">Capabilities caching</span></span>

<span data-ttu-id="ce38f-199">La verifica della sicurezza e la creazione di istanze dei plug-in sono costose.</span><span class="sxs-lookup"><span data-stu-id="ce38f-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="ce38f-200">L'operazione di download si verifica in modo più frequente rispetto all'operazione di autenticazione, ma è probabile che l'utente NuGet medio disponga solo di un plug-in di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="ce38f-201">Per migliorare l'esperienza, NuGet memorizza nella cache le attestazioni dell'operazione per la richiesta specificata.</span><span class="sxs-lookup"><span data-stu-id="ce38f-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="ce38f-202">Questa cache è per plug-in con la chiave del plug-in che è il percorso del plug-in e la scadenza della cache delle funzionalità è di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="ce38f-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="ce38f-203">La cache si trova in `%LocalAppData%/NuGet/plugins-cache` ed è sottoposta a override con la `NUGET_PLUGINS_CACHE_PATH`variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="ce38f-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="ce38f-204">Per cancellare la [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), è possibile eseguire il comando locals con l' `plugins-cache` opzione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="ce38f-205">L' `all` opzione locals ora eliminerà anche la cache dei plug-in.</span><span class="sxs-lookup"><span data-stu-id="ce38f-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="ce38f-206">Indice dei messaggi di protocollo</span><span class="sxs-lookup"><span data-stu-id="ce38f-206">Protocol messages index</span></span>

<span data-ttu-id="ce38f-207">Messaggi versione protocollo *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="ce38f-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="ce38f-208">Chiudi</span><span class="sxs-lookup"><span data-stu-id="ce38f-208">Close</span></span>
    * <span data-ttu-id="ce38f-209">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="ce38f-210">La richiesta non conterrà alcun payload</span><span class="sxs-lookup"><span data-stu-id="ce38f-210">The request will contain no payload</span></span>
    * <span data-ttu-id="ce38f-211">Non è prevista alcuna risposta.</span><span class="sxs-lookup"><span data-stu-id="ce38f-211">No response is expected.</span></span>  <span data-ttu-id="ce38f-212">La risposta corretta è che il processo del plug-in viene immediatamente terminato.</span><span class="sxs-lookup"><span data-stu-id="ce38f-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="ce38f-213">Copia i file nel pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-213">Copy files in package</span></span>
    * <span data-ttu-id="ce38f-214">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="ce38f-215">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-215">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-216">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-216">the package ID and version</span></span>
        * <span data-ttu-id="ce38f-217">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-217">the package source repository location</span></span>
        * <span data-ttu-id="ce38f-218">percorso directory di destinazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-218">destination directory path</span></span>
        * <span data-ttu-id="ce38f-219">oggetto enumerabile di file nel pacchetto da copiare nel percorso della directory di destinazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="ce38f-220">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-220">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-221">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="ce38f-222">oggetto enumerabile di percorsi completi per i file copiati nella directory di destinazione se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="ce38f-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="ce38f-223">Copiare il file del pacchetto (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="ce38f-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="ce38f-224">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="ce38f-225">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-225">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-226">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-226">the package ID and version</span></span>
        * <span data-ttu-id="ce38f-227">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-227">the package source repository location</span></span>
        * <span data-ttu-id="ce38f-228">percorso del file di destinazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-228">the destination file path</span></span>
    * <span data-ttu-id="ce38f-229">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-229">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-230">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="ce38f-231">Ottenere le credenziali</span><span class="sxs-lookup"><span data-stu-id="ce38f-231">Get credentials</span></span>
    * <span data-ttu-id="ce38f-232">Direzione della richiesta: plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="ce38f-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="ce38f-233">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-233">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-234">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-234">the package source repository location</span></span>
        * <span data-ttu-id="ce38f-235">codice di stato HTTP ottenuto dal repository di origine del pacchetto con le credenziali correnti</span><span class="sxs-lookup"><span data-stu-id="ce38f-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="ce38f-236">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-236">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-237">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="ce38f-238">un nome utente, se disponibile</span><span class="sxs-lookup"><span data-stu-id="ce38f-238">a username, if available</span></span>
        * <span data-ttu-id="ce38f-239">una password, se disponibile</span><span class="sxs-lookup"><span data-stu-id="ce38f-239">a password, if available</span></span>

5.  <span data-ttu-id="ce38f-240">Ottenere i file nel pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-240">Get files in package</span></span>
    * <span data-ttu-id="ce38f-241">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="ce38f-242">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-242">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-243">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-243">the package ID and version</span></span>
        * <span data-ttu-id="ce38f-244">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-244">the package source repository location</span></span>
    * <span data-ttu-id="ce38f-245">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-245">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-246">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="ce38f-247">oggetto enumerabile di percorsi di file nel pacchetto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="ce38f-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="ce38f-248">Ottenere le attestazioni dell'operazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-248">Get operation claims</span></span> 
    * <span data-ttu-id="ce38f-249">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="ce38f-250">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-250">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-251">il servizio index. JSON per un'origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="ce38f-252">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-252">the package source repository location</span></span>
    * <span data-ttu-id="ce38f-253">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-253">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-254">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="ce38f-255">oggetto enumerabile di operazioni supportate (ad esempio, download del pacchetto) se l'operazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="ce38f-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="ce38f-256">Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="ce38f-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="ce38f-257">Questo messaggio è stato aggiornato nella versione *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="ce38f-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="ce38f-258">Il client mantiene la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="ce38f-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="ce38f-259">Ottieni hash pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-259">Get package hash</span></span>
    * <span data-ttu-id="ce38f-260">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="ce38f-261">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-261">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-262">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-262">the package ID and version</span></span>
        * <span data-ttu-id="ce38f-263">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-263">the package source repository location</span></span>
        * <span data-ttu-id="ce38f-264">algoritmo hash</span><span class="sxs-lookup"><span data-stu-id="ce38f-264">the hash algorithm</span></span>
    * <span data-ttu-id="ce38f-265">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-265">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-266">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="ce38f-267">hash del file del pacchetto che utilizza l'algoritmo hash richiesto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="ce38f-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="ce38f-268">Ottenere le versioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-268">Get package versions</span></span>
    * <span data-ttu-id="ce38f-269">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="ce38f-270">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-270">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-271">ID del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-271">the package ID</span></span>
        * <span data-ttu-id="ce38f-272">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-272">the package source repository location</span></span>
    * <span data-ttu-id="ce38f-273">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-273">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-274">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="ce38f-275">oggetto enumerabile di versioni del pacchetto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="ce38f-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="ce38f-276">Ottenere l'indice del servizio</span><span class="sxs-lookup"><span data-stu-id="ce38f-276">Get service index</span></span>
    * <span data-ttu-id="ce38f-277">Direzione della richiesta: plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="ce38f-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="ce38f-278">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-278">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-279">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-279">the package source repository location</span></span>
    * <span data-ttu-id="ce38f-280">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-280">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-281">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="ce38f-282">Indice del servizio se l'operazione è stata completata correttamente</span><span class="sxs-lookup"><span data-stu-id="ce38f-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="ce38f-283">Handshake</span><span class="sxs-lookup"><span data-stu-id="ce38f-283">Handshake</span></span>
     * <span data-ttu-id="ce38f-284">Direzione della richiesta:  Plug-in NuGet <-></span><span class="sxs-lookup"><span data-stu-id="ce38f-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="ce38f-285">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-285">The request will contain:</span></span>
         * <span data-ttu-id="ce38f-286">versione corrente del protocollo plugin</span><span class="sxs-lookup"><span data-stu-id="ce38f-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="ce38f-287">versione minima supportata del protocollo plug-in</span><span class="sxs-lookup"><span data-stu-id="ce38f-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="ce38f-288">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-288">A response will contain:</span></span>
         * <span data-ttu-id="ce38f-289">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="ce38f-290">versione del protocollo negoziata se l'operazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="ce38f-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="ce38f-291">Un errore provocherà la terminazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="ce38f-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="ce38f-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="ce38f-292">Initialize</span></span>
     * <span data-ttu-id="ce38f-293">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="ce38f-294">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-294">The request will contain:</span></span>
         * <span data-ttu-id="ce38f-295">versione dello strumento client NuGet</span><span class="sxs-lookup"><span data-stu-id="ce38f-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="ce38f-296">linguaggio efficace dello strumento client NuGet.</span><span class="sxs-lookup"><span data-stu-id="ce38f-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="ce38f-297">Ciò prende in considerazione l'impostazione ForceEnglishOutput, se usata.</span><span class="sxs-lookup"><span data-stu-id="ce38f-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="ce38f-298">timeout della richiesta predefinito, che sostituisce l'impostazione predefinita del protocollo.</span><span class="sxs-lookup"><span data-stu-id="ce38f-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="ce38f-299">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-299">A response will contain:</span></span>
         * <span data-ttu-id="ce38f-300">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="ce38f-301">Un errore provocherà la terminazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="ce38f-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="ce38f-302">Log</span><span class="sxs-lookup"><span data-stu-id="ce38f-302">Log</span></span>
     * <span data-ttu-id="ce38f-303">Direzione della richiesta: plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="ce38f-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="ce38f-304">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-304">The request will contain:</span></span>
         * <span data-ttu-id="ce38f-305">livello di registrazione per la richiesta</span><span class="sxs-lookup"><span data-stu-id="ce38f-305">the log level for the request</span></span>
         * <span data-ttu-id="ce38f-306">messaggio da registrare</span><span class="sxs-lookup"><span data-stu-id="ce38f-306">a message to log</span></span>
     * <span data-ttu-id="ce38f-307">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-307">A response will contain:</span></span>
         * <span data-ttu-id="ce38f-308">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="ce38f-309">Esegui monitoraggio uscita processo NuGet</span><span class="sxs-lookup"><span data-stu-id="ce38f-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="ce38f-310">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="ce38f-311">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-311">The request will contain:</span></span>
         * <span data-ttu-id="ce38f-312">ID processo NuGet</span><span class="sxs-lookup"><span data-stu-id="ce38f-312">the NuGet process ID</span></span>
     * <span data-ttu-id="ce38f-313">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-313">A response will contain:</span></span>
         * <span data-ttu-id="ce38f-314">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="ce38f-315">Prelettura del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-315">Prefetch package</span></span>
     * <span data-ttu-id="ce38f-316">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="ce38f-317">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-317">The request will contain:</span></span>
         * <span data-ttu-id="ce38f-318">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-318">the package ID and version</span></span>
         * <span data-ttu-id="ce38f-319">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-319">the package source repository location</span></span>
     * <span data-ttu-id="ce38f-320">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-320">A response will contain:</span></span>
         * <span data-ttu-id="ce38f-321">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="ce38f-322">Imposta credenziali</span><span class="sxs-lookup"><span data-stu-id="ce38f-322">Set credentials</span></span>
     * <span data-ttu-id="ce38f-323">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="ce38f-324">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-324">The request will contain:</span></span>
         * <span data-ttu-id="ce38f-325">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-325">the package source repository location</span></span>
         * <span data-ttu-id="ce38f-326">ultimo nome utente di origine del pacchetto noto, se disponibile</span><span class="sxs-lookup"><span data-stu-id="ce38f-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="ce38f-327">ultima password di origine del pacchetto nota, se disponibile</span><span class="sxs-lookup"><span data-stu-id="ce38f-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="ce38f-328">ultimo nome utente del proxy noto, se disponibile</span><span class="sxs-lookup"><span data-stu-id="ce38f-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="ce38f-329">ultima password del proxy nota, se disponibile</span><span class="sxs-lookup"><span data-stu-id="ce38f-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="ce38f-330">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-330">A response will contain:</span></span>
         * <span data-ttu-id="ce38f-331">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="ce38f-332">Impostare il livello di registrazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-332">Set log level</span></span>
     * <span data-ttu-id="ce38f-333">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="ce38f-334">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-334">The request will contain:</span></span>
         * <span data-ttu-id="ce38f-335">livello di registrazione predefinito</span><span class="sxs-lookup"><span data-stu-id="ce38f-335">the default log level</span></span>
     * <span data-ttu-id="ce38f-336">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-336">A response will contain:</span></span>
         * <span data-ttu-id="ce38f-337">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="ce38f-338">Messaggi della versione *2.0.0* del protocollo</span><span class="sxs-lookup"><span data-stu-id="ce38f-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="ce38f-339">Ottenere le attestazioni dell'operazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-339">Get Operation Claims</span></span>

* <span data-ttu-id="ce38f-340">Direzione della richiesta:  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="ce38f-341">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-341">The request will contain:</span></span>
        * <span data-ttu-id="ce38f-342">il servizio index. JSON per un'origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="ce38f-343">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="ce38f-343">the package source repository location</span></span>
    * <span data-ttu-id="ce38f-344">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-344">A response will contain:</span></span>
        * <span data-ttu-id="ce38f-345">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="ce38f-346">oggetto enumerabile di operazioni supportate se l'operazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="ce38f-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="ce38f-347">Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="ce38f-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="ce38f-348">Se l'indice del servizio e l'origine del pacchetto sono null, il plug-in può rispondere con l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ce38f-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="ce38f-349">Ottenere le credenziali di autenticazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="ce38f-350">Direzione della richiesta: Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="ce38f-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="ce38f-351">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="ce38f-351">The request will contain:</span></span>
    * <span data-ttu-id="ce38f-352">URI</span><span class="sxs-lookup"><span data-stu-id="ce38f-352">Uri</span></span>
    * <span data-ttu-id="ce38f-353">numero di tentativi</span><span class="sxs-lookup"><span data-stu-id="ce38f-353">isRetry</span></span>
    * <span data-ttu-id="ce38f-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ce38f-354">NonInteractive</span></span>
    * <span data-ttu-id="ce38f-355">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="ce38f-355">CanShowDialog</span></span>
* <span data-ttu-id="ce38f-356">Una risposta conterrà</span><span class="sxs-lookup"><span data-stu-id="ce38f-356">A response will contain</span></span>
    * <span data-ttu-id="ce38f-357">Nome utente</span><span class="sxs-lookup"><span data-stu-id="ce38f-357">Username</span></span>
    * <span data-ttu-id="ce38f-358">Password</span><span class="sxs-lookup"><span data-stu-id="ce38f-358">Password</span></span>
    * <span data-ttu-id="ce38f-359">Messaggio</span><span class="sxs-lookup"><span data-stu-id="ce38f-359">Message</span></span>
    * <span data-ttu-id="ce38f-360">Elenco di tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="ce38f-360">List of Auth Types</span></span>
    * <span data-ttu-id="ce38f-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="ce38f-361">MessageResponseCode</span></span>
