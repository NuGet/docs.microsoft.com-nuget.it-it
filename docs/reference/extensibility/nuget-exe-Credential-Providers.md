---
title: Provider di credenziali nuget.exe
description: nuget.exe i provider di credenziali eseguono l'autenticazione con un feed e vengono implementati come eseguibili da riga di comando che seguono convenzioni specifiche.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238114"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticazione dei feed con nuget.exe provider di credenziali

Nel supporto della versione `3.3` è stato aggiunto per `nuget.exe` provider di credenziali specifici. Successivamente, `4.8` è stato aggiunto il supporto della versione [per i provider di credenziali](NuGet-Cross-Platform-Authentication-Plugin.md) che funzionano in tutti gli scenari della riga di comando ( `nuget.exe` , `dotnet.exe` , `msbuild.exe` ).

Per altri dettagli su tutti gli approcci di autenticazione per, vedere [utilizzo dei pacchetti dai feed autenticati](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)`nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>Individuazione del provider di credenziali nuget.exe

nuget.exe i provider di credenziali possono essere usati in tre modi:

- A **livello globale** : per rendere disponibile un provider di credenziali per tutte le istanze di `nuget.exe` in esecuzione nel profilo dell'utente corrente, aggiungerlo a `%LocalAppData%\NuGet\CredentialProviders` . Potrebbe essere necessario creare la `CredentialProviders` cartella. I provider di credenziali possono essere installati alla radice della `CredentialProviders`  cartella o all'interno di una sottocartella. Se un provider di credenziali dispone di più file/assembly, è possibile utilizzare le sottocartelle per organizzare i provider.

- **Da una variabile di ambiente** : i provider di credenziali possono essere archiviati ovunque e resi accessibili a impostando `nuget.exe` la `%NUGET_CREDENTIALPROVIDERS_PATH%` variabile di ambiente sul percorso del provider. Questa variabile può essere un elenco delimitato da punti e virgola (ad esempio, `path1;path2` ) se sono presenti più percorsi.

- **Insieme a nuget.exe** : nuget.exe i provider di credenziali possono essere inseriti nella stessa cartella del `nuget.exe` .

Quando si caricano i provider di credenziali, `nuget.exe` Cerca nei percorsi precedenti, in ordine, tutti i file denominati `credentialprovider*.exe` , quindi carica i file nell'ordine in cui sono stati trovati. Se nella stessa cartella sono presenti più provider di credenziali, questi vengono caricati in ordine alfabetico.

## <a name="creating-a-nugetexe-credential-provider"></a>Creazione di un provider di credenziali nuget.exe

Un provider di credenziali è un eseguibile della riga di comando, denominato nel formato `CredentialProvider*.exe` , che raccoglie gli input, acquisisce le credenziali nel modo appropriato e quindi restituisce il codice di stato di uscita appropriato e l'output standard.

Un provider deve eseguire le operazioni seguenti:

- Determinare se può fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali. In caso contrario, deve restituire il codice di stato 1 senza credenziali.
- Non modificare `Nuget.Config` (ad esempio l'impostazione delle credenziali).
- Gestire autonomamente la configurazione del proxy HTTP, poiché NuGet non fornisce informazioni sul proxy al plug-in.
- Restituire le credenziali o i dettagli `nuget.exe` dell'errore a scrivendo un oggetto risposta JSON (vedere di seguito) in stdout, usando la codifica UTF-8.
- Facoltativamente, è possibile creare la registrazione traccia aggiuntiva in stderr. Nessun segreto deve essere mai scritto in stderr, perché a livello di dettaglio "normale" o "dettagliato" tali tracce vengono riportate da NuGet alla console.
- I parametri imprevisti devono essere ignorati, garantendo la compatibilità con le versioni future di NuGet.

### <a name="input-parameters"></a>Parametri di input

| Parametro/opzione |Descrizione|
|----------------|-----------|
| URI {valore} | URI di origine del pacchetto che richiede le credenziali.|
| NonInteractive | Se presente, il provider non rilascia richieste interattive. |
| Numero di tentativi | Se presente, indica che il tentativo di un tentativo non riuscito in precedenza è stato ritentato. I provider usano in genere questo flag per assicurarsi che ignorino eventuali cache esistenti e chiedano nuove credenziali, se possibile.|
| Livello di dettaglio {value} | Se presente, uno dei valori seguenti: "Normal", "quiet" o "detailed". Se non viene specificato alcun valore, il valore predefinito è "Normal". I provider devono utilizzarlo come indicazione del livello di registrazione facoltativa da emettere nel flusso di errore standard. |

### <a name="exit-codes"></a>Codici di uscita

| Codice |Risultato | Descrizione |
|----------------|-----------|-----------|
| 0 | Operazione completata | Le credenziali sono state acquisite e sono state scritte in stdout.|
| 1 | ProviderNotApplicable | Il provider corrente non fornisce le credenziali per l'URI specificato.|
| 2 | Errore | Il provider è il provider corretto per l'URI specificato, ma non è in grado di fornire le credenziali. In questo caso, nuget.exe non tenterà di eseguire l'autenticazione e avrà esito negativo. Un esempio tipico è quando un utente annulla un accesso interattivo. |

### <a name="standard-output"></a>Output standard

| Proprietà |Note|
|----------------|-----------|
| Nome utente | Nome utente per le richieste autenticate.|
| Password | Password per le richieste autenticate.|
| Message | Dettagli facoltativi sulla risposta, usati solo per visualizzare dettagli aggiuntivi nei casi di errore. |

Esempio di stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Risoluzione dei problemi relativi a un provider di credenziali

Attualmente, NuGet non fornisce un supporto molto diretto per il debug di provider di credenziali personalizzati; il [problema 4598](https://github.com/NuGet/Home/issues/4598) sta tenendo traccia del lavoro.

È inoltre possibile eseguire le operazioni seguenti:

- Eseguire nuget.exe con l' `-verbosity` opzione per esaminare l'output dettagliato.
- Aggiungere i messaggi di debug a `stdout` in posizioni appropriate.
- Assicurarsi di usare nuget.exe 3,3 o versione successiva.
- Connetti debugger all'avvio con il frammento di codice seguente:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
