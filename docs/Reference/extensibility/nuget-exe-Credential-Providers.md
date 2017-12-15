---
title: il provider di credenziali di NuGet.exe | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3cf592de-39f2-4e7f-a597-62635fdcedfa
description: il provider di credenziali di NuGet.exe autenticarsi con un feed e viene implementato come file eseguibili da riga di comando che seguono le convenzioni specifiche.
keywords: eseguire l'autenticazione con la raccolta, l'autenticazione con il feed di NuGet.exe i provider di credenziali, l'API del provider di credenziali
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82ab4d6e9be0736e008f5bd27d46e1db166d7bb4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="7595b-104">L'autenticazione di feed con il provider di credenziali di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="7595b-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="7595b-105">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="7595b-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="7595b-106">Quando `nuget.exe` è necessario fornire credenziali per l'autenticazione con un feed, la ricerca di essi nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="7595b-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="7595b-107">NuGet cerca innanzitutto le credenziali in `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="7595b-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="7595b-108">NuGet Usa quindi il provider di credenziali di plug-in, soggetti a ordine indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7595b-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="7595b-109">(E l'esempio è la [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="7595b-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="7595b-110">NuGet quindi chiede all'utente le credenziali nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="7595b-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="7595b-111">Si noti che i provider di credenziali descritti di seguito funzionano solo in `nuget.exe` e non in 'dotnet restore' o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7595b-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="7595b-112">Per i provider di credenziali con Visual Studio, vedere [nuget.exe provider di credenziali per Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="7595b-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="7595b-113">il provider di credenziali di NuGet.exe può essere utilizzato in 3 modi:</span><span class="sxs-lookup"><span data-stu-id="7595b-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="7595b-114">**A livello globale**: rendere disponibili per tutte le istanze di un provider di credenziali `nuget.exe` eseguito con il profilo dell'utente corrente, aggiungerlo a `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="7595b-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="7595b-115">Potrebbe essere necessario creare il `CredentialProviders` cartella.</span><span class="sxs-lookup"><span data-stu-id="7595b-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="7595b-116">Provider di credenziali possono essere installati nella radice di `CredentialProviders` cartella o all'interno di una sottocartella.</span><span class="sxs-lookup"><span data-stu-id="7595b-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="7595b-117">Se un provider di credenziali dispone di più file o assembly, è possibile utilizzare le sottocartelle per mantenere i provider organizzati.</span><span class="sxs-lookup"><span data-stu-id="7595b-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="7595b-118">**Una variabile di ambiente**: provider di credenziali possono essere archiviati ovunque e rese accessibili agli `nuget.exe` impostando il `%NUGET_CREDENTIALPROVIDERS_PATH%` variabile di ambiente per il percorso del provider.</span><span class="sxs-lookup"><span data-stu-id="7595b-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="7595b-119">Questa variabile può essere un elenco separato da punto e virgola (ad esempio, `path1;path2`) se si dispone di più percorsi.</span><span class="sxs-lookup"><span data-stu-id="7595b-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="7595b-120">**Insieme a nuget.exe**: il provider di credenziali di nuget.exe può essere inserito nella stessa cartella `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="7595b-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="7595b-121">Durante il caricamento di provider di credenziali, `nuget.exe` esegue la ricerca nei percorsi indicati, in ordine, per qualsiasi file denominato `credentialprovider*.exe`, quindi carica tali file nell'ordine in cui si trovano.</span><span class="sxs-lookup"><span data-stu-id="7595b-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="7595b-122">In presenza di più provider di credenziali nella stessa cartella, caricati in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="7595b-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="7595b-123">Creazione di un provider di credenziali di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="7595b-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="7595b-124">Un provider di credenziali è un file eseguibile da riga di comando, il formato `CredentialProvider*.exe`, che raccoglie gli input, acquisisce le credenziali necessarie e quindi restituisce il codice di stato di uscita appropriato e l'output standard.</span><span class="sxs-lookup"><span data-stu-id="7595b-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="7595b-125">Un provider deve eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7595b-125">A provider must do the following:</span></span>

- <span data-ttu-id="7595b-126">Determinare se è possibile fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="7595b-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="7595b-127">In caso contrario, deve essere restituito il codice di stato 1 senza credenziali.</span><span class="sxs-lookup"><span data-stu-id="7595b-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="7595b-128">Non modificare `Nuget.Config` (ad esempio, l'impostazione delle credenziali non esiste).</span><span class="sxs-lookup"><span data-stu-id="7595b-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="7595b-129">Configurazione del proxy HTTP di handle nel proprio come NuGet non fornisce informazioni sul proxy per il plug-in.</span><span class="sxs-lookup"><span data-stu-id="7595b-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="7595b-130">Restituire le credenziali o i dettagli dell'errore per `nuget.exe` mediante la scrittura di un oggetto di risposta JSON (vedere sotto) in stdout, utilizzando la codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="7595b-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="7595b-131">Facoltativamente, creare la registrazione di traccia aggiuntivi in stderr.</span><span class="sxs-lookup"><span data-stu-id="7595b-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="7595b-132">Nessun segreto deve mai essere scritto in stderr, poiché i livelli di dettaglio "normale" o "dettagliato" tali tracce vengono restituite da NuGet nella console.</span><span class="sxs-lookup"><span data-stu-id="7595b-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="7595b-133">Parametri non previsti devono essere ignorati, fornendo la compatibilità con le versioni future di NuGet.</span><span class="sxs-lookup"><span data-stu-id="7595b-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="7595b-134">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7595b-134">Input parameters</span></span>

| <span data-ttu-id="7595b-135">Parametro /</span><span class="sxs-lookup"><span data-stu-id="7595b-135">Parameter/Switch</span></span> |<span data-ttu-id="7595b-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7595b-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="7595b-137">URI {value}</span><span class="sxs-lookup"><span data-stu-id="7595b-137">Uri {value}</span></span> | <span data-ttu-id="7595b-138">Il pacchetto URI che richiedono le credenziali dell'origine.</span><span class="sxs-lookup"><span data-stu-id="7595b-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="7595b-139">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="7595b-139">NonInteractive</span></span> | <span data-ttu-id="7595b-140">Se presente, provider non viene visualizzato un prompt interattivo.</span><span class="sxs-lookup"><span data-stu-id="7595b-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="7595b-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="7595b-141">IsRetry</span></span> | <span data-ttu-id="7595b-142">Se presente, indica che il tentativo è un nuovo tentativo di un tentativo non riuscito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7595b-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="7595b-143">Provider di questo flag viene utilizzato in genere per assicurarsi che siano ignorare qualsiasi cache esistente e richiedere le nuove credenziali, se possibile.</span><span class="sxs-lookup"><span data-stu-id="7595b-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="7595b-144">Livello di dettaglio {value}</span><span class="sxs-lookup"><span data-stu-id="7595b-144">Verbosity {value}</span></span> | <span data-ttu-id="7595b-145">Se presente, uno dei seguenti valori: "normale", "quiet" o "dettagliato".</span><span class="sxs-lookup"><span data-stu-id="7595b-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="7595b-146">Se viene specificato alcun valore, per impostazione predefinita "normal".</span><span class="sxs-lookup"><span data-stu-id="7595b-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="7595b-147">Provider devono utilizzare questa come un'indicazione del livello di registrazione facoltativo per generare il flusso di errore standard.</span><span class="sxs-lookup"><span data-stu-id="7595b-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="7595b-148">Codici di uscita</span><span class="sxs-lookup"><span data-stu-id="7595b-148">Exit codes</span></span>

| <span data-ttu-id="7595b-149">Codice</span><span class="sxs-lookup"><span data-stu-id="7595b-149">Code</span></span> |<span data-ttu-id="7595b-150">Risultato</span><span class="sxs-lookup"><span data-stu-id="7595b-150">Result</span></span> | <span data-ttu-id="7595b-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7595b-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="7595b-152">0</span><span class="sxs-lookup"><span data-stu-id="7595b-152">0</span></span> | <span data-ttu-id="7595b-153">Riuscito</span><span class="sxs-lookup"><span data-stu-id="7595b-153">Success</span></span> | <span data-ttu-id="7595b-154">Le credenziali sono state acquisite correttamente e sono stati scritti in stdout.</span><span class="sxs-lookup"><span data-stu-id="7595b-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="7595b-155">1</span><span class="sxs-lookup"><span data-stu-id="7595b-155">1</span></span> | <span data-ttu-id="7595b-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="7595b-156">ProviderNotApplicable</span></span> | <span data-ttu-id="7595b-157">Il provider corrente non fornire le credenziali per l'URI specificato.</span><span class="sxs-lookup"><span data-stu-id="7595b-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="7595b-158">2</span><span class="sxs-lookup"><span data-stu-id="7595b-158">2</span></span> | <span data-ttu-id="7595b-159">Errore</span><span class="sxs-lookup"><span data-stu-id="7595b-159">Failure</span></span> | <span data-ttu-id="7595b-160">Il provider è il provider corretto per l'URI specificato, ma non è possibile fornire le credenziali.</span><span class="sxs-lookup"><span data-stu-id="7595b-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="7595b-161">In questo caso, nuget.exe non tenterà di autenticazione e avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="7595b-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="7595b-162">Un esempio tipico è quando un utente annulla un account di accesso interattivo.</span><span class="sxs-lookup"><span data-stu-id="7595b-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="7595b-163">Output standard</span><span class="sxs-lookup"><span data-stu-id="7595b-163">Standard output</span></span>

| <span data-ttu-id="7595b-164">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7595b-164">Property</span></span> |<span data-ttu-id="7595b-165">Note</span><span class="sxs-lookup"><span data-stu-id="7595b-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="7595b-166">Nome utente</span><span class="sxs-lookup"><span data-stu-id="7595b-166">Username</span></span> | <span data-ttu-id="7595b-167">Nome utente per le richieste autenticate.</span><span class="sxs-lookup"><span data-stu-id="7595b-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="7595b-168">Password</span><span class="sxs-lookup"><span data-stu-id="7595b-168">Password</span></span> | <span data-ttu-id="7595b-169">Password per le richieste autenticate.</span><span class="sxs-lookup"><span data-stu-id="7595b-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="7595b-170">Messaggio</span><span class="sxs-lookup"><span data-stu-id="7595b-170">Message</span></span> | <span data-ttu-id="7595b-171">Dettagli facoltativi sulla risposta, è utilizzata solo per visualizzare ulteriori dettagli in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="7595b-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="7595b-172">Stdout di esempio:</span><span class="sxs-lookup"><span data-stu-id="7595b-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="7595b-173">Risoluzione dei problemi relativi a un provider di credenziali</span><span class="sxs-lookup"><span data-stu-id="7595b-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="7595b-174">Al momento, NuGet non fornisce molto supporto diretto per il debug di provider di credenziali personalizzate. [emettere 4598](https://github.com/NuGet/Home/issues/4598) tiene traccia di questo lavoro.</span><span class="sxs-lookup"><span data-stu-id="7595b-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="7595b-175">È inoltre possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7595b-175">You can also do the following:</span></span>

- <span data-ttu-id="7595b-176">Eseguire nuget.exe con il `-verbosity` commutatore per controllare l'output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="7595b-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="7595b-177">Aggiungere i messaggi di debug per `stdout` nelle posizioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="7595b-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="7595b-178">Assicurarsi che si usi nuget.exe 3.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="7595b-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="7595b-179">Collega debugger all'avvio con questo frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="7595b-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="7595b-180">Per ulteriore assistenza, [inviare una richiesta di supporto un nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="7595b-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
