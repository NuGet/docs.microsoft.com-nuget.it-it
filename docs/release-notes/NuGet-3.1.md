---
title: Note sulla versione 3.1 di NuGet
description: Note sulla versione per NuGet 3.1, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545347"
---
# <a name="nuget-31-release-notes"></a>Note sulla versione 3.1 di NuGet

[Note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md) | [note sulla versione di NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3.1 è stato rilasciato il 27 luglio 2015 come estensione in dotazione di Universal Windows Platform SDK per Visual Studio 2015. Questa versione con il SDK della piattaforma Windows è stato recapitato in modo che l'esperienza di sviluppo di Windows è stato possibile sfruttare i vantaggi delle operazioni NuGet multipiattaforma che erano stato avviato in precedenza. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

È consigliabile per gli sviluppatori che dispongono dell'accesso per l'aggiornamento della raccolta di Visual Studio alla versione più recente che è disponibile, come aggiornamenti con nuove funzionalità e correzioni di bug sempre sta per essere pubblicata.

## <a name="nuget-visual-studio-extension"></a>Estensione di NuGet Visual Studio

Problemi e sulle funzionalità in questa versione sono contrassegnate su GitHub con il [attività cardine "3.1 RTM UWP transitiva supporto"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) In totale, abbiamo chiuso 67 problemi della versione 3.1.

### <a name="new-features"></a>Nuove funzionalità

* `project.json` supporto per il supporto UWP di Windows e ASP.NET 5
* Installazione del pacchetto transitiva

Descrizione e definizione di queste funzionalità sono disponibili in un' posizione nella documentazione.

### <a name="deprecated"></a>Deprecato

Le funzionalità seguenti non sono più disponibili per Visual Studio 2015:

* I pacchetti a livello di soluzione non possono più essere installati

Le funzionalità seguenti non sono più disponibili per Visual Studio 2015 e i progetti che usano il `project.json` specifica

* `install.ps1` e `uninstall.ps1` -questi script verranno ignorati durante l'installazione del pacchetto, ripristinare, aggiornare e disinstallare
* Trasformazioni di configurazione verranno ignorate
* Contenuto verrà eseguito, ma non copiato in un progetto.
    * Il team sta lavorando per implementare nuovamente questa funzionalità, segui la discussione e progresso ad: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemi noti

Si sono verificati alcuni problemi noti fornito con questa versione.

* Installazione della versione 3.1 in Windows 10 SDK verrà effettuato il downgrade di qualsiasi versione di NuGet estensione installata in precedenza

## <a name="nuget-command-line"></a>Riga di comando di NuGet

Il file eseguibile da riga di comando di NuGet è stato aggiornato e spostato in una nuova posizione distribuibile in modo che versioni cronologiche di nuget.exe possono continuare a essere rese disponibili.  È possibile scaricare la versione 3.1 beta di nuget.exe per Windows a: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

La nuova posizione distribuibile risiede nell'host dist.nuget.org, con una struttura di cartelle che segue questo modello:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Nuove funzionalità

* NuGet.exe può ripristinare e installare i pacchetti in progetti che usano un `project.json` file.
* NuGet.exe può connettersi a e utilizzare il protocollo di NuGet v3 a: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemi noti ##

1.    Impossibile eseguire il pacchetto con un `project.json` file - [928](https://github.com/NuGet/Home/issues/928)
2.    Non è supportato su Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Non è localizzato - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Non è firmato, proprio come esistenti http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
