---
title: Installazione degli strumenti client di NuGet
description: Istruzioni per l'installazione degli strumenti client, delle interfacce della riga di comando di dotnet e nuget e di Gestione pacchetti per Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 09c859c0ab6767ea80b6a64c194aa2623ee5c505
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610532"
---
# <a name="install-nuget-client-tools"></a>Installare gli strumenti client di NuGet

> **Si desidera installare un pacchetto? Vedere le [modalità di installazione dei pacchetti NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Per usare NuGet, come consumer o autore di pacchetti, è possibile usare gli strumenti dell'interfaccia della riga di comando nonché le funzionalità NuGet in Visual Studio. Questo articolo descrive brevemente le funzionalità dei diversi strumenti, come installarli e un confronto delle [funzionalità disponibili](#feature-availability). Per iniziare a usare NuGet per utilizzare i pacchetti, vedere [Installare e usare un pacchetto (interfaccia della riga di comando di dotnet)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) e [Installare e usare un pacchetto (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Per iniziare a creare i pacchetti NuGet, vedere [Creare e pubblicare un pacchetto .NET Standard (interfaccia della riga di comando dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) e [Creare e pubblicare un pacchetto .NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Descrizione | Download&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Strumento dell'interfaccia della riga di comando per librerie .NET Core e .NET Standard e per qualsiasi [progetto di tipo SDK](resources/check-project-format.md), ad esempio quelli destinati a .NET Framework. Incluso in .NET Core SDK, offre le principali funzionalità NuGet per tutte le piattaforme. A partire da Visual Studio 2017, l'interfaccia della riga di comando dotnet viene installata automaticamente con qualsiasi carico di lavoro correlato a .NET Core.| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Strumento dell'interfaccia della riga di comando per librerie .NET Framework e per qualsiasi [progetto non di tipo SDK](resources/check-project-format.md), ad esempio quelli destinati a librerie .NET Standard. Fornisce tutte le funzionalità di NuGet in Windows e la maggior parte delle funzionalità in Mac e Linux per l'esecuzione in Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | In Windows, fornisce le funzionalità NuGet tramite l'interfaccia utente di Gestione pacchetti e la console di Gestione pacchetti, incluse nei carichi di lavoro correlati a .NET. In Mac, fornisce alcune funzionalità tramite l'interfaccia utente. In Visual Studio Code, le funzionalità di NuGet vengono offerte tramite le estensioni. | [Visual Studio](https://www.visualstudio.com/downloads/) |

Anche l'[interfaccia della riga di comando di MSBuild](reference/msbuild-targets.md) offre la possibilità di ripristinare e creare pacchetti, utile principalmente nei server di compilazione. MSBuild non è uno strumento generico per l'utilizzo di NuGet.

## <a name="cli-tools"></a>Strumenti di interfaccia della riga di comando

I due strumenti di interfaccia della riga di comando NuGet sono `dotnet.exe` e `nuget.exe`. Vedere la [disponibilità delle funzionalità](#feature-availability) per un confronto.

* Per impostare come destinazione .NET Core o .NET Standard, usare l'interfaccia della riga di comando dotnet. L'interfaccia della riga di comando di `dotnet` è richiesta per il formato di progetto di tipo SDK, che usa l'[attributo SDK](/dotnet/core/tools/csproj#additions).
* Per avere come destinazione .NET Framework (solo progetti non in stile SDK), usare l'interfaccia della riga di comando di `nuget.exe`. Se viene eseguita la migrazione del progetto da `packages.config` a PackageReference, usare l'interfaccia della riga di comando dotnet.

### <a name="dotnetexe-cli"></a>Interfaccia della riga di comando di dotnet.exe

L'interfaccia della riga di comando di .NET Core 2.0, `dotnet.exe`, funziona in tutte le piattaforme (Windows, Mac e Linux) e offre le funzionalità principali di NuGet, ad esempio l'installazione, il ripristino e la pubblicazione di pacchetti. `dotnet` supporta l'integrazione diretta con i file di progetto .NET Core (ad esempio `.csproj`) e ciò è utile nella maggior parte degli scenari. `dotnet` supporta anche la compilazione diretta per ogni piattaforma e non richiede di installare Mono.

Installazione:

- Nei computer degli sviluppatori installare [.NET Core SDK](https://aka.ms/dotnetcoregs). A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato.
- Per i server di compilazione, seguire le istruzioni in [Uso di .NET Core SDK e dei relativi strumenti in integrazione continua](/dotnet/core/tools/using-ci-with-cli).

Per informazioni su come usare i comandi di base con l'interfaccia della riga di comando di dotnet, vedere [Installare e usare pacchetti tramite l'interfaccia della riga di comando di dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>Interfaccia della riga di comando di nuget.exe

L'interfaccia della riga di comando di `nuget.exe`, `nuget.exe`, è l'utilità da riga di comando per Windows che offre tutte le funzionalità di NuGet. Può essere eseguita anche in Mac OSX e Linux tramite [Mono](https://www.mono-project.com/docs/getting-started/install/), con alcune limitazioni.

Per informazioni su come usare i comandi di base con l'interfaccia della riga di comando di `nuget.exe`, vedere [Installare e usare pacchetti tramite l'interfaccia della riga di comando di nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

Installazione:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Usare `nuget update -self` in Windows per aggiornare una copia esistente di nuget.exe alla versione più recente.

> [!Note]
> La versione più recente consigliata dell'interfaccia della riga di comando di NuGet è sempre disponibile all'indirizzo `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Per motivi di compatibilità con sistemi di integrazione continua meno recenti, da un URL precedente, `https://nuget.org/nuget.exe`, è attualmente possibile ottenere la [versione 2.8.6 deprecata dell'interfaccia della riga di comando](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: le funzionalità di NuGet sono disponibili tramite estensioni del Marketplace oppure usare gli strumenti di interfaccia della riga di comando `dotnet.exe` o `nuget.exe`.

- Visual Studio per Mac: alcune funzionalità di NuGet sono incorporate direttamente. Per una procedura dettagliata, vedere [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough). Per le altre funzionalità, usare gli strumenti di interfaccia della riga di comando `dotnet.exe` o `nuget.exe`.

- Visual Studio in Windows: **Gestione pacchetti NuGet** è incluso in Visual Studio 2012 e versioni successive. Visual Studio include l'[interfaccia utente di Gestione pacchetti](consume-packages/install-use-packages-visual-studio.md) e la [console di Gestione pacchetti](consume-packages/install-use-packages-powershell.md), tramite cui è possibile eseguire la maggior parte delle operazioni di NuGet.
  - A partire da Visual Studio 2017, il programma di installazione include Gestione pacchetti NuGet in qualsiasi carico di lavoro che usa .NET. Per eseguire l'installazione separatamente o per verificare se l'installazione di Gestione pacchetti è già stata eseguita, eseguire il programma di installazione di Visual Studio e selezionare l'opzione **Singoli componenti > Strumenti per il codice > Gestione pacchetti NuGet**.
  - L'interfaccia utente e la console di Gestione pacchetti sono disponibili unicamente per Visual Studio in Windows e al momento non sono disponibili in Visual Studio per Mac.
  - È richiesto uno strumento dell'interfaccia della riga di comando per supportare le funzionalità di NuGet nell'IDE. È possibile usare l'interfaccia della riga di comando `dotnet` o `nuget.exe`. L'interfaccia della riga di comando `dotnet` viene installata con alcuni carichi di lavoro di Visual Studio, ad esempio .NET Core. L'interfaccia della riga di comando `nuget.exe` deve essere installata separatamente, come descritto in precedenza.
  - I comandi della console di Gestione pacchetti funzionano solo all'interno di Visual Studio in Windows e non all'interno di altri ambienti di PowerShell.
  - Per Visual Studio 2010 e versioni precedenti, installare l'estensione "NuGet Package Manager per Visual Studio".
  - Le estensioni NuGet per Visual Studio 2013 e 2015 possono anche essere scaricate da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Per visualizzare in anteprima le funzionalità NuGet future, installare un' [Anteprima di Visual Studio](https://www.visualstudio.com/vs/preview/), che può essere affiancata alle versioni stabili di Visual Studio. Per segnalare problemi o condividere idee per le anteprime, aprire un problema nel [repository GitHub di NuGet](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Disponibilità delle funzionalità

| Funzionalità | Interfaccia della riga di comando dotnet | Interfaccia della riga di comando nuget (Windows) | Interfaccia della riga di comando nuget (Mono) | Visual Studio (Windows) | Visual Studio per Mac |
| --- | --- | --- | --- | --- | --- |
| Ricerche nei pacchetti |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Installare/disinstallare pacchetti | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Aggiornamento di pacchetti | &#10004; | &#10004; | | &#10004; | &#10004; |
| Ripristinare pacchetti | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Gestire feed di pacchetti (origini) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Gestire i pacchetti in un feed | &#10004; | &#10004; | &#10004; | | |
| Impostare le chiavi API per i feed | | &#10004; | &#10004; | | |
| Creare i pacchetti(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Pubblicazione di pacchetti | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replicare pacchetti |  | &#10004; | &#10004; | | |
| Gestire le cartelle *global-packages* e della cache | &#10004; | &#10004; | &#10004; | | |
| Gestire la configurazione di NuGet | | &#10004; | &#10004; | | |

(1) Non influisce sui file di progetto; usare invece `dotnet.exe`.

(2) Funziona solo con il file `packages.config` e non con file di soluzione (`.sln`).

(3) Varie funzionalità avanzate per i pacchetti sono disponibili solo tramite l'interfaccia della riga di comando, perché non sono rappresentate negli strumenti dell'interfaccia utente di Visual Studio.

(4) Funziona con i file `.nuspec` ma non con i file di progetto.

### <a name="related-topics"></a>Argomenti correlati

- [Installare e gestire pacchetti con Visual Studio](consume-packages/install-use-packages-visual-studio.md)
- [Installare e gestire pacchetti con PowerShell](consume-packages/install-use-packages-powershell.md)
- [Installare e gestire pacchetti con l'interfaccia della riga di comando di dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Installare e gestire pacchetti con l'interfaccia della riga di comando di nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Package Manager Console PowerShell reference (Informazioni di riferimento sull'interfaccia PowerShell per la console di Gestione pacchetti)](reference/powershell-reference.md)
- [Creazione di un pacchetto](create-packages/creating-a-package.md)
- [Pubblicazione di un pacchetto](nuget-org/publish-a-package.md)

Gli sviluppatori che lavorano in ambiente Windows possono anche esplorare [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uno strumento open source autonomo per esplorare, creare e modificare visivamente i pacchetti NuGet. È molto utile, ad esempio, per apportare modifiche sperimentali alla struttura di un pacchetto senza dovere ricompilare il pacchetto.
