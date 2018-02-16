---
title: Note sulla versione Beta di NuGet 3.0 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.0 Beta, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 3.0 note sulla versione Beta, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3a595d002e385ff0330c2eebd0e8439f5dbefbd9
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-30-beta-release-notes"></a>Note sulla versione Beta di NuGet 3.0

[Note sulla versione di anteprima di NuGet 3.0](../release-notes/nuget-3.0-preview.md) | [note sulla versione RC di NuGet 3.0](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta è stata rilasciata per la versione di Visual Studio 2015 CTP 6 23 febbraio 2015. Questa versione, molto al team, come abbiamo un numero di architettura e miglioramenti delle prestazioni per condividere e siamo entusiasti di avviare l'ottimizzazione le impostazioni delle prestazioni sul servizio nuget.org.

È consigliabile disinstallare qualsiasi versione precedente dell'estensione NuGet di Visual Studio 2015 prima di installare questa nuova versione.  Se si verificano problemi con questa versione dell'estensione, si consiglia ripristinare il [versione precedente](http://nuget.codeplex.com/downloads/get/909582) per l'uso con Visual Studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Questo NuGet 3.0 Beta è disponibile per l'installazione in Visual Studio 2015 CTP 6 estensione Gallery. Stiamo lavorando per ottenere presto anteprima Elimina per Visual Studio 2012 e Visual Studio 2013. È stato annunciato in precedenza l'intenzione di [interrompere gli aggiornamenti per Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), e si prendere tale decisione difficile.

## <a name="new-clientserver-api"></a>Nuovo Client/Server API

Abbiamo abbiamo lavorato alcuni dettagli di implementazione per il protocollo client/server NuGet. Il lavoro svolto consiste nel creare "v3 API" per NuGet, che viene progettato attorno a disponibilità elevata per gli scenari critici, ad esempio ripristino del pacchetto e l'installazione dei pacchetti. La nuova API è basata su REST e Hypermedia e sono state selezionate [JSON LD](http://json-ld.org) come il formato della risorsa.

Nei bit di NuGet 3.0 Beta, viene visualizzato una nuova origine pacchetto chiamata "api.nuget.org" nell'elenco a discesa origine pacchetto.   Se si seleziona l'origine del pacchetto, la nuova API utilizzeremo invece connettersi nuget.org. In NuGet 3.0 RC, la nuova origine pacchetto basato su v3 API sostituirà l'origine del pacchetto basato su v2 "nuget.org".  È consigliabile disattivare tutte le altre origini pacchetto pubblico e lasciare api.nuget.org solo il repository pubblici solo pacchetto.

Si è inserire una grande quantità di tempo di compilazione API v3 e continuerà a gestire l'API v2 standard per i vecchi client cerca di accedere al repository pubblico.

## <a name="updated-ui"></a>Interfaccia utente aggiornata

È stato migliorato l'interfaccia utente in questa versione per includere una casella combinata che consente di scegliere un'azione da intraprendere con il pacchetto e modificato il pulsante Anteprima in una casella di controllo nell'area Opzioni della schermata.  L'area di opzioni non è più comprimibile e offre ora un collegamento alla Guida che descrivono le opzioni disponibili.

![Nuova UI NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Registrazione di operazioni

Sono state rimosse finestra modale con informazioni di registrazione che vengono visualizzati rapidamente e nascondere durante l'installazione o disinstallazione.  Questa finestra non aggiunto alcun valore quando effettivamente si desidera visualizzare le informazioni o essere in grado di copiare e incollare da esso.  Al contrario, si sta ora reindirizzamento tutto l'output di registrazione nel riquadro di gestione pacchetti della finestra di Output.  Riteniamo che ciò è più comodo e simile a un report di compilazione che si desidera controllare.


### <a name="focus-on-performance"></a>Concentrarsi sulle prestazioni

Sono stati apportati numerose modifiche nel nome di migliorare le prestazioni delle ricerche di NuGet e operazioni di recupero.  Questo è il numero di un problema dai clienti e Desideravamo per assicurarsi che si viene indirizzati in questa versione.  Abbiamo ottimizzato i server, realizzati una nuova rete CDN e migliorata la query che logica per probabilmente offrire agli utenti più pertinenti di corrispondenza e i risultati della ricerca più veloce di pacchetto.

Man mano che si procede attraverso questa fase dello sviluppo di NuGet 3.0, si verrà ottimizzazione e monitoraggio del servizio di nuget.org per assicurarsi di offrire un'esperienza migliorata.  È non intende esercitare alcun tempo di inattività, ma verrà aggiunta e modifica delle risorse del servizio.  Tenendo sotto controllo il nostro [feed di twitter](http://twitter.com/nuget) per informazioni dettagliate su quando si modifica la configurazione del servizio.

## <a name="building-nuget-with-nuget"></a>Compilazione NuGet con NuGet

È ora abbiamo rielaborata clienti NuGet in diversi componenti che sono a loro volta compilati in pacchetti NuGet. Il riutilizzo del nostra librerie forza la creazione di componenti che sono riutilizzabili e che possono essere inseriti correttamente.  È stato in grado di eliminare il codice duplicato e che è stato illustrato come configurare meglio il processo di sviluppo per supportare la necessità di compilare pacchetti di soluzioni.  Cercare non appena un post di blog in cui verranno presentati per strutturare i progetti di codice e come funziona il processo di compilazione.

## <a name="stay-tuned"></a>In futuro

Tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!
