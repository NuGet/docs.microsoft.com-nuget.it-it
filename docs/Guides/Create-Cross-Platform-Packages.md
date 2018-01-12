---
title: Creare pacchetti NuGet multipiattaforma (per iOS, Android e Windows) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: ae24824b-a138-4d12-a810-1f653ddffd32
description: Procedura dettagliata end-to-end sulla creazione di pacchetti NuGet per Xamarin che usano API native in iOS, Android e Windows.
keywords: creare un pacchetto, pacchetti per Xamarin, pacchetti multipiattaforma
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f372856232f151efcf972881cffbe7d4bb7ed6ee
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="create-cross-platform-packages"></a>Creare pacchetti multipiattaforma

Un pacchetto multipiattaforma contiene codice che usa le API native in iOS, Android e Windows, a seconda del sistema operativo in fase di esecuzione. Anche se si tratta di un'operazione semplice, è preferibile consentire agli sviluppatori di utilizzare il pacchetto da una libreria .NET Standard o PCL tramite una superficie di attacco delle API comune.

In questa procedura dettagliata si creerà un pacchetto NuGet multipiattaforma che può essere usato in progetti per dispositivi mobili su iOS, Android e Windows.

1. [Prerequisiti](#pre-requisites)
1. [Creare la struttura del progetto e il codice di astrazione](#create-the-project-structure-and-abstraction-code)
1. [Scrivere il codice specifico della piattaforma](#write-your-platform-specific-code)
1. [Creare e aggiornare il file con estensione nuspec](#create-and-update-the-nuspec-file)
1. [Creare un pacchetto per il componente](#package-the-component)
1. [Argomenti correlati](#related-topics)

## <a name="pre-requisites"></a>Prerequisiti

1. Visual Studio 2015 con la piattaforma UWP (Universal Windows Platform) e Xamarin. Installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/). È anche possibile usare le edizioni Professional ed Enterprise. Per includere gli strumenti UWP e Xamarin, selezionare un'installazione personalizzata e selezionare le opzioni appropriate.
1. Interfaccia della riga di comando di NuGet. Scaricare la versione più recente di nuget.exe da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta. Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.

> [!Note]
> Poiché nuget.exe è di per sé lo strumento dell'interfaccia della riga di comando e non un programma di installazione, assicurarsi di salvare il file scaricato dal browser invece di eseguirlo.


## <a name="create-the-project-structure-and-abstraction-code"></a>Creare la struttura del progetto e il codice di astrazione

1. Scaricare ed eseguire l'[estensione Plugin for Xamarin Templates](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) per Visual Studio. Questi modelli consentiranno di creare facilmente la struttura del progetto necessaria per questa procedura dettagliata.
1. In Visual Studio fare clic su **File > Nuovo > Progetto**, cercare `Plugin`, selezionare il modello **Plugin for Xamarin**, modificare il nome in LoggingLibrary e fare clic su OK.

    ![Nuovo progetto di app vuota (Xamarin.Forms portabile) in Visual Studio](media/CrossPlatform-NewProject.png)

La soluzione risultante contiene due progetti PCL, oltre a diversi progetti specifici della piattaforma:

- La libreria PCL denominata `Plugin.LoggingLibrary.Abstractions (Portable)` definisce l'interfaccia pubblica (la superficie di attacco delle API) del componente, in questo caso l'interfaccia `ILoggingLibrary` contenuta nel file ILoggingLibrary.cs, dove si definirà l'interfaccia per la libreria.
- L'altra libreria PCL, `Plugin.LoggingLibrary (Portable)`, contiene il codice in CrossLoggingLibrary.cs che individuerà un'implementazione specifica della piattaforma dell'interfaccia astratta in fase di esecuzione. In genere non è necessario modificare questo file.
- Ogni progetto specifico della piattaforma, ad esempio `Plugin.LoggingLibrary.Android`, contiene un'implementazione nativa dell'interfaccia nei rispettivi file LoggingLibraryImplementation.cs, dove si compilerà il codice della libreria.

Per impostazione predefinita, il file ILoggingLibrary.cs del progetto Abstractions contiene una definizione dell'interfaccia, ma nessun metodo. Ai fini di questa procedura dettagliata, aggiungere un metodo `Log` come indicato di seguito:

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>Scrivere il codice specifico della piattaforma

Per eseguire un'implementazione specifica della piattaforma dell'interfaccia `ILoggingLibrary` e dei relativi metodi, seguire questa procedura:

1. Aprire il file `LoggingLibraryImplementation.cs` di ogni progetto della piattaforma e aggiungere il codice necessario, ad esempio (usando il progetto `Plugin.LoggingLibrary.Android`):

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. Ripetere questa implementazione nei progetti per ogni piattaforma che si vuole supportare.
1. Fare clic con il pulsante destro del mouse sul progetto iOS, scegliere **Proprietà**, fare clic sulla scheda **Compilazione** e rimuovere "\iPhone" dalle impostazioni **Percorso di output** e **File di documentazione XML**. Questa operazione viene eseguita solo per facilitare il resto della procedura dettagliata. Salvare il file al termine.
1. Fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Gestione configurazione** e selezionare le caselle **Compilazione** per le librerie PCL e ogni piattaforma supportata.
1. Fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Compila soluzione** per controllare il lavoro e generare gli elementi per cui in seguito verrà creato il pacchetto. Se vengono visualizzati errori su riferimenti mancanti, fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Ripristina pacchetti NuGet** per installare le dipendenze ed eseguire di nuovo la compilazione.

> [!Note]
> Per eseguire la compilazione per iOS, è necessario un Mac in rete connesso a Visual Studio, come descritto in [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) (Introduzione a Xamarin.iOS per Visual Studio). Se non è disponibile un Mac, cancellare il progetto iOS in Gestione configurazione (passaggio 3).


## <a name="create-and-update-the-nuspec-file"></a>Creare e aggiornare il file con estensione nuspec

1. Aprire un prompt dei comandi, passare alla cartella `LoggingLibrary`, di un livello inferiore rispetto alla posizione del file `.sln`, ed eseguire il comando `spec` di NuGet per creare il file `Package.nuspec` iniziale:

```
nuget spec
```

1. Rinominare questo file in `LoggingLibrary.nuspec` e aprirlo in un editor.
1. Aggiornare il file in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato. Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verificherà un errore durante il passaggio di creazione del pacchetto.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```
    
> [!Tip]
> È possibile aggiungere alla versione del pacchetto il suffisso `-alpha`, `-beta` o `-rc` per contrassegnare il pacchetto come non definitivo. Per altre informazioni sulle versioni non definitive, vedere [Versioni non definitive](../create-packages/prerelease-packages.md).

### <a name="add-reference-assemblies"></a>Aggiungere assembly di riferimento

Per includere gli assembly di riferimento specifici della piattaforma, aggiungere il codice seguente all'elemento `<files>` di `LoggingLibrary.nuspec` in modo appropriato alle piattaforme supportate:

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> Per abbreviare i nomi dei file DLL e XML, fare clic con il pulsante destro del mouse su un determinato progetto, scegliere la scheda **Libreria** e modificare i nomi degli assembly.


### <a name="add-dependencies"></a>Aggiungere dipendenze

Se sono presenti dipendenze specifiche per le implementazioni native, usare l'elemento `<dependencies>` con gli elementi `<group>` per specificarle, ad esempio:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

Il codice seguente, ad esempio, imposterà iTextSharp come dipendenza per la destinazione UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>File con estensione nuspec finale

Il file `.nuspec` finale sarà simile al seguente, dove YOUR_NAME deve essere sostituito con un valore appropriato:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>Creare un pacchetto per il componente

Dopo avere completato il file `.nuspec` che fa riferimento a tutti i file da includere nel pacchetto, è possibile eseguire il comando `pack`:

```
nuget pack LoggingLibrary.nuspec
```

Verrà generato `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, verranno visualizzati i contenuti seguenti:

![NuGet Package Explorer che visualizza il pacchetto LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Un file `.nupkg` è solo un file ZIP con un'estensione diversa. È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.


Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Argomenti correlati

- [Informazioni di riferimento sul file con estensione nuspec](../schema/nuspec.md)
- [Pacchetti di simboli](../create-packages/symbol-packages.md)
- [Controllo delle versioni dei pacchetti](../reference/package-versioning.md)
- [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Inclusione di proprietà e destinazioni MSBuild in un pacchetto](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)