---
title: Note sulla versione di NuGet 3.4.2
description: Note sulla versione per NuGet 3.4.2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780246"
---
# <a name="nuget-342-release-notes"></a>Note sulla versione di NuGet 3.4.2

Note sulla versione di [NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Note sulla versione di NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 è stato rilasciato l'8 aprile 2016 per risolvere diversi problemi identificati nella versione 3,4 e 3.4.1.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC è ora disponibile

È possibile scaricare la versione finale candidata di nuget.exe 3.4.2 [qui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Sono state migliorate significativamente le prestazioni degli aggiornamenti in uno scenario specifico, in cui gli aggiornamenti sui pacchetti con grafici con dipendenze approfondite hanno richiesto un tempo molto lungo e sono stati sospesi in Visual Studio.
* il ripristino di NuGet senza traffico di rete è 2,5 x-3x più velocemente in Visual Studio.
* Oltre a questa modifica, è stato risolto un problema per cui la rete veniva raggiunta due volte durante il recupero del numero di aggiornamenti nell'interfaccia utente di Visual Studio. Questo è stato parzialmente responsabile di alcuni problemi di timeout riscontrati dai clienti in 3.4/3.4.1.
* Aggiunta del supporto per l'impostazione di no_proxy

## <a name="fixes"></a>Correzioni

* È stato risolto un problema per cui l'origine nuget.org non era presente nelle impostazioni o nella configurazione di NuGet dopo l'aggiornamento alla 3.4.1.
* Correzione di un problema per cui una modifica di maiuscole e minuscole in FindPackagesById in 3.4.1 interrompe Artifactory.
* Correzione di un problema con FIPS che ha causato errori con il ripristino NuGet con nuget.exe.
* Correzione di un arresto anomalo durante l'esplorazione di origini con URL icona non valido.
* Correzione dei problemi relativi all'Unione di versioni e voci da "tutte le origini".

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemi noti in 3.4.2 Windows x86 CommandLine (RC)

Questi problemi verranno risolti prima della prossima settimana prima di raggiungere la versione RTM.

*  L'esecuzione di NuGet Restore in una soluzione avrà esito negativo se il file della soluzione viene inserito in una gerarchia di cartelle inferiore rispetto ai file di progetto.
*  L'esecuzione del comando NuGet Delete in un pacchetto con il feed V2 avrà esito negativo. In alternativa, usare il feed V3.


Per l'elenco completo delle correzioni e dei miglioramenti in questa versione, vedere l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).