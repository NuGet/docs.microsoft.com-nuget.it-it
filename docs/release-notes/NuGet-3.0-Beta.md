---
title: Note sulla versione di NuGet 3,0 beta
description: Note sulla versione per NuGet 3,0 beta, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776629"
---
# <a name="nuget-30-beta-release-notes"></a>Note sulla versione di NuGet 3,0 beta

Note sulla versione di [NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)  |  [Note sulla versione di NuGet 3,0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3,0 beta è stato rilasciato il 23 febbraio 2015 per la versione di Visual Studio 2015 CTP 6. Questa versione significa molto per il nostro team, in quanto abbiamo un certo numero di miglioramenti dell'architettura e delle prestazioni da condividere e siamo lieti di iniziare a ottimizzare le impostazioni delle prestazioni nel servizio nuget.org.

Prima di installare questa nuova versione, è consigliabile disinstallare una versione precedente dell'estensione NuGet Visual Studio 2015.  Se si verificano problemi con questa versione dell'estensione, è consigliabile ripristinare la [versione precedente](http://nuget.codeplex.com/downloads/get/909582) per l'uso con Visual Studio 2015 Preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Questa versione di NuGet 3,0 beta è disponibile per l'installazione nella raccolta di estensioni di Visual Studio 2015 CTP 6. Si sta lavorando per ottenere la versione di anteprima per Visual Studio 2012 e Visual Studio 2013 molto presto. In precedenza abbiamo condiviso l'intento di [interrompere gli aggiornamenti per Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)e abbiamo deciso di prendere tale decisione.

## <a name="new-clientserver-api"></a>Nuova API client/server

Sono stati elaborati alcuni dettagli di implementazione per il protocollo client/server di NuGet. Il lavoro svolto consiste nel creare "API V3" per NuGet, progettato per la disponibilità elevata per scenari critici come il ripristino dei pacchetti e l'installazione di pacchetti. La nuova API si basa su REST e su ipermedia ed è stato selezionato [JSON-LD](http://json-ld.org) come formato di risorsa.

Nei bit di NuGet 3,0 beta viene visualizzata una nuova origine pacchetto denominata "api.nuget.org" nell'elenco a discesa origine pacchetto.   Se si seleziona l'origine del pacchetto, si userà la nuova API invece di connettersi a nuget.org. In NuGet 3,0 RC questa nuova origine del pacchetto basata sull'API V3 sostituirà l'origine del pacchetto "nuget.org" basata su V2.  È consigliabile disabilitare tutte le altre origini di pacchetti pubbliche e lasciare solo api.nuget.org come solo repository di pacchetti pubblici.

La creazione dell'API V3 è stata molto lunga e continuerà a mantenere l'API standard v2 per i client obsoleti che cercano di accedere al repository pubblico.

## <a name="updated-ui"></a>Interfaccia utente aggiornata

In questa versione è stata migliorata l'interfaccia utente per includere una casella combinata che consente di scegliere un'azione da eseguire con il pacchetto e di passare il pulsante anteprima in una casella di controllo nell'area Opzioni dello schermo.  L'area Opzioni non è più comprimibile e ora fornisce un collegamento alla guida che descrive le opzioni disponibili.

![Nuova interfaccia utente di NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Registrazione operazioni

La finestra modale è stata rimossa con le informazioni di registrazione che verrebbero visualizzate e nascoste durante l'installazione o la disinstallazione.  Questa finestra non ha aggiunto alcun valore quando si desidera visualizzare le informazioni o essere in grado di copiarle e incollarle.  Al contrario, ora viene reindirizzata tutta la registrazione dell'output nel riquadro Gestione pacchetti della finestra di output.  Questo aspetto è più comodo e simile a quello di un tipico report di compilazione che si desidera controllare.


### <a name="focus-on-performance"></a>Concentrarsi sulle prestazioni

Sono state apportate numerose modifiche al nome del miglioramento delle prestazioni delle ricerche NuGet e dei recuperi.  Questo è stato il nostro numero uno dei nostri clienti e volevamo assicurarci che il problema sia stato risolto in questa versione.  Abbiamo ottimizzato i nostri server, abbiamo creato una nuova rete CDN e ho migliorato la logica di corrispondenza delle query per sperare di offrire risultati più rilevanti e più veloci per la ricerca di pacchetti.

Continuando con questa fase dello sviluppo di NuGet 3,0, il servizio nuget.org verrà ottimizzato e monitorato per garantire una migliore esperienza.  Non si prevede di impegnarsi in alcun tempo di inattività, ma verranno aggiunte e modificate le risorse nel servizio.  Per informazioni dettagliate su come modificare la configurazione del servizio, tenere sotto controllo il [feed di Twitter](http://twitter.com/nuget) .

## <a name="building-nuget-with-nuget"></a>Compilazione di NuGet con NuGet

I client NuGet sono stati riprogettati in diversi componenti che vengono incorporati in pacchetti NuGet. Questo nuovo uso delle nostre librerie ci costringe a compilare componenti riutilizzabili e che possono essere inseriti in un pacchetto correttamente.  È stato possibile eliminare il codice duplicato e si è appreso come configurare meglio il processo di sviluppo per supportare la necessità di creare pacchetti in tutte le soluzioni.  È possibile cercare un post di Blog in cui si parlerà di come sono strutturati i progetti di codice e il funzionamento del processo di compilazione.

## <a name="stay-tuned"></a>Rimanere sintonizzati

Per ulteriori informazioni sullo stato di avanzamento e sugli annunci per NuGet 3,0, tenere sotto controllo il [Blog](http://blog.nuget.org) .
