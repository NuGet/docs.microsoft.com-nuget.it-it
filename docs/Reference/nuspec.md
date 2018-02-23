---
title: Informazioni di riferimento sul file .nuspec per NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Il file. nuspec contiene i metadati del pacchetto usati per la compilazione e per fornire informazioni ai consumer del pacchetto.
keywords: informazioni di riferimento su nuspec, metadati dei pacchetti NuGet, manifesto dei pacchetti NuGet, schema di nuspec
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: c52d0a7c0da507cb9688c8a7b2c4eaf54a8ca5c2
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2018
---
# <a name="nuspec-reference"></a>Informazioni di riferimento sul file .nuspec

Un file `.nuspec` è un manifesto XML che contiene i metadati del pacchetto. Questo manifesto viene usato per compilare il pacchetto e per fornire informazioni ai consumer. Il manifesto viene sempre incluso in un pacchetto.

In questo argomento

- [Formato generale e schema](#general-form-and-schema)
- [Token di sostituzione](#replacement-tokens) (usati con un progetto di Visual Studio)
- [Dipendenze](#dependencies)
- [Riferimenti espliciti agli assembly](#explicit-assembly-references)
- [Riferimenti agli assembly del framework](#framework-assembly-references)
- [Inclusione di file di assembly](#including-assembly-files)
- [Inclusione di file di contenuto](#including-content-files)
- [Esempi](#examples)

## <a name="general-form-and-schema"></a>Formato generale e schema

Il file dello schema di `nuspec.xsd` corrente è disponibile nel [repository GitHub di NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

All'interno di questo schema, un file `.nuspec` ha il formato generale seguente:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Per una rappresentazione visiva chiara dello schema, aprire il file di schema in Visual Studio in modalità progettazione e fare clic sul collegamento **XML Schema Explorer**. In alternativa, aprire il file come codice, fare clic con il pulsante destro del mouse nell'editor e scegliere **Mostra in XML Schema Explorer**. In entrambi i casi si ottiene una visualizzazione simile alla seguente (quando è per la maggior parte espansa):

![Visual Studio Schema Explorer con nuspec.xsd aperto](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a>Attributi dei metadati

L'elemento `<metadata>` supporta gli attributi descritti nella tabella seguente.

| Attributo | Obbligatorio | Descrizione |
| --- | --- | --- | 
| **minClientVersion** | No | Specifica la versione minima del client NuGet, imposta da nuget.exe e da Gestione pacchetti di Visual Studio, che può installare questo pacchetto. Questo attributo viene usato ogni volta che il pacchetto dipende da funzionalità specifiche del file `.nuspec` aggiunte in una particolare versione del client NuGet. Ad esempio, un pacchetto che usa l'attributo `developmentDependency` deve specificare "2.8" per `minClientVersion`. Analogamente, un pacchetto che usa l'elemento `contentFiles` (vedere la sezione successiva) deve impostare `minClientVersion` su "3.3". Si noti che poiché i client NuGet prima della versione 2.5 non riconoscono questo flag, essi rifiutano *sempre* di installare il pacchetto indipendentemente dal contenuto di `minClientVersion`. |

### <a name="required-metadata-elements"></a>Elementi dei metadati obbligatori

Anche se gli elementi seguenti sono i requisiti minimi per un pacchetto, è consigliabile aggiungere gli [elementi dei metadati facoltativi](#optional-metadata-elements) per migliorare l'esperienza complessiva degli sviluppatori con il pacchetto.

Questi elementi devono essere visualizzati all'interno di un elemento `<metadata>`.

| Elemento | Descrizione |
| --- | --- |
| **ID** | Identificatore del pacchetto senza distinzione tra maiuscole e minuscole che deve essere univoco in nuget.org o in qualsiasi raccolta in cui risiede il pacchetto. L'ID non può contenere spazi o caratteri non validi per un URL e in genere segue le regole dello spazio dei nomi .NET. Vedere [Choosing a unique package identifier and setting the version number](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) (Scelta di un identificatore univoco del pacchetto e impostazione del numero di versione) per altre indicazioni. |
| **version** | La versione del pacchetto secondo il criterio *principale.secondaria.patch*. I numeri di versione possono includere un suffisso di versione non definitiva, come descritto in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#pre-release-versions). |
| **description** | Descrizione lunga del pacchetto per la visualizzazione dell'interfaccia utente. |
| **authors** | Elenco con valori delimitati da virgola di autori di pacchetti, corrispondenti ai nomi di profili in nuget.org. Questi, visualizzati nella raccolta NuGet in nuget.org, vengono usati per creare riferimenti incrociati ai pacchetti dello stesso autore. |

### <a name="optional-metadata-elements"></a>Elementi dei metadati facoltativi

Questi elementi possono essere visualizzati all'interno di un elemento `<metadata>`.

#### <a name="single-elements"></a>Singoli elementi

| Elemento | Descrizione |
| --- | --- |
| **title** | Titolo del pacchetto facilmente comprensibile per l'utente, usato di solito per la visualizzazione dell'interfaccia utente, ad esempio in nuget.org e in Gestione pacchetti in Visual Studio. Se non specificato, viene usato l'ID del pacchetto. |
| **owners** | Elenco con valori delimitati da virgola di autori di pacchetti, corrispondenti ai nomi di profili in nuget.org. Si tratta spesso dello stesso elenco in `authors` e viene ignorato durante il caricamento del pacchetto in nuget.org. Vedere [Gestione dei proprietari dei pacchetti in nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). |
| **projectUrl** | URL della pagina iniziale del pacchetto, spesso visualizzato nell'interfaccia utente e in nuget.org. |
| **licenseUrl** | URL della licenza del pacchetto, spesso visualizzato nell'interfaccia utente e in nuget.org. |
| **iconUrl** | URL di un'immagine 64x64 con sfondo trasparente da usare come icona per il pacchetto nella visualizzazione dell'interfaccia utente. Assicurarsi che questo elemento contenga l'*URL diretto dell'immagine* e non l'URL di una pagina Web contenente l'immagine. Ad esempio, per utilizzare un'immagine da GitHub, utilizzare il file non elaborato URL *https://github.com/\<username\>/\<repository\>/raw/\<ramo\> / \<logo.png\>*. |
| **requireLicenseAcceptance** | Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo. |
| **developmentDependency** | *(2.8 +)*  Valore booleano che specifica se il pacchetto deve essere contrassegnato come dipendenza solo per lo sviluppo, in modo che il pacchetto non possa essere incluso come dipendenza in altri pacchetti. |
| **summary** | Descrizione breve del pacchetto per la visualizzazione dell'interfaccia utente. Se omesso, viene usata una versione troncata di `description`. |
| **releaseNotes** | *(1.5+)* Descrizione delle modifiche apportate in questa versione del pacchetto, spesso usata nell'interfaccia utente, come la scheda **Aggiornamenti** di Gestione pacchetti di Visual Studio, in sostituzione della descrizione del pacchetto. |
| **copyright** | *(1.5+)* Informazioni sul copyright per il pacchetto. |
| **linguaggio** | ID delle impostazioni locali per il pacchetto. Vedere [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md). |
| **tags** | Elenco di tag e parole chiave delimitati da spazi che descrivono il pacchetto e facilitano l'individuabilità dei pacchetti tramite meccanismi di ricerca e filtro. |
| **serviceable** | *(3.3+)* Solo per uso interno in NuGet. |

#### <a name="collection-elements"></a>Elementi di raccolta

| Elemento | Descrizione |
| --- | --- |
**packageTypes** | *(3.5 +)* Raccolta di zero o più elementi `<packageType>` che specificano il tipo del pacchetto se diverso da un pacchetto di dipendenza tradizionale. Ogni packageType include gli attributi di *name* e *version*. Vedere [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type) (Impostazione di un tipo di pacchetto). |
| **dependencies** | Raccolta di zero o più elementi `<dependency>` che specificano le dipendenze per il pacchetto. Ogni dipendenza include gli attributi *id*, *version*, *include* (3.x+) ed *exclude* (3.x+). Vedere [Dipendenze](#dependencies) di seguito. |
| **frameworkAssemblies** | *(1.2 +)* Raccolta di zero o più elementi `<frameworkAssembly>` che identificano i riferimenti ad assembly .NET Framework richiesti dal pacchetto. Ciò assicura che i riferimenti vengano aggiunti ai progetti che utilizzano il pacchetto. Ogni frameworkAssembly include gli attributi *assemblyName* e *targetFramework*. Vedere [Riferimenti agli assembly del framework](#specifying-framework-assembly-references-gac) più avanti. |
| **references** | *(1.5 +)* Raccolta di zero o più elementi `<reference>` per la denominazione degli assembly nella cartella `lib` del pacchetto, aggiunti come riferimenti al progetto. Ogni riferimento include un attributo *file*. `<references>` può anche contenere un elemento `<group>` con un attributo *targetFramework*, che contiene a sua volta elementi `<reference>`. Se omesso, vengono inclusi tutti i riferimenti in `lib`. Vedere [Riferimenti espliciti agli assembly](#specifying-explicit-assembly-references) più avanti. |
| **contentFiles** | *(3.3 +)* Raccolta di elementi `<files>` che identificano i file di contenuto da includere nel progetto che utilizza il pacchetto. Questi file sono specificati con un set di attributi che descrivono come devono essere usati all'interno del sistema del progetto. Vedere [Inclusione di file di assembly](#specifying-files-to-include-in-the-package) più avanti. |

### <a name="files-element"></a>Files (elemento)

Il nodo `<package>` può contenere un nodo `<files>` come elemento di pari livello di `<metadata>` e/o un elemento `<contentFiles>` in `<metadata>` per specificare quali file di assembly e di contenuto includere nel pacchetto. Vedere [Inclusione di file di assembly](#including-assembly-files) e [Inclusione di file di contenuto](#including-content-files) più avanti in questo argomento per ulteriori dettagli.

## <a name="replacement-tokens"></a>Token di sostituzione

Quando si crea un pacchetto, il [comando `nuget pack`](../tools/cli-ref-pack.md) sostituisce i token delimitati da $ nel nodo `<metadata>` del file `.nuspec` con valori provenienti da un file di progetto o dall'opzione `-properties` del comando `pack`.

Nella riga di comando, i valori dei token vengono specificati con `nuget pack -properties <name>=<value>;<name>=<value>`. Ad esempio, è possibile usare un token come `$owners$` e `$desc$` nel file `.nuspec` e specificare i valori al momento della creazione del pacchetto come indicato di seguito:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Per usare valori da un progetto, specificare il token descritto nella tabella riportata di seguito (AssemblyInfo fa riferimento al file in `Properties`, ad esempio `AssemblyInfo.cs` o `AssemblyInfo.vb`).

Per usare questi token, eseguire `nuget pack` con il file di progetto anziché semplicemente il file `.nuspec`. Ad esempio, quando si usa il comando seguente, i token `$id$` e `$version$` in un file `.nuspec` vengono sostituiti con i valori `AssemblyName` e `AssemblyVersion` del progetto:

```ps
nuget pack MyProject.csproj
```

In genere, quando si dispone di un progetto, si crea inizialmente il file `.nuspec` con `nuget spec MyProject.csproj`, che include automaticamente alcuni di questi token standard. Tuttavia, se un progetto non include i valori per elementi `.nuspec` obbligatori, `nuget pack` ha esito negativo. Inoltre, se si modificano i valori del progetto, assicurarsi di ricompilare prima di creare il pacchetto. Questa operazione può essere eseguita facilmente con l'opzione `build` del comando pack.

Ad eccezione di `$configuration$`, i valori nel progetto vengono usati preferenzialmente rispetto a qualsiasi altro valore assegnato allo stesso token nella riga di comando.

| Token | Origine del valore | Valore
| --- | --- | ---
| **$id$** | File di progetto | AssemblyName dal file di progetto |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion se presente, in caso contrario AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | DLL dell'assembly | Configurazione usata per compilare l'assembly, con impostazione predefinita Debug. Si noti che per creare un pacchetto con la configurazione Rilascio, è sempre necessario usare `-properties Configuration=Release` nella riga di comando. |

I token possono essere usati anche per risolvere i percorsi quando si includono [file di assembly](#including-assembly-files) e [file di contenuto](#including-content-files). I token hanno gli stessi nomi delle proprietà di MSBuild e ciò consente di selezionare i file da includere a seconda della configurazione di compilazione corrente. Ad esempio, se si usano i token seguenti nel file `.nuspec`:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

E si compila un assembly il cui `AssemblyName` è `LoggingLibrary` con la configurazione `Release` in MSBuild, le righe risultanti nel file `.nuspec` nel pacchetto sono le seguenti:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a>Dipendenze

L'elemento `<dependencies>` all'interno di `<metadata>` contiene qualsiasi numero di elementi `<dependency>` che identificano altri pacchetti da cui dipende il pacchetto di livello superiore. Gli attributi per ogni `<dependency>` sono i seguenti:

| Attributo | Descrizione |
| --- | --- |
| `id` | (Obbligatorio) ID pacchetto della dipendenza, ad esempio "EntityFramework" e "NUnit", ovvero il nome di pacchetto che nuget.org mostra nella pagina di un pacchetto. |
| `version` | (Obbligatorio) Intervallo di versioni accettabili come dipendenza. Per la sintassi esatta, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards). |
| include | Elenco delimitato da virgole di tag di inclusione/esclusione (vedere di seguito) che indicano la dipendenza da includere nel pacchetto finale. Il valore predefinito è `none`. |
| exclude | Elenco delimitato da virgole di tag di inclusione/esclusione (vedere di seguito) che indicano la dipendenza da escludere nel pacchetto finale. Il valore predefinito è `all`. I tag specificati con `exclude` hanno la precedenza rispetto a quelli specificati con `include`. Ad esempio, `include="runtime, compile" exclude="compile"` equivale a `include="runtime"`. |

| Tag di inclusione/esclusione | Cartelle di destinazione interessate |
| --- | --- |
| contentFiles | Content  |
| runtime | Runtime, Resources e FrameworkAssemblies  |
| compile | lib |
| build | build (proprietà e destinazioni MSBuild) |
| native | native |
| none | Nessuna cartella |
| tutti | Tutte le cartelle |

Ad esempio, le righe seguenti indicano dipendenze da `PackageA` versione 1.1.0 o successive e da `PackageB` versione 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Le righe seguenti indicano dipendenze dagli stessi pacchetti, ma specificano di includere le cartelle `contentFiles` e `build` di `PackageA` e tutte le cartelle tranne `native` e `compile` di `PackageB`.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Nota: quando si crea un file `.nuspec` da un progetto tramite `nuget spec`, le dipendenze esistenti in tale progetto vengono incluse automaticamente nel file `.nuspec` risultante.

### <a name="dependency-groups"></a>Gruppi di dipendenze

*Versione 2.0+*

In alternativa a un unico elenco semplice, è possibile specificare le dipendenze in base al profilo del framework del progetto di destinazione usando elementi `<group>` all'interno di `<dependencies>`.

Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<dependency>`. Tali dipendenze vengono installate insieme quando il framework di destinazione è compatibile con il profilo di framework del progetto.

L'elemento `<group>` senza un attributo `targetFramework` viene usato come elenco predefinito o di fallback delle dipendenze. Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.

> [!Important]
> Il formato di gruppo non può essere usato in combinazione con un elenco semplice.

L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Riferimenti espliciti agli assembly

L'elemento `<references>` specifica in modo esplicito gli assembly a cui deve fare riferimento il progetto di destinazione quando usa il pacchetto. Quando questo elemento è presente, NuGet aggiunge riferimenti solo agli assembly solo elencati e non aggiunge alcun riferimento per eventuali altri assembly nella cartella `lib` del pacchetto.

Ad esempio, l'elemento `<references>` seguente indica a NuGet di aggiungere riferimenti solo a `xunit.dll` e a `xunit.extensions.dll` anche se sono presenti altri assembly nel pacchetto:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

I riferimenti espliciti vengono generalmente usati per gli assembly solo della fase di progettazione. Quando si usano [contratti di codice](/dotnet/framework/debug-trace-profile/code-contracts), ad esempio, gli assembly del contratto devono essere in prossimità degli assembly di runtime che estendono, in modo che Visual Studio possa trovarli, ma non è necessario che il progetto faccia riferimento agli assembly di contratto oppure che vengano copiati nella cartella `bin` del progetto.

In modo analogo, si possono usare riferimenti espliciti per i framework di unit test, ad esempio XUnit, che richiedono che gli assembly degli strumenti siano collocati in prossimità degli assembly di runtime, ma non che siano inclusi riferimenti del progetto.

### <a name="reference-groups"></a>Gruppi di riferimenti

In alternativa a un unico elenco semplice, è possibile specificare i riferimenti in base al profilo del framework del progetto di destinazione usando elementi `<group>` all'interno di `<references>`.

Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<reference>`. Tali riferimenti vengono aggiunti a un progetto quando il framework di destinazione è compatibile con il profilo di framework del progetto.

L'elemento `<group>` senza un attributo `targetFramework` viene usato come elenco predefinito o di fallback dei riferimenti. Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.

> [!Important]
> Il formato di gruppo non può essere usato in combinazione con un elenco semplice.

L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:

```xml
<references>
    <group>
    <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
    <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Riferimenti agli assembly del framework

Gli assembly del framework sono quelli che fanno parte di .NET Framework e devono essere già presenti nella Global Assembly Cache (GAC) per qualsiasi computer. Grazie all'identificazione di tali assembly all'interno dell'elemento `<frameworkAssemblies>`, un pacchetto può garantire che i riferimenti necessari vengano aggiunti a un progetto nel caso in cui il progetto non includa già tali riferimenti. Tali assembly, ovviamente, non vengono inclusi in un pacchetto direttamente.

L'elemento `<frameworkAssemblies>` contiene zero o più elementi `<frameworkAssembly>`, ognuno dei quali specifica gli attributi seguenti:

| Attributo | Descrizione |
| --- | --- |
| **assemblyName** | (Obbligatorio) Nome completo dell'assembly. |
| **targetFramework** | (Facoltativo) Specifica il framework di destinazione a cui si applica questo riferimento. Se omesso, indica che il riferimento si applica a tutti i framework. Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti. |

L'esempio seguente mostra un riferimento a `System.Net` per tutti i framework di destinazione e un riferimento a `System.ServiceModel` solo per .NET Framework 4.0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Inclusione di file di assembly

Se si seguono le convenzioni descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md), non è necessario specificare in modo esplicito un elenco di file nel file `.nuspec`. Il comando `nuget pack` rileva automaticamente i file necessari.

> [!Important]
> Quando un pacchetto viene installato in un progetto, NuGet aggiunge automaticamente i riferimenti agli assembly alle DLL del pacchetto, *escludendo* quelli denominati `.resources.dll` perché si presuppone che siano assembly satellite localizzati. Per questo motivo, evitare di usare `.resources.dll` per i file che contengono invece codice essenziale per il pacchetto.

Per evitare questo comportamento automatico e controllare in modo esplicito quali file vengono inclusi in un pacchetto, posizionare un elemento `<files>` come elemento figlio di `<package>` (ed elemento di pari livello di `<metadata>`), identificando ogni file con un elemento `<file>` separato. Ad esempio:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Con NuGet 2.x e versioni precedenti e i progetti che usano `packages.config`, l'elemento `<files>` viene usato anche per includere file di contenuto non modificabili quando viene installato un pacchetto. Con NuGet 3.3 + e PackageReference per i progetti, viene invece usato l'elemento `<contentFiles>`. Vedere [Inclusione di file di contenuto](#including-content-files) di seguito per informazioni dettagliate.

### <a name="file-element-attributes"></a>Attributi dell'elemento file

Ogni elemento `<file>` specifica gli attributi seguenti:

| Attributo | Descrizione |
| --- | --- |
| **src** | Percorso del file o dei file da includere, soggetto alle esclusioni specificate dall'attributo `exclude`. Il percorso è relativo al file `.nuspec`, a meno che non venga specificato un percorso assoluto. Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle. |
| **target** | Percorso relativo della cartella all'interno del pacchetto in cui vengono collocati i file di origine, che deve iniziare con `lib`, `content`, `build` o `tools`. Vedere [Creazione di un file .nuspec da una directory di lavoro basata su convenzioni](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **exclude** | Elenco delimitato da punti e virgola dei file o dei modelli di file da escludere dal percorso `src`. Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle. |

### <a name="examples"></a>Esempi

**Singolo assembly**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Singolo assembly specifico di un framework di destinazione**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Set di DLL con un carattere jolly**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**DLL per framework diversi**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Esclusione di file**

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Inclusione di file di contenuto

I file di contenuto sono file non modificabili che un pacchetto deve includere in un progetto. Essendo non modificabili, non sono progettati per essere modificati dal progetto che li utilizza. Alcuni esempi di file di contenuto includono:

- Immagini incorporate come risorse
- File di origine già compilati
- Script che devono essere inclusi con l'output di compilazione del progetto
- File di configurazione per il pacchetto che devono essere inclusi nel progetto ma non richiedono modifiche specifiche del progetto

I file di contenuto vengono inclusi in un pacchetto con l'elemento `<files>`, specificando la cartella `content` nell'attributo `target`. Questi file vengono tuttavia ignorati quando il pacchetto viene installato in un progetto usando PackageReference, che usa invece l'elemento `<contentFiles>`.

Per ottenere la massima compatibilità con i progetti in cui viene utilizzato, un pacchetto specifica idealmente i file di contenuto in entrambi gli elementi.

### <a name="using-the-files-element-for-content-files"></a>Uso dell'elemento files per i file di contenuto

Per i file di contenuto, usare semplicemente lo stesso formato usato per i file di assembly, ma specificare `content` come cartella di base nell'attributo `target`, come illustrato negli esempi seguenti.

**File di contenuto semplici**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**File di contenuto con struttura di directory**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**File di contenuto specifico di un framework di destinazione**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**File di contenuto copiato in una cartella con un punto nel nome**

In questo caso, NuGet rileva che l'estensione in `target` non corrisponde all'estensione in `src`, quindi interpreta la parte del nome in `target` come cartella:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**File di contenuto senza estensione**

Per includere i file senza estensione, usare i caratteri jolly `*` o `**`:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**File di contenuto con percorso completo e destinazione completa**

In questo caso, dato che le estensioni dei file di origine e di destinazione corrispondono, NuGet presuppone che la destinazione sia un nome di file e non una cartella:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Ridenominazione di un file di contenuto nel pacchetto**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Esclusione di file**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Uso dell'elemento contentFiles per i file di contenuto

*NuGet 4.0 + con PackageReference*

Per impostazione predefinita, un pacchetto inserisce il contenuto in una cartella `contentFiles` (vedere di seguito) e `nuget pack` include tutti i file nella cartella usando gli attributi predefiniti. In questo caso non è affatto necessario includere un nodo `contentFiles` nel file `.nuspec`.

Per controllare quali file sono inclusi, l'elemento `<contentFiles>` specifica una raccolta di elementi `<files>` che identificano i file esatti inclusi.

Questi file sono specificati con un set di attributi che descrivono come devono essere usati all'interno del sistema del progetto:

| Attributo | Descrizione |
| --- | --- |
| **include** | (Obbligatorio) Percorso del file o dei file da includere, soggetto alle esclusioni specificate dall'attributo `exclude`. Il percorso è relativo al file `.nuspec`, a meno che non venga specificato un percorso assoluto. Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle. |
| **exclude** | Elenco delimitato da punti e virgola dei file o dei modelli di file da escludere dal percorso `src`. Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle. |
| **buildAction** | Azione di compilazione da assegnare all'elemento di contenuto per MSBuild, ad esempio `Content`, `None`, `Embedded Resource`, `Compile` e così via. Il valore predefinito è `Compile`. |
| **copyToOutput** | Valore booleano che indica se copiare gli elementi di contenuto nella cartella di output della compilazione. Il valore predefinito è false. |
| **flatten** | Valore booleano che indica se copiare gli elementi di contenuto di una singola cartella nell'output di compilazione (true) o se mantenere la struttura di cartelle nel pacchetto (false). Questo flag funziona solo quando il flag copyToOutput è impostato su true. Il valore predefinito è false. |

Quando si installa un pacchetto, NuGet applica gli elementi figlio di `<contentFiles>` dall'alto verso il basso. Se più voci corrispondono allo stesso file, vengono applicate tutte le voci. La voce di livello superiore sostituisce le voci inferiori in presenza di un conflitto per lo stesso attributo.

#### <a name="package-folder-structure"></a>Struttura delle cartelle del pacchetto

Il progetto del pacchetto deve strutturare il contenuto in base al modello seguente:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` può essere `cs`, `vb`, `fs`, `any` o l'equivalente in caratteri minuscoli di uno specifico `$(ProjectLanguage)`
- `TxM` è qualsiasi moniker di framework di destinazione valido supportato da NuGet (vedere [Framework di destinazione](../reference/target-frameworks.md)).
- Qualsiasi struttura di cartelle può essere aggiunta alla fine di questa sintassi.

Ad esempio:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Le cartelle vuote possono usare `.` per rifiutare esplicitamente di fornire contenuti per determinate combinazioni di linguaggio e TxM, ad esempio:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Sezione di esempio contentFiles

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>File. nuspec di esempio

**File `.nuspec` semplice che non specifica dipendenze o file**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <id>sample</id>
    <version>1.2.3</version>
    <authors>Kim Abercrombie, Franck Halmaert</authors>
    <description>Sample exists only to show a sample .nuspec file.</description>
    <language>en-US</language>
    <projectUrl>http://xunit.codeplex.com/</projectUrl>
    <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

**File `.nuspec` con dipendenze**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <id>sample</id>
    <version>1.0.0</version>
    <authors>Microsoft</authors>
    <dependencies>
        <dependency id="another-package" version="3.0.0" />
        <dependency id="yet-another-package" version="1.0.0" />
    </dependencies>
    </metadata>
</package>
```

**File `.nuspec` con file**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <id>routedebugger</id>
    <version>1.0.0</version>
    <authors>Jay Hamlin</authors>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
    <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**File `.nuspec` con assembly di framework**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <id>PackageWithGacReferences</id>
    <version>1.0</version>
    <authors>Author here</authors>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>
        A package that has framework assemblyReferences depending
        on the target framework.
    </description>
    <frameworkAssemblies>
        <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
        <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
        <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
        <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
    </frameworkAssemblies>
    </metadata>
</package>
```

In questo esempio vengono installati i componenti seguenti per destinazioni di progetto specifiche:

- .NET4 -> `System.Web`, `System.Net`
- .NET4 Client Profile -> `System.Net`
- Silverlight 3 -> `System.Json`
- Silverlight 4 -> `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
