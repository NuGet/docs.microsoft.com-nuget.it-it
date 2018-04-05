---
title: Creare pacchetti NuGet di .NET Standard e .NET Framework con Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Procedura dettagliata end-to-end per la creazione di pacchetti NuGet di .NET Standard e .NET Framework con NuGet 3.x e Visual Studio 2015.
keywords: creare un pacchetto, pacchetti .NET Standard, pacchetti .NET Framework
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbe0a0788b5fc9ba37f7db601bd51c3e4f78f5b8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Creare pacchetti .NET Standard e .NET Framework con Visual Studio 2015

**Nota:** Visual Studio 2017 è consigliato per lo sviluppo di librerie .NET Standard. Visual Studio 2015 può funzionare, ma in questa versione gli strumenti .NET Core hanno raggiunto solo lo stato di anteprima. Per utilizzare NuGet 4.x+ e Visual Studio 2017, vedere [Creare e pubblicare un pacchetto con Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md).

La [libreria .NET Standard](/dotnet/articles/standard/library) è una specifica formale delle API .NET che devono essere disponibili in tutti i runtime .NET, per creare in questo modo maggiore uniformità nell'ecosistema .NET. La libreria .NET Standard definisce un set uniforme di API della libreria di classi base per tutte le piattaforme .NET da implementare, indipendentemente dal carico di lavoro. Consente agli sviluppatori di produrre codice utilizzabile in tutti i runtime .NET e riduce, se non elimina, le direttive di compilazione condizionale specifiche della piattaforma nel codice condiviso.

Questa guida illustra la creazione di un pacchetto NuGet destinato a .NET Standard Library 1.4 o .NET Framework 4.6. Una libreria .NET Standard 1.4 funziona in .NET Framework 4.6.1, in Universal Windows Platform 10, in .NET Core e in Mono/Xamarin. Per informazioni dettagliate, vedere la [tabella di mapping .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (documentazione di .NET). È possibile scegliere altre versioni della libreria .NET Standard.

## <a name="prerequisites"></a>Prerequisiti

1. Visual Studio 2015 Update 3
1. (Solo .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/)
1. Interfaccia della riga di comando di NuGet. Scaricare la versione più recente di nuget.exe da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta. Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.

    > [!Note]
    > Poiché nuget.exe è di per sé lo strumento dell'interfaccia della riga di comando e non un programma di installazione, assicurarsi di salvare il file scaricato dal browser invece di eseguirlo.

## <a name="create-the-class-library-project"></a>Creare il progetto di libreria di classi

1. In Visual Studio **File > Nuovo > Progetto**, espandere il nodo **Visual C# > Windows**, selezionare **Libreria di classi (portabile)**, modificare il nome in AppLogger e selezionare **OK**.

    ![Creare il nuovo progetto di libreria di classi](media/NetStandard-NewProject.png)

1. Nella finestra di dialogo **Aggiungi libreria di classi portabile** visualizzata selezionare le opzioni per `.NET Framework 4.6` e `ASP.NET Core 1.0`. (Se la destinazione è .NET Framework, è possibile selezionare qualsiasi opzione appropriata.)

1. Se la destinazione è .NET Standard, fare clic con il pulsante destro del mouse su `AppLogger (Portable)` in Esplora soluzioni, scegliere **Proprietà**, selezionare la scheda **Libreria**, quindi selezionare **Imposta come destinazione la piattaforma standard .NET** nella sezione **Destinazione**. Questa azione richiede di confermare l'operazione e in seguito è possibile selezionare `.NET Standard 1.4` (o un'altra versione disponibile) nell'elenco a discesa:

    ![Impostazione della destinazione su .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Fare clic sulla scheda **Compilazione**, impostare **Configurazione** su `Release` e selezionare la casella **File di documentazione XML**.

1. Aggiungere il codice al componente, ad esempio:

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

1. Impostare la configurazione su Versione, compilare il progetto e controllare che nella cartella `bin\Release` vengano creati i file DLL e XML.

## <a name="create-and-update-the-nuspec-file"></a>Creare e aggiornare il file con estensione nuspec

1. Aprire un prompt dei comandi, passare alla cartella contenente la cartella `AppLogger.csproj` (di un livello inferiore rispetto alla posizione del file `.sln`) ed eseguire il comando `spec` di NuGet per creare il file `AppLogger.nuspec` iniziale:

    ```cli
    nuget spec
    ```

1. Aprire `AppLogger.nuspec` in un editor e aggiornarlo in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato. Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verifica un errore durante il passaggio di creazione del pacchetto.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. Aggiungere gli assembly di riferimento al file `.nuspec`, in particolare la DLL della libreria e il file XML IntelliSense:

    Se la destinazione è .NET Standard, le voci vengono visualizzate in modo simile al seguente:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Se la destinazione è .NET Framework, le voci vengono visualizzate in modo simile al seguente:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Compila soluzione** per generare tutti i file per il pacchetto.

### <a name="declaring-dependencies"></a>Dichiarazione delle dipendenze

Se sono presenti dipendenze da altri pacchetti NuGet, elencarle nell'elemento `<dependencies>` del manifesto con gli elementi `<group>`. Ad esempio, per dichiarare una dipendenza da NewtonSoft.Json 8.0.3 o versione successiva, aggiungere quanto segue:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

La sintassi dell'attributo *version* qui indica che la versione 8.0.3 o successiva è accettabile. Per specificare intervalli di versioni diversi, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Aggiunta di un file leggimi

Creare il file `readme.txt`, inserirlo nella cartella radice del progetto e farvi riferimento nel file `.nuspec`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

Visual Studio visualizza il file `readme.txt` quando il pacchetto viene installato in un progetto. Il file non viene visualizzato quando viene installato in progetti .NET Core o per i pacchetti che vengono installati come dipendenza.

## <a name="package-the-component"></a>Creare un pacchetto per il componente

Dopo avere completato il file `.nuspec` che fa riferimento a tutti i file da includere nel pacchetto, è possibile eseguire il comando `pack`:

```cli
nuget pack AppLogger.nuspec
```

Questo codice genera `AppLogger.YOUR_NAME.1.0.0.nupkg`. Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, vengono visualizzati i contenuti seguenti (per .NET Standard):

![NuGet Package Explorer che visualizza il pacchetto AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Un file `.nupkg` è solo un file ZIP con un'estensione diversa. È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.

Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../create-packages/publish-a-package.md).

Si noti che `pack` richiede Mono 4.4.2 su Mac OS X e non funziona nei sistemi Linux. In un Mac è anche necessario convertire i nomi di percorso di Windows nel file `.nuspec` in percorsi di tipo Unix.

## <a name="related-topics"></a>Argomenti correlati

- [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md)
- [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Includere proprietà e destinazioni MSBuild in un pacchetto](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)
- [Pacchetti di simboli](../create-packages/symbol-packages.md)
- [Controllo delle versioni dei pacchetti](../reference/package-versioning.md)
- [Documentazione della libreria .NET Standard](/dotnet/articles/standard/library)
- [Portabilità in .NET Core da .NET Framework](/dotnet/articles/core/porting/index)
