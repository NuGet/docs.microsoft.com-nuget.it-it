---
title: Note sulla versione di NuGet 3.3 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Note sulla versione per NuGet 3.3 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
keywords: 3.3 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ab5e1ca550297c608017cb56dff32f4bd4bbb885
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-33-release-notes"></a>Note sulla versione 3.3 di NuGet

[Note sulla versione di NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC note](../release-notes/nuget-3.4-RC.md)

3.3 NuGet è stato rilasciato il 30 novembre 2015 con un numero significativo di aggiornamenti dell'interfaccia utente e le funzionalità della riga di comando, nonché una raccolta di correzioni utile ai client NuGet.

## <a name="new-features"></a>Nuove funzionalità

* Sono stati introdotti i provider di credenziali che consentono ai client della riga di comando di NuGet essere in grado di utilizzare facilmente un feed autenticato. [Provider di credenziali di istruzioni su come installare Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) e configurare NuGet ai client di utilizzare, sono disponibili in NuGet Docs.

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Schede separate di esplorazione, installato e gli aggiornamenti disponibili
* Gli aggiornamenti disponibile badge che indica il numero di pacchetti con aggiornamenti disponibili
* Badge pacchetto nell'elenco del pacchetto per indicare se il pacchetto è installato o è disponibile un aggiornamento
* Scaricare conteggio e l'autore aggiunto all'elenco di pacchetti
* Numero massimo di versione disponibili e il numero di versione attualmente installata di elenco di pacchetti
* Pulsanti di azione per consentire l'installazione rapida, aggiornare e disinstallare dall'elenco di pacchetti
* Più chiari pulsanti di azione nel riquadro dettagli di pacchetto
* Data di aggiornamento del pacchetto nel riquadro dettagli di pacchetto
* Consolidare pannello nella visualizzazione soluzione
* Griglia ordinabile dei progetti e dei numeri di versione nella visualizzazione soluzione

## <a name="new-command-line-features"></a>Nuove funzionalità della riga di comando

In questa versione è stata introdotta la `add` e `init` comandi inizializzare repository basati su cartelle come descritto nel [nuget.exe riferimento](../tools/nuget-exe-cli-reference.md). Struttura di repository che vengono costruiti e mantenuti con questa cartella verrà [offrire vantaggi significativi delle prestazioni](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) come descritto nel blog.

## <a name="contentfiles"></a>ContentFiles

Il contenuto è ora supportato in `project.json` gestiti progetti tramite il nuovo `contentFiles` cartella e `.nuspec` `contentFiles` notazione di elemento.  Questo contenuto può essere specificato in modo più diretto dall'autore del pacchetto per le interazioni con i sistemi di progetto.  Ulteriori informazioni su come configurare contentFiles in un `.nuspec` documento, vedere il [. nuspec riferimento](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Variabili locali NuGet memorizzare nella Cache di gestione

NuGet da riga di comando è stato aggiornato per includere informazioni su come gestire la cache locale in una workstation.  Ulteriori informazioni sul comando variabili locali sono disponibile nel [NuGet da riga di comando](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Risoluzione dei problemi

**Problemi rilevanti**

* NuGet da riga di comando ripristinato il supporto per il ripristino dei pacchetti con un file di soluzione in Mono - [1543](https://github.com/NuGet/Home/issues/1543)

L'elenco completo dei problemi che sono stati risolti nella versione 3.3 sono reperibili in GitHub sotto il [attività cardine 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

L'elenco di problemi risolti nella versione della riga di comando 3.3 vengono registrati nella [3.3 attività cardine della riga di comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nella lista di problemi di GitHub che può essere trovato in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)