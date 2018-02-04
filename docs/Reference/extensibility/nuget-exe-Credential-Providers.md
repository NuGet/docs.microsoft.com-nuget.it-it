---
title: il provider di credenziali di NuGet.exe | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: il provider di credenziali di NuGet.exe autenticarsi con un feed e viene implementato come file eseguibili da riga di comando che seguono le convenzioni specifiche.
keywords: eseguire l'autenticazione con la raccolta, l'autenticazione con il feed di NuGet.exe i provider di credenziali, l'API del provider di credenziali
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>L'autenticazione di feed con il provider di credenziali di nuget.exe

*NuGet 3.3 +*

Quando `nuget.exe` è necessario fornire credenziali per l'autenticazione con un feed, la ricerca di essi nel modo seguente:

1. NuGet cerca innanzitutto le credenziali in `Nuget.Config` file.
1. NuGet Usa quindi il provider di credenziali di plug-in, soggetti a ordine indicato di seguito. (E l'esempio è la [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet quindi chiede all'utente le credenziali nella riga di comando.

Si noti che i provider di credenziali descritti di seguito funzionano solo in `nuget.exe` e non in 'dotnet restore' o Visual Studio. Per i provider di credenziali con Visual Studio, vedere [nuget.exe provider di credenziali per Visual Studio](nuget-credential-providers-for-visual-studio.md)

il provider di credenziali di NuGet.exe può essere utilizzato in 3 modi:

- **A livello globale**: rendere disponibili per tutte le istanze di un provider di credenziali `nuget.exe` eseguito con il profilo dell'utente corrente, aggiungerlo a `%LocalAppData%\NuGet\CredentialProviders`. Potrebbe essere necessario creare il `CredentialProviders` cartella. Provider di credenziali possono essere installati nella radice di `CredentialProviders` cartella o all'interno di una sottocartella. Se un provider di credenziali dispone di più file o assembly, è possibile utilizzare le sottocartelle per mantenere i provider organizzati.

- **Una variabile di ambiente**: provider di credenziali possono essere archiviati ovunque e rese accessibili agli `nuget.exe` impostando il `%NUGET_CREDENTIALPROVIDERS_PATH%` variabile di ambiente per il percorso del provider. Questa variabile può essere un elenco separato da punto e virgola (ad esempio, `path1;path2`) se si dispone di più percorsi.

- **Insieme a nuget.exe**: il provider di credenziali di nuget.exe può essere inserito nella stessa cartella `nuget.exe`.

Durante il caricamento di provider di credenziali, `nuget.exe` esegue la ricerca nei percorsi indicati, in ordine, per qualsiasi file denominato `credentialprovider*.exe`, quindi carica tali file nell'ordine in cui si trovano. In presenza di più provider di credenziali nella stessa cartella, caricati in ordine alfabetico.

## <a name="creating-a-nugetexe-credential-provider"></a>Creazione di un provider di credenziali di nuget.exe

Un provider di credenziali è un file eseguibile da riga di comando, il formato `CredentialProvider*.exe`, che raccoglie gli input, acquisisce le credenziali necessarie e quindi restituisce il codice di stato di uscita appropriato e l'output standard.

Un provider deve eseguire le operazioni seguenti:

- Determinare se è possibile fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali. In caso contrario, deve essere restituito il codice di stato 1 senza credenziali.
- Non modificare `Nuget.Config` (ad esempio, l'impostazione delle credenziali non esiste).
- Configurazione del proxy HTTP di handle nel proprio come NuGet non fornisce informazioni sul proxy per il plug-in.
- Restituire le credenziali o i dettagli dell'errore per `nuget.exe` mediante la scrittura di un oggetto di risposta JSON (vedere sotto) in stdout, utilizzando la codifica UTF-8.
- Facoltativamente, creare la registrazione di traccia aggiuntivi in stderr. Nessun segreto deve mai essere scritto in stderr, poiché i livelli di dettaglio "normale" o "dettagliato" tali tracce vengono restituite da NuGet nella console.
- Parametri non previsti devono essere ignorati, fornendo la compatibilità con le versioni future di NuGet.

### <a name="input-parameters"></a>Parametri di input

| Parametro / |Descrizione|
|----------------|-----------|
| URI {value} | Il pacchetto URI che richiedono le credenziali dell'origine.|
| NonInteractive | Se presente, provider non viene visualizzato un prompt interattivo. |
| IsRetry | Se presente, indica che il tentativo è un nuovo tentativo di un tentativo non riuscito in precedenza. Provider di questo flag viene utilizzato in genere per assicurarsi che siano ignorare qualsiasi cache esistente e richiedere le nuove credenziali, se possibile.|
| Livello di dettaglio {value} | Se presente, uno dei seguenti valori: "normale", "quiet" o "dettagliato". Se viene specificato alcun valore, per impostazione predefinita "normal". Provider devono utilizzare questa come un'indicazione del livello di registrazione facoltativo per generare il flusso di errore standard. |

### <a name="exit-codes"></a>Codici di uscita

| Codice |Risultato | Descrizione |
|----------------|-----------|-----------|
| 0 | Riuscito | Le credenziali sono state acquisite correttamente e sono stati scritti in stdout.|
| 1 | ProviderNotApplicable | Il provider corrente non fornire le credenziali per l'URI specificato.|
| 2 | Errore | Il provider è il provider corretto per l'URI specificato, ma non è possibile fornire le credenziali. In questo caso, nuget.exe non tenterà di autenticazione e avrà esito negativo. Un esempio tipico è quando un utente annulla un account di accesso interattivo. |

### <a name="standard-output"></a>Output standard

| Proprietà |Note|
|----------------|-----------|
| Nome utente | Nome utente per le richieste autenticate.|
| Password | Password per le richieste autenticate.|
| Messaggio | Dettagli facoltativi sulla risposta, è utilizzata solo per visualizzare ulteriori dettagli in caso di errore. |

Stdout di esempio:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Risoluzione dei problemi relativi a un provider di credenziali

Al momento, NuGet non fornisce molto supporto diretto per il debug di provider di credenziali personalizzate. [emettere 4598](https://github.com/NuGet/Home/issues/4598) tiene traccia di questo lavoro.

È inoltre possibile eseguire le operazioni seguenti:

- Eseguire nuget.exe con il `-verbosity` commutatore per controllare l'output dettagliato.
- Aggiungere i messaggi di debug per `stdout` nelle posizioni appropriate.
- Assicurarsi che si usi nuget.exe 3.3 o versione successiva.
- Collega debugger all'avvio con questo frammento di codice:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Per ulteriore assistenza, [inviare una richiesta di supporto un nuget.org](https://www.nuget.org/policies/Contact).
