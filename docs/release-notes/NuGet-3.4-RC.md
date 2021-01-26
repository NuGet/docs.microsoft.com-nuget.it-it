---
title: Note sulla versione di NuGet 3,4-RC
description: Note sulla versione per NuGet 3,4 RC, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780236"
---
# <a name="nuget-34-rc-release-notes"></a>Note sulla versione di NuGet 3,4-RC

Note sulla versione di [NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Note sulla versione di NuGet 3,4](../release-notes/nuget-3.4.md)

NuGet 3,4-RC è stato rilasciato il 3 marzo 2016 insieme a Visual Studio 2015 Update 2 RC ed è stato creato con alcuni principi in mente:

* Supporto multipiattaforma
* Miglioramenti delle prestazioni
* Miglioramenti dell'interfaccia utente secondaria

Le funzionalità seguenti sono disponibili in questa versione RC, con più pianificate per la versione finale 3,4.

## <a name="new-features"></a>Nuove funzioni e caratteristiche

* I client NuGet supportano ora la codifica di contenuto gzip dai repository
* Supporto per PDB dai pacchetti nei progetti xproj
* Supporto per le azioni di compilazione iOS e Android nell'elemento contentFiles
* Supporto per i moniker del Framework netstandard e netstandardapp

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Miglioramenti significativi delle prestazioni in particolare sulle schede installate, aggiornate e consolidate
* Le schede installato e aggiornamenti sono ora ordinate in ordine alfabetico
* È stato aggiunto un pulsante di aggiornamento che consente di aggiornare una ricerca

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* I pacchetti a cui viene fatto riferimento in `project.json` che hanno una versione mobile non vengono aggiornati in ogni compilazione. Verranno invece aggiornati solo quando è necessario eseguire il ripristino, la pulizia, la ricompilazione o la modifica `project.json` .
* le origini del repository nuget.org non sono più forzate in una configurazione di progetto quando si usa l'interfaccia utente di configurazione di NuGet.
* NuGet non ripristina più i pacchetti nei progetti condivisi né scrive un file di blocco.
* Si è verificato un errore di rete migliorato ed è stato effettuato un nuovo tentativo di gestione per server non raggiungibili o lenti a risposta.
* I comportamenti della tastiera e del mouse sono stati migliorati nell'interfaccia utente di gestione pacchetti di Visual Studio.
* È ora supportato lo schema più recente `project.json` in DNX.

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)