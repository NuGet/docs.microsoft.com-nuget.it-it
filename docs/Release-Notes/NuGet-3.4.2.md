---
title: Note sulla versione di NuGet sezione 3.4.2 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per l'inclusione di NuGet sezione 3.4.2 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet sezione 3.4.2 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-342-release-notes"></a>Note sulla versione di sezione 3.4.2 NuGet

[Note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet versione 3.4.3 note](../release-notes/nuget-3.4.3.md)

È stata rilasciata NuGet sezione 3.4.2 8 aprile 2016 a risolvere alcuni problemi che sono stati identificati i 3.4 e 3.4.1 rilasciare.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe sezione 3.4.2 RC è ora disponibile

È possibile scaricare la versione finale candidata di nuget.exe sezione 3.4.2 [qui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Sono stati migliorati in modo significativo le prestazioni degli aggiornamenti in uno scenario specifico, in cui gli aggiornamenti per i pacchetti con grafici delle dipendenze completa richiede molto tempo e blocco di Visual Studio.
* il ripristino NuGet senza il traffico di rete è 2.5 x – 3 più veloce in Visual Studio.
* Oltre a questa modifica, è stato risolto un problema in cui si stava raggiunge la rete due volte quando l'aggiornamento di recupero contare nell'interfaccia utente di Visual Studio. Questo è stato parzialmente responsabile di alcuni clienti di problemi di timeout nella 3.4/3.4.1.
* Aggiunta del supporto per l'impostazione no_proxy

## <a name="fixes"></a>Correzioni

* Risolto un problema in nuget.org origine era mancante nella configurazione o impostazioni NuGet dopo l'aggiornamento a 3.4.1.
* Risolto un problema in cui una modifica di maiuscole e minuscole a FindPackagesById in 3.4.1 interruzioni Artifactory.
* Correggere un problema con FIPS che ha generato errori con il ripristino NuGet con nuget.exe.
* Correzione di un arresto anomalo durante l'esplorazione delle origini con l'URL dell'icona non valido.
* Risoluzione dei problemi con l'unione delle versioni e le voci da 'Tutte le origini'.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemi noti nella sezione 3.4.2 riga di comando di Windows x86 (RC)

Questi problemi verranno risolti prima settimana successiva prima viene raggiunto RTM.

*  Ripristino nuget in esecuzione su una soluzione avrà esito negativo se il file della soluzione viene inserito in una gerarchia di cartelle inferiore rispetto ai file di progetto.
*  Eseguire il comando di eliminazione nuget in un pacchetto utilizzando il feed V2 avrà esito negativo. In alternativa, usare feed V3.


Per l'elenco completo delle correzioni e miglioramenti in questa versione, consultare l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).