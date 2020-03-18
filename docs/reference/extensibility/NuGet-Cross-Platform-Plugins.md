---
title: Plug-in NuGet multipiattaforma
description: Plug-in NuGet multipiattaforma per NuGet. exe, dotnet. exe, MSBuild. exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429108"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="74830-103">Plug-in NuGet multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="74830-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="74830-104">È stato aggiunto il supporto NuGet 4.8 + per i plug-in di multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="74830-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="74830-105">Questa operazione è stata realizzata con creando un nuovo modello di estendibilità dei plug-in, che deve essere conforme a un set di regole di funzionamento rigoroso.</span><span class="sxs-lookup"><span data-stu-id="74830-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="74830-106">I plug-in sono file eseguibili autonomi (eseguibili in .NET Core World), che i client NuGet avviano in un processo separato.</span><span class="sxs-lookup"><span data-stu-id="74830-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="74830-107">Si tratta di una vera e propria scrittura, Esegui il plug-in Everywhere.</span><span class="sxs-lookup"><span data-stu-id="74830-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="74830-108">Funzionerà con tutti gli strumenti client NuGet.</span><span class="sxs-lookup"><span data-stu-id="74830-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="74830-109">I plug-in possono essere .NET Framework (NuGet. exe, MSBuild. exe e Visual Studio) o .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="74830-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="74830-110">Viene definito un protocollo di comunicazione con versione tra il client NuGet e il plug-in.</span><span class="sxs-lookup"><span data-stu-id="74830-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="74830-111">Durante l'handshake di avvio, i 2 processi negoziano la versione del protocollo.</span><span class="sxs-lookup"><span data-stu-id="74830-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="74830-112">Per coprire tutti gli scenari di strumenti client NuGet, è necessario disporre sia di un .NET Framework che di un plug-in .NET Core.</span><span class="sxs-lookup"><span data-stu-id="74830-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="74830-113">Di seguito vengono descritte le combinazioni client/Framework dei plug-in.</span><span class="sxs-lookup"><span data-stu-id="74830-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="74830-114">Strumento client</span><span class="sxs-lookup"><span data-stu-id="74830-114">Client tool</span></span>  | <span data-ttu-id="74830-115">Framework</span><span class="sxs-lookup"><span data-stu-id="74830-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="74830-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74830-116">Visual Studio</span></span> | <span data-ttu-id="74830-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="74830-117">.NET Framework</span></span> |
| <span data-ttu-id="74830-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="74830-118">dotnet.exe</span></span> | <span data-ttu-id="74830-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="74830-119">.NET Core</span></span> |
| <span data-ttu-id="74830-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="74830-120">NuGet.exe</span></span> | <span data-ttu-id="74830-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="74830-121">.NET Framework</span></span> |
| <span data-ttu-id="74830-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="74830-122">MSBuild.exe</span></span> | <span data-ttu-id="74830-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="74830-123">.NET Framework</span></span> |
| <span data-ttu-id="74830-124">NuGet. exe in mono</span><span class="sxs-lookup"><span data-stu-id="74830-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="74830-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="74830-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="74830-126">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="74830-126">How does it work</span></span>

<span data-ttu-id="74830-127">Il flusso di lavoro di alto livello può essere descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="74830-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="74830-128">NuGet individua i plug-in disponibili.</span><span class="sxs-lookup"><span data-stu-id="74830-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="74830-129">Quando applicabile, NuGet esegue l'iterazione dei plug-in in ordine di priorità e li avvia uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="74830-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="74830-130">NuGet userà il primo plug-in che può servire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="74830-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="74830-131">I plug-in verranno arrestati quando non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="74830-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="74830-132">Requisiti generali per il plug-in</span><span class="sxs-lookup"><span data-stu-id="74830-132">General plugin requirements</span></span>

<span data-ttu-id="74830-133">La versione del protocollo corrente è *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="74830-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="74830-134">In questa versione, i requisiti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="74830-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="74830-135">Disporre di assembly di firma Authenticode attendibili validi che vengono eseguiti in Windows e mono.</span><span class="sxs-lookup"><span data-stu-id="74830-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="74830-136">Non esiste ancora un requisito di attendibilità speciale per gli assembly eseguiti in Linux e Mac.</span><span class="sxs-lookup"><span data-stu-id="74830-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="74830-137">Problema pertinente</span><span class="sxs-lookup"><span data-stu-id="74830-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="74830-138">Supportare l'avvio senza stato nel contesto di sicurezza corrente degli strumenti client NuGet.</span><span class="sxs-lookup"><span data-stu-id="74830-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="74830-139">Ad esempio, gli strumenti client NuGet non eseguono l'elevazione dei privilegi o l'inizializzazione aggiuntiva all'esterno del protocollo plug-in descritto più avanti.</span><span class="sxs-lookup"><span data-stu-id="74830-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="74830-140">Essere non interattivo, a meno che non venga specificato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="74830-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="74830-141">Rispettare la versione del protocollo di plug-in negoziato.</span><span class="sxs-lookup"><span data-stu-id="74830-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="74830-142">Rispondere a tutte le richieste entro un periodo di tempo ragionevole.</span><span class="sxs-lookup"><span data-stu-id="74830-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="74830-143">Rispettare le richieste di annullamento per qualsiasi operazione in corso.</span><span class="sxs-lookup"><span data-stu-id="74830-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="74830-144">Le specifiche tecniche sono descritte più dettagliatamente nelle specifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="74830-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="74830-145">Plug-in di download del pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="74830-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="74830-146">Plug-in autenticazione NuGet Cross Plat</span><span class="sxs-lookup"><span data-stu-id="74830-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="74830-147">Interazione client-plug-in</span><span class="sxs-lookup"><span data-stu-id="74830-147">Client - Plugin interaction</span></span>

<span data-ttu-id="74830-148">Gli strumenti client NuGet e i plug-in comunicano con JSON su flussi standard (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="74830-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="74830-149">Tutti i dati devono essere codificati in UTF-8.</span><span class="sxs-lookup"><span data-stu-id="74830-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="74830-150">I plug-in vengono avviati con l'argomento "-plugin".</span><span class="sxs-lookup"><span data-stu-id="74830-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="74830-151">Se un utente avvia direttamente un eseguibile del plug-in senza questo argomento, il plug-in può fornire un messaggio informativo invece di attendere un handshake del protocollo.</span><span class="sxs-lookup"><span data-stu-id="74830-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="74830-152">Il timeout dell'handshake del protocollo è di 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="74830-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="74830-153">Il plug-in deve completare il programma di installazione nel minor tempo possibile.</span><span class="sxs-lookup"><span data-stu-id="74830-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="74830-154">Gli strumenti client NuGet eseguiranno una query sulle operazioni supportate da un plug-in tramite il passaggio dell'indice del servizio per un'origine NuGet.</span><span class="sxs-lookup"><span data-stu-id="74830-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="74830-155">Un plug-in può usare l'indice del servizio per verificare la presenza di tipi di servizio supportati.</span><span class="sxs-lookup"><span data-stu-id="74830-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="74830-156">La comunicazione tra gli strumenti client NuGet e il plug-in è bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="74830-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="74830-157">Ogni richiesta ha un timeout di 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="74830-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="74830-158">Se le operazioni dovrebbero richiedere più tempo, il rispettivo processo deve inviare un messaggio di stato per impedire il timeout della richiesta. Dopo 1 minuto di inattività, un plug-in viene considerato inattivo e viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="74830-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="74830-159">Installazione e individuazione di plug-in</span><span class="sxs-lookup"><span data-stu-id="74830-159">Plugin installation and discovery</span></span>

<span data-ttu-id="74830-160">I plug-in verranno individuati tramite una struttura di directory basata sulla convenzione.</span><span class="sxs-lookup"><span data-stu-id="74830-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="74830-161">Gli scenari di integrazione continua/distribuzione continua e gli utenti esperti possono usare variabili di ambiente per eseguire l'override del comportamento.</span><span class="sxs-lookup"><span data-stu-id="74830-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="74830-162">Quando si usano le variabili di ambiente, sono consentiti solo i percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="74830-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="74830-163">Si noti che `NUGET_NETFX_PLUGIN_PATHS` e `NUGET_NETCORE_PLUGIN_PATHS` sono disponibili solo con la versione 5.3 + degli strumenti NuGet e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="74830-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="74830-164">`NUGET_NETFX_PLUGIN_PATHS`: definisce i plug-in che verranno usati dagli strumenti basati su .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="74830-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="74830-165">Ha la precedenza rispetto a `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="74830-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="74830-166">(Solo NuGet versione 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="74830-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="74830-167">`NUGET_NETCORE_PLUGIN_PATHS`: definisce i plug-in che verranno usati dagli strumenti basati su .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="74830-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="74830-168">Ha la precedenza rispetto a `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="74830-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="74830-169">(Solo NuGet versione 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="74830-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="74830-170">`NUGET_PLUGIN_PATHS`: definisce i plug-in che verranno usati per il processo NuGet, priorità mantenuta.</span><span class="sxs-lookup"><span data-stu-id="74830-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="74830-171">Se questa variabile di ambiente è impostata, sostituisce l'individuazione basata sulla convenzione.</span><span class="sxs-lookup"><span data-stu-id="74830-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="74830-172">Viene ignorato se viene specificata una delle variabili specifiche del Framework.</span><span class="sxs-lookup"><span data-stu-id="74830-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="74830-173">Utente-location, il percorso Home di NuGet in `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="74830-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="74830-174">Non è possibile eseguire l'override di questo percorso.</span><span class="sxs-lookup"><span data-stu-id="74830-174">This location cannot be overriden.</span></span> <span data-ttu-id="74830-175">Verrà usata una directory radice diversa per i plug-in .NET Core e .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="74830-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="74830-176">Framework</span><span class="sxs-lookup"><span data-stu-id="74830-176">Framework</span></span> | <span data-ttu-id="74830-177">Percorso di individuazione radice</span><span class="sxs-lookup"><span data-stu-id="74830-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="74830-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="74830-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="74830-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="74830-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="74830-180">Ogni plug-in deve essere installato in una cartella specifica.</span><span class="sxs-lookup"><span data-stu-id="74830-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="74830-181">Il punto di ingresso del plug-in sarà il nome della cartella installata, con le estensioni dll per .NET Core e l'estensione exe per .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="74830-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="74830-182">Attualmente non è disponibile alcuna storia utente per l'installazione dei plug-in.</span><span class="sxs-lookup"><span data-stu-id="74830-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="74830-183">È semplice quanto lo spostamento dei file necessari nella posizione predeterminata.</span><span class="sxs-lookup"><span data-stu-id="74830-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="74830-184">Operazioni supportate</span><span class="sxs-lookup"><span data-stu-id="74830-184">Supported operations</span></span>

<span data-ttu-id="74830-185">Sono supportate due operazioni nel nuovo protocollo plug-in.</span><span class="sxs-lookup"><span data-stu-id="74830-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="74830-186">Nome operazione</span><span class="sxs-lookup"><span data-stu-id="74830-186">Operation name</span></span> | <span data-ttu-id="74830-187">Versione minima del protocollo</span><span class="sxs-lookup"><span data-stu-id="74830-187">Minimum protocol version</span></span> | <span data-ttu-id="74830-188">Versione minima del client NuGet</span><span class="sxs-lookup"><span data-stu-id="74830-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="74830-189">Scarica pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-189">Download Package</span></span> | <span data-ttu-id="74830-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="74830-190">1.0.0</span></span> | <span data-ttu-id="74830-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="74830-191">4.3.0</span></span> |
| [<span data-ttu-id="74830-192">autenticazione</span><span class="sxs-lookup"><span data-stu-id="74830-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="74830-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="74830-193">2.0.0</span></span> | <span data-ttu-id="74830-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="74830-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="74830-195">Esecuzione di plug-in nel runtime corretto</span><span class="sxs-lookup"><span data-stu-id="74830-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="74830-196">Per gli scenari di NuGet in dotnet. exe, è necessario che i plug-in siano in grado di eseguire il runtime specifico di DotNet. exe.</span><span class="sxs-lookup"><span data-stu-id="74830-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="74830-197">Si tratta del provider di plug-in e del consumer per assicurarsi che venga usata una combinazione dotnet. exe/plugin compatibile.</span><span class="sxs-lookup"><span data-stu-id="74830-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="74830-198">Un potenziale problema può verificarsi con i plug-in della posizione utente quando, ad esempio, un file dotnet. exe nel runtime di 2,0 prova a usare un plug-in scritto per il runtime di 2,1.</span><span class="sxs-lookup"><span data-stu-id="74830-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="74830-199">Caching delle funzionalità</span><span class="sxs-lookup"><span data-stu-id="74830-199">Capabilities caching</span></span>

<span data-ttu-id="74830-200">La verifica della sicurezza e la creazione di istanze dei plug-in sono costose.</span><span class="sxs-lookup"><span data-stu-id="74830-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="74830-201">L'operazione di download si verifica in modo più frequente rispetto all'operazione di autenticazione, ma è probabile che l'utente NuGet medio disponga solo di un plug-in di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="74830-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="74830-202">Per migliorare l'esperienza, NuGet memorizza nella cache le attestazioni dell'operazione per la richiesta specificata.</span><span class="sxs-lookup"><span data-stu-id="74830-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="74830-203">Questa cache è per plug-in con la chiave del plug-in che è il percorso del plug-in e la scadenza della cache delle funzionalità è di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="74830-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="74830-204">La cache si trova in `%LocalAppData%/NuGet/plugins-cache` ed è stata sottoposta a override con la variabile di ambiente `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="74830-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="74830-205">Per cancellare la [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), è possibile eseguire il comando locals con l'opzione `plugins-cache`.</span><span class="sxs-lookup"><span data-stu-id="74830-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="74830-206">L'opzione variabili locali `all` eliminerà anche la cache dei plug-in.</span><span class="sxs-lookup"><span data-stu-id="74830-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="74830-207">Indice dei messaggi di protocollo</span><span class="sxs-lookup"><span data-stu-id="74830-207">Protocol messages index</span></span>

<span data-ttu-id="74830-208">Messaggi versione protocollo *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="74830-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="74830-209">Chiudi</span><span class="sxs-lookup"><span data-stu-id="74830-209">Close</span></span>
    * <span data-ttu-id="74830-210">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="74830-211">La richiesta non conterrà alcun payload</span><span class="sxs-lookup"><span data-stu-id="74830-211">The request will contain no payload</span></span>
    * <span data-ttu-id="74830-212">Non è prevista alcuna risposta.</span><span class="sxs-lookup"><span data-stu-id="74830-212">No response is expected.</span></span>  <span data-ttu-id="74830-213">La risposta corretta è che il processo del plug-in viene immediatamente terminato.</span><span class="sxs-lookup"><span data-stu-id="74830-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="74830-214">Copia i file nel pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-214">Copy files in package</span></span>
    * <span data-ttu-id="74830-215">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="74830-216">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-216">The request will contain:</span></span>
        * <span data-ttu-id="74830-217">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-217">the package ID and version</span></span>
        * <span data-ttu-id="74830-218">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-218">the package source repository location</span></span>
        * <span data-ttu-id="74830-219">percorso directory di destinazione</span><span class="sxs-lookup"><span data-stu-id="74830-219">destination directory path</span></span>
        * <span data-ttu-id="74830-220">oggetto enumerabile di file nel pacchetto da copiare nel percorso della directory di destinazione</span><span class="sxs-lookup"><span data-stu-id="74830-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="74830-221">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-221">A response will contain:</span></span>
        * <span data-ttu-id="74830-222">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="74830-223">oggetto enumerabile di percorsi completi per i file copiati nella directory di destinazione se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="74830-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="74830-224">Copiare il file del pacchetto (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="74830-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="74830-225">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="74830-226">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-226">The request will contain:</span></span>
        * <span data-ttu-id="74830-227">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-227">the package ID and version</span></span>
        * <span data-ttu-id="74830-228">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-228">the package source repository location</span></span>
        * <span data-ttu-id="74830-229">percorso del file di destinazione</span><span class="sxs-lookup"><span data-stu-id="74830-229">the destination file path</span></span>
    * <span data-ttu-id="74830-230">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-230">A response will contain:</span></span>
        * <span data-ttu-id="74830-231">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="74830-232">Ottenere le credenziali</span><span class="sxs-lookup"><span data-stu-id="74830-232">Get credentials</span></span>
    * <span data-ttu-id="74830-233">Direzione della richiesta: plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="74830-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="74830-234">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-234">The request will contain:</span></span>
        * <span data-ttu-id="74830-235">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-235">the package source repository location</span></span>
        * <span data-ttu-id="74830-236">codice di stato HTTP ottenuto dal repository di origine del pacchetto con le credenziali correnti</span><span class="sxs-lookup"><span data-stu-id="74830-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="74830-237">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-237">A response will contain:</span></span>
        * <span data-ttu-id="74830-238">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="74830-239">un nome utente, se disponibile</span><span class="sxs-lookup"><span data-stu-id="74830-239">a username, if available</span></span>
        * <span data-ttu-id="74830-240">una password, se disponibile</span><span class="sxs-lookup"><span data-stu-id="74830-240">a password, if available</span></span>

5.  <span data-ttu-id="74830-241">Ottenere i file nel pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-241">Get files in package</span></span>
    * <span data-ttu-id="74830-242">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="74830-243">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-243">The request will contain:</span></span>
        * <span data-ttu-id="74830-244">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-244">the package ID and version</span></span>
        * <span data-ttu-id="74830-245">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-245">the package source repository location</span></span>
    * <span data-ttu-id="74830-246">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-246">A response will contain:</span></span>
        * <span data-ttu-id="74830-247">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="74830-248">oggetto enumerabile di percorsi di file nel pacchetto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="74830-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="74830-249">Ottenere le attestazioni dell'operazione</span><span class="sxs-lookup"><span data-stu-id="74830-249">Get operation claims</span></span> 
    * <span data-ttu-id="74830-250">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="74830-251">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-251">The request will contain:</span></span>
        * <span data-ttu-id="74830-252">il servizio index. JSON per un'origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="74830-253">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-253">the package source repository location</span></span>
    * <span data-ttu-id="74830-254">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-254">A response will contain:</span></span>
        * <span data-ttu-id="74830-255">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="74830-256">oggetto enumerabile di operazioni supportate (ad esempio, download del pacchetto) se l'operazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="74830-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="74830-257">Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="74830-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="74830-258">Questo messaggio è stato aggiornato nella versione *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="74830-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="74830-259">Il client mantiene la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="74830-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="74830-260">Ottieni hash pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-260">Get package hash</span></span>
    * <span data-ttu-id="74830-261">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="74830-262">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-262">The request will contain:</span></span>
        * <span data-ttu-id="74830-263">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-263">the package ID and version</span></span>
        * <span data-ttu-id="74830-264">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-264">the package source repository location</span></span>
        * <span data-ttu-id="74830-265">algoritmo hash</span><span class="sxs-lookup"><span data-stu-id="74830-265">the hash algorithm</span></span>
    * <span data-ttu-id="74830-266">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-266">A response will contain:</span></span>
        * <span data-ttu-id="74830-267">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="74830-268">hash del file del pacchetto che utilizza l'algoritmo hash richiesto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="74830-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="74830-269">Ottenere le versioni di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-269">Get package versions</span></span>
    * <span data-ttu-id="74830-270">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="74830-271">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-271">The request will contain:</span></span>
        * <span data-ttu-id="74830-272">ID del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-272">the package ID</span></span>
        * <span data-ttu-id="74830-273">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-273">the package source repository location</span></span>
    * <span data-ttu-id="74830-274">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-274">A response will contain:</span></span>
        * <span data-ttu-id="74830-275">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="74830-276">oggetto enumerabile di versioni del pacchetto se l'operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="74830-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="74830-277">Ottenere l'indice del servizio</span><span class="sxs-lookup"><span data-stu-id="74830-277">Get service index</span></span>
    * <span data-ttu-id="74830-278">Direzione della richiesta: plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="74830-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="74830-279">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-279">The request will contain:</span></span>
        * <span data-ttu-id="74830-280">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-280">the package source repository location</span></span>
    * <span data-ttu-id="74830-281">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-281">A response will contain:</span></span>
        * <span data-ttu-id="74830-282">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="74830-283">Indice del servizio se l'operazione è stata completata correttamente</span><span class="sxs-lookup"><span data-stu-id="74830-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="74830-284">Handshake</span><span class="sxs-lookup"><span data-stu-id="74830-284">Handshake</span></span>
     * <span data-ttu-id="74830-285">Direzione della richiesta: < NuGet-> plug-in</span><span class="sxs-lookup"><span data-stu-id="74830-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="74830-286">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-286">The request will contain:</span></span>
         * <span data-ttu-id="74830-287">versione corrente del protocollo plugin</span><span class="sxs-lookup"><span data-stu-id="74830-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="74830-288">versione minima supportata del protocollo plug-in</span><span class="sxs-lookup"><span data-stu-id="74830-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="74830-289">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-289">A response will contain:</span></span>
         * <span data-ttu-id="74830-290">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="74830-291">versione del protocollo negoziata se l'operazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="74830-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="74830-292">Un errore provocherà la terminazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="74830-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="74830-293">Inizializza</span><span class="sxs-lookup"><span data-stu-id="74830-293">Initialize</span></span>
     * <span data-ttu-id="74830-294">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="74830-295">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-295">The request will contain:</span></span>
         * <span data-ttu-id="74830-296">versione dello strumento client NuGet</span><span class="sxs-lookup"><span data-stu-id="74830-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="74830-297">linguaggio efficace dello strumento client NuGet.</span><span class="sxs-lookup"><span data-stu-id="74830-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="74830-298">Ciò prende in considerazione l'impostazione ForceEnglishOutput, se usata.</span><span class="sxs-lookup"><span data-stu-id="74830-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="74830-299">timeout della richiesta predefinito, che sostituisce l'impostazione predefinita del protocollo.</span><span class="sxs-lookup"><span data-stu-id="74830-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="74830-300">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-300">A response will contain:</span></span>
         * <span data-ttu-id="74830-301">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="74830-302">Un errore provocherà la terminazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="74830-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="74830-303">File di log</span><span class="sxs-lookup"><span data-stu-id="74830-303">Log</span></span>
     * <span data-ttu-id="74830-304">Direzione della richiesta: plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="74830-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="74830-305">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-305">The request will contain:</span></span>
         * <span data-ttu-id="74830-306">livello di registrazione per la richiesta</span><span class="sxs-lookup"><span data-stu-id="74830-306">the log level for the request</span></span>
         * <span data-ttu-id="74830-307">messaggio da registrare</span><span class="sxs-lookup"><span data-stu-id="74830-307">a message to log</span></span>
     * <span data-ttu-id="74830-308">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-308">A response will contain:</span></span>
         * <span data-ttu-id="74830-309">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="74830-310">Esegui monitoraggio uscita processo NuGet</span><span class="sxs-lookup"><span data-stu-id="74830-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="74830-311">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="74830-312">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-312">The request will contain:</span></span>
         * <span data-ttu-id="74830-313">ID processo NuGet</span><span class="sxs-lookup"><span data-stu-id="74830-313">the NuGet process ID</span></span>
     * <span data-ttu-id="74830-314">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-314">A response will contain:</span></span>
         * <span data-ttu-id="74830-315">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="74830-316">Prelettura del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-316">Prefetch package</span></span>
     * <span data-ttu-id="74830-317">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="74830-318">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-318">The request will contain:</span></span>
         * <span data-ttu-id="74830-319">ID e versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-319">the package ID and version</span></span>
         * <span data-ttu-id="74830-320">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-320">the package source repository location</span></span>
     * <span data-ttu-id="74830-321">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-321">A response will contain:</span></span>
         * <span data-ttu-id="74830-322">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="74830-323">Impostare le credenziali</span><span class="sxs-lookup"><span data-stu-id="74830-323">Set credentials</span></span>
     * <span data-ttu-id="74830-324">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="74830-325">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-325">The request will contain:</span></span>
         * <span data-ttu-id="74830-326">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-326">the package source repository location</span></span>
         * <span data-ttu-id="74830-327">ultimo nome utente di origine del pacchetto noto, se disponibile</span><span class="sxs-lookup"><span data-stu-id="74830-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="74830-328">ultima password di origine del pacchetto nota, se disponibile</span><span class="sxs-lookup"><span data-stu-id="74830-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="74830-329">ultimo nome utente del proxy noto, se disponibile</span><span class="sxs-lookup"><span data-stu-id="74830-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="74830-330">ultima password del proxy nota, se disponibile</span><span class="sxs-lookup"><span data-stu-id="74830-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="74830-331">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-331">A response will contain:</span></span>
         * <span data-ttu-id="74830-332">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="74830-333">Impostare il livello di registrazione</span><span class="sxs-lookup"><span data-stu-id="74830-333">Set log level</span></span>
     * <span data-ttu-id="74830-334">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="74830-335">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-335">The request will contain:</span></span>
         * <span data-ttu-id="74830-336">livello di registrazione predefinito</span><span class="sxs-lookup"><span data-stu-id="74830-336">the default log level</span></span>
     * <span data-ttu-id="74830-337">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-337">A response will contain:</span></span>
         * <span data-ttu-id="74830-338">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="74830-339">Messaggi della versione *2.0.0* del protocollo</span><span class="sxs-lookup"><span data-stu-id="74830-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="74830-340">Ottenere le attestazioni dell'operazione</span><span class="sxs-lookup"><span data-stu-id="74830-340">Get Operation Claims</span></span>

* <span data-ttu-id="74830-341">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="74830-342">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-342">The request will contain:</span></span>
        * <span data-ttu-id="74830-343">il servizio index. JSON per un'origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="74830-344">percorso del repository di origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="74830-344">the package source repository location</span></span>
    * <span data-ttu-id="74830-345">Una risposta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-345">A response will contain:</span></span>
        * <span data-ttu-id="74830-346">codice di risposta che indica il risultato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74830-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="74830-347">oggetto enumerabile di operazioni supportate se l'operazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="74830-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="74830-348">Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="74830-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="74830-349">Se l'indice del servizio e l'origine del pacchetto sono null, il plug-in può rispondere con l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="74830-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="74830-350">Ottenere le credenziali di autenticazione</span><span class="sxs-lookup"><span data-stu-id="74830-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="74830-351">Direzione della richiesta: plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="74830-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="74830-352">La richiesta conterrà:</span><span class="sxs-lookup"><span data-stu-id="74830-352">The request will contain:</span></span>
    * <span data-ttu-id="74830-353">Uri</span><span class="sxs-lookup"><span data-stu-id="74830-353">Uri</span></span>
    * <span data-ttu-id="74830-354">Numero di tentativi</span><span class="sxs-lookup"><span data-stu-id="74830-354">isRetry</span></span>
    * <span data-ttu-id="74830-355">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="74830-355">NonInteractive</span></span>
    * <span data-ttu-id="74830-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="74830-356">CanShowDialog</span></span>
* <span data-ttu-id="74830-357">Una risposta conterrà</span><span class="sxs-lookup"><span data-stu-id="74830-357">A response will contain</span></span>
    * <span data-ttu-id="74830-358">Username</span><span class="sxs-lookup"><span data-stu-id="74830-358">Username</span></span>
    * <span data-ttu-id="74830-359">Password</span><span class="sxs-lookup"><span data-stu-id="74830-359">Password</span></span>
    * <span data-ttu-id="74830-360">Message</span><span class="sxs-lookup"><span data-stu-id="74830-360">Message</span></span>
    * <span data-ttu-id="74830-361">Elenco di tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="74830-361">List of Auth Types</span></span>
    * <span data-ttu-id="74830-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="74830-362">MessageResponseCode</span></span>
