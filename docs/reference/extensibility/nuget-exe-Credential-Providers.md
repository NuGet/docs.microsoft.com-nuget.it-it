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
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticazione di feed con provider nuget.exe credenziali

Nella versione `3.3` è stato aggiunto il supporto per provider di credenziali `nuget.exe` specifici. Da allora, nella versione è stato aggiunto il supporto per i provider di credenziali che funzionano in tutti gli scenari della riga di comando `4.8` [](NuGet-Cross-Platform-Authentication-Plugin.md) ( , `nuget.exe` , `dotnet.exe` `msbuild.exe` ).

Per [altri dettagli su tutti gli approcci di](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) autenticazione per , vedere Utilizzo di pacchetti da feed autenticati `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe individuazione del provider di credenziali

nuget.exe provider di credenziali possono essere usati in 3 modi:

- **A livello globale:** per rendere disponibile un provider di credenziali per tutte le istanze di eseguite nel `nuget.exe` profilo dell'utente corrente, aggiungerlo a `%LocalAppData%\NuGet\CredentialProviders` . Potrebbe essere necessario creare la `CredentialProviders` cartella. I provider di credenziali possono essere installati nella radice della cartella `CredentialProviders`  o all'interno di una sottocartella. Se un provider di credenziali dispone di più file/assembly, è possibile usare le sottocartelle per mantenere organizzati i provider.

- **Da una variabile di ambiente**: i provider di credenziali possono essere archiviati ovunque e resi accessibili impostando la variabile di ambiente sul percorso del `nuget.exe` `%NUGET_CREDENTIALPROVIDERS_PATH%` provider. Questa variabile può essere un elenco separato da punti e virgola (ad esempio, `path1;path2` ) se si dispone di più posizioni.

- **Insieme nuget.exe**: nuget.exe provider di credenziali possono essere inseriti nella stessa cartella di `nuget.exe` .

Quando si caricano i provider di credenziali, cerca nei percorsi precedenti, nell'ordine, qualsiasi file denominato , quindi carica i `nuget.exe` `credentialprovider*.exe` file nell'ordine in cui vengono trovati. Se nella stessa cartella sono presenti più provider di credenziali, vengono caricati in ordine alfabetico.

## <a name="creating-a-nugetexe-credential-provider"></a>Creazione di un provider nuget.exe credenziali

Un provider di credenziali è un eseguibile della riga di comando, denominato nel formato , che raccoglie gli input, acquisisce le credenziali in base alle esigenze e quindi restituisce il codice di stato di uscita appropriato e `CredentialProvider*.exe` l'output standard.

Un provider deve eseguire le operazioni seguenti:

- Determinare se può fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali. In caso contrario, deve restituire il codice di stato 1 senza credenziali.
- Non modificare `NuGet.Config` (ad esempio, l'impostazione delle credenziali).
- Gestire la configurazione del proxy HTTP da sola, in quanto NuGet non fornisce informazioni sul proxy al plug-in.
- Restituire credenziali o dettagli dell'errore scrivendo un oggetto risposta JSON (vedere di `nuget.exe` seguito) in stdout, usando la codifica UTF-8.
- Facoltativamente, generare la registrazione di traccia aggiuntiva in stderr. Non è mai necessario scrivere segreti in stderr, poiché a livelli di dettaglio "normali" o "dettagliate" tali tracce vengono echeggiate da NuGet nella console.
- I parametri imprevisti devono essere ignorati, garantendo la compatibilità con le versioni future di NuGet.

### <a name="input-parameters"></a>Parametri di input

| Parametro/opzione |Descrizione|
|----------------|-----------|
| URI {value} | URI di origine del pacchetto che richiede le credenziali.|
| NonInteractive | Se presente, il provider non emettere richieste interattive. |
| IsRetry | Se presente, indica che questo tentativo è un nuovo tentativo di un tentativo non riuscito in precedenza. I provider usano in genere questo flag per assicurarsi di ignorare qualsiasi cache esistente e richiedere nuove credenziali, se possibile.|
| Livello di dettaglio {value} | Se presente, uno dei valori seguenti: "normal", "quiet" o "detailed". Se non viene specificato alcun valore, il valore predefinito è "normal". I provider devono usarlo come indicazione del livello di registrazione facoltativo da generare nel flusso di errore standard. |

### <a name="exit-codes"></a>Codici di uscita

| Codice |Risultato | Descrizione |
|----------------|-----------|-----------|
| 0 | Operazione completata | Le credenziali sono state acquisite correttamente e sono state scritte in stdout.|
| 1 | ProviderNotApplicable | Il provider corrente non fornisce le credenziali per l'URI specificato.|
| 2 | Operazioni non riuscite | Il provider è il provider corretto per l'URI specificato, ma non può fornire credenziali. In questo caso, nuget.exe ritentare l'autenticazione e avrà esito negativo. Un esempio tipico è quando un utente annulla un account di accesso interattivo. |

### <a name="standard-output"></a>Output standard

| Proprietà |Note|
|----------------|-----------|
| Username | Nome utente per le richieste autenticate.|
| Password | Password per le richieste autenticate.|
| Message | Dettagli facoltativi sulla risposta, usati solo per visualizzare dettagli aggiuntivi nei casi di errore. |

Stdout di esempio:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>Risoluzione dei problemi relativi a un provider di credenziali

Attualmente, NuGet non offre un supporto diretto per il debug di provider di credenziali personalizzati. [il problema 4598](https://github.com/NuGet/Home/issues/4598) sta verificando questo lavoro.

È inoltre possibile eseguire le operazioni seguenti:

- Eseguire nuget.exe con `-verbosity` l'opzione per esaminare l'output dettagliato.
- Aggiungere messaggi di debug `stdout` a nelle posizioni appropriate.
- Assicurarsi di usare nuget.exe 3.3 o versione successiva.
- Collegare il debugger all'avvio con questo frammento di codice:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
