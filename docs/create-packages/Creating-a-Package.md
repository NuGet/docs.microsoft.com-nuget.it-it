---
title: Come creare un pacchetto NuGet
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 1bc67927ddc463dcc3a0abe80fe20e625e188e63
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981171"
---
# <a name="creating-nuget-packages"></a>Creazione di pacchetti NuGet

Indipendentemente dalle operazioni eseguite dal pacchetto o dal tipo di codice contenuto, `nuget.exe` viene usato per rendere disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori. Per installare `nuget.exe`, vedere [Installare l'interfaccia della riga di comando di NuGet](../install-nuget-client-tools.md#nugetexe-cli). Si noti che `nuget.exe` non è incluso automaticamente in Visual Studio.

Da un punto di vista tecnico, un pacchetto NuGet è solo un file ZIP rinominato con l'estensione `.nupkg` e i cui contenuti rispettano determinate convenzioni. Questo argomento descrive il processo dettagliato di creazione di un pacchetto che soddisfa tali convenzioni. Per una procedura dettagliata specifica, vedere [Guida introduttiva: Creare e pubblicare un pacchetto](../quickstart/create-and-publish-a-package.md).

La creazione di un pacchetto inizia con il codice compilato (assembly), i simboli e/o altri file che si vuole distribuire come pacchetto. Vedere [Panoramica e flusso di lavoro](overview-and-workflow.md). Questo processo è indipendente dalla compilazione o comunque dalla generazione dei file inseriti nel pacchetto, anche se è possibile usare le informazioni contenute in un file di progetto per mantenere sincronizzati i pacchetti e gli assembly compilati.

> [!Note]
> Questo argomento si applica a tipi di progetto diversi dai progetti .NET Core, che usano Visual Studio 2017 e NuGet 4.0+. In questi progetti .NET Core, NuGet usa direttamente le informazioni contenute nel file di progetto. Per informazioni dettagliate, vedere [Creare pacchetti .NET Standard con Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) e [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md).

## <a name="deciding-which-assemblies-to-package"></a>Scelta degli assembly per cui creare un pacchetto

La maggior parte dei pacchetti per utilizzo generico contiene uno o più assembly che gli altri sviluppatori possono usare nei propri progetti.

- In generale, l'ideale è avere un assembly per ogni pacchetto NuGet, purché ogni assembly abbia una propria utilità. Se ad esempio è presente un file `Utilities.dll` che dipende da `Parser.dll` e `Parser.dll` è utile di per sé, creare un pacchetto per ognuno. In questo modo gli sviluppatori possono usare `Parser.dll` indipendentemente da `Utilities.dll`.

- Se la libreria è costituita da più assembly che non hanno una propria utilità, è consigliabile combinarli in un solo pacchetto. Usando l'esempio precedente, se `Parser.dll` contiene codice che viene usato solo da `Utilities.dll`, è consigliabile tenere `Parser.dll` nello stesso pacchetto.

- Analogamente, se `Utilities.dll` dipende da `Utilities.resources.dll` e quest'ultimo non è utile di per sé, inserirli entrambi nello stesso pacchetto.

Le risorse sono di fatto un caso particolare. Quando un pacchetto viene installato in un progetto, NuGet aggiunge automaticamente alle DLL del pacchetto i riferimenti agli assembly, *escludendo* quelli denominati `.resources.dll` perché si presuppone che siano assembly satellite localizzati. Vedere [Creazione di pacchetti localizzati](creating-localized-packages.md). Per questo motivo, evitare di usare `.resources.dll` per i file che contengono invece codice essenziale per il pacchetto.

Se la libreria contiene assembly di interoperabilità COM, seguire le linee guida aggiuntive in [Creazione di pacchetti con assembly di interoperabilità COM](#authoring-packages-with-com-interop-assemblies).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Ruolo e struttura del file con estensione nuspec

Dopo avere deciso per quali file si vuole creare un pacchetto, il passaggio successivo prevede la creazione di un manifesto del pacchetto in un file XML `.nuspec`.

Il manifesto:

1. Descrive i contenuti del pacchetto e viene incluso nel pacchetto.
1. Gestisce la creazione del pacchetto e indica a NuGet come installare il pacchetto in un progetto. Il manifesto, ad esempio, identifica le altre dipendenze del pacchetto in modo che NuGet possa installare anche tali dipendenze quando viene installato il pacchetto principale.
1. Contiene le proprietà sia obbligatorie che facoltative, come descritto di seguito. Per informazioni dettagliate, incluse le altre proprietà non citate qui, vedere [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).

Proprietà obbligatorie:

- Identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto.
- Numero di versione specifico nel formato *Major.Minor.Patch[-Suffix]* dove *-Suffix* identifica le [versioni preliminari](prerelease-packages.md)
- Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)
- Informazioni sull'autore e sul proprietario.
- Descrizione estesa del pacchetto.

Proprietà facoltative comuni:

- Note sulla versione
- Informazioni sul copyright
- Breve descrizione dell'[interfaccia utente di Gestione pacchetti in Visual Studio](../tools/package-manager-ui.md)
- ID impostazioni locali
- URL della home page e della licenza
- URL dell'icona
- Elenchi di dipendenze e riferimenti
- Tag di supporto per le ricerche nella raccolta

Di seguito è riportato un file `.nuspec` tipico (ma fittizio), con commenti che descrivono le proprietà:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md). È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `include` ed `exclude` nell'elemento `dependency`. Vedere la [sezione Dipendenze delle informazioni di riferimento sul file .nuspec](../reference/nuspec.md#dependencies).

Poiché il manifesto è incluso nel pacchetto creato, per trovare altri esempi, esaminare i pacchetti esistenti. Una valida fonte è la cartella *global-packages* nel computer, la posizione della quale viene restituita dal comando seguente:

```cli
nuget locals -list global-packages
```

Andare a qualsiasi cartella *pacchetto\versione*, copiare il file `.nupkg` in un file `.zip`, quindi aprire il file `.zip` ed esaminare il file `.nuspec`.

> [!Note]
> Quando si crea un file `.nuspec` da un progetto di Visual Studio, il manifesto contiene token che vengono sostituiti con le informazioni provenienti dal progetto quando il pacchetto viene compilato. Vedere [Creazione del file con estensione nuspec da un progetto di Visual Studio](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>Creazione del file con estensione nuspec

La creazione di un manifesto completo inizia in genere con un file `.nuspec` di base generato con uno dei metodi seguenti:

- [Directory di lavoro basata sulle convenzioni](#from-a-convention-based-working-directory)
- [DLL dell'assembly](#from-an-assembly-dll)
- [Progetto di Visual Studio](#from-a-visual-studio-project)    
- [Nuovo file con valori predefiniti](#new-file-with-default-values)

Si modifica quindi il file manualmente in modo che descriva il contenuto esatto che dovrà essere incluso nel pacchetto finale.

> [!Important]
> I file `.nuspec` generati contengono segnaposto che devono essere modificati prima di creare il pacchetto con il comando `nuget pack`, che ha esito negativo se il file `.nuspec` contiene segnaposto.

### <a name="from-a-convention-based-working-directory"></a>Da una directory di lavoro basata sulle convenzioni

Dato che un pacchetto NuGet è solo un file ZIP rinominato con l'estensione `.nupkg`, spesso è più semplice creare la struttura di cartelle desiderata nel file system locale, quindi creare il file `.nuspec` direttamente da tale struttura. Il comando `nuget pack` aggiunge quindi automaticamente tutti i file in tale struttura di cartelle, escluse le cartelle che iniziano con `.`, per poter mantenere i file privati nella stessa struttura.

Il vantaggio di questo approccio è che non è necessario specificare nel manifesto i file che si vuole includere nel pacchetto, come illustrato più avanti in questo argomento. È sufficiente fare in modo che il processo di compilazione generi l'esatta struttura di cartelle da inserire nel pacchetto, per poter facilmente includere altri file che altrimenti potrebbero non fare parte di un progetto:

- Contenuto e codice sorgente da inserire nel progetto di destinazione.
- Script di PowerShell. I pacchetti usati in NuGet 2.x possono includere anche script di installazione, non supportati in NuGet 3.x e versioni successive.
- Trasformazioni della configurazione esistente e dei file del codice sorgente di un progetto.

Le convenzioni delle cartelle sono le seguenti:

| Cartella | Descrizione | Azione durante l'installazione del pacchetto |
| --- | --- | --- |
| (radice) | Percorso del file readme.txt | Visual Studio visualizza un file readme.txt nella radice del pacchetto quando il pacchetto viene installato. |
| lib/{tfm} | File di assembly (`.dll`), di documentazione (`.xml`) e di simboli (`.pdb`) per il moniker del framework di destinazione (TFM, Target Framework Moniker) specificato | Gli assembly vengono aggiunti come riferimenti per la compilazione, oltre che per il runtime. `.xml` e `.pdb` vengono copiati nelle cartelle di progetto. Per la creazione di sottocartelle specifiche del framework di destinazione, vedere [Supporto di più framework di destinazione](supporting-multiple-target-frameworks.md). |
| ref/{tfm} | File di assembly (`.dll`) e di simboli (`.pdb`) per il moniker del framework di destinazione (TFM, Target Framework Moniker) specificato | Gli assembly vengono aggiunti come riferimenti solo per la fase di compilazione. Non verrà quindi copiato nulla nella cartella bin del progetto. |
| runtimes | File di assembly (`.dll`), di simboli (`.pdb`) e di risorse native (`.pri`) specifici dell'architettura | Gli assembly vengono aggiunti come riferimenti solo per il runtime. Gli altri file vengono copiati nelle cartelle di progetto. Deve esistere sempre un assembly specifico `AnyCPU` corrispondente (TFM) sotto la cartella `/ref/{tfm}` per fornire l'assembly della fase di compilazione corrispondente. Vedere [Supporto di più framework di destinazione](supporting-multiple-target-frameworks.md). |
| contenuto | File arbitrari | I contenuti vengono copiati nella radice del progetto. La cartella **content** può essere considerata come la radice dell'applicazione di destinazione che in definitiva utilizza il pacchetto. Per fare in modo che il pacchetto aggiunga un'immagine nella cartella */images* dell'applicazione, inserirla nella cartella *content/images* del pacchetto. |
| build | File `.targets` e `.props` MSBuild | Vengono automaticamente inseriti nel file di progetto o in `project.lock.json` (NuGet 3.x+). |
| tools | Script di PowerShell e programmi accessibili dalla console di Gestione pacchetti | La cartella `tools` viene aggiunta alla variabile di ambiente `PATH` solo per la console di Gestione pacchetti, in particolare *non* alla variabile `PATH` impostata per MSBuild durante la compilazione del progetto. |

Poiché la struttura di cartelle può contenere un numero indeterminato di assembly per un numero indeterminato di framework di destinazione, questo metodo è necessario quando si creano pacchetti che supportano più framework 

In ogni caso, dopo avere creato la struttura di cartelle desiderata, eseguire il comando seguente in tale cartella per creare il file `.nuspec`:

```cli
nuget spec
```

Anche in questo caso, il file `.nuspec` generato non contiene riferimenti espliciti ai file nella struttura di cartelle. NuGet include tutti i file automaticamente quando viene creato il pacchetto. È tuttavia necessario modificare i valori dei segnaposto nelle altre parti del manifesto.

### <a name="from-an-assembly-dll"></a>Da una DLL dell'assembly

Nel semplice caso della creazione di un pacchetto da un assembly, è possibile generare un file `.nuspec` dai metadati nell'assembly usando il comando seguente:

```cli
nuget spec <assembly-name>.dll
```

Usando questo formato, alcuni segnaposto nel manifesto vengono sostituiti con i valori specifici dell'assembly. La proprietà `<id>`, ad esempio, viene impostata sul nome dell'assembly e `<version>` viene impostata sulla versione dell'assembly. Le altre proprietà del manifesto non hanno tuttavia valori corrispondenti nell'assembly e perciò contengono ancora i segnaposto.

### <a name="from-a-visual-studio-project"></a>Da un progetto di Visual Studio

La creazione di un file `.nuspec` da un file `.csproj` o `.vbproj` è utile perché viene fatto automaticamente riferimento agli altri pacchetti che sono stati installati in tale progetto come a dipendenze. È sufficiente usare il comando seguente nella stessa cartella del file di progetto:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Il file `<project-name>.nuspec` risultante contiene *token* che in fase di creazione del pacchetto vengono sostituiti con i valori del progetto, inclusi i riferimenti agli altri pacchetti già installati.

Un token è delimitato dai simboli `$` su entrambi i lati della proprietà del progetto. Ad esempio, il valore `<id>` in un manifesto generato in questo modo solitamente viene visualizzato come segue:

```xml
<id>$id$</id>
```

Questo token viene sostituito con il valore `AssemblyName` del file di progetto in fase di creazione del pacchetto. Per il mapping esatto dei valori del progetto ai token di `.nuspec`, vedere le [informazioni di riferimento in Token di sostituzione](../reference/nuspec.md#replacement-tokens).

I token evitano di dover aggiornare i valori fondamentali, ad esempio il numero di versione, nel file `.nuspec` quando si aggiorna il progetto. È sempre possibile sostituire i token con valori letterali, se necessario. 

Tenere presente che sono disponibili diverse altre opzioni di creazione del pacchetto quando si usa un progetto di Visual Studio, come illustrato più avanti in [Esecuzione di nuget pack per generare il file con estensione nupkg](#running-nuget-pack-to-generate-the-nupkg-file).

#### <a name="solution-level-packages"></a>Pacchetti a livello di soluzione

*Solo NuGet 2.x. Non disponibile in NuGet 3.0+.*

NuGet 2.x supportava la nozione di pacchetto a livello di soluzione che installa strumenti o comandi aggiuntivi per la console di Gestione pacchetti (contenuti della cartella `tools`), ma non aggiunge riferimenti, contenuto o personalizzazioni delle compilazioni ai progetti della soluzione. Tali pacchetti non contengono file nelle cartelle `lib`, `content` o `build` dirette e nessuna dipendenza ha file nelle rispettive cartelle `lib`, `content` o `build`.

NuGet tiene traccia dei pacchetti a livello di soluzione installati in un file `packages.config` nella cartella `.nuget`, invece che nel file `packages.config` del progetto.

### <a name="new-file-with-default-values"></a>Nuovo file con valori predefiniti

Il comando seguente crea un manifesto predefinito con segnaposto, che assicura di iniziare con la struttura di file corretta:

```cli
nuget spec [<package-name>]
```

Se si omette \<package-name\>, il file risultante è `Package.nuspec`. Se come nome si specifica ad esempio `Contoso.Utility.UsefulStuff`, il file è `Contoso.Utility.UsefulStuff.nuspec`.

Il file `.nuspec` risultante contiene segnaposto per i valori come `projectUrl`. Assicurarsi di modificare il file prima di usarlo per creare il file `.nupkg` finale.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Scelta di un identificatore univoco del pacchetto e impostazione del numero di versione

L'identificatore del pacchetto (elemento `<id>`) e il numero di versione (elemento `<version>`) sono i due valori più importanti del manifesto perché identificano in modo univoco il codice esatto contenuto nel pacchetto.

**Procedure consigliate per l'identificatore del pacchetto:**

- **Univocità**: l'identificatore deve essere univoco in nuget.org o in qualsiasi raccolta che ospita il pacchetto. Prima di scegliere un identificatore, eseguire una ricerca nella raccolta applicabile per controllare se il nome è già in uso. Per evitare conflitti, è consigliabile usare il nome della società come prima parte dell'identificatore, ad esempio `Contoso.`.
- **Nomi simili a spazi dei nomi**: seguono un modello simile a quello degli spazi dei nomi in .NET, usando la notazione del punto invece dei trattini. Usare, ad esempio, `Contoso.Utility.UsefulStuff` invece di `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`. Per gli utenti è anche utile che l'identificatore del pacchetto corrisponda agli spazi dei nomi usati nel codice.
- **Pacchetti di esempio**: se si produce un pacchetto di codice di esempio che illustra come usare un altro pacchetto, collegare `.Sample` come suffisso all'identificatore, come in `Contoso.Utility.UsefulStuff.Sample`. Il pacchetto di esempio avrà naturalmente una dipendenza dall'altro pacchetto. Quando si crea un pacchetto di esempio, usare il metodo della directory di lavoro basata sulle convenzioni descritto in precedenza. Nella cartella `content` inserire il codice di esempio in una cartella denominata `\Samples\<identifier>` come in `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Procedure consigliate per la versione del pacchetto:**

- In generale, impostare la versione del pacchetto in modo che corrisponda alla libreria, anche se non è strettamente necessario. È davvero semplicissimo quando si limita un pacchetto a un singolo assembly, come descritto precedentemente in [Scelta degli assembly per cui creare un pacchetto](#deciding-which-assemblies-to-package). In generale, tenere presente che, durante la risoluzione delle dipendenze, di per sé NuGet gestisce le versioni dei pacchetti, non le versioni degli assembly.
- Quando si usa uno schema della versione non standard, tenere in considerazione le regole di controllo delle versioni di NuGet, come illustrato in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).

> Per informazioni sul controllo delle versioni, vedere anche la serie seguente di brevi post di blog:
>
> - [Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Affrontare l'inferno delle DLL)
> - [Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: L'algoritmo principale)
> - [Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificazione tramite i reindirizzamenti di binding)

## <a name="setting-a-package-type"></a>Impostazione di un tipo di pacchetto

Con NuGet 3.5+, i pacchetti possono essere contrassegnati con uno specifico *tipo di pacchetto* per indicarne l'uso previsto. I pacchetti non contrassegnati con un tipo, inclusi tutti i pacchetti creati con versioni precedenti di NuGet, usano il tipo `Dependency` per impostazione predefinita.

- I pacchetti di tipo `Dependency` aggiungono asset in fase di compilazione o di esecuzione ad applicazioni e librerie e possono essere installati in qualsiasi tipo di progetto, presupponendo che siano compatibili.

- I pacchetti di tipo `DotnetCliTool` sono estensioni dell'[interfaccia della riga di comando di .NET](/dotnet/articles/core/tools/index) e vengono richiamati dalla riga di comando. Tali pacchetti possono essere installati solo nei progetti .NET Core e non hanno effetto sulle operazioni di ripristino. Per altre informazioni su queste estensioni in base al progetto, vedere la documentazione sull'[estendibilità in .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- I pacchetti di tipo personalizzato usano un identificatore di tipo arbitrario che è conforme alle stesse regole di formato degli ID dei pacchetti. I tipi diversi da `Dependency` e `DotnetCliTool`, tuttavia, non vengono riconosciuti da Gestione pacchetti NuGet in Visual Studio.

I tipi di pacchetto vengono impostati nel file `.nuspec`. Per la compatibilità con le versioni precedenti è meglio *non* impostare in modo esplicito il tipo `Dependency` e basarsi invece sul fatto che NuGet presuppone questo tipo quando non viene specificato alcun tipo.

- `.nuspec`: indica il tipo di pacchetto in un nodo `packageTypes\packageType` sotto l'elemento `<metadata>`:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a>Aggiunta di un file leggimi e di altri file

Per specificare direttamente i file da includere nel pacchetto, usare il nodo `<files>` nel file `.nuspec`, che *segue* il tag `<metadata>`:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Quando si usa l'approccio della directory di lavoro basata sulle convenzioni, è possibile inserire il file readme.txt nella radice del pacchetto e gli altri contenuti nella cartella `content`. Non sono necessari elementi `<file>` nel manifesto.

Quando si include un file denominato `readme.txt` nella radice del pacchetto, Visual Studio visualizza i contenuti del file come testo normale subito dopo avere installato direttamente il pacchetto. I file leggimi non vengono visualizzati per i pacchetti installati come dipendenze. Ecco ad esempio come viene visualizzato il file leggimi per il pacchetto HtmlAgilityPack:

![Visualizzazione di un file leggimi per un pacchetto NuGet durante l'installazione](media/Create_01-ShowReadme.png)

> [!Note]
> Se si include un nodo `<files>` vuoto nel file `.nuspec`, NuGet non include nel pacchetto altri contenuti diversi dal contenuto della cartella `lib`.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>Inclusione di proprietà e destinazioni MSBuild in un pacchetto

In alcuni casi, potrebbe essere necessario aggiungere destinazioni o proprietà di compilazione personalizzata nei progetti che utilizzano il pacchetto, ad esempio l'esecuzione di uno strumento o processo personalizzato durante la compilazione. A tale scopo, inserire i file nel formato `<package_id>.targets` o `<package_id>.props` (ad esempio `Contoso.Utility.UsefulStuff.targets`) nella cartella `\build` del progetto.

I file nella cartella radice `\build` sono considerati adatti a tutti i framework di destinazione. Per fornire file specifici del framework, inserirli prima nelle sottocartelle appropriate, come di seguito:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Nel file `.nuspec` assicurarsi quindi di fare riferimento a questi file nel nodo `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

La possibilità di includere file props e targets di MSBuild in un pacchetto è stata [introdotta con NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), pertanto è consigliabile aggiungere l'attributo `minClientVersion="2.5"` all'elemento `metadata` per indicare la versione client NuGet minima richiesta per utilizzare il pacchetto.

Quando installa un pacchetto con i file `\build`, NuGet aggiunge elementi `<Import>` di MSBuild nel file di progetto che puntano ai file `.targets` e `.props`. `.props` viene aggiunto all'inizio del file di progetto, `.targets` viene aggiunto alla fine. Viene aggiunto un elemento `<Import>` di MSBuild condizionale separato per ogni framework di destinazione.

I file `.props` e `.targets` di MSBuild per l'assegnazione di più framework di destinazione possono essere posizionati nella cartella `\buildCrossTargeting`. Durante l'installazione del pacchetto, NuGet aggiunge elementi `<Import>` corrispondenti al file di progetto, a condizione che il framework di destinazione non sia impostato (la proprietà MSBuild `$(TargetFramework)` deve essere vuota).

Con NuGet 3.x, le destinazioni non vengono aggiunte al progetto, ma vengono rese disponibili tramite `project.lock.json`.

## <a name="authoring-packages-with-com-interop-assemblies"></a>Creazione di pacchetti con assembly di interoperabilità COM

I pacchetti che contengono gli assembly di interoperabilità COM devono includere un [file di destinazioni](#including-msbuild-props-and-targets-in-a-package) appropriato in modo che i metadati `EmbedInteropTypes` corretti vengano aggiunti ai progetti usando il formato PackageReference. Per impostazione predefinita, i metadati `EmbedInteropTypes` sono sempre false per tutti gli assembly quando viene usato PackageReference, quindi il file di destinazioni aggiunge i metadati in modo esplicito. Per evitare conflitti, il nome della destinazione deve essere univoco. L'ideale è usare una combinazione del nome del pacchetto dell'assembly che viene incorporato, sostituendo `{InteropAssemblyName}` nell'esempio riportato di seguito con tale valore. Per un esempio, vedere anche [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Si noti che, quando si usa il formato di gestione `packages.config`, l'aggiunta di riferimenti agli assembly dai pacchetti fa sì che NuGet e Visual Studio cerchino gli assembly di interoperabilità COM e impostino `EmbedInteropTypes` su true nel file di progetto. In questo caso viene eseguito l'override delle destinazioni.

Per impostazione predefinita inoltre gli [asset di compilazione non vengono trasferiti in modo transitivo](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). I pacchetti creati come descritto qui funzionano diversamente quando ne viene eseguito il pull come dipendenza transitiva da un progetto al riferimento al progetto. L'utente del pacchetto ne può consentire il trasferimento modificando il valore predefinito di PrivateAssets in modo che non includa la compilazione.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>Esecuzione di nuget pack per generare il file con estensione nupkg

Quando si usa un assembly o la directory di lavoro basata sulle convenzioni, creare un pacchetto eseguendo `nuget pack` con il file `.nuspec`, sostituendo `<project-name>` con il nome file specifico:

```cli
nuget pack <project-name>.nuspec
```

Quando si usa un progetto di Visual Studio, eseguire `nuget pack` con il file di progetto, che carica automaticamente il file `.nuspec` del progetto e sostituisce il token usando i valori del file di progetto:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> L'uso diretto del file di progetto è necessario per la sostituzione dei token perché il progetto è l'origine dei valori dei token. La sostituzione dei token non avviene se si usa `nuget pack` con un file `.nuspec`.

In tutti i casi, `nuget pack` esclude le cartelle che iniziano con un punto, ad esempio `.git` o `.hg`.

NuGet indica se sono presenti errori nel file `.nuspec` che richiedono una correzione, ad esempio se si dimentica di modificare i valori dei segnaposto nel manifesto.

Dopo la corretta esecuzione di `nuget pack`, è disponibile un file `.nupkg` che è possibile pubblicare in una raccolta appropriata, come illustrato in [Pubblicazione di un pacchetto](../create-packages/publish-a-package.md).

> [!Tip]
> Per esaminare un pacchetto dopo averlo creato, è possibile aprirlo nello strumento [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), che offre una visualizzazione grafica dei contenuti del pacchetto e del manifesto. È anche possibile rinominare il file `.nupkg` risultante in un file `.zip` ed esplorarne il contenuto direttamente.

### <a name="additional-options"></a>Opzioni aggiuntive

Tra le altre funzionalità, è possibile usare diverse opzioni della riga di comando con `nuget pack` per escludere i file, eseguire l'override del numero di versione nel manifesto e modificare la cartella di output. Per un elenco completo, vedere le [informazioni di riferimento sul comando pack](../tools/cli-ref-pack.md).

Le seguenti sono alcune opzioni comuni ai progetti di Visual Studio:

- **Progetti di riferimento**: se il progetto fa riferimento ad altri progetti, è possibile aggiungere i progetti a cui si fa riferimento come parte del pacchetto o come dipendenze, usando l'opzione `-IncludeReferencedProjects`:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Questo processo di inclusione è ricorsivo, quindi se `MyProject.csproj` fa riferimento ai progetti B e C e tali progetti fanno riferimento a D, E e F, i file di B, C, D, E e F vengono inclusi nel pacchetto.

    Se un progetto a cui si fa riferimento include un proprio file `.nuspec`, NuGet aggiunge invece tale progetto a cui si fa riferimento come dipendenza.  È necessario creare un pacchetto per il progetto e pubblicarlo separatamente.

- **Configurazione della build**: per impostazione predefinita, NuGet usa la configurazione della build predefinita impostata nel file di progetto, in genere *Debug*. Per creare un pacchetto per i file da una configurazione della build differente, ad esempio *Release*, usare l'opzione `-properties` con la configurazione:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Simboli**: per includere i simboli che consentono agli utenti di eseguire il codice del pacchetto un'istruzione alla volta nel debugger, usare l'opzione `-Symbols`:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Test dell'installazione pacchetto

Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto. I test assicurano che i file necessari vengano inseriti nei percorsi corretti all'interno del progetto.

È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../consume-packages/ways-to-install-a-package.md).

Per i test automatizzati, il processo di base è il seguente:

1. Copiare il file `.nupkg` in una cartella locale.
1. Aggiungere la cartella alle origini del pacchetto usando il comando `nuget sources add -name <name> -source <path>`. Vedere [nuget sources](../tools/cli-ref-sources.md). Si noti che è necessario impostare l'origine locale solo una volta in ogni computer.
1. Installare il pacchetto da tale origine usando `nuget install <packageID> -source <name>` dove `<name>` corrisponde al nome dell'origine specificata in `nuget sources`. Specificando l'origine, il pacchetto viene con certezza installato solo da tale origine.
1. Esaminare il file system per controllare che i file siano installati correttamente.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../create-packages/publish-a-package.md).

Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:

- [Controllo delle versioni dei pacchetti](../reference/package-versioning.md)
- [Supporto di più framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md)
- [Trasformazioni di file di origine e di configurazione](../create-packages/source-and-config-file-transformations.md)
- [Localizzazione](../create-packages/creating-localized-packages.md)
- [Versioni non definitive](../create-packages/prerelease-packages.md)

Sono infine disponibili altri tipi di pacchetti da tenere presenti:

- [Pacchetti nativi](../create-packages/native-packages.md)
- [Pacchetti di simboli](../create-packages/symbol-packages.md)
