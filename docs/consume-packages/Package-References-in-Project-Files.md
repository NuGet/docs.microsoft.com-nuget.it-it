---
title: Formato PackageReference NuGet (riferimenti a pacchetti nei file di progetto)
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 +, Visual Studio 2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c2dfce8de6b28aaee99e3d5ab75cd28950a8cb0f
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812833"
---
# <a name="package-references-packagereference-in-project-files"></a>Riferimenti a pacchetti (PackageReference) nei file di progetto

I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` separato. L'uso di PackageReference non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file `NuGet.config` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione del comportamento di NuGet](configuring-nuget-behavior.md).

Con PackageReference è anche possibile usare condizioni MSBuild per scegliere i riferimenti ai pacchetti in base a framework di destinazione, configurazione, piattaforma o altri raggruppamenti. Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto. (Per altri dettagli, vedere [Pack e restore di NuGet come destinazioni MSBuild ](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Supporto dei tipi di progetto

Per impostazione predefinita, PackageReference viene usato per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update) e versioni successive, con l'eccezione dei progetti UWP C++. I progetti .NET Framework supportano PackageReference, ma usano attualmente `packages.config` per impostazione predefinita. Per usare PackageReference, eseguire la [migrazione](../reference/migrate-packages-config-to-package-reference.md) delle dipendenze da `packages.config` nel file di progetto e quindi rimuovere packages.config.

Le app ASP.NET destinate a .NET Framework includono solo un [supporto limitato](https://github.com/NuGet/Home/issues/5877) per PackageReference. I tipi di progetto C++ e JavaScript non sono supportati.

## <a name="adding-a-packagereference"></a>Aggiunta di PackageReference

Aggiungere una dipendenza nel file di progetto usando la sintassi seguente:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Controllo della versione della dipendenza

La convenzione per specificare la versione di un pacchetto è uguale quando si usa `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Uso di PackageReference per un progetto senza PackageReference
Avanzato: Se non si hanno pacchetti installati in un progetto (nessun PackageReference nel file di progetto e nessun file packages.config), ma si vuole ripristinare il progetto con stile PackageReference, è possibile impostare una proprietà del progetto RestoreProjectStyle su PackageReference nel file di progetto.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
Questa opzione può essere utile se si fa riferimento a progetti con stile PackageReference (progetti con stile SDK o csproj esistenti). In questo modo, sarà possibile fare riferimento "in modo transitivo" dal progetto ai pacchetti a cui fanno riferimento tali progetti.

## <a name="floating-versions"></a>Versioni mobili

Le [versioni mobili](../consume-packages/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Controllo degli asset delle dipendenze

È possibile che si usi una dipendenza esclusivamente come strumento di sviluppo e che non si voglia esporla nei progetti che utilizzano il pacchetto. In questo scenario, è possibile usare i metadati `PrivateAssets` per controllare questo comportamento.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

I tag di metadati seguenti controllano gli asset delle dipendenze:

| Tag | Description | Valore predefinito |
| --- | --- | --- |
| IncludeAssets | Questi asset verranno utilizzati | tutti |
| ExcludeAssets | Questi asset non verranno utilizzati | none |
| PrivateAssets | Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre | contentfiles;analyzers;build |

I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:

| Value | Description |
| --- | ---
| compile | Contenuti della cartella `lib`. Controlla se il progetto può essere compilato in base agli assembly nella cartella |
| runtime | Contenuti delle cartelle `lib` e `runtimes`. Controlla se questi assembly verranno copiati nella directory di output build |
| contentFiles | Contenuto della cartella `contentfiles` |
| build | Proprietà e destinazioni nella cartella `build` |
| analyzers | Analizzatori .NET |
| nativi | Contenuto della cartella `native` |
| none | Non viene usato alcuno dei valori precedenti. |
| tutti | Tutti i valori precedenti (ad eccezione di `none`) |

Nell'esempio seguente, il progetto utilizzerà tutti gli elementi tranne i file di contenuto dal pacchetto e tutti gli elementi, tranne gli analizzatori e i file di contenuto, verranno trasferiti al progetto padre.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Si noti che dato che `build` non è incluso in `PrivateAssets`, le destinazioni e le proprietà *verranno trasferite* al progetto padre. Si consideri, ad esempio, che il riferimento precedente viene usato in un progetto che compila un pacchetto NuGet chiamato AppLogger. AppLogger può utilizzare le destinazioni e le proprietà da `Contoso.Utility.UsefulStuff`, analogamente ai progetti che utilizzano AppLogger.

## <a name="adding-a-packagereference-condition"></a>Aggiunta di una condizione PackageReference

È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà. Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.

Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`. In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria. Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Un pacchetto compilato con questo progetto indica che Newtonsoft.Json è incluso come dipendenza solo per una destinazione `net452`:

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a>Blocco delle dipendenze
*Questa funzionalità è disponibile con NuGet **4.9** o versione successiva e con Visual Studio 2017 **15.9** o versione successiva.*

L'input per il ripristino NuGet è un set di riferimenti al pacchetto dal file di progetto (dipendenze dirette o di primo livello) e l'output è una chiusura completa di tutte le dipendenze del pacchetto, incluse le dipendenze transitive. NuGet prova a produrre sempre la stessa chiusura completa di dipendenze del pacchetto se l'elenco PackageReference di input non è stato modificato. Esistono tuttavia alcuni scenari in cui non è possibile farlo. Ad esempio:

* Quando si usano versioni mobili, ad esempio `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. Anche se in questo caso la finalità è il passaggio alla versione più recente a ogni ripristino dei pacchetti, esistono scenari in cui gli utenti richiedono che il grafo venga bloccato su una determinata versione più recente e passi a una versione successiva, se disponibile, in caso di movimento esplicito.
* Viene pubblicata una versione più recente del pacchetto che risponde ai requisiti di versione di PackageReference. Ad esempio, 

  * Giorno 1: si è specificato `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, ma le versioni disponibili nei repository NuGet erano 4.1.0, 4.2.0 e 4.3.0. In questo caso, NuGet restituirebbe 4.1.0 (la versione minima più vicina)

  * Giorno 2: Viene pubblicata la versione 4.0.0. NuGet troverà ora la corrispondenza esatta e inizierà a restituire 4.0.0

* Una versione del pacchetto specifica viene rimossa dal repository. Anche se nuget.org non consente l'eliminazione dei pacchetti, non tutti i repository di pacchetti presentano questo vincolo. NuGet trova di conseguenza la corrispondenza migliore quando non può restituire la versione eliminata.

### <a name="enabling-lock-file"></a>Abilitazione del file di blocco
Per rendere persistente la chiusura completa delle dipendenze del pacchetto, è possibile acconsentire esplicitamente alla funzionalità di file di blocco impostando la proprietà MSBuild `RestorePackagesWithLockFile` per il progetto:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Se questa proprietà viene impostata, il ripristino NuGet genererà un file di blocco, il file `packages.lock.json`, nella directory radice del progetto, che elenca tutte le dipendenze del pacchetto. 

> [!Note]
> Quando nella directory radice di un progetto è presente il file `packages.lock.json`, il file di blocco viene sempre usato con il ripristino anche se la proprietà `RestorePackagesWithLockFile` non è impostata. Un altro modo per acconsentire esplicitamente a questa funzionalità è quindi quello di creare un file `packages.lock.json` fittizio vuoto nella directory radice del progetto.

### <a name="restore-behavior-with-lock-file"></a>Comportamento di `restore` con il file di blocco
Se un file di blocco è presente per il progetto, NuGet lo usa per eseguire `restore`. NuGet esegue un rapido controllo per verificare se sono state apportate modifiche alle dipendenze del pacchetto indicate nel file di progetto (o nei file dei progetti dipendenti) e, se non sono presenti modifiche, si limita a ripristinare i pacchetti indicati nel file di blocco. Non viene eseguita alcuna rivalutazione delle dipendenze del pacchetto.

Se NuGet rileva una modifica nelle dipendenze definite indicate nei file di progetto, rivaluta il grafo del pacchetto e aggiorna il file di blocco in modo da riflettere la nuova chiusura del pacchetto per il progetto.

Per CI/CD e altri scenari in cui non si vogliono modificare le dipendenze del pacchetto immediatamente, è possibile farlo impostando `lockedmode` su `true`:

Per dotnet.exe, eseguire:
```
> dotnet.exe restore --locked-mode
```

Per msbuild.exe, eseguire:
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

È anche possibile impostare questa proprietà MSBuild condizionale nel file di progetto:
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Se la modalità di blocco è `true`, verranno ripristinati i pacchetti esatti elencati nel file di blocco. Il ripristino avrà invece esito negativo se le dipendenze del pacchetto definite per il progetto sono state aggiornate dopo la creazione del file di blocco.

### <a name="make-lock-file-part-of-your-source-repository"></a>Rendere il file di blocco parte del repository di origine
Se si compila un'applicazione, un file eseguibile e il progetto in questione sono alla inizio della catena di dipendenze, quindi archiviare il file di blocco nel repository di codice sorgente in modo che NuGet possa usarlo durante il ripristino.

Se tuttavia il progetto è un progetto libreria che non viene distribuito o un progetto di codice comune da cui dipendono altri progetti, **non è consigliabile** archiviare il file di blocco come parte del codice sorgente. È possibile mantenere il file di blocco, ma le dipendenze del pacchetto bloccato per il progetto di codice comune, elencate nel file di blocco, non possono essere usate durante il ripristino o la compilazione di un progetto che dipende da questo progetto di codice comune.

Ad esempio:
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
Se `ProjectA` ha una dipendenza da `PackageX` versione `2.0.0` e fa anche riferimento a `ProjectB` che dipende da `PackageX` versione `1.0.0`, il file di blocco per `ProjectB` elencherà una dipendenza da `PackageX` versione `1.0.0`. Quando tuttavia `ProjectA` viene compilato, il file di blocco conterrà una dipendenza da `PackageX` versione **`2.0.0`** e **non** `1.0.0` come elencato nel file di blocco per `ProjectB`. Di conseguenza, il file di blocco di un progetto di codice comune ha poca influenza sui pacchetti risolti per i progetti che dipendono da esso.

### <a name="lock-file-extensibility"></a>Estendibilità di file di blocco
È possibile controllare diversi comportamenti di ripristino con file di blocco, come descritto di seguito:

| Opzione | Opzione MSBuild equivalente | 
|:---  |:--- |
| `--use-lock-file` | Avvia l'uso del file di blocco per un progetto. In alternativa, è possibile impostare la proprietà `RestorePackagesWithLockFile` nel file di progetto | 
| `--locked-mode` | Abilita la modalità di blocco per il ripristino. Questa opzione è utile negli scenari CI/CD in cui si vogliono rendere ripetibili le compilazioni. A tal fine, è anche possibile impostare la proprietà MSBuild `RestoreLockedMode` su `true` |  
| `--force-evaluate` | Questa opzione è utile con i pacchetti con la versione mobile definita nel progetto. Per impostazione predefinita, il ripristino NuGet non aggiornerà automaticamente la versione del pacchetto a ogni ripristino, a meno che il ripristino non venga eseguito con l'opzione `--force-evaluate`. |
| `--lock-file-path` | Definisce un percorso di file di blocco personalizzato per un progetto. A questo scopo, è anche possibile impostare la proprietà MSBuild `NuGetLockFilePath`. Per impostazione predefinita, NuGet supporta `packages.lock.json` nella directory radice. Se nella stessa directory sono presenti più progetti, NuGet supporta il file di blocco `packages.<project_name>.lock.json` specifico del progetto |
