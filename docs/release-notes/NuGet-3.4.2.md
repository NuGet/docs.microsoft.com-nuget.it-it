---
title: Note sulla versione di NuGet 3.4.2
description: Note sulla versione per NuGet 3.4.2 inclusi noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549151"
---
# <a name="nuget-342-release-notes"></a>Note sulla versione di NuGet 3.4.2

[Note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [note sulla versione di NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 è stato rilasciato l'8 aprile 2016 a risolvere alcuni problemi che sono stati identificati durante la 3.4 e 3.4.1 di rilascio.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC è ora disponibile

È possibile scaricare la versione finale candidata di nuget.exe 3.4.2 [qui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* È stato migliorato in modo significativo le prestazioni degli aggiornamenti in uno scenario specifico, in cui gli aggiornamenti per i pacchetti con grafici di dipendenza completa richiede molto tempo e all'avvio di Visual Studio.
* ripristino di NuGet senza il traffico di rete è 2,5 x-3 volte più veloce all'interno di Visual Studio.
* Oltre a questa modifica, è stato risolto un problema in cui abbiamo stavamo raggiungere la rete due volte quando il numero di recupero dell'aggiornamento nell'interfaccia utente di Visual Studio. Questo è stato parzialmente responsabile per alcuni clienti di problemi di timeout esperti in 3.4/3.4.1.
* Aggiunta del supporto per l'impostazione no_proxy

## <a name="fixes"></a>Correzioni

* Risolto un problema in cui origine di nuget.org non presente nella configurazione o impostazioni NuGet dopo l'aggiornamento a 3.4.1.
* Risolto un problema in cui una modifica di maiuscole e minuscole a FindPackagesById in 3.4.1 interrompe Artifactory.
* Risolto un problema con FIPS che generava errori di ripristino di NuGet con nuget.exe.
* Corretto un arresto anomalo durante l'esplorazione delle origini con l'URL dell'icona non valido.
* Risoluzione dei problemi con l'unione delle versioni e le voci da 'Tutte le origini'.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemi noti nella sezione 3.4.2 Windows x86 della riga di comando (RC)

Questi problemi verranno risolti anticipata prossima settimana prima sono stati raggiunti RTM.

*  Ripristino di nuget in esecuzione su una soluzione avrà esito negativo se il file della soluzione viene inserito in una gerarchia di cartelle inferiore rispetto ai file di progetto.
*  Esegue il comando di eliminazione di nuget in un pacchetto con il feed V2 avrà esito negativo. Usare feed di V3.


Per l'elenco completo delle correzioni e miglioramenti in questa versione, consultare l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).