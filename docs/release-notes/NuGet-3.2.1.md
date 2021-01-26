---
title: Note sulla versione di NuGet 3.2.1
description: Note sulla versione per NuGet 3.2.1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776520"
---
# <a name="nuget-321-release-notes"></a>Note sulla versione di NuGet 3.2.1

Note sulla versione di [NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Note sulla versione di NuGet 3,3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 per la riga di comando è stato rilasciato il 12 ottobre 2015 con alcune ottimizzazioni e correzioni per la versione 3,2 ed è disponibile da [dist.NuGet.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Miglioramenti

* NuGet ora usa il file di configurazione con la combinazione di maiuscole e minuscole originale di `NuGet.Config` .  Questo è importante nei sistemi operativi con distinzione tra maiuscole e minuscole [1427](https://github.com/NuGet/Home/issues/1427)
* Il ripristino NuGet ignorerà ora i progetti DNX ( `*.xproj` ) che devono essere elaborati con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Ottimizzazione dell'utilizzo della rete quando si utilizzano `index.json` i dati di registrazione del pacchetto [1426](https://github.com/NuGet/Home/issues/1426)
* Miglioramento della gestione del download delle risorse per una maggiore affidabilità con i servizi V2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correzioni

* Aggiornamento di NuGet aggiorna correttamente i `.csproj` / `.vcxproj` riferimenti [1483](https://github.com/NuGet/Home/issues/1483)
* È ora possibile impedire la creazione di una cartella locale. NuGet quando non è possibile trovare SpecialFolders. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)
* Gestione migliorata dei pacchetti nella cache locale danneggiata durante il download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Un elenco completo dei problemi risolti per la riga di comando e l'estensione di Visual Studio è disponibile nell' [attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) NuGet di GitHub 3.2.1

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)