---
title: Note sulla versione di NuGet 3,1
description: Note sulla versione per NuGet 3,1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776531"
---
# <a name="nuget-31-release-notes"></a>Note sulla versione di NuGet 3,1

Note sulla versione di [NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Note sulla versione di NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3,1 è stato rilasciato il 27 luglio 2015 come estensione in bundle per piattaforma UWP (Universal Windows Platform) SDK per Visual Studio 2015. Questa versione è stata distribuita con Windows Platform SDK, in modo che l'esperienza di sviluppo di Windows potesse sfruttare i vantaggi del lavoro multipiattaforma NuGet precedentemente avviato. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

Si consiglia agli sviluppatori che hanno accesso a Visual Studio Gallery di eseguire l'aggiornamento alla versione più recente disponibile, perché vengono sempre pubblicati aggiornamenti con correzioni di bug e nuove funzionalità.

## <a name="nuget-visual-studio-extension"></a>Estensione NuGet di Visual Studio

I problemi e le funzionalità di questa versione sono contrassegnati in GitHub con l' [attività cardine "3,1 RTM UWP supporto transitivo"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  in totale, sono stati chiusi 67 problemi nella versione 3,1.

### <a name="new-features"></a>Nuove funzioni e caratteristiche

* `project.json` supporto per il supporto per Windows UWP e ASP.NET 5
* Installazione di pacchetti transitivi

La descrizione e la definizione di queste funzionalità sono disponibili altrove nella documentazione.

### <a name="deprecated"></a>Deprecato

Le funzionalità seguenti non sono più disponibili per Visual Studio 2015:

* Non è più possibile installare i pacchetti a livello di soluzione

Le funzionalità seguenti non sono più disponibili per Visual Studio 2015 e i progetti che usano la `project.json` specifica

* `install.ps1` e `uninstall.ps1` -questi script verranno ignorati durante l'installazione, il ripristino, l'aggiornamento e la disinstallazione del pacchetto
* Le trasformazioni di configurazione verranno ignorate
* Il contenuto verrà mantenuto, ma non copiato in un progetto.
    * Il team sta lavorando per riimplementare questa funzionalità, seguire la discussione e lo stato di avanzamento in: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemi noti

In questa versione sono stati introdotti numerosi problemi noti.

* L'installazione della versione 3,1 con Windows 10 SDK effettuerà il downgrade di qualsiasi versione dell'estensione NuGet installata in precedenza

## <a name="nuget-command-line"></a>Riga di comando NuGet

Il file eseguibile della riga di comando NuGet è stato aggiornato e spostato in un nuovo percorso distribuibile in modo che le versioni cronologiche di nuget.exe possano continuare a essere rese disponibili.  È possibile scaricare la versione beta 3,1 di nuget.exe per Windows in: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Il nuovo percorso distribuibile si trova nell'host dist.nuget.org, con una struttura di cartelle che segue questo modello:

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Nuove funzioni e caratteristiche

* nuget.exe possibile ripristinare e installare i pacchetti in progetti che utilizzano un `project.json` file.
* nuget.exe possibile connettersi e utilizzare il protocollo NuGet V3 in: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemi noti ##

1.    Impossibile eseguire il pacchetto in un `project.json` file- [928](https://github.com/NuGet/Home/issues/928)
2.    Non è supportato in mono- [1059](https://github.com/NuGet/Home/issues/1059)
3.    Non è localizzato- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    Non è firmato, proprio come il http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073) esistente
