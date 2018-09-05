---
title: Note sulla versione Beta di NuGet 3.0
description: Note sulla versione per NuGet 3.0 Beta, tra cui i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550913"
---
# <a name="nuget-30-beta-release-notes"></a>Note sulla versione Beta di NuGet 3.0

[Note sulla versione di anteprima di NuGet 3.0](../release-notes/nuget-3.0-preview.md) | [note sulla versione per NuGet 3.0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta è stato rilasciato per la versione di Visual Studio 2015 CTP 6 23 febbraio 2015. Questa versione significa molto al nostro team, come abbiamo un numero di architettura e miglioramenti delle prestazioni da condividere e siamo lieti di avviare l'ottimizzazione le impostazioni delle prestazioni nel nostro servizio di nuget.org.

È consigliabile disinstallare qualsiasi versione precedente dell'estensione NuGet di Visual Studio 2015 prima di installare questa nuova versione.  Se si verificano problemi con questa versione dell'estensione, è consigliabile si ripristina il [versione precedente](http://nuget.codeplex.com/downloads/get/909582) per l'uso con Visual Studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Questo NuGet 3.0 Beta è disponibile per l'installazione in Visual Studio 2015 CTP 6 raccolta di estensioni. Stiamo lavorando per sfuggire cadute di anteprima per Visual Studio 2012 e Visual Studio 2013 molto presto. È stato annunciato in precedenza il nostro obiettivo per [interrompere gli aggiornamenti per Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), e si è presa questa decisione difficile.

## <a name="new-clientserver-api"></a>Nuovo Client/Server API

Questo abbiamo lavorato su alcuni dettagli di implementazione per il protocollo client/server di NuGet. Il lavoro svolto consiste nel creare "v3 API" per NuGet, che viene progettato attorno a disponibilità elevata per scenari critici, ad esempio il ripristino dei pacchetti e l'installazione dei pacchetti. La nuova API è basata su REST e abbiamo selezionato Ipermedia e abbiamo [JSON-LD](http://json-ld.org) come il formato della risorsa.

I bit di NuGet 3.0 Beta, visualizza una nuova origine pacchetto denominata "api.nuget.org" nell'elenco a discesa origine pacchetto.   Se si seleziona tale origine del pacchetto, si userà la nuova API invece di connettersi in nuget.org. In NuGet 3.0 RC, la nuova origine pacchetto v3 basati su API sostituirà l'origine del pacchetto basato su v2 "nuget.org".  È consigliabile disabilitare tutte le altre origini di pacchetti pubblici e lasciare api.nuget.org solo il repository dei pacchetti solo pubblico.

È molto tempo nella creazione di API v3 e scoperto continuerà a gestire l'API v2 standard per i vecchi client che cercano di accedere al repository pubblico.

## <a name="updated-ui"></a>Interfaccia utente aggiornata

È stato migliorato l'interfaccia utente in questa versione per includere una casella combinata che è possibile scegliere un'azione da intraprendere con il pacchetto e passa il pulsante Anteprima in una casella di controllo nell'area delle opzioni dello schermo.  Area delle opzioni non è più comprimibile e offre ora un collegamento alla Guida che descrive le opzioni disponibili.

![Nuova UI NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Registrazione delle operazioni

È stata rimossa la finestra modale con le informazioni di registrazione che vengono visualizzati rapidamente e nascondere durante l'installazione o disinstallazione.  In questa finestra non aggiunto alcun valore quando si sarebbe davvero desidera vedere le informazioni o essere in grado di copiare e incollare da quest'ultimo.  Al contrario, si sta ora reindirizzando tutto l'output di registrazione nel riquadro di gestione pacchetti della finestra di Output.  Riteniamo che questo è più comodo e simile a un report di compilazione che si desidera esaminare.


### <a name="focus-on-performance"></a>Concentrarsi sulle prestazioni

Sono state apportate numerose modifiche nel nome migliorando le prestazioni delle ricerche di NuGet e operazioni di recupero.  Questo era il problema numero uno dai nostri clienti e volevamo essere sicuri che viene soddisfatta in questa versione.  Abbiamo il server, realizzato una nuova rete CDN, ottimizzati e migliorata la query corrispondente per la logica per si spera offrire agli utenti più rilevante e i risultati della ricerca del pacchetto più veloce.

Nel corso del processo durante questa fase dello sviluppo di NuGet 3.0, si verrà ottimizzazione e monitoraggio del servizio di nuget.org per assicurarsi di offrire un'esperienza migliorata.  Microsoft non pianificare coinvolgere i tempi di inattività, ma verrà aggiunta e modifica delle risorse del servizio.  Teniamo d'occhio nostro [feed di twitter](http://twitter.com/nuget) per informazioni dettagliate su quando si modifica la configurazione del servizio.

## <a name="building-nuget-with-nuget"></a>Compilazione NuGet con NuGet

È ora stata rearchitected i nostri clienti di NuGet in diversi componenti che sono a loro volta da compilare in pacchetti NuGet. Questo riutilizzo dei nostri librerie forza la creazione di componenti che vengono riutilizzate e che possono essere inseriti correttamente.  È stato in grado di eliminare il codice duplicato e abbiamo imparato a meglio configurare il processo di sviluppo per supportare la necessità di compilare pacchetti per tutto le nostre soluzioni.  Cercare un post di blog a breve in cui si discuterà come sono strutturati i progetti di codice e come funziona il processo di compilazione.

## <a name="stay-tuned"></a>Continua a seguirci

Teniamo d'occhio [nostro blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!
