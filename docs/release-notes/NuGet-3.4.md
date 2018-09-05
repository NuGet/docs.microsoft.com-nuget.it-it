---
title: Note sulla versione 3.4 di NuGet
description: Note sulla versione per NuGet 3.4, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551191"
---
# <a name="nuget-34-release-notes"></a>Note sulla versione 3.4 di NuGet

[Note sulla versione 3.4-RC di NuGet](../release-notes/nuget-3.4-RC.md) | [note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 è stata rilasciata il 30 marzo 2016 come parte di Visual Studio 2015 Update 2 e Visual Studio 15 Preview versione e sia stato generato con alcuni principi in mente:

* Supporto multipiattaforma
* Miglioramenti delle prestazioni
* Miglioramenti dell'interfaccia utente secondari

Le funzionalità seguenti sono state aggiunte in precedenza in RC e sono state aggiornate o completate per la versione 3.4:

## <a name="new-features"></a>Nuove funzionalità

* I client NuGet supportano ora codifica di contenuto gzip dai repository
* Supporto per i file PDB dai pacchetti nei progetti xproj
* Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles
* Supporto per i moniker netstandard e netstandardapp di framework

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Miglioramenti significativi delle prestazioni in particolare nelle schede installato, gli aggiornamenti e consolida
* Aggregazione 'Tutte le origini pacchetto' origine è disponibile con l'unione dei risultati ricerca appropriato
* Installazione e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico
* Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare
* Opzioni di compilazione più recente nella parte superiore dell'elenco versione

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* I pacchetti a cui fa riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione. Al contrario, si aggiornerà solo quando era necessario ripristinare, pulire, ricompilare o modificare `project.json`.
* origini di repository NuGet.org non sono forzate non è più in una configurazione di progetto quando si usa l'interfaccia utente di configurazione NuGet.
* Non è più NuGet Ripristina i pacchetti in progetti condivisi né scrive un file di blocco.
* È stata migliorata l'errore di rete e ripetere la gestione per il server non è raggiungibile o rallentare di risposta.
* I comportamenti di tastiera e mouse sono stati migliorati nella UI di gestione pacchetti Visual Studio.
* Supportiamo ora la versione più recente `project.json` dello schema in DNX.

## <a name="breaking-changes"></a>Modifiche di interruzione

* I numeri di versione del pacchetto vengono normalizzati ora nel formato *principali*. *minori*. *patch*-*prerelease* ognuno dei componenti principale, secondaria e applicare patch vengono considerati come numeri interi e rilasciare gli eventuali zeri iniziali.  Le informazioni di versione non definitive viene considerate come una stringa e non vengono applicate modifiche ad esso. Questi numeri vengono usati nelle query per i client NuGet e la ricerca forniti dal servizio di nuget.org.  Altre informazioni sono reperibili nella documentazione di NuGet sotto [Prerelease versioni](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problemi noti

* **Problema:** agli utenti di Windows 10 v1511 potrebbero verificarsi problemi o anche un blocco di Visual Studio con Powershell in Visual Studio negli scenari seguenti:
    * Installazione / disinstallazione dei pacchetti che hanno install.ps1 / script uninstall.ps1
    * Il caricamento di progetti con uno script init.ps1 script (ad esempio Entity Framework)
    * Pubblicazione di contenuto web

* **Soluzione alternativa:** assicurarsi che l'installazione di Windows 10 con le patch più recenti applicate, expecially gennaio 2016 (KB 3124263) o un aggiornamento successivo.  Altri dettagli sono disponibili su [problema #1638 su GitHub](http://github.com/nuget/home/issues/1638)

* **Problema:** i reindirizzamenti del protocollo NuGet versione 2 sono interrotti.
I repository NuGet personalizzati che reindirizzano le richieste a un host alternativo non soddisfano la richiesta di reindirizzamento.
* **Soluzione alternativa:** per risolvere questo problema, configurare l'URI del repository di pacchetti in modo che punti al percorso del server reindirizzato.
Per altre informazioni, vedere [richiesta pull di GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)