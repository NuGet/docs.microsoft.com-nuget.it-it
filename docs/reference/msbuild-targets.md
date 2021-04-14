---
title: NuGet eseguire il pack e il ripristino come MSBuild destinazioni
description: NuGet pack e restore possono funzionare direttamente come MSBuild destinazioni con NuGet 4.0+.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 47411641db47884f79f2bc9a4aa00035fc79993b
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387374"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet eseguire il pack e il ripristino come MSBuild destinazioni

*NuGet 4.0+*

Con il [formato PackageReference,](../consume-packages/package-references-in-project-files.md) 4.0+ può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto NuGet anziché usare un file `.nuspec` separato.

Con MSBuild 15.1+, è anche un primo livello con le destinazioni NuGet e come descritto di MSBuild `pack` `restore` seguito. Queste destinazioni consentono di usare come si farebbe NuGet con qualsiasi altra attività o MSBuild destinazione. Per istruzioni sulla creazione di NuGet un pacchetto tramite , vedere Creare un pacchetto MSBuild [ NuGet usando MSBuild ](../create-packages/creating-a-package-msbuild.md). (Per NuGet 3.x e versioni precedenti usano invece i [comandi pack](../reference/cli-reference/cli-ref-pack.md) [e restore](../reference/cli-reference/cli-ref-restore.md) tramite l'interfaccia della riga NuGet di comando.

## <a name="target-build-order"></a>Ordine di compilazione delle destinazioni

Poiché `pack` e `restore` sono  MSBuild destinazioni, è possibile accedervi per migliorare il flusso di lavoro. Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo la creazione del pacchetto. È possibile farlo aggiungendo quanto segue nel file di progetto:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Analogamente, è possibile scrivere MSBuild un'attività, scrivere la propria destinazione e utilizzare NuGet le proprietà MSBuild nell'attività.

> [!NOTE]
> `$(OutputPath)` è relativo e prevede che il comando sia in esecuzione dalla radice del progetto.

## <a name="pack-target"></a>Destinazione pack

Per i progetti .NET che usano il formato , l'uso di disegna input dal file di progetto da `PackageReference` usare nella creazione di un `msbuild -t:pack` NuGet pacchetto.

Nella tabella seguente vengono descritte le MSBuild proprietà che è possibile aggiungere a un file di progetto all'interno del primo `<PropertyGroup>` nodo. È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida. Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [ `.nuspec` file](../reference/nuspec.md).

> [!NOTE]
> `Owners` Le `Summary` proprietà e da non sono supportate con `.nuspec` MSBuild .

| nuspecAttributo/valore | Proprietà diMSBuild | Predefinito | Note |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | `$(AssemblyName)` da MSBuild |
| `Version` | `PackageVersion` | Versione | È compatibile con semver, ad esempio `1.0.0` `1.0.0-beta` , o `1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | empty | `PackageVersion`L'impostazione sovrascrive`PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | empty | `$(VersionSuffix)` da MSBuild . Sovrascrittura `PackageVersion` delle impostazioni `PackageVersionSuffix` |
| `Authors` | `Authors` | Nome utente dell'utente corrente | Elenco di autori di pacchetti separati da punto e virgola, corrispondenti ai nomi dei profili nuget.org. Questi vengono visualizzati in Gallery in nuget.org e vengono usati per creare riferimenti incrociati ai NuGet pacchetti da parte degli stessi autori. |
| `Owners` | N/D | Non presente in nuspec | |
| `Title` | `Title` | Il tipo `PackageId` | Titolo del pacchetto facilmente comprensibile per l'utente, usato di solito per la visualizzazione dell'interfaccia utente, ad esempio in nuget.org e in Gestione pacchetti in Visual Studio. |
| `Description` | `Description` | "Descrizione del pacchetto" | Descrizione lunga per l'assembly. Se `PackageDescription` non viene specificato, questa proprietà viene utilizzata anche come descrizione del pacchetto. |
| `Copyright` | `Copyright` | empty | Informazioni sul copyright per il pacchetto. |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo. |
| `license` | `PackageLicenseExpression` | empty | Corrisponde a `<license type="expression">`. Vedere [Creazione di un pacchetto di un'espressione di licenza o di un file di licenza.](#packing-a-license-expression-or-a-license-file) |
| `license` | `PackageLicenseFile` | empty | Percorso di un file di licenza all'interno del pacchetto se si usa una licenza personalizzata o una licenza a cui non è stato assegnato un identificatore SPDX. È necessario creare un pacchetto esplicito del file di licenza a cui si fa riferimento. Corrisponde a `<license type="file">`. Vedere [Creazione di un pacchetto di un'espressione di licenza o di un file di licenza.](#packing-a-license-expression-or-a-license-file) |
| `LicenseUrl` | `PackageLicenseUrl` | empty | L'oggetto `PackageLicenseUrl` è deprecato. In sostituzione usare `PackageLicenseExpression` o `PackageLicenseFile`. |
| `ProjectUrl` | `PackageProjectUrl` | empty | |
| `Icon` | `PackageIcon` | empty | Percorso di un'immagine nel pacchetto da utilizzare come icona del pacchetto. È necessario creare un pacchetto esplicito del file di immagine dell'icona a cui si fa riferimento. Per altre informazioni, vedere [Creazione di un pacchetto di un file di immagine icona](#packing-an-icon-image-file) e [ `icon` metadati.](./nuspec.md#icon) |
| `IconUrl` | `PackageIconUrl` | empty | `PackageIconUrl` è deprecato a favore di `PackageIcon` . Tuttavia, per la migliore esperienza di livello inferiore, è necessario `PackageIconUrl` specificare oltre a `PackageIcon` . |
| `Readme` | `PackageReadmeFile` | empty | È necessario creare un pacchetto esplicito del file Leggimi a cui si fa riferimento.|
| `Tags` | `PackageTags` | empty | Elenco di tag con valori delimitati da punto e virgola che designa il pacchetto. |
| `ReleaseNotes` | `PackageReleaseNotes` | empty | Note sulla versione per il pacchetto. |
| `Repository/Url` | `RepositoryUrl` | empty | URL del repository usato per clonare o recuperare il codice sorgente. Esempio: *https://github.com/ NuGet / NuGet . Client.git*. |
| `Repository/Type` | `RepositoryType` | empty | Tipo di repository. Esempi: `git` (impostazione predefinita), `tfs` . |
| `Repository/Branch` | `RepositoryBranch` | empty | Informazioni facoltative sul ramo del repository. `RepositoryUrl` deve essere specificato anche per includere questa proprietà. Esempio: *master* ( NuGet 4.7.0+). |
| `Repository/Commit` | `RepositoryCommit` | empty | Commit del repository o set di modifiche facoltativo per indicare l'origine su cui è stato compilato il pacchetto. `RepositoryUrl` deve essere specificato anche per includere questa proprietà. Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+). |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | Non supportato | | |

### <a name="pack-target-inputs"></a>Input destinazione pack

| Proprietà | Descrizione |
| - | - |
| `IsPackable` | Valore booleano che specifica se dal progetto può essere creato un pacchetto. Il valore predefinito è `true`. |
| `SuppressDependenciesWhenPacking` | Impostare su `true` per eliminare le dipendenze del pacchetto dal pacchetto NuGet generato. |
| `PackageVersion` | Specifica la versione che avrà il pacchetto risultante. Accetta tutte le forme di NuGet stringa di versione. Il valore predefinito corrisponde al valore di `$(Version)`, vale a dire della proprietà `Version` nel progetto. |
| `PackageId` | Specifica il nome del pacchetto risultante. Se non specificato, l'impostazione predefinita per l'operazione `pack` corrisponde all'uso di `AssemblyName` o del nome della directory come nome del pacchetto. |
| `PackageDescription` | Descrizione lunga del pacchetto per la visualizzazione dell'interfaccia utente. |
| `Authors` | Elenco di autori di pacchetti separati da punti e virgola, corrispondenti ai nomi dei profili nuget.org. Questi elementi vengono visualizzati nella raccolta in nuget.org e vengono usati per creare riferimenti incrociati ai NuGet pacchetti degli stessi autori. |
| `Description` | Descrizione lunga per l'assembly. Se non viene specificato, questa proprietà viene usata anche `PackageDescription` come descrizione del pacchetto. |
| `Copyright` | Informazioni sul copyright per il pacchetto. |
| `PackageRequireLicenseAcceptance` | Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo. Il valore predefinito è `false`. |
| `DevelopmentDependency` | Valore booleano che specifica se il pacchetto è contrassegnato come dipendenza di solo sviluppo, impedendo che il pacchetto venga incluso come dipendenza in altri pacchetti. Con `PackageReference` ( 4.8+), questo flag indica anche che gli asset in fase di compilazione NuGet vengono esclusi dalla compilazione. Per altre informazioni, vedere [Supporto di DevelopmentDependency per PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference). |
| `PackageLicenseExpression` | Identificatore [o espressione di licenza SPDX,](https://spdx.org/licenses/) ad esempio `Apache-2.0` . Per altre informazioni, vedere [Creazione di un pacchetto di un'espressione di licenza o di un file di licenza.](#packing-a-license-expression-or-a-license-file) |
| `PackageLicenseFile` | Percorso di un file di licenza all'interno del pacchetto se si usa una licenza personalizzata o una licenza a cui non è stato assegnato un identificatore SPDX. |
| `PackageLicenseUrl` | L'oggetto `PackageLicenseUrl` è deprecato. In sostituzione usare `PackageLicenseExpression` o `PackageLicenseFile`. |
| `PackageProjectUrl` | |
| `PackageIcon` | Specifica il percorso dell'icona del pacchetto, relativo alla radice del pacchetto. Per altre informazioni, vedere [Creazione di un pacchetto di un file di immagine dell'icona.](#packing-an-icon-image-file) |
| `PackageReleaseNotes` | Note sulla versione per il pacchetto. |
| `PackageReadmeFile` | File Leggimi per il pacchetto. |
| `PackageTags` | Elenco di tag con valori delimitati da punto e virgola che designa il pacchetto. |
| `PackageOutputPath` | Determina il percorso di output in cui verrà rilasciato il pacchetto creato. Il valore predefinito è `$(OutputPath)`. |
| `IncludeSymbols` | Valore booleano che indica se al momento della creazione del pacchetto deve essere creato un pacchetto aggiuntivo di simboli. Il formato del pacchetto di simboli è controllato dalla proprietà `SymbolPackageFormat`. Per altre informazioni, vedere [IncludeSymbols](#includesymbols). |
| `IncludeSource` | Valore booleano che indica se il processo di creazione del pacchetto deve creare un pacchetto di origine. Il pacchetto di origine contiene il codice sorgente della libreria, nonché i file PDB. I file di origine vengono posizionati nella directory `src/ProjectName` del file del pacchetto risultante. Per altre informazioni, vedere [IncludeSource.](#includesource) |
| `PackageType` | |
| `IsTool` | Specifica se tutti i file di output devono essere copiati nella cartella *tools* anziché nella cartella *lib*. Per altre informazioni, vedere [IsTool](#istool). |
| `RepositoryUrl` | URL del repository usato per clonare o recuperare il codice sorgente. Esempio: *https://github.com/ NuGet / NuGet . Client.git*. |
| `RepositoryType` | Tipo di repository. Esempi: `git` (impostazione predefinita), `tfs` . |
| `RepositoryBranch` | Informazioni facoltative sul ramo del repository. `RepositoryUrl` È inoltre necessario specificare per includere questa proprietà. Esempio: *master* ( NuGet 4.7.0+). |
| `RepositoryCommit` | Commit del repository o insieme di modifiche facoltativo per indicare l'origine in base alla quale è stato compilato il pacchetto. `RepositoryUrl` È inoltre necessario specificare per includere questa proprietà. Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+). |
| `SymbolPackageFormat` | Specifica il formato del pacchetto di simboli. Se "symbols.nupkg", viene creato un pacchetto di simboli legacy con estensione *symbols.nupkg* contenente file PDB, DLL e altri file di output. Se "snupkg", viene creato un pacchetto di simboli snupkg contenente i PDB portatili. Il valore predefinito è "symbols.nupkg". |
| `NoPackageAnalysis` | Specifica che non deve `pack` eseguire l'analisi del pacchetto dopo la compilazione del pacchetto. |
| `MinClientVersion` | Specifica la versione minima del client in grado di installare questo pacchetto, applicata da nuget.exe NuGet e dal Visual Studio Gestione pacchetti. |
| `IncludeBuildOutput` | Questo valore booleano specifica se gli assembly di output di compilazione devono essere suddivisi o meno nel file con estensione *nupkg.* |
| `IncludeContentInPack` | Questo valore booleano specifica se eventuali elementi di tipo vengono `Content` inclusi automaticamente nel pacchetto risultante. Il valore predefinito è `true`. |
| `BuildOutputTargetFolder` | Specifica la cartella in cui inserire gli assembly di output. Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework. Per altre informazioni, vedere [Assembly di output.](#output-assemblies) |
| `ContentTargetFolders` | Specifica il percorso predefinito di tutti i file di contenuto se `PackagePath` non è specificato. Il valore predefinito è "content;contentFiles". Per altre informazioni, vedere [Including content in a package](#including-content-in-a-package) (Includere contenuto in un pacchetto). |
| `NuspecFile` | Percorso relativo o assoluto del *.nuspec* file utilizzato per la creazione di un pacchetto. Se specificato, viene usato esclusivamente per **la** creazione di pacchetti di informazioni e le informazioni nei progetti non vengono usate. Per altre informazioni, vedere [Packing using a .nuspec ](#packing-using-a-nuspec-file). |
| `NuspecBasePath` | Percorso di base per il *.nuspec* file. Per altre informazioni, vedere [Packing using a .nuspec ](#packing-using-a-nuspec-file). |
| `NuspecProperties` | Elenco con valori delimitati da punto e virgola di coppie chiave=valore. Per altre informazioni, vedere [Creazione di un pacchetto tramite . .nuspec ](#packing-using-a-nuspec-file) |

## <a name="pack-scenarios"></a>Scenari pack

### <a name="suppressing-dependencies"></a>Eliminazione delle dipendenze

Per eliminare le dipendenze del pacchetto dal pacchetto generato, impostare su che consentirà di ignorare tutte le dipendenze NuGet `SuppressDependenciesWhenPacking` dal file `true` nupkg generato.

### `PackageIconUrl`

`PackageIconUrl` è deprecato a favore della [`PackageIcon`](#packageicon) proprietà . A partire dalla NuGet versione 5.3 e Visual Studio 2019 versione 16.3, genera l'avviso `pack` [NU5048](./errors-and-warnings/nu5048.md) se i metadati del pacchetto specificano solo `PackageIconUrl` .

### `PackageIcon`

> [!Tip]
> Per mantenere la compatibilità con le versioni precedenti con client e origini che non supportano ancora `PackageIcon` , specificare sia che `PackageIcon` `PackageIconUrl` . Visual Studio per i `PackageIcon` pacchetti provenienti da un'origine basata su cartelle.

#### <a name="packing-an-icon-image-file"></a>Creazione di un pacchetto di un file di immagine dell'icona

Quando si imballa un file di immagine dell'icona, usare la proprietà per specificare il percorso del `PackageIcon` file dell'icona, relativo alla radice del pacchetto. Assicurarsi inoltre che il file sia incluso nel pacchetto. Le dimensioni del file di immagine sono limitate a 1 MB. I formati di file supportati includono JPEG e PNG. È consigliabile una risoluzione dell'immagine di 128x128.

Ad esempio:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Esempio di icona del pacchetto](https://github.com/NuGet/Samples/tree/main/PackageIconExample).

Per nuspec l'equivalente, esaminare il riferimento [ nuspec per l'icona](nuspec.md#icon).

### <a name="packagereadmefile"></a>PackageReadmeFile

Quando si esegue il pacchetto di un file Leggimi, è necessario usare la proprietà per specificare il percorso del pacchetto, relativo alla `PackageReadmeFile` radice del pacchetto. Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto. I formati di file supportati includono solo Markdown (*md*).

Ad esempio:

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

Per nuspec l'equivalente, esaminare il riferimento [ nuspec per il file Leggimi](nuspec.md#readme).

### <a name="output-assemblies"></a>Assembly di output

`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`. I file di output copiati dipendono dagli elementi MSBuild forniti dalla `BuiltOutputProjectGroup` destinazione.

Esistono due proprietà che è possibile usare nel file di progetto o nella riga di comando per controllare la MSBuild  posizione degli assembly di output:

- `IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.
- `BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output. Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.

### <a name="package-references"></a>Riferimenti ai pacchetti

Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Riferimenti da progetto a progetto

I riferimenti da progetto a progetto vengono considerati per impostazione predefinita come NuGet riferimenti al pacchetto. Ad esempio:

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

Se si vuole copiare tutto il contenuto solo in una o più cartelle radice specifiche (anziché in entrambe), è possibile usare la proprietà , che per impostazione predefinita è `content` `contentFiles` MSBuild "content;contentFiles", ma può essere impostata su qualsiasi altro nome `ContentTargetFolders` di cartella. Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.

`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola. Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto. Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

È anche disponibile una MSBuild proprietà , che per impostazione predefinita è `$(IncludeContentInPack)` `true` . Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.

Altri metadati specifici di tipo pack che è possibile impostare per uno degli elementi precedenti includono e che impostano i valori e ```<PackageCopyToOutput>``` ```<PackageFlatten>``` sulla voce ```CopyToOutput``` ```Flatten``` ```contentFiles``` nell'output nuspec .

> [!Note]
> Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.
>
> Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.

### <a name="includesymbols"></a>IncludeSymbols

Quando si usa `MSBuild -t:pack -p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.

### <a name="includesource"></a>IncludeSource

Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine. Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante. Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.

Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Creazione di un pacchetto di un'espressione di licenza o di un file di licenza

Quando si usa un'espressione di licenza, usare la `PackageLicenseExpression` proprietà . Per un esempio, vedere [l'esempio di espressione di licenza](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Per altre informazioni sulle espressioni di licenza e sulle licenze accettate da NuGet .org, vedere Metadati [delle licenze.](nuspec.md#license)

Quando si esegue il pacchetto di un file di licenza, usare la proprietà per specificare il percorso del `PackageLicenseFile` pacchetto, relativo alla radice del pacchetto. Assicurarsi inoltre che il file sia incluso nel pacchetto. Ad esempio:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Per un esempio, vedere [l'esempio di file di licenza](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).

> [!NOTE]
> È possibile `PackageLicenseExpression` specificare solo uno di , e alla `PackageLicenseFile` `PackageLicenseUrl` volta.

### <a name="packing-a-file-without-an-extension"></a>Creazione di un pacchetto di un file senza estensione

In alcuni scenari, ad esempio quando si imballa un file di licenza, è possibile includere un file senza estensione.
Per motivi cronologici, NuGet  &  MSBuild considerare i percorsi senza un'estensione come directory.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[File senza un esempio di estensione](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).

### <a name="istool"></a>IsTool

Quando si usa `MSBuild -t:pack -p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`. Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.

### <a name="packing-using-a-nuspec-file"></a>Creazione di un pacchetto con un `.nuspec` file

Anche se è [consigliabile](../reference/msbuild-targets.md#pack-target) includere tutte le proprietà che in genere si trovano nel file nel file di progetto, è possibile scegliere di usare un file per il pacchetto `.nuspec` del `.nuspec` progetto. Per un progetto non di tipo SDK che usa , è necessario importare in modo che sia possibile eseguire l'attività di `PackageReference` `NuGet.Build.Tasks.Pack.targets` tipo pack. È comunque necessario ripristinare il progetto prima di poter imballare un nuspec file. Un progetto di tipo SDK include le destinazioni di tipo pack per impostazione predefinita.

Il framework di destinazione del file di progetto non è pertinente e non viene usato quando si imballa un oggetto nuspec . Le tre proprietà MSBuild seguenti sono rilevanti per la creazione di un pacchetto tramite `.nuspec` :

1. `NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.
1. `NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore. A causa del funzionamento dell'analisi della riga di comando, è necessario MSBuild specificare più proprietà nel modo seguente: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: percorso di base per il file `.nuspec`.

Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Si noti che la creazione di un oggetto using dotnet.exe o msbuild comporta anche nuspec la compilazione del progetto per impostazione predefinita. Questa operazione può essere evitata passando la proprietà a dotnet.exe, che equivale all'impostazione nel file di progetto, insieme all'impostazione ```--no-build``` ```<NoBuild>true</NoBuild> ``` nel file di ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` progetto.

Un esempio di file *con estensione csproj* per il pacchetto di nuspec un file è:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Punti di estensione avanzati per creare un pacchetto personalizzato

La `pack` destinazione fornisce due punti di estensione che vengono eseguiti nella compilazione interna specifica del framework di destinazione. I punti di estensione supportano inclusi il contenuto e gli assembly specifici del framework di destinazione in un pacchetto:

- `TargetsForTfmSpecificBuildOutput` target: usare per i file all'interno `lib` della cartella o di una cartella specificata tramite `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` target: usare per i file all'esterno di `BuildOutputTargetFolder` .

#### `TargetsForTfmSpecificBuildOutput`

Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificBuildOutput)` proprietà . Per tutti i file che devono accedere a (lib per impostazione predefinita), la destinazione deve scrivere tali file in ItemGroup e impostare `BuildOutputTargetFolder` i due valori di metadati `BuildOutputInPackage` seguenti:

- `FinalOutputPath`: percorso assoluto del file. Se non viene specificato, l'identità viene usata per valutare il percorso di origine.
- `TargetPath`: (Facoltativo) Impostare quando il file deve essere inserito in una sottocartella all'interno di , ad esempio gli assembly satellite che si trova `lib\<TargetFramework>` nelle rispettive cartelle delle impostazioni cultura. Il valore predefinito è il nome del file.

Esempio:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### `TargetsForTfmSpecificContentInPackage`

Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificContentInPackage)` proprietà . Per tutti i file da includere nel pacchetto, la destinazione deve scrivere tali file in ItemGroup e `TfmSpecificPackageFile` impostare i metadati facoltativi seguenti:

- `PackagePath`: percorso in cui deve essere restituito il file nel pacchetto. NuGet viene generato un avviso se più file vengono aggiunti allo stesso percorso del pacchetto.
- `BuildAction`: azione di compilazione da assegnare al file, necessaria solo se il percorso del pacchetto si trova nella `contentFiles` cartella . Il valore predefinito è "None".

Esempio:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>Destinazione restore

`MSBuild -t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:

1. Lettura di tutti i riferimenti da progetto a progetto
1. Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione
1. Passare MSBuild dati a NuGet.Build.Tasks.dll
1. Esecuzione di restore
1. Download dei pacchetti
1. Scrittura dei file di asset, delle destinazioni e delle proprietà

La `restore` destinazione funziona per i progetti che usano il formato PackageReference.
`MSBuild 16.5+` include anche [il supporto del consenso](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) esplicito per il `packages.config` formato.

> [!NOTE]
> La `restore` destinazione non deve essere [eseguita](#restoring-and-building-with-one-msbuild-command) in combinazione con la `build` destinazione .

### <a name="restore-properties"></a>Ripristino delle proprietà

Le impostazioni di ripristino aggiuntive possono MSBuild derivare dalle proprietà nel file di progetto. I valori possono essere impostati anche dalla riga di comando tramite l'opzione `-p:` (vedere gli esempi riportati di seguito).

| Proprietà | Descrizione |
|--------|--------|
| `RestoreSources` | Elenco delimitato da punto e virgola delle origini di pacchetti. |
| `RestorePackagesPath` | Percorso della cartella dei pacchetti dell'utente. |
| `RestoreDisableParallel` | Consente di limitare i download a uno alla volta. |
| `RestoreConfigFile` | Percorso per un file `Nuget.Config` da applicare. |
| `RestoreNoCache` | Se true, evita l'uso di pacchetti memorizzati nella cache. Vedere [Gestione dei pacchetti globali e delle cartelle della cache.](../consume-packages/managing-the-global-packages-and-cache-folders.md) |
| `RestoreIgnoreFailedSources` | Se true, ignora le origini di pacchetti in errore o mancanti. |
| `RestoreFallbackFolders` | Cartelle di fallback, usate nello stesso modo in cui viene usata la cartella dei pacchetti utente. |
| `RestoreAdditionalProjectSources` | Origini aggiuntive da usare durante il ripristino. |
| `RestoreAdditionalProjectFallbackFolders` | Cartelle di fallback aggiuntive da usare durante il ripristino. |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | Esclude le cartelle di fallback specificate in `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | Percorso di `NuGet.Build.Tasks.dll`. |
| `RestoreGraphProjectInput` | Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti. |
| `RestoreUseSkipNonexistentTargets`  | Quando i progetti vengono raccolti tramite MSBuild , determina se vengono raccolti usando l'ottimizzazione. `SkipNonexistentTargets` Se non è impostato, il valore predefinito è `true` . La conseguenza è un comportamento fail-fast quando non è possibile importare le destinazioni di un progetto. |
| `MSBuildProjectExtensionsPath` | Cartella di output, che per impostazione predefinita `BaseIntermediateOutputPath` è e la cartella `obj` . |
| `RestoreForce` | Nei progetti basati su PackageReference, forza la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo. La specifica di questo flag è simile all'eliminazione del `project.assets.json` file. In questo modo non viene ignorata la http-cache. |
| `RestorePackagesWithLockFile` | Acconsente esplicitamente all'uso di un file di blocco. |
| `RestoreLockedMode` | Eseguire il ripristino in modalità bloccata. Ciò significa che il ripristino non rivaluta le dipendenze. |
| `NuGetLockFilePath` | Percorso personalizzato per il file di blocco. Il percorso predefinito è accanto al progetto ed è denominato `packages.lock.json` . |
| `RestoreForceEvaluate` | Forza il ripristino per ricalcolare le dipendenze e aggiornare il file di blocco senza alcun avviso. |
| `RestorePackagesConfig` | Opzione di consenso esplicito che ripristina i progetti con packages.config. Supporto solo `MSBuild -t:restore` con . |
| `RestoreUseStaticGraphEvaluation` | Opzione di consenso esplicito per l'uso della valutazione a MSBuild grafo statico anziché della valutazione standard. La valutazione dei grafi statici è una funzionalità sperimentale notevolmente più veloce per i repository e le soluzioni di grandi dimensioni. |

#### <a name="examples"></a>Esempio

Riga di comando:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

File di progetto:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Output del ripristino

Il ripristino crea i file seguenti nella cartella `obj` di compilazione:

| File | Descrizione |
|--------|--------|
| `project.assets.json` | Contiene il grafico delle dipendenze di tutti i riferimenti al pacchetto. |
| `{projectName}.projectFileExtension.nuget.g.props` | Riferimenti alle MSBuild proprietà contenute nei pacchetti |
| `{projectName}.projectFileExtension.nuget.g.targets` | Riferimenti alle MSBuild destinazioni contenute nei pacchetti |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Ripristino e compilazione con MSBuild un comando

A causa del fatto che può ripristinare pacchetti che portano a destinazione e proprietà, le valutazioni di ripristino e compilazione vengono eseguite NuGet MSBuild con proprietà globali diverse.
Ciò significa che quanto segue avrà un comportamento imprevedibile e spesso errato.

```cli
msbuild -t:restore,build
```

 L'approccio consigliato è invece:

```cli
msbuild -t:build -restore
```

La stessa logica si applica ad altre destinazioni simili a `build` .

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>Ripristino di PackageReference e packages.config progetti con MSBuild

Con MSBuild la versione 16.5+, packages.config sono supportati anche per `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore è disponibile solo con `MSBuild 16.5+` e non con `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Ripristino con valutazione MSBuild di grafi statici

> [!NOTE]
> Con MSBuild la versione 16.6+, è stata aggiunta una funzionalità sperimentale per usare la valutazione del grafo statico dalla riga di comando che migliora significativamente il tempo di ripristino per repository NuGet di grandi dimensioni.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

In alternativa, è possibile abilitarlo impostando la proprietà in un oggetto Directory.Build.Props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> A Visual Studio 2019.x e 5.x, questa funzionalità è considerata sperimentale e NuGet acconsente esplicitamente. Seguire [ NuGet /Home#9803](https://github.com/NuGet/Home/issues/9803) per informazioni dettagliate su quando questa funzionalità verrà abilitata per impostazione predefinita.

Il ripristino a grafo statico modifica la parte msbuild del ripristino, la lettura e la valutazione del progetto, ma non l'algoritmo di ripristino. L'algoritmo di ripristino è lo stesso in tutti gli NuGet strumenti ( NuGet exe, MSBuild exe, dotnet.exe e Visual Studio).

In pochissimi scenari, il ripristino di grafi statici può comportarsi in modo diverso dal ripristino corrente e alcuni PackageReference o ProjectReference dichiarati potrebbero risultare mancanti.

Per semplificare l'esecuzione, come controllo una sola volta, quando si esegue la migrazione al ripristino statico dei grafi, è consigliabile eseguire:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet non *deve segnalare* alcuna modifica. Se viene visualizzata una discrepanza, determinare un problema in [ NuGet /Home](https://github.com/nuget/home/issues/new).

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