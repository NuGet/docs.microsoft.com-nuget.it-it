---
title: Note sulla versione di NuGet 3.2.1
description: Note sulla versione per NuGet 3.2.1, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548190"
---
# <a name="nuget-321-release-notes"></a>Note sulla versione di NuGet 3.2.1

[Note sulla versione di NuGet 3.2](../release-notes/nuget-3.2.md) | [note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 per la riga di comando è stato rilasciato il 12 ottobre 2015 grazie a una serie di ottimizzazioni e correzioni per la versione 3.2 ed è disponibile dal [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Miglioramenti

* NuGet ora Usa il file di configurazione con le maiuscole e minuscole originali di `NuGet.Config`.  Questo aspetto è importante nei sistemi operativi distinzione maiuscole/minuscole [1427](https://github.com/NuGet/Home/issues/1427)
* Ripristino di NuGet ignorerà ora progetti dnx (`*.xproj`) che deve essere elaborato con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Ottimizzata l'utilizzo della rete quando si lavora con `index.json` e i dati di registrazione del pacchetto [1426](https://github.com/NuGet/Home/issues/1426)
* Download delle risorse migliorate funzionalità di gestione per essere più affidabile con i servizi v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correzioni

* Aggiornamento di NuGet aggiorni correttamente `.csproj` / `.vcxproj` riferimenti [1483](https://github.com/NuGet/Home/issues/1483)
* Impediscono ora di creazione quando un SpecialFolders.UserProfile non è possibile individuare una cartella locale .nuget [1531](https://github.com/NuGet/Home/issues/1531)
* La gestione dei pacchetti nella cache locale che sono danneggiate durante il download migliorata [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Un elenco completo dei problemi risolti per l'estensione di riga di comando e Visual Studio è disponibili in GitHub di NuGet [3.2.1 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)