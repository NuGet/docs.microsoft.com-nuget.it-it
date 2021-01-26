---
title: Note sulla versione di NuGet 3,3
description: Note sulla versione per NuGet 3,3, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776504"
---
# <a name="nuget-33-release-notes"></a>Note sulla versione di NuGet 3,3

Note sulla versione di [NuGet 3.2.1](../release-notes/nuget-3.2.1.md)  |  [Note sulla versione di NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)

NuGet 3,3 è stato rilasciato il 30 novembre 2015 con un numero significativo di aggiornamenti dell'interfaccia utente e funzionalità della riga di comando, oltre a una raccolta di utili correzioni per i client NuGet.

## <a name="new-features"></a>Nuove funzioni e caratteristiche

* Sono stati introdotti i provider di credenziali che consentono ai client della riga di comando NuGet di funzionare senza interruzioni con un feed autenticato. Le [istruzioni su come installare il provider di credenziali Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) e configurare i client NuGet per usarlo sono disponibili nella documentazione di NuGet.

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Schede di esplorazione, installazione e aggiornamento separate
* Aggiorna il badge disponibile che indica il numero di pacchetti con aggiornamenti disponibili
* Notifiche del pacchetto nell'elenco dei pacchetti per indicare se il pacchetto è installato o se è disponibile un aggiornamento
* Numero di download e autore aggiunti all'elenco dei pacchetti
* Numero di versione più elevato e numero di versione attualmente installato nell'elenco dei pacchetti
* Pulsanti di azione per consentire l'installazione rapida, l'aggiornamento e la disinstallazione dall'elenco dei pacchetti
* Pulsanti di azione più chiari nel pannello dei dettagli del pacchetto
* Data di aggiornamento del pacchetto nel pannello dei dettagli del pacchetto
* Consolidare il pannello nella visualizzazione soluzione
* Griglia ordinabile di progetti e numeri di versione installati nella visualizzazione soluzione

## <a name="new-command-line-features"></a>Nuove funzionalità della riga di comando

In questa versione sono stati introdotti i `add` `init` comandi e per inizializzare i repository basati su cartelle come descritto nel [ riferimentonuget.exe](../reference/nuget-exe-cli-reference.md). I repository costruiti e gestiti con questa struttura di cartelle offriranno [vantaggi significativi](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) in materia di prestazioni, come descritto nel Blog.

## <a name="contentfiles"></a>ContentFiles

Il contenuto è ora supportato nei `project.json` progetti gestiti tramite la nuova `contentFiles` notazione di elementi e cartelle `.nuspec` `contentFiles` .  Questo contenuto può essere specificato più direttamente dall'autore del pacchetto per le interazioni con i sistemi di progetto.  Altre informazioni su come configurare contentFiles in un `.nuspec` documento sono disponibili nel [riferimento. NuSpec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Gestione cache NuGet locale

La riga di comando di NuGet è stata aggiornata per includere informazioni su come gestire le cache locali in una workstation.  Altre informazioni sul comando variabili locali sono disponibili nella Guida di [riferimento alla riga di comando di NuGet](../reference/cli-reference/cli-ref-locals.md).

## <a name="fixed-issues"></a>Problemi risolti

**Problemi rilevanti**

* Supporto della riga di comando di NuGet ripristinato per il ripristino di pacchetti con un file di soluzione in mono- [1543](https://github.com/NuGet/Home/issues/1543)

L'elenco completo dei problemi risolti nella versione 3,3 è disponibile in GitHub nell' [attività cardine 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

L'elenco dei problemi risolti nella versione della riga di comando 3,3 viene registrato nell' [attività cardine di 3,3 Command-Line](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)