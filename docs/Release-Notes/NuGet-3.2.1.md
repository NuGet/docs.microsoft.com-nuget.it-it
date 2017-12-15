---
title: Note sulla versione di NuGet 3.2.1 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d27c3bb9-8db1-439a-a134-54e20b7a7766
description: "Note sulla versione per l'inclusione di NuGet 3.2.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 3.2.1 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2001d9518a34bbd5f2879de6123ec13abf4ae08
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-321-release-notes"></a>Note sulla versione di NuGet 3.2.1

[Note sulla versione 3.2 NuGet](../release-notes/nuget-3.2.md) | [note sulla versione 3.3 NuGet](../release-notes/nuget-3.3.md)

NuGet 3.2.1 per la riga di comando è stato rilasciato il 12 ottobre 2015 con un numero limitato di ottimizzazioni e le correzioni per la versione 3.2 ed è disponibile da [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Miglioramenti

* NuGet Usa ora il file di configurazione con le maiuscole e minuscole originale di `NuGet.Config`.  Questo aspetto è importante nei sistemi operativi distinzione maiuscole/minuscole [1427](https://github.com/NuGet/Home/issues/1427)
* Ripristino NuGet ora ignorerà i progetti dnx (`*.xproj`) che deve essere elaborato con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Ottimizzazione dell'utilizzo della rete quando si lavora con `index.json` e dati di registrazione del pacchetto [1426](https://github.com/NuGet/Home/issues/1426)
* Download di risorse migliorate funzionalità di gestione per essere più affidabili con servizi v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correzioni

* NuGet correttamente l'aggiornamento `.csproj` / `.vcxproj` riferimenti [1483](https://github.com/NuGet/Home/issues/1483)
* Impediscono ora di creazione quando un SpecialFolders.UserProfile non è possibile individuare una cartella. NuGet locale [1531](https://github.com/NuGet/Home/issues/1531)
* La gestione dei pacchetti nella cache locale che sono danneggiate durante il download migliorata [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Un elenco completo dei problemi descritti per l'estensione di riga di comando e Visual Studio è disponibile in NuGet GitHub [3.2.1 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nell'elenco di problemi di GitHub in cui è reperibile in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)