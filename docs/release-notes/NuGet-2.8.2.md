---
title: Note sulla versione di NuGet 2.8.2
description: Note sulla versione per NuGet 2.8.2, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551148"
---
# <a name="nuget-282-release-notes"></a>Note sulla versione di NuGet 2.8.2

[Note sulla versione di NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 è stato rilasciato il 22 maggio 2014.  Questa versione è incluso solo le modifiche di nuget.exe della riga di comando, il pacchetto NuGet. Server e altri pacchetti NuGet.  La versione non include un'estensione di Visual Studio aggiornata o estensione di WebMatrix.

## <a name="notable-updates"></a>Aggiornamenti importanti

Gli aggiornamenti più importanti riguardano il nuget.exe della riga di comando e il pacchetto NuGet. Server (per i feed NuGet self-hosted).

### <a name="important-nugetexe-bug-fixes"></a>Correzioni di Bug importanti nuget.exe

1. [NuGet.exe Push ha esito negativo e mantiene nuovo tentativo in corso](https://nuget.codeplex.com/workitem/4000)
1. [NuGet.exe Push non viene inviato correttamente le credenziali di autenticazione di base](https://nuget.codeplex.com/workitem/4109)
1. [NuGet.exe Push non seguire reindirizzamento temporaneo](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Correzione di Bug importanti NuGet. Server

1. [Valore errato della IsAbsoluteLatestVersion restituito da NuGet. Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Pacchetti aggiornati

Gli aggiornamenti di NuGet. Server e nuget.exe della riga di comando sono disponibili come gli aggiornamenti dei pacchetti NuGet.  Si sono verificati altri pacchetti aggiornati con 2.8.2 anche.

Ecco l'elenco dei pacchetti aggiornati:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (il pacchetto, non l'estensione)

## <a name="all-changes"></a>Tutte le modifiche
Non vi sono 10 problemi risolti nella versione. Per un elenco completo delle operazioni elementi risolti in NuGet 2.8.2, vista la [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
