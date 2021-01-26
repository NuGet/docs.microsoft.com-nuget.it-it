---
title: Note sulla versione di NuGet 3,0 RC
description: Note sulla versione per NuGet 3,0 RC, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776570"
---
# <a name="nuget-30-rc-release-notes"></a>Note sulla versione di NuGet 3,0 RC

Note sulla versione di [NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)  |  [Note sulla versione di NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3,0 RC è stato rilasciato il 29 aprile 2015 con la versione di Visual Studio 2015 RC. Questa versione include numerose correzioni di bug importanti, miglioramenti delle prestazioni e aggiornamenti per supportare i nuovi Framework.  È disponibile solo per Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Continuazione dell'attenzione sulle prestazioni

La stabilità e le prestazioni delle query NuGet continuano a essere un argomento attivo su cui ci stiamo concentrando.  Con questa versione, è consigliabile iniziare a visualizzare le operazioni di ricerca molto rapide nell'interfaccia utente e nel sito Web di NuGet.  Stiamo monitorando il servizio e come usi il servizio per poter continuare a ottimizzare queste operazioni.

## <a name="significant-issues-resolved"></a>Problemi significativi risolti

Per stabilizzare i client NuGet, sono stati risolti molti problemi come parte di questa versione.  Ecco solo un breve elenco di alcuni dei problemi più importanti risolti:

* Come parte della ridenominazione del Framework K per ASP.NET 5, i moniker del Framework sono stati aggiornati per gestire il [collegamento](https://github.com/NuGet/Home/issues/215) DNX e dnxcore
* Aggiunta della documentazione della guida dai collegamenti nel [collegamento](https://github.com/NuGet/Home/issues/232) dell'interfaccia utente di Visual Studio
* Gestione migliore dei riferimenti complessi in `.nuspec` con [collegamento](https://github.com/NuGet/Home/issues/276) a riferimenti a Framework delimitati da virgole
* Correzione del supporto per le impostazioni cultura giapponesi ( [collegamento](https://github.com/NuGet/Home/issues/253) )
* Aggiornamento del client per consentire ai progetti ASP.NET 5 di usare il [collegamento](https://github.com/NuGet/Home/issues/219) nuovo endpoint V3
* Aggiornamento per gestire meglio la cartella dei pacchetti con il [collegamento](https://github.com/NuGet/Home/issues/56) al controllo del codice sorgente
* [Collegamento](https://github.com/NuGet/Home/issues/17) del supporto fisso per i pacchetti satellite
* [Collegamento](https://github.com/NuGet/Home/issues/18) con correzione del supporto per i file di contenuto specifici del Framework

## <a name="github-presence-overhaul"></a>Revisione della presenza in GitHub

Sono state apportate alcune modifiche ai [repository del codice sorgente su GitHub](http://github.com/nuget/home).  Se si verificano problemi con il client NuGet Visual Studio, i comandi di PowerShell o l'eseguibile da riga di comando, è possibile registrare tali problemi e monitorarne lo stato di avanzamento nell' [elenco dei problemi del repository Home di GitHub](http://github.com/nuget/home/issues).  Si stanno verificando problemi per la raccolta nel [repository nugetgallery di GitHub](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Rimanere sintonizzati

Per ulteriori informazioni sullo stato di avanzamento e sugli annunci per NuGet 3,0, tenere sotto controllo il [Blog](http://blog.nuget.org) .