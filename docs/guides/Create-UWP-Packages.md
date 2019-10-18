---
title: Creare pacchetti NuGet per la piattaforma UWP (Universal Windows Platform)
description: Procedura dettagliata end-to-end sulla creazione di pacchetti NuGet con un componente Windows Runtime per la piattaforma UWP (Universal Windows Platform).
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380760"
---
# <a name="create-uwp-packages"></a>Creare pacchetti UWP

La [piattaforma UWP (Universal Windows Platform)](https://developer.microsoft.com/windows) è una piattaforma applicativa comune per ogni dispositivo che esegue Windows 10. In questo modello le app UWP possono chiamare sia le API WinRT comuni a tutti i dispositivi che le API (incluse Win32 e .NET) specifiche della famiglia di dispositivi su cui l'app è in esecuzione.

Questa procedura dettagliata descrive come creare un pacchetto NuGet con un componente UWP nativo (incluso un controllo XAML) che può essere usato in progetti sia gestiti che nativi.

## <a name="prerequisites"></a>Prerequisites

1. Visual Studio 2017 o Visual Studio 2015. Installare l'edizione 2017 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/). È anche possibile usare le edizioni Professional ed Enterprise.

1. Interfaccia della riga di comando di NuGet. Scaricare la versione più recente `nuget.exe` da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta (il download include direttamente il file `.exe`). Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.

## <a name="create-a-uwp-windows-runtime-component"></a>Creare un componente Windows Runtime UWP

1. In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C++ > Windows > Universale**, selezionare il modello **Componente Windows Runtime (Windows universale)** , modificare il nome in ImageEnhancer e fare clic su OK. Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.

    ![Creazione di un nuovo progetto del componente Windows Runtime UWP](media/UWP-NewProject.png)

1. Fare clic con il pulsante destro sul progetto in Esplora soluzioni, scegliere **Aggiungi > Nuovo elemento**, fare clic sul nodo **Visual C++ > XAML**, selezionare **Controllo basato su modelli**, modificare il nome in AwesomeImageControl.cpp e fare clic su **Aggiungi**:

    ![Aggiunta di un nuovo elemento Controllo basato su modelli XAML al progetto](media/UWP-NewXAMLControl.png)

1. Fare clic con il pulsante destro del mouse in Esplora soluzioni e scegliere **Proprietà**. Nella pagina delle proprietà espandere **Proprietà di configurazione > C/C++** e fare clic su **File di output**. Nel riquadro a destra impostare il valore di **Genera file di documentazione XML** su Sì:

    ![Impostazione di Genera file di documentazione XML su Sì](media/UWP-GenerateXMLDocFiles.png)

1. Fare clic con il pulsante destro del mouse sulla *soluzione*, scegliere **Compilazione batch** e selezionare le tre caselle Debug nella finestra di dialogo, come illustrato sotto. Ciò assicura che, quando si esegue una compilazione, venga generato un set completo di elementi per ogni sistema di destinazione supportato da Windows.

    ![Compilazione batch](media/UWP-BatchBuild.png)

1. Nella finestra di dialogo Compilazione batch fare clic su **Compila** per verificare il progetto e creare i file di output necessari per il pacchetto NuGet.

> [!Note]
> In questa procedura dettagliata vengono usati gli elementi Debug per il pacchetto. Per il pacchetto non di debug, selezionare invece le opzioni Versione nella finestra di dialogo Compilazione batch e fare riferimento alle cartelle Versione risultanti nei passaggi che seguono.

## <a name="create-and-update-the-nuspec-file"></a>Creare e aggiornare il file con estensione nuspec

Per creare il file `.nuspec` iniziale, eseguire i tre passaggi elencati sotto. Le sezioni che seguono forniscono quindi indicazioni dettagliate sugli altri aggiornamenti necessari.

1. Aprire un prompt dei comandi e passare alla cartella contenente `ImageEnhancer.vcxproj`, che sarà una sottocartella sotto la posizione in cui si trova il file della soluzione.
1. Eseguire il comando `spec` di NuGet per generare `ImageEnhancer.nuspec`. Il nome del file viene ricavato dal nome del file `.vcxproj`:

    ```cli
    nuget spec
    ```

1. Aprire `ImageEnhancer.nuspec` in un editor e aggiornarlo in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato. Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verifica un errore durante il passaggio di creazione del pacchetto.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Per i pacchetti compilati per uso pubblico, prestare particolare attenzione all'elemento `<tags>`, perché questi tag consentono ad altri utenti di trovare il pacchetto e di conoscerne le funzioni.

### <a name="adding-windows-metadata-to-the-package"></a>Aggiunta di metadati Windows al pacchetto

Un componente Windows Runtime richiede metadati che descrivono tutti i tipi disponibili pubblicamente, per consentire ad altre app e librerie di utilizzare il componente. Questi metadati sono contenuti in un file con estensione winmd, che viene creato quando si compila il progetto e deve essere incluso nel pacchetto NuGet insieme a un file XML con dati IntelliSense che viene compilato nello stesso momento.

Aggiungere il nodo `<files>` seguente al file `.nuspec`:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>Aggiunta di contenuto XAML

Per includere un controllo XAML con il componente, è necessario aggiungere il file XAML contenente il modello predefinito per il controllo (generato dal modello di progetto). Anche questo va inserito nella sezione `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>Aggiunta di librerie di implementazione native

Nel componente la logica principale del tipo ImageEnhancer si trova nel codice nativo, che è contenuto nei diversi assembly `ImageEnhancer.dll` generati per ogni runtime di destinazione (ARM, x86 e x64). Per includerli nel pacchetto, farvi riferimento nella sezione `<files>` insieme ai file di risorse PRI associati:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Aggiunta del file con estensione targets

Per i progetti C++ e JavaScript che potrebbero utilizzare il pacchetto NuGet è poi necessario un file con estensione targets per identificare i file di assembly e winmd necessari. iC# progetti e Visual Basic eseguono questa operazione automaticamente. Creare questo file copiando il testo seguente in `ImageEnhancer.targets` e salvarlo nella stessa cartella del file di `.nuspec`. _Nota_: questo file `.targets` deve avere lo stesso nome dell'ID di pacchetto (ad esempio, l'elemento `<Id>` nel file `.nupspec`):

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

Fare quindi riferimento a `ImageEnhancer.targets` nel file `.nuspec`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>File con estensione nuspec finale

Il file `.nuspec` finale sarà simile al seguente, dove YOUR_NAME deve essere sostituito con un valore appropriato:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Creare un pacchetto per il componente

Dopo avere completato il file `.nuspec` che fa riferimento a tutti i file da includere nel pacchetto, è possibile eseguire il comando `pack`:

```cli
nuget pack ImageEnhancer.nuspec
```

Questo codice genera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, vengono visualizzati i contenuti seguenti:

![NuGet Package Explorer che visualizza il pacchetto ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Un file `.nupkg` è solo un file ZIP con un'estensione diversa. È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.

Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Argomenti correlati

- [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md)
- [Pacchetti di simboli](../create-packages/symbol-packages-snupkg.md)
- [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md)
- [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Includere proprietà e destinazioni MSBuild in un pacchetto](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)
