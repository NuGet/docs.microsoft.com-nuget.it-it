---
title: Note sulla versione per NuGet 3.0 RC
description: Note sulla versione per NuGet 3.0 RC, tra cui i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551719"
---
# <a name="nuget-30-rc-release-notes"></a>Note sulla versione per NuGet 3.0 RC

[Note sulla versione di NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [note sulla versione di NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC è stato rilasciato con la versione di Visual Studio 2015 RC il 29 aprile 2015. Questa versione include un numero di importanti correzioni di bug, miglioramenti delle prestazioni e gli aggiornamenti per supportare i nuovi Framework.  Disponibile solo per Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Continua lo stato attivo sulle prestazioni

La stabilità e prestazioni delle query di NuGet continuano a essere un argomento di grande interesse che ci concentriamo sui.  Con questa versione, è consigliabile iniziare a visualizzare le operazioni di ricerca molto rapida nel sito Web di NuGet UI and.  Viene eseguito il monitoraggio il servizio e modo in cui si utilizza il servizio in modo che è possibile continuare a ottimizzare queste operazioni.

## <a name="significant-issues-resolved"></a>Importanti problemi risolti

Per stabilizzare i client NuGet, è stato risolto numerosi problemi come parte di questa versione.  Qui è solo un breve elenco di alcuni dei problemi più importanti risolti:

* Durante la ridenominazione di framework K per ASP.NET 5, moniker del framework sono stati aggiornati per la gestione di dnx e dnxcore [collegamento](https://github.com/NuGet/Home/issues/215)
* È stata aggiunta documentazione della Guida dai collegamenti nell'interfaccia utente Visual Studio [collegamento](https://github.com/NuGet/Home/issues/232)
* Gestione più efficace dei riferimenti complessi nel `.nuspec` con i riferimenti ai framework delimitato da virgole [collegamento](https://github.com/NuGet/Home/issues/276)
* Corretto il supporto per lingue giapponese [collegamento](https://github.com/NuGet/Home/issues/253)
* Il client aggiornato per consentire l'utilizzo di nuovi endpoint v3 per i progetti ASP.NET 5 [collegamento](https://github.com/NuGet/Home/issues/219)
* Cartella dei pacchetti aggiornati per ottenere una migliore handle con controllo del codice sorgente [collegamento](https://github.com/NuGet/Home/issues/56)
* Correzione del supporto per pacchetti satellite [collegamento](https://github.com/NuGet/Home/issues/17)
* Corretto il supporto per i file di contenuto specifico del framework [collegamento](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Completamente rinnovata di presenza di GitHub

Sono state apportate alcune modifiche al nostro [su GitHub repository di codice sorgente](http://github.com/nuget/home).  Se si verificano problemi con il client di NuGet di Visual Studio, i comandi di Powershell o dalla riga di comando eseguibile è possibile accedere a questi problemi e monitorare lo stato di avanzamento nei nostri [elenco di problemi del repository GitHub Home](http://github.com/nuget/home/issues).  Microsoft sta verificando problemi per la raccolta nel nostro [repository GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Continua a seguirci

Teniamo d'occhio [nostro blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!