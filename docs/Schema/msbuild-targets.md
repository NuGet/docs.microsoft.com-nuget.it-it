---
title: Pack e restore di NuGet come destinazioni MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: I comandi pack e restore di NuGet possono essere usati direttamente come destinazioni MSBuild con NuGet 4.0 +.
keywords: NuGet e MSBuild, destinazione pack NuGet, destinazione restore NuGet
ms.reviewer:
- karann-msft
ms.openlocfilehash: 169d73709eeb17aade7d99da66bbb4f346f8093f
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Pack e restore di NuGet come destinazioni MSBuild

*NuGet 4.0+*

Con il formato PackageReference, NuGet 4.0 + può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto, invece di usare un file `.nuspec` separato.

Con MSBuild 15.1 +, anche NuGet è un membro di MSBuild di prima classe con le destinazioni `pack` e `restore` come descritto di seguito. Queste destinazioni consentono di usare NuGet come qualsiasi altra attività o destinazione MSBuild. Per NuGet 3.x e versioni precedenti, usare invece i comandi [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) tramite l'interfaccia della riga di comando di NuGet.

## <a name="target-build-order"></a>Ordine di compilazione delle destinazioni

Dato che `pack` e `restore` sono destinazioni MSBuild, è possibile accedervi per ottimizzare il flusso di lavoro. Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averlo creato. È possibile farlo aggiungendo quanto segue nel file di progetto:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

Analogamente, è possibile scrivere un'attività MSBuild, scrivere la propria destinazione e utilizzare proprietà NuGet nell'attività MSBuild.

## <a name="pack-target"></a>Destinazione pack

Quando si usa la destinazione pack, vale a dire `msbuild /t:pack`, MSBuild recupera i relativi input dal file di progetto. La tabella seguente descrive le proprietà di MSBuild che possono essere aggiunte a un file di progetto all'interno del primo nodo `<PropertyGroup>`. È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida. Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [file `.nuspec`](../schema/nuspec.md).

Si noti che le proprietà `Owners` e `Summary` da `.nuspec` non sono supportate con MSBuild.

| Valore di attributo/NuSpec | Proprietà MSBuild | Impostazione predefinita | Note |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) da MSBuild |
| Versione | PackageVersion | Versione | Compatibile con SemVer, ad esempio "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | vuoto | L'impostazione di PackageVersion sovrascrive PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | vuoto | $(VersionSuffix) da MSBuild. L'impostazione di PackageVersion sovrascrive PackageVersionSuffix |
| Autori | Autori | Nome utente dell'utente corrente | |
| Proprietari | N/D | Non presente in NuSpec | |
| Titolo | Titolo | PackageId| |
| Descrizione | Descrizione | "Descrizione del pacchetto" | |
| Copyright | Copyright | vuoto | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| LicenseUrl | PackageLicenseUrl | vuoto | |
| ProjectUrl | PackageProjectUrl | vuoto | |
| IconUrl | PackageIconUrl | vuoto | |
| Tag | PackageTags | vuoto | I tag sono delimitati da punto e virgola. |
| ReleaseNotes | PackageReleaseNotes | vuoto | |
| RepositoryUrl | RepositoryUrl | vuoto | |
| RepositoryType | RepositoryType | vuoto | |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Riepilogo | Non supportato | | |

### <a name="pack-target-inputs"></a>Input destinazione pack

- IsPackable
- PackageVersion
- PackageId
- Autori
- Descrizione
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>Scenari pack

### <a name="packageiconurl"></a>PackageIconUrl

Come parte della modifica per il [problema NuGet 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` verrà infine modificato in `PackageIconUri` e può essere un percorso relativo a un file di icona che verrà incluso alla radice del pacchetto risultante.

### <a name="output-assemblies"></a>Assembly di output

`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`. I file di output copiati dipendono da quanto fornito da MSBuild dalla destinazione `BuiltOutputProjectGroup`.

Sono disponibili due proprietà di MSBuild che è possibile usare nel file di progetto o nella riga di comando per controllare la destinazione degli assembly di output:

- `IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.
- `BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output. Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.

### <a name="package-references"></a>Riferimenti ai pacchetti

Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Riferimenti da progetto a progetto

I riferimenti da progetto a progetto sono considerati per impostazione predefinita come riferimenti a pacchetti NuGet, ad esempio:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Inclusione di contenuto in un pacchetto

Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente. Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Se si vuole copiare tutto il contenuto sono in cartelle radice specifiche (invece di copiarlo sia in `content` che in `contentFiles`), è possibile usare la proprietà di MSBuild `ContentTargetFolders`, che ha il valore predefinito "content;contentFiles" ma può essere impostata su qualsiasi altro nome di cartella. Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.

`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola. Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto. Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

È disponibile anche una proprietà di MSBuild `$(IncludeContentInPack)`, con valore predefinito `true`. Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.

Altri metadati specifici di pack che è possibile impostare per qualsiasi elemento precedente includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, che impostano i valori ```CopyToOutput``` e ```Flatten``` sulla voce ```contentFiles``` nel file nuspec di output.

> [!Note]
> Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.
>
> Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.

### <a name="includesymbols"></a>IncludeSymbols

Quando si usa `MSBuild /t:pack /p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.

### <a name="includesource"></a>IncludeSource

Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine. Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante. Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.

Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.

### <a name="istool"></a>IsTool

Quando si usa `MSBuild /t:pack /p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`. Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.

### <a name="packing-using-a-nuspec"></a>Creazione di un pacchetto con un file .nuspec

È possibile usare un file `.nuspec` per creare un pacchetto del progetto, a condizione di disporre di un file di progetto per importare `NuGet.Build.Tasks.Pack.targets`, in modo da poter eseguire l'attività pack. Le tre proprietà di MSBuild seguenti sono rilevanti per la creazione di pacchetti con un file `.nuspec`:

1. `NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.
1. `NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore. A causa della modalità di funzionamento dell'analisi della riga di comando di MSBuild, è necessario specificare più proprietà come indicato di seguito: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: percorso di base per il file `.nuspec`.

Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a>Destinazione restore

`MSBuild /t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:

1. Lettura di tutti i riferimenti da progetto a progetto
1. Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione
1. Passaggio dei dati msbuild a NuGet.Build.Tasks.dll
1. Esecuzione di restore
1. Download dei pacchetti
1. Scrittura dei file di asset, delle destinazioni e delle proprietà

### <a name="restore-properties"></a>Ripristino delle proprietà

Possono esistere ulteriori impostazioni di ripristino derivate da proprietà di MSBuild nel file di progetto. I valori possono essere impostati anche dalla riga di comando tramite l'opzione `/p:` (vedere gli esempi riportati di seguito).

| Proprietà | Descrizione |
|--------|--------|
| RestoreSources | Elenco delimitato da punto e virgola delle origini di pacchetti. |
| RestorePackagesPath | Percorso della cartella dei pacchetti dell'utente. |
| RestoreDisableParallel | Consente di limitare i download a uno alla volta. |
| RestoreConfigFile | Percorso per un file `Nuget.Config` da applicare. |
| RestoreNoCache | Se true, consente di evitare l'uso della cache Web. |
| RestoreIgnoreFailedSources | Se true, ignora le origini di pacchetti in errore o mancanti. |
| RestoreTaskAssemblyFile | Percorso di `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti. |
| RestoreOutputPath | Cartella di output. Per impostazione predefinita, la cartella `obj`. |

#### <a name="examples"></a>Esempi

Riga di comando:

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

File di progetto:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a>Output del ripristino

Il ripristino crea i file seguenti nella cartella `obj` di compilazione:

| File | Descrizione |
|--------|--------|
| `project.assets.json` | In precedenza `project.lock.json` |
| `{projectName}.projectFileExtension.nuget.g.props` | Riferimenti alle proprietà di MSBuild contenute nei pacchetti |
| `{projectName}.projectFileExtension.nuget.g.targets` | Riferimenti alle destinazioni di MSBuild contenute nei pacchetti |

### <a name="packagetargetfallback"></a>PackageTargetFallback

L'elemento `PackageTargetFallback` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti. È progettato per consentire ai pacchetti che usano un [TxM](../schema/target-frameworks.md) dotnet di interagire con pacchetti compatibili che non dichiarano un TxM dotnet. Se il progetto usa il TxM dotnet, devono averlo anche tutti i pacchetti da cui il progetto dipende, a meno che non si aggiunga `<PackageTargetFallback>` al progetto, in modo da rendere compatibili con dotnet le piattaforme che non lo sono.

Ad esempio, se il progetto usa il TxM `netstandard1.6` e un pacchetto dipendente contiene solo `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, la compilazione del progetto avrà esito negativo. Se si vuole includere solo quest'ultima DLL, è possibile aggiungere un `PackageTargetFallback` come segue per segnalare che la DLL `portable-net45+win81` è compatibile:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Per dichiarare un fallback per tutte le destinazioni nel progetto, non specificare l'attributo `Condition`. È anche possibile estendere qualsiasi `PackageTargetFallback` esistente includendo `$(PackageTargetFallback)` come illustrato di seguito:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Sostituzione di una libreria da un grafico di ripristino

Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta. Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
