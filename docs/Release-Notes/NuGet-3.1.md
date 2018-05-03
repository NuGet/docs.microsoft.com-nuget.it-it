---
title: Note sulla versione 3.1 di NuGet
description: Note sulla versione per NuGet 3.1 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-31-release-notes"></a>Note sulla versione 3.1 di NuGet

[Note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md) | [note sulla versione di NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3.1 è stata rilasciata 27 luglio 2015 come estensione in dotazione di Universal Windows Platform SDK per Visual Studio 2015. Questa versione con il SDK della piattaforma Windows messo a disposizione in modo che l'esperienza di sviluppo di Windows può sfruttare il lavoro multipiattaforma NuGet che era stato avviato in precedenza. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

È consigliabile gli sviluppatori che dispongono dell'accesso per l'aggiornamento della raccolta di Visual Studio per la versione più recente è disponibile, come sempre attualmente vengono pubblicati gli aggiornamenti con le nuove funzionalità e correzioni di bug.

## <a name="nuget-visual-studio-extension"></a>Estensione di NuGet di Visual Studio

Problemi e le funzionalità in questa versione sono contrassegnate su GitHub con il [attività cardine "3.1 del supporto transitiva UWP RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) In totale, è stato chiuso 67 problemi nella versione 3.1.

### <a name="new-features"></a>Nuove funzionalità

* `project.json` supporto per il supporto della piattaforma UWP Windows e ASP.NET 5
* Installazione del pacchetto transitiva

Descrizione e la definizione di queste funzionalità sono disponibili in un' posizione nella documentazione.

### <a name="deprecated"></a>Deprecato

Le funzionalità seguenti non sono più disponibili per Visual Studio 2015:

* Pacchetti a livello di soluzione non possono più essere installati

Le funzionalità seguenti non sono più disponibili per Visual Studio 2015 e i progetti che usano il `project.json` specifica

* `install.ps1` e `uninstall.ps1` -questi script verranno ignorati durante l'installazione del pacchetto, ripristinare, aggiornare e disinstallare
* Trasformazioni di configurazione verranno ignorate
* Il contenuto verrà eseguito, ma non è stato copiato in un progetto.
    * Il team sta lavorando per implementare nuovamente questa funzionalità, seguire la discussione e sullo stato di avanzamento in: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemi noti

Si sono verificati alcuni problemi noti forniti con questa versione.

* Installazione della versione 3.1 con Windows 10 SDK verrà effettuato il downgrade di qualsiasi versione di estensione NuGet che era stato precedentemente installato

## <a name="nuget-command-line"></a>NuGet da riga di comando

Il file eseguibile da riga di comando di NuGet è stato aggiornato e viene spostato in una nuova posizione distribuibile in modo da versioni precedenti di nuget.exe possono continuare a essere rese disponibili.  È possibile scaricare la versione 3.1 beta di nuget.exe per Windows, visitare: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Il nuovo percorso distribuibile risiede nell'host dist.nuget.org, con una struttura di cartelle che segue questo modello:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Nuove funzionalità

* NuGet.exe è possibile ripristinare e installare i pacchetti in progetti che utilizzano un `project.json` file.
* NuGet.exe possono connettersi e utilizzare il protocollo di NuGet v3 a: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemi noti ##

1.    Non è possibile eseguire pack rispetto a un `project.json` file - [928](https://github.com/NuGet/Home/issues/928)
2.    Non è supportato in Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Non è localizzato - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Non è firmato, esattamente come esistenti http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)
