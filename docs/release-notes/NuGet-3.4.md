---
title: Note sulla versione 3.4 di NuGet
description: Note sulla versione per NuGet 3.4, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820472"
---
# <a name="nuget-34-release-notes"></a>Note sulla versione 3.4 di NuGet

[NuGet 3.4 RC note](../release-notes/nuget-3.4-RC.md) | [note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 il 30 marzo 2016 è stato rilasciato come parte di Visual Studio 2015 Update 2 e Release di Visual Studio 15 Preview ed è stata compilata con alcuni principi in mente:

* Supporto multipiattaforma
* Miglioramenti delle prestazioni
* Piccoli miglioramenti dell'interfaccia utente

Le funzionalità seguenti sono aggiunti in precedenza in RC e sono state aggiornate o completate per la versione 3.4:

## <a name="new-features"></a>Nuove funzionalità

* I client NuGet ora supportano la codifica di contenuto gzip dai repository
* Supporto per PDB dai pacchetti nei progetti xproj
* Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles
* Supporto per il moniker del framework moniker netstandard e netstandardapp

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Miglioramenti significativi delle prestazioni in particolare nelle schede installato, aggiornamenti e Consolidate
* Origine di aggregazione 'Tutte le origini pacchetti' è disponibile con l'unione di risultati di ricerca corretta
* Installato e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico
* Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare
* Opzioni di compilazione più recente nella parte superiore dell'elenco versione

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Pacchetti di cui viene fatto riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione. Al contrario, si aggiornerà solo quando forzato per il ripristino, pulire, ricompilare o modificare `project.json`.
* le origini dei repository NuGet.org non forzate in una configurazione di progetto quando si utilizza l'interfaccia utente di configurazione NuGet.
* NuGet non ripristina i pacchetti in progetti condivisi né scrive un file di blocco.
* Abbiamo migliorati errore di rete e ripetere la gestione di server non è raggiungibile o lento a rispondere.
* I comportamenti di tastiera e mouse vengono aggiornati nell'UI gestione pacchetto di Visual Studio.
* È ora supportano la versione più recente `project.json` schema DNX.

## <a name="breaking-changes"></a>Modifiche di interruzione

* Numeri di versione del pacchetto vengono normalizzati ora nel formato *principali*. *secondaria*. *patch*-*provvisoria* ogni versione principale e secondaria e applicare patch vengono considerati come numeri interi ed eliminare eventuali zeri iniziali.  Le informazioni sulla versione provvisoria viene considerate come una stringa e non vengono applicate modifiche a esso. Questi numeri vengono usati nelle query per i client NuGet e la ricerca fornito dal servizio di nuget.org.  Ulteriori dettagli, vedere la documentazione di NuGet in [versione provvisoria versioni](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problemi noti

* **Problema:** gli utenti di Windows 10 v1511 potrebbero riscontrare problemi o anche un blocco di Visual Studio con Powershell in Visual Studio negli scenari seguenti:
    * L'installazione / disinstallazione di pacchetti con install.ps1 / uninstall.ps1 script
    * Il caricamento di progetti che dispone di uno script init.ps1 (ad esempio EntityFramework)
    * Pubblicazione di contenuto web

* **Soluzione alternativa:** assicurarsi che l'installazione di Windows 10 è applicate le patch più recenti, expecially gennaio 2016 (KB 3124263) o un aggiornamento successivo.  Ulteriori dettagli sono disponibili su [problema #1638 di GitHub](http://github.com/nuget/home/issues/1638)

* **Problema:** i reindirizzamenti del protocollo NuGet versione 2 sono interrotti.
I repository NuGet personalizzati che reindirizzano le richieste a un host alternativo non soddisfano la richiesta di reindirizzamento.
* **Soluzione alternativa:** per risolvere questo problema, configurare l'URI del repository di pacchetti nelle impostazioni in modo che punti al percorso del server reindirizzato.
Per ulteriori informazioni, vedere [richiesta pull GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Continuiamo a tenere traccia dei problemi nella lista di problemi di GitHub che può essere trovato in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)