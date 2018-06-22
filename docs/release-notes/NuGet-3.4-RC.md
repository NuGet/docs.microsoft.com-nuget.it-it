---
title: Note sulla versione 3.4 RC NuGet
description: Note sulla versione per NuGet 3.4 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820820"
---
# <a name="nuget-34-rc-release-notes"></a>Note sulla versione 3.4 RC NuGet

[Note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md) | [note sulla versione di NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC è stato rilasciato il 3 marzo 2016 insieme a Visual Studio 2015 Update 2 RC ed è stata compilata con alcuni principi in mente:

* Supporto multipiattaforma
* Miglioramenti delle prestazioni
* Piccoli miglioramenti dell'interfaccia utente

Le funzionalità seguenti sono disponibili in questa RC, con più pianificato per la versione finale 3.4.

## <a name="new-features"></a>Nuove funzionalità

* I client NuGet ora supportano la codifica di contenuto gzip dai repository
* Supporto per PDB dai pacchetti nei progetti xproj
* Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles
* Supporto per il moniker del framework moniker netstandard e netstandardapp

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Miglioramenti significativi delle prestazioni in particolare nelle schede installato, aggiornamenti e Consolidate
* Installato e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico
* Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Pacchetti di cui viene fatto riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione. Al contrario, si aggiornerà solo quando forzato per il ripristino, pulire, ricompilare o modificare `project.json`.
* le origini dei repository NuGet.org non forzate in una configurazione di progetto quando si utilizza l'interfaccia utente di configurazione NuGet.
* NuGet non ripristina i pacchetti in progetti condivisi né scrive un file di blocco.
* Abbiamo migliorati errore di rete e ripetere la gestione di server non è raggiungibile o lento a rispondere.
* I comportamenti di tastiera e mouse vengono aggiornati nell'UI gestione pacchetto di Visual Studio.
* È ora supportano la versione più recente `project.json` schema DNX.

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nella lista di problemi di GitHub che può essere trovato in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)