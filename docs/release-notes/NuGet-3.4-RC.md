---
title: Note sulla versione 3.4-RC di NuGet
description: Note sulla versione per NuGet 3.4 RC, tra cui i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546754"
---
# <a name="nuget-34-rc-release-notes"></a>Note sulla versione 3.4-RC di NuGet

[Note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md) | [note sulla versione di NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC è stato rilasciato il 3 marzo 2016 insieme a Visual Studio 2015 Update 2 RC e sia stato generato con alcuni principi in mente:

* Supporto multipiattaforma
* Miglioramenti delle prestazioni
* Miglioramenti dell'interfaccia utente secondari

Le funzionalità seguenti sono disponibili in RC, con più previsto per la versione finale 3.4.

## <a name="new-features"></a>Nuove funzionalità

* I client NuGet supportano ora codifica di contenuto gzip dai repository
* Supporto per i file PDB dai pacchetti nei progetti xproj
* Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles
* Supporto per i moniker netstandard e netstandardapp di framework

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Miglioramenti significativi delle prestazioni in particolare nelle schede installato, gli aggiornamenti e consolida
* Installazione e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico
* Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* I pacchetti a cui fa riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione. Al contrario, si aggiornerà solo quando era necessario ripristinare, pulire, ricompilare o modificare `project.json`.
* origini di repository NuGet.org non sono forzate non è più in una configurazione di progetto quando si usa l'interfaccia utente di configurazione NuGet.
* Non è più NuGet Ripristina i pacchetti in progetti condivisi né scrive un file di blocco.
* È stata migliorata l'errore di rete e ripetere la gestione per il server non è raggiungibile o rallentare di risposta.
* I comportamenti di tastiera e mouse sono stati migliorati nella UI di gestione pacchetti Visual Studio.
* Supportiamo ora la versione più recente `project.json` dello schema in DNX.

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)