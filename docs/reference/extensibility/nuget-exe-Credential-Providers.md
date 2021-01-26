---
title: Provider di credenziali nuget.exe
description: nuget.exe i provider di credenziali eseguono l'autenticazione con un feed e vengono implementati come eseguibili da riga di comando che seguono convenzioni specifiche.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 285504508fa88c96f5c7a23f15ef14d81ebc21e1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777764"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="f0fa7-103">Autenticazione dei feed con nuget.exe provider di credenziali</span><span class="sxs-lookup"><span data-stu-id="f0fa7-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="f0fa7-104">Nel supporto della versione `3.3` è stato aggiunto per `nuget.exe` provider di credenziali specifici.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="f0fa7-105">Successivamente, `4.8` è stato aggiunto il supporto della versione [per i provider di credenziali](NuGet-Cross-Platform-Authentication-Plugin.md) che funzionano in tutti gli scenari della riga di comando ( `nuget.exe` , `dotnet.exe` , `msbuild.exe` ).</span><span class="sxs-lookup"><span data-stu-id="f0fa7-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="f0fa7-106">Per altri dettagli su tutti gli approcci di autenticazione per, vedere [utilizzo dei pacchetti dai feed autenticati](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)`nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="f0fa7-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="f0fa7-107">Individuazione del provider di credenziali nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f0fa7-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="f0fa7-108">nuget.exe i provider di credenziali possono essere usati in tre modi:</span><span class="sxs-lookup"><span data-stu-id="f0fa7-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="f0fa7-109">A **livello globale**: per rendere disponibile un provider di credenziali per tutte le istanze di `nuget.exe` in esecuzione nel profilo dell'utente corrente, aggiungerlo a `%LocalAppData%\NuGet\CredentialProviders` .</span><span class="sxs-lookup"><span data-stu-id="f0fa7-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="f0fa7-110">Potrebbe essere necessario creare la `CredentialProviders` cartella.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="f0fa7-111">I provider di credenziali possono essere installati alla radice della `CredentialProviders`  cartella o all'interno di una sottocartella.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="f0fa7-112">Se un provider di credenziali dispone di più file/assembly, è possibile utilizzare le sottocartelle per organizzare i provider.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="f0fa7-113">**Da una variabile di ambiente**: i provider di credenziali possono essere archiviati ovunque e resi accessibili a impostando `nuget.exe` la `%NUGET_CREDENTIALPROVIDERS_PATH%` variabile di ambiente sul percorso del provider.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="f0fa7-114">Questa variabile può essere un elenco delimitato da punti e virgola (ad esempio, `path1;path2` ) se sono presenti più percorsi.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="f0fa7-115">**Insieme a nuget.exe**: nuget.exe i provider di credenziali possono essere inseriti nella stessa cartella del `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="f0fa7-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="f0fa7-116">Quando si caricano i provider di credenziali, `nuget.exe` Cerca nei percorsi precedenti, in ordine, tutti i file denominati `credentialprovider*.exe` , quindi carica i file nell'ordine in cui sono stati trovati.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="f0fa7-117">Se nella stessa cartella sono presenti più provider di credenziali, questi vengono caricati in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="f0fa7-118">Creazione di un provider di credenziali nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f0fa7-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="f0fa7-119">Un provider di credenziali è un eseguibile della riga di comando, denominato nel formato `CredentialProvider*.exe` , che raccoglie gli input, acquisisce le credenziali nel modo appropriato e quindi restituisce il codice di stato di uscita appropriato e l'output standard.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="f0fa7-120">Un provider deve eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0fa7-120">A provider must do the following:</span></span>

- <span data-ttu-id="f0fa7-121">Determinare se può fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="f0fa7-122">In caso contrario, deve restituire il codice di stato 1 senza credenziali.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="f0fa7-123">Non modificare `Nuget.Config` (ad esempio l'impostazione delle credenziali).</span><span class="sxs-lookup"><span data-stu-id="f0fa7-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="f0fa7-124">Gestire autonomamente la configurazione del proxy HTTP, poiché NuGet non fornisce informazioni sul proxy al plug-in.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="f0fa7-125">Restituire le credenziali o i dettagli `nuget.exe` dell'errore a scrivendo un oggetto risposta JSON (vedere di seguito) in stdout, usando la codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="f0fa7-126">Facoltativamente, è possibile creare la registrazione traccia aggiuntiva in stderr.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="f0fa7-127">Nessun segreto deve essere mai scritto in stderr, perché a livello di dettaglio "normale" o "dettagliato" tali tracce vengono riportate da NuGet alla console.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="f0fa7-128">I parametri imprevisti devono essere ignorati, garantendo la compatibilità con le versioni future di NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f0fa7-129">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="f0fa7-129">Input parameters</span></span>

| <span data-ttu-id="f0fa7-130">Parametro/opzione</span><span class="sxs-lookup"><span data-stu-id="f0fa7-130">Parameter/Switch</span></span> |<span data-ttu-id="f0fa7-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f0fa7-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="f0fa7-132">URI {valore}</span><span class="sxs-lookup"><span data-stu-id="f0fa7-132">Uri {value}</span></span> | <span data-ttu-id="f0fa7-133">URI di origine del pacchetto che richiede le credenziali.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="f0fa7-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f0fa7-134">NonInteractive</span></span> | <span data-ttu-id="f0fa7-135">Se presente, il provider non rilascia richieste interattive.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="f0fa7-136">Numero di tentativi</span><span class="sxs-lookup"><span data-stu-id="f0fa7-136">IsRetry</span></span> | <span data-ttu-id="f0fa7-137">Se presente, indica che il tentativo di un tentativo non riuscito in precedenza è stato ritentato.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="f0fa7-138">I provider usano in genere questo flag per assicurarsi che ignorino eventuali cache esistenti e chiedano nuove credenziali, se possibile.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="f0fa7-139">Livello di dettaglio {value}</span><span class="sxs-lookup"><span data-stu-id="f0fa7-139">Verbosity {value}</span></span> | <span data-ttu-id="f0fa7-140">Se presente, uno dei valori seguenti: "Normal", "quiet" o "detailed".</span><span class="sxs-lookup"><span data-stu-id="f0fa7-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="f0fa7-141">Se non viene specificato alcun valore, il valore predefinito è "Normal".</span><span class="sxs-lookup"><span data-stu-id="f0fa7-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="f0fa7-142">I provider devono utilizzarlo come indicazione del livello di registrazione facoltativa da emettere nel flusso di errore standard.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="f0fa7-143">Codici di uscita</span><span class="sxs-lookup"><span data-stu-id="f0fa7-143">Exit codes</span></span>

| <span data-ttu-id="f0fa7-144">Codice</span><span class="sxs-lookup"><span data-stu-id="f0fa7-144">Code</span></span> |<span data-ttu-id="f0fa7-145">Risultato</span><span class="sxs-lookup"><span data-stu-id="f0fa7-145">Result</span></span> | <span data-ttu-id="f0fa7-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f0fa7-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="f0fa7-147">0</span><span class="sxs-lookup"><span data-stu-id="f0fa7-147">0</span></span> | <span data-ttu-id="f0fa7-148">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="f0fa7-148">Success</span></span> | <span data-ttu-id="f0fa7-149">Le credenziali sono state acquisite e sono state scritte in stdout.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="f0fa7-150">1</span><span class="sxs-lookup"><span data-stu-id="f0fa7-150">1</span></span> | <span data-ttu-id="f0fa7-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="f0fa7-151">ProviderNotApplicable</span></span> | <span data-ttu-id="f0fa7-152">Il provider corrente non fornisce le credenziali per l'URI specificato.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="f0fa7-153">2</span><span class="sxs-lookup"><span data-stu-id="f0fa7-153">2</span></span> | <span data-ttu-id="f0fa7-154">Errore</span><span class="sxs-lookup"><span data-stu-id="f0fa7-154">Failure</span></span> | <span data-ttu-id="f0fa7-155">Il provider è il provider corretto per l'URI specificato, ma non è in grado di fornire le credenziali.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="f0fa7-156">In questo caso, nuget.exe non tenterà di eseguire l'autenticazione e avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="f0fa7-157">Un esempio tipico è quando un utente annulla un accesso interattivo.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="f0fa7-158">Output standard</span><span class="sxs-lookup"><span data-stu-id="f0fa7-158">Standard output</span></span>

| <span data-ttu-id="f0fa7-159">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f0fa7-159">Property</span></span> |<span data-ttu-id="f0fa7-160">Note</span><span class="sxs-lookup"><span data-stu-id="f0fa7-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="f0fa7-161">Username</span><span class="sxs-lookup"><span data-stu-id="f0fa7-161">Username</span></span> | <span data-ttu-id="f0fa7-162">Nome utente per le richieste autenticate.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="f0fa7-163">Password</span><span class="sxs-lookup"><span data-stu-id="f0fa7-163">Password</span></span> | <span data-ttu-id="f0fa7-164">Password per le richieste autenticate.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="f0fa7-165">Message</span><span class="sxs-lookup"><span data-stu-id="f0fa7-165">Message</span></span> | <span data-ttu-id="f0fa7-166">Dettagli facoltativi sulla risposta, usati solo per visualizzare dettagli aggiuntivi nei casi di errore.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="f0fa7-167">Esempio di stdout:</span><span class="sxs-lookup"><span data-stu-id="f0fa7-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="f0fa7-168">Risoluzione dei problemi relativi a un provider di credenziali</span><span class="sxs-lookup"><span data-stu-id="f0fa7-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="f0fa7-169">Attualmente, NuGet non fornisce un supporto molto diretto per il debug di provider di credenziali personalizzati; il [problema 4598](https://github.com/NuGet/Home/issues/4598) sta tenendo traccia del lavoro.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="f0fa7-170">È inoltre possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0fa7-170">You can also do the following:</span></span>

- <span data-ttu-id="f0fa7-171">Eseguire nuget.exe con l' `-verbosity` opzione per esaminare l'output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="f0fa7-172">Aggiungere i messaggi di debug a `stdout` in posizioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="f0fa7-173">Assicurarsi di usare nuget.exe 3,3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f0fa7-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="f0fa7-174">Connetti debugger all'avvio con il frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f0fa7-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
