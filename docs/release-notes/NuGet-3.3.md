---
title: Note sulla versione 3.3 di NuGet
description: Note sulla versione per NuGet 3.3, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546647"
---
# <a name="nuget-33-release-notes"></a>Note sulla versione 3.3 di NuGet

[Note sulla versione di NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC note](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 è stata rilasciata il 30 novembre 2015 con un numero significativo degli aggiornamenti dell'interfaccia utente e le funzionalità della riga di comando, nonché una raccolta di correzioni utile per i client NuGet.

## <a name="new-features"></a>Nuove funzionalità

* Sono stati introdotti i provider di credenziali che consentono ai client della riga di comando di NuGet essere in grado di integrarsi facilmente con un feed autenticato. [Provider di credenziali di istruzioni su come installare Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) e configurare NuGet ai client di usare, sono disponibili in NuGet Docs.

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Schede separate di esplorazione, installato e gli aggiornamenti disponibili
* Badge disponibili gli aggiornamenti che indica il numero di pacchetti con aggiornamenti disponibili
* Notifiche pacchetto nell'elenco di pacchetti per indicare se il pacchetto viene installato o è disponibile un aggiornamento
* Download di conteggio e autore aggiunto all'elenco dei pacchetti
* Numero di versione disponibile più alto e il numero di versione attualmente installata nell'elenco di pacchetti
* Pulsanti di azione per consentire l'installazione rapida, aggiornare e disinstallare dall'elenco dei pacchetti
* Pulsanti di azione più chiari nel pannello dei dettagli del pacchetto
* Data di aggiornamento del pacchetto nel pannello dei dettagli del pacchetto
* Consolidare pannello nella visualizzazione della soluzione
* Griglia ordinabile di progetti e i numeri di versione installata nella visualizzazione della soluzione

## <a name="new-command-line-features"></a>Nuove funzionalità della riga di comando

In questa versione è stato introdotto il `add` e `init` comandi per inizializzare i repository basati su cartelle come descritto nel [nuget.exe riferimento](../tools/nuget-exe-cli-reference.md). Struttura di repository in cui vengono costruiti e gestiti in questa cartella verrà [offrire vantaggi significativi delle prestazioni](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) come descritto nel blog.

## <a name="contentfiles"></a>contentFiles

È ora supportato contenuto nel `project.json` progetti tramite il nuovo gestiti `contentFiles` cartella e `.nuspec` `contentFiles` notazione elemento.  Questo contenuto può essere specificato in modo più diretto dall'autore del pacchetto per le interazioni con i sistemi di progetto.  Altre informazioni su come configurare contentFiles in una `.nuspec` documento è reperibile nella [riferimento file con estensione nuspec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Variabili locali NuGet memorizza nella Cache di gestione

Il riga di comando di NuGet è stato aggiornato per includere informazioni su come gestire le cache in una workstation locale.  Altre informazioni sul comando variabili locali sono disponibile nel [riferimento della riga di comando di NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Risoluzione dei problemi

**Errori rilevanti**

* Supporto ripristinato da riga di comando di NuGet per il ripristino dei pacchetti con un file di soluzione su Mono - [1543](https://github.com/NuGet/Home/issues/1543)

L'elenco completo dei problemi che sono stati risolti nella versione 3.3 è reperibile in GitHub con il [3.3 attività cardine](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

L'elenco dei problemi risolti nella versione di riga di comando 3.3 vengono registrati nella [3.3 attività cardine della riga di comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)