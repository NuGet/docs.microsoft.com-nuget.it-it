---
title: Note sulla versione di NuGet 3,4
description: Note sulla versione per NuGet 3,4, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776422"
---
# <a name="nuget-34-release-notes"></a>Note sulla versione di NuGet 3,4

Note sulla versione [di NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3,4 è stato rilasciato il 30 marzo 2016 come parte della versione Visual Studio 2015 Update 2 e Visual Studio 15 Preview ed è stato creato con alcuni principi in mente:

* Supporto multipiattaforma
* Miglioramenti delle prestazioni
* Miglioramenti dell'interfaccia utente secondaria

Le funzionalità seguenti sono state aggiunte in precedenza in RC e sono state aggiornate o completate per la versione 3,4:

## <a name="new-features"></a>Nuove funzioni e caratteristiche

* I client NuGet supportano ora la codifica di contenuto gzip dai repository
* Supporto per PDB dai pacchetti nei progetti xproj
* Supporto per le azioni di compilazione iOS e Android nell'elemento contentFiles
* Supporto per i moniker del Framework netstandard e netstandardapp

## <a name="new-user-interface-features"></a>Nuove funzionalità dell'interfaccia utente

* Miglioramenti significativi delle prestazioni in particolare sulle schede installate, aggiornate e consolidate
* L'origine dell'aggregazione ' tutte le origini pacchetti ' è disponibile con Unione dei risultati di ricerca corretta
* Le schede installato e aggiornamenti sono ora ordinate in ordine alfabetico
* È stato aggiunto un pulsante di aggiornamento che consente di aggiornare una ricerca
* Opzioni di compilazione più recenti all'inizio dell'elenco di versioni

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* I pacchetti a cui viene fatto riferimento in `project.json` che hanno una versione mobile non vengono aggiornati in ogni compilazione. Verranno invece aggiornati solo quando è necessario eseguire il ripristino, la pulizia, la ricompilazione o la modifica `project.json` .
* le origini del repository nuget.org non sono più forzate in una configurazione di progetto quando si usa l'interfaccia utente di configurazione di NuGet.
* NuGet non ripristina più i pacchetti nei progetti condivisi né scrive un file di blocco.
* Si è verificato un errore di rete migliorato ed è stato effettuato un nuovo tentativo di gestione per server non raggiungibili o lenti a risposta.
* I comportamenti della tastiera e del mouse sono stati migliorati nell'interfaccia utente di gestione pacchetti di Visual Studio.
* È ora supportato lo schema più recente `project.json` in DNX.

## <a name="breaking-changes"></a>Modifiche di rilievo

* I numeri di versione del pacchetto vengono ora normalizzati nel formato *principale*. *minore*. *patch* - di *versione preliminare*   Ogni principale, minore e patch viene considerato come numeri interi ed Elimina gli zeri iniziali.  Le informazioni sulla versione preliminare vengono considerate come una stringa e non vengono applicate modifiche. Questi numeri vengono usati nelle query dai client NuGet e dalla ricerca fornita dal servizio nuget.org.  Per altri dettagli, vedere la documentazione di NuGet in [versioni provvisorie](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problemi noti

* **Problema:** Gli utenti di Windows 10 v1511 possono riscontrare problemi o anche un arresto anomalo di Visual Studio con PowerShell in Visual Studio negli scenari seguenti:
    * Installazione/disinstallazione di pacchetti con script install.ps1/uninstall.ps1
    * Caricamento di progetti con uno script di init.ps1 (ad esempio EntityFramework)
    * Pubblicazione di contenuto Web

* **Soluzione alternativa:** Assicurarsi che per l'installazione di Windows 10 siano applicate le patch più recenti, soprattutto il 2016 gennaio (KB 3124263) o un aggiornamento successivo.  Ulteriori informazioni sono disponibili sul [problema GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problema:** i reindirizzamenti del protocollo NuGet versione 2 sono interrotti.
I repository NuGet personalizzati che reindirizzano le richieste a un host alternativo non soddisfano la richiesta di reindirizzamento.
* **Soluzione alternativa:**  Per risolvere questo problema, configurare l'URI del repository del pacchetto in impostazioni in modo che punti al percorso del server reindirizzato.
Per altre informazioni, vedere [#387 della richiesta pull di GitHub](https://github.com/NuGet/NuGet.Client/pull/387).

Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)