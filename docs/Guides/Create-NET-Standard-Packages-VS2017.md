---
title: Creare pacchetti NuGet di .NET Standard 2.0 con Visual Studio 2017 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: Procedura dettagliata end-to-end per la creazione di pacchetti NuGet di .NET Standard 2.0 con NuGet 4.x e Visual Studio 2017.
keywords: creare un pacchetto, pacchetti .NET Standard, .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Creare pacchetti .NET Standard 2.0 con Visual Studio 2017

*Si applica a NuGet 4.x+ e MSBuild 15.3+ forniti con Visual Studio 2017 Update 3. Per le versioni precedenti di Visual Studio 2017, queste istruzioni si applicano a .NET Standard da 1.4 a 1.6 modificando la proprietà \<TargetFramework\>. Per usare NuGet 3.x+, vedere [Creare pacchetti .NET Standard con Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

La [libreria .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) è una specifica formale delle API .NET che devono essere disponibili in tutti i runtime .NET, per creare in questo modo maggiore uniformità nell'ecosistema .NET. La libreria .NET Standard definisce un set uniforme di API della libreria di classi base per tutte le piattaforme .NET da implementare, indipendentemente dal carico di lavoro. Consente agli sviluppatori di produrre PCL che possono essere usate in tutti i runtime .NET e riduce, se non elimina, le direttive di compilazione condizionale specifiche della piattaforma nel codice condiviso.

Questa guida illustra la creazione di un pacchetto nuget per la libreria .NET Standard 2.0 con Visual Studio 2017 Update 3 e NuGet 4.0.

1. [Prerequisiti](#pre-requisites)
1. [Creare il progetto di libreria di classi](#create-the-netstandard-class-library-project)
1. [Modificare i metadati nel file con estensione csproj](#edit-metadata-in-the-csproj-file)
1. [Creare un pacchetto per il componente](#package-the-component)
1. [Argomenti correlati](#related-topics)

## <a name="pre-requisites"></a>Prerequisiti

Per questa procedura dettagliata è necessario Visual Studio 2017 Update 3 con il carico di lavoro **Sviluppo multipiattaforma .NET Core**. È possibile installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional ed Enterprise.

Il carico di lavoro necessario viene visualizzato come segue nel programma di installazione di Visual Studio:

![Carico di lavoro Sviluppo multipiattaforma .NET Core nel programma di installazione di Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>Creare il nuovo progetto di libreria di classi .NET Standard

1. In Visual Studio **File > Nuovo > Progetto**, espandere il nodo **Visual C# > .NET Standard**, selezionare **Class Library (Net Standard)** (Libreria di classi - .Net Standard), modificare il nome in AppLogger e fare clic su OK.

    ![Creare il nuovo progetto di libreria di classi](media/NuGet4-02-NewProject.png)

1. Impostare la configurazione della build su **Release**.
1. Fare clic con il pulsante destro del mouse sul progetto `AppLogger` in Esplora soluzioni, scegliere **Proprietà**, selezionare la scheda **Compilazione**, selezionare la casella per **File di documentazione XML** e impostare il nome file su `AppLogger.xml`, quindi salvare il progetto.

1. Aggiungere il codice al componente, ad esempio il seguente (che chiaramente visualizza solo i messaggi nella console):

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Compilare il progetto (con la configurazione Release) e controllare che nella cartella `bin\Release\netstandard2.0` vengano creati i file DLL e XML.

## <a name="edit-metadata-in-the-csproj-file"></a>Modificare i metadati nel file con estensione csproj

Con i progetti NuGet 4.0 e .NET Core, i metadati del pacchetto sono contenuti direttamente nel file `.csproj` invece che in file esterni, ad esempio `.nuspec`. Per una descrizione completa di tali metadati, vedere [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md#pack-target).

1. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere **Modifica AppLogger.csproj** e quindi modificare il primo gruppo di proprietà per includere le informazioni sul pacchetto, ad esempio le seguenti:

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Salvare il progetto, quindi fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Compila soluzione** per generare nuovamente tutti i file per il pacchetto, questa volta con i metadati corretti.


## <a name="package-the-component"></a>Creare un pacchetto per il componente

NuGet 4.0 supporta una destinazione pack tramite MSBuild versione 15.1+ (incluso MSBuild 15.3 come parte di Visual Studio 2017 Update 3) quando il progetto contiene i metadati del pacchetto necessari, aggiunti nella sezione precedente. Per richiamare MSBuild in questo modo, è sufficiente specificare nella riga di comando la destinazione pack nella stessa cartella del file `.csproj`:

    msbuild /t:pack /p:Configuration=Release

Per opzioni aggiuntive con `msbuild /t:pack`, inclusi ad esempio i file di contenuto, i simboli e il codice sorgente, vedere [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md#pack-target).

In ogni caso, il comando precedente genera `AppLogger.YOUR_NAME.1.0.0.nupkg` nella cartella `bin\Release` per impostazione predefinita, perché compila tale configurazione. Se si omette l'opzione `/p`, la configurazione predefinita sarà `Debug`. 

Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, verranno visualizzati i contenuti seguenti:

![NuGet Package Explorer che visualizza il pacchetto AppLogger](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> Un file `.nupkg` è solo un file ZIP con un'estensione diversa. È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.

Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Argomenti correlati

- [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md) contiene tutti i dettagli della descrizione del pacchetto direttamente nel file di progetto.
- [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md) descrive tutte le opzioni per l'uso di `msbuild /t:pack` per creare il pacchetto.
- [Documentazione della libreria .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Portabilità in .NET Core da .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
