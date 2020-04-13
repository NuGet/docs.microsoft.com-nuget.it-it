---
title: Creare pacchetti NuGet per la piattaforma UWP (Universal Windows Platform)
description: Una procedura dettagliata end-to-end della creazione di pacchetti NuGet utilizzando un componente di Windows Runtime per la piattaforma Windows universale in C .
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231805"
---
# <a name="create-uwp-packages-c"></a>Creazione di pacchetti UWP (c'è)Create UWP packages (C

La [piattaforma UWP (Universal Windows Platform)](/windows/uwp) è una piattaforma applicativa comune per ogni dispositivo che esegue Windows 10. In questo modello le app UWP possono chiamare sia le API WinRT comuni a tutti i dispositivi che le API (incluse Win32 e .NET) specifiche della famiglia di dispositivi su cui l'app è in esecuzione.

In questa procedura dettagliata si crea un pacchetto NuGet con un componente UWP di C' (incluso un controllo XAML) che può essere usato in progetti gestiti e nativi.

## <a name="prerequisites"></a>Prerequisiti

1. Visual Studio 2019. Installare la Community Edition 2019 gratuitamente da [visualstudio.com](https://www.visualstudio.com/); è possibile utilizzare anche le edizioni Professional ed Enterprise.

1. Interfaccia della riga di comando di NuGet. Scaricare la versione più recente `nuget.exe` da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta (il download include direttamente il file `.exe`). Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario. [Altre informazioni](/nuget/reference/nuget-exe-cli-reference#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Creare un componente Windows Runtime UWP

1. In Visual Studio scegliere **File > Nuovo > progetto,** cercare "uwp c'è", selezionare il modello Componente Windows Runtime **(Windows universale),** fare clic su Avanti, modificare il nome in ImageEnhancer e fare clic su Crea. Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.

    ![Creazione di un nuovo progetto del componente Windows Runtime UWP](media/UWP-NewProject-CS.png)

1. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, selezionare **Aggiungi > nuovo elemento**, selezionare Controllo **basato su modelli**, modificare il nome in AwesomeImageControl.cs e fare clic su **Aggiungi:**

    ![Aggiunta di un nuovo elemento Controllo basato su modelli XAML al progetto](media/UWP-NewXAMLControl-CS.png)

1. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e selezionare Proprietà.Right-click the project in Solution Explorer and select **Properties.** Nella pagina Proprietà scegliere la scheda **Compila** e abilitare **File di documentazione XML:**

    ![Impostazione di Genera file di documentazione XML su Sì](media/UWP-GenerateXMLDocFiles-CS.png)

1. Fare clic con il pulsante destro del mouse sulla *soluzione,* selezionare **Compilazione batch**, selezionare le cinque caselle di compilazione nella finestra di dialogo come illustrato di seguito. Ciò assicura che, quando si esegue una compilazione, venga generato un set completo di elementi per ogni sistema di destinazione supportato da Windows.

    ![Compilazione batch](media/UWP-BatchBuild-CS.png)

1. Nella finestra di dialogo Compilazione batch fare clic su **Compila** per verificare il progetto e creare i file di output necessari per il pacchetto NuGet.

> [!Note]
> In questa procedura dettagliata vengono usati gli elementi Debug per il pacchetto. Per il pacchetto non di debug, selezionare invece le opzioni Versione nella finestra di dialogo Compilazione batch e fare riferimento alle cartelle Versione risultanti nei passaggi che seguono.

## <a name="create-and-update-the-nuspec-file"></a>Creare e aggiornare il file con estensione nuspec

Per creare il file `.nuspec` iniziale, eseguire i tre passaggi elencati sotto. Le sezioni che seguono forniscono quindi indicazioni dettagliate sugli altri aggiornamenti necessari.

1. Aprire un prompt dei comandi e passare alla cartella contenente `ImageEnhancer.csproj`, che sarà una sottocartella sotto la posizione in cui si trova il file della soluzione.
1. Eseguire [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) il comando `ImageEnhancer.nuspec` da generare (il nome del `.csroj` file viene ricavato dal nome del file):

    ```cli
    nuget spec
    ```

1. Aprire `ImageEnhancer.nuspec` in un editor e aggiornarlo in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato. Non lasciare alcun valore di $propertyName. Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verifica un errore durante il passaggio di creazione del pacchetto.

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
        <copyright>Copyright 2020</copyright>
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
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
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

All'interno del componente, la logica di base del Tipo ImageEnhancer `ImageEnhancer.winmd` è nel codice nativo, contenuto nei vari assembly generati per ogni runtime di destinazione (ARM, ARM64, x86 e x64). Per includerli nel pacchetto, farvi riferimento nella sezione `<files>` insieme ai file di risorse PRI associati:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Creare un pacchetto per il componente

Con il `.nuspec` completamento che fa riferimento a tutti i file che è [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) necessario includere nel pacchetto, è possibile eseguire il comando:

```cli
nuget pack ImageEnhancer.nuspec
```

Questo codice genera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, vengono visualizzati i contenuti seguenti:

![NuGet Package Explorer che visualizza il pacchetto ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Un file `.nupkg` è solo un file ZIP con un'estensione diversa. È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.

Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Argomenti correlati

- [Riferimento .nuspec](../reference/nuspec.md)
- [Pacchetti di simboli](../create-packages/symbol-packages-snupkg.md)
- [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md)
- [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Includere proprietà e destinazioni MSBuild in un pacchetto](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)
