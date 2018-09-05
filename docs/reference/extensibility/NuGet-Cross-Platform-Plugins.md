---
title: NuGet cross-platform i plug-in
description: NuGet cross platform i plug-in per NuGet.exe, dotnet.exe, msbuild.exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548206"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet cross-platform i plug-in

In NuGet 4.8 è stato aggiunto il supporto per la cross-platform i plug-in.
Si è ottenuta con creando un nuovo modello di estendibilità di plug-in, che deve essere conforme a un set di regole dell'operazione di tipo strict.
I plug-in sono file eseguibili indipendenti (runnables nel mondo .NET Core), che avviano i client di NuGet in un processo separato.
Si tratta di una scrittura true una sola volta, eseguire ovunque plug-in. Funzionerà con tutti gli strumenti client NuGet.
I plug-in può essere solo .NET Framework (NuGet.exe, MSBuild.exe e Visual Studio), o .NET Core (dotnet.exe).
È definito un protocollo di comunicazione con controllo delle versioni tra il Client di NuGet e il plug-in. Durante l'handshake di avvio, i 2 processi negoziano la versione del protocollo.

Per coprire tutti gli scenari di strumenti client NuGet, uno necessarie di .NET Framework sia un plug-in .NET Core.
Di seguito vengono descritte le combinazioni di framework client/del plug-in.

| Strumento client  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| NuGet.exe su Mono | .NET Framework |

## <a name="how-does-it-work"></a>Come funziona

Il flusso di lavoro di alto livello può essere descritte come segue:

1. NuGet consente di individuare i plug-in disponibili.
1. Quando applicabile, NuGet scorre i plug-in ordine di priorità e viene avviato uno alla volta.
1. NuGet verrà utilizzato il primo plug-in grado di servire la richiesta.
1. I plug-in verrà arrestata quando non sono più necessari.

## <a name="general-plugin-requirements"></a>Requisiti di plug-in generale

È la versione corrente del protocollo *2.0.0*.
In questa versione, i requisiti sono i seguenti:

- Dispone di un assembly firma Authenticode in valida e attendibile che verrà eseguito in Windows e Mono. È richiesta alcun trust speciali per gli assembly ancora in esecuzione in Linux e Mac. [Problema pertinente](https://github.com/NuGet/Home/issues/6702)
- Supporta l'avvio senza stato nel contesto di sicurezza corrente degli strumenti client NuGet. Ad esempio, gli strumenti client NuGet non eseguirà l'elevazione dei privilegi o un'inizializzazione aggiuntiva all'esterno del protocollo di plug-in descritti più avanti.
- Modo non interattivo, a meno che non specificato in modo esplicito.
- Rispettare la versione del protocollo negoziato plug-in.
- Rispondere a tutte le richieste nel periodo di tempo ragionevole.
- Soddisfa le richieste di annullamento per qualsiasi operazione in corso.

Le specifiche tecniche sono descritto più dettagliatamente le specifiche seguenti:

- [Plug-in di Download del pacchetto NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet cross-plat plug-in di autenticazione](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Client - l'interazione di plug-in

Strumenti client NuGet e il plug-in di comunicare con JSON nei flussi standard (stdin, stdout, stderror). Tutti i dati devono essere con codificata UTF-8.
I plug-in vengono avviate con l'argomento "-plug-in". Nel caso in cui un utente avvia direttamente un plug-in eseguibile senza questo argomento, il plug-in può concedere a un messaggio informativo anziché attendere un handshake del protocollo.
Timeout di handshake del protocollo è 5 secondi. Il plug-in deve completare l'installazione in come oltre a una quantità possibile.
Strumenti client NuGet saranno supportati per di un plug-in operazioni di query passando l'indice del servizio per un'origine NuGet. Un plug-in può usare l'indice del servizio per verificare la presenza di tipi di servizio supportato.

La comunicazione tra gli strumenti client NuGet e il plug-in è bidirezionale. Ogni richiesta ha un timeout di 5 secondi. Se le operazioni sono considerate allungamento dei tempi per il processo corrispondente deve inviare un messaggio di stato di avanzamento a evitare il timeout della richiesta. Dopo un minuto di inattività un plug-in è considerato inattivo e viene arrestata.

## <a name="plugin-installation-and-discovery"></a>Individuazione e l'installazione di plug-in

I plug-in verrà individuato tramite una struttura di directory basato sulle convenzioni.
Scenari di integrazione continua/recapito Continuo e gli utenti esperti possono usare una variabile di ambiente per eseguire l'override del comportamento.

- `NUGET_PLUGIN_PATHS` -Definisce i plug-in che verrà usato per tale processo di NuGet, priorità sono riservate. Se è impostata questa variabile di ambiente, viene eseguito l'override dell'individuazione basato sulle convenzioni.
-  Percorso utente, il percorso della home page di NuGet in `%UserProfile%/.nuget/plugins`. Questo percorso non può essere sottoposta a override. Verrà usata una directory radice diversa per plug-in .NET Core e .NET Framework.

| Framework | Percorso radice individuazione  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Ogni plug-in deve essere installato nella relativa cartella.
Il punto di ingresso di plug-in è il nome della cartella di installazione, con le estensioni di file DLL per .NET Core ed estensione .exe per .NET Framework.

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
> Attualmente non è disponibile nessuna storia utente per l'installazione del plug-in. È semplice, basta spostare i file necessari nel percorso predeterminato.

## <a name="supported-operations"></a>Operazioni supportate

Due operazioni sono supportate con il nuovo protocollo di plug-in.

| Nome dell'operazione | Versione minima del protocollo | Versione client NuGet minima |
| -------------- | ----------------------- | --------------------- |
| Scaricare il pacchetto | 1.0.0 | 4.3.0 |
| [Autenticazione](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Esecuzione di plug-in con il runtime corretto

Per NuGet negli scenari dotnet.exe, necessario essere in grado di eseguire in tale specifica del runtime del dotnet.exe plug-in.
È attivo il provider di plug-in e i consumer per assicurarsi che viene utilizzata una combinazione di dotnet.exe/plugin compatibile.
Potrebbe verificarsi un problema potenziale con i plug-in di percorso utente quando, ad esempio, un dotnet.exe sotto il runtime 2.0 tenta di usare un plug-in scritto per il runtime 2.1.

## <a name="capabilities-caching"></a>Funzionalità di memorizzazione nella cache

La verifica di sicurezza e le istanze di plug-in è costosa. L'operazione di download accade molto più frequente rispetto dell'operazione di autenticazione, tuttavia, l'utente medio di NuGet è solo potrebbe avere un plug-in di autenticazione.
Per migliorare l'esperienza, NuGet memorizza nella cache le attestazioni di operazione per la richiesta specificata. Questa cache è per ogni plug-in con la chiave di plug-in corso il percorso del plug-in, e la scadenza per la cache questa funzionalità è di 30 giorni. 

La cache si trova `%LocalAppData%/NuGet/plugins-cache` e di eseguire l'override con la variabile di ambiente `NUGET_PLUGINS_CACHE_PATH`. Per cancellare questa [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), sarà possibile eseguire le variabili locali con il `plugins-cache` opzione.
Il `all` opzione variabili locali adesso eliminerà anche la cache di plug-in. 

## <a name="protocol-messages-index"></a>Indice dei messaggi di protocollo

Versione del protocollo *1.0.0* messaggi:

1.  Chiudi
    * Richiesta direzione: NuGet -> plug-in
    * La richiesta non conterrà alcun payload
    * È prevista alcuna risposta.  La risposta appropriata è per il processo di plug-in uscire immediatamente.

2.  Copiare i file nel pacchetto
    * Richiesta direzione: NuGet -> plug-in
    * Conterrà la richiesta:
        * l'ID del pacchetto e versione
        * percorso del repository di origine del pacchetto
        * percorso di directory di destinazione
        * enumerabile di file del pacchetto da copiare nel percorso di directory di destinazione
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione
        * enumerabile di percorsi completi per i file copiati nella directory di destinazione se l'operazione è riuscita

3.  Copiare il file di pacchetto (con estensione nupkg)
    * Richiesta direzione: NuGet -> plug-in
    * Conterrà la richiesta:
        * l'ID del pacchetto e versione
        * percorso del repository di origine del pacchetto
        * il percorso del file di destinazione
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione

4.  Ottenere le credenziali
    * Richiesta direzione: plug-in -> NuGet
    * Conterrà la richiesta:
        * percorso del repository di origine del pacchetto
        * il codice di stato HTTP ottenuto dal repository di origine del pacchetto usando le credenziali correnti
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione
        * un nome utente, se disponibile
        * una password, se disponibile

5.  Ottenere i file di pacchetto
    * Richiesta direzione: NuGet -> plug-in
    * Conterrà la richiesta:
        * l'ID del pacchetto e versione
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione
        * oggetto enumerabile di percorsi di file del pacchetto se l'operazione è riuscita

6.  Ottenere le attestazioni di operazione 
    * Richiesta direzione: NuGet -> plug-in
    * Conterrà la richiesta:
        * il servizio Index per un'origine pacchetto
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione
        * oggetto enumerabile di operazioni supportate (ad esempio: download del pacchetto) se l'operazione ha esito positivo.  Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.

> [!Note]
> Questo messaggio è stato aggiornato nella versione *2.0.0*. È nel client per mantenere la compatibilità con le versioni precedenti.

7.  Ottenere l'hash del pacchetto
    * Richiesta direzione: NuGet -> plug-in
    * Conterrà la richiesta:
        * l'ID del pacchetto e versione
        * percorso del repository di origine del pacchetto
        * l'algoritmo hash
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione
        * un hash del file del pacchetto usando l'algoritmo hash richiesto se l'operazione è riuscita

8.  Ottenere le versioni dei pacchetti
    * Richiesta direzione: NuGet -> plug-in
    * Conterrà la richiesta:
        * l'ID del pacchetto
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione
        * enumerabile di versioni del pacchetto se l'operazione è riuscita

9.  Ottenere l'indice del servizio
    * Richiesta direzione: plug-in -> NuGet
    * Conterrà la richiesta:
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione
        * l'indice del servizio se l'operazione è riuscita

10.  Handshake
     * Richiesta direzione: plug-in NuGet <> –
     * Conterrà la richiesta:
         * la versione corrente del protocollo plug-in
         * la versione minima supportata di versione del protocollo plug-in
     * Una risposta conterrà:
         * un codice di risposta che indica il risultato dell'operazione
         * la versione del protocollo negoziato se l'operazione ha esito positivo.  Un errore comporterà la terminazione del plug-in.

11.  inizializzare
     * Richiesta direzione: NuGet -> plug-in
     * Conterrà la richiesta:
         * la versione dello strumento client di NuGet
         * NuGet lingua del client degli strumenti efficace.  Si prende in considerazione l'impostazione ForceEnglishOutput, se utilizzato.
         * il timeout di richiesta predefinito, che sostituisce il valore predefinito di protocollo.
     * Una risposta conterrà:
         * un codice di risposta che indica il risultato dell'operazione.  Un errore comporterà la terminazione del plug-in.

12.  Registro
     * Richiesta direzione: plug-in -> NuGet
     * Conterrà la richiesta:
         * il livello di registrazione per la richiesta
         * un messaggio da registrare
     * Una risposta conterrà:
         * un codice di risposta che indica il risultato dell'operazione.

13.  Uscita dal processo di monitoraggio NuGet
     * Richiesta direzione: NuGet -> plug-in
     * Conterrà la richiesta:
         * l'ID di processo di NuGet
     * Una risposta conterrà:
         * un codice di risposta che indica il risultato dell'operazione.

14.  Prelettura del pacchetto
     * Richiesta direzione: NuGet -> plug-in
     * Conterrà la richiesta:
         * l'ID del pacchetto e versione
         * percorso del repository di origine del pacchetto
     * Una risposta conterrà:
         * un codice di risposta che indica il risultato dell'operazione

15.  Insieme di credenziali
     * Richiesta direzione: NuGet -> plug-in
     * Conterrà la richiesta:
         * percorso del repository di origine del pacchetto
         * l'ultimo pacchetto noti origine nome utente, se disponibile
         * l'ultima password di origine di pacchetti note, se disponibile
         * l'ultimo noti nome utente proxy, se disponibile
         * l'ultima password nota proxy, se disponibile
     * Una risposta conterrà:
         * un codice di risposta che indica il risultato dell'operazione

16.  Livello del set di log
     * Richiesta direzione: NuGet -> plug-in
     * Conterrà la richiesta:
         * il livello di registrazione predefinito
     * Una risposta conterrà:
         * un codice di risposta che indica il risultato dell'operazione

Versione del protocollo *2.0.0* messaggi

17. Ottenere le attestazioni di operazione

* Richiesta direzione: NuGet -> plug-in
    * Conterrà la richiesta:
        * il servizio Index per un'origine pacchetto
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * un codice di risposta che indica il risultato dell'operazione
        * oggetto enumerabile di operazioni supportate se l'operazione ha esito positivo.  Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.

    Se l'origine di indice e pacchetto del servizio è null, il plug-in può rispondere con l'autenticazione.

18. Ottenere le credenziali di autenticazione

* Richiesta direzione: NuGet -> plug-in
* Conterrà la richiesta:
    * URI
    * isRetry
    * Non interattive
    * CanShowDialog
* Conterrà una risposta
    * Nome utente
    * Password
    * Messaggio
    * Elenco dei tipi di autenticazione
    * MessageResponseCode