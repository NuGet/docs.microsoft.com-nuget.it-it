---
title: Note sulla versione di NuGet 2.8.2
description: Note sulla versione per NuGet 2.8.2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780364"
---
# <a name="nuget-282-release-notes"></a>Note sulla versione di NuGet 2.8.2

Note sulla versione di [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 è stato rilasciato il 22 maggio 2014.  Questa versione include solo le modifiche apportate al nuget.exe riga di comando, al pacchetto NuGet. Server e ad altri pacchetti NuGet.  La versione non include un'estensione di Visual Studio aggiornata o un'estensione di WebMatrix.

## <a name="notable-updates"></a>Aggiornamenti rilevanti

Gli aggiornamenti più significativi sono stati inclusi nella nuget.exe riga di comando e nel pacchetto NuGet. Server (per i feed NuGet indipendenti).

### <a name="important-nugetexe-bug-fixes"></a>Correzioni di bug importanti nuget.exe

1. [nuget.exe push ha esito negativo e continua a riprovare](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe push non invia correttamente le credenziali di autenticazione di base](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe push non segue il reindirizzamento temporaneo](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Correzione di bug NuGet. Server importante

1. [Il valore di IsAbsoluteLatestVersion restituito da NuGet. Server non è corretto](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Pacchetti aggiornati

Le correzioni della riga di comando nuget.exe e NuGet. Server vengono fornite come aggiornamenti dei pacchetti NuGet.  Sono stati aggiornati anche altri pacchetti con 2.8.2.

Ecco l'elenco dei pacchetti aggiornati:

1. [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (pacchetto, non estensione)

## <a name="all-changes"></a>Tutte le modifiche
Sono stati risolti 10 problemi nella versione. Per un elenco completo degli elementi di lavoro corretti in NuGet 2.8.2, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
