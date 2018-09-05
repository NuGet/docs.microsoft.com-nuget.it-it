---
title: Provider di credenziali NuGet.exe
description: i provider di credenziali NuGet.exe autenticarsi con un feed e vengono implementati come file eseguibili della riga di comando che seguono le convenzioni specifiche.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550189"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>L'autenticazione di feed con i provider di credenziali nuget.exe

*NuGet 3.3 +*

Quando `nuget.exe` necessita di credenziali per l'autenticazione con un feed, Cerca li nel modo seguente:

1. NuGet cerca innanzitutto le credenziali in `Nuget.Config` file.
1. NuGet Usa quindi i provider di credenziali plug-in, soggette a ordine indicato di seguito. (E l'esempio è il [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet quindi chiede all'utente le credenziali nella riga di comando.

Si noti che i provider di credenziali descritti di seguito funzionano solo in `nuget.exe` e non in 'dotnet restore' o Visual Studio. Per i provider di credenziali con Visual Studio, vedere [nuget.exe i provider di credenziali per Visual Studio](nuget-credential-providers-for-visual-studio.md)

i provider di credenziali NuGet.exe sono utilizzabili in 3 modi:

- **A livello globale**: per rendere disponibili per tutte le istanze di un provider di credenziali `nuget.exe` eseguito al profilo dell'utente corrente, aggiungerlo alla `%LocalAppData%\NuGet\CredentialProviders`. Potrebbe essere necessario creare il `CredentialProviders` cartella. I provider di credenziali possono essere installati nella radice di `CredentialProviders` cartella o all'interno di una sottocartella. Se un provider di credenziali dispone di più file o assembly, è possibile utilizzare le sottocartelle per mantenere i provider organizzati.

- **Da una variabile di ambiente**: i provider di credenziali possono essere archiviati in qualsiasi posizione e rese accessibili agli `nuget.exe` impostando il `%NUGET_CREDENTIALPROVIDERS_PATH%` variabile di ambiente per il percorso del provider. Questa variabile può essere un elenco delimitato da punto e virgola (, ad esempio, `path1;path2`) se si dispone di più sedi.

- **Insieme a nuget.exe**: i provider di credenziali nuget.exe possono essere inseriti nella stessa cartella `nuget.exe`.

Quando si caricano i provider di credenziali `nuget.exe` cerca i percorsi precedenti, in ordine, per qualsiasi file denominato `credentialprovider*.exe`, quindi carica tali file nell'ordine in cui si trovano. In presenza di più provider di credenziali nella stessa cartella, caricati in ordine alfabetico.

## <a name="creating-a-nugetexe-credential-provider"></a>Creazione di un provider di credenziali nuget.exe

Un provider di credenziali è un file eseguibile da riga di comando, il formato `CredentialProvider*.exe`, che raccoglie gli input, acquisisce le credenziali come appropriato e quindi restituisce il codice di stato di uscita appropriato e l'output standard.

Un provider deve eseguire le operazioni seguenti:

- Determinare se è possibile fornire le credenziali per l'URI di destinazione prima di iniziare l'acquisizione delle credenziali. In caso contrario deve restituire il codice di stato 1 senza credenziali.
- Non modificare `Nuget.Config` (ad esempio, l'impostazione delle credenziali esiste).
- Configurazione del proxy HTTP di handle in modo autonomo, come NuGet non fornisce informazioni sul proxy per il plug-in.
- Restituisce le credenziali o i dettagli dell'errore per `nuget.exe` mediante la scrittura di un oggetto di risposta JSON (vedere sotto) a stdout, usando la codifica UTF-8.
- Creare facoltativamente la registrazione di traccia aggiuntivi in stderr. Alcun segreto non deve mai essere scritte in stderr, poiché i livelli di dettaglio "normale" o "dettagliato" tali tracce vengono restituite da NuGet alla console.
- Parametri imprevisti devono essere ignorati, fornendo la compatibilità con le versioni future di NuGet.

### <a name="input-parameters"></a>Parametri di input

| Parametro/Switch |Descrizione|
|----------------|-----------|
| URI {value} | URI che richiede credenziali per l'origine pacchetto.|
| Non interattive | Se presente, provider non viene visualizzato un prompt interattivo. |
| isRetry | Se presente, indica che questo tentativo è un nuovo tentativo di un tentativo non riuscito in precedenza. I provider usano in genere questo flag per assicurarsi di ignorare tutte le cache esistenti e richiedere le nuove credenziali se possibile.|
| Livello di dettaglio {value} | Se presente, uno dei seguenti valori: "normale", "quiet" o "dettagliato". Se viene specificato alcun valore, valore predefinito è "normale". Provider devono utilizzare ciò come un'indicazione del livello di registrazione facoltative per generare il flusso di errore standard. |

### <a name="exit-codes"></a>Codici di uscita

| Codice |Risultato | Descrizione |
|----------------|-----------|-----------|
| 0 | Riuscito | Le credenziali sono state acquisite correttamente e sono stati scritti in stdout.|
| 1 | ProviderNotApplicable | Il provider corrente non fornisce le credenziali per l'URI specificato.|
| 2 | Errore | Il provider è il provider corretto per l'URI specificato, ma non è possibile fornire le credenziali. In questo caso, nuget.exe non tenterà di eseguire l'autenticazione e avrà esito negativo. Un esempio tipico è quando un utente annulla un accesso interattivo. |

### <a name="standard-output"></a>Output standard

| Proprietà |Note|
|----------------|-----------|
| Nome utente | Nome utente per le richieste autenticate.|
| Password | Password per le richieste autenticate.|
| Messaggio | Dettagli facoltativi relative alla risposta, usato solo per visualizzare altri dettagli in caso di errore. |

Esempio stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Risoluzione dei problemi relativi a un provider di credenziali

Al momento, NuGet non fornisce molto supporto diretto per il debug di provider di credenziali personalizzate. [emettere 4598](https://github.com/NuGet/Home/issues/4598) tiene traccia di questo lavoro.

È inoltre possibile eseguire le operazioni seguenti:

- Eseguire nuget.exe con il `-verbosity` passa a esaminare l'output dettagliato.
- Aggiungere i messaggi di debug `stdout` nelle posizioni appropriate.
- Assicurarsi che si usi nuget.exe 3.3 o versioni successive.
- Collega debugger all'avvio con questo frammento di codice:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Per ulteriore assistenza, [inviare una richiesta di supporto un nuget.org](https://www.nuget.org/policies/Contact).
