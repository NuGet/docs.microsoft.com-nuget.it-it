---
title: Note sulla versione di NuGet 3.2.1
description: Note sulla versione per l'inclusione di NuGet 3.2.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-321-release-notes"></a>Note sulla versione di NuGet 3.2.1

[Note sulla versione di NuGet 3.2](../release-notes/nuget-3.2.md) | [note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 per la riga di comando è stato rilasciato il 12 ottobre 2015 con un numero limitato di ottimizzazioni e le correzioni per la versione 3.2 ed è disponibile da [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Miglioramenti

* NuGet Usa ora il file di configurazione con le maiuscole e minuscole originale di `NuGet.Config`.  Questo aspetto è importante in sistemi operativi distinzione maiuscole/minuscole [1427](https://github.com/NuGet/Home/issues/1427)
* Ripristino NuGet ora ignorerà i progetti dnx (`*.xproj`) che deve essere elaborato con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Con ottimizzazione dell'utilizzo della rete quando si lavora `index.json` e i dati di registrazione del pacchetto [1426](https://github.com/NuGet/Home/issues/1426)
* Download ottimale delle risorse gestione per essere più affidabili con i servizi v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correzioni

* NuGet correttamente l'aggiornamento `.csproj` / `.vcxproj` riferimenti [1483](https://github.com/NuGet/Home/issues/1483)
* Impediscono ora di creazione quando un SpecialFolders.UserProfile non è possibile individuare una cartella. NuGet locale [1531](https://github.com/NuGet/Home/issues/1531)
* La gestione dei pacchetti nella cache locale che sono danneggiate durante il download migliorata [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Un elenco completo dei problemi descritti per l'estensione di riga di comando e Visual Studio è disponibile in NuGet GitHub [3.2.1 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nella lista di problemi di GitHub che può essere trovato in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)