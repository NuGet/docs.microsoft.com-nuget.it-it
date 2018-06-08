---
title: Procedura dettagliata per il ripristino dei pacchetti NuGet con Team Foundation Build
description: Descrizione dettagliata della procedura per il ripristino di pacchetti NuGet con Team Foundation Build (sia TFS che Visual Studio Team Services).
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 1b7dcc351626e60e0444cf1d48b8f09cc23aa157
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817034"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Configurazione del ripristino dei pacchetti con Team Foundation Build

Questo articolo presenta in modo dettagliato le procedure per ripristinare i pacchetti nell'ambito della [compilazione di Team Services](/vsts/build-release/index) per il controllo della versione di Git e Team Services.

Anche se questa procedura dettagliata è specifica per lo scenario d'uso di Visual Studio Team Services, i concetti si applicano anche ad altri sistemi di controllo della versione e di compilazione.

Si applica a:

- Progetti MSBuild personalizzati in esecuzione in qualsiasi versione di TFS
- Team Foundation Server 2012 o versione precedente
- Modelli di processi personalizzati di Team Foundation Build di cui è stata eseguita la migrazione a TFS 2013 o versioni successive
- Modelli del processo di compilazione da cui è stata rimossa la funzionalità di ripristino Nuget

Se si usa Visual Studio Team Services o Team Foundation Server 2013 con i relativi modelli del processo di compilazione, il ripristino automatico dei pacchetti avviene come parte del processo di compilazione.

## <a name="the-general-approach"></a>Approccio generale

Un vantaggio dell'uso di NuGet è la possibilità di usarlo per evitare l'archiviazione dei file binari nel sistema di controllo della versione.

Questo aspetto è particolarmente interessante se si usa un sistema di [controllo della versione distribuito](http://en.wikipedia.org/wiki/Distributed_revision_control) come Git, perché gli sviluppatori devono clonare un intero repository, compresa la cronologia completa, prima di poter lavorare in locale. L'archiviazione dei file binari può causare un aumento significativo delle dimensioni del repository, perché i file binari vengono in genere archiviati senza compressione delta.

NuGet supporta il [ripristino dei pacchetti](../consume-packages/package-restore.md) come parte della compilazione già da molto tempo. L'implementazione precedente presentava un circolo vizioso per i pacchetti che volevano estendere il processo di compilazione, perché NuGet ripristinava i pacchetti durante la compilazione del progetto. MSBuild non consente tuttavia di estendere la compilazione durante la compilazione. Si potrebbe sostenere che è un problema di MSBuild, ma è in effetti un problema intrinseco. A seconda dell'aspetto che è necessario estendere, potrebbe essere troppo tardi effettuarne la registrazione al momento del ripristino del pacchetto.

Per evitare questo problema, è necessario assicurarsi che i pacchetti vengano ripristinati come primo passaggio del processo di compilazione:

```cli
nuget restore path\to\solution.sln
```

Quando il processo di compilazione ripristina i pacchetti prima di compilare il codice, non è necessario archiviare i file `.targets`

> [!Note]
> I pacchetti devono essere creati in modo da consentire il caricamento in Visual Studio. In caso contrario, può essere ancora necessario archiviare i file `.targets` in modo che altri sviluppatori possano semplicemente aprire la soluzione senza dover prima ripristinare i pacchetti.

Il progetto dimostrativo seguente illustra come configurare la compilazione in modo che non sia necessario archiviare le cartelle `packages` e i file `.targets`. Illustra anche come configurare una compilazione automatizzata in Team Foundation Service per questo progetto di esempio.

## <a name="repository-structure"></a>Struttura del repository

Il progetto dimostrativo è un semplice strumento da riga di comando che usa l'argomento della riga di comando per eseguire query in Bing. È destinato a .NET Framework 4 e usa molti dei [pacchetti BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) e [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

La struttura del repository è simile alla seguente:

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

È possibile notare che non sono stati archiviati né la cartella `packages` né qualsiasi file `.targets`.

È stato tuttavia archiviato il file `nuget.exe`, perché è necessario durante la compilazione. Seguendo una convenzione ampiamente diffusa, il file è stato archiviato in una cartella `tools` condivisa.

Il codice sorgente è disponibile nella cartella `src`. Anche se la demo usa una singola soluzione, si può facilmente immaginare che questa cartella possa contenere più di una soluzione.

### <a name="ignore-files"></a>Ignorare i file

> [!Note]
> Esiste attualmente un [bug noto del client NuGet](https://nuget.codeplex.com/workitem/4072) a causa del quale il client aggiunge comunque la cartella `packages` al controllo della versione. La soluzione alternativa consiste nel disabilitare l'integrazione del controllo del codice sorgente. A tale scopo, è necessario un file `Nuget.Config ` nella cartella `.nuget` parallela alla soluzione. Se questa cartella non esiste ancora, è necessario crearla. In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) aggiungere il contenuto seguente:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Per comunicare al sistema di controllo della versione che non si intende archiviare il contenuto delle cartelle **packages**, sono stati anche aggiunti i file da ignorare sia per Git (`.gitignore`) che per il controllo della versione di Team Foundation (`.tfignore`). Questi file descrivono i modelli di file che non si vuole archiviare.

Il file `.gitignore` è simile al seguente:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

Il file `.gitignore` offre [molte potenzialità](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Ad esempio, se in genere non si vuole archiviare il contenuto della cartella `packages`, ma si vogliono rispettare le indicazioni precedenti di archiviare i file `.targets`, è possibile usare la regola seguente:

    packages
    !packages/**/*.targets

Questa regola escluderà tutte le cartelle `packages` ma includerà di nuovo tutti i file `.targets` contenuti. È possibile trovare un modello per i file `.gitignore` su misura per le esigenze degli sviluppatori di Visual Studio [qui](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Il controllo della versione di Team Foundation supporta un meccanismo molto simile tramite il file [tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control). La sintassi è sostanzialmente la stessa:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

Per questa demo, il processo di compilazione viene mantenuto piuttosto semplice. Si creerà un progetto MSBuild che compila tutte le soluzioni assicurandosi che i pacchetti vengano ripristinati prima di compilare le soluzioni.

Questo progetto includerà le tre destinazioni convenzionali `Clean`, `Build` e `Rebuild`, oltre a una nuova destinazione `RestorePackages`.

- Le destinazioni `Build` e `Rebuild` dipendono entrambe da `RestorePackages`. Ciò assicura di poter eseguire sia `Build` che `Rebuild`, nonché di essere certi del ripristino dei pacchetti.
- `Clean`, `Build` e `Rebuild` richiamano la destinazione MSBuild corrispondente in tutti i file di soluzione.
- La destinazione `RestorePackages` richiama `nuget.exe` per ogni file di soluzione. Questa operazione viene eseguita tramite la [funzionalità di invio in batch di MSBuild](/visualstudio/msbuild/msbuild-batching).

Il risultato è il seguente:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>Configurazione di Team Build

Team Build offre vari modelli di processo. Per questa dimostrazione, si usa Team Foundation Service. Le installazioni locali di TFS saranno comunque molto simili.

Per Git e il controllo della versione di Team Foundation sono disponibili modelli diversi di Team Build, pertanto le operazioni seguenti varieranno in base al sistema di controllo della versione in uso. In entrambi i casi, è sufficiente selezionare il file build.proj come progetto da compilare.

Prima di tutto verrà esaminato il modello di processo per Git. Nel modello basato su Git, la compilazione viene selezionata tramite la proprietà `Solution to build`:

![Processo di compilazione per Git](media/PackageRestoreTeamBuildGit.png)

Si noti che questa proprietà è un percorso nel repository. Dato che il file `build.proj` del progetto di esempio si trova nella radice, è stato usato semplicemente `build.proj`. Se si posizionasse il file di compilazione in una cartella denominata `tools`, il valore sarebbe `tools\build.proj`.

Nel modello del controllo della versione di Team Foundation, il progetto viene selezionato tramite la proprietà `Projects`:

![Processo di compilazione per il controllo della versione di Team Foundation](media/PackageRestoreTeamBuildTFVC.png)

A differenza del modello basato su Git, il controllo della versione di Team Foundation supporta le selezioni (il pulsante sul lato destro con tre puntini). Per evitare errori di digitazione, è quindi consigliabile usarle per selezionare il progetto.
