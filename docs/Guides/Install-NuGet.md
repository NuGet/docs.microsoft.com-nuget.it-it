---
title: Installazione degli strumenti client di NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: Istruzioni per l'installazione degli strumenti client, dell'interfaccia della riga di comando e di Gestione pacchetti per Visual Studio.
keywords: interfaccia della riga di comando nuget.exe, strumenti client NuGet, Gestione pacchetti NuGet, console di Gestione pacchetti NuGet, NuGet per Visual Studio, canale beta NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>Installazione degli strumenti client di NuGet

> [!Tip]
> **Se servono istruzioni per installare un pacchetto, vedere [Guida introduttiva - Usare un pacchetto](../Quickstart/Use-a-Package.md).**

Esistono due strumenti principali per creare, pubblicare e utilizzare pacchetti NuGet:

1. L'[**interfaccia della riga di comando di NuGet**](#nuget-cli) è l'utilità della riga di comando per Windows che fornisce tutte le funzionalità di NuGet. Può essere eseguita anche in Mac OSX e Linux tramite Mono o tramite l'interfaccia della riga di comando di .NET Core (`dotnet`).
1. [**Gestione pacchetti NuGet in Visual Studio**](#nuget-package-manager-in-visual-studio) (solo Windows) è uno strumento GUI per la gestione dei pacchetti e include una console di PowerShell tramite cui è possibile usare alcuni comandi NuGet direttamente all'interno di Visual Studio. L'interfaccia utente e la console di Gestione pacchetti sono entrambi inclusi in Visual Studio (in Windows) 2012 e versioni successive e possono essere installati manualmente per le versioni precedenti.

    In Visual Studio per Mac, le funzionalità NuGet sono incorporate direttamente. Per una procedura dettagliata, vedere [Inserimento di un pacchetto NuGet nel progetto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).

    Visual Studio Code attualmente non include il supporto predefinito per NuGet. Usare l'interfaccia della riga di comando di NuGet o l'[interfaccia della riga di comando di dotnet](../Tools/dotnet-Commands.md).

L'interfaccia della riga di comando e Gestione pacchetti NuGet supportano entrambi le operazioni seguenti:

- Ricerche nei pacchetti
- Installazione di pacchetti
- Aggiornamento di pacchetti
- Disinstallazione di pacchetti
- Ripristino di pacchetti (solo tramite interfaccia utente in Gestione pacchetti)
- Gestione delle origini NuGet

Le funzionalità seguenti sono supportate solo nell'interfaccia della riga di comando di NuGet:

- Gestione dei pacchetti (nuget.org o feed privato)
- Creazione di pacchetti 
- Pubblicazione di pacchetti
- Gestione di NuGet.config
- Gestione delle cache NuGet
- Replica di un pacchetto

> [!Note]
> Un altro strumento utile è [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uno strumento open source autonomo per esplorare, creare e modificare visivamente i pacchetti NuGet. È molto utile, ad esempio, per apportare modifiche sperimentali alla struttura di un pacchetto senza dovere ricompilare il pacchetto ogni volta.
> La toolchain dell'[interfaccia della riga di comando .NET Core](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) multipiattaforma, usata per lo sviluppo di applicazioni .NET Core, supporta vari comandi NuGet, ad esempio delete, locals, push, pack e restore. 

## <a name="nuget-cli"></a>Interfaccia della riga di comando di NuGet

L'interfaccia della riga di comando di NuGet consente di accedere a tutte le funzionalità di NuGet e può essere eseguita in Windows, Mac OSX e Linux, come descritto nelle sezioni seguenti.

### <a name="windows"></a>Windows

**Download diretto:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> Con NuGet 1.4+ è possibile usare `nuget update -self` per aggiornare la copia esistente di nuget.exe alla versione più recente.

**Altri metodi:**

- **Chocolatey**: installare il pacchetto Chocolatey [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) tramite il client [Chocolatey](http://chocolatey.org). 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: installare il pacchetto [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) dalla console di Gestione pacchetti in Visual Studio.

    > [!Note]
    > **Per gli utenti di NuGet 2.x**: a causa di modifiche sostanziali introdotte in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) punta all'ultima versione stabile di NuGet 2.x per evitare potenziali interruzioni per i sistemi di integrazione continua.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX e Linux

In Mac OSX e Linux, esistono due modi per eseguire l'interfaccia della riga di comando di NuGet:

- Installare [.NET Core SDK](https://www.microsoft.com/net/download/core), che include le funzionalità principali di NuGet. I download sono elencati anche in [github.com/dotnet/cli](https://github.com/dotnet/cli). Se sono necessarie funzionalità più complete, scegliere la seconda opzione descritta di seguito per usare `nuget.exe` con Mono.

- Installare [Mono](http://www.mono-project.com/docs/getting-started/install/) e quindi usare l'eseguibile della riga di comando `nuget.exe` per Windows (versione 3.2 e versioni successive) da [nuget.org/downloads](https://nuget.org/downloads). L'esecuzione di NuGet in Mono è soggetta alle limitazioni seguenti:

    - Comandi di cui è stato testato il funzionamento:
        - config
        - delete
        - guida
        - install
        - list
        - push
        - setApiKey
        - sources
        - spec

    - Comandi che funzionano parzialmente:
        - pack: funziona con i file `.nuspec` ma non con i file di progetto.
        - restore: funziona con i file `packages.config` e `project.json` ma non con i file di soluzione (`.sln`).

    - Comandi che non funzionano:
        - update

### <a name="related-topics"></a>Argomenti correlati

- [Informazioni di riferimento sull'interfaccia della riga di comando di NuGet](../tools/nuget-exe-cli-reference.md)
- [Creazione di un pacchetto](../create-packages/creating-a-package.md)
- [Pubblicazione di un pacchetto](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Gestione pacchetti NuGet in Visual Studio

Gestione pacchetti NuGet è incluso in ogni edizione di Visual Studio in Windows 2012 e versioni successive. Include l'interfaccia utente di Gestione pacchetti ([riferimento](../tools/package-manager-ui.md)) e la console di Gestione pacchetti tramite cui è possibile accedere agli strumenti forniti con alcuni pacchetti ([riferimento](../tools/package-manager-console.md)).

Il programma di installazione di Visual Studio 2017 include Gestione pacchetti NuGet in qualsiasi carico di lavoro che usa .NET. Per eseguire l'installazione separatamente o per verificare che Gestione pacchetti sia installato, eseguire il programma di installazione di Visual Studio 2017 e selezionare l'opzione **Singoli componenti > Strumenti per il codice > Gestione pacchetti NuGet**.

> [!Note]
> La console richiede [PowerShell 2.0](http://support.microsoft.com/kb/968929), che sarà già installato in Windows 7 o versione successiva e Windows Server 2008 R2 o versione successiva.
>
> I comandi della console di Gestione pacchetti, inoltre, funzionano solo all'interno di Visual Studio in Windows. Usare l'interfaccia della riga di comando di NuGet al di fuori di tale ambiente, inclusi Visual Studio per Mac e Visual Studio Code.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Installazione di Gestione pacchetti per Visual Studio 2010 e versioni precedenti

*Questi passaggi non sono necessari per Visual Studio 2012 e versioni successive, che includono già Gestione pacchetti.*

1. In Visual Studio 2010 e versioni precedenti, fare clic su **Strumenti > Estensioni e aggiornamenti**.
1. Passare a **Online**, quindi cercare "NuGet Package Manager per Visual Studio" e fare clic su **Download**.
1. Nella finestra di dialogo del programma di installazione fare clic su **Installa**.
1. Al termine dell'installazione, riavviare Visual Studio.

> [!Tip]
> Se non si riesce a usare la finestra di dialogo **Estensioni e aggiornamenti** in Visual Studio (ad esempio, perché è bloccata da un proxy), è possibile scaricare le estensioni per Visual Studio 2013 e 2015 direttamente all'indirizzo [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

### <a name="updating-the-package-manager"></a>Aggiornamento di Gestione pacchetti

Per Visual Studio 2015 Update 2 e versioni successive, Gestione pacchetti viene aggiornato automaticamente all'ultima versione stabile.

Per Visual Studio 2015 Update 1 e versioni precedenti, scegliere il comando **Strumenti > Estensioni e aggiornamenti** e fare clic sulla scheda **Aggiornamenti** per vedere se è disponibile una nuova versione di Gestione pacchetti.  

### <a name="nuget-previews"></a>Versioni di anteprima di NuGet

Se si desidera visualizzare in anteprima le funzionalità future di NuGet, installare [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), una versione di anteprima affiancata alle versioni stabili di Visual Studio.

Si noti che il canale beta di NuGet precedente (`https://dotnet.myget.org/F/nuget-beta/vsix/`) per Visual Studio 2015 non viene più usato.

Per segnalare problemi relativi a qualsiasi versione di NuGet o per condividere idee, aprire un problema nel [repository GitHub di NuGet](https://github.com/Nuget/Home).

### <a name="related-topics"></a>Argomenti correlati

- [Package Manager UI reference (Informazioni di riferimento sull'interfaccia utente di Gestione pacchetti)](../tools/package-manager-ui.md)
- [Package Manager Console reference (Informazioni di riferimento sulla console di Gestione pacchetti)](../tools/package-manager-console.md)
- [Package Manager Console PowerShell reference (Informazioni di riferimento sull'interfaccia PowerShell per la console di Gestione pacchetti)](../tools/powershell-reference.md)