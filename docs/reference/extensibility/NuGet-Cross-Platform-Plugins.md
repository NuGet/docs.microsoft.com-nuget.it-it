---
title: Plug-in NuGet multipiattaforma
description: Plug-in NuGet multipiattaforma per NuGet. exe, dotnet. exe, MSBuild. exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380504"
---
# <a name="nuget-cross-platform-plugins"></a>Plug-in NuGet multipiattaforma

È stato aggiunto il supporto NuGet 4.8 + per i plug-in di multipiattaforma.
Questa operazione è stata realizzata con creando un nuovo modello di estendibilità dei plug-in, che deve essere conforme a un set di regole di funzionamento rigoroso.
I plug-in sono file eseguibili autonomi (eseguibili in .NET Core World), che i client NuGet avviano in un processo separato.
Si tratta di una vera e propria scrittura, Esegui il plug-in Everywhere. Funzionerà con tutti gli strumenti client NuGet.
I plug-in possono essere .NET Framework (NuGet. exe, MSBuild. exe e Visual Studio) o .NET Core (dotnet. exe).
Viene definito un protocollo di comunicazione con versione tra il client NuGet e il plug-in. Durante l'handshake di avvio, i 2 processi negoziano la versione del protocollo.

Per coprire tutti gli scenari di strumenti client NuGet, è necessario disporre sia di un .NET Framework che di un plug-in .NET Core.
Di seguito vengono descritte le combinazioni client/Framework dei plug-in.

| Strumento client  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet. exe | .NET Core |
| NuGet. exe | .NET Framework |
| MSBuild. exe | .NET Framework |
| NuGet. exe in mono | .NET Framework |

## <a name="how-does-it-work"></a>Funzionamento

Il flusso di lavoro di alto livello può essere descritto di seguito:

1. NuGet individua i plug-in disponibili.
1. Quando applicabile, NuGet esegue l'iterazione dei plug-in in ordine di priorità e li avvia uno alla volta.
1. NuGet userà il primo plug-in che può servire la richiesta.
1. I plug-in verranno arrestati quando non sono più necessari.

## <a name="general-plugin-requirements"></a>Requisiti generali per il plug-in

La versione del protocollo corrente è *2.0.0*.
In questa versione, i requisiti sono i seguenti:

- Disporre di assembly di firma Authenticode attendibili validi che vengono eseguiti in Windows e mono. Non esiste ancora un requisito di attendibilità speciale per gli assembly eseguiti in Linux e Mac. [Problema pertinente](https://github.com/NuGet/Home/issues/6702)
- Supportare l'avvio senza stato nel contesto di sicurezza corrente degli strumenti client NuGet. Ad esempio, gli strumenti client NuGet non eseguono l'elevazione dei privilegi o l'inizializzazione aggiuntiva all'esterno del protocollo plug-in descritto più avanti.
- Essere non interattivo, a meno che non venga specificato in modo esplicito.
- Rispettare la versione del protocollo di plug-in negoziato.
- Rispondere a tutte le richieste entro un periodo di tempo ragionevole.
- Rispettare le richieste di annullamento per qualsiasi operazione in corso.

Le specifiche tecniche sono descritte più dettagliatamente nelle specifiche seguenti:

- [Plug-in di download del pacchetto NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Plug-in autenticazione NuGet Cross Plat](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Interazione client-plug-in

Gli strumenti client NuGet e i plug-in comunicano con JSON su flussi standard (stdin, stdout, stderr). Tutti i dati devono essere codificati in UTF-8.
I plug-in vengono avviati con l'argomento "-plugin". Se un utente avvia direttamente un eseguibile del plug-in senza questo argomento, il plug-in può fornire un messaggio informativo invece di attendere un handshake del protocollo.
Il timeout dell'handshake del protocollo è di 5 secondi. Il plug-in deve completare il programma di installazione nel minor tempo possibile.
Gli strumenti client NuGet eseguiranno una query sulle operazioni supportate da un plug-in tramite il passaggio dell'indice del servizio per un'origine NuGet. Un plug-in può usare l'indice del servizio per verificare la presenza di tipi di servizio supportati.

La comunicazione tra gli strumenti client NuGet e il plug-in è bidirezionale. Ogni richiesta ha un timeout di 5 secondi. Se le operazioni dovrebbero richiedere più tempo, il rispettivo processo deve inviare un messaggio di stato per impedire il timeout della richiesta. Dopo 1 minuto di inattività, un plug-in viene considerato inattivo e viene arrestato.

## <a name="plugin-installation-and-discovery"></a>Installazione e individuazione di plug-in

I plug-in verranno individuati tramite una struttura di directory basata sulla convenzione.
Gli scenari di integrazione continua/distribuzione continua e gli utenti esperti possono usare variabili di ambiente per eseguire l'override del comportamento. Quando si usano le variabili di ambiente, sono consentiti solo i percorsi assoluti. Si noti che `NUGET_NETFX_PLUGIN_PATHS` e `NUGET_NETCORE_PLUGIN_PATHS` sono disponibili solo con la versione 5.3 + degli strumenti NuGet e versioni successive.

- `NUGET_NETFX_PLUGIN_PATHS`: definisce i plug-in che verranno usati dagli strumenti basati su .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio). Ha la precedenza rispetto a `NUGET_PLUGIN_PATHS`. (Solo NuGet versione 5.3 +)
- `NUGET_NETCORE_PLUGIN_PATHS`: definisce i plug-in che verranno usati dagli strumenti basati su .NET Core (dotnet. exe). Ha la precedenza rispetto a `NUGET_PLUGIN_PATHS`. (Solo NuGet versione 5.3 +)
- `NUGET_PLUGIN_PATHS`: definisce i plug-in che verranno usati per il processo NuGet, priorità mantenuta. Se questa variabile di ambiente è impostata, sostituisce l'individuazione basata sulla convenzione. Viene ignorato se viene specificata una delle variabili specifiche del Framework.
-  Utente-location, il percorso Home di NuGet in `%UserProfile%/.nuget/plugins`. Non è possibile eseguire l'override di questo percorso. Verrà usata una directory radice diversa per i plug-in .NET Core e .NET Framework.

| Framework | Percorso di individuazione radice  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Ogni plug-in deve essere installato in una cartella specifica.
Il punto di ingresso del plug-in sarà il nome della cartella installata, con le estensioni dll per .NET Core e l'estensione exe per .NET Framework.

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
> Attualmente non è disponibile alcuna storia utente per l'installazione dei plug-in. È semplice quanto lo spostamento dei file necessari nella posizione predeterminata.

## <a name="supported-operations"></a>Operazioni supportate

Sono supportate due operazioni nel nuovo protocollo plug-in.

| Nome operazione | Versione minima del protocollo | Versione minima del client NuGet |
| -------------- | ----------------------- | --------------------- |
| Scarica pacchetto | 1.0.0 | 4.3.0 |
| [Autenticazione](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Esecuzione di plug-in nel runtime corretto

Per gli scenari di NuGet in dotnet. exe, è necessario che i plug-in siano in grado di eseguire il runtime specifico di DotNet. exe.
Si tratta del provider di plug-in e del consumer per assicurarsi che venga usata una combinazione dotnet. exe/plugin compatibile.
Un potenziale problema può verificarsi con i plug-in della posizione utente quando, ad esempio, un file dotnet. exe nel runtime di 2,0 prova a usare un plug-in scritto per il runtime di 2,1.

## <a name="capabilities-caching"></a>Caching delle funzionalità

La verifica della sicurezza e la creazione di istanze dei plug-in sono costose. L'operazione di download si verifica in modo più frequente rispetto all'operazione di autenticazione, ma è probabile che l'utente NuGet medio disponga solo di un plug-in di autenticazione.
Per migliorare l'esperienza, NuGet memorizza nella cache le attestazioni dell'operazione per la richiesta specificata. Questa cache è per plug-in con la chiave del plug-in che è il percorso del plug-in e la scadenza della cache delle funzionalità è di 30 giorni. 

La cache si trova in `%LocalAppData%/NuGet/plugins-cache` ed è stata sottoposta a override con la variabile di ambiente `NUGET_PLUGINS_CACHE_PATH`. Per cancellare la [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), è possibile eseguire il comando locals con l'opzione `plugins-cache`.
L'opzione variabili locali `all` eliminerà anche la cache dei plug-in. 

## <a name="protocol-messages-index"></a>Indice dei messaggi di protocollo

Messaggi versione protocollo *1.0.0* :

1.  Chiudi
    * Direzione della richiesta: plug-in NuGet->
    * La richiesta non conterrà alcun payload
    * Non è prevista alcuna risposta.  La risposta corretta è che il processo del plug-in viene immediatamente terminato.

2.  Copia i file nel pacchetto
    * Direzione della richiesta: plug-in NuGet->
    * La richiesta conterrà:
        * ID e versione del pacchetto
        * percorso del repository di origine del pacchetto
        * percorso directory di destinazione
        * oggetto enumerabile di file nel pacchetto da copiare nel percorso della directory di destinazione
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.
        * oggetto enumerabile di percorsi completi per i file copiati nella directory di destinazione se l'operazione è riuscita

3.  Copiare il file del pacchetto (. nupkg)
    * Direzione della richiesta: plug-in NuGet->
    * La richiesta conterrà:
        * ID e versione del pacchetto
        * percorso del repository di origine del pacchetto
        * percorso del file di destinazione
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.

4.  Ottenere le credenziali
    * Direzione della richiesta: plugin-> NuGet
    * La richiesta conterrà:
        * percorso del repository di origine del pacchetto
        * codice di stato HTTP ottenuto dal repository di origine del pacchetto con le credenziali correnti
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.
        * un nome utente, se disponibile
        * una password, se disponibile

5.  Ottenere i file nel pacchetto
    * Direzione della richiesta: plug-in NuGet->
    * La richiesta conterrà:
        * ID e versione del pacchetto
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.
        * oggetto enumerabile di percorsi di file nel pacchetto se l'operazione è riuscita

6.  Ottenere le attestazioni dell'operazione 
    * Direzione della richiesta: plug-in NuGet->
    * La richiesta conterrà:
        * il servizio index. JSON per un'origine del pacchetto
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.
        * oggetto enumerabile di operazioni supportate (ad esempio, download del pacchetto) se l'operazione ha avuto esito positivo.  Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.

> [!Note]
> Questo messaggio è stato aggiornato nella versione *2.0.0*. Il client mantiene la compatibilità con le versioni precedenti.

7.  Ottieni hash pacchetto
    * Direzione della richiesta: plug-in NuGet->
    * La richiesta conterrà:
        * ID e versione del pacchetto
        * percorso del repository di origine del pacchetto
        * algoritmo hash
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.
        * hash del file del pacchetto che utilizza l'algoritmo hash richiesto se l'operazione è riuscita

8.  Ottenere le versioni del pacchetto
    * Direzione della richiesta: plug-in NuGet->
    * La richiesta conterrà:
        * ID del pacchetto
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.
        * oggetto enumerabile di versioni del pacchetto se l'operazione è riuscita

9.  Ottenere l'indice del servizio
    * Direzione della richiesta: plugin-> NuGet
    * La richiesta conterrà:
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.
        * Indice del servizio se l'operazione è stata completata correttamente

10.  Handshake
     * Direzione della richiesta: < NuGet-> plug-in
     * La richiesta conterrà:
         * versione corrente del protocollo plugin
         * versione minima supportata del protocollo plug-in
     * Una risposta conterrà:
         * codice di risposta che indica il risultato dell'operazione.
         * versione del protocollo negoziata se l'operazione ha avuto esito positivo.  Un errore provocherà la terminazione del plug-in.

11.  Initialize
     * Direzione della richiesta: plug-in NuGet->
     * La richiesta conterrà:
         * versione dello strumento client NuGet
         * linguaggio efficace dello strumento client NuGet.  Ciò prende in considerazione l'impostazione ForceEnglishOutput, se usata.
         * timeout della richiesta predefinito, che sostituisce l'impostazione predefinita del protocollo.
     * Una risposta conterrà:
         * codice di risposta che indica il risultato dell'operazione.  Un errore provocherà la terminazione del plug-in.

12.  Registro
     * Direzione della richiesta: plugin-> NuGet
     * La richiesta conterrà:
         * livello di registrazione per la richiesta
         * messaggio da registrare
     * Una risposta conterrà:
         * codice di risposta che indica il risultato dell'operazione.

13.  Esegui monitoraggio uscita processo NuGet
     * Direzione della richiesta: plug-in NuGet->
     * La richiesta conterrà:
         * ID processo NuGet
     * Una risposta conterrà:
         * codice di risposta che indica il risultato dell'operazione.

14.  Prelettura del pacchetto
     * Direzione della richiesta: plug-in NuGet->
     * La richiesta conterrà:
         * ID e versione del pacchetto
         * percorso del repository di origine del pacchetto
     * Una risposta conterrà:
         * codice di risposta che indica il risultato dell'operazione.

15.  Imposta credenziali
     * Direzione della richiesta: plug-in NuGet->
     * La richiesta conterrà:
         * percorso del repository di origine del pacchetto
         * ultimo nome utente di origine del pacchetto noto, se disponibile
         * ultima password di origine del pacchetto nota, se disponibile
         * ultimo nome utente del proxy noto, se disponibile
         * ultima password del proxy nota, se disponibile
     * Una risposta conterrà:
         * codice di risposta che indica il risultato dell'operazione.

16.  Impostare il livello di registrazione
     * Direzione della richiesta: plug-in NuGet->
     * La richiesta conterrà:
         * livello di registrazione predefinito
     * Una risposta conterrà:
         * codice di risposta che indica il risultato dell'operazione.

Messaggi della versione *2.0.0* del protocollo

17. Ottenere le attestazioni dell'operazione

* Direzione della richiesta: plug-in NuGet->
    * La richiesta conterrà:
        * il servizio index. JSON per un'origine del pacchetto
        * percorso del repository di origine del pacchetto
    * Una risposta conterrà:
        * codice di risposta che indica il risultato dell'operazione.
        * oggetto enumerabile di operazioni supportate se l'operazione ha avuto esito positivo.  Se un plug-in non supporta l'origine del pacchetto, il plug-in deve restituire un set vuoto di operazioni supportate.

    Se l'indice del servizio e l'origine del pacchetto sono null, il plug-in può rispondere con l'autenticazione.

18. Ottenere le credenziali di autenticazione

* Direzione della richiesta: plug-in NuGet->
* La richiesta conterrà:
    * URI
    * numero di tentativi
    * Non interattiva
    * CanShowDialog
* Una risposta conterrà
    * Nome utente
    * Windows 10
    * Messaggio
    * Elenco di tipi di autenticazione
    * MessageResponseCode
