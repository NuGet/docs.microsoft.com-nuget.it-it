---
title: Informazioni di riferimento sul file project.json per NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d64fa6d8-a3f7-4c72-95d3-1a964375ccb8
description: In alcuni tipi di progetto, il file project.json include l'elenco aggiornato dei pacchetti NuGet usati nel progetto.
keywords: project.json per NuGet, riferimenti al pacchetto NuGet, dipendenze NuGet, project.lock.json
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e8763c22bda0c384b8bb1a00078a314e4bedc262
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="projectjson-reference"></a>Riferimenti di project.json

*NuGet 3.x+*

Il file `project.json` include un elenco dei pacchetti usati in un progetto, noto come formato di riferimento del pacchetto. Prevale su `packages.config`, ma viene a sua volta sostituito da [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) con NuGet 4.0+.

Il file [`project.lock.json`](#projectlockjson) (descritto sotto) viene anche usato nei progetti che impiegano `project.json`.

`project.json` presenta la struttura di base seguente, dove ognuno dei quattro oggetti di primo livello può avere un numero indeterminato di oggetti figlio:

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }  
}
```
 
## <a name="dependencies"></a>Dipendenze

Elenca le dipendenze del pacchetto NuGet per il progetto nel formato seguente:

```json
"PackageID" : "version_constraint"
```
  
Ad esempio:

```json
"dependencies": {   
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"   
}
```

Nella sezione `dependencies` la finestra di dialogo Gestione pacchetti NuGet aggiunge le dipendenze del pacchetto al progetto.

L'ID del pacchetto corrisponde all'ID del pacchetto in nuget.org, che è uguale all'ID usato nella console di Gestione pacchetti: `Install-Package Microsoft.NETCore`.

Quando si ripristinano i pacchetti, il vincolo della versione `"5.0.0"` implica `>= 5.0.0`, vale a dire che se la versione 5.0.0 non è disponibile sul server, ma la 5.0.1 lo è, NuGet installa la 5.0.1 e avvisa dell'aggiornamento. In caso contrario, NuGet seleziona la versione più bassa possibile corrispondente al vincolo.

Per altre informazioni dettagliate sulle regole di risoluzione, vedere [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).

### <a name="managing-dependency-assets"></a>Gestione degli asset delle dipendenze

Per controllare quali asset delle dipendenze confluiscono nel progetto di primo livello, specificare un set di tag delimitati da virgole nelle proprietà `include` ed `exclude` del riferimento alle dipendenze. I tag sono elencati nella tabella seguente:

| Tag di inclusione/esclusione | Cartelle di destinazione interessate |
| --- | --- |
| contentFiles | Content  |
| runtime | Runtime, Resources e FrameworkAssemblies  |
| compile | lib |
| build | build (proprietà e destinazioni MSBuild) |
| native | native |
| nessuno | Nessuna cartella |
| tutti | Tutte le cartelle |

I tag specificati con `exclude` hanno la precedenza rispetto a quelli specificati con `include`. Ad esempio, `include="runtime, compile" exclude="compile"` equivale a `include="runtime"`.

Ad esempio, per includere le cartelle `build` e `native` di una dipendenza, usare il codice seguente:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

Per escludere le cartelle `content` e `build` di una dipendenza, usare il codice seguente:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>Framework

Elenca i framework in cui viene eseguito il progetto, ad esempio `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Nella sezione `frameworks` è consentita una sola voce. Fanno eccezione i file `project.json` per i progetti ASP.NET compilati con la toolchain DNX deprecata, che consente più destinazioni.

## <a name="runtimes"></a>Runtimes

Elenca i sistemi operativi e le architetture in cui l'app viene eseguita, ad esempio `win10-arm`, `win8-x64`, `win8-x86`.

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

Non è necessario specificare un runtime per un pacchetto contenente una libreria PCL che può essere eseguita in qualsiasi runtime. Ciò deve valere anche per qualsiasi dipendenza. In caso contrario, è necessario specificare i runtime.


## <a name="supports"></a>Supports

Definisce un set di controlli per le dipendenze dei pacchetti. È possibile definire dove si prevede che la libreria PCL o l'app venga eseguita. Le definizioni non sono restrittive perché il codice può essere eseguito altrove, ma, se si specificano questi controlli, NuGet controlla che tutte le dipendenze siano rispettate nei TxM elencati. Alcuni esempi di valori validi sono `net46.app`, `uwp.10.0.app` e così via.

Questa sezione verrà popolata automaticamente quando si seleziona una voce nella finestra di dialogo delle destinazioni Libreria di classi portabile.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Imports

Le importazioni sono progettate per consentire ai pacchetti che usano il TxM `dotnet` di interagire con pacchetti che non dichiarano un TxM dotnet. Se il progetto usa il TxM `dotnet`, anche tutti i pacchetti da cui si dipende devono avere un TxM `dotnet`, a meno che non si aggiunga il codice seguente a `project.json` per consentire alle piattaforme non `dotnet` di essere compatibili con `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Se si usa il TxM `dotnet`, il sistema del progetto PCL aggiunge l'istruzione `imports` appropriata in base alle destinazioni supportate.

## <a name="differences-from-portable-apps-and-web-projects"></a>Differenze rispetto alle app portabili e ai progetti Web

Il file `project.json` usato da NuGet è un subset di quello presente nei progetti ASP.NET Core. In ASP.NET Core `project.json` viene usato per i metadati del progetto, le informazioni di compilazione e le dipendenze. Se viene usato in altri sistemi di progetto, questi tre elementi vengono divisi in file separati e `project.json` contiene meno informazioni. Ecco le differenze principali:

- Nella sezione `frameworks` può essere presente un solo framework.

- Il file non può contenere le dipendenze, le opzioni di compilazione e così via presenti nei file `project.json` DNX. Dal momento che può esserci un solo framework, non ha senso immettere dipendenze specifiche del framework.

- La compilazione viene gestita da MSBuild, quindi le opzioni di compilazione, le definizioni del preprocessore e così via fanno tutte parte del file di progetto MSBuild e non di `project.json`.

In NuGet 3+ non è previsto che gli sviluppatori modifichino manualmente `project.json`, perché è l'interfaccia utente di Gestione pacchetti in Visual Studio a modificare il contenuto. Ciò premesso, è ovviamente possibile modificare il file, ma è necessario compilare il progetto per avviare un ripristino del pacchetto o richiamare il ripristino in un altro modo. Vedere [Ripristino di pacchetti](../Consume-Packages/Package-Restore.md).


## <a name="projectlockjson"></a>project.lock.json

Il file `project.lock.json` viene generato durante il processo di ripristino dei pacchetti NuGet nei progetti che usano `project.json`. Contiene uno snapshot di tutte le informazioni generate quando NuGet analizza il grafo dei pacchetti e include la versione, i contenuti e le dipendenze di tutti i pacchetti del progetto. Il sistema di compilazione lo usa per scegliere i pacchetti pertinenti da un percorso globale quando si compila il progetto invece di dipendere da una cartella di pacchetti locale nel progetto stesso. Ne deriva un miglioramento delle prestazioni di compilazione perché è necessario leggere solo `project.lock.json` invece di più file `.nuspec` separati.

`project.lock.json` viene automaticamente generato durante il ripristino del pacchetto, quindi può essere omesso dal controllo del codice sorgente aggiungendolo ai file `.gitignore` e `.tfignore`. Vedere [Pacchetti e controllo del codice sorgente](../Consume-Packages/Packages-and-Source-Control.md). Se tuttavia lo si include nel controllo del codice sorgente, la cronologia modifiche indica le modifiche apportate alle dipendenze nel corso del tempo.
