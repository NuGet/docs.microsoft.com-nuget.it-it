---
title: Installazione degli strumenti client di NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Istruzioni per l'installazione degli strumenti client, delle interfacce della riga di comando di dotnet e nuget e di Gestione pacchetti per Visual Studio.
keywords: interfaccia della riga di comando dotnet.exe, interfaccia della riga di comando nuget.exe, strumenti client NuGet, Gestione pacchetti NuGet, console di Gestione pacchetti NuGet, NuGet per Visual Studio, canale beta NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 07ca66b44a981f7fcc108e1b4d97c0cf5e206a6f
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2018
---
# <a name="installing-nuget-client-tools"></a>Installazione degli strumenti client di NuGet

> **Se servono istruzioni per installare un pacchetto, Vedere [Modi per installare pacchetti NuGet](consume-packages/ways-to-install-a-package.md).**

Per utilizzare NuGet, come consumer o autore di pacchetti, è possibile usare [strumenti dell'interfaccia della riga di comando multipiattaforma](#cli-tools) nonché le [funzionalità NuGet in Visual Studio](#visual-studio). Questo articolo descrive brevemente le funzionalità dei diversi strumenti, come installarli e un confronto delle [funzionalità disponibili](#feature-availability).

| Tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Descrizione | Download&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Incluso in .NET Core SDK, offre le principali funzionalità NuGet per tutte le piattaforme. | [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Fornisce tutte le funzionalità di NuGet in Windows e la maggior parte delle funzionalità in esecuzione in [Mono](http://www.mono-project.com/docs/getting-started/install/) su Mac e Linux. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Fornisce le funzionalità NuGet tramite l'interfaccia utente di Gestione pacchetti e la console di Gestione pacchetti. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

Anche l'[interfaccia della riga di comando di MSBuild](reference/msbuild-targets.md) offre la possibilità di ripristinare e creare pacchetti, utile principalmente nei server di compilazione. MSBuild non è in caso contrario uno strumento generico per l'utilizzo di NuGet.

## <a name="cli-tools"></a>Strumenti di interfaccia della riga di comando

I due strumenti di interfaccia della riga di comando NuGet sono `dotnet.exe` e `nuget.exe`. Vedere la [disponibilità delle funzionalità](#feature-availability) per un confronto.

### <a name="dotnetexe-cli"></a>Interfaccia della riga di comando di dotnet.exe

L'interfaccia della riga di comando di .NET Core 2.0, `dotnet.exe`, funziona in tutte le piattaforme (Windows, Mac e Linux) e offre le funzionalità principali di NuGet, ad esempio l'installazione, il ripristino e la pubblicazione di pacchetti. 'dotnet' supporta l'integrazione diretta con i file di progetto .NET Core (ad esempio `.csproj`) e ciò è utile nella maggior parte degli scenari. `dotnet` supporta anche la compilazione diretta per ogni piattaforma e non richiede di installare Mono.

Installazione:

- Nei computer degli sviluppatori installare [.NET Core SDK](https://aka.ms/dotnetcoregs).
- Per i server di compilazione, seguire le istruzioni in [Uso di .NET Core SDK e dei relativi strumenti in integrazione continua](/dotnet/core/tools/using-ci-with-cli).

Per altre informazioni, vedere [Strumenti dell'interfaccia della riga di comando di .NET Core](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x).

### <a name="nugetexe-cli"></a>Interfaccia della riga di comando di nuget.exe

L'interfaccia della riga di comando di NuGet, `nuget.exe`, è l'utilità della riga di comando per Windows che fornisce tutte le funzionalità di NuGet. Può essere eseguita anche in Mac OSX e Linux tramite Mono con alcune limitazioni. A differenza di `dotnet`, l'interfaccia della riga di comando `nuget.exe` non influisce sui file di progetto.

Installazione:

[!INCLUDE[install-cli](includes/install-cli.md)]

> [!Tip]
> Usare `nuget update -self` per aggiornare una copia esistente di nuget.exe alla versione più recente.

> [!Note]
> La versione più recente consigliata dell'interfaccia della riga di comando di NuGet è sempre disponibile all'indirizzo `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Per motivi di compatibilità con sistemi di integrazione continua meno recenti, da un URL precedente, `https://nuget.org/nuget.exe`, è sempre possibile ottenere la versione 2.8.6 dell'interfaccia della riga di comando.

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: le funzionalità di NuGet sono disponibili tramite estensioni del Marketplace oppure usare gli strumenti di interfaccia della riga di comando `dotnet.exe` o `nuget.exe`.
- Visual Studio per Mac: alcune funzionalità di NuGet sono incorporate direttamente. Per una procedura dettagliata, vedere [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough). Per le altre funzionalità, usare gli strumenti di interfaccia della riga di comando `dotnet.exe` o `nuget.exe`.

- Visual Studio in Windows: **Gestione pacchetti NuGet** è incluso in Visual Studio 2012 e versioni successive. Gestione pacchetti include l'[interfaccia utente di Gestione pacchetti](tools/package-manager-ui.md) e la [console di Gestione pacchetti](tools/package-manager-console.md), tramite cui è possibile eseguire la maggior parte delle operazioni di NuGet.
  - L'interfaccia utente e la console di Gestione pacchetti sono disponibili unicamente per Visual Studio in Windows e al momento non sono disponibili in Visual Studio per Mac.
  - Visual Studio non include automaticamente l'interfaccia della riga di comando `nuget.exe`, che deve essere installata separatamente, come descritto in precedenza.
  - I comandi della console di Gestione pacchetti funzionano solo all'interno di Visual Studio in Windows e non all'interno di altri ambienti di PowerShell.
  - Il programma di installazione di Visual Studio 2017 include Gestione pacchetti NuGet in qualsiasi carico di lavoro che usa .NET. Per eseguire l'installazione separatamente o per verificare che Gestione pacchetti sia installato, eseguire il programma di installazione di Visual Studio 2017 e selezionare l'opzione **Singoli componenti > Strumenti per il codice > Gestione pacchetti NuGet**.
  - Per Visual Studio 2010 e versioni precedenti, installare l'estensione "NuGet Package Manager per Visual Studio".
  - Le estensioni NuGet per Visual Studio 2013 e 2015 possono inoltre essere scaricate da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Se si desidera visualizzare in anteprima le funzionalità future di NuGet, installare [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), una versione di anteprima affiancata alle versioni stabili di Visual Studio. Per segnalare problemi o condividere idee per le anteprime, aprire un problema nel [repository GitHub di NuGet](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Disponibilità delle funzionalità

| Funzionalità | Interfaccia della riga di comando dotnet | Interfaccia della riga di comando nuget (Windows) | Interfaccia della riga di comando nuget (Mono) | Visual Studio (Windows) | Visual Studio per Mac |
| --- | --- | --- | --- | --- | --- |
| Ricerche nei pacchetti |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Installare/disinstallare pacchetti | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| Aggiornamento di pacchetti | &#10004; | &#10004; | | &#10004; | &#10004; |
| Ripristinare pacchetti | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| Gestire feed di pacchetti (origini) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Gestire i pacchetti in un feed | &#10004;(1) | &#10004; | &#10004; | | |
| Impostare le chiavi API per i feed | | &#10004; | &#10004; | | |
| Creare pacchetti(4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| Pubblicazione di pacchetti | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| Replicare pacchetti |  | &#10004; | &#10004; | | |
| Gestione delle cache NuGet | &#10004; | &#10004; | &#10004; | | |
| Gestire la configurazione di NuGet | | &#10004; | &#10004; | | |

(1) Pacchetti solo in nuget.org

(2) Non influisce sui file di progetto; usare invece `dotnet.exe`.

(3) Funziona solo con il file `packages.config` e non con file di soluzione (`.sln`).

(4) Sono disponibili varie funzionalità avanzate per i pacchetti solo tramite l'interfaccia della riga di comando, perché non sono rappresentate negli strumenti dell'interfaccia utente di Visual Studio.

(5) Funziona con i file `.nuspec` ma non con i file di progetto.

### <a name="related-topics"></a>Argomenti correlati

- [Comandi dotnet](tools/dotnet-commands.md)
- [Informazioni di riferimento sull'interfaccia della riga di comando di NuGet](tools/nuget-exe-cli-reference.md)
- [Package Manager UI reference (Informazioni di riferimento sull'interfaccia utente di Gestione pacchetti)](tools/package-manager-ui.md)
- [Package Manager Console reference (Informazioni di riferimento sulla console di Gestione pacchetti)](tools/package-manager-console.md)
- [Package Manager Console PowerShell reference (Informazioni di riferimento sull'interfaccia PowerShell per la console di Gestione pacchetti)](tools/powershell-reference.md)
- [Creazione di un pacchetto](create-packages/creating-a-package.md)
- [Pubblicazione di un pacchetto](create-packages/publish-a-package.md)

Gli sviluppatori che lavorano in ambiente Windows possono anche esplorare [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uno strumento open source autonomo per esplorare, creare e modificare visivamente i pacchetti NuGet. È molto utile, ad esempio, per apportare modifiche sperimentali alla struttura di un pacchetto senza dovere ricompilare il pacchetto.
