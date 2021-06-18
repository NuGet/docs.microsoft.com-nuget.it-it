---
title: nuget.exe provider di credenziali
description: nuget.exe i provider di credenziali eseguono l'autenticazione con un feed e vengono implementati come eseguibili della riga di comando che seguono convenzioni specifiche.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323830"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="6f762-103">Autenticazione di feed con provider nuget.exe credenziali</span><span class="sxs-lookup"><span data-stu-id="6f762-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="6f762-104">Nella versione `3.3` è stato aggiunto il supporto per provider di credenziali `nuget.exe` specifici.</span><span class="sxs-lookup"><span data-stu-id="6f762-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="6f762-105">Da allora, nella versione è stato aggiunto il supporto per i provider di credenziali che funzionano in tutti gli scenari della riga di comando `4.8` [](NuGet-Cross-Platform-Authentication-Plugin.md) ( , `nuget.exe` , `dotnet.exe` `msbuild.exe` ).</span><span class="sxs-lookup"><span data-stu-id="6f762-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="6f762-106">Per [altri dettagli su tutti gli approcci di](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) autenticazione per , vedere Utilizzo di pacchetti da feed autenticati `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="6f762-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="6f762-107">nuget.exe individuazione del provider di credenziali</span><span class="sxs-lookup"><span data-stu-id="6f762-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="6f762-108">nuget.exe provider di credenziali possono essere usati in 3 modi:</span><span class="sxs-lookup"><span data-stu-id="6f762-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="6f762-109">**A livello globale:** per rendere disponibile un provider di credenziali per tutte le istanze di eseguite nel `nuget.exe` profilo dell'utente corrente, aggiungerlo a `%LocalAppData%\NuGet\CredentialProviders` .</span><span class="sxs-lookup"><span data-stu-id="6f762-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="6f762-110">Potrebbe essere necessario creare la `CredentialProviders` cartella.</span><span class="sxs-lookup"><span data-stu-id="6f762-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="6f762-111">I provider di credenziali possono essere installati nella radice della cartella `CredentialProviders`  o all'interno di una sottocartella.</span><span class="sxs-lookup"><span data-stu-id="6f762-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="6f762-112">Se un provider di credenziali dispone di più file/assembly, è possibile usare le sottocartelle per mantenere organizzati i provider.</span><span class="sxs-lookup"><span data-stu-id="6f762-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="6f762-113">**Da una variabile di ambiente**: i provider di credenziali possono essere archiviati ovunque e resi accessibili impostando la variabile di ambiente sul percorso del `nuget.exe` `%NUGET_CREDENTIALPROVIDERS_PATH%` provider.</span><span class="sxs-lookup"><span data-stu-id="6f762-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="6f762-114">Questa variabile può essere un elenco separato da punti e virgola (ad esempio, `path1;path2` ) se si dispone di più posizioni.</span><span class="sxs-lookup"><span data-stu-id="6f762-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="6f762-115">**Insieme nuget.exe**: nuget.exe provider di credenziali possono essere inseriti nella stessa cartella di `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="6f762-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="6f762-116">Quando si caricano i provider di credenziali, cerca nei percorsi precedenti, nell'ordine, qualsiasi file denominato , quindi carica i `nuget.exe` `credentialprovider*.exe` file nell'ordine in cui vengono trovati.</span><span class="sxs-lookup"><span data-stu-id="6f762-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="6f762-117">Se nella stessa cartella sono presenti più provider di credenziali, vengono caricati in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="6f762-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="6f762-118">Creazione di un provider nuget.exe credenziali</span><span class="sxs-lookup"><span data-stu-id="6f762-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="6f762-119">Un provider di credenziali è un eseguibile della riga di comando, denominato nel formato , che raccoglie gli input, acquisisce le credenziali in base alle esigenze e quindi restituisce il codice di stato di uscita appropriato e `CredentialProvider*.exe` l'output standard.</span><span class="sxs-lookup"><span data-stu-id="6f762-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="6f762-120">Un provider deve eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f762-120">A provider must do the following:</span></span>

- <span data-ttu-id="6f762-121">Determinare se può fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="6f762-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="6f762-122">In caso contrario, deve restituire il codice di stato 1 senza credenziali.</span><span class="sxs-lookup"><span data-stu-id="6f762-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="6f762-123">Non modificare `NuGet.Config` (ad esempio, l'impostazione delle credenziali).</span><span class="sxs-lookup"><span data-stu-id="6f762-123">Not modify `NuGet.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="6f762-124">Gestire la configurazione del proxy HTTP da sola, in quanto NuGet non fornisce informazioni sul proxy al plug-in.</span><span class="sxs-lookup"><span data-stu-id="6f762-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="6f762-125">Restituire credenziali o dettagli dell'errore scrivendo un oggetto risposta JSON (vedere di `nuget.exe` seguito) in stdout, usando la codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="6f762-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="6f762-126">Facoltativamente, generare la registrazione di traccia aggiuntiva in stderr.</span><span class="sxs-lookup"><span data-stu-id="6f762-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="6f762-127">Non è mai necessario scrivere segreti in stderr, poiché a livelli di dettaglio "normali" o "dettagliate" tali tracce vengono echeggiate da NuGet nella console.</span><span class="sxs-lookup"><span data-stu-id="6f762-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="6f762-128">I parametri imprevisti devono essere ignorati, garantendo la compatibilità con le versioni future di NuGet.</span><span class="sxs-lookup"><span data-stu-id="6f762-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6f762-129">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6f762-129">Input parameters</span></span>

| <span data-ttu-id="6f762-130">Parametro/opzione</span><span class="sxs-lookup"><span data-stu-id="6f762-130">Parameter/Switch</span></span> |<span data-ttu-id="6f762-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6f762-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="6f762-132">URI {value}</span><span class="sxs-lookup"><span data-stu-id="6f762-132">Uri {value}</span></span> | <span data-ttu-id="6f762-133">URI di origine del pacchetto che richiede le credenziali.</span><span class="sxs-lookup"><span data-stu-id="6f762-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="6f762-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6f762-134">NonInteractive</span></span> | <span data-ttu-id="6f762-135">Se presente, il provider non emettere richieste interattive.</span><span class="sxs-lookup"><span data-stu-id="6f762-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="6f762-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="6f762-136">IsRetry</span></span> | <span data-ttu-id="6f762-137">Se presente, indica che questo tentativo è un nuovo tentativo di un tentativo non riuscito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6f762-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="6f762-138">I provider usano in genere questo flag per assicurarsi di ignorare qualsiasi cache esistente e richiedere nuove credenziali, se possibile.</span><span class="sxs-lookup"><span data-stu-id="6f762-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="6f762-139">Livello di dettaglio {value}</span><span class="sxs-lookup"><span data-stu-id="6f762-139">Verbosity {value}</span></span> | <span data-ttu-id="6f762-140">Se presente, uno dei valori seguenti: "normal", "quiet" o "detailed".</span><span class="sxs-lookup"><span data-stu-id="6f762-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="6f762-141">Se non viene specificato alcun valore, il valore predefinito è "normal".</span><span class="sxs-lookup"><span data-stu-id="6f762-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="6f762-142">I provider devono usarlo come indicazione del livello di registrazione facoltativo da generare nel flusso di errore standard.</span><span class="sxs-lookup"><span data-stu-id="6f762-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="6f762-143">Codici di uscita</span><span class="sxs-lookup"><span data-stu-id="6f762-143">Exit codes</span></span>

| <span data-ttu-id="6f762-144">Codice</span><span class="sxs-lookup"><span data-stu-id="6f762-144">Code</span></span> |<span data-ttu-id="6f762-145">Risultato</span><span class="sxs-lookup"><span data-stu-id="6f762-145">Result</span></span> | <span data-ttu-id="6f762-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6f762-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="6f762-147">0</span><span class="sxs-lookup"><span data-stu-id="6f762-147">0</span></span> | <span data-ttu-id="6f762-148">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="6f762-148">Success</span></span> | <span data-ttu-id="6f762-149">Le credenziali sono state acquisite correttamente e sono state scritte in stdout.</span><span class="sxs-lookup"><span data-stu-id="6f762-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="6f762-150">1</span><span class="sxs-lookup"><span data-stu-id="6f762-150">1</span></span> | <span data-ttu-id="6f762-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="6f762-151">ProviderNotApplicable</span></span> | <span data-ttu-id="6f762-152">Il provider corrente non fornisce le credenziali per l'URI specificato.</span><span class="sxs-lookup"><span data-stu-id="6f762-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="6f762-153">2</span><span class="sxs-lookup"><span data-stu-id="6f762-153">2</span></span> | <span data-ttu-id="6f762-154">Operazioni non riuscite</span><span class="sxs-lookup"><span data-stu-id="6f762-154">Failure</span></span> | <span data-ttu-id="6f762-155">Il provider è il provider corretto per l'URI specificato, ma non può fornire credenziali.</span><span class="sxs-lookup"><span data-stu-id="6f762-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="6f762-156">In questo caso, nuget.exe ritentare l'autenticazione e avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6f762-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="6f762-157">Un esempio tipico è quando un utente annulla un account di accesso interattivo.</span><span class="sxs-lookup"><span data-stu-id="6f762-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="6f762-158">Output standard</span><span class="sxs-lookup"><span data-stu-id="6f762-158">Standard output</span></span>

| <span data-ttu-id="6f762-159">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6f762-159">Property</span></span> |<span data-ttu-id="6f762-160">Note</span><span class="sxs-lookup"><span data-stu-id="6f762-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="6f762-161">Username</span><span class="sxs-lookup"><span data-stu-id="6f762-161">Username</span></span> | <span data-ttu-id="6f762-162">Nome utente per le richieste autenticate.</span><span class="sxs-lookup"><span data-stu-id="6f762-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="6f762-163">Password</span><span class="sxs-lookup"><span data-stu-id="6f762-163">Password</span></span> | <span data-ttu-id="6f762-164">Password per le richieste autenticate.</span><span class="sxs-lookup"><span data-stu-id="6f762-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="6f762-165">Message</span><span class="sxs-lookup"><span data-stu-id="6f762-165">Message</span></span> | <span data-ttu-id="6f762-166">Dettagli facoltativi sulla risposta, usati solo per visualizzare dettagli aggiuntivi nei casi di errore.</span><span class="sxs-lookup"><span data-stu-id="6f762-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="6f762-167">Stdout di esempio:</span><span class="sxs-lookup"><span data-stu-id="6f762-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="6f762-168">Risoluzione dei problemi relativi a un provider di credenziali</span><span class="sxs-lookup"><span data-stu-id="6f762-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="6f762-169">Attualmente, NuGet non offre un supporto diretto per il debug di provider di credenziali personalizzati. [il problema 4598](https://github.com/NuGet/Home/issues/4598) sta verificando questo lavoro.</span><span class="sxs-lookup"><span data-stu-id="6f762-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="6f762-170">È inoltre possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f762-170">You can also do the following:</span></span>

- <span data-ttu-id="6f762-171">Eseguire nuget.exe con `-verbosity` l'opzione per esaminare l'output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="6f762-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="6f762-172">Aggiungere messaggi di debug `stdout` a nelle posizioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="6f762-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="6f762-173">Assicurarsi di usare nuget.exe 3.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6f762-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="6f762-174">Collegare il debugger all'avvio con questo frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="6f762-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
