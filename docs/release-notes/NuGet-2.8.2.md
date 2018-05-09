---
title: Note sulla versione di NuGet 2.8.2
description: Note sulla versione per l'inclusione di NuGet 2.8.2 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-282-release-notes"></a>Note sulla versione di NuGet 2.8.2

[Note sulla versione di NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 è stato rilasciato il 22 maggio 2014.  Questa versione è incluso solo le modifiche per la riga di comando di nuget.exe, il pacchetto NuGet.Server e altri pacchetti NuGet.  La versione non include un'estensione aggiornata di Visual Studio o estensione di WebMatrix.

## <a name="notable-updates"></a>Aggiornamenti importanti

Gli aggiornamenti più importanti siano stati di nuget.exe della riga di comando e il pacchetto NuGet.Server (per i feed NuGet indipendente).

### <a name="important-nugetexe-bug-fixes"></a>Correzioni di Bug importanti nuget.exe

1. [NuGet.exe Push ha esito negativo e mantiene nuovo tentativo in corso](https://nuget.codeplex.com/workitem/4000)
1. [NuGet.exe Push non invia correttamente le credenziali di autenticazione di base](https://nuget.codeplex.com/workitem/4109)
1. [NuGet.exe Push non seguire reindirizzamento temporaneo](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Correzione di Bug importanti NuGet.Server

1. [Valore non corretto di IsAbsoluteLatestVersion restituito da NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Pacchetti aggiornati

Le nuget.exe della riga di comando e le correzioni NuGet.Server vengono fornite come aggiornamenti pacchetto NuGet.  Si sono verificati altri pacchetti aggiornati con 2.8.2 anche.

Di seguito è riportato l'elenco dei pacchetti aggiornati:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (il pacchetto, non l'estensione)

## <a name="all-changes"></a>Tutte le modifiche
Si sono verificati i 10 problemi risolti nella versione. Per un elenco completo delle operazioni gli elementi corretti in NuGet, 2.8.2 visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
