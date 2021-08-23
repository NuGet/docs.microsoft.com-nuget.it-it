---
title: NuGet 5.11 Note sulla versione
description: Note sulla versione per NuGet 5.11, tra cui nuove funzionalità, correzioni di bug e controller di dominio.
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728437"
---
# <a name="nuget-511-release-notes"></a>NuGet 5.11 Note sulla versione

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Installato</sup> con il carico Visual Studio 2019 con .NET Core
  
> [!NOTE]
> Visual Studio 16.11, MSBuild 16.11 e .NET 5.0.400+ richiede NuGet.exe 5.11 o versione successiva.

## <a name="summary-whats-new-in-511"></a>Riepilogo: Novità della versione 5.11

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug:**

* Strumenti -> Opzioni -> NuGet Gestione pacchetti stringa viene troncata - [#10779](https://github.com/NuGet/Home/issues/10779)

* Blocco quando viene generato l'evento PackagesMissingStatusChanged [- #10854](https://github.com/NuGet/Home/issues/10854)

* Il NuGet client ignora l'impostazione NO_PROXY- [#10902](https://github.com/NuGet/Home/issues/10902)

**[Elenco di tutti i problemi risolti in questa versione - 5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[Elenco dei commit in questa versione - 5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>Commenti e suggerimenti

I commenti degli utenti sono importanti.  Se si verificano problemi con [](https://github.com/NuGet/Home/issues) questa versione, vedere i GitHub e Visual Studio [developer Community](https://developercommunity.visualstudio.com/) problemi esistenti.  Per nuovi problemi all'interno NuGet, segnalare un GitHub [problema](https://github.com/NuGet/Home/issues/new).
Per informazioni NuGet problemi di esperienza, è [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) possibile segnalarci tramite l'opzione Segnala un problema disponibile nell'IDE preferito in Guida > **segnalare un problema**.
