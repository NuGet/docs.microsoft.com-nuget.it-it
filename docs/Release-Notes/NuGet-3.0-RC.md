---
title: Note sulla versione RC di NuGet 3.0 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.0 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "NuGet 3.0 RC note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc-release-notes"></a>Note sulla versione RC di NuGet 3.0

[Note sulla versione Beta di NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [note sulla versione di NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC il 29 aprile 2015 è stata rilasciata con la versione di Visual Studio 2015 RC. Questa versione presenta una serie di importanti correzioni di bug, miglioramenti delle prestazioni e gli aggiornamenti per supportare nuovi Framework.  È disponibile solo per Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Continua lo stato attivo sulle prestazioni

Stabilità e prestazioni delle query NuGet continuano a essere un argomento che è trattata in.  Con questa versione, è consigliabile iniziare visualizzare le operazioni di ricerca molto rapida NuGet UI e sito Web.  Viene eseguito il monitoraggio il servizio e come utilizzare il servizio in modo da potere continuare a ottimizzare queste operazioni.

## <a name="significant-issues-resolved"></a>Importanti problemi risolti

Per stabilizzare i client NuGet, è risolvere molti problemi come parte di questa versione.  Di seguito è solo un breve elenco di alcuni dei più importanti problemi risolti:

* Durante la ridenominazione di framework K per ASP.NET 5, moniker del framework sono stati aggiornati per gestire dnx e dnxcore [collegamento](https://github.com/NuGet/Home/issues/215)
* Aggiunta di documentazione della Guida dai collegamenti nell'interfaccia utente Visual Studio [collegamento](https://github.com/NuGet/Home/issues/232)
* Migliore gestione dei riferimenti complessi in `.nuspec` con i riferimenti framework delimitato da virgole [collegamento](https://github.com/NuGet/Home/issues/276)
* Fissa il supporto per lingue giapponese [collegamento](https://github.com/NuGet/Home/issues/253)
* Il client aggiornato per consentire l'utilizzo di nuovi endpoint v3 per i progetti di ASP.NET 5 [collegamento](https://github.com/NuGet/Home/issues/219)
* Cartella di pacchetti di handle aggiornata per una migliore controllo del codice sorgente [collegamento](https://github.com/NuGet/Home/issues/56)
* Supporto per i pacchetti satellite fissa [collegamento](https://github.com/NuGet/Home/issues/17)
* Supporto per i file di contenuto specifico del framework corretti [collegamento](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Revisione di presenza di GitHub

È stato apportato alcune modifiche per il nostro [origine repository di codice su GitHub](http://github.com/nuget/home).  Se si dispone di eventuali problemi con il client NuGet di Visual Studio, i comandi di Powershell o la riga di comando eseguibile è possibile accedere a questi problemi e monitorare lo stato di avanzamento nel nostro [elenco di problemi di repository GitHub Home](http://github.com/nuget/home/issues).  Microsoft sta verificando problemi per la raccolta nel nostro [repository GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>In futuro

Tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!